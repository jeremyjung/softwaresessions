+++
title = "Paul Frazee on Bluesky and ATProto"

description = "Building a decentralized social network"

[extra]
episode_url = "https://pinecast.com/listen/042a1259-9a40-4f0e-868c-395946e8e8c1.mp3"
social_title = "Paul Frazee on Bluesky and ATProto"
social_banner = "057-paul-frazee.png"
social_description = "Building a decentralized social network"
+++

Paul Frazee is the CTO of Bluesky. He previously worked on the Beaker browser and the peer-to-peer social media protocol Secure Scuttlebutt.

Paul discusses how Bluesky and ATProto got started, scaling up a social media site, what makes ATProto decentralized, lessons ATProto learned from previous peer-to-peer projects, and the challenges of content moderation.

This episode originally aired on Software Engineering Radio.


## Related Links

- [Bluesky](https://bsky.app/)
- [ATProtocol](https://atproto.com/)
- [ATProto for distributed systems engineers](https://atproto.com/articles/atproto-for-distsys-engineers)
- [Bluesky and the AT Protocol: Usable Decentralized Social Media](https://arxiv.org/abs/2402.03239)
- [Decentralized Identifiers (DIDs)](https://www.w3.org/TR/did-core/)
- [ActivityPub](https://www.w3.org/TR/activitypub/)
- [Webfinger](https://datatracker.ietf.org/doc/html/rfc7033)
- [Beaker web browser](https://en.wikipedia.org/wiki/Beaker_(web_browser))
- [Secure Scuttlebutt](https://scuttlebutt.nz)

--

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

[00:00:00] **Jeremy:** Today I am talking to Paul Frazee. He's the current CTO of bluesky, and he previously worked on other decentralized applications like Beaker and Secure Scuttlebutt.

[00:00:15] **Paul:** Thanks for having me.


## What's bluesky

[00:00:16] **Jeremy:** For people who aren't familiar with bluesky, what is it?

[00:00:20] **Paul:** So bluesky is an open social network, simplest way to put it, designed in particular for high scale. That's kind of one of the big requirements that we had when we were moving into it. and it is really geared towards making sure that the operation of the social network is open amongst multiple different organizations.

[00:00:44] So we're one of the operators, but other folks can come in, spin up the software, all the open source software, and essentially have a full node with a full copy of the network active users and have their users join into our network. And they all work functionally as one shared application.

[00:01:03] **Jeremy:** So it, it sounds like it's similar to Twitter but instead of there being one Twitter, there could be any number and there is part of the underlying protocol that allows them to all connect to one another and act as one system.

[00:01:21] **Paul:** That's exactly right. And there's a metaphor we use a lot, which is comparing to the web and search engines, which actually kind of matches really well. Like when you use Bing or Google, you're searching the same web. So on the AT protocol on bluesky, you use bluesky, you use some alternative client or application, all the same, what we're we call it, the atmosphere, all one shared network, 

[00:01:41] **Jeremy:** And more than just the, the client. 'cause I think sometimes when people think of a client, they'll think of, I use a web browser. I could use Chrome or Firefox, but ultimately I'm connecting to the same thing. But it's not just people running alternate clients, right?

[00:01:57] **Paul:** Their own full backend to it. That's right. Yeah. Yeah. The anchoring point on that being the fire hose of data that runs the entire thing is open as well. And so you start up your own application, you spin up a service that just pipes into that fire hose and taps into all the activity.


## History of AT Protocol

[00:02:18] **Jeremy:** Talking about this underlying protocol maybe we could start where this all began so people get some context for where this all came from.

[00:02:28] **Paul:** For sure. All right, so let's wind the clock back here in my brain. We started out 2022, right at the beginning of the year. We were formed as a, essentially a consulting company outside of Twitter with a contract with Twitter. And, uh, our goal was to build a protocol that could run, uh, Twitter, much like the way that we just described, which set us up with a couple of pretty specific requirements.

[00:02:55] For one, we had to make sure that it could scale. And so that ended up being a really important first requirement. and we wanted to make sure that there was a strong kind of guarantees that the network doesn't ever get captured by any one operator. The idea was that Twitter would become the first, uh, adopter of the technology.

[00:03:19] Other applications, other services would begin to take advantage of it and users would be able to smoothly migrate their accounts in between one or the other at any time. Um, and it's really, really anchored in a particular goal of just deconstructing monopolies. Getting rid of those moats that make it so that there's a kind of a lack of competition, uh, between these things.

[00:03:44] And making sure that, if there was some kind of reason that you decided you're just not happy with what direction this service has been going, you move over to another one. You're still in touch with all the folks you were in touch with before. You don't lose your data. You don't lose your, your your follows. Those were the kind of initial requirements that we set out with. The team by and large came from, the decentralized web, movement, which is actually a pretty, large community that's been around since, I wanna say around 2012 is when we first kind of started to form. It got really made more specifically into a community somewhere around 2015 or 16, I wanna say.

[00:04:23] When the internet archives started to host conferences for us. And so that gave us kind of a meeting point where all started to meet up there's kind of three schools of thought within that movement. There was the blockchain community, the, federation community, and the peer-to-peer community.

[00:04:43] And so blockchain, you don't need to explain that one. You got Federation, which was largely ActivityPub Mastodon. And then peer-to-peer was IPFS, DAT protocol, um, secure scuttlebutt. But, those kinds of BitTorrent style of technologies really they were all kind of inspired by that.

[00:05:02] So these three different kind of sub communities we're all working, independently on different ways to attack how to make these open applications. How do you get something that's a high scale web application without one corporation being the only operator? When this team came together in 2022, we largely sourced from the peer-to-peer group of the decentralized community.


## Scaling limitations of peer-to-peer

[00:05:30] **Paul:** Personally, I've been working in the space and on those kinds of technologies for about 10 years at that stage. And, the other folks that were in there, you know, 5-10 each respectively. So we all had a fair amount of time working on that. And we had really kind of hit some of the limitations of doing things entirely using client devices. We were running into challenges about reliability of connections. Punching holes to the individual device is very hard. Synchronizing keys between the devices is very hard. Maintaining strong availability of the data because people's devices are going off and on, things like that. Even when you're using the kind of BitTorrent style of shared distribution, that becomes a challenge.

[00:06:15] But probably the worst challenge was quite simply scale. You need to be able to create aggregations of a lot of behavior even when you're trying to model your application as largely peer wise interactions like messaging. You might need an aggregation of accounts that even exist, how do you do notifications reliably?

[00:06:37] Things like that. Really challenging. And what I was starting to say to myself by the end of that kind of pure peer-to-peer stent was that it can't be rocket science to do a comment section. You know, like at some point you just ask yourself like, how, how hard are we willing to work to, to make these ideas work?

[00:06:56] But, there were some pretty good pieces of tech that did come out of the peer-to-peer world. A lot of it had to do with what I might call a cryptographic structure. things like Merkel trees and advances within Merkel Trees. Ways to take data sets and reduce them down to hashes so that you can then create nice signatures and have signed data sets at rest at larger scales.

[00:07:22] And so our basic thought was, well, all right, we got some pretty good tech out of this, but let's drop that requirement that it all run off of devices. And let's get some servers in there. And instead think of the entire network as a peer-to-peer mesh of servers. That's gonna solve your scale problem.

[00:07:38] 'cause you can throw big databases at it. It's gonna solve your availability problems, it's gonna solve your device sync problems. But you get a lot of the same properties of being able to move data sets between services. Much like you could move them between devices in the peer-to-peer network without losing their identifiers because you're doing this in direction of, cryptographic identifiers to the current host.

[00:08:02] That's what peer-to-peer is always doing. You're taking like a public key or hash and then you're asking the network, Hey, who has this? Well, if you just move that into the server, you get the same thing, that dynamic resolution of who's your active host. So you're getting that portability that we wanted real bad.

[00:08:17] And then you're also getting that kind of in meshing of the different services where each of them is producing these data sets that they can sink from each other. So take peer-to-peer and apply it to the server stack. And that was our kind of initial thought of like, Hey, you know what? This might work.

[00:08:31] This might solve the problems that we have. And a lot of the design fell out from that basic mentality.


## Crytographic identifiers and domain names

[00:08:37] **Jeremy:** When you talk about these cryptographic identifiers, is the idea that anybody could have data about a person, like a message or a comment, and that could be hosted different places, but you would still know which person that originally came from. Is that, is that the goal there? 

[00:08:57] **Paul:** That's exactly it. Yeah. Yeah. You wanna create identification that supersedes servers, right? So when you think about like, if I'm using Twitter and I wanna know what your posts are, I go to twitter.com/jeremy, right? I'm asking Twitter and your ID is consequently always bound to Twitter. You're always kind of a second class identifier.

[00:09:21] We wanted to boost up the user identifier to be kind of a thing freestanding on its own. I wanna just know what Jeremy's posts are. And then once you get into the technical system it'll be designed to figure out, okay, who knows that, who can answer that for you? And we use cryptographic identifiers internally.

[00:09:41] So like all the data sets use these kind of long URLs to identify things. But in the application, the user facing part, we used domain names for people. Which I think gives the picture of how this all operates. It really moves the user accounts up into a free standing first class identifier within the system.

[00:10:04] And then consequently, any application, whatever application you're using, it's really about whatever data is getting put into your account. And then that just exchanges between any application that anybody else is using.

[00:10:14] **Jeremy:** So in this case, it sounds like the identifier is some long string that, I'm not sure if it's necessarily human readable or not. You're shaking your head no.

[00:10:25] **Paul:** No.

[00:10:26] **Jeremy:** But if you have that string, you know it's for a specific person. And since it's not really human readable, what you do is you put a layer on top of it which in this case is a domain that somebody can use to look up and find the identifier.

[00:10:45] **Paul:** Yeah, yeah, yeah. So we just use DNS. Put a TXT record in there, map into that long string, or you could do a `.well-known` file on a web server if that's more convenient for you. And then the ID that's behind that, the non-human readable one, those are called DIDs which is actually a W3C spec. Those then map to a kind of a certificate. What you call a DID document that kind of confirms the binding by declaring what that domain name should be. So you get this bi-directional binding. And then that certificate also includes signing keys and active servers. So you pull down that certificate and that's how the discovery of the active server happens is through the DID system.


## What's stored on a PDS

[00:11:29] **Jeremy:** So when you refer to an active server what is that server and what is that server storing?

[00:11:35] **Paul:** It's kinda like a web server, but instead of hosting HTML, it's hosting a bunch of JSON records. Every user has their own document store of JSON documents. It's bucketed into collections. Whenever you're looking up somebody on the network you're gonna get access to that repository of data, jump into a collection.

[00:11:58] This collection is their post collection. Get the rkey (Record Key), and then you're pulling out JSON at the end of it, which is just a structured piece of stuff saying here's the CreatedAt, here's the text, here's the type, things like that. One way you could look at the whole system is it's a giant, giant database network.


## Servers can change, signing keys change, but not DID

[00:12:18] **Jeremy:** So if someone's going to look up someone's identifier, let's say they have the user's domain they have to go to some source, right? To find the user's data. You've mentioned, I think before, the idea that this is decentralized and by default I would, I would picture some kind of centralized resource where I send somebody a domain and then they give me back the identifier and the links to the servers.

[00:12:46] So, so how does that work in practice where it actually can be decentralized?

[00:12:51] **Paul:** I mentioned that your DID that non-human readable identifier, and that has that certificate attached to it that lists servers and signing keys and things like that.

[00:13:00] So you're just gonna look up inside that DID document what that server is your data repository host. And then you contact that guy and say, all right, I'm told you're hosting this thing. Here's the person I'm looking for, hand over the hand over the data. It's really, you know, pretty straightforward.

[00:13:18] The way that gets decentralized is by then to the fact that I could swap out that active server that's in my certificate and probably wanna rotate the signing keys 'cause I've just changed the, you know. I don't want to keep using the same signing keys as I was using previously because I just changed the authority.

[00:13:36] So that's the migration change, change the hosting server, change out the signing keys. Somebody that's looking for me now, they're gonna load up my document, my DID document. They're gonna say, okay, new server, new keys. Pull down the data. Looks good, right? Matches up with the DID doc.

[00:13:50] So that's how you get that level of portability. But when those changes happen, the DID doesn't change, right? The DID document changes. So there's the level of indirection there and that's pretty important because if you don't have a persistent identifier whenever you're trying to change out servers, all those backlinks are gonna break.

[00:14:09] That's the kind of stuff that stops you from being able to do clean migrations on things like web-based services. the only real option is to go out and ask everybody to update their data. And when you're talking about like interactions on the social network, like people replying to each other, there's no chance, right?

[00:14:25] Every time somebody moves you're gonna go back and modify all those records. You don't even control all the records from the top down 'cause they're hosted all over the web. So it's just, you can't do it. Generally we call this account portability, that you're kinda like phone number portability that you can change your host, but, so that part's portable, but the ID stays the same.

[00:14:45] And keeping that ID the same is the real key to making sure that this can happen without breaking the whole system.

[00:14:52] **Jeremy:** And so it, it sounds like there's the decentralized id, then there's the decentralized ID document that's associated with that points you to where the actual location of your, your data, your posts, your pictures and whatnot. but then you also mentioned that they could change servers.

[00:15:13] So let's say somebody changes where their data is, is stored, that would change the servers, I guess, in their document. But 

[00:15:23] then how do all of these systems. Know okay. I need to change all these references to your old server, to these new servers, 

[00:15:32] **Paul:** Yeah. Well, the good news is that you only have to, you, you got the public data set of all the user's activity, and then you have like internal caches of where the current server is. You just gotta update those internal caches when you're trying to contact their server. Um, so it's actually a pretty minimal thing to just like update like, oh, they moved, just start talking to update my, my table, my Redis, that's holding onto that kind of temporary information, put it on ttl, that sort of thing.


## Most communication won't be between servers, it will be from event streams

[00:16:01] **Paul:** And, honestly, in practice, a fair amount of the system for scalability reasons doesn't necessarily work by servers directly contacting each other. It's actually a little bit more like how, I told you before, I'm gonna use this metaphor a lot, the search engines with the web, right? What we do is we actually end up crawling the repositories that are out in the world and funneling them into event streams like a Kafka. And that allows the entire system to act like a data processing pipeline where you're just tapping into these event streams and then pushing those logs into databases that produce these large scale aggregations.

[00:16:47] So a lot of the application behavior ends up working off of these event logs. If I reply to somebody, for instance, I don't necessarily, it's not, my server has to like talk to your server and say, Hey, I'm replying to you. What I do is I just publish a reply in my repository that gets shot out into the event logs, and then these aggregators pick up that the reply got created and just update their database with it.

[00:17:11] So it's not that our hosting servers are constantly having to send messages with each other, you actually use these aggregators to pull together the picture of what's happening on the network.

[00:17:22] **Jeremy:** Okay, so like you were saying, it's an event stream model where everybody publishes the events the things that they're doing, whether that's making a new post, making a reply, that's all being posted to this event stream. And then everybody who provides, I'm not sure if instances is the right term, but an implementation of the atmosphere protocol (Authenticated Transfer protocol).

[00:17:53] They are listening for all those changes and they don't necessarily have to know that you moved servers because they're just listening for the events and you still have the same identifier.

[00:18:10] **Paul:** Generally speaking. Yeah. 'cause like if you're listening to one of these event streams what you end up looking for is just the signature on it and making sure that the signature matches up. Because you're not actually having to talk to their live server. You're just listening to this relay that's doing this aggregation for you.

[00:18:27] But I think actually to kind of give a little more clarity to what you're talking about, it might be a good idea to refocus how we're talking about the system here. I mentioned before that our goal was to make a high scale system, right? We need to handle a lot of data. If you're thinking about this in the way that Mastodon does it, the ActivityPub model, that's actually gonna give you the wrong intuition.

## Designing the protocol to match distributed systems practices (Event sourcing / Stream processing)

[00:18:45] **Paul:** 'cause we chose a dramatically different system. What we did instead was we picked up, essentially the same practices you're gonna use for a data center, a high scale application data center, and said, all right, how do you tend to build these sorts of things? Well, what you're gonna do is you're gonna have, multiple different services running different purposes.

[00:19:04] It gets pretty close to a microservices approach. You're gonna have a set of databases, and then you're going to, generally speaking for high scale, you're gonna have some kind of a kafka, some kind of a event log that you are tossing changes about the state of these databases into. And then you have a bunch of secondary systems that are tapping into the event log and processing that into, the large scale, databases like your search index, your, nice postgres of user profiles.

[00:19:35] And that makes sure that you can get each of these different systems to perform really well at their particular task, and then you can detach them in their design. for instance, your primary storage can be just a key value store that scales horizontally. And then on the event log, you, you're using a Kafka that's designed to handle.

[00:19:58] Particular semantics of making sure that the messages don't get dropped, that they come through at a particular throughput. And then you're using, for us, we're using like ScyllaDB for the big scale indexes that scales horizontally really well. So it's just different kind of profiles for different pieces.

[00:20:13] If you read Martin Kleppman's book, data Intensive applications I think it's called or yeah. A lot of it gets captured there. He talks a lot about this kind of thing and it's sometimes called a kappa architecture is one way this is described, event sourcing is a similar term for it as well.

[00:20:30] Stream processing. That's pretty standard practices for how you would build a traditional high scale service. so if you take, take this, this kind of microservice architecture and essentially say, okay, now imagine that each of the services that are a part of your data center could be hosted by anybody, not just within our data center, but outside of our data center as well and should be able to all work together.

[00:20:57] Basically how the AT Proto is designed. We were talking about the data repository hosts. Those are just the primary data stores that they hold onto the user keys and they hold onto those JSON records. And then we have another service category we call Relay that just crawls those data repositories and sucks that in that fire hose of data we were talking about that event log.


## App views pull data from relay and produces indexes and threads

[00:21:21] **Paul:** And then we have what we call app views that sit there and tail the index and tail the log, excuse me, and produce indexes off of it, they're listening to those events and then like, making threads like okay, that guy posted, that guy replied, that guy replied.

[00:21:37] That's a thread. They assemble it into that form. So when you're running an application, you're talking to the AppView to read the network, and you're talking to the hosts to write to the network, and each of these different pieces sync up together in this open mesh. So we really took a traditional sort of data center model and just turned it inside out where each piece is a part of the protocol and communicate it with each other and therefore anybody can join into that mesh.

[00:22:07] **Jeremy:** And to just make sure I am tracking the data repository is the data about the user. So it has your decentralized identifier, it has your replies, your posts, And then you have a relay, which is, its responsibility, is to somehow find all of those data repositories and collect them as they happen so that it can publish them to some kind of event stream.

[00:22:41] And then you have the AppView which it's receiving messages from the relay as they happen, and then it can have its own store and index that for search. It can collect them in a way so that it can present them onto a UI. That's sort of thing that's the user facing part I suppose.

[00:23:00] **Paul:** Yeah, that's exactly it. And again, it's, it's actually quite similar to how the web works. If you combine together the relay and the app view, you got all these different, you know, the web works where you got all these different websites, they're hosting their stuff, and then the search engine is going around, aggregating all that data and turning it into a search experience.

[00:23:19] Totally the same model. It's just being applied to, more varieties of data, like structured data, like posts and, and replies, follows, likes, all that kinda stuff. And then instead of producing a search application at the end. I mean, it does that too, but it also produces a, uh, you know, timelines and threads and, um, people's profiles and stuff like that.

[00:23:41] So it's actually a pretty bog standard way of doing, that's one of the models that we've seen work for large scale decentralized systems. And so we're just transposing it onto something that kind of is more focused towards social applications

[00:23:58] **Jeremy:** So I think I'm tracking that the data repository itself, since it has your decentralized identifier and because the data is cryptographically signed, you know, it's from a specific user. I think the part that I am still not quite sure about is the relays. I, I understand if you run all the data repositories, you know where they are, so you know how to collect the data from them.

[00:24:22] But if someone's running another system outside of your organization, how do they find, your data repositories? Or do they have to connect to your relay? What's the intention for that?


## Data hosts request relays to pull their data

[00:24:35] **Paul:** That logic runs, again, really similar to how search engines find out about websites. So there is actually a way for, one of these, data hosts to contact Relay and say, Hey, I exist. You know, go ahead and get my stuff. And then it'll be up to the relay to decide like if they want it or not.

[00:24:52] Right now, generally we're just like, yeah, you know, we, we want it. But as you can imagine, as the thing matures and gets to higher scale, there might be some trust kind of things to worry about, you know? So that's kind of the naive operation that currently exists. But over time as the network gets bigger and bigger, it'll probably involve some more traditional kind of spiraling behaviors because as more relays come into the system, each of these hosts, they're not gonna know who to talk to.


## Relays can bootstrap who they know about by talking to other relays

[00:25:22] **Paul:** You're trying to start a new relay. What they're gonna do is they're going to discover all of the different users that exist in the system by looking at what data they have to start with. Probably involve a little bit of a manual feeding in at first, whenever I'm starting up a relay, like, okay, there's bluesky's relay.

[00:25:39] Lemme just pull what they know. And then I go from there. And then anytime you discover a new user you don't have, you're like, oh, I wanna look them up. Pull them into the relay too. Right. So there's a, pretty straightforward, discovery process that you'll just have to bake into a relay to, to make sure you're calling as much the network as possible.


## ActivityPub federation vs AT Proto

[00:25:57] **Jeremy:** And so I don't think we've defined the term federation, but maybe you could explain what that is and if that is what this is.

[00:26:07] **Paul:** We are so unsure.

[00:26:10] **Jeremy:** Okay.

[00:26:11] **Paul:** Yeah. This has jammed is up pretty bad. Um, because I think everybody can, everybody pretty strongly agrees that ActivityPub is federation, right? and ActivityPub kind of models itself pretty similarly to email in a way, like the metaphors they use is that there's inboxes and outboxes and, and every ActivityPub server they're standing up the full vertical stack.

[00:26:37] They set up, the primary hosting, the views of the data that's happening there. the interface for the application, all of it, pretty traditional, like close service, but then they're kind of using the perimeter. they're making that permeable by sending, exchanging, essentially mailing records to each other, right?

[00:26:54] That's their kind of logic of how that works. And that's pretty much in line with, I think, what most people think of with Federation. Whereas what we're doing isn't like that we've cut, instead of having a bunch of vertical stacks communicating horizontally with each other, we kind of sliced in the other direction.

[00:27:09] We sliced horizontally into, this microservices mesh and have all the different, like a total mix and match of different microservices between different operators. Is that federation? I don't know. Right. we tried to invent a term, didn't really work, you know, At the moment, we just kind of don't worry about it that much, see what happens, see what the world sort of has to say to us about it.

[00:27:36] and beyond that, I don't know.

[00:27:42] **Jeremy:** I think people probably are thinking of something like, say, a Mastodon instance when you're, when you're talking about everything being included, The webpage where you view the posts, the Postgres database that's keeping the messages.

[00:28:00] And that same instance it's responsible for basically everything.

[00:28:06] **Paul:** mm-Hmm 

[00:28:06] **Jeremy:** And I believe what you're saying is that the difference with, the authenticated transfer protocol, is that the 

[00:28:15] **Paul:** AT Protocol, Yep.

[00:28:17] **Jeremy:** And the difference there is that you've, at the protocol level, you've split it up into the data itself, which can be validated completely separately from other parts of the system.

[00:28:31] You could have the JSON files on your hard drive and somebody else can have that same JSON file and they would know that who the user is and that these are real things that user posted. That's like a separate part. And then the relay component that looks for all these different repositories that has people's data, that can also be its own independent thing where its job is just to output events.

[00:29:04] And that can exist just by itself. It doesn't need the application part, the, the user facing part, it can just be this event stream on itself. and that's the part where it sounds like you can make decisions on who to, um, collect data from. I guess you have to agree that somebody can connect to you and get the users from your data repositories.

[00:29:32] And likewise, other people that run relays, they also have to agree to let you pull the users from theirs.

[00:29:38] **Paul:** Yeah, that's right. Yeah.

[00:29:41] **Jeremy:** And so I think the Mastodon example makes sense. And, but I wonder if the underlying ActivityPub protocol forces you to use it in that way, in like a whole full application that talks to another full application.

[00:29:55] Or is it more like that's just how people tend to use it and it's not necessarily a characteristic of the protocol.

[00:30:02] **Paul:** Yeah, that's a good question actually. so, you know, generally what I would say is pretty core to the protocol is the expectations about how the services interact with each other. So the mailbox metaphor that's used in ActivityPub, that design, if I reply to you, I'll update my, local database with what I did, and then I'll send a message over to your server saying, Hey, by the way, add this reply.

[00:30:34] I did this. And that's how they find out about things. That's how they find out about activity outside of their network. that's the part that as long as you're doing ActivityPub, I suspect you're gonna see reliably happening. That's that, I can say for sure that's a pretty tight requirement.

[00:30:50] That's ActivityPub. If you wanted to split it up the way we're talking about, you could, I don't know, I don't know if you necessarily would want to. Because I don't know. That's actually, I think I'd have to dig into their stack a little bit more to see how meaningful that would be. I do know that there's some talk of introducing a similar kind of an aggregation method into the ActivityPub world which I believe they're also calling a relay and to make things even more complicated.

[00:31:23] And NOSTR has a concept of a relay. So these are three different protocols that are using this term. I think you could do essentially what a search engine does on any of these things. You could go crawling around for the data, pull them into a fire hose, and then, tap into that aggregation to produce, bigger views of the network.

[00:31:41] So that principle can certainly apply anywhere. AT Protocol, I think it's a little bit, we, we focused in so hard from that on that from the get go, we focus really hard on making sure that this, the data is, signed at rest. That's why it's called the authenticated transfer protocol. And that's a nice advantage to have when you're running a relay like this because it means that you don't have to trust the relay.

[00:32:08] Like generally speaking, when I look at results from Google, you know, I'm trusting pretty well that they're accurately reflecting what's on the website, which is fine. You know, there's, that's not actually a huge risk or anything. But whenever you're trying to build entire applications and you're using somebody else's relay, you could really run into things where they say like, oh, you know what Paul tweeted the other day, you know, I hate dogs.

[00:32:28] They're like, no, I didn't. That's a lie, right? You just sneak in Little lies like that over a while, it becomes a problem. So having the signatures on the data is pretty important. You know, if you're gonna be trying to get people to cooperate, uh, you gotta manage the trust model. I know that ActivityPub does have mechanisms for signed records.


## Issuers with ActivityPub identifiers

[00:32:44] **Paul:** I don't know how deep they go if they could fully replace that, that utility. and then Mastodon ActivityPub, they also use a different identifier system that they're actually taking a look at DIDs um, right now, I don't know what's gonna happen there. We're, we're totally on board to, you know, give any kind of insight that we got working on 'em.

[00:33:06] But at, at the moment, they use I think it's WebFinger based identifiers they look like emails. So you got host names in there and those identifiers are being used in the data records. So you don't get that continuous identifier. They actually do have to do that hey, I moved update your records sort of thing.

[00:33:28] And that causes it to, I mean, it works like decently well, but not as well as it could. They got us to the point where it moves your profile over and you update all the folks that were following you so they can update their follow records, but your posts, they're not coming right, because that's too far into that mesh of interlinking records.

[00:33:48] There's just no chance. So that's kind of the upper limit on that, it's a different set of choices and trade-offs. You're always kind of asking like, how important is the migration? Does that work out? Anyway, now I'm just kind of digging into differences between the two here.


## Issues with an identifier that changes and updating old records

[00:34:07] **Jeremy:** So you were saying that with ActivityPub, all of the instances need to be notified that you've changed your identifier but then all of the messages that they had already received. They don't point to the new identifier somehow.

[00:34:24] **Paul:** Yeah. You run into basically just the practicalities of actual engineering with that is what happens, right? Because if you imagine you got a multimillion user social network. They got all their posts. Maybe the user has like, let's say a thousand posts and 10,000 likes. And that, activity can range back three years.

[00:34:48] Let's say they changed their identifier, and now you need to change the identifier of all those records. If you're in a traditional system that's already a tall order, you're going back and rewriting a ton of indexes, Anytime somebody replied to you, they have these links to your posts, they're now, you've gotta update the identifiers on all of those things.

[00:35:11] You could end up with a pretty significant explosion of rewrites that would have to occur. Now that's, that's tough. If you're in a centralized model. If you're in a decentralized one, it's pretty much impossible because you're now, when you notify all the other servers like, Hey, this, this changed. How successful are all of them at actually updating that, that those, those pointers, it's a good chance that there's things are gonna fall out of correctness. that's just a reality of it. And if, so, if you've got a, if you've got a mutable identifier, you're in trouble for migrations. So the DID is meant to keep it permanent and that ends up being the anchoring point. If you lose control of your DID well, that's it.


## Managing signing keys by server, paper key reset

[00:35:52] **Paul:** Your, your account's done. We took some pretty traditional approaches to that, uh, where the signing keys get managed by your hosting server instead of like trying to, this may seem like really obvious, but if you're from the decentralization community, we spend a lot of time with blockchains, like, Hey, how do we have the users hold onto their keys?

[00:36:15] You know, and the tooling on that is getting better for what it's worth. We're starting to see a lot better key pair management in like Apple's ecosystem and Google's ecosystem, but it's still in the range of like, nah, people lose their keys, you know? So having the servers manage those is important.

[00:36:33] Then we have ways of exporting paper keys so that you could kind of adversarially migrate if you wanted to. That was in the early spec we wanted to make sure that this portability idea works, that you can always migrate your accounts so you can export a paper key that can override.

[00:36:48] And that was how we figured that out. Like, okay, yeah, we don't have to have everything getting signed by keys that are on the user's devices. We just need these master backup keys that can say, you know what? I'm done with that host. No matter what they say, I'm overriding what they, what they think. and that's how we squared that one.

[00:37:06] **Jeremy:** So it seems like one of the big differences with account migration is that with ActivityPub, when you move to another instance, you have to actually change your identifier. 

[00:37:20] And with the AT protocol you're actually not allowed to ever change that identifier. And maybe what you're changing is just you have say, some kind of a lookup, like you were saying, you could use a domain name to look that up, get a reference to your decentralized identifier, but your decentralized identifier it can never change.

[00:37:47] **Paul:** It, it, it can't change. Yeah. And it shouldn't need to, you know what I mean? It's really a total disaster kind of situation if that happens. So, you know that it's designed to make sure that doesn't happen in the applications. We use these domain name handles to, to identify folks. And you can change those anytime you want because that's really just a user facing thing.

[00:38:09] You know, then in practice what you see pretty often is that you may, if you change hosts, if you're using, we, we give some domains to folks, you know, 'cause like not everybody has their own domain. A lot of people do actually, to our surprise, people actually kind of enjoy doing that. But, a lot of folks are just using like paul.bsky.social as their handle.

[00:38:29] And so if you migrated off of that, you probably lose that. Like your, so your handle's gonna change, but you're not losing the followers and stuff. 'cause the internal system isn't using paul.bsky.social, it's using that DID and that DID stays the same.


## Benefits of domain names, trust signal

[00:38:42] **Jeremy:** Yeah. I thought that was interesting about using the domain names, because when you like you have a lot of users, everybody's got their own sub-domain. You could have however many millions of users. Does that become, does that become an issue at some point?

[00:39:00] **Paul:** Well, it's a funny thing. I mean like the number of users, like that's not really a problem 'cause you run into the same kind of namespace crowding problem that any service is gonna have, right? Like if you just take the subdomain part of it, like the name Paul, like yeah, only, you only get to have one paul.bsky.social.

[00:39:15] so that part of like, in terms of the number of users, that part's fine I guess. Uh, as fine as ever. where gets more interesting, of course is like, really kind of around the usability questions. For one, it's, it's not exactly the prettiest to always have that B sky.social in there. If we, if we thought we, if we had some kind of solution to that, we would use it.

[00:39:35] But like the reality is that, you know, now we're, we've committed to the domain name approach and some folks, you know, they kind of like, ah, that's a little bit ugly. And we're like, yeah that's life. I guess the plus side though is that you can actually use like TLD the domain. It's like on pfrazee.com.

[00:39:53] that starts to get more fun. it can actually act as a pretty good trust signal in certain scenarios. for instance, well-known domain names like nytimes.com, strong authentication right there, we don't even need a blue check for it. Uh, similarly the .gov, domain name space is tightly regulated.

[00:40:14] So you actually get a really strong signal out of that. Senator Wyden is one of our users and so he's, I think it's wyden.senate.gov and same thing, strong, you know, strong identity signal right there. So that's actually a really nice upside. So that's like positives, negatives.

[00:40:32] That trust signal only works so far. If somebody were to make pfrazee.net, then that can be a bit confusing. People may not be paying attention to .com vs .net, so it's not, I don't wanna give the impression that, ah, we've solved blue checks. It's a complicated and multifaceted situation, but, it's got some juice.

[00:40:54] It's also kinda nice too, 'cause a lot of folks that are doing social, they're, they've got other stuff that they're trying to promote, you know? I'm pretty sure that, uh, nytimes would love it if you went to their website. And so tying it to their online presence so directly like that is a really nice kind of feature of it.

[00:41:15] And tells a I think a good story about what we're trying to do with an open internet where, yeah, everybody has their space on the internet where they can do whatever they want on that. And that's, and then thethese social profiles, it's that presence showing up in a shared space. It's all kind of part of the same thing.

[00:41:34] And that that feels like a nice kind of thing to be chasing, you know? And it also kind of speaks well to the naming worked out for us. We chose AT Protocol as a name. You know, we back acronymed our way into that one. 'cause it was a @ simple sort of thing. But like, it actually ended up really reflecting the biggest part of it, which is that it's about putting people's identities at the front, you know, and make kind of promoting everybody from a second class identity that's underneath Twitter or Facebook or something like that.

[00:42:03] Up into. Nope, you're freestanding. You exist as a person independently. Which is what a lot of it's about.

[00:42:12] **Jeremy:** Yeah, I think just in general, not necessarily just for bluesky, if people had more of an interest in getting their own domain, that would be pretty cool if people could tie more of that to something you basically own, right?

[00:42:29] I mean, I guess you're leasing it from ICANN or whatever, but, 

[00:42:33] yeah, rather than everybody having an @Gmail, Outlook or whatever they could actually have something unique that they control more or less.

[00:42:43] **Paul:** Yeah. And we, we actually have a little experimental service for registering domain names that we haven't integrated into the app yet because we just kind of wanted to test it out and, and kind of see what that appetite is for folks to register domain names way higher than you'd think we did that early on.

[00:43:01] You know, it's funny when you're coming from decentralization is like an activist space, right? Like it's a group of people trying to change how this tech works. And sometimes you're trying to parse between what might come off as a fascination of technologists compared to what people actually care about.

[00:43:20] And it varies, you know, the domain name thing to a surprising degree, folks really got into that. We saw people picking that up almost straight away. More so than certainly we ever predicted. And I think that's just 'cause I guess it speaks to something that people really get about the internet at this point.

[00:43:39] Which is great. We did a couple of other things that are similar and we saw varied levels of adoption on them. We had similar kinds of user facing, opening up of the system with algorithms and with moderation. And those have both been pretty interesting in and of themselves.


## Custom feed algorithms

[00:43:58] **Paul:** So with algorithms, what we did was we set that up so that anybody can create a new feed algorithm. And this was kind of one of the big things that you run into whenever you use the app. If you wanted to create a new kind of for you feed you can set up a service somewhere that's gonna tap into that fire hose, right?

[00:44:18] And then all it needs to do is serve a JSON endpoint. That's just a list of URLs, but like, here's what should be in that feed. And then the bluesky app will pick that up and, and send that, hydrate in the content of the posts and show that to folks. I wanna say this is a bit of a misleading number and I'll explain why but I think there's about 35,000 of these feeds that have been created.

[00:44:42] Now, the reason it's little misleading is that, I mean, not significantly, but it's not everybody went, sat down in their IDE and wrote these things. Essentially one of our users created, actually multiple of our users made little platforms for building these feeds, which is awesome. That's the kinda thing you wanna see because we haven't gotten around to it.

[00:44:57] Our app still doesn't give you a way to make these things. But they did. And so lots of, you know, there it is. Cool. Like, one, one person made a kind of a combinatorial logic thing that's like visual almost like scratch, it's like, so if it has this hashtag and includes these users, but not those users, and you're kind of arranging these blocks and that constructs the feed and then probably publish it on your profile and then folks can use it, you know?

[00:45:18] And um, so that has been I would say fairly successful. Except, we had one group of hackers do put in a real effort to make a replacement for you feed, like magic algorithmic feed kind of thing. And then they kind of kept up going for a while and then ended up giving up on it. Most of what we see are actually kind of weird niche use cases for feeds.

[00:45:44] You get straightforward ones, like content oriented ones like a cat feed, politics feed, things like that. It's great, some of those are using ML detection, so like the cat feed is ML detection, so sometimes you get like a beaver in there, but most of the time it's a cat. And then we got some ones that are kind of a funny, like change in the dynamic of freshness.

[00:46:05] So, uh, or or selection criteria, things that you wouldn't normally see. Um, but because they can do whatever they want, you know, they try it out. So like the quiet posters ended up being a pretty successful one. And that one just shows people you're following that don't post that often when they do just those folks.

[00:46:21] It ended up being, I use that one all the time because yeah, like they get lost in the noise. So it's like a way to keep up with them. 


## Custom moderation and labeling

[00:46:29] **Paul:** The moderation one, that one's a a real interesting situation. What we did there essentially we wanted to make sure that the moderation system was capable of operating across different apps so that they can share their work, so to speak.

[00:46:43] And so we created what we call labeling. And labeling is a metadata layer that exists over the network. Doesn't actually live in the normal data repositories. It uses a completely different synchronization because a lot of these labels are getting produced. It's just one of those things where the engineering characteristics of the labels is just too different from the rest of the system.

[00:47:02] So we created a separate synchronization for this, and it's really kind of straightforward. It's, here's a URL and here's a string saying something like NSFW or Gore, or you know, whatever. then those get merged onto the records brought down by the client and then the client, you know, based on the user's preferences.

[00:47:21] We'll put like warning screens up, hide it, stuff like that. So yeah, these label streams can then, you know, anybody that's running a moderation service can, you know, are publishing these things and so anybody can subscribe to 'em. And you get that kind of collaborative thing we're always trying to do with this.

[00:47:34] And we had some users set up moderation services and so then as an end user you find it, it looks like a profile in the app and you subscribe to it and you configure it and off you go. That one has had probably the least amount of adoption throughout all of 'em. It's you know, moderation.

[00:47:53] It's a sticky topic as you can imagine, challenging for folks. These moderation services, they do receive reports, you know, like whenever I'm reporting a post, I choose from all my moderation services who I wanna report this to. what has ended up happening more than being used to actually filter out like subjective stuff is more kind of like either algorithmic systems or what you might call informational.

[00:48:21] So the algorithmic ones are like, one of the more popular ones is a thing that's looking for, posts from other social networks. Like this screenshot of a Reddit post or a Twitter post or a Facebook post. Because, which you're kinda like, why, you know, but the thing is some folks just get really tired of seeing screenshots from the other networks.

[00:48:40] 'cause often it's like, look what this person said. Can you believe it? You know, it's like, ah. Okay, I've had enough. So one of our users aendra made a moderate service that just runs an ML that detects it, labels it, and then folks that are tired of it, they subscribe to it and they're just hide it, you know?

[00:48:57] And so it's like a smart filter kind of thing that they're doing. you know, hypothetically you could do that for things like spiders, you know, like you've got arachniphobia, things like that. that's like a pretty straightforward, kind of automated way of doing it. Which takes a lot of the spice, you know, outta out of running moderation.

[00:49:15] So that users have been like, yeah, yeah, okay, we can do that. 

[00:49:20] Those are user facing ways that we tried to surface the. Decentralized principle, right? And make take advantage of how this whole architecture can have this kind of a pluggability into it.


## Users can self host now

[00:49:33] **Paul:** But then really at the end of the day, kind of the important core part of it is those pieces we were talking about before, the hosting, the relay and the, the applications themselves, having those be swappable in completely. so we tend to think of those as kind of ranges of infrastructure into application and then into particular client side stuff.

[00:49:56] So a lot of folks right now, for instance, they're making their own clients to the application and those clients are able to do customizations, add features, things like that, as you might expect, 

[00:50:05] but most of them are not running their own backend. They're just using our backend. But at any point, it's right there for you. You know, you can go ahead and, and clone that software and start running the backend. If you wanted to run your own relay, you could go ahead and go all the way to that point.

[00:50:19] You know, if you wanna do your own hosting, you can go ahead and do that. Um, it's all there. It's really just kind of a how much effort your project really wants to take. That's the kind of systemically important part. That's the part that makes sure that the overall mission of de monopolizing, social media online, that's where that really gets enforced.

[00:50:40] **Jeremy:** And so someone has their own data repository with their own users and their own relay. they can request that your relay collect the information from their own data repositories. And that's, that's how these connections get made.

[00:50:58] **Paul:** Yeah. And, and we have a fair number of those already. Fair number of, we call those the self hosters right? And we got I wanna say 75 self hoster going right now, which is, you know, love to see that be more, but it's, really the folks that if you're running a service, you probably would end up doing that.

[00:51:20] But the folks that are just doing it for themselves, it's kind of the, the nerdiest of the nerds over there doing that. 'cause it doesn't end up showing itself in the, in the application at all. Right? It's totally abstracted away. So it, that, that one's really about like, uh, measure your paranoia kind of thing.

[00:51:36] Or if you're just proud of the self-hosting or, or curious, you know, that that's kind of where that sits at the moment.


## AT Protocol beyond bluesky

[00:51:42] **Jeremy:** We haven't really touched on the fact that there's this underlying protocol and everything we've been discussing has been centered around the bluesky social network where you run your own, instance of the relay and the data repositories with the purpose of talking to bluesky, but the protocol itself is also intended to be used for other uses, right?

[00:52:06] **Paul:** Yeah. It's generic. The data types are set up in a way that anybody can build new data types in the system. there's a couple that have already begun, uh, front page, which is kind of a hacker news clone. There's Smoke Signals, which is a events app. There's Blue Cast, which is like a Twitter spaces, clubhouse kind of thing.

[00:52:29] Those are the folks that are kind of willing to trudge into the bleeding edge and deal with some of the rough edges there for pretty I think, obvious reasons. A lot of our work gets focused in on making sure that the bluesky app and that use case is working correctly.

[00:52:43] But we are starting to round the corner on getting to a full kind of how to make alternative applications state. If you go to the atproto.com, there's a kind of a introductory tutorial where that actually shows that whole stack and how it's done. So it's getting pretty close. There's a couple of still things that we wanna finish up.

[00:53:04] **jeremy** so in a way you can almost think of it as having an eventually consistent data store on the network, You can make a traditional web application with a relational database, and the source of truth can actually be wherever that data repository is stored on the network.

[00:53:24] **paul** Yeah, that's exactly, it is an eventually consistent system. That's exactly right. The source of truth is there, is their data repo. And that relational database that you might be using, I think the best way to think about it is like secondary indexes or computed indexes, right? They, reflect the source of truth.

[00:53:43] **Paul:** This is getting kind of grandiose. I don't tend to poses in these terms, but it is almost like we're trying to have an OS layer at a protocol level. It's like having your own

[00:53:54] Network wide database or network-wide file system, you know, these are the kind of facilities you expect out of a platform like an os And so the hope would be that this ends up getting that usage outside of just the initial social, uh, app, like what we're doing here.

[00:54:12] If it doesn't end up working out that way, if this ends up, you know, good for the Twitter style use case, the other one's not so much, and that's fine too. You know, that's, that's our initial goal, but we, we wanted to make sure to build it in a way that like, yeah, there's evolve ability to, it keeps, it, keeps it, make sure that you're getting kinda the most utility you can out of it.


## Peer-to-peer and the difficulty of federated queries

[00:54:30] **Jeremy:** Yeah, I can see some of the parallels to some of the decentralized stuff that I, I suppose people are still working on, but more on the peer-to-peer side, where the idea was that I can have a network host this data. but, and in this case it's a network of maybe larger providers where they could host a bunch of people's data versus just straight peer to peer where everybody has to have a piece of it.

[00:54:57] And it seems like your angle there was really the scalability part.

[00:55:02] **Paul:** It was the scalability part. And there's great work happening in peer-to-peer. There's a lot of advances on it that are still happening. I think really the limiter that you run into is running queries against aggregations of data. Because you can get the network, you know, BitTorrent sort of proved that you can do distributed open horizontal scaling of hosting.

[00:55:29] You know, that basic idea of, hey, everybody's got a piece and you sync it from all these different places. We know you can do things like that. What nobody's been able to really get into a good place is running, queries across large data sets. In the model like that, there's been some research in what is, what's called federated queries, which is where you're sending a query to multiple different nodes and asking them to fulfill as much of it as they can and then collating the results back. But it didn't work that well. That's still kind of an open question and until that is in a place where it can like reliably work and at very large scales, you're just gonna need a big database somewhere that does give the properties that you need. You need these big indexes. And once we were pretty sure of that requirement, then from there you start asking, all right, what else about the system

[00:56:29] Could we make easier if we just apply some more traditional techniques and merge that in with the peer-to-peer ideas? And so key hosting, that's an obvious one. You know, availability, let's just have a server. It's no big deal. But you're trying to, you're trying to make as much of them dumb as possible.

[00:56:47] So that they have that easy replaceability.


## Moderation challenges

[00:56:51] **Jeremy:** Earlier you were talking a a little bit about the moderation tools that people could build themselves. There was some process where people could label posts and then build their own software to determine what a feed should show per a person. 

[00:57:07] **Paul:** Mm-Hmm

[00:57:07] **Jeremy:** But, but I think before that layer for the platform itself, there's a base level of moderation that has to happen.

[00:57:19] **Paul:** yeah.

[00:57:20] **Jeremy:** And I wonder if you could speak to, as the app has grown, how that's handled.

[00:57:26] **Paul:** Yeah. the, you gotta take some requirements in moderation pretty seriously to start. And with decentralization. It sometimes that gets a little bit dropped. You need to have systems that can deal with questions about CSAM. So you got those big questions you gotta answer and then you got stuff that's more in the line of like, alright, what makes a good platform?

[00:57:54] What kind of guarantees are we trying to give there? So just not legal concerns, but you know, good product experience concerns. That's something we're in the realm of like spam and and abusive behavior and things like that. And then you get into even more fine grain of like what is a person's subjective preference and how can they kind of make their thing better?

[00:58:15] And so you get a kind of a telescoping level of concerns from the really big, the legal sort of concerns. And then the really small subjective preference kind of concerns. And that actually that telescoping maps really closely to the design of the system as well. Where the further you get up in the kind of the, in that legal concern territory, you're now in core infrastructure.

[00:58:39] And then you go from infrastructure, which is the relay down into the application, which is kind of a platform and then down into the client. And that's where we're having those labelers apply. And each of them, as you kind of move closer to infrastructure, the importance of the decision gets bigger too.

[00:58:56] So you're trying to do just legal concerns with the relay right? Stuff that you objectively can, everybody's in agreement like Yeah, yeah, yeah. You know, no bigs don't include that. The reason is that at the relay level, you're anybody that's using your relay, they depend on the decisions you're making, that sort of selection you're doing, any filtering you're doing, they don't get a choice after that.

[00:59:19] So you wanna try to keep that focus really on legal concerns and doing that well. so that applications that are downstream of it can, can make their choices. The applications themselves, you know, somebody can run a parallel I guess you could call it like a parallel platform, so we got bluesky doing the microblogging use case, other people can make an application doing the microblogging use case. So there's, there's choice that users can easily switch, easily enough switch between, it's still a big choice.

[00:59:50] So we're operating that in many ways. Like any other app nowadays might do it. You've got policies, you know, for what's acceptable on the network. you're still trying to keep that to be as, you know, objective as possible, make it fair, things like that. You want folks to trust your T&amp;S team. Uh, but from the kind of systemic decentralization question, you get to be a little bit more opinionated.

[01:00:13] Down all the way into the client with that labeling system where you can, you know, this is individuals turning on and off preferences. You can be as opinionated as you want on that letter. And that's how we have basically approached this. And in a lot of ways, it really just comes down to, in the day to day, you're the moderation, the volume of moderation tasks is huge.

[01:00:40] You don't actually have high stakes moderation decisions most of the time. Most of 'em are you know pretty straightforward. Shouldn't have done that. That's gotta go. You get a couple every once in a while that are a little spicier or a policy that's a little spicier. And it probably feels pretty common to end users, but that just speaks to how much moderation challenges how the volume of reports and problems that come through.

[01:01:12] And we don't wanna make it so that the system is seized up, trying to decentralize itself. You know, it needs to be able to operate day to day. What you wanna make is, you know, back pressure, you know, uh, checks on that power so that if an application or a platform does really start to go down the wrong direction on moderation, then people can have this credible exit.

[01:01:36] This way of saying, you know what, that's a problem. We're moving from here. And somebody else can come in with different policies that better fit people's people's expectations about what should be done at, at these levels. So yeah, it's not about taking away authority, it's about checking authority, you know, kind of a checks and balances mentality.

[01:01:56] **Jeremy:** And high level, 'cause you saying how there's such a high volume of, of things that you know what it is, you'd know you wanna remove it, but there's just so much of it. So is there, do you have automated tools to label these things? Do you have a team of moderators? Do they have to understand all the different languages that are coming through your network?

[01:02:20] Yes, yes, yes and yes. Yeah. You use every tool at your disposal to, to stay on top of it. cause you're trying to move as fast as you can, folks. The problems showing up, you know, the slower you are to respond to it, the, the more irritating it is to folks. Likewise, if you make a, a missed call, if somebody misunderstands what's happening, which believe me, is sometimes just figuring out what the heck is going on is hard.

[01:02:52] **Paul:** People's beefs definitely surface up to the moderation misunderstanding or wrong application. Moderators make mistakes so you're trying to maintain a pretty quick turnaround on this stuff. That's tough. And you, especially when to move fast on some really upsetting content that can make its way through, again, illegal stuff, for instance, but more videos, stuff like that, you know, it's a real problem.

[01:03:20] So yeah, you're gotta be using some automated systems as well. Clamping down on bot rings and spam. You know, you can imagine that's gotten a lot harder thanks to LLMs just doing text analysis by dumb statistics of what they're talking about that doesn't even work anymore.

[01:03:41] 'cause the, the LLMs are capable of producing consistently varied responses while still achieving the same goal of plugging a online betting site of some kind, you know? So we do use kind of dumb heuristic systems for when it works, but boy, that won't work for much longer.

[01:04:03] And we've already got cases where it's, oh boy, so the moderation's in a dynamic place to say the least right now with, with LLMs coming in, it was tough before and now it's, now it's real interesting. Uh, so you use everything you can and you keep playing the cat and mouse game. And that's that.

[01:04:26] **Jeremy:** Are the tools that you use were they all built in-house or are there... 

[01:04:31] **Paul:** Not all of them. We do use a couple of services that are out there. For one with the CSAM stuff, there's a company called Thorn that is actually set up to handle that. Obviously it's a very sensitive kind of thing. They maintain these hash fingerprint databases that we check in every post, Hey, this is on your database.

[01:04:58] We also use a service called Hive to help us automatically detect pornography and gore. we're still tuning that one, but it hits significantly. It's correct more than it's incorrect. And we  encourage users to self label their stuff. 'cause you know good actors don't want to be posting NSFW to people that don't wanna get it.

[01:05:23] We do see people do it, but we still need to have that extra check. And so we're running that kind of detection on it and things like that. And then we got a couple of in-house things, something called automod which you could find the source for. That's just sitting there and it's a Go  code base that's sitting there and running all kinds of heuristics trying to detect kinds of patterns of behavior that we've identified as being a problem.

[01:05:48] Often that has to do with spam and then it's people.

[01:05:53] **Jeremy:** I think with any application that has user generated content, it just seems like such a huge challenge to deal with.

[01:06:06] **Paul:** It is, it really is. And, it's the thing, you know, it shows up in a lot of places. What we're talking about is kind of the, what's funny is what we're talking about is the obvious way that it shows up. And even that it's not really apparent to the average person just how much that really is.

[01:06:23] It's a pretty big task, but it also makes its way into product development. And is one of those hidden costs that shows up all over the place? There's that meme about, oh, I can build Twitter at a weekend, kind of thing.

[01:06:45] **Jeremy:** Right.

[01:06:46] **Paul:** Which, there's a lot of reasons why, building a a microblogging app, had a lot of time to reflect on how many weekends it was taken to build it, you know, and why, why it took longer than a weekend for us.

[01:07:04] Certainly targeting a lot of different platforms, will do it to you. React native makes that a lot easier these days and I give them a plug. They've been great. The moderation, the safety, that, that part of the design that you gotta work into all new features, that is a real hidden cost of product development that you gotta take seriously from the get go.

[01:07:28] And you gotta look at every, everything you do and say, what, how's this gonna get messed with where people are gonna do with this? And I think our track record has been pretty good. There're definitely moments where we get something out and go, ah, you know, didn't think of that. Which is, that's just how it goes.

[01:07:45] But that shows up everywhere.

[01:07:48] **Jeremy:** I didn't even think about the fact where you had mentioned the LLMs, where now people just have the power to generate posts that are indistinguishable from people. So I don't know. I don't know where we're going here, but...

[01:08:04] **Paul:** Somewhere new.

[01:08:10] **Jeremy:** Any closing thoughts or other things you want to mention?

[01:08:13] **Paul:** Yeah, this has been an interesting project. I'm happy with how it's gone so far for sure. The first question that we had when we started out was just whether or not it would scale, because historically folks that work in the decentralization space, that's what jams us up pretty bad. In obvious ways, peer to peer.

[01:08:31] But even blockchains actually got jammed up real bad on scaling. And that's kind of why the NFT bubble popped as hard as it did when it did was everybody knows the transaction fees got really high. It's 'cause the system got too crowded. So making these big scale systems that have open operation is a real challenge.

[01:08:51] And that's the part that so far, we're up to now 11 million registered accounts, and we sit at somewhere around 1.5 to 2 million DAU and we haven't identified anything that makes us think, oh, that's a scaling limit for this design. We're pretty sure that it can make its way all the way to the kind of scale that people expect out of this.

[01:09:12] So I'm really happy to see just kind of from the engineering side of things, like getting that validated has felt pretty good about this project. And so I'm, I'm pretty curious to see kind of how this all unfolds moving forward. I'm feeling very happy with the outcome so far and just actually genuinely interested on a personal level to see how, how these dynamics play out over time.

[01:09:36] Really looking forward to seeing somebody else start to operate full nodes like we are. I think that'll be a great milestone that we're trying to head for. And hopefully in a year or two, I think we kind of need to make a little social network in a box, make it a little bit easier for somebody to just press a button and get the whole thing going.

[01:09:55] That's a milestone in the future I'm looking forward to. other than that. a lot of my day to day just comes down to, A lot of it's just running the social app and learning all the lessons that come along with that, which has been a trip in and of itself.

[01:10:07] But you know, the, all the source code, um, is available on GitHub. So if you wanna see how we do it, it's right there. And if you're an application developer, I think in particular, the social app repo is pretty interesting to look at. That's a React native repository. You can see the full thing.

[01:10:26] **Paul:** Lots of good forkable code in there if you're building an app. So I would definitely check that out. All the protocol code is up there. We got specs up on the app protocol website, so atproto.com, you can check all that out. Some good intro material, things like that. You want to learn a little bit more about how all this works?

[01:10:43] Find out on atproto.com. Yeah, so it's it's all up there. It's all ready to, ready to look at.

[01:10:50] **Jeremy:** And if people wanna follow you or see what you're up to, 

[01:10:53] **Paul:** You're gonna jump on bluesky and on pfrazee.com.

[01:10:57] **Jeremy:** Paul, thank you so much for taking the time.

[01:11:00] **Paul:** Absolutely. Thank you.