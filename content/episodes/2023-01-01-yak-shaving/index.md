+++
title = "Victor Adossi on Yak Shaving"

description = "Victor talks about his stack and side projects"

[extra]
episode_url = "https://pinecast.com/listen/9e1646da-2f0d-432c-be41-4995c4180468.mp3"
+++

Victor is a software consultant in Tokyo who describes himself as a yak shaver. He writes on his blog at [vadosware](https://vadosware.io) and curates [Awesome F/OSS](https://awsmfoss.com/), a mailing list of open source products. He's also a contributor to the [Open Core Ventures blog](https://opencoreventures.com/blog/).

Before our conversation Victor wrote a [structured summary of how he works on projects](https://vadosware.io/post/software-sessions-interview-2022/). I recommend checking that out in addition to the episode.

### Topics covered:

- Most people should use [Dokku](https://dokku.com/) or [CapRover](https://caprover.com/) 
- But he uses [Kubernetes](https://kubernetes.io/) anyways
- Hosting a Database in Kubernetes
- Learning technology
- You don't really know a thing until something goes wrong
- History of Frontend Development
- Context from lower layers of the stack and historical projects
- Good project pages have comparisons to other products
- Choosing technologies
- Language choice affects maintainability
- Knowing an ecosystem
- Victor's preferred stack
- Technology bake offs
- Posting findings means you get free corrections
- Why people use medium instead of personal sites

### Victor

- [VADOSWARE](https://vadosware.io/) - Blog
- [How Victor works on Projects](https://vadosware.io/post/software-sessions-interview-2022/) - Companion post for this episode
- [Awesome FOSS](https://awsmfoss.com/) - Curated list of OSS projects
- [NimbusWS](https://nimbusws.com/) - Hosted OSS built on top of budget cloud providers
- [Unvalidated Ideas](https://unvalidatedideas.com/) - Startup ideas for side project inspiration
- [PodcastSaver](https://podcastsaver.com/nerds) - Podcast index that allows you to choose Postgres or MeiliSearch and compare performance and results of each

### Victor's preferred stack

- [Docker](https://www.docker.com/) - Containers
- [Kubernetes](https://kubernetes.io/) - Container provisioning (Though at the beginning of the episode he suggests [Dokku](https://dokku.com/) for single server or [CapRover](https://caprover.com/) for multiple)
- [TypeScript](https://www.typescriptlang.org/) - JavaScript with syntax for types. Victor's default choice.
- [Rust](https://www.rust-lang.org/) - Language he uses if doing embedded work, performance is critical, or more correctness is desired
- [Haskell](https://www.haskell.org/) - Language he uses if correctness and type system is the most important for the project
- [Postgresql](https://www.postgresql.org/) - General purpose database that's good enough for most use cases including full text search.
- [KeyDB](https://docs.keydb.dev/) - Redis compatible database for caching. Acquired by Snap and then made open source. Victor uses it over Redis because it is multi threaded and supports flash storage without a Redis Enterprise license.
- [Pulumi](https://www.pulumi.com/) - Provision infrastructure with the languages you're already using instead of a specialized one or YAML
- [Svelte](https://www.svelte.dev/) and [SvelteKit](https://kit.svelte.dev/) - Preferred frontend stack. Previously used [Nuxt](https://nuxtjs.org/).

### Search engines

- [Postgres Full Text Search vs the rest](https://supabase.com/blog/postgres-full-text-search-vs-the-rest)
- [Optimizing Postgres Text Search with Trigrams](https://alexklibisz.com/2022/02/18/optimizing-postgres-trigram-search)
- [OpenSearch](https://opensearch.org/) - Amazon's fork of Elasticsearch
- [typesense](https://typesense.org/)
- [meilisearch](https://www.meilisearch.com/)
- [sonic](https://github.com/valeriansaliou/sonic)
- [Quickwit](https://github.com/quickwit-oss/quickwit)

### JavaScript build tools
- [Babel](https://babeljs.io/)
- [SWC](https://swc.rs/)
- [Webpack](https://webpack.js.org/)
- [esbuild](https://esbuild.github.io/)
- [parcel](https://parceljs.org/)
- [Vite](https://vitejs.dev/)
- [Turbopack](https://turbo.build/pack)

### JavaScript frameworks
- [React](https://reactjs.org/)
- [Vue](https://vuejs.org/)
- [Svelte](https://svelte.dev/)
- [Ember](https://emberjs.com/)

### Frameworks built on top of frameworks
- [Next](https://nextjs.org/) - React
- [Nuxt](https://nuxtjs.org/) - Vue
- [SvelteKit](https://kit.svelte.dev/) - Svelte
- [Astro](https://astro.build/) - Multiple

### Historical JavaScript tools and frameworks
- [Underscore](https://underscorejs.org/)
- [jQuery](https://jquery.com/)
- [MooTools](https://mootools.net/)
- [Backbone](https://backbonejs.org/)
- [AngularJS](https://angularjs.org/)
- [Knockout](https://knockoutjs.com/)
- [Aurelia](https://aurelia.io/)
- [GWT](https://www.gwtproject.org/)
- [Bower](https://bower.io/) - Frontend package manager
- [Grunt](https://gruntjs.com/) - Task runner
- [Gulp](https://gulpjs.com/) - Task runner

### Related Links

- [Dokku](https://dokku.com/) - Open source single-host alternative to Heroku
- [Cloud Native Buildpacks](https://buildpacks.io/) - Buildpacks created by Heroku and Pivotal and used by Dokku
- [CapRover](https://caprover.com/) - An open source PaaS-like abstraction built on top of Docker Swarm
- [Kelsey Hightower's tweet about being cautious about running databases on Kubernetes](https://twitter.com/kelseyhightower/status/1109715314709692417)
- [Settling the Myth of Transparent HugePages for Databases](https://www.percona.com/blog/2019/03/06/settling-the-myth-of-transparent-hugepages-for-databases/)
- [Kubernetes Container Storage Interface (CSI)](https://kubernetes-csi.github.io/docs/)
- [Kubernetes Local Persistent Volumes](https://kubernetes.io/docs/concepts/storage/volumes/#local)
- [Longhorn](https://longhorn.io/) - Distributed block storage for Kubernetes
- [Postgres docs](https://www.postgresql.org/docs/current/index.html)
- [Postgres TOAST](https://wiki.postgresql.org/wiki/TOAST)
- [Everything I've seen on optimizing Postgres on ZFS](https://vadosware.io/post/everything-ive-seen-on-optimizing-postgres-on-zfs-on-linux/)
- [Kubernetes Workload Resources](https://kubernetes.io/docs/concepts/workloads/controllers/)
- [Kubernetes Network Plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)
- [Kubernetes Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
- [Traefik](https://traefik.io/)
- [Kubernetes the Hard Way](https://github.com/kelseyhightower/kubernetes-the-hard-way) (Setting up a cluster in a way that optimizes for learning)
- [How does TLS work](https://freecontent.manning.com/how-does-tls-work/)
- [Let's Encrypt](https://letsencrypt.org/)
- [Cert manager for Kubernetes](https://cert-manager.io/)
- [Choose Boring Technology](https://boringtechnology.club/)
- [A Linux user's guide to Logical Volume Management](https://opensource.com/business/16/9/linux-users-guide-lvm)
- [Docker networking overview](https://docs.docker.com/network/)
- [Kubernetes Scheduler](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/)
- [Tauri](https://tauri.app/) - Build desktop applications with web technology and Rust
- [ripgrep](https://github.com/BurntSushi/ripgrep) - CLI tool to recursively search directory for a regex pattern (Meant to be a rust replacement for grep)
- [angle-grinder / ag](https://github.com/rcoh/angle-grinder) - CLI tool to parse and process log files written in rust
- [Object.observe ECMAScript Proposal to be Withdrawn](https://www.infoq.com/news/2015/11/object-observe-withdrawn/)
- [Ruby on Rails](https://rubyonrails.org/) - Ruby web framework
- [Django](https://www.djangoproject.com/) - Python web framework
- [Laravel](https://laravel.com/) - PHP web framework
- [Adonis](https://adonisjs.com/) - JavaScript
- [NestJS](https://nestjs.com/) - JavaScript
- [What is a NullPointerException, and how do I fix it?](https://stackoverflow.com/questions/218384/what-is-a-nullpointerexception-and-how-do-i-fix-it)
- [Mastodon](https://joinmastodon.org/)
- [Clap](https://github.com/clap-rs/clap) - CLI argument parser for Rust
- [AWS CDK](https://aws.amazon.com/cdk/) - Provision AWS infrastructure using programming languages
- [Terraform](https://www.terraform.io/) - Provision infrastructure with terraform language
- [URL canonicalization of duplicate pages and the use of the canonical tag](https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls) - Used by [dev.to](https://dev.to) to send google traffic to the original blogpost instead of dev.to

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** This episode, I talk to Victor Adossi who describes himself as a yak shaver. Someone who likes trying a whole bunch of different technologies, seeing the different options. We talk about what he uses, the evolution of front end development, and his various projects.

Talking to just different people it's always good to get where they're coming from because something that works for Google at their scale is going to be different than what you're doing with one of your smaller projects.

[00:00:31] **Victor:** Yeah, the context. Of course in direct conflict with that statement, I definitely use Google technology despite not needing to at all right? Like, you know, 99% of people who are doing like people like to call it indiehacking or building small products could probably get by with just Dokku. If you know Dokku or like CapRover. Are two projects that'll be like, Oh, you can just push your code here, we'll build it up like a little mini Heroku PaaS thing and just go on one big server, right? Like 99% of the people could just use that. But of course I'm not doing that. So I'm a bit of a hypocrite in that sense.

I know what I should be doing, but I'm not doing that. I am writing a Kubernetes cluster with like five nodes for no reason. Uh, yeah, I dunno, people don't normally count the controllers.

[00:01:24] **Jeremy:** Dokku and CapRover, I think those are where it's supposed to create a heroku like experience I think it's based off of the heroku buildpacks right? At least Dokku is?

[00:01:36] **Victor:** Yeah Buildpacks has actually been spun out into like a community thing so like pivotal and heroku, it's like buildpacks.io, they're trying to build a wider standard around it so that more people can get involved.

And buildpacks are actually obviously fantastic as a technology and as a a process piece. There's not much else like them and you know, that's obvious from like Heroku's success and everything. I know Dokku uses that. I don't know that Caprover does, but I haven't, I haven't really run Caprover that much.

They, they probably do. Like at this point if you're going to support building from code, it seems silly to try and build your own buildpacks. Cause that's what you will do, eventually. So you might as well use what's there. 

Anyway, this is like just getting to like my personal opinions at this point, but like, if you think containers are a bad idea in 2022, You're wrong, you should, you should stop. Like you should, you should stop. Think about it. I mean, obviously there's not, um, I got a really great question at an interview once, which is, where are containers a bad idea?

That's probably one of the best like recent interview questions I've ever gotten cause I was like, Oh yeah, I mean, like, you can't, it can't be perfect everywhere, right? Nothing's perfect everywhere. So it's like, where is it? Uh, and of course the answer was networking, right? (unintelligible) 

So if you need absolute performance, but like for just about everything else. Containers are kind of it at this point. Like, time has born it out, I think. So yeah, I always just like bias at taking containers at this point. So I'm probably more of a CapRover person than a Dokku person, even though I have not used, I don't use CapRover.

[00:03:09] **Jeremy:** Well, like something that I've heard with containers, and maybe it's changed recently, but, but something that was kind of holdout was when people would host a database sometimes they would oh we just don't wanna put this in a container and I wonder if like that matches with your thinking or if things have changed.

[00:03:27] **Victor:** I am not a database administrator right like I read postgres docs and I read the, uh, the Postgres documentation, and I think I know a bit about postgres but I don't commit right like so and I also haven't, like, oh, managed X terabytes on one server that you are making sure never goes down kind of deal.

But the stickiness for me, at least from when I've run, So I've done a lot of tests with like ZFS and Postgres and like, um, and also like just trying to figure out, and I run Postgres in Kubernetes of course, like on my cluster and a lot of the stuff I found around is, is like fiddly kernel things like sort of base kernel settings that you need to have set.

Like, you know, stuff like should you be using transparent huge pages, like stuff like that. But once you have that settled. Containers are just processes with name spacing and resource control, right? Like, that's it. there are some other ins and outs, but for the most part, if you're fine running a process, so people ran processes, right?

And they were just completely like unprotected. Then people made users for the processes and they limited the users and ran the processes, right? Then the next step is now you can run a process and then do the limiting the name spaces in cgroups dynamically. Like there, there's, there's sort of not a humongous difference, unless you're hitting something very specific.

Uh, but yeah, databases have been a point of contention, but I think, Kelsey Hightower had that tweet yeah. That was like, um, don't run databases in Kubernetes. And I think he called it back.

[00:04:56] **Victor:** I don't know, but I, I know that was uh, was one of those things that people were really unsure about at first, but then after people sort of like felt it out, they were like, Oh, it's actually fine. Yeah.

[00:05:06] **Jeremy:** Yeah I vaguely remember one of the concerns having to do with persistent storage. Like there were challenges with Kubernetes and needing to keep that storage around and I don't know if that's changed yeah or if that's still a concern.

[00:05:18] **Victor:** Uh, I'd say that definitely has changed. Uh, and it was, it was a concern, depending on where you were. Mostly people who are running AKS or EKS or you know, all those other managed Kubernetes, they're just using EBS or like whatever storage provider is like offering for storage.

Most of those people don't actually have that much of a problem with, storage in general. 

Now, high performance storage is obviously different, right? So like, so you'll, you're gonna have to start doing manual, like local volume management and stuff like that. it was a problem, because obviously CSI (Kubernetes Container Storage Interface) didn't exist for some period of time, and like there was, it was hard to know what to do for if you were just running a Kubernetes cluster. I think a lot of people were just using local, first of all, local didn't even exist for a bit.

Um, they were just using host path, right? And just like, Oh, it's on the disk somewhere. Where do we, we have to go get it right? Or we have to like, sort of manage that. So that was something most people weren't ready for, especially if you were just, if you weren't like sort of a, a, a traditional sysadmin and used to doing that stuff.

And then of course local volumes came out, but I think they still had to be, um, pre-provisioned. So that's sysadmin stuff that most people, you know, maybe aren't, aren't necessarily ready for. Uh, and then most of the general solutions were slow. So like, I used Longhorn (https://longhorn.io) for a long time and Longhorn, Longhorn's great. And super easy to set up, but it can be slower and you can have some, like, delays in mount time. it wasn't ideal for, for most people. 

So yeah, I, overall it's true. Databases, Databases in Kubernetes were kind of fraught with peril for a while, but it wasn't for the reason that, it wasn't for the fundamental reason that Kubernetes was just wrong or like, it wasn't the reason most people think of, which is just like, Oh, you're gonna break your database.

It's more like, running a database is hard and Kubernetes hasn't solved all the hard problems. Like, cuz that's what Kubernetes does. It basically solves a lot of problems in a very generic way. Right. So it just hadn't solved all those problems yet at this point. I think it's got decent answers on a lot of them.

So I, I mean, I don't know. I I do it. Don't, don't take what I'm saying to your, you know, PM meeting or your standup meeting, uh, anyone who's listening. But it's more like if you could solve the problems with databases in the sense before. You could probably solve 'em on Kubernetes now with a good understanding of Kubernetes.

Cause at the end of the day, it's all the same stuff. Just Kubernetes makes it a little easier to, uh, do it dynamically.

[00:07:50] **Jeremy:** It sounds like you could do it before, but some of the, I guess the tools or the ways of doing persistent storage were not quite there yet, or they were difficult to use. And so that was why people at the start were like, Okay, maybe it's not a good idea, but, now maybe there's some established practices for how you should run a database in Kubernetes.

And I, I suppose the other aspect too is that, like you were saying, Kubernetes is its own thing. You gotta learn Kubernetes and all its intricacies. And then running a database is also its own challenge. So if you stack the two of them together and, and the path was not really clear then maybe at the start it wasn't the best idea. Um, uh, if somebody was going to try it out now, was there like a specific resource you looked at or a specific path to where like okay this is is how I'm going to do it. 

[00:08:55] **Victor:** I'll just say what I normally recommend to everybody.

Cause it depends on which path you wanna go right? If you wanna go down like running a database path first and figure that out, fill out that skill tree. Like go read the Postgres docs. 

Well, first of all, use Postgres. That's the first tip there. But like, read those documents. And obviously you don't have to understand everything. You won't understand everything. But knowing the big pieces and sort of letting your brain see the mention of like a whole bunch of things, like what is toast?

Oh, you can do compression on columns. Like, you can do some, some things concurrently. Um, you know, what ALTER TABLE looks like. You get all that stuff kind of in your head. Um, and then I personally really believe in sort of learning by building and just like iterating. you won't get it right the first time. It's just like, it's not gonna happen. You're get, you can, you can get better the first time, right? By being really prepared and like, and leave yourself lots of outs, but you kind of have to like, get it out there. Do do your best to make sure that you can't fail, uh, catastrophically, right?

So this is like, goes back to that decision to like use ZFS as the bottom of this I'm just like, All right, well, I, I'm not a file systems expert, but if I. I could delegate some of that, you know, some of that, I can get some of that knowledge from someone else. Um, and I can make it easier for me to not fail catastrophically.

For the database side, actually read documentation on Postgres or the whatever database you're going to use, make sure you at least understand that. Then start running it like locally or whatever. Again, Docker use, use Docker locally.

It's, it's, it's fine. and then, you know, sort of graduate to running sort of more progressively, more complicated versions. what I would say for the Kubernetes side is actually similar. the Kubernetes docs are really good. they're very large. but they're good.

So you can actually go through and know all the, like, workload, workload resources, know, like what a config map is, what a secret is, right? Like what etcd is doing in this whole situation. you know, what a kublet is versus an API server, right? Like the, the general stuff, like if you go through all that, you should have like a whole bunch of ideas at least floating around in your head. And then once you try and start setting up a server, they will all start to pop up again, right? And they'll all start to like, you, like, Oh, okay, I need a CNI (Container Networking) plugin because something needs to make the services available, right? Or something needs to power the ingress, right? Like, if I wanna be able to get traffic, I need an ingress object.

But what listens, what does that, what makes that ingress object do anything? Oh, it's an ingress controller. nginx, you know, almost everyone's heard of nginx, so they're like, okay. Um, nginx, has an ingress control. Actually there's, there used to be two, I assume there's still two, but there's like one that's maintained by Kubernetes, one that's maintained by nginx, the company or whatever.

I use traefik, it's fantastic. but yeah, so I think those things kind of fall out and that is almost always my first way to explain it and to start building. And tinkering iteratively. So like, read the documentation, get a good first grasp of it, and then start building yourself because you'll, you'll get way more questions that way.

Like, you'll ask way more questions, you won't be able to make progress. Uh, and then of course you can, you know, hop into slacks or like start looking around and, and searching on the internet. oh, one of the things that really helped me out early learning Kubernetes was, Kelsey Hightower's, um, learn Kubernetes the hard way. I'm also a big believer in doing things the hard way, at least knowing what you're choosing to not know, right? distributing file system, Deltas, right? Or like changes to a file system over the network is not a new problem. Other people have solved it. There's a lot of complexity there. but if you at least know the sort of surface level of what the thing does and what it's supposed to do and how it's supposed to do it, you can make a decision on, Oh, how deep am I going to go?

Right? To prevent yourself from like, making a mistake or going too deep in the rabbit hole. If you have an idea of the sort of ecosystem and especially like, Oh, here, like the basics of how I can use this thing, that's generally very good. And doing things the hard way is a great way to get a, a feel for that, right?

Cause if you take some chunk and like, you know, the first level of doing things the hard way, uh, or, you know, Kelsey Hightower's guide is like, get a machine, right? Like, so, like, if you somehow were like, Oh, I wanna run a Kubernetes cluster. but, you know, I don't want use necessarily EKS and you wanna learn it the hard way.

You have to go get a machine, right? If you, if you're not familiar, if you run on Heroku the whole time, like you didn't manage your own machines, you gotta go like, figure out EC2, right? Or, I personally use, hetzner I love hetzner, so you have to go figure out hetzner, digital ocean, whatever.

Right. And then the next thing's like, you know, the guide's changed a lot, and I haven't, I haven't looked at it in like, in years, actually a while since I, since I've sort of been, I guess living it, but it's, it's like generate certificates, right? So if you've never dealt with SSL and like, sort of like, or I should say TLS uh, and generating certificates and how that whole dance works, right?

Which is fascinating because it's like, oh, right, nothing's secure on the internet, except that we distribute root certificates on computers that are deployed in every OS, right? Like, that's a sort of fundamental understanding you may not go deep enough to realize, but if you are fascinated by it, trying to do it manually would lead you down that path.

You'd be like, Oh, what, like what is this thing? What is a CSR? Like, why, who is signing my request? Right? And it's like, why do we trust those people? Right? And it's like, you know, that kind of thing comes out and I feel like you can only get there from trying to do it, you know, answering the questions you can.

Right. And again, it takes some judgment to know when you should not go down a rabbit hole. uh, and then iterating. of course there are people who are excellent at explaining. you can find some resources that are shortcuts. But, uh, I think particularly my bread and butter has been just to try and do it the hard way.

Avoid pitfalls or like rabbit holes when you can. But know that the rabbit hole is there, and then keep going. And sometimes if something's just too hard, you're not gonna get it the first time. Like maybe you'll have to wait like another three months, you'll try again and you'll know more sort of ambiently about everything else.

You get a little further that time. that's how I feel about that. Anyway.

[00:15:06] **Jeremy:** That makes sense to me. I think sometimes when people take on a project, they try to learn too many things at the same time. I, I think the example of Kubernetes and Postgres is pretty good example, where if you're not familiar with how do I install Postgres on bare metal or a vm, trying to make sense of that while you're trying to into is probably gonna be pretty difficult.

So, so splitting them up and learning them individually, that makes a lot of sense to me. And the whole deciding how deep you wanna go. That's interesting too, because I think that's very specific to the person right because sometimes you wanna go a little deeper because otherwise you don't understand how the two things connect together.

But other times it's just like with the example with certificates, some people they may go like, I just put in let's encrypt it gives me my cert I don't care right then, and then, and some people they wanna know like okay how does the whole certificate infrastructure work which I think is interesting, depending on who you are, maybe you go ahh maybe it doesn't really matter right.

[00:16:23] **Victor:** Yeah, and, you know, shout out to Let's Encrypt . It's, it's amazing, right? think Singlehandedly the most, most of the deployment of HTTPS that happens these days, right? so many so many of like internet providers and uh, sort of service providers will use it right?

Under the covers. Like, Hey, we've got you free SSL through Let's Encrypt, right? Like, kind of like under the, under the covers. which is awesome. And they, and they do it. So if you're listening to this, donate to them. I've done it. So now that, now the pressure is on whoever's listening, but yeah, and, and I, I wanna say I am that person as well, right?

Like, I use, Cert Manager on my cluster, right? So I'm just like, I don't wanna think about it, but I, you know, but I, I feel like I thought about it one time. I have a decent grasp. If something changes, then I guess I have to dive back in. I think it, you've heard the, um, innovation tokens idea, right?

I can't remember the site. It's like, um, do, like do boring tech or something.com (https://boringtechnology.club/) . Like it shows up on sort of hacker news from time to time, essentially. But it's like, you know, you have a certain amount of tokens and sort of, uh, we'll call them tokens, but tolerance for complexity or tolerance for new, new ideas or new ways of doing things, new processes.

Uh, and you spend those as you build any project, right? you can be devastatingly effective by just sticking to the stack, you know, and not introducing anything new, even if it's bad, right? and there's nothing wrong with LAMP stack, I don't wanna annoy anybody, but like if you, if you're running LAMP or if you run on a hostgator, right?

Like, if you run on so, you know, some, some service that's really old but really works for you isn't, you know, too terribly insecure or like, has the features you need, don't learn Kubernetes then, right? Especially if you wanna go fast. cuz you, you're spending tokens, right? You're spending, essentially brain power, right?

On learning whatever other thing. So, but yeah, like going back to that, databases versus databases on Kubernetes thing, you should probably know one of those before you, like, if you're gonna do that, do that thing. You either know Kubernetes and you like, at least feel comfortable, you know, knowing Kubernetes extremely difficult obviously, but you feel comfortable and you feel like you can debug.

Little bit of a tangent, but maybe that's even a better, sort of watermark if you know how to debug a thing. If, if it's gone wrong, maybe one or five or 10 or 20 times and you've gotten out. Not without documentation, of course, cuz well, if you did, you're superhuman.

But, um, but you've been able to sort of feel your way out, right? Like, Oh, this has gone wrong and you have enough of a model of the system in your head to be like, these are the three places that maybe have something wrong with them. Uh, and then like, oh, and then of course it's just like, you know, a mad dash to kind of like, find, find the thing that's wrong.

You should have confidence about probably one of those things before you try and do both when it's like, you know, complex things like databases and distributed systems management, uh, and orchestration.

[00:19:18] **Jeremy:** That's, that's so true in, in terms of you are comfortable enough being able to debug a problem because it's, I think when you are learning about something, a lot of times you start with some kind of guide or some kind of tutorial and you follow the steps. And if it all works, then great.

Right? But I think it's such a large leap from that to something went wrong and I have to figure it out. Right. Whether it's something's not right in my Dockerfile or my postgres instance uh, the queries are timing out. so many things that could go wrong, that is the moment where you're forced to figure out, okay, what do I really know about this not thing?

[00:20:10] **Victor:** Exactly. Yeah. Like the, the rubber's hitting the road it's uh you know the car's about to crash or has already crashed like if I open the bonnet, do I know what's happening right or am I just looking at (unintelligible).

And that's, it's, I feel sort a little sorry or sad for, for devs that start today because there's so much. Complexity that's been built up. And a lot of it has a point, but you need to kind of have seen the before to understand the point, right? So I like, I like to use front end as an example, right? Like the front end ecosystem is crazy, and it has been crazy for a very long time, but the steps are actually usually logical, right?

Like, so like you start with, you know, HTML, CSS and JavaScript, just plain, right? And like, and you can actually go in lots of directions. Like HTML has its own thing. CSS has its own sort of evolution sort of thing. But if we look at JavaScript, you're like, you're just writing JavaScript on every page, right?

And like, just like putting in script tags and putting in whatever, and it's, you get spaghetti, you get spaghetti, you start like writing, copying the same function on multiple pages, right? You just, it, it's not good. So then people, people make jquery, right? And now, now you've got like a, a bundled set of like good, good defaults that you can, you can go for, right?

And then like, you know, libraries like underscore come out for like, sort of like not dom related stuff that you do want, you do want everywhere. and then people go from there and they go to like backbone or whatever. it's because Jquery sort of also becomes spaghetti at some point and it becomes hard to manage and people are like, Okay, we need to sort of like encapsulate this stuff somehow, right?

And like the new tools or whatever is around at the same timeframe. And you, you, you like backbone views for example. and you have people who are kind of like, ah, but that's not really good. It's getting kind of slow.

Uh, and then you have, MVC stuff comes out, right? Like Angular comes out and it's like, okay, we're, we're gonna do this thing called dirty checking, and it's gonna be, it's gonna be faster and it's gonna be like, it's gonna be less sort of spaghetti and it's like a little bit more structured. And now you have sort of like the rails paradigm, but on the front end, and it takes people to get a while to get adjusted to that, but then that gets too heavy, right?

And then dirty checking is realized to be a mistake. And then, you get stuff like MVVM, right? So you get knockout, like knockout js and you got like Durandal, and like some, some other like sort of front end technologies that come up to address that problem. Uh, and then after that, like, you know, it just keeps going, right?

Like, and if you come in at the very end, you're just like, What is happening? Right? Like if it, if it, if someone doesn't sort of boil down the complexity and reduce it a little bit, you, you're just like, why, why do we do this like this? Right? and sometimes there's no good reason.

Sometimes the complexity is just like, is unnecessary, but having the steps helps you explain it, uh, or helps you understand how you got there. and, and so I feel like that is something younger people or, or newer devs don't necessarily get a chance to see. Cause it just, it would take, it would take very long right? And if you're like a new dev, let's say you jumped into like a coding bootcamp. I mean, I've got opinions on coding boot camps, but you know, it's just like, let's say you jumped into one and you, you came out, you, you made it. It's just, there's too much to know. sure, you could probably do like HTML in one month.

Well, okay, let's say like two weeks or whatever, right? If you were, if you're literally brand new, two weeks of like concerted effort almost, you know, class level, you know, work days right on, on html, you're probably decently comfortable with it. Very comfortable. CSS, a little harder because this is where things get hard.

Cause if you, if you give two weeks for, for HTML, CSS is harder than HTML kind of, right? Because the interactions are way more varied. Right? Like, and, and maybe it's one of those things where you just, like, you, you get somewhat comfortable and then just like know that in the future you're gonna see something you don't understand and have to figure it out. Uh, but then JavaScript, like, how many months do you give JavaScript? Because if you go through that first like, sort of progression that I, I I, I, I mentioned everyone would have a perfect sort of, not perfect but good understanding of the pieces, right? Like, why did we start transpiling at all? Right? Like, uh, or why did you know, why did we adopt libraries?

Like why did Bower exist? No one talks about Bower anymore, obviously, but like, Bower was like a way to distribute front end only packages, right? Um, what is it? Um, Uh, yes, there's grunt. There's like the whole build system thing, right? Once, once we decide we're gonna, we're gonna do stuff to files before we, before we push. So there's grunt, there's, uh, gulp, which is like grunt, but like, Oh, we're gonna do it all in memory. We're gonna pipe, we're gonna use this pipes thing to make sure everything goes fast. then there's like, of course that leads like the insanity that's webpack. And then there's like parcel, which did better.

There's vite there's like, there's all this, there's this progression, but how many months would it take to know that progression? It, it's too long. So they end up just like, Hey, you're gonna learn react. Which is the right thing because it's like, that's what people hire for, right? But then you're gonna be in react and be like, What's webpack, right?

And it's like, but you can't go down. You can't, you don't have the time. You, you can't sort of approach that problem from the other direction where you, which would give you better understanding cause you just don't have the time. I think it's hard for newer devs to overcome this.

Um, but I think there are some, there's some hope on the horizon cuz some things are simpler, right? Like some projects do reduce complexity, like, by watching another project sort of innovate so like react. Wasn't the first component, first framework, right? Like technically, I, I think, I think you, you might have to give that to like, to maybe backbone because like they had views and like marionette also went with that.

Like maybe, I don't know, someone, someone I'm sure will get in like, send me an angry email, uh, cuz I forgot you Moo tools or like, you know, Ember Ember. They've also, they've also been around, I used to be a huge Ember fan, still, still kind of am, but I don't use it. but if you have these, if you have these tools, right?

Like people aren't gonna know how to use them and Vue was able to realize that React had some inefficiencies, right? So React innovates the sort of component. So Reintroduces the component based model component first, uh, front end development model. Vue sees that and it's like, wait a second, if we just export this like data object, and of course that's not the only innovation of Vue, but if we just export this data object, you don't have to do this fine grained tracking yourself anymore, right?

You don't have to tell React or tell your the system which things change when other things change, right? Like you, you don't have to set up this watching and stuff, right? Um, and that's one of the reasons, like Vue is just, I, I, I remember picking up Vue and being like, Oh, I'm done. I'm done with React now.

Because it just doesn't make sense to use React because they Vue essentially either, you know, you could just say they learned from them or they, they realize a better way to do things that is simpler and it's much easier to write. Uh, and you know, functionally similar, right? Um, similar enough that it's just like, oh they boil down some of that complexity and we're a step forward and, you know, in other ways, I think.

Uh, so that's, that's awesome. Every once in a while you get like a compression in the complexity and then it starts to ramp up again and you get maybe another compression. So like joining the projects that do a compression. Or like starting to adopting those is really, can be really awesome. So there's, there's like, there's some hope, right?

Cause sometimes there is a compression in that complexity and you you might be lucky enough to, to use that instead of, the thing that's really complex after years of building on it.

[00:27:53] **Jeremy:** I think you're talking about newer developers having a tough time making sense of the current frameworks but the example you gave of somebody starting from HTML and JavaScript going to jquery backbone through the whole chain, that that's just by nature of you've put in a lot of time right you've done a lot of work working with each of these technologies you see the progression 

as if someone is starting new just by nature of you being new you won't have been able to spend that time

[00:28:28] **Victor:** Do you think it could work? again, the, the, the time aspect is like really hard to get like how can you just avoid spending time um to to learn things that's like a general problem I think that problem is called education in the general sense.

But like, does it make sense for a, let's say a bootcamp or, or any, you know, school right? To attempt to guide people through the previous solutions that didn't work, right? Like in math, you don't start with calculus, right? It just wouldn't, it doesn't make sense, right? But we try and start with calculus in software, right?

We're just like, okay, here's the complexity. You've got all of it. Don't worry. Just look at this little bit. If, you know, if the compiler ever spits out a weird error uh oh, like, you're, you're, you're in for trouble cuz you, you just didn't get the. get the basics. And I think that's maybe some of what is missing.

And the thing is, it is like the constraints are hard, right? No one has infinite time, right? Or like, you know, even like, just tons of time to devote to learning, learning just front end, right? That's not even all of computing, That's not even the algorithm stuff that some companies love to throw at you, right?

Uh, or the computer sciencey stuff. I wonder if it makes more sense to spend some time taking people through the progression, right? Because discovering that we should do things via components, let's say, or, or at least encapsulate our functionality to components and compose that way, is something we, we not everyone knew, right?

Or, you know, we didn't know wild widely. And so it feels like it might make sense to touch on that sort of realization and sort of guide the student through, you know, maybe it's like make five projects in a week and you just get progressively more complex. But then again, that's also hard cause effort, right?

It's just like, it's a hard problem. But, but I think right now, uh, people who come in at the end and sort of like see a bunch of complexity and just don't know why it's there, right? Like, if you've like, sort of like, this is, this applies also very, this applies to general, but it applies very well to the Kubernetes problem as well.

Like if you've never managed nginx on more than one machine, or if you've never tried to set up a, like a, to format your file system on the machine you just rented because it just, you know, comes with nothing, right? Or like, maybe, maybe some stuff was installed, but, you know, if you had to like install LVM (Logical Volume Manager) yourself, if you've never done any of that, Kubernetes would be harder to understand.

It's just like, it's gonna be hard to understand. overlay networks are hard for everyone to understand, uh, except for network people who like really know networking stuff. I think it would be better. But unfortunately, it takes a lot of time for people to take a sort of more iterative approach to, to learning.

I try and write blog posts in this way sometimes, but it's really hard. And so like, I'll often have like an idea, like, so I call these, or I think of these as like onion, onion style posts, right? Where you either build up an onion sort of from the inside and kind of like go out and like add more and more layers or whatever.

Or you can, you can go from the outside and sort of take off like layers. Like, oh, uh, Kubernetes has a scheduler. Why do they need a scheduler? Like, and like, you know, kind of like, go, go down. but I think that might be one of the best ways to learn, but it just takes time. Or geniuses and geniuses who are good at two things, right?

Good at the actual technology and good at teaching. Cuz teaching is a skill and it's very hard. and, you know, shout out to teachers cuz that's, it's, it's very difficult, extremely frustrating. it's hard to find determinism in, in like methods and solutions.

And there's research of course, but it's like, yeah, that's, that's a lot harder than the computer being like, Nope, that doesn't work. Right? Like, if you can't, if you can't, like if you, if the function call doesn't work, it doesn't work. Right. If the person learned suboptimally, you won't know Right. Until like 10 years down the road when, when they can't answer some question or like, you know, when they, they don't understand. It's a missing fundamental piece anyway. 

[00:32:24] **Jeremy:** I think with the example of front end, maybe you don't have time to walk through the whole history of every single library and framework that came but I think at the very least, if you show someone, or you teach someone how to work with css, and you have them, like you were talking about components before you have them build a site where there's a lot of stuff that gets reused, right? Maybe you have five pages and they all have the same nav bar.

[00:33:02] **Victor:** Yeah, you kind of like make them do it.

[00:33:04] **Jeremy:** Yeah. You make 'em do it and they make all the HTML files, they copy and paste it, and probably your students are thinking like, ah, this, this kind of sucks

[00:33:16] **Victor:** Yeah 

[00:33:18] **Jeremy:** And yeah, so then you, you come to that realization, and then after you've done that, then you can bring in, okay, this is why we have components.

And similarly you brought up, manual dom manipulation with jQuery and things like that. I, I'm sure you could come up with an example of you don't even necessarily need to use jQuery. I think people can probably skip that step and just use the the, the API that comes with the browser.

But you can have them go in like, Oh, you gotta find this element by the id and you gotta change this based on this, and let them experience the. I don't know if I would call it pain, but let them experience like how it was. Right. And, and give them a complex enough task where they feel like something is wrong right. Or, or like, there, should be something better. And then you can go to you could go straight to vue or react. I'm not sure if we need to go like, Here's backbone, here's knockout.

[00:34:22] **Victor:** Yeah. That's like historical. Interesting.

[00:34:27] **Jeremy:** I, I think that would be an interesting college course or something that.

Like, I remember when, I went through school, one of the classes was programming languages. So we would learn things like, Fortran and stuff like that. And I, I think for a more frontend centered or modern equivalent you could go through, Hey, here's the history of frontend development here's what we used to do and here's how we got to where we are today.

I think that could be actually a pretty interesting class yeah

[00:35:10] **Victor:** I'm a bit interested to know you learned fortran in your PL class.

I, think when I went, I was like, lisp and then some, some other, like, higher classes taught haskell but, um, but I wasn't ready for haskell, not many people but fortran is interesting, I kinda wanna hear about that.

[00:35:25] **Jeremy:** I think it was more in terms of just getting you exposed to historically this is how things were. Right. And it wasn't so much of like, You can take strategies you used in Fortran into programming as a whole. I think it was just more of like a, a survey of like, Hey, here's, you know, here's Fortran and like you were saying, here's Lisp and all, all these different languages nd like at least you, you get to see them and go like, yeah, this is kind of a pain. 

[00:35:54] **Victor:** Yeah 

[00:35:55] **Jeremy:** And like, I understand why people don't choose to use this anymore but I couldn't take away like a broad like, Oh, I, I really wish we had this feature from, I think we were, I think we were using Fortran 77 or something like that.

I think there's Fortran 77, a Fortran 90, and then there's, um, I think,

[00:36:16] **Victor:** Like old fortran, deprecated 

[00:36:18] **Jeremy:** Yeah, yeah, yeah. So, so I think, I think, uh, I actually don't know if they're, they're continuing to, um, you know, add new things or maintain it or it's just static. But, it's, it's more, uh, interesting in terms of, like we were talking front end where it's, as somebody who's learning frontend development who is new and you get to see how, backbone worked or how Knockout worked how grunt and gulp worked.

It, it's like the kind of thing where it's like, Oh, okay, like, this is interesting, but let us not use this again. Right?

[00:36:53] **Victor:** Yeah. Yeah. Right. But I also don't need this, and I will never again

[00:36:58] **Jeremy:** yeah, yeah. It's, um, but you do definitely see the, the parallels, right? Like you were saying where you had your, your Bower and now you have NPM and you had Grunt and Gulp and now you have many choices

[00:37:14] **Victor:** Yeah.

[00:37:15] **Jeremy:** yeah. I, I think having he history context, you know, it's interesting and it can be helpful, but if somebody was. Came to me and said hey I want to learn how to build websites. I get into front end development. I would not be like, Okay, first you gotta start moo tools or GWT.

I don't think I would do that but it I think at a academic level or just in terms of seeing how things became the way they are sure, for sure it's interesting.

[00:37:59] **Victor:** Yeah. And I, I, think another thing I don't remember who asked or why, why I had to think of this lately. um but it was, knowing the differentiators between other technologies is also extremely helpful right? So, What's the difference between ES build and SWC, right? Again, we're, we're, we're leaning heavy front end, but you know, just like these, uh, sorry for context, of course, it's not everyone a front end developer, but these are two different, uh, build tools, right?

For, for JavaScript, right? Essentially you can think of 'em as transpilers, but they, I think, you know, I think they also bundle like, uh, generally I'm not exactly sure if, if ESbuild will bundle as well. Um, but it's like one is written in go, the other one's written in Rust, right? And sort of there's, um, there's, in addition, there's vite which is like vite does bundle and vite does a lot of things.

Like, like there's a lot of innovation in vite that has to have to do with like, making local development as fast as possible and also getting like, you're sort of making sure as many things as possible are strippable, right? Or, or, or tree shakeable. Sorry, is is is the better, is the better term. Um, but yeah, knowing, knowing the, um, the differences between projects is often enough to sort of make it less confusing for me.

Um, as far as like, Oh, which one of these things should I use? You know, outside of just going with what people are recommending. Cause generally there is some people with wisdom sometimes lead the crowd sometimes, right? So, so sometimes it's okay to be, you know, a crowd member as long as you're listening to the, to, to someone worth listening to.

Um, and, and so yeah, I, I think that's another thing that is like the mark of a good project or, or it's not exclusive, right? It's not, the condition's not necessarily sufficient, but it's like a good projects have the why use this versus x right section in the Readme, right? They're like, Hey, we know you could use Y but here's why you should use us instead.

Or we know you could use X, but here's what we do better than X. That might, you might care about, right? That's, um, a, a really strong indicator of a project. That's good cuz that means the person who's writing the project is like, they've done this, the survey. And like, this is kind of like, um, how good research happens, right?

It's like most of research is reading what's happening, right? To knowing, knowing the boundary you're about to push, right? Or try and sort of like push one, make one step forward in, um, so that's something that I think the, the rigor isn't in necessarily software development everywhere, right?

Which is good and bad. but someone who's sort of done that sort of rigor or, and like, and, and has, and or I should say, has been rigorous about knowing the boundary, and then they can explain that to you. They can be like, Oh, here's where the boundary was. These people were doing this, these people were doing this, these people were doing this, but I wanna do this.

So you just learned now whether it's right for you and sort of the other points in the space, which is awesome. Yeah. Going to your point, I feel like that's, that's also important, it's probably not a good idea to try and get everyone to go through historical artifacts, but if just a, a quick explainer and sort of, uh, note on the differentiation, Could help for sure. Yeah. I feel like we've skewed too much frontend. No, no more frontend discussion this point.

[00:41:20] **Jeremy:** It's just like, I, I think there's so many more choices where the, the mental thought that has to go into, Okay, what do I use next I feel is bigger on frontend.

I guess it depends on the project you're working on but if you're going to work on anything front end if you haven't done it before or you don't have a lot of experience there's so many build tools so many frameworks, so many libraries that yeah, but we

[00:41:51] **Victor:** Iterate yeah, in every direction, like the, it's good and bad, but frontend just goes in every direction at the same time Like, there's so many people who are so enthusiastic and so committed and and it's so approachable that like everyone just goes in every direction at the same time and like a lot of people make progress and then unfortunately you have try and pick which, which branch makes sense.

[00:42:20] **Jeremy:** We've been kind of talking about, some of your experiences with a few things and I wonder if you could explain the the context you're thinking of in terms of the types of projects you typically work on like what are they what's the scale of them that sort of thing.

[00:42:32] **Victor:** So I guess I've, I've gone through a lot of phases, right? In sort of what I use in in my tooling and what I thought was cool. I wrote enterprise java like everybody else. Like, like it really doesn't talk about it, but like, it's like almost at some point it was like, you're either a rail shop or a Java shop, for so many people.

And I wrote enterprise Java for a, a long time, and I was lucky enough to have friends who were really into, other kinds of computing and other kinds of programming. a lot of my projects were wrapped around, were, were ideas that I was expressing via some new technology, let's say. Right?

So, I wrote a lot of haskell for, for, for a while, right? But what did I end up building with that was actually a job board that honestly didn't go very far because I was spending much more time sort of doing, haskell things, right? And so I learned a lot about sort of what I think is like the pinnacle of sort of like type development in, in the non-research world, right?

Like, like right on the edge of research and actual usability. But a lot of my ideas, sort of getting back to the, the ideas question are just things I want to build for myself. Um, or things I think could be commercially viable or like do, like, be, be well used, uh, and, and sort of, and profitable things, things that I think should be built.

Or like if, if I see some, some projects as like, Oh, I wish they were doing this in this way, Right? Like, I, I often consider like, Oh, I want, I think I could build something that would be separate and maybe do like, inspired from other projects, I should say, Right? Um, and sort of making me understand a sort of a different, a different ecosystem.

but a lot of times I have to say like, the stuff I build is mostly to scratch an itch I have. Um, and or something I think would be profitable or utilizing technology that I've seen that I don't think anyone's done in the same way. Right? So like learning Kubernetes for example, or like investing the time to learn Kubernetes opened up an entire world of sort of like infrastructure ideas, right?

Because like the leverage you get is so high, right? So you're just like, Oh, I could run an aws, right? Like now that I, now that I know this cuz it's like, it's actually not bad, it's kind of usable. Like, couldn't I do that? Right? That kind of thing. Right? Or um, I feel like a lot of the times I'll learn a technology and it'll, it'll make me feel like certain things are possible that they, that weren't before.

Uh, like Rust is another one of those, right? Like, cuz like Rust will go from like embedded all the way to WASM, which is like a crazy vertical stack. Right? It's, that's a lot, That's a wide range of computing that you can, you can touch, right? And, and there's, it's, it's hard to learn, right? The, the, the, the, uh, the, the ramp to learning it is quite steep, but, it opens up a lot of things you can write, right?

It, it opens up a lot of areas you can go into, right? Like, if you ever had an idea for like a desktop app, right? You could actually write it in Rust. There's like, there's, there's ways, there's like is and there's like, um, Tauri is one of my personal favorites, which uses web technology, but it's either I'm inspired by some technology and I'm just like, Oh, what can I use this on?

And like, what would this really be good at doing? or it's, you know, it's one of those other things, like either I think it's gonna be, Oh, this would be cool to build and it would be profitable. Uh, or like, I'm scratching my own itch. Yeah. I think, I think those are basically the three sources.

[00:46:10] **Jeremy:** It's, it's interesting about Rust where it seems so trendy, I guess, in lots of people wanna do something with rust, but then in a lot of they also are not sure does it make sense to write in rust? Um, I, I think the, the embedded stuff, of course, that makes a lot of sense.

And, uh, you, you've seen a sort of surge in command line apps, stuff ripgrep and ag, stuff like that, and places like that. It's, I think the benefits are pretty clear in terms of you've got the performance and you have the strong typing and whatnot and I think where there's sort of the inbetween section that's kind of unclear to me at least would I build a web application in rust I'm not sure that sort of thing

[00:47:12] **Victor:** Yeah. I would, I characterize it as kind of like, it's a tool toolkit, so it really depends on the problem. And think we have many tools that there's no, almost never a real reason to pick one in particular right? 

Like there's, Cause it seems like just most of, a lot of the work, like, unless you're, you're really doing something interesting, right?

Like, uh, something that like, oh, I need to, I need to, like, I'm gonna run, you know, billions and billions of processes. Like, yeah, maybe you want erlang at that point, right? Like, maybe, maybe you should, that should be, you know, your, your thing. Um, but computers are so fast these days, and most languages have, have sort of borrowed, not borrowed, but like adopted features from others that there's, it's really hard to find a, a specific use case, for one particular tool.

Uh, so I often just categorize it by what I want out of the project, right? Or like, either my goals or project goals, right? Depending on, and, or like business goals, if you're, you know, doing this for a business, right? Um, so like, uh, I, I basically, if I want to go fast and I want to like, you know, reduce time to market, I use type script, right?

Oh, and also I'm a, I'm a, like a type zealot. I, I'd say so. Like, I don't believe in not having types, right? Like, it's just like there's, I think it's crazy that you would like have a function but not know what the inputs could be. And they could actually be anything, right? , you're just like, and then you have to kind of just keep that in your head.

I think that's silly. Now that we have good, we, we have, uh, ways to avoid the, uh, ceremony, right? You've got like hindley Milner type systems, like you have a way to avoid the, you can, you know, predict what types of things will be, and you can, you don't have to write everything everywhere. So like, it's not that.

But anyway, so if I wanna go fast, the, the point is that going back to that early, like the JS ecosystem goes everywhere at the same time. Typescript is excellent because the ecosystem goes everywhere at the same time. And so you've got really good ecosystem support for just about everything you could do.

Um, uh, you could write TypeScript that's very loose on the types and go even faster, but in general it's not very hard. There's not too much ceremony and just like, you know, putting some stuff that shows you what you're using and like, you know, the objects you're working with. and then generally if I wanna like, get it really right, I I'll like reach for haskell, right?

Cause it's just like the sort of contortions, and again, this takes time, this not fast, but, right. the contortions you can do in the type system will make it really hard to write incorrect code or code that doesn't, that isn't logical with itself. Of course interfacing with the outside world. Like if you do a web request, it's gonna fail sometimes, right?

Like the network might be down, right? So you have to, you basically pull that, you sort of wrap that uncertainty in your system to whatever degree you're okay with. And then, but I know it'll be correct, right? But and correctness is just not important. Most of like, Oh, I should , that's a bad quote. Uh, it's not that correct is not important.

It's like if you need to get to market, you do not necessarily need every single piece of your code to be correct, Right? If someone calls some, some function with like, negative one and it's not an important, it's not tied to money or it's like, you know, whatever, then maybe it's fine. They just see an error and then like you get an error in your back and you're like, Oh, I better fix that.

Right? Um, and then generally if I want to be correct and fast, I choose rust these days. Right? Um, these days. and going back to your point, a lot of times that means that I'm going to write in Typescript for a lot of projects. So that's what I'll do for a lot of projects is cuz I'll just be like, ah, do I need like absolute correctness or like some really, you know, fancy sort of type stuff.

No. So I don't pick haskell. Right. And it's like, do I need to be like mega fast? No, probably not. Cuz like, cuz so I don't necessarily don't necessarily need rust. Um, maybe it's interesting to me in terms of like a long, long term thing, right? Like if I, if I'm think, oh, but I want x like for example, tight, tight, uh, integration with WASM, for example, if I'm just like, oh, I could see myself like, but that's more of like, you know, for a fun thing that I'm doing, right?

Like, it's just like, it's, it's, you don't need it. You don't, that's premature, like, you know, that's a premature optimization thing. But if I'm just like, ah, I really want the ability to like maybe consider refactoring some of this out into like a WebAssembly thing later, then I'm like, Okay, maybe, maybe I'll, I'll pick Rust.

Or like, if I, if I like, I do want, you know, really, really fast, then I'll like, then I'll go Rust. But most of the time it's just like, I want a good ecosystem so I don't have to build stuff myself most of the time. Uh, and you know, type script is good enough. So my stack ends up being a lot of the time just in type script, right? Yeah.

[00:52:05] **Jeremy:** Yeah, I think you've encapsulated the reason why there's so many packages on NPM and why there's so much usage of JavaScript and TypeScript in general is that it, it, it fits the, it's good enough. Right? And in terms of, in terms of speed, like you said, most of the time you don't need of rust.

Um, and so typescript I think is a lot more approachable a lot of people have to use it because they do front end work anyways. And so that kinda just becomes the I don't know if I should say the default but I would say it's probably the most common in terms of when somebody's building a backend today certainly there's other languages but JavaScript and TypeScript is everywhere.

[00:52:57] **Victor:** Yeah. Uh, I, I, I, another thing is like, I mean, I'm, of ignored the, like, unreasonable effectiveness of like rails Cause there's just a, there's tons of just like rails warriors out there, and that's great. They're they're fantastic. I'm not a, I'm not personally a huge fan of rails but that's, uh, that's to my own detriment, right?

In, in some, in some ways. But like, Rails and Django sort of just like, people who, like, I'm gonna learn this framework it's gonna be excellent. It most, they have a, they have carved out a great ecosystem for themselves. Um, or like, you know, even php right? PHP and like Laravel, or whatever. Uh, and so I'm ignoring those, like, those pockets of productivity, right?

Those pockets of like intense productivity that people like, have all their needs met in that same way. Um, but as far as like general, general sort of ecosystem size and speed for me, um, like what you said, like applies to me. Like if I, if I'm just like, especially if I'm just like, Oh, I just wanna build a backend, Like, I wanna build something that's like super small and just does like, you know, maybe a few, a couple, you know, endpoints or whatever and just, I just wanna throw it out there.

Right? Uh, I, I will pick, yeah. Typescript. It just like, it makes sense to me. I also think note is a better. VM or platform to build on than any of the others as well. So like, like I, by any of the others, I mean, Python, Perl, Ruby, right? Like sort of in the same class of, of tool.

So I I am kind of convinced that, um, Node is better, than those as far as core abilities, right? Like threading Right. Versus the just multi-processing and like, you know, other, other, other solutions and like, stuff like that. So, if you want a boring stack, if I don't wanna use any tokens, right?

Any innovation tokens I reach for TypeScript.

[00:54:46] **Jeremy:** I think it's good that you brought up. Rails and, and Django because, uh, personally I've done, I've done work with Rails, and you're right in that Rails has so many built in, and the ways to do them are so well established that your ability to be productive and build something really fast hard to compete with, at least in my experience with available in the Node ecosystem.

Um, on the other hand, like I, I also see what you mean by the runtimes. Like with Node, you're, you're built on top of V8 and there's so many resources being poured into it to making it fast and making it run pretty much everywhere. I think you probably don't do too much work with managed services, but if you go to a managed service to run your code, like a platform as a service, they're gonna support Node.

Will they support your other preferred language? Maybe, maybe not,

You know that they will, they'll be able to run node apps so but yeah I don't know if it will ever happen or maybe I'm just not familiar with it, but feel like there isn't a real rails of javascript.

[00:56:14] **Victor:** Yeah, you're, totally right.

There are, there are. It's, it's weird. It's actually weird that there, like Uh, but, but, I kind of agree with you. There's projects that are trying it recently. There's like Adonis, um, there is, there are backends that also do, like, will do basic templating, like Nest, NestJS is like really excellent.

It's like one of the best sort of backend, projects out there. I I, I but like back in the day, there were projects like Sails, which was like very much trying to do exactly what Rails did, but it just didn't seem to take off and reach that critical mass possibly because of the size of the ecosystem, right?

Like, how many alternatives to Rails are there? Not many, right? And, and now, anyway, maybe let's say the rest of 'em sort of like died out over the years, but there's also like, um, hapi HAPI, uh, which is like also, you know, similarly, it was like angling themselves to be that, but they just never, they never found the traction they needed.

I think, um, or at least to be as wide, widely known as Rails is for, for, for the, for the Ruby ecosystem, um, but also for people to kind of know the magic, cause. Like I feel like you're productive in Rails only when you imbibe the magic, right? You, you, know all the magic context and you know the incantations and they're comforting to you, right?

Like you've, you've, you have the, you have the sort of like, uh, convention. You're like, if you're living and breathing the convention, everything's amazing, right? Like, like you can't beat that. You're just like, you're in the zone but you need people to get in that zone. And I don't think node has, people are just too, they're too frazzled.

They're going like, there's too much options. They can't, it's hard to commit, right? Like, imagine if you'd committed to backbone. Like you got, you can't, It's, it's over. Oh, it's not over. I mean, I don't, no, I don't wanna, you know, disparage the backbone project. I don't use it, but, you know, maybe they're still doing stuff and you know, I'm sure people are still working on it, but you can't, you, it's hard to commit and sort of really imbibe that sort of convention or, or, or sort of like, make yourself sort of breathe that product when there's like 10 products that are kind of similar and could be useful as well.

Yeah, I think that's, that's that's kind of big. It's weird that there isn't a rails, for NodeJS, but, but people are working on it obviously. Like I mentioned Adonis, there's, there's more. I'm leaving a bunch of them out, but that's part of the problem. 

[00:58:52] **Jeremy:** On, on one hand, it's really cool that people are trying so many different things because hopefully maybe they can find something that like other people wouldn't have thought of if they all stick same framework. but on the other hand, it's ... how much time have we spent jumping between all these different frameworks when what we could have if we had a rails.

[00:59:23] **Victor:** Yeah the, the sort of wasted time is, is crazy to think about it uh, I do think about that from time to time. And you know, and personally I waste a lot of my own time. Like, just, just recently, uh, something I've working on, for a long time. I came back to it after just sort of leaving it on the shelf for a while and I was like, You know what?

I should rewrite this in rust. I, I really should. and so I talked myself into it, and I'm like, You know what? It's gonna be so much easier to deploy. I'm just gonna have one binary. I'm not gonna have to deal with anything else. I'm just like, it'll be, it'll be so much better. I'll, I'll be a lot more confident in the code I write.

And then sort of going through it and like finishing this a, a chunk of it and the kind of project it is, is like I'll have a lot of sort of, different services, right? That, that, that sort of do a similar thing, but a sort of different flavor of a, of a thing, if that makes sense. And I know that I can just go back to typescript on the second one, right?

Like, I'm, I'm doing one and I'm just like, and that's what I've decided to do. Cause I'm just like, Yeah, no, this doesn't make any sense. like, I'm spending way too much time, um, when the other thing is like, is good enough. and like, I think maybe just if you feel that, if you can, like, don't know if you stay, stay aware of just like, Oh, how much friction am I encountering and maybe I should switch. Like if you know rails and you know, typescript, you should probably use Rails, if you're bought into the magic of Rails, right? And, and of course Rails is also another thing that has always has great support from, Platforms as service companies. Rails is always gonna be, you know, have great support right, Because it's just one of those places where it's so nice and cozy that, you know, people who use it are just like, the people who don't want to think about the server underneath.

[01:01:03] **Jeremy:** I think that combination is really powerful. Like you were talking earlier about working with Kubernetes and learning how all that works and how to run a database and all that. And if you think about the Heroku experience, right? You create your, your Rails app. You tell Heroku I want a database and then you push it. you don't have to worry about pods or Docker or any of that. They take care of all of it for you so I think that certainly there's a value to going deeper and, and learning about how to host things yourself and things like that but I can totally understand if you have the money, uh, especially if for a business would say I don't wanna do this type of ops work I don't want to learn how to set up a cluster just want to push it to a heroku and be done with it. 

[01:02:00] **Victor:** Yeah, You don't, no one gives you an award for learning how to, like wrangle LVM right? No no gives you that. They just like, you know you either make it to market or you don't. Uh, and it's like, uh, like I, mean, I'd love to hear about what you sort optimize but I feel like all, it's all about what you want to optimize for.

Like, are you optimizing for time to market? Are you optimizing for, a code base that people won't be able to mess up later? Right? Like a lot of just, you know, seed stage startups or like just early startups or big companies, like, it doesn't matter. We'll rewrite anyway. Right? That like the eBay example was a great, was a great sort of indication of that like it will get rewritten. So maybe it doesn't make sense. Maybe it's silly to, to optimize for strong code base the beginning. Um, 

[01:02:45] **Jeremy:** I think it, uh, at the beginning, especially if you don't have an established audience, like you're not getting any money, then pick something that the team knows and that, you know, um, or at least the majority does, because that, I think, makes the biggest difference in speed. Speed. Because let's, let's say you, you were giving an example of I would use haskell if I need to be correct, and I would use rust if I need to be fast. but if you are picking something everybody knows and you don't have some very specific requirement, for the most part, if you're using something you already know, it's going to be built faster, it's going to be easier to read and maintain and it'll probably be more correct just because you're more familiar with that whole... 

[01:03:50] **Victor:** So I, I agreed right up until the last point I feel like correctness is one of those, if you use a tool that lets you be too sloppy you can't stop people from being sloppy Right? Uh, like I think, and this is actually something I was thinking of earlier today, is like, I think writing good code is either people being disciplined or better systems, and of course it doesn't matter in every case, Right. and so like, so in cases where like, it, it's just not that important and, and it's better to just let it error and then someone just goes and like, fixes it, right? But if you do that too long, you get you can get spaghetti, right? You can get either spaghetti or you can get a code base that's suffering from a lot of technical debt. Uh, and it, it won't be a problem early on, but when it is, it's a big problem, right? and can drain a lot of, a lot of time. but 99% of the time, I agree.

You don't need anything other than like TypeScript or Rails or like Django, or you could, you could use perl if you want php obviously, like, you know, Right? Like, you, you could get very far, very fast with those. And often it's like, not even necessary to go anywhere else. But the only little thing I'd say is just like, I find that it's, It's so hard to be correct if you're not getting any help from your compiler, right?

Like, for me, at the very least, right? Like, if you're not getting any help from the language, it's so hard to like, write stuff. That's correct. That doesn't ship with bugs in it. Right? There was, um, there's a whole period of time where everyone was getting really excited about writing tests that were like, Oh, make sure to like, write a test with negative one.

Right? Like, just like, you know, like the next level test stuff was just like, Oh, but what if you like, you know, you gotta, I mean, and this is true, right? You have to think like, how could your system possibly be broken, right? Like, like thinking of how to break a system is hard. It's different from thinking of how to build a system, right?

It's a different skill set. But like some of those things you should really just be protected from, I think a big, uh, moment in my career was like seeing option I, I'd been lucky enough to have friends that were like exploring with stuff like, um, like haskell, super early on and like common lisp and sort of like, and reading Hacker News, shout out to AJ cuz like, that's his name.

But like, there's a, there's a person that was like, just kind of like, sort of like exploring the frontier. And then I would like hear a little bit and be like, Ooh, that's interesting. And like, kind of like, take a look, but option coming in. Like, I think Java 8 was like, wait a second option should be everywhere, right?

Because it's like NPEs Null Pointer Exceptions should almost, like, they shouldn't really be a thing, right? Like, and then you are like, Oh, wait, option should be here, but that means it has to be there and it kind of like, it just infects everything. And normally stuff that infects everything is bad, right?

You're just like, Oh no, this is bad. I better take it out. But then you're like, Wait a second. But option is right because I don't know if that thing is not a null actually right. Like the language doesn't give me that. So then, you know, you kind of stumble upon non nullable types, right? As a language feature.

And so it's, it's really hard to quantify, but I think things like that can make a, a, a, a worthwhile difference in, base choice of language as far as correctness goes and in preventing. But I also know that like, people are just blazing by in rails like, just like absolutely without the care in the world, and they're doing great and they, like, they have the, all the integrations and it's all, it's working out great for them.

But I personally just like, I'm just like, I have to, I feel the compulsion. I'm just like, I feel the compulsion and I'm just like, I need to at least do typescript and then I have a little bit more protection from myself. Uh, and then I can, and then I can go on. And it's also, it's like, it's also an excuse for me to like, write less tests as well.

Like a little bit like, you know, I'm just like, you know, I, I, I, there's, there's some, there's some, Assurance that I don't have to like go back and actually write that negative one test like the first time, Right. It in practice, like technically you, you, you should, cuz like, you know, at run time it's, it is a completely different world, right?

Like typescript is like a compile time thing thing. But if you, if you write your types well enough, you, you, you're, you're protected from some amount of that. And I find that that helps me. Personally. So, so that's the, that's the one place I'm just like, ah, I do like that correctness stuff,

[01:08:13] **Jeremy:** Yeah. Yeah. I, I think like, I, I do agree in a general sense with languages that have static type checking where, you know, at compile time whether something can even run, that can make a big difference. Maybe correctness wasn't the right word, but I you work in an ecosystem, whether Rails or Django or something else, you kind of know all of the, the gotchas, I guess? if you're, if you're, let's say you're building a product with Haskell and you've never Haskell before, I feel like yes, you have a lot of strong guarantees from the type system, but there are going to be things about the language or the ecosystem that you, you'll just miss just because you haven't been in it.

And I think that's what I meant by correctness in that you're going to make mistakes, either logical mistakes or mistakes in structure, right? Because if you, if you think about a Rails app, one of the things that I think is really powerful is that you can go to a company day one that uses rails and if they haven't done anything too crazy, you have a general sense of where things are some extent.

And when you're building something from scratch in a language and ecosystem you don't understand, um there's just so many scrapes and cuts you have to get before you're proficient right Um, so I, so I think that is more what I was thinking of yeah.

[01:10:01] **Victor:** Oh yeah. I, I'd fully agree with that yeah I fully agree with that. you don't know what you, what you don't know right. When you, uh, when you start, um especially with a new ecosystem, right because you just, everything's hard. You have to go figure out everything you have to go try and decide between two libraries that do similar things despite, you know, like knowing how it's done in another language.

But you gotta like figure out how it's done in this language, et cetera. But it's like, well, you know, at least decisions are easier elsewhere sometimes, right? Like, like in the database level or like, maybe the infrastructure level or, but yeah, I, I totally get that. It's just, most of the time you just want to go with that, uh, that faster, that faster thing, you know, Feels funny to say of course.

Cuz I never do this (laughs) . for I never, like all my, all my projects on, on essentially crazy stacks. But, but I, I try and I try and be mindful about is how much of my toil right now is even a good idea, right? Like, depending on my goals. Again, like going back to like that, it depends on what you're optimizing for right if you're optimizing for learning or like getting a really good fundamental understanding of something, then yeah, sure. If you're optimizing for like getting to market? Sure. that's a different answer. If you're, if you are optimizing for, like, being able to hire developers to work alongside you, right?

Like making it easy to hire teammates in the future, that's a different set of languages maybe. so yeah, I don't know. I kind of give the, the weasel answer, which is, you know, it depends , hmm right? But, um, yeah.

[01:11:32] **Jeremy:** Especially if you're, you're learning or you're doing personal projects for yourself, then yeah, if you, if you want to know how to use haskell better, then yeah, go for it. Use, use haskell, um, uh, or use rust and so on. I think another thing I think about is the deployment so if personal you are running a SaaS or you're running something that you deploy internally, then I think something like Rails, Django is totally fine especially if you use a platform as a service, then there's so many resources for you. But if your goal is to give you an example, like Mastodon, right? So we have the whole,twitter substitute thing.

Mastodon is written in Rails and it has a number of dependencies, right? you have to have Sidekiq, which runs the Workers, Elastisearch for search, um, Postgres for the database and Nginx and so on. And for somebody who's running an instance for a bunch of people, totally makes sense, right?

No big deal. where I think it's maybe a little trickier is, and I don't know if this is the intent of, Mastodon or ActivityPub in but some people, they wanna host their own instance, right? Um, rather than signing up for mastodon.social and having a whole bunch of people in one instance, they wanna able to control their instance.

They wanna host it themselves. And I think for that Rails the, the resources that it requires are a little high for that kind of small usage. So, in an example like that, if I wanted something that I wanted to be able to easily give to you and you could host it, then something like a Go or a Rust I think would make a lot of sense you can run the binary, right? And, you don't have to worry about all the things that go around running a Ruby application. 

So I think that's something to think about as well. And, and we talked about command line apps as well, right? If you're gonna build a command line app and you want it to run on Windows, well the person on Windows is not gonna have python or ruby so again having it in Go or in Rust makes a lot of sense there so that's another think I would think about who is it going to be given to and who is going to deploy it as well.

[01:14:25] **Victor:** Yeah. That's um, that's a great point, uh, because it makes me think of sort of explosion of sysadmins writing go when it first came out I, don't know if I imagined this or I think it was real, but like there were just so, uh, up until then, like most sysadmins would be they'd like obviously like get to know their routers or their, you know, their switches and their, you know, their servers and like racking, stacking doing all that stuff.

Languages and like frameworks can unlock a certain group of people or like unblock a certain group of people and like unlock their sort of productivity. So like Ansible was one of those first things that was like really sort of easy to understand and like, Oh, you can imperatively set this machine up.

But a side effect is you get a lot of sysadmins that know Python, right? So like, now a lot of like the sort of black art stuff is accessible to you. Like, or, sorry, I say accessible to you as in accessible to me as the non sysadmin, right? Cause I'm just like, Oh, I can run this like little script this person wrote, uh, in Python and it like, will do all this stuff, right?

That I, I would've never been able to do before. And maybe I learned a little bit more about that, about that system, right? And so I, I, I saw something similar and go where people were writing a bunch of tools that were just really easy to run, right? Really, really easy to run everywhere. Um, and that means easy to download, easy to like, you know, everything's easier and, A lot of hard things got a lot easier, right? Uh, and this is same with Rust. Like, I, I believe that library that most people use is like clap, I've built a few things with Clap and it's like, it gives you excellent, uh, I guess you'd call them affordances or like ability to make a high quality CLI program with very little effort, right?

Uh, and so that means you end up writing really decent binaries, right? With like, good help texts and like reasonable like, you know, options and stuff like that. and then it's really easy to deploy to Windows, right? And like other, other platforms, uh, like you said, you don't have to try and bundle Python or, or whatever else the sort of interpreter class of languages. So yeah, I think that I'd agree that like just languages and, and, and sort of frameworks can, can unlock, easier creation of certain kinds of apps and certain sort of groups of people to share their knowledge or like to, to, to make a, a tool that's more usable by everyone else.

It could be like, kind of like a, multiplicative factor right. Just like, I made this really, really intense Python script, but like now, but to use it, you'd have to like install Python on Windows, like manage your environments, whatever. Like, I don't know if you're using pyenv, maybe you are, maybe you aren't.

Do you get the wheel? Like what, what do you do with that? no, I'll just give you a, executable and you have an executable and then now you can use all the tools that like normally work with an executable or with something that like produces output and it's just faster for everybody and everybody like just, you know, gets more value

[01:17:17] **Jeremy:** Cool. Well, is there anything else you wanted to, to mention or, or talk about?

[01:17:26] **Victor:** I don't know. oh yeah, I guess, I guess I could just like say my stack, right? Um, Oh, I, I really love Sveltekit. I've been kind of all in on Sveltekit for the front end for a while now. it feels like I've used, um, I've used nuxt I've used, like, I've used a lot of frameworks, but I'm trying to think of, of frameworks that like, do the, um, like I think, I think a local, if not global maximum for front end development is power of the front end component driven sort of paradigm and server side rendering, right?

Because there's like, what are the big advantages of using something like Rails or like whatever else that, that just, just, that's completely server side is that the pages are fast, the pages are always fast. It's there, but they don't have interactivity. Right. we've taken a weird path to get here and it looks really wasteful and maybe it is really wasteful, but at this point we now have kind of both kind of like glued and like hacked into one thing.

And I think that class of tools is like, is, is is a local maximum, if not, if not global. so, so yeah. So like, there's like next, nuxt, sveltekit. There's, there's other solutions. There's Astro like there's, there's, which is Astro's really recent.

Um, there's Ember, right? Shout out to Ember right. People, people still pushing that forward as well, which is great. but yeah, so I, I've SvelteKit also, and this is again in like direct conflict to what we've talked about this entire time, which is like, use established things that get you there fast. but like SvelteKit isn't at 1.0 yet, but it is excellent.

Like, I, I am more productive in it than I ever was with Nuxt. Um, and again, Nuxt has changed a lot since I've, you know, sort of made the switch and like, you know, maybe I, maybe it deserves a rethink and like re revisiting it, but I'm so productive with SvelteKit. I just, like, I don't mind. And like half the time I'll just, I'll just use SvelteKit, uh, and my database and then be done like no middle layer.

So like no API layer. I just like stuff it into the SvelteKit app, and then use, postgres on the backend and then I'm done and, and I feel like that's been really productive, you know, again, this is outside of the, the world where you use a rails or whatever.

Um, so yeah. So that's, that's been my stack for a lot of the products I've done recently. so yeah, if I, if I had to, I guess say something about like front end, like give SvelteKit a try. It's pretty good. Uh, and obviously like databases, just use Postgres. Stop using other things. don't, don't do that.

And like infrastructure stuff, I think Kubernetes is cool, but you probably don't need it.

Uh, I like Pulumi. I feel like no one, like I've been recommending Pulumi for a long time over Terraform. So it's just like DSLs have limits and those limits are a bad idea to have when you, like, the rest of your time is spent with no limits, right.

With like just general computing. Right. So, and Pulumi is just like, you can do your general computing and infrastructure stuff too, and it's, I feel like it's, it's always, you know, been better, but, but anyway, yeah. That's like, that's kind of my stack 

[01:20:26] **Jeremy:** So pulumi is um, it's a way to provision infrastructure, but is there a language for it?

[01:20:35] **Victor:** It integrates with the language you use. And  Terraform has caught up in that respect, right? Cause you have that now. but how it works is still slightly different right because if I remember correctly they still generate a Terraform file and execute that file it's, still a little bit different, which is like, it's, and it's AWS' CDK as well, right? So, so the world that's sort of caught up to where, what Pulumi is doing. But you know, I, I think it was like, I don't know, terraform 12 or something like that where it was just like, we've added better for loops.

I'm like, okay, at this point, like this is, that's the indication of like, you now need general, like you, you, you're now the dsl, like DSLs can have for loops, but it's like if you're starting to like pluck, you know, general computing languages, we have really good general computing languages right there.

You know, that was kind of my, indication to be like, okay, I Pulumi is the way, uh, for me, um again, This doesn't matter cuz like at work you're gonna, you're probably using Terraform, like, you know, just every, just like, there's, you know, everyone's using certain tools and you don't have a choice. Sometimes you have to use certain tools, but I personally have my, uh, have my pet pet likes and stuff.

[01:21:49] **Jeremy:** How about for caching?

[01:21:53] **Victor:** Uh, KeyDB. I go into rabbit holes a lot. I call myself a yak shaver cause I shave a lot of yaks and it doesn't benefit anyone really except for me most of the time. But there are lots of redis alikes out there. And the best feature set is right now KeyDB.

There's like, there's, there's one called Tendis there's, um, which is like, um, a little bit like more distributed. There's like SSdb, which will do it off disk, which is, I think because we have such fast disks now, it's good enough for a bunch of applications. Right. Especially if, like, if your alternative was like, you know, a much farther away sort of, you know, calls the farther away service.

There's Pelican out of Twitter, so they have a whole, they've got like a caching, it's like a framework kind of, right? Like they, they, they've sort of built a kernel of like really interesting caching, um, originally like sort of to serve their memcache workloads and stuff. But it's kind of grown in like, in lots of directions as well.

KeyDB is, was the most compelling and still is to, to me for, from a resource usage. Multi threading, obviously, like it is multi threaded, so it is now, it's it's way faster. Right. Um, and also like it offers flash storage, using the SSD when you can. And, and that's, Those are game changers. Right. And, and of course all the, you know, usual and clusters, right? It clusters without you, you know, paying Redis Labs any money or whatever. Um, which is, which is fine. You know, people opensource projects and, and businesses have to, you know, make money. That is a thing. But yeah, KeyDB is, is my, uh, I, whenever I'm about to spin up redis, I don't, and I spin up uh, also they were bought by Snap or bought hell of an aquihire.

I think if, if you, cuz I think sometimes that has like a negative pejorative context to it. Like you didn't, like, oh, you didn't make a billion dollars, you just got aquihired or whatever. But hell of an aquihire. Um, and, and so all of it's like free now, like all of the, like all the, the premium features are becoming free.

And I'm like, this is, this is like, I won the lottery, right? Cause um, you know, you get all the, the, the awesome stuff outta KeyDB for, for free. Um, so yeah, Caching KeyDB. I do KeyDB.

[01:24:11] **Jeremy:** KeyDB. I haven't heard of that one.

[01:24:14] **Victor:** Oh yeah, it's, um, yeah it's like keydb.dev.

[01:24:17] **Jeremy:** Oh KeyDB.

[01:24:18] **Victor:** It's awesome. They did YC.

[01:24:23] **Jeremy:** Oh, it uses the Redis wire protocol 

[01:24:28] **Victor:** Like Redis is like, is the leader, unless you're using memcached for some other reason and then like obvious like have to use memcached, whatever. But, um, but yeah, Redis is like the sort of app external cache dujour for basically everywhere and when I wanna run Redis, I run KeyDB.

[01:24:51] **Jeremy:** And for search, do you just in search in postgres or turn to something else? 

[01:24:59] **Victor:** Oh, you've asked a dangerous question. So I recently did some, uh, some writing. So I, I, I, so recently, um, like this year, I've branched out and done a little bit more experiments in writing for companies that have an interesting you know developer product or sometimes where like, you know, my sort of like interest and stuff just aligned, right?

So like, uh, I've worked with, um, OCV Open Core Ventures, um, which is on Sid, if you know Sid from GitLab, That's his, um, his, uh, his fund, uh, and then also Supabase, which does, um, you know, awesome stuff on Postgres. And, you know, it's fully open source that, that company is amazing as well. and search has been a thing.

So Postgres has full text search, SQLite has full text search. They both have it built in. they're very good and I think great approximations for like V1s at the very least, maybe even farther. because a lot of the time if someone's in your product and they're searching something's wrong usually, right?

Like, like, unless you have vast gobs of data, like this means your UX is not good enough for something, right? Um, but um, that said, I almost always start with Postgres full text search. and then I have the, um, there, there are, there's a huge crop of new search engines, right? So if we consider open search to be new, as in like the fork of Amazon from, from Elastic search, there's that, there's a project called Meilisearch.

There's a project called TypeSense. Um, there's Sonic, uh, there's like, um, Tantivy, uh, which which is like the, can be under net. There's like quickwit, which is like shifted to logging a little bit. Like that's their like, path to sort of, um, profitability. I, I think, I think they, they sort of shifted a little bit.

there's a bunch more that I'm, I'm missing. And so that's what I wrote about and had a lot of fun writing about for Supabase very recently. And this was, um, this was something I just had written down, right? So I was just like, I need to do a blog post. And I, I write on my blog a lot, so I'm just like, Alright.

I write up yak shaves to my blog a lot and I'm, and I was just like, I need to try and just use some of these, right? Because there's so many and they all look pretty good. And they have to have learned, like the golden standard is like, uh, solr, right? Lucene, right? Like, it's like, it's like solr and lucene and like, you know, that or whatever.

And, but a lot of times you just don't need, like, you don't necessarily need every single feature of lucene. And so there are so many new projects that are look decent. Uh, and so I got a chance to, to to sort of, I was paid to do some of that experimentation, which is awesome cause I would've done it anyway.

But it's nice to be paid to do it, on search stuff. and I actually have a project I like, I liked that so much that I made a project to try and get a more representative dataset. So I started a site called podcastsaver.com I use the podcast index, right?

Which has a lot of sort of like podcast information. And, know, if someone doesn't know about podcasts, there's like an RSS feed, right? Which is kind of like a, you can think of an XMLy uh, format where people like podcasts are just a publish of a RSS feed and the RSS feed has links to where to download the actual files, right?

So it's really open, right? Um, and so I used, um, that the structure of that to index, in multiple search engines at once, right? Running alongside each other, the information from the podcast index. this is was fun for me cuz it was like an extension of that other project. It was a really good way to test them against each other.

Very fast, right? Like, or, or like in real time. So like right now, um, if you go to podcastsaver.com and you search a podcast, it will go to one of the search engines randomly. So right now there is Postgres FTS, plus Trigram. So, so there is, um, there's also a thing called, um, Tri Trigram searches another really good like, um, sort of basic search feature.

And there's Meilisearch. So both of those are implemented right now. And there's actually a little nerds link, right? Which will show you how many, how many podcasts there are, right? So, so how many documents, essentially you can kind of assume there are. Um, and it'll show you how fast each search engine did, right?

At sort of returning an answer. Now it's a little bit of a problem because I don't you need to do some manual work to figure out whether the answer was good, right? If you're really fast but give a garbage answer, that's not good. But in general, like, so you can, you can actually use the nerd tab to control, You can like switch to only Postgres, uh, and I do that with like cookies and you can, um, you can force it to go to Postgres and you can see the quality of the answers for yourself.

But they're generally, it's pretty good from both. Like it's not, it's not terrible from, from both. So I'm, I'm kind of like glossing over that part right now, but you can see the performance and it's actually, it's like meilisearch does a great job, right? Um, and you know, there's obviously some complexity in running another service and there's some other caveats and stuff like that, but it's, it's pretty good.

And over time, I want to add more. So I wanna add, you know, at the very least typesense, like people have reached out, so like, I, I made a, a comment on this, on Hacker news and like there's a long road ahead for that and like, I honestly shouldn't be working on that cuz I have other things that I'm like, you know, I, I'm really should be full time on.

Um, But like, that's a thing I'm trying to, I'm trying to do sort of grow in the future a little bit more cuz it's just like, it's so fascinating to, to like, everything's so cheap. Like computer is cheap, you know, like there's awesome projects out there with like really advanced functionality that we can just run, like, for free or not, not for free, but like, you don't have to do the work to like build a search engine.

There's like five out there. So all you, the only thing that's missing is like knowing which one's the best fit for you and like, you can just find that out. Yeah.

[01:30:46] **Jeremy:** Are there any I guess early conclusions in terms of you like Meilisearch because of X or? 

[01:30:53] **Victor:** Yeah, the, the super supabase blog post, uh, was, was a little bit better in terms of, uh, takeaways. I can say that from like meilisearch is definitely faster like meilisearch was harder for me to load and like it took a, a little bit longer cuz you know, you have to do the network call.

And to be fair, if you choose Postgres, it's in the database. So like, your copying is a lot easier. Like, manipulating stuff is a lot easier. Um, but right now when I look at the stats, like Meilisearch goes way faster. It's like almost always under a hundred milliseconds, right? And that's including, you know, um, that network, you know, round trip.

Um, but you know, Postgres is like, I don't know, I just, I just, I think it's, I I'm just so, I'm so biased. Like it is not a good idea to ever bet against Postgres, right? Like, obviously meilisearch is be like, it doesn't make sense for Postgres to be better than purpose-built tools. Um, because they are fully focused, right?

Like, they should be, they should be optimal. Cuz they, they, they don't have any other sort of conflicting constraints to think about. But Postgres is very good. It's just like, it's, it's so excellent and it, it keeps moving. Like it keeps getting better. It gets better and better every year, every like, every quarter. It's hard to not bet on it. So I often, So, so, so yeah, so I just, I, if you, I, I would say based on pure performance of podcastserver.com right now, the data lends itself to saying pick meilisearch. unfortunately that data set is incomplete. I don't have typesense up. I don't have all these other like search engines up.

So, so it's, it's, it's limited. there was also, like in the supabase post, you'll see there, there was support for like, um, misspellings and stuff was different among search engines. So there's also that axis as well. But if you happen to be running on Postgres, I really do suggest just, just give Postgres FTS a try, even if it was just Trigram search.

Like even if you just do Trigram search and do like a sort of like fuzzy search bar, cause that's probably like what a V1 would look like. Anyway, try that and then go off and like, you know, and then like, if you need like crazy faceting or like, you know, you know, really advanced features, then jump off.

Uh, but I, I don't know, that's not interesting cause I feel like it already kind of confirms what I think. So I think other people, other people need to need to do this. I need other people to please replicate, uh, and uh, come up with better, better ideas than I have

[01:33:20] **Jeremy:** but I think that's a good start in, in terms of when you're comparing different solutions, whether it's databases or, I don't know what you call these, but what do you call an elasticsearch?

[01:33:32] **Victor:** Search engine.

[01:33:34] **Jeremy:** You go to open source projects or the company websites and they'll have their charts and go we're x times faster than Y.

But I, I think actually having a running instance where they're going against the same data, I think that's, that's helpful really for anyone trying to compare something to for someone having gone through the time. And I think that a lot of other things too not just search engines where you could have hey, I have my system and it's got, uh I don't know five different databases or something like that. I, I'm not sure the logistics of how you would do it,

[01:34:15] **Victor:** Like with redis. Like just like all the Redis likes, like just all run, run 'em all at the same time. Someone needs to do that 

[01:34:26] **Jeremy:** Could be you.

[01:34:27] **Victor:** Ahaha no! I do too much! Like the redis thing is obvious, right? Redis is easier, like comparing these redises and there's some great blog posts out there also that like kind of do it. But like a running service is like a really good way of like showing like, oh, this is like, we hit this cache, you know, x times a second with like, and it's like this, like naturally random sort of traffic.

This is how it performed, this is how they performed against each other. These were like the, the resources allotted or whatever. But yeah, that stuffs, that stuffs really cool. I feel like people haven't done it or aren't doing it enough. 

[01:35:01] **Jeremy:** Yeah. I guess thing about, putting together one of these tests as well, especially when you make it live is then you have to spend the time and spend the money to maintain it right and I think, uh, if somebody's not paying you to do it's gotta be uh, Yeah. You gotta want it that bad to put it together.

[01:35:22] **Victor:** Hey, but you know what? we can go full circle just use Kubernetes, 

Its easy if you just use Kubernetes man.

[01:35:33] **Jeremy:** First you gotta learn... Where, where were we? First start with postgres, kubernetes.

[01:35:42] **Victor:** Yeah. If you wanna use Kubernetes first, you start with Postgres and... It's like, what?

[01:35:49] **Jeremy:** So, learn these ten other things first then you can start to build your project.

[01:35:58] **Victor:** Yeah, it's silly but I know people out there have the knowledge I just feel like it's, it's like, you they just need to do some of this stuff, right? Like, it's just like, they just like need to like, have the idea or just like go, just go try it Uh, and hopefully we, get more of like, in the future.

Just like, cause, cause at some point, like there's gonna be so much choice that you're like, how are you gonna decide? How does anyone decide these days? Right? Like, you know, more people have to dedicate their time to like, trying out different things, but also sharing it. Cause I think just inside companies, you do this, you do the bakeoffs, right?

Everyone does the bakeoffs to try and figure out, you know, within a week or whatever, whether, whether they should use, let's say like Buddy Base or App Smith, right? Like, just like you, just like the rest of the team has no idea what those are, right? But someone, Does the Bakeoff maybe start sharing Bakeoffs?

There it is. There's another app idea. I, I think of a lot of ideas, and this is a, there's another one, right? Just make a site where people can share their bakeoff, like just share their bakeoff results with certain products. And then that knowledge just being available to people is like, is massively, is massively valuable.

And it, it kind of helps, it helps the products that are mentioned because they can figure out what to change, right? it kind of makes the market more efficient, right? In that vague, uh, capitalistic sense where it's like, oh, like then, you know, if everyone has a chance to improve, then we get a better product at the end of the day.

But, um, yeah, I dunno, Hopefully more people more people yak shave, please, more people waste your time. Uh, not waste, uh, use your time to, uh, to yak shave. It's, it's, it's fine. 

[01:37:32] **Jeremy:** Well I think you have something at the end of it sometimes you can yak shave and at the end it's kind of like, well, I, I played with it and oh well.

Versus you having something to show for it. 

[01:37:50] **Victor:** Yeah, that's true. Yeah. I won't talk about all the other projects that went absolutely nowhere.

But, uh, but yeah, I think you always feel selfish if you learn something to, and I should, I should rephrase this like I am definitely a selfish person. Like you know, like, I'm not, this is not altruism, right? It's just like, but at some point it feels like, man, someone should really know this other stuff, right? Like, if you, if you've found something that's like, interesting, like it's, it's like someone should know, cuz someone who's better at it will be like, Oh, like no, this part and this part.

Like, it's like everyone kind of wins. which is, which is awesome. So, I dunno, maybe if more people have that feeling, they'll like, they'll like share some of their stuff and like maybe you do a thing and it doesn't help you, but then someone else comes along and they're like, Oh, because I read this, I know how to do this.

And like, and then if they give that back too, it's, uh, it's pretty awesome. But anyway, that's all pie in the sky,

[01:38:57] **Jeremy:** I think in general, the fact that you are running a blog and, you know, you do your posts on Hacker News and, and so on. The fact that you're sharing what you've learned, I think it's is super valuable. And I think that goes for anybody who is learning a new technology or working on a problem and you run into issues or things you get stuck on for sure yeah you should share that and the way I've heard described There's always someone on the internet just waiting to tell you why you're wrong. 

[01:39:35] **Victor:** Oh yeah. Yeah. 

[01:39:36] **Jeremy:** And provided that they're right. That can be very helpful. Right?

[01:39:40] **Victor:** Yeah. Yeah. I, I actually, I love I, I personally like it because if you're a hacker in the, you know, hacker news sense that's excellent. That's like a free compiler right?

It's like a free checker right? If you just sit next to someone who is amazing at X.

And you just start bouncing ideas of like, around X and like how to do whatever it is off of them, you get it compiled.

They're just like, No, you can't do that cuz of X, Y, and Z. And you're like, Oh, okay, great. I've just saved myself like, you know, months of like thinking I could do it and like, now I know I can't do it. And the internet is great cuz it gives you access to like, to those people who are like, Yeah. And knowing it first, but if you realize that like, oh, they've chosen to share some wisdom with me like that, like, you know, or, or like trying to, Right.

Assuming you're correct, Like, even if they're not correct. Um, it's, it's, it's pretty awesome. So, so I personally welcome that. Of course it doesn't feel good to be wrong, right? I don't like that. But, um, I love it when someone like take, took the time to be like, No, your, your view on this is wrong because of this.

Or like, you know, like 99% of the time you don't need that. You should have just done this, right? Cause then I learn, a lot of my posts will have updates at the top. Right. So like when someone, like, you know, when I posted the, the thing about the throat mic to like hack me is people were like, This sounds terrible,

I was like, I didn't think it was that bad, but, uh, but I was like, you know, maybe I, maybe I shouldn't use this, uh, all the time, but it, it, you know, it was, it was like obvious that, oh, I should have, I should have never made the post without including a sample of the audio at the top, right? So like, I like went back and like an update for that and then, and then people like discussing about like, Oh, you should have used a bone conducting mic instead.

Like, and like all this other stuff that I just like didn't think about. I'm like, Oh, awesome. 

And then like I update the post I go on with my life, so anyway, more people please do that and don't post it on Medium. Please don't do that. Stop, stop that. If you like, if you, if you write software, do not like, please put it some, put your writing about software somewhere else, unless, I don't know, You have to or something.

[01:41:52] **Jeremy:** You've reached your article limit.

[01:41:57] **Victor:** Yeah, yeah. Oh, also shout out to the web archive. The best way to get almost any article, right? I don't think people in the general populace know this?

But like 99% of the time if you're trying to you just go to the web archive.

It's common knowledge for us. Um, but, but it's not Common knowledge for everybody else and it just feels like they're making a lot of stuff available and legally, right. Cuz like, you know, there's like the, the precedent right now I think is, is is in favor of scraping, right? If you make a thing available to the internet, right?

LinkedIn got ruled against a while ago, but like, if you make a thing available to the internet, uh, publicly available without signing in or whatever it is assumed public, right? So it's just like, yeah, whenever I read something I'm just like, ah, article limit. I hop right on. I hop right on archive today.

But, but I just feel like it's like, it's, it's sad that developers put like, put knowledge enmasse into that particular, It's not a trap. Cause I don't, it's like I don't dislike medium, I don't have any necessarily like animosity towards medium, but it's just like we should be the most capable of, putting up something like maintaining our own websites.

Right. If it's like the death of the personal website, why is it dying with developers? Like, we should be the most capable. We have no hope of the regular world putting out websites if, if it's hard for us.

[01:43:32] **Jeremy:** I, I mean, I think for stuff like medium maybe sometimes it's the, the technical aspect of not wanting to set up your own site but, I think a large part of it is the social aspect. Like with Medium, you have discoverability you have the likes system, if they even call it that. Um, I think that's the same reason why people can be happy to post on twitter, right?

Um, but when it comes to posting on their own blog, it's like well, I post and then nobody comes and sees it, right? Or I don't get the, I don't get the, Well, the thing is too, like, they could be seeing it but you don't get the feedback and you don't get, you don't get the dopamine hit of like, Oh, I got 40 likes on Medium or Twitter or whatever.

And I think that's one of the challenges with personal sites where I totally agree with you. Wish people would do it and do more but I also understand you are on a little bit of an island unless you can get people to come and interact with you.

[01:44:44] **Victor:** There's another idea, right? Like just, you know, can you build a self hostable, but decentralized by default, medium clone. there's that's like a personal site that you could easily host you know, like, almost like WordPress, like let's say, right? Um, but with the, with enough metrics, with like, with the engagement stuff built in, even though it's not like powering a company essentially, right?

Cause like the incentives behind building in the engagement, like pumping up engagement. Make sense? If you're running a company cuz you like, you know, you're trying to get MAUs up so you can do your next round or like, you know, make more revenue. Wonder if, I don't know. Yeah, it's just like, like that is a great point cuz it's like, you don't get the positive reinforcement if you don't have the likes and the things that a company would add, right?

Like, as opposed to just like, Oh, I set up nginx and like my site's up or whatever. Like, not that anyone does that these days, but, yeah, that's, that's that's interesting. It's just like, could you make it really like just increasing the engagement of doing it yourself or like, you know, having that. Huh. 

[01:45:56] **Jeremy:** I think sites have, have tried, I mean, it's not quite the same thing, but, dev.to, if you've seen that, like, uh, they, they have, um, I can't remember what it's called, I think it's like a canonical link or something. but basically you can post on their site and then you can put the canonical link to your own website.

And so then when somebody searches on Google, the, the traffic goes to your site. It doesn't bring up dev.to.

And then, people can comment and like on dev.to so I thought it was an interesting idea. I, I don't know how many people use it or take advantage but that's one approach anyways.

[01:46:44] **Victor:** Yeah, that's actually, that's cool. I don't know enough about that space. I guess.

That sounds awesome. That sounds like actually, you know, useful and like a good middle ground right in like encouraging the ecosystem but also like capturing some of that, of that value, right?

In terms of like just SEO juice, I guess, if you wanna, what, what you wanna call it. But that's awesome. I don't know, I, I, I've always thought of like dev.to And, and clearly I was, you know, at least wrong in part of dev.to Is just like medium 2.0 for, but more developer focused. Um, but I will find great blog posts on there, um, you know, more often than not, and it's just like, okay, yeah, that's, that's awesome.

Like, it, it, it works. Uh, and this canonical link thing sounds actually like very good for, um, for everybody involved, so. Awesome. Sounds like they're, they're good.

[01:47:36] **Jeremy:** Yeah, if people wanna check out you're up to, what, what, you're working on, where should they head?

[01:47:43] **Victor:** Oh God. Uh, well, like, I have my blog at, um, vadosware.io, so V A D O S WARE projects I work biggest ones right now. Oh, I guess three. Um, uh, like I, we mentioned Podcast Saver, which is cool. Uh, if you need to download podcasts, do that.

Um, I send out ideas. I send out ideas every week that I think are like valuable. valuable and like things you could turn up into like a startup or a SaaS and like kind of focus on like validating. Cuz like one thing I've learned the hard way is that validating ideas is more important than having them.

Uh, cuz you can think something is good and it won't, won't attract anybody. Um, or you know, if you don't put it in front of people, they'll, it's not gonna take off. so I do that. I send that out at like unvalidatedideas.com So that's, that's a, you know, that's the domain. 

I also started, um, trying to highlight FOSS projects cuz in yak shaving what you do is you come across a lot of awesome free and open source projects that are just like, oh, like this is a whole world and like this is like pretty polished and it's like pretty good and I just bookmark So I was just like, I have so many bookmarks, it doesn't make sense that I hold all of them. Um, and like I, someone else has, should see this. So I send out, and this is uh, new for me cuz I send out that newsletter every day. So it's a daily newsletter for like free and open source projects that do, you know, do whatever, like, do lots of various things.

And that is at Awesome Foss. So you can actually spell it multiple ways, but a w s m f o s s.com. So like, awesome without the vowels. Um, but also just if you spell it normally like a normal person, like awesome the word f o s s.com. Um, so that's, that's going. 

And then the, the thing that's actually like taking up all my time is nimbus, um, Nimbus Web Services is what I'm calling it.

Uh, it's not out yet, there's nothing to try there, but it is, it is my attempt, to host free and open source software. But give, 10-30% back of revenue, so not profit. Right. Cause they can be different things and like, you know, see the movie industry for like, how that can go wrong, of revenue back to open source projects that, uh, that made the software that I'm hosting.

And I, I think there's more interesting things to be done there, right? Like it can, I can be more aggressive with that. Right. If it, if it works out. Cuz it's just like, you know, it scales so well, you know, see Amazon, right. but yeah, so if you're, if you're interested in that checkout, nimbusws.com.

And that's it. I've, I've plugged everything. Everything plugged.

[01:50:38] **Jeremy:** Yeah that last one sounds pretty, pretty ambitious. So good luck.

[01:50:42] **Victor:** Thanks for taking the time. 

</div>