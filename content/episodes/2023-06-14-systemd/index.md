+++
title = "Anita Zhang and Alvaro Leiva on systemd at Meta"

description = "Anita and Alvaro discuss systemd and the psystemd python library"

[extra]
episode_url = "https://pinecast.com/listen/99e782d7-806c-4fc9-8a20-dd5b105dde9e.mp3"
social_title = "Anita Zhang and Alvaro Levia on systemd at Meta"
social_description = "Linux Userspace and Production Engineering"
+++

systemd is a service manager for Linux. It is the first process that runs on many Linux distributions and manages all other user processes. It includes utilities for logging, process isolation, process dependencies, socket activation, and many other tasks.

psystemd is a python library to communicate with systemd over dbus from python as an alternative to shelling out from an application to control services.

Anita Zhang is an engineerd managerd at Meta and Alvaro Levia is a production engineer at Meta.

I attended their [systemd workshop](https://www.socallinuxexpo.org/scale/20x/presentations/workshop-guided-journey-heart-systemd) at the [Southern California Linux Expo](https://www.socallinuxexpo.org/scale/20x).

### Topics covered:

- What's systemd?
- Giving talks and workshops
- cgroups and namespaces
- systemd timers vs cron
- Migrating from CentOS 6 to 7
- Production engineers need to go lower in the stack to debug applications
- Meta's Linux userspace team
- Use of public cloud at Meta
- Meta's bootcamp
- Pystemd

### Mastodon
- [Anita Zhang](https://fosstodon.org/@anitazha)
- [Alvaro Leiva](https://fosstodon.org/@aleivag)

### Workshop
- [systemd workshop](https://github.com/systemdemo/workshop)

### Conference talks
- [Journey into the Heart of systemd - Scale 19x](https://www.youtube.com/live/FMnvvfBYypY?feature=share&t=24791)
- [Systemd: why you should care as a Python developer - PyCon 2018](https://www.youtube.com/watch?v=ZUX9Fx8Rwzg)
- [Move Fast without Breaking things - Scale 18x](https://www.youtube.com/watch?v=yJsFw9H3Y4A)
- [Solving All the Problems with systemd - LISA18](https://www.youtube.com/watch?v=_OLwb8zV9r4)
- [Using systemd to high level languages - All Systems Go!](https://www.youtube.com/watch?v=lBQgMGPxqNo)
- [The Curious Case of Memory Growth - Scale 19x](https://www.youtube.com/live/FMnvvfBYypY?feature=share&t=1511)

### Related Links

- [systemd](https://www.freedesktop.org/wiki/Software/systemd/)
- [psystemd](https://github.com/systemd/pystemd)
- [systemd-run](https://www.freedesktop.org/software/systemd/man/systemd-run.html)
- [systemd-timers](https://www.freedesktop.org/software/systemd/man/systemd.timer.html)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">


## Introductions

[00:00:00] **Jeremy:** So today I'm talking to Avaro Leiva and Anita Zhang. Avaro is the author of the pystemd library and he's a production engineer at Meta. And Anita is an engineerd managerd at Meta, and I'll let her explain that further.

[00:00:19] **Jeremy:** But thank you both for joining me today. 

[00:00:21] **Anita:** Yeah, thanks for having us. 

[00:00:24] **Jeremy:** I guess where we could start, Anita, maybe you could explain a little bit your, your title that I just gave you there. 


## engineerd managerd

[00:00:31] **Anita:** Yeah, so by default I, I should be a software engineering manager, but when I transitioned to management, I was not, Ready to go public with, um, my transition.

So I kind of hid it by, changing the title. we have some weird systems in place that grep on like the word engineer. So I had to keep engineer in there somehow. and so I kind of polled my friends what I should change my title to, and they're like, oh, you're gonna support the systemd team, so you should change it to like managerd.

So I was like, sounds good. engineerd, managerd. 

I didn't wanna get kicked out of any workplace groups, for example, that required me to be an engineer. 

[00:01:15] **Jeremy:** Oh, okay. 

[00:01:17] **Anita:** Or like engineering function, I guess. 

[00:01:19] **Jeremy:** Yeah. Yeah. And you just gotta title it yourself, so as long as you got engineer in it, you're good. 

[00:01:24] **Anita:** Yeah, pretty much. Some people have really fun titles like Chief Potato Officer and things like that.

[00:01:32] **Jeremy:** So what groups does the, uh, the potato officer get to go in? 

[00:01:37] **Anita:** Yeah. Not the C level ones. (laughs) 


## What's systemd?

[00:01:42] **Jeremy:** I guess maybe to, to start, we should explain to people who aren't familiar, uh, what systemd is. So if either of you wanna wanna take that one.

[00:01:52] **Alvaro:** so people who doesn't know, right?

So systemd is today is your init system, right? Is the thing that manage your, your process. and the best way to understand this, it is like when your computer, it needs to execute something. And that's something is what we call pid one. And that pid one is the thing that is gonna manage everything from now from there on, right?

Uh, in the most basic level, if you remember how to, how does program start, how does like an idea becomes a program? Uh, you need to fork exec, right? So that means that something has to be at the top of that tree and that is systemd. now that can be anything, right? So there was a time where that was like systemv and there was also like upstart, uh, today's systemd is the thing that, uh, it's shipped in most distributions.

[00:02:37] **Jeremy:** Yeah, because I, I definitely remember when I first started working with Linux, uh, it was with CentOS 6, and when I would want to run a service, I would have to go and write a bash script and kind of have all these checks for, is this thing running?

Does it have permission to these things, which user is it running as, and so there was a lot of stuff that I remember having to do before systemd came out. 

[00:03:08] **Alvaro:** The good old days as we call them, 

[00:03:11] **Jeremy:** Or the bad old days. 

[00:03:13] **Anita:** Yeah. Depending on who you ask.

[00:03:15] **Alvaro:** Yeah. So, so that is super interesting because, um, During those time, like you said, you have to write a first script.

That means that you were basically yourself, your own service manager, right? So ideas as simple as, is my program running? There was no real answer. You have to figure it out, right? So if you run a program, uh, you maybe would create a pid file which hold the p or the pid of the process, of the main process, right?

And then something needs to check, oh, is this file exist? Does the file exist and does the content of this file actually match to a process? And then you grab the process. So it was all these ideas that you had to do, and then for, you have to do it for every single software that you would deploy on your machine, right?

That also makes really hard to parallelize stuff, right? Because you have no concept of dependencies. So if your computer has to put, uh, I, I dunno if you remember like long time ago, like Linux machine would, takes like five minutes to boot like your desktop. I remember like openSUSE. I can't remember, like 2008, 2007.

Uh, it would take like five minutes to boot and then Ubuntu came and, and it start like immediately. And it was because, you can parallelize things, but you cannot do that if all you're running are bash script.


## Why was systemd chosen to be included in Linux distributions?

[00:04:26] **Jeremy:** I remember before the Linux distributions didn't include it.

And I wonder if you have any insight into how systemd got chosen to be the thing to manage our processes and basically how we got to where we are today. 

[00:04:44] **Anita:** I mean, we can kind of speculate a little bit. at the time when Lennart started systemd, um, with. Kai Sievers probably messed up his name there. Um, they were all at Red Hat and Red Hat manages fedora these days and I believe fedoras kind of like the bleeding edge for a lot of the new software ideas. Um, and when they picked up systemd as the defaults, um, eventually it started to trickle down to the rest of their distributions through RHEL and to CentOS and at the same time, I think other distributions started to see how useful it was in terms of managing all the different processes and services.

Um, I know Debian at one point had kind of a vote on like whether they should make systemd either default or like, make it easy to switch between both. And then they decided to just stick with systemd because it's, I mean, the public agrees that it's like easy to use and it's more useful.

It abstracts away a lot of things that they had to manually do before


## Who is interested in systemd? Who comes to your talks and workshops?

[00:05:43] **Jeremy:** Something I've been kind of curious about. So just this year at SCaLE uh, you ran a, a workshop teaching people how to use systemd and, and sort of what it is about. I guess when, when you get people coming to these workshops, what are they typically, where are they typically coming from? Are they like system administrators or are they software developers?

Like when you run these workshops, who are you looking for as your audience? 

[00:06:13] **Alvaro:** To be fair, this was the first time that we actually did a workshop for this. But we have like, talk about this in, in many like conferences. here's what happened, right? So every time that you put systemd on the title of, uh, of a talk, you are like baiting people into coming in, right?

Because you do want to hear like some people who are still like reluctant from that war that happened like a few years ago. Between systemd and Ups tart right? most of the people who we get are, I would say like, software engineers, people who do software, and at least the question that I always get a lot, it is like, why should I care about systemd um, if I run everything on my containers in my Docker containers, right?

The other type of audience that you get, you do get system administrators. Uh, but in general those people only cares about starting and stopping services don't really care about like the, like the nice other features that systemd has to offer. And then you get people who just wanna start like flame wars and I'm here for them.


## Why give talks and workshops on systemd?

[00:07:13] **Jeremy:** In previous years, you've given conference talks and, and things like that related to systemd. And I wonder for, for both of you where, where the, the interests came from, where this is something that you feel strongly enough about that you wanna give talks about it.

Because it's like, a lot of times when people give a conference talk, it's about, like new front end technology or some, you know, new shiny thing. Whereas systemd is like, it's like very valuable, but it's something that I feel like a lot of people don't think about.

And so I'm just kind of curious where the interest came for, for both of you.

[00:07:52] **Anita:** I think I just like giving talks and teaching in general. So if I have work that I found really exciting or interesting, then I'd want to like tell people about it and like teach them and like show them something cool. I think systemd is kind of a really good topic in that case because a lot of people want to learn more about it.

Today there's like lots of new developments going on in systemd. So there's like a lot of basic stuff that you can learn, but also a lot of new advanced topics that are changing every year as well. aside from that, there's also like more generally applicable things. Like everyone wants to know how to debug something if you're like a software engineer or developer or even a sysadmin.

Um, so last year I did a debugging talk. there's a lot of overlap I'd say how about you Alvaro?

[00:08:48] **Alvaro:** For me, it, my interest in systemd started in, back when I was working on Instagram, we needed to migrate from CentOS6 to CentOS7. and that was the transition where you would have like a random init system to systemd, right?

So we needed to migrate all of our scripts from like shell script to whatever shell script is going to interact with systemd. And that's when I was like, I don't like this. So I also have a thing where if I find something that doesn't have an Python API for it, I go and create a Python api. So I, I create pystemd like during that time.

And I guess for me, the first reaction was when I was digging up systemd was like, whoa, can systemd do that? Like, like really, like I can like manage, network firewalls, right? Can I, can I stop my service from actually accessing the internet without having to deal with iptables at the time?

So that's kind of like the feeling that I wanted to show people when I, when we do these these talks and, and these workshops, right? It's why like most of our talks, eh, have light demos in them because we do want to show people like, Hey, like, this is real. You can use it. 

[00:09:55] **Jeremy:** I don't know if this was a conscious decision on your part, but the thing about things like systemd is they, they feel like more foundational things that don't change that quickly.

Like if you look at front end development, for example, at at meta you've got React, and that ecosystem changes so often that it's like there's always this new thing, you learn the way to do it and then it changes, right? Whereas I feel like when you're in the Linux user space and you're with systemd, like they're adding new things, but the, the.

Foundations kind of stay the same. I'm not sure if that sounds accurate to both of you. 

[00:10:38] **Anita:** Yeah, I'd say a lot of the, there are a lot of stable building blocks in systemd, but at Meadow we also have a kernel team, which is working on like new kernel features all the time. They take years possibly to adopt, but with systemd, if we're able to influence the community and like get those kernel features in earlier, then like we can start to really shape what the future of operating systems look like.

So it's not, it's very like not short term, uh, work that we're doing. It's a lot of long term, uh, work. 

[00:11:11] **Jeremy:** Yeah, that's, that's interesting in that I didn't even think about the fact that you are sitting at the, the user level with systemd, but you kind of know what you want. And so if there's things that the kernel can do to support that, you're having that involvement.

With the open source community, make sure that you have your, your say get put in there. Yeah.

[00:11:33] **Anita:** Mm-hmm. 

[00:11:35] **Alvaro:** It, it goes both way, right? So one part it is like, yeah, sure, we want features and we create them. Um, and we actually wanted to those to be upstream because we like, one thing that you should, you should never do is manage internal patches for like, things like the kernel, because that's rebase hell.

Um, but you also want to be like part of the community and, and, and, and get the benefit of like, being part of it.


## Who should care about systemd?

[00:11:59] **Jeremy:** And so, like one thing you mentioned ear earlier, Alvaro, is that people will sometimes ask you, I'm running my application in, in Docker containers. Why do I care about systemd? So, so maybe you could explain like, how you would respond to that. Yeah. 

[00:12:17] **Alvaro:** Well for more, for most people who actually run their application container I'd say like, no, you probably shouldn't care.

Right? Like, you're good where you are. But in general, like, like system is foundational in the sense that it is the first thing that your computer boots your computer doesn't boot off of Docker or Kubernetes or, or any like that. So like something has to run these applications. there's also like a lot of value is that not all applications exist in the vacuum.

Like, uh, like let me give you an example. Like if you have a web server, When people are uploading stuff to the web server, you will upload temporary things and then you have to clean it up after a while. So you may want to take advantage of systemd timers or cron or, or whatever you want, right?

While the classical container view is that your pid one of the container is the application that you're running, right? So you do want to have like this whole ecosystem, Not all companies can run on containers. not everything can run in containers. So that's basically where all the things start to, to getting into shape.

There's a lot of value in understanding how programs actually like exist, right? With the thing that I told you at the beginning of how an idea becomes a program understanding like, like you hit, you are in your bash, right? And you hit ls Star full enter, right? What happened in your machine?

Understanding all the things, uh, there is a lot of value and understanding how systemd works. It's, it, it provides, uh, like that knowledge for you. 

[00:13:39] **Jeremy:** So for the average engineer at Meta who is relying on your team to deploy their, their code, I guess, if that's the right term, do you think that they're ever needing to think about systemd or is that kind of more like the responsibility of your team and they're just worried about like, I put my thing into my container and I don't, I don't worry about it.

[00:14:04] **Anita:** I think there's like a whole level of the stack that sh ideally we should not even care or know that we're running systemd below them. I think that's, say we're doing our job well, cuz then the abstraction is good enough that they don't have to worry about it. But there's like a whole class of engineers below that that have to, you know, support the systems that run our on bare metal and infrastructure and make it happen.

And those are the people who really care about what we're putting in systemd or like what the corner cases are and things like that. 

[00:14:37] **Jeremy:** Yeah, that, that makes sense. I mean, one of the talks that was at SCaLE was, uh, Brian Cantrill um, he gave a talk about the forgotten operator, and he was talking about how people forget that there are actual servers behind all the things we're deploying to, right?

[00:14:55] **Anita:** Mm-hmm. 

[00:14:55] **Jeremy:** There is a person that you're racking the machines and plugging the power, and like, even though there's all these abstractions in front, that still exists. And so it sounds like things happening at the kernel level and the Linux user space and systemd that's also true because all this infrastructure that people are using to deploy their software on your team is the one who has to keep that running and to keep that running, they need to understand, uh, systemd and, and all these foundational Linux pieces.

Yeah. 

[00:15:27] **Anita:** Mm-hmm. Yeah. 

[00:15:29] **Alvaro:** Like with that said um, I, and maybe it's because I'm very close to to, to the source. Um, and, and you know, like, like I said, like when, when all your tool is a hammer, everything looks like a nail? Well, that hammer for me, a lot of the times it is like even like cgroups or, or namespaces or even like systemd itself, right?

there is a lot of times where, um, like for instance, a few years ago we have not, like, like last year or something, uh, we had an application that was very was very hard to load, right? It used a lot of memory. And so we start with, with a model where we would load like a, like a parent process and then child process would deal with, with, um, with the actual work of the thing, the classical model of our server.

Now, the thing is that each of the sub process that would run would need to run, uh, on a separate set of privileges, right? So it would really need to run as different users. And that was like very easy to do. But now we actually wanted to some process to run with a, with only view of the file system while the parent process actually doesn't have to do that, right?

Uh, or we want to limit the amount of CPU that a child process would use. So like all of these things, we were able like to, to swap it out uh, with using like systemd and, and, uh, like, like a good, Strategy for like, you create a process, you create a new cgroup, you put that into the cgroup, you create the namespace, uh, you add this process into that namespace, and then you have like all this architecture, and it's pretty free because forking it's free in general.

[00:17:01] **Anita:** Actually, Alvaro's comment reminded me of like why we even ended up building the systemd team in the first place. It's kind of like if we have all these teams trying to touch cgroups on their own or like manage processes on their own, they're all gonna do it a different way and not, all of them will be ideal or like, to put it bluntly, I guess, we're really aiming to try and provide like a unified, really good foundational experience, for the layers above us.

And so, systemd and the other things that go into the operating system are a step to get there.


## What are cgroups and namespaces?

[00:17:40] **Jeremy:** And so for someone who's not familiar with the concept of cgroups or of namespaces, could you kind of give like a brief description?

[00:17:50] **Anita:** so namespaces are, uh, we're talking about the kernel feature where, um, there are different ways to isolate, uh, different resources to the process or like, so that they have their own view of certain things, the network or, the processes and things like that. Um, and Cgroup stand for control groups.

It's, at meta we only use Cgroups v2 which is a way to organize your processes into, Kind of like a directory view. but processes will be grouped into different, folders, shall you say, but that allows you to, uh, manage the resources between different groups of processes, which is how systemd does its services.

[00:18:33] **Alvaro:** So a, a control group will allow you to impose restrictions on how each system uses the resources, right? So with a cgroup, you can say, only use 20% of cpu, and the, and the kernel will take care of that. Uh, while namespace it is basically how you view the system around you. So like your mount directory like, like where does your home points to?

that's, I would say it's more on the namespace side of things. So one is the view then one is the actual, the restrictions. And like Anita said, like systemd does a very clever thing. It doesn't have two, is not the. It's not why cgroups exist, but every time that you start a systemd service, systemd will create a cgroup for that service and will put every process in that cgroup, even though all cgroups would end up being the same, for instance.

But eh, you can now like have a consolidated list of what process belong to a service. So a simple question like, like what services has my Apache web service started? That's show you how old I am. But yeah, you can answer that now because you just look at the cgroup, you don't look at the process tree.

[00:19:42] **Jeremy:** So it, it sounds like the, the namespacing is maybe more for the purposes of security, like you said, giving you a certain view of your, your system. and the cgroups are more for restricting resources, but also, like you said, being able to see what are all the processes, um, are associated. Um, so that you, you don't have a process that spins up other processes and then you don't know who owns those, and then you don't know how to shut 'em all down.

That, that takes care of that for you. 

[00:20:17] **Alvaro:** So I, I always reluctant to use the word security or privacy. I would like to use the word isolation. Yeah. And then if people want to impose the idea of security and privacy to those, that's fine, but it's, but it's mostly about isolation. 

[00:20:32] **Anita:** Yeah. Namespaces are what back all the container technologies are.

Anytime you run things in a container, it's probably using some kind of name spacing. But yeah, you, you kind of hit the nail in the head. Isolation versus like resource control 

[00:20:46] **Alvaro:** As Anita just said that's what fits on containers, uh, namespaces and cgroup like a big mix of those. But that doesn't mean that the only reason why those things exist are for containers.

You can take advantage of those technologies without actually having to think of a container. 


## systemd timers vs cron

[00:21:04] **Jeremy:** Something you had mentioned a little bit earlier is, is how systemd has other features and one of them was, was timers. And I was kind of curious, cuz you said you could, you wanna schedule a job, you can run it using cron or you can run it using systemd timers.

And it, I feel like whenever I see people scheduling jobs, they're always talking about cron but, but not so much about systemd timers. So I was curious if you had any thoughts on that.

[00:21:32] **Anita:** I don't know. I feel like it's used pretty interchangeably these days. Um, like even when people say cron they're actually running a systemd timer with the cron format, for their time. 

[00:21:46] **Alvaro:** So the, the advantage of of systemd timers over cron is, is basically two, right? The first one it is that, you get more control on the time, right?

So you have monotonic and absolute times, right? Which is basically like, you can say like this, start five minutes after the previous run. Or you can say this, start after five minutes after the vote, right? So those are two type of time, that is the first one, uh, which may be irrelevant for most people, but that's it.

Uh, the other one is that you actually have advantage over the, you take full advantage of systemd, right? In current you say run this process, right? And how that process run, it's basically controlled by the process itself, right? So if you, uh, like if the crontab is for the user, that's good for you, but if you want to like nice it or make it use less cpu, that's what it is.

Well, with systemd you say, This cron will start the service and the service, you take full fledged advantage of all the things a service can do. 

[00:22:45] **Jeremy:** From what I could tell, looking at the, the timers api, it, it felt like it would be a lot easier to kind of see when things ran, get, you know, get a log of, I ran this time job and it, it failed.

Um, it seemed like systemd had a lot more kind of built in to, to kind of look into that. but, uh, yeah, like Anita was saying, like when you, you hear kind of cron all the time, but like you said, maybe it's, maybe they're not actually using cron all the time. They're just saying cron 

[00:23:18] **Alvaro:** Well, I would say this for cron like the, the time, the time, uh, syntax for it, it's pretty, it's pretty easy to understand, even though I never remember where, I remember where weekday is, right? The fourth, which one is which? 

[00:23:32] **Jeremy:** I, I'm with Anita. I need to look it up whenever I'm gonna use it. (laughs) 

[00:23:36] **Anita:** Yeah. I use a cron translator when I have to use cron format. 

[00:23:41] **Alvaro:** This is like, like a flags to tar, right?

Like, I never remember which, which flags to put. 

[00:23:48] **Anita:** Yeah, that's true. 

[00:23:50] **Alvaro:** We didn't talk about this, we haven't talked about systemd-run, but one of the advantages of the, one of the advantages of using timers is that you can schedule them on demand, right? So like cron if you wanna schedule something over time, you need to modify the cron the cron file.

Uh, and that's, it's problem right? With systemd, you can have like ephemeral units and so you can say like, just for now, go and run this process five hours from now. Like, and after that, just forget about it. 

[00:24:21] **Jeremy:** Yeah, the, during the workshop you mentioned systemd-run and I hadn't even heard of it. And after I saw that I was like, wow, this, this could be really useful.

[00:24:32] **Alvaro:** It is quite useful.


## How have things changed at meta?

[00:24:34] **Jeremy:** One of the things you had mentioned, I, I guess you've, you've been at Meta for, for quite a while and you were talking about how you started with having all these scripts you were running on CentOS 6 and getting off of that to something more standard. I wonder if you could speak a little bit to that, that process.

Like what did things look like then and, and how have they they changed over the years?

[00:25:01] **Alvaro:** I would say the following thing, right? Like Anita said, like for most engineers, the day to day of things don't really change that much, because this is foundational things, right? So if you have to fundamentally change the way that you run applications every couple of years, then you waste a lot of time, right?

It's not the same as you say, like react where, or, or in the old days, angular where angular one, angular two, angular three, and then it's gone, right? Like, so, so I, I would say it like for the average engineers things don't change that much, uh, for the other type of engineers, like, like us who we, who that we really care about, like how things run.

like having a, an API where you can like query the state of your service. Like if like asking like, is my service running with an API that returns true or false, that is actually like a volume value that you can like, Transferring in your application, uh, that, that helps a lot on, on distributed systems.

a lot of like our container infrastructure that we use internally at Meta is based on a lot of these ideas and technologies. 

[00:26:05] **Anita:** Yeah, thinking back to the CentOS 6 to 7 migration, I wasn't on like the any operating systems team at the time, but I was working with them and I also was on a team that had to migrate, figure out how to migrate our scripts and things over. so the one thing that did make it easy is that the OS team, uh, we deploy all our things using Chef.

Maybe you've heard like Puppet and Ansible, that's our version, the Open Source Chef code. Um, and they wrote some really good documentation on how to migrate, from Runit, which is what we were using before to systemd. it was. a very large scale effort across multiple teams to kind of make sure their stuff works, do the OS upgrade and then get used to using systemd.

[00:26:54] **Jeremy:** And so the, the team who is performing this migration, that's not the product team. That would be the, is it production engineering? Is that, is that what you called that? 

[00:27:09] **Alvaro:** So, so I was at the other side of, of that, of that table where I, the same as Anita, we were doing the migration more how most things work at Facebook is that it's a combination of the team that is responsible for the technology and the teams who uses the technology.

Right. So we are a company, so we. Can like, move together. it's the same thing when you upgrade kernels. Most of the time the kernel team will do the effort to upgrade the kernels, and when they hit a roadblock or something, they will call for the owner of the service and the owner of the service can help debug uh, for the case of CentOS 6 and CentOS 7, eh, I was the PE at Instagram P Stand for Production Engineer.

I was the PE at Instagram who did most of the migration of our fleet. So I, I rewrote most of the things because I understand how our things work, and the OS team provide like the support to understanding like, like when can I use some things, when can I use not other things. There was the equivalent of ChatGPT at those days, right?

I was just ask them how to do stuff. They will gimme recipes. so, so it it's kind of like, like a mix, uh, work, uh, between those two teams. Uh, Anita, maybe you can talk a little bit about what you talk when you were upgrading the version of systemd and you found a bug? 

[00:28:23] **Anita:** Oh, the, like regular systemd upgrades nowadays?

I, I'd say it's a lot easier these days. I mean, since the, at the time when we did the CentOS 6 to 7 migration, it was like, our fleet was a lot more fragmented. I'd say nowadays it's a lot more homogenous, which makes, which makes it easier. yeah, in the early versions there were some kind of obscure like, interactions with the kernel or like, um, we, we make pretty heavy use of systemd to run our container system.

So, uh, if we run into any corner cases, um, like pretty obscure stuff sometimes, because we make pretty heavy use of the resource control properties. we usually those end up on the GitHub tracker, things like that. 

[00:29:13] **Alvaro:** That's the side effect of hiring very smart people. They do very smart things that are very hard to understand. (laughs) 

[00:29:21] **Jeremy:** That's kind of an interesting point about you, you saying you're using these, these features, you know, of the kernel very heavily because, you're kind of running your own infrastructure, I think even your own data centers, so you're kind of forced to go to this level, it sounds like just because of the sheer number of services you're running and the fact that like, you have to find a way to pack 'em all onto the same machine.

Does that, does that sound right? 

[00:29:54] **Anita:** Yeah, I'd say at, at our scale, like it's more cost effective to act, own the servers and run all everything on it ourselves versus like, you know, leasing from, uh, AWS or something, which we've also explored in the past. But that also means we need more engineers to build and run things on our servers.

[00:30:16] **Jeremy:** Yeah. So the, the distinction between, let's say you're a, a small company or a mid-size company and you pay AWS or, or Google to, to do your hosting for you, then you may not necessarily get exposed to a lot of the, the kernel level problems or even the Linux user space problems because you're, you're working at a higher level and that's why you don't necessarily encounter those kinds of things.

[00:30:46] **Anita:** I'd say not, not necessarily. I think, once you get even like slightly lower in the stack where you're just like on your own server, Then you will want to start really looking into like what systemd's doing, how does it interact with other, uh, services, um, on your server, and how can you like connect these different features together?

[00:31:08] **Alvaro:** One of the things that every developer who who works like has to worry about is log right, and that, and that's the first time that you actually start interacting with systemdata available, right? So you have to understand, like maybe it's not just tail /var/log foo, but log right. Maybe it's just journalctl and it's like, what?

But yeah. 

[00:31:32] **Jeremy:** Yeah. That's a good point too about whenever you're working with the operating system, like you're deploying onto a Linux machine. Regardless of the distribution, if you're the person who's responsible for that, you, you need to know this stuff. Right. Otherwise it's kind of like, you're just putting stuff out there and hoping for the best.

Yeah. 

[00:31:54] **Alvaro:** Yeah. There, there's also another thing that, I dunno if I've said this before, but, a lot of the times you don't have to know these technologies, but knowing them will help you do your work better.

[00:32:05] **Jeremy:** Yeah, totally. I mean, I think that that applies to pretty much anything in, in development, right? I, I've heard often that some people will say, you take the level that you work at currently and then kind of just go down one level. Right. And then, so you can kind of see what's underneath that. And you don't necessarily need to keep digging, cuz eventually if you keep digging, you're getting into, you know, machine instructions and whatnot.

But, um, Yeah, maybe just one level is, is good to, to give you a better sense of what's 

happening. 


## Production engineers need to go lower in the stack to be able to debug applications 

[00:32:36] **Alvaro:** Um, every time that I, that I, that somebody ask me like, what is the difference between a PE and a SWE, uh, software engineer, production engineer, typical conference, uh, one of the biggest difference that I, that I say is that a PE would tends to ask a lot of questions going the same thing that you're saying, we're trying to go down the stack, right?

And I always ask the following question, eh, do you know how time dot sleep is implemented? Right? Do you like, like if you, if you were to see time dot sleep on your Python program, like do you actually know what is doing under the hood, right? Is it a while true? While the time, is it doing a signal interrupt?

Is it doing a select on a file descriptor with a timeout? Like what is it doing? would you be able to implement it? And the reason why I say this, because like when you're debugging an application, like somebody something's using your cpu, right? And then you see that line on your code, you. You can debug every single line of your code.

But also there's a lot of value to say like, no time.sleep doesn't cause CPU to spike. Right. Because it's implemented in a way that it would not be possible to do that.


## Meta's linux user space team

[00:33:39] **Jeremy:** Another thing that I think might be kind of interesting to talk about is, so Meta has this Linux user space team. And I, I wonder like including your role in it, but just as a whole, like what does that actually mean day to day?

Like, what are the kinds of problems people are facing that, a user space team would be handling? 

[00:34:04] **Anita:** Hmm. It's kind of large cuz now that the team's grown out to encompass a few other things as well. But I'll focus on the Linux user space part. the team started off, on the software engineering side as the systemd developer team.

So our job was really to contribute to the community. and both, you know, help with, problems and bugs that show up in upstream, um, while also bringing in new features, that we think would be useful both at Meta and to like, folks, in the Linux community as a whole. so we still play a heavy role in, systemd.

We also support it, uh, within the fleet, like we roll out new releases and things like that. but we're also working on a few other projects in. User space. Um, BP filter is one of them, which is, uh, how can we convert like IP tables and network filtering, into BPF programs. Um, on the production engineering side, they focus a lot on, the community engagements.

So in addition to supporting CentOS they also handle, or they like support several packages in Fedora, Debian and other distributions, really figuring out how we can, be a better member of the open source community, and, you know, make connections there and things like that. 

[00:35:30] **Jeremy:** And, and what was your, your process for getting in involved with this team?

Because it sounded like maybe it either didn't exist at the start, or it was really small and, and now it's really, really grown. 

[00:35:44] **Anita:** So I was kind of the first member of like the systemd team, if you would call it that. Um, it spun out of containers. So my manager at the time, who's now my director, was he kind of made a call out on workplace looking for people who'd be willing to, contribute to systemd.

He was, supporting the containers team at the time who after the CentOS 7 migration, they realized the potential that systemd could have, making their jobs a lot easier when it came to developing the container backend. and so along with that, they also needed someone to help, you know, fix bugs, put in new features and things that would, tie into the goals of the containers team.

Um, and eventually now our host management team, I was the first person who reached out to him and said, Hey, I wanna give this a try. I was on the security team at the time and I always had dreams of going back into like, operating systems development and getting better at it. So yeah, that's kind of how I ended up in this space.

A few years later, he decided, Hey, we should build a team and you should like hire some people who will also do this with you and increase our investments in systemd. so that's how we kind of built out the Linux user space team to encompass systemd and more like operating system, projects.


## Working on the internal security team vs the linux userspace team

[00:37:12] **Jeremy:** And so when you were working on the security team before, was that on software internal to meta or were you also involved with, you know, the open source, user space side as well? 

[00:37:24] **Anita:** That was all internal at the time. Which was kind of a regret because there was a lot of stuff that I would've liked to talk about externally.

But I think, moving to Linux user space made me realize like, oh, there's so much more potential in open source projects, in security, which is still like very closed source from our side. 

[00:37:48] **Jeremy:** And, and so like in your experience, what have been some of the big differences? I mean, definitely getting to talk about it is a big one.

but like in terms of your day-to-day, what are the big differences between working on something internal versus something that that's open source? 

[00:38:04] **Anita:** I have to talk more with external folks. we're, pretty regular members of like the systemd like conclave sync that we have with the other upstream maintainers.

Um, Oh yeah. There's a lot more like cross company or an external open source community building that we have to do. it kind of puts into perspective like how we manage our time and also our relationships versus like internally, like everyone you work with works at Meta. we kind of have, uh, some shared leadership at the top.

it is a little faster to turn around, um, because, you know, you can just ping people on work chat. But the, all of the systems there are closed source. So, um, there's not like this swath of people outside that you can ask about when it comes to open source things. 

[00:38:58] **Jeremy:** You can't, can't look in, discord or whatever for questions about, internal meta infrastructure to other people.

It's gotta be. all in the same place. Yeah. 

[00:39:10] **Anita:** Yeah. And I'd say with like the open source projects, there's a lot of potential to tap into, expertise and talent that just doesn't exist internally. That's what I found really valuable, cuz people have really great ideas outside as well. Um, and we should like, listen to them and figure out how to build that into their systems and also ours 


## Alvaro's work at meta

[00:39:31] **Jeremy:** And, Avaro, I don't know when you first started, was that on internal, infrastructure and tooling as well?

[00:39:39] **Alvaro:** Yeah, so, um, my path is different than Anita and actually my path and Anita doesn't share any common edges. so I, I don't work at the user space or the Linux kernel or anything. I always work in teams adjacent to it. Uh, but. It's always been very interesting to know these technologies, right? So I started working on Instagram and then I did a lot of the work in containers in migrations at where, where we build psystemd

and also like getting to know more about that technologies. We did, uh, a small pilot on using casync which is a very old tool that like, it's only for the fans, (laughs) it's still on systemd repository, I dunno if that's used or anything, but it was like a very cool idea of how to distribute images. Uh, and in Instagram we do very fast deployments.

So we deploy, or back then we used to deploy the source code, of Instagram every seven minutes, right? So every seven minutes, every time that a developer did commit to master, uh, we pushed that into production in less than an hour and we did that every seven minutes. So we were like planning to, to use those technologies for that.

Um, And then I moved to another team inside of Meta, which is called Cloud Foundation, where we do a lot of like cloud infrastructure, uh, like public cloud. Uh, that's the area, that is very much not talked much about. but I keep like contributing to, to like this world. never really work on, on, on those teams inside of Meta.

[00:41:11] **Jeremy:** So I guess it's your, your team is responsible for working with the engineers who work on product to be able to take their code and, and deploy it. And it's kind of like you work in combination with the user space team or the systemd team to make sure that what you're doing can be supported by them.

Is that kind of an accurate description? 

[00:41:35] **Alvaro:** Yeah, that's, that's, that's definitely not an exhaustive description, but yeah, that's the, we, we, we do that. 


## Public cloud at meta

[00:41:42] **Jeremy:** It's interesting that you're, you're talking about public cloud now. So when you move to public cloud, are you using VMs kind of like you would in a data center, or is it, you're actually looking at the more managed services and things like that?

[00:41:57] **Alvaro:** So I'm gonna take a small detour and say like, something that is funny. When I got hired by Facebook, we were working on Instagram. So Instagram was just an acquisition for, for, for meta right. And Instagram ran on AWS. So why wasn't the original team who were moving stuff from AWS into the internal data centers at Meta?

On the team that I work now, uh, we work to support workloads that cannot run on meta infrastructure either for legal reasons, or for, for practical reasons. Right, because we don't have the hardware, uh, capability or legal resource because the government ask us, like, this cannot be on, on your data center or security, right?

We don't wanna run this, this binary that we don't understand on our network. We do want to work in isolation. and the same thing that Anita was saying, where their team are building the common ways of using these tools, like systemd, and user space. we do the same thing, but for using cloud technologies.

So in a way that is more similar to meta. So that's the detour now the, to answer your actual question, uh, we do a potpourri of things, right? So since we manage infrastructure and then teams deploy their code, they are better suited to know how their code, gets to run. Uh, with that said, we do have our preferred ways of how you would run stuff.

and it's a combination of user containers, uh, open source containers, and and also like VMs 


## There's a big difference between VMs and meta and in public cloud

[00:43:23] **Jeremy:** So it, it sounds like in this case, you're, you're still using VMs even in public cloud, so the way that you do deployments, the location is different, but the actual software and infrastructure that you're running is, is similar.

[00:43:39] **Alvaro:** So there's there's a lot of difference. Between the two things, right. So, the uniformity of hardware at Facebook, or our data centers, makes deploying things very simple, right? while in, in the cloud, you first, you don't get that uniformity because everybody like builds their AMIs as, as they want to build it.

But also like a meta, we use, one operating system, in the cloud, you are a little bit more free of what you want. And one of the reasons why you want to go to the cloud is because you can run stuff on. On, on, on the way that that meta will run. Right? So, so even though we have something that are similar, it's not as simple like, oh, just change your deployment from like this data center to like whatever us is one think you would 

run.

[00:44:28] **Jeremy:** Can, can you give an example of something where you wouldn't be able to run it on Meta's, image that they would choose to go to public cloud to run a different image for? 

[00:44:41] **Alvaro:** So, um, so in, in general, like if the government ask us, like, this is not necessarily like, like the US government, right? So, and like if the government ask us like, hey, like you need to keep this transaction on, on our territory, right?

for logs, for all the reasons, for whatever, right? like, and, and we wanted to be in the place, we would have to comply. And that's where we will probably use this, this kind of technologies security is another one that is pretty good. And the other one, it is like, in it general, like, like, uh, like disaster recovery, right?

If, if meta is down in a way where we cannot communicate with each other using metas technologies, right? Like you would need to have like a bootstrap point. 

[00:45:23] **Jeremy:** Is, is it the case where you are not able to put, uh, meta's image up into public cloud? Because you were, The examples you gave was more about location, right?

Where you're saying we need to host in public cloud because it needs to be in this country, but then I think you were also saying the, the actual images you would use on AWS right. Would be. I don't know, maybe you'd be using Amazon Linux or maybe you'd be using a different, os entirely.

And is that mainly because you're just not able to deploy the same images you have, uh, in-house? 

[00:46:03] **Alvaro:** So in, in, in general, uh, this is kind of like very hard to to explain, but, but, uh, if, if we would have to deploy code to a, machine and that machine would, would, would be accessed by people who are not like meta employees and we have no way of getting them to sign NDAs then we would not deploy meta code into that machine.

Uh, because that's Sorry. No, not Pi PI's personal information. I was, uh, ip, sorry, that's that's the word. Yeah. Yeah. 

[00:46:31] **Jeremy:** So, okay. So if there's, so if you're in public cloud, there's certain things that you just won't put there just because. Those are only allowed to run on Metas own infrastructure.

[00:46:44] **Alvaro:** Yeah 


## Meta's bootcamp

[00:46:44] **Jeremy:** Earlier you were talking about Instagram was an acquisition and they were in AWS were, were you there at the time or you joined, after? 

[00:46:54] **Alvaro:** No, I joined. I joined after I joined to, to meta. The way that Meta does hiring, at least for my area, is that you get hired as a production engineer, but you don't get assigned to a team.

So you go through a process called boot camp where you get to try different teams and figure out what things you like. I try a couple of different teams, turns out that I like it to work at the Instagram. 

[00:47:15] **Jeremy:** And so at that time they were already running on Facebook's internal infrastructure and they had migrated off of AWS

[00:47:24] **Alvaro:** We were on the process of finishing that migration. 

[00:47:28] **Jeremy:** So by the time you were there, yeah. Basically get, getting everything out of AWS and then into meta's internal. 

[00:47:35] **Alvaro:** Yeah. And, and, and everything is, is a very hard terms to, to define. Uh, I would say like, like most of all, like the bulk of things we were putting it in inside, like, at least what we call our Django servers.

Like they were all just moving into internal infrastructure. 


## How Anita started

[00:47:52] **Jeremy:** This kind of touches on the, the whole boot camp thing, but, Anita, I saw that you, you interned at Facebook and then you took a position there, when you ended up taking a position, I'm kind of curious what were the different projects you looked at or, or how did you end up settling on the one you chose?

[00:48:11] **Anita:** Yeah, I interned, um, and I joined straight out of university. I went into bootcamp similar to Alvaro and I got the chance to explore several different teams. I knew I was never gonna do UI that was just like not my thing. Um, so I focused, uh, my search on all like backend infrastructure teams. Um, obviously security, uh, was one of them because that's the team I was in interning on.

Um, I also explored, the kind of testing infra team. we call it sandcastle. It runs our internal like unit tests and things. and I also explored one of the, ads infrastructure backend teams. so it was mainly just, you know, getting to know the people, um, seeing which projects appealed to me the most.

Um, and then, you know, I kind of chose based on that, I, I think I've always chosen. My work based on how interesting the project sounded, uh, which has worked out in my favor as far as I could tell.


## How Alvaro started

[00:49:14] **Jeremy:** How, how about, you Alvaro what were the, the different projects you looked at when you first started? 

[00:49:20] **Alvaro:** So, As a PE you do have a more restrictive, uh, number of teams that you can, that you can join.

Uh, like I don't get an option to work in ui. Not that I wanted, but, (laughs) I, I, it's, it's so long ago. Uh, I remember I did look at, um, at MySQL as a team, uh, that was also one of the cool team. Uh, we had at that time, uh, distribute, uh, engine, uh, to, to run work, like if, like celery or something like that. But internally, I really like the constable distribute like workloads, um, and.

I can't remember. I think I did put, come with the Messenger team, that I, I ended up having like a good relationship with their TL their tech lead, uh, but never actually like joined that team. And I believe because she have me have a, a PHP task and it was like, no, I'm not down for doing PHP 

[00:50:20] **Jeremy:** Only Python. Huh? 

[00:50:21] **Alvaro:** Exactly. Python.

Python. Because it's just above C level.


## Psystemd

[00:50:27] **Jeremy:** I mean related to that, you, you started the, the psystemd project. And so I wonder if you could explain what the context behind that was. Like what sparked I need to make this, this library? 

[00:50:41] **Alvaro:** So it's, it's a confluence of two things. The first one, it is like, again, if I see something that doesn't have a Python API for it, I.

Feels the strong urge to create one. I have done this a couple of times, mostly internally, but also externally. that was one. And when, while we were doing the migration, I, I, I honestly, I really hate text processing. So the classical thing was like, if you wanna know if your application's running, you do systemctl, you shell out to systemctl status, then parse the output, find the, find the status column.

Okay. And I didn't like that. And I start reading about like, systemd uh, and I got in contact with the or I saw like the dbus implementation of systemd. And that was, I thought that was a very interesting idea how that opened all the doors. Right? Uh, so I got a demo working like in a couple of hours.

and then I said like, okay, now how do we make this pythonic? And then I created that and I just created, again, just for migrating Instagram. That was the idea. Then, uh, one of the team members who work with Anita, but also one who doesn't work with us anymore, they saw this and said like, Hey, like this looks like a good thing to open source it.

So it was like, sure, like I'm happy to opensource it. So we opensource it and then we went to all System Go, which is a very nice interesting conference that happened in Berlin where like all the head for like user space get together. and, and I talk about it and people seems to like it, and that's the story of that.

[00:52:15] **Jeremy:** And so this was replacing, I guess, like you were saying, a lot of people were shelling out and running cat commands and things like that from their Python scripts. And this was meant to be a layer on top of that. 

[00:52:30] **Alvaro:** Yes. So it, it does a couple of things. So first of all, inspecting the processes or, or like the services, getting that information out.

That's one of the main usage. But also like starting or stopping or like doing all that operations that you want to do. Uh, knowing the state of, of, of services, uh, that's also another thing that people take advantage of. The other thing that people take advantage of is to modify the status of the, of the processes at runtime, like changing properties, like increasing or decreasing the CPU threshold.

because systemd provides a very nice API or interface to modify the cgroups properties that otherwise you would need to kind of understand the tree structure that, uh, that, that whatever. so that's what people tend to use this mostly internally. 

[00:53:23] **Jeremy:** And so it, it sounds like at least on the production engineering side, you're primarily working in, in Python.

is that something that's the teams before were using Python and so everybody just continues using Python? Or is there kind of like more structure or thought put into that? 

[00:53:41] **Alvaro:** I would say the following thing about it, um, like in in general, uh, there's, there's not a direction on which language you should use.

It's pretty natural which language you should use, but with without said, there's not a Potpourri of languages inside of, of meta. most teams use c c plus plus Python and rust and that's it. There's go, that appears every once in a while there. Sorry, I should not talk about this like, like, or talk like this about this, but eh, there are team who are actually like very fond of go and they use it and they contribute a lot to that space.

It's just not. That much, uh, use internally. I have always gravitated towards Python. That has been the language that teach me how to do real coding. and that's the language that got me a job at meta. So I tends to work mostly on that. Yeah. 

[00:54:31] **Anita:** Hey, you forgot hack Alvaro. Our web services. (laughs) 

[00:54:37] **Alvaro:** Yes. Yes. Uh, so I would say like, the most used language at Meta is actually PHP

it's just like used by, by one particular product. That, that is the Facebook product. Yes. So our, our entire web interface, eh, or web stack uses a combination of hack, which is a compiled php, which is better than uncompiled php, also known as vanilla php. Uh, there is a lot of like GraphQL, React, and, I think that's it. 

[00:55:07] **Anita:** Infrastructure is largely like c plus plus Python, and now Rust is getting a huge following as well. 

[00:55:15] **Alvaro:** Yeah. Like, like Rust. Rust is, I I would say it's the fastest growing language inside, inside of Meta.

And the thing is that there is also what you call like the bootstrap problem. Um, there's like today, if I wanted do my python program and I have a function that fails one every three times, I can add a decorator that is retry, that retries every time that something fails for a timeout, right? And that's built in and it's there used and it's documented.

And I can look at source code that uses this to understand how, how works. When you start with a new language, you don't get the things. So people have to build them. So there's the bootstrap problem. 

[00:55:55] **Jeremy:** That's also an opportunity as well, right? Like if you are the ones building sort of the foundations, then you, you have an opportunity to be the ones who have the core libraries that people are, are using every day.

Whereas if a language has been around a while, it's kind of, some of that stuff is already set, right? And you may or may not like the APIs, but that's what people use. So that's what we, that's what we do.

One of the last things I'd kind of like to ask, so Anita, you moved into management in just the last year or two or so, and I'm kind of curious what your experience has. Been like, was that a conscious decision where you wanted to go from engineering, uh, software engineering to management?

Or maybe you could talk a little bit to that. 

[00:56:50] **Anita:** Oh man, it hasn't even been a year yet. I feel like so much time has passed already. Uh, no, I never had any plans to go into management. I love being an engineer. I love being in the code. but, I'd say my, my current manager and uh, my director, you know, who hired me into the Linux user space team, kind of.

Sold me a little bit on the idea of like, Hey, if you wanna like, keep pushing more projects, you wanna build out the team that you wanna see working on these things, um, you can consider going into management, taking it slow in a, what we call a T L M role, which is like a tech lead manager, role where you kind of spend some time doing development, and leading the team while also supporting, the engineers as a manager doing the hiring and the relationship building and things that you do in management.

so that actually worked out quite well for me, despite Alvaro shaking his head at first. I really enjoyed being able to split my time into kind of the key projects that I really wanted to work on, um, while also supporting the engineers and having them build out, um, New features in systemd and kind of getting their own foothold in the community as well.

but I'd say like in the past few months, it's been pretty crazy. I, I probably naively thought that I'd have a little more control over, I don't know. My destiny has a manager and that's like a hundred percent not true. (laughs) Um, you're, you are kind of at both the whims of your engineers and also the people above you.

And you kind of have to strike that balance. But, um, my favorite part still, just being able to hide the nasty stuff away from the engineers, let them focus on their work and enjoy what engineers wanna do best, which is just like coding, designing, and like, you know, doing fun, open source stuff.

[00:58:56] **Alvaro:** I will say like, Anita may laugh about me for, because like she's on the other side, but one thing that I least I find very cool at Meta is that managers are not seen as your boss. Right? They're still like a teammate who just basically has a different roles. This is why like when you're an engineer, you can transition to be a manager and that's, it's not considered a promotion that's considered like a, a like an horizontal step and vice versa, you can come back, right.

from a manager into, into like an engineer. Yeah. 

[00:59:25] **Jeremy:** That was what I would say. And, uh, I guess when you were shaking your head, I'm guessing this means you, you don't wanna become a manager anytime soon. 

[00:59:35] **Alvaro:** So I, I never closed the door on that, but I was checking my head to the work of a tlm. Right. Uh, so the tlm TL stands for Tech Lead and m stands for manager.

so you're basically both, but with the time of only one. So, uh, Anita was able to pull it off. I don't think I would be able to pull up like, double duty on that. 

[00:59:56] **Anita:** Yeah. Unfortunately I support too many people now to do the TL stuff as deeply as I used to, but I still have find some time to code a little bit here and there.

[01:00:09] **Jeremy:** So you were talking a little bit about how things have been crazy the last few months. If, if someone is making the transition into management, like what are the kinds of things that you would tell them to, to look out for or to be aware that's coming? 

[01:00:27] **Anita:** Um, when I, before I transitioned, I talked to a lot of managers about like, oh, what was like, you know, the hardest part about management.

And they all have kind of their own horror story about what happened to them when they transitioned or even like, difficult things that happened to them during management. I'd say don't expect it to be easy. you're gonna make a lot of mistakes usually in like the interpersonal relationship side, and it's really just about learning how to learn from your mistakes, pick back up and do better next time.

I think, um, you know, if people like books, the Making of a Manager by Julie Jo, she was a designer, and also a manager, at then Facebook. She's no longer here. but she has a really good book on like what you can expect when you transition into management. the other thing I'd say is don't go into management without having a management chain that you can really trust.

I'd say that can kind of make or break your first few years as a manager, whether you'll enjoy it or not, or even like whether you'll be able to get through the hard times.

[01:01:42] **Jeremy:** Good point. Yeah. I mean, I think whenever you take on anything new, right? Having the support of the people above you or just around you as well is like, that makes such a big difference, right? Even like the situation can be bad, but if everyone is supportive, then you can, you can get through it.

[01:02:02] **Anita:** Yeah, that's absolutely right.

[01:02:04] **Jeremy:** I think that's a good place to wrap up unless either of you have anything else that you thought we should have talked about.

so if people want to check out what you're working on, what you're up to, um, how can they find you?

[01:02:20] **Anita:** well, I guess we're both on matrix now. Uh, I'm Anita Zha on Matrix, a n i t a z h A. we both have Twitters as well. If you just search up our names. Nope. Yeah, you're on Twitter. Yeah. 

[01:02:36] **Alvaro:** There is an impostor with my name, right? Actually it's not an impostor. It's just me. I just never log into Twitter anymore. 

[01:02:40] **Anita:** We both have Mastodon now as well?

Yes. Fosstodon we're both frequently at conferences as well. what's, what's coming up next? I think it's, uh, devconf cZ in the Czech Republic. and then, uh, all systems go in September. 

[01:02:57] **Alvaro:** You sent something in Canada? 

[01:03:01] **Anita:** Oh, yeah. L F F L F S M M B P F is coming up. That's a, that's more of a kernel conference, though.

[01:03:09] **Alvaro:** An acryonym that is longer than the actual word. Yes. Yeah. 

[01:03:12] **Jeremy:** That's a lot. That's a lot of letters. 

[01:03:14] **Anita:** It's a, it's a mouthful. (laughs) 

[01:03:18] **Jeremy:** That's very neat that you get to, to kind of go to all these different conferences and, and actually get, to meet the people in, in person that are, you know, working with the same things you are and, get to be in the same room.

I think that's a, that's a real privilege. Yeah. 

[01:03:35] **Anita:** Yeah, for sure. 

[01:03:38] **Jeremy:** All right. Well, Anita and Alvaro, thank you so much for chatting with me today. 

[01:03:43] **Alvaro:** Thank you for hosting. 

[01:03:45] **Anita:** Yeah. Thanks for the opportunity. This is a lot of fun. 

</div>