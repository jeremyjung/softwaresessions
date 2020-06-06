+++
title = "Building Scalable Systems Safely in Ruby with Samuel Williams"

description = "Samuel explains the difference between concurrency and parallelism, the dangers of writing multithreaded code, how languages like Node, Go, and Erlang safely handle parallelism, and his efforts to improve the Ruby concurrency ecosystem."

[extra]
episode_url = "https://media.transistor.fm/710f68e5.mp3"
+++

Samuel is a member of the Ruby core team.  He's working on making it safer and easier to write concurrent applications in Ruby.

### Samuel
- [Samuel's website](https://www.codeotaku.com/index)
- [@ioquatix](https://twitter.com/ioquatix)

### Conference Talks
- [Fibers are the Right Solution](https://www.youtube.com/watch?v=qKQcUDEo-ZI)
- [The Journey to One Million](https://www.youtube.com/watch?v=Dtn9Uudw4Mo)

### Related links
- [Asynchronous Ruby](https://www.codeotaku.com/journal/2018-06/asynchronous-ruby/index)
- [Fibers Are the Right Solution](https://www.codeotaku.com/journal/2018-11/fibers-are-the-right-solution/index)
- [Early Hints and HTTP/2 Push with Falcon](https://www.codeotaku.com/journal/2019-02/falcon-early-hints/index)
- [2019 Ruby Association Grant](https://www.ruby.or.jp/en/news/20191031)
- [Source with comments on why the Global VM Lock exists](https://github.com/ruby/ruby/blob/master/thread.c)

### Ruby gems
- [Async](https://github.com/socketry/async)
- [Falcon](https://github.com/socketry/falcon)

### Timestamps
- 0:51 - What's concurrency? What's parallelism?
- 5:49 - Piping commands between Unix processes provides easy parallelism
- 6:58 - Some types of applications abstract out threads/processes,
- 9:27 - Many Ruby gems have thread safety issues
- 10:44 - The CRuby Global VM Lock hides thread safety issues
- 11:24 - The problems with threads and shared mutable state
- 13:58 - Examples of mutexes causing problems in Ruby gems.
- 19:09 - What a deadlock is and how it causes problems
- 19:51 - Running separate processes to get parallelism and using an external database to communicate
- 21:01 -  Lightweight process model used by Go and Erlang vs threads in Ruby
- 23:50 - Why async was created
- 24:38 - What is Celluloid? (Actor based concurrency for Ruby)
- 26:29 - Problems with shared global state in Celluloid
- 27:12 -  Lifecycle management problems (getting and cleaning up objects)
- 28:19 - Maintaining Celluloid IO, issues with the library
- 29:43 - What's async?
- 32:00 - What's an event loop?
- 35:20 - How tasks execute in an event loop
- 37:29 - How IO tasks are scheduled with IO.select
- 39:41 - The importance of predictable and sequential code
- 41:48 - Comparing async library to async/await
- 45:23 - What node got right with its worker model
- 47:10 - How async/await works
- 48:35 - Fibers as an alternative to callbacks
- 51:10 - How async uses fibers, minimizes need to change code
- 56:19 - Libraries don't have to know they're using async
- 64:55 - Reasons for the CRuby Global VM Lock
- 67:13 - Guilds as a solution
- 69:14 - Sharing state across threads
- 71:33 - Limitations of Ruby GC at 10-20K connections
- 72:00 - Sharing state across processes
- 73:12 - Handling CPU bound tasks with threads and processes
- 77:42 - Which dependencies are messing with state? (Check memory allocations, sockets closed)
- 85:00 - Async in production
- 87:17 - Wrap up

---

## Transcript

[Click here to help me correct the transcript on GitHub!](https://github.com/jeremyjung/softwaresessions/edit/master/content/episodes/2019-11-06-building-scalable-systems-safely-in-ruby-with-samuel-williams/index.md)

<div class="transcript">

**Samuel** Thank you. Yeah, it's really great to be here. 

**Jeremy** A lot of these topics are related to performance. Let's get the ground terms defined first.

What is concurrency? 

**Samuel** There are lots of different ways of defining this terminology but it is helpful to have a shared understanding which is consistent. Otherwise, you can say one thing and someone understands something completely different. I like to use an umbrella term asynchronicity which means without time.

And under the umbrella we have concurrency and parallelism. They are similar terms and you can argue that they mean the same thing but I tend to think of concurrency as interleaving work. If you have a job and you execute that and you have another job, which you execute and interleave those units of work on the same processor, then that's a form of concurrency because you're sharing the one processor with multiple tasks.

If you look at parallelism, it's when you have two tasks which are running simultaneously on two different processes. So those two different concepts-- one is sharing a single unit of hardware between multiple tasks and one is running multiple tasks on multiple independent processes.

**Jeremy** Essentially when you have parallelism, you're saying you have concurrency because concurrency is working on multiple tasks at the same time, but not necessarily executing at the same time. Is that correct? 

**Samuel** I like to be a bit more specific with the separation of those two terms just because I think it's helpful when looking at actual programming models.

I like to separate them out. I like to think of parallelism as strictly when you have multiple hardware units and multiple jobs running on those hardware units independently whereas concurrency is sort of strictly running multiple jobs on a single hardware unit. Now of course you can you can mix and match it together. 

For example any job that can run concurrently could also be considered running in parallel if you consider one processor to be parallel. But it's kind of a misnomer you think-- Okay, well parallelism means at least a minimum of two things. You can't have a line parallel without some other line it's a relationship between two things. 

So yeah, I like to think of those things strictly as being different just because I think it's easier to talk about the different models. If you decide to blur those lines, then it's more difficult to talk about concurrency and parallelism and how they impact models of programming and models of computation. 

**Jeremy** You prefer to keep them completely separate. So let's say you have a single core CPU. It can only be doing one thing at a time so that could at most have concurrency. But as soon as you introduce a dual-core CPU you would say that my program or my tasks are executing in parallel and not really using the term concurrency.

**Samuel** Yeah, I mean ultimately when you have two cores then you can run tasks on those cores in a concurrent fashion. But you can also run two jobs completely independently and they run in parallel. So I guess the value of it is that when you talk about parallelism you start needing to think about synchronization primitives across multiple cores. Whereas with concurrency you are limited to the issues that arise only when interleaving jobs. So the nature of the synchronization primitives needed is quite different.

If you think about normal computer programs that run in sequence you're essentially interleaving one statement after another. It's a little bit confusing to think about it like that but in that sense the dependencies just follow naturally from the sequential processing.

If you tried to run every line of a computer program on a different CPU core you would need to synchronize each individual line. Thinking about that, if you look at how concurrency and parallelism affect the models of computation-- I think it's more useful to think about concurrency as just interleaving jobs on a single piece of hardware versus parallelism which introduces a whole level of additional complexity with regards to synchronization.

So it's like a juggler. He's juggling 10 balls that's concurrency. And you have 10 jugglers juggling one ball each. That's parallelism. You can take any real world situation where one person is doing  multiple things and you just multiply it by the unit number of people and it's parallelism. There's no reason why you can't have 10 people juggling ten balls each, and then you have a mixed model. But I think it's useful to have terms that explicitly refer to one person juggling 10 balls and 10 people juggling one ball to me. It's useful to have that separation. Otherwise we just have this huge ambiguity when we're talking about it. 

**Jeremy** Got it. So let's say someone is first learning about how to improve the performance of their application. It sounds like you would suggest they first start with concurrency because then they don't have to worry about the synchronization?

**Samuel** That is quite a interesting question in the sense that some programs naturally lend themselves to being broken into separate pieces. 

For example when you run commands in a Unix system and you pipe the output from one command to the input of another command naturally those commands because they are interfacing with the pipe that's communicating from one process to the next those two processes can run completely in parallel and you get that essentially for free. You don't need to think about it.

Whereas when you think about a program and they don't necessarily know how to scale it up. You don't want to impose on them all the overhead of saying well, you could have multiple threads and then you need to basically load your configuration and then split your work up into multiple separate pieces. Make a thread for each piece of work and then at the end combine it all back together like a map reduce approach. I think ultimately parallelism can sometimes be super easy for people to use and sometimes it becomes super complicated. It just depends on the kind of problem you're trying to solve and in the same vein concurrency is the same kind of thing because it really depends on the kind of problem you're trying to solve. 

For example concurrency is something which in the case of async for example. It is feasible to take a program which is largely sequential and improve the scalability of it. If you have a web server that's processing independent request those requests can run independently of each other. Whether you use threads or parallelism or concurrency to improve the performance is largely hidden from the user so that they don't need to know which approach is being used to improve the performance of their code. 

But sometimes you get to the point where you have a program where these issues do become intertwined with the logic of the code. So in that situation then you do need to be aware of how parallelism is affecting your code whether you're doing locking correctly or if using a more concurrent style approach like how is the event driven system working and are you using callbacks or async/await or some other approach?

It really depends. At some level you can write programs and you can utilize hardware resources more efficiently without necessarily any cognitive overhead in terms of how you're writing your code. And in other situations your code is going to be intimately aware of how it's using those resources and that's probably the more tricky situation irrespective of whether you use parallelism or concurrency.

**Jeremy** So in a lot of cases the developer can rely on components that have already been built for example you wrote the async library. People who are using a framework like rails. They're built on top of a web server like Puma which already uses threads. So in a lot of cases the developer doesn't necessarily have to worry about how the concurrency or how the parallelism is being accomplished because that part has been packaged up so that the developer doesn't work with it directly. 

**Samuel** Absolutely, When I'm looking at how to solve these issues I'm thinking: What kind of concerns should the developer have in their mind when they write in this code? Do they want to think about how the code is being scaled up or do they just want to get on with writing their code in the most logical way possible? And I think that is the key difference between parallelism and concurrency with respect to programming models because ultimately parallelism introduces a lot of potential issues that people may not even be aware of when they're writing code and that ultimately is going to become more of a problem with Ruby. As we embrace things like JRuby and TruffleRuby we have actual threads.

Recently I grabbed a copy of the RubyGems database and I looked at the top 10,000 gems by download count, looked at those gems, analyzed the source code, and I looked at which gems have mutex, thread, or synchronized key words in the code somewhere. Then out of that list I just went through them and I looked at the various usage of mutex, thread, and synchronize primitives.

It was not a pretty picture. In about the ten gems that I looked at I found probably about half of them have threading issues which are relatively trivial to encounter in just typical situations. The concern there is systems like Puma where you have multiple threads serving requests, are they safe? And CRuby, which is the common interpreter used by most people these days has something called the Global VM lock and that prevents multiple lines of Ruby executing simultaneously in parallel. So you're kind of restricted to a form of concurrency with CRuby, even though it appears to have multiple threads.

So developers who write code can have threading issues but they don't realize it or it's not apparent that there are issues. Because the code appears to work. But then you run that code on JRuby or TruffleRuby or an implementation of Ruby that has real threads and the whole thing just falls to pieces.

Parallelism introduces too many concerns without good enough isolation and avoiding shared global state. It's just very tricky for developers to build systems that are actually robust and reliable.

**Jeremy** And this shared global State you're referring to you were talking about mutexes and things like that.

And those are locks to attempt to prevent different threads from touching the same global state at the same time?

**Samuel** Yes. I'll just briefly explain what a mutex is for and the kind of situations I saw it being used in the code that I looked in. 

You might have have an operation and the operation is expensive. So you want to cache the results of the operation so that subsequent parts of your program that might want to do the same operation don't have to recompute that. An example might be looking at a remote web service and pulling down some data and then caching it. So what you would do is you would have a hash table and you would compute a hash key.

It could be the URL of the request plus maybe the parameters that you're posting. And the value of that would be the result of that request. For example, it may be that request takes 30 seconds or something. It's a slow request. So you build this cache and then you deploy that using puma and now you have eight threads maybe sharing that global cache.

The problem is if two threads interleave the operations. So what that means is you have two threads making the same request. They both check to see if the key is in the cache. It's not so they both make the same request and then they come back and they're trying to write the results into the cache.

Their operation is not thread safe. And so that can cause the cache to actually become irreparably damaged. Like internally the data structure in the computer will become damaged and that could cause the program to crash. The idea is that the operation should be mutually exclusive so mutex is just short for mutually exclusive. What that means is in your operation you're fetching the remote resource and putting it into the cache.

You put a mutex around it so only one thread can enter that part of the program at a time. That prevents these kinds of collisions from occurring in your programming and causing these unexpected side effects or crashes or whatever disasters can happen. So ultimately with a shared global state you'll put a mutex around it and what I saw in the code that I analyzed was mostly a very poor implementation of this shared global state.

There are other reasons why it's bad we can talk about them in a bit. But I guess I'll give a specific example. One of the ones I was looking at recently was nokogiri which is a very popular gem for parsing XML and when you do a CSS query on a document it maps it into an XPath selector.

And then the XPath selector is cached. So it caches your CSS selector string as the hash key and the XPath is the value that's computed because that process like a little bit slow is going to parse the CSS and turn it into some like AST and then turn it into an XPath. So you know it's a little bit slow and they want it to be fast.

They have this operation. It's a block that says without cache and inside that they basically switch caching off and then they do the operation and they switch caching back on. And when caching is switched off the code path that goes to the mutex is disabled. The problem is if two threads call it without cache function and they interleave the switching off and switching on the first thread switches it off then second through comes and goes oh it's switched off so I'm fine. Then the first thread switches it back on and the second thread goes well, it was switched off when I started so I'm going to switch it off. Now I'm done. So you start off with the cache enabled these two threads interact and then the cache is permanently disabled.

And so you just end up with variations on these race conditions and I have to say it's a little bit shocking to see how many gems have these kinds of issues. They're relatively trivial to fix but the reality is they're out there and they're out in production code right now. So that's the problem. 

**Jeremy** And is the reason why this hasn't been an issue so far specifically because of the the global VM lock you mentioned before? Even though these aren't thread safe because only one thing can execute at a time we're not getting a segfault when these two things are trying to access the same thing.

**Samuel** I've only tested about five different gems and of those five gems I was not able to get a segfault yet although I did get some pretty unusual results in JRuby. Coming to your back to your question. Yes, the main reason why a lot of these issues aren't so obvious is because CRuby does impose a form of mutual exclusion on ruby code.

There are definitely situations where I've seen it break in CRuby as well. I was recently looking at another one. I was looking at Faraday. And Faraday, they have a mutex which is good and they used it to lock around setting up their connection structures because Faraday's is supposed to be thread safe. You can use it on any thread. 

**Jeremy** Faraday is a HTTP client. 

**Samuel** That's correct. Yes, I should have mentioned that and what they have is they have an instance variable called middleware mutex and they write:

```ruby
@middleware_mutex ||= begin 
    require 'monitor'
    Monitor.new
end
```
Monitor is a form of re-entrant mutex. ([middleware_mutex is racey](https://github.com/lostisland/faraday/issues/1065))

It means that if you lock it once you can lock it again in the same thread and it won't block.  And because they lazily initialize the mutex if you hit that function with 10 threads you either have one thread which creates the mutex and successfully lazily initializes the instance variable or if you're really unlucky all 10 threads lazily initialize their own mutexes 10 times and you have ten separate mutexes and it's pretty bad.

That code flow can occur on CRuby as well as JRuby and TruffleRuby. You're more likely to see it on TruffleRuby and JRuby just because they don't have the GVL so they don't have any implicit form of mutual exclusion on Ruby code. 

I guess ultimately if you're using Faraday and you're expecting stuff like this to work correctly that one in a million time your app crashes and you don't know why-- maybe it's there. Who knows? These issues are just super insidious. They cause very difficult to diagnose problems. So parallelism, to try and put a summary is just something which introduces so many issues and we're just scratching the surface really with regards to the kinds of problems that exist. 

**Jeremy** And in all these cases the problem stemmed from needing to use a mutex and in a lot of these cases I'm guessing there is some kind of shared collection. 

**Samuel** That's correct shared global state is basically the key that holds together all of these problems. So yeah, I think ultimately what it comes down to is if you have a gem or a library that has shared global gtate you need to be incredibly careful with how that works in a multi-threaded environment because the chance of it being wrong is probably a lot higher than the chance of it being correct based on my experience.

**Jeremy** Because it's so easy to miss something or make a mistake.

**Samuel** Yeah you just have to miss one thing and then something disastrous can happen. It doesn't take a lot and I think that's the problem with parallelism. Ultimately any kind of shared mutable state can potentially introduce these issues and actually the interaction between different parts of your code is very difficult to reason about. There was one fragment of code in the AWS gem. I was trying to figure out if I could get it to deadlock. Any code that takes a lock like goes `Mutex.synchronize` and then yields back to user code can deadlock because if you don't have a re-entrant mutex, like you're not using a monitor. Then what can happen is you lock your mutex and then you call the user code and then the user code essentially tries to go back into that code. So the code that has the mutex and it tries to lock it again.

And as soon as you do that you have instant deadlock. The program will just simply stop working. Fortunately I think in Ruby it will just crash it won't just hang. But there's lots of different ways parallelism can create problems and I think if you look at how people are using Ruby in the real world, you start to realize things like unicorn where we have a single process is not such a bad idea. Sometimes using multiple threads in Ruby is more hassle than it's worth.

**Jeremy** And in the case of unicorn they're spawning multiple processes, right? And they don't have any kind of shared state? Is that why they don't run into the same problem? 

**Samuel** Yes, with unicorn the way that web server works and feel free to correct me if you know I'm wrong but--

It loads your application and then it forks a number of child processes and then those processes essentially just handle one request at a time and so the value of that is you don't have any parallelism issues. There's no chance of two threads trying to access the same shared state because every process has its own copy of memory.

**Jeremy** And so in the case that you need to share state amongst your different processes. It would have to be through a separate application like a database or redis. 

**Samuel** Redis, a database, even a Unix pipe would be okay. Go is a language which tries to solve this problem by forcing or by encouraging people to use channels. A channel is a communication between two go routines where you can send objects and information between them but it's not shared mutable state because basically when the object goes in one end of the channel, it gets serialized and comes out the other end and so the two processes they can't clobber each other's data. Erlang uses the same approach actually erlang has a way of communicating between lightweight processes in a similar fashion to avoid any kind of issue with shared global state and I think if you look at where ruby's going maybe guilds whatever they can end up being called. It's the same kind of model. It's trying to avoid having any chance of shared mutable state just because basically experience shows us it's impossible to deal with it in general. 

**Jeremy** They're sidestepping the problem of sharing mutable state and sending these-- I guess they're not operating system processes, but they're lightweight runtime processes.

**Samuel** That's correct. 

**Jeremy** So then all these processes would be very chatty. They would all have to send messages to one another to duplicate the--

**Samuel** I mean there are definitely overheads with it. If you have a specific kind of problem and you can isolate your problem in the runtime of the problem to a specific of circumstances. Then using threads can be a great solution and can scale very well. But just for general purpose code where you have people who aren't necessarily aware of the issues. You don't want to necessarily expose them to all that pain and frustration. 

Ultimately I think with the lightweight process model you get most of the benefits of scalability with very few of the pain points. So obviously with go and erlang you have specific semantics and syntax in the language to support that. But using a message bus or redis or a database for communicating between processes is a totally fine way to do it. It might not be as efficient as something which is built directly in the language-- the runtime is designed around its form of concurrency and parallelism. But it's not a big deal you can do it. 

**Jeremy** So I guess in the case of go and erlang they have a runtime that's built around this concept of lightweight processes and message passing and with something like Ruby where that's not built into the runtime. You're saying well, maybe instead of having the runtime manage processes you would spawn operating system processes and talk between them with a message bus or something like that. 

**Samuel** Yeah, absolutely. When you look at how Ruby is positioned right now obviously threads are the predominant model for achieving scalability whether that is a good idea or not. I think we can show that it's not actually that great. It might be okay in practice if you can avoid pitfalls. But what my analysis showed me is a lot of these gems that people are using that are super popular. They have potentially thread safety issues. I've only looked at 10 of them. What about the other 10,000? It's quite concerning. 

I think a different approach is needed for ruby and I think that's what brought me to async. The reason why I built async was because I got frustrated with Celluloid. And don't get me wrong. I really like the ideas behind Celluloid. But Celluloid was very difficult to test because it depended on shared global state and if you had one spec fail it wouldn't necessarily clean up the shared global state that it left behind like you'd have actors that were still sitting in the global namespace. 

**Jeremy** Could you briefly explain what Celluloid is? 

**Samuel** Yes, so Celluloid was a very popular framework for ruby actor based concurrency and even some form of parallelism as well because you could run them on separate threads. The way that it works is you have objects and those objects have methods and when you call a method on an object, it's not synchronous, it's asynchronous. 

And so what that means is when you go `object.do_something` what you're actually doing is you're making a little message. You're packaging up all the arguments into that message and you're putting it into the object's mailbox. And then the remote object is basically polling on its mailbox saying did a message come in? Did a message come in? 

When it gets a message, it will do the work and then if required will post a response back to the object and so it runs in a way which allows those objects to operate in parallel. If you have a lot of objects they can work together to solve problems and they can run in parallel. They run independently, and if one object crashes you can restart it. And so there's some robustness guarantees as well. It was quite popular. 

**Jeremy** On the surface, it sounds a bit like the go channels or erlang processes just brought into Ruby. Does that sound correct? 

**Samuel** To a certain extent. The detail of how these systems fit together makes them different. Erlang with its lightweight processes. Go with its Goroutines, and Celluloid with its actors they're all similar. They're all trying to solve the same classic problems but the way they go around doing it is quite different and the semantics is where they differ quite significantly.

In terms of how you handle robustness issues, how you handle failures, how you handle that state and state transitions? All those things can be quite different between those systems. 

**Jeremy** And in the case of Celluloid there were problems with shared global state. How is that in the context of Celluloid? 

**Samuel** So in Celluloid when you create an actor and you instantiate it, it becomes part of the ruby process. It becomes global state and you can communicate with it and when you're running specs you want to go okay set up parameters for my spec. It could be you load a configuration file or you prepare your object in a certain state and then you essentially do something and test that the result was what you wanted. Ideally if you run that spec it's isolated so that if you run the spec and it fails it won't impact some other subsequent spec in the case of running tests. 

So in Celluloid those actors would sit in the global namespace. If you were trying to test them you had to do a lot of scaffolding to spin them up and tear them down at the end of the spec. There was no implicit state management or lifecycle Management in them and a big thing for me that I think trips up a lot of users is life cycle management. What I mean by lifecycle management is creating an object, using an object, and getting rid of an object.

Surprisingly enough a lot of code doesn't do that very well. An example would be code that connects a socket to a remote system, communicates with it, doesn't close it, and then expects the garbage collector to go and close it when it goes out of scope. In my mind a lot of that stuff should be more explicit because I think it avoids a lot of potential issues and potential bugs. So life cycle management is super important and I think Celluloid really lacked a good model for lifecycle management. 

**Jeremy** And you created a new library called async which is centered around concurrency. How does async work and how does it compare?

**Samuel** So at a certain point I was maintaining Celluloid IO which is an event-driven IO reactor which could operate inside a Celluloid actor and I was maintaining that because I was building a tool called Ruby DNS and Ruby DNS is a ruby client and server DNS implementation you can use it for doing all sorts of crazy things. 

Like one example is a DNS server that hooks up to Wikipedia. So if you query the DNS server for a keyword it will return the first paragraph from Wikipedia. And I was just interested in like how do you scale it up? How do you build something in Ruby that makes sense and is scalable with straightforward logical code and we almost managed to get to a 1.0 release.

I had Ruby DNS all lined up to go and there were specs in Ruby DNS that would just randomly crash for no obvious reason because of issues in Celluloid or Celluloid IO and I could not fix those issues. After about six months of just trying to make that work I was like this is crazy. We're never going to fix these issues. We're going around in circles. So at that point I was like, okay. I'm sick of not being in control of the thing which underpins Ruby DNS. I'm just going to build something. It can't be that hard. So that was when async was born. Async was the product of frustration. 

And so async takes what I think were the best parts of Celluloid plus a model for lifecycle that makes sense in the scope of Ruby and then turns it into something which I could run Ruby DNS on top of and run my specs and not have them crash and just be super reliable. 

Async essentially is just a reactor which lets you do things like non-blocking I/O and timers and then on top of that everything else like sockets and networking and so on and so forth. Then on top of that is Ruby DNS, which is essentially just doing network IO. And now that I think of it the motivation was actually that Wikipedia DNS because what actually happened was I was using I can't remember if it was with EventMachine or Celluloid but I wanted to have a DNS server that could receive the request for cats.wikipedia and then it would do a web request to Wikipedia's API which would get back the first paragraph. And it turned out that there was no way to combine that Web request with the DNS server because the web request I think I was using like rest-client that just assumed a multi-threaded environment. So that request would block and then my Ruby DNS which is running either EventMachine or Celluloid. It was event-driven so as soon as you would have one request come in, that would do that web request, the whole thing would just lock up for the duration of the web call. No other requests could be processed at the same time. And so I was just like, this is crazy. Like we can't take these two components and make them work together. I'd have to go from event driven back to multi threads and you can't spawn one thread per DNS query it's insane it would just never scale. So I was like, it's got to be a better way to solve this problem and combine all these pieces and I think you know, ultimately that's what led to async. How do you build something which lets you do this? And so now Ruby DNS can do it. You can do that kind of thing. You can have a DNS server that will create event-driven queries and then if you do a web request then that is also part of that event Loop so it won't block other requests. 

**Jeremy** Yeah, so it sounds like the one of the big frustrations came out of the fact that you were working with something that used an event loop and then to do other parts of work you were using a library that was expecting threads and the two just don't work well together. Could you kind of talk a little bit more about what an event loop is and what it is in relation to non-blocking I/O and when you would use that instead of threads? 

**Samuel** Right, it's a really good question. So, what an event loop comes down to is literally just a loop. And in that Loop you can do a couple of different things. It really depends on what your goals are. If we just focus on the simplest kind of event loop which would just be timers essentially you have a piece of code like your own code that you want to run and you want to say after 3 seconds do this. And so what your loop is going to be doing is it's going to be saying I have a list of things that the user wants to do and one of those things is waiting for three seconds and then doing some stuff. 

So essentially what your event loop would look like is a loop which would basically say okay I have list of timers and one that's going to expire the soonest is this one for three seconds. So I'm going to sleep for 3 seconds. And after three seconds, I'm going to go back to the users code and that can be through a callback or some other approach. We can we talk about later how fibers work. We'll just assume we're using callbacks. So that is really the simplest event loop. So what's happening is you're looking at some list of timeouts you are choosing the one that times out the soonest and then you're sleeping for that duration. After that duration is expired you resume the user's code. If the user wants to do something more advanced for example networking then you need to incorporate elements of what kind of things can I read from and what kind of things can I write to. 

A typical networking operation will be reading some data, doing some processing, and writing a result back out for example. Network latency is normally massive like on the order of milliseconds. And so what would happen is you would basically have a socket which is connected to something or listening for a connection to come in then you would try and read from that socket. Now in the case of multiple threads that operation is a blocking operation. So what that means is a thread goes to sleep until there's data available to be read on this socket. While that thread is sleeping it's not using a CPU. So other threads can run. And the main point is that you can also do the same thing in a non-blocking fashion in the reactor so that when you try and read from a socket rather than sleeping in the operating system waiting for data to be available you go to the reactor and say "Hey, I want to register my interest in this socket, tell me when it's readable and call me once it is readable." And so you schedule that IO into the reactor. The reactor does every other operation that it can do until it comes back and the operating system says hey there's data available for you. And the reactor will then resume that code in this case via a call back. And so the value in that ultimately is that the overhead is a lot less potentially. So the event loop is just looping over and over again. In the case of async there's timers, jobs, and IO and those three things are basically interleaved in a way which minimizes latency. And then the user code essentially is just waiting until the operation can continue and when it can continue it will resume. In the meantime, if you're just waiting then other tasks will run and if no tasks can run it's literally just sleeping in the operating system waiting for something to happen. 

**Jeremy** And when you're making these operating system calls, like for example for IO you were saying you have some call back where let's say you want to read a file and the operating system is going to let you know when the files have been read or when it has a portion ready for you. Are you able to execute your Ruby code at the same time while the operating system is doing that kind of work? 

**Samuel** Yeah, so, essentially in async and even in general run loops. I guess you will schedule multiple tasks. Those tasks run concurrently. So while one task might be waiting for an I/O operation another task could be waiting on a timer and another task could be executing a loop parsing some data or something. Because they run concurrently those tasks can never run in parallel. It's not a form of parallelism. They're always scheduled one after the other based on the availability of data or a timer or something else in the event loop. Essentially those tasks are user-driven and in the case of like a web server, for example, every request would be its own task. And so those tasks, those requests while they never run in parallel they were running concurrently. So a typical example would be receiving a request and the user is posting an image like a two megabyte image. It could take maybe a few seconds to upload that data. So while that one task is waiting for the data to come in another task can be executing and processing some other part of another request or different requests for a different user. So essentially those tasks are the core abstraction by which those units of work execute independently and the event loop essentially multiplexes between them. 

**Jeremy** And is it your async code that has a scheduler built-in that's deciding when each test should run?

**Samuel** The event loop is literally a loop which is going around in a circle and the core part is the timers and the list of outstanding jobs that would be resumed by nature of them being outstanding. And finally the core part is the IO. And the IO operation waiting for an event to occur. There are various different ways you can implement them. 

The most typical one is `IO.select`. and `IO.select` takes four arguments and the most important ones are the first two and the last one. The first two is a list of sockets you want to know if those sockets have data available. The second one is a list of sockets and you want to know if those sockets can be written to, the buffer is empty. 

Obviously the operating system has a buffer and that data is going out across the network. And if you put too much data in there you can't put any more. And the final argument is the timeout which is how long it will wait. For any of those events to occur like something to become readable or something to become writable. So `IO.select` is the most basic thing. And so what you do is you slot that in there into the event loop and you basically say: I have a list of tasks which are waiting on IO for it to become readable. I have a list of tasks which are waiting for IO to become writable. And I have a list of tasks, which are waiting on timers and the shortest timer is like, I don't know a hundred milliseconds. 

So you'll take all those readable IOs and put them in the first argument. You take all the writable IOs and put them in the second argument. You take the timer and put it in the last argument. And what that operation will do is like a sleep. But essentially if any events occur on those sockets, it will wake up immediately and you can resume the users code from that point and so that just sits in the event loop in and the event loop spins around around around and executes that over and over again and if there's no timeouts, then you sleep forever until some network event occurs. 

**Jeremy** It's almost like the operating system call, the `IO.select` call is I don't know if you would call that scheduling but it's deciding when your function should wake up and start receiving?

**Samuel** Yeah, I mean ultimately the operating system probably has a certain amount of variability with regards to network data and when that comes in and how it wakes things up. One of the things that I have thought about a lot with async is how to make it as predictable as possible.  I think ultimately the way to look at it is that predictability in code is good. If you write a program and you expected it executes one instruction after another like one line of code after another that's a normal expectation. And even if things are running out of order it's nice to have some cognitive model of how those things fit together. 

So when you write your program and you have two tasks and they're executing so you have a task and it's making a child task in async. There is one guarantee which I found quite useful and it's when a parent spawns a child task that child task will run until the first blocking operation occurs and then it will go back to the parent. So because of that you can make certain assumptions about how the code behaves and you can have a cognitive model which when you're debugging code it really helps if you have a cognitive model for how things are fitting together. I guess I've tried to avoid getting too far away from sequential code because I think that is when you start making things really complicated. Async tries to keep things as simple as possible, as sequential is possible, and these points where you have non determinism we ultimately try and minimize the chances they're making the code complicated to understand. 

**Jeremy** Yeah, it reminds me of when you run a debugger against multi-threaded code and you're trying to step line by line and it's jumping from thread to thread and it's really hard to know: Okay, where am I going next?

**Samuel** Absolutely. So there are certain elements of async which are deterministic. And I think one thing I've been thinking about recently is there are some elements of async which are non deterministic. And because you get the sense of: oh, I understand what's going I understand how this is working how it fits together. Sometimes when you have situations when that non-determinism creeps in and causes some kind of issue. But I think sometimes it's unavoidable. Sometimes you need to introduce non-determinism. It's just part of the program. 

I was thinking about comparing async versus async/await. So this is very confusing. Async uses fibers, which I can explain in a moment and there's another pattern called async/await and they're kind of opposite sides of the same coin. Async/await you basically use keywords and those keywords are used to indicate operations, which may introduce non-determinism into your program. If you try and read from a socket you may end up executing some other code while that data is coming into the system and then you'll be resumed back at that point. So if you have global mutable state you know from line to line, you can't necessarily make assumptions about that global mutable state unless you put some kind of semaphore or mutex around it in async/await. You also have explicit points at which non determinism is introduced in those points clearly shown by the use of those keywords and so on. The opposite situation with async is you don't have those keywords. It's valuable because you don't overload the language with a lot of extra syntax, and you don't have to explain this is this extra syntax. And in fact, what's really interesting is I've played around with retrofitting existing code bases with async and a lot of the time it just works. You can take an existing code base and you can stick it into an async reactor and inject the appropriate concurrency primitives. And it will just work which is really amazing to me. But obviously you can't do the same with async/await because you have the extra syntax and extra key words, you need to inject into your code. So I think going back to that main point is just not making the code too complicated and trying to keep things as sequential as possible. But there's definitely this nature of non-determinism and you can't avoid that with something which is involving event loops and event-driven callbacks. 

**Jeremy** Right, but you can minimize the surface that you have no control over.

**Samuel** Absolutely. I think that's what I've tried to do with async and the nature of that discussion about synchronous versus non determinism execution, I'm thinking okay, how do we actually make this easier for the user and try and avoid running into some common pitfalls. But I have to admit it's exciting sometimes you do still have issues. It's non-trivial like any kind of concurrency any kind of asynchronicity. It's non-trivial and that's why I think things like Puma and Falcon which try and isolate the user from that complexity. I think they are the way to go. But, again coming back to that discussion like threads just there are too many situations where threads introduce too many problems. And I think the defacto is sequential code running on a single thread or a single process. That is kind of the defacto concurrency model that people understand and anything more complicated and it's just a disaster waiting to happen. So yeah, I'm very aware of that. Ruby is ruby and we appreciate ruby for being an awesome language for a lot of different reasons and I think a certain kind of semantic simplicity that ruby has I've tried to embrace it in async. 

**Jeremy** Yeah, I mean one of the things that I've noticed outside of Ruby whether it's JavaScript or C sharp or you were talking earlier about erlang and go. They all have concurrency primitives that are built on top of threads or on top of a reactor and it seems like everyone's trying to solve this problem to try and get people away from manually spawning processes and manually spawning threads.  

**Samuel** But it's gone in the opposite direction with node.js because they made workers which are isolated child processes that communicate using some channel type setup. So I think what's interesting is that node.js just from ignoring all the semantic issues with JavaScript. The semantic model of how node.js executes is a really good model because it's a single threaded asynchronous event loop and in my mind, that is the best balance between years of facing complexity and scalability. I don't think you can really get much better than that without compromising one of those two but in the end like if you look at what node.js has done is they've basically had enough situations where having true parallelism was critical that they had to introduce some extra concept which was this worker concept where you can basically spin up child processes. And I think what's fascinating about that is it shows that event loops aren't sort of a one and only solution. 

I'm often in awe at the original creators of Unix for how insightful they were about the problems people would need to solve. The way that processes, threads, and all that stuff that's together. The more I dig into it the more in awe I am of how it works and I think what's interesting is if you look at this kind of the cycle of reinventing the wheel that seems to happen sort of every ten or twenty yeah I don't know like people are sort of rediscovering what was already discovered. I mean fibers, aren't new. It's not like I like came up with that concept at all. The original use case of fibers were... I said, I would talk about fibers so is it worth going over them? 

**Jeremy** Yeah, let's go into that. So that we get an understanding of where you're coming from. 

**Samuel** So, async it's the opposite side of the coin to a system like async/await. Async/await is a syntactic sugar over callbacks. So when you write async/await inside a function what happens is when that function is compiled by the interpreter into some kind of byte code. It's actually transformed into a state machine. This is the most common way it's done and what happens is your function has an extra argument. And that argument is where to go to when you come back into the function. And so essentially async/await is a transform of your function into a callback style approach. Callbacks are a way of dealing with events that occur in a system. But the problem with callbacks is they lose all the context in which the sequential flow of those events occurred. So if you're trying to do some complicated process what you end up having to do is build this ginormous state machine which takes the callbacks and feeds those events into the state machine and the state machine produces some meaningful output. And that is very error-prone that the chance of it causing problems is very high. And so async/await manually generates that state machine for you from your sequential code. So you write your sequential code. You put in these points where you can have non-blocking operations and then that gets transformed into this giant state machine which then gets run by the event loop. 

The alternative to that is to use something like a fiber. The way I've seen it described is we know what a routine. A function or method and the general term for that is routine. And a routine is something which has a call operation which lets you go to the top of the routine or method or function you start executing it and at some point or if you just run off the end you return back to the caller.  So you've got these two you have a routine and these two operations call and return. Then you have what's called a coroutine. And a coroutine has this call and return operation, but it's a superset of a routine it also has resume and yield. What resume and yield do semantically is when you call a function you execute some of it and you get to a certain point and you can call yield and that yield goes back to the caller but it doesn't lose the state of the function where it was all the local values stay the same. When you call resume on that method it will go back to the point where it last called yield and all the state will be as it was. Then it will continue executing until you get to return and then it will exit and that will be the end of that method invocation. So a fiber essentially captures that state of the function execution in its own stack. So you take a coroutine in the semantic model of a coroutine and you attach to that a stack. And so when you enter a function that is a fiber it allocates a stack for its own behavior and all its locals and anything else that calls. And when you call yield operation what that does is it switches the stack to the stack that it came from. So basically it's a stack swapping operation. And so basically all that's happening is that call is just literally the call instruction on your CPU and then yield becomes like a return but you swapped the stack at the same time and then resume is like a call but you swap the stack. And then return you deallocate the stack because you're done with them. So fibers they're almost identical to a thread but the context switching is controlled by the user of the fiber rather than the operating system which transparently decides oh your time is up. I'm going to do something else now. And so the benefit of that is composability and determinism. You know how the program is going to behave because you explicitly have these points where you schedule the operations to suspend and resume. 

So fibers are used by async to manage those individual tasks every task in async is backed by a fiber. So your code inside a task executes sequentially and it runs like you'd expect and those tasks that are running in concurrent fashion. They are actually fibers. They're backed by a fiber and so when you perform an I/O operation that would block you actually end up calling `Fiber.yield` and `Fiber.yield` goes back to the reactor. And when the reactor says your operation is ready to continue the operating system says that the event loop calls `Fiber.resume` and it will go back into your task where you left off and keep on executing. It's another way of avoiding the ginormous state machine that you have with callbacks. But I think it's a bit more predictable than async/await and you avoid all this syntax overhead. So they're really just two sides of the same coin. But they have different trade-offs and I prefer the trade-offs of fibers. 

**Jeremy** You have these functions that have more information about themselves and can maintain their own state and like you were saying that allows you to write library code that's simpler in order to switch between all these different functions that are running and resume them. Whereas in the case of the async/await keywords the library code that needs to be written to jump between all of these traditional functions has to be a lot more complicated and possibly a lot less predictable. 

**Samuel** Yeah, I mean, that's a really good point. You don't have to look very far to see the effort that goes on in the Rust ecosystem or the NodeJS ecosystem. Adapting all the libraries to support promises and async/await and all the adapter patterns they use to turn promises into async/await and vice versa and this year I ran into this bug recently I was using GitHub actions. In Ruby you have the system method which executes something using the shell and there's just there's no built-in NodeJS method which works in a way that is async you have to use a call back or something. So you end up wrapping this in a promise and 30 lines of code later you have this thing which you're not even sure if it works correctly. This is surprising me a lot. So I think the great thing about using fibers is that the code does not need to be modified in order to run in a concurrent fashion. If you take existing code and you put it into an async task and you inject the right primitives. One example I'll give you that I've tested myself is `net/http` the standard lib code from Ruby. I've made some wrapper classes if you inject those wrapper classes into the module if you just literally go like: 

```ruby
Net::HTTP::TCPSocket = Async::IO::TCPSocket
```

Then HTTP becomes just completely asynchronous, which I think is amazing. Because it doesn't require any additional keywords or changes to Net::HTTP it just works. And to me the value of that is massive because you can take any code base in theory and use it in async and have it become asynchronous. The same applies to SQL and ActiveRecord. ActiveRecord is a little bit tricky because ActiveRecord makes a lot of assumptions about threads. So when I've tried to make that work I've had to use monkey patching which is unfortunate. But in theory I've got examples where I've done benchmarks between Puma and Falcon and all I've done is I've used an asynchronous postgres connection and the scalability with Falcon and async postgres is just crazy compared to Puma. and of course, you don't expect that in the real world to be as big of an improvement but it's not uncommon to have database queries take a few hundred milliseconds and there's no reason why you shouldn't be servicing other requests in the meantime. So you can definitely improve scalability through that approach. 

The other one that was really fascinating to me was `redis-rb`. So I made a pull request because `redis-rb` supports this driver kind of abstraction where you can basically swap in something which provides the core communication with the redis server and I wrote one that used Async IO and it was not only the shortest driver out of all of them but with very minor issues the whole test suite just passed it was like well, it's amazing. It all just worked. I don't know if that would work in the real world because async redis also makes some assumptions about multi-threading. But it was exciting to me that you could take something like as big as-- redis-rb has a lot of specs and so essentially that you could take something like that. Write this 50 line wrapper to make the IO asynchronous and then everything just basically worked it blew me away. I think these kind of situations where you have legacy code. You don't want to rewrite all of it. But you want to improve the scalability. I think async looks like it can do that and the reality now is to get companies on board and people on board with the whole thing and let's do it. Let's take some Legacy code and make it scalable just by this transparent non-blocking I/O and potentially other things as well. 

**Jeremy** And you were saying this is possible because the method signatures don't change and the objects that return don't change so you can write an async version of a library. And as long as the API is identical. If code is running inside a reactor or it's not running inside a reactor it'll work just as well. 

**Samuel** That's correct. And that's almost a little bit of a different point from the one I was just making but it's equally valuable. So what's interesting is that one of the things that I thought about when I was building async was users shouldn't need to know if the code they're invoking is event driven. Why should the user be forced to set up the environment? They just want to call a function and it does something. They don't have to go: Oh this function could be async so I better make sure I'm running inside of an async  reactor or something like this. 

So what I did was I explored these options. And so when you write in Ruby:

```ruby
Async do
# ...
end
```

in your code, What that does is if you are in a reactor already, it makes a task and it will run that task concurrently with any of the tasks in the system. 

But if there's no reactor currently running and you run `async do ... end` in your code it will create the reactor for you and run your code inside a task. So inside your library code, if you want to use async you can hide async the user will never know about it. And to me that is another element of the whole approach to lifecycle and managing the expectations of a user. 

I'll just give you simple concrete example of that. In Ruby DNS when you start the Ruby DNS server, it uses that approach so here's like an async block at the top level entry point. If you want to control the life cycle of the DNS server as a consumer of that library you create your own event Loop like you go: 

```ruby
Async do
  task = Async::DNS.run
end
```
or whatever. Then that returns a task, which you can wait on, stop it, you can kill it, whatever you want to do you have complete control over its life cycle. But if you don't, if you just call: `Async::DNS.run` it will spin up a reactor and that means it will block until the server has finished. You basically get the best of both worlds in terms of semantics. If you want to control it then you can and if you don't want to control it then you just ignore it. Again it comes back to making the experience for the user as simple as possible. They shouldn't need to know how the code is working or what concurrency model it's using or what parallelism models it's using. You shouldn't need to worry about that from the point of view of the consumer. It's like a method you call it and you do something with the result if you need to. 

**Jeremy** I think that part is pretty exciting because it really makes it a real possibility that as people update libraries or as they create new libraries. They can make use of async and take advantage of the reactor. 

And like you said the people who are adding the library to their gemfile. They may have no idea that it's using any of this and they can continue to use it in their existing apps and maybe later they find out a little bit more about what async is and how it works and they decide to add it in later and they still don't really have to change a whole lot with their code. 

**Samuel** Yeah, that's a really good summary. In my case, we have some legacy system setup using [passenger](https://www.phusionpassenger.com/) as a web server and it is running per process and we have some issues where we need concurrency in a single request. And even though we're using passenger we can use async inside passenger. 

Obviously the event loop is going to block the request. But within that async block we can do asynchronous behavior interacting with redis and upstream APIs and at the end of that block everything comes back and the request continues and nothing is leaked outside of their block. There's no global state or anything like that. So in that sense it's a really powerful set of abstractions. 

What I've been thinking of for the past couple of years is what is the right semantic model? I don't really care about the code that much although I do care about the naming. Naming is a big deal. But what is really important is the semantic model. That we have the right semantic model for how people build scalable systems is absolutely critical and right now ruby just gives so many mixed messages. There are so many different ways to do things and as a developer, there are so many ways that can go horribly wrong and my research is really just showing that. It's all very well saying like oh thread safety, you know, it's an issue but really like having these tangible examples and looking through the code myself really just made me think. Oh, well, this is pretty bad. 

**Jeremy** Yeah, this is more about the library ecosystem I guess. 

**Samuel** Yeah, I mean like at the end of the day when you're building a library. Another one I looked at is the money gem which has 22 million downloads and that gem has thread safety issues. In fact a pretty critical one. I mean I don't think anyone is affected otherwise they probably would have figured it out by now. But there's this shared Global state it's called the bank's store. And it stores exchange rates. If you access that store from multiple threads. In my test I was trying to hammer it. I had a hundred threads adding a thousand exchange rates each. And at the end of that test you would expect a hundred times a thousand, right? So like what then at the end of my test like I had 18. I had 18 exchange rates in the store and it's because the threads were clobbering each other. And what was even worse was not only were the threads clobbering each other but actually within one thread you could write an exchange rate to the hash table and then you could read it back and it wasn't there. It was gone. 

So I think people are trying to make these gems and it's not really a criticism because I have no entitlement regarding people making code and giving away for free. It's awesome that people are doing it. But, look we have a landscape and a semantic model that just promotes disaster basically because I've had people talk to me saying things like we only deploy multi-process because we are not confident that ruby is capable of dealing with multiple threads and I think when I heard that my heart went out to the JRuby and TruffleRuby team. They've worked so hard to make threads a reality in ruby and now we're in this really crazy situation where we have all this code [where] those problems are just magnified a thousand times. 

So the only solution and this is not really causation it's more like correlation. The reason why I made async was because I see it as being the only solution to this kind of complexity. Single-threaded asynchronous I/O and timers and event driven behavior is ultimately the only way we're going to isolate these kind of problems and build up code that can actually work correctly. I think it's gonna be pretty painful to be honest. I don't think it's a trivial issue to address. I think like independently these bugs can be found and solved but I think as a whole ecosystem trying to move this whole thing forward that is really the key and it's going to be the difficult element. 

And maybe guilds are the way to do it. But the thing is with guilds assuming they're some little erlang lightweight processes or go routines or whatever is then you have to check everyone's code and somehow get it to work in that context. So async is like a bridge between those two things because async works today in ruby you can take basically any ruby code throw in async and parts of your code will scale better depending on how much effort you spend on it. 

But if you take something like a [guild](https://www.youtube.com/watch?v=XiujvihOLq8). Potentially removing thread, removing mutex, like do those things operate inside guilds? I don't know. So then all the code that depends on mutexes and threads could be become broken for example. Then you look at things like how message passing needs to work or all those changes to the semantic model which is really going to affect existing code. So it's going to be tricky it's going to be a complicated thing to come to terms with I think as a as a community and as a ecosystem of libraries. But it's possible to solve those problems and I think async is my stick in the ground saying yeah, this is what we can achieve right now with what we've got. 

**Jeremy** Yeah, and I think what's kind of interesting about these issues with threading and all these different libraries is that when a lot of people talk about rubies performance, they talk about the global VM lock they talk about: I can't run things at the same time because of this lock. But I'm wondering if that lock is actually what is protecting a lot of these libraries. It's what's allowing a lot of them to run without seg faulting due to the existence of that lock. 

**Samuel** That is a really good question. And I think what I can say is. the process of understanding the GVL. Was almost like spiritually transformative. When I was a teenager and and working through my first programs and mucking around with C and Python and other languages and you hear about this thing called the GVL. You think why would they put the GVL it seems like such a stupid idea to lock around all that stuff. Why can't I make real threads? What is the logic of it? And you have this irritation at least I did. I was just irritated as it seems to be such an impure thing to have in an interpreter. Why would you leave all that performance on the table? And then you slowly come to terms with like why it's there. I think the Pinnacle of it for me was when I read the comments. I think I might have been `thread.c` or `thread.h` I'll look it up and I'll tell you afterwards but there's a comment at the top of one of those files it says: 

Here are the five possibilities. What are the options? If we have a GVL or we don't have a GVL. If we have fine grain locking versus not and you suddenly realize defining classes, defining methods, method caches, all these things in the Ruby VM are not thread safe at all. And to make them thread-safe would basically be impossible. And so I think when you look at guilds or the idea of lightweight processes as a separate semantic form of asynchronicity within Ruby starts to become much more appealing because then you start to model it more explicitly around the life cycle of the user's code. 

I have a bunch of gems I want to load so I want to load all that code into memory and then I want to make one guild per processor in my system. And each of those guilds has access to this shared region of memory which essentially becomes immutable. And those eight guilds operate independently but they're in the same process address space so you can do things like sharing immutable objects between them. And then you can do things like have independent garbage collection. So if you wanted to have say thirty two guilds because of garbage collection overheads you could do that. And so you start to build a more complex semantic model and erlang for example each erlang process has its own garbage collector. Guilds try and solve the problems. My original opinion was like I said to Koichi why don't we just make threads work without the GVL? You know JRuby has done at TruffleRuby has done it. Why can't we do it? I think he thought I was a bit crazy. 

I think the only solution is the one that they're proposing just because it's pragmatic. In a way like as a software engineer and as a computer scientist. I don't believe anyone who encounters that and seriously thinks about it isn't at least slightly disappointed that is the solution. But I have to say going through that whole process from when I was a kid and just coming to terms with programming and hearing about things like the python had it's own GVL and just thinking why would they leave all their performance right on the table? But then you suddenly realize over time every step you take you just realize how complex the whole thing is. And then you read that comment at the top of the `thread.c`. And you think yeah, okay. No, this is probably the best option out of all possibilities. 

**Jeremy** Right, it's like a lot of things where we see something and we think it's dumb and then you dive a little bit deeper down and then you realize there's very good reasons why people make the decisions they do and life is more complex than we sometimes think it is. 

At the beginning of the conversation you were talking a lot about how shared mutable state is a problem. In the context of the async library. If someone has state that they want to share between the different reactors or the different tasks. What kind of way should they approach that?

**Samuel** Async provides another gem called [async-container](https://github.com/socketry/async-container). And what  async container does is it abstracts parallelism between JRuby, TruffleRuby, and CRuby. 

In CRuby if you have eight CPUs, you want eight processes running. If you're in JRuby and you have eight CPUs, you want eight threads and the same for TruffleRuby. And so what async-container does is you give it a block of code and it will run it as many times as it can that makes sense on your current hardware. So the way that Falcon utilizes that for example is Falcon has this block where it loads your application, creates a server, and then starts processing requests and it runs it inside an async-container. So on CRuby it uses 8 child processes and on JRuby it uses 8 threads. 

So to come back to your question. Like how do you communicate between those systems? So in the Falcon examples, there is a chat example and the simplest way you can do that is you just tell Falcon to run with one process or one container. And so you basically have only one reactor. And you have a semaphore or something you manage the state if you need to and essentially just have like a list of users and it's a hash table of user to socket or web socket or whatever and then you can write message at just like NodeJS. If you've ever written a chat system in NodeJS it's exactly the same. And you can run Falcon just like NodeJS using one process. And you can probably handle like I don't know I recently heard someone did a million web sockets in async and falcon on one process (laughs). That can scale pretty far. 

But at the point that you get past about I would say 10000-20000 connections starts to become the point where the Ruby garbage collector causes issues and Aaron Patterson who has been working on the compacting GC. He was pretty excited to try to understand that problem and see if he could figure out a solution. It's quite a complicated problem because of the way fibers work and we need to do stack scanning. 

But anyway, I made you a question. How do you get these things to communicate because of the way async-container works in the way that I recommend that people use async-container for their server systems so that you get the maximum amount of parallelism out of your hardware. You need to either use something like redis, a database, or even just a shared unix pipe or something to communicate between them. And that is the simplest way to achieve scalable cross reactor communication because for example if you use redis then you can run Falcon on a cluster of machines and all those reactors will be able to communicate with each other. You won't have to do anything. It'll just work out of the box. If you use a database then it's basically the same thing. If you use a thing like a unix socket or IPC, then you're limited to the current system. So, there's a number of light solutions in there. The simplest one being run it like NodeJS with one process and that's sufficient for some use cases. If you need more scalability than use something else to do the communication. I have played around with implementing a message bus in pure Ruby that fits into async but I think it's just better at this point to use redis it's more mature. It was more for fun to see if it was possible. 

**Jeremy** The async-container concept that would also apply when you have something very CPU bound that you want to run on another process as well. 

**Samuel** Absolutely. So async container serves two main purposes. The first purpose is to say here is a block of code. Run it in one reactor per CPU core. That's one main sort of semantic mode of operation. The other mode of operation is spin up this task and run it as efficiently as possible and so on CRuby it will fork and make a child process and on JRuby will make a thread and so. That allows you to do things like job processing or if you just want to spin up a whole bunch of isolated tasks. You can do the same thing. So you can do that. And I guess in the first situation where you're spinning out like a number of tasks. Async-container recently got the support for gracefully reloading those tasks. So that's used inside Falcon to do things like graceful restarts. So you can reload your application without dropping connections and so on. So async-container serves as the the foundation that bridges the gap between CRuby and JRuby and TruffleRuby in a way that the users don't have to worry about it. Async-container is a vehicle for getting parallelism out of your implementation. And it creates async reactors per CPU process and then you can get concurrency. So it layers it all up and in a way like you don't have to be concerned about how that layering happens. You just write your code and you say make me containers make me eight of them make me 30 of them and it will just work. 

**Jeremy** That's really exciting because it sounds like you built out this whole ecosystem in terms of tiers. If you're building an application you start with using the async library and using the async I/O library and just working in a single process without having to create threads and things like that. And if you have a need for actual parallelism then you bring in async-container. And like you were saying as far as the shared state you can make use of things external to Ruby but basically gets you the same result in terms of using external database or pipes.

**Samuel** I mean plenty of people use things like memcache for PHP systems, right? It's super common because PHP has a one shot process model. So when you get a request it basically spins up an interpreter and it discards them, which is awesome. As you don't need a super complicated GC. It's pretty clever. 

And in the same sense dropping them in memcache. We don't have an async adapter for memcache yet, but it's definitely on the cards. We're just really polishing up the asynchronous redis implementation and it's actually being used by a number of people now, which is pretty cool. 

But ultimately. You know when you look at shared mutable state sometimes doing it in process is just a bad idea anyway. I think when you look at it from a semantic point of view. If you have code which is depending on shared mutable state it's very hard to reason about how it behaves in any given situation because it could just depends on so many factors. 

So the whole async ecosystem is built around isolated classes which are layered together or composed together to get the behavior you want but there's no hidden internal state which is shared between those instances. Like you will never run into a situation where-- never say never right? But in theory is designed around those those kind of concepts that you make a class, you set it up, you do something with it, and you finish with it. And then there is the lifecycle. Lifecycle is a really big thing and making code predictable to users is just in my mind like the most to me personally. It's really important. Like I want to be able to reason about the code I write. If I can't something is horribly wrong (laughs). 

**Jeremy** Yeah, that's a conversation a lot of language communities are having now in terms of, what are your dependencies and do you understand what's happening in them? I think in a lot of cases it's almost impossible to really understand all the things that you're including in your program. 

**Samuel** So one really exciting thing that came out of a conversation just a few days ago was this idea around trying to understand exactly what you just talked about. What are your hidden dependencies? 

And so to give you an idea of what we currently do with async. There's a gem called async-rspec and that gem implements a whole bunch of convenient rspec contexts like one is for detecting socket leaks like if you forgot to close the socket then it will give you a warning and fail the spec. You can go expect block of code to not allocate any strings or to allocate one string of size 3 megabytes or you can put constraints on memory allocations and falcon has a whole ton of them. So we don't have any memory usage regressions and another one recently came out of this conversation we were having was the idea of saying this block of code should not mutate any global state. 

We don't know if it's possible to implement or not. Of course, I can go and start working on the CRuby hooks that are necessary maybe makes sense. But the idea was imagine if you could just put in your specs like: this whole spec by the time this spec is finished the memory that all the memory that ruby is looking at has not changed like there is no obvious side effect of running this code and the idea would be that you could take an existing system and evaluate where are the issues? 

Let's take the Money gem for example and I add an exchange rate and hold on a moment this shared global has been modified. Did you realize it was happening? Maybe that's obvious, but maybe it's not obvious when that gem is layered ten layers deep in some other person's library you just don't know right? So the idea is that could you take something like your own code and then check how pure is this? Is it something which is modifying or accessing global state or is it something which is isolated to its own state and I think you'd have to have certain exceptions because sometimes you do have local caches so you'll be able to say some expect this block of code to not modify anything except for this thing. Anyways it's kind of Pie in the Sky dreaming, but it will be really interesting to see if something like that was possible through ruby. We just need to add some trace point hooks for when you modify a variable like global variable or instance variable something like that. And if you could do that if you could track those changes, yeah that to that to me seems like a really incredible tool for trying to understand code and understand where things could possibly go wrong.  So there's tons of code out there like that does detect race conditions and multi-threaded code. I don't know if you saw the recent article, but Google implemented a race detector in the Linux kernel and they literally found hundreds of race conditions. What hope is there for the rest of us if the Linux kernel developers can't get all of those conditions correct? You just shouldn't need to care about this stuff.

**Jeremy** Any help that the computer can give us as developers we can always use. That's really been pushed with languages like Rust and Elm. An attempt to have the computer help us more in terms of discovering mistakes. And I know with Ruby definitely we could use that given its Dynamic nature, but it's it's hard right? 

**Samuel** Yeah in C++. We have the [Undefined Behavior Sanitizer](https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html) UB SAN and A SAN [AddressSanitizer](https://github.com/google/sanitizers/wiki/AddressSanitizer) and they are just amazing tools for looking at how code behaves if you have multi-threaded code. So I've implemented fibers for C++ as well. Actually Ruby was the Prototype and C++ was the real deal was for a commercial contract. It was really fascinating because the address sanitizer was super helpful at pointing at issues with like handling memory, use after free, and potential issues. I just think we lack sufficient tooling for Ruby in those areas. We're starting to get it. Me looking through code manually and trying to figure out if there's race conditions is kind of you know. What we need to do is we have to scan through the top 10,000 gems and go which of these gems have potential race conditions and then figure it out. It's just not feasible for one person to go through all this stuff and deal with it. But the potential risk is massive.

**Jeremy** Yeah, I would imagine with C or C++ it's just a matter of time investment right? We have so much critical infrastructure that's built on top of those languages that there are probably companies that are funding that type of tooling. 

**Samuel** I think yes and no. My understanding is like the address sanitizer and the undefined Behavior sanitizer came from Google. So obviously they invested heavily in C++ and obviously with the race condition detector they heavily invested in Linux. So I don't think they do it just out of the goodness of their heart, but it just makes sense to them to do it, which is very nice and they give it to everyone so that's awesome. 

I guess with Ruby we're at a point where concurrency and scalability is potentially becoming a bigger issue. So having appropriate tooling to help detect issues and manage them would make sense. And I think one of the big fears that people might have of async would be what kind of issues might I have that I didn't realize I had. But it's kind of tricky. It's one of those things that when you look at async you think okay. Well, it's single-threaded and it's isolated. So what are the potential issues that you could have with it? And the potential issues are more to do with people who have assumed code will run strictly sequentially, but those issues also exist with threads and are actually worse. I'm giving a presentation at Ruby World Conference in Japan in a couple of weeks and my goal is to put it out there. Yes, you should be fearful of concurrency and parallelism and that includes async to a certain extent but you should be more fearful of threads and systems that use threads because the potential chance of issue objectively looking at code is much worse. And I think that that's the problem we're faced with right now. 

**Jeremy** You've put a lot of thought into this ecosystem for async. So I'm really excited to see people run with that and we get more of a focus on concurrency and Ruby and maybe not think about threads so much. 

**Samuel** Yeah, I'm super excited people are starting to use it. It's not just casual and I just tried it out. People are using it in production systems and they're giving good feedback. Okay it worked or we had this issue or we had one person who tried it. Was super excited. Deployed Falcon. Falcon is like zero point something so it's not really stable. I mean, it's still in an unstable point and we had a funny joke. We just said it was the longest issue in GitHub's history. He was trying to replace Puma with Falcon for this middleware proxy serving hundreds of maybe even gigabytes of data per minute or something and Falcon had some issues with leaking sockets based on their use case and we fix some of them. And what was fascinating was that there's two ways of looking at it. You could go Falcon's not as good as Puma or Falcon's not as good as X or async is not as good as threads or whatever or you can say. There is one person who has been toiling away for a couple of years who's passionate about these issues and the fact that Falcon performs 99% as good as Puma. This is just incredible and in some situations can perform way better. So that's the exciting thing if you can get on board with it, if the people can get excited about it, and try it out. That is just the most awesome thing ever. I'm really excited by people who invest effort in it and I have had some of the most amazing experiences over the past year with people who have been excited and yourself included. So I thank you so much for that. 

**Jeremy** Thanks for putting in the work and you know for agreeing to chat today. You put a lot of thought into the API and into the documentation. I remember in the past looking at Celluloid and trying to get to grips with what it was doing and how to use it. And I found it a lot more challenging and I found that async was a lot easier to jump into, take a look at some of the examples, and really see the case for why this could be something really great for Ruby. So thanks so much for for doing all of that.

**Samuel** You're totally welcome. Thank you. Thank you as well for trying it out. 

**Jeremy** To wrap up for anyone who's interested in checking out async or checking out falcon or the work you're doing. Where should they head? 

**Samuel** The best place to go right now is probably the GitHub page for async, I'm sure we can post a link to that.

**Jeremy** Yeah, we'll get that in the notes. 

**Samuel** And you know, we don't really have a forum. We do use gittir for chat but what I would suggest is if you have questions, sometimes those questions are actually actionable documentation changes. So, please feel free to submit issues even for just basic questions because if you have that question then clearly the documentation needs to be improved so I welcome interactions through GitHub issues. 

**Jeremy** I know you've given a couple of conference talks. So we'll be sure to get those in the notes and you've got one coming up you said in just a couple of weeks, right? 

**Samuel** That's correct. Yeah, that should be exciting. I'm supposed to submit the slides today, but I'm still working on them is that normal is everyone in that situation? I'm not sure. 

**Jeremy** I've heard different things. There's some people who are very let's very organized. Yeah, very organized and then--

**Samuel** Some people who are still writing the slides on the day before the presentation.

**Jeremy** They're like I need to go to a quiet place so I could just finish and it's like all right. You're going to have three this year?

**Samuel** Yeah, it's been crazy things that are picking up steam, things are happening. It's super exciting. Matz is interested in it. That's awesome. I'm always excited about all this stuff. It's just incredible and it blows my mind 

**Jeremy** I watched your last video where you had the 1 million connections you had Matz press the button to get that last one. So, that's awesome. 

**Samuel** Yeah, it was awesome. Hanging out with Matz and the rest of the Ruby team-- they're such an awesome bunch of people. So yeah, I'm super honored to be invited and involved.

**Jeremy** Cool, thank you again for agreeing to come on and look forward to seeing where the future of async goes and the future of ruby in general. 

**Samuel** Thank you so much. 

</div>