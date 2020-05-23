---
title: On Making More Expressive Frameworks
description: The fundamental expressiveness of frameworks hasn't materially increased since Rails, with the exception of React's component-based views. With StateCharts now finally hitting web application development shores, we have a chance to start advancing this substrate.
date: 2020-05-23
tags:
  - anecdote
layout: layouts/post.njk
---

There are two really good ideas to come out of the JS community in the past couple of years.

1. Real-time compiled static graphs (Apollo Federation, Webpack v5 Federation, Hasura, Prisma, etc)
2. Usage of StateCharts as a first-class abstraction inside web applications (api and ui).

I'm self-admitted fanboy of one technology: Ruby on Rails. Over the past year, I've become a self-admitted fanboy of another: StateCharts. More specifically, a js-based implementation named [XState](https://xstate.js.org/).

In addition to actually being used to drive executing code, you can start using XState to drive [other areas of the system](https://www.youtube.com/watch?v=tpNmPKjPSFQ).

## A Personal Experiment

I've had many situations where the UI components I'm building are complex enough that regular unit testing doesn't cut it. XState can readily address this pain point by modelling each interaction in isolation, then generating interaction pathways.

`<an-aside>`
If you don't mind some messy code, check out [Dwight Job Application](https://github.com/ZempTime/dwight-job-application/). This takes a ~10 question multi-step wizard and exhaustively generates test cases of various ways of traversing through it.

Hint: there are 764 ways to fail. There's only 1 way Dwight would hire you. He has high standards, after all.

You can just directly interact with the test plans. This is insanely cool!

```
  console.log(testPlans1.filter((p) => p.paths[0].segments.length > 7).length);  // 2312
  console.log(testPlans1.filter((p) => p.paths[0].segments.length > 8).length);  // 2000
  console.log(testPlans1.filter((p) => p.paths[0].segments.length > 9).length);  // 1440
  console.log(testPlans1.filter((p) => p.paths[0].segments.length > 10).length); // 704
  console.log(testPlans1.filter((p) => p.paths[0].segments.length > 11).length);  // 384
  console.log(testPlans1.filter((p) => p.paths[0].segments.length > 12).length);  // 0
```

`</an-aside>`

## Expressiveness vs Substrate

The fundamental expressiveness of frameworks hasn't materially increased since Rails, with the exception of React's component-based views. With StateCharts now finally hitting web application development shores, we have a chance to start advancing the substrate frameworks are built upon. Even though we're addressing more and more complex problems, the expressiveness of our toolset isn't keeping pace.

There is a world of opportunity to build new conventions, an order-of-magnitude more expressive and capable before, by leaning into StateCharts as a first-class part of the substrate that makes frameworks run.

Thinking about tools which can help everyone create things is my true happy place, so I wanted to share the discussion. Here's a post ideating through better routing for js-based web frameworks, and what it could look like by drawing upon Rails + integrating XState: [Possible Wish/Idea: XState as Framework Substrate](https://spectrum.chat/statecharts/general/possible-wish-idea-xstate-as-framework-substrate~be115fb6-60e7-4c45-91d8-0092bbcdb93b)

In addition to routing and testing, other areas include:

- Fixture data generation (for use in tests)
- Modelling deployments (testing combinations of feature flags and known states)
- Dir structure linting
- Flexible/typesafe data modeling
- Visualization
- Application/domain specific concept portability (anywhere that can accept SCXML)

If you've any interest in this vein of thought, let's talk. :)
