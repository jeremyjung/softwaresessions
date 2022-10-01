+++
title = "Xe Iaso on Tailscale"

description = "Xe Iaso explains why Tailscale isn't a Virtual Pain Network"

[extra]
episode_url = "https://media.transistor.fm/0a2a6e6d/7740aae4.mp3"
+++

Xe Iaso is the Archmage of Infrastructure at Tailscale and previously worked at Heroku.

This episode originally aired on Software Engineering Radio but includes some additional discussion about their blog near the end of the episode.

### Topics covered:

- Use cases for VPNs
- Simplifying service authentication by identifying users via IP
- Peer-to-peer vs centralized "Virtual Pain Networks"
- Tailscale's tech stack and why they forked the go compiler
- DERP relay servers
- Struggling with the iOS network extension size limit
- The surprisingly small amount of infrastructure required to run a VPN
- Running your company on your own product
- Working at Heroku vs Tailscale
- Using the socratic style of debate in technical blog posts


### Related Links

- [@theprincessxena](https://twitter.com/theprincessxena)
- [Xe's Blog](https://xeiaso.net/)
- [ACL samples](https://tailscale.com/kb/1018/acls/#introduction)
- [Go links origin story](https://www.trot.to/blog/2020/07/09/go-links-origin-story)
- [How Tailscale works](https://tailscale.com/blog/how-tailscale-works)
- [Tailscale SSH](https://tailscale.com/tailscale-ssh/)
- [How Tailscale assigns IP addresses](https://tailscale.com/kb/1033/ip-and-dns-addresses/)
- [Hey linker, can you spare a meg?](https://tailscale.com/blog/go-linker/)
- [My Blog is Hilariously Overengineered to the Point People Think it's a Static Site](https://xeiaso.net/talks/how-my-website-works)
- [The Sheer Terror of PAM](https://xeiaso.net/talks/rustconf-2022-sheer-terror-pam)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** Today I'm talking to Xe Iaso, they're the archmage of infrastructure at tailscale, and they also have a great blog everyone should check out. 

Xe, welcome to software engineering radio.

[00:00:12] **Xe:** Thanks. It's great to be here. 

[00:00:14] **Jeremy:** I think the first thing we should start with, is what's a, a VPN, because I think some people they may have used it to remote into their workplace or something like that. But I think the, the scope of what it's good for and what it does is a lot broader than that. So maybe you could talk a little bit about that first.

[00:00:31] **Xe:** Okay. a VPN is short for virtual private network. It's basically a fake network that's overlaid on top of existing networks. And then you can use that network to do whatever you would with a normal computer network. this term has been co-opted by companies that are attempting to get into the, like hide my ass style market, where, you know, you encrypt your internet information and keep it safe from hackers.

But, uh, so it makes it really annoying and hard to talk about what a VPN actually is. Because tailscale, uh, the company I work for is closer to like the actual intent of a VPN and not just, you know, like hide your internet traffic. That's already encrypted anyway with another level of encryption and just make a great access point for, uh, three letter agencies.

But are there, use cases, past that, like when you're developing a piece of software, why would you decide to use a VPN outside of just because I want my, you know, my workers to be able to get access to this stuff.

[00:01:42] **Xe:** So something that's come up, uh, when I've been working at tailscale is that sometimes we'll make changes to something. And it'll be changes to like the user experience of something on the admin panel or something. So in a lot of other places I've worked in order to have other people test that, you know, you'd have to push it to the cloud.

It would have to spin up a review app in Heroku or some terrifying terraform of abomination would have to put it out onto like an actual cluster or something. But with tail scale, you know, if your app is running locally, you just give like the name of your computer and the port number. And you know, other people are able to just see it and poke it and experience it.

And that basically turns the, uh, feedback cycle from, you know, like having to wait for like the state of the world to converge, to, you know, make a change, press F five, give the URL to a coworker and be like, Hey, is this Gucci?

they can connect to your app as if you were both connected to the same switch.

[00:02:52] **Jeremy:** You don't have to worry about, pushing to a cloud service or opening ports, things like that.

[00:02:57] **Xe:** Yep. It will act like it's in the same room, even when they're not it'll even work. if you're at both at Starbucks and the Starbucks has reasonable policies, like holy crap, don't allow devices to connect to each other directly. so you know, you're working on. Like your screenplay app at your Starbucks or something, and you have a coworker there and you're like, Hey, uh, check this out and, uh, give them the link.

And then, you know, they're also seeing the screenplay editor.

[00:03:27] **Jeremy:** in terms of security and things like that. I mean, I'm picturing it kind of like we were sitting in the same room and there's a switch and we both plugged in. Normally when you do something like that, you kind of have, full access to whatever else is on the switch. Uh, you know, provided that's not being blocked by a, a firewall.

is there like a layer of security on top of that, that a VPN service like tailscale would provide.

[00:03:53] **Xe:** Yes. Um, there are these things called access control lists, which are kind of like firewall rules, except you don't have to deal with like the nightmare of writing an IP tables rule that also works in windows firewall and whatever they use in Mac OS. The ACL rules are applied at the tailnet level for every device in the tailnet.

So if you have like developer machines, you can put people into groups as things like developers and say that developer machines can talk to production, but not people in QA. They can only talk to testing and people on SRE have, you know, permissions to go everywhere and people within their own teams can connect to each other. you can make more complicated policies like that fairly easily.

[00:04:44] **Jeremy:** And when we think about infrastructure for, for companies, you were talking about how there could be development, infrastructure, production, infrastructure, and you kind of separate it all out. when you're working with cloud infrastructure. A lot of times, there's the, I always forget what it stands for, but there's like IAM.

There's like policies that you can set up with the cloud provider that says these users can access this, or these machines can access this. And, and I wonder from your perspective, when you would choose to use that versus use something at the, the network or the, the VPN level.

[00:05:20] **Xe:** The way I think about it is that things like IAM enforce, permissions for like more granularly scoped things like can create EC2 instances or can delete EC2 instances or something like that. And that's just kind of a different level of thing. uh, tailscale, ACLs are more, you know, X is allowed to connect to Y or with tailscale, SSH X is allowed to connect as user Y.

and that's really different than like arbitrary capability things like IAM offers.

you could think about it as an IAM system, but the main permissions that it's exposing are can X connect to Y on Zed port.

[00:06:05] **Jeremy:** What are some other use cases where if you weren't using a VPN, you'd have to do a lot more work or there's a lot more complexity, kind of what are some cases where it's like, okay, using a VPN here makes a lot of sense.

(The quick and simple guide to go links https://www.trot.to/go-links) 

[00:06:18] **Xe:** There is a service internal to tailscale called go, which is a, clone of Google's so-called go links where it's basically a URL shortener that lives at http://go. And, you know, you have go/something to get to some internal admin service or another thing to get to like, you know, the company directory and notion or something, and this kind of thing you could do with a normal setup, you know, you could set it up and have to do OAuth challenges everywhere and, you know, have to put and make sure that everyone has the right DNS configuration so that, it shows up in the right place.

And then you have to deal with HTTPS um, because OAuth requires HTTPS for understandable and kind of important reasons. And it's just a mess. Like there's so many layers of stuff like the, the barrier to get, you know, like just a darn URL, shortener up turns from 20 minutes into three days of effort trying to, you know, understand how these various arcane things work together.

You need to have state for your OAuth implementation. You need to worry about what the hell a a JWT is (sigh) . It's it it's just bad. And I really think that something like tailscale with everybody has an IP address. In order to get into the network, you have to sign in with your, auth provider, your, a provider tells tailscale who you are.

So transitively every IP address is tied to an owner, which means that you can enforce access permission based on the IP address and the metadata about it that you grab from the tailscale. daemon, it's just so much simpler. Like you don't have to think about, oh, how do I set up OAuth this time? What the hell is an oauth proxy?

Um, what is a Kubernetes? That sort of thing you just think about like doing the thing and you just do it. And then everything else gets taken care of it. It's like kind of the ultimate network infrastructure, because it's both omnipresent and something you don't have to think about. And I think that's really the power of tailscale.

[00:08:39] **Jeremy:** typically when you would spin up a, a service that you want your developers or your system admins, to be able to log into, you would have to have some way of authenticating and authorizing that user. And so you were talking about bringing in OAuth and having your, your service understand that.

But I, I guess what you're saying is that when you have something like tailscale, that's kind of front loaded, I guess you, you authenticate with tail scale, you get onto the network, you get your IP. And then from that point on you can access all these different services that know like, Hey, because you're on the network, we know you're authenticated and those services can just maybe map that IP that's not gonna change to like users in some kind of table. Um, and not have to worry about figuring out how do I authenticate this user.

[00:09:34] **Xe:** I would personally more suggest that you use the, uh, whois, uh, look up route in the tailscale daemon's local API, but basically, yeah, you don't really have to worry too much about like the authentication layer because the authentication layer has already been done. You know, you've already done your two factor with Gmail or whatever, and then you can just transitively push that property onto your other machines.

[00:10:01] **Jeremy:** So when you talk about this, this whois daemon, can you give an example of I'm in the network now I'm gonna make a service call to an application. what, what am I doing with this? This whois daemon?

[00:10:14] **Xe:** It's more of like a internal API call that we expose via tailscaled's, uh, Unix, socket. but basically you give it an IP address and a port, and it tells you who the person is. It's kind of like the Unix ident protocol in a way, except completely not. And at a high level, you know, if you have something like a proxy for Grafana, you have that proxy for Grafana, make a call to the local tailscale daemon, and be like, Hey, who was this person?

And the tailscale, daemon will spit back at JSON object. Like, oh, it's this person on this device and there you can do additional logic like maybe you shouldn't be allowed to delete things from an iOS device, you know, crazy ideas like that. there's not really support for like arbitrary capabilities and tailscaled at the time of recording, but we've had some thoughts would be cool.

[00:11:17] **Jeremy:** would that also include things like having roles, for example, even if it's just strings, um, that you get back so that your application would know, okay. This person, is supposed to have admin access to this service based on what I got back from, this, this service.

[00:11:35] **Xe:** Not currently, uh, you can probably do it via convention or something, but what's currently implemented in the actual, like, source code and user experience that they, you can't do that right now. Um, it is something that I've been, trying to think about different ways to solve, but it's also a problem.

That's a bit big for me personally, to tackle.

[00:11:59] **Jeremy:** there's, there's so many, I guess, different ways of doing it. That it's kind of interesting to think of a solution that's kind of built into the, the network. Yeah.

[00:12:10] **Xe:** Yeah. and when I describe that authentication thing to some people, it makes them recoil in shock because there's kind of a Stockholm syndrome type effect with security, for a lot of things where, the easy way to do something and the secure way to do something are, you know, like completely opposite and directly conflicting with each other in almost every way.

And over time, people have come to associate security or like corporate VPNs as annoying, complicated, and difficult. And the idea of something that isn't annoying, complicated or difficult will make people reject it, like just on principle, because you know, they've been trained that, you know, VPN equals virtual pain network and it, it's hard to get that association outta people's heads because you know, a lot of VPNs are virtual pain networks.

Like. I used to work for Salesforce and Salesforce had this corporate VPN where no matter what you did, all of your traffic would go out to the internet from their data center. I think it was in San Francisco or something. And I was in the Seattle area. So whenever I had the VPN on my latency to Google shot up by like eight times and being a software person, you know, I use Google the same way that others breathe and it, it was just not fun.

And I only had the VPN on for the bare minimum of when I needed it. And, oh God, it was so bad.

[00:13:50] **Jeremy:** like some people, when they picture a VPN, they picture exactly what you're describing, where all of my traffic is gonna get routed to some central point. It's gonna go connect to the thing for me and then send the result back. so maybe you could talk a little bit about why that's, that's maybe a wrong assumption, I guess, in the case of tailscale, or maybe in the case of just more modern VPN solutions.

[00:14:13] **Xe:** Yeah. So the thing that I was describing is what I've been lovingly calling the, uh, single point of failure as a service type model of VPN, where, you know, you have like the big server somewhere, it concentrates all the connections and, you know, like does things to make the computer feel like they've teleported over there, but overall it's a single point of failure.

And if that falls over, you know, like goodbye, VPN. everybody's just totally screwed. And in contrast, tailscale does a more peer-to-peer thing so that everyone is basically on equal footing. Everyone can send traffic directly to each other, and if it can't get directly to there, it'll use a network of, uh, relay servers, uh, lovingly called Derp and you don't have to worry about, your single point of failure in your cluster, because there's just no single point of failure.

Everything will directly communicate as much as possible. And if it can't, it'll still communicate anyway.

[00:15:18] **Jeremy:** let's say I start up my computer and I wanna connect to a server in a data center somewhere at the very beginning, am I connecting to some server hosted at tailscale? And then. There's some kind of negotiation process where after that I connect directly or do I just connect directly straight away?

[00:15:39] **Xe:** If you just turn on your laptop and log in, you know, to it signs into tailscale and gets you on the tailnet and whatnot, then it will actually start all connections via Derp just so that it can negotiate the, uh, direct connection. And in case it can't, you know, it's already connected via Derp so it just continues the connection with Derp and this creates a kind of seamless magic type experience where doing things over Derp is slower.

Yes, it is measurably slower because you know, like you're not going directly, you're doing TCP inside of TCP. And you know, that comes with a average minefield of lasers or whatever you call it. And it does work though. It's not ideal if you wanna do things like copy large amounts of data, but if you want just want ssh into prod and see the logs for what the heck is going on and why you're getting paged at 3:00 AM. it's pretty great.

[00:16:40] **Jeremy:** What you, you were calling Derp is it where you have servers kind of all over the world and somehow it determines which one's, I guess, is it which one's closest to your destination or which one's closest to you. I'm kind of

[00:16:54] **Xe:** It's really interesting. It's one of the most weird distributed systems, uh, type things that I've ever seen. It's the kind of thing that could only come outta the mind of an X Googler, but basically every tailscale, every tailscale node has a connection to all of the Derp servers and through process of, you know, latency testing.

It figures out which connection is the fastest and the lowest latency. And it calls that it's home Derp but because it's connected to everything is connected to every Derp you can have two people with different home Derps getting their packets relayed too other clients from different Derps.

So, you know, if you have a laptop in Ottawa and a laptop in San Francisco, the laptop in San Francisco will probably use the, uh, Derp that's closest to it. But the laptop in Ottawa will also use the Derp that's closest to it. So you get this sort of like asynchronous thing, and it actually works out a lot better in practice, than you're probably imagining.

[00:17:52] **Jeremy:** And then these servers, what was the, the technical term for them? Are they like relays or what's

[00:17:58] **Xe:** They're relays. Uh, they only really deal with encrypted wire guard packets, and there's, no way for us at tailscale, to see the contents of Derp messages, it is literally just a forwarder. It, it literally just forwards things based on the key ID.

[00:18:17] **Jeremy:** I guess if tail scale isn't able to decrypt the traffic, is, is that because the, the keys are only on the user's devices, like it's on their laptop and on the server they're trying to reach, or

[00:18:31] **Xe:** Yeah. The private keys are live and die with those devices or the devices they were minted on. And the public keys are given to the coordination server and the coordination server spreads those around to every device in your tailnet. It does some limiting so that like, if you don't have ACL access to something, you don't get the private key, you don't get the, uh, public key for it.

The public key, not the private key, the public key, not the private key. And yeah. Then, you know, you just go that way and it'll just figure it out. It's pretty nice.

[00:19:03] **Jeremy:** When we're kind of talking about situations where it can't connect directly, that's where you would use the relay. what are kind of the typical cases where that happens, where you, you aren't able to just connect directly?

[00:19:17] **Xe:** Hotel, wifi and paranoid network security setups, hotel wifi is the most notorious one because you know, you have like an overpriced wifi connection. And if you bring, like, I don't know like, You you're recording a bunch of footage on your iPhone. And because in, 2022. The iPhone has the USB2 connection on it.

And you know, you wanna copy that. You wanna use the network, but you can't. So you could just let it upload through iCloud or something, or, you know, do the bare minimum. You need to get the, to get the data off with Derp it wouldn't be ideal, but it would work. And ironically enough, that entire complexity involved with, you know, doing TCP inside of TCP to copy a video file over to your laptop might actually be faster than USB2, which is something that I did the math for a while ago.

And I just started laughing.

[00:20:21] **Jeremy:** Yeah, that that is pretty, pretty ridiculous 

[00:20:23] **Xe:** welcome to the future, man (laughs) .

[00:20:27] **Jeremy:** in terms of connecting directly, usually when you have a computer on the internet, you don't have all your ports open, you don't necessarily allow, just anybody to send you traffic over UDP and so forth. let's say I wanna send, UDP data to a, a server on my network, but, you know, maybe it has some TCP ports open. I I'm assuming once I connect into the network via the VPN, I'm able to use other protocols and ports that weren't necessarily exposed. Is that correct?

[00:21:01] **Xe:** Yeah, you can use UDP. you can do basically anything you would do on a normal network except multicast um, because multicast is weird.

I mean, there's thoughts on how to handle multicast, but the main problem is that like wireguard, which is what is tail tailscale is built on top of, is, so called OSI model layer three network, where it's at like, you know, the IP address level and multicast is a layer two or data link layer type thing.

And, those are different numbers and, you can't really easily put, you know, like broadcast packets into IP, uh, IPV4 thinks otherwise, but, uh, in practice, no people don't actually use the broadcast address.

[00:21:48] **Jeremy:** so for someone who's, they, they have a project or their company wants to get started. I mean, what does onboarding look like? What, what do they have to do to get all these devices talking to one another?

[00:22:02] **Xe:** basically you, install tail scale, you log in with a little GUI thing or on a Linux server, you run tailscale up, and then you all log to the, to a, like a G suite account with the same domain name. So, you know, if your domain is like example.com, then everybody logs in with their example.com G suite account.

And, there is no step three, everything is allowed and everything can just connect and you can change the permissions from there. By default, the ACLs are set to a, you know, very permissive allow everyone to talk to everyone on any port. Uh, just so that people can verify that it's working, you know, you can ping to your heart's content.

You can play Minecraft with others. You can, you know, host an HTTP server. You can SSH into your development box and and write blog post with emacs, whatever you want.

[00:22:58] **Jeremy:** okay, you install the, the software on your servers, your workstations, your laptops, and so on. And then at, after that there's some kind of webpage or dashboard you would go in and say, I want these people to be able to access these things and 

[00:23:14] **Xe:** Mm-hmm 

[00:23:15] **Jeremy:** these ports and so on.

[00:23:17] **Xe:** you, uh, can customize the access control rules with something that looks like JSON, but with trailing commas and comments allowed, and you can go from there to customize basically anything to your heart's content. you can set rules so that people on the DevOps team can access everything, but you know, maybe marketing doesn't need access to the production database.

So you don't have to worry about that as much.

[00:23:45] **Jeremy:** there's, there's kind of different options for VPNs. CloudFlare access, zero tier, there's, there's some kind of, I think it's Nebula from slack or something like that. so I was kind of curious from your perspective, what's the, difference between those kinds of services and, and tailscale.

[00:24:04] **Xe:** I'm gonna lead this out by saying that I don't totally understand the differences between a lot of them, because I've only really worked with tailscale. I know things about the other options, but, uh, I have the most experience with tailscale but from what I've been able to tell, there are things that tailscale offers that others don't like reverse mapping of IP addresses to people, or, there's this other feature that we've been working on, where you can embed tail scale as a library inside your go application, and then write a internal admin service that isn't exposed to the internet, but it's only exposed over tailscale.

And I haven't seen a way to do those things with those others, but again, I haven't done much research. Um, I understand that zero tier has some layer, two capabilities, but I've, I don't have enough time in the day to look into.

[00:25:01] **Jeremy:** There's been different, I guess you would call them VPN protocols. I mean, there's people have probably worked with IP sec in some situations they may have heard of OpenVPN, wireguard. in the case of tailscale, I believe you chose to build it on top of wireguard.

So I wonder if you could talk a little bit about why, you chose wireguard and, and maybe what makes it unique.

[00:25:27] **Xe:** I wasn't on the team that initially wrote like the core of tailscale itself. But from what I understand, wire guard was chosen because, what overhead, uh, it's literally, you just encrypt the packets, you send it to the other server, the other server decrypts them. And you know, you're done. it's also based purely on the public key. Um, the key pairs involved. And from what I understand, like at the wireguard protocol level, there's no reason why you, why you would need an IP address at all in theory, but in practice, you kind of need an IP address because you know, everything sucks. But also wire guard is like UDP only, which I think it at it's like core implementation, which is a step up from like AnyConnect and OpenVPN where they have TCP modes.

So you can experience the, uh, glorious, trash fire of TCP in TCP. And from what I understand with wireguard, you don't need to set up a certificate authority or figure out how the heck to revoke certificates. Uh, you just have key pairs and if a node needs to be removed, you delete the key pair and you're done.

And I think that really matches up with a lot of the philosophy behind how tailscale networks work a lot better. You know, you have a list of keys and if the network changes the list of keys changes, that's, that's the end of the story.

So maybe one of the big selling points was just What has the least amount of things I guess, to deal with, or what's the, the simplest, when you're using a component that you want to put into your own product, you kind of want the least amount of things that could go wrong, I guess.

[00:27:14] **Xe:** Yeah. It's more like simple, but not like limiting. Like, for example, a set of tinker toys is simple in that, you know, you can build things that you don't have to worry too much about the material science, but a set of tinker toys is also limiting because you know, like they're little wooden, dowels and little circles made out of wind that you stick the dowels into, you know, you can only do so much with it.

And I think that in comparison, wireguard is simple. You know, there's just key pairs. They're just encryption. And it's simple in it's like overall theory and it's implementation, but it's not limiting. Like you can do pretty much anything you want with it.

inherently whenever we build something, that's what we want, but that's a, that's an interesting way of putting it. Yeah.

[00:28:05] **Xe:** Yeah. It. It can be kind of annoyingly hard to figure out how to make things as simple as they need to be, but still allow for complexity to occur. So you don't have to like set up a keyboard macro to write if error not equals nil over and over.

[00:28:21] **Jeremy:** I guess the next thing I'd like to talk a little bit about is. We we've covered it a little bit, but at a high level, I understand that that tailscale uses wireguard, which is the open source, VPN protocol, I guess you could call it. And then there's the client software. You're saying you need to install on each of the servers and workstations.

But there's also a, a control plane. and I wonder if you could kind of talk a little bit about I guess at a high level, what are all the different components of, of tailscale?

[00:28:54] **Xe:** There's the agent that you install in your devices. The agent is basically the same between all the devices. It's all written in go, and it turns out that go can actually cross compile fairly well. So you have. Your, you know, your implementation in go, that is basically the, the same code, more or less running on windows, MacOS, freeBSD, Android, ChromeOS, iOS, Linux.

I think I just listed all the platforms. I'm not sure, but you have that. And then there's the sort of control plane on tailscale's side, the control plane is basically like control, uh, which is, uh, I think a get smart reference. and that is basically a key dropbox. So, you know, you You authenticate through there. That's where the admin panel's hosted. And that's what tells the different tailscale nodes uh, the keys of all the other machines on the tailnet. And also on tailscale side there's, uh, Derp which is a fleet of a bunch of different VPSs in various clouds, all over the world, both to try to minimize cost and to, uh, have resiliency because if both digital ocean and Vultr go down globally, we probably have bigger problems.

[00:30:15] **Jeremy:** I believe you mentioned that the, the clients were written in go, are the control plane and the relay, the Derp portion. Are those also written in go or are they

[00:30:27] **Xe:** They're all written and go, yeah,

go as much as possible. Yeah.

It's kind of what happens when you have some ex go team members is the core people involved in tail scale, like. There's a go compiler fork that has some additional patches that go upstream either can't accept, uh, won't accept or hasn't yet accepted, for a while. It was how we did things like trying to shave off by bites from binary size to attempt to fit it into the iOS network extension limit.

Because for some reason they only allowed you to have 15 megabytes of Ram for both like your application and working Ram. And it turns out that 15 megabytes of Ram is way more than enough to do something like OpenVPN. But you know, when you have a peer-to-peer VPN engine, it doesn't really work that well.

So, you know, that's a lot of interesting engineering challenge.

[00:31:28] **Jeremy:** That was specifically for iOS. So to run it on an iPhone.

[00:31:32] **Xe:** Yeah. Um, and amazingly after the person who did all of the optimization to the linker, trying to get the binary size down as much as possible, like replacing Unicode packages was something that's more coefficient, you know, like basically all but compressing parts of the binary to try to save space. Then the iOS, I think 15 beta dropped and we found out that they increased the network extension Ram limit to 50 megabytes and the look of defeat on that poor person's face. I feel very bad for him.

[00:32:09] **Jeremy:** you got what you wanted, but you're sad about it,

[00:32:12] **Xe:** Yeah.

[00:32:14] **Jeremy:** so that's interesting too. you were using a fork of the go compiler 

[00:32:19] **Xe:** Basically everything that is built is built using, uh, the tailscale fork, of the go compiler.

[00:32:27] **Jeremy:** Going forward is the sort of assumption is that's what you'll do, or is it you're, you're hoping you can get this stuff upstreamed and then eventually move off of it.

[00:32:36] **Xe:** I'm pretty sure that, I, I don't know if I can really make a forward looking statement like that, but, I've come to accept the fact that there's a fork of the go compiler. And as a result, it allows a lot more experimentation and a bit more of control, a bit more control over what's going on. like I'm, I'm not like the most happy with it, but I've, I understand why it exists and I'm, I've made my peace with it.

[00:33:07] **Jeremy:** And I suppose it, it helps somewhat that the people who are working on it actually originally worked on the, go compiler at Google. Is that right?

[00:33:16] **Xe:** Oh yeah. If, uh, there weren't ex go team people working on that, then I would definitely feel way less comfortable about it. But I trust that the people that are working on it, know what they're doing at least enough.

[00:33:30] **Jeremy:** I, I feel like, that's, that's kind of the position we put ourselves in with software in general, right? Is like, do we trust our ourselves enough to do this thing we're doing?

[00:33:39] **Xe:** Yeah. And trust is a bitch.

[00:33:44] **Jeremy:** um, I think one of the things that's interesting about tail scale is that it's a product that's kind of it's like network infrastructure, right? It's to connect you to your other devices. And that's a little different than somebody running a software as a service. And so. how do you test something that's like built to support a network and, and how is that different than just making a web app or something like that.

[00:34:11] **Xe:** Um, well, it's a lot more complicated for one, especially when you have to have multiple devices in the mix with multiple different operating systems. And I was working on some integration tests, doing stuff for a while, and it was really complicated. You have to spin up virtual machines, you know, you have to like make sure the virtual machines are attempting to download the version of the tailscale client you wanna test and. It's it's quite a lot in practice.

[00:34:42] **Jeremy:** I mean, do you have a, a lab, you know, with Android phones and iPhones and laptops and all this sort of stuff, and you have some kind of automated test suite to see like, Hey, if these machines are in Ottawa and, my servers in San Francisco, like you're mentioning before that I can get from my iPhone to this server and the data center over here, that kind of thing.

[00:35:06] **Xe:** What's the right way to phrase this without making things look bad. Um, it's a work in progress. It it's, it's really a hard problem to solve, uh, especially when the company is fully remote and, uh, like. Address that's listed on the business records is literally one of the founders condos because you know, the company has no office.

So that makes the logistics for a lot of this. Even more fun.

[00:35:37] **Jeremy:** Probably any company that's in an early stage feels the same way where it's like, everything's a work in progress and we're just gonna, we're gonna keep going and we're gonna get there. And as long as everything keeps running, we're good.

[00:35:50] **Xe:** Yeah. I, I don't like thinking about it in that way, because it kind of sounds like pessimistic or defeatist, but at some level it's, it, it really is a work in progress because it's, it's a hard problem and hard problems take a lot of time to solve, especially if you want a solution that you're happy with.

[00:36:10] **Jeremy:** And, and I think it's kind of a unique case too, where it's not like if it goes down, it's like people can't do their job. Right. So it's yeah.

[00:36:21] **Xe:** Actually, if tail scales like control plane goes down, I don't think people would notice until they tried to like boot up a, a reboot, a laptop, or connect a new device to their tailnet. Because once, once all the tailscale agents have all of the information they need from the control plate, you know, they just, they just continue on independently and don't have to care.

Derp is also fairly independent of the, like the key dropbox component. And, you know, if that, if that goes down Derp doesn't care at all,

[00:37:00] **Jeremy:** Oh, okay. So if the control plane is down, as long as you had authenticated earlier in the day, you can still, I don't know if it's cached or something, but you can still continue to reach the relay servers, the Derp servers or your, 

[00:37:15] **Xe:** other nodes. Yeah. I, I'm pretty sure that in most cases, the control plane could be down for several hours a day and nobody would notice unless they're trying to deal with the admin panel.

[00:37:28] **Jeremy:** Got it. that's a little bit of a relief, I suppose, for, for all of you running it,

[00:37:33] **Xe:** Yeah. Um, it's also kind of hard to sell people on the idea of here is a VPN thing. You don't need to self host it and they're like, what? Why? And yeah, it can be fun.

[00:37:49] **Jeremy:** though, I mean, I feel like anybody who has, self-hosted a VPN, they probably like don't really wanna do it. I don't know. Maybe I'm wrong.

[00:38:00] **Xe:** well, so a lot of the idea of wanting to self host it is, uh, I think it's more of like trying to be self-sufficient and not have to rely on other companies, failures dictating your company's downtime. And, you know, like from some level that's very understandable. And, you know, if, you know, like tail scale were to get bought out and the new owners would, you know, like basically kill the product, they'd still have something that would work for them.

I don't know if like such a defeatist attitude is like productive. But it is certainly the opinion that I have received when I have asked people why they wanna self-host. other people, don't want to deal with identity providers or the, like, they wanna just use their, they wanna use their own identity provider.

And what was hilarious was there was one, there was one thing where they were like our old VPN server died once and we got locked out of our network. So therefore we wanna, we wanna self-host tailscale in the future so that this won't happen again.

And I'm like, buddy, let's, let's just, let's just take a moment and retrace our steps here. CAuse I don't think you mean what you think you mean.

[00:39:17] **Jeremy:** yeah, yeah. 

[00:39:19] **Xe:** In general, like I suggest people that, you know, even if they're like way deep into the tailscale, Kool-Aid they still have at least one other method of getting into their servers. Ideally, two. I, I admit that I'm, I come from an SRE style background and I am way more paranoid than most, but it, I usually like having, uh, a backup just in case.

[00:39:44] **Jeremy:** So I, I suppose, on, on that note, let's, let's talk a little bit about your role at tailscale. the title of the archmage of infrastructure is one of the, the coolest titles I've, uh, I've seen. So maybe you can go a little bit into what that entails at, at tailscale.

[00:40:02] **Xe:** I started that title as a joke that kind of stuck, uh, my intent, my initial intent was that every time someone asked, I'd say, I'd have a different, you know, like mystic sounding title, but, uh, archmage of infrastructure kind of stuck. And since then, I've actually been pivoting more into developer relations stuff rather than pure software engineering.

And, from the feedback that I've gotten at the various conferences I've spoken at, they like that title, even though it doesn't really fit with developer relations work at all, it it's like it fits because it doesn't. You know, that kind of coney kind of way.

[00:40:40] **Jeremy:** I guess this would go more into the, the infrastructure side, but. What does the, the scale of your infrastructure look like? I mean, I, I think that you touched a little bit on the fact that you have relay servers all over the place and you've got this control plane, but I wonder if you could give people a little bit of perspective of what kind of undertaking this is.

[00:41:04] **Xe:** I am pretty sure at this point we have more developer laptops and the like, than we do production servers. Um, I'm pretty sure that the scale of the production of production servers are in the tens, at most. Um, it turns out that computers are pretty darn and efficient and, uh, you don't really need like a lot of computers to do something amazing.

[00:41:27] **Jeremy:** the part that I guess surprises me a little bit is, is the relay servers, I suppose, because, I would imagine there's a lot of traffic that goes through those. are you finding that just most of the time they just aren't needed and usually you can make a direct connection and that's why you don't need too many of these.

[00:41:45] **Xe:** From what I understand. I don't know if we actually have a way to tell, like what percentage of data is going over the relays versus not. And I think that was an intentional decision, um, that may have been revisited I'm operating based off of like six to 12 month old information right now. But in general, like the only state that the relay servers has is in Ram.

And whenever the relay, whenever you disconnect the server, the state is dropped.

[00:42:18] **Jeremy:** Okay.

[00:42:19] **Xe:** and even then that state is like, you know, this key is listening. It is, uh, connected, uh, in case you wanna send packets over here, I guess. 

it's a bit less bandwidth than you're probably thinking it's not like enough to max it out 24/7, but it is, you know, measurable and there are some, you know, costs associated with it. This is also why it's on digital ocean and vulture and not AWS. but in general, it's a lot less than you'd think. I'm pretty sure that like, if I had to give a baseless assumption, I'd say that probably about like 85% of traffic goes directly.

And the remaining is like the few cases in the whole punching engine that we haven't figured out yet. Like Palo Alto fire walls. Oh God. Those things are a nightmare.

[00:43:13] **Jeremy:** I see. So it's most of the traffic actually ends up. Being straight peer to peer. Doesn't have to go through your infrastructure. And, and therefore it's like, you don't need too many machines, uh, to, to make this whole thing work.

[00:43:28] **Xe:** Yeah. it turns out that computers are pretty darn fast and that copying data is something that computers are really good at doing. Um, so if you have, you know, some pretty darn fast computers, basically just sitting there and copying data back and forth all day, like it, you can do a lot with shockingly little.

Um, when I first started, I believe that the Derp VMs were using like sometimes as little as one core and 512 megabytes of Ram as like a primary Derp. And, you know, we only noticed when, there were some weird connection issues for people that were only on Derp because there were enough users that the machine had ran out of memory.

So we just, you know, upped the, uh, virtual machine size and called it a day. But it's, it's truly remarkable how mu how far you can get with very little

[00:44:23] **Jeremy:** And you mentioned the relay servers, the, the Derp servers were on services like digital ocean and Vultr. I'm assuming because of the, the bandwidth cost, for the control plane, is, is that on AWS or some other big cloud provider?

[00:44:39] **Xe:** it's on AWS. I believe it's in EU central 1.

[00:44:44] **Jeremy:** You're helping people connect from device to device and in a situation like that. what does monitoring look like in, in incidents? Like what are you looking for to determine like, Hey, something's not working.

[00:44:59] **Xe:** there's monitoring with, you know, Prometheus, Grafana, all of that stuff. there are some external probing things. there's also some continuous functional testing for trying to connect to tailscale and like log in as an account. And if that fails like twice in a row, then, you know, something's very wrong and, you know, raise the alarm.

But in general. A lot of our monitoring is kind of hard at some level because you know, we're tailscale at a tailscale can't always benefit from tailscale to help operate tail scale because you know, it's tailscale. Um, so it, it still trying to figure out how to detangle the chicken and egg situation.

It's really annoying.

there's the, the term dog fooding, right? Where they're saying like, oh, we, we run, um, our own development on our own platform or our own software. but I could see when your product is network infrastructure, VPNs, where that could be a little, little dicey.

[00:46:06] **Xe:** Yeah, it is very annoying. But I I'm pretty sure we'll figure something out. It is just a matter of when, another thing that's come up is we've kind of wanted to use tailscale's SSH features, where you specify ACLs in your, you specify ACL rules to allow people to SSH, to other nodes as various users.

but if that becomes your main access to production, then you know, like if tailscale is down and you're tailscale, like how do you get in, uh, then there's been various philosophical discussions about this. it's also slightly worse if you use what's called check mode in SSH, where, uh, tail scale, SSH without check mode, you know, you just, it, the, the server checks against the policy rules and the ACL and if it. if it's okay, it lets you in. And if not, it says no, but with check mode, there's also this like eight hour, there's this like eight hour quote unquote lifetime for you to have like sudo mode on GitHub, where you do an auth an auth challenge with your auth aprovider. And then, you know, you're given a, uh, Hey, this person has done this thing type verification.

And if that's down and that goes through the control plane, and if the control plane is down and you're tailscale, trying to debug the control plane, and in order to get into the control plane over tailscale, you need to use the, uh, control plane. It, you know, that's like chicken and egg problem level 78,

which is a mythical level of chicken egg problem that, uh, has only been foretold in the legends of yore or something.

[00:47:52] **Jeremy:** at that point, it sounds like somebody just needs to, to drive to the data center and plug into the switch.

[00:47:59] **Xe:** I mean, It's not, it's not going to, it probably wouldn't be like, you know, we need to get a person with an angle grinder off of Craigslist type bad. Like it was with the Facebook BGP outage, but it it's definitely a chicken and egg problem in its own right.

it makes you do a lot of lateral thinking too, which is also kind of interesting.

[00:48:20] **Jeremy:** When, when you say lateral thinking, I'm just kind of curious, um, if you have an example of what you mean.

[00:48:27] **Xe:** I don't know of any example that isn't NDAed. Um, but basically, you know, tail scale is getting to the, to the point where tailscale is relying on tailscale to make tailscale function and you know, yeah. This is classic oroboros style problem.

I've heard a, uh, a wise friend of mine said that that is an ideal problem to have, which sounds weird at face value. But if you're getting to that point, that means that you're successful enough that, you know, you're having that problem, which is in itself a good thing, paradoxically.

[00:49:07] **Jeremy:** better to have that problem than to have nobody care about the product. Right.

[00:49:12] **Xe:** Yeah.

[00:49:13] **Jeremy:** kind of on that, that note, um, you mentioned you worked at, at Salesforce, uh, I believe that was working on Heroku. I wonder if you could talk a little about your experience working at, you know, tailscale, which is kind of more of a, you know, early startup versus, uh, an established company like Salesforce.

[00:49:36] **Xe:** So at the time I was working at Heroku, it definitely didn't feel like I was working at Salesforce for the majority of it. It felt like I was working, you know, at Heroku, like on my resume, I listed as Heroku. When I talked about it to people, I said, I worked at Heroku and that sales force was this, you know, mythical, Ohana thing that I didn't have to deal with unless I absolutely had to.

By the end of the time I was working at Heroku, uh, the salesforce, uh, sort of started to creep in and, you know, we moved from tracking issues in GitHub issues. Like we were used to, to using their, oh, what's the polite way to say this, their creation, which is, which was like the moral equivalent of JIRA implemented on top of Salesforce.

You had to be behind the VPN for it. And, you know, every ticket had 20 fields and, uh, there were no templates. And in comparison with tail scale, you know, we just use GitHub issues, maybe some like things in notion for doing like longer term tracking or Kanban stuff, but it's nice to not have. you know, all of the pomp and ceremony of filling out 20 fields in a ticket for like two sentences of this thing is obviously wrong and it's causing X to happen.

Please fix.

[00:51:08] **Jeremy:** I, I like that, that phrase, the, the creation, that's a very, very diplomatic term.

[00:51:14] **Xe:** I mean, I can think of other ways to describe it, but I'm pretty sure those ways wouldn't be allowed on the podcast. So

[00:51:25] **Jeremy:** Um, but, but yeah, I, I know what you mean for sure where, it, it feels like there's this movement from, Hey, let's just do what we need. Like let's fill in the information that's actually relevant and don't do anything else to a shift to, we need to fill in these 10 fields because that's the thing we do.

Yeah.

[00:51:48] **Xe:** Yeah. and in the time I've been working for tail scale, I'm like employee ID 12. And, uh, tail scale has gone from a company where I literally know everyone to just recently to the point where I don't know everyone anymore. And it's a really weird feeling. I've never been in a, like a small stage startup that's gotten to this size before, and I've described some of my feelings to other people who have been there and they're like, yeah, welcome to the club. So I figure a lot of it is normal. from what I understand, though, there's a lot of intentionality to try to prevent tail skill from becoming, you know, like Google style, complexity, organizational complexity, unless that is absolutely necessary to do something.

[00:52:36] **Jeremy:** it's a function of size, right? Like as you have more people, more teams, then more process comes in. that's a really tricky balance to, to grow and still keep that feeling of, I'm just doing the thing, I'm doing the work rather than all this other process stuff.

[00:52:57] **Xe:** Yeah, but it, I've also kind of managed to pigeonhole myself off into a corner with devrel stuff. And that's been nice. I've been working a bunch with, uh, like marketing people and, uh, helping out with support occasionally and doing a, like a godawful amount of writing.

[00:53:17] **Jeremy:** the, the writing, for our audience's benefit, I, I think they should, they should really check out your blog because I think that the way you write your, your articles is very thoughtful in terms of the balance of the actual example code or example scripts and the descriptions and, and some there's a little bit of a narrative sometimes too.

So, 

[00:53:40] **Xe:** Um, I'm actually more of a prose writer just by like how I naturally write things. And a lot of the style of how I write things is, I will take elements from, uh, the Socratic style of dialogue where, you know, you have the student and the teacher. And, you know, sometimes the student will ask questions that the teacher will answer.

And I found that that's a particularly useful way to help model understanding or, you know, like put side concepts off into their own little blurbs or other things like that. I also started doing those conversation things with, uh, furry art, specifically to dunk on a homophobe that was getting very angry at furry art being in, uh, another person's blog.

And that's it, it's occasionally fun to go into the, uh, orange website of bad takes and see the comments when people complain about it. oh gosh, the bad takes are hilariously good. Sometimes.

[00:54:45] **Jeremy:** it's good that you have like a, a positive, mindset around that. I know some people can read, uh, that sort of stuff and go, you know, just get really bummed out. 

[00:54:54] **Xe:** One of the ways I see it is that a lot of the time algorithms are based on like sheer numbers. So if you like get something that makes people argue in the comments, that number will go up and because there's more comments on it, it makes more people more likely to, to read the article and click on it.

So, sometimes I have been known to sprinkle, what's the polite way to say this. I've been known to sprinkle like intentionally kind of things that will, uh, get people and make them want to argue about it in the comments. Purely to make the engagement numbers rise up, which makes more people likely to read the article.

And, it's kind of a dirty practice, but you know, it makes more people read the article and more people benefit. So, you know, like it's kind of morally neutral, I guess.

[00:55:52] **Jeremy:** usually that, that seems like, a sketchy thing. But I feel like if it's in service to, uh, like a technical blog post, I mean, why not? Right.

[00:56:04] **Xe:** And a lot of the times I'll usually have the like, uh, kind of bad take, be in a little conversation blurb thing so that people will additionally argue about the characterization of, you know, the imaginary cartoon shark or whatever.

[00:56:20] **Jeremy:** That's good. It's the, uh, it's the Xe Xe universe that they're, they're stepping into.

[00:56:27] **Xe:** I've heard people describe it, uh, lovingly as the xeiaso.net cinematic universe.

I've had some ideas on how to expand it in the future with more characters that have more different kind of diverse backgrounds. But, uh, it turns out that writing this stuff is hard. Like actually very hard because you have to get this right.

You have to get the right balance of like snark satire, uh, like enlightenment. And

it's, it's surprisingly harder than you'd think. Um, but after a while, I've just sort of managed to like figure out as I'm writing where the side tangents come off and which ones I should keep and which ones I should, uh, prune and which ones can also help, Gain deeper understanding with a little like Socratic dialogue to start with a Mo like an incomplete assumption, like an incomplete picture.

And then, you know, a question of, wait, what about this thing? Doesn't that conflict with that? And like, well, yes. technically it does, but realistically we don't have to worry about that as much. So we can think about it just in terms of this bigger model and, uh, that's okay. Like, uh, I mentioned the OSI model earlier, you know, like the seven layer OSI model it's, you know, genuinely overkill for basically everything, except it's a really great conceptual model for figuring out the difference between, you know, like an ethernet cable, an ethernet, like the ethernet card, the IP stack TCP and, you know, TLS or whatever.

I have a couple talks that are gonna be up by the time this is published. Uh, one of them is my, uh, rustconf talk on my, or what was it called? I think it was called the surreal horrors of PAM or something where I discussed my experience, trying to bug a PAM module in rust, uh, for work. And, uh, it's the kind of story where, you know, it's bad when you have a break point on dlopen.

[00:58:31] **Jeremy:** That sounds like a nightmare.

[00:58:32] **Xe:** Oh yeah. Like part of the attempting to fix that process involved, going very deep. We're talking like an HTML frame set in the internet archive for sunOS documentation that was written around the time that PAM was used. Like it's things that are bad enough were like everything in the frame set, but the contents had eroded away through bit rot and you know, you're very lucky just to have what you do.

[00:59:02] **Jeremy:** well, I'm, I'm glad it was. It was you and not me. we'll get to, to hear about it and, and not have to go through the, the suffering ourselves.

[00:59:11] **Xe:** yeah. One of the things I've been telling people is that I'm not like a brilliant programmer. Like I know a bunch of people who are definitely way smarter than me, but what I am is determined and, uh, determination is a bit stronger of a force than you'd think.

[00:59:27] **Jeremy:** Yeah. I mean, without it, nothing gets done. Right.

[00:59:30] **Xe:** Yeah.

[00:59:31] **Jeremy:** as we wrap up, is there anything we missed or anything else you wanna mention? 

[00:59:36] **Xe:** if you wanna look at my blog, it's on xeiaso.net. That's X, E I a S o.net. Um, that's where I post things. You can see, like the 280 something articles at time of recording. It's probably gonna get to 300 at some point, oh God, it's gonna get to 300 at some point. Um, and yeah, from, I try to post articles about weekly, uh, depending on facts and circumstances, I have a bunch of talks coming up, like one about the hilarious over engineering I did in my blog.

And maybe some more. If I get back positive responses from calls for paper submissions,

[01:00:21] **Jeremy:** Very cool. Well, Xe thank you so much for, for coming on software engineering radio.

[01:00:27] **Xe:** Yeah. Thank you for having me. I hope you have a good day and, uh, try out tailscale, uh, note my bias, but I think it's great.

</div>