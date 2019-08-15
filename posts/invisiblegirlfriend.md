---
title: The Development Behind InvisibleGirlfriend
description: This is the first public war story I have, and the lesson about design patterns I learned here has influenced me ever since in many, many places beyond coding.
date: 2015-08-06
tags:
  - anecdote
layout: layouts/post.njk
---

In the first version of Invisible Girlfriend, you could have multiple girlfriends. I had actual methods in the code named “elope,” and “divorce” to manage the intricacies of your desired relationship(s), but even at this point I called them “Partners” because I knew there were plans for the Invisible Boyfriend side (which I was also coding for). But even that was tenuous.

There were so many unknowns that I decided to have fun with it. I rewrote the default “Update” buttons on pages where you could view or edit your girlfriend with text like, “Let’s Date” or “Bye, Stephanie” (if your girlfriend was named Stephanie and you wanted to break up with her). This drew smiles and some giggles from the rest of the IG team the first time I demoed what I’d envisioned for them.

In a startup, one of the hardest parts of development is knowing what to do when you’re completely in the weeds. I wasn’t given any wireframes or hard requirements. My instructions were, “You’re the developer. Here’s the business situation. Build something.”

## Birth of a Startup Developer

In response to the situation and after some conversations with the Giant Hat team, I made a couple conscious decisions about my development strategy going in that proved surprisingly effective, both for Team Invisible and in several other projects since then.

Context: this was a consulting/client relationship, but I’ve given the same advice to help friends get started freelancing and it's worked beautifully. So whether you’re freelance, consulting, a technical cofounder, or one of the first engineers on the team, here are the lessons I’ve learned that can be useful for you.

Here are the decisions I made, along with the related lessons and examples:

### Include and educate your client on as much of the development process as possible.

This means actually talking out loud and typing in code in front of them so they can see their product grow in front of their eyes. They don’t need to understand how to map arrays or anything, but you’re defining domain concepts, naming things, and making hundreds of tiny decisions on the fly while you’re developing. Having them in the thought process builds immense comfort, trust, and understanding between you so the relationship can actually function like a partnership — and this style of business relationship produces the best software.

In this case, Invisible Girlfriend CEO Kyle Tabor proved an extremely willing partner. An engineer by trade, he had dropped his job to do Invisible Girlfriend full-time. He’d already had a bunch of commits in the repository, and while they weren’t pretty, they worked. In a matter of weeks (or maybe even days I’m not sure) he’d been able to grok Rails and splice together working features from the random information exhaust of the web.

It was kind of nerve-wracking because I was still a pretty new developer, and he’s really sharp. Every now and then, he’d get this look in his eye and his body language would change, and a subtle dread would creep up inside me right before he’d make a statement because — damn it — he was usually right, and I was the one who was supposed to know this stuff!

This brings me to point out the two most important words in this guideline: _“as possible.”_ Some clients fear technology, and you shouldn’t code in front of them or include them in technical decisions — that's why they hired you. Others, once they see human-readable code and learn git, warm up immensely and become a lot closer to their product, but still lean on you for most things. Maybe others will be comfortable talking over wireframes, sketches, anything that's not actually code. Others, like Kyle, will soak everything up and run with it.

Yes, sometimes you’ll have to spend a couple hours to clean up their latest commits, but they’re the heart and soul of the project. The more you empower them, the higher the flexibility of the entire venture, and this is way more important than the quality of the code. They’ll learn quickly. And cleaning up, correcting, teaching, will make you better at what you do, too. Empowering Kyle as much as possible was far and away one of the most central factors to IG's early app development momentum.

Now I’m not talking a Subway restaurant-style, make-it-in-front-of-you web application. I mean “as much as possible” to apply to both developer and client. With Invisible Girlfriend, I needed some development time alone to really think through things, too.

I’m gonna paraphrase something my friend/mentor [Chris Oliver](https://twitter.com/@excid3) once told me:

> There are two kinds of tension that happen during development. One is when you’re undergoing the grind of learning the domain better, revealing and grappling with more of the problem yourself. The other is when the systems you’ve built are getting in your way, and it's time to refactor.

So, which tension are you feeling? If you’re feeling the tension and confusion of learning, keep at it. This is what precedes breakthroughs.

But if you’re feeling resistance from the way you set up the code, or your business relationship, it's time to change something. Do you need more space? Or do they need a different level of exposure and engagement to be comfortable?

### Build what you actually think would be best, not what they ask for.

This is the most important guideline. It sounds dangerous, but its not. This is actually more of a realization I keep having over and over in different situations.

This guideline presupposes that, as a developer, you have agency in the situation. If you build something off-spec, the powers that be won’t throw a hissy fit. If you’re in a situation where you’re a developer for a startup, whether consulting or in-house, you need to have agency.

Whatever you ship, you are responsible for. That is the product of the job you do, the decisions you make, and a part of your time here on earth. Until we have apps that build apps and there’s no need to hire programmers any more, you are the human link in the chain that is closest to the machine and you _will_ see things differently from your understanding of both people, and computer. This is precisely what makes you valuable.

---

_Caveat: some clients want coders at the lowest price who just build to spec. This is a completely valid way of doing things if it makes both parties happy. In fact, this is often a better fit for people than the way I’m suggesting, especially in larger companies and with programmers who derive satisfaction primarily from code quality. However, I can’t be at my highest and best use for this kind of client so this isn’t the kind of client I work with, nor the kind of developer I’m speaking to._

---

You don’t get agency at the start of any project, ever. You have to build your capacity to be listened to, and earn it. Here’s how you do that:

1). _First, you must immerse yourself in the business context._ This means thoroughly understanding three areas: your client, your client’s customers, and the domain.

Kyle, and the rest of the IG team, knew the idea was a hypothesis - it's absurd on the surface. But at the time, Kyle didn’t have income. So the most important thing for him was this: either validating, or invalidating, the legitimacy of the business as fast as possible.

At the time (this has changed a lot since), IG’s customers were all people in varying situations who needed one thing: plausible deniability. Indisputable proof that they were in a relationship with a real person.

We were in the wild west in terms of the domain. Giving people the ability to text, and receive a custom response in real time, is the simple experience that proves out the entire situation. So how, exactly, were people going to interact with their partner? AI? Other people? Some chat bot?

Understanding these things meant it was clear that I needed to provide the infrastructure for people to be able to text, and for those texts to reach any possible “partner” backend the IG team wanted to plug in.

2). _Secondly, ask why._ When the client has prescribed something, and the reason why they would want it is unclear to you, it is your duty to figure out why they want it. Then decide if you agree that it is the best solution. Your understanding of the technical possibilities should not be discounted, because often, people can’t exactly explain, and they’re reacting to the perceived technical limitations in their head.

In the case of Invisible Girlfriend, the _why_’s were plentiful and obvious. Why did administrators need to be able to step in and take over text conversations? Because IG isn’t a sexting service. Why do we need to ensure the phone #’s people put in were actually for their phone? Because enterprising “friends” might be trying to play a joke on them. We have to validate the person entering the phone # is actually the person who owns the phone. Etc etc.

So when I say, build what you think is best, it might sound like I’m encouraging discord. But I hope you can see that it's actually about finding alignment in the situation, and trusting your own judgement to deliver on what they actually need, and not just what they say they want.

### Be careful when you feel proud, but embrace when you feel happy.

This next part is horribly embarrassing for me.

For this project, I wanted to be “legit.” I bought the Gang of Four Design Patterns book, read all sorts of blog posts, I was gung ho. The app/ directory had a /services folder, a /commands folder, a /proxies folder…man oh man, was I gonna be the _professional developer._ I was so proud.

I wanted to use “patterns.” I wanted to do this “right.” So to counter my fears of judgement and failure I reached out to thinking that wasn’t my own and used it as a crutch.

And you know what? At the end of the last paid Friday of my working on it, I stayed in the IG office frantically trying out different code. Everything I’d written worked in isolation, but it didn’t _work._ This was because I’d introduced so much mutable state everywhere that it was just terrible to debug because there were so many hidden side effects.

> The moment when you allow yourself to feel proud, feel superior, that’s when your ego creeps in through the back door.

When I left their office, the whole system still wasn’t working and I’d resolved that I was just going to do it anyway paid or not. Before I got the chance, [Brad Urani](https://twitter.com/@bradurani) hopped in and cleaned up the horrible statefulness by moving things into class methods with explicit parameters. Then it worked! It had been so close, a couple lines off, but it didn’t work.

He then pointed out to me that I had in fact actually used a pattern, extremely appropriately. The one area where I had just sat there and thought about it was the texting engine between partners and the various backends. He pointed out that I’d introduced a command pattern in a way that just naturally fit the situation. After that, the next time I pulled Design Patterns out of my bag, I actually read with comprehension for the first time.

But what really nailed this whole thing home for me, was that I’d placed it in the /services directory. Well, thank god its all in a private repo.

Anyway, here’s why you need to be careful when you’re proud, and it's subtle. The part of this project where I made good decisions, produced good code, and gave the IG team the functionality, space and understanding to go on, get users, get revenue, win a Webby, etc…(all them — I didn’t act in the play, just set the stage) was when I sat around, thought about the situation, came up with a best guess, and iterated.

When I was proud, meaning, feeling superior in my head but not my heart, everything I did was shit. It worked, but it was shit. When I was worried about failing, about how other people would think about me, focus on these areas was what lead me down this path.

And that’s the important realization: the moment when you allow yourself to feel proud, feel superior, that’s when your ego creeps in through the back door. That’s when you start becoming blind to the nuance of the situation, and diluting the awareness and flexibility that you need to see and process properly. This is when bad decisions happen, when you choose to apply a pattern instead of just letting the right one emerge in the wild.

But the most important part of the project is how it affected the lives of the people who signed up for it. And this part is really easy to get distanced from, but it's actually the most important. Despite my code mistakes, I never let go of this and stayed focused on the big win: what actually using it feels like.

When I saw [The Today Show](https://www.today.com/video/today/56841982) trying out the software I’d helped build, seeing the functions I wrote putting smiles on Jen’s face as she interacted with Derek Deter, I was touched, and super happy. Knowing that I’d contributed to 40k+ people (at that point) having gleeful, personal moments, actually being able to viscerally connect that consequence in the world with the code I wrote, it was surreal.

This feels like a really private moment for me, but it deserves to be in this post, too. After that moment, I realized that up until that point I’d been subconsciously questioning why I was a developer. All that contribution…for what? I’d gotten as far as I had because I’d made a decision to be a developer, but I didn’t know what was next. When I finally got to connect with the fact that I could produce better lives for people at scale, the happiness is addictive and constructive. If you’re a new developer, chase this moment, and bask in it.

### Seek Expedience through Experience.

I’ve come to believe there’s a continuum which looks like this:

Startup Developer <— — — — — — — > Academic Developer

Figure out what the business situation is, and choose your development style accordingly. Basically, it boils down to: how much the domain and design live in your head, as opposed to being cemented into the codebase? To generalize:

Big gov’t contract, tons of liability? You’re probably gonna wanna get all specs signed off, going to be on a big team, and have a large budget. Prefer TDD, and academic development.

Lower budget, crazy idea, smaller team? Don’t even write in tests until something breaks in production (with obvious exceptions around payments, sensitive info, etc).

The only thing that can inform you on where minefields are is experience. To get the most experience the most quickly, be happy, but not proud, and figure out how each feature should fall in this spectrum. Then see how it does later, down the line. Use that knowledge to change the way you do things upstream, but remember:

<blockquote class="small">Tech businesses aren’t successful because they had perfect code and systems. They’re successful because they got a product to market fast and at the right time. They got out their protoype fast (hacks and all), tested and tweaked it, and then scaled. It is wholly arrogant to believe you will have a product on first launch that will be widely acclaimed and quickly adopted. Often it will take fast, iterative changes and tweaks with a small userbase and constant feedback until the right mix of features and pricing are met, along with aggressive marketing - and then growth happens.
<p class="attribution text-right">-- from <a href="https://bigeng.io/post/118399425343/why-the-way-we-look-at-technical-debt-is-wrong" target="_blank">Why the Way We Look At Technical Debt is Wrong</a></p>
</blockquote>

## Remember

1. Include and educate your client on as much of the development process as possible.
2. Build what you actually think would be best, not what they ask for.
3. Be careful when you feel proud, but embrace when you feel happy.
4. Seek Expedience through Experience.

This doesn't mean you have an excuse not to have clean directory structures, performant code (<100ms load times), or not write any tests. This means that, in order to learn where you truly need those things, you have to to make mistakes and trust your first-hand experience over everything else, because this will lead to your greatest utility in the long run.

> We are actually user experience designers first and foremost who happen to be able to build their ideas. The design and structure of your code is a user experience on its own. - [Chris Oliver](https://twitter.com/@excid3)

These pithy phrases sum up a lot of experience I’ve had since the last round of blog posts I wrote ([LaunchCode Placement Series](https://chriszempel.com/blog)). If anything is unclear or you have any questions, feel free to comment, email me at: chris.m.zempel.com or tweet me [@ZempTime](https://twitter.com/@zemptime).

_P.S. Add ‘IGQ’ to the subject line of your email (stands for InvisibleGirlfriendQuestion in my head) and I’ll be sure to read it/get back to you faster than if you didn’t put it there._
