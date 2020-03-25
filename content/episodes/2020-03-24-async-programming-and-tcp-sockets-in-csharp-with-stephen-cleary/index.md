+++
title = "Async Programming and TCP Sockets in C# with Stephen Cleary"

description = "Stephen explains asynchronous programming with async/await and TCP sockets in C#"

[extra]
episode_url = "https://media.transistor.fm/b5857173.mp3"
+++

Stephen Cleary is the author of the Concurrency in C# Cookbook and a Microsoft MVP. He has also written many blog posts on asynchronous programming.

We discuss:

- Why he calls manual thread creation legacy code
- Using Async/Await and the Task Parallel Library instead of Threads
- APIs to avoid when writing concurrent applications
- Why you shouldn't write TCP Sockets
- Continuously reading from a socket to detect errors
- Building state machines to manage socket connections

### Related Links:
- [Personal Site](http://www.stephencleary.com/)
- [@aSteveCleary](https://twitter.com/aSteveCleary)
- [Getting Started with Async/Await](https://blog.stephencleary.com/2012/02/async-and-await.html)
- [TCP/IP Sockets](https://blog.stephencleary.com/2009/04/tcpip-net-sockets-faq.html)
- [There is no Thread](https://blog.stephencleary.com/2013/11/there-is-no-thread.html)
- [Concurrency in C# Cookbook](https://stephencleary.com/book/)

### Music by Crystal Cola:
- Intro: [12:30 AM](https://crystalcola.bandcamp.com/track/12-30-am)
- Outro: [Orion](https://crystalcola.bandcamp.com/track/orion)

---

### Transcript

You can help edit this transcript at [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy** This is Jeremy Jung and you're listening to Software Sessions. Something I've had to do in my career is socket programming. Talking to services or devices via raw TCP instead of a nice abstraction like HTTP.

I remember searching the internet for answers and finding almost nothing, plenty of posts on how to talk to an HTTP end point, or build a website with Javascript, but very little on raw TCP. But there was one exception, an FAQ from a developer named Steven Cleary.

I wanted to get his advice on how to write socket applications. It turns out he's also the author of the Concurrency in C# cookbook.

So I start by asking him, should we still be manually creating threads?

The creator of the Ruby programming language said that he regrets adding threads to the language. Is there still a need for manual thread creation in C sharp?

**Stephen** Boy, that's a great question. he didn't want threads at all in the language?

**Jeremy** So I think he didn't want a publicly accessible API to manually create a thread

**Stephen** Gotcha. That does make sense. One of the often quoted lines from my book is, as soon as you type new thread, that is. Use the thread constructor of the thread class. Um, you've already got legacy code. Um, that was one of my favorite lines to write, and it's been quoted several times.  And, and the reason is manual threads or manual thread creation in most cases is not necessary anymore.

If you're on windows, pretty much the only remaining use case for a manual thread is just COM interop. Which hopefully you don't have to do, but some people do. So, so  (laughs)  it still exists. these days there's so much, more that we can do just by putting work on the thread pool. Um, there's higher level APIs with parallel programming and things like that.

I am not at all familiar with the rust language  their standard library, but I'm sure that they have, every modern aPI like that. you know, Assuming you're not doing COM interop in that language (laughs), it would make sense that you wouldn't want to use a manual thread.

I think that's true for pretty much every modern language.

**Jeremy** Just to be clear, that was the creator of the Ruby programming.

**Stephen** Ruby, sorry, did I say Rust? 

Again, I'm not familiar with Rust either, I'm afraid, yeah. Ruby is a much higher level programming language and I can understand why they wouldn't want to encourage manual creation of threads.

**Jeremy** Currently you can create threads in Ruby, but there is a global lock on, the interpreter. So you can have multiple threads running, but only one of them can be executing at the same time. And so they're trying to figure out new ways of building concurrency primitives to kind of work around that. But the tricky part is, is that people who have built Ruby applications they've started threads in their own applications. And so if they change the behavior to for example allow things to execute in parallel it's going to break a ton of stuff.

And they can't do that. So it's kind of an interesting problem that they're trying to figure out going forward.

**Stephen** Right. Ruby is used so much that that would be a big backwards compatibility issue.

That sounds like a big challenge. Yeah. you know, go has a really interesting way of doing concurrency. that's very different from other languages. Most languages take a more traditional, here's your threads, Here's some higher level stuff you can do on top of it.

All the threads run concurrently with shared memory. You know, those are all kind of common patterns in most languages, but it sounds like the way forward for Ruby might be looking at something more like a. I don't know if I want to say quite like exactly like a go model, but something more like that where you have really independent, interpreters that don't directly share memory.

**Jeremy** I think they are thinking about something like that,  creating some kind of  lightweight process within their run time having some kind of restricted way of sharing data between these runtime processes. So I think that's sort of the approach they're currently considering

**Stephen** Yeah. JavaScript did something similar too, you know, there's actually the whole, I might get the terminology wrong here cause I'm not a Javascript genius, but,  I think it's a web is a web workers? they're, they're actually like a separate thread, but they can't directly share memory. So you don't run into all those kind of issues with the concurrent execution.

**Jeremy** Yeah. I was actually talking to one of the, the Ruby core team members and they were saying that they thought  one of the. forward thinking things that JavaScript did was it never allowed you to create threads, right? You just had the one, the one thread in your, your browser and so that's kind of what allowed them to come up later with, this sort of web workers concept. And because they had never given anyone access to threads, they could kind of force everybody to use an event loop pattern. Right? Because if you didn't have asynchronous cause, then everything would just kind of lock up in the browser.

And it also allowed them to, to bring in sort of this web workers concept later and not break everyone's applications.

**Stephen** Right. Yeah. I think forcing one thread definitely allowed them to develop more advanced asynchronous capabilities before a lot of other languages had it. .NET eventually, did kind of leapfrog them a bit with async and await later on down the line. But then JavaScript just picked it up right away. Like, oh, what a great idea. We'll take that too!

**Jeremy** We've been talking about concurrency, right?  in your words, like what, what is concurrency?

**Stephen** There's no standard for what all these different terms mean.  But I've always tried to stay consistent in my own writing, as far as what the terms, concurrency and asynchrony and parallelism actually mean. the way that I use these terms is concurrency is any way of doing more than one thing at a time.

So parallelism. Is using multiple threads to accomplish concurrency. It's one kind of concurrency. Uh, That's the way I use those terms. and that's what most people kind of jump to the conclusion of is, Oh, well, I'm doing more than one thing at one time. There must be more than one thread, because that's been true for most languages for decades.

I mean, unless you're doing old school asynchronous programming, which was so difficult that most people never bothered with it. It was cheaper to buy oversized computers than it was to train all the developers and to learn and maintain some horribly complicated asynchronous software.

These days. Asynchronous code is a lot easier. So it's becoming more mainstream. Concurrency being more than one thing at a time. Parallelism being one form of concurrency, using threads.  And then asynchrony being another kind of concurrency where you're not dependent on a thread,  you know, waiting for an operation to complete. Um, you're freeing up the current thread is, is really the core idea of asynchrony.

**Jeremy** I think one of the maybe misconceptions people have is when they're using the async await keywords, they may assume that things are running in parallel.  What's actually going on under the hood there?

**Stephen** Right. There's reasons that people think that, and sometimes it can actually run in parallel. Uh, so you can actually have code written with async and await that will run in parallel. Um, so it can definitely be confusing. But essentially the way that I describe it is the async keyword is first off, just like a marker for your method that really tells the compiler. I want you to take my method, chop it up into pieces and make a state machine out of it. this is to enable easier asynchronous programming. The older styles of asynchronous programming are much more difficult, and the async and await is really just a better syntax for doing asynchronous code. So that's the async keyword. 

The await keyword takes an argument, and this is true across every language that uses async and await. Um, so this is true across Python and JavaScript and C sharp and all the others. The await keyword takes an argument that can be in an awaitable the C-sharp term is awaitable   and the await keyword if that, uh, awaitable is not actually complete, it will return from the current asynchronous method. And when it returns, it returns an incomplete, awaitable, a task, in C sharp. And by combining this pattern you can create asynchronous code that actually yields off the current thread. And the whole idea is at the lowest level. You know, it's usually some kind of IO. 

So you've sent out some HTTP requests, for example, is a common one. You're calling some API. Well, you've sent out the bytes on the wire. No thread needs to sit around there blocked waiting for it to come back. That's the whole idea of asynchronous code. So you instead, await to receive that response and that thread is then freed up to do other things. That method returns. The thread can do whatever it wants, and then later on that task completes. Does that make sense? I don't know if I've ever actually tried to describe that using just verbal words before.

**Jeremy** You make a method call that is async, and inside of the method, you will have, lines of code some are just normal synchronous lines of code. So they execute from top to bottom, right? Like adding some numbers or something like that.

And then within the method, you may have lines of code that have await in front of them.

And, uh, whenever you hit one of those, if it's making an asynchronous call the example we'll maybe use is for HTTP client, right?

You can request some data from a URL, and so you're in this function and the HTTP client is asynchronous and you're putting await, in front of that asynchronous call, correct?

**Stephen** Yes.

**Jeremy** When I reach that point, it goes and makes the call and then the operating system is handling, the actual networking call. But while that's occurring, I guess the C sharp runtime or interpreter can actually leave that function and go work on something else. Like, for example, rendering the UI. Uh, while the operating system is still taking care of that, that IO operation, that network call.

**Stephen** Yeah. So let's work through an example. I like that example. 

So if you have a button click method, and this method is an async method, and it calls await on an HTTPClient Get. First off, every asynchronous method starts executing synchronously. So when you call like await HTTPClient.Get that's exactly the same thing as calling HTTPClient.get without the await getting the task back and then doing an await on that task so it synchronously sends out that data. And then while it's waiting for the response, it returns back an incomplete task, that task will become completed later when the operating system gets the response back.
Now. Our code, it returns to our code. Our code then does the await we await on that task. Await looks at the task. It's not complete yet, so it actually returns back from that button click event handler. And at that point we're actually returning back to the UI main loop. So the UI can continue to be responsive.

Now later on, that response comes back. And so that task that was returned from the get async on HTTP client is completed now, and then that causes our method, our event handler, our button click event handler to continue executing to resume executing at the point of that await. One phrase that I use is an await can pause that method. It doesn't pause a thread, it doesn't block the thread, but it pauses that method. And then later on, after that task completes, that method continues executing. And then picks up from where it left off and just continues executing on down. So that's an example of an asynchronous method resuming when its task completes.

**Jeremy** And throughout this whole process, you only have one thread, is that correct?

**Stephen** Yes and no. Um, The whole idea behind async and await  or asynchronous code in general, is that There's no thread that's blocked, waiting for that response to come back. Now there are other threads involved. So the operating system,  when it receives the packet on the network or whatever and it may need to wait for several packets. Right? So there's actually like a ThreadPool thread that's kind of borrowed it checks. Oh, is the response complete yet? Okay. Yes or no. so there's a thread pool thread that's kind of used very, very briefly, you know, in the conclusion of that.

And this is a normal thing with most asynchronous operations, it does kind of implicitly depend on the presence of available ThreadPool threads as well. There are very briefly used other threads. I have an article on my blog called, "there is no thread" that explains that in more detail.

So the idea is there's few other briefly used threads, but the idea that there's a thread blocked waiting for that response to come back, that's not happening with asynchronous code whereas it would with the synchronous code. If you're using the old web client allowed both synchronous and asynchronous methods. If you're using it a synchronous web client method, well you are blocking that thread until the response comes back.

**Jeremy** But in sort of this whole sequence of events, the user never had to really think about that thread. They never had to worry about, scheduling this HTTP request to happen. because  the standard library or the construct of task and async await that's built in to .NET has sort of handled that all for them.

**Stephen** Yes. And the vast, vast majority of the time, you never even have to think about it. It does occasionally come up if you're doing something that completely exhausted the ThreadPool. there are situations where then you can have asynchronous tasks unable to complete, or they're delayed from completing because there are no available ThreadPool threads.
That's very rare, but it can happen.

The vast, vast majority, and I mean like over 99% of code doesn't have to worry about it. the, the default settings on the ThreadPool from Microsoft  are very well tuned and they pay attention to all of their metrics, very closely and, and have put a lot of work into the default values.
That said you can change them. There are settings that can set to influence a thread pool. Tell it to have more minimum threads at all times and that kind of thing. But by and large, the defaults are appropriate and the ThreadPool self tunes over time. So if it's busier, it, it'll add its own threads, and when it's less busy, it'll kill some off. again, Microsoft has put a ton of work into having a thread pool that, easily handles the vast majority of scenarios.

**Jeremy** And when you're making, let's say, a set of HTTP requests, let's say you made four in a row, is there any kind of guarantee of the ordering of when those requests will happen.

**Stephen** So yes, you can by default asynchrony just the async and await keywords if you await one thing. And then await the next call and then await the next call and then await the next call. Yeah, those will always happen one after another in order. asynchrony does preserve the order of the code.

Now there's another way that you can work with those kinds of calls. And that is, it can make all four calls at once and you can take all four of those tasks that are returned and use a library method called Task.WhenAll, and what that does is it gives you a task that completes when all four of those tasks have complete.
So you can say just await Task.WhenAll, and stick all four of those tasks in there. And then you know that they are all complete. And then, and in that case, you're actually doing an asynchronous form of concurrency where you have four different requests all going out at the same time. And when they all come back. All those responses come back. Then your code resume is executing after that await.

**Jeremy** In that case, when you're doing the WhenAll, and they're executing at the same time.  I guess we can't assume order anymore because like you said we can consider them to be effectively happening at the same time.

**Stephen** That is correct, yes. Anytime you're using Task.WhenAll or Task.WhenAny those multiple tasks, they can be concurrent. And that's actually kind of looping back to where some people have played around with async and await in like a console application, for example. And they can observe this behavior where:

Hey, you know, I've got all four of these methods doing something at the same time, and they can even be on different threads because the console application by default will run your code on a thread pool thread after it resumed from an await. It has to run it somewhere and on a console application, that's a logical place to run it.

So a lot of people first learning async and await, it's not ideal because a lot of people, when they, when they are first learning about a subject in C sharp, they will start up a new console application, to play around with it. And that, that's totally normal with async and await.

It's usually better to actually start up like a windows forms project or a WPF project and play around with async and await in there, because that scenario is different. Than the console application. A lot of things in the console applications end up on the ThreadPool, just because they have nowhere else to run whereas in a UI application, it's a more normal scenario for async and await, I'll put it that way.

**Jeremy** Yeah. so C sharp as a language has been around for, I think it's been 20 years now. Right? 

**Stephen** I don't know  (laughs) 

**Jeremy** It's been a while  (laughs) 

**Stephen** In its early days. I refused to touch it, so  (laughs) 
I was strictly C plus plus back then.

**Jeremy** And over the years there's been many ways of doing things in terms of concurrency. If it were up to you what are the ways of performing concurrency that you would remove or encourage people to, to not look at when they're building new applications?

**Stephen** Oh boy. That's a great question  (laughs) . I'm going to get myself in some hot water here cause I don't know if I've ever told anybody all these, well, the thread class obviously. really these days it should only be used for COM interop. There are certain things that you just should never use.

Um, the task constructor, for example, you should just never new up a new task. And, and that's something that, again, you know, people who are coming into task, who have never used task before, what are they going to do? You know, the very first thing, their first sample code is going to be new up at the task, and that's, and they have no way of knowing that's completely wrong.

So the task constructor is definitely something that should never be used. there's a lot of things that have unsafe defaults. Task.Factory.StartNew, you see around quite a bit. I really discourage its use. if you want to run something on the ThreadPool use Task.Run. If you want to run something somewhere else with a custom scheduler, then use a task factory, not Task.Factory. Those are very different. There's some discussion on the task type itself. I'm kinda content with where it is, but because it can be two different things, it can either represent code that can run or it can just represent this future or promise type of something that's going to complete in the future. And the second way is how it's usually used in async and await. And the first way is how it's usually used in the task parallel library. So you've got this core type task. That's like the main type being used by async and await. Although these days we have value tasks and other things now that are becoming more common, but it's still the main type used in async and await and it's also the main type used in the task parallel library. But the way it's used is completely different in those two worlds.

There was some discussion, when Microsoft was creating async and await about should they create like a new promise type instead, maybe, maybe not. It's really hard to look back and say. Even now years later, it's really hard to say, yes, that was the right decision, or, no, that was the wrong decision. I'm content with task. but, but the one other thing, and this is where I might get into some hot water that I would say never use, is all these methods that say, run this code on the UI thread.

So there's several different methods like that.  Winforms had Control.Invoke and then dispatcher has something, I can't remember now, but you know, essentially I think it might actually be an invoke async on dispatcher or core dispatcher. Um, so WPF has it UWP has it, all these different things, have this way of saying, run this code back on the UI thread. And that's wrong. I'm going to go out on a limb and say, I can't think of any good reason to use that code. It almost always makes the code less testable and less maintainable, and there's better solutions out there if you want just to, get the results of something back to the UI thread, then return it and use await or something like that. If you want to notify the UI thread of progress. Then use  IProgress of T. There's an interface specifically for that. So I think that those API's  have encouraged code that doesn't really follow best practices and is harder to test as a result. Harder to reuse.

**Jeremy** Yeah, I guess you would say the proper way to do it rather than using these calls that explicitly say, I need to run this code on the UI thread, you would do something more, implicit, like you were saying, if you have a event handler for something happening on the UI, like a button click for example, if you used, 
async and await, it would automatically bring you back to the UI thread whenever you, hit one of those await calls. And that's preferred rather than saying, you know, like the Control.Invoke example, you're referring to.

**Stephen** Right. The way I kind of think of it is what you want is your UI or your controllers and things like that. In ASP.NET you want that edge code driving your business code. What you don't want is your business code driving the UI.
You want the UI to drive the business code and display its progress and its results and things like that. You don't want your business code to even be aware that there's a UI.
**Jeremy** Okay. Yeah. Let's say you clicked a button and that called a function. That's sort of your business code. the business code would have to use this Control.Invoke call  it would have to know that, Hey, I need to return my value back to the UI thread, but that, that shouldn't even be its problem.

**Stephen** Right. And then there's usually like a pass off of here, business code. Here's the control that you should use to, you know, to, to synchronize back to the UI code. And then the business code actually knows about the UI when it shouldn't. Now that's more of like, you know, a purity thing. I wouldn't like, you know, die on a hill for it or anything like that, but I would prefer that those APIs didn't exist because there are better solutions out there.

**Jeremy** How about other examples? Like WebClient versus HTTPClient?
Are there examples of classes that, you know, were created before and they made sense, but then now you probably shouldn't use them anymore?

**Stephen** Well, that's a good question. That one has a more nuanced answer because there's some benefit to being able to run synchronous code, sometimes even IO. you know, web client code can be a synchronous, and in some cases that's what you want. you don't need the asynchrony.

And I am speaking more from like a, a practical matter here because. I would say, yeah, make it asynchronous. It's IO based. It should obviously be asynchronous, but then you have to kind of manage that with, okay, well we only have so much time in a day, and this whole project is already using synchronous code.

Is it worthwhile to change? Well, that's a whole different question. Right? You've got like the purity aspect of it of, well, yeah, of course it should be asynchronous. And then you've got the more real world aspect of, yeah, maybe someday, but not right now. And so I think that WebClient in particular?

I don't really see a problem with it. Sometimes it's easier to do a synchronous call than it is to do an asynchronous call and find some way to block on it. If you're not ready to go to adopt asynchrony in that part of the code.

**Jeremy** It's more in the context of if you have an application that wasn't written with asynchrony in mind, right. Not necessarily for new applications.

In your book you said on the server side and you gave asp.net as an example. You said parallel processing is rarely done because the server host already does parallelism and for this reason, server-side code shouldn't perform parallel processing.

What did you mean by that exactly? And how should people think about that when they're writing ASP.NET applications?

 **Stephen** That's a problem that I've seen other people do. That's a problem that I've done. Uh, rather, embarrassingly, even. Knowing better, like after I wrote that, I actually had a situation where I wanted to, to really reduce,  the round trip time for a certain request on asp.net.

It was one request. You know one route and the only way to do it is through parallelism because it's CPU bound. So it's doing a lot of CPU work. And so I actually went ahead. I said I know what I'm doing and I made it parallel and the server performance just died. I mean it. It was horrible. And I ended up reverting it just a couple of days later and said, all right  (laughs) , lesson learned I should have followed my own advice. 

The reason is ASP.NET is a multi-threaded server to begin with, so it's already using the thread pool.  So use asynchrony on ASP.NET absolutely. Because then that frees up those ThreadPool threads to handle other requests. You can handle many more requests using asynchrony on ASP.NET but using parallelism on ASP.NET where you're using those multiple threads together well now, instead of one thread per request, or even the zero in the case of some asynchronous calls, while, it's in the asynchronous part, it's actually using zero threads. So instead of using zero or one threads. Now you're using, 10, 12 threads to process one request, and then that very quickly throws ASP.NET off.

ASP.NET is designed around the idea that it controls the threads. You know, it passes out the threads to the requests, and if one request suddenly takes 12 threads from the thread pool,  it doesn't respond well to that.

**Jeremy** Using asynchronous calls is good. So using async to do IO when you're in an ASP.NET request is good. But what you might need to think a little bit more closely about is if you're running a lot of tasks or you're using, the parallel library
library things like that.

**Stephen** Yes, exactly. Anything with a Parallel or a Task.Run. Should, in most cases be avoided on ASP.NET. You know, if you're talking internal website and you know there'll never be more than two users or so at a time or something like that, you know, this is special scenario, but if you're, if you've got anything public facing, I would, I would not use Parallel or Task.Run on ASP.NET at all.

**Jeremy** If you have something that's fairly CPU bound, how would you recommend running that?

**Stephen** On ASP.NET? Just run it directly, right on the requests thread that, that's what I would say. So don't use Task.Run so let's walk through an example of that. Just real quickly. Async and await, lets you yield a thread. It lets that thread go back to the thread pool, which is great. on ASP.NET especially, you know, you can scale your server out, you know, to handle 10 times as many requests if they're all asynchronous many times.

So some people think, well, I want to use async and await and I've got this CPU bound or this CPU bound code, so I'm just going to throw it into a Task.Run, and then I can await the Task.Run. Well. Yes. But walk through what happens here. Your, your request starts running asp.net hands you a request thread, your request starts executing, your handler starts executing, and then you send some code to Task.Run, which takes another thread from the thread pool to run that code. And then you await the task.run, which allows you to return your original thread back to the thread pool.

Well, yeah, you've returned that original thread, but you're also taking another thread and now you've got, you know two threads interacting and it's actually slower. You know, you've got the task switching and all that. so it's actually slower in the end. And you didn't actually solve anything by using Task.Run on ASP.NET. 

In the UI scenario completely different. Right? Because you have one thread that's special, the UI thread, you want to use async and await on that in order to free up the UI to remain responsive. In that case, you don't want to run the CPU bound code directly cause it would block up your UI for a few seconds or whatever. Instead you can toss it into a Task.Run and await that, and now you are running that on a ThreadPool thread and you're awaiting back allowing the UI thread to be responsive.

So it's a great pattern to use in UI applications, but not one that should be used on ASP.NET applications.

**Jeremy** Does it ever make sense to, I know in some other languages still use the concept of job queues. If the requesters are making things that are fairly CPU bound, are going to take some time, is there any equivalent to that that you might consider in asp.net?

**Stephen** Job queues... So you're saying like, like if a request comes in, you want to do something, it might take some time. So in the meantime, you know what, what are you going to do? Is that requests, can you actually send the response yet or are we talking more like a and more like background kind of work?

**Jeremy** I'm thinking more like it could be sent to say another process or another server to kind of do the work. and then you could respond back. but in the meantime, you're not just holding up that one server. You know, trying to process the information.

**Stephen** Gotcha. Right. so async and await doesn't do that. Uh, some people. When they first start using async and await on asp.net, they think, well, if I await this, then it should return back, you know, an HTTP response to the client. But that's not actually what happens. Uh, when you await on async or on asp.net when you await, you're actually just yielding that thread back to the ThreadPool. The response has not actually been completed yet or sent yet. So there's nothing like that built into asp.net. But that is a pattern that is very common. So you have a very reliable queue, way back in the day, I would've said, MSMQ believe it or not. Um, but  (laughs)  these days, you know, it's more like Azure queues or AWS simple queues.
You know, some kind of like a reliable queue where you write to the queue and then, you know the message is there and then you can return back, you know, maybe some kind of an ID or something. Hey, you know, this is, I started your job for you. and then your client can be notified or poll for the response or the result of that job, which can happen sometime later after a backend process has actually processed the queue.

**Jeremy** When you write an asp.net application, you can specify whether your controller actions are async or not. I think some people assume they should make everything async, and some people really just don't know. What would be your advice there?

**Stephen** Well, so the, the Microsoft defaults.  I think are all async these days, you know, especially if you're looking at ASP.NET Core, you know, you say, give me a new controller. Well, it gives you all asynchronous methods. And some people have questioned that saying, why are the defaults asynchronous? And I think the reason is most of the time they're doing some kind of IO, oftentimes with a database, right?
You're either reading or writing to a database at some point during the handling of that request. Um, there are some that don't. But I think most controller actions are naturally asynchronous these days. but the thing is if it doesn't have any asynchronous work to do, then yeah, absolutely make it synchronous.

I've seen some confusion the other way too saying, well, should we just make every method everywhere asynchronous? Well, no, absolutely not.  if you just have synchronous work to do than just keep it synchronous.

**Jeremy** In terms of ASP.NET specifically, do you think it's kind of worth the cognitive load of someone deciding which one should be sync and which ones should be async or, by default, would they just leave it as async?

**Stephen** Well, so if you, if you have an asynchronous method, like one actually marked async and you'd never actually await anything, the compiler will give you a warning and it'll say, Hey, you know, you're not actually doing any asynchronous work in here. And you can use that to clean up the code. 

Similarly, if you have a synchronous method, and this is the way that I prefer to transform code from synchronous and asynchronous is you find some API that you're calling like a database query and say, well, that's doing IO, that should be asynchronous and then you await it right? And then the compiler will say, Oh, you're using an await without an async, and it'll guide you into transforming that method signature and all that. It'll say, right in the compiler error, Hey, your method should actually look like this, and you can take it right out of there and just paste it right in.

**Jeremy** Yeah, so actually you don't have to think too hard because visual studio or whatever IDE you're using will kind of give you hints in terms of, Hey, you made this function async, but you really don't need it to be, so go ahead and fix it for me.

**Stephen** Right. Yes. Yeah. The the thing that you don't want to do that I've seen some people do is say, well, I need to await something, so I'm just going to await like some random, I've seen like await a completed task, or you know, await Task.Yield, um, just because they think they need something to await.

But that, that's the wrong mentality. Your code is actually synchronous. So give it a synchronous API.

**Jeremy** Maybe about 10 years ago you did a lot of posting on writing socket applications or programming TCP/IP. With the current API that C# provides,  what would be your advice to someone who is, creating and managing longterm TCP/IP connections? What are the classes they should be using and what should be their strategy?

**Stephen** Boy. That's a good question. As far as like raw TCP/IP sockets go, my very first piece of advice is always don't do it  (laughs) . Um, uh, because there are a lot of pitfalls when you start going down that road. yeah, so I would say, you know, first try your best not to do it. use HTTP HTTP2, uh, WebSockets, you know, SignalR or maybe use something like that.

There's newer ones coming you know that the Google one.

**Jeremy** GRPC?

**Stephen** Yes. Thank you. GRPC use something like that if you possibly can, um, that has an established standard that, handles all of the really low level details for you. But if you really can't avoid it and sometimes you can't, I have always just used the socket class directly, for a couple of reasons. One is it's pretty close to the Berkeley socket API, so that you can actually take things written for like Unix systems and say, all right, so this is roughly equivalent to this socket code in C sharp.

And also you know exactly what it's doing. The socket class is a very thin veneer over the Winsock APIs, which are pretty much Berkeley with some more advanced stuff around asynchronous capabilities. But yeah, that's what I would actually recommend.

I mean, they have stream based abstractions and things like that, which I'm not as familiar with, to be honest. I've always primarily used the socket class or my own kind of like wrappers around that.

**Jeremy** So, um, cause I believe their TCP client class. They have asynchronous methods for connection, they give you access to a network stream that also has asynchronous reads and writes.  And I think what you're saying is you maybe don't recommend people use that and instead they use the socket directly

**Stephen** Yeah, and, and again, you know, part of it was because, you know, when I learned TCP IP that was like the late nineties it was like 98 to 2000 was when I learned TCP/IP.

And the reason I learned it was because nobody else at the company wanted to learn it. We had to add it to our product. Nobody else wanted to learn it. All the old programmers were like, not me. Make the new kid do it. So I got, I don't even remember what books they were, but I had three books this thick. I kid you not and buried in these books because the internet didn't help. Buried in these books where all the lessons that I eventually put into the blog posts, yeah. 

Like 10 years later I finally wrote it all up, but I learned all that like 10 years earlier from these huge thick books, cause it wasn't around that information just wasn't there. You couldn't find it. So it was a tough journey. And it was all Berkeley, right? Everybody used the Berkeley sockets. That's like universal and the socket class is the .NET equivalent of that. So maybe it's, I dunno, I actually, I should give TCP client a try. I'm actually talking on TCP sockets two months from now. I'm giving a talk on it,
It depends on the, the. the protocol that you're using, but some, a lot of protocols require you to have a continuously going asynchronous read. Um, you have to have a continuous read going at all times in order to detect some error conditions. So just as long as you're doing that continuous read, I think using either one would be fine. Personally, I don't mind passing buffers around as opposed to reading from a stream. But, I think really that's, that's the main advantage that TCPClient gives you, right? It's a stream abstraction. Another big thing to keep in mind there is that there's actually two streams. There is an input stream and there's an output stream and you want to treat those completely separately.

**Jeremy** A lot of times when you're working with TCP devices, there's this request and response flow where you're writing something and you need to get something back and you need to kind of associate or I guess connect the two together. Right.  what's kind of your, your strategy for that?

**Stephen** Your simpler protocols are really just like one command, and then the response comes and you never have more than one command in flight. Those ones are easy because the response is always for the last command. For ones where you can overlap, or even have commands going either way... for those ones, I tend to just use a dictionary. You've got that look up, here's all the requests that I have in flight, and then when one comes back you can just look at it right up in the dictionary there.

The one tricky part about command response, protocols is, is how to detect when it's gone dead. This is something that we don't really think about, but after a TCP/IP connection is established there's nothing that guarantees it's still established. One of the things, or one of the API that I really dislike is the IsConnected on the socket because it doesn't actually mean it's connected. It means, as far as I know, this is not connected  (laughs) . That's what it actually means. It's not like, Hey, I just checked it. It's still connected. No. That's not what it's doing. after a TCP connection is established and those packets have gone back and forth establishing the connection, unless one side sends data over that connection, no more packets go through it.

So you have no idea if that computer has been rebooted, if your application has died on the other end, if, you know, if maybe the routers have gone down in between and there's no longer a path over there. you have no idea about any of that stuff until you actually try to send. And so for this reason, in order to detect those kinds of scenarios, a lot of command response protocols have like a heartbeat message.

So it's, it's a like a NOOP message. You just send it out every 10 minutes or whatever, however long you you want to put it for. And the other side just says, yep, I got it. Now once you send data then the TCP IP protocol will kick in and retry and stuff like that if necessary, and then eventually give you back an error saying, Hey, we couldn't actually deliver this packet, but you actually have to send data in order for that to happen.

**Jeremy** And so let's say when you have a bunch of connections that you're establishing at the same time.. How would you structure your application to make all those connections and to make sure that the back and forth between each of them is isolated?

**Stephen** I have worked on systems that would try to establish a bunch of connections at once. and the, the main thing is, you know, you end up like with a kind of a state machine for each one, and that's what you want to do is separate or have a separate state machine for each one of those.

**Jeremy** And for each one of those, you would have a separate,  I don't know if the term is connection, but you said for both input and output, you would handle those separately, right? What does that look like?

**Stephen** Yes. Yeah the key there is that there's actually two streams per socket connection. And again, a lot of times that gets overlooked cause we think about it being one stream. You know we send data and we receive data. There's actually two streams. There's a sending stream and a receiving stream.

I don't know if sending and receiving is quite the best terms for those, but from one, from each side, there's a sending and receiving stream. And those are actually separate streams. And what you want to do is, in in the general case, you want to be reading all the time. So you're constantly reading.

As soon as one read completes with and gives you some data, you want to start another read immediately, even if you're not expecting  any kind of packet because well think about those heartbeat packets for example.  When you write to the outgoing socket stream, that write is considered complete, not when it reaches the other side of the stream, but when it actually gets to the network layer of the operating system.

At that point, your write is complete. It was successful. The end, you have no further indication of whether it even gets to its target or not. If the underlying network layer tries to send that packet out and they can't find that machine, it's not running anymore, whatever, it will flag an error on that socket.

But it has no way to get you that information. So your socket now knows it's in an error state, but your write already completed successfully. You will not know it's in an an error state until you either write again or whatever. If you have a continuous read going on, then that gives you a way for the operating system to say, hey, you know, this socket just died. I tried to send data, I couldn't get it through. Your socket's dead now. That continuous read allows you to detect when errors happen immediately or as soon as possible as well as read any actual incoming packets and be ready for that.

**Jeremy** And so that also means that as soon as the read recognizes there's a failure, then you would know not to attempt to write again and maybe just to recreate the, the socket. Is that what you would typically do?

**Stephen** Yes. Yeah. So for error handling, pretty much, no matter what the error is, you should always just close the socket. That's been my go to error handling forever  (laughs) . Um, just close the socket. Don't try to recover anything, just that, that's, that's the end of that socket. As soon as an error, any error happens, And then usually you want to wait a bit, just in case, because sometimes there are some errors that can happen immediately. Like if your local network cable is unplugged and your computer has no network. The, the operating system will give you an error immediately and when you try to connect to something,  but you don't want to be like stuck in that tight loop retrying immediately and getting immediate errors. Generally speaking you want to delay a second or two before retrying.

**Jeremy** And when you have sort of this flow of your application or people being able to, to make requests over the socket, do you need to have any kind of semaphore or any kind of limitation preventing people from sending commands while a previous one is being sent.

**Stephen** Okay. Well, that depends on what your application is doing. To be honest, a lot or most of my TCP IP work has been with non-public facing sockets. So it's things on dedicated networks with I guess you could call them, like IOT device kind of things. In that scenario, I've focused more on getting it working and less on security but especially for anything public facing, you need, guardrails around everything. 

If somebody tries to send you a packet that's two gigabytes, you know, you have to say no, you know, or message, that's two gigabytes. Um, so there's limitations. And if you look into like HTTP the protocol, for example there's very little security built into HTTP as well.

They can send whatever message length they want, and then it's up to. Servers like ASP.NET or IIS to say, well, we're going to put like a reasonable limitation on how much, how much data you can throw at us and that kind of thing.

**Jeremy** Right. I guess I'm thinking more in terms of if we use the example of an IOT device, and let's say there's a command to,  just to turn on a light, for example, and you can make a request to the device to turn it on and it'll respond with, Hey, I turned it on.  If somebody makes a request to turn on that light and while it's in the process of being sent, they click the button again and say I want to turn it on again. Inherently in how the asynchronous programming works. Will it wait for the first request to finish before the second one gets made?

**Stephen** Oh, so if you're talking to the same socket. so there is a stream abstraction for sockets. So one request will go down. And then unless there's something in your code to prevent it, the next request will follow it right away. It will see that as two requests to turn the light on. And maybe that's something you need to prevent with your device and maybe not. It depends on the device. Maybe you can only handle one request at a time or something like that and say, well, we don't want to send the next request until we get a response.

If that's a limitation of that device then yeah, your code would have to manage that in like some kind of a state machine kind of way. And maybe you can NO-OP that second one, you know, treat it as like, while we're driving to the steady state instead of sending commands. There's different ways to model that really depend on the device you're working with.

**Jeremy** But in terms of the stream abstraction, that would force the first write to complete before the second write starts? Is that correct?

**Stephen** Yes. So as long as you write the one command, and it is completely written and then the second command comes in, then yeah, it would be one after the other. This is more rare, but it is possible that a write can partially complete. And you don't want to be in the situation where we've got like one write that partially completed and then another command got written to that NetworkStream that is possible to happen with raw TCP/IP sockets.

But yeah, I mean, it is rare, but it is possible. So you would want to have like a queue of writes  if you're going to allow that kind of usage.

**Jeremy** Okay, That would not be taken care of,  by the stream abstraction. You would actually have to keep track of, I finished my first one,  the second request I need to queue until that one is done.

**Stephen** As far as I know. Yes. I have not looked at the TCP client internals. so it is possible that say they're doing their own queuing because you can write that and expose that as a streaming  abstraction. It is possible to do. Um, I don't know if they're doing that or not.

**Jeremy**  Are there any other things that you can think of that, that people commonly get wrong when it comes to to socket programming?

**Stephen** Mmm. Yeah. There is one other major topic that is a very common question actually. And that is a lot of people. Well, you know, like I had TCP/IP in college and we learned all about the network stack and the OSI layers and all that thing.  And along the way I learned, TCP/IP splits stuff up into packets and sends it over the network, and then those packets are reassembled. That made sense. Um, but I think of that notion of a packet, throws people off sometimes because they get the idea and I did too when I started doing TCP/IP that I can send a packet and I can receive a packet that's not at all what we're doing when we're writing with sockets.

Our abstraction is a stream. It is not a packet or even a series of packets. It's actually a stream. There's no way to send a packet, and there's no way to detect where the packet boundaries are when you're reading from a stream, or were should say, cause they're not there anymore. This idea of a packet I think trips people up. Because they think I can send a message and that message will be received in its entirety in a single call to receive from the socket or read from the stream. And this is a problem, especially I think, because people try it out locally and the operating system will say, okay, yeah, you sent this much data, I can send it right over it's no problem. There's no delay. It's all in one packet. I don't know if it even gets to the network layer, honestly, it knows it's going to the same machine, it acts that way locally. And then they actually tried to use that in the real world and it all falls apart because it's not actually a packet abstraction. It's a stream abstraction. 

So if you're sending a message, you have to somehow say, this is how big my messages are that's encoded in the message. Use length prefixing or delimiters, to divide up messages. Those are the two most common ways. HTTP has this really weird thing where in one of the text headers as ASCII text and it's optional, so it may not be there. HTTP. It was uh, it was designed pretty early on. In people's understanding about sockets. And I think if you look at HTTP2 now, completely different protocol,  much easier to program against. I think.

**Jeremy** Yeah, so that's kind of interesting. So you're saying in HTTP1. there's no guarantee that you'll actually know, how large the messages, how many bytes you need to read in. Is that correct?

**Stephen** Right. I know that's true on the response. I'm not sure about the request headers, but I know it's true on the response you can send, you know, you can send to your headers, but not include the content length header. And then just stream a bunch of data. And you know, whenever you close the socket is when it's done, essentially.

**Jeremy** Yeah. Cause I guess because HTTP, when you make requests the expectation is that when you're done, you close the connection. 

**Stephen** Originally, yes. Originally. Yeah. And then they had the extensions where you could keep the connection alive. With HTTP/2, I think you could even do like multiplexing. So you're doing like multiple simultaneous requests over the same connection.

It got a lot more complicated. But you can see the difference between a Content Length header and not when you download a file. Because if the server gave you a content length, you can see the progress bar filling up. If it did not give you a content length, you just see it spinning right? It's like I don't know how, how far along we are, but I've gotten this much so far, you know, cause that's all, you know.

**Jeremy** That's interesting. Yeah. I never, never thought about the reason behind that.

So I think we're, gonna start wrapping up, but before we do, is there anything else about async programming, socket programming or anything you can think of that you think we should have talked about or mentioned?

**Stephen** Oh boy. Um, yeah. I would say use async if you can. Don't use raw sockets if you can avoid it  (laughs) . Uh, that's about it. I think.

**Jeremy** Where can people  follow you, see what you're up to and, and check out your book "Concurrency in C#"?.
**Stephen** Yeah. So most things are on my website, stephencleary.com. I've got a link to my book from there, I've got a blog, which I've been neglecting lately. I'm so sorry. Uh, uh, I'm occasionally on Twitter, Oh, stack overflow. Of course. I'm on stack overflow a lot. I answer a lot of questions there.

**Jeremy** Thank you so much for coming on the show, Steven.

**Stephen** Well, thank you for having me, Jeremy.

**Jeremy** That was my conversation with Steven. If you want to get show notes or a transcript for this episode, you can get that at softwaresessions.com
I'll see you in a couple of weeks.

</div>