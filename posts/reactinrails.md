---
title: React in Rails - The Gotchas
description: React is great for doing heavy UI lifting in Rails apps by making your UI interactions easy to reason about and change. However, as someone who is quite familiar with Rails but passingly proficient in JS, there are some gotchas you're going to run into that other guides didn't cover for me. This isn't a cohesive "clone this feature" article. This is the quick-and-dirty, let's get you to functional and help you avoid some mines I stepped on article.
date: 2016-11-12
tags:
  - guide
layout: layouts/post.njk
---

## When to React

React is great for doing heavy UI lifting in Rails apps. It's super easy to drop in and make your life better by making your UI interactions easy to reason about and change. However, as someone who is quite familiar with Rails but passingly proficient in JS, there are some gotchas you're going to run into that other guides didn't cover for me. This isn't a cohesive "clone this feature" article. This is the quick-and-dirty, let's get you to functional and help you avoid some mines I stepped on article.

Save yourself an hour. Give this a glance over. It's bite-sized.

**Context:** you know what you're trying to build, and what needs to happen. But the js, coffeescript, what have you...it's getting unwieldy. There are a lot of elements on the page interacting with each other, and some unintended consequences keep popping out all over the place. Like a dark, underwater cliff descending into black water, you know the code is operating beyond the edges of your mind where you can't consider it all.

There are two kinds of discomfort a developer feels:

1. Not knowing the domain well enough
2. You're fighting the system you've set up

When you run into #2 while building out a Rails app, and the issue is getting a specific interaction/component/form/page right, this is what I view as the proper time to reach for React. Through React, you adopt some constraints to transform your application into one that works with you where you need it.

## The Best Resource (bookmark this link)

The single greatest resource for getting a handle on React is in their docs, located [here](https://facebook.github.io/react/docs/thinking-in-react.html). Read this page quite carefully because it is right.

They say "Start with a Mock." You'll notice that it's not even a step, its an assumption. I recommend you set up your page like this (example of what it looked like while I built filtering by tag for these blog posts):

```
<h1>Your view<h1>
<%= react_component("PostNavigator", { posts: @posts } ) %>
<%= render partial: "post_navigator", locals: {posts: @posts} %>
```

Have your react component on top. Then have you reference, your target, down on bottom. I don't have a reason for this other than seeing the React component slowly overtake my attempt in coffeescript was an extremely satisfying development process, and kept me focused on every page refresh, so give it a shot.

## Passing State from Child Elements to Parent Elements

When confronted with a problem where I don't even begin to know where to focus, I fall back upon this question as a guide:

> What is the smallest thing that could be universal that will allow everything else to happen?

In React, the answer to this question is to make the flow of your state explicit/able to be easily reasoned about. Doing this at first is difficult, confusing, and counterintuitive. Then you realize the tradeoff eliminates the majority of the complexity you'll deal with. Somewhere in your component architecture, you're going to define a place where all the state enters. Usually this is a parent component of some kind.

**Please Note:** I'm not going to be displaying cohesive code samples from here on out. I'm going to be displaying just the portions that pertain to the gotchas, mostly drawing from the "Thinking in React" docs.

Counterintuitively, this means that when you type into your text field form, it's not actually your form that's receiving the input. The input is instead being sent up to the place where all state enters, then being rerendered as a form with that text.

Even for something as simple as tag filtering, it's much easier to reason about one component that maintains an array of selected tags and rendering everything based upon that, than having each different selection option on the page knowing if its selected or not, and managing the communication between all those components.

They call this "inverse data flow."

### How this works in code

The important line is here where they "bind" the `handleUserInput` function to the parent component. This means when you type anything in, it's passed into this function, and actually flows upstream not to the form itself but to the parent component.

```
class FilterableProductTable extends React.Component {
  constructor(props) {
    ...
    this.handleUserInput = this.handleUserInput.bind(this);
    ...
  }
}
```

To make sure you feed the state to the parent component, you simply pass this function down to the child component(s), so they can pass data to the function on the parent component so the parent can deal with it:

```
  render() {
    return (
      <div>
        <SearchBar
          onUserInput={this.handleUserInput}
        />
      </div>
    );
  }
```

Because this example is a little older, the syntax is much easier now. To filter by tags, my parent component needs to know at a given time which ones are selected and which ones aren't. So, I pass each `TagFilterOption` two functions: one to tell the parent object when a tag is selected or deselected.

```
return <TagFilterOption tag={tag} isSelected={isSelected} addSelectedTag={this.addSelectedTag} removeSelectedTag={this.removeSelectedTag} />
```

You don't have to explicitly bind the function to the parent component, anymore. You can simply pass in `this.functionOnParentComponent` as an argument. Just make sure you've got that function defined on your parent component.

### Part 3: Mapping in Javascript: the big gotcha

I've got a variety of tags, and I want the ability to filter by each one. So obviously, the easiest way to build out my tag filters are just to take my array of tags and turn each one into a filter, right?

```
    var tagFilterOptions = this.props.tags.map(function(tag, index) {
      return <TagFilterOption tag={tag} isSelected={isSelected} key={tag} addSelectedTag={this.addSelectedTag} removeSelectedTag={this.removeSelectedTag} />
    });
```

This doesn't work, although it might look like it should.

When using `map` in javascript, it accepts a [couple of arguments](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map).

```
var new_array = arr.map(callback[, thisArg])
```

The callback function which actually produces the value you're mapping to an array, and the `thisArg` which defines what `this` is inside the callback function! So we need to set this explicitly, or it will be something else we don't want it to be.

And we want to make sure `this` is our parent component, so we can pass down the functions which will handle the state change.

```
    var tagFilterOptions = this.props.tags.map(function(tag, index) {
      ...
    }, this);
```

It wasn't until I stared at the documentation that I realized `this` was the case (heh).

## Passing Data from Models into Components

Initially, this is super simple:

```
<%= react_component("PostNavigator", { posts: @posts, tags: Post::TAGS, tag_definitions: Post::TAG_DEFINITIONS } ) %>
```

This will convert `@posts` to json, then store it all as a data attribute on the component. The component will then be able to use this.

However, if you need more advanced stuff (like including nested associations on each record), take a look at [Jbuilder](https://github.com/rails/jbuilder)

## Concluding Thoughts

React in Rails workflow:

- Always build out a hardcoded version in a standard ERB template
- Start moving it into react at the lowest levels of the components. This way, you're not guessing about your abstractions, nor will you have to fight your own expectations when the moment comes that you discover how it needs to be set up.
- Abuse data attributes at the start!
