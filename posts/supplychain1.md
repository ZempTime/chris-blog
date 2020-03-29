---
title: Segmenting Software Development Work by Demand
description: Improving the way we ship software by understanding different work streams.
date: 2020-03-29
tags:
  - anecdote
layout: layouts/post.njk
---

In any human body of thought there tends to be two distinct groups of content. "Source" material, produced rarely by innovative thinkers, and "derivative" material, which is both the continued exploration and reframing of the source ideas and the overwhelming majority of content.

Recently, I feel I've reached the point of diminished returns when reading "IT" books. These include:

* The Devops Handbook
* The Phoenix Project
* Accelerate
* Various bodies of thought, like sAFE, LESS, anything "agile," etc

This isn't to say these books or approaches are bad. In fact, they're quite good. Their contents changed my behavior. I haven't listed ones I've read and wouldn't suggest, or haven't read yet. I have listed specific ones which were worthy of my time. In practice a "source" book might not be _the_ source book (in a chronological sense), but if it's your first exposure to a set of good ideas, it becomes _your_ source book.

However, these are all slightly derivative work, in that they're the reframing and more-specific interpretation of a more generalized body of thought. Thanks to the reccomendation of my friend Kai, I recently stumbled across what I'd consider a true "source" book (at least for me) - [The Supply Chain Revolution](https://www.amazon.com/Supply-Chain-Revolution-Innovative-Competitive/dp/0814438784).

Consider that logistics and supply chains need to deal with _all_ manner of products and problems, not just one specific kind (like software). In some fairly direct ways, the thinking around these problems is what's directly transferred into the realm of software development. There are some specific differences between the more generalized problems of "supply chains" and the more specialized area of "software development" which cause huge problems if you transfer and apply the ideas directly and unmodified. However, I still consider this a fertile area of thought, because the application of more general ideas to your _specific_ situation will always eventually result in better-adapted approaches than rigidly following the already-slightly-adapted approaches prescribed in books.

In this post, I'd like to explore one idea from the supply chain/logistics domain that's been a massive miss on part of existing IT literature. But before I get to that, we need to talk through common pitfalls of direct idea transferrence that I hope will deepen the insight and impact of the missing idea to be discussed immediately after.

## Problems with Supply Chains to Software

Here are some starting points:

* **For some reason, companies have lots of troubles converting capital into good software.** Companies that can produce incredibly complex and intricate products at massive scale often can't make good software. Why is this? I'd actually suggest building software, in isolation, isn't intrinsically _hard_...
* **Approaches that've had to survive and adapt to the real world tend to be better than approaches that haven't.** People are often hesitant to pursue ideas which are good and make sense for them without approval from some other authority (as if any of us know what we're doing!).

The opposite of the second point is people will often pursue approaches if there's been enough investment on behalf of others to propel it past some credibility threshold. People will blindly apply what they read in books or see online because it's "safe." Then, once settled, no form of error-correction kicks in to start adapting their approach to their circumstances.

This is the major reason you can't directly transfer thought from supply chains to software. Software is considerably more highly-dimensional. There are far fewer physical constraints at play than physically constructing and moving materials, far higher variance in the skill of individual practitioners and much more extreme potential outcomes (read: power law territory) approaches can accrue over time. This causes most developers to have a kneejerk negative reaction when "business people" want to directly simplify, reduce, and componentize software development. The other problem here is, most developers can't articulate why this is _so wrong_.

The resulting situation is that this lazy upstream thinking is a risk-offsetting exercise from non-engineering units onto engineering units.

Once you figure out a way to compensate for a given dimension, you begin to be able to directly transfer thought from one area to another.

## Demand

When do most companies decide to improve customer service? When they realize it helps them sell more products. What do most companies do wrong when they do this? They don't tailor their service offerings to customer segments. Where you see this in software development front-and-center is when you need to get out a hotfix, but all your existing deployment processes get in the way. In fact, I think segmenting customers by service level is one of the best and most obvious ideas I've heard in a long time.

When you don't tailor your service offerings by segment, and you do increase service, what you're doing is offering more service to everyone at the same increased level. This is bad because it increases cost significantly vs the actual benefit you get as a business from the increased amount of service you're offering. An example of an attempt at compensating for this is classifying "bug" tickets according to priorities, and splitting them up into queues based upon this classification. Wouldn't we get the same benefit if we did something similar, sooner in the process?

Where do companies go wrong in how they interact with customers? This question, slightly transformed is, where does engineering go wrong when interacting with upstream business units? The costs of these service level increases aren't visible to, for example, project management, who have no incentive to choose the right service level. ("Yes, we should fix all bugs in 24h. Also, while doing this, we need to ship an extra major feature in addition to the one you were already scheduled for and nervous about.")

This effect happens a lot in general (think real estate, hr, IT, procurement, etc). These functions are centralized with the hope that costs will be reduced through economies of scale. What happens instead is costs of shared services go through the roof instead of going down.

Why does this happen? **It's hard to drive scale in the services area unless you completely restructure work processes.** When directly exposed to the costs for a service, it's easy to set expectations correctly. When costs get centralized, nobody challenges the need for a higher service level because there's either no disincentive, or no mechanism to do so (the supplying org doesn't have service levels available to even choose from). To directly pull an example from the book, "It's like everyone ordering the most expensive dish on the menu because they'll all be splitting the bill equally no matter what they order."

Most companies, in fact, lack an understanding of what the needs at various service levels even are. They classify areas of different demand by the way their sales or marketing departments do, using psychographics or demographics. Dimensions that are more useful are things like volume, profitability, strategic importance of an account.

## Ground-up vs Modular

Most companies have single, do-it-all production chains that don't do anything very well and get bogged down. (Ex: your entire organization shares the same, singular jenkins instance). This incurs the massively increased, but indirect, shared costs penalty discussed above. 

An alternative approach is having separate production chains based on whether the service you offer is fast-moving, slow-moving, or customized. Which of these production chains you're in has direct impact on where you should spend time refactoring, and how you should approach building different pieces of your application or platform.  Breaking up your pipelines into multiple, parallel flows allows it so each flow can be optimized for the type of demand.

In fact, addressing these different service levels is the play behind trunk-based development: lower all the barriers so considerably that your single production chain is fast and low-overhead enough you don't run into problems because you can decentralize all choice out across the organization. Of course, this necessitates you really _are_ one organization, and not competing sub-organizations servicing various and radically different kind of requirements (fast-moving, slow-moving, custom).

In some areas of your application, you'll have fast-moving areas of production. These areas of work should have corresponding cost-efficient, low-customization, and high-throughput focused pipelines. A characteristic of this kind of pipeline to look for are features where the basic version is quite valuable, and further customization is considerably less so. For example, being able to _send transactional email_ to various subsets of your userbase at all. That these be fully customizable with fancy headers, styling, etc doesn't offer that much more benefit compared to being able to click "reset password." (Note: this only applies for _transactional_ email. I suspect most engineers systemically undervalue being able to tune and customize marketing email).

In some areas of your application, you'll have areas where custom & ground-up productions becomes appropriate. Example: you could eliminate massive amounts of data entry by writing a one-off script to convert a heavily-structured excel spreadsheet into data for your system. Does your source control, build pipelines, security guidelines or testing approaches contain the ability to service such a request?

In other areas, you'll have slow-moving areas of production. This long lead time makes it appropriate to invest in a modular system up-front so that can deal with the kinds of customization requirements you need so you can quickly respond to what your customers are asking for. Characteristics of what to look for here are high-complexity, high-customization features.

## How to listen

There's much more to this idea of tailoring service offerings to customer segments. This idea has impact in the dimensions of service, revenue, and risk. I won't be getting into these in this post. Rather, the final area I'd like to circle back to is: why is building good software so hard for organizations who can otherwise do incredible things?

One of the larger contributors is not segmenting customers by service level. You can tell when this is happening incorrectly when some of your engineers are reacting negatively to the way work is structured, but can't explain to you why they feel that way. (Some engineers are always too optimistic, some are too pessimistic, and some either don't care or aren't skilled enough to know better. The ones to pay attention to are the ones who've shipped complex features and have good track records with reactions that trend in either direction.)

When 1) your addressable markets aren't clear, 2) these markets aren't divided into segments determined by business metrics (not sales & marketing ones), and 3) you have no intentional strategy (or awareness) around where your custom, fast-, and slow-moving production chains are, what you're doing is making sure your engineering organization isn't informed enough to provide you the right information to go-to-market in the best way.

If you can't listen for and interpret this feedback, you'll systemically offset risk onto the engineering organization in the way you structure work for them. This results in death marches, mid-stream "recalibrations" where you ask all your engineers to hastily get together forecasts they'll be held accountable for, and most importantly: you're now self-selecting over the long-term for low- and medium-quality programmers. The good ones, the ones who can give you the feedback and help you go-to-market, will leave because they'll see this pattern occurring over and over. This departure will cut you out of all their friends, too (who are other high-quality programmers).

It also makes sense to adopt different production chains based on business context. This is why you see so much conflicting argument amongst programmers surrounding technical debt.

The right answer doesn't come from a book. It comes from continuously applying error-correction that makes sense in your environment. Taken to the other extreme, it becomes possible to develop a massive competitive advantage by differentiating yourself and developing a service model that's difficult for competition to match. This must be supported by production chains that can respond to demand correctly, and scale where needed.

Drop me a line @zemptime if any of these ideas really struck a nerve with you, good or bad. I'd love to get some feedback on what ideas to translate across domains next!