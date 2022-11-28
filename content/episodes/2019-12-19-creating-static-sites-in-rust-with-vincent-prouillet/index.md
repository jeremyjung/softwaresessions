+++
title = "Creating Static Sites in Rust with Vincent Prouillet"

description = "Vincent Prouillet talks about his experience building the Zola static site generator and reflects back on five years of work with Rust."

[extra]
episode_url = "https://pinecast.com/listen/ab5a137d-8870-42cb-bf52-f52bf4d0253b.mp3"
+++

Vincent is the creator of [Zola](https://www.getzola.org) (Formerly Gutenburg), a Static Site Generator built with [Rust](https://www.rust-lang.org/) and [Tera](https://github.com/Keats/tera), a Jinja2-like template engine.

If you create a site with Zola, Vincent would appreciate you adding your site to the [EXAMPLES](https://github.com/getzola/zola/blob/master/EXAMPLES.md) file in the repository.

You can also take a look at the source for [this website](https://github.com/jeremyjung/softwaresessions), which is currently built with Zola.

### Vincent Prouillet
- [Personal Site](https://www.vincentprouillet.com/)
- [@20100Prouillet](https://twitter.com/20100Prouillet)

### Zola
- [Zola Website](https://www.getzola.org)
- [Zola Forum](https://zola.discourse.group/)

### Tools/Crates used by Zola
- [pulldown-cmark](https://github.com/raphlinus/pulldown-cmark) (Markdown)
- [syntec](https://github.com/trishume/syntect) (Syntax highlighting using Sublime Text definitions)
- [rayon](https://github.com/rayon-rs/rayon) (Parallel computation)
- [heaptrack](https://github.com/KDE/heaptrack) (Memory Profiler)

### Static Site Hosts
- [Github Pages](https://pages.github.com/)
- [Netlify](https://www.netlify.com/)

### Crates for Web Applications
- [jsonwebtoken](https://github.com/Keats/jsonwebtoken)
- [Bcrypt](https://github.com/Keats/rust-bcrypt)
- [Validator](https://github.com/Keats/validator)

### Compiled Template Engines
- [askama](https://github.com/djc/askama)
- [maud](https://maud.lambda.xyz/)
- [horrowshow](https://github.com/Stebalien/horrorshow-rs)

### Runtime Template Engines
- [Tera](https://github.com/Keats/tera) ([Jinja2](https://www.palletsprojects.com/p/jinja/)-like HTML template engine)
- [ramhorns](https://github.com/maciejhirsz/ramhorns)
- [rust-mustache](https://github.com/nickel-org/rust-mustache) 

### Static Site Generators
- [Hugo](https://www.gohugo.io)
- [Jekyll](https://www.jekyllrb.com)
- [Pelican](https://blog.getpelican.com/)

### Other links
- [Forestry](https://forestry.io/) (WYSIWYG CMS for Static Sites)
- [Keyword Arguments RFC](https://github.com/rust-lang/rfcs/issues/323)
- [kickstart](https://github.com/Keats/kickstart) (Scaffolding tool)

### Timestamps

- [00:00:19] What's a static site generator?
- [00:03:12] How easy is it to build and edit a site?
- [00:07:18] Why create a new static site generator?
- [00:11:55] The Tera template engine and Vincent's experience building it
- [00:17:13] Creating filters and tests to use with Tera
- [00:23:49] What's a taxonomy?
- [00:25:08] Mapping content to URLs
- [00:30:13] The experience of being an open source maintainer
- [00:33:17] Rust crates and features used by Zola
- [00:36:17] How the Rust ecosystem ensured fast performance
- [00:39:55] Is Rust ready for web applications?
- [00:42:45] What applications are best suited to Rust now?
- [00:46:10] Issues or things you wish existed in Rust?
- [00:50:28] Helping out with Zola

Theme music is [12:30 AM](https://crystalcola.bandcamp.com/track/12-30-am) by Crystal Cola.

---

### Transcript

<div class="transcript">

**Jeremy:** Hey, this is Jeremy Jung. On this episode of Software Sessions,
I'm talking to Vincent Prouillet, the creator of the Zola static site generator.

We get into why you would use a static side generator, creating Zola with Rust
programming language, and his thoughts on building web applications in Rust.
Vincent, welcome to the show.

**Vincent:** Hi, thanks for having me.

**Jeremy:** To start, for those who aren't familiar with static site generators, could you explain what they are?

**Vincent:** Yeah, so the idea of a static site generator, in most cases, is
that you have some contents which is usually in Markdown and you want to output
a site or some HTML. And what the static site generator does is take that
Markdown and convert it to HTML. Usually there's some kind of templating going
on so you can have your own theme, your own design, and it outputs static HTML
files, which means that your site can be hosted anywhere. It can be just S3
buckets it doesn't have a backend so think of it like WordPress, but your site
doesn't have an actual backend. It's just some files that you can set anywhere
and that should work.

**Jeremy:** And, how is this different than like a long time ago, people used to just write HTML by hand and they would build their web pages one at a time. What makes this different than those old days?

**Vincent:** That's a good point. If you have a very basic site, like just a few pages, it's probably not worth it to use a static site engine. You can just
write your HTML and that's going to be fine.

The main use case for Zola and other static site engines usually is around
blogs. That's more or less the main use case. There are a few others like
landing pages and knowledge bases but let's focus on blog for now. When you have a blog you might have categories, tags, taxonomies— anything you want. You want to sort your blog posts so they appear in order. You might want to do some things, like, if you're a programmer you might have syntax or code in your blog post that you want to highlight. You might want to do some more complex things like embed YouTube videos or images anything like that which scales okay if you're writing HTML. Like, if you're writing one blog post a year it's fine. If you have dozens, hundreds it's starting to be much harder to do, because let's say you're writing the HTML by hand. If you want to change something in your design, you just need to update everything. With a static site engine you just update the template and all the pages will be updated automatically when it's rendering.

So it's just easier to scale basically and, yeah, you gets lots of nice features that you might not get, like for example, most static site engine will get you a RSS feed, get you a sitemap, get you some other things that might be much more annoying to do yourself. One of the example would be, Zola builds a search index for your content if you want to, and that's not something you want to write by hand.

**Jeremy:** And so basically you can create these templates and Zola or a static site generator in general can perform things like syntax highlighting,
generating RSS feeds, letting you search your website, things like that. And
that's kind of all taken care of for you.

**Vincent:** Yeah, So the main point of static site engines is they're really
easy to get started, hopefully. So in most cases you can just grab a theme from
Hugo or Jekyll whatever you're using and you can just write your Markdown. You
type a command— `jekyll server`, `hugo server`, or whatever it is, and you have
your site up and working in five seconds. This is just much easier than writing
by hand.

And then, yeah, you get all the nice things that you might expect, like, if you
want to do for example internationalization you can link to the same pages in
the other languages and everything, which is kind of a pain when you are doing
everything by hand.

**Jeremy:** So it sounds like for somebody who is making a blog, they just
choose a theme and the only thing they need to do is create Markdown files and
edit those files and all of the actual posts will be generated for them. There's nothing else they need to do.

**Vincent:** Pretty much. Like, hopefully if it's easy enough to use, with
static site engine it should pretty much be that.

And there are some WYSIWYG interfaces for static site generators. Like I think
there's one called [forestry.io](https://forestry.io) if I remember correctly.

So you can still have your WYSIWYG interface like the WordPress admin, but at
the end you just get some static files, basically. I haven't used forestry so I
can't comment on how good it is, but it's possible to build something like that.

**Jeremy:** Provide a WYSIWYG and that WYSIWYG would generate Markdown files.

**Vincent:** Yeah. You just write it as you would in WordPress. And the fact
that it's static, I'm guessing it can be completely hidden. You don't have to
know about it.

**Jeremy:** So I guess that means that static sites, they're not necessarily
just for people who are developers, but they could also be used by someone who's building a marketing site or a blog for people who aren't technical.

**Vincent:** Yeah for these cases you need to have a WYSIWYG, or someone that is knowledgeable with Markdown, but it is possible because it's kind of an
abstraction, and then you can build on it with a WYSIWYG and the user might not
ever know.

It's just another way of working. So obviously you have some limitations,
because you don't have a backend. So if you want to have something like
analytics, for example, you can use Google Analytics but it's not going to be as nice as WordPress because you can customize things there. It's just more
limited.

**Jeremy:** You're more limited in functionality, but it's much easier to
deploy, much easier to host because as you were saying before, it's basically
all static HTML and possibly JavaScript, CSS, and you don't need any kind of
special hosting or backend.

**Vincent:** Oh yeah, basically you can just host it on pretty much anywhere. I
used to use S3 buckets because there's a thing when you create the buckets, and
you can just drop your HTML files there, set up a domain name and you're pretty
much set to self serve and it's costing probably not even a couple of cents a
month.

There are lots of other tools like Netlify which has free hosting for static
sites, and GitHub Pages has free hosting for static sites because it doesn't
really cost anything to host. It's just serving some HTML files, it's cheap.

**Jeremy:** Yeah, I've noticed that there are a lot of blog posts within the
developer space, of people talking about, how I built my blog and there's kind
of all these pages on how I built it, and all the time it took, but it sounds
like in this case you should be able to get up and running pretty quickly, as
long as you just pick the theme and just start writing Markdown and deploy to,
like you said, S3, Netlify, that sort of thing.

**Vincent:** Yeah, pretty much. As long as you don't do it like me, and just
write the static site generator.

**Jeremy:** Yeah. So I wanted to ask about that because there are a lot of
choices for static site generators. There's Jekyll and Hugo and Gatsby and so
forth. What made you decide to create another one?

**Vincent:** So at the time I think it was 2016, something like that. I had
about four or five different static sites online. One of them was in Pelican
which is a Python static site generator and everything else was in Hugo. So just for context, the Pelican one, since it's Python you actually have to have a Python environment, and it was kind of slow. Like, generating my site was taking over a minute, I think. And I had very few posts at the time.

I discovered Hugo which is written in Go. So you just need a binary — you can
just drop the binary anywhere in your computer, and you run it and it's going to generate your site in milliseconds. So obviously that was very interesting. And yeah, I made about four or five sites in Hugo and the experience is pretty good for the most part. The main issue I have with Hugo is that it uses the Golang template engine, which I find very frustrating. And every single time I had to change something on one of the sites I was just spending, like, an hour trying to remember how the template engine was working.

So at the same time I was playing with Rust. I think I just checked on my blog
because I couldn't remember, but I found out about Rust about five years ago. So before 1.0 and I did one crate, which is a package in Rust, and it was pretty cool and I really wanted to find a good excuse, basically, to work on some projects. And at the time it was pretty empty, the ecosystem, because there was almost nothing, like, for a template engine for example. There was `handlebars`, and everything else was based on Rust macros so you couldn't use it for a static site generator. So there was only `handlebars`. And since most of my time is Python developer I'm used to a template engine called Jinja2, which is the one mostly used with flask, and the Django template engine, which is kind of very similar to Liquid in Ruby, and Twig in PHP, I think it's called.

So at the time I started basically with a friend, thinking of a project for
static site generation, because it's kind of an easy project to start with. You
just take some Markdown and output HTML. How hard can it be, really? And we just had the code to load Markdown and then we realize, like, okay, it's missing the template engine, because we didn't really want to use `handlebars`. We wanted something more like Jinja. And, yeah, I went down the rabbit hole and I ended up writing the Tera template engine, which is very very similar to Jinja2. Since I use that for work, I just wanted something that is close enough, and familiar to everyone coming from Python or Ruby. So it's easy to use because familiarity is very important, I think.

After the slight detour, I came back to work on— at the time it was called
Gutenberg. And I think the first release was in 2017, and it was very very basic compared to what it is now. I looked at the release post on my blog, and I mean, it does quite a few things but compared to the current version it's very basic. 

And yeah, I mean, it got some traction. I think part of it was because it was in Rust, when Rust was basically popping up everywhere. Blog posts about Rust were getting to the top of Hacker News and everything all the time. So I think it got some traction from that. And then, quite a few people started using it, and starts getting a lot of contributors now, so that's pretty good.

**Jeremy:** And you were talking about how you first started building Gutenberg, or I guess now it's Zola, and was the very first thing you worked on, was it that conversion from Markdown to HTML? Was that the very first piece?

**Vincent:** Yeah. So at the time, with my friend we didn't really have a— we
didn't really look at the ecosystem at all. So we just first tried to find
whatever Markdown crates existed at the time. And when we manage to load the
Markdown, and convert it to HTML, we realized that it was missing the template
engine. It was like, hmm. That's a bit of a blocker, so back to the board.

**Jeremy:** So could you go into a little bit more about, what's involved in
building a template engine and what a template engine is?

**Vincent:** Yeah, of course. So, there are two kinds of template engines.
There's a compiled template engine, which in Rust would be something like
`askama` or `maud`, `horrorshow`, which are some kind of DSL, which are
basically Rust macros that get expanded to Rust code. And this kind is very fast because in the end, it's just Rust code and most of them you get type checking as well, which is very nice.

But to make that work, you need to have Rust basically so you need to have the
`rustc` compiler, which you can't really ask someone creating their own
templates, writing their own HTML templates, to just compile that site with
`rustc`. So there's a second category which is interpreted template engine,
which are essentially programming languages, kind of. There are a few
variations, like, you can have templates, but have no logic whatsoever, almost
something like `handlebars` which is just rendering, but you can't do some more
advanced things, like setting values in the templates, or doing some math in the templates, for example. And Tera is trying to be closer to Jinja, where you can actually write Python in the template.

So obviously we can't go that high level but you can do math, you can do a lot
of things in a template, compared to what would be possible in some other
template engine. But, yeah, it just allowing you to do a lot of things, it has a lot of logic. There's another one in Rust called `ramhorns`, I believe, which is very very good as well. But usage is limited, because when people are writing templates, theme, for a site, you never know what they're going to want to do. And it's better in that case to just try to give them as much as possible, and hopefully it will work out in the end.

But yes, even now Tera is still missing some pieces. Like, just today I had
someone asking me if there was a way to add negative filters in Tera. It is when you have an object, you can actually right now, filter objects based on an
attribute's value. So you can say, okay, give me all the posts where the year is 2018, and that person wanted to do the opposite, so give me all the posts that are not from 2018, and this is not currently implemented. So it's kind of a balance. You don't want to go crazy in terms of features but you want to let the user be able to do most of what they actually want to do. And it's kind of
tricky.

**Jeremy:** So if I understand correctly, a template engine is where somebody
would write out, say, their HTML, but then be able to introduce, additional
behavior or additional Rust code that would be compiled down to the end result
that ends up in the HTML. To give an example, if I had a blog post and I wanted
to have a pretty-printed timestamp, and maybe an estimate of how long it would
take to read the post, I could write some special code that's specific to Tera,
specific to the templating engine, that would retrieve the date that I had
created the post, and maybe the number of words that are in the post, and be
able to execute Rust code to come back with a estimated time for how long it
would take to read, and maybe a pretty-printed date and time, that sort of
thing. Does that sound correct?

**Vincent:** Yeah, exactly. The only thing I would change from the definition is just that a template engine is not necessarily for HTML. For a static site
generator it's the case, but you can also generate Rust files, Python files,
XML, JSON. It's basically just a way to get some text outputs based on some
context.

**Jeremy:** And is everything that the user is able to do, whether that's have a conditional like an if statement, or the example we gave before, is the syntax or the design for that, is that all created by you or is the user able to execute arbitrary Rust code?

**Vincent:** So in Tera, "blocks" as they're called are defined at the grammar
level, since it's basically interpreted language, and users cannot define their
own blocks, but they can easily write their own filters. So a filter, for
example in Tera would be, to get back to the previous example, you might have a
date and you can do `| date(format="...")` and you can pass the format you want
to be formatted, and that specific date filter will actually execute code based
on the value that was input before the pipe.

So it's kind of like Unix where you just pipe values from function to functions
in a terminal. So you can define your own filters, you can define your own
tests, which is something, like, let's say, you want to say "if number is odd",
like, in that case "odd" is a test but you can define your own tests. So for
example you could have "if filename is gzip" and that would be a Rust function,
and you will get the filename as an input, and you can do whatever you want on
that, and you can return in that case a boolean, saying whether it's a gzip or
not.

There's a third type of things you can customize in Tera, which are functions.
So in Jinja2 it's super easy, because you can just set whatever function you
want to in a dict, and that works but it's a bit more complex in Tera because
it's compiled. For example in Zola, if you want to get a page from another page, let's say you want to get the last three posts on section or something, you can call a function called `get_section` with a path and that function will return the last three posts, all the posts for that section, but everything there is executing in code, so it's just a way to interact with a behind the scenes roughly. Another example which is less hard to think of is a function to get the dates, the current dates, current timestamp. Or a random number, or something like that. So yeah, you can define your own. Zola and Tera comes with some built-in and that's the hook to customize your own template engine, basically. I believe there's some way you can customize the block level, but it's not really the way Jinja2 and Django works, so I try to match as much as possible that behavior.

**Jeremy:** And so earlier you were talking about the filters, and you were
saying how it's similar to a Unix pipe. So I believe you were saying that you
could have a set of data, whether that's a collection of posts or it could be
just a string, and then you would have a pipe character, and you could basically pass that information to a function that would transform the data in some way.

Is that a function that the user is able to create themselves, or is that
limited to ones that are already built into Tera?

**Vincent:** No. Users can define their own filters.

**Jeremy:** And when they create their own filter, they would be writing
standard Rust code in order to do that?

**Vincent:** Yeah. It's essentially just a function that takes the inputs, which is— so the way Tera works is, it converts everything to JSON. So it takes a JSON value, some arguments, which for example, if you have a "date format" filter you might have a format argument, and it returns a value, and it's just a normal function. In V1 of Tera, filters, tests, and functions are actually traits, so you can implement it in more than just a function, but for the easy case, yeah, it's a function.

**Jeremy:** We were talking about how there's a bunch of different static site
generators, and it sounds like this may be one of the distinguishing factors for Zola, because if somebody wants to write their own functions, they're able to do so in Rust.

**Vincent:** Yeah, and I wasn't clear enough. So for Zola, we need to add it to
the code of Zola because— so when what I meant about users can add their own
filters is, users of Tera in Rust code. So users of a static site generator
can't define their own tests, because otherwise they would still need to have
some Rust compiler to make it work, and that's going to be messy. But if you
want to you can create your own fork and add a function, but that's the same in
everything. It's not as nice as, let's say Pelican, for example, which is
Python. And on my site at the time, I needed some specific function, so I just
added a Python file, and it was working, because you can pick it up. But yeah,
in Zola and Go you would need to define it in the Zola binary first.

**Jeremy:** I see. So it would have to be a part of Zola. That's interesting
too, to think about, like, how Tera itself is really the standalone piece that
kind of does a lot of things in Zola, but is ultimately, you know, not tied to
it.

**Vincent:** Yeah. I try to not keep it tied too much, obviously, since I'm
using Tera for Zola, I find more bugs and I find more use cases than I would
have found otherwise. But yeah, I don't tie it to Zola, because I'm using it for other tools, like, I have one tool called `kickstart`, which is just to generate projects easily. So if you're familiar with Cookiecutter, it's pretty much the same thing in Rust. And, yeah, in that case, I mean, it could be templating anything, so it could be templating Markdown files, Python, Rust, whatever. So it's important for me to not have it tied completely to Zola.

**Jeremy:** You had mentioned earlier one of the features of Zola is something
called a taxonomy. I noticed a number of static site generators have this
feature. Could you explain, what that is and what's the use case for it?

**Vincent:** Yeah, so the most common use cases is probably for blogs, so you
have categories, tags. Let's say you're writing an article about Rust. You can
add a category of "programming", add a tag "rust", for example. And your static
site generator will automatically generate some specific pages for that
category, and that tag, and you can find easily all the articles with the tag
"rust", for example. So it's just another way to organize contents, which gets
automatically generated by the static site generator, so you don't have to
really think about it.

**Jeremy:** Let's say you're using the blog post example. If I had a blog post
about Zola, I might be able to reach it at `/posts/zola`. But because that post
was also about Rust, I might be able to access it at `/rust/zola` in addition to `/posts/zola`?

**Vincent:** Usually that would be more like `/tags/zola`, but that's the gist
of it, yeah.

**Jeremy:** And so if you have contents that are related, like to give you an
example, for a podcast where you might have episodes. So you might have
`/episodes/zola`, for example. And if you had information that was related to
it, like, let's say we had a transcript for our conversation now, would it be
possible to, have `/episode/zola/transcript`, or would that have to be in its
own unrelated URL?

**Vincent:** So the way Zola works is, kind of, let you do your own thing with
the URLs. So that kind of depends on how you set things up. You could do it
manually. So in Zola every time you create a folder, it creates a path,
basically. And every time you create a Markdown file it creates a page at that
exact path unless you override it. But that's kind of up to you, where you can
easily do some asset colocation. So you could have a folder for episode one, and in it you could have a Markdown file where you're describing what's happening. You could have transcripts, in I don't know what kind of format— if it's like a page, would it be a different page?

**Jeremy:** Yeah. Let's assume that, if you were to look at the transcript, you
would want it to be rendered as a template, be rendered as a page.

**Vincent:** Yeah I think in that case I would probably do it manually. This way you have control of exactly how things work, and yeah, you can select the
templates to render for each page easily. But I think it would be just easier to just do it manually. I don't think there would be a way to do it automatically.

**Jeremy:** So Zola would not necessarily be aware that the two things are
linked, but just by putting the files in the correct place would build out the
URL, to kind of match what you're looking for.

**Vincent:** Yeah. You could always have— I mean, every page and section in Zola has something called an extra dictionary, where you can put whatever data you want. So one way would be to just manually add the path to the related page, and then you can just add the link to it, if it's present. But there's no way to automatically relate contents between each other.

**Jeremy:** Yeah, that makes sense. We've been talking a lot about how static
sites and how Zola are used in the context of blogs, but you also mentioned that there might be some other use cases. What are the other use cases, or maybe what's, kind of, the most complex example you've seen of someone building with Zola?

**Vincent:** I think the weirdest is one I've made myself as a theme. It's
called "book", which is the same template as gitbook— I don't know if you're
familiar with it, but it's a sidebar, and content next to it, which is made to
look like a book. And basically a lot of things going on in the templates to
make sure that we're getting the right page, and the next section, and the
figures and everything. It's probably the most complex usage of Tera I've seen.
The most complex usage of Zola— there are some people doing some interesting
things. Sometimes, like, asking for a specific features for their own use cases, and it's kind of hard to say yes, because you want to make sure that use case is useful for more than one person. But yeah, in terms of example, I don't have anything like the name itself coming up to mind.

**Jeremy:** Are there any features of Zola you often see people misunderstand,
or are misused, or any advice you'd give to new users?

**Vincent:** I think most of it is my fault with the documentation not being
clear enough in some ways. So right now, someone is helping me with that
documentation. So it should be hopefully better.

I think the most confusion happens with how section works because it's kind of a concept that— so just for context, a section is a folder, basically. When you
have a folder it creates a section, and you can define some specific contents by putting a file called `_index.md`. And in that section that's where you control things like whether all the posts of the files in that section will be
paginated, how they will be sorted, how they will be— something that is called
transparent section. So sometimes you just want to pass all the contents of that section to go one of above. So yeah, I think section is probably the most hard to understand. And yeah, I think at that point it's just better documentation, and yeah, we're working on that.

**Jeremy:** And sections, it seems like that would be to basically hold
collections of content, whether that's blog posts, or podcast episodes, or
anything like that.

**Vincent:** Yeah, pretty much.

**Jeremy:** So you've been working on Zola for over two years now, right?

**Vincent:** Yeah.

**Jeremy:** What are the biggest lessons you've learned from working on it?
Whether that's about maintaining an open source project or about Rust, like
basically anything you can think of.

**Vincent:** I think a very very nice thing is, when sometimes I receive an
e-mail saying like, oh, I really like Zola, it's amazing, that helps a lot,
like, because I have quite a few crates, packages, in Rust, and it's always nice to receive something like that. It just motivates me and I guess anyone
receiving this kind of messages.

I was expecting more, I'll just say negativity, because sometimes let's say
developers are not very kind online. But, yeah, otherwise it's been pretty good
so far. And yeah, in terms of learning about code, I mean it's one of the bigger projects I've worked in terms of codebase, outside of other work things of course. And I think right now, it's at something like almost 20,000 lines and it's still feeling quite good and basically sometimes, I just spend more time seeing emails, like sometimes I just get 10 emails about various projects, and the time I allocate to do some open source, it's just gone just by replying to some questions. And yeah, otherwise collaborating with a bunch of people. I've seen lots of people coming to Zola having never used Rust, and doing that first Rust pull request on Zola, and that's really cool.

**Jeremy:** Yeah, that's really neat, because I think a lot of people are kind
of interested in Rust, but they're not really sure what types of projects they
can get started with, or how they should start learning. I've heard from a lot
of people that, actually static site generators, when you're learning a new
language, that's actually a great place to start, just because there's so many
things involved, whether that's working with the file system or working with
strings or network, that kind of thing. There's kinds of lots of well-defined
problems for people to dive into.

**Vincent:** Yeah. And usually it's kind of well-isolated so you can focus on
something specific. So let's say you want to add a small feature about Markdown
rendering for example. You know that it's going to happen in one place, and
that's fine. It's not like some crazy web app where they might be signals
everywhere. It's just well-defined and with Rust, the compiler is really helping you as well. So anytime you don't know what you're doing, you just read the error, and it kind of tells you what to do sometimes. Sometimes not really, but most of the time.

**Jeremy:** Yeah. And one of the things that we had kind of talked about was,
you were building Zola and you realized, oh, there's no templating engine. So
that's why you needed to build Tera. Were there any other large gaps in terms of crates or things like that you found while you were building Zola?

**Vincent:** Yeah. So for Zola itself, it's lined up pretty well because there
was `pulldown-cmark`, which is the Markdown crate that was released kind of at
the same time. There's also an amazing crate called `syntect`, which does syntax highlighting based on the Sublime Text syntax definition. So you get the exact same syntax highlighting as in Sublime. And at the time it was pretty much all the stars aligning, and after the template engine there was nothing really blocking.

Pretty much all of my other crates were for web stuff, really. That I think it's still kind of not there yet, but at the time it was even worse.

**Jeremy:** Since you've started using Rust, after, you know, working on Zola
and after all your experience with Rust, how has your use of Rust changed? Have
there been stylistic changes to the way you write your code, or the way you
organize that sort of thing?

**Vincent:** I think kind of in the last couple of years, the `rustfmt` tool
became more stable, which is a tool— if you're familiar with go, like `gofmt`,
or `prettier` in Javascript— that just formats your code. So now I don't really
think about the style itself. I just run that and commit. Sometimes I don't even look at it, I just commit.

In terms of new features that I'm using, I'm not really using that many new
features compared to other tools, like, there's no need for async/await or
anything like that. For Zola I'm not too exposed with other new things. On my
other crates, yes. But with Zola itself, the main thing I learned with Zola was
using a cargo workspace, which is just splitting your code in different modules.

The main reason for doing that was because the compilation time was getting
terrible every time I was making a change. So I just split it in some smaller
crates, that makes it much faster.

And yeah, other than that I became more aware of potentially bad things in terms of performance, and just general idiomatic Rust, as I get to write more and more. But yeah, nothing—- no huge change basically.

**Jeremy:** You had mentioned specifically about performance, and how you didn't really have a need for async/await and things like that. One of the defining features of Zola is the fact that it is very fast. So I was kind of wondering, is that specific to just Rust's runtime being very fast, or are there specific concurrency or parallelism related primitives that you're using to have that be the case?

**Vincent:** So I think like there's two or three main things contributing to
the speed. So the first one is obviously Rust. It's very very fast, and the good thing is that lots of very smart people are working on very fast crates as well.

So `pulldown-cmark` is very fast, syntax highlighting is very fast, pretty much
everything is very fast. So you end up, even if you kind of don't think too much about performance, you end up with something decent.

The second thing that is really really amazing is a crate called `rayon` which
is parallelism. Allows you to make it super easy. To create an iterator in Rust
you just do `.iter`, and you get the iterator and you'd just do your action on
it. And `rayon` is a crate where you can just do `.par_iter`, and you'll get
everything working in parallel. And yeah, the moment I started using `rayon` the speed went much higher, because I was just doing everything in parallel, and using all my cores instead of just waiting.

**Jeremy:** Hmm. So that's like, anytime you have a list of things that you want to accomplish.

**Vincent:** Yeah another very helpful thing is, that since I started Zola which would be something I should have mentioned before, just learn how to do
performance benchmarking better. So I'm using a tool called `heaptrack` to
easily see where the allocations are, how much memory was allocated. And it's
pretty much something I use in most of my crates now, just to find out if I'm
duplicating some data when I could avoid it, or find something crazy when I'm
doing a refactoring and I forget there's a clone somewhere, and now it's just
happening 10,000 times. It just going to show it to me and I can easily find
find even the line, and just look at it. So that's something that was very very
helpful to diagnose performance issues in all my Rust crates.

**Jeremy:** And is this something where you just add it and it automatically
kind of detects things, or is it more you have to add lines into your code to
collect metrics?

**Vincent:** So you only need to, in your `Cargo.toml` you just need to say
`[profile.release]` with `debug = true`, which gets you the debug symbols. And
you just put `heaptrack` before, and then you run your binary and it's
automatically going to connect all the statistics of allocations. And it
generates a report, and then you can just look at it. You don't need to touch
anything in your code.

**Jeremy:** Hm, that's great. The crates ecosystem having very performant
crates. Which kind of allowed you to gain parallelism without a lot of
additional work. And then finally just performing, you know, benchmarking and
metrics with what, what was the last one called?

**Vincent:** `heaptrack`. I think it's only available on Linux.

**Jeremy:** And one of the things I've noticed, just kind of looking through
some of your blog posts is that you have a lot of experience building web
applications, and you have a few crates outside of just Zola and Tera, related
to, say, `jsonwebtoken` and `bcrypt`, and things like that. At this current
point is Rust in a good state to build web applications? Like, what's your
thought on the ecosystem right now?

**Vincent:** So I think it's going to get much better from now. The most awaited feature for web servers, async/await was released in the last Rust version, and it's going to allow a much much more ergonomic syntax, basically. For example I did use `actix-web` recently, which is probably the main web framework in Rust right now.

And at the time, you still had to put everything into futures manually, and just use combinators everywhere. It was not really easy to use, compared to— even Go, or anything interpreted like Python and Ruby. But I think now that we have async/await it should get much better. So yeah, I think 2019 probably not yet, but 2020 it could be a beginning of some good stuff in terms of web services.

**Jeremy:** So if you were to build a web application today, whether that's, an
API or, a full server rendered application, you would probably use, say, Python
versus using Rust, because it's still just too early.

**Vincent:** Yeah, definitely.

**Jeremy:** When you were making your crates, we had mentioned, like,
`jsonwebtoken` and `bcrypt`. Were you using those in production applications?

**Vincent:** No, I don't actually use that much of my own crates in production.
The only one I'm using is `tera` and Zola and `kickstart`. But everything web-
related, most of it started— I think it was, like, four years ago, something
like that. The first crate I did, `jsonwebtoken`, I was just going through the
list of my dependencies in my flask app, and just looking at crates.io which is
the package repository and looking if there was something to do that, and if
there wasn't I would just make one crate if possible. So that's pretty much
`jsonwebtoken`, `bcrypt`, `validator`. All of those are pretty much something I
made because it was missing in the ecosystem but I'm not actually using them in
any of my projects.

**Jeremy:** For someone who's looking into using Rust now, what do you think are the types of projects that are best suited for Rust?

**Vincent:** I think probably any command line tool, because there's an amazing
crate called `clap` which makes it super easy to generate a nice CLI interface,
and that's already a battle out of the way. And then you can just focus on
whatever you want. It's quite fun to write a command line interface compared to
a library, because, let's say you want to write I don't know a library for
stripe, or something like that I mean it might be fun, but it's probably not as
fun as making some kind of a common line game or whatever, if you're just trying to learn the language.

**Jeremy:** And once you're going beyond just learning the language, are there
any types of production applications that you personally would say "I would
choose to build this in Rust."

**Vincent:** Yeah, so pretty much anything that requires speed. So for example,
at work we do write biology things. So based on, for example some file format
parser, and analysis we're doing, we're doing them in Rust because it's much
faster. And then we just expose some Python interface to it. But it's— yeah, if
you need something that is very reliant on speed and performance, it's probably
a good idea to look at if you can build it as a small library or something like
that. And compare, because, like, if you're already using Go, I don't think
there's going to be a huge difference in the Rust and Go runtime. So it's kind
of really up to you as well, if you just want to learn the language it can be
used for anything.

**Jeremy:** In terms of just developer productivity, have you found on average,
does it still take you longer to build a Rust application than it would if you
were working in Python or JavaScript?

**Vincent:** So I think it it depends really on the kind of thing you're
building. For example something like Tera, which is a library where I'm using
lots of enums and using lots of type systems, I think it's probably much much
easier than writing that in Python. I mean Python is probably going to be much
shorter, but I can make changes in Tera, like completely change half of the
code, and I just look at the errors from the compiler, and just fix it and then
run the tests and pretty much all of it will pass. In Python or any non-typed
language, it would be much harder. Like, you just have to have way more tests,
and run it a lot. So yeah, that's something that I think is actually easier to
write in.

And for things that are harder, yeah, I think web right now is kind of hard
depending on what you're doing. I mean, there are some people who are using Rust for web. We actually do use a bit of Rust for web at work, but unless you have, like, a huge number of users it's probably not really worth it right now. Just better to wait for the next batch, or the next versions of frameworks next year.

**Jeremy:** What are the biggest pain points you've had with Rust? Have there
been any?

**Vincent:** Probably compilation time. My previous laptop is now six years old, and yeah, I see compilation time sometimes where just, you had time to go make tea and come back, and yeah, it kind of sucks. It's getting better, and if you need to you can still split your project into components, a workspace, and that's going to help a lot. But it's still kind of slow, especially if your
project is quite big or you're depending on, for example, the S3 crates, the AWS crate called `rusoto` is very complete because it's autogenerated from— I can't remember from where it's autogenerated, but this basically covers all the AWS services, with all the various intermediary structs and everything. So it's a lot of code and compiling that is taking ages, and if you're using it in your project, it is just going to add, I don't know, 40 seconds to your compilation time.

**Jeremy:** Wow.

**Vincent:** I mean obviously after that you have `cargo check`, which only
recompiles things that have changed. But like, for example, if you're building a Docker image and it's going to build it, that's getting a bit more painful.
Comparing it, I built a Go binary the other day, and compilation was done in,
like, one second or two. I mean, I know the compiler doesn't do as much, but
it's kind of a dream.

**Jeremy:** Right. Are there any any crates or changes to the language that you
wish existed currently?

**Vincent:** Yeah, the main one I want would be keyword parameters. And named
parameters, just because it makes it much more robust. So I know that you're not supposed to use booleans as arguments, but sometimes you just don't want to
create an enum just for a small thing, or create the builder pattern to generate the options for a function. It would be very nice to be explicit about the parameter name or value, even have default values. I think for me that's the feature I would like to see the most. It's just that it's not a high priority.

There's a few pre-RFC on it but it's still at the discussion stage. I mean it's
not a huge feature but I think in terms of readability it adds a lot.

**Jeremy:** Yeah. And then, like you said, if it's at the pre-RFC stage, at
least it looks like people are interested and things are starting to move
forward.

**Vincent:** Yeah, Well it's interesting because there are a lot of people that
are interested and some people that don't want it so it's kind of—

**Jeremy:** Ah. What are your hopes for the future of Rust? Like in, let's say,
in five years, what are you hoping that you'll be doing with Rust?

**Vincent:** Well probably being able to just go to crates.io and find every
single crate I need that works, with documentation, that would be amazing. So
yeah, probably have a big ecosystem which— I mean, it's getting on its way. It's already much better than it was a couple of years ago, and it seems like more and more people are starting to use it, so it gets more and more, nice open source projects to be able to use from.

And yeah, in five years would be very very nice if we had some nice web
framework as well. Something let's say, like Django or FastAPI. Something
similar in Rust would be very nice, because really the main issue I had with web was the syntax before, but with async/await there's potential for the syntax to be very nice to use, so looking forward to it.

**Jeremy:** Finally, if someone's interested in helping out with Zola or any of
your other projects, what's the best way for them to start?

**Vincent:** So in most of my projects there should be some tags like "help
wanted" or "good first issue". So if you want to start with Zola specifically, I think probably best to just look at the issues and see if there's any of those tagged. Or you can also send me an e-mail if you have questions.

Zola also has a forum if you go to getzola.org there's a link to the forum, and
you can ask questions there as well. And just feel free to ask any question.
Even if it's just like, why are you doing this, what is this Rust thing,
whatever. I try to reply to everyone so don't hesitate, and yeah, just look at
the issues. If you get confused with some documentation. Don't hesitate to do
pull requests, that's always helpful. Anything can help basically.

**Jeremy:** Cool we'll be sure to get the links to the forum and to Zola and
your other projects as well into the show notes.

Finally to wrap up, is there anything else that you'd like to mention or think
that we should have talked about?

**Vincent:** Oh that's a good question, I didn't think about that. Yeah, I think something that would be helpful is, if you're using Zola it would be nice to add yourself to the examples file on the repo, just so we have more examples to look from for people looking for inspiration. Not much else really.

**Jeremy:** Cool. So if somebody is interested in doing that, they would open a
pull request and add their site?

**Vincent:** Yeah it's a Markdown file in the repository, so you can just edit
it from GitHub directly if you want.

**Jeremy:** And to wrap up, how can people follow what you're doing and follow
Zola?

**Vincent:** So the best place would probably be the forum for Zola, and the
issue tracker. I don't really use any social network. I have a twitter account
but it's fairly silent, I'd say. I don't really look at it very often. I think
The best way would be GitHub issues, probably.

**Jeremy:** And, as we mentioned before, we'll get a link to that in the notes.

**Vincent:** Okay, perfect.

**Jeremy:** I want to thank you so much for talking to me today. And teaching us about static sites, about Zola, and about Rust. I think it's going to be an
interesting conversation for people to hear.

**Vincent:** Yeah, no worries.

**Jeremy:** Thanks again to Vincent for coming on the show. You get shown us for this episode at softwaresessions.com and make sure to check out Zola at
getzola.org. Our theme music is by Crystal Cola. Also, I just redesigned the
software sessions website using Zola. So if you haven't been to the site
recently, check it out. I'm adding transcripts to both current and previous
episodes. If you're enjoying the show, please share it with someone. You can
also send me an email and let me know what you think. All right, I'll see you
next time.

</div>