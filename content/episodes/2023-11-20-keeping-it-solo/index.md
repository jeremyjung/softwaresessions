+++
title = "Mike Perham on Keeping it solo (RubyConf 2023)"

description = "Sidekiq, Ruby's limitations, and sustaining open source"

[extra]
episode_url = "https://pinecast.com/listen/7ea24476-bf37-4a31-bc34-d4f2c80c0a70.mp3"
social_title = "Mike Perham on keeping it solo (RubyConf 2023)"
social_banner = "055-mike-perham.png"
social_description = "Sidekiq, Ruby's limitations, and sustaining open source"
+++

Mike Perham is the creator of Sidekiq, a background job processor for Ruby. He's also the creator of Faktory a similar product for multiple language environments.

We talk about the RubyConf keynote and Ruby's limitations, supporting products as a solo developer, and some ideas for funding open source like a public utility.

Recorded at RubyConf 2023 in San Diego.

--

## A few topics covered:
- Sidekiq (Ruby) vs Faktory (Polyglot)
- Why background job solutions are so common in Ruby
- Global Interpreter Lock (GIL)
- Ractors (Actor concurrency)
- Downsides of Multiprocess applications
- When to use other languages
- Getting people to pay for Sidekiq
- Keeping a solo business
- Being selective about customers
- Ways to keep support needs low
- Open source as a public utility

## Mike
- [Mike's blog](https://www.mikeperham.com/)
- [mastodon](https://ruby.social/@getajobmike)
- [Sidekiq](https://sidekiq.org/)
- [faktory](https://contribsys.com/faktory/)
- [From Employment to Independence](https://codecodeship.com/blog/2023-04-14-mike-perham)

## Ruby
- [Ractor](https://docs.ruby-lang.org/en/master/ractor_md.html)
- [The Practical Effects of the GVL on Scaling in Ruby](https://www.speedshop.co/2020/05/11/the-ruby-gvl-and-scaling.html)

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

## Introduction

[00:00:00] **Jeremy:** I'm here at RubyConf San Diego with Mike Perham. He's the creator of Sidekiq and Faktory. 

[00:00:07] **Mike:** Thank you, Jeremy, for having me here. It's a pleasure.


## Sidekiq

[00:00:11] **Jeremy:** So for people who aren't familiar with, I guess we'll start with Sidekiq because I think that's what you're most known for. If people don't know what it is, maybe you can give like a small little explanation.

[00:00:22] **Mike:** Ruby apps generally have two major pieces of infrastructure powering them. You've got your app server, which serves your webpages and the browser. And then you generally have something off on the side that... It processes, you know, data for a million different reasons, and that's generally called a background job framework, and that's what Sidekiq is.

[00:00:41] It, Rails is usually the thing that, that handles your web stuff, and then Sidekiq is the Sidekiq to Rails, so to speak.

[00:00:50] **Jeremy:** And so this would fit the same role as, I think in Python, there's celery. and then in the Ruby world, I guess there is, uh, Resque is another kind of job.

[00:01:02] **Mike:** Yeah, background job frameworks are quite prolific in Ruby. the Ruby community's kind of settled on that as the, the standard pattern for application development. So yeah, we've got, a half a dozen to a dozen different, different examples throughout history, but the major ones today are, Sidekiq, Resque, DelayedJob, GoodJob, and, and, and others down the line, yeah.


## Why background jobs are so common in Ruby

[00:01:25] **Jeremy:** I think working in other languages, you mentioned how in Ruby, there's this very clear, preference to use these job scheduling systems, these job queuing systems, and I'm not. I'm not sure if that's as true in, say, if somebody's working in Java, or C sharp, or whatnot. And I wonder if there's something specific about Ruby that makes people kind of gravitate towards this as the default thing they would use.

[00:01:52] **Mike:** That's a good question. What makes Ruby... The one that so needs a background job system. I think Ruby, has historically been very single threaded. And so, every Ruby process can only do so much work. And so Ruby oftentimes does, uh, spin up a lot of different processes, and so having processes that are more focused on one thing is, is, is more standard.

[00:02:24] So you'll have your application server processes, which focus on just serving HTTP responses. And then you have some other sort of focused process and that just became background job processes. but yeah, I haven't really thought of it all that much. But, uh, you know, something like Java, for instance, heavily multi threaded.

[00:02:45] And so, and extremely heavyweight in terms of memory and startup time. So it's much more frequent in Java that you just start up one process and that's it. Right, you just do everything in that one process. And so you may have dozens and dozens of threads, both serving HTTP and doing work on the side too. Um, whereas in Ruby that just kind of naturally, there was a natural split there.


## Global Interpreter Lock

[00:03:10] **Jeremy:** So that's actually a really good insight, because... in the keynote at RubyConf, Mats, the creator of Ruby, you know, he mentioned the, how the fact that there is this global, interpreter lock, 

[00:03:23] or, or global VM lock in Ruby, and so you can't, really do multiple things in parallel and make use of all the different cores. And so it makes a lot of sense why you would say like, okay, I need to spin up separate processes so that I can actually take advantage of, of my, system.

[00:03:43] **Mike:** Right. Yeah. And the, um, the GVL. is the acronym we use in the Ruby community, or GIL. Uh, that global lock really kind of is a forcing function for much of the application architecture in Ruby. Ruby, uh, applications because it does limit how much processing a single Ruby process can do. So, uh, even though Sidekiq is heavily multi threaded, you can only have so many threads executing.

[00:04:14] Because they all have to share one core because of that global lock. So unfortunately, that's, that's been, um, one of the limiter, limiting factors to Sidekiq scalability is that, that lock and boy, I would pay a lot of money to just have that lock go away, but. You know, Python is going through a very long term experiment about trying to remove that lock and I'm very curious to see how well that goes because I would love to see Ruby do the same and we'll see what happens in the future, but, it's always frustrating when I come to another RubyConf and I hear another Matt's keynote where he's asked about the GIL and he continues to say, well, the GIL is going to be around, as long as I can tell.

[00:04:57] so it's a little bit frustrating, but. It's, it's just what you have to deal with.


## Ractors

[00:05:02] **Jeremy:** I'm not too familiar with them, but they, they did mention during the keynote I think there Ractors or something like that. There, there, there's some way of being able to get around the GIL but there are these constraints on them. And in the context of Sidekiq and, and maybe Ruby in general, how do you feel about those options or those solutions?

[00:05:22] **Mike:** Yeah, so, I think it was Ruby 3. 2 that introduced this concept of what they call a Ractor, which is like a thread, except it does not have the global lock. It can run independent to the global lock. The problem is, is because it doesn't use the global lock, it has pretty severe constraints on what it can do.

[00:05:47] And the, and more specifically, the data it can access. So, Ruby apps and Rails apps throughout history have traditionally accessed a lot of global data, a lot of class level data, and accessed all this data in a, in a read only fashion. so there's no race conditions because no one's changing any of it, but it's still, lots of threads all accessing the same variables.

[00:06:19] Well, Ractors can't do that at all. The only data Ractors can access is data that they own. And so that is completely foreign to Ruby application, traditional Ruby applications. So essentially, Ractors aren't compatible with the vast majority of existing Ruby code. So I, I, I toyed with the idea of prototyping Sidekiq and Ractors, and within about a minute or two, I just ran into these, these, uh...

[00:06:51] These very severe constraints, and so that's why you don't see a lot of people using Ractors, even still, even though they've been out for a year or two now, you just don't see a lot of people using them, because they're, they're really limited, limited in what they can do. But, on the other hand, they're unlimited in how well they can scale.

[00:07:12] So, we'll see, we'll see. Hopefully in the future, they'll make a lot of improvements and, uh, maybe they'll become more usable over time.


## Downsides of multiprocess (Memory usage)

[00:07:19] **Jeremy:** And with the existence of a job queue or job scheduler like Sidekiq, you're able to create additional processes to get around that global lock, I suppose. What are the... downsides of doing so versus another language like we mentioned Java earlier, which is capable of having true parallelism in the same process.

[00:07:47] **Mike:** Yeah, so you can start up multiple Ruby processes to process things truly in parallel. The issue is that you do get some duplication in terms of memory. So your Ruby app maybe take a gigabyte per process. And, you can do copy on write forking. You can fork and get some memory sharing with copy on write semantics on Unix operating systems.

[00:08:21] But you may only get, let's say, 30 percent memory savings. So, there's still a significant memory overhead to forking, you know, let's say, eight processes versus having eight threads. You know, you, you, you may have, uh, eight threads can operate in a gigabyte process, but if you want to have eight processes, that may take, let's say, four gigabytes of RAM.

[00:08:48] So you, you still, it's not going to cost you eight gigabytes of RAM, you know, it's not like just one times eight, but, there's still a overhead of having those separate processes.

[00:08:58] **Jeremy:** would you say it's more of a cost restriction, like it costs you more to run these applications, or are there actual problems that you can't solve because of this restriction.

[00:09:13] **Mike:** Help me understand, what do you mean by restriction? Do you mean just the GVL in general, or the fact that forking processes still costs memory?

[00:09:22] **Jeremy:** I think, well, it would be both, right? So you're, you have two restrictions right now. You have the, the GVL, which means you can't have parallelism within the same process. And then your other option is to spin up a bunch of processes, which you have said is the downside there is that you're using a lot more RAM.

[00:09:43] I suppose my question is that Does that actually stop you from doing anything? Like, if you throw more money at the problem, you go like, we're going to have more instances, I'll pay for the RAM, it's fine, can that basically get you out of these situations or are these limitations actually stopping you from, from doing things you could do in other languages?

[00:10:04] **Mike:** Well, you certainly have to manage the multiple processes, right? So you've gotta, you know, if one child process crashes, you've gotta have a parent or supervisor process watching all that and monitoring and restarting the process. I don't think it restricts you. Necessarily, it just, it adds complexity to your deployment.

[00:10:24] and, and it's just a question of efficiency, right? Instead of being able to deploy on a, on a one gigabyte droplet, I've got to deploy to a four gigabyte droplet, right? Because I just, I need the RAM to run the eight processes. So it, it, it's more of just a purely a function of how much money am I going to have to throw at this problem.

[00:10:45] And what's it going to cost me in operational costs to operate this application in production?


## When to use other languages?

[00:10:53] **Jeremy:** So during the. Keynote, uh, Matz had mentioned that Rails, is really suitable as this one person framework, like you can have a very small team or maybe even yourself and, and build this product. And so I guess from... Your perspective, once you cross a certain threshold, is like, what Ruby and what Sidekiq provides not enough, and that's why you need to start looking into other languages?

[00:11:24] Or like, where's the, turning point, or the, if you 

[00:11:29] **Mike:** Right, right. The, it's all about the problem you're trying to solve, right? At the end of the day, uh, the, the question is just what are we trying to solve and how are we trying to solve it? So at a higher level, you got to think about the architecture. if the problem you're trying to solve, if the service you're trying to build, if the app you're trying to operate.

[00:11:51] If that doesn't really fall into the traditional Ruby application architecture, then you, you might look at it in another language or another ecosystem. something like Go, for instance, can compile down to a single binary, which makes deployment really easy. It makes shipping up a product. on to a user's machine, much simpler than deploying a Ruby application onto a user's desktop machine, for instance, right?

[00:12:22] Um, Ruby does have this, this problem of how do you package everything together and deploy it somewhere? Whereas Go, when you can just compile to a single binary, now you've just got a single thing. And it's just... Drop it on the file system and execute it. It's easy. So, um, different, different ecosystems have different application architectures, which empower different ways of solving the same problems.

[00:12:48] But, you know, Rails as a, as a one man framework, or sorry, one person framework, It, it, I don't, I don't necessarily, that's a, that's sort of a catchy marketing slogan, but I just think of Rails as the most productive framework you can use. So you, as a single person, you can maximize what you ship and the, the, the value that you can create because Rails is so productive.

[00:13:13] **Jeremy:** So it, seems like it's maybe the, the domain or the type of application you're making. Like you mentioned the command line application, because you want to be able to deliver it to your user easily. Just give them a binary, something like Go or perhaps Rust makes a lot more sense. and then I could see people saying that if you're doing something with machine learning, like the community behind Python, it's, they're just, they're all there.

[00:13:41] So


## Room for more domains in Ruby

[00:13:41] **Mike:** That was exactly the example I was going to use also. Yeah, if you're doing something with data or AI, Python is going to be a more, a more traditional, natural choice. that doesn't mean Ruby can't do it. That doesn't mean, you wouldn't be able to solve the problem with Ruby. And, and there's, that just also means that there's more space for someone who wants to come in and make an impact in the Ruby community.

[00:14:03] Find a problem that Ruby's not really well suited to solving right now and build the tooling out there to, to try and solve it. You know, I, I saw a talk, from the fellow who makes the Glimmer gem, which is a native UI toolkit. Uh, a gem for building native UIs in Ruby, which Ruby traditionally can't do, but he's, he's done an amazing job at sort of surfacing APIs to build these, um, these native, uh, native applications, which I think is great.

[00:14:32] It's awesome. It's, it's so invigorating to see Ruby in a new space like that. Um, I talked to someone else who's doing the Polars gem, which is focused on data processing. So it kind of takes, um, Python and Pandas and brings that to Ruby, which is, is awesome because if you're a Ruby developer, now you've got all these additional tools which can allow you to solve new sets of problems out there.

[00:14:57] So that's, that's kind of what's exciting in the Ruby community right now is just bring it into new spaces.


## Faktory

[00:15:03] **Jeremy:** In addition to Sidekiq, you have, uh, another product called Faktory, I believe. And so does that serve a, a similar purpose? Is that another job scheduling, job queueing system?

[00:15:16] **Mike:** It is, yes. And it's, it's, it's similar in a way to Sidekiq. It looks similar. It's got similar concepts at the core of it. At the end of the day, Sidekiq is limited to Ruby. Because Sidekiq executes in a Ruby VM, it executes the jobs, and the jobs are, have to be written in Ruby because you're running in the Ruby VM.

[00:15:38] Faktory was my attempt to bring, Sidekiq functionality to every other language. I wanted, I wanted Sidekiq for JavaScript. I wanted Sidekiq for Go. I wanted Sidekiq for Python because A, a lot of these other languages also could use a system, a background job system. And the problem though is that.

[00:16:04] As a single man, I can't port Sidekiq to every other language. I don't know all the languages, right? So, Faktory kind of changes the architecture and, um, allows you to execute jobs in any language. it, it replaces Redis and provides a server where you just fetch jobs, and you can use it from it.

[00:16:26] You can use that protocol from any language to, to build your own worker processes that execute jobs in whatever language you want.

[00:16:35] **Jeremy:** When you say it replaces Redis, so it doesn't use Redis, um, internally, it has its own.

[00:16:41] **Mike:** It does use Redis under the covers. Yeah, it starts Redis as a child process and, connects to it over a Unix socket. And so it's really stable. It's really fast. from the outside, the, the worker processes, they just talk to Faktory. They don't know anything about Redis at all.

[00:16:59] **Jeremy:** I see. And for someone who, like we mentioned earlier in the Python community, for example, there is, um, Celery. For someone who is using a task scheduler like that, what's the incentive to switch or use something different?

[00:17:17] **Mike:** Well, I, I always say if you're using something right now, I'm not going to try and convince you to switch necessarily. It's when you have pain that you want to switch and move away. Maybe you have Maybe there's capabilities in the newer system that you really need that the old system doesn't provide, but Celery is such a widely known system that I'm not necessarily going to try and convince people to move away from it, but if people are looking for a new system, one of the things that Celery does that Faktory does not do is Celery provides like data adapters for using store, lots of different storage systems, right?

[00:17:55] Faktory doesn't do that. Faktory is more, has more of the Rails mantra of, you know, Omakase where we choose, I choose to use Redis and that's it. You don't, you don't have a choice for what to use because who cares, you know, at the end of the day, let Faktory deal with it. it's, it's not something that, You should even necessarily be concerned about it.

[00:18:17] Just, just try Faktory out and see how it works for you. Um, so I, I try to take those operational concerns off the table and just have the user focus on, you know, usability, performance, and that sort of thing. but it is, it's, it's another background job system out there for people to try out and see if they like that.

[00:18:36] And, and if they want to, um, if they know Celery and they want to use Celery, more power to Faktory them. 


## Sidekiq (Ruby) or Faktory (Polyglot)

[00:18:43] **Jeremy:** And Sidekiq and Faktory, they serve a very similar purpose. For someone who they have a new project, they haven't chosen a job. scheduling system, if they were using Ruby, would it ever make sense for them to use Faktory versus use Sidekiq?

[00:19:05] **Mike:** Uh Faktory is excellent in a polyglot situation. So if you're using multiple languages, if you're creating jobs in Ruby, but you're executing them in Python, for instance, um, you know, if you've, I have people who are, Creating jobs in PHP and executing them in Python, for instance. That kind of polyglot scenario, Sidekiq can't do that at all.

[00:19:31] So, Faktory is useful there. In terms of Ruby, Ruby is just another language to Faktory. So, there is a Ruby API for using Faktory, and you can create and execute Ruby jobs with Faktory. But, you'll find that in the Ruby community, Sidekiq is much widely... much more widely used and understood and known. So if you're just using Ruby, I think, I think Sidekiq is the right choice.

[00:19:59] I wouldn't look at Faktory. But if you do need, find yourself needing that polyglot tool, then Faktory is there.


## Temporal

[00:20:07] **Jeremy:** And this is maybe one, maybe one layer of abstraction higher, but there's a product called Temporal that has some of this job scheduling, but also this workflow component. I wonder if you've tried that out and how you think about that product?

[00:20:25] **Mike:** I've heard of them. I don't know a lot about the product. I do have a workflow API, the Sidekiq batches, which allow you to fan out jobs and then, and then execute callbacks when all the jobs in that, in that batch are done. But I don't, provide sort of a, a high level. Graphical Workflow Editor or anything like that.

[00:20:50] Those to me are more marketing tools that you use to sell the tool for six figures. And I don't think they're usable. And I don't think they're actually used day to day. I provide an API for developers to use. And developers don't like moving blocks of code around in a GUI. They want to write code. And, um, so yeah, temporal, I, like I said, I don't know much about them.

[00:21:19] I also, are they a venture capital backed startup?

[00:21:22] **Jeremy:** They are, is my understanding,

[00:21:24] **Mike:** Yeah, that, uh, any, any sort of venture capital backed startup, um, who's building technical infrastructure. I, I would look long and hard at, I'm, I think open source is the right core to build on. Of course I sell commercial software, but. I'm bootstrapped. I'm profitable.

[00:21:46] I'm going to be around forever. A VC backed startup, they tend to go bankrupt, because they either get big or they go out of business. So that would be my only comment is, is, be a little bit leery about relying on commercial venture capital based infrastructure for, for companies, uh, long term.


## Getting people to pay for Sidekiq

[00:22:05] **Jeremy:** So I think that's a really interesting part about your business is that I think a lot of open source maintainers have a really big challenge figuring out how to make it as a living. The, there are so many projects that they all have a very permissive license and you can use them freely one example I can think of is, I, I talked with, uh, David Kramer, who's the CTO at Sentry, and he, I don't think they use it anymore, but they, they were using Nginx, right?

[00:22:39] And he's like, well, Nginx, they have a paid product, like Nginx. Plus that or something. I don't know what the name is, but he was like, but I'm not going to pay for it. Right. I'm just going to use the free one. Why would I, you know, pay for the, um, the paid thing? So I, I, I'm kind of curious from your perspective when you were coming up with Sidekiq both as an open source product, but also as a commercial one, how did you make that determination of like to make a product where it's going to be useful in its open source form?

[00:23:15] I can still convince people to pay money for it.

[00:23:19] **Mike:** Yeah, the, I was terrified, to be blunt, when I first started out. when I started the Sidekiq project, I knew it was going to take a lot of time. I knew if it was successful, I was going to be doing it for the next decade. Right? So I started in 2012, and here I am in 2023, over a decade, and I'm still doing it.

[00:23:38] So my expectation was met in that regard. And I knew I was not going to be able to last that long. If I was making zero dollars, right? You just, you burn out. Nobody can last that long. Well, I guess there are a few exceptions to that rule, but yeah, money, I tend to think makes things a little more sustainable for sure.

[00:23:58] Especially if you can turn it into a full time job solving and supporting a project that you, you love and, and is, is, you know, your, your, your baby, your child, so to speak, your software, uh, uh, creation that you've given to the world. but I was terrified. but one thing I did was at the time I was blogging a lot.

[00:24:22] And so I was telling people about Sidekiq. I was telling people what was to come. I was talking about ideas and. The one thing that I blogged about was financial experiments. I said bluntly to the, to, to the Ruby community, I'm going to be experimenting with financial stability and sustainability with this project.

[00:24:42] So not only did I create this open source project, but I was also publicly saying I I need to figure out how to make this work for the next decade. And so eventually that led to Sidekiq Pro. And I had to figure out how to build a closed source Ruby gem, which, uh, There's not a lot of, so I was kind of in the wild there.

[00:25:11] But, you know, thankfully all the pieces came together and it was actually possible. I couldn't have done it if it wasn't possible. Like, we would not be talking if I couldn't make a private gem. So, um, but it happened to work out. Uh, and it allowed me to, to gate features behind a paywall effectively. And, and yeah, you're right.

[00:25:33] It can be tough to make people pay for software. but I'm a developer who's selling to other developers, not, not just developers, open source developers, and they know that they have this financial problem, right? They know that there's this sustainability problem. And I was blunt in saying, this is my solution to my sustainability.

[00:25:56] So, I charge what I think is a very fair price. It's only a thousand dollars a year to a hobbyist. That may seem like a lot of money to a business. It's a drop in the bucket. So it was easy for developers to say, Hey, listen, we want to buy this tool for a thousand bucks. It'll ensure our infrastructure is maintained for the next decade.

[00:26:18] And it's, and it's. And it's relatively cheap. It's way less than, uh, you know, a salary or even a laptop. So, so that's, that's what I did. And, um, it's, it worked out great. People, people really understood. Even today, I talk to people and they say, we, we signed up for Sidekiq Pro to support you. So it's, it's, it's really, um, invigorating to hear people, uh, thank me and, and they're, they're actively happy that they're paying me and our customers.

[00:26:49] **Jeremy:** it's sort of, uh, maybe a not super common story, right, in terms of what you went through. Because when I think of open core businesses, I think of companies like, uh, GitLab, which are venture funded, uh, very different scenario there. I wonder, like, in your case, so you started in 2012, and there were probably no venture backed competitors, right?

[00:27:19] People saying that we're going to make this job scheduling system and some VC is going to give me five million dollars and build a team to work on this. It was probably at the time, maybe it was Rescue, which was...

[00:27:35] **Mike:** There was a venture backed system called IronMQ,

[00:27:40] **Jeremy:** Hmm.

[00:27:41] **Mike:** And I'm not sure if they're still around or not, but they... They took, uh, one or more funding rounds. I'm not sure exactly, but they were VC backed. They were doing, background jobs, scheduled jobs, uh, you know, running container, running container jobs. They, they eventually, I think, wound up sort of settling on Docker containers.

[00:28:06] They'll basically spin up a Docker container. And that container can do whatever it wants. It can execute for a second and then shut down, or it can run for, for however long, but they would, um, yeah, I, yeah, I'll, I'll stop there because I don't know the actual details of exactly their system, but I'm not sure if they're still around, but that's the only one that I remember offhand that was around, you know, years ago.

[00:28:32] Yeah, it's, it's mostly, you know, low level open source infrastructure. And so, anytime you have funded startups, they're generally using that open source infrastructure to build their own SaaS. And so SaaS's are the vast majority of where you see sort of, uh, commercial software.

[00:28:51] **Jeremy:** so I guess in that way it, it, it gave you this, this window or this area where you could come in and there wasn't, other than that iron, product, there wasn't this big money that you were fighting against. It was sort of, it was you telling people openly, I'm, I'm working on this thing.

[00:29:11] I need to make money so that I can sustain it. And, if you, yeah. like the work I do, then, you know, basically support me. Right. And, and so I think that, I'm wondering how we can reproduce that more often because when you see new products, a lot of times it is VC backed, right?

[00:29:35] Because people say, I need to work on this. I need to be paid. and I can't ask a team to do this. For nothing, right? So

[00:29:44] **Mike:** Yeah. It's. It's a wicked problem. Uh, it's a really, really hard problem to solve if you take vc you there, that that really kind of means that you need to be making tens if not hundreds of millions of dollars in sales. If you are building a small or relatively small. You know, put small in quotes there because I don't really know what that means, but if you have a small open source project, you can't charge huge amounts for it, right?

[00:30:18] I mean, Sidekiq is a, I would call a medium sized open source project, and I'm charging a thousand bucks for it. So if you're building, you know, I don't know, I don't even want to necessarily give example, but if you're building some open source project, and It's one of 300 libraries that people's applications will depend on.

[00:30:40] You can't necessarily charge a thousand dollars for that library. depending on the size and the capabilities, maybe you can, maybe you can't. But there's going to be a long tail of open source projects that just, they can't, they can't charge much, if anything, for them. So, unfortunately, we have, you know, these You kind of have two pathways.

[00:31:07] Venture capital, where you've got to sell a ton, or free. And I've kind of walked that fine line where I'm a small business, I can charge a small amount because I'm bootstrapped. And, and I don't need huge amounts of money, and I, and I have a project that is of the right size to where I can charge a decent amount of money.

[00:31:32] That means that I can survive with 500 or a thousand customers. I don't need to have a hundred million dollars worth of customers. Because I, you know, when I started the business, one of the constraints I said is I don't want to hire anybody. I'm just going to be solo. And part of the, part of my ability to keep a low price and, and keep running sustainably, even with just You know, only a few hundred customers is because I'm solo.

[00:32:03] I don't have the overhead of investors. I don't have the overhead of other employees. I don't have an office space. You know, my overhead is very small. So that is, um, you know, I just kind of have a unique business in that way, I guess you might say.


## Keeping the business solo

[00:32:21] **Jeremy:** I think that's that's interesting about your business as well But the fact that you've kept it you've kept it solo which I would imagine in most businesses, they need support people. they need, developers outside of maybe just one. Um, there's all sorts of other, I don't think overhead is the right word, but you just need more people, right?

[00:32:45] And, and what do you think it is about Sidekiq that's made it possible for it to just be a one person operation?

[00:32:52] **Mike:** There's so much administrative overhead in a business. I explicitly create business policies so that I can run solo. you know, my support policy is officially you get one email ticket or issue per quarter. And, and anything more than that, I can bounce back and say, well, you're, you're requiring too much support.

[00:33:23] In reality, I don't enforce that at all. And people email me all the time, but, but things like. Things like dealing with accounting and bookkeeping and taxes and legal stuff, licensing, all that is, yeah, a little bit of overhead, but I've kept it as minimal as I can. And part of that is I don't want to hire another employee because then that increases the administrative overhead that I have.

[00:33:53] And Sidekiq is so tied to me and my knowledge that if I hire somebody, they're probably not going to know Ruby and threading and all the intricate technical detail necessary to build and maintain and support the system. And so really you'll kind of regress a little bit. We won't be able to give as good support because I'm busy helping that other employee.


## Being selective about customers

[00:34:23] **Mike:** So, yeah, it's, it's a tightrope act where you've got to really figure out how can I scale myself as far as possible without overwhelming myself. The, the overwhelming thing that I have that I've never been able to solve. It's just dealing with billing inquiries, customers, companies, emailing me saying, how do we buy this thing?

[00:34:46] Can I get an invoice? Every company out there, it seems wants an invoice. And the problem with invoicing is it takes a lot more. manual labor and administrative overhead to issue that invoice to collect payment on the invoice. So that's one of the reasons why I have a very strict policy about credit card only for, for the vast majority of my customers.

[00:35:11] And I demand that companies pay a lot more. You have to have a pretty big enterprise license if you want an invoice. And if the company, if the company comes back and complains and says, well, you know, that's ridiculous. We don't, we don't want to pay that much. We don't need it that much. Uh, you know, I, I say, okay, well then you have two, two things, two, uh, two things.

[00:35:36] You can either pay with a credit card or you can not use Sidekiq. Like, that's, that's it. I'm, I don't need your money. I don't want the administrative overhead of dealing with your accounting department. I just want to support my, my customers and build my software. And, and so, yeah, I don't want to turn into a billing clerk.

[00:35:55] So sometimes, sometimes the, the, the best thing in business that you can do is just say no.

[00:36:01] **Jeremy:** That's very interesting because I think being a solo... Person is what probably makes that possible, right? Because if you had the additional staff, then you might say like, Well, I need to pay my staff, so we should be getting, you know, as much business as

[00:36:19] **Mike:** Yeah. Chasing every customer you can, right. But yeah.

[00:36:22] Every customer is different. I mean, I have some customers that just, they never contact me. They pay their bill really fast or right on time. And they're paying me, you know, five figures, 20, a year. And they just, it's a, God bless them because those are, are the.

[00:36:40] Best customers to have and the worst customers are the ones who are paying 99 bucks a month and everything that they don't understand or whatever is a complaint. So sometimes, sometimes you, you want to, vet your customers from that perspective and say, which one of these customers are going to be good?

[00:36:58] Which ones are going to be problematic?

[00:37:01] **Jeremy:** And you're only only person... And I'm not sure how many customers you have, but 

[00:37:08] **Mike:** I have 2000

[00:37:09] **Jeremy:** 2000 customers. 

[00:37:10] Okay. 

[00:37:11] **Mike:** Yeah.

[00:37:11] **Jeremy:** And has that been relatively stable or has there been growth

[00:37:16] **Mike:** It's been relatively stable the last couple of years. Ruby has, has sort of plateaued. Um, it's, you don't see a lot of growth. I'm getting probably, um, 15, 20 percent growth maybe. Uh, so I'm not growing like a weed, like, you know, venture capital would want to see, but steady incremental growth is, is, uh, wonderful, especially since I do very little.

[00:37:42] Sales and marketing. you know, I come to RubyConf I, I I tweet out, you know, or I, I toot out funny Mastodon Toots occasionally and, and, um, and, and put out new releases of the software. And, and that's, that's essentially my, my marketing. My marketing is just staying in front of developers and, and, and being a presence in the Ruby community.

[00:38:06] But yeah, it, it's, uh. I, I, I see not a, not a huge amount of churn, but I see enough sales to, to, to stay up and keep my head above water and to keep growing, um, slowly but surely.


## Support needs haven't grown

[00:38:20] **Jeremy:** And as you've had that steady growth, has the support burden not grown with it?

[00:38:27] **Mike:** Not as much because once customers are on Sidekiq and they've got it working, then by and large, you don't hear from them all that much. There's always GitHub issues, you know, customers open GitHub issues. I love that. but yeah, by and large, the community finds bugs. and opens up issues. And so things remain relatively stable.

[00:38:51] I don't get a lot of the complete newbie who has no idea what they're doing and wants me to, to tell them how to use Sidekiq that I just don't see much of that at all. Um, I have seen it before, but in that case, generally, I, I, I politely tell that person that, listen, I'm not here to educate you on the product.

[00:39:14] It's there's documentation in the wiki. Uh, and there's tons of, of more Ruby, generic Ruby, uh, educational material out there. That's just not, not what I do. So, so yeah, by and large, the support burden is, is not too bad because once people are, are up and running, it's stable and, and they don't, they don't need to contact me.

[00:39:36] **Jeremy:** I wonder too, if that's perhaps a function of the price, because if you're a. new developer or someone who's not too familiar with how to do job processing or what they want to do when you, there is the open source product, of course. but then the next step up, I believe is about a hundred dollars a month.

[00:39:58] And if you're somebody who is kind of just getting started and learning how things work, you're probably not going to pay that, is my guess. And so you'll never hear from them.

[00:40:11] **Mike:** Right, yeah, that's a good point too, is the open source version, which is what people inevitably are going to use and integrate into their app at first. Because it's open source, you're not going to email me directly, um, and when people do email me directly, Sidekiq support questions, I do, I reply literally, I'm sorry I don't respond to private email, unless you're a customer.

[00:40:35] Please open a GitHub issue and, um, that I try to educate both my open source users and my commercial customers to try and stay in GitHub issues because private email is a silo, right? Private email doesn't help anybody else but them. If I can get people to go into GitHub issues, then that's a public record.

[00:40:58] that people can search. Because if one person has that problem, there's probably a dozen other people that have that same problem. And then that other, those other 11 people can search and find the solution to their problem at four in the morning when I'm asleep. Right? So that's, that's what I'm trying to do is, is keep, uh, keep everything out in the open so that people can self service as much as possible.


## Sidekiq open source

[00:41:24] **Jeremy:** And on the open source side, are you still primarily the main contributor? Or do you have other people that are

[00:41:35] **Mike:** I mean, I'd say I do 90 percent of the work, which is why I don't feel guilty about keeping 100 percent of the money. A lot of open source projects, when they look for financial sustainability, they also look for how can we split this money amongst the team. And that's, that's a completely different topic that I've.

[00:41:55] is another reason why I've stayed solo is if I hire an employee and I pay them 200, 000 a year as a developer, I'm meanwhile keeping all the rest of the profits of the company. And so that almost seems a little bit unfair. because we're both still working 40 hours a week, right? Why am I the one making the vast majority of the, of the profit and the money?

[00:42:19] Um, so, uh, I've always, uh, that's another reason why I've stayed solo, but, but yeah, having a team of people working on something, I do get, regular commits, regular pull requests from people, fixing a bug that they found or just making a tweak that. that they saw, that they thought they could improve.

[00:42:42] A little more rarely I get a significant improvement or feature, as a pull request. but Sidekiq is so stable these days that it really doesn't need a team of people maintaining it. The volume of changes necessary, I can easily keep up with that. So, I'm still doing 90 95 percent of the work.


## Are there other Sidekiq-like opportunities out there?

[00:43:07] **Jeremy:** Yeah, so I think Sidekiq has sort of a unique positioning where it's the code base itself is small enough where you can maintain it yourself and you have some help, but primarily you're the main maintainer. And then you have enough customers who are willing to, to pay for the benefit it gives them on top of what the open source product provides.

[00:43:36] cause it's, it's, you were talking about how. Every project people work on, they have, they could have hundreds of dependencies, right? And to ask somebody to, to pay for each of them is, is probably not ever going to happen. And so it's interesting to think about how you have things like, say, you know, OpenSSL, you know, it's a library that a whole bunch of people rely on, but nobody is going to pay a monthly fee to use it.

[00:44:06] You have things like, uh, recently there was HashiCorp with Terraform, right? They, they decided to change their license because they, they wanted to get, you know, some of that value back, some of the money back, and the community basically revolted. Right? And did a fork. And so I'm kind of curious, like, yeah, where people can find these sweet spots like, like Sidekiq, where they can find this space where it's just small enough where you can work on it on your own and still get people to pay for it.

[00:44:43] It's, I'm trying to picture, like, where are the spaces?


## Open source as a public utility

[00:44:48] **Mike:** We need to look at other forms of financing beyond pure capitalism. If this is truly public infrastructure that needs to be maintained for the long term, then why are we, why is it that we depend on capitalism to do that? Our roads, our water, our sewer, those are not Capitalist, right? Those are utilities, that's public infrastructure that we maintain, that the government helps us maintain.

[00:45:27] And in a sense, tech infrastructure is similar or could be thought of in a similar fashion. So things like Open Collective, things like, uh, there's a, there's a organization in Europe called NLNet, I think, out of the Netherlands. And they do a lot of grants to various open source projects to help them improve the state of digital infrastructure.

[00:45:57] They support, for instance, Mastodon as a open source project that doesn't have any sort of corporate backing. They see that as necessary social media infrastructure, uh, for the long term. And, and I, and I think that's wonderful. I like to see those new directions being explored where you don't have to turn everything into a product, right?

[00:46:27] And, and try and market and sale, um, and, and run ads and, and do all this stuff. If you can just make the case that, hey, this is, this is useful public infrastructure that so many different, um, Technical, uh, you know, applications and businesses could rely on, much like FedEx and DHL use our roads to the benefit of their own, their own corporate profits.

[00:46:53] Um, why, why, why shouldn't we think of tech infrastructure sort of in a similar way? So, yeah, I would like to see us explore more. in that direction. I understand that in America that may not happen for quite a while because we are very, capitalist focused, but it's encouraging to see, um, places like Europe, uh, a little more open to, to trialing things like, cooperatives and, and grants and large long term grants to, to projects to see if they can, uh, provide sustainability in, in, you know, in a new way.

[00:47:29] **Jeremy:** Yeah, that's a good point because I think right now, a lot of the open source infrastructure that we all rely on, either it's being paid for by large companies and at the whim of those large companies, if Google decides we don't want to pay for you to work on this project anymore, where does the money come from?

[00:47:53] Right? And on the other hand, there's the thousands, tens of thousands of people who are doing it. just for free out of the, you know, the goodness of their, their heart. And that's where a lot of the burnout comes from. Right. So I think what you're saying is that perhaps a lot of these pieces that we all rely on, that our, our governments, you know, here in the United States, but also around the world should perhaps recognize as this is, like you said, this is infrastructure, and we should be.

[00:48:29] Paying these people to keep the equivalent of the roads and, and, uh, all that working. 

[00:48:37] **Mike:** Yeah, I mean, I'm not, I'm not claiming that it's a perfect analogy. There's, there's, there's lots of questions that are unanswered in that, right? How do you, how do you ensure that a project is well maintained? What does that even look like? What does that mean? you know, you can look at a road and say, is it full of potholes or is it smooth as glass, right?

[00:48:59] It's just perfectly obvious, but to a, to a digital project, it's, it's not as clear. So, yeah, but, but, but exploring those new ways because turning everybody into a businessman so that they can, they can keep their project going, it, it, it itself is not sustainable, right? so yeah, and that's why everything turns into a SaaS because a SaaS is easy to control.

[00:49:24] It's easy to gatekeep behind a paywall and it's easy to charge for, whereas a library on GitHub. Yeah. You know, what do you do there? You know, obviously GitHub has sponsors, the sponsors feature. You've got Patreon, you've got Open Collective, you've got Tidelift. There's, there's other, you know, experiments that have been run, but nothing has risen to the top yet.

[00:49:47] and it's still, it's still a bit of a grind. but yeah, we'll see, we'll see what happens, but hopefully people will keep experimenting and, and maybe, maybe governments will start. Thinking in the direction of, you know, what does it mean to have a budget for digital infrastructure maintenance?

[00:50:04] **Jeremy:** Yeah, it's interesting because we, we started thinking about like, okay, where can we find spaces for other Sidekiqs? But it sounds like maybe, maybe that's just not realistic, right? Like maybe we need more of a... Yeah, a rethinking of, I guess the, the structure of how people get funded. Yeah.

[00:50:23] **Mike:** Yeah, sometimes the best way to solve a problem is to think at a higher level. You know, we, the, the sustainability problem in American Silicon Valley based open source developers is naturally going to tend toward venture capital and, and capitalism. And I, you know, I think, I think that's, uh, extremely problematic on a, on a lot of different, in a lot of different ways.

[00:50:47] And, and so sometimes you need to step back and say, well, maybe we're, maybe we just don't have the right tool set to solve this problem. But, you know, I, I. More than that, I'm not going to speculate on because it is a wicked problem to solve.

[00:51:04] **Jeremy:** Is there anything else you wanted to, to mention or thought we should have talked about?

[00:51:08] **Mike:** No, I, I, I loved the talk, of sustainability and, and open source. And I, it's, it's a, it's a topic really dear to my heart, obviously. So I, I am happy to talk about it at length with anybody, anytime. So thank you for having me.

[00:51:25] **Jeremy:** All right. Thank you very much, Mike.