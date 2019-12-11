+++
title = "Rust in Production with Armin Ronacher"

description = "Armin Ronacher talks about getting into Rust, when to use it, writing Rust extensions for Python, building web applications with actix, creating debugging libraries, and the Rust ecosystem."

[extra]
episode_url = "https://media.transistor.fm/d60c954f.mp3"
+++

Armin is the creator of the Flask web framework, the Jinja2 template engine, and many other open source projects. He's currently the Director of Engineering at Sentry.

### Topics
- Deciding when to use Rust
- Concurrency in Rust
- When to create a separate service
- Introducing Rust at Sentry
- Challenges of writing Python modules in Rust
- Creating Symbolicator, a Rust web service that processes debug files
- Using Actix to create Symbolicator
- Why Rust doesn't need a Django or Rails equivalent
- Concerns about the stability of the Rust ecosystem and the lack of shared - solutions
- What's missing in the Rust ecosystem
- Why developers need better debugging tools

If you're interested in helping Armin build an open source debugging community, reach out to him via [e-mail](mailto:armin@ronacher.eu) or [twitter](http://twitter.com/mitsuhiko).

This episode is part of the [Rustacean Station](https://rustacean-station.org/) feed.  Check it out if you're interested in hearing more about Rust.

### Armin Ronacher
- [Personal Site](http://armin.ronacher.eu/)
- [@mitsuhiko](https://twitter.com/mitsuhiko)

### Sentry
- [Building Sentry: Symbolicator](https://blog.sentry.io/2019/06/13/building-a-sentry-symbolicator)
- [Symbolicator](https://www.github.com/getsentry/symbolicator)
- [Semaphore](https://github.com/getsentry/semaphore)
- [Milksnake](https://github.com/getsentry/milksnake)

### Other Links
- [Actix](https://actix.rs/)
- [Rocket](https://rocket.rs/)
- [Wasmer](https://wasmer.io/)
- [Existential Types](https://github.com/rust-lang/rfcs/blob/master/text/2071-impl-trait-existential-types.md)
- [Tokio Tower](https://github.com/tower-rs/tokio-tower)
- [RFC to add Backtraces to standard error in Rust](https://github.com/rust-lang/rfcs/blob/master/text/2504-fix-error.md)
- [Future](https://doc.rust-lang.org/nightly/core/future/trait.Future.html)
- [Erlang](https://www.erlang.org/)

### Timestamps
- 0:37 - What got you interested in Rust?
- 2:19 - Abstraction with good performance in Rust vs Python
- 4:11 - Rust doesn't need asynchronous code
- 5:31 - Building thread safe applications
- 6:26 - What excited you about using Rust?
- 8:20 - Sentry
- 11:02 - Introducing Rust to Sentry
- 13:10 - Anything easier to write in Rust vs Python?
- 16:14 - Writing extensions vs writing services
- 19:22 - Flow of sending a minidump to Symbolicator
- 21:56 - Symbolicator makes sense as a service
- 23:26 - Building a better debugging world
- 24:33 - More things symbolicator does
- 25:27 - What's Milksnake
- 28:04 - Other ways to embed Rust in Python
- 30:08 - Why use Actix for Symbolicator?
- 34:44 - Is it too early to write web applications?
- 37:30 - What would you do differently in hindsight?
- 42:20 - Don't want a Django or Rails
- 43:58 - When to write a web application?
- 47:34 - What do you wish existed in Rust?
- 49:57 - Game backends
- 51:44 - Anything else?
- 53:26 - Why companies aren't using Rust for web development
- 54:23 - Why async/await is not the only blocker for web development
- 56:43 - Resources for web development in Rust
- 58:24 - Wrap Up

---

## Transcript

Transcript for this episode is coming soon.