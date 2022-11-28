+++
title = "WebAssembly on the Server with Krustlet"

description = "Taylor Thomas explains how Krustlet runs WebAssembly modules in Kubernetes and why it's a promising option for the future of server side applications."

[extra]
episode_url = "https://pinecast.com/listen/d20fe073-c099-46a4-99b2-5c19c9a7cc47.mp3"
social_title = "WebAssembly on the Server with Krustlet"
social_description = "Running WebAssembly inside Kubernetes"
+++

[Taylor Thomas](https://twitter.com/_oftaylor) is an Engineer at Azure, the core maintainer of the Kubernetes Package Manager [Helm](https://helm.sh/), and a member of the Krustlet team.

### Timestamps 

- [00:55] - Kubernetes
- [07:37] - WebAssembly
- [12:06] - WebAssembly Runtimes and WASI Specification
- [15:42] - WebAssembly vs Containers vs Native Binaries
- [25:11] - Krustlet and the case for writing it in Rust
- [30:52] - Missing APIs in WASI 
- [33:38] - Wascc vs Wasmtime runtimes
- [38:15] - Rust ecosystem for Kubernetes and WebAssembly
- [40:23] - Comparing other languages to Rust
- [45:09] - Rust learning curve, experiences as a beginner
- [53:16] - Next steps for Krustlet and WebAssembly

### Related Links

- [@_oftaylor](https://twitter.com/_oftaylor)
- [Krustlet](https://github.com/deislabs/krustlet)
- [Kubernetes](https://kubernetes.io/)
- [Open Container Initiative](https://opencontainers.org/)
- [WebAssembly](https://webassembly.org/)
- [WASI](https://wasi.dev/)
- [Wasmtime](https://wasmtime.dev/)
- [waSCC](https://wascc.dev/)
- [WebAssembly meets Kubernetes with Krustlet](https://cloudblogs.microsoft.com/opensource/2020/04/07/announcing-krustlet-kubernetes-rust-kubelet-webassembly-wasm/)
- [Introducing Krustlet, the WebAssembly Kubelet](https://deislabs.io/posts/introducing-krustlet/)
- [Kubernetes: A Rusty Friendship](https://deislabs.io/posts/kubernetes-a-rusty-friendship/)
- [The Safety Boat: Kubernetes and Rust](https://msrc-blog.microsoft.com/2020/04/29/the-safety-boat-kubernetes-and-rust/)
- [A Heaping Helping of Stacks](https://deislabs.io/posts/a-heaping-helping-of-stacks/)

This episode is also posted on [Rustacean Station](https://rustacean-station.org/).

Music by Crystal Cola: [12:30 AM](https://crystalcola.bandcamp.com/track/12-30-am) / [Orion](https://crystalcola.bandcamp.com/track/orion)

---

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

Jeremy: [00:00:00] Hey, this is Jeremy Jung. This episode, I'm talking to Taylor Thomas about running WebAssembly on the server with Rust. He's an engineer on the Azure team. The core maintainer of Helm, which is a package manager for Kubernetes. And he's currently working on Krustlet, which runs WebAssembly applications within Kubernetes. 

Also, during our conversation, you're going to hear us talk about WASM. That's shorthand for WebAssembly. All right. I hope you enjoy my talk with Taylor. Taylor thanks for joining me today.

Taylor: [00:00:30] Thank you for having me, Jeremy. This is my first Rust related podcast so it's exciting for me. I'm a fairly new rustacean all things considered, so I'm happy to be here.

Jeremy: [00:00:41] For people who aren't familiar with the world of kubernetes and containerization all these different things. Could you start by explaining at a high level what Kubernetes is?

Taylor: [00:00:55] Yeah, so Kubernetes, is a container orchestrator. And you've probably at least heard of Docker if you're in the technology world even if you haven't used it. But Docker is a technology that made something called containers popular and useful. Those technologies have been around for a while inside of the Linux kernel that's why they call it a container everything is inside of this thing and contained in this process. It uses C groups and kernel namespaces. There's a couple of different things under the hood that are going on. But basically it allows you to create an artifact that can be bundled up into something called an image.

And that image can be passed around and then be used multiple times. So often people will compare those to VMs. VMs were a big revelation, right? Because you didn't have to go literally put in a new blade if you needed a new server or reboot something you had to instead just say, okay, I want a new VM. 

But you still had to install a whole operating system. It was like spinning up a new computer. And so containers made that even more simple because instead of having to do that, it's using the same shared underlying, kernel calls and things underneath the hood, but everything's isolated. And so if you want to spin up three different instances of an nginx server all you'd have to do is create three containers that are all running at the same time and those will all have the same specification that you basically baked into there. An immutable artifact. If you want to create a new one it has a new hash and a new version. So this was really good for people, but the problem is how do you orchestrate it across everything?

And that's where Kubernetes came in. So Kubernetes takes that and says, okay, well we have a huge fleet of nodes. That's out there. How do I schedule each of these containers properly so that they're either not on the same place or that they meet certain requirements or that I have a certain number of them.

It takes care of all that including some of the underlying networking connections so that you can connect all your containers to each other in a distributed and actually self-healing way it goes through loops. And if something goes wrong, it will try to heal that container and make it come back to a normal running state.

And so it is a very powerful technology it's caught on... maybe it's caught on a little too much in some people's opinions, but it's a useful tool for containers that came about and a lot of people are using it for underlying infrastructure projects.

Jeremy: [00:03:16] It reminds me a little bit of when you're using something like AWS and it has auto-scaling for VMs. And let's say that you have an application and it runs on virtual machines. And you would be able to tell AWS as more people are accessing my application I want you to create new VMs [and] run new instances of my application.

Something like Kubernetes is able to do something similar, but maybe at a more generic level of being able to figure out. Okay. How many machines do I have access to? And anytime I'm asked to run something, I'll go and find the right machine to run it on. And it's always going to be in the context of these containers. Did I kind of get that right?

Taylor: [00:04:15] Yes, it's very much a generic tool across all these different things. And nowadays you can run it with, with windows or Linux or mostly windows and Linux. But there are some limitations there, but yes, it's a very generic tool. In terms of being able to connect what you want and use what you want to, to make this distributed platform easy.

And like you said it will scale things. If you've done something in AWS where you have the elastic things where they'll scale it's a similar thing. There's something in Kubernetes that you can set up that it will automatically scale to make sure that you have the right around right amount of capacity for what you're doing.

Jeremy: [00:04:50] And I think this takes away the need for the developer to need to understand where their applications are going to run. It's. You give some kind of configuration to Kubernetes and say, here's my app. And then it just figures out, where to run it and how many instances to run and that sort of thing.

Taylor: [00:05:12] Yeah, it's really meant as a dev ops or SRE kind of tool that instead of it being a. they have to like custom tailor machines. They already have these Docker images in place and can just run them, like you said. you just give it the configuration and it is still involved. It's not like a magic bullet there, but you don't have to care as much about where it goes if you've configured everything properly, it just kinda does it.

Jeremy: [00:05:36] I wonder if you could paint a picture of, where containers fit in between just running a full machine versus running a single process on a computer.

Taylor: [00:05:47] Essentially a container is just a running process, a single process. And because it's a single running process, you can run multiple of them on a machine. The tools that you need installed, all the binaries, all those different things are encapsulated inside of this container.

And so that way you can run 10 of them on a machine instead of spinning up 10 servers. So it allows a little bit more density, and obviously you still have to be careful about what noisy neighbor problems and other things that normally happen in infrastructure, but it allows for much more condensed areas. And the spin up is much quicker. If you have a small image that you have to get getting a new one and spinning it up is easily under 30 seconds every time. bigger images can take longer, but even then it's still faster than provisioning a full VM for what you're trying to do. And so this fits for a lot of different kinds of services that, don't need like very, like large, large requirements on the system.

And even if you do have large requirements, you can use Kubernetes in a way that can be helpful.

Jeremy: [00:06:45] And so you're talking about how these containers are a process running on the system. So for example, if I were to in windows, look at the task manager or in Linux, just run ps, I would see individual processes for each of these containers that are being run.

Taylor: [00:07:05] Yes. It really depends on the implementation, but essentially that's, what's going on. There's with Docker, there's some other underlying details, so we don't need to get into, but essentially you would see processes that, that are spun up that are, are doing the work, but they are just processes underneath the hood instead of being a full operating system.

Jeremy: [00:07:23] Next, I want to talk a little bit about, WebAssembly, because I know that's an important part of the krustlet project that you work on. Could you explain a little bit about what WebAssembly is at a high level?

Taylor: [00:07:37] Yeah, so WebAssembly, as you can probably guess from the name is a tool that was originally designed for the web. Now, that's I think the original creators didn't necessarily intend it to be that way, but that's the name that it has. And that's what it's used for. There's multiple, companies and, big websites use WebAssembly. And the idea behind WebAssembly is that you can create a binary that can then be consumed. So it's compiled code that can then be run in the browser. So giving you the speed of compiled code. While also, still being sandboxed inside of the browser sandbox environment.

So this allows for some very performant things to be done. You have things like rendering tools. I know one that I've seen an example I always give is one. I like Autodesk, which they're maker of CAD tools and rendering tools. They have a lot of online things that run WebAssembly. Because it's, it gives it the performance.

It needs to be able to do those more complex tasks. And so that's where WebAssembly started, but the idea is WebAssembly could be used anywhere. And when you pull out a WebAssembly from just the browser, it allows you to have kind of a universal interface and what this is called, they've defined it. And there's a working group and it's still very much a work in progress, but it's called WASI, which stands for WebAssembly system interface.

And that interface is a definition of basically how it can interact with the system. And the nice thing about it is it still that sandboxed model, you have to grant explicit permission to do anything. So if you want it to be able to access a file somewhere, you have to grant access to that file ahead of time before you start it, It's not there yet, but I assume when we get to some of the networking socket support in there, it will also have those. You have to grant specific permission for it to do it. Whereas opposed to containers, you have a little bit a different security model because you're still running like into the normal Linux security things that you have to deal with.

there's ways to break out of a container. There's not really a way to break out of a WebAssembly module in the same way. because. You, you're not, you're not running in these, like you're running a compiled code thing somewhere instead of basically like a shim over specific binaries or things that are being run.

so that's, that's the main difference, and this allows things to be run on any system. one of the things that we, we saw with Docker and that we were really hoping when, when we, when we had that Docker was that it could run anywhere. But if we're being honest with ourselves, it can't really run anywhere Docker and containers in general are a Linux tool. Now there's people, well, who at Microsoft and elsewhere have made Windows containers, a thing, they work, they work well there's some really cool work they've done. And there's nothing. I have nothing to say against that. They're they they've done great work, but, but really if you have a nginx container, You can't run that on a windows machine.

You can run it on a windows machine, but it's technically running a Linux VM behind the scenes, same thing on a Mac. And so it isn't truly this, ideal of write once run anywhere. Now, obviously there there's still technical challenges there. You can't do it completely, but you can come. So if I compile a WebAssembly module, a WASI compatible.

WebAssembly module on my Mac. I can pass it to you and you can run it on a windows machine, on a Linux machine, on a raspberry PI. It doesn't matter because, and it'll be the exact same code. so that is a very powerful thing that we saw in WebAssembly that fits also fairly well inside of this container space and what we could do with it.

Jeremy: [00:11:12] Help me to understand a little bit more about what WebAssembly actually is, because does WebAssembly itself have byte code or some kind of language that you're, you're passing to? a runtime, like for example, an example I can think of is. the Java virtual machine where people can write many different types of languages, such as, I believe Clojure and Scala, they can write a language that generates Java byte code and is run by the Java virtual machine.

And so you can run those applications anywhere that you can run the Java virtual machine is WebAssembly similar? Is there a language for WebAssembly that is the target for say rust or C or different languages that you want to run in WebAssembly?

Taylor: [00:12:06] That's a really good question. It is similar in the sense that it does write code that then can be interpreted anywhere and there are various WASM runtimes. The reference implementation that we're using within the Krustlet project is called Wasmtime. And that's the one that's following the Waze spec, and is essentially the reference implementation for the WASI WASI specification.

And, that one can run on, on any of these systems that you've mentioned, and it has a byte code that it interprets in that way. And there's very, there's, there's a lot of technical details we could dive into there that I'm not a huge expert on, I know the basics, but there's some that are just like JIT compilers, right?

So just in time, there's some that are like, compiled at,  like a pre compilation step that can happen before. all of these things can happen but the thing is, is this is much more lightweight and small and constrained than the Java the JVM would be in this case. Right. So it's a, it's a much smaller and compressed use case, but it does have the similarity that it is byte code being interpreted by some sort of runtime.

Jeremy: [00:13:09] And, and this, this byte code, cause you've been talking about how there are different, I guess, implementations of the WebAssembly runtime. You, you gave a Wasmtime as an example of that. Does that mean that as long as you target, the WebAssembly bytecode that any of these different runtimes could run that code?

Is, is that how it works?

Taylor: [00:13:35] Yeah. And that's why the WASI specification is kind of the thing that's making it work on the server side rather than just in the web is because we need those specifications for how to interface with different things on the machine. and so there's also this other thing called interface types, which also defines like how you can interchange different data types in between different parts of applications.

To be clear. This is an area that's still under heavy development, for example, Wasmtime and WASI in general, hasn't even finalized their network specifications. So you have to kind of do work arounds and things to get net working in place. Now that's coming this, but like, this is very bleeding edge in that sense.

Jeremy: [00:14:17] And so this bike code can run in the browser in whatever WebAssembly runtime is built into the browser. And then it can also run outside the browser in a runtime, such as  Wasmtime. And it sounds like the, the distinction there is that. When you're running outside of the browser, you need some kind of consistent API to be able to access the file system, access network, things like that.

which would normally be handled by the browser, but once you take it outside of the browser, you need some common interface that knows how to make system calls to open a file on windows versus open a file on, on Linux. And that's what a runtime like Wasmtime would do by implementing what WASI describes is that sort of, did I get that right there?

Taylor: [00:15:10] Yeah, that's a, that's a great summary of how this works.

Jeremy: [00:15:14] Cool. so one of the questions that, I think people often have is when you work with languages like rust or, or go, they can be compiled ahead of time, you can get a binary that you can run directly on your operating system, for languages like those what are the benefits of using WebAssembly to run an application versus just using that binary?

Taylor: [00:15:42] It just depends on, I guess, the situation you're trying to do with it. Like there's certain tools, like the idea is what we have with, with WASM right now, isn't meant to replace Docker entirely, I think it opens up new cases for people who aren't,  who aren't like already into Docker or need to, or have some specific things.

But also this makes there, there's a certain amount of portability and security that comes from using WASM. obviously if you build a binary and then you build it for each system, you have the, the native things all built in all ready to go, which has a distinct advantage over some, like having to work through an interface, however, that security model is what gives us, a lot of hope for the future of this, because you have to explicitly grant permissions.

and it's a compile once. I don't have to compile my windows version. I don't have to. So you don't have to worry about cross compiling tool chains or the different VMs that you have to spin up to build one for ARM and for Mac and for Linux and for windows and you know, all those, all the different targets.

You don't have to worry about that with wasm you just build the, build the one binary and it's ready to go. it's also very, very small. If you do some, even without optimizations, you're talking like a meg or two megs for for a simple application. As opposed to a full binary, when, when you build it and rest binaries are fairly small, go, binaries are larger cause they've compiled in the runtime, but like rust, even though their binaries are small, this is even smaller. And if you strip it out, you can get it under a meg, depending on what it's doing. 

Now that size really matters with something like Kubernetes.

So if you start with a container and you pull down an image, some of those images, even if you're using like the very slim things are still. 20 30, 40 megs. Now that's not a big deal, but there's some of these bigger ones, especially when people are doing, some of the bigger applications are close to a gig.

Now that's not recommended. I know people say, but that's not a recommended practice. Yes. I know it's not. But in PRA and what actually happens in reality is people will do that. And so when you pull down, if you have a new version, even though they've cashed certain layers and things are the same, it's still takes a while to pull the new version and start it up.

Whereas WASM is just these tiny modules. And even if we haven't done something super big, but I'm guessing that even if it's only, even if it's huge, it's only a few megs. And so then you're, you're pulling this down and this is very quick and very fast. And the added security benefits on top of that, where you're not having to deal with the same security layers as what is available inside of a container, that, that, yeah, very explicit grants on your security surface.

Is a very powerful thing for us inside of Kubernetes on the server side.

Jeremy: [00:18:29] And that security piece is a little interesting, is that when you're building the WebAssembly application that you're explicitly building in this application will have permissions to the file system at these paths, or kind of what does that look like?

Taylor: [00:18:48] So it's not built in at compile time. Now there is one. when we get talking a little bit more about Krustlet, we have another implementation and there's one that, was started by capital one called wascc. which is WebAssembly, secure capabilities, connector. There's lots of W's here in this space.

And so this, this wascc runtime actually does things called capabilities where you can, explicitly you're actually supposed to explicitly say, I need this capability and I'm signed to have this capability, but WASM by default and the WASI spec, you grant it at runtime. You say, I'm going to give you access to this file, or I'm going to give you the permission to do this thing. So those things are done at the very beginning of your runtime, not when you're compiling it.

Jeremy: [00:19:33] Hmm. Interesting. And then, so that would be some kind of configuration file, maybe that would say, okay, when you run, this WASM application. Only give access to these permissions. And like you were saying before, that's much simpler than something like a Docker container where your permissions model is actually based off of a Linux operating system.

Taylor: [00:19:57] Yes. It's much simpler in that sense. I mean, you're still, there's, there's more overhead involved if you were to spinning this up completely manually, you have to say, okay. I need to give access to this directory and I need to give access to this thing, but Kubernetes kind of takes care of that for you.

And we do that inside of Krustlet with, with what we're doing to kind of abstract some of that away. So you don't have to do it. So, I mean, it's, it's like most security tradeoffs, right? Like the most secure thing is a server. That's not connected to the internet and is inside of a locked room, right? Like that's, and you can only access it in, in that room with a badge.

Like that's, that's like the most secure you can get, but that computer is kind of useless. so that's the idea behind, the, the security trade off is now you're just being explicit about what you're granting instead of just having all these implicit things of, Oh, I can access the network and I can access this thing and I can access this thing, which comes by default as running a process on a, on an operating system.

Jeremy: [00:20:50] When you were talking about being able to run the WASM application anywhere, that sounds like. benefit because normally when you have a build server, for, for example, an open source project, you'll see that they have to target all these different operating systems. They may have to build their application for, six or eight different OSS.

And in the case of using WebAssembly, they could just build it once and it would technically run on any of those. It sounds like. We've been talking about WebAssembly on the server. before we get into how Krustlet runs WASM applications, if I had a WASM application and I just wanted to run it on my machine, what does that look like?

Is there some kind of package manager or, how am I running these applications?

Taylor: [00:21:43] So there's a couple of different ways that these can be shared around. There's no, specific. implementation right now. the thing that we started with, with inside of Krustlet itself, as we use the OCI specification, which is the exact same thing that the containers use, it's just storing as a different artifact type.

Uh, there's some work by the people, working on WASC, they have something called gantry. and there's a couple other people who are looking into how you're supposed to store modules. So the idea behind all this, we have to figure out what exactly want to do. So it's kind of a little bit in the air.  we have a tool that was built by somebody on the team called WASM to OCI, and it does the work of pushing that to a container registry that supports Arbitrary artifacts. And so what you can do is take that and pull that down and it just pulls down the compiled module file.

It's always something.wasm, and then you can use whatever runtime you want to use to run it. So you can download wasmtime and install that you can down. You could do a there's Wasmer, there's Wasm3, which is for kind of optimized for embedded devices. Those are the kinds of things that, that you can do.

Just, you have to choose the runtime that you want to use. And then you have to grab the module from somewhere, wherever that might be right now, which is still, like I said, a little bit of a loosey goosey kind of thing.

Jeremy: [00:23:10] and, if I was just in the context of running an application on my computer without involving Kubernetes or anything like that, would it be where I get a single file? That's the WASM application. And then I pass that into say wasmtime or something like that, just at the command line. And that's how I would run it.

Taylor: [00:23:32] Yeah, that's exactly how it would work locally. Now, obviously we're, we're working on building us to make it even more fully featured. The ideal would be that then you can have an application that can be easily swapped across machines. I mean, imagine if you had something like notepad. Or some sort of editor and then you could do it there and then just take that same application and then have it somewhere else.

without worrying about what kind of system it is, you could have your raspberry PI 4 running a random desktop somewhere, and you could pass it over to a server and, do a virtual desktop session. Like you could do anything crazy that you wanted to by passing that around.

Jeremy: [00:24:09] cool. Yeah. I mean, it's, it's this idea of having a truly universal binary, I guess, having the ability to copy this application anywhere and run it without having to worry about, I guess basically anything you just need to have a wise and runtime.

Taylor: [00:24:26] Yeah. And that gives it some quite a bit of power. Right? Cause you could jump from an edge device. I'm using edge in the loosest possible term. Cause it could mean anything, but like any type of edge device, all the way to. I server I'm running in a data center. It can be anything along that whole spectrum of different servers that can run this, any can pass it around.

And it can, you can even start to think about how you could maybe hot swap it, right? Like you could point at one running implementation of it. And then when you don't have access to that, because you lose internet, you could point it at a local instance of how to run this.

Jeremy: [00:24:57] very cool.  now maybe we should go a little bit more into Krustlet. I know you've talked a little bit about what it is, but maybe you could go a little more into detail about what Krustlet is.

Taylor: [00:25:11] Yeah. So Krustlet stands for Kubernetes Rust kubelet. Lots of Ks. The main idea behind Krustlet was we wanted to create, we want it to reimplement the kubelet, which a kubelet is basically the, the binary that runs on a Kubernetes node that connects it to the cluster and runs it and joins. So that's, that's a kubelet and. we wanted to write it, write it so we could do WebAssembly. And now the reason we wrote it in rust was for a couple reasons. Number one, since you're probably listening to this because you like rust and you do rust, rust has probably the best WebAssembly support for, for server side things.

most languages at this point actually have WebAssembly support, but it's mostly geared towards the browser, but, WASI is something you can easily add in. It's actually, you just use rustup and do rustup component or rustup target add wasm32 dash WASI. And that's how simple it is to start compiling for WASI compatible WASM binaries in rust.

and so that is a, very powerful and useful tool to have around. If you can do it that easily. If you look at some of the other examples like C or C plus, plus you have to, customize clang properly or download the CA the already preconfigured tool chain and use that clang and then also you have a couple of other languages that support it, but rust was fully featured language that we could use it with, but also rust has caught our attention for a while, just because of its application inside of distributed systems and compute, like normally it's looked at as a systems engineering language, but can we use it in these cloud applications, this idea of cloud native as the buzz word right now? can it be used in a cloud native way? And so it was a secondary goal here was to prove that it could be, could be done like that.

Plus you add on all of the safety and security and, correctness features inside of rust. And it really helps us out. So we wrote several blog posts about that, that I can probably send around or, or link around if you send out show notes. but the main idea is that pre, it has prevented us from shooting ourselves in the foot.

Go has really easy concurrency things. There's sometimes that's one of the things that I most miss about using go for, for some of this is if I want to do concurrency. work. It's quite simple to set up, it's built into the language. It's very simple to do. But the thing is, is that there are bugs that we got caught where we'd sit there and be like, where everyone gets mad and like, why are you getting mad at me borrow checker, like, well, I've done everything. And then you're like, Oh, like it's caught that down the line. I'm going to, if I were to do this, I'd have two people trying to read the same data and that has been very useful and exciting for us because it's stopped us from doing those things. So the guarantee that when your rust code compiles, that it will be correct, even if it's not necessarily the right code, it's at least correct.

And you're not going to have weird database access issues. Inside of, of your code. And so that was the secondary reason that we found it was, it's just very powerful for doing that. And it also it's, it's expressiveness with traits and how generics work gave us a good deal of flexibility inside of Kubernetes.

having dealt with both extensively with both the. Kubernetes rust client and the Kubernetes go client, the Kubernetes rust client, it's much more ergonomic due to how traits work and generics. And so that was just something that we really enjoyed coming over. But it also, like I said, the main thing was that it had such good WASM support already built in and really most of the WASM runtimes are being written in rust right now.

So it makes sense for us to be in this space. So that's why this project was created. was to do is to have the ability to easily run, rust things inside or easily run WASM inside of Kubernetes. So that's, why we used rust and why we came up with Krustlet.

Jeremy: [00:29:07] Yeah, that makes a lot of sense because it had reminds me of, I had a conversation with a Armin Ronacher in an earlier episode and he works with century on  different debugging tools and things like that. And the reason why they chose to use rust in parts of Sentry is because there are a lot of existing tools or a lot of existing crates in Rust related to compilers or related to, reading debug files and things like that. And so in your case, the, the community had already done a lot of work in WebAssembly, and that's why it made sense to choose rust. So I think it's interesting how there's these certain niches that people have built up and, continue to cultivate and continue to bring additional projects in because of that, that base it's, it's very cool.

 You had mentioned a little bit earlier about how rust has really good support for WebAssembly. And so it's easy to get something up and running in WebAssembly using rust. but you had also mentioned with WASI that there are only certain features of the system that are implemented.

Like you had mentioned that there aren't network calls implemented yet. And I wonder when you're writing a rust application, do you have to do anything special when you're trying to target WASI, for example, if I were to make a network call in my rust application, and I try to compile it to be run in WebAssembly is the, the command line tool going to tell me you're trying to use an API that, that doesn't exist.

Like how does that part work?

Taylor: [00:30:52] that right now is a very rough edge. It just depends. I haven't tried to direct compile in with a network call yet, but. Most of the time, if you're doing something, that can't be compiled, the co the compiler will go in and say, like, I can't find a linked thing. Like when it's trying to link and do things, like, I can't find anything that links this together or that I'm able to compile this in and it'll spit out there.

And sometimes it's very obtuse. It just depends on what it is. This is, like I said, it's a very rough edge right now. because it is so new, when, when you are compiling, but for the most part, you actually write things the same way.  There's some things that you might need to pull in, to make sure that you don't, do something incorrectly or that you've had the correct things attached to the data structure or whatever it might be for the specific case.

There's actually some good examples inside of like wasmtime and a couple other places. But for the most part, you write code pretty much how you just normally would.

Jeremy: [00:31:45] so it sounds like currently, like you said, you pretty much write code as normal. You run it through the command line utility, and then you may get a helpful error message or you may get one that's really hard to decode and then you basically start digging around the internet, trying to find out, what might be wrong.

Taylor: [00:32:05] Yeah, that's kind of how it goes. Now. Luckily, people are very responsive to this, in, in the community. but we're working with them to, to work around this and there are possibilities of using networking. So, the wascc examples. That's one of the reasons we chose to use wascc is because it has networking support built in.

Now, the way it works is kind of just working around the problem. You have a capability that's built for the native system. And so if you're doing it on a, on a Mac there's, you can either load it from like a dylib file or like a, an object file of some kind, or you can have it compiled in, which is what we do in Krustlet.

And so when we build it for windows, It gets that compiled part for windows when we build it for, for Mac, it's going to have that compiled thing in there. And so like it's just working around it by creating a component of the system that is then linked by wascc to be able to talk forward calls around.

And so when something calls the networking thing, that call gets forwarded to the WebAssembly module, which handles it and passes it back out. There's not actual networking. Inside of the module itself. And so it works around it. It's a bit different of a model. It's an actual better model as opposed to, the wasmtime implementation and Crescent, which is more of a working like a standard container.

I use that term very, very loosely. It's more like I have a process I'm running that process as, for as long as it wanted to. And then it's done as opposed to responding to specific like action or actor calls that come in from a, from a host.

Jeremy: [00:33:38] so wasmtime and, and WASC are two, different WebAssembly run times. when you're talking about these processes running as actors, I guess, would that be. This would be a case where if you want to run a number of processes and you want them to communicate with one another, that's when you would choose wascc.

I'm trying to understand when you would use one runtime versus the other

Taylor: [00:34:04] Yeah. So right now, like if you were to go download Krustlet right now and try it, basically you have, if you were going to be using Wasmtime, the only way to communicate is by like data on files. Cause it can access files. So you could mount a shared volume and then like pass it off so it could do data processing, but it can't do communication very well until we get the, until WASI finalizes, how it's going to do networking.

if you want to do a full thing with WASC. So the thing with WASC is, you can use it entirely out of Kubernetes as its own thing. It's almost, it's, it's very similar to like a functions as a service kind of kind of tool. You write your things in whatever language, compile them to a WASM module. And then it handles connecting all those things together.

And the capabilities model around it gives it a security, an additional security layer that you have to, things are signed. So all your modules have to be signed. And then you have to, say that it has access to specific capability. So whether it can access another capability that another WebAssembly module is exposing or whatever, you can glue all these together so that you could pass calls around.

and it also has actually a, an ad hoc networking tool called lattice to connect multiple nodes together. So it can run entirely outside of Kubernetes. but it also has a bunch of tooling and things around it. So when you're going to do it, you're buying into that system and you have to know that that's what you're doing.

Wasmtime sometime is meant to be, like I said, following that same WASI specifications. So as soon as WASI gets networking and then we'll implement the networking stuff, just because we want to make sure that we have the more, like here's the vanilla option, how you glue it together. If you want more of this like quick functions kind of thing, then wascc is an amazing tool.

And so we implemented that because we've been, we've been collaborating with them for a long time. and so we've, we've had that implementation there so that it can be show another way wascc can be used while also helping people who want to try this right now and hack around to do things with networking.

Jeremy: [00:36:00] Does that mean there is some specific API call, I guess, that you're using within your WASC actors that allows it to communicate with the other actors. but it's not like general network calls. It's, it's a very constrained API. Is, is that right?

Taylor: [00:36:16] Yeah, there's an underlying thing called they call wapc yeah. WAPC so it's a WebAssembly protocol. I can't remember. Basically. It's a, it's the protobuf of the, this world.  it's a message protocol. Here's how I'm sending a message back and forth.

And so each actor is what it's called, is a WebAssembly module that can respond to specific events. And so it registers specific event handlers for those events. And when the, the underlying host that's running all these, gets it it dispatches those events to the actors and to, to run.

Jeremy: [00:36:49] and so if you were using that with Krustlet then, the, the way that the actors communicate with one another or communicate with the host, that would be configured automatically by Kruslet I guess, or, or what is the, 

Taylor: [00:37:04] To an extent.

Jeremy: [00:37:05] Okay.

Taylor: [00:37:06] That's why I was saying that it can be used more fully featured outside of the Kubernetes world. but it has a distinct place inside of Krustlet as well. And so Krustlet will do some of the configuration to a point like it makes sure all the capabilities and stuff are configured, but we're, for example, we're still trying to define, well, if somebody wants to add other capabilities, How do they define that?

Which normally you do, there's a freestyle block inside of a Kubernetes configuration called an annotation. So we're thinking, well, do we do it with an annotation or do we do it with another tool we don't know yet, but right now it does that base configuration link of it. It'll set up, make sure you have like an HTTP server access and that you have access to do logging and that you have access to do all those things.

It sets up for you. But we have to still define a way of what's the, what's a safe way for a user to say, I need this capability.

Jeremy: [00:37:56] When you've been developing Krustlet you've, you've mentioned how there's a lot of existing WebAssembly, capability in rust or projects, built in rust. are there other parts of the rust ecosystem or specific crates that, that helped you speed up your development a lot?

Taylor: [00:38:15] Yeah, there are, in terms of development tools, I have really loved, Cargo expand when they're doing some of the macro stuff. Async things do a lot of like additional, macro things that like build stuff out or, or wrap things in. So it's kind of nice to see that. I also learned about a bunch of different tools around how to debug stack overflow's because we were accidentally pinning some stuff too early and it was causing a stack overflow that we didn't discover until windows. because there's a smaller stack and so that, like, there were some really interesting things on the nightly compiler, like how to print, type sizes, that was really helpful in identifying things that could have gone wrong. and looking at like our other tools we've really enjoyed, the Kubernetes crate for it. It's called uh Kube. And that one has some really awesome, awesome tools in it, that are, very helpful. I think a lot of them are things that people have heard of ser serde, or sir, I can never, I feel like that's 

Jeremy: [00:39:17] Right.

Taylor: [00:39:17] that's a constant debate in the rust community.

Um,

Jeremy: [00:39:19] I, yeah, I thought it was Serde, but I don't know.

Taylor: [00:39:23] And I think it's Serde because it's serialize, deserialize, but anyway, yeah, so that's there, that we've used a lot of, and has been very helpful. obviously the tokio runtime has been helpful for us as well. But really like, it just depends. Like if there's not like any other crazy tools we've used outside of it, I do have to say a huge, a huge thanks to those who are, those who were working on, like the Kube crate and, and some of these other things we've, we've been able to contribute back as we found bugs, and other stuff.

I love the rust rust TLS crate as well, which has been very helpful for windows because then we don't have to have an open SSL dependency. and so that those are, those are the different things that have been, I guess, really helpful to us as I've like looked through and seen all the different things that we've done in our, in our code.

 Jeremy: [00:40:11] At the start of the episode, you mentioned you're relatively new to Rust, the languages you had used previously. would that be like go or what are some of the other languages you have a lot of experience with.

Taylor: [00:40:23] Yeah, I am a, re stationed by way of go. I've kind of like moved all over the place. so I've done a lot. I mean, I've done a lot of Python, like for glue code when I've done some more SRE work. I did node, back when it was starting to become a thing. Right. And then moved on to go, and then we have.

and then I've been doing some rust, since then, so yeah, it's just, I come from go, that's my main background before this was a lot of go because I was in the Kubernetes space, really heavily, well, I still am. And so that, that's where I got my go experience from. So that's my, that's my background where they're coming from go to rust is really the current thing that that's happened.

Jeremy: [00:40:59] And since you, you have experienced with go, I'm wondering, are there things that you miss from go either in the language itself, the runtime, or even just the ecosystem that you wish that rust had?

Taylor: [00:41:16] Yeah, there's a few things we've run into here. I overall, I am very pleased with, with, with the rust, and would choose it for a lot of different cloud projects, depending on what you're into. I think. Go, this is totally personal opinion here, but I think go is very well suited for smaller, like true microservices or anything.

Similar, very, very small constraints tools, because it's quick to get started. It has such a constraint vocabulary. And one of the things I appreciate particularly, and some people hate this and some people like it, but I like that generally there is a way to do something in in go. There's sometimes two, sometimes three, but most times there is a way to do it.

And when coming to Rust, there was 40 different ways to do the exact same thing. And so that was, that was something that I missed. The other thing I've said is that I really, I kind of mentioned, I said before that the concurrency story is much better in go and now it doesn't provide the same security or not security, correctness that.

Rust provides, but it's so much easier to get started and to spit things back and forth. And it's just been, as a relatively new rustacean, I kind of get frustrated by the fact that there are two, three async implementations.

Jeremy: [00:42:40] Tokyo,  async standard.

Taylor: [00:42:43] Yeah. Those are the two that I know. I think there was one more right?

Jeremy: [00:42:46] I think there's uh smol, I think it's how you say it.

Taylor: [00:42:49] Yeah, Smol

Jeremy: [00:42:50] I don't know.

Taylor: [00:42:50] It's supposed to be like a tiny yeah. But yeah, it's so, and I know that's a common complaint and people have done a lot of work on those, but it's very frustrating because you like get bought into that specific implementation and it's like,  let's choose one and make it part of the standard library, or make it the blessed crate or whatever it is just so we can all standardize and not have to like have weird hook ins to each run time and. all those those kinds of things, so that that's been fairly difficult to, to like work with sometimes, most of it's just otherwise like ergonomics.

I know that, we're going to be writing a blog post on this soon, but inside Krustlet we were, doing a state machine graph. It was more, it's kind of like a cross between like a traditional state machine and uh walking, a graph, that we were doing to be able to. Encapsulate the logic inside of, inside of Krustlet a little bit better.

Cause they were turning into monster functions that were just ridiculous. And because of that, we started to run into some of these things in go, you have the, you have their interfaces, right? And these interfaces, you can just keep calling through and chaining through, but because of how the, the type security that comes through, Through the trait system and things here in rust, it made a really difficult to find a way to just iterate.

And we finally found a way around it. It was a little bit, a little bit clunky and well like I said, we're going to write a blog post on it. Kind of explain everything, but there's just some of those things where the boundaries rust puts on you make some things very difficult to figure out, to make it work in a way that's both rusty, but also readable, to someone trying to write it.

that was one of those things. Like, I just see some of those rough edges sometimes that just, and I'm not sure if there's a way to solve that. That's that could just be me airing my grievances. But like, that's something that I miss. There's a little bit more flexibility that comes from the go model, with some of the things that we've, that we've run into here.

But like I said, I, I feel that that's worth it, given the security and things that we've gotten in return.

Jeremy: [00:44:49] so you mentioned one of the things with rust is that there's, there's so many different ways to do the same thing. And as you were learning the language, I wonder what was your approach to figuring out what is the ergonomic way to do things? And I guess just how to pick up rust in general.

Taylor: [00:45:09] all right. It was a combination of Clippy. And I mean, everybody loves Clippy. Some people get really mad at Clippy, but like Clippy at least tells me like, Oh, Hey, like, you're right, but this, you could do this more efficiently or you could avoid an extra allocation or you could do all those, those kinds of things.

learning to read the compiler messages. You get trained from like reading other compile. Like when other things fail, you look where the compile error failed, what line? And then you go there. Because normally it doesn't give you very much information, but with rust, you have to go through and read like, Oh, okay.

It's telling me this went out of scope here or was passed, passed here, and you need to go do this, or you need to go do this, or you need to go do this. all those things can be, can be very useful when you're reading a rust comp, like rest compiler error message. So those are the other things.

The other thing I had, and this is. I think one of the bottlenecks is that I had to go to an experienced rustacean who was working like a couple of experienced ones to go get the help. And there, that's what I love about the rust community. People are very willing to help. There's like the rust mentors page.

I know was mentioned at rust conf recently that I hadn't heard about. but the big problem is that that's still kind of a bottleneck. Whereas with other languages I've been able to find like at least semi clear examples of. This is a good way to do it, or this is how, this is how these things are handled.

I mean, an example of this is to string  (to_string) versus to owned (to_owned)  which technically they almost do the same thing when you're doing it with like, from, is there a proper name for ampersand string? Like just the, like the string slice, right. those things, the, to own versus to string.

Really what it turned into is there used to be a difference, but then there was now it's just clear. Like I just need this as a string, then I use two string. But if I'm using it in a case where I, I have one, but I need a cop an owned copy then I used to own  (to_owned) , even though they're I think they, at this point they call the same underlying logic.

And so learning those kinds of things I had to learn from people I didn't there wasn't like something could say, Hey, like here's the history of this? Or. even in the documentation, which rust's documentation of the functions is really good. It doesn't say like, you should use this here or here there there's no specific suggestions. And so, if there's one thing that I hope we can improve is maybe how we can document like the intermediate level cause getting started there's stuff, but then otherwise you're kind of bottlenecks at specific, like asking other rustaceans, Hey, how do I do this thing?

And that makes it a little bit harder for people.

Jeremy: [00:47:40] I'm not sure what the, what the solution for that is. Whether that's, like you said some other intermediate guide or, but then again, it's kind of like, How do you, determine what to put in there and how do people get directed to that versus the relationship you're talking about, where you're, you're talking to experienced people and they just have all that context in their head and they can tell you, it's a hard problem to solve for sure.

Taylor: [00:48:05] Well, yeah, and like I said, the compiler's fantastic. A lot of times you like learn from the compiler messages and that's how I finally learned that. Um when you give a static constraint on a trait that you're not saying it has to be static, it just has to fit into a static, which like, I was like mind blown moment right there.

And I was like, Oh, that's cool. Okay. I get it now. But before I'm like, I don't want to make this static. That's going to like bloat the size of this. And I like, I can't have this allocated on a stack. Like, this is huge, but it's like, no, It's just saying this needs to fit in a static. And I'm like, okay. And I learned that I think from a compiler, I could be wrong, but I think that the compiler said this doesn't fit in something or whatever.

And I'm like, wait a second. And I, and I dug into it and found it. So I think that a lot of the work that people discussed this at rustconf about making the compiler, just kind of guide you through things and anticipate it is quite impressive. And I'm very, very happy with that. So maybe that is that intermediate way that eventually get there.

But I'm just saying that I think that the there's some tooling there, but when people get in that, that learning curve is just a little bit, I like to describe it as logarithmic, right? Like it's just, you have that initial punch over the top.

And then once you understand that you can be quite capable of producing things quickly. 

Jeremy: [00:49:17] You were talking about some of the. Issues you ran into or roadblocks where you needed to get more intermediate help or talk to people more experienced. I wonder when you first started, how did you first start learning Rust?

Did you go through the, the breast programming book? Did you start making little small projects? I'm curious how you approach that.

Taylor: [00:49:42] Yeah, I did a combination of both. I tried to do some of the like rest by example, the rust book, just some of the basics. And then I tried implementing, I tried reimplementing some parts of, of, different projects that had in the past or things I just wanted to try.

And then I went on with trying to like actually implement in a real project, which was Krustlet. And you can see if you actually look at the Krustlet code, you can see where like, Oh, they must have been new there and we've been going through and cleaning that up as we go along. But having that real project and something I could like go towards, that's how I learn best.

It's just having like an actual goal of either reimplementing something or, Or, or finding like an actual project to go, like dig into. And that's how, that's how I work, but it's a little bit different for every person

Jeremy: [00:50:33] Was there a moment, I guess, where you felt like you were really struggling and then once you pass this point that, rust clicked for you or was it, did it feel pretty straightforward as you were going through the process?

Taylor: [00:50:47] it was a little bit gradual. more than like a specific moment where I was like, Oh, everything clicked. I do have those moments. Like I mentioned before, like when I understood what, like a static constraint on a trait means, like that was like, Oh, like mind blown. I finally get it. but it was more of a once I started like actually doing like more complex traits or trait bounds.

I think what I finally felt I was getting it was when I could do something like that. Where T equals this plus or T this plus this and, N is this plus this, like with the like long constraints at the end of a function and like understood what it was doing and why I did it that way. And I think also a combination of, of implementing some of the traits, like as ref, as mut ref those kinds of things that I could pull out or like convert, or have a wrapper type.

And I'm like, okay, I'm finally getting how all this glues together. that's when I that's, when I noticed, I think, okay, like I can, I can do this now. Like I can put together some, some cool things. but yeah, it comes, each thing comes with its own accomplishments. Like I had mentioned before, we had the state machine that we've just finished and we're cleaning up right now.

And that, that state machine thing was like, okay, like we finally got something that worked.  I think it's recently where I felt like, okay, I feel like I can actually be a good contributor to the community and maybe even start mentoring others properly because I have the knowledge to do it because now, now we create something new that as far as we can tell, like, people haven't done something like this in rust before, outside of just toy things.

And so like, we're, that's why I'm excited. I wish we had had like that today. So I could say, Oh, here's this blog post, but I'm really excited for that, because we're going to talk about like all the work we built on from people in the community who had posted about it and all these things in it. Okay. We managed to get something that works.

It's still like has rough edges. It still has things, but we've got something that works well for us. And so I, I that's, that's been fairly recent. And so I think there's just moments where like, I keep understanding more, but for me it was more of a gradual turning of like, Oh, and then all of a sudden I realized like, Oh no, I think I've gotten to the point where I know it, it wasn't like a click. Like I know what it is. Oh, I just realized I actually know what I'm doing now.

Jeremy: [00:52:56] Yeah. Yeah, no, that, that makes sense. You've been mentioning how Krustlet, has some rough edges.

And I know on the project page, it mentions how it's highly experimental. What do you think are the, the big parts that are, that are currently missing for somebody who would want to go in and actually host their application using Krustlet?

Taylor: [00:53:16] well, one of them is completely outside of working ends, which is networking, in Waze. we're, we're trying to work with the community to do that. And we're going to see if there's a way we can only solidify and jump in and work on that. but we're getting close. So, this is no one can hold us to this, but we're hoping to get towards a 1.0 Release towards the end of the year, beginning of next year.

and so like around the holiday season, things will slow down, whatever. So that's why we don't know it could be January, February, and that's what we're hoping for. And really the big things that we have are, we have basic volume support. but we don't have cloud volumes support. So we're going to be looking in a way of how we can make sure every provider can, can use this.

We're trying to solidify the API at the same time with that, because we have people who are writing other providers and a provider is just something that is an implementation of a runtime. And so we've written ours in for WASM, but we have another person who's a core maintainers, his name's Kevin.

and he's been, recently made a core maintainer of the project as well. And he's working on one for containers. so he's just moving the container implementation stuff over to rust because of all the security benefits and things. And so we need volume support for all the providers, and then we're going to try, and then we're going to figure out a way we can abstract the networking, probably using the same interfaces that Kubernetes has already defined, so that we can have networking implementations more, more readily available and connected into these things from, the rest of the Kubernetes world.

And then after that, we need to have like a real demos  like we have demos, but we need like some, like, I want, like, here's a real application as far in so far as you can make it real and take that and put together, some bootstrapping things. So it's easier for people to set it up. We want to make it as one click as possible to set it up.

And so. Those are kind of the things we're looking at and that people can, can look for rough edges. But if you want it for it, for example, if you want it to trigger like data pipeline processing, you can use just wascc or you can glue together wascc and a WASI provider, which is the wasmtime one. You can glue both of those together or have two of them running and you can trigger a data chain using an HTTP call and then process the data using one.

You can do that right now. we had, an intern on our team over the summer and she did some work with, on raspberry pies using a raspberry PI Kubernetes cluster, and then using Krustlet to read soil sensors. You can do some fun things with it. It's just not all the way there. And that's partially because of where things like this is, this is bleeding edge, and that's why we put like the big warning sign on the reading.

Like, like, please don't run this in production. Like you're you're this is so new. Not just the project itself, but also the technology around it. And so that's what those are kind of like the steps we have. So, at this point I would say, I maybe would remove the highly from Krustlet's description Hm I, if I was really wanting to, because now it's just, this is an experimental project.

That's kind of the goal for the future here, but we're not that far out from having something more it's a 1.0 where people can actually people can start using it in a real way and maybe not perfectly, but in a real way.

Jeremy: [00:56:27] Last year, Solomon, the CTO of Docker, he had tweeted that if WASI and WASM had existed in 2008, then they wouldn't have needed to create Docker. And I'm wondering from your perspective, thinking about the future of, WASM and Krustlet, do you think that.

Running applications in WASM could become the default for, for server side applications in the future.

Taylor: [00:56:59] It's a possibility. I wouldn't peg it entirely for sure. I, I think it will be a mix. People are just like getting on board with Kubernetes stuff and containers, which sometimes like, like I said, I think some people go way too. Far into it and don't think they just like, Oh, they hear Kubernetes and buzzword and want to do it.

But people are still just barely getting to that thing. So it'll be a long time if it does become the default. But I think it has the ability to, reach a very specific audience right now and have that grow. a lot of these constrained environments, like edge computing, you can't run Docker on there it's too much, too much overhead.

They just can't handle it. But you could run, WASM modules. it also allows you to pack things in more tightly because if everything's a small process, that's just this tiny little thing and tiny little binaries. You can run that with. we can run a lot more than you could with containers right now.

So I wouldn't say that it's going to, it's not a container killer, nor is that our current goal. Like we didn't, we didn't think that, like, we don't want to disparage that other technology. That's, that's something we still use a lot and effectively. but I, I do think that there is going to be some takeover of that space, at least in a small measure with all this stuff from wasm and WASI.

Because of its just portability and the ideal of we'd be closer to a write, write once compile, once and run anywhere kind of situation, people say it's a pipe dream. I think we'll never get completely there. Even with WASM, there's still constraints. There's still things that will be in place, but this makes it easier.

And having, if, if every language gets to the point where you can do it with rust, where you just say, here's my Wasi target and build it. That to me sounds like a very powerful way of doing it and not just for server side. I think that can reinvent a lot of things with normal applications as well. Just because of how portable they are and how then, applications could be tied to you instead of just like being tied to a computer or whatever it might be.

So there's some really interesting ideas here. It's just. There's those, those ones are a little bit further out, but I do think even in the short term, we'll start seeing some good applications where WASI will be WASI, compatible WASM, binaries will be a better choice than using a container.

Jeremy: [00:59:17] and it sounds like maybe in the short term you were talking about edge computing and that might be something like where you have a CDN, running application code. At their, their edge nodes, something like Cloudflare's workers or Fastly has an equivalent. are you thinking that might be where, where these things start?

Taylor: [00:59:39] I think that's where it's already started in one sense. And that's one of the reasons we chose Kubernetes is we think there's more beyond Kubernetes and server side on my team. That's that's our belief that we believe there's more to that, but everybody is getting into trying to do Kubernetes and have this Kubernetes has become an API layer that people understand that a lot of people use and enabling WASM through that API gives people a reason.

We want people to start using this and say, Hey, like, why doesn't my insert language of choice? Have the support for WASM. I like WASI binaries. Can we please get that? And then as people do that, we start getting more motion around it.

Jeremy: [01:00:19] I know when. I talk to people about WebAssembly a, sometimes what I'll hear is they'll say, well, I'm happy writing JavaScript in the browser. Why do I care about WebAssembly right. And so, like you say, if there are more use cases for running other than, just in the browser, then that might inspire other languages like Python or Ruby, or who knows what other languages too, to focus on getting them to work on WebAssembly. So I think that's, that's pretty exciting. so I think that's a good, good place to start wrapping up. if people want to learn more about Krustlet or, about what you're working on, where should they head?

Taylor: [01:01:00] I would definitely start with, the actual project site. So that's deislabs/krustlet on, github. there is also some, some posts that we have in various places. I wish there was like one amalgamation of all of this, but, you can look at the, it's deislabs.io/posts. I believe.

Let me just double check that.

Jeremy: [01:01:23] and we can probably get the krustlets specific, posts and then put those in the show notes as well.

Taylor: [01:01:28] Yeah, and I can send those, but yeah, it's deislabs.io/posts. that's posts for all of our projects, but you'll see some, at least three blog posts there about Krustlet. one was around our, our stack and heap allocation problems that we had and some lessons learned there. so those are, those are some other places you can go.

We have some other posts that hopefully we can send in the show notes that kind of give an overview of the different things that the reasoning behind this, if you're more interested at this from a high level, like a business perspective, we have a post for that we have some other things about the security things we got from it that we've posted around.

So, there's, there's lots of sources of information there, but if you really want to get started and look at the project and install it and try it out, go ahead and check out. deislabs/krustlet on get hub. And that one will have the docs and everything you need to get started.

Jeremy: [01:02:19] Very cool. Taylor, thank you so much for talking to me today. It's been interesting learning about Krustlet and WASM. Kubernetes and all of that. And I think it's going to be very interesting to see where it goes in the future.

Taylor: [01:02:33] Well, thank you very much for having me. And hopefully everyone finds at least some of this interesting and useful.

</div>