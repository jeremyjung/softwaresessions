+++
title = "Scott Hanselman on .NET"

description = "Scott Hanselman explains what .NET is, where it's used, why it has multiple runtimes, its intermediary language, and the many domains that use it"

[extra]
episode_url = "https://pinecast.com/listen/dc85e47d-037a-42c6-9f64-63bd8e83c0be.mp3"
social_title = "What's .NET?"
social_banner = "036-scott-hanselman.png"
social_description = "What .NET is and the many places it's used"
+++

Scott is the Community Program Manager for the .NET team at Microsoft and the host of the Hanselminutes podcast.

This episode originally aired on Software Engineering Radio.

Personal Links and Projects:
- [@shanselman](https://twitter.com/shanselman)
- [Hanselminutes](https://www.hanselminutes.com/)
- [Blog](https://www.hanselman.com/)
- [YouTube Channel](https://www.youtube.com/channel/UCL-fHOdarou-CR2XUmK48Og) 

Related Links:
- [.NET (How to get started)](https://dot.net)
- [What is .NET?](https://www.youtube.com/watch?v=bEfBfBQq7EE)
- [Common Language Runtime (CLR) Overview](https://docs.microsoft.com/en-us/dotnet/standard/clr)
- [NuGet (package manager)](https://www.nuget.org/)
- [Techempower Benchmarks (ASP.NET core)](https://www.techempower.com/benchmarks/#section=data-r19&hw=ph&test=composite)
- [Mono runtime (Cleanroom .NET implementation)](https://www.mono-project.com/)
- [Unity (Write games using C#)](https://unity.com/)
- [Xamarin (.NET Mobile apps)](https://dotnet.microsoft.com/apps/xamarin)
- [.NET nanoFramework (embedded devices / microcontrollers)](https://www.nanoframework.net/)
- [.NET foundation](https://dotnetfoundation.org/)
- [.NET interactive](https://www.hanselman.com/blog/announcing-net-interactive-try-net-includes-net-notebooks-and-more)
- [Blazor (Client web apps with .NET)](https://dotnet.microsoft.com/apps/aspnet/web-apps/blazor)
- [Single file deployment and executable](https://docs.microsoft.com/en-us/dotnet/core/deploying/single-file)
- [All About Span: Exploring a New .NET Mainstay](https://docs.microsoft.com/en-us/archive/msdn-magazine/2018/january/csharp-all-about-span-exploring-a-new-net-mainstay)
- [Virtual Desktop is what VR needs](https://hanselminutes.com/758/virtual-desktop-is-what-vr-needs-with-guy-godin)
- [SE Radio 394 Chris McCord on Phoenix LiveView](https://www.se-radio.net/2020/01/episode-394-chris-mccord-on-phoenix-liveview/)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

Jeremy: [00:00:00] Today I'm talking to Scott Hanselman. He's a partner program manager at Microsoft, the host of over 750 episodes of the Hanselminutes podcast. And he's got a YouTube channel. He's got a lot of interesting videos. one of the series I really enjoy is one called computer stuff they didn't teach you. You're all over the place. Scott, welcome to software engineering Radio.

Scott: [00:00:22] Thank you for having me. Yeah. I was an adjunct professor for a while and I realized that in all of my career choices and all of my volunteerism and outreach, it's just me trying to get back to teaching. So I just started a TikTok. So I'm like the old man on TikTok now. But it's turned out to be really great.

And I've got to engage with a bunch of people that I would never have found on any other social platform. So whether you find me on my podcast, my blog, which is almost 20 years old now, my YouTube or my TikTok or my Twitter, it's pretty much the same person. I'm a professional enthusiast, but that's all done in the spare time because my primary job is to own community for visual studio.

Jeremy: [00:01:02] That experience of being a teacher in so many ways is one of the big reasons why I wanted to have you on today, because I think in the videos and things you put out, you do a really good job of explaining concepts and just making them approachable. So I thought today we could talk a little bit about .NET and what that ecosystem is because I think there's a lot of people who they know .NET is a thing, they know it exists, but they don't really know what that means. So, maybe you could start with defining what is .NET?

Scott: [00:01:37] Sure, so Microsoft is historically not awesome at naming stuff. And, I joke about the idea that 20 years ago, Microsoft took over a top level domain, right? Thereby destroying my entire .org plan to take over the world. When they made the name .NET they were coming out of COM and C and C++ involved component object models.

And they had made a new runtime while Java was doing its thing in a new language and a new family of languages. And then they gave it a blanket name. So while, Java was one language on one runtime, which allowed us to get very clear and fairly understandable acronyms like JRE, Java, runtime, environment, and JDK... Microsoft came out of the gate with here's .NET and C# and VB and you know, COBOL.NET and this and that. And this is a multilanguage runtime. In fact, they called it a CLR, a common language runtime. So rather than saying here's C#, it's a thing. They said here's .NET. And it can run any one of N number of languages now.

The reality is that if you look over time, Java ended up being kind of a more generic runtime and people run all kinds of languages on the Java runtime. .NET now has C#, which I think is arguably first among equals as its language. Although we also have VB and F# as well as a number of niche languages, but the .NET larger envelope name as a marketing thing remains confusing. If they had just simply said, Hey, there's a thing called C# it probably would have cleared things up. So, yeah. Sorry. That was a bit of a long answer and it didn't actually get to the real answer. 

Jeremy: [00:03:24] So, I mean, you had mentioned how there was this runtime that C# runs on top of. Is that the same as the JVM? Like the Java virtual machine?

Scott: [00:03:36] Right. So as with any VM, whether it be V8 or the JVM, when you could take C# and you compile it, you compile it to an intermediate language. We call it IL. Java folks would call it a byte code and it's basically a process or non-specific assembler. For lack of another word. If you looked at the code, you would see things like, you know, load, you know, load four byte string into, you know, pseudo register type of stuff.

And, um, you would not be able to identify that this came from C#. It would just look like this kind of middle place between apples and apple juice. It's kind of apple sauce. It's pre chewed, but not all the way. And then what's interesting about C# is that when you compile it into a DLL, a dynamic link library or Linux which is like a shared object where you compile it into an executable.

The executable contains that IL, but the executable doesn't know the processor it's going to run on. That's super interesting, because that means then I could go over to an ARM processor or an Intel x86 or an x64 or whatever, an iPhone theoretically. And then there's that last moment. And then that jitter that just-in-time compiler goes and takes it the last mile, that local runtime, in this case, the CLR, the common language runtime takes that IL.

Chews it finally up into apple juice. And then does the processor specific optimizations that it needs to do. And this is an oversimplification because the, the pipeline is quite long and pretty exquisite. In fact, for example, if you're on varying levels of processor on varying versions of x64, or on an AMD versus on a, uh, an Intel machine.

There's all kinds of optimizations you can do as well as switches that we can do as developers and config files to give hints about a particular machine. Is this a server machine? Is this a client machine? Does it, is it memory constrained? Uh, does it have 64 processors? Can we prep this stuff both with a naive JIT a naive just-in-time compilation, or then over time, learn, literally learning over the runtime cycle of the process and go, you know, I bet we could optimize this better then swap out in while it's running a new implementation so we can actually do a multi-layered JIT. So here's the, I want to start my application fast and run this for loop.

You know, this for loop's been running for a couple of thousand milliseconds and it's kind of not awesome. I bet you, we can do better then we do a second pass. Swap out the function table, drop a new one in, and now we're going even faster. So our jitter, particularly a 64 bit jitter is really quite extraordinary in that respect.

Jeremy: [00:06:29] That's pretty interesting because I think a question that a lot of people might have is what's, what's the reason for having this intermediary language and not compiling straight to machine code. And what it sounds like, what you're saying is that, it can actually at runtime figure out like how can I run things more efficiently based on what's being executed in the program.

Scott: [00:06:50] Right. So when you are running a strongly typed language that has the benefits and the speed of drawing type language. and you also choose to compile it to a processor specific representation. We, we usually as developers and deployers think about things in terms of architectures like this is for an arm processor, but is this a raspberry PI, is it an Android device you really want to get down to the stepping individual versions of like an Intel?

For example, I'm talking to you right now on an Intel. But it's a desktop class processor. That was the first one released many, many years ago. It doesn't have the same instruction set as a modern i9 or a Xeon or something like that. So we have to be able to know what instruction sets are available and do the right thing.

And then if you add in things like, um, SIMD or doing, you know, data parallelization at the CPU level, If that's available, we might treat a vector of floats differently than we would on another thing. So how much information up front do we know about deployment and is it worth doing all that work on the developer's machine?

And this is the important part, which may not necessarily reflect the reality of where it's going to get deployed. You know, my desktop does not represent a machine in Azure or Heroku or AWS. So getting up to the point where we know as much as we can. And then letting the, the runtime environment, adapt to the true representation of what's happening on the, on the, on the final machine.

That doesn't mean that we can't go and do native compilation or what's called end gen or native image generation that if we know a whole lot, but, um, it provides a lot of value if we wait until the end.

Jeremy: [00:08:34] Yeah, that's an interesting point too, in that if we are compiling down to an intermediate language on our own development machines, then we don't have to worry about like, having all these different targets right. Of saying I'm going to build for this specific type of ARM processor you know, all these different places that our application could possibly go because the runtime has taken care of that for us.

Scott: [00:08:58] Right. And I think that's one of those things where it's taking care of it for us, unless we choose to, it reminds me of the time. Uh, if you remember, when we went from, you know, mostly manual shift cars to automatic shift cars, but people who bought fancy Audis and BMWs were like, you know, when I'm going to the shops to get groceries, I'm cool with automatic, but I really like the ability to downshift.

And then we started to see these hybrid cars that had, you know, D and R for drive in reverse and then a little move left and move right. To take control. And like, I'm going to tell the automatic transmission on this car that I really want to run at higher rpms. .NET tries to do that. It gives you both the ability to just say, you know, do what you're gonna do. I trust the defaults, but then a ton of switches, if you choose to really know about, uh, that, that ending environment.

Jeremy: [00:09:50] We've been talking about the common language runtime, which I believe you said is the equivalent of the Java virtual machine. You also mentioned how there are languages that are built to target the intermediate language that, that runtime uses like C# and VB and things like that. And you touched on this earlier before, but I feel like we haven't quite defined what .NET really is like, is it that runtime and so on?

Scott: [00:10:18] Okay. so .NET as an all encompassing marketing term, I would say is the ecosystem. Just as Java is a language and also an ecosystem. So when someone says, I know .NET, I would assume that they are at the very least familiar with C#. They know how to compile code and deploy code. They might be able to be a website maker, or they might be an iPhone developer.

That's where .NET starts getting complicated. Because it is an ecosystem. Someone could work. Let's say two people could work for 10 years in the ecosystem, and one could be entirely microservices and containers on the backend, in the cloud. And the other person could be Android and Unity and games and Xbox, and they are both .NET Developers, except they never touched each other's environment.

One is entirely a game and mobile app developer and the other one is entirely a backend developer. That's where it's harder now. I think the same thing is true in the Java world. Although I would argue that you'd be surprised how many places that you can find .NET, whether it be, in a Python notebook, you can run .NET And C# and an IPYMB in a notebook and Jupiter um, on, you know, on the Google cloud or you can run it on a microcontroller, not a microprocessor, but literally on a tiny 256 K micro controller, all of that is, is .NET. 

Now .NET is also somewhat unique, uh, amongst ecosystems in that it has a very large, what we call BCL the base class library. One of the examples might be that we know with a Python or with a JavaScript. You say console.log, hello world. We got the same thing. And then it's like, Hey, I need a really highly optimized, a vector of floats with a complicated math processing. Well, you have to go and figure out which one of those libraries you want to pull in. Right? There's lots of options in the Python world. There's lots of options in the Java world, the JavaScript world, but then you have to go hunting for the right library. You have to start thinking.

Microsoft, I think is somewhat more prescriptive in that our base class library, the stuff that's included by default has everything from regular expressions to math, to, you know, representations of memory all the way up to putting buttons on the screen.

So you don't always have to go out to the third party until it's, uh, it's time to get into higher level abstractions. And that has made .NET historically attractive to enterprises because when you're picking a framework, And it has a whole ton of ecosystem things. Who do you throttle when it doesn't work? Right? 

There's an old joke that people picked IBM because they got, it gave them one throat to choke. Uh, people who are in enterprises typically will buy a Microsoft thing and then they'll buy a support license and then they can call Microsoft when it is. Um, now fast forward for 20 years, Microsoft has a balance between a strong base class library and enrich open-source environment.

So it's a little bit more complicated, but the historical context behind why Microsoft ended up in enterprises is because of that base class library and all of those libraries that were available out of the box.

Jeremy: [00:13:20] And that's sort of in direct contrast to something like say JavaScript where people are used to going to the node package manager and getting a whole bunch of different dependencies that have been developed by other people. It sounds like with .NET, the philosophy is more that Microsoft is going to give you most of what you'll need and you can sort of stay in that environment.

Scott: [00:13:46] I would say that that was the original philosophy. I would say that that was pre open source Microsoft. So maybe 10 and 15 years ago. I would think that that is not a philosophy that is very conducive to a healthy, open source ecosystem. But it was early on when it was like, here's a thing you kind of buy, you didn't really buy it, but like it comes with windows and you buy visual studio.

When I joined about 13-14 years ago, myself and others are really pushing open source because we came from the open source community. And as we started introducing things like Azure and services .NET is free, has been free. Is now open source visual studio code, visual studio community are all free. So the stuff I work on, I actually have nothing to sell.

As such, um, it's better to have a healthy community. So we have things like NuGet so NuGet and N U G E T is the same as NPM is the same as Maven. It's our package manager environment. And that is, uh, allows you to pull both Microsoft libraries and third-party libraries. And we want to encourage an open source community that then, you know, pays open source framework, uh, creators for their work using things like github sponsors. 

People who are working in enterprises now need to understand that if you pick just the stuff that Microsoft gives you out of the box, you may be limited in the diversity of cool stuff that's happening. But if you go and start using open source technology, You might need to go and pay a support contract for those different tools or frameworks, depending on whether it's a, you know, a reimagination of ASP.NET or web framework.

And you say, I don't like the one Microsoft has. I'm going to use this one or an OAuth identity server that Microsoft does not ship out of the box. It's a missing piece. Therefore use this third party identity server.

Jeremy: [00:15:33] What are some things that you or Microsoft has done to encourage people to build open source stuff for .NET?

Scott: [00:15:43] Well, early on Microsoft was, uh, you know, attempted to open source .NET By creating a thing called rotor, R O T O R, which was a way of saying, Hey, Java, everyone in, in, in academia is using Java. We have one too, but. It didn't exist. The only real open source licenses at the time were GPL, so Microsoft made a very awkward, this is about 20 years ago, very awkward overture, where it's like, here's a zip file with a weird license that Microsoft made called the MSPL, the Microsoft permissive license.

And here's a kind of a neutered version of .NET That you could potentially use. And it wasn't source it wasn't open source. It was source opened. It's like, here's a zip file. Like, go, go play with this. There were no take backs. Fundamentally Microsoft was not a member of the open-source community. They were just like, Hey, look, we have one too.

When we started creating ASP.NET MVC, the model view controller stuff, which is kind of the Ruby on Rails for .NET. The decision was made by a bunch of folks on the team that I worked on and encouraged by me and others who think like me. Just open source the thing and do takebacks it's it's not just, Hey there's Hey, you can watch us write code and do nothing about it, but the takebacks is so important.

And the rise of GitHub and social coding enabled that even more. So now actually about 60% of .NET comes from outside Microsoft. It is truly collaborative. Now Microsoft used to patent a bunch of stuff and they'd patent stuff all over the place and everyone would be worried. I don't want to commit to this because it might be patented, but then they made the patent promise to say that any of the patents that covered .NET won't be things that will be enforced.

And then they donated .NET to the .NET foundation, which is a third party foundation, much like many other open source foundations and .NET and all of the things within it, the logos and the code and the copyrights are all owned by that. So if Microsoft, God forbid were to disappear or, uh, stop caring about .NET, it is the communities that can be built and deployed and run entirely outside of .NET. So it's overtures like that to try to make sure that people understand that this isn't going anywhere, it's truly open source and then take backs is such a big thing. And this has been going on now for, for many, many years, most people who think .NET and probably the folks that are listening to this show are thinking the big giant enterprise monolith that only runs on Windows that came out in the early 2000s.

Now it is a lightweight cross-platform open source framework that runs in containers and runs on Linuxes and raspberry pis. It's totally open and it's totally open source all the way down. The compilers, open source, all the libraries, everything.

Jeremy: [00:18:21] To your point of people, picturing .NET being closed source running only on windows. I think an important component to that is the fact that there have been multiple .NET runtimes right? There's been the framework there's been core. There's been mono. I wonder if you could elaborate a little bit on what each of those are and what role they fit in today.

Scott: [00:18:46] That is a very, very astute and important observation. So if I were to take Java byte code, Uh, I've taken Java source code and I've turned it into Java byte code. There are multiple Java runtimes, Java VMs that one could call upon it's from Oracle and there's Zeus and there's different open source, open JBMs and whatnot.

There are even interpreters. You can run that through a whole series of them. There's X. You can imagine a pie chart of all the different Java VMs that are available. Now. Certainly there's the 80% case, but there are lots of other ones. The same thing applied in the .NET ecosystem. There is the .NET framework that shipped and ships continually still with windows.

And the .NET framework and its associated CLR, I would say is a, and I'm putting my fingers in quotes here, a .NET. But to your point, there are multiple .NETs. Plural. Mono is a really interesting one because it is an open source, clean room reimplementation of the original Windows-based .NET and clean room in that they did not look at the source code.

They looked at the interface. So if I said to you, Jeremy, um, here's the interface for `System.String`, write me an implementation of this interface here are the unit tests and you wrote yourself Jeremy specific `System.String`. And it, it worked, it passed all the tests. Now, you know, who knows under load, it might behave differently.

But for the most part, you made a, a clean room reimplementation of that. Mono did that for all of .NET proper, but then that became a new .NET. So for those that are listening, they can't see us or see a screencast. But imagine that I go out to the command line and with a Microsoft implementation of .NET, I make a new console app.

It says `Console.WriteLine`. Then I compile it into an executable. I can then run that with Mono. So I created it on one environment and I ran it with another. So I, I did the compilation and the first, the first bit of chewing, and then the finally the jitter would run through mono because the IL language is itself a standard that has been submitted to the standards organizations.

And it is a thing. So if you and I were, uh, you know, advanced computer science students in university, that might be an interesting homework assignment, right? A IL you know, interpreter or write an IL jitter. And if you can successfully consume IL that has been created by one of these many .NETs you have passed the course. 

Then .NET core is a complete reimplementation opensource cross-platform with no specific ties to windows. And that's the .NET that has kind of, we're hoping will be rebranded just .NET. So five years from now, people won't think about .NET core .NET framework. They'll just think about .NET. 

It will run great on windows. It'll run great on Linux it'll run great right in the cloud, yada yada, yada. That is a kind of a third .NET. We're trying to unify all of those with the release of .NET 5, which just came out and .NET 5 we picked the number because it's greater than 4, which was the last version of .NET on windows.

But we also skipped a number because .NET Core 3. Would have been confusing if we named it .NET Core 4, again, Microsoft not being good at naming stuff. You imagine two lines heading to the right .NET framework and .NET core. They then converge into one .NET. The idea being to have one CLR, one common language runtime, one set of compilers and one base class library.

So that if someone were to learn that. If we harken back to the middle of the beginning of our conversation, when I said that there was a theoretical .NET developer out there, who's a gamer and there's another one who's doing backend work. They should be using the same libraries. They should be using the same languages.

They should have a familiarity with everything up to, but not including the implementation specific details of their systems, so that if a unity person or a, uh, decided to become a backend developer or a backend developer decides to move over to make iPhone games, they're going to say, Oh, This is all the system, dot this and that stuff I'm familiar with. That's a `System.String`. I appreciate that. As opposed to picking an iPhone or an Android specific implementation of a library.

Jeremy: [00:23:09] If .NET core is the open source reimplementation of the .NET Framework, and you've also got, you were talking about how mono is this clean room implementation of it? What role does, does mono play, currently?

Scott: [00:23:25] Hmm. Good question. So mano was originally created by, uh, Miguel de Icaza and the folks that were trying to actually make an outlook competitor on Linux that then turned into the Xamarin, uh, company X, A M A R I N and Xamarin, um, then was a different reimplementation, which allowed them to do interesting stuff like, can we take that IL and send it over to I'm doing a thing called SGEN, uh, and generating, you know, uh code that would run on an iPhone or code that we're running on an Android and they created a whole mobile ecosystem and then Microsoft bought them.

So then, because mono and .NET work on the same team we're getting together right now and we're actively merging those together. Now, originally mono was really well known that it was a just nice, solid, clean C code. You could basically clone the repo run configure run make, and it would build while the windows, implementation of .NET Core and .NET Core in general, wasn't super easy to build it.

Wasn't just a clone configure and make. A lot of work has been done to make the best parts of mono be the best parts of .NET core, as opposed to like disassembling one and, you know, taking them apart and making this frankenbuild, we want to make it so.net core is, is a, uh, a re-imagining of both original .NET framework and windows and the best of a cross platform one.

So that is currently in the process in that .NET 5 .NET 6 wave. So this year in, um, in November, we will release .NET 6, and that will also be an LTS or a long-term support release. So those of you who are familiar with Ubuntu's concept of LTS those long short term long-term support versions will have, you know, many years, three years plus of support.

And by then the mono .NET merge will kind of be complete. And then you'll find that .NET core will basically run everywhere that mono would. It doesn't mean mono as an ecosystem goes away. It just becomes another, uh, not the supported version of .NET, uh, at a runtime level.

Jeremy: [00:25:31] When we look at the Java virtual machine and we look at that ecosystem, there are languages like Scala and Clojure, things that were not made by the creator of the JVM. But are new languages that target that runtime.

And I wonder, from your perspective, why there was never that sort of community, with the common language runtime?

Scott: [00:25:56] I would think that because the interest from academia early on 20 years ago was primarily around Java. And Microsoft was slow on the uptake from an open source perspective that, um, slowed down possible implementations of other languages. And then .NET got so popular and C# evolved because C# is now on version nine, the C# that you wrote the idiomatic C# of 2001 is not the idiomatic C# with includes, you know, records and async and await and interesting things that have shown up on C# and then been borrowed by other languages, async await, being a great example, linq language, integrated query, being another thing that didn't exist, that language has evolved fast enough that people didn't feel that it was worth the effort. And it was really F# that picked an entirely different philosophy in the, in the functional way, by doing kind of an Ocaml style thing. And because C# and F# are so different from each other, they really fit nicely. They're as different as English and another language that isn't Latin-based, you know, And they meaning that they add flavor to the environment.

That doesn't mean that there aren't going to continue to be niche languages. Uh, but there was also things like IronRuby and IronPython, but they weren't really needed because the Python and Ruby runtimes already worked quite well.

Jeremy: [00:27:16] We've been talking about .NET and sort of the parts that, make up .NET, but I was wondering, other languages have niches, right? You have go maybe for more systems type programming or Python for machine learning. Are there niches for .NET?

Scott: [00:27:33] Oh, yeah. I mean, so when I would, I would, I would generally push back on the idea of niche though, because I don't want to use niche as a diminutive right. I kind of like the term domain specific just in the sense of you know, when in Finland speak Finnish, that doesn't mean that we would say, Hey, you know, Finnish didn't win.

Like we're not all speaking. It's not the, it's not the language. That one. But we don't want to think about things like that. There are great languages that exist for a reason because people want to do different stuff with them. So for example a really well thought of language in the .NET space is F# and F# is a functional language.

So for people who are familiar with OCaml and Haskell and things like that, and people who want to go and create a language that is, you know, very correct, very maintainable, very clear that has a real focus on you managing the problem domain. As opposed to the details of, of imperative programming. Um, it has immutable data structures by default.

There's a lot more type inference than there is in C#. Um, a lot of people use F# in the financial services industry. and it also has some interesting language features like records and discriminated unions, uh, that, uh, C# people are just now kind of getting hip to.

Jeremy: [00:28:47] What I typically see or what I think people sort of believe when they think of .NET is they think of enterprise applications. And I'm wondering if you, have some examples of things that are sort of beyond that space.

Scott: [00:29:03] Sure. So when I think of .NET, like in the past, I would think of like big windows apps with giant rows of tabs and text boxes over data. You know, if I go to my eye doctor and I see the giant weird application that he's running, that's multiple colors and lot of grids and stuff. And I think, Oh, that must be written in .NET.

Those are the applications of 20 years ago. The other thing that I think people think about when they think about .NET is it's a thing that is tied to windows and built on windows and probably takes about gigabytes of space. .NET core is meant to be more like node and more like go than it is to be like .NET Framework.

So for example, if I were to create a microservice using .NET core, I go out to the command line and I type `dotnet new`. Web or `dotnet new empty`, or `dotnet new console`. And then I can say `dotnet publish` and I can bring in a runtime. And we talked before about how you could keep things very non-specific until the last minute and let the runtime on the deployed machine decide.

Or you could say, you know, this is going to a raspberry PI, it's going to be a microservice on a raspberry PI. I want it to be as small as possible. So there's multiple steps. We've gone to, we made this little microservice and we published it. Then we publish all of the support, DLLs, the dynamic link libraries, the shared objects.

If it's going to Linux all of the native bindings that, that provide that binding between the runtime and, the native processor and the native operating system, all the system calls then that is right now, about 150, 180 megs on .NET. But then we look at the tree of function calls. And we say, you know, this is a micro service.

It only does like six things. It looks at the weather, it calls like six native functions. Then we do what's called tree trimming or tree shaking and we shake, we give it a good shake. And then we basically delete all of the functions that are never called. And we know those things, right. We can, we can introspect the code and we can shake this thing and we can get microservices down to 30, 40 megs.

Now again, you might say, well, compared to go or compared to writing that in C. Sure. But you're talking about still maintaining the jitter, the garbage collector, the strongly typed abilities of .NET. All of the great features of this cool environment shook, shaken, shaken, shaken down to, you know, 30, 40 megs.

And then you can pack that tightly into a container, even better if the container layer above it. And if you imagine a multi-stage Docker container, doesn't include the compiler. Doesn't include the SDK and the container above. It includes the runtime itself. You might only deploy, you know, 10, 15 megs.

You can really pack nicely together a .NET microservice and then a whole series of them. Thousands of them potentially into something like Kubernetes. That's a very fundamentally different thing than the giant .NET application that took two gigs on your hard drive. 

This is the cool part, though. A giant, we call it windows forms or that WPF, that windows presentation application that often we find in large enterprises moves slowly because the not, not run slowly, but move slowly from an, um, from a dev ops perspective because the enterprise is afraid to update it, or they need to wait for windows to get the version of .NET that they want because .NET has historically been tied to windows.

Which sucks then that application and the whole team behind it gets depressed. What if we could take the cool benefits that I just described around containers back port it, so that, that giant application at my doctor's office ships its own local copy of .NET, which it can then maintain, manage, and, and deal with it's it's on its own.

All in a local folder. Doesn't need to wait for windows. That's really cool. Then they could do that, that, that prejudging basically do a native image generation and even create a single executable where inside is .NET. So then I give you my doctor's office dot exe. You double click on it. You install nothing.

It simply unfolds like a flower into memory. Including all of the benefits. Now it's not generated native code at this point, right? It's .NET in an envelope that then blooms and then runs with all native dependencies that it needs. That is pretty cool. And that actually really generates excitement in the enterprises so that they can bring those older applications to, to modern techniques like dev ops and, uh, as well as a huge, huge perf speed up like two X, three X per speed up.

Jeremy: [00:33:47] When you talk about a perf speed up, why would including the, the .NET runtime with the application result in a perf speed up?

Scott: [00:33:55] It's not that we're including the, the, the .NET runtime that caused the perf speedup. It's that 20 years of improvement in jitter, 20 years of understanding the garbage collector, rather than using the .NET that shipped with windows, they can use the one that understands. Again, a callback to the beginning instruction sets that are newer and modern as SIMD, SSE2, all the different things that one could potentially exploit when on a newer system. Those things are we get huge numbers and actually .NET itself .NET 5 is 2 or 3x over .NET core three, which is 2 or 3x over. So a huge perf push has been happening and actually all the benchmarks are public. So if you go to techempower, the tech empower benchmarks, you can see that we're having a wonderfully fun kind of competition, a bit of a thumb war with, you know, the gos and the Java's and the, you know, groovy on rails of the world.

To the point where we're actually bumping up against the laws of physics. We can put out, you know, seven or 8 million requests a second. And then you notice that we all bundle at the top and .NET kind of moves within a couple of percentage of another one. And the reason is, is that we've saturated the network.

So without a 10 gigabit network, there's literally nothing, no more bytes can be pushed. So .NET is no longer in the middle or to the far right of the, uh, of the long tail of the curve. We're right up against anything else. And sometimes as fast as 10x, faster than things like node.

Jeremy: [00:35:23] So it sounds like going from the .net framework to .net core and rebuilding that, uh, you've been able to get these, giant speed improvements. You were giving the example of a windows desktop application and saying that, uh, you could take this that was built for the .net framework, um, and run it on .NET core.

I'm wondering, is that a case where somebody can just take their existing project, take their existing code and just choose to run it? Or is, does there have to be some kind of conversion process?

Scott: [00:35:56] So that's a great question. So it depends on if you're doing anything that is like super specific or weird. Like if you were. A weird application, then, then you might bump up against an edge case. The same thing, the same thinking applies. If you were trying to take an application cross-platform or example, I did a tiny mini virtual machine and an operating system for a advanced class in computer science.

15, 20 years ago, I was able. To take that application, which was written and compiled in .net 1.1 and move it to .NET core and run in a container and then run on a raspberry PI because it was completely abstract. It was using byte arrays and, and, and list of T and kind of pretty straightforward base class library stuff.

It didn't call the registry. It didn't call any windows APIs. So I was able to take a 15 year old app and move it in about a day. Another example, my blog, which used to run on .NET to my blog has over 19 years old now has recently been ported from .NET 2 to 4, then .NET core. And now .NET 5 runs in the cloud in Linux, in a container. With 80% of the code, the same, the stuff that isn't the same that I had to actually consciously work around with the help of my friend Mark Downey was, well, we called the registry. The registry is a windows thing. It doesn't exist. So what's the, you know, what's the implementation, is it a JSON file now? Is it an XML file? You know, when it runs in a container, it needs to talk to certain mapped file system things while before it was assuming. Okay. Back slashes or a C:. So implementation details need to move over. Another thing that is interesting to point out though, is that there are primitives, there are language and runtime primitives that didn't exist before that exists now.

And one of the most important one is a thing that's called span of T `Span<T>`. And this is the idea of a completely new way of thinking about. Arbitrary continuous bits of memory. Like you want to be at a high level language and then messing around in bite arrays. Or do you want to think about things at that higher level, but then also re avoid reallocation and copying of memory around.

So something very simple, like some HTTP headers come in, you know, if you're doing 7 million of these a second, this can add up right. And it's like, well, usually we take a look at that chunk of memory and we copy it into an array and then we start using higher level constructs to deal with that. Now I have a list of char and then we for loop around the list of char that's kind of gross.

And then you find out that you're in the garbage collector a lot because you're allocating memory and you're copying stuff around. You could take that older code, update it to you, use span of T and represent that contiguous region of arbitrary memory differently rather than an array, a span you can point to native memory or even memory managed on a staff back and then deal with stuff.

For example, parsing or maneuvering within HTTP header with no allocations. So a really great example, you'd ask for an example of an application that you couldn't believe. VR desktop. Are you familiar with VR desktop as it relates to the Oculus quest? Okay. So the Oculus quest is the Facebook VR thing, right?

And it's an Android phone on your face and it's, you can use it unplugged. And then people say, well, I got this Android phone on my face. I'd really like to plug it in with a USB cable and use the power of my desktop. But then I got to ship those bits across the USB and then have a client application that allows me to use it as a dumb client.

Okay. You would expect an application that someone would write to do that would be written in C or C++ or something really low level VR desktop allows you to actually see your windows desktop and ship those bits across the wire, across the literal wire, the USB or wirelessly is written entirely in C#. And you can use really smart memory allocation techniques. And the trick is don't allocate any memory and C# is more than fast enough to have less than 20 millisecond jitter on frames so that it is buttery smooth, even over wireless. And I did a whole podcast on that with the Guy Godin the Canadian, a gentleman who wrote VR desktop.

Jeremy: [00:40:23] That's really interesting because you're talking about areas where typically when you think of a managed language, like, C#, you're able to use it in more environments than you, you might normally think of.  And, I also kind of wonder, you have the new Apple machines coming out. They have their arm processors instead of the x86 processors. what is the state of.net when targeting an arm environment? Can somebody simply take that IL that's on one machine, bring it on to the arm machine and it just works?

Scott: [00:41:01] Yep. So if you are putting, if you're taking over the, the IL and I'm on a windows machine right now, I'm on an X64 machine, and I go, `dotnet new console`. And I go, `dotnet run` and it works on my X64 machine. And I say, `dotnet publish`. I can then take that, that library over to the raspberry PI or an arm machine say `dotnet run`.

And because I'm saying `dotnet run` with the local .NET runtime, it will pick up that IL and it will just run. So I have run using my now 19-20 year old blog. As an example, I have run that entire blog on a raspberry PI unchanged. Once I had worked out the portability issues, like once I had worked out the portability issues like back slashes versus forward slashes and assumptions like that.

So once the underlying syscalls line up, absolutely. And we actually announced in July of 2020 that we will support .NET core on the new Mac hardware. And  there are requirements for .NET and .NET core on, you know, Apple like arm 64 and big sur, that would be required to get that runtime working.

But yes, the goal would be to have native processes versus Rosetta to processes working. And that work is happening.

Jeremy: [00:42:24] We were talking about like the typical enterprise application, you've got a, windows forms application  is it possible for somebody with an application like that to, to target arm?

Scott: [00:42:36] So right now there is there's multiple layers. So the compiler yes. The runtime. Yes. The application. Yes. At the point where, if I were going to run on windows arm, like a surface pro X or something like that, we would need support for, I believe windows forms, winforms and WPF. I don't know that those are working right now, but those apps still run because just like we have the, the Rosetta, you know, Emulator can emulate x86 stuff.

So for example, paint.net is a great.net application that is basically Photoshop, but it's four bucks, um, that it runs entirely on .NET core and it runs just fine on a surface pro X in an emulated state. And I believe that the intent of course is to get everything running everywhere. So yeah, I would be sad if it didn't. That's a little outside my group, but the people that are working on that stuff. And by the way, the great thing about this go and look at the GitHub issues, right? So, you know, if you look on, I'm looking right now on a .net issue, 4879, where they're talking about the plan is supporting .NET core 3 and 5 on Rosetta 2 via emulation and .NET 6 supported in both native on ARM architecture and Rosetta two.

And there's in fact, a .NET runtime. A tracking issue. That's called support Apple Silicon, and they walk through where they're at current status on both mono and .NET six.

Jeremy: [00:44:00] very cool.

Scott: [00:44:01] Yeah, it is cool. It's cool. Because you get to like, actually see what we're doing, right? Like before you had to know somebody at Microsoft and then call your friend and be like, Hey, what's going on?

We are literally doing the work in, open on GitHub. So if the, if the tech journalist would pay more attention to the actual commits, they would get like scoops weeks before an a blog post came out because you're like, I just saw that, you know, the check-in for, you know, they had an Apple Silicon show up in the .NET but-da-da.

Jeremy: [00:44:26] Might get a little bit technical for the average journalist though. 

One of the things that you've been talking about is how with .NET Core, you have a lot of cross-platform capabilities. I wonder from an adoption standpoint, what you've seen, like are there people actually running their services and Linux and Docker, Kubernetes, that sort of thing.

Scott: [00:44:48] Yeah .NET. Um, one of the things that we try to make sure that it works everywhere. So we've seen huge numbers, not only on Azure, but AWS has a very burgeoning, uh, .NET Community, as well as their SDKs all work on .NET. Same with Google cloud. we're trying to be really friendly and supportive of anyone because I want it to run everywhere.

So for example, at our recent .NET conf, which is our little virtual conference that we make, we had Kelsey Hightower from Google cloud, like their main Google cloud Kubernetes person. Learn.net in a weekend, and then deploy to Kubernetes on Google cloud. We're seeing a huge uptick on .NET 5. So that unified version where we took.net core and the.net framework and unified them, it's the most quickly adopted .NET ever.

I mentioned before that like 60% of the, commits are coming from outside the community. We're seeing big numbers, you know, stack overflow is moving to dot has moved to .NET core. They're actually showing their perf. And most of the games that you run are already running on .NET. And, you know, if you see a unity game, there's .NET and C# running in that a lot of the mobile games that you're seeing, um, one of the other things that we're noticing is that more and more students and young people are getting involved.

Um, so we're really trying to put a lot of work into that. One of the other things that's kind of cool that we should talk about before the end is a thing called blazor. Have you heard about that?

Jeremy: [00:46:07] Yeah. Maybe you could explain it to our audience. 

Scott: [00:46:09] So just like, um, if we use Ruby on rails, as an example, I'd like to use other frameworks as an example, like builds cool stuff on top of it. So it's like you pick your Ruby, whether it be JRuby or, and Ruby or whatever. And then you've got your framework on top of that and then other frameworks, and then you layer on your layer and your layer.

.NET has this thing called ASP.NET active server pages. .NET. It's a stupid old name. You can make, web APIs that are JSON and XML based API APIs. You can make a standard model view controller type environments. You can do a thing called razor pages where you can basically mix and match C# and HTML.

But if you want to do those higher level, enterprise applications where you just don't want to learn Java script. We've actually taken the CLR and compiled it to web assembly and we can run the CLR inside V8. But then if you actually hit F12 tools on a blazor page, laser is bla Zed, O R hit F 12.

You go, and you hit a blazor page. You can see the DLLs, the actual dynamic link libraries coming over the wire. And then the intermediate language that we've been talking about so much on this podcast gets interpreted on the client side, which allows a whole new family of people. That already knows C#.

Like those individuals that we spoke to spoke about at the beginning, you've got someone with 10 years experience in unity and someone else got 10 years experience on the backend. I never got around to learning JavaScript. They can write C# they can target the browser. And then the browser itself runs.net and then blazor allows them to create spa applications, single page applications, much like, you know, Gmail and Twitter and in PWAs, progressive web apps.

So one could go and create an app. And rather than an electron kind of an app, which is using JavaScript and a whole host of tools, they can make a blazor app, have it run natively anywhere they can then pin it to their mobile phone or their taskbar on windows and they're there suddenly a web developer, and it's a really great environment for those big enterprise applications or those more line of business type apps, because the data binding is just so clean and then that backend can be anything.

So blazor is a really great environment and a pretty interesting technical achievement to get .NET itself running within the context of the browser.

Jeremy: [00:48:33] Does that mean that somehow you've been able to fit the .NET core runtime, in web assembly? I'm trying to understand how that works.

Scott: [00:48:40] Yep. That's exactly. That's exactly right. So remember how we mentioned before that this isn't the multi gigabyte thing that everyone is so afraid of, you basically bring down. I think it's like 15 or 20 megs, which is, you know, a little bit big, but if you think about the homepage of the verge, it's not that big, right.

I've seen PNGs bigger than the .net, uh, runtime. Uh, once you bring that down, of course, if you put that on a, on a CDN. that's handled. I think it's actually even smaller than that. It's not that big of a deal because once it's down, it's cached and that is really the .NET core, you know, mono runtime running within the context of WebAssembly and then you're just calling local browser things.

But here's the cool part. Let's say you don't like any of that, let's say I've described this whole thing. You like the application model. I want to write C#. But you don't want to download and like put a lot of work into getting the local CPU and the local V8 implementation to do that. You can actually not run the .NET framework and the .NET core rather, pardon me on the client side, but you can have it run on the server side and then you open a socket between the front end and the backend.

So then the events that occur. On the client side, get shuttled over web sockets to a stateful server. So there's blazor, which is client side, and then there's blazor server, which means it can run anywhere on any device. So then it's more of a programming model thing. You still don't have to write any JavaScript because you'll be addressing the Dom the document object model within the browser from the server side.

The messaging then goes magically over the web sockets. You basically, you have a persistent channel bus running between the front end and the back end. So you get to choose.

Jeremy: [00:50:28] yeah, we did a show on Phoenix live view, and it sounds like this is a very similar concept, except that you get the choice of having that run in the server or run locally in the client.

Scott: [00:50:40] Yeah. And I think the folks on Ruby on rails are doing similar kinds of things. It's this idea of, you know, bringing HTML back, maybe getting a little less JavaScript heavy, and really thinking about shoving around islands of marked markup. Right. If I have a pretty basic, you know, master detail page and I click on something and I just want to send back a card.

Is that really need to be a full blown react view? Angular application is the idea is you, you make a call to get some data, you ship the HTML back and you swap out a div. So it's trying to find a balance between, too much JavaScript and, uh, and too many post backs. And I think it, it hits a nice balance.

Blazor is seeing huge pickup, particularly in people who have found JavaScript to be somewhat daunting.

Jeremy: [00:51:27] I think we've been talking about things that are a little more cutting edge in terms of what's happening in the .NET ecosystem. Things like web assembly. what else are Microsoft's priorities for the future of .NET? 

Are you hoping to move into some more ahead of time compilation environments, For example, where you need something really small, that can run on IoT type devices. What's the future of .NET from your perspective?  

Scott: [00:51:57] All of the above. If you take a look at the microsoft .NET IOT, um, repository on github, we've got bindings for dozens and dozens and dozens of sensors and screens and things like that. We have partnerships with folks like PI top. So if you're teaching .NET, you can go in inside of your browser in a Jupiter kind of an environment, uh, go and, um, communicate with actual physical hardware and call GPIO general purpose IO directly. Uh, we're also partnering with folks like wilderness labs, which has a wonderful implementation of .NET Based on mono that allows you to write straight C# on a tiny micro processor, not a micro controller, pardon me uh, rather than a microprocessor and create, you know, commercial grade applications like, uh, you know, uh, uh, thermostat running in .NET, which again, takes those different people that I've mentioned before, who have familiarity with the ecosystem, but maybe not familiarity with the deployment and turns them into IOT developers.

So there's a huge group of people that are thinking about stuff like that. We've also seen 60 frames a second games being written in the browser using blazor. So we are finding that it is performant enough to go and do you know, we've seen, you know, gradients and different games like that. Being implemented using the canvas, uh, with blazor server running it's, uh, at its heart, the intent is for it to be kind of a great environment for everyone anywhere.

Um, and then if you go to the .NET website, which D O T.net dot.net, we can actually run it in the browser. And write the code and hit run so you can learn .NET without downloading anything. And then there's also some excitement around .NET interactive have notebooks, which allows you to use F# and C# in Jupiter notebooks and mix and match it with different languages.

You could have JavaScript, D3JS, some SVG visualizations, using C# all in the browser entirely in the, uh, in the Jupiter notebooks IPYMB ecosystem.

Jeremy: [00:54:00] So when you talk about, .NET Everywhere. It's really increasing the number of domains that you can use .NET at, and like be the person who maybe you built, uh, enterprise windows applications before, but now you're able to take those same skills and like you said, make a game or something like that.

Scott: [00:54:20] Exactly. It doesn't mean that you can't or shouldn't be a polyglot, but the idea is that there's this really great ecosystem that already exists. Why shouldn't those people be enabled to have fun anywhere?

I think that's a great note to end on. So for people who want to check out what you're up to, or learn more about .net, where should they head?  

Scott: [00:54:42] Well, they can find me just by Googling for Hanselman, Google, with being, if it makes you happy. Um, everything I've got is linked off of hanselman.com. And then if they're interested in learning more about .NET, they can go to just Google for .NET and you'll find dotnet.microsoft.com. Uh, within the download page, you'll see that we work on Mac, Linux, Docker, windows, and, um, if you already have visual studio code, just download the .NET SDK, go to the command line type `dotnet new console`, and open it up.

And visual studio code VS code will automatically get the extensions that you need and you can start playing around. Feel free to ask me any questions. We've got a whole community section of our website, whether it be stack overflow or Reddit or discord or code newbies or tick tock, we are there and we want to make you successful.

Jeremy: [00:55:29] Very cool. Well, Scott, thank you so much for chatting with me today.

Scott: [00:55:34] Thank you. I appreciate your very deep questions and you clearly did your research and I appreciate that.

</div>