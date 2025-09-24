+++
title = "Elizabeth Figura on Wine and Proton"

description = "Running Windows applications on other operating systems"

[extra]
episode_url = "https://pinecast.com/listen/ac0c2ba9-3fab-40a2-b1ab-8bc7bb6000c3.mp3"
social_title = "Elizabeth Figura on Wine and Proton"
social_description = "Running Windows applications on other operating systems"
+++

Elizabeth Figura is a Wine developer at Code Weavers.

We discuss how Wine and Proton make it possible to run Windows applications on other operating systems.

## Related links

- [WineHQ](https://www.winehq.org/)
- [Proton](https://github.com/ValveSoftware/Proton)
- [Crossover](https://www.codeweavers.com/crossover)
- [Direct3D](https://learn.microsoft.com/en-us/windows/win32/direct3d)
- [MoltenVK](https://github.com/KhronosGroup/MoltenVK)
- [XAudio2](https://learn.microsoft.com/en-us/windows/win32/xaudio2/xaudio2-introduction)
- [Mesa 3D Graphics Library](https://mesa3d.org/)

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

## Intro

[00:00:00] **Jeremy:** Today I am talking to Elizabeth Figuera. She's a wine developer at Code Weavers. And today we're gonna talk about what that is and, uh, all the work that goes into it. 

[00:00:09] **Elizabeth:** Thank you Jeremy. I'm glad to be here.


## What's Wine 

[00:00:13] **Jeremy:** I think the first thing we should talk about is maybe saying what Wine is because I think a lot of people aren't familiar with the project. 

[00:00:20] **Elizabeth:** So wine is a translation layer. in fact, I would say wine is a Windows emulator. That is what the name originally stood for. it re implements the entire windows. Or you say win 32 API. so that programs that make calls into the API, will then transfer that code to wine and and we allow that Windows programs to run on, things that are not windows. So Linux, Mac, os, other operating systems such as Solaris and BSD. it works not by emulating the CPU, but by re-implementing every API, basically from scratch and translating them to their equivalent or writing new code in case there is no, you know, equivalent.


## System Calls

[00:01:06] **Jeremy:** I believe what you're doing is you're emulating system calls. Could you explain what those are and, and how that relates to the project?

[00:01:15] **Elizabeth:** Yeah. so system call in general can be used, referred to a call into the operating system, to execute some functionality that's built into the operating system. often it's used in the context of talking to the kernel windows applications actually tend to talk at a much higher level, because there's so much, so much high level functionality built into Windows. When you think about, as opposed to other operating systems that we basically, we end up end implementing much higher level behavior than you would on Linux.

[00:01:49] **Jeremy:** And can you give some examples of what some of those system calls would be and, I suppose how they may be higher level than some of the Linux ones.

[00:01:57] **Elizabeth:** Sure. So of course you have like low level calls like interacting with a file system, you know, created file and read and write and such. you also have, uh, high level APIs who interact with a sound driver.

[00:02:12] **Elizabeth:** There's, uh, one I was working on earlier today, called XAudio where you, actually, you know, build this bank of of sounds. It's meant to be, played in a game and then you can position them in various 3D space. And the, and the operating system in a sense will, take care of all of the math that goes into making that work.

[00:02:36] **Elizabeth:** That's all running on your computer and. And then it'll send that audio data to the sound card once it's transformed it. So it sounds like it's coming from a certain space. a lot of other things like, you know, parsing XML is another big one. That there's a lot of things. The, there, the, the, the space is honestly huge

[00:02:59] **Jeremy:** And yeah, I can sort of see how those might be things you might not expect to be done by the operating system. Like you gave the example of 3D audio and XML parsing and I think XML parsing in, in particular, you would've thought that that would be something that would be handled by the, the standard library of whatever language the person was writing their application as.

[00:03:22] **Jeremy:** So that's interesting that it's built into the os.

[00:03:25] **Elizabeth:** Yeah. Well, and languages like, see it's not, it isn't even part of the standard library. It's higher level than that. It's, you have specific libraries that are widespread but not. Codified in a standard, but in Windows you, in Windows, they are part of the operating system. And in fact, there's several different, XML parsers in the operating system. Microsoft likes to deprecate old APIs and make new ones that do the same thing very often.

[00:03:53] **Jeremy:** And something I've heard about Windows is that they're typically very reluctant to break backwards compatibility. So you say they're deprecated, but do they typically keep all of them still in there? 

[00:04:04] **Elizabeth:** It all still It all still works.

[00:04:07] **Jeremy:** And that's all things that wine has to implement as well to make sure that the software works as well.

[00:04:14] **Jeremy:** Yeah.

[00:04:14] **Elizabeth:** Yeah. And, and we also, you know, need to make it work. we also need to implement those things to make old, programs work because there is, uh, a lot of demand, at least from, at least from people using wine for making, for getting some really old programs, working from the. Early nineties even.


## What people run with Wine (Productivity, build systems, servers)

[00:04:36] **Jeremy:** And that's probably a good, thing to talk about in terms of what, what are the types of software that, that people are trying to run with wine, and what operating system are they typically using?

[00:04:46] **Elizabeth:** Oh, in terms of software, literally all kinds, any software you can imagine that runs on Windows, people will try to run it on wine. So we're talking games, office software productivity, software accounting. people will run, build systems on wine, build their, just run, uh, build their programs using, on visual studio, running on wine. people will run wine on servers, for example, like software as a service kind of things where you don't even know that it's running on wine. really super domain specific stuff. Like I've run astronomy, software, and wine. Design, computer assisted design, even hardware drivers can sometimes work unwind. There's a bit of a gray area.


## How games are different

[00:05:29] **Jeremy:** Yeah, it's um, I think from. Maybe the general public, or at least from what I've seen, I think a lot of people's exposure to it is for playing games. is there something different about games versus all those other types of, productivity software and office software that, that makes supporting those different.

[00:05:53] **Elizabeth:** Um, there's some things about it that are different. Games of course have gotten a lot of publicity lately because there's been a huge push, largely from valve, but also some other companies to get. A lot of huge, wide range of games working well under wine. And that's really panned out in the, in a way, I think, I think we've largely succeeded.

[00:06:13] **Elizabeth:** We've made huge strides in the past several years. 5, 5, 10 years, I think. so when you talk about what makes games different, I think, one thing games tend to do is they have a very limited set of things they're working with and they often want to make things run fast, and so they're working very close to the me They're not, they're not gonna use an XML parser, for example.

[00:06:44] **Elizabeth:** They're just gonna talk directly as, directly to the graphics driver as they can. Right. And, and probably going to do all their own sound design. You know, I did talk about that XAudio library, but a lot of games will just talk directly as, directly to the sound driver as Windows Let some, so this is a often a blessing, honestly, because it means there's less we have to implement to make them work. when you look at a lot of productivity applications, and especially, the other thing that makes some productivity applications harder is, Microsoft makes 'em, and They like to, make a library, for use in this one program like Microsoft Office and then say, well, you know, other programs might use this as well. Let's. Put it in the operating system and expose it and write an API for it and everything. And maybe some other programs use it. mostly it's just office, but it means that office relies on a lot of things from the operating system that we all have to reimplement.

[00:07:44] **Jeremy:** Yeah, that's somewhat counterintuitive because when you think of games, you think of these really high performance things that that seem really complicated. But it sounds like from what you're saying, because they use the lower level primitives, they're actually easier in some ways to support.

[00:08:01] **Elizabeth:** Yeah, certainly in some ways, they, yeah, they'll do things like re-implement the heap allocator because the built-in heap allocator isn't fast enough for them. That's another good example.


## What makes some applications hard to support (Some are hard, can't debug other people's apps)

[00:08:16] **Jeremy:** You mentioned Microsoft's more modern, uh, office suites. I, I've noticed there's certain applications that, that aren't supported. Like, for example, I think the modern Adobe Creative Suite. What's the difference with software like that and does that also apply to the modern office suite, or is, or is that actually supported?

[00:08:39] **Elizabeth:** Well, in one case you have, things like Microsoft using their own APIs that I mentioned with Adobe. That applies less, I suppose, but I think to some degree, I think to some degree the answer is that some applications are just hard and there's, and, and there's no way around it. And, and we can only spend so much time on a hard application. I. Debugging things. Debugging things can get very hard with wine. Let's, let me like explain that for a minute because, Because normally when you think about debugging an application, you say, oh, I'm gonna open up my debugger, pop it in, uh, break at this point, see what like all the variables are, or they're not what I expect. Or maybe wait for it to crash and then get a back trace and see where it crashed. And why you can't do that with wine, because you don't have the application, you don't have the symbols, you don't have your debugging symbols. You don't know anything about the code you're running unless you take the time to disassemble and decompile and read through it. And that's difficult every time. It's not only difficult, every time I've, I've looked at a program and been like, I really need to just. I'm gonna just try and figure out what the program is doing.

[00:10:00] **Elizabeth:** It takes so much time and it is never worth it. And sometimes you have to, sometimes you have no other choice, but usually you end up, you ask to rely on seeing what calls it makes into the operating system and trying to guess which one of those is going wrong. Now, sometimes you'll get lucky and it'll crash in wine code, or sometimes it'll make a call into, a function that we don't implement yet, and we know, oh, we need to implement that function. But sometimes it does something, more obscure and we have to figure out, well, like all of these millions of calls it made, which one of them is, which one of them are we implementing incorrectly? So it's returning the wrong result or not doing something that it should. And, then you add onto that the. You know, all these sort of harder to debug things like memory errors that we could make. And it's, it can be very difficult and so sometimes some applications just suffer from those hard bugs. and sometimes it's also just a matter of not enough demand for something for us to spend a lot of time on it.

[00:11:11] **Elizabeth:** Right.

[00:11:14] **Jeremy:** Yeah, I can see how that would be really challenging because you're, like you were saying, you don't have the symbols, so you don't have the source code, so you don't know what any of this software you're supporting, how it was actually written. And you were saying that I. A lot of times, you know, there may be some behavior that's wrong or a crash, but it's not because wine crashed or there was an error in wine.

[00:11:42] **Jeremy:** so you just know the system calls it made, but you don't know which of the system calls didn't behave the way that the application expected.

[00:11:50] **Elizabeth:** Exactly.


## Test suite (Half the code is tests)

[00:11:52] **Jeremy:** I can see how that would be really challenging. and wine runs so many different applications. I'm, I'm kind of curious how do you even track what's working and what's not as you, you change wine because if you support thousands or tens thousands of applications, you know, how do you know when you've got a, a regression or not?

[00:12:15] **Elizabeth:** So, it's a great question. Um, probably over half of wine by like source code volume. I actually actually check what it is, but I think it's, i, I, I think it's probably over half is what we call is tests. And these tests serve two purposes. The one purpose is a regression test. And the other purpose is they're conformance tests that test, that test how, uh, an API behaves on windows and validates that we are behaving the same way. So we write all these tests, we run them on windows and you know, write the tests to check what the windows returns, and then we run 'em on wine and make sure that that matches. and we have just such a huge body of tests to make sure that, you know, we're not breaking anything. And that every, every, all the code that we, that we get into wine that looks like, wow, it's doing that really well. Nope, that's what Windows does. The test says so. So pretty much any code that we, any new code that we get, it has to have tests to validate, to, to demonstrate that it's doing the right thing.

[00:13:31] **Jeremy:** And so rather than testing against a specific application, seeing if it works, you're making a call to a Windows system call, seeing how it responds, and then making the same call within wine and just making sure they match.

[00:13:48] **Elizabeth:** Yes, exactly. And that is obviously, or that is a lot more, automatable, right? Because otherwise you have to manually, you know, there's all, these are all graphical applications.

[00:14:02] **Elizabeth:** You'd have to manually do the things and make sure they work. Um, but if you write automateable tests, you can just run them all and the machine will complain at you if it fails it continuous integration.


## How compatibility problems appear to users

[00:14:13] **Jeremy:** And because there's all these potential compatibility issues where maybe a certain call doesn't behave the way an application expects. What, what are the types of what that shows when someone's using software? I mean, I, I think you mentioned crashes, but I imagine there could be all sorts of other types of behavior.

[00:14:37] **Elizabeth:** Yes, very much so. basically anything, anything you can imagine again is, is what will happen. You can have, crashes are the easy ones because you know when and where it crashed and you can work backwards from there. but you can also get, it can, it could hang, it could not render, right? Like maybe render a black screen. for, you know, for games you could very frequently have, graphical glitches where maybe some objects won't render right? Or the entire screen will be read. Who knows? in a very bad case, you could even bring down your system and we usually say that's not wine's fault. That's the graphics library's fault. 'cause they're not supposed to do that, uh, no matter what we do. But, you know, sometimes we have to work around that anyway. but yeah, there's, there's been some very strange and idiosyncratic bugs out there too.

[00:15:33] **Jeremy:** Yeah. And like you mentioned that uh, there's so many different things that could have gone wrong that imagine's very difficult to find. Yeah. And when software runs through wine, I think,


## Performance is comparable to native

[00:15:49] **Jeremy:** A lot of our listeners will probably be familiar with running things in a virtual machine, and they know that there's a big performance impact from doing that.

[00:15:57] **Jeremy:** How does the performance of applications compare to running natively on the original Windows OS versus virtual machines?

[00:16:08] **Elizabeth:** So. In theory. and I, I haven't actually done this recently, so I can't speak too much to that, but in theory, the idea is it's a lot faster. so there, there, is a bit of a joke acronym to wine. wine is not an emulator, even though I started out by saying wine is an emulator, and it was originally called a Windows emulator. but what this basically means is wine is not a CPU emulator. It doesn't, when you think about emulators in a general sense, they're often, they're often emulators for specific CPUs, often older ones like, you know, the Commodore emulator or an Amiga emulator. but in this case, you have software that's written for an x86 CPU. And it's running on an x86 CPU by giving it the same instructions that it's giving on windows. It's just that when it says, now call this Windows function, it calls us instead. So that all should perform exactly the same. The only performance difference at that point is that all should perform exactly the same as opposed to a, virtual machine where you have to interpret the instructions and maybe translate them to a different instruction set. The only performance difference is going to be, in the functions that we are implementing themselves and we try to, we try to implement them to perform. As well, or almost as well as windows. There's always going to be a bit of a theoretical gap because we have to translate from say, one API to another, but we try to make that as little as possible. And in some cases, the operating system we're running on is, is just better than Windows and the libraries we're using are better than Windows.

[00:18:01] **Elizabeth:** And so our games will run faster, for example. sometimes we can, sometimes we can, do a better job than Windows at implementing something that's, that's under our purview. there there are some games that do actually run a little bit faster in wine than they do on Windows.

[00:18:22] **Jeremy:** Yeah, that, that reminds me of how there's these uh, gaming handhelds out now, and some of the same ones, they have a, they either let you install Linux or install windows, or they just come with a pre-installed, and I believe what I've read is that oftentimes running the same game on both operating systems, running the same game on Linux, the battery life is better and sometimes even the performance is better with these handhelds.

[00:18:53] **Jeremy:** So it's, it's really interesting that that can even be the case.

[00:18:57] **Elizabeth:** Yeah, it's really a testament to the huge amount of work that's gone into that, both on the wine side and on the, side of the graphics team and the colonel team. And, and of course, you know, the years of, the years of, work that's gone into Linux, even before these gaming handhelds were, were even under consideration.


## Proton and Valve Software's role

[00:19:21] **Jeremy:** And something. So for people who are familiar with the handhelds, like the steam deck, they may have heard of proton. Uh, I wonder if you can explain what proton is and how it relates to wine.

[00:19:37] **Elizabeth:** Yeah. So, proton is basically, how do I describe this? So, proton is a sort of a fork, uh, although we try to avoid the term fork. It's a, we say it's a downstream distribution because we contribute back up to wine. so it is a, it is, it is a alternate distribution fork of wine. And it's also some code that basically glues wine into, an embedding application originally intended for steam, and developed for valve. it has also been used in, others, but it has also been used in other software. it, so where proton differs from wine besides the glue part is it has some, it has some extra hacks in it for bugs that are hard to fix and easy to hack around as some quick hacks for, making games work now that are like in the process of going upstream to wine and getting their code quality improved and going through review.

[00:20:54] **Elizabeth:** But we want the game to work now, when we distribute it. So that'll, that'll go into proton immediately. And then once we have, once the patch makes it upstream, we replace it with the version of the patch from upstream. there's other things to make it interact nicely with steam and so on. And yeah, I think, yeah, I think that's, I got it.

[00:21:19] **Jeremy:** Yeah. And I think for people who aren't familiar, steam is like this, um, I, I don't even know what you call it, like a gaming store and a 

[00:21:29] **Elizabeth:** store game distribution service. it's got a huge variety of games on it, and you just publish. And, and it's a great way for publishers to interact with their, you know, with a wider gaming community, uh, after it, just after paying a cut to valve of their profits, they can reach a lot of people that way. And because all these games are on team and, valve wants them to work well on, on their handheld, they contracted us to basically take their entire catalog, which is huge, enormous. And trying and just step by step. Fix every game and make them all work.

[00:22:10] **Jeremy:** So, um, and I guess for people who aren't familiar Valve, uh, softwares the company that runs steam, and so it sounds like they've asked, uh, your company to, to help improve the compatibility of their catalog.

[00:22:24] **Elizabeth:** Yes. valve contracted us and, and again, when you're talking about wine using lower level libraries, they've also contracted a lot of other people outside of wine. Basically, the entire stack has had a tremendous, tremendous investment by valve software to make gaming on Linux work. Well.


## The entire stack receives changes to improve Wine compatibility

[00:22:48] **Jeremy:** And when you refer to the entire stack, like what are some, some of those pieces, at least at a high level.

[00:22:54] **Elizabeth:** I, I would, let's see, let me think. There is the wine project, the. Mesa Graphics Libraries. that's a, that's another, you know, uh, open source, software project that existed, has existed for a long time. But Valve has put a lot of, uh, funding and effort into it, the Linux kernel in various different ways.

[00:23:17] **Elizabeth:** the, the desktop, uh, environment and Window Manager for, um, are also things they've invested in.

[00:23:26] **Jeremy:** yeah. Everything that the game needs, on any level and, and that the, and that the operating system of the handheld device needs.


## Wine's history

[00:23:37] **Jeremy:** And wine's been going on for quite a while. I think it's over a decade, right?

[00:23:44] **Elizabeth:** I believe. Oh, more than, oh, far more than a decade. I believe it started in 1990, I wanna say about 1995, mid nineties. I'm, I probably have that date wrong. I believe Wine started about the mid nineties.

[00:24:00] **Jeremy:** Mm.

[00:24:00] **Elizabeth:** it's going on for three decades at this rate.

[00:24:03] **Jeremy:** Wow. Okay.

[00:24:06] **Jeremy:** And so all this time, how has the, the project sort of sustained itself? Like who's been involved and how has it been able to keep going this long?

[00:24:18] **Elizabeth:** Uh, I think as is the case with a lot of free software, it just, it just keeps trudging along. There's been. There's been times where there's a lot of interest in wine. There's been times where there's less, and we are fortunate to be in a time where there's a lot of interest in it. we've had the same maintainer for almost this entire, almost this entire existence. Uh, Alexander Julliard, there was one person starting who started, maintained it before him and, uh, left it maintainer ship to him after a year or two. Uh, Bob Amstat. And there has been a few, there's been a few developers who have been around for a very long time. a lot of developers who have been around for a decent amount of time, but not for the entire duration. And then a very, very large number of people who come and submit a one-off fix for their individual application that they want to make work.

[00:25:19] **Jeremy:** How does crossover relate to the wine project? Like, it sounds like you had mentioned Valve software hired you for subcontract work, but crossover itself has been around for quite a while. So how, how has that been connected to the wine project?

[00:25:37] **Elizabeth:** So I work for, so the, so the company I work for is Code Weavers and, crossover is our flagship software. so Code Weavers is a couple different things. We have a sort of a porting service where companies will come to us and say, can we port my application usually to Mac? And then we also have a retail service where Where we basically have our own, similar to Proton, but you know, older, but the same idea where we will add some hacks into it for very difficult to solve bugs and we have a, a nice graphical interface. And then, the other thing that we're selling with crossover is support. So if you, you know, try to run a certain application and you buy crossover, you can submit a ticket saying this doesn't work and we now have a financial incentive to fix it. You know, we'll try to, we'll try to fix your, we'll spend company resources to fix your bug, right? So that's been so, so code we v has been around since 1996 and crossover, I don't know the date, but it's crossover has been around for probably about two decades, if I'm not mistaken.

[00:27:01] **Jeremy:** And when you mention helping companies port their software to, for example, MacOS.

[00:27:07] **Jeremy:** Is the approach that you would port it natively to MacOS APIs or is it that you would help them get it running using wine on MacOS?

[00:27:21] **Elizabeth:** Right. That's, so that's basically what makes us so unique among porting companies is that instead of rewriting their software, we just, we just basically stick it inside of crossover and, uh, and, and make it run.

[00:27:36] **Elizabeth:** And the idea has always been, you know, the more we implement, the more we get correct, the, the more applications will, you know, work. And sometimes it works out that way. Sometimes not really so much. And there's always work we have to do to get any given application to work, but. Yeah, so it's, it's very unusual because we don't ask companies for any of their code. We don't need it. We just fix the windows API

[00:28:07] **Jeremy:** And, and so in that case, the ports would be let's say someone sells a MacOS version of their software. They would bundle crossover, uh, with their software.

[00:28:18] **Elizabeth:** Right? And usually when you do this, it doesn't look like there's crossover there. Like it just looks like this software is native, but there is soft, there is crossover under the hood.


## Loading executables and linked libraries

[00:28:32] **Jeremy:** And so earlier we were talking about how you're basically intercepting the system calls that these binaries are making, whether that's the executable or the, the DLLs from Windows. Um, but I think probably a lot of our listeners are not really sure how that's done. Like they, they may have built software, but they don't know, how do I basically hijack, the system calls that this application is making.

[00:29:01] **Jeremy:** So maybe you could talk a little bit about how that works.

[00:29:04] **Elizabeth:** So there, so there's a couple steps to go into it. when you think about a program that's say, that's a big, a big file that's got all the machine code in it, and then it's got stuff at the beginning saying, here's how the program works and here's where in the file the processor should start running. that's, that's your EXE file. And then in your DLL files are libraries that contain shared code and you have like a similar sort of file. It says, here's the entry point. That runs this function, this, you know, this pars XML function or whatever have you.

[00:29:42] **Elizabeth:** And here's this entry point that has the generate XML function and so on and so forth. And, and, then the operating system will basically take the EXE file and see all the bits in it. Say I want to call the pars XML function. It'll load that DLL and hook it up. So it, so the processor ends up just seeing jump directly to this pars XML function and then run that and then return and so on.

[00:30:14] **Elizabeth:** And so what wine does, is it part of wine? That's part of wine is a library, is that, you know, the implementing that parse XML and read XML function, but part of it is the loader, which is the part of the operating system that hooks everything together. And when we load, we. Redirect to our libraries. We don't have Windows libraries.

[00:30:38] **Elizabeth:** We like, we redirect to ours and then we run our code. And then when you jump back to the program and yeah.

[00:30:48] **Jeremy:** So it's the, the loader that's a part of wine. That's actually, I'm not sure if running the executable is the right term.

[00:30:58] **Elizabeth:** no, I think that's, I think that's a good term. It's, it's, it's, it starts in a loader and then we say, okay, now run the, run the machine code and it's executable and then it runs and it jumps between our libraries and back and so on.

[00:31:14] **Jeremy:** And like you were saying before, often times when it's trying to make a system call, it ends up being handled by a function that you've written in wine. And then that in turn will call the, the Linux system calls or the MacOS system calls to try and accomplish the, the same result.

[00:31:36] **Elizabeth:** Right, exactly.

[00:31:40] **Jeremy:** And something that I think maybe not everyone is familiar with is there's this concept of user space versus kernel space. you explain what the difference is?

[00:31:51] **Elizabeth:** So the way I would explain, the way I would describe a kernel is it's the part of the operating system that can do anything, right? So any program, any code that runs on your computer is talking to the processor, and the processor has to be able to do anything the computer can do.

[00:32:10] **Elizabeth:** It has to be able to talk to the hardware, it has to set up the memory space. That, so actually a very complicated task has to be able to switch to another task. and, and, and, and basically talk to another program and. You have to have something there that can do everything, but you don't want any program to be able to do everything. Um, not since the, not since the nineties. It's about when we realized that we can't do that. so the kernel is a part that can do everything. And when you need to do something that requires those, those permissions that you can't give everyone, you have to talk to the colonel and ask it, Hey, can you do this for me please? And in a very restricted way where it's only the safe things you can do. And a degree, it's also like a library, right? It's the kernel. The kernels have always existed, and since they've always just been the core standard library of the computer that does the, that does the things like read and write files, which are very, very complicated tasks under the hood, but look very simple because all you say is write this file. And talk to the hardware and abstract away all the difference between different drivers. So the kernel is doing all of these things. So because the kernel is a part that can do everything and because when you think about the kernel, it is basically one program that is always running on your computer, but it's only one program. So when a user calls the kernel, you are switching from one program to another and you're doing a lot of complicated things as part of this. You're switching to the higher privilege level where you can do anything and you're switching the state from one program to another. And so it's a it. So this is what we mean when we talk about user space, where you're running like a normal program and kernel space where you've suddenly switched into the kernel.

[00:34:19] **Elizabeth:** Now you're executing with increased privileges in a different. idea of the process space and increased responsibility and so on.

[00:34:30] **Jeremy:** And, and so do most applications. When you were talking about the system calls for handling 3D audio or parsing XML. Are those considered, are those system calls considered part of user space and then those things call the kernel space on your behalf, or how, how would you describe that?

[00:34:50] **Elizabeth:** So most, so when you look at Windows, most of most of the Windows library, the vast, vast majority of it is all user space. most of these libraries that we implement never leave user space. They never need to call into the kernel. there's the, there only the core low level stuff. Things like, we need to read a file, that's a kernel call. when you need to sleep and wait for some seconds, that's a kernel. Need to talk to a different process. Things that interact with different processes in general. not just allocate memory, but allocate a page of memory, like a, from the memory manager and then that gets sub allocated by the heap allocator. so things like that. 

[00:35:31] **Jeremy:** Yeah, so if I was writing an application and I needed to open a file, for example, does, does that mean that I would have to communicate with the kernel to, to read that file?

[00:35:43] **Elizabeth:** Right, exactly.

[00:35:46] **Jeremy:** And so most applications, it sounds like it's gonna be a mixture. You're gonna have a lot of things that call user space calls. And then a few, you mentioned more low level ones that are gonna require you to communicate with the kernel.

[00:36:00] **Elizabeth:** Yeah, basically. And it's worth noting that in, in all operating systems, you're, you're almost always gonna be calling a user space library. That might just be a thin wrapper over the kernel call. It might, it's gonna do like just a little bit of work in end call the kernel. 

[00:36:19] **Jeremy:** 

[00:36:19] **Elizabeth:** In fact, in Windows, that's the only way to do it. Uh, in many other operating systems, you can actually say, you can actually tell the processor to make the kernel call. There is a special instruction that does this and just, and it'll go directly to the kernel, and there's a defined interface for this. But in Windows, that interface is not defined. It's not stable. Or backwards compatible like the rest of Windows is. So even if you wanted to use it, you couldn't. and you basically have to call into the high level libraries or low level libraries, as it were, that, that tell you that create a file. And those don't do a lot.

[00:37:00] **Elizabeth:** They just kind of tweak their parameters a little and then pass them right down to the kernel.

[00:37:07] **Jeremy:** And so wine, it sounds like it needs to implement both the user space calls of windows, but then also the, the kernel, calls as well. But, but wine itself does that, is that only in Linux user space or MacOS user space?

[00:37:27] **Elizabeth:** Yes. This is a very tricky thing. but all of wine, basically all of what is wine runs in, in user space and we use. Kernel calls that are already there to talk to the colonel, to talk to the host Colonel. You have to, and you, you get, you get, you get the sort of second nature of thinking about the Windows, user space and kernel.

[00:37:50] **Elizabeth:** And then there's a host user space and Kernel and wine is running all in user, in the user, in the host user space, but it's emulating the Windows kernel. In fact, one of the weirdest, trickiest parts is I mentioned that you can run some drivers in wine. And those drivers actually, they actually are, they think they're running in the Windows kernel. which in a sense works the same way. It has libraries that it can load, and those drivers are basically libraries and they're making, kernel calls and they're, they're making calls into the kernel library that does some very, very low level tasks that. You're normally only supposed to be able to do in a kernel. And, you know, because the kernel requires some privileges, we kind of pretend we have them. And in many cases, you're even the drivers are using abstractions. We can just implement those abstractions kind of over the slightly higher level abstractions that exist in user space.

[00:39:00] **Jeremy:** Yeah, I hadn't even considered the being able to use hardware devices, but I, I suppose if in, in the end, if you're reproducing the kernel, then whether you're running software or you're talking to a hardware device, as long as you implement the calls correctly, then I, I suppose it works.

[00:39:18] **Elizabeth:** Cause you're, you're talking about device, like maybe it's some kind of USB device that has drivers for Windows, but it doesn't for, for Linux. 

[00:39:28] **Elizabeth:** no, that's exactly, that's a, that's kind of the, the example I've used. Uh, I think there is, I think I. My, one of my best success stories was, uh, drivers for a graphing calculator.

[00:39:41] **Jeremy:** Oh, wow.

[00:39:42] **Elizabeth:** That connected via USB and I basically just plugged the windows drivers into wine and, and ran it. And I had to implement a lot of things, but it worked. But for example, something like a graphics driver is not something you could implement in wine because you need the graphics driver on the host. We can't talk to the graphics driver while the host is already doing so.

[00:40:05] **Jeremy:** I see. Yeah. And in that case it probably doesn't make sense to do so 

[00:40:11] **Elizabeth:** Right?

[00:40:12] **Elizabeth:** Right. It doesn't because, the transition from user into kernel is complicated. You need the graphics driver to be in the kernel and the real kernel. Having it in wine would be a bad idea. Yeah.

[00:40:25] **Jeremy:** I, I think there's, there's enough APIs you have to try and reproduce that. I, I think, uh, doing, doing something where,

[00:40:32] **Elizabeth:** very difficult

[00:40:33] **Jeremy:** right. 


## Poor system call documentation and private APIs

[00:40:35] **Jeremy:** There's so many different, calls both in user space and in kernel space. I imagine the, the user space ones Microsoft must document to some extent, but, oh. Is that, is that a

[00:40:51] **Elizabeth:** well, sometimes,

[00:40:54] **Jeremy:** Sometimes. Okay.

[00:40:55] **Elizabeth:** I think it's actually better now than it used to be. But some, here's where things get fun, because sometimes there will be, you know, regular documented calls. Sometimes those calls are documented, but the documentation isn't very good. Sometimes programs will just sort of look inside Microsoft's DLLs and use calls that they aren't supposed to be using. Sometimes they use calls that they are supposed to be using, but the documentation has disappeared. just because it's that old of an API and Microsoft hasn't kept it around. sometimes some, sometimes Microsoft, Microsoft own software uses, APIs that were never documented because they never wanted anyone else using them, but they still ship them with the operating system. there was actually a kind of a lawsuit about this because it is an antitrust lawsuit, because by shipping things that only they could use, they were kind of creating a trust. and that got some things documented. At least in theory, they kind of haven't stopped doing it, though.

[00:42:08] **Jeremy:** Oh, so even today they're, they're, I guess they would call those private, private APIs, I suppose.

[00:42:14] **Elizabeth:** I suppose. Uh, yeah, you could say private APIs. but if we want to get, you know, newer versions of Microsoft Office running, we still have to figure out what they're doing and implement them.

[00:42:25] **Jeremy:** And given that they're either, like you were saying, the documentation is kind of all over the place. If you don't know how it's supposed to behave, how do you even approach implementing them?

[00:42:38] **Elizabeth:** and that's what the conformance tests are for. And I, yeah, I mentioned earlier we have this huge body of conformance tests that double is regression tests. if we see an API, we don't know what to do with or an API, we do know, we, we think we know what to do with because the documentation can just be wrong and often has been. Then we write tests to figure out what it's supposed to behave. We kind of guess until we, and, and we write tests and we pass some things in and see what comes out and see what. The see what the operating system does until we figure out, oh, so this is what it's supposed to do and these are the exact parameters in, and, and then we, and, and then we implement it according to those tests.

[00:43:24] **Jeremy:** Is there any distinction in approach for when you're trying to implement something that's at the user level versus the kernel level?

[00:43:33] **Elizabeth:** No, not really. And like I, and like I mentioned earlier, like, well, I mean, a kernel call is just like a library call. It's just done in a slightly different way, but it's still got, you know, parameters in, it's still got a set of parameters. They're just encoded differently. And, and again, like the, the way kernel calls are done is on a level just above the kernel where you have a library, that just passes things through. Almost verbatim to the kernel and we implement that library instead.

[00:44:10] **Jeremy:** And, and you've been working on i, I think, wine for over, over six years now.

[00:44:18] **Elizabeth:** That sounds about right.


## Debugging and having broad knowledge of Wine

[00:44:20] **Jeremy:** What does, uh, your, your day to day look like? What parts of the project do you, do you work on?

[00:44:27] **Elizabeth:** It really varies from day to day. and I, I, a lot of people, a lot of, some people will work on the same parts of wine for years. Uh, some people will switch around and work on all sorts of different things.

[00:44:42] **Elizabeth:** And I'm, I definitely belong to that second group. Like if you name an area of wine, I have almost certainly contributed a patch or two to it. there's some areas I work on more than others, like, 3D graphics, multimedia, a, I had, I worked on a compiler that exists, uh, socket. So networking communication is another thing I work a lot on. day to day, I kind of just get, I, I I kind of just get a bug for some program or another. and I take it and I debug it and figure out why the program's broken and then I fix it. And there's so much variety in that. because a bug can take so many different forms like I described, and, and, and the, and then the fix can be simple or complicated or, and it can be in really anywhere to a degree.

[00:45:40] **Elizabeth:** being able to work on any part of wine is sometimes almost a necessity because if a program is just broken, you don't know why. It could be anything. It could be any sort of API. And sometimes you can hand the API to somebody who's got a lot of experience in that, but sometimes you just do whatever. You just fix whatever's broken and you get an experience that way.

[00:46:06] **Jeremy:** Yeah, I mean, I was gonna ask about the specialized skills to, to work on wine, but it sounds like maybe in your case it's all of them.

[00:46:15] **Elizabeth:** It's, there's a bit of that. it's a wine. We, the skills to work on wine are very, it's a very unique set of skills because, and it largely comes down to debugging because you can't use the tools you normally use debug.

[00:46:30] **Elizabeth:** You have to, you have to be creative and think about it different ways. Sometimes you have to be very creative. and programs will try their hardest to avoid being debugged because they don't want anyone breaking their copy protection, for example, or or hacking, or, you know, hacking in sheets. They want to be, they want, they don't want anyone hacking them like that.

[00:46:54] **Elizabeth:** And we have to do it anyway for good and legitimate purposes. We would argue to make them work better on more operating systems. And so we have to fight that every step of the way.

[00:47:07] **Jeremy:** Yeah, it seems like it's a combination of. F being able, like you, you were saying, being able to, to debug. and you're debugging not necessarily your own code, but you're debugging this like behavior of,

[00:47:25] **Jeremy:** And then based on that behavior, you have to figure out, okay, where in all these different systems within wine could this part be not working?

[00:47:35] **Jeremy:** And I, I suppose you probably build up some kind of, mental map in your head of when you get a, a type of bug or a type of crash, you oh, maybe it's this, maybe it's here, or something 

[00:47:47] **Elizabeth:** Yeah. That, yeah, there is a lot of that. there's, you notice some patterns, you know, after experience helps, but because any bug could be new, sometimes experience doesn't help and you just, you just kind of have to start from scratch.


## Finding a bug related to XAudio

[00:48:08] **Jeremy:** At sort of a high level, can you give an example of where you got a specific bug report and then where you had to look to eventually find which parts of the the system were the issue?

[00:48:21] **Elizabeth:** one, one I think good example, that I've done recently. so I mentioned this, this XAudio library that does 3D audio. And if you say you come across a bug, I'm gonna be a little bit generics here and say you come across a bug where some audio isn't playing right, maybe there's, silence where there should be the audio. So you kind of, you look in and see, well, where's that getting lost? So you can basically look in the input calls and say, here's the buffer it's submitting that's got all the audio data in it. And you look at the output, you look at where you think the output should be, like, that library will internally call a different library, which programs can interact with directly.

[00:49:03] **Elizabeth:** And this our high level library interacts with that is the, give this sound to the audio driver, right? So you've got XAudio on top of, um. mdev, API, which is the other library that gives audio to the driver. And you see, well, the ba the buffer is that XAudio is passing into MM Dev, dev API. They're empty, there's nothing in them. So you have to kind of work through the XAudio library to see where is, where's that sound getting lost? Or maybe, or maybe that's not getting lost. Maybe it's coming through all garbled. And I've had to look at the buffer and see why is it garbled. I'll open up it up in Audacity and look at the weight shape of the wave and say, huh, that shape of the wave looks like it's, it looks like we're putting silence every 10 nanoseconds or something, or, or reversing something or interpreting it wrong. things like that. Um, there's a lot of, you'll do a lot of, putting in print fs basically all throughout wine to see where does the state change. Where was, where is it? Where is it? Right? And then where do things start going wrong?

[00:50:14] **Jeremy:** Yeah. And in the audio example, because they're making a call to your XAudio implementation, you can see that Okay, the, the buffer, the audio that's coming in. That part is good. It, it's just that later on when it sends it to what's gonna actually have it be played by the, the hardware, that's when missing. So,

[00:50:37] **Elizabeth:** We did something wrong in a library that destroyed the buffer. And I think on a very, high level a lot of debugging, wine is about finding where things are good and finding where things are bad, and then narrowing that down until we find the one spot where things go wrong. There's a lot of processes that go like that.

[00:50:57] **Jeremy:** like you were saying, the more you see these problems, hopefully the, the easier it gets to, to narrow down where,

[00:51:04] **Elizabeth:** Often. Yeah. Especially if you keep debugging things in the same area.


## How much code is OS specific?c

[00:51:09] **Jeremy:** And wine supports more than one operating system. I, I saw there was Linux, MacOS I think free BSD. How much of the code is operating system specific versus how much can just be shared across all of them?

[00:51:27] **Elizabeth:** Not that much is operating system specific actually. so when you think about the volume of wine, the, the, the, vast majority of it is the high level code that doesn't need to interact with the operating system on a low level. Right? Because Windows keeps putting, because Microsoft keeps putting lots and lots of different libraries in their operating system. And a lot of these are high level libraries. and even when we do interact with the operating system, we're, we're using cross-platform libraries or we're using, we're using ics. The, uh, so all these operating systems that we are implementing are con, basically conformed to the posix standard. which is basically like Unix, they're all Unix based. Psic is a Unix based standard. Microsoft is, you know, the big exception that never did implement that. And, and so we have to translate its APIs to Unix, APIs. now that said, there is a lot of very operating system, specific code. Apple makes things difficult by try, by diverging almost wherever they can. And so we have a lot of Apple specific code in there. 

[00:52:46] **Jeremy:** another example I can think of is, I believe MacOS doesn't support, Vulkan

[00:52:53] **Elizabeth:** yes. Yeah.Yeah, That's a, yeah, that's a great example of Mac not wanting to use, uh, generic libraries that work on every other operating system. and in some cases we, we look at it and are like, alright, we'll implement a wrapper for that too, on top of Yuri, on top of your, uh, operating system. We've done it for Windows, we can do it for Vulkan. and that's, and then you get the Molten VK project. Uh, and to be clear, we didn't invent molten vk. It was around before us. We have contributed a lot to it.


## Direct3d, Vulkan, and MoltenVK

[00:53:28] **Jeremy:** Yeah, I think maybe just at a high level might be good to explain the relationship between Direct 3D or Direct X and Vulcan and um, yeah. Yeah. Maybe if you could go into that.

[00:53:42] **Elizabeth:** so Direct 3D is Microsoft's 3D API. the 3D APIs, you know, are, are basically a way to, they're way to firstly abstract out the differences between different graphics, graphics cards, which, you know, look very different on a hardware level.

[00:54:03] **Elizabeth:** Especially. They, they used to look very different and they still do look very different. and secondly, a way to deal with them at a high level because actually talking to the graphics card on a low level is very, very complicated. Even talking to it on a high level is complicated, but it gets, it can get a lot worse if you've ever been a, if you've ever done any graphics, driver development. so you have a, a number of different APIs that achieve these two goals of, of, abstraction and, and of, of, of building a common abstraction and of building a, a high level abstraction. so OpenGL is the broadly the free, the free operating system world, the non Microsoft's world's choice, back in the day.

[00:54:53] **Elizabeth:** And then direct 3D was Microsoft's API and they've and Direct 3D. And both of these have evolved over time and come up with new versions and such. And when any, API exists for too long. It gains a lot of croft and needs to be replaced. And eventually, eventually the people who developed OpenGL decided we need to start over, get rid of the Croft to make it cleaner and make it lower level.

[00:55:28] **Elizabeth:** Because to get in a maximum performance games really want low level access. And so they made Vulcan, Microsoft kind of did the same thing, but they still call it Direct 3D. they just, it's, it's their, the newest version of Direct 3D is lower level. It's called Direct 3D 12. and, and, Mac looked at this and they decided we're gonna do the same thing too, but we're not gonna use Vulcan.

[00:55:52] **Elizabeth:** We're gonna define our own. And they call it metal. And so when we want to translate D 3D 12 into something that another operating system understands. That's probably Vulcan. And, and on Mac, we need to translate it to metal somehow. And we decided instead of having a separate layer from D three 12 to metal, we're just gonna translate it to Vulcan and then translate the Vulcan to metal. And it also lets things written for Vulcan on Windows, which is also a thing that exists that lets them work on metal.

[00:56:30] **Jeremy:** And having to do that translation, does that have a performance impact or is that not really felt?

[00:56:38] **Elizabeth:** yes. It's kind of like, it's kind of like anything, when you talk about performance, like I mentioned this earlier, there's always gonna be overhead from translating from one API to another. But we try to, what we, we put in heroic efforts to. And try, try to make sure that doesn't matter, to, to make sure that stuff that needs to be fast is really as fast as it can possibly be.

[00:57:06] **Elizabeth:** And some very clever things have been done along those lines. and, sometimes the, you know, the graphics drivers underneath are so good that it actually does run better, even despite the translation overhead. And then sometimes to make it run fast, we need to say, well, we're gonna implement a new API that behaves more like windows, so we can do less work translating it. And that's, and sometimes that goes into the graphics library and sometimes that goes into other places.


## Targeting Wine instead of porting applications

[00:57:43] **Jeremy:** Yeah. Something I've found a little bit interesting about the last few years is

[00:57:49] **Jeremy:** Developers in the past, they would generally target Windows and you might be lucky to get a Mac port or a Linux port. And I wonder, like, in your opinion now, now that a lot of developers are just targeting Windows and relying on wine or, or proton to, to run their software, is there any, I suppose, downside to doing that?

[00:58:17] **Jeremy:** Or is it all just upside, like everyone should target Windows as this common platform?

[00:58:23] **Elizabeth:** Yeah. It's an interesting question. I, there's some people who seem to think it's a bad thing that, that we're not getting native ports in the same sense, and then there's some people who. Who See, no, that's a perfectly valid way to do ports just right for this defacto common API it was never intended as a cross platform common API, but we've made it one.

[00:58:47] **Elizabeth:** Right? And so why is that any worse than if it runs on a different API on on Linux or Mac and I? Yeah, I, I, I guess I tend to, I, that that argument tends to make sense to me. I don't, I don't really see, I don't personally see a lot of reason for, to, to, to say that one library is more pure than another.

[00:59:12] **Elizabeth:** Right now, I do think Windows APIs are generally pretty bad. I, I'm, this might be, you know, just some sort of, this might just be an effect of having to work with them for a very long time and see all their flaws and have to deal with the nonsense that they do. But I think that a lot of the. Native Linux APIs are better. But if you like your Windows API better. And if you want to target Windows and that's the only way to do it, then sure why not? What's wrong with that?

[00:59:51] **Jeremy:** Yeah, and I think the, doing it this way, targeting Windows, I mean if you look in the past, even though you had some software that would be ported to other operating systems without this compatibility layer, without people just targeting Windows, all this software that people can now run on these portable gaming handhelds or on Linux, Most of that software was never gonna be ported. So yeah, absolutely. And

[01:00:21] **Elizabeth:** that's 

[01:00:22] **Jeremy:** having that as an option. Yeah.

[01:00:24] **Elizabeth:** That's kind of why wine existed, because people wanted to run their software. You know, that was never gonna be ported. They just wanted, and then the community just spent a lot of effort in, you know, making all these individual programs run. Yeah.

[01:00:39] **Jeremy:** I think it's pretty, pretty amazing too that, that now that's become this official way, I suppose, of distributing your software where you say like, Hey, I made a Windows version, but you're on your Linux machine. it's officially supported because, we have this much belief in this compatibility layer.

[01:01:02] **Elizabeth:** it's kind of incredible to see wine having got this far. I mean, I started working on a, you know, six, seven years ago, and even then, I could never have imagined it would be like this.

[01:01:16] **Elizabeth:** So as we, we wrap up, for the developers that are listening or, or people who are just users of wine, um, is there anything you think they should know about the project that we haven't talked about?

[01:01:31] **Elizabeth:** I don't think there's anything I can think of.

[01:01:34] **Jeremy:** And if people wanna learn, uh, more about the wine project or, or see what you're up to, where, where should they, where should they head?


## Getting support and contributing

[01:01:45] **Elizabeth:** We don't really have any things like news, unfortunately. Um, read the release notes, uh, follow some, there's some, there's some people who, from Code Weavers who do blogs. So if you, so if you go to codeweavers.com/blog, there's some, there's, there's some codeweavers stuff, uh, some marketing stuff. But there's also some developers who will talk about bugs that they are solving and. And how it's easy and, and the experience of working on wine.

[01:02:18] **Jeremy:** And I suppose if, if someone's. Interested in like, like let's say they have a piece of software, it's not working through wine. what's the best place for them to, to either get help or maybe even get involved with, with trying to fix it?

[01:02:37] **Elizabeth:** yeah. Uh, so you can file a bug on, winehq.org,or, or, you know, find, there's a lot of developer resources there and you can get involved with contributing to the software. And, uh, there, there's links to our mailing list and IRC channels and, uh, and, and the GitLab, where all places you can find developers.

[01:03:02] **Elizabeth:** We love to help you. Debug things. We love to help you fix things. We try our very best to be a welcoming community and we have got a long, we've got a lot of experience working with people who want to get their application working. So, we would love to, we'd love to have another.

[01:03:24] **Jeremy:** Very cool. Yeah, I think wine is a really interesting project because I think for, I guess it would've been for decades, it seemed like very niche, like not many people

[01:03:37] **Jeremy:** were aware of it. And now I think maybe in particular because of the, the Linux gaming handhelds, like the steam deck,wine is now something that a bunch of people who would've never heard about it before, and now they're aware of it.

[01:03:53] **Elizabeth:** Absolutely. I've watched that transformation happen in real time and it's been surreal.

[01:04:00] **Jeremy:** Very cool. Well, Elizabeth, thank you so much for, for joining me today.

[01:04:05] **Elizabeth:** Thank you, Jeremy. I've been glad to be here.
