+++
title = "Deployment from Scratch"

description = "Josef Strzibny the author of Deployment from Scratch discusses how to self host applications"

[extra]
episode_url = "https://pinecast.com/listen/725d02a6-7bce-4d38-8796-73e2ae3c702a.mp3"
+++

Josef Strzibny is the author of Deployment from Scratch and a current Fedora contributor. He previously worked on the Developer Experience team at Red Hat.

This episode originally aired on Software Engineering Radio. 

Related Links:
- [Deployment from Scratch](https://deploymentfromscratch.com/)
- [@strzibnyj](https://twitter.com/strzibnyj)
- [systemd](https://www.freedesktop.org/wiki/Software/systemd/)
- [Introduction to Control Groups](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/resource_management_guide/chap-introduction_to_control_groups)
- [SELinux](https://wiki.centos.org/HowTos/SELinux)
- [Fedora](https://getfedora.org/)
- [Rocky Linux](https://rockylinux.org/)
- [Puma](https://puma.io/)
- [AppSignal](https://www.appsignal.com/)
- [Datadog](https://www.datadoghq.com/)
- [Rollbar](https://rollbar.com/)
- [Skylight](https://www.skylight.io/)
- [Bootstrapping a multiplayer server with Elixir at X-Plane](https://elixir-lang.org/blog/2021/07/29/bootstraping-a-multiplayer-server-with-elixir-at-x-plane/)
- [StackExchange Performance](https://stackexchange.com/performance)
- [Chruby](https://github.com/postmodern/chruby)
- [Password Safe](https://pwsafe.org/)
- [Vault](https://www.vaultproject.io/)
- [Rails Custom Credentials](https://guides.rubyonrails.org/security.html#custom-credentials)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** Today, I'm talking to Josef Strzibny.

He's the author of the book deployment from scratch. A fedora contributor. And he previously worked on the developer experience team at red hat. 

Josef welcome to software engineering radio. 

[00:00:13] **Josef:** Uh, thanks for having me. I'm really happy to be here. 

There are a lot of commercial services for hosting applications these days. One that's been around for quite a while is Heroku, but there's also services like render and Netlify. why should a developer learn how to deploy from scratch and why would a developer choose to self host an application 

[00:00:37] **Josef:** I think that as a web engineers and backend engineers, we should know a little bit more how we run our own applications, that we write. but there is also a business case, right?

For a lot of people, this could be, uh, saving money on hosting, especially with managed databases that can go, high in price very quickly. and for people like me, that apart from daily job have also some side project, some little project they want to, start and maybe turn into a successful startup, you know but it's at the beginning, so they don't want to spend too much money on it, you know?

And, I can deploy and, serve my little projects from $5 virtual private servers in the cloud. So I think that's another reason to look into it. And business wise, if you are, let's say a bigger team and you have the money, of course you can afford all these services. But then what happened to me when I was leading a startup, we were at somewhere (?) and people are coming and asking us, we need to self host their application.

We don't trust the cloud. And then if you want to prepare this environment for them to host your application, then you also need to know how to do it. Right? I understand completely get the point of not knowing it because already backend development can be huge.

You know, you can learn so many different databases, languages, whatever, and learning also operations and servers. It can be overwhelming. I want to say you don't have to do it all at once. Just, you know, learn a little bit, uh, and you can improve as you go. Uh, you will not learn everything in a day. 

[00:02:28] **Jeremy:** So it sounds like the very first reason might be to just have a better understanding of, of how your applications are, are running. Because even if you are using a service, ultimately that is going to be running on a bare machine somewhere or run on a virtual machine somewhere. So it could be helpful maybe for just troubleshooting or a better understanding how your application works.

And then there's what you were talking about with some companies want to self-host and, just the cost aspect. 

[00:03:03] **Josef:** Yeah. for me, really, the primary reason would be to understand it because, you know, when I was starting programming, oh, well, first of there was PHP and I, I used some shared hosting thing, just some SFTP. Right. And they would host it for me. It was fine. Then I switched to Ruby on Rails and at the time, uh, people were struggling with deploying it and I was asking myself, so, okay, so you ran rails s like for a server, right. It starts in development, but can you just do that on the server for, for your production? You know, can you just rails server and is that it, or is there more to it? Or when people were talking about, uh, Linux hardening, I was like, okay, but you know, your Linx distribution have some good defaults, right. So why do you need some further hardening? What does it mean? What to change? So for me, I really wanted to know, uh, the reason I wrote this book is that I wanted to like double down on my understanding that I got it right. 

**Jeremy:** Yeah, I can definitely relate in the sense that I've also used Ruby and Ruby on rails as well. And there's this, this huge gap between just learning how to run it in a development environment on your computer versus deploying it onto a server and it's pretty overwhelming. So I think it's, it's really great that, that you're putting together a book that, that really goes into a lot of these things that I think that usually aren't talked about when people are just talking about learning a language. 

[00:04:39] **Josef:** you can imagine that a lot of components you can have into this applications, right? You have one database, maybe you have more databases. Maybe you have a redis key-value store. Uh, then you might have load balancers and all that jazz. And I just want to say that there's one thing I also say in the book, like try to keep it simple. If you can just deploy one server, if you don't need to fulfill some SLE (SLA) uh, uptime, just do the simplest thing first, because you will really understand it. And when there was an error you will know how to fix it because when you make things complex for you, then it will be kind of lost, very quickly. So I try to really make things as simple as possible to stay on top of them.

[00:05:25] **Jeremy:** I think one of the first decisions you have to make, when you're going to self host an application is you have to decide which distribution you're going to use. And there's things like red hat and Ubuntu, and Debian and all these different distributions. And I'm wondering for somebody who just wants to deploy their application, whether that's rails, Django, or anything else, what are the key differences between them and, and how should they choose a distribution?

[00:05:55] **Josef:** if you already know one particular distribution, there's no need to constantly be on the hunt for a more shiny thing, you know, uh, it's more important that you know it well and, uh, you are not lost. Uh, that said there are differences, you know, and there could be a long list from goals and philosophy to who makes it whether community or company, if it's showing distribution or not, lack of support, especially for security updates, uh, the kind of init systems, uh, that is used, the kind of c library that is used packaging format, package manager, and for what I think most people will care about number of packages and the quality or version, right?

Because essentially the distribution is distribution of software. So you care about the software. If you are putting your own stuff, on top of it. you maybe don't care. You just care about it being a Linux distribution and that's it. That's fine. But if you are using more things from the distribution, you might star, start caring a little bit more.

You know, other thing is maybe a support for some mandatory access control or in the, you know, world of Docker, maybe the most minimal image you can get established because you will be building a lot of, a lot of times the, the Docker image from the Docker file. And I would say that two main family of systems that people probably know, uh, ones based on Fedora and those based on Debian, right from Fedora, you have, uh, Red Hat Enterprise Linux, CentOS, uh, Rocky Linux.

And on the Debian side you have Ubuntu which is maybe the most popular cloud distribution right now. And, uh, of course as a Fedora packager I'm kind of, uh, in the fedora world. Right. But if I can, if I can mention two things that I think makes sense or like our advantage to fedora based systems. And I would say one is modular packages because it's traditional systems for a long time or for only one version of particular component like let's say postgresql, uh, or Ruby, uh, for one big version.

So that means, uh, either it worked for you or it didn't, you know, with databases, maybe you could make it work. With ruby and python versions. usually you start looking at some version manager to compile their own version because the version was old or simply not the same, the one your application uses and with modular packages, this changed and now in fedora and RHEL and all this, We now have several options to install. There are like four different versions of postgresql for instance, you know, four different versions of redis, but also different versions of Ruby, python, of course still, you don't get all of the versions you want. So for some people, it still might not work, but I think it's a big step forward because even when I was working at Red Hat, we were working on a product called software collections.

This was kind of trying to solve this thing for enterprise customers, but I don't think it was particularly a good solution. So I'm quite happy about this modularity effort, you know, and I think the modular packages, I look into them recently are, are very better, but I will say one thing don't expect to use them in a way you use your regular version manager for development.

So, if you want to be switching between versions of different projects, that's not the use case for them, at least as I understand it, not for now, you know, but for server that's fine. And the second, second good advantage of Fedora based system, I think is good initial SELinux profile settings, you know, SE Linux is security enhanced Linux.

What it really is, is a mandatory access control. So, on usual distribution, you have a discrete permissions that you set that user set themselves on their directories and files, you know, but this mandatory access control means that it's kind of a profile that is there beforehand, the administrators prepares. And, it's kind of orthogonal to those other security, uh, boundaries you have there. So that will help you to protect your most vulnerable, uh, processes because especially with SELinux, there are several modes. So there is, uh, MLS (?) mode for like that maybe an army would use, you know, but for what we use, what's like the default, uh, it's uh, something called targeted policy.

And that means you are targeting the vulnerable processes. So that means your services that we are exposing to external world, like whether it's SSH, postgresql, nginx, all those things. So you have a special profile for them. And if someone, some, attacker takes over, of your one component, one process, they still cannot do much more than what the component was, uh, kind of prepared to do.

I think it's really good that you have this high-quality settings already made because other distributions, they might actually be able to run with SELinux. But they don't necessarily provide you any starting points. You will have to do all your policies yourself. And SELinux is actually a quite complex system, you know, it's difficult.

It's even difficult to use it as a user. Kind of, if you see some tutorials for CentOS, uh, you will see a lot of people mentioned SELinux maybe even turning it off, there's this struggle, you know, and that's why I also, use and write like one big chapter on SELinux to get people more familiar and less scared about using it and running with it.

[00:12:00] **Jeremy:** So SELinux is, it sounds like it's basically something where you have these different profiles for different types of applications. You mentioned SSH, for example, um, maybe there could be one for nginx or, or one for Postgres. And they're basically these collections of permissions that a process should be able to have access to whether that's, network ports or, file system permissions, things like that.

And they're, they're kind of all pre-packaged for you. So you're saying that if you are using a fedora based distribution, you could, you could say that, I want SSH to be allowed. So I'm going to turn on this profile, or I want nginx to be used on this system. So I'm going to turn on this profile and those permissions are just going to be applied to the process that that needs it is that is that correct?

[00:12:54] **Josef:** Well, actually in the base system, there will be already a set of base settings that are loaded, you know, and you can make your own, uh, policy models that you can load. but essentially it works in a way that, uh, what's not really permitted and allowed is disallowed.

that's why it can be a pain in the ass. And as you said, you are completely correct. You can imagine it as um nginx as a reverse proxy, communicating with Puma application server via Unix socket, right? And now nginx will need to have access to that socket to be even being able to write to a Unix socket and so on.

So things like that. Uh, but luckily you don't have to know all these things, because it's really difficult, especially if you're starting up. Uh, so there are set of tools and utilities that will help you to use SELinux in a very convenient way. So what you, what you do, what I will suggest you to do is to run SELinux in a permissive mode, which means that, uh, it logs any kind of violations that application does against your base system policies, right?

So you will have them in the log, but everything will work. Your application will work. So we don't have to worry about it. And after some time running your application, you've ran these utilities to analyze these logs and these violations, and they can even generate a profile for you. So you will know, okay, this is the profile I need.

This is the access to things I need to add. once after you do that, if, if there will be some problems with your process, if, if some article will try to do something else, they will be denied.

That action is simply not happening. Yeah. But because of the utilities, you can kind of almost automate how, how you make a profile and that way is much, much easier.

Yeah. 

[00:14:54] **Jeremy:** So, basically the, the operating system, it comes with all these defaults of things that you're allowed to do and not allowed to do, you turn on this permissive flag and it logs all the things that it would have blocked if you, were enforcing SELinux. And then you can basically go in and add the things that are, that are missing.

[00:15:14] **Josef:** Yes exactly right. 

[00:15:16] **Jeremy:** the, next thing I'd like to go into is, one of the things you talk about in the book is about how your services, your, your application, how it runs, uh, as, as daemons. And I wonder if you could define what a daemon is?

[00:15:33] **Josef:** Uh, you can think about them as a, as a background process, you know, something that continuously runs In the background. Even if the virtual machine goes down and you reboot, you just want them again to be restarted and just run at all times the system is running.

[00:15:52] **Jeremy:** And for things like an application you write or for a database, should the application itself know how to run itself in the background or is that the responsibility of some operating system level process manager?

[00:16:08] **Josef:** uh, every Linux operating system has actually, uh, so-called init system, it's actually the second process after the Linux kernel that started on their system, it has a process ID of one. And it's essentially the parent of all your processes because on Linux, you have always parents and children. Because you use forking to make new, make new processes. And so this is your system process manager, but obviously systemd if it's your system process manager, you already trusted with all the systems services, you can also trust them with your application, right? I mean, who else would you trust even if you choose some other purchase manager, because there are many, essentially you would have to wrap up that process manager being a systemd service, because otherwise there is, you wouldn't have this connection of systemd being a supreme supervisor of your application, right?

When, uh, one of your services struggle, uh, you want it to be restarted and continue. So that's what a systemd could do for you. If you, you kind of design everything as a systemd service, for base packages like base postgresql they've already come with a systemd services, very easy to use. You just simply start it and it's running, you know, and then for your application, uh, you would write a systemd service, which is a little file.

There are some directives it's kind of a very simple and straightforward, uh, because before, before systemd people were using the services with bash and it was kind of error prone, but now with systemd it's quite simple. They're just a set of directives, uh, that you learn. you tell systemd, you know, under what user you should run, uh, what working directory you want it to be running with.

Uh, is there a environment file? Is there a pidfile? And then, uh, A few other things. The most important being a directive called ExecStart, which tells systemd what process to start, it will start a process and it will simply oversee oversee it and will look at errors and so on. 

[00:18:32] **Jeremy:** So in the past, I know there used to be applications that were written where the application itself would background itself. And basically that would allow you to run it in the background without something like a systemd. And so it sounds like now, what you should do instead is have your application be built to just run in the foreground.

and your process manager, like systemd can be configured to, um, handle restarting it, which user is running it. environment variables, all sorts of different things that in the past, you might've had to write in your own bash script or write into the application itself.

[00:19:14] **Josef:** And there's also some. other niceties about systemd because for example, you can, you can define how reloading should work. So for instance, you've just changed some configuration and you've want to achieve some kind of zero downtime, ah, change, zero downtime deploy, you know, uh, you can tell systemd how this could be achieved with your process and if it cannot be achieved, uh, because for instance, uh, Puma application server.

It can fork processes, and it can actually, it can restart those processes in a way that it will be zero downtime, but when you want to change to evolve (?) Puma process. So what do you do, right? And uh systemd have this nice uh thing called, uh, socket activation. And with system socket activation, you can make another unit.

Uh, it's not a service unit. It's a socket unit there are many kinds of units in systemd. And, uh, you will basically make a socket unit that would listen to those connections and then pass them to the application. So while application is just starting and then it could be a completely normal restart, which means stopping, starting, uh, then it will keep the connections open, keep the sockets open and then pass them. when the application is ready to, to process them.

[00:20:42] **Jeremy:** So it sounds like if, and the socket you're referring to these would be TCP sockets, for example, of someone trying to access a website.

[00:20:53] **Josef:** Yes, but actually worked with Unix. Uh, socket as well. Okay. 

[00:20:58] **Jeremy:** so in, in that example, Um, let's say a user is trying to go to a website and your service is currently down. You can actually configure systemd to, let the user connect and, and wait for another application to come back up and then hand that connection off to the application once it's, once it's back up.

[00:21:20] **Josef:** yes, exactly. That, yeah. 

[00:21:23] **Jeremy:** you're basically able to remove some of the complexity out of the applications themselves for some of these special cases and, and offload those to, to systemd.

[00:21:34] **Josef:** because yeah, otherwise you would actually need a second server, right? Uh, you will have to, uh, start second server, move traffic there and upgrade or update your first server. And exchange them back and with systemd socket activation you can avoid doing that and still have this final effect of zero downtime deployment. 

[00:21:58] **Jeremy:** So the, this, this introduction of systemd as the process manager, I think there's, this happened a few years ago where a lot of Linux distributions moved to using systemd and there, there was some, I suppose, controversy around that. And I'm kind of wondering, um, if you have any perspective on, on why there's some people who, really didn't want that to happen, know, why, why that's something people should worry about or, or, or not.

[00:22:30] **Josef:** Yeah. there were, I think there were few things, One one was for instance, the system logging that suddenly became a binary format and you need a special utility to, to read it. You know, I mean, it's more efficient, it's in a way better, but it's not plain text rich, all administrators prefer or are used to. So I understand the concern, you know, but it's kind of like, it's fine.

You know, at least to me, it it's fine. And the second, the second thing that people consistently force some kind of system creep because uh systemd is trying to do more and more every year. So, some people say it's not the Unix way, uh systemd should be very minimal in its system and not do anything else.

It's it's partially true, but at the same time, the things that systemd went into, you know, I think they are essentially easier and nice to use. And this is the system, the services I can say. I certainly prefer how it's done now, 

[00:23:39] **Jeremy:** Yeah. So it sounds like we've been talking about systemd as being this process manager, when the operating system first boots systemd starts, and then it's responsible for starting, your applications or other applications running on the same machine. Uh, but then it's also doing all sorts of other things.

Like you talked about that, that socket activation use case, there's logging. I think there's also, scheduled jobs. There's like all sorts of other things that are part of systemd and that's where some people, disagree on whether it should be one application that's handling all these things.

[00:24:20] **Josef:** Yeah. Yeah. Uh, you're right with the scheduling job, like replacing Cron, you have, now two ways how to do it. But, you can still pretty much choose, what you use, I mean, I still use Cron, so I don't see a trouble there. we'll see. We'll see how it goes. 

[00:24:40] **Jeremy:** One of the things I remember I struggled with a little bit when I was learning to deploy applications is when you're working locally on your development machine, um, you have to install a language runtime in a lot of cases, whether that's for Ruby or Python, uh, Java, anything like that. And when someone is installing on their own machine, they often use something like a, a version manager, like for example, for Ruby there's rbenv and, for node, for example, there's, there's NVM, there's all sorts of, ways of installing language, run times and managing the versions.

How should someone set up their language runtime on a server? Like, would they use the same tools they use on their development machine or is it something different.

[00:25:32] **Josef:** Yeah. So there are several ways you can do, as I mentioned before, with the modular packages, if you find the version there. I would actually recommend try to do it with the model package because, uh, the thing is it's so easy to install, you know, and it's kind of instant. it takes no time on your server.

It's you just install it. It's a regular package. same is true when building a Docker, uh, docker image, because again, it will be really fast. So if you can use it, I would just use that because it's like kind of convenient, but a lot of people will use some kind of version manager, you know, technically speaking, they can only use the installer part.

Like for instance, chruby with ruby-install to install new versions. Right. but then you would have to reference these full paths to your Ruby and very tedious. So what I personally do, uh, I just really set it up as if I am on a developer workstation, because for me, the mental model of that is very simple.

I use the same thing, you know, and this is true. For instance, when then you are referencing what to start in this ExecStart directive and systedD you know, because you have several choices. For instance, if you need to start Puma, you could be, you could be referencing the address that is like in your user home, .gem, Ruby version number bin Puma, you know, or you can use this version manager, they might have something like chruby-exec, uh, to run with their I (?) version of Ruby, and then you pass it, the actual Puma Puma part, and it will start for you, but what you can also do.

And I think it's kind of beautiful. You can do it is that you can just start bash, uh, with a login shell and then you just give it the bundle exec Puma command that you would use normally after logging. Because if you install it, everything, normally, you know, you have something.

you know, bashprofile that will load that environment that will put the right version of Ruby and suddenly it works.

And I find it very nice. Because even when you are later logging in to your, your, uh, box, you log in as that user as that application user, and suddenly you have all the environment, then it just can start things as you are used to, you know, no problem there. 

[00:28:02] **Jeremy:** yeah, something I've run in into the past is when I would install a language runtime and like you were kind of describing, I would have to type in the, the full path to, to get to the Ruby runtime or the Python runtime. And it sounds like what you're saying is, Just install it like you would on your development machine.

And then in the systemd configuration file, you actually log into a bash shell and, and run your application from the bash shell. So it has access to the, all the same things you would have in an interactive, login environment. Is that, is that right?

[00:28:40] **Josef:** yeah, yeah. That's exactly right. So it will be basically the same thing. And it's kind of easy to reason about it, you know, like you can start with that might be able to change it later to something else, but, it's a nice way of how to do it. 

[00:28:54] **Jeremy:** So you mentioned having a user to run your application. And so I'm wondering how you decide what Linux users should run your applications. Are you creating a separate user for each application you run? Like, how are you making those decisions?

[00:29:16] **Josef:** yes, I am actually making a new user for, for my application. Well, at least for the part of the application, that is the application server and workers, you know, so nginx um, might have own user, postgresql might have his own user, you know, I'm not like trying to consolidate that into one user, but, uh, in terms of rails application, like whatever I run Puma or whenever I run uh sidekiq, that will be part of the one user, you know, application user.

Uh, and I will appropriately set the right access to the directories. Uh, so it's isolated from everything else, 

[00:30:00] **Jeremy:** Something that I've seen also when you are installing Ruby or you're installing some other language runtime, you have. The libraries, like in the case of Ruby there's there's gems. and when you're on your development machine and you install these, these gems, these packages, they, they go into the user's home directory.

And so you're able to install and use them without having let's say, um, sudo or root access. is that something that you carry over to your, your deployments as well, or, or do you store your, your libraries and your gems in some place that's accessible outside of that user? I'm just wondering how you approach it.

[00:30:49] **Josef:** I would actually keep it next to next to my application, this kind of touches maybe the question or where to put your application files on the system. so, uh, there is something called FHS, file system hierarchy standard, you know, that, uh, Linux distributions use, they, of course use it with some little modifications here and there.

And, uh, this standard is basically followed by packagers and enforced in package repositories. Uh, but other than that, it's kind of random, you know, it could be a different path and, uh, it says where certain files should go. So you have /home we have /usr/bin for executables. /var for logs and so on and so on.

And now when you want to put your, your application file somewhere, you are thinking about to put them, right. Uh, you have essentially, I think like three options, for, for one, you can put it to home because it's, as we talked about, I set up a dedicated user for that application. So it could make sense to put it in home.

Why I don't like putting it at home is because there are certain labeling in SELinux that kind of, makes your life more difficult. it's not meant to be there, uh, essentially on some other system. Uh, without SELinux, I think it works quite fine. I also did before, you know, it's not like you cannot do it.

You can, uh, then you have, the, kind of your web server default location. You know, like /usr/share/nginx/html, or /var/www, and these systems will be prepared for you with all these SELinux labeling. So when you put files there, uh, things will mostly work, but, and I also saw a lot of people do that because this particular reason, what I don't like about it is that if nginx is just my reverse proxy, you know, uh, it's not that I am serving the files from there.

So I don't like the location for this reason. If it will be just static website, absolutely put it there that's the best location. then you can put it to some arbitrary location, some new one, that's not conflicting with anything else. You know, if you want to follow the a file system hierarchy standard, you put it to /srv, you know, and then maybe slash the name of the application or your domain name, hostname you can choose, what you like.

Uh, so that's what I do now. I simply do it from scratch to this location. And, uh, as part of the SELinux, I simply make a model, make a, make a profile, uh, an hour, all this paths to work. And So to answer your question where I would put this, uh, gems would actually go to this, to this directory, it will be like /apps/gems, for instance.

there's a few different places people could put their application, they could put it in the user's home folder, but you were saying because of the built-in SELinux rules SELinux is going to basically fight you on that and prevent you from doing a lot of things in that folder.

[00:34:22] **Jeremy:** what you've chosen to do is to, to create your own folder, that I guess you described it as being somewhat arbitrary, just being a folder that you consistently are going to use in all your projects. And then you're going to configure SELinux to allow you to run, uh, whatever you want to run from this, this custom folder that you've decided.

[00:34:44] **Josef:** Yeah, you can say that you do almost the same amount of work for home or some other location I simply find it cleaner to do it this way and in a way. I even fulfilled the FHS, uh, suggestion, to put it to /srv but, uh, yeah, it's completely arbitrary. You can choose anything else. Uh, sysadmins choose www or whatever they like, and it's fine.

It'll work. There's there's no problem. There. And, uh, and for the gems, actually, they could be in home, you know, but I just instruct bundler to put it to that location next to my application. 

[00:35:27] **Jeremy:** Okay. Rather than, than having a common folder for multiple applications to pull your libraries or your gems from, uh, you have it installed in the same place as the application. And that just keeps all your dependencies in the same place.

[00:35:44] **Josef:** Yep, 

[00:35:45] **Jeremy:** and the example you're giving, you're, you're putting everything in /srv/ and then maybe the name of your application. Is that right? 

[00:35:55] **Josef:** Yeah. 

[00:35:55] **Jeremy:** Ok. Yeah. Cause I've, I've noticed that, Just looking at different systems. I've seen people install things into /opt. installed into /srv and it can just be kind of, tricky as, as somebody who's starting out to know, where am I supposed to put this stuff?

So, so basically it sounds like just, just pick a place and, um, at least if it's in slash srv then sysadmins who are familiar with, the, the standard file system hierarchy will will know to, to look at.

[00:36:27] **Josef:** yeah. Yeah. opt is also a yeah, common location, as you say, or, you know, if it's actually a packaged web application fedora it can even be in /usr/share, you know? So, uh, it might not be necessarily in locations we talked about before 

one of the things you cover in the book is. Setting up a deployment system and you're using, shell scripts in the case of the book. And I was wondering how you decide when shell scripts are sufficient and when you should consider more specialized tools like Ansible or chef puppet, things like.

[00:37:07] **Josef:** yeah, I chose bash in the book because you get to see things without obstructions. You know, if I would be using, let's say Ansible and suddenly we are writing some YAML files and, uh, you are using a lot of, lot of Python modules to Ansible use and you don't really know what's going on at all times. So you learn to do things with ansible 2.0, let's say, and then new ansible comes out and you have to rely on what you did, you know, and I've got to rewrite the book. Uh, but the thing is that, with just Bash I can show, literally just bash commands, like, okay, you run this and this happens, And, another thing uh why I use it is that you realize how simple something can be.

Like, you can have a typical cluster with sssh, uh, and whatever in maybe 20 bash commands around that, so it's not necessarily that difficult and, uh, it's much easier to actually understand it if it's just those 20, uh, 20 bash comments. Uh, I also think that learning a little bit more about bash is actually quite beneficial because you encounter them in various places.

I mean, RPM spec files, like the packages are built. That's bash, you know, language version managers, uh, like pyenv rbenv that's bash. If you want to tweak it, if you have a bug there, you might look into source code and try to fix it. You know, it will be bash. Then Docker files are essentially bash, you know, their entry points scripts might be bash.

So it's not like you can avoid bash. So maybe learning a little bit. Just a little bit more than, you know, and be a little bit more comfortable. I think it can get you a long way because even I am not some bash programmer, you know, I would never call myself like that. also consider this like, uh, you can have full featured rails application, maybe in 200 lines of bash code up and running somewhere.

You can understand it in a afternoon, so for a small deployment, I think it's quite refreshing to use bash and some people miss out on not just doing the first simple thing possible that they can do, but obviously when you go like more team members, more complex applications or a suite of applications, things get difficult, very fast with bash.

So obviously most people will end up with some higher level too. It can be Ansible. Uh, it can be chef, it might be Kubernetes, you know, so, uh, my philosophy, uh, again, it's just to keep it simple. If I can do something with bash and it's like. 100 lines, I will do this bash because when I come back to it in, after three years, it will work and I can directly see what I have to fix.

You know, if there's a postgresql update at this new location whatever, I, I immediately know what to look and what to change. And, uh, with high-level tooling, you kind of have to stay on top of them, the new versions and, updates. So that's the best is very limited, but, uh, it's kind of refreshing for very small deployment you want to do for your side project. 

[00:40:29] **Jeremy:** Yeah. So it sounds like from a learning perspective, it's beneficial because you can see line by line and it's code you wrote and you know exactly what each thing does. Uh, but also it sounds like when you have a project that's relatively small, maybe there, there aren't a lot of different servers or, the deployment process isn't too complicated.

You actually choose to, to start with bash and then only move to, um, something more complicated like Ansible or, or even Kubernetes. once your project has, has gotten to a certain size.

[00:41:03] **Josef:** you, you would see it in the book. I even explain a multiple server deployment using bash uh, where you can actually keep your components like kind of separate. So like your database have its own life cycle has its own deploy script and your load balancer the same And even when you have application servers.

Maybe you have more of them. So the nice thing is that when you first write your first script to provision one server configure one server, then you simply, uh, write another Uh, supervising script, that would call this single script just in the loop and you will change the server variable to change the IP address or something.

And suddenly you can deploy tomorrow. Of course, it's very basic and it's, uh, you know, it doesn't have some, any kind of parallelization to it or whatever, but if you have like three application servers, you can do it and you understand it almost immediately. You know, if you are already a software engineer, there's almost nothing to understand and you can just start and keep going.

[00:42:12] **Jeremy:** And when you're deploying to servers a lot of times, you're dealing with credentials, whether that's private keys, passwords or, keys to third-party APIs. And when you're working with this self hosted environment, working with bash scripts, I was wondering what you use to store your credentials and, and how those are managed.

I use a desktop application called password safe, uh, that can save my passwords and whatever. and you can also put their SSH keys, uh, and so on.

[00:42:49] **Josef:** And then I simply can do a backup of this keys and of this password to some other secure physical location. But basically I don't use any service, uh, online for that. I mean, there are services for that, especially for teams and in clouds, especially the, big clouds they might have their own services for that, but for me personally, again, I just, I just keep it as simple as I can. It's just on my, my computer, maybe my hard disk. And that's it. It's nowhere else. 

[00:43:23] **Jeremy:** So, so would this be a case of where on your local machine, for example, you might have a file that defines all the environment variables for each server. you don't check that into your source code repository, but when you run your bash scripts, maybe read from that file and, use that in deploying to the server?

[00:43:44] **Josef:** Yeah, Uh, generally speaking. Yes, but I think with rails, uh, there's a nice, uh, nice option to use, their encrypted credentials. So basically then you can commit all these secrets together with your app and the only thing you need to keep to yourself, it's just like one variable. So it's much more easy to store it and keep it safe because it's just like one thing and everything else you keep inside your repository.

I know for sure there are other programs that we have in the same way that can be used with different stacks that doesn't have this baked in, because rails have have it baked in. But if you are using Django, if you are using Elixir, whatever, uh, then they don't have it. But I know that there are some programs I don't remember the names right now, but, uh, they essentially allow you to do exactly the same thing to just commit it to source control, but in a secure way, because it's, encrypted.

[00:44:47] **Jeremy:** Yeah, that's an interesting solution because you always hear about people checking in passwords and keys into their source code repository. And then, you know, it gets exposed online somehow, but, but in this case, like you said, it's, it's encrypted and, only your machine has the key. So, that actually allows you to, to use the source code, to store all that.

[00:45:12] **Josef:** Yeah. I think for teams, you know, for more complex deployments, there are various skills, various tools from HashiCorp vault, you know, to some cloud provider's things, but, uh, you can really start And, keep it very, very simple.

[00:45:27] **Jeremy:** For logging an application that you're, you're self hosting. There's a lot of different managed services that exist. Um, but I was wondering what you use in a self hosted environment and, whether your applications are logging to standard out, whether they're writing to files themselves, I was wondering how you typically approach that.

[00:45:47] **Josef:** Yeah. So there are lots of logs you can have, right from system log, your web server log application log, database log, whatever. and you somehow need to stay on top of them because, uh, when you have one server, it's quite fine to just look in, in and look around. But when there are more servers involved, it's kind of a pain and uh so people will start to look in some centralized logging system.

I think when you are more mature, you will look to things like Datadog, right. Or you will build something of your own on elastic stack. That's what we do on the project I'm working on right now. But I kind of think that there's some upfront costs uh, setting it all up, you know, and in terms of some looking at elastic stack we are essentially building your logging application.

Even you can say, you know, there's a lot of work I also want to say that you don't look into your logs all that often, especially if you set up proper error and performance monitoring, which is what I do with my project is one of the first thing I do.

So those are services like Rollbar and skylight, and there are some that you can self host so if people uh, want to self host them, they can. But I find it kind of easier to, even though I'm self hosting my application to just rely on this hosted solution, uh, like rollbar, skylight, appsignal, you know, and I have to say, especially I started to like appsignal recently because they kind of bundle everything together.

When you have trouble with your self hosting, the last thing you want to find yourself in a situation when your self hosted logs and sources, error reporting also went down. It doesn't work, you know, so although I like self-hosting my, my application.

[00:47:44] **Josef:** I kind of like to offload this responsibility to some hosted hosted providers.

[00:47:50] **Jeremy:** Yeah. So I think that in and of itself is a interesting topic to cover because we've mostly been talking about self hosting, your applications, and you were just saying how logging might be something that's actually better to use a managed service. I was wondering if there's other. Services, for example, CDNs or, or other things where it actually makes more sense for you to let somebody else host it rather than your 

[00:48:20] **Josef:** I think that depends. Logging for me. It's obvious. and then I think a lot of, lots of developers kind of fear databases. So there are they rather have some kind of, one click database you know, replication and all that jazz back then so I think a lot of people would go for a managed database, although it may be one of those pricy services it's also likes one that actually gives you a peace of mind, you know? maybe I would just like point out that even though you get all these automatic backups and so on, maybe you should still try to make your own backup, just for sure. You know, even someone promised something, uh, your data is usually the most valuable thing you have in your application, so you should not lose it.

And some people will go maybe for load balancer, because it's may be easy to start. Like let's say on DigitalOcean, you know, uh, you just click it and it's there. But if you've got opposite direction, if you, for instance, decide to, uh, self host your uh load balancer, it can also give you more, options what to do with that, right?

Because, uh, you can configure it differently. You can even configure it to be a backup server. If all of your application servers go down. Which is maybe could be interesting use case, right? If you mess up and your application servers are not running because you are just messing with, with them. 

Suddenly it's okay. Because your load balancers just takes on traffic. Right. And you can do that if it's, if it's your load balancer, the ones hosted are sometimes limited. So I think it comes to also, even if the database is, you know, it's like maybe you use some kind of extension that is simply not available. That kind of makes you, uh, makes you self host something, but if they offer exactly what you want and it's really easy, you know, then maybe you just, you just do it.

And that's why I think I kind of like deploying to uh, virtual machines, uh, in the cloud because you can mix and match all the services do what you want and, uh, you can always change the configurations to fit, to, uh, meet your, meet your needs. And I find that quite, quite nice.

[00:50:39] **Jeremy:** oOne of the things you talk about near the end of your book is how you, you start with a single server. You have the database, the application, the web server, everything on the same machine. And I wonder if you could talk a little bit about how far you can, you can take that one server and why people should consider starting with that approach. 

Uh, I'm not sure. It depends a lot on your application. For instance, I write applications that are quite simple in nature. I don't have so many SQL calls in one page and so on.

[00:51:13] **Josef:** But the applications I worked for before, sometimes they are quite heavy and, you know, even, with little traffic, they suddenly need a more beefy server, you know, so it's a lot about application, but there are certainly a lot of good examples out there. For instance. The team, uh, from X-Plane flight simulator simulator, they just deploy to one, one server, you know, the whole backend all those flying players because it's essentially simple and they even use elixir which is based on BEAM VM, which means it's great for concurrency for distributed systems is great for multiple servers, but it's still deployed to one because it's simple. And they use the second only when they do updates to the service and otherwise they can, they go back to one.

ANother one would be maybe Pieter Levels (?) a maker that already has like a $1 million business. And it's, he has all of his projects on one server, you know, because it's enough, you know why you need to make it complicated. You can go and a very profitable service and you might not leave one server. It's not a problem. Another good example, I think is stackoverflow. They have, I think they have some page when they exactly show you what servers they are running. They have multiple servers, but the thing is they have only a few few servers, you know, so those are the examples that goes against maybe the chant of spinning up hundreds of servers, uh, in the cloud, which you can do.

It's easy, easier when you have to do auto scaling, because you can just go little by little, you know, but, uh, I don't see the point of having more servers. To me. It means more work. If I can do it, if one, I do it. But I would mention one thing to pay attention to, when you are on one server, you don't want suddenly your background workers exhaust all the CPU so that your database cannot serve, uh, your queries anymore right? So for that, I recommend looking into control groups or cgroups on Linux. When you create a simple slice, which is where you define how much CPU power, and how much memory can be used for that service. And then you attach it to, to some processes, you know, and when we are talking about systemd services.

They actually have this one directive, uh, where you specify your, uh, C group slice. And then when you have this worker server and maybe it even forks because it runs some utilities, right? For you to process images or what not, uh, then it will be all contained within that C group. So it will not influence the other services you have and you can say, okay, you know, I give worker service only 20% of my CPU power because I don't care if they make it fast or not.

It's not important. Important is that, uh, every visitor still gets its page, you know, and it's, they are working, uh, waiting for some background processes so they will wait and your service is not going down.

[00:54:34] **Jeremy:** yeah. So it sort of sounds like the difference between if you have a whole bunch of servers, then you have to, Have some way of managing all those servers, whether that's Kubernetes or something else. Whereas, um, an alternative to that is, is having one server or just a few servers, but going a little bit deeper into the capabilities of the operating system, like the C groups you were referring to, where you could, you could specify how much CPU, how much Ram and, and things, for each service on that same machine to use.

So it's kind of. Changing it, I don't know if it's removing work, but it's, it's changing the type of work you do. 

[00:55:16] **Josef:** Yeah, you essentially maybe have to think about it more in a way of this case of splitting the memory or CPU power. Uh, but also it enables you to use, for instance, Unix sockets instead of TCP sockets and they are faster, you know, so in a way it can be also an advantage for you in some cases to actually keep it on one server.

And of course you don't have a network trip so another saving. So to get there, that service will be faster as long as it's running and there's no problem, it will be faster. And for high availability. Yeah. It's a, it's obviously a problem. If you have just one server, but you also have to think about it in more complex way to be high available with all your component components from old balancers to databases, you suddenly have a lot of things.

You know, to take care and that set up might be complex, might be fragile. And maybe you are better off with just one server that you can quickly spin up again. So for instance, there's any problem with your server, you get alert and you simply make a new one, you know, and if you can configure it within 20, 30 minutes, maybe it's not a problem.

Maybe even you are still fulfilling your, uh, service level contract for uptime. So I think if I can go this way, I prefer it simply because it's, it's so much easy to, to think about it. Like that.

[00:56:47] **Jeremy:** This might be a little difficult to, to answer, but when you, you look at the projects where you've self hosted them, versus the projects where you've gone all in on say AWS, and when you're trying to troubleshoot a problem, do you find that it's easier when you're troubleshooting things on a VM that you set up or do you find it easier to troubleshoot when you're working with something that's connecting a bunch of managed services? 

[00:57:20] **Josef:** Oh, absolutely. I find it much easier to debug anything I set on myself, uh, and especially with one server it's even easier, but simply the fact that you build it yourself means that you know how it works. And at any time you can go and fix your problem. You know, this is what I found a problem with services like digital ocean marketplace.

I don't know how they call this self, uh, hosted apps that you can like one click and have your rails django app up, up and running. I actually used when I, uh, wasn't that skilled with Linux and all those things, I use a, another distribution called. A turnkey Linux. It's the same idea. You know, it's like that they pre prepare the profile for you, and then you can just easily run it as if it's a completely hosted thing like heroku, but actually it's your server and you have to pay attention, but I actually don't like it because.

You didn't set it up. You don't know how it's set up. You don't know if it has some problems, some security issues. And especially the people that come for these services then end up running something and they don't know. I believe they don't know because when I was running it, I didn't know. Right. So they are not even know what they are running.

So if you really don't want to care about it, I think it's completely fine. There's nothing wrong with that. But just go for that render or heroku. And make your life easier, you know,

[00:58:55] **Jeremy:** Yeah, it sounds like the solutions where it's like a one-click install on your own infrastructure. you get the bad parts of, of both, like you get the bad parts of having this machine that you need to manage, but you didn't set it up. So you're not really sure how to manage it.

you don't have that team at Amazon who, can fix something for you because ultimately it's still your machine. So That could have some issues there. 

[00:59:20] **Josef:** Yeah. Yeah, exactly. I will. I would recommend it or if you really decide to do it, at least really look inside, you know, try to understand it, try to learn it, then it's fine. But just to spin it up and hope for the best, uh, it's not the way to go 

[00:59:37] **Jeremy:** In, in the book, you, you cover a few different things that you use such as Ruby on rails and nginx, Redis, postgres. Um, I'm assuming that the things you would choose for applications you build in self hosts. You want them to have as little maintenance as possible because you're the one who's responsible for all of it.

I'm wondering if there's any other, applications that you consider a part of your default stack that you can depend on. And, that the, the maintenance burden is, is low. 

[01:00:12] **Josef:** Yeah. So, uh, the exactly right. If I can, I would rather minimize the amount of, uh, dependencies I have. So for instance, I would think twice of using, let's say elastic search, even though I used it before. And it's great for what it can do. Uh, if I can avoid it, maybe I will try to avoid it. You know, you can have descent full text search with Postgres today.

So as long as it would work, I would uh, personally avoid it. Uh, I think one relation, uh, database, and let's say redis is kind of necessary, you know, I I've worked a lot with elixir recently, so we don't use redis for instance. So it's kind of nice that you can limit, uh, limit the number of dependencies by just choosing a different stack.

Although then you have to write your application in a little different way. So sometimes even, yeah. In, in such circumstances today, this could be useful. You know, I, I think, it's not difficult to, to run it, so I don't see, I don't see a problem there. I would just say that with the services, like, uh, elastic search, they might not come with a good authentication option.

For instance, I think asked et cetera, offers it, but not in the free version. You know, so I would just like to say that if you are deploying a component like that, be aware of it, that you cannot just keep it completely open to the world, you know? Uh, and, uh, maybe if you don't want to pay for a version that has it, or maybe are using it at the best, it doesn't have it completely.

You could maybe build out just a little bit tiny proxy. That would just do authentication and pass these records back and forth. This is what you could do, you know, but just not forget that, uh, you might run something unauthenticated.

I was wondering if there is any other, applications or capabilities where you would typically hand off to a managed service rather than, than trying to deal with yourself. 

[01:02:28] **Josef:** Oh, sending emails, not because it's hard. Uh, it's actually surprisingly easy to start sending your own emails, but the problem is, uh, the deliverability part, right? Uh, you want your emails to be delivered and I think it's because of the amount of spam everybody's sending.

It's very difficult to get into people's boxes. You know, you simply be flagged, you have some unknown address, uh, and it would just it would just not work. So actually building up some history of some IP address, it could take a while. It could be very annoying and you don't even know how to debug it. You, you cannot really write Google.

Hey, you know, I'm, I'm just like this nice little server so just consider me. You cannot do that. Uh, so I think kind of a trouble. So I would say for email differently, there's another thing that just go with a hosted option. You might still configure, uh, your server to be sending up emails. That could be useful.

For instance, if you want to do some little thing, like scanning your system, a system log and when you see some troublesome. Logging in all that should, it shouldn't happen or something. And maybe you just want an alert on email to be sent to you that something fishy is going on. And so you, you can still set up even your server, not just your main application and might have a nice library for that, you know, to send that email, but you will still need the so-called relay server. to just pass your email. You. Yeah, because building this trust in an email world, that's not something I would do. And I don't think as a, you know, independent in the maker developer, you can really have resources to do something like that. So will be a perfect, perfect example for that. Yeah.

[01:04:22] **Jeremy:** yeah, I think that's probably a good place to start wrapping up, but is there anything we missed that you think we should have talked about? 

[01:04:31] **Josef:** we kind of covered it. Maybe, maybe we didn't talk much about containers, uh, that a lot of people nowadays, use. uh, maybe I would just like to point out one thing with containers is that you can, again, do just very minimal approach to adopting containers. You know, uh, you don't need to go full on containers at all.

You can just run a little service, maybe your workers in a container. For example, if I want to run something, uh, as part of my application, the ops team, the developers that develop this one component already provide a Docker file. It's very easy way to start, right? Because you just deployed their image and you run it, that's it.

And they don't have to learn what kind of different stack it is, is a Java, is it python, how I would turn it. So maybe you care for your own application, but when you have to just take something that's already made, and it has a Docker image, you just see the nice way to start. And one more thing I would like to mention is that you also don't really need, uh, using services like Docker hub.

You know, most people would use it to host their artifacts that are built images, so they can quickly pull them off and start them on many, many servers and blah, blah. But if you have just one server like me, but you want to use containers. And I think it's to just, you know, push the container directly. 

Essentially, it's just an archive.

And, uh, in that archive, there are few folders that represent the layers. That's the layers you build it. And the Docker file and that's it. You can just move it around like that, and you don't need any external services to run your content around this little service.

[01:06:18] **Jeremy:** Yeah. I think that's a good point because a lot of times when you hear people talking about containers, uh, it's within the context of Kubernetes and you know, that's a whole other thing you have to learn. You have to learn not only, uh, how containers work, but you have to learn how to deploy Kubernetes, how to work with that.

And, uh, I think it's, it's good to remind people that it is possible to, to just choose a few things, run them as containers. Uh, you don't need to. Like you said, even run, everything as containers. You can just try a few things. 

[01:06:55] **Josef:** Yeah, exactly.

[01:06:57] **Jeremy:** Where can people, uh, check out the book and where can they follow you and see what you're up to.

[01:07:04] **Josef:** uh, so they can just go to deploymentfromscratch.com. That's like the homepage for the book. And, uh, if they want to follow up, they can find me on twitter. Uh, that would be, uh, slash S T R Z I B N Y J like, uh, J and I try to put updates there, but also some news from, uh, Ruby, Elixir, Linux world. So they can follow along.

[01:07:42] **Jeremy:** Yeah. I had a chance to, to read through the alpha version of the book and there there's a lot of, really good information in there. I think it's something that I wish I had had when I was first starting out, because there's so much that's not really talked about, like, when you go look online for how to learn Django or how to learn Ruby on Rails or things like that, they teach you how to build the application, how to run it on your, your laptop.

but there's this, this very, large gap between. What you're doing on your laptop and what you need to do to get it running on a server. So I think anybody who's interested in learning more about how to deploy their own application or even how it's done in general. I think they'll find the book really valuable.

[01:08:37] **Josef:** Okay. Yeah. Thank you. Thank you for saying that. Uh, makes me really happy. And as you say, that's the idea I really packed, like kind of everything. You need in that book. And I just use bash so, it's easier to follow and keep it without any abstractions. And then maybe you will learn some other tools and you will apply the concepts, but you can do whatever you want.

[01:09:02] **Jeremy:** All right. Well, Josef thank you, so much for talking to me today.

[01:09:05] **Josef:** Thank you, Jeremy. 

</div>