+++
title = "David Cramer on Application Monitoring with Sentry"

description = "David discusses error tracking with Sentry, the difficulty of instrumenting front-end applications, how Sentry's architecture has evolved, and their reasoning behind switching to the Business Source License"

[extra]
episode_url = "https://pinecast.com/listen/e8ea0061-11b6-457e-bb8a-cb378fb89f76.mp3"
social_title = "David Cramer on Sentry"
social_description = "Intelligent error tracking as a substitute for logs"
+++

Sentry is an application monitoring tool that notifies developers of errors and performance problems. It's intended to surface problems instead of requiring developers to look through logs or dashboards to identify what the problem is.

David Cramer is the co-founder and CTO of Sentry.

This episode originally aired on Software Engineering Radio.

### Topics covered:

- What's Sentry?
- Treating performance problems as errors
- Why you might no need logs
- Identifying common problems in applications and frameworks
- Issues with Open Telemetry data
- Why front-end applications are difficult to instrument
- The evolution of Sentry's architecture
- Switching from a permissive license to the Business Source License

### Related Links

- [Sentry](https://www.sentry.io/)
- [David's Blog](https://cra.mr/)
- [Sentry 9.1 and Upcoming Changes](https://blog.sentry.io/2019/05/14/sentry-9-1-and-upcoming-changes/)
- [Re-Licensing Sentry](https://blog.sentry.io/2019/11/06/relicensing-sentry/)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** Today I'm talking to David Kramer. He's the founder and CTO of Sentry. David, welcome to Software Engineering Radio.

[00:00:08] **David:** Thanks for having me. Excited for today's conversation.


## What's Sentry?

[00:00:11] **Jeremy:** I think the first thing we could start with is defining what Sentry is. I know some people refer to it as an error tracker. Some people have referred to it as, an application performance monitoring tool. I wonder if you could kind of describe in, in your words what it is.

[00:00:30] **David:** You know, as somebody who doesn't work in marketing, I just tell it how it is. So Sentry started out doing error monitoring, which. You know, dependent on who you talk to, you might just think of as logging, right? Like that's the honest truth. It is just logging just a different shape or form. these days it's hard to not classify us as just an APM tool that's like the industry that exists.

It's like the tools people understand. So I would just say it's an APM tool, right? We do a bunch of things within that space, and maybe it's not, you know, item for item the same as say a product like New Relic. but a lot of the overlap's there, so it's like errors performance, which is like latency and sort of throughput.

And then we have some stuff that just goes a little bit deeper within that. The, the one thing i would say that is different for us versus a lot of these tools is we actually only do application monitoring. So we don't do any since like systems or infrastructure monitoring. Meaning Sentry is not gonna tell you when you need to replace a hard drive or even that you need new hard, like more disk space or something like that because it's just, it's a domain that we don't think is relevant for sort of our customers and product.


## Application Performance Monitoring is about finding crashes and performance problems that users would associate with bugs

[00:01:31] **Jeremy:** For people who aren't familiar with the term application performance monitoring, what is that compared to just error tracking?

[00:01:41] **David:** The way I always reason about it, this is what I tell new hires and what I would tell, like my mother, if I had to explain what I do, is like, you load Uber and it crashes. We all know that's bad, right? That's error monitoring. We capture the crash report, we send it to developers. You load Uber and it's a 30 second spinner, like a loading indicator as a customer.

Same outcome for me. I assume the app is broken, right? So we also know that's bad. Um, but that's different than a crash. Okay. Sentry captures that same thing and send it to developers. lastly the third example we use, which is a little bit more. I think, untraditional, but a non-traditional rather, uh, you load the Uber app and it's like a blank screen or there's no button to submit, like log in or something like this.

So it's kind of like a, it's broken, but it maybe isn't erroring and it's not like a slow thing. Right. Same outcome. It's probably a bug of some sorts. Like it's what an end user would describe it as a bug. So for me, APM just translates to there are bugs, user perceived bugs in your application and we're able to monitor and, and help the software teams sort of prioritize and resolve those, those concerns.

[00:02:42] **Jeremy:** Earlier you were talking about actual crashes, and then your second case is, may be more of if the app is running slowly, then that's not necessarily a crash, but it's still something that an APM would monitor.

[00:02:57] **David:** Yeah. Yeah. And I, I think to be fair, APM, historically, it's not a very meaningful term. Like I as a, when I was more of just an individual contributor, I would associate APM to, like, there's a dashboard that will tell me what's slow in my application, which it does. And that is kind of core to APM, but it would also, none of the traditional tools, pre sentry would actually tell you why it's broken, like when there's an error, a crash.

It was like most of those tools were kind of useless. And I don't know, I do actually know, but I'm gonna pretend I don't know about most people and just say for myself. But most of the time my problems are errors. They are not like it's fast or slow, you know? and so we just think of it as like it's a holistic thing to say, when I've changed the application and something's broken, or it's a bug, you know, what is that bug?

How do we help people fix it? And that comes from a lot of different, like data signals and things like that. the end result is still the same. You either are gonna fix it or it's not important and you ignore it. I don't know. So it's a pretty straightforward, premise for us. But again, most companies in the space, like the traditional company is when you grow a big company, what happens is like you build one thing and then you build lots of check boxes to sell more things.

And so I think a lot of the APM vendors, like they've created a lot of different products. Like RUM is a good example of another acronym that lives with an APM. And I would tell you RUM is completely meaningless. It, it stands for real user monitoring. And so I'm like, well, what's not real about monitoring the application?

Well, nothing's not real, but like they created a new category because that's how marketing engines work. And that new category is more like analytics than it is like application telemetry. And it's only because they couldn't collect the app, the application telemetry at the time. And so there's just a lot of fluff, i would say.

But at the end of the day too, like developers or engineering teams, it's like new version of the application. You broke something, let's tell you about it so you can fix it.


## You might not need logging or performance monitoring

[00:04:40] **Jeremy:** And, and so earlier you were saying how this is a kind of logging, but there's also other companies, other products that are considered like logging infrastructure. Like I, I would think of companies like Paper Trail or Log Tail. So what space does Sentry fill that's that's different than that kind of logging?

[00:05:03] **David:** Um, so the way I always think about it, and this is both personally true, and what I advise other folks is when you're building something new, when you start from zero, right, you can often take Sentry put it in, and that's good enough. You don't even need performance monitoring. You just need like errors, right?

Like you're just causing bugs all the time. And you could do that with logging, but like the delta between air monitoring and logging is night and day. From a user experience, like error monitoring for us, or what we built at the very least, aggregates the errors. It, it helps you understand the frequency. It helps you when they're new versus old.

it really gives you a lot of detail where logs don't, and so you don't need logging often. And I will tell you today at Sentry. Engineers do not use logs for the most part. Uh, I had a debate with one of our, our team members about it, like, why does he use logs recently? But you should not need them because logs serve a different purpose.

Like if you have traces which tell you like, like fast and slow in a bunch of other network data and you have this sort of crash report collection or error monitoring thing, logs become like a compliance or an audit trail or like a security forensics, tool, and there's just not a lot of value that you would get out of them otherwise, like once in a while, maybe there's like some weird obscure use case, but generally speaking, you can just pretend that you don't need logs most days.

Um, and to me that's like an evolution of the industry. And so when, when Sentry is getting started, most people were still logs. And if you go talk to SRE teams, they're like, oh, login is what we know. Some of that's changed a little bit, but. But at the end of the day, they should only be needed for more complicated audit trails because they're just not a good solution to the problem.

It's just free form data. Structured or not, doesn't really matter. It's not aggregated. It's not something that you can really use. And it's why whenever you see logging tools, um, not even the papertrails of the world, but the bigger ones like Splunk or Cabana, it's like this weird, what we describe as choose your own adventure.

Like go have fun, build your dashboards and try to make the logs useful kind of story. Whereas like something like Sentry, it's just like, why would you waste any time trying to build dashboards when we can just tell you when something new is broken? Like that's the ideal situation.

[00:06:59] **Jeremy:** So it sounds like maybe the distinction is with a more general logging tool, like you mentioned Splunk and Kibana it's a collection of all this information. of things happening, even though nothing's necessarily wrong, whereas Sentry is more Sentry is it's going to log things, but it's only going to log things if Sentry believes something is wrong, either because of a crash or because of some kind of performance issue.


## People don't want to dig through logs or dashboards, they want to be told when something is wrong and whyMost software is built the same way, so we know common problems

[00:07:28] **David:** Yeah. I, i would say it's about like actionability, right? Like, like nobody wants to spend their time digging through logs, digging through dashboards. Metrics are another good example of this. Like just charts with metrics on them. Yeah. They tell me something's happening. If there's lots of log statements, they tell me something's going on, but they're not, they're not optimized to like, help me solve a problem, right?

And so our philosophy was always like, we haven't necessarily nailed this in all cases for what it's worth, but. It was like, the goal is we identify an actual problem, like close to like a root cause kind of problem, and we escalate that up and that's it. Uh, versus asking somebody to like go have to like build these dashboards, build these things, figure out what data matters and all this because most software looks exactly the same.

Like if you have a web service, it doesn't matter what language it's written in, it doesn't matter how different you think your architecture is from somebody else's, they're all the same. It's like you've got a request, you've got a database, you've got some cache, you've got all these like known, known quantity things, and the slowness comes from the same places.


## Errors are structured while logs are not

[00:08:25] **David:** The errors come from the same places. They're all exhibiting the same kinds of behavior. So logging is very unstructured. And what I mean by that is like there's no schema. Like you can hypothetically like make it JSON and everybody does that, but it's still unstructured. Whereas like errors, it's, it's a tight schema.

It's like there's a type of error, there's a message for the error, there's a stack trace, there's all these things that you know. Right. And as soon as you know and you define those things, you can just build better products. And so distributed tracing is similar. Hypothetically, it's a little bit abstract to be fair, but hypothetically, distributed tracing is creating a schema out of basically network annotations.

And somebody will yell at me for just simplifying it to that. I would tell 'em that's what it is. But, same goal in mind. If you know what the data is, you can take action on it. It's not quite entirely true. Um, because tracing is much more freeform. For example, it doesn't say if you have a SQL statement, it should be like this, it should be formatted this way, things like that.

whereas like stack traces, there's a file name, there's there's a line number, there's like all these things, right? And so that's how I think about the delta between what is useful information and what isn't, I guess. And what allows you to actually build things like Sentry versus just build abstract exploration.


## Inferring problems rather than having user identify them

[00:09:36] **Jeremy:** Kind of paint the picture of how someone would get started with a tool like Sentry. Do they need to tell Sentry anything about their application? Do they need to modify their source code at all? give us a picture of how that works.

[00:09:50] **David:** Yeah, like one of our fundamentals, which I think applies for any real business these days is you've gotta like reduce user friction, right? Like you've gotta make it dead simple to use. Uh, and for us there were, there was like kind of a fundamental driving constraint behind that. So in many situations, um, APM vendors especially will require you to run an agent a basically like some kind of process that runs on your servers somewhere.

Well, if you look at modern tech stacks, that doesn't really work because I don't run the servers half my stuff's in the browser, or it's a mobile app or a desktop app, and. Even if I do have those servers, it's like an entirely different team that controls them. So deploying like a sidecar, an agent is actually like much more complicated.

And so we, we looked at that and also because like, it's much easier to have control if you just ship within the application. We're like, okay, let's build like an SDK and dependency that just injects into the, the application that runs, set an API key and then you're done. And so what that translates for Sentry is we spend a lot of time knowing what Django is or what Rails is or what expresses like all these frameworks.

And just knowing how to plug into the right signals in those frameworks. And then at that point, like the user doesn't have to do anything. And so like the ideal outcome for Sentry is like you install the dependency in whatever language makes sense, right? You somehow configure the API key and maybe there's a couple other minor settings you add and that gives you the bare bones and that's it.

Like it should just work from there. Now there's a lot you can do on top of that to enrich data and whatnot, but for the most part, especially for errors, like that's good enough. And that, that's always been a fundamental goal of ours. And I, I think we actually do it phenomenally well.

[00:11:23] **Jeremy:** So it sounds like it infers things about the application without manual configuration. Can you give some examples of the kind of things that Sentry knows without the user having to tell it?

[00:11:38] **David:** Yeah. So a good example. So on the errors side, we know literally everything because an error object in each language has all these attributes with it. It, it gives you the stack trace, it gives you a lot of these things. So that one's straightforward. On the performance side, we use a combination of leveraging some like open source, I guess implementations, like open telemetry where it's got all this instrumentation already and we can just soak that in, um, as well as we automatically instrument a bunch of stuff.

So for example, say you've got like a Python application and you're using, let's say like SQL Alchemy or something. I don't actually know if this is how our SDK works right now, but, we will build something that's aware of that library and make sure it can automatically instrument the things it needs to get the right information out of it.

And be fair. That's always been true for like APM vendors and stuff like that. The delta is, we've often gone a lot deeper. And so for Python for example, you plug it into an application, we'll capture things like the error, error object, which is like exception class name exception value, right? Stack trace, file, name, line number, all those normal things,

function name. We'll also collect source code. So we'll, we'll give you sort of surrounding source code blocks for each line in the stack trace, which makes it infinitely easier to consume. And then in Python and, and php, and I forget if we do this anywhere else right now, we'll actually even allow you to collect what are called stack locals.

So it'll, it'll give you basically the variables that are defined almost like a debugger. And that is actually, actually like game changing from a development point of view. Because if I can go look in production when there's an incident or a bug and I can actually see the state of the application. , I, I never need to know like, oh, what was going on here?

Oh, what if like, do I need to go reproduce this somehow? I always have the right information. And so all of that for us is automatic and we only succeed like, it, it's, it's like by definition inside of Sentry, it has to be automatic. Like if we ask the user to do anything whatsoever, we're failing. And so whenever we design any product or anything, and to be fair, this is how every product company should operate.

it's gotta be with as little user input as humanly possible. And so you can't always pull that off. Sometimes you have to have users configure stuff, but the goal should always be no input.


## Detecting errors through unhandled exceptions

[00:13:42] **Jeremy:** So you, you're talking about getting a stack trace, getting, the state of variables, source code. That sounds like that's primarily gonna be through unhandled exceptions. Would you say that's, that's the primary way that you get error?

[00:13:58] **David:** Yeah, you can integrate in other ways. So you can like trigger our API to capture an, uh, an exception. You can also, for better or worse, it's not always good. You can integrate through logging adapters. So if you're already using a logging framework and you log their errors there, we can often capture those.

However, I will say in most cases, people use the logging APIs wrong and the data becomes junk. A good, a good example of this is like, uh, it varies per language. So I'm just gonna go to Python because Python is like sort of core to Sentry. Um, in Python you have the ability to log messages, you can log them as errors, you can log like actual error objects as errors.

But what usually happens is somebody does a try-catch. They, they capture the error they rescue from it. They create a logging call, like log dot error or something, put the, the error message or value in there. And then they send that upstream. And what happens is the stack trace is gone because we don't know that it's an error object.

And so for example, in Python, there's actually an an A flag. You pass the logging call to make sure that stack trace stays present. But if you don't know that the data becomes junk all of a sudden, and if we don't have a stack trace, we can't actually aggregate data because like there's just not enough information to like, to run hashing on it.

And so, so there are a lot of ways, I guess, to capture the information, but there are like good ways and there are bad ways and I think it, it's in everybody's benefit when they design their, their apt to like build some of these abstractions. And so like as an example, when, whenever I would start a new project these days, I will add some kind of helper function for me to like log an exception when I like, try catch and then I can just plug in whatever I need later if I want to enrich the data or if I wanna send that to Sentry manually or send it to logs manually.

And it just makes life a lot easier versus having to go back and like augment every single call in the code base.

[00:15:37] **Jeremy:** So it, it sounds like. When you're using a tool like Sentry, there's gonna be the, the unhandled exceptions, which are ones that you weren't expecting. So those should I guess happen without you catching them. And then the ones that you perhaps do anticipate, but you still consider to be a problem, you would catch that and then you would add some kind of logging statement to your code that talks to Sentry directly.


## Finding issues like performance problems (N+1 queries) that are not explicit errorsz

[00:16:05] **David:** Potentially. Yeah. It becomes a, a personal choice to be fair at that, at that point. but yeah, the, the way, one of the ways we've been thinking about this lately, because we've been changing our error monitoring product to not just be about errors, so we call it issues, and that's in the guise of like, it's like an issue tracker, a bug tracker.

And so we started, we started putting what are effectively like, almost like static analysis concerns inside of this issue tracker. So for example, In our performance monitor, we'll do something called like detect n plus one queries, which is where you execute a, a duplicate query in a loop. It's not necessarily an error.

It might not be causing a problem, but it could be causing a problem in the future. But it's like, you know, the, the, the qualities of it are not the same as an error. Like it's not necessarily causing the user to experience a bug. And so we've started thinking more about this, and, and this is the same as like logging errors that you handle.

It's like, well, they're not really, they're not really bugs. It's like expected behavior, but maybe you still want to keep it like tracking somewhere. And I think about like, you know, Lins and things like that, where it's like, well, I've got some things that I definitely should be fixing. Then I've got a bunch of other stuff that's like informing me that maybe I should take action on or not.

But only I, the human can really know at the end of the day, right, if I, if I should prioritize that or not. And so that's how I kind of think about like, if I'm gonna try catch and then log. Yeah, you should probably collect that data. It's probably less important than like the, these other concerns, like, like an actual unhandled exception.

But you do, you do want to know that they're happening and whatnot. And so, I dunno, Sentry has not had a strong opinion on this historically. We're just like, send us whatever you want to capture in this regard, and you can pay for it, that's fine. It's like usage based, you know? we're starting to think a lot more about what should that look like if we, if we go back to like, what's the, what's the opinion we have for how you should use the product or how you should solve these kinds of software problems.

[00:17:46] **Jeremy:** So you gave the example of detecting n plus one queries is, is that like being aware of the framework or the ORM the person is using and that's how you're determining this? Or is it at more of a lower level than that? 

[00:18:03] **David:** it is, yeah. It's at the framework level. So this is actually where Open Telemetry causes a lot of harm, uh, for us because we need to know what a database query is. Uh, we need to know like the structure of the query because we actually wanna parse it out in a lot of cases. Cause we actually need to identify if it's duplicate, right?

And we need to know that it's a database query, not a random annotation that you've added. Um, and so what we do is within these traces, which is like if you, if you don't know what a trace is, it's basically just like, it's a tree, like a tree structure. So it's like A calls B, calls C, B also calls D and E and et cetera, right?

And so you just, you know, it's a trace. Um, and so we actually just look at that trace data. We try to find these patterns, which is like, okay, B was a, a SQL query or something. And every single sibling of B is that same SQL query, but sort of removing certain parameters and stuff for the value. So we'll look at that data and we'll try to pull out anomalies.

So m plus one is an example of like a fairly obvious anti pattern that everybody knows is bad and can be optimized. Uh, but there's a lot of other that are a little bit more subjective. I'll give you an example. If you execute three SQL statements back to back, one could argue that you could just batch those SQL statements together.

I would argue most of the time it doesn't matter and I don't need to do that. And also it's not guaranteed that that is better. So it becomes much more like, well, in my particular situation this is valuable, but in this other situation it might not be. And that's where I go back to like, it's almost like a linter, you know?

But we're trying to infer all of that from the data stream. So, so Sentry's kind of, we're kind of a backwards product company. So we build our product from a technology vision, not from customers want this, or we have this great product vision or anything like that. And so in our case, the technology vision is like, there's a lot of application data that comes in, a lot of telemetry, right?

Errors, traces. We have a bunch of other streams now. within that telemetry there is like signal. And so one, it's all structured data so we know what it is so we can actually interpret it. And then we can identify that signal that might be a problem. And that signal in our case is often going to translate to like this issue concept.

And then the goal is like, well, can we identify these problems for people and surface them versus the choose your own adventure model, which is like, we'll just capture everything and feed it to the user and they can figure out what matters. Because again, a web service is a web service. A database is a database.

They're all the same problems for everybody. All you know, it's just, and so that's kind of the model we've built and are continuing to evolve on and, and so far works pretty well to, to curate a lot of these workflows.

## Want to infer everything, but there are challenges

[00:20:26] **Jeremy:** You talked a little bit about how people will sometimes use tracing. And in cases like that, they may need some kind of session ID to track. Somebody making a call to a service and that talks to a database and that talks to other services. And you, inside of your application, you have to instrument some way of tracking.

This all came from this one request. Is that something that Sentry can infer or is there something that the developer has to put into play so that you can track that sort of thing?

[00:21:01] **David:** Yeah, so it's, it's like a bit of both. And i would say our goal is that we can infer everything. The reality is there is so much complexity and there's too much of a, like, too many technologies in the world. Like I was complaining about this the other day, like, the classic example on web service is if we have a middleware hook, We kind of know request response, usually that's how middleware would work, right?

And so we can infer a lot from there. Like basically we can infer the boundaries, which is a really big deal. Okay. That's one thing is boundaries is a problem. What we, we describe that as a transaction. So like when the request starts. When the request ends, right? That's a very important boundary for everybody to understand because when I'm working on the api, I care about the API boundary.

I actually don't care about what the database is doing at its low level or what the JavaScript application might be doing above it. I want my boundary. So that's one that we kind of can do. But it's hard in a lot of situations because of the way frameworks and technology has been designed, but at least traditional stuff like a, a traditional web stack, it works like a Rails app or a DDjango app or PHP app kind of thing, right?

And then within that it becomes, well, how do you actually build a trace versus just have a bunch of arbitrary labels? And so we have a bunch of complicated tech within each language that tries to establish that tree. and then we annotate a lot of things along the way. And so we will either leverage Open Telemetry, which is an open format spec that ideally has very high quality data.

Ideally, not realistically, but ideally it has high quality data. Every library author implements it great, everybody's happy. We don't have to do anything ever again. The reality is that data is like all over the map because there's not like strict requirements for what, how the data should be labeled and stuff.

And not everything even has that data. Like not everything's instrumented with open telemetry. So we also have a bunch of stuff that, unrelated to using that we'll say, okay, we know what this library is, we're gonna try to infer some characteristics from this library, or we know what maybe like the DDjango template engine is.

So we're gonna try to infer like when the template renders so you can capture that block of information. it is a very imperfect science and I would tell you like it's not, even though like Open Telemetry is a very fun topic for people. It is not necessarily good, like it's not in a good state. Could will it ever be good?

I don't know in all honesty, but like the data quality is like all over the map and so that's honestly one of our biggest challenges to making this experience that, you know, tells you what's going on in your database so it tells you what's going on with the cash or things like this is like, I dunno, the cash might be called something completely random in one implementation and something totally different in another.

And so it's a lot of like, like data normalization that you have to deal with. But for the most part, those libraries of things you don't control can and will be instrumented. Now the other interesting thing, which we'll see how this works out, so, so one thing Sentry tries to do there, we have all these layers of telemetry, so we have errors and traces, right?

Those are pretty high level concepts. We also have profiling data, which is very, very, very, very low level. So it's usually only if you have like disc. I like. It's where is all the CPU time being spent in my application? Mostly not waiting. Like waiting's usually like a network call, right? But it's like, okay, I have a loop that's doing a lot of math, or I'm writing a bunch of stuff to disc and that's really slow.

Like often those are not instrumented or it's like these black box areas of a performance. And so what we're trying to do with profiling data, instead of just showing you flame charts and stuff, is actually say, could we fill in these gaps in these traces? Like basically like, Hey, I've got a long period of time where the app's doing something.

You know, here's an API call, here's the database stuff. But then there's this block, okay, what's that function or something? Can we pull that out of the profiling data? And so in that case, again, that's just automatic because the profile actually knows everything about the application and know it. It has full access to the function and the stack and everything, right?

And so the dream is that you would just always have everything filled in the, the customer never has to do anything with one minor asterisk. And the asterisk is what I would call like business context. So a good example would be, You might wanna associate requests with a specific customer or something like that.

Like you might wanna say, well it's uh, I don't know, Goldman Sachs or one of these big companies or something. So you can know like, well when Goldman Sachs is having performance issues or whatever it is, oh maybe I should focus on them cuz maybe they pay you a lot of money or something. Right. Sentry would never know that at the end of the day.

So we also have these like kind of tagging contextual APIs that will say like, tell us some informations, maybe it's like customer, maybe it's something else that's relevant to your application. And we'll keep that data associated with the telemetry that's like present, you know, um, but the, at least the telemetry, like again, application's just worth the same, should be, there should be a day in the next few years that it's just all automatic.

and again, the only challenge today is like, can it be high quality and automatic? And so that, that's like to be determined.

[00:25:50] **Jeremy:** What you're kind of saying is the ideal is being able to look at this profiling information and be able to build a full picture of. a, a call from beginning to end, all the different things to talk to, but I guess what's the, what's the reality today? Like, what, what is Sentry able to determine, in the world we live in right now?

[00:26:11] **David:** So we've done a lot of this like performance detection stuff already. So we actually can do a lot now. We put a lot of time into it and I, I will tell you, if you look at other tools trying to do tracing, their approach is much more abstract. It's like your traditional monitoring tool that's like, we're just gonna collect a lot of signals and maybe we'll find magic anomaly detection or something going on in it, which, you know, props, but that can figure that out.

But, a lot of what we've done is like, okay, we kind of know what this data looks like. Let's go after this very like known quantity problem. Let's normalize the data. And let's make it happen like that's today. Um, the enrichment of profiles is new for us, but it, we actually can already do it. It's not perfect.


## Detection of blocking the UI thread in mobile apps

[00:26:49] **David:** Um, and I think we're launching something in April or May, something around the, that timeframe where hopefully for the, the technologies we can instrument, we're actually able to surface that in a useful way. but as an example that, that concept that I was talking about, like with n plus one queries, the team built something using profiling data.

and I think this, this might be for like a mobile app more so than anything where mobile apps have this problem of, it's, you've got a main thread and if you block that main thread, the app is basically frozen. You see this on desktop apps all the time. You, you very rarely see it on web apps anymore.

But, but it's a really big problem when you have a web, uh, a mobile or desktop app because you don't want that like thing to be non-responsive. Right? And so one of the things they did was detect when you're doing like file io on the main thread, you know, right. When you're writing a disc, which is probably a slow thing or something like that, that's gonna block the whole thing.

Because you should just do it on a separate thread. It's like an easy fix, potentially may not be a problem, but it could become a problem. Same thing as n plus one. But what's really interesting about it is what the team did is like they used the profiling data to detect it because we already know threads and everything in there, and then they actually recreated a stack trace out of that profiling data when it's surfaced.

So it's actually like useful data with that. You could like that I or you as a developer might know how to take and actually be like, oh, this is where it happens at the source code. I can actually figure it out and go fix it myself. And to me, like as like I, I'm still very much in the weeds with software that is like one of the biggest gaps to most things.

Is it just, it doesn't make it easy to consume or like take action on, right? Like if I've got a, a chart that says my error rate is high, what am I gonna do with that? I'm like, okay, what's breaking? That's immediately my next question. Right? Okay. This is the error. Where is that error happening at? Again, my next question, it, it's literally just root cause analysis, right?

Um, and so that, that to me is very exciting. and I, I don't know that we're the first people to do that, I'm not sure. But like, if we can make that kind of data, that level of actionable and consumable, that's like a big deal for me because I will tell you is like I have 20 years of software experience. I still hate flame charts and like I struggle to use them.

Like they're not a friendly visualization. They're almost like a, a hypothetically necessary evil. But I also think one where nobody said like, do we even need to use that? Do we need that to be like the way we operate? and so anyways, like I guess that's my long-winded way of saying like, I'm very excited for how we can leverage that data and change how it's used.

[00:29:10] **Jeremy:** Yeah. So it sounds like in this example, both in the mobile app blocking the UI or the n plus one query is the Sentry, suppose, SDK or instrumentation that's hooked inside of your application. There are certain behaviors that it knows are, are not like ideal I guess, just based on. people's prior experience, like your own developers know that, hey, if you block the UI thread in this mobile application, then you're gonna have performance problems.

And so that way, rather than just telling you, Hey, your app is slow, it can tell you your app is slow and it's because you're blocking the UI thread.


## Don't just aggregate metrics, the error tracker should have an opinion on what actual problems are

[00:29:55] **David:** Exactly, and I, and I actually think, I don't know why so many people don't recognize this gap, because at the end of the day, like, I don't know, I don't need more people to tell me response times are bad or anything. I need you to have an opinion about what's good because. The only way it's like math education, right?

Like, yeah, you learn the basics, but you're not expected to say, go to calc, but, and then like, do all the fundamentals. You're like, don't get a calculator and start simplifying the problem. Like, yeah, we're gonna teach you a few of these things so you understand it. We're gonna teach you how to use a calculator and then just use the calculator and then make it easier for everybody else.

But we're also not teaching you how to build a calculator because who cares? Like, that's not the purpose of it. And so for me, this is like, we should be helping people sort of get to the finish line instead of making them run the entirety of the race over and over if they don't need to. I don't, I don't know if that's a good analogy, but that has been the biggest gap, I think, in so much of this software throughout the industry.

And it's, it's, it's common everywhere. And there's no reason for that gap to exist these days. Like the technology's fine. And the technology's been fine for like 10 years. Like Sentry started in oh eight at this point. And I think there was only one other company I recall at the time that was doing anything that was even similar to like air monitoring and Sentry when we built it, we're just like, what if we just go deeper?

What if we collect all this information that will help you debug the problem instead of just stopping it like a log aggregator or something kind of thing, so we can actually have an opinion about it. And I, I genuinely, it baffles me that more people do not think this way because it was not a hard problem at the time.

It's certainly not hard these days, but there's still very, I mean, a lot more people do it now. They've seen Sentry successful and there's a lot of similar implementations, but it's, it's just amazes me. It's like, why don't you, why don't people try to make the data more actionable and more useful, the teams versus just collect more of it, you know?


## 40 people working on learning the common issues with languages and frameworks

[00:31:41] **Jeremy:** it, it sounds like maybe the, the popularity of the stack the person is using or of the framework means that you're gonna have better insights, right? Like if somebody makes a, a Django application or a Rails application, there's all these lessons that your team has picked up in terms of, Hey, if you use the ORM this way, your application is gonna be slow.

Whereas if somebody builds something totally homegrown, you won't know these patterns and you won't be able to like help as much basically.

[00:32:18] **David:** Yeah. Yeah, that's exactly, and, and you might think that that is a challenge, but then you look at how many employees exist at like large tech companies and it's, it's not that big of a deal, like, , you might even think collecting all the information for each, like programming, runtime or framework is a challenge.

We have like 40 people that work on that and it's totally fine. Like, and, and so I think actually all these scale just fine. Um, but you do have to understand like the domain, right? And so the counter version of this is if you look at say like browser applications, like very rich, uh, single page application type experiences.

It's not really obvious like what the opinions are. Like, like if, if you, and this is like real, like if you go to Sentry, it's, it's kind of slow, like the app is kind of slow. Uh, we even make fun of ourselves for how slow it is cuz it's a lot of JavaScript and stuff. If you ask somebody internally, Hey, how would we make pick a page fast?

They're gonna have no clue. Like, even if they have like infinite domain experience, they're gonna be like, I'm not entirely sure. Because there's a lot of like moving parts and it's not even clear what like, like good is right? Like we know n plus one is bad. So we can say not doing that is the better solution.

And so if you have a JavaScript app, which is like where a lot of the slowness will come from is like the render times itself. Like how do you fix it? You, you can't actually build a product that tells you what to fix without knowing how to fix it, right? And so some of these newer and very fast moving targets are, are frankly very difficult for us.

Um, and so that's one thing that I think is a challenge for the entire industry. And so, like, as an example, a lot of the browser folks have latched onto web vitals, which are just metrics that hopefully tell you something about the application, but they're not always actionable either. It'll be like, the idea with like web vitals is like, okay, time to interactive is an an important metric.

It's like how long until the page loads that a user can do what they're probably there to do. Okay. Like abstractly, it makes sense to us, but like put into action. How do I optimize time to interactive? Don't block the page. That's one thing. I don't know. Defer assets, that's another thing. Okay. So you've gotta like, you've gotta build a technology that knows these assets could be deferred and aren't.

Okay, which ones can be deferred? I don't know. Like, it, it, it's like such a deep rabbit hole. And then the problem is, six months from now, the tech will have completely changed, right? And it won't have like, necessarily solved some of these problems. It will just have changed and they're now a completely different shape of problem.

But still the same fundamental like user experience is the same, you know? Um, and to me that's like the biggest challenge in the industry right now is that like dilemma of the browser at the end of the day. And so even from our end, we're like, okay, maybe we should step back, focus on servers again, focus on web services.

Those are known quantities. We can do that really well. We can sort of change that to be better than it's been in the past and easier to consume with things like our n plus one detections. Um, and then take like a holistic, fresh look at browser and say, okay, now how would we solve this to make sure we can actually really latch onto the problems that like people have and, and we understand, right?

And, you know, we'll see when we get there. I don't think any product does a great job these days for helping, uh, solve those problems. . But I think even without the, the products, like I said, like even our team would be like, fixing this is gonna take months because it's gonna take months just to figure out exactly where the, the common bottlenecks are and all these other things within an application. And so I, I guess what I mean to say with that is there's a lot of opportunity, I think with the moving landscape of technology, we can find a way to, whether it's standardized or Sentry, can find a way to make that data actionable want it something in between there.


## There are many ways to build things on the frontend with JavaScript which makes it harder to detect common problems compared to backend

[00:35:52] **Jeremy:** So it sounds like what you're saying, With the, the back end, there's almost like a standard way of doing things or a way that a lot of people do it the same way. Whereas on the front end, even if you're looking at a React application, you could look at tenant react applications and they could all be doing state management a totally different way.

They could be like the, the way that the application is structured could be totally different, and that makes it difficult for you to infer sort of these standard patterns on the front end side.

[00:36:32] **David:** Yeah, that's definitely true. And it, it goes, it's even worse than that because well, one, there's just like the nature of JavaScript, which is asynchronous in the sense of like, it's a lot of callbacks and things like that. And so that already makes it hard to understand what's going on, uh, where things are happening.

And then you have these abstractions like React, which are very good, but like they pull a lot of that away. And so, as an example of a common problem, you load the application, it has to do a lot of stuff to make the page render. You might call that hydration or whatever. Okay. And then there's a completely different state, which is going from, it's already hydrated.

Page one, I, I've done an interaction or something. Or maybe I've navigated a page too, that's an entirely different, like, sort of performance problem. But that hydration time, that's like a known thing. That's kind of like time to interactive, right? But if the problem is in your framework, which a lot of it is like a lot of the problems today exist because of frameworks, not because of the technology's bad or the framework's bad, but just because it's abstracted and it's really hard to make it work in all these situations, it's complicated.

And again, they have the same problem where it's like changing non sem. And so if the problem is the framework is somehow incorrectly re rendering the page as an example, and this came up recently, for some big technology stack, it's re rendering the page. That's a really bad problem for the, the customer because it's making the, it's probably actually causing a lot of CPU seconds.

This is why like your Chrome browser tabs are using so much memory in cpu, right? How do you fix that? Can you even fix that? Do you just say, I don't know, blame the technology? Is that the solution? Maybe that is right, but how would we even blame the technology like that alone, just to identify why it's happening.

and you need to know the why. Right? Like, that is such a hard problem these days. And, and personally, I think the only solution is if the industry sort of almost like standardizes on a way to like, on a belief of how this should be optimized and how it should be measured and monitored kind of thing.

Because like how errors work is like a standardization effectively. It may not be like a formal like declaration of like, this is what an error is, but more or less they always have the same attributes because we've all kind of understood that. Like those are the valuable things, right? Okay. I've got a server rendered application that has client interaction, which is sort of the current generation of the technology.

We need to standardize on what, like that web request, like response life cycle is, right? and what are the moving targets within there. And it just, to me, I, I honestly feel like a lot of what we use every day in technology is like beta. Right. And it's, I think it's one of the reasons why we're constantly always having to up, like upgrade and, and refactor and, and, and shift dependencies and things like that because it is not, it's very much a prototype, right?

It's a moving target, which I personally do not think is great for the industry because like customers do not care. They do not care that you're using some technology that like needs a change every few months and things like that. now it has improved things to be fair. Like web applications are much more like interactive and responsive sometimes.

Um, but it is a very hard problem I think for a lot of people in the world.

[00:39:26] **Jeremy:** And, and when you refer to, to things feeling like beta, I suppose, are, are you referring to the frameworks people are using or the libraries they're using to support their front end development? I, I'm curious what you're, you're thinking there.

[00:39:41] **David:** Um, I think it's everything. Even like the browser APIs are constantly shifting. It's, that's gotten a little bit better. But even the idea like type script and stuff, it's just like we're running like basically compilers to make all this code work. And, and so the, even that they're constantly adding features just because they can, which means behaviors are constantly changing.

But like, if you look at a real world example, like React is like the, the most dominant technology. It's very well designed for managing the dom. It's basically just a rendering engine at the end of the day. It's like it's managed to process updates to the dom. Okay. Makes sense. But we've all learned that these massive single page applications where you build all your application logic and loaded into a bundle is a problem.

Like, like, I don't know how big Sentry's bundle is, but it's multiple megs in size and it takes a little while for like a, even on fast fiber here in the Bay Area, it takes a, you know, several seconds for the UI to load. And that's not ideal. Like, it's like at some point half of us became okay with this.

So we're like, okay, what we need to do is go back, literally just go back 10 years and we need to render it on the server. And then we need some stuff that makes interactions, you know, highly responsive in the UI or dynamic content in the ui, you know, bring, it's like bringing back jQuery or something.

And so we're kind of going full circle, but that is actually like very complicated because the way people are trying to do is like, okay, we wanna, we wanna have the rendering engine operate the same on the server and is on as on the client, right? So it's like we just write one, path of code that basically it's like a template engine to some degree, right?

And okay, that makes sense. Like we can all get behind that kind of model. But that is actually really hard to make work with a lot of people's software and, and I think the challenge and framers have adopted it, right? So they've taken this, so for example, it's like, uh, react server components, which is basically just like, can we render it on the server and then also keep that same interaction in the ui.

But the problem is like frameworks take that, they abstract it and so it's another layer of complexity on something that is already enormously complex. And then they add their own flavor onto it, like their own opinions for maybe what the world way the world is going. And I will say like personally, I find those.

Those flavors to be very hard to adapt to like things that are tried and true or importantly in this context, things that we know how to monitor and fix, right? And so I, I don't know what, what the be all end all is, but my thesis on this is you need to treat the UI like a template engine, and that's it.

Remove all like complexity behind it. And so if you think about that, the term I've labeled it as, which I did not come up with, I saw this from somebody at some point, is like, it's like your front end as a service. Like you need to take that application that renders on the server and the front end, and it's just an entirely different application, which is annoying.

and it just calls your APIs and that's how it gets the data it needs. So you're literally just treating it as if it's like a single page application that can't connect to your database. But the frameworks have not quite done that. And they're like, no, no, no. We'll connect to the database and we'll do all this stuff, but then it doesn't work because you've got, like, it works this way on the back end and this way on the front end anyways.

Again, long winded way of saying like, it's very complicated. I don't think the technology can solve it today. I think the technology has to change before these problems can actually genuinely become solvable. And that's why I think the whole thing is like a beta, it's like, it's very much like a moving target that we're eventually we'll get there and it's definitely had value, but I don't know that, um, responsiveness for low latency connections is where the value has been created.

You know, for like folks with bad internet and say remote Africa or something, like I'm sure the internet is not a very fun place for them to use these days.


## Some frontend code runs on the server and some in the browser which creates challenges

[00:43:05] **Jeremy:** I guess one of the things you mentioned is there's this, almost like this split where you have the application running on the server. It has its own set of rules because it, like you said, has access to the database and it can do things that you can't do in the browser, and then you have to sort of run the same application in the browser, but it's not quite the same application because it doesn't have access to the same things in the browser.

So you have this weird disconnect, I suppose.

[00:43:35] **David:** Yeah. Yeah. And, and, and then the challenges is like a developer that's actually complicated for you from the experience point of view, cuz you have to know somehow, okay, these things are ta, these are actually running on the server and only on the server. And like, so I think the two biggest technologies that try to do this, um, or at least do it well enough, or the two that I've used, there might be some others, um, are NextJS and remix and they have very different takes on how to do this.

But, remix is the one I use most recently. So I, I'll comment on that. But like, there's a, a way that you kind of say, well, this only runs on, I think the client as an example. And that helps you a little bit. You're like, okay, this is only gonna render on the client. I can, I actually can think about that and reason about that.

But then there's this thing like, okay, sometimes this runs on the server, only this part runs on the server. And it's, it just becomes like the mental capacity to figure out what's going on and debug it is like so difficult. And that database problem is like the, the normal problem, right? Like of like, I can only query the database on the server because I need secure credentials or something.

Okay. I understand that as a developer, but I don't understand how to make sure the application is doing what I expect it to do and how to fix it if something goes wrong. And that, that's why I think. , I'm a, I'm a believer in constraints. The only way you make progress is you simplify problems. Like you just give up on solving the complicated thing and you make the problem simpler.

Right? And so for me, that's why I'm like, just take the database outta the equation. We can create APIs from the client, from the server, same security levels. Okay? Make it so it can only do that and it has to be run as almost like a UI only thing. Now that creates complexity cuz you have to run this other service, right?

And, and like I personally do not wanna have to spin up a bunch of containers just to write like a simple like web application. but again, I, I think the problem has not been simplified yet for a lot of folks. Like React did this to be fair, um, it made it a lot easier to, to build UI that was responsive and, and just updated values when they changed, you know, which was a big deal for a long period of time.

But I feel like everything after has not quite reached that that area, whereas it's simple and even react is hard to debug when it doesn't do what you want it to do. So I don't know, there, there's so gaps I guess is what i would say. And. Hopefully, hopefully, you know, in the next five years we'll kind of see this come to completion because it does feel like it's, it's getting closer to that compromise.

You know, where like we used to have pure server rendered apps with some weird janky JavaScript on top. Now we've got this bridge of really complicated, you know, JavaScript on top, and the server apps are also complicated and it's just, it's a nightmare. And then this newer generation of these frameworks that work for some types of technology, but not all.

And, and we're kind of almost coming full circle to like server rendered, you know, everything. But with like allowing the same level of interactions that we've been desiring, I guess, on the web. So, and I, fingers crossed this gets better, but right now I do not see like a clear like, oh, it's definitely there.

I can see it coming. I'm like, well, we're kind of making progress. I don't love being the beta tester of the whole thing, but we're kind of getting there. And so, you know, we'll see.


## There are multiple ways to write mobile apps as well (flutter, react native, web views)

[00:46:36] **Jeremy:** I guess you, you've been saying this whole shifting landscape of how Front End works has made it difficult for Sentry to provide like automatic instrumentation and things like that for, for mobile apps. Is that a different story? Like is it pretty standardized in terms of how do you instrument an Android app or an iOS app.

[00:46:58] **David:** Sort of, but also, no, like, a good example here is like early days mobile, it's a native application. You ship a binary known quantity, right? Or maybe you embedded a web browser, but like, that was like a very different thing. Okay. And then they did things where like, okay, more of it's like embedded web browser type stuff, or dynamically render content.

So that's now a moving target. the current version of that, which I'm not a mobile dev so like people have strong opinions on both sides of this fence, but it's like, okay, do you use like a, a hybrid framework which allows you to build. Say, uh, react native, which is like arou you to sort of write a JavaScript ish thing and it runs on both Android and mobile, but not really well on either.

Um, or do you write a native, native app, which is like a known quantity, but then you may maintain like two code bases, have two degrees of expertise and stuff. Flutters the same thing. so there's still that version of complexity that goes on within it. And I, I think people care less about mobile cuz it impacts people less.

Like, you know, there's that whole generation of like, oh, mobile's the future, everything's gonna be mobile, let's not become true. Uh, mobile's very important, but like we have desktops still. We use web software all the time, half the time on mobile. We're just using the web software at the end of the day, so at least we know that's a thing.

And I think, so I think that investment in mobile has died down some. Um, but some companies like mobile is like their main experience or one of their driving experience is like a, like a company like DoorDash, mobile is as important as web, if not more, right? Because of like the types of customers.

Spotify probably same thing, but I don't know, Sentry. We don't need a mobile app, who cares? It's irrelevant to the problem space, right? And so I, I think it's just not quite taken on. And so mobile is still like this secondary citizen at a lot of companies, and I think the evolution of it has been like complicated.

And so I, I think a lot of the problems are known, but maybe people care less or there's just less customers. And so the weight doesn't, like, the weight is wildly different. Like JavaScript's probably like a hundred times the size from an investment point of view for everyone in the world than say mobile applications are, is how I would think about it.

And so whether mobile is or isn't solved is almost irrelevant to the, the, the like general problem at hand. and I think at the very least, like mobile applications, there's like, there's like a tool chain where you can debug a lot of stuff that works fairly well and hasn't changed over the years, whereas like the web you have like browser tools, but that's about it. So.


## Mobile apps can have large binaries or pull in lots of dependencies at runtime

[00:49:16] **Jeremy:** So I guess with mobile. Um, I was initially thinking of native apps, but you're, you're bringing up that there's actually people who would make a native app that's just a web view for a webpage, or there's React native or there's flutters, so there's actually, it really isn't standard how to make a mobile app.

[00:49:36] **David:** Yeah. And even within those, it comes back to like, okay, is it now the same problem where we're loading in a bunch of JavaScript or downloading a bunch of JavaScript and content remotely and stuff? And like, you'll see this when you install a mobile app, and sometimes the binaries are huge, right?

Sometimes they're really small, and then you load it up and it's downloading like several gigs of data and stuff, right? And those are completely different patterns. And even within those like subsets, I'm sure the implementations are wildly different, right? And so, you know, I, that may not be the same as like the runtime kind of changing, but I remember there was this, uh, this must be a decade ago.

I, I used, I still am a gamer, but. Um, early in my career I worked a lot with like games like World of Warcraft and stuff, and I remember when games started launching progressive loading where it's like you could download a small chunk of the game and actually start playing and maybe the textures were lower, uh, like resolution and everything was lower fidelity and, and you could only go so far until the game fully installed.

But like, imagine like if you're like focused on performance or something like that, measuring it there is completely different than measuring it once, say everything's installed, you know? And so I think those often become very complex use cases. And I think that used to be like an extreme edge case that was like such a, a hyper-specific optimization for like what The Warcraft, which is like one of the biggest games of all time that it made sense, you know, okay, whatever.

They can build their own custom tooling and figure it out from there. And now we've taken that degree of complexity and tried to apply it to everything in the world. And it's like uhoh, like nobody has the teams or the, the, the talent or the, the experience to necessarily debug a lot of these complicated problems just like Sentry like.

You know, we're not dealing with React internals. If something's wrong in the React internals, it's like somebody might be able to figure it out, but it's gonna take us so much time to figure out what's going on, versus, oh, we're rendering some html. Cool. We understand how it works. It's, it's a known, known problem.

We can debug it. Like there's nothing to even debug most of the time. Right. And so, I, I don't know, I think the industry has to get to a place where you can reason about the software, where you have the calculator, right. And you don't have to figure out how the calculator works. You just can trust that it's gonna work for you.


## How Sentry's stack has become more complex over time

[00:51:35] **Jeremy:** so kind of. Shifting over a little bit to Sentry's internals. You, you said that Sentry started in, was it 2008 you said?

[00:51:47] **David:** Uh, the open source project was in 2008. Yeah.

[00:51:50] **Jeremy:** 

The stack that's used in Sentry has evolved. Like I remembered that there was a period where I think you could run it with a pretty minimal stack, like I think it may have even supported SQLite.

[00:52:02] **David:** Yeah.

[00:52:03] **Jeremy:** And so it was something that people could run pretty easily on their own.

But things have, have obviously changed a lot. And so I, I wonder if you could speak to sort of the evolution of that process. Like when do you decide like, Hey, this thing that I built in 2008, Is, you know, not gonna cut it. And I really need to re-architect what this system is.

[00:52:25] **David:** Yeah, so I don't know if that's actually the reality of why things have changed, that it's like, oh, this doesn't work anymore. We've definitely introduced complexity in the sense of like, probably the biggest shift for Sentry was like, it used to be everything, and it was a SQL database, and everything was kind of optional.

I think half that was maintainable because it was mostly built by. And so I could maintain like an architectural vision that kept it minimal. I had the experience to figure it out and duct tape the right things. Um, so that was one thing. And I think eventually, you know, that doesn't scale as you're trying to do more and build more into the product.

So there's some complexity there. but for the most part you can, it can still be a SQL database, whatever. Could it be SQLite forever? Probably not. But it was, it was gold when you could run SQLite in the development environment cuz it was super fast, right? Um, and so then there was like the evolution of that to where we started adding more complex services.

So one example was, uh, we needed a key value store and we needed to like store blob data because storing them in the SQL database was highly inefficient and becoming very expensive. And so we wrote just an abstraction that could sort in the database or, and at the, the technology at the time was React, uh, Riak, not to be confused with React.

And that was just like, you can almost think of it like, uh, big Table or naively S3 or something. It's literally just like get set, delete where the operation's available to us. And then actually we're totally fine. So it meant like we could swap it out for more scalable technology, but you could also ignore swapping it out and at some point you've got like a maintenance burden for like handling these different code paths, right?

Because that's also the era when Sentry was only open source or primarily open source. So primarily just ran it yourself, you know? then we started adopting SaaS we're starting to build more complexity. Basically the constraints we put into place are actually causing problems now. So we need to change the constraints, which means supporting all these things, it's hard.

So that's one thing that happens right now. I would not excuse it and say you couldn't still keep things simple. I think that's a thing, but that takes a lot of rigor and at some point you're like, is it worth it? You know? Especially when primarily, uh, especially in this day and age, things are just SaaS services and we've all kind of accepted that.

But that was one, and then there was a big shift where we wanted to consume and make scalable and fast a lot of data, right? Like there's already lots of errors. Like, I don't know how many, like. I, I'm, I'm certain Sentry like sucks in hundreds of thousands of events a second on a bad day. On a slow day.

So I'm sure it's a huge amount of data that we get these days. and that takes a certain scale, right? And it's actually very hard to handle small scale and large scale at some point. And obviously we're optimizing for the SaaS. So at some point we're like, okay, let's a, we need a better solution for storing the events, something that we'll be able to like, write them in, search them very fast, take a lot of the load off the database, and so we adopt a click house.

And I think that's kind of when, that's like the, whatever the saying is, like straw that broke the camel's back or something. I don't, I don't know the saying, but, um, where everything started to get more complex and that's when all of a sudden it's like, you need like 15 docker containers and, and this isn't even microservices.

This isn't even like the worst version of this. Hell, you know, it's just like, and I think it's, it's unfortunate that that's like what it's come to is like you have to run a lot of these complex services. And I think this is not even representative of just centuries growth. It's like the whole industry where we've.

We've made things a little bit more complicated than it needs to be in a lot of cases. and so I, I think it's just like, it was that shift, and then it's like when we wanted to build performance monitoring, we needed all these new things. And even in the product today, like if you just want to use it for air monitoring, whether you're a SaaS customer or self-hosted, there's still a lot going on, right?

Okay, maybe that's fine. Maybe that's a reality. But right now, like this year, we're gonna redo a lot of the product because it's too complicated. There's too much going on, and it, it becomes like a distraction. Like you load up the AWS console or even gcps just as bad these days where there's like 800 different services and you're like, I don't know what, like, who cares?

Like why do I need any of this? And half of 'em are the same thing. And that is the worst part is half of them are the same thing, or, or they're not achieving different goals, would be how I think about it. And Sentry is not that. But the biggest companies in our space are that like, if you use Datadog, it's the same thing.

And there's like go to the Datadog's pricing page and you're like, oh my God, there are so many different things in here. I don't even know what the difference is between some of these products. Right. And so we're, we're very conscious of this, and I think, I don't know that we can reduce the technology complexity that much if at all these days, other than maybe making it a little bit easier to not have to run everything for, for the open source side of things.

But the product burden is still there when you're like, how do I even reason about all this stuff that's going on and why does it even need to happen this way? So I, I don't know, it, it's like a sad thing to some degree, but, uh, at the same time, like we've been able to build like such a significant product that does, it works for so many different people and it, it solves so many different problems.

And it's still, you can, not as easily, but you can still can run it on your own hardware. And I'm amazed when like a single human runs it on like a VPS or something. which it for, for newer generation people is, a virtual private server. Okay. Like a Linode or a digital ocean, something cheap. Um, because it is a lot of stuff, it's a lot of services to run and a lot of them are Java and they take a lot of memories.

So


## As the product transitioned from a self hosted protect to a SaaS product the ability to pick and choose components for self hosting went away and the number of required components went up

[00:57:27] **Jeremy:** What it sounds like is that that version of the software that used to be able to run with pretty minimal dependencies, I, I think, you know, you would have a relational database. I think you had read us in there, and now there's like you said, click house, there's zookeeper, there's, is there Kafka?

[00:57:46] **David:** There is Kafka.

[00:57:47] **Jeremy:** There's a, there's a lot of different pieces and from what you're telling me is, is it's kind of a function of going from this company that's like, here, here's this open source software that anybody can run themselves to. This is really a SaaS company. This is like, We need to focus on being able to run this at scale and the use case of somebody running it themselves or at their own business is just like kind of not that important anymore.

At least to, you know, that that's not the priority. And, and that's why you kind of made these decisions because they were suited to building a, a SaaS platform that can service a lot of customers.

[00:58:28] **David:** Yeah, that that is a huge chunk of it. I think there was also the thing, like for example, that key value store. At some point we sported Cassandra, we never used Cassandra ourself, but it was in the code base. We're not gonna maintain that. It might be broken for all we know. Yeah, there's a CI system and at some point you've gotta say like, no, that's not happening.

And that was actually a good decision. Like less variability is huge for infrastructure, right? And that doesn't require it to be more complicated. But like if we just say too bad you can't run Cassandra, run a key val, like run, I don't know, you know, big table or something that we actually use ourselves.

It's like maybe you don't want to, but it's like we're not making any money and nobody's maintaining all these like adapters for these different databases like we supported like Django does. So we sort of did. But like MSSQL, which I assume is still a thing, I'm not sure, um, no idea if it ever worked correctly, was performant or not.


## There is duplication in dependencies (RabbitMQ and Kafka) but the engineering work required to remove one of them is not worth it

[00:59:20] **David:** You know, that, and that's the same dilemma, SQLite, right? And so I think SQLite was fine for development environments. Who cares for production? No chance does it function for us. But, um, I don't know. So I think it's sort of a necessary evil, but, but it doesn't have to be complicated. So a good example today is we still require something like Rabbit, MQ and Kafka.

Why do we need two things that are effectively brokers? We don't. It's just like, , like why would it be a priority to replace like the old system that powers all this or combine it with the new system that powers these new things? It's like, it's a lot of engineering work, right? And so there is that compromise of velocity in there that we're forever facing.

And this doesn't even begin to touch on like the newer stuff that we're gonna open source. Like I don't even think we've open sourced, uh, one of our first acquisition, which was the profiling stuff. I think that might still be closed source. We're gonna open source that, uh, we acquired code cov recently.

We're gonna open source that. Um, and so those are more moving parts that even add more complexity to the product. And so one of the, and to be fair, this complexity, uh, cascades in the development environment and experience and stuff. So, so it's worthwhile to fix. but as an example, you should be able to say, I'm just working on maybe the errors stuff or the issues product, so I don't need to run all this other stuff.

And that same decision can also say, oh, the customer only wants to like use this for the errors product so they don't need to run all this other stuff. Right? You like, you can solve both of those goals and I think it just requires. Intent behind it doesn't necessarily mean it will make it that much simpler, but it is a path towards enabling that simplicity.

[01:00:51] **Jeremy:** it's also probably aligning with how the business is structured, right? Like, I don't think you offer a self-hosted, commercially supported plan, right? So in that regard there, there isn't really. The need from the company side to, to say like, Hey, let's, let's make these cases where you can deploy it and only install two of the dependencies because you only need that much.

it, it's like very different from, a, a system or a product that was not really a SaaS or, or it could be a SaaS but but also had a on-premise, option. Like you could take I, I suppose Atlassian's Suite as an example where they have their cloud service, but there's also a lot of businesses that run it onsite.

So there's probably different decisions that, that they have to make.


## Made an intentional decision to not build on-premise software so they could focus on product instead of support

[01:01:44] **David:** Yeah. Yeah, a hundred percent. And I'm actually curious, like, you know, the model from a technology angle is probably similar to GitLab and I, I, I'm not a GitLab user. but I wonder if, if folks like that have the same complexity where they're like, here's our 15 different products and it's sort of open sourcey, you know, and we, ours at least was intentional.

We're like, we're not building on-prem software. We don't wanna be in that business. We don't want these support contracts for Cassandra and random shit. We basically don't want to have to have an outsourced ops team, you know, for this work. It's just not interesting. It's not building a product at the end of the day.

And so I think it was like, that was probably one of the best decisions we ever made was like, yes, it's open source. We're building an open source service, like a SaaS service at the end of the day. And that's the reality of things. Right. And that was such a big deal for us, because yeah, like I, I, it's like it's hard to keep the complexity in check no matter what if, if you get to any reasonable size.

Right? And like big ambitions are one of the most important things you can have, in my opinion, for building anything. Even if it's not like, oh, we wanna build a big company. You want to be able to build something that solves like significant scope of problems, right? And there's more value for Sentry as a whole if we can solve more problems under sort of the same kind of landscape, right?

If nothing else, because whether it's true or not, the the reality is like, Nobody wants to run 20 different tools or whatever it is, right? Like usually what happens is you have to, because like one tool cannot rule them all, but if the problem is the same shape, the technology should be able to be reused to solve that problem.

And that, that's where we go back to like, well, we have errors and we have n plus one issues, and they're kind of the same. So how do we make the product just surface both of those use cases, right? Same technology, same product for the most part. and then inherently here comes the complexity. So,


## Choosing what to open source and choosing the Business Source License for the main application to prevent competitors from reselling their service while allowing people to learn from the source code

[01:03:26] **Jeremy:** Uh, you, you've mentioned a. A little bit about how there are parts of Sentry that are open source, and I know that there's different licenses applied to different parts of the product, so I wonder if you could explain sort of how those decisions are made and, and maybe you could explain the, the business source license as well.

[01:03:49] **David:** Yeah. So once upon a time Sentry was BSD licensed, uh, and that was the server itself. And Sentry's got a lot of open source stuff or a lot of projects and services and stuff. Um, but the core of the server was like super liberally licensed. Everything else was fairly liberally licensed. Like we never used GPLs uh, we never used proprietary licenses.

We had some closed source stuff, but it's irrelevant. It was like our data analytics and billing code and stuff like that. But, so as all this, it was all just like, like liberal free. You could use it. No strings, no open core, no nothing. Uh, and then we had constant annoying conversations with people trying to sell our software.

And to be clear, Sentry has always been built by myself and people that we've employed at the company. Sometimes people contribute small patches, but that's wildly different than maintaining or actually developing the software. And so it's best to think of Sentry as like, yes, it's open source, but it was built by our company.

the SDKs and integrations, that's different, but the core service, right? And so we had this thing where people, like companies were trying to sell it, they didn't wanna give back financially or they didn't contribute both basically. And so we're like, this is annoying and this is literally the decision tree.

This is annoying. Let's stop them from doing that so we can no longer think about this problem. And so at that point we said we're gonna change how we do licensing at Sentry for open source. If it's part of the service, the core service, it becomes bsl, which I'll explain in a minute. If it's anything else that doesn't run the core service like an SDK or anything that needs embedded in customer applications, it must use a liberal license.

And so, , we did this because I did not want an open core model. An open core, if you're not familiar, usually what it translates to is here's the shitty version of the open source product that you can use for free, no strings attached, and here's the good version. That costs minimum 50 to a hundred thousand dollars a year.

Something along those lines. It becomes a obnoxious selling pair or paradigm. I hate that model so much as a, as a consumer that I refuse to build it. And if it was not for companies trying to sell our stuff, we would still be BSD or Apache license for the server, right? Unfortunately, in humanity you can't take on good faith and definitely in like capitalism, you cannot operate on good faith, so, so we relicensed the BSL and bsl, the way I think about it is eventually open source.

And so open source has a lot of different angles. You can think of it as open source, like free software that I can use just for free or open source is like, I can take that software, do whatever I want with it, which is the most extreme version or open source. I can use the code in other ways or something like that, right?

There's all these kind of variations of the thing, but I think the most are like. I can do whatever I want with it, or it's free. And I actually think a lot of people mostly care about open source from, its the, its free angle. And so bsl, what it lets us do is say it's free. You can't sell it. So we, we blocked off people from like, sort of cannibalizing our ability to fund the development.

and in three years, which is the time horizon we picked, you can do, um, I think it the, the lowest you can do with BSLs four years or the high longest duration, you can do something like every year. It's like your personal choice. after three years it becomes Apache licensed and a lot of open source advocates who will be like, well, like three years is a lifetime.

I'm like, that's cool. We're not here to let other people build businesses at a Sentry. So I could, I could care less about those arguments, right? I want people to be able to run it self-hosted because like I want everybody to be able to use our. I don't need people to be able to sell it. I don't need people to be able to take it and do whatever they want with it.

It's, it's irrelevant like right to the world. But after three years, all that knowledge that we've gained in that prior art becomes public domain. Right? And so we still achieve almost like this knowledge share. Um, and you can, it's still source. You can view the source, you can like be inspired by it. And it's, it's software.

It's like, it's only so protected at the end of the day. Um, and so that's what it is for us, right? So it allows us to keep it open source. So like what is on Sentry io again, other than some proprietary stuff that's like billing code is literally like that mainline branch is what we're shipping to production at the end of the day.

And I mean, that's cool like that, that's like a lot of the ways in the spirit of open source, but it, it doesn't pray for humanity to be like nice humans all the time. Right? Like it protects the business and the development and the, you know, tens to hundreds of millions of dollars we poured into like r and d over the years, right?

[01:07:55] **Jeremy:** it, it sounds like the decision you made is probably very similar to other vendors like Mongo and, elastic trying to think of some other examples. I guess Cockroach is

[01:08:08] **David:** Yeah. Cockroach is another good one. It is very similar. The difference is like, there's very few companies that operate like Sentry in the world that are like a SaaS service that happens to be open source. Most of those are like infrastructure that you probably wanna run yourself. And most of those, they're billing.

Uh, their, the way they make money is actually still you running that software yourself, right? And so they may not be open core, some of them are, but they're still a lot of, it's fundamentally not a cloud service that they're selling. Like they will try. But like, you know, if, if you're looking at like Elastic, most people use it because they can run it on prem.

Otherwise, I'm just gonna use whatever the Google checkboxy button click thing is at the end of the day. but there are a lot of people, even the BSL model, there's a lot of people use it. Like Cockroach is one of the first that I recall that used it and we were inspired and, and learned about it from.

I could not tell you who else uses it, but there, it, it's become a more popular thing. And whether it's the right solution or not, there needs to be something that is mainstream that people use that achieves this, that basically is the bsl. And I hopefully it's a BSL or some knockoff. Because the problem is if you have 15 different flavors of this license, legal review is not fun.

And if legal review is not fun, it gets blocked in companies. Right? And so Mongo is its own license. Elastic I think is its own license. They're both like proprietary things that are one-offs that have to go through a legal review. BSL is a known quantity with a clause. So all legal has to do is like review that clause and say, does this clause, is that safe enough for us or not?

Right? So it's a very like simple decision at that point. And so, I don't know, hopefully the industry figures that out instead of constantly bickering about what is and isn't open source. Cuz that would be a much better spend of people's time these days.


## Early on, pick a permissive license and worry about the licensing later. If you're successful then you can change it later if needed.

[01:09:44] **Jeremy:** if you're building a new product, I mean, when you look back at, at Sentry, started with the BSD license, which is a very permissive license. what's the, things you would look at to decide that you're gonna start this new product with a permission permissive license versus go straight to the the BSL license.

[01:10:04] **David:** Yeah, I honestly, I would just not get distracted by that choice early on in a project. I think, I think it depends on what you're building, in all honesty. Like if I were building something that was designed, it was like infrastructure that was like so low friction that you could just spin it up and it worked like very well.

Amazon's gonna sell that shit. They're gonna take it. They're gonna be like, cool, we can spin this up for you too. And then they're gonna, I mean, you're gonna struggle, right? Like I think now is that actually what would happen? I don't know. But that's a risk, right? And I think this was like the kind of risk people like Cockroach were worried about was like Amazon might sell it.

Because they saw that like elastic, that happened to them. Now Elastic is done fine. Nobody should be sad for Elastic. They've made plenty of money with Amazon selling it on top, like it doesn't really matter. Right? like pity the executives there or something that doesn't really matter. But for a early stage project, it's so irrelevant.

Like if you make your license restrictive, you will get less adoption. So unless the, your open source project is only gonna be used by a hundred companies in the world, having a restrictive license is only gonna harm you. Right. And so you can do it, but I just wouldn't. And open core is the same thing.

Like I, it's just like, yeah, like I, I don't know. Like this is the glory of sass. It's like you can build an open source thing and not care that it's open source now because you can just sell a cloud service and people will buy the cloud service no matter what. Right. Like centuries model when we raised our seed funding, , it was, it was BSD license time, super free, super open.

And people were like, well, why would anybody pay for it? And I'm like, it doesn't matter if they don't pay for Sentry, they won't pay for anything in the industry because we will build the best thing and it will be so free and good that nobody will have a choice, like, but to use it. Right? And the reality is, if you are a reasonable company, you don't wanna spend a bunch of engineering hours and time and money on running this random service that you can just outsource.

Like that's true for everything in the world, right? And, and that, that was the reality for Sentry. Like I said, there was no like actual risk to the business. It was just like, frankly, it was just pissing me off that I had this one company that was constantly trying to sell our shit. And so I'm like, you know what?

This is my middle finger to you is the BSL license and I can never think about you again now. but we were already a successful business when that that came along. Like people already use the SaaS service. Not everybody, but plenty of people. And so for me it was just like, is your goal that you want lots of customers using your thing, use a permissive license?

Like you're, otherwise, you're like over optimizing for a non-com. It's the same thing with like people that they'll build like random open source stuff and they use like GPL or something. Do you really want your, you, it's almost like you wanna put your politics on another company. Like you wanna force them to contribute back, who cares?

They're either gonna contribute back or not. Like it's still open source at the end of the day. Don't like restrict people's usage if you're just building like something on the side. And so like we actually have a policy internally, we won't license anything as a GPL variant. Like it, it's just not something we think is the right approach to open source.

Right. And again, you can have an opinion on it doesn't really matter to us, but we're like, no, if it's open source, if it's actually intended to be like the free open source, it should be free without the constraints. Who cares if somebody monetizes it? Like that's the beauty of open source is like, it helps everybody, you know, it's, it's almost like a, a charity to some degree.

So, so I'd say I have a lot of strong opinions about it, but mostly it's like, don't distract yourself with things that don't matter. Cause it's like a broad statement for anything, let alone the open source licensing.

[01:13:22] **Jeremy:** Yeah, that, that, that makes sense. I mean, you, you don't know that your product is gonna get adoption to begin with. Right? So it's probably, you would take a path similar to Sentry where you have something permissive, you see, do people care? Is this actually a business? And then once it becomes one, then you can maybe worry about licensing.

[01:13:42] **David:** Exactly. Exactly. Yeah. Because you can always change the license later or you can find another thing to augment the software you've built that allows you to monetize it, which is super common. Like you see this like, uh, there's been a lot of stuff that's raised funding recently. The core is still open source, true free open source.

And then they're like, this is how we're gonna monetize development via some mechanism, like some cloud services or something. That's not true for everybody. You can't just take open source and monetize it. But like, if that's what you wanted to do, why would, why'd you build open source in the first place, right?

Like um, just save yourself a headache. Like I think Nginx I dunno how well they've done as a business. But like, what are you gonna monetize in Nginx? It already just works. Oh, you got some like cloud analytics. It's cool. Like maybe they were useful. I never used them. Um, but like, I'm not gonna buy that.

But that was just like, oh, Nginx is so successful. Could we monetize it? Versus could we build a business that actually is open source? One's like very intentional versus, you know, capitalistic, i would say, or predatory to some degree. I'm not talking shit about the Nginx folks. I love the, the product and the business, but you know, it's a much harder thing to do.

[01:14:47] **Jeremy:** You, you love the product, but don't need to pay for it.

[01:14:50] **David:** Exactly. Yeah. I don't even know. Uh, we probably still use the product, but these days that's more of a commodity than anything like the web server. So,

[01:14:59] **Jeremy:** So as as we wrap up, is there anything else that you thought we should have brought up?

[01:15:07] **David:** um, no, I, I mean, I think this was, this was fun. you know, I, I'm very much an authentic person. I, I think it's like I'm not a marketer. I like talking about things that add value to folks' lives, not just like pitching products and stuff. So I think it's good to go deeper on the, the things which is fun.

Um, I don't know, Sentry's doing a lot of cool stuff. Hopefully people like it. If you don't tell us GitHub issues, tweet at me. We take every piece of feedback very, very seriously. Um, so yeah,

[01:15:33] **Jeremy:** And if, uh, people wanna see what you're up to, check out Sentry, where should they head?

[01:15:39] **David:** uh, Sentry io we're get Sentry on Twitter. Hopefully by the time this airs, Twitter still exists. But, um, yeah, on Sentry io GitHub, we're get Sentry. Sentry somewhere. You search for us, you'll find us. We're very, very, um, active on GitHub though, so that's a good, good forum if you wanna participate that way.

[01:15:57] **Jeremy:** David, thank you so much for coming on Software Engineering Radio.

[01:16:01] **David:** Absolutely. And, and thanks again for having me. 

</div>