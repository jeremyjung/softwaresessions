+++
title = "eBay Architecture"

description = "Randy Shoup describes how eBay's architecture evolved over the last few decades"

[extra]
episode_url = "https://media.transistor.fm/c2f9a0ac/e9741336.mp3"
+++

Randy Shoup is the VP of Engineering and Chief Architect at eBay. He was previously the VP of Engineering at WeWork and Stitch Fix, a Director of Engineering at Google Cloud where he worked on App Engine, and a Chief Engineer and Distinguished Architect at eBay in 2004.

This episode originally aired on Software Engineering Radio.

### Topics covered:

- eBay's origins as a single C++ class
- The five-year migration to Java services
- Sharing a database between the old and new systems
- Building a distributed tracing system
- Working with bare metal
- Why most companies should stick to cloud
- Why individual services should own their own data storage
- How scale has caused solutions to change
- Rejoining a former company
- The Accelerate Book
- Improving delivery time. 

### Related Links

- [@randyshoup](https://www.twitter.com/randyshoup)
- [OpenTelemetry](https://opentelemetry.io/)
- [LightStep](https://lightstep.com/)
- [Honeycomb](https://www.honeycomb.io/)
- [Accelerate Book](https://itrevolution.com/accelerate-book/)
- [The Memo](https://chrislaing.net/blog/the-memo/)
- [Value Stream Mapping](https://www.purdue.edu/leansixsigmaonline/blog/value-stream-mapping/)
- [The Epic Story of Dropbox’s Exodus from the Amazon Cloud Empire](https://www.wired.com/2016/03/epic-story-dropboxs-exodus-amazon-cloud-empire)


### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** Today, I'm talking to Randy Shoup, he's the VP of engineering and chief architect at eBay.

[00:00:05] **Jeremy:** He was previously the VP of engineering at WeWork and stitch fix, and he was also a chief engineer and distinguished architect at eBay back in 2004. Randy, welcome back to software engineering radio. This will be your fifth appearance on the show. I'm pretty sure that's a record.

[00:00:22] **Randy:** Thanks, Jeremy, I'm really excited to come back. I always enjoy listening to, and then also contributing to software engineering radio.

Back at, Qcon 2007, you spoke with Markus Volter he's he was the founder of SE radio. And you were talking about developing eBay's new search engine at the time.

[00:00:42] **Jeremy:** And kind of looking back, I wonder if you could talk a little bit about how eBay was structured back then, maybe organizationally, and then we can talk a little bit about the, the tech stack and that sort of thing.

[00:00:53] **Randy:** Oh, sure. Okay. Yeah. Um, so eBay started in 1995. I just want to like, you know, orient everybody. Same, same as the web. Same as Amazon, same as a bunch of stuff. So E-bay was actually almost 10 years old when I joined. That seemingly very old first time. Um, so yeah. What was ebay's tech stack like then? So E-bay current has gone through five generations of its infrastructure.

It was transitioning between the second and the third when I joined in 2004. Um, so the. Iteration was Pierre Omidyar, the founder three-day weekend three-day labor day weekend in 1995, playing around with this new cool thing called the web. He wasn't intending to build a business. He just was playing around with auctions and wanted to put up a webpage.

So he had a Perl backend and every item was a file and it lived on this little 486 tower or whatever you had at the time. Um, so that wasn't scalable and wasn't meant to be. The second generation of eBay's architecture was what we called V2 very, you know, creatively, uh, that was a C++ monolith. Um, an ISAPI DLL with essentially well at its worst, which grew to 3.4 million lines of code in that single DLL and basically in a single class, not just in a single, like repo or a single file, but in a single class.

So that was very unpleasant to work in. As you can imagine, um, eBay had about a thousand engineers at the time and they were, you know, as you can imagine, like really stepping on each other's toes and not being able to make much forward progress. So starting in, I want to call it 2002. So two years before I joined, um, they were migrating to the creatively named V3 and V3 architecture was Java, and.

you know, not microservices, but like we didn't even have that term, but it wasn't even that it was mini applications. So I'm actually going to take a step back. V2 was a monolith. So like all of eBay's code in that single DLL and like that was buying and selling and search and everything. And then we had two monster databases, a primary and a backup big Oracle machines on some hardware that was bigger, you know, bigger than refrigerators and that ran eBay for a bunch of years, before we changed the upper part of the stack, we, um, chopped up the, that single monolithic database into a bunch of, um, domain specific databases or entity specific databases, right?

So a set of databases around users, you know, sharded by the user ID could talk about all that. If you want, you know, items again, sharded by item ID transactions, sharded by transaction ID... I think when I joined, it was the several hundred instances of, uh, Oracle databases, um, you know, spread around, but still that monolithic front end.

And then in 2002, I wanna say we started migrating into that V3 that I was saying, okay. So that's, uh, that was a rewrite in Java, again, many applications. So you take the front end and instead of having it be in one big unit, it was this, uh, ER file, EAR, file, if run and people remember back to, you know, those stays in Java, um, you know, 220 different of those.

So like here is the, you know, one of them for the search pages, you know, so the, you know, one application be the search application and it would, you know, do all the search related stuff, the handful of pages around search, uh, ditto for, you know, the buying area, ditto for the, you know, checkout area, ditto for the selling area...

220 of those. Um, and that was again, domain, um, vertically sliced domains. And then the relationship between those V3, uh, applications and the databases was a many to many things. So like many applicants, many of those applications interact with items. So they would interact with those item databases. Many of them would interact with users.

And so they would interact with a user databases, et cetera, uh, happy to go into as much gory detail as you want about all that. But like, that's what, uh, but we were in the transition period. You know, when I, uh, between the V2 monolith to the V3 mini applications in, uh, 2004, I'm just going to pause there and like, let me know where you want to take it.

[00:05:01] **Jeremy:** Yeah. So you were saying that it was, um, it started as Perl, then it became a C++, and that's kind of interesting that you said it was all in one class, right? So it's wow. That's gotta be a gigantic 

[00:05:16] **Randy:** I mean, completely brutal. Yeah. 3.4 million lines of code. Yeah. We were hitting compiler limits on the number of methods per class.

[00:05:22] **Jeremy:** Oh my gosh.

[00:05:23] **Randy:** I'm, uh, uh, scared that I have that. I happen to know that at least at the time, uh, Microsoft allowed you 16 K uh, methods per class, and we were hitting that limit.

So, uh, not great.

[00:05:36] **Jeremy:** So it's just kind of interesting to think about how do you walk through that code, right? You have, I guess you just have this giant file.

[00:05:45] **Randy:** Yeah. I mean, there were, you know, different methods. Um, but yeah, it was a big man. I mean, it was a monolith, it was, uh, you know, it was a spaghetti mess. Um, and you know, as you can imagine, Amazon went through a really similar thing by the way. So this wasn't soup. I mean, it was bad, but like we weren't the only people that were making that, making that a mistake.

Um, and just like Amazon, where they were, uh, they did like one update a quarter (laughs) , you know, at that period, like 2000, uh, we were doing something really similar, like very, very slow. Um, you know, updates and, uh, when we moved to V3, you know, the idea was to get to do changes much faster. And we were very proud of ourselves starting in 2004 that we, uh, upgraded the whole site every two weeks.

And we didn't have to do the whole site, but like each of those individual applications that I was mentioning, right. Those 220 applications, each of those would roll out on this biweekly cadence. Um, and they had interdependencies. And so we rolled them out in this dependency order in any way, lots of, lots of complexity associated with that.

Um, yeah, there you go.

[00:06:51] **Jeremy:** the V3 that, that was written in Java, I'm assuming this was a, as a complete rewrite. You, you didn't use the C++ code at all.

[00:07:00] **Randy:** Yeah. And, uh, it was, um, we migrated, uh, page by page. So, uh, you know, in the transition period, which lasted probably five years, um, there were pages, you know, in the beginning, all pages were served by V2. In the end, all pages are served by V3 and, you know, over time you iterate and you like rewrite in parallel, you know, rewrite and maintain in parallel the V3 version of XYZ page and the V2 version of XYZ page.

Um, and then when you're ready, you start to test out at low percentages of traffic, you know, what would, what does V3 look like? Is it correct? And when it isn't do you go and fix it, but then ultimately you migrate the traffic over, um, to fully take, get fully be in the V3 world, and then you, you know, remove or comment out or whatever.

The, the code that supported that in the V2 monolith.

[00:07:54] **Jeremy:** And then you had mentioned using Oracle databases. Did you have a set for V2 and a separate V3 and you were kind of trying to keep them in sync?

[00:08:02] **Randy:** Oh, great question. Thank you for asking that question. No, uh, no. We had the databases. Um, so again, as I mentioned, we had pre-demonolith that's my that's a technical term, uh, pre broken up the databases starting in, let's call it 2000. Uh, actually I'm almost certain that's 2000. Cause we had a major site outage in 1999, which everybody still remembers who was there at the time.

Uh wasn't me or I wasn't there at the time. Uh, but you know, you can look it up. Uh, anyway, so yeah, starting in 2000, we broke up that monolithic database into what I was telling you before those entity aligned databases. Again, one set for items, one set for users, one set for transactions, you know, dot dot, dot, um, and that division of those databases was shared.

You know, those databases were shared between. The three using those things and then V sorry, V2 using those things and V3 using those things. Um, and then, you know, so we've completely decoupled the rewrite of the database, you know, kind of data storage layer from the rewrite of the application layer, if that makes sense.

[00:09:09] **Jeremy:** Yeah. So, so you had V2 that was connecting to these individual Oracle databases. You said like they were for different types of entities, like maybe for items and users and things like that. but it was a shared database situation where V2 was connected to the same database as V3. Is that right?

[00:09:28] **Randy:** Correct and also in V3, even when done. Different V3 applications, were also connecting to the same database, again, like anybody who used user, anybody who used the user entity, which is a lot we're connecting to the user suite of databases and anybody who used the item entity, which again is a lot, um, you were connecting to the item databases, et cetera.

So yeah, it was this many to many that's, I'm trying to say many to many relationship between applications in the V3 world and databases.

[00:10:00] **Jeremy:** Okay. Yeah, I think I, I got it because

[00:10:03] **Randy:** It's easier with a diagram.

[00:10:04] **Jeremy:** yeah. W 'cause when you, when you think about services now, um, you think of services having dependencies on other services. Whereas in this case you would have multiple services that rather than talking to a different service, they would all just talk to the same database.

They all needed users. So they all needed to connect to the user's database.

[00:10:24] **Randy:** Right exactly. And so, uh, I don't want to jump ahead in this conversation, but like the problems that everybody has, everybody who's feeling uncomfortable at the moment. You're right. To feel uncomfortable because that wasn't unpleasant situation and microservices, or more generally the idea that individual services would own their own data.

And only in the only are interactions to the service would be through the service interface and not like behind the services back to the, to the data storage layer. Um, that's better. And Amazon discovered that, you know, uh, lots of people discovered that around that same, around that same early two thousands period.

And so yeah, we had that situation at eBay at the time. Uh, it was better than it was before. Right, right. Better than a monolithic database and a monolithic application layer, but it definitely also had issues. Uh, as you can imagine,

[00:11:14] **Jeremy:** you know, thinking about back to that time where you were saying it's better than a monolith, um, what were sort of the trade-offs of, you know, you have a monolith connecting to all these databases versus you having all these applications, connecting to all these databases, like what were the things that you gained and what did you lose if that made sense?

[00:11:36] **Randy:** Hmm. Yeah. Well, I mean, why we did it in the first place is develop is like isolation between development teams right? So we were looking for developer productivity or the phrase we used to use was feature velocity, you know, so how quickly would we be able to move? And to the extent that we could move independently, you know, the search team could move independently from the buying team, which could move independently from the selling team, et cetera.

Um, that was what we were gaining. Um, what were we losing? Uh, you know, when you're in a monolith situation, If there's an issue, you know, where it is, it's in the monolith. You might not know where in the monolith. Um, but like there's only one place that could be. And so an issue that one has, uh, when you break things up into smaller units, uh, especially when they have this, you know, shared, shared mutable state, essentially in the form of these databases, like who changed that column?

What, you know, what's the deal. Uh, actually we did have a solution for that or something that really helped us, which was, um, now 20, more than 20 years ago, we had something that we would now call distributed tracing where, uh, actually I talked about this way back in the 2007 thing, cause it was pretty cool, uh, at the time, uh, You know, just like the spans one would create using a modern distributed tracing, you know, open telemetry or, you know, any of the disruptive tracing vendors.

Um, just like you would do that. We, we didn't use the term span, but that same idea where, um, we could, and the goal was the same to like debug stuff. So, uh, every time we were about to make a database call, we would say, Hey, I'm about to make this data, you know, we would log we about to make this database call and then it would happen.

And then we would log whether it was successful or not successful. We could see how long it took, et cetera. Um, and so we built our own, you know, monitoring system, which, which we called central application logging or CAL, uh, totally proprietary to eBay. I'm happy to talk about whatever gory details you want to know about that, but it was pretty cool certainly way back in 2000.

It was, and that was our mitigation against the thing I'm telling you, which is, you know, when something, when not. Something is weird in the database. We can kind of back up and figure out where it might've happened, or things are slow. What's, you know, what's the deal. And, uh, you know, cause sometimes the database is slow for reasons.

Um, and what, which, what thing is, you know, from an application perspective, I'm talking to 20 different databases, but things are slow. Like what is it? And, um, CAL helped us to, to figure out both elements of that, right? Like what applications are talking to, what databases and what backend services and like debug and diagnose from that perspective.

And then for a given application, what, you know, databases in backend services are you talking to? And, um, debug that. And then we have the whole, and then we, um, we, we had monitors on those things and we would notice when databases would, where be a lot of errors or where, when database is starting in slower than they used to be.

Um, and then. We implemented what people would now call circuit breakers, where we would notice that, oh, you know, everybody who's trying to talk to database 1, 2, 3, 4 is seeing it slow down. I guess 1, 2, 3, 4 is unhappy. So now flip everybody to say, don't talk to 1, 2, 3, 4, and like, just that kind of stuff.

You're not going to be able to serve. Uh, but whatever, that's better than stopping everything. So I hope that makes sense. Like, you know, so all these, all these like modern resilience techniques, um, we always had, we had our own proprietary names for them, but you know, we, we implemented a lot of them way back when,

[00:15:22] **Jeremy:** Yeah. And, and I guess just to contextualize it for the audience, I mean, this was back in 2004. Oh it back in 2000.

[00:15:32] **Randy:** Again, because we had this, sorry to interrupt you because we have, the problem is that we were just talking about where application many applications are talking to many services and databases and we didn't know what was going on. And so we needed some visibility into what was going on.

Sorry, go ahead.

[00:15:48] **Jeremy:** yeah. Okay. So all the way back in 2000, there's a lot less, Services out there, like nowadays you think about so many software as a service products. if you were building the same thing today, what are some of the services that people today would just go and say like, oh, I'll just, I'll just pay for this and have this company handle it for me. You know, that wasn't available, then

[00:16:10] **Randy:** sure. Well, there. No, essentially, no. Well, there was no cloud cloud didn't happen until 2006. Um, and there were a few software as a service vendors like Salesforce existed at the time, but they weren't usable in the way you're thinking of where I could give you money and you would operate a technical or technological software service on my behalf.

Do you know what I mean? So we didn't have any of the monitoring vendors. We didn't have any of the stuff today. So yeah. So what would we do, you know, to solve that specific problem today? Uh, I would, as we do today, I would, uh, instrument everything with open telemetry because that's generic. Thank you, Ben Siegelman and LightStep for starting that whole open sourcing process, uh, of that thing and, and, um, getting all the vendors to, you know, respect it.

Um, and then I would shoot, you know, for my backend, I would choose one of the very many wonderful, uh, you know, uh, distributed tracing vendors of which there are so many, I can't remember, but like LightStep is one honeycomb... you know, there were a bunch of, uh, you know, backend, um, distributed tracing vendors in particular, you know, for that.

Uh, what else do you have today? I mean, we could go on for hours on this one, but like, we didn't have distributed logging or we didn't have like logging vendors, you know? So there was no, uh, there was no Splunk, there was no, um, you know, any, any of those, uh, any of the many, uh, distributed log, uh, or centralized logging vendor, uh, vendors.

So we didn't have any of those things. We didn't. like caveman, you know, we rent, we, uh, you know, had our own data. We built our own data centers. We racked our own servers. We installed all the OSS in them, you know, uh, by the way, we still do all that because it's way cheaper for us at our scale to do that.

But happy to talk about that too. Uh, anyway, but yeah, no, the people who live in, I don't know if this is where you want to go in 2022, the software developer has this massive menu of options. You know, if you only have a credit card, uh, and it doesn't usually cost that much, you can get a lot of stuff done from the cloud vendors, from the software service vendors, et cetera, et cetera.

And none of that existed in 2000.

[00:18:31] **Jeremy:** it's really interesting to think about how different, I guess the development world is now. Like, cause you mentioned how cloud wasn't even really a thing until 2006, all these, these vendors that people take for granted. Um, none of them existed. And so it just, uh, it must've been a very, very different time.

[00:18:52] **Randy:** Well, we didn't know. It was every, every year is better than the previous year, you know, in software every year. You know? So at that time we were really excited that we had all the tools and capabilities that, that we did have. Uh, and also, you know, you look back from, you know, 20 years in the future and, uh, you know, it looks caveman, you know, from that perspective.

But, uh, it was, you know, all those things were cutting edge at the time. What happened really was the big companies rolled their own, right. Everybody, you know, everybody built their own data centers, rack their own servers. Um, so at least at scale and the best you could hope for the most you could pay anybody else to do is rack your servers for you.

You know what I mean? Like there were external people, you know, and they still exist. A lot of them, you know, the Rackspaces you know Equinixes, et cetera of the world. Like they would. Have a co-location facility. Uh, and you, you know, you ask them please, you know, I'd like to buy the, these specific machines and please rack these specific machines for me and connect them up on the network in this particular way.

Um, that was the thing you could pay for. Um, but you pretty much couldn't pay them to put software on there for you. That was your job. Um, and then operating. It was also your job, if that makes sense.

[00:20:06] **Jeremy:** and then back then, would that be where. Employees would actually have to go to the data center and then, you know, put in their, their windows CD or their Linux CD and, you know, actually do everything right there.

[00:20:18] **Randy:** Yeah. 100%. Yeah. In fact, um, again, anybody who operates data centers, I mean, there's more automation, but the conceptually, when we run three data centers ourselves at eBay right now, um, and all of our, all of our software runs on them. So like we have physical, we have those physical data centers. We have employees that, uh, physically work in those things, physical.

Rack and stack the servers again, we're smarter about it now. Like we buy a whole rack, we roll the whole rack in and cable it, you know, with one big chunk, uh, sound, uh, as distinct from, you know, individual wiring and the networks are different and better. So there's a lot less like individual stuff, but you know, at the end of the day, but yeah, everybody in quotes, everybody at that time was doing that or paying somebody to do exactly that.

Right. Yeah.

[00:21:05] **Jeremy:** Yeah. And it's, it's interesting too, that you mentioned that it's still being done by eBay. You said you have three, three data centers. because it seems like now maybe it's just assumed that someone's using a cloud service or using AWS or whatnot. And so, oh, go ahead.

[00:21:23] **Randy:** I was just going to say, well, I'm just going to riff off what you said, how the world has changed. I mean, so much, right? So. Uh, it's fine. You didn't need to say my whole LinkedIn, but like I used to work on Google cloud. So I've been, uh, I've been a cloud vendor, uh, at a bunch of previous companies I've been a cloud consumer, uh, at stitch fix and we work in other places.

Um, so I'm fully aware, you know, fully, fully, personally aware of, of all that stuff. But yeah, I mean, there's this, um, you know, eBay is in the, uh, eBay is at the size where it is actually. Cost-effective very, cost-effective, uh, can't tell you more than that, uh, for us to operate our own, um, uh, our own infrastructure, right?

So, you know, you know, one would expect if Google didn't operate their own infrastructure, nobody would expect Google to use somebody else's right. Like that, that doesn't make any economic sense. Um, and, uh, you know, Facebook is in the same category. Uh, for a while, Twitter and PayPal have been in that category.

So there's like this clap, you know, there are the known hyperscalers, right. You know, the, the Google, Amazon, uh, Microsoft that are like cloud vendors in addition to consumers internally have their own, their own clouds. Um, and then there's a whole class of other, um, places that operate their own internal clouds in quotes.

Uh, but don't offer them externally and again, uh, Facebook or Meta, uh, you know, is one example. eBay's another, you know, there's a, I'm making this up. Dropbox actually famously started in the cloud and then found it was much cheaper for them to operate their own infrastructure again, for the particular workloads that they had.

Um, so yeah, there's probably, I'm making this up. Let's call it two dozen around the world of these, I'm making this term up many hyperscalers, right? Like self hyperscalers or something like that. And eBay's in that category.

[00:23:11] **Jeremy:** I know this is kind of a, you know, a big what if, but you were saying how once you reach a certain scale, that's when it makes sense to move into your own data center. And, uh, I'm wondering if, if E-bay, had started more recently, like, let's say in the last, you know, 10 years, I wonder if it would've made sense for it to start on a public cloud and then move to, um, you know, its own infrastructure after it got bigger, or if you know, it really did make sense to just start with your own infrastructure from the start.

[00:23:44] **Randy:** Oh, I'm so glad you asked that. Um, the, the answer is obvious, but like, I'm so glad you asked that because I love to make this point. No one should ever, ever start by building your own servers and your own (laughs) cloud. Like, No, there's be, uh, you should be so lucky (laughs) after years and years and years that you outgrow the cloud vendors.

Right. Um, it happens, but it doesn't happen that often, you know, it happens so rarely that people write articles about it when it happens. Do you know what I mean? Like Dropbox is a good example. So yes, 100% anytime. Where are we? 2022. Any time in, more than the last 10 years? Um, yeah, let's call it. Let's call it 2010, 2012.

Right. Um, when cloud had proved itself over and you know, many times over, um, anybody who starts since that time should absolutely start in the public cloud. There's no argument about it. Uh, and again, one should be so lucky that over time, you're seeing successive zeros added to your cloud bill, and it becomes so many zeros that it makes sense to shift your focus toward building and operating your own data centers.

That's it. I haven't been part of that transition. I've been the other way, you know, at other places where, you know, I've migrated from owned data centers and colos into, into public cloud. Um, and that's the, that's the more common migration. And again, there are, there are a handful, maybe not even a handful of, uh, companies that have migrated away, but when they do, they've done all the math, right.

I mean, uh, Dropbox has done some great, uh, talks and articles about, about their transition and boy, the math makes sense for them. So, yeah.

[00:25:30] **Jeremy:** Yeah. And it also seems like maybe it's for certain types of businesses where moving off of public cloud. Makes sense. Like you mentioned Dropbox where so much of their business is probably centered around storage or centered around, you know, bandwidth and, you know, there's probably certain workloads that it's like need to leave public cloud earlier.

[00:25:51] **Randy:** Um, yeah, I think that's fair. Um, I think that, I think that's a, I think that's an insightful comment. Again, it's all about the economics at some point, you know, it's a big investment to, uh, uh, and it takes years to develop the intern, forget the money that you're paying people, but like just to develop the internal capabilities.

So they're very specialized skill sets around building an operating data centers. So like it's a big deal. Um, and, uh, yeah. So are there particular classes of workloads where you would for the same dollar figure or whatever, uh, migrate earlier or later? I'm sure that's probably true. And again, what can absolutely imagine?

Well, when they say Dropbox in this example, um, yeah, it's because like they, they need to go direct to the storage. And then, I mean, like, they want to remove every middle person, you know, from the flow of the bytes that are coming into the storage media. Um, and it makes perfect sense for, for them. And when I understood what they were doing, which was a number of years ago, they were hybrid, right. So they had, they had completely, you know, they kept the top, you know, external layer, uh, in public cloud. And then the, the storage layer was all custom. I don't know what they do today, but people could check.

[00:27:07] **Jeremy:** And I'm kind of coming back to your, your first time at eBay. is there anything you felt that you would've done differently with the knowledge you have now?

but with the technology that existed, then.

[00:27:25] **Randy:** Gosh, that's the 20, 20 hindsight. Um, the one that comes to mind is the one we touched on a little bit, but I'll say it more starkly, the. If I could, if I could go back in time 20 years and say, Hey, we're about to do this V3 transition at eBay. I would not. I would have had us move directly to what we would now call microservices in the sense that individual services own their own data storage and are only interacted with through the public interface.

Um, there's a famous Amazon memo around that same time. So Amazon did the transition from a monolith into what we would now call microservices over about a four or five-year period, 2000 to 2005. And there was a famous Jeff Bezos memo from the early part of that, where, you know, seven, you know, requirements I can't remember them, but you know, essentially it was, you may, you may, you may never, you may never talk to anybody else's database. You may only interact with other services through their public interfaces. I don't care what those public interfaces are, so they didn't standardize around. You know, CORBA or JSON or GRPC, which didn't exist at the time, you know, like they didn't standardize around any, any particular, uh, interaction mechanism, but you did need to again, have this kind of microservice capability, that's modern terminology, um, uh, where, you know, the only services own their own data and nobody can talk in the back door.

So that is the one architectural thing that I wish, you know, with 2020 hindsight, uh, that I would bring back in my time travel to 20 years ago, because that would help. That does help a lot. And to be fair, Amazon, um, Amazon was, um, pioneering in that approach and a lot of people internally and externally from Amazon, I'm told, didn't think it would work, uh, and it, and it did famously.

So that's, that's the thing I would do.

[00:29:30] **Jeremy:** Yeah. I'm glad you brought that up because, when you had mentioned that, I think you said there were 220 applications or something like that at certain scales, people might think like, oh, that sounds like microservices to me. But when you, you mentioned that microservice to you means it having its own data store.

I think that's a good distinction.

[00:29:52] **Randy:** Yeah. So, um, I talk a lot about microservices that have for, for a decade or so. Yeah. I mean, several of the distinguishing characteristics are the micro in microservices is size and scope of the interface, right? So you can have a service oriented architecture with one big service, um, or some very small number of very large services.

But the micro in microservice means this thing does, maybe it doesn't have one operation, but it doesn't have a thousand. The several or the handful or several handfuls of operations are all about this one particular thing. So that's the one part of it. And then the other part of it that is critical to the success of that is owning the, owning your own data storage.

Um, so each service, you know, again, uh, it's hard to do this with a diagram, but like imagine, imagine the bubble of the service surrounding the data storage, right? So like people, anybody from the outside, whether they're interacting synchronously, asynchronously, messaging, synchronous, whatever HTTP doesn't matter are only interacting to the bubble and never getting inside where the, uh, where the data is I hope that makes sense.

[00:31:04] **Jeremy:** Yeah. I mean, I mean, it's a kind of in direct contrast to before you're talking about how you had all these databases that all of these services shared. So it was probably hard to kind of keep track of, um, who had modified data. Um, you know, one service could modify it, then another service control to get data out and it's been changed, but it didn't change it.

So it could be kind of hard to track what's going on.

[00:31:28] **Randy:** Yeah, exactly. Inner integration at the database level is something that people have been doing since probably the 1980s. Um, and so again, I, you know, in retrospect it looks like caveman approach. Uh, it was pretty advanced at the time, actually, even the idea of sharding of, you know, Hey, there are users and the users live in databases, but they don't all live in the same one.

Uh, they live in 10 different databases or 20 different databases. And then there's this layer that. For this particular user, it figures out which of the 20 databases it's in and finds it and gets it back. And, um, you know, that was all pretty advanced. And by the way, that's all those capabilities still exist.

They're just hidden from everybody behind, you know, nice, simple, uh, software as a service, uh, interfaces anyway, but that takes nothing away from your excellent point, which is, yeah. It's, you know, when you're, again, when there's many to many to relations, when there is this many to many relationship between, um, uh, applications and databases, uh, and there's shared mutable state in those databases that when is shared, like that's bad, you know, it's not bad to have state.

It's not bad to have mutable state it's bad to have shared beautiful state.

[00:32:41] **Jeremy:** Yeah. And I think anybody who's kind of interested in learning more about the, you had talked about sharding and things like that. If they go back and listen to your, your first appearance on software engineering radio, um, yeah. It kind of struck me how you were talking about sharding and how it was something that was kind of unique or unusual.

Whereas today it feels like it's very, I don't know, if quaint is the right word, but it's like, um, it's something that, that people kind of are accustomed to now.

[00:33:09] **Randy:** Yeah. Yeah. Um, it's obvious. Um, it seems obvious in retrospect. Yeah. You know, at the time, and by the way, he didn't invent charting. As I said, in 2007, you know, Google and Yahoo and, uh, Amazon, and, you know, it was the obvious, it took a while to reach it, but it's one of those things where once, once people have the, you know, brainwave to see, oh, you know what, we don't actually have to stop store this in one, uh, database.

We can, we can chop that database up into, you know, into chunks. And that, that looks similar to that herself similar. Um, yeah, that was, uh, that was, uh, that was reinvented by lots of, uh, Lots of the big companies at the same time again, because everybody was solving that same problem at the same time. Um, but yeah, when you look back and you, I mean, like, and honestly, like everything that I said there, it's still like this, all the techniques about how you shard things.

And there's lots of, you know, it's not interesting anymore because the problems have been solved, but all those solutions are still the solutions, if that makes any sense, but you know,

[00:34:09] **Jeremy:** Yeah, for sure. I mean, I think anybody who goes back and listens to it. Yeah. Like you said, it's, it's, it's very interesting because it's. it all still applies and it's like, I think the, the solutions that are kind of interesting to me are ones where it's, it's things that could have been implemented long ago, but we just later on realized like, this is how we could do it.

[00:34:31] **Randy:** Well part of it is, as we grow as an industry, we just, we discover new problems. You know, we, we get to the point where, you know, sharding over databases has only a problem when one database doesn't work. You know, when it, when you're the load that you put on that database is too big, or you want the availability of, you know, multiple.

Um, and so that's not a, that's not a day one problem, right? That's a day two or day 2000 and kind of problem. Right. Um, and so a lot of these things, yeah, well, you know, it's software. So like we could have done, we could have done any of these things in older languages and older operating systems and with older technology.

But for the most part, we didn't have those problems or we didn't have them at sufficiently enough. People didn't have the problem that we, you know, um, for us to have solved it as an industry, if that makes any sense.

[00:35:30] **Jeremy:** yeah, no, that's a good point because you think about when Amazon first started and it was just a bookstore, right. And the number of people using the site where, uh, who knows it was, it might've been tens a day or hundreds a day. I don't, I don't know. And, and so, like you said, the problems that Amazon has now in terms of scale are just like, it's a completely different world than when they started.

[00:35:52] **Randy:** Yeah. I mean, probably I'm making it up, but I don't think that's too off to say that it's a billion times more, their problems are a billion fold. You know, what they, what they were

[00:36:05] **Jeremy:** the next thing I'd like to talk about is you came back to eBay I think about has it been about two years ago.

[00:36:14] **Randy:** Two years yeah.

[00:36:15] **Jeremy:** Yeah. And, and so, so tell me about the experience of coming back to an organization that you had been at, you know, 10 years prior or however long it was like, how is your onboarding different when it's somewhere you've been before?

[00:36:31] **Randy:** Yeah. Sure. So, um, like, like you said, I worked at eBay from 2004 to 2011. Um, and I worked in a different role than I have today. I've worked mostly on eBay search engine. Um, and then, uh, I left to co-found a startup, which was in the 99%. So the one, you know, like didn't really do much. Uh, I joined, I worked at Google in the early days of Google cloud, as I mentioned on Google app engine and had a bunch of other roles including more recently, like you said, stitch fix and we work, um, leading those engineering teams.

And, um, so yeah, coming back to eBay as chief architect and, and, you know, leading. Developer platform, essentially a part of eBay. Um, yeah. What was the onboarding like? I mean, lots of things had changed, you know, in the, in the intervening 10 years or so. Uh, and lots had stayed the same, you know, not in a bad way, but just, you know, uh, some of the technologies that we use today are still some of the technologies we used 10 years ago, a lot has changed though.

Um, a bunch of the people are still around. So there's something about eBay that, um, people tend to stay a long time. You know, it's not really very strange for people to be at eBay for 20 years. Um, in my particular team of let's call it 150, there are four or five people that have crossed their 20 year anniversary at the company.

Um, and I also re I rejoined with a bunch of other boomerangs as the term we use internally. So it's, you know, the, um, including the CEO, by the way. So sort of bringing the band back together, a bunch of people that had gone off and worked at it, but at other places have, have come back for various reasons over the last couple of.

So it was both a lot of familiarity, a lot of unfamiliarity, a lot of familiar faces. Um, yup.

[00:38:17] **Jeremy:** So, I mean, having these people who you work with still be there and actually coming back with some of those people, um, what were some of the big, I guess, advantages or benefits you got from, you know, those existing connections?

[00:38:33] **Randy:** Yeah. Well, I mean, as with all things, you know, imagine, I mean, everybody can imagine like getting back together with friends that they had from high school or university, or like you had some people had some schooling at some point and like you get back together with those friends and there's this, you know, there's this implicit trust in most situations of, you know, because you went through a bunch of stuff together and you knew each other, uh, you know, a long time.

And so that definitely helps, you know, when you're returning to a place where again, there are a lot of familiar faces where there's a lot of trust built up. Um, and then it's also helpful, you know, eBay's a pretty complicated place and it's 10 years ago, it was too big to hold in any one person's head and it's even harder to hold it in one person said now, but to be able to come back and have a little bit of that, well, more than a little bit of that context about, okay, here's how eBay works.

And here, you know, here are the, you know, unique complexities of the marketplace cause it's very unique, you know, um, uh, in the world. Um, and so, yeah, no, I mean, it was helpful. It's helpful a lot. And then also, you know, in my current role, um, uh, my, my main goal actually is to just make all of eBay better, you know, so we have about 4,000 engineers and, you know, my team's job is to make all of them better and more productive and more successful and, uh, being able to combine.

Knowing what eBay, knowing the context about eBay and having a bunch of connections to the people that, you know, a bunch of the leaders there, uh, here, um, combining that with 10 years of experience doing other things at other places, you know, that's helpful because you know, now there are things that we do at eBay that, okay, well there, you know, you know, that this other place is doing, this has that same problem and is solving it in a different way.

And so maybe we should, you know, look into that option. So,

[00:40:19] **Jeremy:** so, so you mentioned just trying to make developers, work or lives easier. you start the job. How do you decide what to tackle first? Like how do you figure out where the problems are or what to do next?

[00:40:32] **Randy:** yeah, that's a great question. Um, so, uh, again, my, uh, I lead this thing that we internally called the velocity initiative, which is about just making us, giving us the ability to deliver. Features and bug fixes more quickly to customers. Right. And, um, so what do I figure for that problem? How can we deliver things more quickly to customers and improve, you know, get more customer value and business value?

Uh, what I did, uh, with, in collaboration with a bunch of people is what one would call a value stream map. And that's a term from lean software and lean manufacturing, where you just look end to end at a process and like say all the steps and how long those steps take. So a value stream, as you can imagine, like all these steps that are happening at the end, there's some value, right?

Like we produced some, you know, feature or, you know, hopefully gotten some revenue or like helped out the customer and the business in some way. And so value, you know, mapping that value stream. That's what it means. And, um, Looking for you look at that. And when you can see the end-to-end process, you know, and like really see it in some kind of diagram, uh, you can look for opportunities like, oh, okay, well, you know, if it takes us, I'm making this effort, it takes us a week from when we have an idea to when it shows up on the site.

Well, you know, some of those steps take five minutes. That's not worth optimizing, but some of those steps take, you know, five days and that is worth optimizing. And so, um, getting some visibility into the system, you know, looking end to end with some, with a kind of view of the system systems thinking, uh, that will give you the, uh, the knowledge about, or the opportunities about we know what can be improved.

And so that's, that's what we did. And we didn't talk with all 4,000, you know, uh, engineers are all, you know, whatever, half a thousand teams or whatever we had. Um, but we sampled. And after we talked with three teams who were already hearing a bunch of the same things, you know, so we were hearing in the whole product life cycle, which I like to divide into four stages.

I'd like to say, there's planning. How does an idea become a project or a thing that people work on a software development? How does a project or become committed code software delivery? How does committed code become a feature that people actually use? And then what I call post release iteration, which is okay, it's now there are out there on the site and we're turning it on and off for individual users.

We're learning in analytics and usage in the real world and, and experimenting. And so there were opportunities that eBay at all, four of those stages, um, which I'm happy to talk about, but what we ended up seeing again and again, uh, is that that software delivery part was our current bottleneck. So again, that's the, how long does it take from an engineer when she commits her code to, it shows up as a feature on the site.

And, you know, before we started the work. You know, two years ago before we started the work that I've been doing for the last two years with a bunch of people, um, on average and eBay was like a week and a half. So, you know, it'd be a week and a half between when someone's finished and then, okay. It gets code reviewed and, you know, dot, dot, dot it gets rolled out.

It gets tested, you know, all that stuff. Um, it was, you know, essentially 10 days. And now for the teams that we've been working with, uh, it's down to two. So we used a lot of, um, what people may be familiar with, uh, the accelerate book. So it's called accelerate by Nicole Forsgren. Um, Jez humble and Gene Kim, uh, 2018, like if there's one book anybody should read about software engineering, it's that?

Uh, so please read accelerate. Um, it summarizes almost a decade of research from the state of DevOps reports, um, which the three people that I mentioned led. So Nicole Forsgren, you know, is, uh, is a doctor, uh, you know, she's a PhD and, uh, data science. She knows how to do all this stuff. Um, anyway, so, uh, that when your, when your problem happens to be software delivery.

The accelerate book tells you all the kind of continuous delivery techniques, trunk based development, uh, all sorts of stuff that you can do to, to solve that, uh, solve those problems. And then there are also four metrics that they use to measure the effectiveness of an organization, software delivery. So people might be familiar with, uh, there's deployment frequency.

How often are we deploying a particular application lead time for change? That's that time from when a developer commits her code to when it shows up on the site, uh, change failure rate, which is when we deploy code, how often do we roll it back or hot fix it, or, you know, there's some problem that we need to, you know, address.

Um, and then, uh, meantime to re uh, meantime to restore, which is when we have one of those incidents or problems, how, how quickly can we, uh, roll it back or do that hot fix? Um, and again, the beauty of Nicole Forsgren research summarized in the accelerate book is that the science shows that companies cluster, in other words, Mostly the organizations that are not good at, you know, deployment frequency and lead time are also not good at the quality metrics of, uh, meantime to restore and change failure rate and the companies that are excellent at, you know, uh, deployment frequency and lead time are also excellent at meantime, to recover and, uh, change failure rate.

Um, so companies or organizations, uh, divided into these four categories. So there's a low performers, medium performers, high performers, and then elite performers. And, uh, eBay was solidly eBay on average at the time. And still on average is solidly in that medium performer category. So, uh, and what we've been able to do with the teams that we've been working with is we've been able to move those teams to the high category.

So just super brief. Uh, and I w we'll give you a chance to ask you some more questions, but like in the low category, all those things are kind of measured in months, right. So how long, how often are we deploying, you know, measure that in months? How long does it take us to get a commit to the site? You know, measure that in months, you know, um, where, and then the low performer, sorry.

Uh, the medium performers are like, everything's measured in weeks, right? So like, if we were deploy, you know, couple, you know, once every couple of weeks or once a week, uh, lead time is measured in weeks, et cetera. The, uh, the high-performers things are measured in days and the elite performance things are measured in hours.

And so you can see there's like order of magnitude improvements when you go from, you know, when you move from one of those kind of clusters to another cluster. Anyway. So what we were focused on again, because our problem was software delivery was moving a whole, a whole set of teams from that medium performer category where things are measured in weeks to the, uh, high-performer category, where things are missing.

[00:47:21] **Jeremy:** throughout all this, you said the, the big thing that you focused on was the delivery time. So somebody wrote code and, they felt that it was ready for deployment, but for some reason it took 10 days to actually get out to the actual site. So I wonder if you could talk a little bit about, uh, maybe a specific team or a specific application, where, where, where was that time being spent?

You know, you, you said you moved from 10 days to two days. What, what was happening in the meantime?

[00:47:49] **Randy:** Yeah, no, that's a great question. Thank you. Um, yeah, so, uh, okay, so now, so we, we, we looked end to end of the process and we found that software delivery was the first place to focus, and then there are other issues in other areas, but we'll get to them later. Um, so then for, um, to improve software delivery, now we asked individual teams, we, we, we did something like, um, you know, some conversation like I'm about to say, so we said, hi, it looks like you're deploying kind of once or twice.

If I, if I told you, you had to deploy once a day, tell me all the reasons why that's not going to work. And the teams are like, oh, of course, well, it's a build times take too long. And the deployments aren't automated and you know, our testing is flaky. So we have to retry it all the time and, you know, dot, dot, dot, dot, dot.

And we said, great, you just gave my team, our backlog. Right. So rather than, you know, just coming and like, let's complain about it. Um, which the teams work it's legit for them to complain. Uh, I was a, you know, we were able, because again, the developer program or sorry, the developer platform, you know, is as part of my team, uh, we said, great, like you just gave us, you just told us all the, all your top, uh, issues or your impediments, as we say, um, and we're going to work on them with you.

And so every time we had some idea about, well, I bet we can use Canary deployments to automate the deployment which we have now done. We would pilot that with a bunch of teams, we'd learn what works and doesn't work. And then we would roll that out to everybody. Um, So what were the impediments like? It was a little bit different for each individual team, but in some, it was, uh, the things we ended up focusing on or have been focusing on our build times, you know, so we build everything in Java still.

Um, and, uh, even though we're generation five, as opposed to that generation three that I mentioned, um, still build times for a lot of applications we're taking way too long. And so we, we spend a bunch of time improving those things and we were able to take stuff from, you know, hours down to, you know, single digit minutes.

So that's a huge improvement to developer productivity. Um, we made a lot of investment in our continuous delivery pipelines. Um, so making all the, making all the automation around, you know, deploying something to one environment and checking it there and then deploying it into a common staging environment and checking it there and then deploying it from there into the production environment.

And, um, and then, you know, rolling it out via this Canary mechanism. We invested a lot in something that we call traffic mirroring, which is a, we didn't invent. Other T other places have a different name for this? I don't know if there's a standard industry name. Some people call it shadowing, but the idea is I have a change that I'm making, which is not intended to change the behavior.

Like a lots of changes that we make, bug fixes, et cetera, uh, upgrading to new, you know, open source, dependencies, whatever, changing the version of the framework. There's a bunch of changes that we make regularly day-to-day as developers, which are like, refactorings kind of where we're not actually intending to change the behavior.

And so a tra traffic mirroring was our idea of. You have the old code that's running in production and you, and you fire a request, a production request at that old code and it responds, but then you also fire that request at the new version and compare the results, you know, did the same, Jason come back, you know, between the old version and the new version.

Um, and that's, that's a great way kind of from the outside to sort of black box detect any unintended changes in the, in the behavior. And so we definitely leveraged that very, very aggressively. Um, we've invested in a bunch of other bunch of other things, but, but all those investments are driven by what does the team, what do the particular teams tell us are getting in their way?

And there are a bunch of things that the teams themselves have, you know, been motivated to do. So my team's not the only one that's making improvements. You know, teams have. Reoriented, uh, moved, moved from branching development to trunk based development, which makes a big difference. Um, making sure that, uh, PR approvals and like, um, you know, code reviews are happening much more regularly.

So like right after, you know, a thing that some teams have started doing is like immediately after standup in the morning, everybody does all the code reviews that you know, are waiting. And so things don't drag on for, you know, two, three days, cause whatever. Um, so there's just like a, you know, everybody kind of works on that much more quickly.

Um, teams are building their own automations for things like testing site speed and accessibility and all sorts of stuff. So like all the, all the things that, you know, a team goes through in the development and roll out of their software, they were been spending a lot of time automating and making, making a leaner, making more efficient.

[00:52:22] **Jeremy:** So, so some of those, it sounds like the PR example is really, on the team. Like you're, you're telling them like, Hey, this is something that you internally should change how you work. for things like improving the build time and things like that. Did you have like a separate team that was helping these teams, you know, speed that process up? Or what, what was that 

[00:52:46] **Randy:** like?

Yeah. Great. I mean, and you did give to those two examples are, are like you say, very different. So I'm going to start from, we just simply showed everybody. Here's your deployment frequency for this application? Here's your lead time for this application? Here's your change failure rate. And here's your meantime to restore.

And again, as I didn't mention before. All of the state of DevOps research and the accelerate book prove that by improving those metrics, you get better engineering outcomes and you also get better business outcomes. So like it's scientifically proven that improving those four things matters. Okay. So now we've shown to teams, Hey, you're we would like you to improve, you know, for your own good, but you know, more broadly at eBay, we would like the deployment frequency to be faster.

And we would like the lead time to be shorter. And the insight there is when we deploy smaller units of work, when we don't like batch up a week's worth of work, a month's worth of work, uh, it's much, much less risky to just deploy like an hour's worth of work. Right. And the, and the insight is the hours worth of work fits in your head.

And if you roll it out and there's an issue. First off rolling backs, no big deal. Cause you only, you know, not, you've only lost an hour of work for a temporary period of time, but also like you never have this thing, like what in the world broke? Cause like with a month's worth of work, there's a lot of things that changed and a lot of stuff that could break, but with an hour's worth of work, it's only like one change that you made.

So, you know, when, if something happens, like it's pretty much, pretty much guaranteed to be that thing anyway, that's the back. Uh, that's the backstory. And um, and so yeah, we were just working with individual teams. Oh yeah. So they were, the teams were motivated to like, see what's the biggest bang for the buck in order to improve those things.

Like how can we improve those things? And again, some teams were saying, well, you know what, a huge component of our, of that lead time between when somebody commits and it's, it's a feature on the site, a huge percentage of that. Maybe multiple days, it's like waiting for somebody to code review. Okay, great.

We can just change our team kind of agreements and our team behavior to make that happen. And then yes, to answer your question about. Were the other things like building the Canary capability and traffic mirroring and build time improvements. Those were done by central, uh, platform and infrastructure teams, you know, some of which were in my group and some of which are in peer peer groups, uh, in, in my part of the organization.

So, yeah, so I mean like providing the generic tools and, you know, generic capabilities, those are absolutely things that a platform organization does. Like that's our job. Um, and you know, we did it. And, uh, and then there are a bunch of other things like that around kind of team behavior and how you approach building a particular application that are, are, and should be completely in the control of the individual teams.

And we were trying not to be, not trying not to be, we were definitely not being super prescriptive. Like we didn't come in and we say, we didn't come in and say, alright, by next, by next Tuesday, we want you to be doing trunk based development by, you know, the Tuesday after that, we want to see test-driven development, you know, dot, dot, Um, we would just offer to teams, you know, hear it.

Here's where you are. Here's where we know you can get, because like we work with other teams and we've seen that they can get there. Um, you know, they just work together on, well, what's the biggest bang for the buck and what would be most helpful for that team? So it's like a menu of options and you don't have to take everything off the menu, if that makes sense.

[00:56:10] **Jeremy:** And, and how did that communication flow from you and your team down to the individual contributor? Like you have, I'm assuming you have engineering managers and technical leads and all these people sort of in the chain. How does it

[00:56:24] **Randy:** Yeah, thanks for asking that. Yeah. I didn't really say how we work as an initiative. So every, um, so there are a bunch of teams that are involved. Um, and we have, uh, every Monday morning, so, uh, just so happens. It's late Monday morning today. So we already did this a couple of hours ago, but once a week we get all the teams that are involved, both like the platform kind of provider teams and also the product.

Or we would say domain like consumer teams. And we do a quick scrum of scrums, like a big old kind of stand up. What have you all done this week? What are you working on next week? What are you blocked by kind of idea. And, you know, there are probably 20 or 30 teams again, across the individual platform capabilities and across the teams that, you know, uh, consume this stuff and everybody gives a quick update and they, and, uh, it's a great opportunity for people to say, oh, I have that same problem too.

Maybe we should offline try to figure out how to solve that together. You built a tool that automates the site speed stuff. That's great. I would S I would so love to have that. And, um, so it, uh, this weekly meeting has been a great opportunity for us to share wins, share, um, you know, help that people need and then get, uh, get teams to help with each other.

And also, similarly, one of the platform teams would say something like, Hey, we're about to be done or beta, let's say, you know, this new Canary capability, I'm making this up. Anybody wanna pilot that for us? And then you get a bunch of hands raised of yo, we would be very happy to pilot that that would be great.

Um, so that's how we communicate back and forth. And, you know, it's a big enough. It's kind of like engineering managers are kind of are the kind of level that are involved in that typically. Um, so it's not individual developers, but it's like somebody on most, every team, if that makes any sense. So like, that's kind of how we do that, that like communication, uh, back to the individual developers.

If that makes sense.

[00:58:26] **Jeremy:** Yeah. So it sounds like you would have, like you said, the engineering manager go to the standup and um, you said maybe 20 to 30 teams, or like, I'm just trying to get a picture for how many people are in this meeting.

[00:58:39] **Randy:** Yeah. It's like 30 or 40 people.

[00:58:41] **Jeremy:** Okay. Yeah.

[00:58:42] **Randy:** And again, it's quick, right? It's an hour. So we just go, boom, boom, boom, boom. And we've just developed a cadence of people. We have a shared Google doc and like people like write their little summaries, you know, of what they're, what they've worked on and what they're working on.

So we've over time made it so that it's pretty efficient with people's time. And. Pretty dense in a good way of like information flow, back and forth. Um, and then also separately, we meet more in more detail with the individual teams that are involved. Again, try to elicit, okay, now, where are you now?

Here's where you are. Please let us know what problems you're seeing with this part of the infrastructure or problems you're seeing in the pipelines or something like that. And we're, you know, we're constantly trying to learn and get better and, you know, solicit feedback from teams on what we can do differently.



[00:59:29] **Jeremy:** earlier you had talked a little bit about how there were a few services that got brought over from V2 or V3, basically kind of more legacy or older services that are, have been a part of eBay for quite some time.

And I was wondering if there were things about those services that made this process different, like, you know, in terms of how often you could deploy or, um, just what were some key differences between something that was made recently versus something that has been with the company for a long time?

[01:00:06] **Randy:** Yeah, sure. I mean, the stuff that's been with the company for a long time was best in class. As of when we built it, you know, maybe 15 and sometimes 20 years ago. Um, there actually, I wouldn't even less than a handful. There are, as we speak, there are two or three of those V3. Uh, clusters or applications or services still around and they should be gone in a completely migrated away from, in the next a couple of months.

So like, we're almost at the end of, um, you know, uh, moving all to more modern things. But yeah, you know, I mean, again, uh, stuff that was state-of-the-art, you know, 20 years ago, which was like deploying things once every two weeks, like that was a big deal in 2000 or 2004. Uh, and it's, you know, like that was fast in 2004 and is slow in 2022.

So, um, yeah, I mean, what's the difference? Um, yeah, I mean, a lot of these things, you know, if they haven't already been migrated, there's a reason. And it's because often that they're way in the guts of something that's really important. You know, this is the, this is a core part. I'm making these examples up and they're not even right, but like it's a core part of the payments flow.

It's a core part of, you know, uh, how, uh, sellers get paid. And those aren't examples. We have, those are modern, but you see what I'm saying? Like stuff that's like really core to the business and that's why it's kind of lasted.

[01:01:34] **Jeremy:** And, uh, I'm kind of curious from the perspective of some of these new things you're introducing, like you're talking about, um, improving continuous delivery and things like that. Uh, when you're working with some of these services that have been around a long time, are the teams the rate at which they deploy or the rate at which you find defects is that noticeably different from services that are more recent?

[01:02:04] **Randy:** I mean, and that's true of any legacy at any, at any place. Right? So, um, yeah, I mean, people are legitimately, uh, I have some trepidation that say about, you know, changing something that's, you know, been running the, running the business for a long, long time. And so, you know, it's a lot slower going, uh, exactly because it's not always completely obvious what, um, you know, what the implications are of those changes.

So, you know, we were very careful and we, you know, trust things a whole lot. And, um, you know, maybe we didn't write stuff with a whole bunch of automated tests in the beginning. And so there's a lot of manual stuff there. You know, this is pretty, you know, this is just what happens when you have, uh, you have stuff that, you know, you have a company that's, you know, been around for a long time.

[01:02:51] **Jeremy:** yeah, I guess just, just kind of to start wrapping up as this process of you coming into the company and identifying where the problems are and working on like, um, you know, ways to speed up delivery. Is there, there anything that kind of came up that really surprised you? I mean, you've been at a lot of different organizations. Is there anything about your experience here at eBay that was very different than what you'd seen before?

[01:03:19] **Randy:** No. I mean, it's a great question. I don't think, I mean, I think the thing that's surprising is how unsurprising it is. Like there's not, you know, the details are different. Like, okay. You know, we have this V3, I mean, like, you know, we have some uniquenesses around eBay, but, but, um, but I think what is maybe pleasantly surprising is all the techniques about how one.

Notice the things that are going on, uh, in terms of, you know, again, deployment, frequency, lead time, et cetera, and what techniques you would deploy to like make those things better. Um, all the standard stuff applies, you know, so again, uh, all the, all the techniques that are mentioned in the state of DevOps research and an accelerate and just all the, all the known good practices of software development, they all apply everywhere.

Um, and that's the wonderful, I think that's the wonderful thing. So like maybe the most surprising thing is how unsurprising or how, how, how applicable the, you know, the standard industry standard techniques, uh, are, I mean, I certainly hope that to be true, but that's why we, I didn't really say, but we piloted this stuff with a small number of teams.

Exactly. Because we, you know, we thought, and it would turned out to be true that they applied, but we weren't entirely sure. You know, we didn't know what we didn't know. Um, and we also needed proof points, you know, Not just out there in the world, but at eBay that these things made a difference and it turns out they do. So.

[01:04:45] **Jeremy:** yeah, I mean, I think it's easy for people to kind of get caught up and think like, my problem is unique or my organization is unique and, but it, but it sounds like in a lot of cases, maybe we're not so not so different.

[01:04:57] **Randy:** I mean, the stuff that works tends to work everywhere, the deeds there's always some detail, but, um, but yeah, I mean all aspects of, you know, the continuous delivery and kind of lean approach the software. I mean, we, the industry have yet to find a place where they don't work seriously. You have to find any place where they don't work.

[01:05:19] **Jeremy:** if people want to, um, you know, learn more about the work that you're doing at eBay, or just follow you in general, um, where should.

[01:05:27] **Randy:** Yeah. So, um, I tweet semi-regularly at, at Randy shelf. So my name all one word, R a N D Y S H O U P. Um, I'm not, I had always wanted to be a blogger. Like there is a Randy shop.com and there are some blogs on there, but they're pretty old. Um, someday I hope to be doing more writing. Um, I do a lot of conference speaking though.

So I speak at the Q con conferences. I'm going to be at the craft concert in Budapest in a couple of in week and a half, uh, as of this recording. Um, so you can often find me on, uh, on Twitter or on software conferences.

[01:06:02] **Jeremy:** all right, Randy. Well, thank you so much for coming back on software engineering radio.

[01:06:06] **Randy:** Thanks for having me, Jeremy. This was fun.

</div>