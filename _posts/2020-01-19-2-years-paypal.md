---
layout: post
title: "2 Years @PayPal"
description: "My thoughts on PayPal, my team and my journey here."
date: 2020-01-19
tags: [paypal]
comments: true
share: true

---



This Monday, PayPal India hosted the 2020 batch of tech interns. Almost exactly 2 years ago, I was part of the 2018 intern cohort, and then in August '18, I joined PayPal as a full-time engineer in the same team I interned with. I recently took some time to pen down how this journey has been, and how I feel about PayPal today. 

I first talk about [my team](#what-does-my-team-do), then a bit [about PayPal](#whats-working-at-paypal-like), and then finally about [my journey](#my-journey-so-far-at-paypal) here. Feel free to skip to the sections relevant to you. 

## What does my team do

I'm part of a team called India Product Development, and in one line: it builds PayPal for India. A small group of product  and tech managers, an architect, and engineers - the team decides what features to bring to the product, designs it, executes it, and bug fixes it before handing over things back to the domain (or "owner") teams. This is a rather rare kind of group in the company - you could say the team operates almost like a mini startup - people occasionally wear multiple hats (informally if not officially), we're up against some giant competitors, and we're a closely-knit small group.  How big (or small) are we? We fit in the frame below: 

![team](/assets/team.jpg)*The next time you use PayPal in India, you can praise (or blame) one of these folks for your experience.*

That said, even though we have the mandate and spirit of a startup, working under and on the same stack as a mature big tech public company means we have none of the freedoms that come with a startup (can't burn investor money, can't push crappy code, can't experiment in fail-fast mode with half-baked products). You can think of my team as a more responsible, grown-up kind of startup! (If there ever was a thing like that.) 

Working in a team like this, and in a market like India, can be extremely exciting and at the same time, challenging - figuring out the right next step will often take time; there isn't a lot of dev stability - you're working on one component today and an entirely another one a couple of months later; and deadlines can be extremely tight for everyone at times. That said, when the team delivers - it delivers a complete user experience; that is extremely satisfying and fulfilling to see being used out in the open! 

## What's working at PayPal like

While your mileage with any company will depend hugely on the team you join, there are of course a few common denominators. I'll talk about three of them here - tech, work, and culture.

**First, the tech**. PayPal is a payments company, and payments at its core involves passing messages from one guy to another, in a fast, secure and traceable manner, while being easy to use. The tech exists to support that - so no self-driving cars that also buy and pay for your meal from a drive-thru here. (I'll come back on innovation a bit later though.) I could loosely divide PayPal engineering teams into - core platform teams, application teams (like mine), data science teams, and analytics teams (about which I know little, so I won't talk about them). Core platform devs pretty much choose what they want to use - so we have entire components written in Scala. Application devs until recently had a fixed class of services to choose from, which support our business use cases - backend REST services, frontend web services, batches, messaging daemons, and mobile apps. These applications rely on modern frameworks like Spring, node.js, React, Angular, etc (there are legacy C++ components too, but they're mostly gone). Since very recently, you can also deploy freestyle dockerized applications too in the framework of your choice. Data science teams, again, use pretty much what they think best suits their use case - so you can pick up any buzzword and it's likely that some team somewhere is using it for something. 

**Second, the work**. One of the first things that struck me when I joined the company as an intern was how long it took to get nod/go-ahead for getting things done. PayPal is not a startup, and it shows. When you're working with teams located across several time zones, in a company with well-defined ownerships, getting all the nods for a course of action can be a good chunk of your team's work, especially if you're an [inner sourcing](https://en.wikipedia.org/wiki/Inner_source) team like mine. Secondly, the company obsessively focusses on data security (which, agreed, is crucial to our business), but that makes a developer's life a bit hard, with us having to file tickets for one access after another. That said, most small dev teams enjoy a good deal of independence with their working style, release cadence and coding practices. With more and more teams opening up to inner source and a common stack across teams, it's becoming easier and more common to cross collaborate. (In this respect, our team-contribution graph may be slowly becoming similar to facebook's [here](https://i.imgur.com/XLuaF0h.png) )

**Third, the culture**. There is a great deal of focus on people - they are encouraged to take time off, pursue side hustles, and do whatever it takes to recharge themselves. There is a lot of openness and transparency too - you can question anyone on anything, and honest questions are generally met with honest answers. Paul Graham once wrote that you should be acutely aware of the [things you can't say](http://www.paulgraham.com/say.html) in a group: at PayPal, I feel you can say practically anything, as long as you have a point and you put it respectfully. And even though hierarchies exist, your reach and influence at PayPal can be practically unlimited. The workplace is vibrant and inspiring with some talk, event, or activity happening at all times. All of these things make it easy for people to thrive while having fun!

Lastly, a word on innovation.  Last year, we had three major hackathons in Chennai and one major company-wide innovation tournament - with ideas (both business and tech) ranging from how to promote environmental sustainability through PayPal, to how to extend the payments capabilities to the last segment of users. I think it's safe to say that at PalPal, innovation and wild creativity are not just encouraged, but fostered and groomed. This is the aspect of PayPal that I have personally come to love the most! I only wish we had a way to show our customers *all* of the exciting stuff we keep cooking up inside.

## My journey so far at PayPal

(**Warning**: Lots of jargons in the next paragraph, skip to [tl;dr](#tldr) if you're not from the payments world )

Within India PD, I work with the scrum team that focusses on the second half of the core transaction flow - where I in particular work on the component that validates and routes the payment. I also wrote and owned an app for merchant compliance reminders ("Hey, you're x steps away from being able to receive money"), and have worked recently on the Financial Reference Data System, which is used by downstream services in PayPal to recall static data like MCC codes, sort codes, card BIN properties, etc.

I've also recently been part of a project-on-steroids to introduce support for a new card scheme in PayPal. Participating in integration discussions with a new backend [payments processor](https://en.wikipedia.org/wiki/Payment_processor), and  working on key changes to some core payments components has given me a broad overview of how the payments systems of the world work, and slightly more focussed ideas of some of its aspects - such as 3DS authentication and tokenization.

## tl;dr:

 If I think about what are some of the most important things I learned here:

- A broad idea of how the world's payments systems work. This has by far been the most interesting part of my learning here. 
- How hard, and yet exciting, it is to be a payments business in India - regulations change overnight, customers are spoiled for choice, and none of the competition actually makes any money; and yet - the market is so diverse and huge that the opportunities for innovation (a.k.a. "problems") are going to be endless for some time.
- A taste of how tech teams work, how critical apps are written ("keep it simple") and maintained ("write the tests"). This was also my first experience in life working in a team for an extended time. Coming from college, I had to learn that in a team, it's important to ask for help when you're stuck, that it's perfectly ok to say that you don't know something, and learn to accept that the systems are so complex that you'll never know everything (so it's important to remain curious). All of these things might seem simple and obvious to me (and to you) now, but I clearly remember a time when that was not the case.

## In pictures

I'm putting down some of my favorite snaps from my time at PayPal. I hope they tell you more about PayPal than my words could. Until my next post then! 👋



<center><iframe width="560" height="315" src="https://www.youtube-nocookie.com/embed/G8Rj45CTjGM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>
*Recent college grads and newly minted FTEs, hazing the lovely Patrick, who used to lead our University Programs, at a party concluding our first month at PayPal*.

![friends](/assets/friends.jpg)*To my manager: We weren't slacking off, [our code was compiling!](https://xkcd.com/303/)*  

![hiring_trip](/assets/bits_goa.jpg)*Going back to my college as part of our hiring team. I shadowed senior engineers interviewing students, and it was a humbling experience to be on the other side of the same table I'd been a mere 2 years ago.* 

![celebration](/assets/celebration.gif)*When your code finally works somehow.*

![nook](/assets/nook.jpg)*My favorite nook for slacking off between work.*

 



