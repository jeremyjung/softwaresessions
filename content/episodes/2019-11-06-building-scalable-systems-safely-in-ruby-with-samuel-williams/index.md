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

Transcript for this episode is coming soon.