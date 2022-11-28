+++
title = "Fixing a Broken Development Process with John Doran"

description = "John Doran shares how his team focused on monitoring, continuous integration, and changed their culture to save a SaaS business that was struggling to support its customer base."

[extra]
episode_url = "https://pinecast.com/listen/5cab95d4-45d0-47bf-b595-cc4309ae83a8.mp3"
social_title = "Fixing a Broken Development Process"
social_description = "John Doran shares how his team changed their culture to save a SaaS business struggling with technical problems."
+++

[John Doran](https://twitter.com/johnwildoran) is the CTO of [Phorest](https://www.phorest.com), an application for managing salons and spas.

We discuss:
- Transitioning a desktop application to a SaaS
- Struggling with outages and performance problems
- Moving away from relying on a single person for deployment
- Building a continuous integration pipeline
- Health monitoring for services
- The benefits of docker
- Using AWS managed services like Aurora and ECS

This episode originally aired on Software Engineering Radio.

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy:** [00:00:00] Today I have John Doran with me. John is the director of engineering at Phorest, a Dublin based SAAS company, that processes appointments for the hair and beauty industry. He previously worked as a technical lead at Travelport digital, where he supported major airlines and hotel chains with their mobile platforms.

I'll be speaking with John about the early days of their business, the challenges they faced while scaling and how they were able to reshape their processes and team to overcome these challenges. John, welcome to software engineering radio. 

**John:** [00:00:29] Hey Jeremy, thanks so much for having me. 

**Jeremy:** [00:00:31] The first thing I'd like to discuss is the early days of forest to just give the listeners a little bit of background. What type of product is Phorest? 

**John:** [00:00:40] Sure. So forest is essentially, um, It's a salon software focused in the hair and beauty industry. And it didn't actually start off as that back in 2003, it was actually a messaging service actually built by a few students and Trinity college. One of which was his name was Ronan.

Percevel. Ronan is actually our current CEO. So that in 2003, that messaging service was supporting, um, nightclubs, dentists, various small businesses around Dublin, and the guys were finding it really hard to get some traction in, in those phase different industries. So Ronan actually went and worked as a, as a hair receptionist in a salon.

And what he learned from that was that through using messaging on the platform that they were able to actually increase revenue for salons and actually get more money in the tills, which was hugely powerful thing. So from there, they were able to refocus on the, on that particular industry, they built supplementary features and a product around that messaging service.

So in 2004, it became a kind of a fully fledged appointment book. And from there then they, they integrated that appointment book with the messaging service. So by 2006, then I guess you could classify phorest as a full salon software. So it had things like stock take, financial reporting, and staff rostering. That's fully based salon software system was pretty popular in Ireland and actually by between 2006 and 2008, they became the number one in the industry in Ireland. So what that meant was, you know, the majority of salons in Ireland were running on, on the phorest platform and that was actually an on-premise system. So all the data would have been stored locally in the hair salon.

And there was no backend, 

**Jeremy:** [00:02:30] just so I understand correctly. So you say it was running on premise. It was an appointment system. So is this where somebody would come into the salon and make an appointment and they would enter it into a local computer and it would be just stored there? 

**John:** [00:02:46] Exactly. So, so what Ronan figured out throughout his time, working in the salon that by actually sending customers text messages, to remind them about their appointments really helped cut down the no-show rates, meaning that customers did turn up for their appointments when they were due and meaning that the staff members didn't have to sit around, waiting for customers to walk in.

So as Phorest I guess, as a company developed. We, we moved into building extra features around that core system, which is an appointment book, which manages the day-to-day, uh, rows of a hairstylist. So we built, uh, email and marketing retention tools around that. Okay. I guess a really important point about Phorest's history is when the recession hit in 2008 in Ireland, we, uh, moved into the UK.

So as we were kind of the number one provider in Ireland, we felt that, uh, when the recession hit that we needed to move into the UK, but being on premise meant there was a lot of friction actually installing the system into the salons. So in 2011, they actually took a small seed round to build out, I guess, the cloud backend.

Well, once the kind of cloud backend was built, it took about a year to get it off the ground and released. Um, and as the company kind of gained traction in the UK, they, they migrated all of their premise customers onto the cloud solution. 

**Jeremy:** [00:04:07] I guess you would say that when it was on premise, a lot of the engineering effort or the support effort was probably in keeping the software, working for your customers and just addressing technical issues or questions and things like that. And that was probably taking a lot of your time. Is that correct? 

**John:** [00:04:25] Precisely the, the team was quite small. So we had five engineers who were essentially building it at the cloud backend. And one engineer who was maintaining that Delphi on premise application.

So what was happening was our CEO Ronan was actually the product owner at that time. And the guys were making pretty drastic and kind of quickfire decisions in terms of features being added to the product based on, you know, getting a certain customer in that really needed to pay the bills. And some of those decisions, uh, I guess, made the product a bit more complex, uh, as a group, but it certainly was, it was a big improvement from the on-premise solution.

**Jeremy:** [00:05:03] Hmm. So the on-premise solution you said was written in Delphi, is that correct? 

**John:** [00:05:08] Yeah, 

**Jeremy:** [00:05:09] when it was first started, was it just a single developer? 

**John:** [00:05:13] Exactly. Yeah. So it was, it was literally, uh, put together by some, some outsourcers and a single developer managing it. There was no, there was no real in-house developers.

It was, you know, a little bit of turnover there. But when that small seed round came in with the guys put that together, the foundations of the cloud-based backend, which was a, a Java kind of classic, uh, n-tiered application with web socket to update the appointment screen. If anything changed on the backend.

And, um, you, you would kind of consider it a majestic monolith as such 

**Jeremy:** [00:05:44] When you started the cloud solution. Were you maintaining both systems simultaneously? 

**John:** [00:05:49] Yeah, so, um, for a full year, that goes where we're building out that backend. And at the same time, there was a one guy who was, who was literally maintaining, fixing bugs on that, that Delphi application.

And just to kind of give you an example. Um, one of the guys who was actually working on support, he actually went and taught himself SQL and he used to, to tunnel into the salons at nighttime to fix any database issues. And, um, 

**Jeremy:** [00:06:17] Oh, wow.

**John:** [00:06:17] Yeah. So it was, it was, you know, hardcore stuff. Um, another big thing about not being a cloud-based and, and one of the big reasons we needed to become cloud based was we, you know, as, as people move online and, you know, it's, it's quite common to book, you know, your cinema or some something else online, but, um, Ronan could see that trend coming for online bookings, uh, and we needed to be cloud-based to build, to build out that online booking system.

And just to kind of give you an idea of the scale, like last year, we, we would have processed about over 2 billion euros worth of transactions to the system. So it's really, it's really growing. And, um, you know, it's huge, huge scale at the moment by that, I guess looking, looking back at the past, the guys would have built a great robust system getting us to that 10,000 salon mark, particularly in the UK, but that would have been the point that the guys would have started seeing some, you know, shakiness in terms of stability and the speed at which at which you could deliver new new features.

**Jeremy:** [00:07:22] You were saying the initial cloud version took about a year to create?

**John:** [00:07:26] Exactly. Yeah. 

**Jeremy:** [00:07:27] And you had five engineers working on it after the seed round? At that time, when you first started 

working on the cloud version of the application, did you have a limited rollout to kind of weed out defects? Or how did you start transferring customers over.

**John:** [00:07:46] So there was definitely some reluctant customers to, to move across. We did it, I guess, uh, gradually there was a lot of reluctance for people. People were quite scared of their data, not being stored in their salon. And so it was quite hard to get those, some of those customers across and only two weeks ago, we, we actually officially stopped supporting that final two customers have finished up. So. You know it took us a good seven years to finish that transition. 

**Jeremy:** [00:08:12] Uh, so it was a very gradual transition where you actually, what did you ask customers whether they wanted to move or how did you... 

**John:** [00:08:21] Oh, yeah. It was a huge, huge sales and team effort to, to get people across the line. But I would say the majority of people either would have churned or, or would have moved across the, the more forward-thinking people.

I, you know, they would have been getting new features and a better service. 

**Jeremy:** [00:08:36] Right. So it was kind of more of a marketing push from your side to say, Hey, if you move over to our cloud solution, you'll get all these additional capabilities. But it was ultimately up to them to decide whether they want it to.

**John:** [00:08:47] Yeah. So, um, no, some companies, they. They kind of build that product with a different name and they try and sell it but uh Phorest we actually kept the UI very similar. So it wasn't very intrusive to the users. It was just kind of seen as an upgrade with, um, I guess, less friction. 

**Jeremy:** [00:09:06] Right. Right. I want to talk a little bit about the. Early days where you, you said you spent about a year to build the MVP at that point, let's say after that year had passed, were you still able to iterate quickly in terms of features or were you having any problems with performance or downtime at that point?

**John:** [00:09:28] So in 2012, when the cloud-based product launched, particularly in the UK, once we hit about a thousand customers, we started to see creaking issues in the backend, lots of JVM, garbage collection problems, lots of, uh, database contention and lots of outages.

So we got to a point where we were trying hardware at the problem to, to make things a little bit faster. So what our problems were. We kind of relied a lot on a single person to do a lot of the deployments.  it wasn't really a team effort to, to ship things. It was more so developer finishes code and the machine push it off.

Maybe at the end of the month we would ship. I guess the big problem was the stability. So essentially what, what happened was. In terms of the architecture, we were introducing caches at various levels to try and, um, cope with performance. So, uh, a layer of caching on the client's side was introduced, uh, memcached uh, was introduced, uh, level, level 2 hibernate caching, always just, you know, really focusing on fixing the immediate problem, without looking at kind of the bigger picture, once I said, I mentioned that 2000 salons as a marker, I guess once we hit like 1200.

The guys had to introduce, uh, the idea of silos, which was like essentially 1000 customers are going to be linked to a specific URL and that URL will host the, the API returning back the data that they need. And then the other silo, which would service the other, you know, 200 growing to say thousand businesses.

So essentially if you think about it, you've got, I guess, a big point of failure. If, if that, if that server goes down, There's no load balancing between between servers and those two servers are their biggest size possible. So I guess a big red herring was the, the cost, uh, I guess, implications of that, you know, it was the largest, uh, instance type on Amazon on RDS and EC2 level.

**Jeremy:** [00:11:31] The entire system was on a single instance for each silo?

**John:** [00:11:35] Yeah. So if you imagine, um, when you, when you log in, you'll get returned a URL for a particular silo. So what would happen then would be X businesses go to that silo and X, Y businesses go to the other silo and what that did was basically it load balanced, the businesses at kind of a database level.

**Jeremy:** [00:11:55] You were mentioning how you had like different caching layers, for example, memcached and things like that, but those were all being run on the same instance. Is that correct? 

**John:** [00:12:05] Um, they would have been hosted by Amazon. 

**Jeremy:** [00:12:07] Oh okay. So those would have been, uh, Amazon's hosted services. 

**John:** [00:12:10] So, yeah. Yeah. It's kind of like when you build that MVP or you build that initial stage, your product is kind of, you're focusing on building features.

You're focusing on getting bums on seats and you. It was that point, that 12, 1200 to a thousand. salons that where we felt that pain, that scaling pain. 

**Jeremy:** [00:12:30] So in a way, like you said, you were doing multitenancy, but it was kind of split per thousand customers. 

**John:** [00:12:38] Yeah, exactly. So if you imagine, if, if a failure happened on one of those servers, there is no fault tolerance.

If the deployment goes wrong in terms of like, uh, putting an instance in service, those, those thousand customers can't make purchases, their customers can't make online bookings. There's no appointments being served. You can't run transactions through the till. So, uh, we've caused huge, huge friction. 

**Jeremy:** [00:13:04] Right. Uh, what were the managed services you were using in combination with the EC2 instance? 

**John:** [00:13:12] So, um, a really good decision at the start of the guys moving to cloud was making a big bet on Amazon in terms of utilizing them for RDS, EC2, caching. There was no deployment stack, or there was no deployment, uh, infrastructure as code.

It was all I guess, manually done through Amazon console, which is something that we later address, which we'll chat about it, but it was all, all heavily reliant on Amazon. 

**Jeremy:** [00:13:38] And you had mentioned that you were relying on one person to do deployment. Was, was that still the case at this time? 

**John:** [00:13:46] Yeah, so up until, I guess 2014. Um, It was all reliant on one guy who, who literally had to bring his laptop on holidays with them and tether from cafes. If something went down to deploy new code, he was the only guy who knew how to do it. So it was, it was a huge pain point and bus factor. 

**Jeremy:** [00:14:08] So it sounds like in terms of how the team was split up, there was basically, you have people working on development and you have a single person in the sort of ops role.

**John:** [00:14:21] Yeah. And, uh, essentially when, when this kind of thing happens, you, the people who write the code don't ship it, you get all sorts of problems in terms of dependencies and tangles. And, uh, and you know, just just knowledge, knowledge silos, and also, you know, because the guys were working kind of in their own verticals, uh, different areas of the product.

There was no consistency. Consistency in terms of the engineering values, how they were working, practices, procedures, you know, deployments, that sort of stuff. It was all, it was all very isolated. So, um, people did their own, their own thing. So, uh, you could imagine for say trying to hire someone new would be quite hard because, um, you know, for someone to come in very, very different, depending on which engineer you talk to.

That makes sense? 

**Jeremy:** [00:15:10] Yeah, was, was this a locally located team or was this a remote team? 

**John:** [00:15:16] Most of the guys were actually in Dublin. Um, one or two people traveled a little bit worked remotely and a couple of people did actually move abroad. So it was predominantly based in Dublin, but, um, some people traveled a bit in terms of processes 

**Jeremy:** [00:15:28] For someone knowing how to deploy or how to work on a feature. It was mostly tribal knowledge. It's more just trying to piece together a story from talking to different people. Is that correct? 

**John:** [00:15:42] Precisely. So, um, you, you had no consistency in languages or frameworks. Um, except I would say that that model, it, uh, that, that initial part of the platform was extremely consistent, uh, in terms of the patterns used, uh, the. I guess the way it communicated with database and you know, how the API was built, um, was extremely strong and, uh, is, is the heart of steel is the heart of the organization. So say for example, there was a lot of really good, uh, say integration and unit tests there, but they got abandoned for a little while and we had to bring them back, back to life, to, to, to enable us to start moving faster again, and to give us a lot more confidence.

**Jeremy:** [00:16:32] Hmm. So it sounds like maybe the initial version and the first year or so had a pretty solid foundation, but then as. I'm not sure if it was the team that grew or just the, the rate of features. Uh, would you say that? 

**John:** [00:16:47] I would say it was a combination of the, the growth of the company in terms of the number of customers on it, and the focus on delivering features.

So focusing on feature development rather than tinking about scalability and. Being extremely aware of how, how fast were you gaining customers at that time? Was this a steady increase or large spikes? You're talking to 30% annually. So 30% annually and really, really low churn rate as well. 

**Jeremy:** [00:17:17] So what would you feel was the turning point where it felt like your software had, or your business had to fundamentally change due to the number of customers you had?

**John:** [00:17:28] So it was essentially those issues around stability and cost where we're on sustainable for the business customers complaining, uh, our staff not being able to. To do their job. So, you know, part of Phorest's core values and mission is to help the salon owner grow their business and use, use the tools that we provide to, to do that.

And if people are firefighting, uh, and not being able to, to support our customers, to be able to send, help them send really great marketing campaigns to boost our revenue, if we're not doing that, um, we're, we're firefighting the company would have been pointless. So we weren't fulfilling our mission by coping with outages and panicking all the time. The costs again, we're, we're unsustainable and you know, the team, you know, it was just, I guess, uncomfortable with this, the state we were in. So the turning point would have been, I would say in like 2014, when we, we essentially hired in some people who have more, more experience in.

I would say the high scalability systems and people who, who cared a little bit more about quality and best practices. So when you hire a three or four people like that, you kind of, you bring in a, a different way of thinking you kind of, you hire, hire, hire these dif different values. You know, when you, when you try to. To talk to a team and try and get these things out. They're normally quite organic. If you bring people in from maybe a similar comp at all from a different industry, but similar experience, you, you kind of get that for free. And that's what Phorest did. So, um, basically in 2014, and since now, we've, we've invested heavily in hiring and hiring the right people in terms of how they operate and then in terms of how they think but also bringing that back to our our values and, um, and what we try to do, 

**Jeremy:** [00:19:28] Do you think that bringing in, you know, new new people, new talent is really one of the largest factors that allowed you to make such large changes to change your culture and change your way of thinking? 

**John:** [00:19:41] The other thing would be, I would say the trust, um, that Ronan CEO and the leadership team Phorest has, um, and their openness to change.

Um, I think that, uh, a lot of other organizations will be quite scared of this type of a change in terms of heavily investing in the product to make it better, just like from experience and talking to the people, you know, would have been very easy to, to not invest, uh, you know, and just leave the software ticking along with bugs and handling the downtime, but it was, it was about the organization and their value, their value is around really helping, helping the salon owners and not spending that time firefighting. 

**Jeremy:** [00:20:28] So it sounds like within two years or so of, of launch was when you, uh, decided to, to make this change. 

**John:** [00:20:38] Yeah. So, um, you know, it's not an, not an easy one to make because you know, it's really hard to find talent.

Um, And we, we, we were lucky to, to really get some, some great people in, and it wasn't about making radical change at the start. You know, it started from foundations. So it was teams like, you know, let's get a continuous integration server going here, guys, and, you know, let's bring all of that. Let's bring back all the broken tests and make sure they're running so that we can have a bit more confidence in what we share.

W we, you know, introduce code review code reviews and pull requests back in into things and a bit more collaboration and getting rid of those pockets of knowledge. Um, you know, reliance on individuals. 

**Jeremy:** [00:21:21] I do want to go more into those a little bit later, but before that, when you were having performance issues or having outages before all these changes, how were you finding out?

Was it being reported by users or did you have any kind of process, um, you know, to notify you? 

**John:** [00:21:41] So the quite commenting was basically the phones, which would light up. Um, there was very, very little transparency of what was going on in the system. It got to a stage where we actually installed a physical red button on support floor, which, uh, texted everyone in the engineering team.

**Jeremy:** [00:22:00] Oh, wow. Okay. 

**John:** [00:22:02] Yeah. 

**Jeremy:** [00:22:02] One of the things that we often hear is when a system has issues like this, it's difficult to free up people to fix the underlying problems, um, due to the time investment required. And as you mentioned, all the firefighting going on, how did you overcome this issue? 

**John:** [00:22:24] So I guess. You know, the beforehand it was, it was a matter of, you know, restart the server.

Let's keep going with our features, but it was really bad stopping to think about, um, you know, what really happened here. And, you know, maybe let's write down an incident report and gather some data, but, well, what actually happened under the hood and a few things, you know, a few questions, key questions could be raised from that.

You know, what are we going to do to stop this from happening again? Why didn't we know about it before the customers and, you know, What were the steps we made to, to reproduce some, actually fix this issue and, and what are the actions that are going to happen and how are we going to track that those actions do happen after, after the issue?

**Jeremy:** [00:23:08] Let me see you. If I understand this correctly, you, you actually did build sort of a process when you would have incidents to figure out okay. 

**John:** [00:23:17] That was the first step I would say. Yeah. So let's figure out what happened and how, and it was just about gathering data and getting information about what was, what was really going on.

So let us identify as, you know, common things that happens that may be usually we would just, you know, restart server and forget but or fail over database and forgotten, you know, everything's not normal and a couple of errors, but as we started gathering that data, we started to see common problems. So maybe, you know, Our deployment processes isn't good enough and it's error prone, or this specific message broker isn't fault tolerant, or the IOPS in the database are too high at this time due to these queries happening.

But after we got that data, you know, uh, and we started really digging deep into the system. We realized that this isn't something that you could just take two days in your sprint to start to fix, uh, go, just coming back to your question on, uh, finding that time to, to fix things where we kind of had to make a tough call.

When we looked at everything to, to say, you know, let's stop feature work and let's stop product work. And. Let's fix this property. 

**Jeremy:** [00:24:26] Okay. Yeah. So, so basically you got more information on, on why you were having these problems, why you were having downtime or performance issues and started to build kind of a picture of, and realize that, Oh, this is, this is actually a very large problem.

And then as a company, you made the decision that, okay, we're going to stop feature development. To make sure we have enough resources to really tackle this problem. 

**John:** [00:24:55] Precisely. And, um, from the product side of things, you know, this was a big, big driving factor in it. You know, we wanted to build all these amazing features to help salons to grow, but we just couldn't actually deliver on them.

And we couldn't have any predictability on the way we deliver them, because because of that firefighting and, you know, cause we were sidetracked so much. There was no confidence in, in release cycle and stability or, or what, what we could actually deliver. So, um, yeah, it was, it was a pretty hard decision for us to make in terms of, uh, the business.

Cause we haven't had a lot of deliverables and commitments to customers and to, you know, to our sales team. So we, we have to have to make that call. 

**Jeremy:** [00:25:36] You were mentioning earlier about how you started to bring in a continuous integration process before you had done that. You also mentioned that there were tests in the system initially, but then the tests kind of went away.

Could you kind of elaborate on what you meant by that? 

**John:** [00:25:53] Yeah, so. As I said, like the kind of the core system was built with a lot of integrity and a lot of good patterns. For example, uh, a lot of integration tests, uh, running against, uh, the APIs, uh, were written and maybe were written against a specific feature, but they were never run as a full suite.

So, um, what would happen was there'd be maybe one or two flaky ones. And, um, you know, because there was no continuous integration server, it was, it was easy enough for a developer to run specific tests for that, uh, functionality that they were were were building. But because there was the CI wasn't there, there was no full suite ran.

So when, when it came time to actually do that, we realized, you know, So, you know, 70% of them are broken, 

**Jeremy:** [00:26:40] so they, they were building tests as they developed, but then they were maybe not running those, uh, 

**John:** [00:26:47] before commit 

or merge

**Jeremy:** [00:26:49] right. And so adding the continuous integration process, having, uh, some kind of build process, really forced people to pay attention to whether those tests were working or not 

**John:** [00:27:01] Exactly. Um, and. Just a kind of a step on from that was, you know, um, a huge delay in getting stuff to test because, because we relied on that onw guy to build stuff. Um, and actually that was, you know, done from a, you know, a little Linux box in the engineering floor, um, which was quite temperamental.

Uh, you'd be quite delayed and actually in even just getting stuff into people's hands and kind of what the core of software development is all about right, you know, Getting getting what you build into people's hands and we just couldn't do it 

**Jeremy:** [00:27:34] Just because the, the process of actually doing a build and a deployment was so difficult when you added the continuous integration process.

Uh, were there other benefits that you maybe didn't expect when you started bringing this in?

**John:** [00:27:50] So, um, I, I guess I mentioned the deployments is a big one. I think that. People started to see real, um, benefit in terms of their workflow. I guess, along with the continuous integration, there was, uh, more, more discipline in terms of, uh, how we worked.

So the CI server introduced a better workflow, uh, for us on a, it helped us see real clarity, uh, in terms of the quality of the system, where, where we had coverage, where it didn't and, um, It also helped us break up the system a little bit. So I mentioned majestic monoliths. So it was actually when, when we went to look at it, there was five application servers sitting in one repo and the CI server and some crafty engineering helped us split that up quite well.

To break at the repo into multiple application servers. 

**Jeremy:** [00:28:45] Hmm. So, so actually bringing in the continuous integration actually encouraged you to rearchitect your application and in certain ways, and break it down into smaller pieces. 

**John:** [00:28:56] Exactly. Yeah. And really it was all about confidence. Um, and being able to test and then know that we weren't progressing.

**Jeremy:** [00:29:03] What do you, you think people saw in terms of the pain or the challenges from that sort of monolith set up that you think sort of inspired them to break it up? 

**John:** [00:29:13] The big one was a bug fix in one small, area of the system meant the whole stack had to be redeployed, which took hours and hours. The other thing would have been the speed of development in terms of navigating around a pretty large code base and the slowness of the test suite to run, which was around 25 minutes.

When we, when we started and got them all green, 

**Jeremy:** [00:29:36] the pain of running the tests and having it possible to break so many things with just one change, maybe encourage people to, to shrink things down. So they wouldn't have to think so much about the whole picture all the time. 

**John:** [00:29:50] Exactly. We started to see, you know, a small fix or a small feature breaking something completely non-related typical example would have been due to a HTTP connection configuration on a client, um, breaking completely on, unrelated areas of the system. 

**Jeremy:** [00:30:06] Okay. One thing I'd like to talk about next is the monitoring. Uh, you mentioned earlier that it was really just phone calls would come into support and you even had the, the big red button, you could press uh, what did you do to add monitoring to your application?

**John:** [00:30:25] That's pretty, uh, important to mention that, you know, we talked about making a decision to stop to down tills  (?)  and start fixing stuff. So that's, that's when, uh, we, we started, you know, looking at the monitoring and everything else, like continuous integration, bringing back tests, but at kind of a key point of, uh, of this evolutionary project was, was the monitoring.

Um, so we did a few things. So we, we upgraded our systems to be using new relic. To help us find errors and it was there, but, um, it wasn't being utilized in a good enough way. So we used the APM  (Application Performance Management)  there. We looked at CloudWatch I mean we introduced watch metrics to help us watch traffic, to help us see slow, uh, transactions.

Um, log entries helped us a lot. Uh, in terms of spotting anomalies in the logs, Pingdom was actually a, a really surprising, um, good addition to the monitoring. Um, it's simply just, just calls any health check, endpoint you want. And. That has some, some nice Slack and messaging integration. It was, that was great for us.

It's helped us a lot. So we did a couple of other things like, um, some small end to end tests that would, um, Give us a kind of a heartbeat to how the system was running. Um, and, and they were also gave us the kind of confidence that we would know about an issue before a customer, being able to allow us to get rid of that red button.

**Jeremy:** [00:31:53] All of these are managed services that, that you either send logs to or check health end points on your system. 

Did you configure them somehow, too text your team or send messages to your team when certain conditions were met or 

**John:** [00:32:11] so we, we, we started with just like a simple Slack channel that would, uh, would send us any kind of dev ops related issues into, into there.

And that that's kind of what helped us change the culture a little bit in terms of being more aware of the infrastructure and the operations. And Pingdom was great for set, setting up a team with people who, who would get notifications for various parts of the system. And, uh, our CloudWatch, um, alarms, we set up a little Lambda function that would just forward on uh any critical messages to text us. 

**Jeremy:** [00:32:44] And before this, you said it was basically just user calls and now you are actually shifting to kind of proactively identifying the problems. Yeah. 

**John:** [00:32:54] Yeah, exactly. There was some small, really small alerts there, but nothing as comprehensive as this. We actually, um, we changed some of the applications. We introduced health end points to all of them. So they would report on their ability to connect to message broker, their ability to connect to a database, any dependencies that they actually needed. We would actually check as part of pinging that endpoint. So, if you hit any of our servers, we, any new or older ones, they would all have like a forward slash health endpoint and that would give you back a JSON structure, uh, and give us a good insight into how healthy that component was.

**Jeremy:** [00:33:33] Yeah. And if there was a problem and you were trying to debug issues, were you mostly able to log into these third-party services, like log entries or new Relic to actually track down the problem? 

**John:** [00:33:46] Yeah. So again, th those services gave us that information, but it would always come back to, you know, being, if you needed to get into a server and a big thing, which we'll talk about is Docker.

Um, we, we don't have SSH access into those servers. So we rely on those third parties to give us that information. But in the past, maybe we would have had to get in and, you know, look at the processes and take dumps, but. With log entries and new Relic, we were able to do that stuff without needing to. 

**Jeremy:** [00:34:17] So previously you might have someone actually SSH into the individual boxes and look at log files and things like that.

**John:** [00:34:25] Exactly. So it's quite easy when you've got one server, but with that, as we'll discuss where you've got many small containers and it's extremely complicated 

**Jeremy:** [00:34:34] Next I'd like to talk about, uh, since you mentioned Docker, uh, how did you make the decision to move to Docker? 

**John:** [00:34:42] So it was something our CTO was really aware of and he really wanted us to explore this.

The big benefits for us was that shift in mindset of one guy not being responsible for deployments, but us actually developing and using Docker in our day to day workflow and the cost implications as well. The fact that we could, instead of having that say eight X large, we could have. Running one application server.

We could have 12 containers running on much smaller containers running on an EC2 instances. So it was that idea of being able to, to maximize, uh, CPU and memory. What was a huge, huge benefit for us that we, we, we saw. 

**Jeremy:** [00:35:24] So the, the primary driver was, was almost your. AWS bill or your 

**John:** [00:35:30] Big time. Yeah. Portable applications that, um, you know, w had much less maintenance. We didn't have to go in and worry about it because we had a, I guess, a. We mentioned this earlier, like these kinds of silo tech stacks, we didn't need to worry about a Ruby environment or PHP environment or a Java JVM install. It was just the container.

And that was a hugely big, an important thing for us to do and really kind of well thought out by our CTO at the time. 

**Jeremy:** [00:35:59] So, so you mentioned like Ruby containers and JVMs and things like that. Does your application. I actually have a bunch of different frameworks and a bunch of different languages?

**John:** [00:36:09] Yeah. So, um, as we split out the, that monolith, uh, we also, I guess, started building smaller domain specific, not micro I'd say kind of uh, services responsible for areas of the system, uh, our online booking stack. So if you go to any of our customers, um, you know, you can book a and their point of sale system in the salon, but you can also book on your phone and we have a custom domain for every one of those salon. So it's like phorest.com/book/foundationhair.

Um, if you click on that, you're going to be brought to the online booking stack, which is a, a rails app actually in a, an Ember, Ember JS frontend. So, um, the system, as we started splitting it apart became more and more distributed and Docker was great for us in terms of consistency. And that portability particularly around different text stacks. 

**Jeremy:** [00:37:01] Migrating to Docker, made it easier for you to both develop and to deploy using a bunch of different tech stacks.

**John:** [00:37:08] Exactly. 

**Jeremy:** [00:37:09] When running through your CI pipeline, would you configure it to create an image that you would put into a private registry such as Amazon's elastic container registry? 

**John:** [00:37:18] Yeah. So we made the mistake of building and hosting our own registry at the start. Uh, we quickly realized the pain and that around three, four months in where I'm actually at the same time as Amazon released the ECR.

So I guess the main reason we did that ourselves was because we were early adopters and we pay, paid a little tax on that, but we did, uh, we moved to ECR. So. Our typical application kind of pipeline is uh build unit tests, maybe integration, acceptance tests, build a container. And then some of those applications, they run acceptance tests against the container running on the CI server, uh, push, push to the registry.

And after it's pushed to the registry, then we would configure deployment and trigger it. 

**Jeremy:** [00:38:02] Do you have a manual process where somebody watches the pipeline go through and you make the call to push or not? Or is it a automated process? 

**John:** [00:38:13] Automated. So, um, we built a small kind of deployment framework again, because we were early adopters of Amazon's ECS, uh, their container service.

Uh, so we built a small, um, deployment stack, which which allowed us to, to essentially configure a new services in ECS and deploy new versions of our application through CI to our, uh, ECS clusters. So it was all automated using an infrastructure as code solution, such as cloud formation. So when we were in looking back at the problems in the old good old days, uh, you know, we seen that one was, you know, uh, things were just configured on the AWS console.

And we, we knew we needed infrastructure as code and we needed a repeatability and the ability to recreate stuff. So we, we use cloudformation and essentially what face something very similar to terraform. Um, and we do use Terraform for, for some of our managing our restaurant clusters on some other things.

**Jeremy:** [00:39:16] Okay. So you maybe initially moved from having someone manually going in and creating virtual machines to more of a infrastructure is code approach. 

**John:** [00:39:27] Exactly. Yeah. 

**Jeremy:** [00:39:28] You, you had mentioned that one of the primary drivers of, of using Docker was performance, did you start creating performance metrics so that you knew how much progress you were making on that front?

**John:** [00:39:41] Yeah, so essentially that the effort to kind of make our infrastructure more reliable it's it was a set as kind of a set of steps to get there. And we started with API level testing to make sure that anything we change under the hood, it didn't break the  functionality. And we also wrote a bunch of performance tests, particularly around pulling down appointments, creating appointments and sending large, large volumes of messages.

We, we knew we couldn't have any regressions there. So. We use gattling to do those performance tests. And we, we would run that from continuous integration server and we do various types of soak testing to make sure we weren't weren't taking any steps backwards. 

**Jeremy:** [00:40:23] So each time you would do a deployment, you would run performance tests to ensure that you weren't getting slower, or you weren't having any problems from the new deployment.

**John:** [00:40:34] Yeah, I would say though, that like, uh, this kind of effort and we called it project Darwin internally, this effort to kind of. It had a few goals, but it was all about, you know, becoming fault-tolerant being more scalable, reducing Amazon costs. And during project Darwin, when we, we didn't just move our 1200-1500 salons we didn't just drop them and move them to docker.

There was so many changes under the hood that these performance tests were key to giving us, uh, a pulse on how we were doing. But, um, I guess when we were done with project Darwin and every,  everything was onDocker  and, and everyone was much, much happier. Um, we, we just, we run those performance tests, ad hoc and as, as part of some release pipeline.

**Jeremy:** [00:41:21] Hmm. Okay. So initially you were undergoing a lot of big changes and that was where it was really important to, uh, check the performance metrics with, with every build. 

**John:** [00:41:32] Exactly. Yeah. 

**Jeremy:** [00:41:33] Uh, what were some of the, the big challenges? Cause you mentioned you were changing a lot of things. What were some of the big challenges moving your existing architecture to Docker and to ECS?

**John:** [00:41:47] There was a couple. The biggest there's two huge ones. So one was state. Getting state out of those big servers was extremely hard. We needed to re remove the level two cache because we need, because we needed to turn that one server into smaller, load balanced containers. We needed to remove the state because we didn't want somebody in one term computer terminal, fetching our appointments, and then on their first go mobile app looking at different data.

So we had to get rid of state. And the challenge there was that MySQL performance just wasn't good enough for us. So, um, we actually had to look really hard at migrating to Amazon Aurora, which is what we did again, coming back to cost. Uh, Aurora is much more cost-effective in terms of the system beforehand was provisioned for peak load.

So we, we would have provisioned IOPS for Friday afternoon. The busiest time that the salon was using the system. And we were paying for the same amount on a Sunday night. Compared to Aurora where you're, you're paying for IOPS and the additional benefits of performance around how Amazon rebuilt the storage engine there.

So that's the caching side of things. The other big, big challenge was the VPC. So when you needed to get all of our applications in, into a VPC to to be able to use the latest instance types on Amazon, uh, and also for our application to be able to talk security to Aurora database. So those two are definitely the biggest challenges with the MySQL setup.

**Jeremy:** [00:43:19] It sounded like you had to pay for your peak usage, whereas with Aurora it automatically scales up and down. Is that correct? 

**John:** [00:43:29] Um, no. You're actually charged per read and write. So that would be the big difference.

**Jeremy:** [00:43:34] Oh I see. Per read and write. Okay. So it's just per operation. So you don't actually think about what your needs are going to be.

It kind of just charges you based on how it's used. 

**John:** [00:43:45] The other new really nice thing was, uh, looking back at our incident reports, a really common issue would have been, Hey, the database has run out of storage and Aurora does actually autoscale its storage engine. 

**Jeremy:** [00:43:56] You mentioned removing state from your servers and you, you mentioned removing the level two cache, can you kind of explain sort of at a high level, what that means to those who don't understand that? 

**John:** [00:44:10] Sure. So in the Java world, when you have an ORM framework like hibernate, essentially when you create a database, that cache will store that data, um, in its level two cache. And what that means is that it doesn't need to hit the database for every query.

And that's the, that was the solution for, for Phorest as we were in that MVP slash early days. But it wasn't the solution for us to become fault-tolerant. 

**Jeremy:** [00:44:39] So it would be someone makes a query to an ORM in this case. It's and it's hibernate and, uh, on the server's memory, it would retrieve the results from there instead of from the database.

**John:** [00:44:55] Yeah, exactly. Okay. And that's what I was coming back to around, um, creating an API for a list of appointments. If you had two servers deployed with, with them using an L2 cache, you would get different state because cache, 

**Jeremy:** [00:45:12] you put a different cache in place, or did you remove the cache entirely? 

**John:** [00:45:17] So we removed that cache entirely, but we did have a rest cash, which is, was memcached and that's distributed. And we use cache keys based on, uh, entity versions. So that was distributed and, and worked well with multiple containers behind a load balancer. 

**Jeremy:** [00:45:34] So you removed the, the cache from the individual servers, but you do have a managed Memcached instance that you use. 

**John:** [00:45:42] Yeah, exactly. And getting rid of that level two cache.

Our performance tests told us that MySQL just wasn't performance enough. Whereas Aurora was much better at handling those types of queries, some large joins. It was a big, big relational database. 

**Jeremy:** [00:45:58] So we we've talked about adding in continuous integration, monitoring performance metrics, uh, Aurora Docker. Did any of these processes require large changes to your code base? 

**John:** [00:46:13] To be honest, not really. It was more of a plumbing things together and a lot of orchestration from a human point of view. So, um, people being aware of how all this stuff works and. Uh, essentially making sure that we all knew we're on the right page.

I don't like the biggest, uh, piece of engineering and coding work was the deployment and infrastructure script. So provisioning the VPCs writing the integrations with ECS, uh, that, that sort of thing. But, um, in terms of actual coding, it wasn't too invasive. 

**Jeremy:** [00:46:47] I think that's actually. A positive for a lot of people, because I believe there are people who think they need to do a big, uh, rewrite if they have, you know, performance problems or problems, keeping track of the status of their system.

But I think this is a good case study that shows that you don't necessarily need to do a rewrite. You just need to put additional processes and checks in place and, um, maybe change your. Deployment process to kind of get the results that you weren't 

**John:** [00:47:21] It's about the foundations as well. If you have some really strong people at the start who, you know, pave some good uh, roads there in terms of good practices, like just for example, a really good, uh, Database change management set up some good packaging of the code.

Really good packaging of the code. So it was quite easy for us to slip out five services from that big monolith. It's about the foundations at the start, because it would be quite easy to, to build an MVP with some people who raised, you know, 1000 line PHP scripts and the product works and that's a different case study because, you know, you CA you can't fix that essentially.

**Jeremy:** [00:48:04] Right? So it's because the original foundation was strong that you were able to undergo this sort of transformation 

**John:** [00:48:12] truly yeah

**Jeremy:** [00:48:13] adopting all of these processes, did they resolve all of the key problems your business faced? 

**John:** [00:48:21] When we, when we look back and we see that, you know, all of our systems are running on docker, we see a huge cost benefit.

So uh that problem was certainly solved. We, we were able to see issues before our customers, so we have better transparency, uh, in the system. No longer was, uh, were we dependent on one big server uh, a 1000 customers were no longer dependent on one big server. Um, so it meant that we had really good fault and we do have really good fault tolerance on, on those containers.

If one of them dies, ECS will literally kill it. Uh, bring up a new one. Uh, it will also do some auto scaling for us. Say on a Monday morning, it will, you maybe have eight containers running, but on a Friday, maybe it'll auto scale to 14. So that's been ground bre breaking for us in terms of how we work. We went from shipping monthly to quarterly from between monthly and quarterly to, to daily.

And something I use as a, uh, a team health metric right now is, is our frequency of deployment. And I'd say we're hitting about 25 deployments a week now, compared to the olden days is, is, is great. We always want to get better at it. I would say that those have been really amazing things for us, but also in terms of the team, it's, it's a lot easier for us now to hire a new engineer, um, bringing them in because of this consistency.

And also, um, I guess, uh, we're not relying on these pockets of knowledge anymore. So we, again, around hiring it's, it's a lot easier for someone to come into the system and, and know how things work. And I think in terms of hiring as well, when you talk about the kind of setup it's, uh, it's, you know, you know, there's some, some good stuff happening there.

**Jeremy:** [00:50:10] It sounds like you have a better picture in terms of monitoring the system, you brought your costs down significantly. The deployment process is much easier. The existence of the containers and ECS is kind of serving the purpose of where people used to have to monitor the individual servers and bring them up themselves.

But now you've sort of outsource that to Amazon, to take care of. Uh, does that sound, does that all sound correct? 

**John:** [00:50:42] Yeah. Spot on. 

**Jeremy:** [00:50:43] And I find it interesting too, that you had mentioned that improving all of your process to use actually made it easier to bring new people in. And that's because you were saying things are now more clearly defined in terms of what to do, rather than all of this information kind of being tribal in a sense.

**John:** [00:51:06] Yeah. Like a typical example will be like, Hey, uh, let's redeploy this, uh, bug fix. And so previously, you know, it might be a capistrano deploy or, uh, you know, oh you need to get SSH keys to this thing and, you need to log in here and you need to build this code. On this local machine and try and ship it up.

And that just all goes away. Um, particularly with Docker on that, that continuous integration pipeline is just, it sets a really good set of standards and things that people should find quite easy and repeatable. 

**Jeremy:** [00:51:40] And, uh, so now in terms of deployment, you can use something like cloud formation and you have the continuous integration process that can deploy your software without somebody having to know specifically about how that part works.

**John:** [00:51:58] Exactly. So I would say if we wanted to create like a new service responsible for some new, new functionality in Phorest, uh, say a spring boot application, a Java application. They can simply provide a Docker file and get that deployed to dev staging or production with, I would say 10 lines of YAML configuration.

So you could go from initial set up of a project to, to production in a day. If you wanted to just. Zero friction there I would say. 

**Jeremy:** [00:52:29] It really makes the onboarding a lot easier then 

do you think your team waited too long to change their processes? 

Or do you think these changes came at just the right time? 

**John:** [00:52:42] I would say if we waited any longer, it could have been detrimental to, to, I guess, the health of the business.

I think that the guys did a great job in terms of getting us to a certain point. Well, we would have risked technical decay, I would say. And, uh, what kind of, uh, really, uh, harming the organization. If I had gone any further, I would say it was, it was a lot of work to do this and it could have been easier if.

If we had paid more attention to technical debt and making the right decisions earlier on. So maybe saying no to that customer who wants a bespoke piece of functionality, well, you have to do what you have to do. 

**Jeremy:** [00:53:24] So, so you would say maybe identifying earlier on just how much the current processes were causing you problems.

If you had identified that earlier, um, you think you might have made the decision to try and make these changes, uh, at an earlier time. 

**John:** [00:53:44] Yeah. So the guys earlier were, were making really good decisions, but maybe they didn't have the experience for, you know, higher scale at the scalability solutions and systems.

So it's, it's about hiring the right people at different stages of where the product is evolving. I would say. 

**Jeremy:** [00:54:00] Given what you've gone through with the migration of Phorest, what advice would you give to someone building a new process? What, what can they do to keep ahead of either technical debt or any of the other issues you face?

**John:** [00:54:18] I think it's about how it's, it's actually, uh, a people, um, and cultural thing along with tech decisions. So. Everybody needs to be really aligned in terms of these decisions that they're making, rather than letting people go on an individual basis. I think there needs to be good leadership in terms of getting a group of people thinking the same way.

I reckon the technical currency is, is extremely important. And as your system grows, you need to be able to, to look, look back. And identify areas of pain and by pain, I mean, you know, speed of deployment, uh, speed of development, ability to adapt and change your software. So if you notice that a feature that used to maybe take a week has now taken two weeks.

You know, you probably need to take a really hard look at that area of the system and figure it out. Could it be simplified? Um, and why, why is it taking too long? 

**Jeremy:** [00:55:21] Basically identifying exactly where your pain points are, um, so that you can really focus your efforts and, and have an idea of what you're really going for.

**John:** [00:55:31] Yeah. You need to build, um, an environment of trust. And I will also say that you need to be able to.To be able to be calm, confident, and okay with failure in terms of take taking risks sometimes and saying no to features and customers to be able to, to push back on, on leadership and make sure that you're, you're really evolving the system the right way.

Uh, not just, uh, becoming a feature factory. 

**Jeremy:** [00:56:01] Yeah. It's always going to be a kind of balance on, you know, how much can you pull back, but still stay competitive in whatever space you're in. 

**John:** [00:56:12] Yeah. So what, what we're doing right now based on those lessons is we tried to do like a six to eight week burst of work.

And we would always try and take a week or two wiggle room between that and starting something new to look back at what we just built and make sure we're happy with it. But also look at our, our, our technical backlog and. See if there's anything there that's really pain, you know? And just, even for example, this week, we, we noticed an issue with a lot of builds failing on our CI because of, uh, how, how it was set up to push Docker images.

So, okay. Usually they would fail and that was actually a real pain point for us. Just over the last couple of months, because maybe a deployment, which should take 20 minutes was taking 40. Cause you'd have to re trigger it. So that's just like, that's an example of us looking at what, what was high value and making sure we just fix it before we start something new.

**Jeremy:** [00:57:08] So making sure that you don't kind of end up in the same situation where you started, where. These technical issues sort of build without people noticing them instead kind of in shorter iterations, doing sort of a sanity check and making sure like everything is working and we're all going in the right direction.

**John:** [00:57:27] Yeah. It's about the team. And I mentioned before, it's about, you know, the leadership and a group of people together. Talking through common issues and, you know, maybe meet, meet every two, three weeks. Talk about some key metrics in the system. Why is it this too high? Why is this too low? You know, you can through

kind of through your peers you can really see the pain points and, and they'll, they'll. More than likely tell you them. 

**Jeremy:** [00:57:51] When you look back at all the different technologies and processes you adopted, did you feel that any of them had too much overhead for someone starting out? What was your experience in general?

**John:** [00:58:04] So some people just didn't like doing code reviews. Some people just really just felt that. They could just push, push what they needed and that it was almost a, a, a judgment on them in terms of the code review process, which it totally wasn't. I would say, uh, some people found Jenkins and continuous integration a bit, you know, what's the point.

And so we, we had had some, you know, some pain points there. Um, but as we got to Docker, as people seeing the benefits of, of these things, you know, less bugs going into production, uh, less things, breaking people, being able to go home nice and early in the evening and not be woke up in the middle of night with, uh, you know, an outage call.

Those were all the, the, the benefits, and that's reaping the rewards of, of thinking like this. 

**Jeremy:** [00:58:56] Your team was bringing on a bunch of new things at once. What was your process for adopting all these new things without overwhelming your team? 

**John:** [00:59:06] So it was starting at the foundation. So the continuous integration, the code reviews where we're incrementally brought in and we had regular team meetings to discuss pros and cons.

And it was really important for people to, to input on those things rather than to, to, to just implement them. They would have failed if we hadn't done it like that. It took time. I know it's still, I would say we're still not in a perfect world, but it's about group, group consensus and making sure that everyone everyone's bought in to what we're trying to achieve.

**Jeremy:** [00:59:39] So basically getting everyone in the same room and making sure they understand what exactly the goal is. And everyone's on the same page. 

**John:** [00:59:47] Yeah. So we tried to make a big efforts, uh, particularly for people who are working remotely to get them all in the same room. Once a quarter, we talk about our challenges, talk about our goals, talk about our values and make sure we're all on the same page.

And sometimes we tweak them and you know, that's how we feel. It's best to do it. 

**Jeremy:** [01:00:09] Finally, I want to talk about what's next for, for Phorest. What are the remaining pain points you have now. And what do you plan on tackling next? 

**John:** [01:00:20] So right now we're on 4000 salons on our platform. We're really happy with the state of the infrastructure to get us to maybe 8000-1000 salons, but we need to be really conscious of the company's growth and our goals.

So we need to make sure that we can scale at a much bigger level. And we also need to make sure that our customers aren't affected by, uh, our growth. We were looking at serverless for any kind of newer pieces of the product to see if they can help us reduce costs even more and, and help us stay, stay agile in terms of our infrastructure and how we roll out a couple of years ago, when we launched into the USA, we noticed we, um, It doubled our overhead in terms of infrastructure, operations, and deployment.

And as we grow in the U S we, we need to be really conscious of not making eh any, um, I guess, uh, mistakes from the past. 

**Jeremy:** [01:01:15] So you're mostly looking forward to additional scaling challenges and possibly addressing those with serverless or some other type of technology. 

**John:** [01:01:27] Yeah. So, um, one area in particular will be our SMS sending.

So that's kind of. A plan for the next six to eight months would be to make sure that we can continue to scale at the growth rate of SMS and email sending, which is, is huge in the platform. 

**Jeremy:** [01:01:44] Um, you said so far, you've been experiencing 30% growth year over year. And you said when you moved to the U S you actually doubled your customer base?

**John:** [01:01:56] I'd say we doubled our, uh, overhead in terms of infrastructure. managing  (?) deployments. We we're still very early stage in the US and that's our big focus for the moment. But as we grow there, we, we need to be, I guess, more operationally aware of, of how it's, how it's going over there. There's a much bigger market. 

**Jeremy:** [01:02:17] To kind of cap it off.

How, uh, how can people follow you on the internet? 

**John:** [01:02:21] Sure. So you can grab me on Twitter at Johnwildoran , J O H N W I L Doran. And if you ever wanted to reach out to me and talk to you about any of this type of stuff, I'd love to meet up with you. So feel free to reach out.

</div>