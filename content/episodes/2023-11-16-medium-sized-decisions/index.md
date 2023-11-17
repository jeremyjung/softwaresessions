+++
title = "David Copeland on medium sized decisions (RubyConf 2023)"

description = "Engineering at Stitch Fix, choosing technology, and how different people learn"

[extra]
episode_url = "https://pinecast.com/listen/4c33b02c-2f2e-45a0-ad7b-cc626e4c8a8c.mp3"
social_title = "David Copeland on medium sized decisions (RubyConf 2023)"
social_description = "Engineering at Stitch Fix, choosing technology, and how different people learn"
+++

David was the chief software architect and director of engineering at Stitch Fix. He&#x27;s also the author of a number of books including Sustainable Web Development with Ruby on Rails and most recently Ruby on Rails Background Jobs with Sidekiq.

He talks about how he made decisions while working with a medium sized team (~200 developers) at Stitch Fix.

The audio quality for the first 19 minutes is not great but the correct microphones turn on right after that.

Recorded at RubyConf 2023 in San Diego.

--

## A few topics covered:
- Ruby&#x27;s origins at Stitch Fix
- Thoughts on Go
- Choosing technology and cloud services
- Moving off heroku
- Building a platform team
- Where Ruby and Rails fit in today
- The role of books and how different people learn
- Large Language Model&#x27;s effects on technical content

## Related Links
- [David&#x27;s Blog](https://naildrivin5.com/)
- [Mastodon](https://ruby.social/@davetron5000)

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

## Intro

[00:00:00] **Jeremy:** Today. I want to share another conversation from RubyConf San Diego. This time it&#x27;s with David Copeland. He was a chief software architect and director of engineering at stitch fix.

And at the start of the conversation, you&#x27;re going to hear about why he decided to write the book, sustainable web development with Ruby on rails. Unfortunately, you&#x27;re also going to notice the sound quality isn&#x27;t too good. We had some technical difficulties. But once you hit the 20 minute mark of the recording, the mics are going to kick in. It&#x27;s going to sound way better.

So I hope you stick with it. Enjoy.

## Ruby at Stitch Fix

[00:00:35] **David:** Stitch Fix was a Rails shop. I had done a lot of Rails and learned a lot of things that worked and didn&#x27;t work, at least in that situation.

And so I started writing them down and I was like, I should probably make this more than just a document that I keep, you know, privately on my computer. Uh, so that&#x27;s, you know, kind of, kind of where the genesis of that came from and just tried to, write everything down that I thought what worked, what didn&#x27;t work.

Uh, if you&#x27;re in a situation like me. Working on a product, with a medium sized, uh, team, then I think the lessons in there will be useful, at least some of them. Um, and I&#x27;ve been trying to keep it up over, over the years. I think the first version came out a couple years ago, so I&#x27;ve been trying to make sure it&#x27;s always up to date with the latest stuff and, and Rails and based on my experience and all that.

[00:01:20] **Jeremy:** So it&#x27;s interesting that you mention, medium sized team because, during the, the keynote, just a few moments ago, Matz the creator of Ruby was talking about how like, Oh, Rails is really suitable for this, this one person team, right? Small, small team. And, uh, he was like, you&#x27;re not Google. So like, don&#x27;t worry about, right.

Can you scale to that level? Yeah. Um, and, and I wonder like when you talk about medium size or medium scale, like what are, what are we talking?

[00:01:49] **David:** I think probably under 200 developers, I would say. because when I left Stitch Fix, it was closing in on that number of developers. And so it becomes, you know, hard to...

You can kind of know who everybody is, or at least the names sound familiar of everybody. But beyond that, it&#x27;s just, it&#x27;s just really hard. But a lot of it was like, I don&#x27;t have experience at like a thousand developer company. I have no idea what that&#x27;s like, but I definitely know that Rails can work for like...

200 ish people how you can make it work basically. yeah.

[00:02:21] **Jeremy:** The decision to use Rails, I&#x27;m assuming that was made before you joined?

[00:02:26] **David:** Yeah, the, um, the CTO of Stitch Fix, he had come in to clean up a mess made by contractors, as often happens. They had used Django, which is like the Python version of Rails.

And he, the CTO, he was more familiar with Rails. So the first two developers he hired, also familiar with Rails. There wasn&#x27;t a lot to maintain with the Django app, so they were like, let&#x27;s just start fresh, fresh with Rails. yeah, but it&#x27;s funny because a lot of the code in that Rails app was, like, transliterated from Python.

So you could, it would, it looked like the strangest Ruby code in the world because it was basically, there was no test. So they were like, let&#x27;s just write the Ruby version of this Python just so we know it works. but obviously that didn&#x27;t, didn&#x27;t last forever, so.

[00:03:07] **Jeremy:** So, so what&#x27;s an example of a, of a tell?

Where you&#x27;re looking at the code and you&#x27;re like, oh, this is clearly, it came from Python.

[00:03:15] **David:** You&#x27;d see like, very, very explicit, right? Like Python, there&#x27;s a lot of like single line things. very like, this sounds like a dig, but it&#x27;s very simple looking code. Like, like I don&#x27;t know Python, but I was able to change this Django app.

And I had to, I could look at it and you can figure out immediately how it works. Cause there&#x27;s. Not much to it. There&#x27;s nothing fancy. So, like, this, this Ruby code, there was nothing fancy. You&#x27;d be like, well, maybe they should have memoized that, or maybe they should have taken that into another class, or you could have done this with a hash or something like that.

So there was, like, none of that. It was just, like, really basic, plain code like you would see in any beginning programming language kind of thing. Which is at least nice. You can understand it. but you probably wouldn&#x27;t have written it that way at first in Ruby.


## Thoughts on Go

[00:04:05] **Jeremy:** Yeah, that&#x27;s, that&#x27;s interesting because, uh, people sometimes talk about the Go programming language and how it looks, I don&#x27;t know if simple is the right word, but it&#x27;s something where you look at the code and even if you don&#x27;t necessarily understand Go, it&#x27;s relatively straightforward.

Yeah. I wonder what your thoughts are on that being a strength versus that being, like,

[00:04:25] **David:** Yeah, so at Stitch Fix at one point we had a pro, we were moving off of Heroku and we were going to, basically build a deployment platform using ECS on AWS. And so the deployment platform was a Rails app and we built a command line tool using Ruby.

And it was fine, but it was a very complicated command line tool and it was very slow. And so one of the developers was like, I&#x27;m going to rewrite it in Go. I was like, ugh, you know, because I just was not a big fan. So he rewrote it in Go. It was a bazillion times faster. And then I was like, okay, I&#x27;m going to add, I&#x27;ll add a feature to it.

It was extremely easy. Like, it&#x27;s just like what you said. I looked at it, like, I don&#x27;t know anything about Go. I know what is happening here. I can copy and paste this and change things and make it work for what I want to do. And it did work. And it was, it was pretty easy. so there&#x27;s that, I mean, aesthetically it&#x27;s pretty ugly and it&#x27;s, I, I.

I can&#x27;t really defend that as a real reason to not use it, but it is kind of gross. I did do Go, I did a small project in Go after Stitch Fix, and there&#x27;s this vibe in Go about like, don&#x27;t create abstractions. I don&#x27;t know where I got that from, but every Go I look at, I&#x27;m like we should make an abstraction for this, but it&#x27;s just not the vibe.

They just don&#x27;t like doing that. They like it all written out. And I see the value because you can look at the code and know what it does and you don&#x27;t have to chase abstractions anywhere. But. I felt like I was copying and pasting a lot of, a lot of things. Um, so I don&#x27;t know. I mean, the, the team at Stitch Fix that did this like command line app in go, they&#x27;re the platform team.

And so their job isn&#x27;t to write like web apps all day, every day. There&#x27;s kind of in and out of all kinds of things. They have to try to figure out something that they don&#x27;t understand quickly to debug a problem. And so I can see the value of something like go if that&#x27;s your job, right? You want to go in and see what the issue is.

Figure it out and be done and you&#x27;re not going to necessarily develop deep expertise and whatever that thing is that you&#x27;re kind of jumping into. Day to day though, I don&#x27;t know. I think it would make me kind of sad. (laughs)

[00:06:18] **Jeremy:** So, so when you say it would make you kind of sad, I mean, what, what about it? Is it, I mean, you mentioned that there&#x27;s a lot of copy and pasting, so maybe there&#x27;s code duplication, but are there specific things where you&#x27;re like, oh, I just don&#x27;t?

[00:06:31] **David:** Yeah, so I had done a lot of Java in my past life and it felt very much like that. Where like, like the Go library for making an HTTP call for like, I want to call some web service. It&#x27;s got every feature you could ever want. Everything is tweakable. You can really, you can see why it&#x27;s designed that way.

To dial in some performance issue or solve some really esoteric thing. It&#x27;s there. But the problem is if you just want to get an JSON, it&#x27;s just like huge production. And I felt like that&#x27;s all I really want to do and it&#x27;s just not making it very easy. And it just felt very, very cumbersome. I think that having to declare types also is a little bit of a weird mindset because, I mean, I like to make types in Ruby, I like to make classes, but I also like to just use hashes and stuff to figure it out.

And then maybe I&#x27;ll make a class if I figure it out, but Go, you can&#x27;t. You have to have a class, you have to have a type, you have to think all that ahead of time, and it just, I&#x27;m not used to working that way, so it felt, I mean, I guess I could get used to it, but I just didn&#x27;t warm up to that sort of style of working, so it just felt like I was just kind of fighting with the vibe of the language, kind of.

Yeah,

[00:07:40] **Jeremy:** so it&#x27;s more of the vibe or the feel where you&#x27;re writing it and you&#x27;re like this seems a little too... Explicit. I feel like I have to be too verbose. It just doesn&#x27;t feel natural for me to write this.

[00:07:53] **David:** Right, it&#x27;s not optimized for what in my mind is the obvious case.

And maybe that&#x27;s not the obvious case for the people that write Go programs. But for me, like, I just want to like get this endpoint and get the JSON back as a map. Not any easier than any other case, right? Whereas like in Ruby, right? And you can, I think if you include net HTTP, you can just type get. And it will just return whatever that is.

Like, that&#x27;s amazing. It&#x27;s optimized for what I think is a very common use case. So it makes me feel really productive. It makes me feel pretty good. And if that doesn&#x27;t work out long term, I can always use something more complicated. But I&#x27;m not required to dig into the NetHttp library just to do what in my mind is something very simple.

[00:08:37] **Jeremy:** Yeah, I think that&#x27;s something I&#x27;ve noticed myself in working with Ruby. I mean, you have the standard library that&#x27;s very... Comprehensive and the API surface is such that, like you said there, when you&#x27;re trying to do common tasks, a lot of times they have a call you make and it kind of does the thing you expected or hoped for.

[00:08:56] **David:** Yeah, yeah. It&#x27;s kind of, I mean, it&#x27;s that whole optimized for programmer happiness thing. Like it does. That is the vibe of Ruby and it seems like that is still the way things are. And, you know, I, I suppose if I had a different mindset, I mean, because I work with developers who did not like using Ruby or Rails.

They loved using Go or Java. And I, I guess there&#x27;s probably some psychological analysis we could do about their background and history and mindset that makes that make sense. But, to me, I don&#x27;t know. It&#x27;s, it&#x27;s nice when it&#x27;s pleasant. And Ruby seems pleasant. (laughs)


## Choosing Technology

[00:09:27] **Jeremy:** as a... Software Architect, or as a CTO, when, when you&#x27;re choosing technology, what are some of the things you look at in terms of, you know?

[00:09:38] **David:** Yeah, I mean, I think, like, it&#x27;s a weird criteria, but I think what is something that the team is capable of executing with? Because, like, most, right, most programming languages all kind of do the same thing. Like, you can kind of get most stuff done in most common popular programming languages. So, it&#x27;s probably not...

It&#x27;s not true that if you pick the wrong language, you can&#x27;t build the app. Like, that&#x27;s probably not really the case. At least for like a web app or something. so it&#x27;s more like, what is the team that&#x27;s here to do it? What are they comfortable and capable of doing? I worked on a project with...

It was a mix of like junior engineers who knew JavaScript, and then some senior engineers from Google. And for whatever reason someone had chosen a Rails app and none of them were comfortable or really yet competent with doing Ruby on Rails and they just all hated it and like it didn&#x27;t work very well.

Um, and so even though, yes, Rails is a good choice for doing stuff for that team at that moment. Not a good choice. Right. So I think you have to go in and like, what, what are we going to be able to execute on so that when the business wants us to do something, we just do it. And we don&#x27;t complain and we don&#x27;t say, Oh, well we can&#x27;t because this technology that we chose, blah, blah, blah.

Like you don&#x27;t ever want to say that if possible. So I think that&#x27;s. That&#x27;s kind of the, the top thing. I think second would be how widely supported is it? Like you don&#x27;t want to be the cutting edge user that&#x27;s finding all the bugs in something really. Like you want to use something that&#x27;s stable. Postgres, MySQL, like those work, those are fine.

The bugs have been sorted out for most common use cases. Some super fancy edge database, I don&#x27;t know if I&#x27;d want to be doing, doing that you know?


## Choosing cloud services

[00:11:15] **Jeremy:** How do you feel about the cloud specific services and databases? Like are you comfortable saying like, oh, I&#x27;m going to use... Google Cloud, BigQuery. Yeah.

[00:11:27] **David:** That sort of thing. I think it would kind of fall under the same criteria that I was just, just saying like, so with AWS it&#x27;s interesting &#x27;cause when we moved from Heroku to AWS by EC2 RDS, their database thing, uh, S3, those have been around for years, probably those are gonna work, but they always introduce new things.

Like we, we use RabbitMQ and AWS came out with. Some, I forget what it was, it was a queuing service similar to Rabbit. We were like, Oh, maybe we should switch to that. But it was clear that they weren&#x27;t really ready to support it. So. Yeah, so we didn&#x27;t, we didn&#x27;t switch to that. So I, you gotta try to read the tea leaves of the provider to see are they committed to, to supporting this thing or is this there to get some enterprise client to move into the cloud.

And then the idea is to move off of that transitional thing into what they do support. And it&#x27;s hard to get a clear answer from them too. So it takes a little bit of research to figure out, Are they going to support this or not? Because that&#x27;s what you don&#x27;t want. To move everything into some very proprietary cloud system and have them sunset it and say, Oh yeah, now you&#x27;ve got to switch again.

Uh, that kind of sucks. So, it&#x27;s a little trickier.

[00:12:41] **Jeremy:** And what kind of questions or research do you do? Is it purely a function of this thing has existed for X number of years so I feel okay?

[00:12:52] **David:** I mean, it&#x27;s kind of similar to looking at like some gem you&#x27;re going to add to your project, right? So you&#x27;ll, you&#x27;ll look at how often does it change?

Is it being updated? Uh, what is the documentation? Does it look like someone really cared about the documentation? Does the documentation look updated? Are there issues with it that are being addressed or, or not? Um, so those are good signals. I think, talking to other practitioners too can be good. Like if you&#x27;ve got someone who&#x27;s experienced.

You can say, hey, do you know anybody back channeling through, like, everybody knows somebody that works at AWS, you can probably try to get something there. at Stitch Fix, we had an enterprise support contract, and so your account manager will sometimes give you good information if you ask. Again, it&#x27;s a, they&#x27;re not going to come out and say, don&#x27;t use this product that we have, but they might communicate that in a subtle way.

So you have to triangulate from all these sources to try to. to try to figure out what, what you want to do.

[00:13:50] **Jeremy:** Yeah, it kind of

makes me wish that there was a, a site like, maybe not quite like, can I use, right? Can I use, you can see like, oh, can I use this in my browser? Is there, uh, like an AWS or a Google Cloud?

Can I trust this? Can I trust this? Yeah. Is this, is this solid or not?

[00:14:04] **David:** Right, totally. It&#x27;s like, there&#x27;s that, that site where you, it has all the Apple products and it says whether or not you should buy it because one may or may not be coming out or they may be getting rid of it. Like, yeah, that would... For cloud services, that would be, that would be nice.

[00:14:16] **Jeremy:** Yeah, yeah. That&#x27;s like the Mac Buyer&#x27;s Guide. And then we, we need the, uh, the technology. Yeah. Maybe not buyers. Cloud Provider Buyer&#x27;s Guide, yeah. I guess we are buyers.

[00:14:25] **David:** Yeah, yeah, totally, totally.

[00:14:27] **Jeremy:** it&#x27;s interesting that you, you mentioned how you want to see that, okay, this thing is mature. I think it&#x27;s going to stick around because, I, interviewed, someone who worked on, I believe it was the CloudWatch team.

Okay. Daniel Vassalo, yeah. so he left AWS, uh, after I think about 10 years, and then he wrote a book called, uh, The Good Parts of AWS. Oh! And, if you read his book, most of the services he says to use are the ones that are, like, old. Yeah. He&#x27;s, he&#x27;s basically saying, like, S3, you know you&#x27;re good.

Yeah. Right? but then all these, if you look at the AWS webpage, they have who knows, I don&#x27;t know how many hundreds of services. Yeah. He&#x27;s, he&#x27;s kind of like I worked there and I would not use, you know, all these new services. &#x27;cause I myself, I don&#x27;t trust

[00:15:14] **David:** it yet. Right. And so, and they&#x27;re working there?

Yeah, they&#x27;re working there. Yeah. No. One of the VPs at Stitch Fix had worked on Google Cloud and so when we were doing this transition from Heroku, he was like, we are not using Google Cloud. I was like, really? He&#x27;s like AWS is far ahead of the game. Do not use Google Cloud. I was like, all right, I don&#x27;t need any more info.

You work there. You said don&#x27;t. I&#x27;m gonna believe you. So

[00:15:36] **Jeremy:** what, what was his did he have like a core point?

[00:15:39] **David:** Um, so he never really had anything bad to say about Google per se. Like I think he enjoyed his time there and I think he thought highly of who he worked with and what he worked on and that sort of thing.

But his, where he was coming from was like AWS was so far ahead. of Google on anything that we would use, he was like, there&#x27;s, there&#x27;s really no advantage to, to doing it. AWS is a known quantity, right? it&#x27;s probably still the case. It&#x27;s like, you know, you&#x27;ve heard the nobody ever got fired for using IBM or using Microsoft or whatever the thing is.

Like, I think that&#x27;s, that was kind of the vibe. And he was like, moving all of our infrastructure right before we&#x27;re going to go public. This is a serious business. We should just use something that we know will work. And he was like, I know this will work. I&#x27;m not confident about. Google, uh, for our use case.

So we shouldn&#x27;t, we shouldn&#x27;t risk it. So I was like, okay, I trust you because I didn&#x27;t know anything about any of that stuff at the time. I knew Heroku and that was it. So, yeah.

[00:16:34] **Jeremy:** I don&#x27;t know if it&#x27;s good or bad, but like you said, AWS seems to be the default choice. Yeah. And I mean, there&#x27;s people who use Azure.

I assume it&#x27;s mostly primarily Microsoft. Yeah. And then there&#x27;s Google Cloud. It&#x27;s not really clear why you would pick it, unless there was a specific service or something that only they had.

[00:16:55] **David:** Yeah, yeah. Or you&#x27;re invested in Google, you know, you want to keep everything there. I mean, I don&#x27;t know. I haven&#x27;t really been at that level to make that kind of decision, and I would probably choose AWS for the reasons discussed, but, yeah.


## Moving off Heroku

[00:17:10] **Jeremy:** And then, so at Stitch Fix, you said you moved off of Heroku

[00:17:16] **David:** yeah.

Yeah, so we were heavy into Heroku. I think that we were told that at one point we had the biggest Heroku Postgres database on their platform. Not a good place to be, right? You never want to be the biggest customer person, usually. but the problem we were facing was essentially we were going to go public.

And to do that, you&#x27;re under all the scrutiny. about many things, including the IT systems and the security around there. So, like, by default, a Postgres, a Heroku Postgres database is, like, on the internet. It&#x27;s only secured by the password. all their services are on the internet. So, not, not ideal. they were developing their private cloud service at that time.

And so that would have given us, in theory, on paper, it would have solved all of our problems. And we liked Heroku and we liked the developer experience. It was great. but...

Heroku private spaces, it was still early. There&#x27;s a lot of limitations that when they explained why those limitations, they were reasonable. And if we had. started from scratch on Heroku Private Spaces. It probably would have worked great, but we hadn&#x27;t.

So we just couldn&#x27;t make it work. So we were like, okay, we&#x27;re going to have to move to AWS so that everything can be basically off the internet. Like our public website needs to be on the internet and that&#x27;s kind of it. So we need to, so that&#x27;s basically was the, was the impetus for that. but it&#x27;s too bad because I love Heroku.

It was great. I mean, they were, they were a great partner. They were great. I think if Stitch Fix had started life a year later, Private Spaces. Now it&#x27;s, it&#x27;s, it&#x27;s way different than it was then. Cause it&#x27;s been, it&#x27;s a mature product now, so we could have easily done that, but you know, the timing didn&#x27;t work out, unfortunately.

[00:18:50] **Jeremy:** And that was a compliance thing to,

[00:18:53] **David:** Yeah. And compliance is weird cause they don&#x27;t tell you what to do, but they give you some parameters that you need to meet. And so one of them is like how you control access. So, so going public, the compliance is around the financial data and. Ensuring that the financial data is accurate. So a lot of the systems at Stichfix were storing the financial data.

We, you know, the warehouse management system was custom made. Uh, all the credit card processing was all done, like it was all in some databases that we had running in Heroku. And so those needed to be subject to stricter security than we could achieve with just a single password that we just had to remember to rotate when someone like left the team.

So that was, you know, the kind of, the kind of impetus for, for all of that.

[00:19:35] **Jeremy:** when you were using Heroku, Salesforce would have already owned it then. Did you, did you get any sense that you weren&#x27;t really sure about the future of the platform while you&#x27;re on it or,

[00:19:45] **David:** At that time, no, it seemed like they were still innovating. So like, Heroku has a Redis product now. They didn&#x27;t at the time we wish that they did. They told us they&#x27;re working on it, but it wasn&#x27;t ready. We didn&#x27;t like using the third parties. Kafka was not a thing. We very much were interested in that.

We would have totally used it if it was there. So they were still. Like doing bigger innovations then, then it seems like they are now. I don&#x27;t know. It&#x27;s weird. Like they&#x27;re still there. They still make money, I assume for Salesforce. So it doesn&#x27;t feel like they&#x27;re going away, but they&#x27;re not innovating at the pace that they were kind of back in the day.

[00:20:20] **Jeremy:** it used to feel like when somebody&#x27;s asking, I want to host a Rails app. Then you would say like, well, use Heroku because it&#x27;s basically the easiest to get started. It&#x27;s a known quantity and it&#x27;s, it&#x27;s expensive, but, it seemed for, for most people, it was worth it. and then now if I talk to people, it&#x27;s like.

Not what people suggest anymore.

[00:20:40] **David:** Yeah, because there&#x27;s, there&#x27;s actual competitors. It&#x27;s crazy to me that there was no competitors for years, and now there&#x27;s like, Render and Fly. io seem to be the two popular alternatives. Um, I doubt they&#x27;re any cheaper, honestly, but... You get a sense, right, that they&#x27;re still innovating, still building those platforms, and they can build with, you know, all of the knowledge of what has come before them, and do things differently that might, that might help.

So, I still use Heroku for personal things just because I know it, and I, you know, sometimes you don&#x27;t feel like learning a new thing when you just want to get something done, but, yeah, I, I don&#x27;t know if we were starting again, I don&#x27;t know, maybe I&#x27;d look into those things. They, they seem like they&#x27;re getting pretty mature and.

Heroku&#x27;s resting on its laurels, still.

[00:21:26] **Jeremy:** I guess I never quite the mindset, right? Where you You have a platform that&#x27;s doing really well and people really like it and you acquire it and then it just It seems like you would want to keep it rolling, right? (laughs)

[00:21:38] **David:** Yeah, it&#x27;s, it is wild, I mean, I guess... Why did you, what was Salesforce thinking they were going to get? Uh, who knows maybe the person at Salesforce that really wanted to purchase it isn&#x27;t there. And so no one at Salesforce cares about it. I mean, there&#x27;s all these weird company politics that like, who knows what&#x27;s going on and you could speculate.

all day. What&#x27;s interesting is like, there&#x27;s definitely some people in the Ruby community who work there and still are working there. And that&#x27;s like a little bit of a canary for me. I&#x27;m like, all right, well, if that person&#x27;s still working there, that person seems like they&#x27;re on the level and, and, and, and seems pretty good.

They&#x27;re still working there. It, it&#x27;s gotta be still a cool place to be or still doing something, something good. But, yeah, I don&#x27;t know. I would, I would love to know what was going on in all the Salesforce meetings about acquiring that, how to manage it. What are their plans for it? I would love to know that stuff.

[00:22:29] **Jeremy:** maybe you had some experience with this at Stitch Fix But I&#x27;ve heard with Heroku some of their support staff at least in the past they would, to some extent, actually help you troubleshoot, like, what&#x27;s going on with your app. Like, if your app is, like, using a whole bunch of memory, and you&#x27;re out of memory, um, they would actually kind of look into that, for you, which is interesting, because it&#x27;s like, that&#x27;s almost like a services thing than it is just a platform.

[00:22:50] **David:** Yeah. I mean, they, their support, you would get, you would get escalated to like an engineer sometimes, like who worked on that stuff and they would help figure out what the problem was. Like you got the sense that everybody there really wanted the platform to be good and that they were all sort of motivated to make sure that everybody.

You know, did well and used the platform. And they also were good at, like a thing that trips everybody up about Heroku is that your app restarts every day. And if you don&#x27;t know anything about anything, you might think that is stupid. Why, why would I want that? That&#x27;s annoying. And I definitely went through that and I complained to them a lot.

And I&#x27;m like, if you only could not restart. And they very patiently and politely explained to me why that it needed to do that, they weren&#x27;t going to remove that, and how to think about my app given that reality, right? Which is great because like, what company does that, right? From the engineers that are working on it, like No, nobody does that.

So, yeah, no, I haven&#x27;t escalated anything to support at Heroku in quite some time, so I don&#x27;t know if it&#x27;s still like that. I hope it is, but I&#x27;m not really, not really sure.


## Building a platform team

[00:23:55] **Jeremy:** Yeah, that, uh, that reminds me a little bit of, I think it&#x27;s Rackspace? There&#x27;s, there&#x27;s, like, another hosting provider that was pretty popular before, and they... Used to be famous for that type of support, where like your, your app&#x27;s having issues and somebody&#x27;s actually, uh, SSHing into your box and trying to figure out like, okay, what&#x27;s going on?

which if, if that&#x27;s happening, then I, I can totally see where the, the price is justified. But if the support is kind of like dropping off to where it&#x27;s just, they don&#x27;t do that kind of thing, then yeah, I can see why it&#x27;s not so much of a, yeah,

[00:24:27] **David:** We used to think of Heroku as like they were the platform team before we had our own platform team and they, they acted like it, which was great.

[00:24:35] **Jeremy:** Yeah, I don&#x27;t have, um, experience with, render, but I, I, I did, talk to someone from there, and it does seem like they&#x27;re, they&#x27;re trying to fill that role, um, so, yeah, hopefully, they and, and other companies, I guess like Vercel and things like that, um, they&#x27;re, they&#x27;re all trying to fill that space,

[00:24:55] **David:** Yeah, cause, cause building our own internal platform, I mean it was the right thing to do, but it&#x27;s, it&#x27;s a, you can&#x27;t just, you have to have a team on it, it&#x27;s complicated, getting all the stuff in AWS to work the way you want it to work, to have it be kind of like Heroku, like it&#x27;s not trivial. if I&#x27;m a one person company, I don&#x27;t want to be messing around with that particularly. I want to just have it, you know, push it up and have it go and I&#x27;m willing to pay for that. So it seems logical that there would be competitors in that space. I&#x27;m glad there are. Hopefully that&#x27;ll light a fire under, under everybody.

[00:25:26] **Jeremy:** so in your case, it sounds like you moved to having your own platform team and stuff like that, uh, partly because of the compliance thing where you&#x27;re like, we need our, we need to be isolated from the internet. We&#x27;re going to go to AWS. If you didn&#x27;t have that requirement, do you still think like that would have been the time to, to have your own platform team and manage that all yourself?

[00:25:46] **David:** I don&#x27;t know. We, we were thinking an issue that we were running into when we got bigger, um, was that, I mean, Heroku, it, It&#x27;s obviously not as flexible as AWS, but it is still very flexible. And so we had a lot of internal documentation about this is how you use Heroku to do X, Y, and Z. This is how you set up a Stitch Fix app for Heroku.

Like there was just the way that we wanted it to be used to sort of. Just make it all manageable. And so we were considering having a team spun up to sort of add some tooling around that to sort of make that a little bit easier for everybody. So I think there may have been something around there. I don&#x27;t know if it would have been called a platform team.

Maybe we call, we thought about calling it like developer happiness or because you got developer experience or something. We, we probably would have had something there, but. I do wonder how easy it would have been to fund that team with developers if we hadn&#x27;t had these sort of business constraints around there.

yeah, um, I don&#x27;t know. You get to a certain size, you need some kind of manageability and consistency no matter what you&#x27;re using underneath. So you&#x27;ve got to have, somebody has to own it to make sure that it&#x27;s, that it&#x27;s happening.

[00:26:50] **Jeremy:** So even at your, your architect level, you still think it would have been a challenge to, to. Come to the executive team and go like, I need funding to build this team.

[00:27:00] **David:** You know, certainly it&#x27;s a challenge because everybody, you know, right? Nobody wants to put developers in anything, right? There are, there are a commodity and I mean, that is kind of the job of like, you know, the staff engineer or the architect at a company is you don&#x27;t have, you don&#x27;t have the power to put anybody on anything you, you have the power to Schedule a meeting with a VP or the CTO and they will listen to you.

And that&#x27;s basically, you&#x27;ve got to use that power to convince them of what you want done. And they&#x27;re all reasonable people, but they&#x27;re balancing 20 other priorities. So it would, I would have had to, it would have been a harder case to make that, Hey, I want to take three engineers. And have them write tooling to make Heroku easier to use.

What? Heroku is not easy to use. Why aren&#x27;t, you know, so you really, I would, it would be a little bit more of a stretch to walk them through it. I think a case could be made, but, definitely would take some more, more convincing than, than what was needed in our case.

[00:27:53] **Jeremy:** Yeah. And I guess if you&#x27;re able to contrast that with, you were saying, Oh, I need three people to help me make Heroku easier. Your actual platform team on AWS, I imagine was much larger, right?

[00:28:03] **David:** Initially it was, there was, it was three people did the initial move over. And so by the time we went public, we&#x27;d been on this new system for, I don&#x27;t know, six to nine months. I can&#x27;t remember exactly. And so at that time the platform team was four or five people, and I, I mean, so percentage wise, right, the engineering team was maybe almost 200, 150, 200.

So percentage wise, maybe a little small, I don&#x27;t know. but it kind of gets back to the power of like the rails and the one person framework. Like everything we did was very much the same And so the Rails app that managed the deployment was very simple. The, the command line app, even the Go one with all of its verbosity was very, very simple.

so it was pretty easy for that small team to manage. but, Yeah, so it was sort of like for redundancy, we probably needed more than three or four people because you know, somebody goes out sick or takes a vacation. That&#x27;s a significant part of the team. But in terms of like just managing the complexity and building it and maintaining it, like it worked pretty well with, you know, four or five people.


## Where Rails fits in vs other technology

[00:29:09] **Jeremy:** So during the Keynote today, they were talking about how companies like GitHub and Shopify and so on, they&#x27;re, they&#x27;re using Rails and they&#x27;re, they&#x27;re successful and they&#x27;re fairly large. but I think the thing that was sort of unsaid was the fact that. These companies, while they use Rails, they use a lot of other, technology as well.

And, and, and kind of increasing amounts as well. So, I wonder from your perspective, either from your experience at StitchFix or maybe going forward, what is the role that, that Ruby and Rails plays? Like, where does it make sense for that to be used versus like, Okay, we need to go and build something in Java or, you know, or Go, that sort of thing?

[00:29:51] **David:** right. I mean, I think for like your standard database backed web app, it&#x27;s obviously great. especially if your sort of mindset bought into server side rendering, it&#x27;s going to be great at that. so like internal tools, like the customer service dashboard or... You know, something for like somebody who works at a company to use.

Like, it&#x27;s really great because you can go super fast. You&#x27;re not going to be under a lot of performance constraints. So you kind of don&#x27;t even have to think about it. Don&#x27;t even have to solve it. You can, but you don&#x27;t have to, where it wouldn&#x27;t work, I guess, you know, if you have really strict performance.

Requirements, you know, like a, a Go version of some API server is going to use like percentages of what, of what Rails would use. If that&#x27;s meaningful, if what you&#x27;re spending on memory or compute is, is meaningful, then, then yeah. That, that becomes worthy of consideration. I guess if you&#x27;re, you know, if you&#x27;re making a mobile app, you probably need to make a mobile app and use those platforms.

I mean, I guess you can wrap a Rails app sort of, but you&#x27;re still making, you still need to make a mobile app, that does something. yeah. And then, you know, interestingly, the data science part of Stitch Fix was not part of the engineering team. They were kind of a separate org. I think Ruby and Rails was probably the only thing they didn&#x27;t use over there.

Like all the ML stuff, everything is either Java or Scala or Python. They use all that stuff. And so, yeah, if you want to do AI and ML with Ruby, you, it&#x27;s, it&#x27;s hard cause there&#x27;s just not a lot there. You really probably should use Python. It&#x27;ll make your life easier. so yeah, those would be some of the considerations, I guess.

[00:31:31] **Jeremy:** Yeah, so I guess in the case of, ML, Python, certainly, just because of the, the ecosystem, for maybe making a command line application, maybe Go, um, Go or Rust, perhaps,

[00:31:44] **David:** Right. Cause you just get a single binary. Like the problem, I mean, I wrote this book on Ruby command line apps and the biggest problem is like, how do I get the Ruby VM to be anywhere so that it can then run my like awesome scripts? Like that&#x27;s kind of a huge pain. (laughs) So

[00:31:59] **Jeremy:** and then you said, like, if it&#x27;s Very performance sensitive, which I am kind of curious in, in your experience with the companies you&#x27;ve worked at, when you&#x27;re taking on a project like that, do you know up front where you&#x27;re like, Oh, the CPU and memory usage is going to be a problem, or is it&#x27;s like you build it and you&#x27;re like, Oh, this isn&#x27;t working.

So now I know.

[00:32:18] **David:** yeah, I mean, I, I don&#x27;t have a ton of great experience there at Stitch Fix. The biggest expense the company had was the inventory. So like the, the cost of AWS was just de minimis compared to all that. So nobody ever came and said, Hey, you&#x27;ve got to like really save costs on, on that stuff. Cause it just didn&#x27;t really matter.

at the, the mental health startup I was at, it was too early. But again, the labor costs were just far, far exceeded the amount of money I was spending on, on, um, you know, compute and infrastructure and stuff like that. So, Not knowing anything, I would probably just sort of wait and see if it&#x27;s a problem.

But I suppose you always take into account, like, what am I actually building? And like, what does this business have to scale to, to make it worthwhile? And therefore you can kind of do a little bit of planning ahead there. But, I dunno, I think it would kind of have to depend.

[00:33:07] **Jeremy:** There&#x27;s a sort of, I guess you could call it a meme, where people say like, Oh, it&#x27;s, it&#x27;s not, it&#x27;s not Rails that&#x27;s slow, it&#x27;s the, the database that&#x27;s slow. And, uh, I wonder, is that, is that accurate in your experience, or,

[00:33:20] **David:** I mean, most of the stuff that we had that was slow was the database, because like, it&#x27;s really easy to write a crappy query in Rails if you&#x27;re not, if you&#x27;re not careful, and then it&#x27;s really easy to design a database that doesn&#x27;t have any indexes if you&#x27;re not careful. Like, you, you kind of need to know that, But of course, those are easy to fix too, because you just add the index, especially if it&#x27;s before the database gets too big where we&#x27;re adding indexes is problematic. But, I think those are just easy performance mistakes to make. Uh, especially with Rails because you&#x27;re not, I mean, a lot of the Rails developers at Citrix did not know SQL at all.

I mean, they had to learn it eventually, but they didn&#x27;t know it at all. So they&#x27;re not even knowing that what they&#x27;re writing could possibly be problematic. It&#x27;s just, you&#x27;re writing it the Rails way and it just kind of works. And at a small scale, it does. And it doesn&#x27;t matter until, until one day it does.

[00:34:06] **Jeremy:** And then in, in the context of, let&#x27;s say, using ActiveRecord and instantiating the objects, or, uh, the time it takes to render templates, that kinds of things, to, at least in your experience, that wasn&#x27;t such of an issue.

[00:34:20] **David:** No, and it was always, I mean, whenever we looked at why something was slow, it was always the database and like, you know, you&#x27;re iterating over some active records and then, and then, you know, you&#x27;re going into there and you&#x27;re just following this object graph. I&#x27;ve got a lot of the, a lot of the software at Stitch Fix was like internal stuff and it was visualizing complicated data out of the database.

And so if you didn&#x27;t think about it, you would just start dereferencing and following those relationships and you have this just massive view and like the HTML is fine. It&#x27;s just that to render this div, you&#x27;re. Digging into some active record super deep. and so, you know, that was usually the, the, the problems that we would see and they&#x27;re usually easy enough to fix by making an index or.

Sometimes you do some caching or something like that. and that solved most of the, most of the issues

[00:35:09] **Jeremy:**


## The different ways people learn

[00:35:09] **Jeremy:** so you&#x27;re also the author of the book, Sustainable Web Development with Ruby on Rails. And when you talk to people about like how they learn things, a lot of them are going on YouTube, they&#x27;re going on, uh, you know, looking for blogs and things like that.

And so as an author, what do you think the role is of, of books now?

Yeah,

[00:35:29] **David:** I have thought about this a lot, because I, when I first got started, I&#x27;m pretty old, so books were all you had, really. Um, so they seem very normal and natural to me, but... does someone want to sit down and read a 400 page technical book? I don&#x27;t know. so Dave Thomas who runs Pragmatic Bookshelf, he was on a podcast and was asked the same question and basically his answer, which is my answer, is like a long form book is where you can really lay out your thinking, really clarify what you mean, really take the time to develop sometimes nuanced, examples or nuanced takes on something that are Pretty hard to do in a short form video or in a blog post.

Because the expectation is, you know, someone sends you an hour long YouTube video, you&#x27;re probably not going to watch that. Two minute YouTube video is sure, but you can&#x27;t, you can&#x27;t get into so much, kind of nuanced detail. And so I thought that was, was right. And that was kind of my motivation for writing.

I&#x27;ve got some thoughts. They&#x27;re too detailed. It&#x27;s, it&#x27;s too much set up for a blog post. There&#x27;s too much of a nuanced element to like, really get across. So I need to like, write more. And that means that someone&#x27;s going to have to read more to kind of get to it. But hopefully it&#x27;ll be, it&#x27;ll be valuable. one of the sessions that we&#x27;re doing later today is Ruby content creators, where it&#x27;s going to be me and Noel Rappin and Dave Thomas representing the old school dudes that write books and probably a bunch of other people that do, you know, podcasts videos. It&#x27;d be interesting to see, I really want to know how do people learn stuff?

Because if no one reads books to learn things, then there&#x27;s not a lot of point in doing it. But if there is value, then, you know. It should be good and should be accessible to people. So, that&#x27;s why I do it. But I definitely recognize maybe I&#x27;m too old and, uh, I&#x27;m not hip with the kids or, or whatever, whatever the case is.

I don&#x27;t know.

[00:37:20] **Jeremy:** it&#x27;s tricky because, I think it depends on where you are in the process of learning that thing. Because, let&#x27;s say, you know a fair amount about the technology already. And you look at a book, in a lot of cases it&#x27;s, it&#x27;s sort of like taking you from nothing to something. And so you&#x27;re like, well, maybe half of this isn&#x27;t relevant to me, but then if I don&#x27;t read it, then I&#x27;m probably missing a lot still.

And so you&#x27;re in this weird in be in between zone. Another thing is that a lot of times when people are trying to learn something, they have a specific problem. And, um, I guess with, with books, it&#x27;s, you kind of don&#x27;t know for sure if the thing you&#x27;re looking for is going to be in the book.

[00:38:13] **David:** I mean, so my, so my book, I would not say as a beginner, it&#x27;s not a book to learn how to do Rails. It&#x27;s like you already kind of know Rails and you want to like learn some comprehensive practices. That&#x27;s what my book is for. And so sometimes people will ask me, I don&#x27;t know Rails, should I get your book? And I&#x27;m like, no, you should not.

but then you have the opposite thing where like the agile web development with Rails is like the beginner version. And some people are like, Oh, it&#x27;s being updated for Rails 7. Should I get it? I&#x27;m like, probably not because How to go from zero to rails hasn&#x27;t changed a lot in years. There&#x27;s not that much that&#x27;s going to be new.

but, how do you know that, right? Hopefully the Table of Contents tells you. I mean, the first book I wrote with Pragmatic, they basically were like, The Table of Contents is the only thing the reader, potential reader is going to have to have any idea what&#x27;s in the book. So, You need to write the table of contents with that in mind, which may not be how you&#x27;d write the subsections of a book, but since you know that it&#x27;s going to serve these dual purposes of organizing the book, but also being promotional material that people can read, you&#x27;ve got to keep that in mind, because otherwise, how does anybody, like you said, how does anybody know what&#x27;s, what&#x27;s going to be in there?

And they&#x27;re not cheap, I mean, these books are 50 bucks sometimes, and That&#x27;s a lot of money for people in the U. S. People outside the U. S. That&#x27;s a ton of money. So you want to make sure that they know what they&#x27;re getting and don&#x27;t feel ripped off.

[00:39:33] **Jeremy:** Yeah, I think the other challenge is, at least what I&#x27;ve heard, is that... When people see a video course, for whatever reason, they, they set, like, a higher value to it. They go, like, oh, this video course is, 200 dollars and it&#x27;s, like, seems like a lot of money, but for some people it&#x27;s, like, okay, I can do that. But then if you say, like, oh, this, this book I&#x27;ve been researching for five years, uh, I want to sell it for a hundred bucks, people are going to be, like no. No way.,

[00:40:00] **David:** Yeah. Right. A hundred bucks for a book. There&#x27;s no way. That&#x27;s a, that&#x27;s a lot. Yeah. I mean, producing video, I&#x27;ve thought about doing video content, but it seems so labor intensive. Um, and it&#x27;s kind of like, It&#x27;s sort of like a performance. Like I was mentioning before we started that I used to play in bands and like, there&#x27;s a lot to go into making an even mediocre performance.

And so I feel like, you know, video content is the same way. So I get that it like, it does cost more to produce, but, are you getting more information out of it? I, that, I don&#x27;t know, like maybe not, but who knows? I mean, people learn things in different ways. So,

[00:40:35] **Jeremy:** It&#x27;s just like this perception thing, I think. And, uh, I&#x27;m not sure why that is. Um,

[00:40:40] **David:** Yeah, maybe it&#x27;s newer, right? Maybe books feel older so they&#x27;re easier to make and video seems newer. I mean, I don&#x27;t know. I would love to talk to engineers who are like... young out of college, a few years into their career to see what their perception of this stuff is. Cause I mean, there was no, I mean, like I said, I read books cause that&#x27;s all there was.

There was no, no videos. You, you go to a conference and you read a book and that was, that was all you had. so I get it. It seems a whole video. It&#x27;s fancier. It&#x27;s newer. yeah, I don&#x27;t know. I would love to hear a wide variety of takes on it to see what&#x27;s actually the, the future, you know?

[00:41:15] **Jeremy:** sure, yeah. I mean, I think it probably can&#x27;t just be one or the other, right? Like, I think there are... Benefits of each way. Like, if you have the book, you can read it at your own pace without having to, like, scroll through the video, and you can easily copy and paste the, the code segments,

[00:41:35] **David:** Search it. Go back and forth.

[00:41:36] **Jeremy:** yeah, search it.

So, I think there&#x27;s a place for it, but yeah, I think it would be very interesting, like you said, to, to see, like, how are people learning,

[00:41:45] **David:** Right. Right. Yeah. Well, it&#x27;s the same with blogs and podcasts. Like I, a lot of podcasters I think used to be bloggers and they realized that like they can get out what they need by doing a podcast. And it&#x27;s way easier because it&#x27;s more conversational. You don&#x27;t have to do a bunch of research. You don&#x27;t have to do a bunch of editing.

As long as you&#x27;re semi coherent, you can just have a conversation with somebody and sort of get at some sort of thing that you want to talk about or have an opinion about. And. So you, you, you see a lot more podcasts and a lot less blogs out there because of that. So it&#x27;s, that&#x27;s kind of like the creators I think are kind of driving that a little bit.

yeah. So I don&#x27;t know.

[00:42:22] **Jeremy:** Yeah, I mean, I can, I can say for myself, the thing about podcasts is that it&#x27;s something that I can listen to while I&#x27;m doing something else. And so you sort of passively can hopefully pick something up out of that conversation, but... Like, I think it&#x27;s maybe not so good at the details, right? Like, if you&#x27;re talking code, you can talk about it over voice, but

can you really visualize it?

Yeah, yeah, yeah. I think if you sit down and you try to implement something somebody talked about, you&#x27;re gonna be like, I don&#x27;t know what&#x27;s happening.

[00:42:51] **David:** Yeah.

[00:42:52] **Jeremy:** So, uh, so, so I think there&#x27;s like these, these different roles I think almost for so like maybe you know the podcast is for you to Maybe get some ideas or get some familiarity with a thing and then when you&#x27;re ready to go deeper You can go look at a blog post or read a book I think video kind of straddles those two where sometimes video is good if you want to just see, the general concept of a thing, and have somebody explain it to you, maybe do some visuals.

that&#x27;s really good. but then it can also be kind of detailed, where, especially like the people who stream their process, right, you can see them, Oh, let&#x27;s, let&#x27;s build this thing together. You can ask me questions, you can see how I think. I think that can be really powerful. at the same time, like you said, it can be hard to say, like, you know, I look at some of the streams and it&#x27;s like, oh, this is a three hour stream and like, well, I mean, I&#x27;m interested.

I&#x27;m interested, but yeah, it&#x27;s hard enough for me to sit through a, uh, a three hour movie,

[00:43:52] **David:** Well, then that, and that gets into like, I mean, we&#x27;re, you know, we&#x27;re at a conference and they, they&#x27;re doing something a little, like, there are conference talks at this conference, but there&#x27;s also like. sort of less defined activities that aren&#x27;t a conference talk. And I think that could be a reaction to some of this too.

It&#x27;s like I could watch a conference talk on, on video. How different is that going to be than being there in person? maybe it&#x27;s not that different. Maybe, maybe I don&#x27;t need to like travel across the country to go. Do something that I could see on video. So there&#x27;s gotta be something here that, that, that meets that need that I can&#x27;t meet any other way.

So it&#x27;s all these different, like, I would like to think that&#x27;s how it is, right? All this media all is a part to play and it&#x27;s all going to kind of continue and thrive and it&#x27;s not going to be like, Oh, remember books? Like maybe, but hopefully not. Hopefully it&#x27;s like, like what you&#x27;re saying. Like it&#x27;s all kind of serving different purposes that all kind of work together.

Yeah.

[00:44:43] **Jeremy:** I hope that&#x27;s the case, because, um, I don&#x27;t want to have to scroll through too many videos.

[00:44:48] **David:** Yeah. The video&#x27;s not for me.


## Large Language Models

[00:44:50] **Jeremy:** I, I like, I actually do find it helpful, like, like I said, for the high level thing, or just to see someone&#x27;s thought process, but it&#x27;s like, if you want to know a thing, and you have a short amount of time, maybe not the best, um, of course, now you have all the large language model stuff where you like, you feed the video in like, Hey, tell, tell, tell me, uh, what this video is about and give me the code snippets and all that stuff.

I don&#x27;t know how well it works, but it seems

[00:45:14] **David:** It&#x27;s gotta get better. Cause you go to a support site and they&#x27;re like, here&#x27;s how to fix your problem, and it&#x27;s a video. And I&#x27;m like, can you just tell me? But I&#x27;d never thought about asking the AI to just look at the video and tell me. So yeah, it&#x27;s not bad.

[00:45:25] **Jeremy:** I think, that&#x27;s probably where we&#x27;re going. So it&#x27;s, uh, it&#x27;s a little weird to think about, but,

[00:45:29] **David:** yeah, yeah. I was just updating, uh, you know, like I said, I try to keep the book updated when new versions of Rails come out, so I&#x27;m getting ready to update it for Rails 7.

1 and in Amazon&#x27;s, Kindle Direct Publishing as their sort of backend for where you, you know, publish like a Kindle book and stuff, and so they added a new question, was AI used in the production of this thing or not? And if you answer yes, they want you to say how much, And I don&#x27;t know what they&#x27;re gonna do with that exactly, but I thought it was pretty interesting, cause I would be very disappointed to pay 50 for a book that the AI wrote, right?

So it&#x27;s good that they&#x27;re asking that? Yeah.

[00:46:02] **Jeremy:** I think the problem Amazon is facing is where people wholesale have the AI write the book, and the person either doesn&#x27;t review it at all, or maybe looks at a little, a little bit. And, I mean, the, the large language model stuff is very impressive, but If you have it generate a technical book for you, it&#x27;s not going to be good.

[00:46:22] **David:** yeah. And I guess, cause cause like Amazon, I mean, think about like Amazon scale, like they&#x27;re not looking at the book at all. Like I, I can go click a button and have my book available and no person&#x27;s going to look at it. they might scan it or something maybe with looking for bad words. I don&#x27;t know, but there&#x27;s no curation process there.

So I could, yeah. I could see where they could have that, that kind of problem. And like you as the, as the buyer, you don&#x27;t necessarily, if you want to book on something really esoteric, there are a lot of topics I wish there was a book on that there isn&#x27;t. And as someone generally want to put it on Amazon, I could see a lot of people buying it, not realizing what they&#x27;re getting and feeling ripped off when it was not good.

[00:47:00] **Jeremy:** Yeah, I mean, I, I don&#x27;t know, if it&#x27;s an issue with the, the technical stuff. It probably is. But I, I know they&#x27;ve definitely had problems where, fiction, they have people just generating hundreds, thousands of books, submitting them all, just flooding it.

[00:47:13] **David:** Seeing what happens.

[00:47:14] **Jeremy:** And, um, I think that&#x27;s probably... That&#x27;s probably the main reason why they ask you, cause they want you to say like, uh,

yeah, you said it wasn&#x27;t.

And so now we can remove your book.

[00:47:24] **David:** right. Right. Yeah. Yeah.

[00:47:26] **Jeremy:** I mean, it&#x27;s, it&#x27;s not quite the same, but it&#x27;s similar to, I don&#x27;t know what Stack Overflow&#x27;s policy is now, but, when the large language model stuff started getting big, they had a lot of people answering the questions that were just. Pasting the question into the model

[00:47:41] **David:** Which because they got it from

[00:47:42] **Jeremy:** and then

[00:47:43] **David:** The Got model got it from Stack Overflow.

[00:47:45] **Jeremy:** and then pasting the answer into Stack Overflow and the person is not checking it.

Right. So it&#x27;s like, could be right, could not be right. Um, cause, cause to me, it&#x27;s like, if, if you generate it, if you generate the answer and the answer is right, and you checked it, I&#x27;m okay with that.

[00:48:00] **David:** Yeah. Yeah.

[00:48:01] **Jeremy:** but if you&#x27;re just like, I, I need some karma, so I&#x27;m gonna, I&#x27;m gonna answer these questions with, with this bot, I mean, then maybe

[00:48:08] **David:** I could have done that. You&#x27;re not adding anything.

Yeah, yeah.

[00:48:11] **Jeremy:** it&#x27;s gonna be a weird, weird world, I think.

[00:48:12] **David:** Yeah, no kidding. No kidding.

[00:48:15] **Jeremy:** that&#x27;s a, a good place to end it on, but is there anything else you want to mention,

[00:48:19] **David:** No, I think we covered it all just yeah, you could find me online. I&#x27;m Davetron5000 on Ruby. social Mastodon, I occasionally post on Twitter, but not that much anymore. So Mastodon&#x27;s a place to go.

[00:48:31] **Jeremy:** David, thank you so much

[00:48:32] **David:** All right. Well, thanks for having me.