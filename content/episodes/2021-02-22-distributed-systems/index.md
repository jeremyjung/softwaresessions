+++
title = "Distributed Systems and Careers with Shubheksha Jalan"

description = "Shubheksha talks about service observability, the importance of job titles, and the difference between sponsors and mentors."

[extra]
episode_url = "https://pinecast.com/listen/9daafe46-b631-4c0e-adbf-aa515aa961a5.mp3"
social_title = "Distributed Systems and Careers"
social_banner = "035-shubheksha-jalan.png"
social_description = "Observability, job titles, and sponsors vs mentors"
+++

[Shubheksha](https://twitter.com/ScribblingOn) is a Software Engineer at Apple. She previously worked at Monzo and Microsoft.

Personal Links and Projects:
- [@scribblingon](https://twitter.com/scribblingon)
- [Lessons learnt in year three as a software engineer](https://shubheksha.com/posts/2020/08/lessons-learnt-in-year-three-as-a-software-engineer/)
- [Personal Site](https://shubheksha.com/)
- [Systems Recipes](https://systems.recipes/) 
- [Computers Illustrated](https://www.instagram.com/computers_illustrated/)

Podcast appearances on getting into the industry through open source:
- [Code Newbie](https://www.codenewbie.org/podcast/open-source-newbie)
- [Software Engineering Daily](https://softwareengineeringdaily.com/2017/02/07/open-source-contribution-with-shubheksha-jalan/)

Related Links:
- [Monzo Service Graph](https://monzo.com/blog/we-built-network-isolation-for-1-500-services)
- [Go context](https://www.linode.com/docs/guides/go-context/)
- [An Illustrated Proof of the CAP theorem](https://mwhittaker.github.io/blog/an_illustrated_proof_of_the_cap_theorem/)
- [Apache Cassandra](https://cassandra.apache.org/)
- [Distributed System Building Block: Flake Ids](http://yellerapp.com/posts/2015-02-09-flake-ids.html)
- [Protocol Buffers](https://developers.google.com/protocol-buffers)
- [Go rpc](https://golang.org/pkg/net/rpc/)
- [Consul](https://www.consul.io/)
- [Envoy](https://www.envoyproxy.io/)
- [What is a Runbook?](https://www.pagerduty.com/resources/learn/what-is-a-runbook/)
- [Error Budgets Explained](https://www.bmc.com/blogs/error-budgets/)
- [Kubernetes](https://kubernetes.io/)
- [Go by Example: Errors](https://gobyexample.com/errors)

Music by [Crystal Cola](https://crystalcola.bandcamp.com/).

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy:** This is Jeremy Jung and you're listening to software sessions. Today, I'm talking to Shubheksha Jalan about working with distributed systems, the go programming language and some of the lessons she's learned being a software engineer for the last three years. Previously, she worked as a backend engineer at Monzo Bank. And before that she was a software engineer at Microsoft. 

Shubheksha, thank you so much for joining me today. 

**Shubheksha:** Thank you so much for having me.

**Jeremy:** You picked up a lot of experience with distributed systems at Monzo bank. Could you start with explaining what a distributed system is?

**Shubheksha:** Yeah. So the main premise and the main difference,  between like, a distributed and a non distributed system, is that a distributed system has more than one node. And when I say a node, I mean just computers, machines, servers. So it's basically a network of interconnected nodes that is being asked to behave as a singular entity and present itself as, as something that's not really disjoint.

And that's kind of where the trouble starts. something that you hear a lot of people who work with distributed systems say is that just don't do it unless you really really need to because like things spiral out of control very, very quickly. Because like, when you have a single machine, you don't have to think about like communication over the network.

You don't have to think about like distributing storage. You don't have to think about so many other things, whereas with like, when you have multiple machines, you have to think about coordination. You have to think about communication and like at what levels and like what sort of reliability you need and all of that.

So on and so forth. So it just gets super tricky.

**Jeremy:** Yeah. And when we talk about distributed systems, you mentioned about how it's having multiple nodes. And I think a more traditional type of application is where you would expect to have a load balancer and some web servers behind the load balancer and having those talk to a database and those that involves multiple nodes or multiple systems. But, I guess in that case, would you consider that to be a distributed system or not really?

**Shubheksha:** I think, yeah, like if something is going over the network and like, you have to sort of make those trade offs, I think I would still call it a distributed system. And like right now, like it's not just the big companies that are building and deploying distributed systems. It's pretty much everyone, like even small startups, especially like, because the cloud has become so dominant now, like the cloud is essentially a giant distributed system that we sort of take parts off and deploy our stuff, which is isolated from all of the other stuff that's also deployed on it. But like from the perspective of a cloud provider, it is a big big distributed system. And like, even when you, as a customer are using a cloud provider, you are, your code is deployed. You don't even know where, and it's still to you like if you spin up like multiple EC2 instances, for example, that is a distributed system.

**Jeremy:** It's almost not so much that the different nodes are doing different things I guess it's just the fact that you have to deal with the network at all. And that's where all of these additional troubles or, or challenges come in.

**Shubheksha:** Yeah, I think, yeah, that's probably a more accurate way to put it. Like, I can't really think of a system that you can like reasonably fit on a single machine right now. especially with the way, like we provision things, in the cloud. So yeah, by that definition, pretty much everything that we are building is a distributed system at some level.

**Jeremy:** Mmm you were saying earlier about how don't build one if you don't need to. But now it almost sounds like everything is one, right?

**Shubheksha:** Yeah. To some level. Yeah. Everything is one. Yeah.

**Jeremy:** When people first start getting started with having a system that involves the network, what are some common mistakes you see people make?

**Shubheksha:** Like a lot of people misunderstand the CAP theorem. The CAP theorem, is basically one of the most popular theorems in distributed systems literature and it states  that like CAP stands for consistency, availability and network partitions.

And there's a lot of debate around like what those terms actually mean. So I don't want to go into that right now because that'll probably take up the rest of our time. CAP theorem states that you can only have two out of those three things at a given point of time.

And a lot of people sort of take that to heart and take it way too literally whereas there's a great blog post about this, which we should definitely link in the show notes, but which argues that like network partitions are not really optional. There's no way you can have a network that's a hundred percent reliable, like that's not humanly possible.

And there's also like some confusion around like what the terms, availability and consistency mean, And that's also like a huge source of debate and confusion in the community. And like a lot of people when they, when they sort of start working. They don't really understand what that means in what context, because those terms are very, very overloaded in tech in general.

And like one thing means like five different things depending on the context. So yeah, it can be really hard to get started.

**Jeremy:** Mm, and since it's a little difficult to pin down, what CAP means, I guess, for somebody who's, who's starting out. what would you suggest they they focus on to make sure that when they build something, that it works, I guess is one way to put it.

**Shubheksha:** I think that's, that's a very hard question to answer in like a generalized manner. It, it depends on your requirements and like, what is your end goal? What sort of like availability and reliability characteristics that you're looking for, from the system, for example, if it's a, if it's a system that's like sorting some critical data in that case, like consistency would be more valuable compared to variability, like it's a trade off.

Like everything else. So it really depends on the use case and yeah, like what you hope to achieve with the system.

**Jeremy:** Do you have a example from your experience where you, you chose those trade offs and could kind of walk us through that process?

**Shubheksha:** Uh, no, I don't think most people would have to deal with this day to day. And if you do, it's probably not a very good sign.

Like at Monzo, we had like a pretty unified platform. We did not have to like, think about this, at like, that level and go into it like super deep.

**Jeremy:** If I understand correctly there are engineers who build infrastructure or build tooling so that the software engineers or the backend software engineers don't have to worry about is this going to be eventually consistent or is this being partitioned instead you have some kind of API that's layered on top of that. Is that correct?

**Shubheksha:** Yeah. So you don't have to worry about like partitioning or anything like that. Like that's just taken care of. you just write a database schema, you deploy it and like data gets populated. You're not super worried about how that's done.

**Jeremy:** Hmm. And when you give the example of a database schema, is this like a commercial product or an open source product? Or is this something built in house at Monzo?

**Shubheksha:** Oh no. This is Cassandra.

**Jeremy:** Oh Okay. Then it's the Cassandra database developers. They are the ones who had to think about the CAP theory and work out the trade offs that they wanted to decide on.

And you, as the engineer, you just have to know how to use Cassandra.

**Shubheksha:** Yeah. And like we deploy it ourselves as well. So it can get a little tricky there too. You can fine tune it, it has a lot of knobs. So you have to give consideration to that and configure it accordingly basically.

**Jeremy:** I don't know if this applies to Cassandra specifically, but sometimes when people talk about distributed systems they talk about things like eventual consistency of how in your database, the latest change may not always be there when you go out to read it as a, as a backend software engineer. Is that something that you have to to think about and work around?

**Shubheksha:** So that also depends to an extent on the configuration and the type of data. if you know some data might not be present when you're reading it, like you have to guard for it. But like a very common pattern that's used is like, if you don't find something in the database, then you just assume that it's not present at all.

So like you try to read by a particular ID and if it's not present, then you create a new one. we don't have to deal with eventual consistency at every step. I would say like, I'm sure Cassandra does something in the background to deal with that. But yeah, like usually the assumption we make is that like, yeah, if it's not found in the database, then you just go and create it.

**Jeremy:** Mm, okay. I guess another thing I would ask about is you have all these different nodes you're referring to in a distributed system, and they all need some way of communicating with each other. what are some, some good protocols or ways for different nodes to communicate?

**Shubheksha:** something that I have been using at Monzo, or like I used to use at Monzo is a protobufs. It is a project that has been released by Google and it basically specifies how different services will communicate over the wire. So that sort of standardizes it and you have to still take care of like, some of the marshaling and unmarshaling.

But yeah, like it does most of the, the job on its own because when you're communicating on like, suppose you have two different services deployed on two different machines and machines, and you need a way to make them talk to each other, you know, you basically need some sort of a language that both of them understand.

So like if one is speaking French, and if one is speaking German, they can't really talk. So like, protobufs are sort of like both of them are talking in English and they can understand what they're saying.

**Jeremy:** And protobuf is the serialization format. Right. So that's a way that you can get a message from one system to another. But how is the, the transport handled? Like, are you using web services or some kind of message bus? 

**Shubheksha:** Oh, yeah. So, that's mostly done over HTTP. Like wire remote procedure calls. Like, that's the most common thing I've seen you basically have some sort of a wrapper around, uh, like go's HTTP primitives to suit the needs of your system.

**Jeremy:** Hmm. Okay. you have HTTP endpoints in each service and you send that service, a protobuf message,

**Shubheksha:** Via a remote procedure call yeah.

**Jeremy:** If you're using HTTP, each node or each service has to know where the other machine is or how to reach the other machines, how is that managed in a in a system? 

**Shubheksha:** that's sort of done, by some sort of service discovery mechanism, something that's super commonly used is Consul by HashiCorp. The job of that piece of software is to basically find out what service is deployed where. That's the other challenge with distributed systems, because you have so many things all over the place, you need to sort of keep track and have an inventory of like what is where so that if you get a request for a particular endpoint, you know where to send it.

you can use like a service discovery, uh, tool like Consul or you can use something like Envoy, which is a network proxy, and which sort of helps you uh do something similar.

**Jeremy:** And from the, the back engine engineers perspective, if you are using Envoy, um, or Consul or something like that, when you're writing out your end points or which HTTP endpoint you're going to talk to, what does that look like? Is there some central repository you go to and you just put that URL in and Consul or Envoy handles the rest?

**Shubheksha:** Oh, no. So like as soon as you deploy your service, basically, the platform will be aware of it. And all of the manifests that are associated with your service will get deployed and Envoy will pick the changes up.

For example, a new service, you need to make your proxy aware of it. So there will be some amount of configuration involved either you can do that by hand, or you can do that in an automated way.

**Jeremy:** So it's, it's almost like, adding your service to the system, making it aware that it exists. rather than having to know exactly who you're talking to, that's all handled by, some kind of infrastructure team or by the product.

**Shubheksha:** Yeah. So all of that, like, all of the platform components are basically deployed by a separate team.

**Jeremy:** Hmm. Okay. If you are outside of that team, a lot of this complexity--

**Shubheksha:** Is hidden away from you, yeah. And I have mixed feelings about that.

I feel like as a backend engineer, I would still want to know how things work. And like, part of that is just because I'm a curious person by nature. But like part of it is I, I genuinely think like developers should know where their code is running and how it's running and like the different characteristics of it, like making it too opaque is not really helpful. And like, I think it's needed to be like a holistic all around engineer basically.

**Jeremy:** Yeah, because I wonder how that impacts when there's a problem and you need to debug the problem. How do you determine whether it's something happening on the infrastructure side versus a bug in the code? That sort of thing.

**Shubheksha:** Yeah. So that can be a tricky one. Like you have to go through like multiple layers of investigation to figure out at what level the problem is like you usually start with the code and when, like, and also depending on like your monitoring and alerting, like, if it's something really clear that like a node is down, then you know that yes, it is an infrastructure problem.

But if like the error rate is high. Then it is very likely to be a code problem, but yeah, like in some cases it can be very difficult to figure out like, what is actually going on and like, what is the symptom and what is the cause.

**Jeremy:** And in the context of a distributed system, are there specific tools or strategies you would use to try and figure out what's going on?

**Shubheksha:** So this really depends on the system and like how well it's monitored. Like. my main takeaway was that like observability and monitoring should be a first class citizen of the design process, rather than an afterthought that you just add in, after you're done building the entire system, like that goes a long, long way in helping people debug because like, as, as a team grows or as a company grows and as the system grows,  it can get so unwieldy that it, it can be super hard to keep track of what's going on and what, what is being added where. That's one of my main, main takeaways that yes, you should always think about observability, right from the start rather than treating it like an afterthought.

And in terms of like investigation, I'm not really sure if there are like specific tactics I would use. Like that's just something. Like you watch and learn other people do. And like it's so specific to the technologies and the kind of platform that you're dealing with. But yeah, like the best thing I have found about like incidents and like on call and all of that is that you just, you have to watch a lot of people who are really good at it. Do it again and again, and again, ask them questions and like, see what workflows and mental models they have and like the kind of patterns that they have built over time. And just go from there. 

It starts to makes sense after a while like, initially it just seems like magic you just keep staring and you're like, how did this person know that, you know, this is where they had to look. And like that's where the bug was. I like to think about it as like, you just have to form mental models. Like the more familiar you are with something the stronger your mental models are. And like you have to update them. with time with changes, all sorts of things and they just stick after a while.

**Jeremy:** Do you have any specific examples of a time you were trying to debug something and some of the steps that you took and trying to resolve it?

**Shubheksha:** Oh yeah, after like I was, I used to be on the, on call rotation at Monzo. So like I was involved in lots of incidents and like, usually we had pretty decent run books, about like, what to do when a spe specific alert went off.

So we used to just usually follow the steps and if we were like completely out of our depth, then try a bunch of things. Throw darts randomly and see what sticks. Like sometimes you just don't know what else you can do. Like every outage is not like super straightforward, super simple. You have to like, look around, hit at like five different things and like see where it hurts basically. So yeah.

**Jeremy:** And in terms of the run books you were mentioning, would that be a case where there was a problem previously and then somebody, documented how they fixed the problems, then you would address that the same way next time?

**Shubheksha:** Usually yes, usually yes. Or something like if like something was being tested and there's a very clear process to like, test whether it's working or not. Something like that would be documented as a runbook as well.

**Jeremy:** Can you give us a little bit of a picture of specifics in terms of, are you SSH going into machines or are you looking at a bunch of log files? What, what is, uh, that troubleshooting process often look like?

**Shubheksha:** I'm not sure if I'm supposed to talk about this, especially because I'm not at Monzo anymore, so yeah, I'd be a little cautious talking about that right now.

**Jeremy:** Okay. That's fair. You had mentioned observability being really important before. what are some examples of things that you can add to your services or add to your infrastructure to make this debugging process a lot easier?

**Shubheksha:** So one of the main things that, uh, I think work great in practice is error budgets. Having some sort of definition of this is what is acceptable in terms of a particular service or a particular system returning errors. And like, if it crosses that threshold, then it's like, yes, this is our priority. We need to fix it. 

Like a lot of the SRE (Site Reliability Engineering) work can not be postponed indefinitely, which is what happens in a lot of companies. That are trying to do SRE but badly. So, yeah, so like that's something that I really like as a philosophy. in terms of like monitoring, I think what I'm trying to get at, when I say that like monitoring should be a first class citizen, is that you should be very clear about the output that you expect from the system or what does healthy, not healthy look like for your system, because if you have that, then you can derive metrics from it and vice versa. If you're not able to come up with good metrics for your system, then have you looked closely enough at like what the system is trying to achieve?

**Jeremy:** Yeah. I think that idea of error budgets is really interesting because I think a common problem people have is they'll log everything and there will be errors that happen, but people just expect it right? They go, Oh, it's flashing warnings, but don't worry about it. It normalizes it, but nobody really knows when it's an actual problem.

**Shubheksha:** Yup. Yeah. Like, yeah. So basically yeah if you're logging everything and there are errors that are expected errors then yeah how do you differentiate whether an error is an expected error or it's an unexpected error like that's just a slippery slope that you don't really want to tread on.

And people get used to it. Like if a service keeps spewing errors and nobody really cares then if there's an actual outage, it's very easy to dismiss that yeah. that's what this service does and we have seen it before and it wasn't a problem. So yeah. It's probably fine.

**Jeremy:** Like you were saying, it's observing what you expect the system to do. So I guess, would that just be looking at. a normal day and looking at your error rate and seeing if people are able to successfully complete whatever they're trying to do on the system. and then if you actually start receiving, I guess, trouble tickets or you receive complaints from customers, that's when you can determine oh this error rate being this percentage and people complaining at this time means that this is probably a real issue. Something like that?

**Shubheksha:** Yeah, that's a very tricky question to answer because like, yeah, it's, it's hard to know what the right error budget is. Like, that's a much harder question to answer then, you know, just having an error budget. So yeah, like initially, like it it's just playing around and seeing like what sort of throughput the system has, what's the expected load and like all of those things and coming up with some metric and like tweaking it over time as you learn more about the system.

**Jeremy:** And with these systems, I'm assuming there are a lot of different nodes, a lot of different services. How do you debug or kind of work with this sort of system on your own local machine? Like, are you spinning up all these different services and having them talk or do you have some kind of separate testing environment? What does that look like?

**Shubheksha:** Yeah. Usually there is a separate testing or staging environment, which tries to mimic the production environment. And on your local computer, you can usually spin up a bunch of containers. Obviously it's nowhere close to like having an actual copy of the production environment, but for simple enough changes it can work.

But usually there are like testing environment, which will give you most of the same capabilities as a production environment, where you can test changes, but it's like the other problem is keeping them in sync. That's also a really, really hard problem. So a lot of times like staging environments exist, but like even when you're deploying to production after testing and staging, it's like fingers crossed.

I don't really know what's going to happen. We'll just deploy and see what breaks. Because yeah, the environments can divert quite a bit.

**Jeremy:** In terms of the staging environment, would that be where you have a bunch of fake data that's similar to production and then you have tooling to have transactions that would normally occur in production and staging?

**Shubheksha:** So like mimicking stuff as much as possible to whatever extent. Yeah.

**Jeremy:** How would engineers coordinate if you have this staging environment, I don't imagine everybody has their own.

**Shubheksha:** Yeah. That can get that can get tricky as well, because like people can override changes and like if they they're testing at the same time and they don't know, and like they're deploying on the same, the same service, so that's one benefit of microservices that like, if your service is small enough that multiple people will not be working on it at the same time, then you sort of reduce that contention.

But yeah, like if there are multiple people who are working on the same service, then they have to coordinate somehow to just figure out who's using the environment when and like testing stuff. So the other thing is like having some, a small subset of the staging environment given to like every single engineer, but like, yeah, that's, that's obviously not very simple to achieve, especially if you have like an engineering organization that is growing quite a bit.

**Jeremy:** How large was the engineering team at Monzo?

**Shubheksha:** I think it was about 150 engineers.

**Jeremy:** Hmm, 150. Okay. So in your experience, when you were working on a service, were you able to work on it in isolation where you would work out what the contract should be between services. So you didn't actually need to talk to the whole system for a lot of the time? Or what did that look like?

**Shubheksha:** I think most of the time it was like a single person working on a single service. And yeah, if you do, need to work on the same service with someone else, and usually it was, it was never more than two people in my experience then yeah you just, you coordinate with them and just give them a heads up that yes, you're doing this and you'll be deploying your changes. 

**Jeremy:** And your service most likely is talking to other services. So would that be a part of this design process where you work out what the contract should be and that sort of thing?

**Shubheksha:** Ah, so usually that was pretty straightforward. Like it was a simple RPC. So you do not have to think about it too much. Like you just know that service A will talk to service B to fetch some data XYZ. 

**Jeremy:** So I guess before you started working on the service, you might provide to the other team, or whoever owns that other service here is the protobuf message that I intend to receive and that sort of thing.

**Shubheksha:** Yes. So mostly like if like a service A talking to service B. Service B will have its own handlers and like its own, proto files and all of that. And I just reuse that in my service to talk to service A.

**Jeremy:**  And then likewise, if somebody was talking to your service, you would provide them your proto files or schema.

**Shubheksha:** Yeah.

**Jeremy:** Another thing about having all these different services is I would imagine that they are all being updated at different times.

What are some of the challenges or things that you have to look out for when you're updating services in a distributed system?

**Shubheksha:** The biggest problem is dependencies what depends on what, like the. Dependency graph can be pretty difficult to sort of map out, especially if you have like a really large sprawling system with like dependencies all over the place. If you're deploying, like 4 services, let's say, and like A depends on B, which depends on C. 

That's a problem in any distributed system. Like if you have like especially something modular, like just tracking the dependencies in that entire system can be a huge task. And like, it can inform a lot of other decisions, like in what order do you deploy things?

And like, if you want to remove something, like, it just leads to this rabbit hole because like, yeah, if you want to delete a service, you need to first figured out, like if it's if there's anything else that's depending on it, otherwise a bunch of things will break and you won't really realize that.

**Jeremy:** And how do you, keep track of that. Is there some kind of chart or some kind of document? Like how do people know what they can change?

**Shubheksha:** A lot of it is just in people's heads. Like you talk to people who have worked on that part that you're working on. And like, they'll usually be pretty familiar with like the sort of dependencies that exist. I think. We tried to like map out all of the dependencies at once and like someone posted about this on Twitter as well.

But like, they actually tried to create a dependency graph of like all the services that we had and yeah, it was not a pretty picture,

**Jeremy:** Hmm. Because how many services are we talking about here? Is it like hundreds

**Shubheksha:** 1500

**Jeremy:** 1500 plus. Wow. 

**Shubheksha:** Yep. 

**Jeremy:** That's pretty wild because basically you're relying on maybe going into email or chat and going like, Hey, I'm going to update this service. Uh, which ones might this break?

**Shubheksha:** Yeah. So that can get tricky and that does make like onboarding people a little bit harder. Like there are there are trade offs, both good and bad ones when you have a system like that. It's not all bad. It's not all good.

**Jeremy:** 1500 is-- it seems like nobody at the company could even really know exactly what's happening at that scale. I wonder from your perspective, how do you decide when something should be split off you know  into an individual service versus having a service take care of more things?

**Shubheksha:** Yeah, so that was usually pretty scoped, We try to let a service do one thing and do it well, rather than trying to like, put a bunch of functionality into the same thing. So that, that was usually the rule of thumb that we followed for every new service that we designed.

**Jeremy:** Hm. Cause it seems like a bit of a trade off in that. If there's a problem with that one service, then you have a very localized place on where to work on. But on the other hand, like you said, if you have this dependency graph, you might need to step through 10, 20, 30 services to find the root problem.

**Shubheksha:** Yeah, there were definitely code paths that can get that big and that long. So yeah.

**Jeremy:** In traditional systems, we think of concepts like transactions with a relational database. For example, you may want to update a bunch of different records and have that all complete as one action. When, when you're talking about a distributed system and you need to talk to 5, 10, 20, however many services, how do transactions work in distributed systems?

**Shubheksha:** I'm very tempted to say they don't (laughs). Uh, so yeah, so this is, a really really interesting field within itself, like within distributed systems itself and transactions like distributed transactions are really really hard, like transactions themselves are super hard, even on a single machine. 

And then you like add all of this complexity and you're just like, yeah galaxy brain (laughs) . I'm not super familiar with this topic, but I've read a bit because it's just like super fascinating. And like, usually you try to offload all of that. 

One way you can do it is via a managed service. You don't have to care like where your database is running, how it's running, you just use APIs, you throw stuff at it and you know, it's going to be stored.

There's a bunch of fine tuning and configuration you can do yes. But yeah, you don't know how to think about like the nitty gritty of it. Distributed transactions, like there's also different definitions for it. Like what do you mean? 

I mean, when you say a distributed transaction, like, a transaction, that's executing on multiple machines or transaction, that's like gathering data from multiple machines before returning it to you? A transaction that's I don't know, halted to be executed on different machines? So yeah, it can get really complicated.

**Jeremy:** Yeah, I'm thinking from the perspective of Monzo is a bank, right? So, you might pull money out of an account and transfer it to somebody else like a very basic example. And maybe as a part of that process, you need to talk to 10 different services and let's say on the sixth service call, it fails, but those previous five have already executed whatever they're going to execute.

**Shubheksha:** Ah, right. I see what you mean. Do we roll all of that back? Or like, do we, yeah, so like we did not roll stuff back. But yeah, like you have to account for that in your error handling logic that what happens if it fails at this step and like XYZ has already happened?

**Jeremy:** Could you give like an example of one way you might handle something like that?

**Shubheksha:** Uh, let me think. I'm not sure. I possibly dealt with a situation like that because like all of the tables were scoped to the service that you were working on. So like nobody else, like no other service can access the tables that you had within your service. So that's simplified a lot of things. And usually there was a lot of correlation by IDs.

So like if you're generating flake IDs in one service and it fails and it doesn't generate an id, then it will not be found. And you know something has gone wrong. So you basically just like log and bail and stop proceeding. But obviously around the parts that move money we had a lot more robust error handling around that. Yeah.

**Jeremy:** Yeah. So I guess that's one thing that could help you track, as you were saying, having an ID that passes from service to service. So,

**Shubheksha:** So that's usually accomplished by go's context package. So you have some sort of a trace ID that's like passed through the lifetime of a request all the way down. Uh, so you know, that yes, like all of those calls were part of the same request.

**Jeremy:** Hmm. Okay. And then that would mean that you could go to some kind of logging or monitoring service and actually see, like, these are the five services that we're trying to handle it, and this was the results. I guess there's like two parts there's there's figuring out which services and which calls were part of the same transaction.

And then like you were saying earlier if something goes wrong, how do we correct for it? And yeah, that sounds like a very, very challenging problem (laughs).

**Shubheksha:** Yeah. Yeah. Like one of the main problems with distributed systems is when things go wrong, you don't know what's going to break where. Like a lot of things break and then you just have to like start searching for, okay, what has gone wrong, where, and like something completely different in a completely different part of the system might just be like breaking something else in a completely different part of the system. And like, as your system grows, it's impossible to keep track of all of it in your head, especially like a single person cannot do that.

So it can just be really hard to like, have a big picture view of the system and figure out what's going on, where

**Jeremy:** Mm, and it sounded like in your experience that that knowledge of what was going, where and how things interacted. A lot of that was sort of tribal in a way. Like there were people who, who knew how the pieces fit together. Um, but it's tough to really have this document or this source of truth.

**Shubheksha:** Yeah

**Jeremy:** Yeah, I can imagine that being like you were saying earlier, very difficult in terms of onboarding. Yeah.

**Shubheksha:** Yep.

**Jeremy:** I guess another thing about when you have distributed systems and you have all these different services. Presumably one of the benefits is so that you can scale up certain parts of the system.

I wonder from your perspective, how do you kind of figure out which parts of the systems need to be scaled up and what are some strategies for, if you're really hitting barriers, a performance in a certain part of the system, how you deal with that?

**Shubheksha:** Usually metrics. If you're constantly getting alerts that yes, like a particular node or like a particular part on a particular node is constantly hitting its memory and CPU usage, or, you know, you're going to be performing some sort of like heavy workload on a particular service and you scale it up preemptively or like an alert fires, and then you scale it up.

So that's like a very manual way to go about it. Uh, and in terms of performance constraints. So a lot of that was handled by our infrastructure team and I personally did not work on like fine tuning uh performance as such on any of the parts of the system that I worked on. But like what I saw other people doing, was that like, you have to go on chasing, profiling, and figuring out where that bottleneck is.

And like, sometimes it can just be your bug. That's like, like you're leaking goroutines or something like that, or like you're leaking memory somewhere else. So stuff like that, like usually you just, you have to keep profiling till you figure what's going on and then fix it.

**Jeremy:** And for you as the person who's building the services and handing them off to the infrastructure team, was there any contract or specification written up where you said like, Hey, my service is going to do this. And I think it's going to be able to process this many messages or this many transactions a second.

And then that's how the infrastructure team can figure out how much to scale or how did that work?

**Shubheksha:** Yeah. So there was some amount of load testing that was done for like services that were really, really high throughput with the infrastructure team so that they like were in the loop and like they knew what was going on and they can scale up preemptively.

**Jeremy:** In your experience as a backend engineer, we've talked about the infrastructure team. Are there any other teams that you would find yourself working on a regular basis?

**Shubheksha:** Not really, no, it was mostly backend and and infrastructure. And in some cases security as well. If you needed like a particular like their input on something particular that we were working with.

**Jeremy:** Would they provide some kind of audit to tell you, like, this is where potential issues might be or?

**Shubheksha:** Yeah. Like something like that, or like, if you just need their input on like a particular security strategy, like if you wanted to like store some, critical data or something like that, how do we do that? Or like, what would be the best way to go about it so stuff like that.

**Jeremy:** During your time at Monzo, you were writing systems in, in Go What do you think makes Go a good choice for distributed systems or for the type of work you were doing in general?

**Shubheksha:** One of the main things that I like about it is that it's super easy to pick up. This was my first job with Go like first, full time job. I was learning Go a little before that, but I was able to pick up very, very quickly. I think what attracted people to Go like, this was definitely a huge part of it.

Then the fact that it was backed by Google and, and it wasn't going to like just vanish overnight was also really helpful. And I think, it really started from docker and docker sort of shot into the limelight and it sort of made it the defacto language of cloud native infrastructure and it just kept catching on.

And then Kubernetes came along and then because Kubernetes was written in Go, everything else started to be written in Go. It has a lot of neat features that I think make it uh really really, easy to sort of start building stuff with it. One of them is definitely like how good the standard libraries are and how easy it is to sort of build on top of them.

And like first-class support for concurrency, which can be a huge, huge pain to sort of implement on its own and like a lot of languages don't support those primitives out of the box. Like it's really good for those sorts of use cases as well. And yeah, it's just easy and fun to learn.

**Jeremy:** So basically it was easy for you to step in as a new employee, and start learning how services work just because the language was easy to pick up. um, and yeah, that, that built in support for concurrency. I wonder, are there any things compared to your experience with other languages where you, that you didn't like about go.

**Shubheksha:** Mmm, I think, yeah, this is, this is like a very common and controversial opinion, uh, in the go community, but like sometimes it can feel very repetitive like, especially the error handling bits where you're like constantly checking for errors. I can appreciate explicit error handlings but like, yeah, sometimes it can just feel like you're writing the same block of code, like 50 times in the same file.

And that can be a little bit annoying. It's super verbose. Like it just, verbose, not in the Java sense, but more in the, you should know what you're doing sense, like, it tries to be as simple as possible rather than being as clever as possible and making things harder to understand 

**Jeremy:** And the the error example you were giving, I'm assuming that's because go doesn't have exceptions. Is that right?

**Shubheksha:** Yes, Go does not have a concept of exceptions at all. you're supposed to do  explicitly check for errors every single step and then decide what you're going to do. So in a way, it sort of makes you think harder about like the ways in which your code fails and what you're supposed to do after that, which is a good thing.

**Jeremy:** Right in some cases you have a very deeply nested call stack, And you might be accustomed to throwing an exception deep and at the, outer level, just handling that. Um, but with Go at every single level of the stack. You would need to check the error.

What do I want to return or, yeah okay.

**Shubheksha:** So you have to bubble the error up. You need to make sure you're bubbling the right error up. You have to augment it with all of the information and the metadata that you need, which will help you debug the problem no matter at what layer it occurred at so that can definitely be sometimes tricky.

**Jeremy:** Yeah, I can definitely see, um, I guess why it'd be good and bad. Maybe we should move on to you recently wrote a post about the lessons you learned in your third year as being a software engineer. I thought we could go through a few of those points and maybe, get into where you're coming from with those. I think the first point you had mentioned was just doing things like working on projects and doing the work isn't enough. You have to know how to, how to market it as well.

**Shubheksha:** Yeah.

**Jeremy:** You had talked about marketing to the right people. are you talking about people who are internal at your company or outside and, and how do you find what you consider to be the right people?

**Shubheksha:** Oh, that's a really good point. I think it's a bit of both like internally in terms of like progression and like the stakeholders of your project and all of the other people that you work on on a day to day basis. And externally just to build a network and like, let people know what you're working on and what you're learning.

Like I'm a huge fan of like learning in public in general. That's just something that brings a lot of good things your way if you do it right.

**Jeremy:** Things like blog posts or conference talks, things like that.  Another thing you mentioned was how, how titles matter. And I know that there's a lot of discussion where people say like, Oh, it doesn't really matter. But, um, you were saying like, they really do matter. And. from your perspective, how dod the roles of, of titles change from, from company to company?

**Shubheksha:** I think it. It really depends on the size of the company as well. Uh, that's one of the main factors, like how well established the company is, how many engineers do they have? Like how much do they like place weight on the title internally? Like there are companies where like there are meetings, which are exclusively for people who have a certain level or a certain title.

So in that case, like, it's very obvious that if you don't get promoted then you get you're stuck, you're losing out because you're literally not allowed to attend. A certain set of meetings that you would probably benefit from. And in, in like in other ways it can also like halt your progression. And when I say titles matter, I don't say that.

Like, just because you're a senior engineer, you know, more I don't believe in like, just number of, years of experience, it's about the quality of the work that you have done more than like just the sheer amount of time that you've put in. But. In terms of like how people perceive you, what they expect from you and what they assume about you definitely shifts when you have like a title attached to your name.

**Jeremy:** And in your career or just in people's careers in general, how much, weight or priority should people put into making sure that they, they have like a. impressive title or a high title. especially when you think about, you were saying how it changes between the size of the organization.

Um, somebody who's a CTO at a three person company it's not the same as at a 5,000 person company. I wonder what your thoughts are on that.

**Shubheksha:** Uh, yeah, that's a really good question. I think like what I mentioned in the next point is that it, it's very easy to get caught up in that, in the climb. Like when it comes to career ladders, but that can also be very detrimental and that relates directly to the fact that it's not just years of experience, it's actually the quality of those years of experience that actually counts towards like how good you are.

If you, if you run after two months, it can just be like a second full time job. It can completely drain you. You'll stop learning, you stop actually doing what you enjoy. And you'll just blindly chase a title. Like that's not a good position to be in because like, you have to balance it out. 

At the same time if you feel like you're just getting stuck, you're not getting promoted. You're not getting to the level you want to be at. It might just be time to like, change. And see what's out there, and if there's someone who will treat you better, but like, it really depends on what you value more because a title change can bring you better job prospects, especially if it's a change from like just software engineer to senior software engineer, then you just have to much wider pool of roles available to you. So it really depends on the stage of the career you're at. And what do you value personally?

**Jeremy:** In your posts, you had talked about chasing promotions, What are some of the things that you might find yourself doing that are more going for the promotion rather than growing yourself? technically or, you know, skill wise?

**Shubheksha:** That depends on what your company values and what do they base promotions on? So like if they have a very rigid structure where it's like a bunch of check boxes that you have to tick, then a lot of people will try to game that system. And they'll just try to do things maybe at the expense of their growth, as well as the expense of what's good for the company just to get ahead and get promoted.

So that's not beneficial for the employee or the company. But yeah, like a lot of, frameworks that are like of that fashion, where you have to check a bunch of boxes in order to get promoted often like end up in people doing things that they are being incentivized to, but in a very wrong way,

**Jeremy:** Right. So I guess it's looking at what your organization's process is and figuring out is it, you know, some of it is not the stuff you want to do, but you just kind of get it done and you can move on or whether the process it's so, difficult.

And, and so, um, um broken, yeah, basically, uh, that it's worth just moving on to another, another organization. Your, your next point, I think was about, uh, how sponsors are so important. And I wonder if you could explain a little bit about what you mean by a sponsor versus, a mentor or somebody else?

**Shubheksha:** Yeah. So the difference between uh sponsors and mentors is that I think mentors, the way I think about it at least is that mentors are very passive in the way they help you vs sponsors are very active. Like mentors will be there for you. They will help you. You can go ask them questions, whereas with sponsors, they will actively put your name in the hat for opportunities help you connect with people and like send opportunities that they think are a good fit your way, and they will be your advocate.

Rather than you having to ask your mentor to be your advocate. So I think that's, that's the main difference. And like, there's also the question of sort of like the sponsor's reputation being at stake in a certain sense that they, they basically take a chance on you and they trust you enough to put their reputation on the line in order to do right and good by you, which is not the case with mentors.

**Jeremy:** It sounds like a sponsor would be someone who is vouching for you, right. Or is giving you recommendations. 

**Shubheksha:** Yes, essentially. Yeah. Someone who watches for you in like rooms either you're not in, is familiar with your work, actively advocates for it.

**Jeremy:** Hmm. And that could be someone within your organization, for example, saying, I think that you would be a great fit for this project and telling other managers about that, or it could even be someone outside of your work, just saying if you're looking for a position or something, they might say, Oh, I know somebody who would be a great fit for this conference talk or this job, that, that sort of thing.

**Shubheksha:** Precisely. Yeah.

**Jeremy:** Do you have any specific advice for how people should.. I don't know if seek out is the right word but to build up a network of sponsors,

**Shubheksha:** I get that a lot. And I have a blog post in the works for it, which I'm trying to think about, but like, it's really hard to put in words, like it's just like a lot of networking and like reaching out to people and like slowly and steadily sort of surrounding yourself with people that you can admire and look up to and who will be like willing to vouch for you.

So like there's no direct, straight method to do it. I can't prescribe like if you follow step one, two, three, that, yes, you'll definitely have it. I think it's just, it just takes time on a lot of effort and patience, because I remember at like, when I started, like, I was desperately looking for mentors and I was just like reaching out to people and I just felt like I could do so much if I just needed the guidance and it was really really hard to find.

So yeah, like I completely empathize with like people who are struggling with it at the moment. And it's, it's really hard. A lot of people are like super busy. They don't have time. And so it's it can just feel like bad to sort of ask for their time as well. So, yeah, that's also something I definitely struggle with, but like don't have concrete steps, at the moment, will, hopefully have something to say and publish it in a blog post.

**Jeremy:** Yeah. I mean, I wonder from your personal experience, I remember a few years ago you went on a few podcasts to talk about your experience, getting into open source and things like that.

You know, looking back on the process you went through, is that a path that you would recommend to other people, or do you have thoughts on how you might have approached that differently now?

**Shubheksha:** I think I got very lucky at like some steps. Like I did not set out I did not plan it out uh that way it just sort of happened. And yeah. So like, I don't think I would take a different path. Like I like along the way, especially via open source like I met so many great people who have been amazing mentors and sponsors for me, but like I did not seek them out.

The, the other thing that I realized was like, you can't meet people and be like, Oh, you're my mentor. Like, that's a relationship. That's built over time as you learn from each other. And the other thing is, yeah, it's a two way relationship. It's not just you leeching off the other person and like trying to, you know, like all, like take away all of their knowledge and like sort of embedded it in your brain.

That's not how it works. Like even if you have less knowledge compared to the other person, they can still learn something from you and like, it's always good to have that mindset rather than, you know, the hero mindset where you're like, Oh my God, this person is, is God. And like, I want to learn everything from them like that doesn't help.

Like placing people on a pedestal, basically. Like it eases the pressure on them as well. And it helps you be more comfortable too. So like a lot of my mentor, like sponsor relationships are like that where we have a bunch of like mutual interests and we talk about it and we learn from each other. So like a lot of them are like, not even like formalized, like we never, like had a conversation where we were like, Oh, like, we are like a mentor and a mentee now, like a sponsor and a sponsee now, like yeah, you just, you sort of build those kind of bonds with people and where they feel comfortable watching for you.

And you just take it from there.

**Jeremy:** That makes a lot of sense just because relationships in general are very much, it's not you meet somebody and you go, we are going to be friends, right? 

**Shubheksha:** It just takes time. Yeah.

**Jeremy:** Yeah. So I can see how it'd be too difficult to pin down what are the steps you should take? I'm looking forward to the blog posts though.

**Shubheksha:** Yeah. Thank you.

**Jeremy:** I think the last thing you had mentioned in the post was you were talking about how programming got easier over time. And I wonder, were there any specific milestones you remember of things that were really hard and then it, all of a sudden, it just clicked over the years

**Shubheksha:** I think uh one of the main things I remember was like, just on designing containers and how they work. Like it was literally like a light bulb moment with where like I just, I just felt like, yes, I finally understand what it is. And like, there have been times over the years where I have felt like that without like actively trying to something that I've experienced very frequently is like, I learn about something.

Like say right now and I'll understand maybe like 40% of it. And then I'll come back and revisit it, like from another topic or like an adjacent topic. And I finally understand it and maybe I've been like working with it or around it in the intervening months, but like, it's not like I sat down and I tried to like, learn about it or anything like that.

But like when you're understanding builds up. During the intervening time, you sort of realize that you've not only learned the thing that you were actually learning, but a lot of adjacent concepts also makes sense. And it can be very hard to have this perspective when you're starting out because you're just like, none of this makes sense, like what is going on.

But yeah, it, like your understanding sort of grows and compounds in a similar way to money, I would say. And it's very hard to remember that when you're just starting out.

**Jeremy:** Yeah, I can definitely relate to that where I think it's, it's very difficult. And I think a lot of people want to be able to sit down and read a book or go through a course and go like, okay, I now know this thing. Uh, but I have the same experience with you where, uh, it's just working on problems that are not even hitting.

Always the main thing, but it's related to it and all of a sudden it might suddenly click. Yeah.

**Shubheksha:** Yeah.

**Jeremy:** Cool. Well, I think that's a good place to wrap up, but are there any other things you, uh, you'd like to mention or think we should have talked about.

**Shubheksha:** No, I think we covered a lot of ground and it was really fun chat thank you so much.

**Jeremy:** Cool. where can people follow you online to see what you're up to and what you're you're going to be doing next?

**Shubheksha:** they can follow me on Twitter. Uh, that's where I'm most active. Uh, my handle is scribblingon, I have a website which is shubheksha dot com and that's where I post all of my writing.

**Jeremy:** Cool. Shubheksha, thank you so much for joining me today.

**Shubheksha:** Thank you so much.

</div>