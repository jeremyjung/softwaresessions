+++
title = "Luca Casonato on Deno"

description = "Luca explains JavaScript runtimes, why Deno was created, the difficulty of shipping new features in NodeJS, and the importance of web standards"

[extra]
episode_url = "https://pinecast.com/listen/f7267767-dff8-437b-8ff7-d7b95d4ff919.mp3"
+++

Deno is a JavaScript runtime that has a comprehensive standard library, web-standard APIs, and a built in linter, code formatter, and test runner. It was created by the creator of Node with the intent of [fixing the things he regretted about NodeJS](https://www.youtube.com/watch?v=M3BM9TB-8yA).

Luca Casonato is the tech lead for [Deno Deploy](https://deno.com/deploy) and a [TC39](https://tc39.es/) delegate.

This episode originally aired on Software Engineering Radio. This version includes additional sections on the standard library and permissions model.

### Topics covered:

- What's a JavaScript runtime
- How V8 is used
- Why Deno was created
- The W3C WinterCG for server-side JavaScript
- Why it's difficult to ship new features in Node
- The benefits of web standards
- Creating an all-inclusive toolset like Rust and Go
- Deno's node compatibility layer
- Choosing what to put in a standard library
- Use cases for WebAssembly
- Benefits and implementation of Deno Deploy
- Reasons to deploy on the edge
- What's coming next

### Luca

- [Luca Casonato](https://lcas.dev/)
- [@lcasdev](https://mastodon.social/@lcasdev)

### Deno
- [Homepage](https://deno.land/)
- [Deploy](https://deno.land/)
- [Showcase](https://deno.land/showcase)
- [Subhosting](https://deno.com/subhosting)
- [Fresh web framework](https://fresh.deno.dev/)
- [The anatomy of an Isolate Cloud](https://deno.com/blog/anatomy-isolate-cloud)
- [10 Things I Regret About Node.js - Ryan Dahl - JSConf EU](https://www.youtube.com/watch?v=M3BM9TB-8yA)

### Deno Users
- [Netlify Edge Functions](https://supabase.com/docs/guides/functions)
- [Deno at Slack](https://deno.com/blog/slack-open-beta)
- [GitHub Flat Data](https://githubnext.com/projects/flat-data/)
- [Shopify Oxygen](https://shopify.dev/custom-storefronts/oxygen)

### Related links
- [Cache Web API](https://deno.com/blog/v1.26#cache-web-api)
- [V8](https://v8.dev/) (JavaScript and WebAssembly engine)
- [TC39](https://tc39.es/) (JavaScript specification group)
- [Web-interoperable Runtimes Community Group (WinterCG)](https://wintercg.org/)
- [Cloudflare Workers](https://workers.cloudflare.com/) (Deno Deploy competitor)
- [How Cloudflare KV works](https://developers.cloudflare.com/workers/learning/how-kv-works/)
- [CockroachDB](https://www.cockroachlabs.com/product/) (Distributed database)
- [XKCD Standards Comic](https://xkcd.com/927/)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:07] **Jeremy:** Today I'm talking to Luca Casonato. He's a member of the Deno Core team and a TC 39 Delegate. 

[00:00:06] **Luca:** Hey, thanks for having me.

## What's a runtime?


[00:00:07] **Jeremy:** So today we're gonna talk about Deno, and on the website it says, Deno is a runtime for JavaScript and TypeScript. So I thought we could start with defining what a runtime is.

[00:00:21] **Luca:** Yeah, that's a great question. I think this question actually comes up a lot. It's, it's like sometimes we also define Deno as a headless browser, or I don't know, a, a JavaScript script execution tool. what actually defines runtime? I, I think what makes a runtime a runtime is that it is a, it's implemented in native code.

It cannot be self-hosted. Like you cannot self-host a JavaScript runtime. and it executes JavaScript or TypeScript or some other scripting language, without relying on, well, yeah, I guess it's the self-hosting thing. Like it's, it's essentially a, a JavaScript execution engine, which is not self-hosted.

So yeah, it, it maybe has IO bindings, but it doesn't necessarily need to like, it. Maybe it allows you to read the, from the file system or, or make network calls. Um, but it doesn't necessarily have to. It's, I think the, the primary definition is something which can execute JavaScript without already being written in JavaScript.


## How V8 and JavaScript runtimes are related


[00:01:20] **Jeremy:** And when we hear about JavaScript run times, whether it's Deno or Node or Bun, or anything else, we also hear about it in the context of v8. Could you explain the relationship between V8 and a JavaScript run time?

[00:01:36] **Luca:** Yeah. So V8 and, and JavaScript core and Spider Monkey, these are all JavaScript engines. So these are the low level virtual machines that can execute or that can parse your JavaScript code. turn it into byte code, maybe turn it into, compiled machine code, and then execute that code. But these engines, Do not implement any IO functions.

They do not. They implement the JavaScript spec as is written. and then they provide extension hooks for, they call these host environments, um, like environments that embed these engines to provide custom functionalities to essentially poke out of the sandbox, out of the, out of the virtual machine. Um, and this is used in browsers.

Like browsers have, have these engines built in. This is where they originated from. Um, and then they poke holes into this, um, sandbox virtual machine to do things like, I don't know, writing to the dom or, or console logging or making fetch calls and all these kinds of things. And what a runtime essentially does, a JavaScript runtime is it takes one of these engines and.

It then provides its own set of host APIs, like essentially its own set of holes. It pokes into the sandbox. and depending on what the runtime is trying to do, um, the weight will do. This is gonna be different and, and the sort of API that is ultimately exposed to the end user is going to be different.

For example, if you compare Deno and node, like node is very loosey goosey, about how it pokes holds into the sandbox, it sort of just pokes them everywhere. And this makes it difficult to enforce things like, runtime permissions for example. Whereas Deno is much more strict about how it, um, pokes holds into its sandbox.

Like everything is either a web API or it's behind in this Deno name space, which means that it's, it's really easy to find, um, places where, where you're poking out of the sandbox. and really you can also compare these to browsers. Like browsers are also JavaScript run times. Um, they're just not headless.

JavaScript run times, but JavaScript run times that also have a ui. and. . Yeah. Like there, there's, there's a whole Bunch of different kinds of JavaScript run times, and I think we're also seeing a lot more like embedded JavaScript run times. Like for example, if you've used React Native before, you, you may be using Hermes as a, um, JavaScript engine in your Android app, which is like a custom JavaScript engine written just for, for, for React native.

Um, and this also is embedded within a, like react native run time, which is specific to React native. so it's also possible to have run times, for example, that are, that can be where the, where the back backing engine can be exchanged, which is kind of cool.

[00:04:08] **Jeremy:** So it sounds like V8's role, one way to look at it is it can execute JavaScript code, but only pure functions. I suppose you

[00:04:19] **Luca:** Pretty much. Yep.

[00:04:21] **Jeremy:** Do anything that doesn't interact with IO so you think about browsers, you were mentioning you need to interact with a DOM or if you're writing a server side application, you probably need to receive or make HTTP requests, that sort of thing.

And all of that is not handled by v8. That has to be handled by an external runtime.

[00:04:43] **Luca:** Exactly Like, like one, one. There's, there's like some exceptions to this. For example, JavaScript technically has some IO built in with, within its standard library, like math, random. It's like random number. Generation is technically an IO operation, so, Technically V8 has some IO built in, right? And like getting the current date from the user, that's also technically IO

So, like there, there's some very limited edge cases. It's, it's not that it's purely pure, but V8 for example, has a flag to turn it completely deterministic. which means that it really is completely pure. And this is not something which run times usually have. This is something like the feature of an engine because the engine is like so low level that it can essentially, there's so little IO that it's very easy to make deterministic where a runtime higher level, um, has, has io, um, much more difficult to make deterministic.

[00:05:39] **Jeremy:** And, and for things like when you're working with JavaScript, there's, uh, asynchronous programming

[00:05:46] **Luca:** mm-hmm.


## Concurrent JavaScript execution

[00:05:47] **Jeremy:** So you have concurrency and things like that. Is that a part of V8 or is that the responsibility of the run time?

[00:05:54] **Luca:** That's a great question. So there's multiple parts to this. There's the part, um, there, there's JavaScript promises, um, and sort of concurrent Java or well, yes, concurrent JavaScript execution, which is sort of handled by v8, like v8. You can in, in pure v8, you can create a promise, and you can execute some code within that promise.

But without IO there's actually no way to defer time, uh, which means that in with pure v8, you can either, you can create a promise. Which executes right now. Or you can create a promise that never executes, but you can't create a promise that executes in 10 seconds because there's no way to measure 10 seconds asynchronously.

What run times do is they add something called an event loop on top of this, um, on top of the base engine and that event loop, for example, like a very simple event loop, for example, might have a timer in it, which every second looks at if there's a timer schedule to run within that second.

And if it does, if, if that timer exists, it'll go call out to V8 and say, you can now execute that promise. but V8 is still the one that's keeping track of, of like which promises exist, and the code that is meant to be invoked when they resolve all that kind of thing. Um, but the underlying infrastructure that actually invokes which promises get resolved at what point in time, like the asynchronous, asynchronous IO is what this is called.

This is driven by the event loop, um, which is implemented by around time. So Deno, for example, it uses, Tokio for its event loop. This is a, um, an event loop written in Rust. it's very popular in the Rust ecosystem. Um, node uses libuv. This is a relatively popular runtime or, or event loop, um, implementation for c uh, plus plus.

And, uh, libuv was written for Node. Tokio was not written for Deno. But um, yeah, Chrome has its own event loop implementation. Bun has its own event loop implementation.

[00:07:50] **Jeremy:** So we, we might go a little bit more into that later, but I think what we should probably go into now is why make Deno, because you have Node that's, uh, currently very popular. The co-creator of Deno, to my understanding, actually created Node. So maybe you could explain to our audience what was missing or what was wrong with Node, where they decided I need to create, a new runtime.


## Why create a new runtime? (standards compliance)

[00:08:20] **Luca:** Yeah. So the, the primary point of concern here was that node was slowly diverging from browser standards with no real path to, to, to, re converging. Um, like there was nothing that was pushing node in the direction of standards compliance and there was nothing, that was like sort of forcing node to innovate.

and we really saw this because in the time between, I don't know, 2015, 2018, like Node was slowly working on esm while browsers had already shipped ESM for like three years. , um, node did not have fetch. Node hasn't had, or node only at, got fetch last year. Right? six, seven years after browsers got fetch.

Node's stream implementation is still very divergent from, from standard web streams. Node was very reliant on callbacks. It still is, um, like promises in many places of the Node API are, are an afterthought, which makes sense because Node was created in a time before promises existed. Um, but there was really nothing that was pushing Node forward, right?

Like nobody was actively investing in, in, in improving the API of Node to be more standards compliant. And so what we really needed was a new like Greenfield project, which could demonstrate that actually writing a new server side run. Is A viable, and b is totally doable with an API that is more standards combined.

Like essentially you can write a browser, like a headless browser and have that be an excellent to use JavaScript runtime, right? And then there was some things that were I on top of that, like a TypeScript support because TypeScript was incredibly, or is still incredibly popular. even more so than it was four years ago when, when Deno was created or envisioned, um, this permission system like Node really poked holes into the V8 sandbox very early on with, with like, it's gonna be very difficult for Node to ever, ever, uh, reconcile this, this.

Especially cuz the, some, some of the APIs that it, that it exposes are just so incredibly low level that like, I don't know, you can mutate random memory within your process. Um, which like if you want to have a, a secure sandbox like that just doesn't work. Um, it's not compatible. So there was really needed to be a place where you could explore this, um, direction and, and see if it worked.

And Deno was that. Deno still is that, and I think Deno has outgrown that now into something which is much more usable as, as like a production ready runtime. And many people do use it, in production. And now Deno is on the path of slowly converging back with Node, um, in from both directions. Like Node is slowly becoming more standards compliant. and depending on who you ask this was, this was done because of Deno and some people said it would had already been going on and Deno just accelerated it. but that's not really relevant because the point is that like Node is becoming more standard compliant and, and the other direction is Deno is becoming more node compliant.

Like Deno is implementing node compatibility layers that allow you to run code that was originally written for the node ecosystem in the standards compliant run time. so through those two directions, the, the run times are sort of, um, going back towards each other. I don't think they'll ever merge. but we're, we're, we're getting to a point here pretty soon, I think, where it doesn't really matter what runtime you write for, um, because you'll be able to write code written for one runtime in the other runtime relatively easily.

[00:12:03] **Jeremy:** If you're saying the two are becoming closer to one another, becoming closer to the web standard that runs in the browser, if you're talking to someone who's currently developing in node, what's the incentive for them to switch to Deno versus using Node and then hope that eventually they'll kind of meet in the middle.

[00:12:26] **Luca:** Yeah, so I think, like Deno is a lot more than just a runtime, right? Like a runtime executes JavaScript, Deno executes JavaScript, it executes type script. But Deno is so much more than that. Like Deno has a built-in format, or it has a built-in linter. It has a built-in testing framework, a built-in benching framework.

It has a built-in Bundler, it, it like can create self-hosted, um, executables. yeah, like Bundle your code and the Deno executable into a single executable that you can trip off to someone. Um, it has a dependency analyzer. It has editor integrations. it has, Yeah. Like I could go on for hours, (laughs) about all of the auxiliary tooling that's inside of Deno, that's not a JavaScript runtime.

And also Deno as a JavaScript runtime is just more standards compliant than any of the other servers at Runtimes right now. So if, if you're really looking for something which is standards complaint, which is gonna like live on forever, then it's, you know, like you cannot kill off the Fetch API ever.

The Fetch API is going to live forever because Chrome supports it. Um, and the same goes for local storage and, and like, I don't know, the Blob API and all these other web APIs like they, they have shipped and browsers, which means that they will be supported until the end of time. and yeah, maybe Node has also reached that with its api probably to some extent.

but yeah, don't underestimate the power of like 3 billion Chrome users. that would scream immediately if the Fetch API stopped working Right?

[00:13:50] **Jeremy:** Yeah, I, I think maybe what it sounds like also is that because you're using the API that's used in the browser places where you deploy JavaScript applications in the future, you would hope that those would all settle on using that same API so that if you were using Deno, you could host it at different places and not worry about, do I need to use a special API maybe that you would in node?


## WinterCG (W3C group for server side JavaScript)

[00:14:21] **Luca:** Yeah, exactly. And this is actually something which we're specifically working towards. So, I don't know if you've, you've heard of WinterCG? It's a, it's a community group at the W3C that, um, CloudFlare and, and Deno and some others including Shopify, have started last year. Um, we're essentially, we're trying to standardize the concept of what a server side JavaScript runtime is and what APIs it needs to have available to be standards compliant.

Um, and essentially making this portability sort of written down somewhere and like write down exactly what code you can write and expect to be portable. And we can see like that all of the big, all of the big players that are involved in, in, um, building JavaScript run times right now are, are actively, engaged with us at WinterCG and are actively building towards this future.

So I would expect that any code that you write today, which runs. in Deno, runs in CloudFlare, workers runs on Netlify Edge functions, runs on Vercel's Edge, runtime, runs on Shopify Oxygen, is going to run on the other four. Um, of, of those within the next couple years here, like I think the APIs of these is gonna converge to be essentially the same.

there's obviously gonna always be some, some nuances. Um, like, I don't know, Chrome and Firefox and Safari don't perfectly have the same API everywhere, right? Like Chrome has some web Bluetooth capabilities that Safari doesn't, or Firefox has some, I don't know, non-standard extensions to the error object, which none of the other runtimes do.

But overall you can expect these front times to mostly be aligned. yeah, and I, I think that's, that's really, really, really excellent and that, that's I think really one of the reasons why one should really consider, like building for, for this standard runtime because it, it just guarantees that you'll be able to host this somewhere in five years time and 10 years time, with, with very little effort.

Like even if Deno goes under or CloudFlare goes under, or, I don't know, nobody decides to maintain node anymore. It'll be easy to, to run somewhere else. And also I expect that the big cloud vendors will ultimately, um, provide, manage offerings for, for the standards compliant JavaScript on time as well.


## Is Node part of WinterCG?

[00:16:36] **Jeremy:** And this WinterCG group is Node a part of that as well?

[00:16:41] **Luca:** Um, yes, we've invited Node, um, to join, um, due to the complexities of how node's, internal decision making system works. Node is not officially a member of WinterCG. Um, there is some individual members of the node, um, technical steering committee, which are participating. for example, um, James m Snell is, is the co-chair, is my co-chair on, on WinterCG.

He also works at CloudFlare. He's also a node, um, TSC member, Mateo Colina, who has been, um, instrumental to getting fetch landed in Node, um, is also actively involved. So Node is involved, but because Node is node and and node's decision making process works the way it does, node is not officially listed anywhere as as a member.

but yeah, they're involved and maybe they'll be a member at some point. But, yeah, let's. , see (laughs) 

[00:17:34] **Jeremy:** Yeah. And, and it, so it, it sounds like you're thinking that's more of a, a governance or a organizational aspect of note than it is a, a technical limitation. Is that right?

[00:17:47] **Luca:** Yeah. I obviously can't speak for the node technical steering committee, but I know that there's a significant chunk of the node technical steering committee that is, very favorable towards, uh, standards compliance. but parts of the Node technical steering committee are also not, they are either indifferent or are actively, I dunno if they're still actively working against this, but have actively worked against standards compliance in the past.

And because the node governance structure is very, yeah, is, is so, so open and let's, um, and let's, let's all these voices be heard, um, that just means that decision making processes within Node can take so long, like. . This is also why the fetch API took eight years to ship. Like this was not a technical problem.

and it is also not a technical problem. That Node does not have URL pattern support or, the file global or, um, that the web crypto API was not on this, on the global object until like late last year, right? Like, these are not technical problems, these are decision making problems. Um, and yeah, that was also part of the reason why we started Deno as, as like a separate thing, because like you can try to innovate node, from the inside, but innovating node from the inside is very slow, very tedious, and requires a lot of fighting.

And sometimes just showing somebody, from the outside like, look, this is the bright future you could have, makes them more inclined to do something.


## Why it takes so long to ship new features in Node

[00:19:17] **Jeremy:** Do, do you have a sense for, you gave the example of fetch taking eight years to, to get into node. Do you, do you have a sense of what the typical objection is to, to something like that? Like I, I understand there's a lot of people involved, but why would somebody say, I, I don't want this

[00:19:35] **Luca:** Yeah. So for, for fetch specifically, there was a, there was many different kinds of concerns. Um, one of the, I, I can maybe list two of them. One of them was for example, that the fetch API is not a good API and as such, node should not have it. which is sort of. missing the point of, because it's a standard API, how good or bad the API is is much less relevant because if you can share the API, you can also share a wrapper that's written around the api.

Right? and then the other concern was, node does need fetch because Node already has an HTTP API. Um, so, so these are both kind of examples of, of concerns that people had for a long time, which it took a long time to either convince these people or, or to, push the change through anyway. and this is also the case for, for other things like, for example, web, crypto, um, like why do we need web crypto?

We already have node crypto, or why do we need yet another streams? Implementation node already has four different streams implementations. Like, why do we need web streams? and the, the. Like, I don't know if you know this XKCD of, there's 14 competing standards. so let's write a 15th standard, to unify them all.

And then at the end we just have 15 competing standards. Um, so I think this is also the kind of concern that people were concerned about, but I, I think what we've seen here is that this is really not a concern that one needs to have because it ends up that, or it turns out in the end that if you implement web APIs, people will use web APIs and will use web APIs only for their new code.

it takes a while, but we're seeing this with ESM versus require like new code written with require much less common than it was two years ago. And, new code now using like Xhr, whatever it's called, form request or. You know, the one, I mean, compared to using Fetch, like nobody uses that name.

Everybody uses Fetch. Um, and like in Node, if you write a little script, like you're gonna use Fetch, you're not gonna use like Nodes, htp, dot get API or whatever. and we're gonna see the same thing with Readable Stream. We're gonna see the same thing with Web Crypto. We're gonna see, see the same thing with Blob.

I think one of the big ones where, where Node is still, I, I, I don't think this is one that's ever gonna get solved, is the, the Buffer global and Node. like we have the Uint8, this Uint8 global, um, and like all the run times including browsers, um, and Buffer is like a super set of that, but it's in global scope.

So it, it's sort of this non-standard extension of unit eight array that people in node like to use and it's not compatible with anything else. Um, but because it's so easy to get at, people use it anyway. So those are, those are also kind of problems that, that we'll have to deal with eventually. And maybe that means that at some point the buffer global gets deprecated and I don't know, probably can never get removed.

But, um, yeah, these are kinds of conversations that the no TSE is going have to have internally in, I don't know, maybe five years.


## Write once, have it run on any hosting platform

[00:22:37] **Jeremy:** Yeah, so at a high level, What's shipped in the browser, it went through the ECMAScript approval process. People got it into the browser. Once it's in the browser, probably never going away. And because of that, it's safe to build on top of that for these, these server run times because it's never going away from the browser.

And so everybody can kind of use it into the future and not worry about it. Yeah.

[00:23:05] **Luca:** Exactly. Yeah. And that's, and that's excluding the benefit that also if you have code that you can write once and use in both the browser and the server side around time, like that's really nice. Um, like that, that's the other benefit.

[00:23:18] **Jeremy:** Yeah. I think that's really powerful. And that right now, when someone's looking at running something in CloudFlare workers versus running something in the browser versus running something in. it's, I think a lot of people make the assumption it's just JavaScript, so I can use it as is. But it, it, there are at least currently, differences in what APIs are available to you.

[00:23:43] **Luca:** Yep. Yep.


## Why bundle so many things into Deno?

[00:23:46] **Jeremy:** Earlier you were talking about how Deno is more than just the runtime. It has a linter, formatter, file watcher there, there's all sorts of stuff in there. And I wonder if you could talk a little bit to the, the reasoning behind that

[00:24:00] **Luca:** Mm-hmm.

[00:24:01] **Jeremy:** Having them all be separate things.

[00:24:04] **Luca:** Yeah, so the, the reasoning here is essentially if you look at other modern run time or mo other modern languages, like Rust is a great example. Go is a great example. Even though Go was designed around the same time as Node, it has a lot of these same tools built in. And what it really shows is that if the ecosystem converges, like is essentially forced to converge on a single set of built-in tooling, a that built-in tooling becomes really, really excellent because everybody's using it.

And also, it means that if you open any project written by any go developer, any, any rest developer, and you look at the tests, you immediately understand how the test framework works and you immediately understand how the assertions work. Um, and you immediately understand how the build system works and you immediately understand how the dependency imports work.

And you immediately understand like, I wanna run this project and I wanna restart it when my file changes. Like, you immediately know how to do that because it's the same everywhere. Um, and this kind of feeling of having to learn one tool and then being able to use all of the projects, like being able to con contribute to open source when you're moving jobs, whatever, like between personal projects that you haven't touched in two years, you know, like being able to learn this once and then use it everywhere is such an incredibly powerful tool.

Like, people don't appreciate this until they've used a runtime or, or, or language which provides this to them. Like, you can go to any go developer and ask them if they would like. There, there's this, there's this saying in the Go ecosystem, um, that Go FMT is nobody's favorite, but, or, uh, wait, no, I don't remember what the, how the saying goes, but the saying essentially implies that the way that go FMT formats code, maybe not everybody likes, but everybody loves go F M T anyway, because it just makes everything look the same.

And like, you can read your friend's code, your, your colleagues code, your new jobs code, the same way that you did your code from two years ago. And that's such an incredibly powerful feeling. especially if it's like well integrated into your IDE you clone a repository, open that repository, and like your testing panel on the left hand side just populates with all the tests, and you can click on them and run them.

And if an assertion fails, it's like the standard output format that you're already familiar with. And it's, it's, it's a really great feeling. and if you don't believe me, just go try it out and, and then you will believe me, (laughs) 

[00:26:25] **Jeremy:** Yeah. No, I, I'm totally with you. I, I think it's interesting because with JavaScript in particular, it feels like the default in the community is the opposite, right? There's so many different ways. Uh, there are so many different build tools and testing frameworks and, formatters, and it's very different than, like you were mentioning, a go or a Rust that are more recent languages where they just include that, all Bundled in. Yeah.

[00:26:57] **Luca:** Yeah, and I, I think you can see this as well in, in the time that average JavaScript developer spends configuring their tooling compared to a rest developer. Like if I write Rust, I write Rust, like all day, every day. and I spend maybe two, 3% of my time configuring Rust tooling like. Doing dependency imports, opening a new project, creating a format or config file, I don't know, deleting the build directory, stuff like that.

Like that's, that's essentially what it means for me to configure my rest tooling. Whereas if you compare this to like a front-end JavaScript project, like you have to deal with making sure that your React version is compatible with your React on version, it's compatible with your next version is compatible with your ve version is compatible with your whatever version, right?

this, this is all not automatic. Making sure that you use the right, like as, as a front end developer, you developer. You don't have just NPM installed, no. You have NPM installed, you have yarn installed, you have PNPM installed. You probably have like, Bun installed. And, and, and I don't know to use any of these, you need to have corepack enabled in Node and like you need to have all of their global bin directories symlinked into your or, or, or, uh, included in your path.

And then if you install something and you wanna update it, you don't know, did I install it with yarn? Did I install it with N pNPM? Like this is, uh, significant complexity and you, you tend to spend a lot of time dealing with dependencies and dealing with package management and dealing with like tooling configuration, setting up esent, setting up prettier.

and I, I think that like, especially Prettier, for example, really showed, was, was one of the first things in the JavaScript ecosystem, which was like, no, we're not gonna give you a config where you, that you can spend like six hours configuring, it's gonna be like seven options and here you go. And everybody used it because, Nobody likes configuring things.

It turns out, um, and even though there's always the people that say, oh, well, I won't use your tool unless, like, we, we get this all the time. Like, I'm not gonna use Deno FMT because I can't, I don't know, remove the semicolons or, or use single quotes or change my tab width to 16. Right? Like, wait until all of your coworkers are gonna scream at you because you set the tab width to 16 and then see what they change it to.

And then you'll see that it's actually the exact default that, everybody uses. So it'll, it'll take a couple more years. But I think we're also gonna get there, uh, like Node is starting to implement a, a test runner. and I, I think over time we're also gonna converge on, on, on, on like some standard build tools.

Like I think ve, for example, is a great example of this, like, Doing a front end project nowadays. Um, like building new front end tooling that's not built on Vite Yeah. Don't like, Vite's it's become the standard and I think we're gonna see that in a lot more places.


## We should settle on what tools to use

[00:29:52] **Jeremy:** Yeah, though I, I think it's, it's tricky, right? Because you have so many people with their existing projects. You have people who are starting new projects and they're just searching the internet for what they should use. So you're, you're gonna have people on web pack, you're gonna have people on Vite, I guess now there's gonna be Turbo pack, I think is another one that's

[00:30:15] **Luca:** Mm-hmm.

[00:30:16] **Jeremy:** There's, there's, there's all these different choices, right? And I, I think it's, it's hard to, to really settle on one, I guess,

[00:30:26] **Luca:** Yeah,

[00:30:27] **Jeremy:** uh, yeah.

[00:30:27] **Luca:** like I, I, I think this is, this is in my personal opinion also failure of the Node Technical Steering committee, for the longest time to not decide that yes, we're going to bless this as the standard format for Node, and this is the standard package manager for Node. And they did, they sort of did, like, they, for example, node Blessed NPM as the standard, package manager for N for for node.

But it didn't innovate on npm. Like no, the tech nodes, tech technical steering committee did not force NPM to innovate NPMs, a private company ultimately bought by GitHub and they had full control over how the NPM cli, um, evolved and nobody forced NPM to, to make sure that package install times are six times faster than they were.

Three years ago, like nobody did that. so it didn't happen. And I think this is, this is really a failure of, of the, the, the, yeah, the no technical steering committee and also the wider JavaScript ecosystem of not being persistent enough with, with like focus on performance, focus on user experience, and, and focus on simplicity.

Like things got so out of hand and I'm happy we're going in the right direction now, but, yeah, it was terrible for some time. (laughs) 


## Node compatibility layer

[00:31:41] **Jeremy:** I wanna talk a little bit about how we've been talking about Deno in the context of you just using Deno using its own standard library, but just recently last year you added a compatibility shim where people are able to use node libraries in Deno.

[00:32:01] **Luca:** Mm-hmm.

[00:32:01] **Jeremy:** And I wonder if you could talk to, like earlier you had mentioned that Deno has, a different permissions model.

on the website it mentions that Deno's HTTP server is two times faster than node in a Hello World example. And I'm wondering what kind of benefits people will still get from Deno if they choose to use packages from Node.

[00:32:27] **Luca:** Yeah, it's a great question. Um, so I think a, again, this is sort of a like, so just to clarify what we actually implemented, like what we have is we have support for you to import NPM packages. Um, so you can import any NPM package from NPM, from your type script or JavaScript ECMAScript module, um, that you have, you already have for your Deno code.

Um, and we will under the hood, make sure that is installed somewhere in some directory globally. Like PNPM does. There's no local node modules folder you have to deal with. There's no package of Jason you have to deal with. Um, and there's no, uh, package. Jason, like versioning things you need to deal with.

Like what you do is you do import cowsay from NPM colon cowsay at one, and that will import cowsay with like the semver tag one. Um, and it'll like do the sim resolution the same way node does, or the same way NPM does rather. And what you get from that is that essentially it gives you like this backdoor to a callout to all of the existing node code that Isri been written, right?

Like you cannot expect that Deno developers, write like, I don't know. There was this time when Deno did not really have that many, third party modules yet. It was very early on, and I don't know the, you either, if you wanted to connect to Postgres and there was no Postgres driver available, then the solution was to write your own Postgres driver.

And that is obviously not great. Um, (laughs) . So the better solution here is to let users for these packages where there's no Deno native or, or, or web native or standard native, um, package for this yet that is importable with url. Um, specifiers, you can import this from npm. Uh, so it's sort of this like backdoor into the existing NPM ecosystem.

And we explicitly, for example, don't allow you to, create a package.json file or, import bare node specifiers because we don't, we, we want to stay standards compliant here. Um, but to make this work effectively, we need to give you this little back door. Um, and inside of this back door. All hell is like, or like everything is terrible inside there, right?

Like inside there you can do bare specifiers and inside there you can like, uh, there's package.json and there's crazy node resolution and underscore underscore DIRNAME and common js. And like all of that stuff is supported inside of this backdoor to make all the NPM packages work. But on the outside it's exposed as this nice, ESM only, NPM specifiers.

and the, the reason you would want to use this over, like just using node directly is because again, like you wanna use TypeScript, no config, like necessary. You want to use, you wanna have a formatter you wanna have a linter, you wanna have tooling that like does testing and benchmarking and compiling or whatever.

All of that's built in. You wanna run this on the edge, like close to your users and like 30 different, 35 different, uh, points of presence. Um, it's like, Okay, push it to your git repository. Go to this website, click a button two times, and it's running in 35 data centers. like this is, this is the kind of ex like developer experience that you can, you do not get.

You, I will argue that you cannot get with Node right now. Like even if you're using something like ts-node, it is not possible to get the same level of developer experience that you do with Deno. And the, the, the same like speed at which you can iterate, iterate on your projects, like create new projects, iterate on them is like incredibly fast in Deno.

Like, I can open a, a, a folder on my computer, create a single file, may not ts, put some code in there and then call Deno Run may not. And that's it. Like I don't, I did not need to do NPM install I did not need to do NPM init -y and remove the license and version fields and from, from the generated package.json and like set private to true and whatever else, right?

It just all works out of the box. And I think that's, that's what a lot of people come to deno for and, and then ultimately stay for. And also, yeah, standards compliance. So, um, things you build in Deno now are gonna work in five, 10 years, with no hassle.


## Node shims and testing

[00:36:39] **Jeremy:** And so with this compatibility layer or this, this shim, is it where the node code is calling out to node APIs and you're replacing those with Deno compatible equivalents?

[00:36:54] **Luca:** Yeah, exactly. Like for example, we have a shim in place that shims out the node crypto API on top of the web crypto api. Like sort of, some, some people may be familiar with this in the form of, um, Browserify shims. if anybody still remembers those, it's essentially. , your front end tooling, you were able to import from like node crypto in your front end projects and then behind the scenes your web packs or your browser replies or whatever would take that import from node crypto and would replace it with like the shim that was essentially exposed the same APIs node crypto, but under the hood, wasn't implemented with native calls, but was implemented on top of web crypto, or implemented in user land even.

And Deno does something similar. there's a couple edge cases of APIs that there's, where, where we do not expose the underlying thing that we shim to, to end users, outside of the node shim. So like there's some, some APIs that I don't know if I have a good example, like node nextTick for example.

Um, like to properly be able to shim node nextTick, you need to like implement this within the event loop in the runtime. and. , you don't need this in Deno, because Deno, you use the web standard queueMicrotask to, to do this kind of thing. but to be able to shim it correctly and run node applications correctly, we need to have this sort of like backdoor into some ugly APIs, um, which, which natively integrate in the runtime, but, yeah, like allow, allow this node code to run.

[00:38:21] **Jeremy:** A, anytime you're replacing a component with a, a shim, I think there's concerns about additional bugs or changes in behavior that can be introduced. Is that something that you're seeing and, and how are you accounting for that?

[00:38:38] **Luca:** Yeah, that's, that's an excellent question. So this is actually a, a great concern that we have all the time. And it's not just even introducing bugs, sometimes it's removing bugs. Like sometimes there's bugs in the node standard library which are there, and people are relying on these bugs to be there for the applications to function correctly.

And we've seen this a lot, and then we implement this and we implement from scratch and we don't make that same bug. And then the test fails or then the application fails. So what we do is, um, we actually run node's test suite against Deno's Shim layer. So Node has a very extensive test suite for its own standard library, and we can run this suite against, against our shims to find things like this.

And there's still edge cases, obviously, which node, like there was, maybe there's a bug which node was not even aware of existing. Um, where maybe this, like it's is, it's now standard, it's now like intended behavior because somebody relies on it, right? Like the second somebody relies on, on some non-standard or some buggy behavior, it becomes intended.

Um, but maybe there was no test that explicitly tests for this behavior. Um, so in that case we'll add our own tests to, to ensure that. But overall we can already catch a lot of these by just testing, against, against node's tests. And then the other thing is we run a lot of real code, like we'll try run Prisma and we'll try run Vite and we'll try run NextJS and we'll try run like, I don't know, a bunch of other things that people throw at us and, check that they work and they work and there's no bugs. Then we did our job well and our shims are implemented correctly. Um, and then there's obviously always the edge cases where somebody did something absolutely crazy that nobody thought possible. and then they'll open an issue on the Deno repo and we scratch our heads for three days and then we'll fix it.

And then in the next release there'll be a new bug that we added to make the compatibility with node better. so yeah, but I, yeah. Running tests is the, is the main thing running nodes test.


## Performance should be equal or better

[00:40:32] **Jeremy:** Are there performance implications? If someone is running an Express App or an NextJS app in Deno, will they get any benefits from the Deno runtime and performance?

[00:40:45] **Luca:** Yeah. It's actually, there is performance implications and they're usually. The opposite of what people think they are. Like, usually when you think of performance implications, it's always a negative thing, right? It's always okay. Like you, it's like a compromise. like the shim layer must be slower than the real node, right?

It's not like we can run express faster than node can run, express. and obviously not everything is faster in Deno than it is in node, and not everything is faster in node than it is in Deno. It's dependent on the api, dependent on, on what each team decided to optimize. Um, and this also extends to other run times.

Like you can always cherry pick results, like, I don't know, um, to, to make your runtime look faster in certain benchmarks. but overall, what really matters is that you do not like, the first important step for for good node compatibility is to make sure that if somebody runs your code or runs their node code in Deno or your other run type or whatever, It performs at least the same.

and then anything on top of that great cherry on top. Perfect. but make sure the baselines is at least the same. And I think, yeah, we have very few APIs where we behave, where we, where, where like there's a significant performance degradation in Deno compared to Node. Um, and like we're actively working on these things.

like Deno is not a, a, a project that's done, right? Like we have, I think at this point, like 15 or 16 or 17 engineers working on Deno, spanning across all of our different projects. And like, we have a whole team that's dedicated to performance, um, and a whole team that's dedicated node compatibility.

so like these things get addressed and, and we make patch releases every week and a minor release every four weeks. so yeah, it's, it's not a standstill. It's, uh, constantly improving.


## What should go into the standard library?

[00:42:27] **Jeremy:** Uh, something that kind of makes Deno stand out as it's standard library. There's a lot more in there than there is in in the node one. 

[00:42:38] **Luca:** Mm-hmm. 

[00:42:39] **Jeremy:** Uh, I wonder if you could speak to how you make decisions on what should go into it.

[00:42:46] **Luca:** Yeah, so early on it was easier. Early on, the, the decision making process was essentially, is this something that a top 100 or top 1000 NPM library implements? And if it is, let's include it. and the decision making is still short of based on that. But right now we've already implemented most of the low hanging fruit.

So things that we implement now are, have, have discussion around them whether we should implement them. And we have a process where, well we have a whole team of engineers on our side and we also have community members that, that will review prs and, and, and make comments. Open issues and, and review those issues, to sort of discuss the pros and cons of adding any certain new api.

And sometimes it's also that somebody opens an issue that's like, I want, for example, I want an API to, to concatenate two unit data arrays together, which is something you can really easily do node with buffer dot con cat, like the scary buffer thing. and there's no standards way of doing that right now.

So we have to have a little utility function that does that. But in parallel, we're thinking about, okay, how do we propose, an addition to the web standards now that makes it easy to concatenate iterates in the web standards, right? yeah, there's a lot to it. Um, but it's, it's really, um, it's all open, like all of our, all of our discussions for, for, additions to the standard library and things like that.

It's all, all, uh, public on GitHub and the GitHub issues and GitHub discussions and GitHub prs. Um, so yeah, that's, that's where we do that.

[00:44:18] **Jeremy:** Yeah, cuz to give an example, I was a little surprised to see that there is support for markdown front matter built into the standard library. But when you describe it as we look at the top a hundred thousand packages, are people looking at markdown? Are they looking at front matter? I, I'm sure there's a fair amount that are so that that makes sense.

[00:44:41] **Luca:** Yeah, like it sometimes, like that one specifically was driven by, like, our team was just building a lot of like little blog pages and things like that. And every time it was either you roll your own front matter part or you look for one, which has like a subtle bug here and the other one has a subtle bug there and really not satisfactory with any of them.

So, we, we roll that into the standard library. We add good test coverage for it good, add good documentation for it, and then it's like just a resource that people can rely on. Um, and you don't, you then don't have to make the choice of like, do I use this library to do my front meta parsing or the other library?

No, you just use the one that's in the standard library. It's, it's also part of this like user experience thing, right? Like it's just a much nicer user experience, not having to make a choice, about stuff like that. Like completely inconsequential stuff. Like which library do we use to do front matter parsing? (laughs)

[00:45:32] **Jeremy:** yeah. I mean, I think when, when that stuff is not there, then I think the temptation is to go, okay, let me see what node modules there are that will let me parse the front matter. Right. And then it, it sounds like probably ideally you want people to lean more on what's either in the standard library or what's native to the Deno ecosystem.

Yeah.

[00:46:00] **Luca:** Yeah. Like the, the, one of the big benefits is that the Deno Standard Library is implemented on top of web standards, right? Like it's, it's implemented on top of these standard APIs. so for example, there's node front matter libraries which do not run in the browser because the browser does not have the buffer global.

maybe it's a nice library to do front matter pricing with, but. , you choose it and then three days later you decide that actually this code also needs to run in the browser, and then you need to go switch your front matter library. Um, so, so those are also kind of reasons why we may include something in Strand Library, like maybe there's even really good module already to do something.

Um, but if there's certain reliance on specific node features that, um, we would like that library to also be compatible with, with, with web standards, we'll, uh, we might include in the standard library, like for example, YAML Parser, um, or the YAML Parser in the standard library is, is a fork of, uh, of the node YAML module.

and it's, it's essentially that, but cleaned up and, and made to use more standard APIs rather than, um, node built-ins.

[00:47:00] **Jeremy:** Yeah, it kind of reminds me a little bit of when you're writing a front end application, sometimes you'll use node packages to do certain things and they won't work unless you have a compatibility shim where the browser can make use of certain node APIs. And if you use the APIs that are built into the browser already, then you won't, you won't need to deal with that sort of thing.

[00:47:26] **Luca:** Yeah. Also like less Bundled size, right? Like if you don't have to shim that, that's less, less code you have to ship to the client.


## WebAssembly use cases

[00:47:33] **Jeremy:** Another thing I've seen with Deno is it supports running web assembly.

[00:47:40] **Luca:** Mm-hmm.

[00:47:40] **Jeremy:** So you can export functions and call them from type script. I was curious if you've seen practical uses of this in production within the context of Deno.

[00:47:53] **Luca:** Yeah. there's actually a Bunch of, of really practical use cases, so probably the most executed bit of web assembly inside of Deno right now is actually yes, build like, yes, build has a web assembly, build like yeses. Build is something that's written and go. You have the choice of either running. Um, natively in machine code as, as like an ELF process on, on Linux or on on Windows or whatever.

Or you can use the web assembly build and then it runs in web assembly. And the web assembly build is maybe 50% slower than the, uh, native build, but that is still significantly faster than roll up or, or, or, or I don't know, whatever else people use nowadays to do JavaScript Bun, I don't know. I, I just use es build always, um,

So, um, for example, the Deno website, is running on Deno Deploy. And Deno Deploy does not allow you to run Subprocesses because it's, it's like this edge run time, which, uh, has certain security permissions that it's, that are not granted, one of them being sub-processes. So it needs to execute ES build. And the way it executes es build is by running them inside a web assembly.

Um, because web assembly is secure, web assembly is, is something which is part of the JavaScript sandbox. It's inside the JavaScript sandbox. It doesn't poke any holes out. Um, so it's, it's able to run within, within like very strict security context. . Um, and then other examples are, I don't know, you want to have a HTML sanitizer, which is actually built on the real HTML par in a browser.

we, we have an hdml sanitizer called com or, uh, ammonia, I don't remember. There's, there's an HTML sanitizer library on denoland slash x, which is built on the html parser from Firefox. Uh, which like ensures essentially that your html, like if you do HTML sanitization, you need to make sure your HTML par is correct, because if it's not, you might like, your browser might parse some HTML one way and your sanitizer pauses it another way and then it doesn't sanitize everything correctly.

Um, so there's this like the Firefox HTML parser compiled to web assembly. Um, you can use that to. HTML sanitization, or the Deno documentation generation tool, for example. Uh, Deno Doc, there's a web assembly built for it that allows you to programmatically, like generate documentation for, for your type script modules.

Um, yeah, and, and also like, you know, deno fmt is available as a WebAssembly module for programmatic access and a Bunch of other internal Deno, programs as well. Like, or, uh, like components, not programs.

[00:50:20] **Jeremy:** What are some of the current limitations of web assembly and Deno for, for example, from web assembly, can I make HTTP requests? Can I read files? That sort of thing.

[00:50:34] **Luca:** Mm-hmm. . Yeah. So web assembly, like when you spawn as web assembly, um, they're called instances, WebAssembly instances. It runs inside of the same vm, like the same, V8 isolate is what they're called, but. it does not have it, it's like a completely fresh sandbox, sort of, in the sense that I told you that between a runtime and like an engine essentially implements no IO calls, right?

And a runtime does, like a runtime, pokes holds into the, the, the engine. web assembly by default works the same way that there is no holes poked into its sandbox. So you have to explicitly poke some holes. Uh, if you want to do HTTP calls, for example, when, when you create web assembly instance, it gives you, or you can give it something called imports, uh, which are essentially JavaScript function bindings, which you can call from within the web assembly.

And you can use those function bindings to do anything you can from JavaScript. You just have to pass them through explicitly. and. . Yeah. Depending on how you write your web assembly, like if you write it in Rust, for example, the tooling is very nice and you can just call some JavaScript code from your Rust, and then the build system will automatically make sure that the right function bindings are passed through with the right names.

And like, you don't have to deal with anything. and if you're writing go, it's slightly more complicated. And if you're writing like raw web assembly, like, like the web assembly, text format and compiling that to a binary, then like you have to do everything yourself. Right? It's, it's sort of the difference between writing C and writing JavaScript.

Like, yeah. What level of abstraction do you want? It's definitely possible though, and that's for limitations. it, the same limitations as, as existing browsers apply. like the web assembly support in Deno is equivalent to the web assembly support in Chrome. so you can do, uh, many things like multi-threading and, and stuff like that already.

but especially around, shared mutable memory, um, and having access to that memory from JavaScript. That's something which is a real difficulty with web assembly right now. yeah, growing web assembly memory is also rather difficult right now. There's, there's a, there's a couple inherent limitations right now with web assembly itself.

Um, but those, those will be worked out over time. And, and Deno is like very up to date with the version of, of the standard, it, it implements, um, through v8. Like we're, we're, we're up to date with Chrome Beta essentially all the time. So, um, yeah. Any, anything you see in, in, in Chrome beta is gonna be in Deno already.


## Deno Deploy

[00:52:58] **Jeremy:** So you talked a little bit about this before, the Deno team, they have their own, hosting. Platform called Deno Deploy. So I wonder if you could explain what that is.

[00:53:12] **Luca:** Yeah, so Deno has this really nice, this really nice concept of permissions which allow you to, sorry, I'm gonna start somewhere slightly, slightly unrelated. Maybe it sounds like it's unrelated, but you'll see in a second. It's not unrelated. Um, Deno has this really nice permission system which allows you to sandbox Deno programs to only allow them to do certain operations.

For example, in Deno, by default, if you try to open a file, it'll air out and say you don't have read permissions to read this file. And then what you do is you specify dash, dash allow read um, maybe you have to give it. they can either specify, allow, read, and then it'll grant to read access to the entire file system.

Or you can explicitly specify files or folders or, any number of things. Same goes for right permissions, same goes for network permissions. Um, same goes for running subprocesses, all these kind of things. And by limiting your permissions just a little bit. Like, for example, by just disabling sub-processes and foreign function interface, but allowing everything else, allowing reeds and allowing network access and all that kind of stuff.

we can run Deno programs in a way that is significantly more cost effective to you as the end user than, and, and like we can cold start them much faster than, like you may be able to with a, with a more conventional container based, uh, system. So what, what do you, what Deno Deploy is, is a way to run JavaScript or Deno Code, on our data centers all across the world with very little latency.

like you can write some JavaScript code which execute, which serves HTTP requests deploy that to our platform, and then we'll make sure to spin that code up all across the world and have your users be able to access it through some URL or, or, or some, um, custom domain or something like that. and this is some, this is very similar to CloudFlare workers, for example.

Um, and it's like Netlify Edge functions is built on top of Deno Deploy. Like Netlify Edge functions is implemented on top of Deno Deploy, um, through our sub hosting product. yeah, essentially Deno Deploy is, is, um, yeah, a cloud hosting service for JavaScript, um, which allows you to execute arbitrary JavaScript.

and there there's a couple, like different directions we're going there. One is like more end user focused, where like you link your GitHub repository and. Like, we'll, we'll have a nice experience like you do with Netlify and Versace, that word like your commits automatically get deployed and you get preview deployments and all that kind of thing.

for your backend code though, rather than for your front end websites. Although you could also write front-end websites and you know, obviously, and the other direction is more like business focused. Like you're writing a SaaS application and you want to allow the user to customize, the check like you're writing a SaaS application that provides users with the ability to write their own online store.

Um, and you want to give them some ability to customize the checkout experience in some way. So you give them a little like text editor that they can type some JavaScript into. And then when, when your SaaS application needs to hit this code path, it sends a request to us with the code, we'll execute that code for you in a secure way.

In a secure sandbox. You can like tell us you, this code only has access to like my API server and no other networks to like prevent data exfiltration, for example. and then you do, you can have all this like super customizable, code in inside of your, your SaaS application without having to deal with any of the operational complexities of scaling arbitrary code execution, or even just doing arbitrary code execution, right?

Like it's, this is a very difficult problem and give it to someone else and we deal with it and you just get the benefits. yeah, that's Deno Deploy, and it's built by the same team that builds the Deno cli. So, um, all the, all of your favorite, like Deno cli, or, or Deno APIs are available in there.

It's just as web standard is Deno, like you have fetch available, you have blob available, you have web crypto available, that kind of thing. yeah.


## Running code in V8 isolates

[00:56:58] **Jeremy:** So when someone ships you their, their code and you run it, you mentioned that the, the cold start time is very low. Um, how, how is the code being run? Are people getting their own process? It sounds like it's not, uh, using containers. I wonder if you could explain a little bit about how that works.

[00:57:20] **Luca:** Yeah, yeah, I can, I can give a high level overview of how it works. So, the way it works is that we essentially have a pool of, of Deno processes ready. Well, it's not quite Deno processes, it's not the same Deno CLI that you download. It's like a modified version of the Deno CLI based on the same infrastructure, that we have spun up across all of our different regions across the world, uh, across all of our different data centers.

And then when we get a request, we'll route that request, um, the first time we get request for that, that we call them deployments, that like code, right? We'll take one of these idle Deno processes and will assign that code to run in that process, and then that process can go serve the requests. and these process, they're, they're, they're isolated and they're, you.

it's essentially a V8 isolate. Um, and it's a very, very slim, it's like, it's a much, much, much slimmer version of the Deno cli essentially. Uh, which the only thing it can do is JavaScript execution and like, it can't even execute type script, for example, like type script is we pre-process it up front to make the the cold start faster.

and then what we do is if you don't get a request for some amount of. , we'll, uh, spin down that, um, that isolate and, uh, we'll spin up a new idle one in its place. And then, um, if you get another request, I don't know, an hour later for that same deployment, we'll assign it to a new isolate. And yeah, that's a cold start, right?

Uh, if you have an isolate which receives, or a, a deployment rather, which receives a Bunch of traffic, like let's say you receive a hundred requests per second, we can send a Bunch of that traffic to the same isolate. Um, and we'll make sure that if, that one isolate isn't able to handle that load, we'll spin it out over multiple isolates and we'll, we'll sort of load balance for you.

Um, and we'll make sure to always send to the, to the point of present that's closest to, to the user making the request. So they get very minimal latency. and they get we, we've these like layers of load balancing in place and, and, and. I'm glossing over a Bunch of like security related things here about how these, these processes are actually isolated and how we monitor to ensure that you don't break out of these processes.

And for example, Deno Deploy does, it looks like you have a file system cuz you can read files from the file system. But in reality, Deno Deploy does not have a file system. Like the file system is a global virtual file system. which is, is, uh, yeah, implemented completely differently than it is in Deno cli.

But as an end user you don't have to care about that because the only thing you care about is that it has the exact same API as the Deno cli and you can run your code locally and if it works there, it's also gonna work in deploy. yeah, so that's, that's, that's kind of. High level of Deno Deploy. If, if any of this sounds interesting to anyone, by the way, uh, we're like very actively hiring on, on Deno Deploy.

I happen to be the, the tech lead for, for a Deno Deploy product. So I'm, I'm always looking for engineers, to, to join our ranks and, and build cool distributed systems. Deno.com/jobs.

[01:00:15] **Jeremy:** for people who aren't familiar with the isolates, are these each run in their own processes, or do you have a single process and that has a whole Bunch of isolates inside it?

[01:00:28] **Luca:** in, in the general case, you can say that we run, uh, one isolate per process. but there's many asterisks on that. Um, because, it's, it's very complicated. I'll just say it's very complicated. Uh, in, in the general case though, it's, it's one isolate per process.

Yeah.


## Configuring permissions

[01:00:45] **Jeremy:** And then you touched a little bit on the permissions system. Like you gave the example of somebody could have a website where they let their users give them code to execute. how does it look in terms of specifying what permissions people have? Like, is that a configuration file? Are those flags you pass in?

What, what does that look?

[01:01:08] **Luca:** Yeah. So, so that product is called sub hosting. It's, um, slightly different from our end user platform. Um, it's essentially a service that allows you to, like, you email us, well, we'll send you a, um, onboard you, and then what you can do is you can send HTTP requests to a certain end point with a, authentication token and.

a reference to some code to execute. And then what we'll do is, we'll, um, when we receive that HTTP request, we'll fetch the code, it's spin up and isolate, execute the code. execute the code. We serve the request, return you the response, um, and then we'll pipe logs to you and, and stuff like that.

and the, and, and part of that is also when we, when we pull the, um, the, the code for to spin up the isolate, that code doesn't just include the code that we're executing, but also includes things like permissions, and, and various other, we call this isolate configuration. Um, you can inspect, this is all public.

we have public docs for this at Deno.com/subhosting. I think. Yes, Deno.com/subhosting.

[01:02:08] **Jeremy:** And is that built on top of something that's a part of the public Deno project, the open source part? Or is this specific to this sub hosting product?

[01:02:19] **Luca:** Um, so the underlying engine or underlying runtime that executes the code here, like all of the code execution is performed by code, which is execute, which is public. Like all our, our, yeah, it uses, the Deno CLI just strips out a Bunch of stuff. It doesn't need the orchestration code, is not public.

The orchestration code is proprietary. and yeah, if you have use cases that where you would like to run this orchestration code on your own infrastructure, and yeah, you have interesting use cases, please email us. We would love to hear from you.

[01:02:51] **Jeremy:** separate from the, the orchestration, if it's more of an example of, let's say I deploy a Deno application and in the case that someone was able to get some, like malicious code or URLs into my application, could I tell Deno I only want this application to be able to call out to these URLs for just as an example?

[01:03:18] **Luca:** yes. So it's, it's slightly more complicated because you can't actually tell it that it can only call out to specific URLs, but you can tell it to call out only to specific domains or IP addresses. which sort of the same thing, but, uh, just slightly different layer of abstraction. Yeah, you can do that.

the allow net flag, allows you to specify a set of domains to allow requests to those domains. Yes,

[01:03:41] **Jeremy:** I see. So on the, user facing open source part, there are configuration flags where you could say, I want this application to be able to access these domains, or I don't want it to be able to use IO or whatever

[01:03:56] **Luca:** Yeah, exactly.

[01:03:57] **Jeremy:** their, their flags.

[01:03:59] **Luca:** Yeah. And, and on, on subhosting, this is done via the isolate configuration, which is like a JSON blob. And, yeah, like there, there's, it's, but ultimately it's all, it's all sort of, the same concept, just slightly different interfaces because like, like the, the subhosting one needs to be programmatic interface instead of, uh, something you type as an end user.

Right?




## Why deploy your application on the edge?

[01:04:20] **Jeremy:** One of the things you mentioned about Deno Deploy is it's, centered around deploying your application code to a Bunch of different locations. And you also mentioned the, the cold start times very low.

could you kind of give the case for wanting your application code at a Bunch of different sites?

[01:04:38] **Luca:** Mm-hmm. . Yeah. So the, the, the, the main benefit of this is that when your user makes request for your application, um, you don't have to round trip back to, um, wherever centrally hosted your application would otherwise be. Like, if you are, a, a startup, even if you're just in the US for example, it's nice to have, points of presence, not just on one of the US coasts, but on both of the US coasts because that means that your round trip time is not gonna be a hundred milliseconds, but it's gonna be 20 milliseconds.

this sort of relies on. the, like, this doesn't, there's obviously always the problem here that if your database lives in only one of the two coasts, you still need to do the round trip. And there's solutions to this, which is one caching, uh, that's the, the, the obvious sort of boring solution. Um, and then there's the solution of using databases which are built exactly for this.

For example, CockroachDB is a database which is Postgres compatible, but it's really built for, um, global distribution and built for being able to shard data across regions and have different, um, primary regions for different, uh, shards of your, of your, of your tables. which means, for example, you could have the, your users on the East coast, their data could live on a database in the east coast and your users on the west coast, their data could live on a database on the west coast.

and. your like admin panel needs to show all of them. It has an aggregate view over both coasts, right? like this is something which, which something like CockroachDB can do and it can be a really great, um, great thing here. And, we acknowledge that this is not something which is very easy to do right now and Deno tries to make everything very easy.

So you can imagine that this is something we're working on and we're working on, on database solutions. And actually I should more generally say persistent solutions that allow you to persist data, in a way that makes sense for an edge system like this. Um, where the data has persisted close to users that need it.


## Consistency in local development vs deployment

[01:06:44] **Luca:** Um, and data is cached around the world. and you still have sort of semantics, which, which are consistent with the semantics that you have, when you're locally developing your application. Like you don't want, for example, your local application development. , you don't want there to be like strong consistency there, but then in production you have eventual consistency where suddenly, I don't know, all of your code breaks because you didn't, your US west region didn't pick up the changes from US east because it's eventually consistent, right?

I mean, this is a problem that we see with a lot of the existing solutions here. like specifically CloudFlare KV for example. CloudFlare KV is, um, a single primary is a system with, with single primary, um, right regions, where there's just a Bunch of caching going on. And this leads to ventral consistency, which can be very confusing for, for end user developers.

Um, especially because if you're using this locally, the local emulator does not emulate the eventual consistency, right? so this, this, this can become very confusing very quickly. And so a, anything that we build in, in this persistence field, for example, we take very, we very seriously, um, Weigh these trade offs and make sure that if there's something that's eventually consistent, it's very clear and it works the same way, the same eventually consistent way in the cli.

[01:08:03] **Jeremy:** So for someone, let's say they haven't made that jump yet to use a cockroach. They, they just have their. their database instance in AWS East or whatever. does having the code at the edge where it all ends up needing to go to east, is that better than having the code be located next to the database?

[01:08:27] **Luca:** Yeah. Yeah. It, it, it totally does. Um, there's, there's def there's different, um, there, there's trade-offs here, right? Obviously, like if you have a, a, if you have an admin panel, for example, or a, a like user dashboard, which is very, very reliant on data from your database, and for every single request needs to fetch fresh data from the database, then maybe the trade off isn't worth it.

But most applications are not like that. Most applications are, for example, you have a landing page and that landing page needs to do AB tests. and those AB tests are based on some heuristic that you can fetch from the database every five seconds. That's fine. Like, it doesn't need to be perfect, right?

So you, you have caching in place, which, um, like by doing this caching locally to the user, um, and, and still being able to programmatically control this, like based on, I don't know, the user's user agent or, the IP address of the user or the region of the user, or. the past browsing history of that user through as, as measured by their cookies or whatever else, right?

being able to do these highly user customized actions very close to the user, means that like latency is, is like, this is a much better user experience than if you have to do the roundtrip, especially if you're a, a startup or, or, or, or a, um, service which is globally distributed and, and serves not just users in the US or the EU but like all across the world.


## Caching options

[01:09:52] **Jeremy:** And when you talk about caching in the context of Deno Deploy, is there a cache native to the system or are you expecting someone to have, uh, a Redis or a memcached, that sort of thing?

[01:10:07] **Luca:** Yeah. So Deno Deploy, actually has, there's a built, there's a, there's a web cache api, um, which is also the web cache API that's used by service workers and, and others. and CloudFlare also implements this cache api. Um, and this is something that's implemented in Deno cli, and it's gonna be coming to Deploy this quarter, which is, that's the native way to do caching, and otherwise you can also use Redis you can use services like Upstash or, uh, even like primitive in-memory caches where it's just an LRU that's in memory, like a, like a JavaScript data structure, right?

or even just a JavaScript map or JavaScript object, with a, with a time on it. And you automatically, and like every time you read from it and the time is above some certain threshold, you delete the cache and go fetch it again, right? Like this is, there's many things that you could consider a cache that are not like Redis or, or, or, or like the web cache api.

So there's, there's ways to do that. And there's also a Bunch of, like, modules on, in the standard library, or not in the standard library story in the, in the third party module registry and also on NPM that you can use to, to implement different cache behaviors.

[01:11:15] **Jeremy:** And when you give the example of a in memory cache, when you're running in Deno deploy, you're running in these isolates, which presumably can be shut down at any time. So what kind of guarantees do users have that whatever they put into memory will still be there?

[01:11:34] **Luca:** none like the, it's, it's a cache, right? The cache can be evicted at any time. Your isolate can be restarted at any time. It can be shut down. You can be moved to a different region. The data center could go for, go down for maintenance. Like this is something your application has to be built in, in a way that it is tolerant to, to restarts essentially.

but because it's a cache, that's fine. Because if the cache expires or, or, or the cache is cleared through some external means, the worst thing that happens is that you have a cold request again, right? And, if you're serving like a hundred requests a second, I can essentially guarantee to you that not every single request will invoke a cold start.

Like, I can guarantee to you that probably less than 0.1% of requests will, will cause a cold start. this is not like SLA anywhere. Um, because it's like totally up to, to however the, the system decides to scale you. but yeah, like it's, it, it would be very wasteful for us, for example, to spin up a new isolate for every request.

So we don't, we reuse isolates wherever possible. yeah. It's like it's in our best interest to not cold start you, um, because it's expensive for us to do all the CPU work to, to cold start an isolate, right?


## Working with CDNs

[01:12:47] **Jeremy:** and typically with applications, people will put a, a CDN in front and they'll use things like cache control headers to be able to serve straight from the CDN Is that a supported use case with Deno Deploy or are there anything that, anything that people should be aware of when they're doing that sort of thing?

[01:13:09] **Luca:** Yeah, so you can do that. Um, like you could put a cache in front of Deploy but in most cases it's really not necessary. Um, because the main reasons people use CDNs is, it is essentially to like do this global distribution problem, right? Like you, you want to be able to cache close to users, but if your end application is already executing close to users, the cost of a, of a, of serving something, like serving a request from a JavaScript cache is like marginal.

It's so low. there's, there's like no nearly no CPU time involved here. it's, it's network bandwidth. That's the, that's the limiting factor and that's the limiting factor for all CDNs. Uh, so, so whether you're serving on Deploy or you have a, a separate CDN that you put in front of it, hmm. not really that big a difference.

Like you can do it. but I don't know. Deno.com doesn't, or, or, and Deno.land, like they don't have a CDN in front of them. They're running bare on, on Deno Deploy and, yeah, it's fine.

[01:14:06] **Jeremy:** So for, even for things like images, for example, something that. Somebody might store in object storage and put a CDN in in front. 

[01:14:17] **Luca:** Mm-hmm. 

[01:14:18] **Jeremy:** are you suggesting that people could put it on Deno deployed directly or just kind of curious what your thoughts are there?

[01:14:26] **Luca:** Yeah. Uh, like if you have a blog and your profile image is, is part of your blog, right? And you can put that in your static file folder and serve that directly from your Deno Deploy application, like that's totally cool. Uh, you should do that because that's obvious and that's the obvious way to do things.

if you're specifically building like a, image serving CDN , go reach out to us because we'd love to work with you. But also, um, like there's probably different constraints that you have. Um, like you probably very, very, very much care about network bandwidth costs, um, because that is like your one number one primary cost factor.

so yeah, it's just what's the trade off? What, what trade-offs are you willing to make? Like does some other provider give you a lower network bandwidth cost? I would argue that if you're building an, like an image cdn, then you'd probably, like, even if you have to write your application code in Haskell or in whatever, it's probably worth it if you can get like a cent cheaper gigabyte transfer fees.

just because that is like 100% of your, of your costs, um, is, is network bandwidth. So it's really a trade off based on what, what you're trying to build.


## Workloads currently not handled by Deno Deploy (Coming soon)

[01:15:36] **Jeremy:** And if I understand correctly, Deno Deploy, it's centered around applications. That take HTTP requests. So it could be a website, it could be an API that sort of thing. and sometimes when people build applications, they have other things surrounding them. They'll, they'll need scheduled jobs. They may need some form of message queue, things like that.

Things that don't necessarily fit into what Deno Deploy currently hosts. And so I wonder for things like that, what you recommend people would do while working with Deno Deploy.

[01:16:16] **Luca:** Yeah. Great question. unfortunately I can't tell you too much about that without, like, spoiling everything (laughs), but what I'm gonna say is you should keep your eyes peeled on our blog over the next two to three months here. I consider message queues and like, especially message queues they are a persistence feature and we are currently working on persistence features.

So yeah, that's all I'm gonna say. But, uh, you can expect Deno deployed to do things other than, um, just HTTP requests in the not so far. Future, and like cron jobs and stuff like that. Also, uh, at some point, yeah.


## Who's using deno?

[01:16:54] **Jeremy:** All right. We'll look, we'll look out for that I guess as we wrap up, maybe you could give some examples of who's using Deno and, and what types of projects do you think are are ideal for Deno?

[01:17:11] **Luca:** Yeah. yeah. Uh, Deno or Deno Deploy, like do you know, like, do you know as in all of Deno or Deno deploy specifically?

[01:17:17] **Jeremy:** I, I mean, I guess either (laughs)

[01:17:19] **Luca:** Okay. . Okay. Okay. Yeah, yeah. Uh, let's, let's do it. So, one really cool use case, for example, for Deno is Slack. Uh, slack has this app platform that they're building, um, which allows you to execute arbitrary JavaScript from within inside of Slack, in response to like slash commands and like actions. I dunno if you've ever seen like those little buttons you can have in messages if you press one of those buttons, like that can execute some Deno code.

And Slack has built like this entire platform around that, and it makes use of Deno's like security features and, and built in tooling and, and all that kind of thing. Um, and that's really cool. And Netlify has built edge functions like, which is like a really, really awesome primitive they have for, for being able to customize outgoing requests to even, come up with completely new requests on the spot, um, as part of their CDN layer.

Uh, also built on top of Deno. And GitHub has built, like this platform called, flat, which allows you to like sort of, um, on cron schedules, pull data, um, into git repositories and, and process that and, and post-process that and, and, and do do things with that. And it's integrated with GitHub actions, all kind of thing.

It's kind of cool. Supabase also has some Edge has like an Edge functions product that's built on top of Deno. I'm just thinking about other, like those are, those are the obvious ones that are on the homepage. there's, I, I know for example, there's a image CDN actually that's serves images with Deno, like 400 million of them a day.

kind of related to what we were talking about earlier. Actually, I don't know if it's still 400 million. I think it's more, um, the last data I got from them was like maybe eight months ago. So probably more at this point. Um, . Yeah. A Bunch of cool, cool, cool things like that. Um, we have like a really active discord channel and there's always people showcasing what kind of stuff they built in there that we have a showcase channel.

I think that's like, if, if you're really interested in like what people are, what cool things people are building with, you know, that's like, that's a great place to, to look. I think actually we maybe also have a showcase. Do we have Deno.land/showcase? I don't remember. Show case. Oh yeah, we do Deno.com/showcase, which is a page of like a Bunch of Yeah. Projects built with Deno or, or, or products using Deno or, um, other things like that.

[01:19:35] **Jeremy:** Cool. if people wanna learn more about Deno or see what you're up to, where should they head?

[01:19:42] **Luca:** Yeah. Uh, if you wanna learn more about Deno Cli, head to Deno.land. If you wanna learn more about Deno Deploy, head to Deno.com/deploy. Um, if you want to chat to me, uh, you can hit me up on my website, lcas.dev. if you wanna chat about Deno, you can go to discord.gg/deno. yeah, and if you're interested in any of this and thought that maybe you have something to contribute here, you can either become an open source contributor on our open source project, or this is really something you wanna work on and you like distributed systems or systems engineering or fast performance, head to deno.com/jobs and, send in your resume.

We're, we're very actively hiring and, be super excited to, to, work with you.

[01:20:20] **Jeremy:** All right, Luca. Well thank you so much for coming on Software Engineering Radio.

[01:20:24] **Luca:** Thank you so much for having me.

</div>