+++
title = "The good parts of AWS with Daniel Vassallo"

description = "Daniel discusses how he chooses AWS services and his thoughts on the culture and future of Amazon"

[extra]
episode_url = "https://media.transistor.fm/b039e563.mp3"
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

This transcript is incomplete.  You can help me edit it at [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy**  Today I'm talking to Daniel Vassallo about his book, the good parts of AWS. Daniel, thank you for joining me on software sessions.

**Daniel** Thank you, Jeremy. Thank you for having me.

**Jeremy** You wrote a book called the good parts of AWS, which suggests there are bad parts or parts most developers shouldn't look at. How did we get to this point? How did we end up with so many services that developers don't even know where to start?

**Daniel** There was so much popularity especially in the enterprise world, that it doesn't speak to the developers anymore. Like I remember I used to use AWS at the very beginning more than 10 years ago, where the website was super simple.

There were like four services. If I remember correctly, code examples, if not on the front page, like a quicker way where you can as a developer understand what you could use and what value you could get. 

But I think nowadays, even me, like I go to the AWS website and I barely understand because it's speaking to CTOs of big fortune 500 companies like lots of buzzwords and jargon and blockchain and machine learning, and it's daunting. 

It's very hard for somebody to go to product pages and understand what options are available.

But not to mention that there are many many ways of doing the same thing. Like if you want to have a database, I think on AWS there are five different options. I think AWS also doesn't do a great job explaining the differences. 

Like, you know this is good for this so there is still a gap in terms of how to think about things.

I don't think that there are bad parts I think there are less important parts that I sort of decided to pick. And by the way, it doesn't even mean that the things I didn't cover in the book are not worth looking at or not worth using.

I try to pick the things that are definitely worth looking at. I, that's nearly every non-trivial application would likely benefit to have to at least consider these things. 

And they are only the things I had firsthand experience with. So I tried to stay away from things that I didn't know much about and just write about what I think are the most important parts.

**Jeremy** Where is your background coming from? What kinds of applications were you building?

**Daniel** So before I joined Amazon, before, so I joined Amazon in 2010. So over nine years ago. 

I was a full stack developer. I was working in a couple of small startups where I was building applications frontend backend databases the usual thing.

I was part of the CloudWatch team, which is the monitoring product in AWS. And. Sort of the main focus was on backend web services. So basically our interface tended to stop mostly with the API we're just building, these web services that stored metric data log data about how applications are, are working.

I tried to in the book focus on things that are more broader than specific backends or database focus or front-end focused. Not every application would need to use everything, obviously right? 

I like this concept of a default choice, which is a bit of a subjective perspective. I admit but, for example. If I needed to store files somewhere in the cloud my default choice would be to use S3 right?

It's just super hard to beat in terms of price per storage or availability or the durability. I like to think about to this heuristic where I have like default choices where I would just default to some things unless I really believed that this default choice wasn't good enough for me.

I try to present ideas like that. Like if you want to have a server in the cloud, EC2, is a perfect case, much more than Lambda and other things that are much more limited than a full server. Same with dynamoDB. 

I think Amazon does it a disservice by describing it as a database. I like to think of it more like a data structure that is significantly simpler than what we tend to expect from a traditional DBMS where you have lots of features, that you would be disappointed if you expected them from DynamoDB. 

I think DynamoDB is much closer to something like Redis. Than it is to my sequence that, and I think if you think about it that way, that makes it much easier to see whether it fits your needs or not. Like, can I fit all my data inside a very primitive data structure that's highly durable and highly available.

If yes, great, it's a good default choice. But if you need stored procedures and triggers and joins and subqueries that run close to the data then you're going to have a hard time. You can probably find a way to work around these limitations, but it's probably going to be very hard to use.

I go through I don't remember exactly how many services that I cover  I think a dozen with this high level perspective on how you think about things. Which, I think is a simpler way to reason about them than just reading the Amazon product pages.

**Jeremy** Right. Which is, when you go to the Amazon homepage and you click that button that shows you all the services. It's kind of insane, right?

**Daniel** It's daunting. Yeah. It's daunting. And that's the problem you see a databases category and then you see six things under it and you click on all of them in a new tab. And it's so hard to understand what's the difference or which one you should choose and things like that.

**Jeremy** You had mentioned dynamo DB and how you felt like it's more of a data structure than a database, and I'm kind of curious, why you decided to choose that to be your default data store rather than something like a RDS, like some kind of relational database store.

**Daniel** I try to have a slightly more nuanced take, I would say DynamoDB, is a good thing to consider as a default. I would basically ask yourself, can my data fit? Because I think if it fits, DynamoDB spares you from a lot of burden and operational things that you would have to deal with even if you were to go with RDS that are things like setting up backups and making sure that you're not running out of memory and the primary keys and you know that the indices are fitting in memory and IOPS and things like that.

DynamoDB abstracts everything away from you, it's really great. For many web applications and web services, the database tends to be one of the most challenging things to keep running.

DynamoDB can be very helpful, but I think the important thing is it depends. Two things to think about is whether you can live with this access pattern of just reading off a b-tree. And the pricing as well, which I touch on in the book sometimes the pricing can be a significantly more expensive.

That can be cost prohibitive depending on how you, how you're using it. If you realize that DynamoDB doesn't make sense for your case, then I think, yeah, RDS is a perfect example. I didn't write too much about RDS in the book because I don't have recent experience.

I used RDS At Amazon, in 2011 so a very long time ago. And to be honest, this was quite a terrible experience. We had all sorts of problems, from sort of databases getting stuck like for 45 minutes and not being able to do anything about with them. Fail overs happening randomly and not failing over like all these kinds of things that you don't want to happen with the database.

But to be fair, I believe many of these things have improved significantly. I would feel comfortable using RDS, if I needed it. But I don't have the first hand experience to be able to sort of highlight any quirks or any other things that I am missing. That's the only reason why it doesn't appear in the book.
I didn't feel I had the right to write about it.

Something that I think is a bit risky in the RDS world is Aurora. It's fascinating technology I really like this idea where data and the compute are separated.

When you had a typical database you scaled everything together. If you wanted more space or more memory or more CPU, everything could go together. 

One of the problems, ends up being like if you have a database that has lots of data but it's not running, you have sort of these disproportionate resources that are under utilized or they're bottlenecked and things like that.

Aurora manages to keep the data separate from the compute and running a query can spin up more compute on demand and things like that. But from what I heard again, this is mostly heard second hand, is that one of the things Aurora tried to do is be MySQL. And I don't know if with other databases as well. The problem that happened is that the behavior is not really that compatible but the interface is right the queries are the same, but for example, you might expect that adding a column to a table in MySQL would be harmless while in Aurora it might lock up. This is not a real example, but things like this right.  

I think there was a Reddit post a couple of few months ago where someone highlighted lots of things like this, which are quite scary like things when you're using MySQL, they're just non-disruptive but when you do, when you use Aurora they ended up being very catastrophic or very problematic things. 

And I think this is a problem with immature technology, right? I mean, MySQL has been around for, I don't know, for 20 or more years, millions of users running it every day millions of hours of usage. Aurora's just a couple of years sold. 

It's tries to be a drop in replacement for a database that has been around for like two decades at least. And it's just a very hard thing to do. In general I tend not very tempted to just jump into the latest and greatest by default. 

I like the devil that I know, even if there are problems. I think there's lots of value that many people underappreciate and many people in tech tend to underappreciate out of the, the test of time. The more software gets used the better it gets typically because the more issues get revealed the more bugs gets fixed and things like that.

**Jeremy** When I think of the tried and true, I think of things like MySQL or Postgres so it's interesting that AWS has been around so long that cloud only services like DynamoDB and S3 are now in that category.

**Daniel** I think, I think that's true for a part of them. I think that's the trap sometimes because I completely agree DynamoDB and S3 I would put them into the category of the tried and true. 

S3 because it's used by everyone. DynamoDB is used extensively within Amazon, and I think even outside it's decently popular.

But there are probably another hundred or so services that are I would definitely not fit in that category. Amazon launches, I don't know dozens of new services over the year right and many of these I've seen it myself that just get launched with very limited usage like the first users are almost literally the first users.

I wouldn't necessarily avoid them at all costs I think it would be very prudent to treat them differently than other things. Because if they're offering something particularly valuable for what you're trying to do, I think they're still worth considering.

What I think is potentially harmful is the idea that. Newer is better just automatically, which I see sometimes happening in the databases and compute as well. I think there's a bit of this problem even in the Lambda API gateway and that kind of thing there seems to be this impression that the default should be that if I'm hosting a web application it should be on Lambda which I think is an insane default. 

I actually like Lambda at lot, but I think, it's over utilized for what it is intended to do.

And actually I'm very optimistic about the serverless future where we're building web applications without having to think about the operating system and the hardware underneath it. So lots of potential. But if you're building something today, you have to look at the options that exist today.

And there's still lots of issues, with running a sophisticated web application, not some trivial, you know, hackathon project right, completely  on Lambda and API gateway. Right. In my opinion.

**Jeremy** You were talking earlier about, Aurora and you know, I wasn't even aware that the internals, you know, like you were saying, you're giving an example where  you add columns or you make some kind of change and the behavior of Aurora may not be the same as the actual open source project. And so I wonder, like, when people are choosing services from AWS, you know, for example, whether it's RDS or it's ElastiCache, or these managed services that AWS offers, how can people find out or determine if it really behaves the way that they're going to expect in terms of the, the open source product.

**Daniel** I think you can read between the lines a little bit and I think AWS makes it not super clear, but it's not completely obscure. And there are two types of managed services that I had to do was that AWS literally takes the open source projects and and hosts it as is.

And this is the typical MySQL running on RDS. To be honest, I don't know if there are some minor changes to it. There might be a but  I wouldn't expect them to be a significant. Sometimes there are limitations, sometimes you might not be able to change some settings and this is common. 

For example, in the elasticsearch hosted service there's lots of things that you can't modify if you choose them, but these are easier to reason about because there's typically a limitations page in the documentation.

But then there's another category of services. I think, DocumentDB that implements the Mongo DB interface. These are not the real thing. Amazon built a brand new piece of technology and just made the API compatible with it. So in the latter category you can't expect the test of time that would have exercised the open source technology to apply to these things. It's because it's literally just a different black box behind it. I think you can tell.

It's not immediately clear just from reading the names of the products.
But I think if you dig a little deeper, you can tell whether this is actually the old thing or it's not. Again, like I am not saying that for example, DocumentDB or anything is necessarily bad, but they're new tech that I think it's safe to assume that when they were launched, almost nobody used them.

I'm sure though that would have been a few beta testers and whatever. But this is far from MongoDB which has been around, I'm sure it has problems as well, but it's different. First of all. Many of its problems are well known, and if you are to Google them you'll probably find behaviors and workarounds and things like that, um, or many have been fixed.

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

</div>