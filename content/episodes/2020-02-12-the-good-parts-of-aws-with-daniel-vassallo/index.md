+++
title = "The good parts of AWS with Daniel Vassallo"

description = "Daniel discusses how he chooses AWS services and his thoughts on the culture and future of Amazon"

[extra]
episode_url = "https://pinecast.com/listen/2f357754-6f26-45f5-afde-bfb6ea06b588.mp3"
+++

Daniel is the co-author of the book "The Good Parts of AWS" and previously worked at AWS on the CloudWatch team.  He left last year after over 8 years at Amazon to work on his own projects.

He's currently working on an end-to-end encrypted user database SaaS called Userbase.  Daniel is also openly sharing his experiences building an audience, writing a book, and building Userbase on twitter.

We talk about:
- Why AWS has so many services
- His default AWS stack and how he chose it (Dynamo, SQS, S3 and EC2)
- Why he uses EC2 over ECS or EBS
- The difference between SQS and Kinesis
- The future of AWS

### Daniel Vassallo
- [Personal Site](https://danielvassallo.com/)
- [@dvassallo](https://twitter.com/dvassallo)

### Other Links
- [The Good Parts of AWS](https://gumroad.com/l/aws-good-parts)
- [Userbase](https://userbase.com/)
- [Only Intrinsic Motivation Lasts](https://danielvassallo.com/only-intrinsic-motivation-lasts/)

---

### Transcript

You can help edit this transcript at [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy**  Today I'm talking to Daniel Vassallo about his book, the good parts of AWS. Daniel, thank you for joining me on software sessions.

**Daniel** Thank you, Jeremy. Thank you for having me.

**Jeremy** You wrote a book called the good parts of AWS, which suggests there are bad parts or parts most developers shouldn't look at. How did we get to this point? How did we end up with so many services that developers don't even know where to start?

**Daniel** There was so much popularity in the enterprise world, that it doesn't speak to the developers anymore. Like I remember I used to use AWS at the very beginning more than 10 years ago, where the website was super simple.

There were like four services. If I remember correctly, code examples, if not on the front page, like a quicker way where you can as a developer understand what you could use and what value you could get. 

But I think nowadays, even me, like I go to the AWS website and I barely understand because it's speaking to CTOs of big Fortune 500 companies right lots of buzzwords and jargon and blockchain and machine learning, and it's daunting. 

It's very hard for somebody to go to product pages and understand what options are available.

Not to mention that there are many many ways of doing the same thing. Like if you want to have a database, I think on AWS there are five different options. I think AWS also doesn't do a great job explaining the differences. 

Like, you know this is good for this so there is still a gap in terms of how to think about things.

I don't think that there are bad parts I think there are less important parts that I sort of decided to pick. And by the way, it doesn't even mean that the things I didn't cover in the book are not worth looking at or not worth using.

I try to pick the things that are definitely worth looking at. I, that's nearly every non-trivial application would likely benefit to have to at least consider these things. 

And they are only the things I had firsthand experience with. So I tried to stay away from things that I didn't know much about and just write about what I think are the most important parts.

**Jeremy** Where is your background coming from? What kinds of applications were you building?

**Daniel** So before I joined Amazon, before, so I joined Amazon in 2010. So over nine years ago. 

I was a full stack developer. I was working in a couple of small startups where I was building applications frontend backend databases the usual thing.

I was part of the CloudWatch team, which is the monitoring product in AWS. And sort of the main focus was on backend web services. So basically our interface tended to stop mostly with the API we're just building, these web services that stored metric data log data about how applications are working.

I tried to in the book focus on things that are more broader than specific backends or database focus or front-end focused. Not every application would need to use everything, obviously right? 

I like this concept of a default choice, which is a bit of a subjective perspective. I admit but, for example: If I needed to store files somewhere in the cloud my default choice would be to use S3 right?

It's just super hard to beat in terms of price per storage or availability or the durability. I like to think about this heuristic where I have default choices where I would just default to some things unless I really believed that this default choice wasn't good enough for me.

I try to present ideas like that. Like if you want to have a server in the cloud, EC2, is a perfect case, much more than Lambda and other things that are much more limited than a full server. Same with DynamoDB. 

I think Amazon does it a disservice by describing it as a database. I like to think of it more like a data structure that is significantly simpler than what we tend to expect from a traditional DBMS where you have lots of features, that you would be disappointed if you expected them from DynamoDB. 

I think DynamoDB is much closer to something like Redis than it is to MySQL. If you think about it that way, that makes it much easier to see whether it fits your needs or not. Like, can I fit all my data inside a very primitive data structure that's highly durable and highly available?

If yes, great, it's a good default choice. But if you need stored procedures and triggers and joins and subqueries that run close to the data then you're going to have a hard time. You can probably find a way to work around these limitations, but it's probably going to be very hard to use.

I go through I don't remember exactly how many services that I cover I think a dozen with this high level perspective on how you think about things. Which, I think is a simpler way to reason about them than just reading the Amazon product pages.

**Jeremy** Right. Which is, when you go to the Amazon homepage and you click that button that shows you all the services. It's kind of insane, right?

**Daniel** It's daunting. Yeah. It's daunting. And that's the problem you see a databases category and then you see six things under it and you click on all of them in a new tab. And it's so hard to understand what's the difference or which one you should choose and things like that.

**Jeremy** You had mentioned DynamoDB and how you felt like it's more of a data structure than a database, and I'm curious, why you decided to choose that to be your default data store rather than something like RDS, some kind of relational database store.

**Daniel** I try to have a slightly more nuanced take. I would say DynamoDB, is a good thing to consider as a default. I would basically ask yourself, can my data fit? Because I think if it fits, DynamoDB spares you from lots of burden and operational things that you would have to deal with even if you were to go with RDS that are things like setting up backups and making sure that you're not running out of memory and the primary keys and you know that the indices are fitting in memory and IOPS and things like that.

DynamoDB abstracts everything away from you, it's really great. For many web applications and web services, the database tends to be one of the most challenging things to keep running.

DynamoDB can be very helpful, but I think the important thing is it depends. Two things to think about is whether you can live with this access pattern of just reading off a b-tree. And the pricing as well, which I touch on in the book sometimes the pricing can be a significantly more expensive.

That can be cost prohibitive depending on how you're using it. If you realize that DynamoDB doesn't make sense for your case, then I think, yeah, RDS is a perfect example. I didn't write too much about RDS in the book because I don't have recent experience.

I used RDS At Amazon, in 2011 so a very long time ago. And to be honest, this was quite a terrible experience. We had all sorts of problems, from sort of databases getting stuck like for 45 minutes and not being able to do anything with them. Failovers happening randomly and not failing over like all these kinds of things that you don't want to happen with the database.

But to be fair, I believe many of these things have improved significantly. I would feel comfortable using RDS if I needed it. But I don't have the first hand experience to be able to sort of highlight any quirks or any other things that I am missing. That's the only reason why it doesn't appear in the book.
I didn't feel I had the right to write about it.

Something that I think is a bit risky in the RDS world is Aurora. It's fascinating technology. I really like this idea where data and the compute are separated.

When you have a typical database you scaled everything together. If you wanted more space or more memory or more CPU, everything could go together. 

One of the problems ends up being like if you have a database that has lots of data but it's not running, you have sort of these disproportionate resources that are under utilized or they're bottlenecked and things like that.

Aurora manages to keep the data separate from the compute and running a query can spin up more compute on demand and things like that. But from what I heard again, this is mostly heard second hand, is that one of the things Aurora tried to do is be MySQL. And I don't know if with other databases as well. The problem that happened is that the behavior is not really that compatible but the interface is right? The queries are the same but for example, you might expect that adding a column to a table in MySQL would be harmless while in Aurora it might lock up. This is not a real example, but things like this right?

I think there was a Reddit post a few months ago where someone highlighted lots of things like this which are quite scary. Things when you're using MySQL they're non-disruptive but when you use Aurora they ended up being very catastrophic or very problematic things.

And I think this is a problem with immature technology, right? I mean, MySQL has been around for, I don't know, for 20 or more years, millions of users running it every day millions of hours of usage. Aurora's just a couple of years old. 

It's tries to be a drop in replacement for a database that has been around for like two decades at least. And it's just a very hard thing to do. In general I tend not very tempted to just jump into the latest and greatest by default. 

I like the devil that I know, even if there are problems. I think there's lots of value that many people underappreciate and many people in tech tend to underappreciate the test of time. The more software gets used the better it gets typically because the more issues get revealed the more bugs gets fixed and things like that.

**Jeremy** When I think of the tried and true, I think of things like MySQL or Postgres so it's interesting that AWS has been around so long that cloud only services like DynamoDB and S3 are now in that category.

**Daniel** I think that's true for a part of them. I think that's the trap sometimes because I completely agree DynamoDB and S3 I would put them into the category of the tried and true. 

S3 because it's used by everyone. DynamoDB is used extensively within Amazon, and I think even outside it's decently popular.

But there are probably another hundred or so services I would definitely not fit in that category. Amazon launches dozens of new services over the year right and many of these I've seen it myself that just get launched with very limited usage like the first users are almost literally the first users.

I wouldn't necessarily avoid them at all costs I think it would be very prudent to treat them differently than other things. Because if they're offering something particularly valuable for what you're trying to do, I think they're still worth considering.

What I think is potentially harmful is the idea that. Newer is better just automatically, which I see sometimes happening in the databases and compute as well. I think there's a bit of this problem even in the Lambda API gateway and that kind of thing there seems to be this impression that the default should be that if I'm hosting a web application it should be on Lambda which I think is an insane default. 

I actually like Lambda at lot, but I think, it's over utilized for what it is intended to do.

And actually I'm very optimistic about the serverless future where we're building web applications without having to think about the operating system and the hardware underneath it. So lots of potential. But if you're building something today, you have to look at the options that exist today.

And there's still lots of issues with running a sophisticated web application, not some trivial, you know, hackathon project right, completely on Lambda and API gateway in my opinion.

**Jeremy** You were talking earlier about, Aurora and I wasn't even aware that the internals like you were saying, you're giving an example where you add columns or you make some kind of change and the behavior of Aurora may not be the same as the actual open source project. And so I wonder when people are choosing services from AWS for example, whether it's RDS or it's ElastiCache, or these managed services that AWS offers, how can people find out or determine if it really behaves the way that they're going to expect in terms of the open source product?

**Daniel** I think you can read between the lines a little bit and I think AWS makes it not super clear, but it's not completely obscured. And there are two types of managed services. The ones that AWS literally takes the open source projects and and hosts it as is.

And this is the typical MySQL running on RDS. To be honest, I don't know if there are some minor changes to it. There might be a but I wouldn't expect them to be a significant. Sometimes there are limitations, sometimes you might not be able to change some settings and this is common. 

For example, in the elasticsearch hosted service there's lots of things that you can't modify if you choose them, but these are easier to reason about because there's typically a limitations page in the documentation.

But then there's another category of services. DocumentDB that implements the Mongo DB interface. These are not the real thing. Amazon built a brand new piece of technology and just made the API compatible with it. So in the latter category you can't expect the test of time that would have exercised the open source technology to apply to these things. It's because it's literally just a different black box behind it.

I think you can tell. It's not immediately clear just from reading the names of the products. But I think if you dig a little deeper, you can tell whether this is actually the old thing or it's not. Again, like I am not saying that for example, DocumentDB or anything is necessarily bad, but they're new tech that I think it's safe to assume that when they were launched, almost nobody used them.

I'm sure though there would have been a few beta testers and whatever. But this is far from MongoDB which has been around, I'm sure it has problems as well, but it's different. First of all. Many of its problems are well known, and if you are to Google them you'll probably find behaviors and workarounds and things like that, um, or many have been fixed.

**Jeremy** You were talking about how you have this heuristic for deciding your default choices, deciding which technologies are stable and which are not. How do you go through that process of deciding what technology you should choose? Like to give you an example, you were mentioning how S3 has been around a long time.

Amazon builds a lot of their products based on top of it, as do many other people. So that kind of makes sense. But with something like say Lambda, which is much more recent, you know, what do you evaluate and what gives you the confidence to decide that? Like this should become a part of my default stack.

**Daniel** Yeah. I think, and this is the reason why this is subjective. One of the main things for me is my own familiarity. I give it lots of weight. 

If I've used it before, I know how it works. I know it's problems. I know where to look if I need help. I give that lots of weight.

Basically, my ultimate test is I try to optimize for choices that are very unlikely to fail me. Taking S3 as an example, if I wanted to store something safe S3 is just perfect for me. I understand it. I understand its performance. I know how it behaves and it's super unlikely that I'm going to find something surprising that it turns out that actually I thought I was saving everything, but nothing got saved or that I thought I might be able to download things at a hundred megabytes a second, but it turns out to be a one megabyte. It's unlikely that I'm going to find weird things. I think that's important. 

In addition to that, I think when it's lack of my own familiarity, I'd give weight to again, like we said before, just a test of time, right?

It's whether something has been used for a long time that I get lots more confidence if something has been adopted especially for something important, like, hosting the application or databases or storage. These are not hard rules because if they were nothing new would ever be used, so, uh, I think this is just a way of thinking and I think it's still worth looking at new things as they come out and keeping an eye and trying things out. But I think this, this sort of approach helps you be more confident when you're making choices that are not to get the situation where there's infinite number of choices sort of make it very daunting cause that's another problem that tends to happen. This is one way of helping you make that choice.

**Jeremy** Yeah. And so like, one thing I'd like to kind of go back to is, you know, we were talking about uh DynamoDB and S3. What are some examples of the kinds of things that somebody would choose to store in S3 versus in DynamoDB or in RDS?

**Daniel** It's funny because DynamoDB and S3 are actually very similar in terms of the interfaces they both have sort of a put and get by a key values API. And they both allow you to sort of list things in order, you know, in S3 by key that you get them in order.
And DynamoDB by the range key I think you nearly can use them interchangeably. I mean, it's probably not exactly true but for many cases. 

I think the main difference between the two, like from a very sort of technical point of view is a matter of performance and price that you're looking at.

Where you're looking at that situation where, the storage cost for S3 is significantly cheaper, I think it's like a tenth of DynamoDB. Not to mention that sometimes you can compress even better in S3. But the cost of writing something, the operation cost is significantly higher in S3.

I think it's a cent per thousand writes or something like that, right? Where in dynamo it's significantly less expensive. Then there's the performance aspect of that, which S3, it has a higher time to first byte of 20 to 50 milliseconds. Whereas in dynamo it can be sub 10 milliseconds.

And, then the other thing is when you're reading something in bulk out of S3, it's significantly faster you can get download speeds of close to a hundred megabytes a second from a single thread. And you can use as many threads as you want. Whereas in dynamo, we have to scan over things and paginate and just even the round trips.

Um, I never really measured the maximum throughput you can get out of DynamoDB, but it's significantly smaller than dynamo. So I think between those two, it's literally a matter of which one makes most sense. Like am I storing lots of small, tiny things that I need to read out only in small segments or am I storing bulky but fewer things that I need to read out like in bulk as fast as possible.

So sort of helps you make the decisions. I think in terms of availability and durability, they're pretty much equivalent. They're both the kinds of services where if you write something, you can for all practical purposes, expect, to never lose it. They're both highly available. You know, like any service, they occasionally experience a blip of issues, but they're one of the most reliable services that AWS has. 

RDS is a bit different. I consider RDS, in a different category than those two, because again, Dynamo are still just data structures in the clouds. They are just this very primitive thing, just two ways of reading and writing data. Databases like RDS, they're just a different machine right where I think they make sense where you need their sophistication, right? Where you need sort of the ability to right sophisticated SQL queries and do joins and do aggregations and that's the nice thing about them that is that any SQL expression that they can use, whether it's when you're using something primitive, uh, like S3 and dynamo, you have to build those, querying capabilities yourself in your application if you want to offer them. And so you're getting a lot more from using RDS, but you're getting a lot more to manage as well. But again, like dynamo, and S3 are two types of services where they're close to zero maintenance as much as possible S3 in particular even more, although even Dynamo is  almost there. Um, I think RDS is far from that. So it's something that you would have to monitor, have alarms, make sure that it hasn't gone down. Cause if it turns off it's your problem, and it's not Amazon. There is not somebody from Amazon that's going to wake up and fix it for you you know? 

Whereas if S3 has an issue, which happens very rarely but if it were to happen, someone from Amazon will wake up and fix it. So that's the main difference between the two.

**Jeremy** Yeah. Using a relational database, it can be a lot more powerful in terms of acquiring capabilities and the things that you can push off to the database rather than your own application. But the trade off you're making is that you have to come up with your own backup solution.
You have to come up with how you're going to scale up the database in terms of telling Amazon, Hey, I need more memory, or I need more compute, that kind of thing.

**Daniel** Yeah. Not only did that, even knowing whether you need more memory, because actually it's not that hard to scale but knowing when you need to scale, you need to keep an eye that you, uh, how do you know how much memory you need. It's a big problem, you know, a complicated question to answer how much CPU do you need?.
Even once you make the choice at what point will you want more and things like that. It all adds to the sort of things that you have on your plate, right. Which, uh, the other services basically eliminate.

**Jeremy** Yeah. I guess the Aurora implementation of RDS, the, the hope is that you would move in the direction of not needing to manage the scaling, but it sounds like it's maybe a little too early

**Daniel** Yeah. I think it's very promising cause I'm very optimistic about that approach I think it's very smart way of doing databases. 

I think it just needs to be treated as something that's new. I think that's the only precaution that I would advise is just if you have some mission critical database that you would absolutely never want to experience any problems I would be very cautious before I just change from Postgres. 

I think, I think both the the customers of Aurora as well as Amazon itself is still yet to learn about its behavior. Cause these are complex pieces of technology that I don't think Amazon intentionally made anything incompatible in terms of behavior that is just things that gets missed out and things that nobody expected because some of these things might not even be documented by the open source solutions. Like they are just behaviors that people ended up expecting from their own experience. And then when they end up using something different, they get surprised.

So these are the issues. And in addition to that, again, one of the problems of something being new is that you tend to find less support. Online, less books, less community, it compounds. Right. So, um, that's another drawback of jumping into the latest and greatest.

**Jeremy** I talked to a guest previously where they were talking about their experience with Aurora and they were saying they found it hard to predict how much things were going to cost and the latency of their queries was a little inconsistent compared to their experience with RDS.

**Daniel** Interesting, yeah.

**Jeremy** It seems like whenever you're going to jump to something new, you want to make sure that you fully understand how it behaves.

**Daniel** If it's important because again if this was a proof of concept or anything like that maybe the latency is not that important for you right? The same thing with Lambda as we touched on beforehand.

There's lots of unpredictable things in Lambda, like in terms of network performance it's completely undocumented and it varies a lot. Depending on your memory and even if your memory is fixed, sometimes downloading from S3 you get 50 megabytes a second, sometimes one megabytes a second right? 

But look, is it important for me? Maybe I'm not using S3 or maybe my objects are so small that it doesn't really matter. It's good to sort of know what are the critical, important things like maybe consistency, performance and the thresholds.
And then if you're considering jumping into something new really understand it well to make sure that you're not going to be surprised by what you find.

**Jeremy** Yeah. That makes a lot of sense. I want to go a little bit more into Lambda. Earlier you were talking about how there's a lot of people who are trying to use API gateway in combination with Lambda as a replacement for a web server for their application. Why do you think that is not a good choice at this point?

**Daniel** Yeah. One of the nice things you have when you don't use Lambda, you have an application running on EC2 or maybe on the container service or something, but less serverless than Lambda is that you can expect that if your application.

If you have a Ruby on Rails applications running on your laptop you can literally just deploy almost without modification. Lambda and even API gateway, they come with so many rules and restrictions from the platform itself that you basically have to write your application to the abstraction that they provide. I think the problem again is that some of these things you end up discovering them later. For example, the, one of the things that surprised me, which is not that surprising when you think about it as that both the API gateway and Lambda claimed that they support web sockets. Which is true, you could build a WebSocket application on it, but the surprising thing is that, uh, every WebSockets message that you receive ends up going to a random Lambda function it's completely stateless.

And this is very different from when you implement WebSockets on a traditional host where you have a connection that's persistent and stateful. And you can keep state in the connection. For example, if you authenticate a user you authenticate once and then it just exchanging packets over that connection.
Whereas with Lambda, you basically have no state as the packet gets sent to a statedless invocation. This ends up being, first of all. Uh, quite challenging because you have to keep state somewhere, maybe in DynamoDB you have to read and write it adds latency. Even though dynamo is fast, you're still making a read and a write maybe an extra 20 milliseconds, but sometimes it ends up the cost ends up becoming prohibitive because you end up touching DynamoDB twice per message. Whereas in its additional application, you're just exchanging packets without touching the database. These are the types of traps that you might end up discovering later that you think, Oh, you know, I can use this, but then you realize that you can't.

And then there are limits. Again, lots of things related to the statelessness, but also to the size limits of the binary that you can deploy things. Many of these things you can work around them, but they just end up being a distraction. I think Lambda is great if you think of it just as a code runner in the cloud. I have a piece of code and I want to run it. Based on some activity and I believe this was the initial vision of Lambda when AWS launched dit. This was the service like if you want to resize an image, as soon as it gets uploaded to S3, this is a perfect use case that you don't have to spin up a server and monitor it.

Like it's the same advantages we're talking about DynamoDB versus RDS. Like it's just less maintenance for you. But I think the customer's when they saw it they ended up sort of thinking, "Oh, I can actually just get rid of my servers and run everything on it" which again, like for a toy project and the demo, you can do it, but then once you start adding sophistication, you start running into lots of limits and other things.
I was just looking at the /AWS subreddit it's like nearly half of the topics are how can I do this in lambda and how can I install an agent or how can I do a cron? How can I do basic things? That would be a very straightforward to do if you had regular web application running on a mature framework like rails for example but they become a complicated things if you're running on lambda.

This is one of my most controversial positions there's lots of people that disagree with this. I might be exaggerating the problems. I don't think it's a hard rule. It's just I think it would be foolish nevertheless to just expect, Lambda and API gateway to be equivalent or a substitute of a more traditional hosts where you actually are renting a real computer.
You're not really getting a computer in the cloud you're just getting something like JS fiddle. Something that just runs a piece of code for you. Very different. So my advice is to just caution. If you're really thinking of building your backend completely on Lambda just be aware, make sure you know what you're getting into.

**Jeremy** Yeah. Just be aware of the limitations and the things that may be very easy with an EC2 instance, but become very complicated when you're using Lambda.

**Daniel** Exactly. Einstein. Actually and things that look easy for a demo because Lambda and API gateway makes it very easy to get something working very well. But then just even for example, sending telemetry out of your Lambda function is just not straightforward something that nearly every production application tends to do.

Sure. There's integration with CloudWatch logs, which is something that I worked with when I was at Amazon. Whenever you want to do more sophisticated things like install an agent for something, a different site that lets you understand what's happening in application. Things start to become very, very difficult or you end up having to create very convoluted pipelines of data going into CloudWatch logs, getting sent to Kinesis string, getting read out of some other thing to be sent somewhere else.

Whereas when you're running on EC2 you install a small program that's just watching some log file and that's it, you sort of forget about it.

**Jeremy** I want to talk a little bit about your decision to choose EC2 as kind of the default choice for compute. There are many services within AWS that take the responsibility of managing the operating system away from the developer. Like for example, the elastic container service, or elastic Beanstalk.

Why did you decide to choose EC2 as your default?

**Daniel** I don't believe that Elastic Beanstalk nor the container service, abstract that much away from you. In reality, you're still responsible for  operating system level settings. File descriptors, sizes, and limits on the OS, whether it's in the guest container, or especially Beanstalk it's mostly just bootstrapping. I think the most value is that It just bootstraps your AWS account, setups up your VPCs and your network settings for like if you have a rails application or traditionally using one of the common frameworks just does it with sort of good settings. It's a good product. And actually from Beanstalk you can as far as I know, modify anything you want and get out of it and migrate out of it completely if you sort of outgrow it if you see that you wanted to customize more than it allows you to.

I have no strong objections about either of those two things I think EC2 is just slightly lower level but not that much lower level that it's significantly harder. I think your responsibilities are still in the same ballpark. On the other hand, it's Lambda That really abstracts the operating system for you, and that's its big value, right?
And that's really really valuable I don't diminish that. You just don't care about whether it's running Ubuntu or CentOS or whatever and settings and things like that. Um, but as we've talked before there's tradeoffs of the platform when you're doing that.

**Jeremy** 
When you're working directly with EC2, how do you keep your instances patched and how do you handle backups for them?

**Daniel** For backups most of my experience is that I never have any state that would be bad if I lose it on the EC2 instances. I have no experience with stateful stores and in fact it's a very hard problem and I would try to delegate as much as possible any states to S3 or DynamoDB, or SQS or Kinesis or other things that are not necessarily AWS services other technologies that are built to maintain states properly so it hasn't been a problem for me. 

For patching again, I think it's something that people tend to overthink the complexities. I think people would be very surprised if they knew how Amazon itself, patches the host but at the end of the day, you could run a cron job that just does yum install security updates or whatever is the command and reboot every week right?
And you could set it to run at a random time and you'll know that you're always sort of running the latest and greatest security patches or things like that right? Which is not very different from what happens behind the scenes inside the system.

That's for operating system level security. And by the way, you could do more sophisticated things than that, obviously. But that pretty much solves the problem. 

For application level, uh, securities, which I think are more important. So that's your software dependencies, your libraries. I think most of the issues tend to be there most of the time. I think the solution there is not different between EC2 or Lambda for that. The only solution is that you have a mechanism to deploy frequently and you're just updating your dependencies often, and you just rolling out changes so it doesn't seem to matter what host you're using.

**Jeremy** One of the features you chose to include is the Simple Queuing Service and one of the things that you mentioned is that there is no strict ordering. So the messages could show up out of order and you could also get duplicate messages. If you're an application where the ordering matters or you don't want to process the same message more than once, how would you handle that either in message design or in your application design?

**Daniel** So first of all, SQS has a feature to enable strict ordering and no duplicates. So, uh, you basically set us, set a setting on the queue for FIFO. But it comes with the limitation of I don't remember the numbers off the top of my head but I think it's something around 200 messages per second or something like that, which I believe you can request to increase that, but I am almost certain that there's a limit on how much you can increase it.
I don't think you know how the strict ordering solution works, but presumably the message needs to meet in a single place somewhere so that they get sort of inserted so this is very likely where the limitation comes from. 

So I think if you have something that you believe will be abundantly clear of those limits, I think this is probably the easiest thing to do if you're not expecting hundreds of messages per second. 

Otherwise, this is a very hard problem. Otherwise, you'd have to probably handle this in your application. Where you have to remember, what you're processing and you'd probably use some other external store, maybe DynamoDB and things like that.
How you end up, what you end up choosing, I think depends a lot on the scale on the throughput can you afford to insert everything in DynamoDB for example, so that you do de-duping there? If not, can you afford to just have a short time window for the de-dupes? Do you really want to guarantee absolutely no duplicates completely or are you okay if you just look at a time window for maybe just a few minutes and then maybe can keep some state in memory right of message IDs that you've seen right things like that. So it's a hard problem.

That's why I think it's nice that SQS has this feature. Um, and I would default to it definitely if I needed strict ordering. But yeah, it's very important that you believe that you're not going to run into the limits because I'm almost certain that there's a hard limit somewhere.

**Jeremy** Another service that you include is Kinesis. Can you explain a little bit about how that differs from SQS and the types of problems it solves?

**Daniel** Yeah. So one of the main properties that's different between the two is Kinesis allows multiple consumers. So I think again, like to describe it as data structures. I think SQS is a typical, is a queue where you can only have one consumer and the consumer, basically pops out the message to consume it.

Whereas Kinesis this is more like a linked list where the consumers can literally just keep a pointer over where they've read. And you can have as many consumers as you want. They all read the same data and exactly in the same order that the other consumers have read it. And Kinesis it actually, allows you to provide strict ordering it's a bit more sophisticated. Duplicates can still emerge so that problem doesn't really get solved in Kinesis. Kinesis basically is an interesting technology for when you want to enqueue things to be processed asynchronously and then you have multiple independent things that even if one of them were to slow down or have a problem, they wouldn't affect each other. Nevertheless, the problem with Kinesis as it exists today, and I think this will improve eventually, is that it's a bit hard to manage. You basically manage capacities with a concept called shards.

Each shard is quite small I think it's one megabyte a second unless it increased recently. To add more shards, you have to split them. So you always have to double the size, which is a bit of a nuisance. You get lots of control
but also lots of responsibility of how you route your messages across the shards. You need to make sure that they're evenly distributed because then you might, even if you have 10 shards you might end up using one completely. So it's definitely a more complicated product than SQS, where it's super simple.
You literally just enqueue and you dequeue from another side it's as simple as it gets. I think Kinesis I included mostly because the alternatives to Kinesis, like for example, Kafka is typically one of the technologies that is considered an alternative. I think Kinesis is, despite all the challenges in managing it, I think it's still simpler than learning Kafka, less moving parts.

It's still sort of pretty much fully managed in terms of availability and durability by AWS. Again, if you write something to Kinesis and you get a 200 okay. You can put as much be assured it's safe and guaranteed and then data expires automatically after a retention period that you can choose.

So that's all managed for you. It's all nice. Whereas if you're running Kafka yourself  you need to set up zookeeper and the database and hosts and monitor them like in my head it's an order of magnitude more complexity. I think it's a niche use case for Kinesis. I wouldn't expect everyone to need it. Actually. I would imagine the opposite very few cases would need it. I think for some, backend work where we need to dispatch asynchronous work. I think it's good depending on what you need to do. It's a good thing to look at when you're considering options.

**Jeremy** One of the things that's not discussed in the book is solutions for a content delivery network or for caching.

When you're building applications yourself, would you use the services provided by AWS or there are those things that you would look outside of AWS for?

**Daniel** I didn't include them again, mostly because I didn't have firsthand experience. CloudFront and CDNs. I think CloudFront is something that I would rely on. Amazon itself relies on it for amazon.com website, things like that. I would definitely say in terms of dependence it passes the test.

For example, even myself for userbase, I'm pretty much using AWS for everything. But for my marketing homepage, it's a static website. I've chosen to deploy it on Netlify. It's significantly simpler and better user experience. You check in something in GitHub 15 seconds later, it's deployed on all the CDNs, all the caches are invalidated, and you get some analytics.

If you were to set up CloudFront, if you go to the console, you've got two pages of options that you need to set and understand and deployments take a long time. Sometimes they take a minute to go to all the CDNs and it's sort of again, like I'm not saying like I would avoid CloudFront by all means, but I think for some use cases, especially for just simple sites. I think CloudFront might be an overkill in sophistication. 

Caches like ElastiCache and things like that. I've never really used any of them. I basically don't really have an opinion on them. But I would probably still be a bit cautious. If I were to study whether I should use them, I would look for limitations and things like that.

Like, why would I use this rather than just run redis myself right? What am I really getting? I wouldn't automatically default to just using them I would really want to be convinced that the little bit of management that AWS is providing is really worth it.

My gut feel is that unlike RDS, RDS it's still just the open source database. And most of the management is still for you, but it is providing some good, valuable management. Like for example, managing fail overs and the backups it's just a click of a button and things like that, and they're very valuable if you had to do them yourself it's quite a lot of work. 

But for things like memcache or redis, I can't see that much value being provided by just the hosting part. But I could be wrong. But if I were to research them, I would go with that type of critical eye and sort of look for, is it really worth it?

**Jeremy** Yeah. Basically try and figuring out like how difficult is it for you to run your own instance on EC2 and if the operational load is fairly low, then you would probably choose to do that rather than use

**Daniel** Probably or maybe even co-host it with my other EC2 instances, which I think is a nice pattern for caches. You'd just have another processor running on your hosts and then it just scales automatically right? Yeah, sort of is probably what I would default to do.

But I would still look into the options, I think is still wise to see whether I would be gaining something important.

**Jeremy** One of the things I thought was interesting is you said you worked on the CloudWatch team and CloudWatch doesn't appear on the list, so I was kind of curious what your thoughts were on that.

**Daniel** Yeah. I think CloudWatch might be worth a sequel a part two I think I would have loved to include CloudWatch. CloudWatch itself has good parts and less good parts let's not call them bad parts. But it's like there are things that I think are are worth using and things are probably there's probably better alternatives. Third party, like outside of AWS. 

Again, I think Amazon does not a very good job in explaining some of the good parts and the important aspects. Uh, and I think there's probably, I don't know if there's a book worth of content or maybe a blog post or something right but at some point, if I find time I intend to elaborate a bit more on what you could do with CloudWatch is I believe many people are not aware of just because it's just poorly documented or not documented at all.

But for what it's worth, I'm using CloudWatch myself for userbase, so it's sort of a signal. For what it's worth. I think you could do a lot in terms of monitoring out of CloudWatch. 

I think in terms of polish and user experience, there's lots of rough edges and some frustrating aspects that are significantly weaker than some other third party solutions but I think it gets the job done. 

For what it's worth pretty much Amazon runs on it right a trillion dollar company one of the biggest tech companies in the world. So it's probably good for you as well if it's good for the company. But, I think needs a more nuanced take cause it wouldn't have fit in sort of the style of the book that I had with sort of short chapters at high level. But I'd love to expand more on it if I find the time.

**Jeremy** Yeah. And you were mentioning how you felt like there were some third party options that might be better. Could you give some examples of something that somebody should consider?

**Daniel** I think it depends because monitoring is such a big space. I think popular solutions, which I think they all have some good things like Datadog, honeycomb, elastic search, and kibana and a few others. I think again it depends whether you're running a small web application with 10 servers or whether you're running something with 10,000 servers, there's lots of different things, or whether you have just a monolithic application, does it just basically horizontal scale like a rails app or whether you have a constellation of 200 microservices.

I think the options here start to change dramatically. What makes sense and what's not right. But, I think this field is evolving a lot, that there isn't really a one thing, sort of one product or one solution that's just the best for everything. I think again, it's hard to give suggestions and sort of in general on this topic. This is one of the reasons it was hard to sort of make it fit in the book.

**Jeremy** One of the things you mentioned earlier was how to host your Userbase website, you chose Netlify because the user experience or the developer experience was so much better. What is your thoughts on services like Heroku, for example, that are a layer on top of AWS, take a lot of the choice and the things that people need to learn when they want to deploy an application.

Why should someone spend the time to learn AWS when there are services that lie on top of it?

**Daniel** No, no. I am a big fan of the Platform as a Service Heroku-style approach. If I was working on a rails application I think Heroku could be my default choice very easily. If you have outgrown Heroku for some reason and you're running into some limits or it's too expensive or whatever. Sure. It's not super easy to migrate but you could do it. It's not that hard. You don't need to necessarily learn AWS or learn all the things.

Or learn EC2 right? Because AWS has many things you could still use Heroku, S3, and DynamoDB for example which I think are very useful tools in your tool chain to consider regardless of where you're hosting the application.

I definitely see a future where for most traditional web applications in general and mobile application and things like that the abstraction away from thinking about the server, the network, the operating system gets abstracted away.

As a developer myself I would feel even more comfortable developing that way. My take on EC2 is it's not necessarily that whatever you're doing, you should use EC2. If you literally want a replica of your computer or close to it somewhere running in the cloud EC2 gives you that. But if what you want is something that runs your Rails application Heroku is that. And even Elastic Beanstalk for example, in the AWS world it's not as abstracted as Heroku you still end up setting up your own instances and have to do some things yourself. It's a layer in-between, but it's bootstraps that for you that that's how I think of Elastic Beanstalk. At least it sets it up without you having to figure it out. All the VPC and security groups and network and load balancer settings and things like that. Yeah. Big fan of the platform as a service tech.

**Jeremy** Yeah. Knowing kind of how AWS works from the inside, what do you think is preventing AWS from building something similar to Heroku? Like having a better developer experience for people.

**Daniel** It's going to sound harsh but I don't think Amazon in general than AWS specifically is good at these things. AWS is really good at providing products that end at the API, something DynamoDB and S3 things like that. When you start to getting into the developer experience, user experience, UI sort of the intangibles, hard to measure that make people happy when you use them. It just doesn't get it. With the company there's something in it it doesn't know how to understand that, how to measure that, how to sort of develop in it. I think this is very visible, if you look at the console it's borderline frustrating barely usable, some part of right in my opinion and I think in the opinion of many, even the documentation and many other things. 

I've definitely seen this from the inside as well it's just really really hard to make a case for the things that are just hard to measure.

You can never say never I mean maybe things change, but I think from at least the time that I left which was exactly a year ago, actually literally today. Things were still like that where the focus pretty much all the way up to the executive level or pretty much the CEO where the focus is on the latencies of APIs and the 99th percentile error rate it's like this is what everyone looks at oh we managed to improve this API speed by two milliseconds. Big wins, right? Which is, which is good this sometimes translates to developer experience, but the more complicated thing like the Netlify experience where I literally just signed up for Netlify connected to my GitHub account, click two buttons to my build command click okay and suddenly I have a URL for my website running where every commit has its own URL, like these small things.

I think sort of the issue with AWS is that the way most of AWS gets built is a bit more project driven. Customers tend to ask for something and Amazon builds it. Customers typically tend to ask, you know, I want this feature that I want this flag, I want this setting and Amazon turns around and builds it and does a good job there. But things don't start with a vision of a highly polished developer experience or user experience.

Which I think is funny one of the examples is that every new initiative every AWS service starts with, I don't know if you heard about it, but with the six page document. This is how AWS builds new things.

Where if you have an idea or you write a six page document, uh, explaining sort of writing pretty much the press release and the FAQ and sort of how things are going to look but it's all text you're banned from putting any images any demos any tables. It has to be all text, which again, like this works really well for when you're doing something very low level that's easy to describe in a sort of relative form: the interface is very slow. 

But it's super hard to describe something where you just experience it and you feel happy about that. That is just, um, it doesn't seem to match. I think,  what works there is like the demos, like the high fidelity demos, the working examples where you just say, Oh look, just type this and this and this happens.
like this is amazing. So yeah, I wouldn't worry too much about Amazon sort of entering or competing with the developer experience focused businesses. You know, it could happen but I wouldn't bet on it.

**Jeremy** It would require like a really big culture shift

**Daniel** A DNA change. Yeah. I see it very hard to happen the way things are structured right? The obsession is on something different all the way up right just a culture that I think started even with the amazon.com the eCommerce business and translated later to AWS as well I believe.

**Jeremy** Yeah. It's interesting because people sometimes talk about how Amazon has this customer obsession, right? And that kind of goes into what you were saying about how people ask for things and then Amazon gives it to them. But they don't pull back a little bit and figure out like what is the story of somebody who wants to build an app? How can we make that experience really smooth for them? It's more about how can we just get them the features they need and if they have to cobble them all together and it's complicated. It's okay.

**Daniel** It is like that. It's definitely something that I've observed. Like it's the way things work and like the customers ask for this. Once the customer asks, you have the mandate, pretty much the obligation not always right but to deliver it.

And that's it. That's how it works. That's how roadmaps get built. I think you, you need to do things differently when you're just trying to keep things simple. And this is the reason why setting something up in AWS ends up being, yeah, you have to patch these 50 things together right?
To have to configure permissions for different AWS services to talk to each other like this is insane. Like, why am I giving permission to CodeBuild to use CodeDeploy? Like these are two AWS services and things like that. Don't get me wrong like I think people are trying to improve these things. It's not like nobody's aware of it. But I believe the environment that exists, the culture right the way things work, it's just super hard to make progress.

And actually I think the progress seems to be happening in the wrong direction, unfortunately. Not intentionally, but I think this is me speculating, but I think it's quite obvious most of AWS as a business nowadays comes from big enterprises and government contracts and things like that, which I think have very different requirements and needs than the indie developer and the small business.

And this is why when you go and spin up an EC2 instance, you get sort of a page of like, you know, 20 options that many of them you won't ever need but they're there because if you're a bank and you have regulation that your server can't be mixed up with someone else's. You know, you have to choose this box right, which is only there because of, you know, some industry or something like that.

**Jeremy** As an overall strategy, I mean, clearly currently AWS is the market leader in terms of cloud providers, but in your opinion looking back at your experience there and how you think the future is going to go. Do you think the strategy of building so many different services and just seeing what sticks, is that a good strategy or do you think that it would be better having less products, but with some more, I guess thought put into them?

**Daniel** Yeah, I think, I think unfortunately, because I wouldn't want to see this happen, but I think AWS will become the IBM of what IBM is today right basically becomes a vendor for big companies, big governments, a consultant even doing what they want because that's where the money is. And any value for the smaller businesses and the small developers and whatever would likely come from maybe other businesses that build on top of AWS
like Heroku for example. It's sort of how I see the evolution happening. I think we're already on trajectory. It's already started. It's hard to really predict when or how or how much may be and I hope actually that it still remains feasible that I could do basic things with AWS without sort of getting to lots of hurdles and things like that.

But if I were to predict how I see it going it's just the pressures of the financial aspects of wall street. Everyone is expecting it to keep growing 40% year on year.
And you know, I think the incentives are structured such that there's a limit to how much the small developers can provide. And if you go chase the $10 billion contracts with the Pentagon or whatever you build very different products. Let's face it. I mean, we're not fooling anyone.

So I'd say the Pentagon definitely has different requirements than I need. And sometimes it's just a distraction. But I think what ends up happening is that the products have evolved to mirror what the big customers wants. Again, we mentioned CloudFront.

I think again, like it's just a different experience. If anyone wants to go to CloudFront and you go set a new distribution or whatever it's called, you get this page that I think you can kind of scroll twice of many different options  and every one has a learn more next to it you go to documentation, which everything is useful but for many people that just want to put some static assets in a CDN it's a lot.  

**Jeremy** Especially when you're a developer and you want to use a CDN, and you go to say CloudFlare and it's like a few clicks, and then you've got this CDN in front of your application.

**Daniel** Right so either AWS sort of become something that most of us will never touch directly again, or maybe and this is maybe the most optimistic is that it remains a power tool a power service. Like if you really want to customize everything you you go there.

Um, but we'll see maybe we'll have another podcast in 10 years and we'll reflect on this prediction (laughs).

**Jeremy** That's a interesting insight. I've definitely seen the trajectory of it starting out as this pretty straight forward simple service for developers to needing to serve more and more large customers get more and more complicated. And now if you're somebody who's new to development and you just want to host something on AWS, going to that console is just

**Daniel** It's daunting. Yeah.

**Jeremy** If people want to check out Userbase or your book or yourself, I know you have a lot of interesting tweets now about your experience running your own business and that sort of thing.

**Daniel** Yeah. I'm mostly active on Twitter, so I'm @dvassallo where I have the links there to my site and my book and my business. And I'm basically documenting my journey. I left Amazon exactly a year ago.
Since then, I've settled mostly on Twitter, but occasionally I write a blog post, but on Twitter, mostly on a daily basis I'm sharing what I'm learning and what I'm seeing, decisions that I'm making some behind the scenes, insight about the business learning, like the books.
For example the book I shared some of my marketing efforts and performance of the book and the sales and things like that, which, I think people find interesting sometimes as an inspiration for somebody wanting to do something similar, you can learn from my mistakes or get inspired by hopefully the good results.

But yeah I'm enjoying this and I have a decent following since I started. I think there's lots of interest right in how things work and how to sort of start your own thing and how to, especially to get through the initial hurdles right this the first time I'm doing some of these things.
The book I had never wrote a book or a digital product so yeah, Twitter is where I share most.

**Jeremy** Very cool. Well, Daniel, thank you so much for joining me today.

**Daniel** Thank you Jeremy. Thanks. This was fun. 

**Jeremy** I hope you enjoyed the conversation with Daniel. You can get show notes for this episode at softwaresessions.com and we'll see you in a couple of weeks.

</div>