+++
title = "Hong Minhee on ActivityPub"

description = "Use cases and implementation"

[extra]
episode_url = "https://pinecast.com/listen/8ff7e875-4af6-4dd2-b411-b8a44582ae78.mp3"
social_title = "Hong Minhee on ActivityPub"
social_description = "Use cases and implementation"
+++

Hong Minhee is an open source developer and the creator of the [Fedify](https://fedify.dev/) ActivityPub server framework.

We talk about how applications like Mastodon and Misskey communicate with one another using ActivityPub. This includes discussions on built-in activites, extending the specification in a backwards compatible way, difficulties implementing JSON-LD, the inbox model, and his experience implementing the specification

Hong Minhee:
- [activitypub profile](https://hollo.social/@hongminhee)
- [fedify](https://fedify.dev/)
- [hollo](https://github.com/dahlia/hollo)

Specifications:
- [ActivityPub W3C specification](https://www.w3.org/TR/activitypub/)
- [JSON Linked Data](https://json-ld.org/)
- [Resource Description Framework](https://www.w3.org/2001/sw/wiki/RDF)
- [W3C Semantic Web Standards](https://www.w3.org/2001/sw/wiki/Main_Page)
- [ActivityPub and WebFinger](https://swicg.github.io/activitypub-webfinger/)
- [ActivityPub and HTTP Signatures](https://swicg.github.io/activitypub-http-signature/)

ActivityPub implementations:
- [Mastodon](https://joinmastodon.org)
- [Misskey](https://misskey-hub.net/)
- [Akkoma](https://akkoma.social/)
- [Pleroma](https://pleroma.social/)
- [Pixelfed](https://pixelfed.org/)
- [Lemmy](https://join-lemmy.org/)
- [Loops](https://loops.video/)
- [GoToSocial](https://gotosocial.org/)
- [ActivityPub support in Ghost](https://activitypub.ghost.org/)
- [Threads has entered the Fediverse](https://engineering.fb.com/2024/03/21/networking-traffic/threads-has-entered-the-fediverse/)

ActivityPub tools:
- [ActivityPub Academy](https://activitypub.academy/)
- [BrowserPub](https://browser.pub/)
- [fedify CLI](https://fedify.dev/cli)

--

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).


## What's ActivityPub?

[00:00:00] **Jeremy:** Today, I'm talking to Hong Minhee. He is the developer of Fedify. A TypeScript library for building ActivityPub server applications. 

The first thing I think we should start with is defining ActivityPub. what is ActivityPub? 

[00:00:16] **Hong:** ActivityPub is the protocol that lets social networks talk to each other and it's officially recommended by W3C. It's what powers this thing we call the Fediverse which is basically a way for different social media platforms to work together. 


## Users of ActivityPub

[00:00:39] **Jeremy:** Can you give some examples that people might have heard of -- either users of ActivityPub or things that are a part of this fediverse?

[00:00:50] **Hong:** Mastodon is probably the biggest one out there. And you know what's interesting? 

Meta threads has actually started implementing ActivityPub this summer. So this still pretty much a one way street right now. In East Asia, especially Japan, there's this really popular microblogging platform called misskey.

It's got so many forks that people actually joke around and called them forkeys. but it's not just about Twitter style microblogging, there's Pixelfed which is kind of like Instagram, but for the fediverse. And those same folks recently launched loops. Which is basically doing what TikTok does, but in the Fediverse.

Then you've got stuff like Lemmy and which are doing the reddit thing up in the Fediverse.

[00:02:00] **Jeremy:** Oh like Reddit.

[00:02:01] **Hong:** Yeah. There are so much more out there that I haven't even mentioned. Um, most of it is open source, which is pretty cool. 

[00:02:13] **Jeremy:** So the first few examples you gave, Mastodon and Meta's threads, they're very similar to, to Twitter, right? So that's what you were calling the, the Microblogging applications.

And I think what you had said, which is a little bit interesting is you had said Metas threads is only one way. So could you kind of describe like what you mean by that?

[00:02:37] **Hong:** Currently meta threads only can be followed by other ActivityPub applications but you cannot follow other people in the fediverse.

[00:02:55] **Jeremy:** People who are using another Microblogging platform like Mastodon can follow someone on Meta's Threads platform. But the other way is not true. If you're on threads, you can't follow someone on Mastodon.

[00:03:07] **Hong:** Yes, that's right.

[00:03:09] **Jeremy:** And that's not a limitation of the protocol itself. That's a design decision or a decision made by Meta.

[00:03:17] **Hong:** Yeah. They are slowly implementing ActivityPub and I hope they will implement complete ActivityPub in the future.


## Interoperability through Activities

[00:03:27] **Jeremy:** And then the other examples you gave, one is I believe it was Pixel Fed is very similar to Instagram. And then the last examples you gave was I think it was Lemmy, you said it's similar to Reddit. Because you mentioned the term Fediverse before and you mentioned that these all use ActivityPub and since these seem like different kinds of applications, what does it mean for them to interact?

Because with Mastodon and Threads I can kind of understand because they're both similar to Twitter. So you're posting messages and replying, but, but what does it mean, for example, for someone on Mastodon to interact with someone on Lemmy which is like Reddit because they seem very different.

[00:04:16] **Hong:** People in Lemmy and Mastodon are called actors and can follow each other. 

They have interactions between them called activities. And there are several types of activities like, create and follow and undo, like, and so on. 

So, ActivityPub applications tend to, use these vocabulary to implement their features. 

So, for example, Lemmy uses like activities for upvoting and like activities for down voting and it's translated to likes in Mastodon. So if you submit a post on Lemmy and it shows up on your Mastodon timeline. If you like that post (it) is upvoting in Lemmy. 

[00:05:36] **Jeremy:** And probably similarly with Pixelfed, which you said is like Instagram, if you follow someone's Pixelfed account in Mastodon and they post a photo in Pixel Fed, they would see it as a post in Mastodon natively and they could give it a like there. 


## Adding activities or properties

[00:05:56] **Jeremy:** And these activities that you mentioned -- So the like and the dislike are those part of ActivityPub itself?

[00:06:05] **Hong:** Yes, and this vocabulary can be extended.

[00:06:10] **Jeremy:** So you can add, additional actions (activities) or are you adding information (properties) to the existing actions?

[00:06:37] **Hong:** 

It is called activity vocabulary, and there are, things like accept, add, arrive, block, create lead, dislike, flag, follow, ignore invite, join, and so on.

So, basically, almost everything you need to build social media is already there in the vocabulary, but if you want to extend some more, you can define your, own vocabulary.

[00:06:56] **Jeremy:** Most of the things that an Instagram or a Twitter, or a Reddit would need is already there. But you're saying that you can have your own vocabulary. So if there's an action or an activity that is not covered by the specification, you can create one yourself.

[00:07:13] **Hong:** Yes. For example, Misskey and Pleroma defined emoji reactor to represent emoji reactions.

[00:07:25] **Jeremy:** Because the systems can extend the vocabulary. What are some other examples of cases where mastodon or any other of these systems has found that the existing vocabulary is not enough. What are some other examples of applications extending it?

[00:07:45] **Hong:** For example, uh, mastodon defined suspended -- suspended property. They are not activities, but they are properties in the activity. 

ActivityPub consists of several types of objects and there are activities and normal objects like, article. they can have properties and there are several existing properties, but they can be also extended. So Mastodon extended some properties they need. So for example, they define suspended or discoverable. 

[00:08:44] **Hong:** Suspended for to tell if an actor is suspended by moderators. Discoverable tells if an actor itself wants to be, searched and indexed, and there are much more properties. Mastodon extended.

## Actors

[00:09:12] **Jeremy:** And these are, these are properties of the actor. These are properties of the user?

[00:09:19] **Hong:** Yes. Actors. 

[00:09:21] **Jeremy:** Cause I think earlier you mentioned that. The concept of a user is an actor, and it sounds like what you're saying is an actor can have all these properties. There's probably a, a username and things like that, but Mastodon has extended the properties so that, you can have a property on whether you wanna be searched or indexed you can have a property that says you're suspended.

So I guess your account, is still there, but can't be used anymore. 

Something we should probably talk about then is, so you have these actors, you have these activities that I'm assuming the actors are performing on one another. What does that data look like and what does the communication look like?

[00:10:09] **Hong:** Actors have their own dereferencable URI and when you look up that URI you get all the info about the actor in JSON-LD format 

[00:10:22] **Jeremy:** JSON-LD?

[00:10:23] **Hong:** Yeah. JSON-LD. linked data. 

(The) Actor has all the stuff you expect to find on a social account name, bio URL to the profile page, profile picture, head image and more. And there are five main types of actors: application, group, organization, person and service.

And you know how sometimes on Mastodon you will see an account marked as a bot?

[00:10:58] **Jeremy:** A bot?

[00:10:59] **Hong:** Yeah. Bot and that's what an actor of type service looks like. And the ActivityPub spec actually let you create other types beyond these five. But I haven't seen anyone actually do that yet.


## JSON-LD

[00:11:15] **Jeremy:** And you mentioned that these are all JSON objects. but the LD part, the linked data part, I'm not familiar with. So what different about the linked data part of the JSON?

[00:11:31] **Hong:** So JSON-LD is the special way of writing RDF. Which was originally used in the semantic web. Usually RDF uses (a) format (that) is called triples.

[00:11:48] **Jeremy:** Triples?

[00:11:49] **Hong:** Yeah, subject and predicate and object.

[00:11:55] **Jeremy:** Subject, predicate, object. Can you give an example of what those three would be?

[00:12:00] **Hong:** For example, is a person, it's a triple. John is a subject and is a predicate 

[00:12:11] **Jeremy:** is, is the predicate.

[00:12:12] **Hong:** Okay. And person is a object. That's great for showing how things are connected, but it is pretty different from how we usually handle data in REST for APIs and stuff. Like normally we say a personal object has property like name, DOB, bio, and so on. And a bunch of subject predicated object triples that's where JSON-LD comes in -- is designed to look more like the JSON we are used to working with, while still being able to represent RDF Graphs.

RDF graph are ontology. It's a way to represent factual data, but is, quite different from, how we represent data in relational database. And it's a bunch of triples each subject and objects are nodes and predicates connect these nodes.

## Semantic Web

[00:13:30] **Jeremy:** You mentioned the Semantic web, what does that mean? What is the semantic web?

[00:13:35] **Hong:** It's a way to represent web in the structural way, is machine readable so that you can, scan the data in the web, using scrapers or crawlers.

[00:13:52] **Jeremy:** Scrapers -- or what was the second one? Crawling.

[00:13:59] **Hong:** Yeah.

Then you can have graph data of web and you can, query information about things from the data.

[00:14:14] **Jeremy:** So is the web as it exists now, is that the Semantic web or is it something different?

[00:14:24] **Hong:** I think it is partially semantic web, you have several metadata in Your HTML. For example, there are several specification for semantic web, like, OpenGraph metadata.

[00:14:32] **Jeremy:** Cause when I think about OpenGraph, I think about the metadata on a webpage that, that tells other applications or websites that if you link to this page: show this image or show this title and description. You're saying that specifically you consider part of the semantic web?

[00:15:05] **Hong:** That's, semantic web.

To make your website semantic web. Your website should be able to, provide structural data. And other people can make Scrapers to scan, structural data from your website. 

There are a bunch of attributes and text for HTML to represent metadata. For example you have relation attribute `rel` so if you have a link with `rel=me` to your another social profile. Then other people can tell two web pages represent the same person.

[00:16:10] **Jeremy:** Oh, I see. So you could have more than one website. Maybe one is your blog and maybe one is your favorite birds or something like that. But you could put a `rel` tag with information about you as a person so that someone who scrapes both websites could look at that tag and see that both of these websites are by, Hong, by this person.

## JSON-LD is difficult to implement and not used as intended

[00:16:43] **Hong:** Yeah. I think JSON-LD is, designed for semantic web, but in reality, ActivityPub implementations, most of them are, not aware of semantic web. 

[00:17:01] **Jeremy:** The choice of JSON Linked Data, the JSON-LD, by the people who made the specification -- They had this idea that things that implemented ActivityPub would be a part of this semantic web, but the actual implementation of a Mastodon or a Pixelfed, they use JSON-LD because it's part of the specification, but the way they use it, it ends up not really being a part of this semantic web.

[00:17:34] **Hong:** Yeah, that's exactly.. 

[00:17:37] **Jeremy:** You've mentioned that implementing it is difficult. What makes implementing JSON LD particularly hard?

[00:17:48] **Hong:** The JSON-LD is quite complex. Which is why a lot of programming language don't even have JSON-LD implementations and it's pretty slow compared to just working with the regular JSON.


So, what happens is a lot of ActivityPub implementations just treat JSON-LD like (it) is regular JSON without using a proper JSON-LD processor. You can do that, but it creates a source of headache. In JSON-LD there are weird equivalences like if a property is missing or if it's an empty array, that means the same thing.

Or if a property has one value versus an array with just that one value in it, same thing.

So when you are writing code to parse JSON-LD, you've got to keep checking if something's an array how long it is and all that is super easy to mess up. It's not just reading JSON-LD that's tricky. Creating it is just as bad. Like you might forget to include the right context metadata for a vocabulary and end up with a JSON-LD document that's either invalid or means something totally different from what you wanted.

Even the big ActivityPub implementations mess this up pretty often. With Fedify we've got a JSON-LD processor built in and we keep running into issues where major ActivityPub implementations create invalidate JSON-LD. We've had to create workaround for all of them, but it's not pretty and causes kind of a mess.

[00:19:52] **Jeremy:** Even though there is a specification for JSON-LD, it sounds like the implementers don't necessarily follow it. So you are kind of parsing JSON-LD, but not really. You're parsing something that. Looks like JSON-LD, but isn't quite it.

[00:20:12] **Hong:** Yes, that's right.

[00:20:14] **Jeremy:** And is that true in the, the biggest implementations, Mastodon, for example, are there things that it sends in its activities that aren't valid JSON-LD?

[00:20:26] **Hong:** Those implementations that had bad JSON-LD tends to fix them soon as a possible. But regressions are so often made. Yeah.

[00:20:45] **Jeremy:** Even within Mastodon, which is probably one of the largest implementers of ActivityPub, there are cases where it's not valid, JSON-LD and somebody fixes it. But then later on there are other messages or other activities that were valid, but aren't valid anymore. And so it's this, it's this back and forth of fixing them and causing new issues it sounds ...

[00:21:15] **Hong:** Yeah. Yeah. Right.

[00:21:17] **Jeremy:** Yeah. That sounds very difficult to deal with.


## How instances communicate (Inbox)

[00:21:20] **Jeremy:** We've been talking about the messages themselves are this special format of JSON that's very particular. but how do these instances communicate with one another? 

[00:21:32] **Hong:** Most of time, it all starts with a follow. Like when John follows Alice, then Alice adds both John and John's inbox URI to her followers list, and after John follows Alice, Whenever Alice posts something new that activities get sent to John's inbox behind the scenes.

This is just one HTTP post request. Even though ActivityPub is built on HTTP. It doesn't really care about the HTTP response beyond did it work or not. If you want to reply to an activity, you need to figure out the standard inbox, URI and send or reply activity there. 

[00:22:27] **Jeremy:** If we define all the terms, there's the actor, which is the person, each actor can send different activities. those activities are in the form of a JSON linked data.

[00:22:40] **Hong:** Yeah.

[00:22:42] **Jeremy:** And everybody has an inbox. And an inbox is an HTTP URL that people post to.

[00:22:50] **Hong:** Right.

[00:22:52] **Jeremy:** And so when you think about that, you had mentioned that if you have a list of followers, let's say you have a hundred followers, would that mean that you have the URLs to all hundred of those follower's inboxes and that you would send one HTTP post to each inbox every time you had a new message?

[00:23:16] **Hong:** Pretty much all ActivityPub implementations have, a thing called shared inbox, it's exactly what it sounds like. One inbox that all actors on a server share. Private stuff like DMs don't go there (it) is just for public posts and thoughts. 

[00:23:36] **Jeremy:** I think we haven't really talked about the fact that, when you have multiple users, usually they're on a server, right? That somebody chooses. So you could have tens of thousands, I don't know how many people can fit on the same server. But, rather than, you having to post to each user individually, you can post to the shared inbox on this server.

So let's say, of your 100 followers, 50 them are on the same server, and you have a new post, you only need to post to the shared inbox once.

[00:24:16] **Hong:** Yes, that's right. 

[00:24:18] **Jeremy:** And in that message you would I assume have links to each of the profiles or actors that you wanted to send that message to.

[00:24:30] **Hong:** Yeah. 


## Scaling challenges

[00:24:31] **Jeremy:** Something that I've seen in the past is there are people who have challenges with scaling. Their Mastodon instance or their implementations of ActivityPub. As the, the number of followers grow, I've seen a post about, ghost one of the companies you work with mentioning that they've had challenges there.

What are the challenges there and, and how do you think those can be resolved?

[00:25:04] **Hong:** To put this in context, when Ghost mentioned the scaling, they were not using Message Queue yet. I'm pretty sure using Message Queue would help a lot of their scaling problems. 

That said it is definitely true that a lot of activity post software has trouble with scaling right now.

I think part of the problem is that everyone's using this purely event driven approach to sending activities around.

One of the big issues is that when their delivery fails it's the sender who has to retry and not the receiver. Plus there's all this overhead because the sender has to authenticate itself with HTTP signatures every time. Actually the ActivityPub spec suggests using polling too so I'd love to see more ActivityPub software try using both approaches together.

[00:26:16] **Jeremy:** You mean the followers would poll who they're following instead of the person posting the messages having to send their posts to everyone's inboxes.

[00:26:29] **Hong:** Yeah.

[00:26:29] **Jeremy:** I see. So that's a part of the ActivityPubs specification, but not implemented in a lot of ActivityPub implementations,

And so it sounds like maybe that puts a lot of burden on the servers that have people with a lot of followers because they have to post to every single, follower server and maybe the server is slow or they can't reach it. And like you said, they have to just keep trying and trying. There could be a lot of challenges there.

[00:27:09] **Hong:** Right. 


## Account migration

[00:27:10] **Jeremy:** We've talked a little bit about the fact that each person each actor is hosted by a server and those servers can host multiple actors. But if you want to move to another server either because your server is shutting down or you just would like to change servers, what are some of the challenges there?

[00:27:38] **Hong:** ActivityPub and Fediverse already have the specification for an account move. It's called [FEP-7628 Move Actor](https://codeberg.org/fediverse/fep/src/branch/main/fep/7628/fep-7628.md). 

First thing you need to do when moving an account is prove that both the old and new accounts belong to the same person. You do this by adding the all accounts, add the URI to the new account's `AlsoKnownAs` property. And then the old account contacts all the other instances it's moving by sending out a move activity.

When a server gets this move activity, it checks that both accounts really do belong to the same parts, and then it makes all the accounts that, uh, were following the, all the accounts start to, following the new one instead.

that's how the new account gets to keep all the, all the accounts follow us. pretty much all, all the major activity post software has this feature built in, for example, Mastodon Misskey you name it.

[00:29:04] **Jeremy:** This is very similar to the post where when you execute a move, the server that originally hosted that actor, they need to somehow tell every single other server that was following that account that you've moved. And so if there's any issues with communicating with one of those servers, or you miss one, then it just won't recognize that you've moved. You have to make sure that you talk to every single server.

[00:29:36] **Hong:** That's right.

[00:29:38] **Jeremy:** I could see how that could be a difficult problem sometimes if you have a lot of followers.

[00:29:45] **Hong:** Yeah.


## Fedify

[00:29:46] **Jeremy:** You've created a TypeScript library Fedify for building ActivityPub powered applications. What was the reason you decided to create Fedify?

[00:29:58] **Hong:** Fedify is (a) ActivityPub servers framework I built for TypeScript. It basically takes away a lot of headaches you'd get trying to implement (an) ActivityPub server from scratch. The whole thing started because I wanted to build hollo -- A single user microblogging platform I built. But when I tried, to implement ActivityPub from (the) ground up it was kind of a nightmare.

Imagine trying to write a CGI program in Perl or C back in the late nineties, where you are manually printing, HTTP headers and HTML as bias. there just wasn't any good abstraction layer to go with. There were already some libraries and frameworks for ActivityPub out there but none of them really hit the sweet spot I was looking for. They were either too high level and rigid. Like you could only build a mastodon clone or they barely did anything at all. Or they were written in languages I didn't really know. 


## Ghost and Fedify

[00:31:24] **Jeremy:** I saw that you are doing some work with, ghost. How is Ghost using fedify?

[00:31:30] **Hong:** Ghost is an open source publishing platform. They have put some money into fedify which is why I get to work on it full time now. Their ActivityPub feature is still in private beta but it should be available to everyone pretty soon.

We work together to improve fedify. Basically they are a user of fedify. They report bugs request new features to fedify then I fix them or implement them, first.

[00:32:16] **Jeremy:** Ghost to my understanding is a blogging platform and a a newsletter platform. So what does it mean for them to implement ActivityPub? What would somebody using Mastodon, for example, get when they follow somebody using Ghost?

[00:32:38] **Hong:** Ghost will have a fediverse handle for each blog. If you follow them in your mastodon or something (similar) then a new post is published. These post will show up (in) your timeline in Mastodon and you can like them or share them. Andin the dashboard of Ghost you can see who liked their posts or shared their posts and so on.

It is like how mastodon works but in Ghost.

[00:33:26] **Jeremy:** I see. So if you are writing a ghost blog and somebody follows your blog from Mastodon, sort of like we were talking about earlier, they can like your post, and on the blog itself you could show, oh, I have 200 likes. And those aren't necessarily people who were on your ghost website, they could be people that were liking your post from Mastodon.

[00:33:58] **Hong:** Yes.


## Misskey / Forkey development in Asia

[00:34:00] **Jeremy:** Something you mentioned at the beginning was there is a community of developers in Asia making forks of I believe of Mastodon, right?

[00:34:13] **Hong:** Yeah.

[00:34:14] **Jeremy:** Do you have experience working in that development community? What's different about it compared to the more Western centric community?

[00:34:24] **Hong:** They are very similar in most ways. The key difference is language of course. They communicate in Japanese primarily. 

They also accept pull requests with English. But there are tons of comments in Japanese in their code. So you need to translate them into English or your first language to understand what code does.


So I think that makes a barrier for Western developers. In fact, many Western developers that contribute to misskey or forkey are able to speak a little Japanese. And many of the developers of misskey and forkey are kind of otaku. 

[00:35:31] **Jeremy:** Oh otaku okay.

[00:35:33] **Hong:** It's not a big deal, but you can see (the) difference in a glance.

[00:35:41] **Jeremy:** Yeah. You mentioned one of the things that I believe misskey implemented was the emoji reactions and maybe one of the reasons they wanted that was so that they could react to each other's posts with you know anime pictures or things like that.

[00:35:58] **Hong:** Yeah, that's right.

[00:36:01] **Jeremy:** You've mentioned misskey and forkey. So is misskey a fork of Mastodon and then is forkey a fork of misskey?

[00:36:10] **Hong:** No, misskey is not a fork of mastodon. (It) is built from scratch. It's its own implementation. And forkeys are forks of Mastodon. 

[00:36:22] **Jeremy:** Oh, I see. But both of those are primarily built by Japanese developers.

[00:36:30] **Hong:** Yes. Whereas Mastodon (is) written in Ruby. Ruby on Rails. But misskey is built in TypeScript.

[00:36:40] **Jeremy:** And because of ActivityPub -- they all implement it. So you can communicate with people between mastodon and misskey because they all understand the same activities.

[00:36:56] **Hong:** Yes.


## Backwards compatible activity implementations

[00:36:57] **Jeremy:** You did mention since there are extensions like misskey has the emoji reactions. When there is an activity that an implementation doesn't support what happens between the two servers? Do you send it to a server's inbox and then the server just doesn't do anything with it?

[00:37:16] **Hong:** Some implementers consider backwards compatibility. So they design (it) to work with other implementations that don't support that activity. 

For example misskey uses like activity for emoji reaction. So if you put an emoji to a Mastodon post then in Mastodon you get one like. So it's intended behavior by misskey developers that they fall back to normal likes.

But sometimes ActivityPub implementers introduce entirely new activity types. For example Pleroma introduced the emoji react. And if you put emoji reaction to Mastodon post from Pleroma in Mastodon you have nothing to see because Mastodon just ignores them. 

[00:38:37] **Jeremy:** If I understand correctly, both misskey and Pleroma are independent implementations of ActivityPub, but with misskey, they can tell when or their message is backwards compatible where it's if you don't understand the emoji reaction, it'll be embedded inside of a like message.

Whereas with Pleroma they send an activity that Mastodon can't understand at all. So it just doesn't do anything.

[00:39:11] **Hong:** Yes, right. But, Misskey also understands (the) emoji react activity. So between pleroma and misskey they have exchanged emoji reactions with no problem.

[00:39:27] **Jeremy:** Oh, I see. So they, they both understand that activity. They both implement it the same way, but then when misskey communicates with Mastodon or with an instance that it knows doesn't understand it, it sends something different.

[00:39:45] **Hong:** Yeah, that's right. 

[00:39:47] **Jeremy:** The servers -- can they query one another to know which activities they support?

[00:39:53] **Hong:** Usually ActivityPub implementations also implement `NodeInfo` specification.

It's like a user agent-like thing in Fediverse. Implementations tell the other instance (if it) is Mastodon or something else. You can query the type of server. 

[00:40:20] **Jeremy:** Okay, so within ActivityPub are each of the servers -- is the term node is that the word they use for each server?

[00:40:31] **Hong:** Yes. Right.

[00:40:32] **Jeremy:** You have the nodes, which can have any number of actors and the servers send activities to one another, to each other's inboxes. And so those are the way they all communicate.

[00:40:49] **Hong:** Yeah.


## Building an ActivityPub implementation

[00:40:50] **Jeremy:** You've implemented ActivityPub with Fedify because you found like there weren't good enough implementations or resources already. Did you implement it based off of the specification or did you look at existing implementations while you were building your implementation?

[00:41:12] **Hong:** To be honest, instead of just, diving into the spec. I usually start by looking at actually ActivityPub software code first. The ActivityPub spec is so vague that you can't really build something just from reading it. So when we talk about ActivityPub, we are actually talking about a whole bunch of other technical standards too, WebFinger, HTTP signatures and more. So you need to understand all of these as well. 

[00:41:47] **Jeremy:** With the specification alone, you were saying it's too vague and so what ends up being -- I'm not sure if it's right to call it a spec, but looking at the implementations that people have already made that collectively becomes the spec because trying to follow the spec just by itself is maybe too difficult.

[00:42:12] **Hong:** Yes. 

[00:42:14] **Jeremy:** Maybe that brings up the issues you were talking about before where you have specifications like JSON-LD where they're so complicated that even the biggest implementations aren't quite following it exactly.

[00:42:28] **Hong:** Yeah. 

[00:42:29] **Jeremy:** If somebody wanted to, to get started with understanding a little bit more about ActivityPub or building something with it where would you recommend they start? 

[00:42:44] **Hong:** I recommend to dig into a lot of code from actual implementations. 

First, Mastodon, Misskey, Akkoma and so on. There are are some really cool tools that have been so helpful. For example, ActivityPub Academy is this awesome mastodon server for debugging ActivityPub. It makes it super easy to create a temporary account and see what activities are going back and forth. 

There is also BrowserPub. BrowserPub is this neat tool for looking up and browsing ActivityPub objects. It's really handy when you want to see how different ActivityPub software handles various features. I also recommend to use Fedify. I've got to mention the Fedify CLI, which comes with some really useful tools.

[00:43:46] **Jeremy:** So if someone uses Fedify they're writing an application in TypeScript, then it sounds like they have to know the high level concepts. They have to know what are the different activities, what is inside of an actor. But the actual implementation of how do I create and parse JSON linked data, those kinds of things are taken care of by the library.

[00:44:13] **Hong:** Yes, right.

[00:44:16] **Jeremy:** So in some ways it seems like it might be good to, like you were saying, use the tools you mentioned to create a test Mastodon account, look at the messages being sent back and forth, and then when you're trying to implement it, starting with something like Fedify might be good because then you can really just focus on the concepts and not worry so much about the, the implementation details.

[00:44:43] **Hong:** Yes, that's right.

[00:44:45] **Jeremy:** Is there anything else you. Wanted to mention or thought we should have talked about?

[00:44:52] **Hong:** Mm. I want to, talk about, a lot of stuff about ActivityPub but it's difficult to speak in English for me, so, it's a shame to talk about it very little.

[00:45:15] **Jeremy:** We need everybody to learn Korean right?

[00:45:23] **Hong:** Yes, please. (laughs)

[00:45:23] **Jeremy:** Yeah. Well, I wanna thank you for taking the time. I know it must have been really challenging to give an interview in, you know, a language that's not your native one. So thank you for spending the time to talk with me.

[00:45:38] **Hong:** Thank you for having me.