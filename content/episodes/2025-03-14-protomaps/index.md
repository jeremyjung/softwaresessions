+++
title = "Brandon Liu on Protomaps"

description = "Using static maps to build sites that last"

[extra]
episode_url = "https://pinecast.com/listen/acfcf9c8-bbe4-4f25-a260-b9751c121590.mp3"
social_title = "Brandon Liu on Protomaps"
social_description = "Using static maps to build sites that last"
+++

Brandon Liu is an open source developer and creator of the [Protomaps](https://protomaps.com/) basemap project.

We talk about how static maps help developers build sites that last, the PMTiles file format, the role of OpenStreetMap, and his experience funding and running an open source project full time.

### Protomaps
- [Protomaps](https://protomaps.com/)
- [PMTiles](https://docs.protomaps.com/pmtiles/)
- [Self-hosted slippy maps, for novices (like me)](https://blog.apps.npr.org/2024/11/26/slippy-maps.html)
- [Why Deploy Protomaps on a CDN](https://docs.protomaps.com/deploy/)

### Protomaps user examples
- [Flickr](https://www.flickr.com/map)
- [Pinball Map](https://pinballmap.com/)
- [Toilet Map](https://www.toiletmap.org.uk/)

### Related projects
- [OpenStreetMap](https://www.openstreetmap.org/)
- [Mapzen](https://www.mapzen.com/)
- [Mapbox GL JS](https://github.com/mapbox/mapbox-gl-js)
- [MapLibre GL JS](https://github.com/maplibre/maplibre-gl-js) (Open source fork of Mapbox GL JS)

### Other links
- [HTTP range requests (MDN)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Range_requests)
- [Hilbert curve](https://en.wikipedia.org/wiki/Hilbert_curve)


## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

## Intro

[00:00:00] **Jeremy:** I'm talking to Brandon Liu. He's the creator of Protomaps, which is a way to easily create and host your own maps. Let's get into it. 

[00:00:09] **Brandon:** Hey, so thanks for having me on the podcast. So I'm Brandon. I work on an open source project called Protomaps. What it really is, is if you're a front end developer and you ever wanted to put maps on a website or on a mobile app, then Protomaps is sort of an open source solution for doing that that I hope is something that's way easier to use than, um, a lot of other open source projects.

## Why not just use Google Maps?

[00:00:36] **Jeremy:** A lot of people are gonna be familiar with Google Maps. Why should they worry about whether something's open source? Why shouldn't they just go and use the Google maps API?

[00:00:47] **Brandon:** So Google Maps is like an awesome thing it's an awesome product. Probably one of the best tech products ever right? And just to have a map that tells you what restaurants are open and something that I use like all the time especially like when you're traveling it has all that data.

And the most amazing part is that it's free for consumers but it's not necessarily free for developers. Like if you wanted to embed that map onto your website or app, that usually has an API cost which still has a free tier and is affordable. But one motivation, one basic reason to use open source is if you have some project that doesn't really fit into that pricing model.

You know like where you have to pay the cost of Google Maps, you have a side project, a nonprofit, that's one reason. But there's lots of other reasons related to flexibility or customization where you might want to use open source instead.


## Protomaps examples

[00:01:49] **Jeremy:** Can you give some examples where people have used Protomaps and where that made sense for them?

[00:01:56] **Brandon:** I follow a lot of the use cases and I also don't know about a lot of them because I don't have an API where I can track a hundred percent of the users. Some of them use the hosted version, but I would say most of them probably use it on their own infrastructure. One of the cool projects I've been seeing is called [Toilet Map](https://www.toiletmap.org.uk/).

And what toilet map is if you're in the UK and you want find a public restroom then it maps out, sort of crowdsourced all of the public restrooms. And that's important for like a lot of people if they have health issues, they need to find that information. And just a lot of different projects in the same vein. 

There's another one called [Pinball Map](https://pinballmap.com/) which is sort of a hobby project to find all the pinball machines in the world. And they wanted to have a customized map that fit in with their theme of pinball. So these sorts of really cool indie projects are the ones I'm most excited about.


## Basemaps vs Overlays

[00:02:57] **Jeremy:** And if we talk about, like the pinball map as an example, there's this concept of a basemap and then there's the things that you lay on top of it. What is a basemap and then is the pinball locations is that part of it or is that something separate?

[00:03:12] **Brandon:** It's usually something separate. The example I usually use is if you go to a real estate site, like Zillow, you'll open up the map of Seattle and it has a bunch of pins showing all the houses, and then it has some information beneath it. That information beneath it is like labels telling, this neighborhood is Capitol Hill, or there is a park here. But all that information is common to a lot of use cases and it's not specific to real estate. So I think usually that's the distinction people use in the industry between like a base map versus your overlay.

The overlay is like the data for your product or your company while the base map is something you could get from Google or from Protomaps or from Apple or from Mapbox that kind of thing.


## PMTiles for hosting the basemap and overlays

[00:03:58] **Jeremy:** And so Protomaps in particular is responsible for the base map, and that information includes things like the streets and the locations of landmarks and things like that. Where is all that information coming from? 

[00:04:12] **Brandon:** So the base map information comes from a project called OpenStreetMap. And I would also, point out that for Protomaps as sort of an ecosystem. You can also put your overlay data into a format called PMTiles, which is sort of the core of what Protomaps is. So it can really do both. It can transform your data into the PMTiles format which you can host and you can also host the base map.

So you kind of have both of those sides of the product in one solution.

[00:04:43] **Jeremy:** And so when you say you have both are you saying that the PMTiles file can have, the base map in one file and then you would have the data you're laying on top in another file? Or what are you describing there?

[00:04:57] **Brandon:** That's usually how I recommend to do it. Oftentimes there'll be sort of like, a really big basemap 'cause it has all of that data about like where the rivers are. Or while, if you want to put your map of toilets or park benches or pickleball courts on top, that's another file. But those are all just like assets you can move around like JSON or CSV files.


## Statically Hosted

[00:05:19] **Jeremy:** And I think one of the things you mentioned was that your goal was to make Protomaps or the, the use of these PMTiles files easy to use. What does that look like for, for a developer? I wanna host a map. What do I actually need to, to put on my servers?

[00:05:38] **Brandon:** So my usual pitch is that basically if you know how to use S3 or cloud storage, that you know how to deploy a map. And that, I think is the main sort of differentiation from most open source projects. Like a lot of them, they call themselves like, like some sort of self-hosted solution. But I've actually avoided using the term self-hosted because I think in most cases that implies a lot of complexity.

Like you have to log into a Linux server or you have to use Kubernetes or some sort of Docker thing. What I really want to emphasize is the idea that, for Protomaps, it's self-hosted in the same way like CSS is self-hosted. So you don't really need a service from Amazon to host the JSON files or CSV files. It's really just a static file. 

[00:06:32] **Jeremy:** When you say static file that means you could use any static web host to host your HTML file, your JavaScript that actually renders the map. And then you have your PMTiles files, and you're not running a process or anything, you're just putting your files on a static file host.

[00:06:50] **Brandon:** Right. So I think if you're a developer, you can also argue like a static file server is a server. It's you know, it's the cloud, it's just someone else's computer. It's really just nginx under the hood. But I think static storage is sort of special. If you look at things like static site generators,  like Jekyll or Hugo, they're really popular because they're a commodity or like the storage is a commodity.

And you can take your blog, make it a Jekyll blog, hosted on S3. One day, Amazon's like, we're charging three times as much so you can move it to a different cloud provider. And that's all vendor neutral. So I think that's really the special thing about static storage as a primitive on the web. 


## Why running servers is a problem for resilience

[00:07:36] **Jeremy:** Was there a prior experience you had? Like you've worked with maps for a very long time. Were there particular difficulties you had where you said I just gotta have something that can be statically hosted?

[00:07:50] **Brandon:** That's sort of exactly why I got into this. I've been working sort of in and around the map space for over a decade, and Protomaps is really like me trying to solve the same problem I've had over and over again in the past, just like once and forever right? Because like once this problem is solved, like I don't need to deal with it again in the future.

So I've worked at a couple of different companies before, mostly as a contractor, for like a humanitarian nonprofit for a design company doing things like, web applications to visualize climate change. Or for even like museums, like digital signage for museums. And oftentimes they had some sort of data visualization component, but always sort of the challenge of how to like, store and also distribute like that data was something that there wasn't really great open source solutions. So just for map data, that's really what motivated that design for Protomaps.

[00:08:55] **Jeremy:** And in those, those projects in the past, were those things where you had to run your own server, run your own database, things like that?

[00:09:04] **Brandon:** Yeah. And oftentimes we did, we would spin up an EC2 instance, for maybe one client and then we would have to host this server serving map data forever. Maybe the client goes away, or I guess it's good for business if you can sign some sort of like long-term support for that client saying, Hey, you know, like we're done with a project, but you can pay us to maintain the EC2 server for the next 10 years.

And that's attractive. but it's also sort of a pain, because usually what happens is if people are given the choice, like a developer between like either I can manage the server on EC2 or on Rackspace or Hetzner or whatever, or I can go pay a SaaS to do it. In most cases, businesses will choose to pay the SaaS.

So that's really like what creates a sort of lock-in is this preference for like, so I have this choice between like running the server or paying the SaaS. Like businesses will almost always go and pay the SaaS.

[00:10:05] **Jeremy:** Yeah. And in this case, you either find some kind of free hosting or low-cost hosting just to host your files and you upload the files and then you're good from there. You don't need to maintain anything.

[00:10:18] **Brandon:** Exactly, and that's really the ideal use case. so I have some users these, climate science consulting agencies, and then they might have like a one-off project where they have to generate the data once, but instead of having to maintain this server for the lifetime of that project, they just have a file on S3 and like, who cares?

If that costs a couple dollars a month to run, that's fine, but it's not like S3 is gonna be deprecated, like it's gonna be on an insecure version of Ubuntu or something. So that's really the ideal, set of constraints for using Protomaps.

[00:10:58] **Jeremy:** Yeah. Something this also makes me think about is, is like the resilience of sites like remaining online, because I, interviewed, Kyle Drake, he runs Neocities, which is like a modern version of GeoCities. And if I remember correctly, he was mentioning how a lot of old websites from that time, if they were running a server backend, like they were running PHP or something like that, if you were to try to go to those sites, now they're like pretty much all dead because there needed to be someone dedicated to running a Linux server, making sure things were patched and so on and so forth. But for static sites, like the ones that used to be hosted on GeoCities, you can go to the internet archive or other websites and they were just files, right? You can bring 'em right back up, and if anybody just puts 'em on a web server, then you're good. They're still alive.


## Case study of news room preferring static hosting

[00:11:53] **Brandon:** Yeah, exactly. One place that's kind of surprising but makes sense where this comes up, is for newspapers actually. Some of the users using Protomaps are the Washington Post. And the reason they use it, is not necessarily because they don't want to pay for a SaaS like Google, but because if they make an interactive story, they have to guarantee that it still works in a couple of years.

And that's like a policy decision from like the editorial board, which is like, so you can't write an article if people can't view it in five years. But if your like interactive data story is reliant on a third party, API and that third party API becomes deprecated, or it changes the pricing or it, you know, it gets acquired, then your journalism story is not gonna work anymore.

So I have seen really good uptake among local news rooms and even big ones to use things like Protomaps just because it makes sense for the requirements.


## Working on Protomaps as an open source project for five years

[00:12:49] **Jeremy:** How long have you been working on Protomaps and the parts that it's made up of such as PMTiles?

[00:12:58] **Brandon:** I've been working on it for about five years, maybe a little more than that. It's sort of my pandemic era project. But the PMTiles part, which is really the heart of it only came in about halfway. 


## Why not make a SaaS?

[00:13:13] **Brandon:** So honestly, like when I first started it, I thought it was gonna be another SaaS and then I looked at it and looked at what the environment was around it.

And I'm like, uh, so I don't really think I wanna do that.

[00:13:24] **Jeremy:** When, when you say you looked at the environment around it what do you mean? Why did you decide not to make it a SaaS?

[00:13:31] **Brandon:** Because there already is a lot of SaaS out there. And I think the opportunity of making something that is unique in terms of those use cases, like I mentioned like newsrooms, was clear. Like it was clear that there was some other solution, that could be built that would fit these needs better while if it was a SaaS, there are plenty of those out there.

And I don't necessarily think that they're well differentiated. A lot of them all use OpenStreetMap data. And it seems like they mainly compete on price. It's like who can build the best three column pricing model. And then once you do that, you need to build like billing and metrics and authentication and like those problems don't really interest me.

So I think, although I acknowledge sort of the indie hacker ethos now is to build a SaaS product with a monthly subscription, that's something I very much chose not to do, even though it is for sure like the best way to build a business.

[00:14:29] **Jeremy:** Yeah, I mean, I think a lot of people can appreciate that perspective because it's, it's almost like we have SaaS overload, right? Where you have so many little bills for your project where you're like, another $5 a month, another $10 a month, or if you're a business, right? Those, you add a bunch of zeros and at some point it's just how many of these are we gonna stack on here?

[00:14:53] **Brandon:** Yeah. And honestly. So I really think like as programmers, we're not really like great at choosing how to spend money like a $10 SaaS. That's like nothing. You know? So I can go to Starbucks and I can buy a pumpkin spice latte, and that's like $10 basically now, right? And it's like I'm able to make that consumer choice in like an instant just to spend money on that.

But then if you're like, oh, like spend $10 on a SaaS that somebody put a lot of work into, then you're like, oh, that's too expensive. I could just do it myself. So I'm someone that also subscribes to a lot of SaaS products. and I think for a lot of things it's a great fit.


## Many open source SaaS projects are not easy to self host

[00:15:37] **Brandon:** But there's always this tension between an open source project that you might be able to run yourself and a SaaS. And I think a lot of projects are at different parts of the spectrum. But for Protomaps, it's very much like I'm trying to move maps to being it is something that is so easy to run yourself that anyone can do it.

[00:16:00] **Jeremy:** Yeah, and I think you can really see it with, there's a few SaaS projects that are successful and they're open source, but then you go to look at the self-hosting instructions and it's either really difficult to find and you find it, and then the instructions maybe don't work, or it's really complicated.

So I think doing the opposite with Protomaps. As a user, I'm sure we're all appreciative, but I wonder in terms of trying to make money, if that's difficult.

[00:16:30] **Brandon:** No, for sure. It is not like a good way to make money because I think like the ideal situation for an open source project that is open that wants to make money is the product itself is fundamentally complicated to where people are scared to run it themselves. Like a good example I can think of is like Supabase.

Supabase is sort of like a platform as a service based on Postgres. And if you wanted to run it yourself, well you need to run Postgres and you need to handle backups and authentication and logging, and that stuff all needs to work and be production ready. So I think a lot of people, like they don't trust themselves to run database backups correctly.

'cause if you get it wrong once, then you're kind of screwed. So I think that fundamental aspect of the product, like a database is something that is very, very ripe for being a SaaS while still being open source because it's fundamentally hard to run. Another one I can think of is like tailscale, which is, like a VPN that works end to end.

That's something where, you know, it has this networking complexity where a lot of developers don't wanna deal with that. So they'd happily pay, for tailscale as a service. There is a lot of products or open source projects that eventually end up just changing to becoming like a hosted service.


## Businesses going from open source to closed or restricted licenses

[00:17:58] **Brandon:** But then in that situation why would they keep it open source, right? Like, if it's easy to run yourself well, doesn't that sort of cannibalize their business model? And I think that's really the tension overall in these open source companies. So you saw it happen to things like Elasticsearch to things like Terraform where they eventually change the license to one that makes it difficult for other companies to compete with them.

[00:18:23] **Jeremy:** Yeah, I mean there's been a number of cases like that. I mean, specifically within the mapping community, one I can think of was Mapbox's. They have Mapbox gl. Which was a JavaScript client to visualize maps and they moved from, I forget which license they picked, but they moved to a much more restrictive license.

I wonder what your thoughts are on something that releases as open source, but then becomes something maybe a little more muddy.

[00:18:55] **Brandon:** Yeah, I think it totally makes sense because if you look at their business and their funding, it seems like for Mapbox, I haven't used it in a while, but my understanding is like a lot of their business now is car companies and doing in dash navigation. And that is probably way better of a business than trying to serve like people making maps of toilets.

And I think sort of the beauty of it is that, so Mapbox, the story is they had a JavaScript renderer called Mapbox GL JS. And they changed that to a source available license a couple years ago. And there's a fork of it that I'm sort of involved in called MapLibre GL. But I think the cool part is Mapbox paid employees for years, probably millions of dollars in total to work on this thing and just gave it away for free.

Right? So everyone can benefit from that work they did. It's not like that code went away, like once they changed the license. Well, the old version has been forked. It's going its own way now. It's quite different than the new version of Mapbox, but I think it's extremely generous that they're able to pay people for years, you know, like a competitive salary and just give that away.

[00:20:10] **Jeremy:** Yeah, so we should maybe look at it as, it was a gift while it was open source, and they've given it to the community and they're on continuing on their own path, but at least the community running Map Libre, they can run with it, right? It's not like it just disappeared.

[00:20:29] **Brandon:** Yeah, exactly. And that is something that I use for Protomaps quite extensively. Like it's the primary way of showing maps on the web and I've been trying to like work on some enhancements to it to have like better internationalization for if you are in like South Asia like not show languages correctly.

So I think it is being taken in a new direction. And I think like sort of the combination of Protomaps and MapLibre, it addresses a lot of use cases, like I mentioned earlier with like these like hobby projects, indie projects that are almost certainly not interesting to someone like Mapbox or Google as a business. But I'm happy to support as a small business myself.


## Financially supporting open source work (GitHub sponsors, closed source, contracts)

[00:21:12] **Jeremy:** In my previous interview with Tom, one of the main things he mentioned was that creating a mapping business is incredibly difficult, and he said he probably wouldn't do it again. So in your case, you're building Protomaps, which you've admitted is easy to self-host. So there's not a whole lot of incentive for people to pay you. How is that working out for you? How are you supporting yourself?

[00:21:40] **Brandon:** There's a couple of strategies that I've tried and oftentimes failed at. Just to go down the list, so I do have GitHub sponsors so I do have a hosted version of Protomaps you can use if you don't want to bother copying a big file around. But the way I do the billing for that is through GitHub sponsors.

If you wanted to use this thing I provide, then just be a sponsor. And that definitely pays for itself, like the cost of running it. And that's great. GitHub sponsors is so easy to set up. It just removes you having to deal with Stripe or something. 'cause a lot of people, their credit card information is already in GitHub.

GitHub sponsors I think is awesome if you want to like cover costs for a project. But I think very few people are able to make that work. A thing that's like a salary job level. It's sort of like Twitch streaming, you know, there's a handful of people that are full-time streamers and then you look down the list on Twitch and it's like a lot of people that have like 10 viewers.

But some of the other things I've tried, I actually started out, publishing the base map as a closed source thing, where I would sell sort of like a data package instead of being a SaaS, I'd be like, here's a one-time download, of the premium data and you can buy it. And quite a few people bought it I just priced it at like $500 for this thing.

And I thought that was an interesting experiment. The main reason it's interesting is because the people that it attracts to you in terms of like, they're curious about your products, are all people willing to pay money. While if you start out everything being open source, then the people that are gonna be try to do it are only the people that want to get something for free.

So what I discovered is actually like once you transition that thing from closed source to open source, a lot of the people that used to pay you money will still keep paying you money because like, it wasn't necessarily that that closed source thing was why they wanted to pay. They just valued that thought you've put into it your expertise, for example.

So I think that is one thing, that I tried at the beginning was just start out, closed source proprietary, then make it open source. That's interesting to people. Like if you release something as open source, if you go the other way, like people are really mad if you start out with something open source and then later on you're like, oh, it's some other license.

Then people are like that's so rotten. But I think doing it the other way, I think is quite valuable in terms of being able to find an audience.

[00:24:29] **Jeremy:** And when you said it was closed source and paid to open source, do you still sell those map exports?

[00:24:39] **Brandon:** I don't right now. It's something that I might do in the future, you know, like have small customizations of the data that are available, uh, for a fee. still like the core OpenStreetMap based map that's like a hundred gigs you can just download. And that'll always just be like a free download just because that's already out there.

All the source code to build it is open source. So even if I said, oh, you have to pay for it, then someone else can just do it right? So there's no real reason like to make that like some sort of like paywall thing. But I think like overall if the project is gonna survive in the long term it's important that I'd ideally like to be able to like grow like a team like have a small group of people that can dedicate the time to growing the project in the long term. But I'm still like trying to figure that out right now.

[00:25:34] **Jeremy:** And when you mentioned that when you went from closed to open and people were still paying you, you don't sell a product anymore. What were they paying for?

[00:25:45] **Brandon:** So I have some contracts with companies basically, like if they need a feature or they need a customization in this way then I am very open to those. And I sort of set it up to make it clear from the beginning that this is not just a free thing on GitHub, this is something that you could pay for if you need help with it, if you need support, if you wanted it.

I'm also a little cagey about the word support because I think like it sounds a little bit too wishy-washy. Pretty much like if you need access to the developers of an open source project, I think that's something that businesses are willing to pay for. And I think like making that clear to potential users is a challenge.

But I think that is one way that you might be able to make like a living out of open source.

[00:26:35] **Jeremy:** And I think you said you'd been working on it for about five years. Has that mostly been full time?

[00:26:42] **Brandon:** It's been on and off. it's sort of my pandemic era project. But I've spent a lot of time, most of my time working on the open source project at this point. So I have done some things that were more just like I'm doing a customization or like a private deployment for some client. But that's been a minority of the time. Yeah.

[00:27:03] **Jeremy:** It's still impressive to have an open source project that is easy to self-host and yet is still able to support you working on it full time. I think a lot of people might make the assumption that there's nothing to sell if something is, is easy to use.

But this sort of sounds like a counterpoint to that.

[00:27:25] **Brandon:** I think I'd like it to be. So when you come back to the point of like, it being easy to self-host. Well, so again, like I think about it as like a primitive of the web. Like for example, if you wanted to start a business today as like hosted CSS files, you know, like where you upload your CSS and then you get developers to pay you a monthly subscription for how many times they fetched a CSS file.

Well, I think most developers would be like, that's stupid because it's just an open specification, you just upload a static file. And really my goal is to make Protomaps the same way where it's obvious that there's not really some sort of lock-in or some sort of secret sauce in the server that does this thing.


## How PMTiles works and building a primitive of the web

[00:28:16] **Brandon:** If you look at video for example, like a lot of the tech for how Protomaps and PMTiles works is based on parts of the HTTP spec that were made for video. And 20 years ago, if you wanted to host a video on the web, you had to have like a real player license or flash. So you had to go license some server software from real media or from macromedia so you could stream video to a browser plugin.

But now in HTML you can just embed a video file. And no one's like, oh well I need to go pay for my video serving license. I mean, there is such a thing, like YouTube doesn't really use that for DRM reasons, but people just have the assumption that video is like a primitive on the web. So if we're able to make maps sort of that same way like a primitive on the web then there isn't really some obvious business or licensing model behind how that works. Just because it's a thing and it helps a lot of people do their jobs and people are happy using it. So why bother?

[00:29:26] **Jeremy:** You mentioned that it a tech that was used for streaming video. What tech specifically is it?

[00:29:34] **Brandon:** So it is byte range serving. So when you open a video file on the web, So let's say it's like a 100 megabyte video. You don't have to download the entire video before it starts playing. It streams parts out of the file based on like what frames... I mean, it's based on the frames in the video. So it can start streaming immediately because it's organized in a way to where the first few frames are at the beginning.

And what PMTiles really is, is it's just like a video but in space instead of time. So it's organized in a way where these zoomed out views are at the beginning and the most zoomed in views are at the end. So when you're like panning or zooming in the map all you're really doing is fetching byte ranges out of that file the same way as a video.

But it's organized in, this tiled way on a space filling curve. IIt's a little bit complicated how it works internally and I think it's kind of cool but that's sort of an like an implementation detail.

[00:30:35] **Jeremy:** And to the person deploying it, it just looks like a single file.

[00:30:40] **Brandon:** Exactly in the same way like an mp3 audio file is or like a JSON file is.

[00:30:47] **Jeremy:** So with a video, I can sort of see how as someone seeks through the video, they start at the beginning and then they go to the middle if they wanna see the middle. For a map, as somebody scrolls around the map, are you seeking all over the file or is the way it's structured have a little less chaos? 

[00:31:09] **Brandon:** It's structured. And that's kind of the main technical challenge behind building PMTiles is you have to be sort of clever so you're not spraying the reads everywhere. So it uses something called a hilbert curve, which is a mathematical concept of a space filling curve. Where it's one continuous curve that essentially lets you break 2D space into 1D space.

So if you've seen some maps of IP space, it uses this crazy looking curve that hits all the points in one continuous line. And that's the same concept behind PMTiles is if you're looking at one part of the world, you're sort of guaranteed that all of those parts you're looking at are quite close to each other and the data you have to transfer is quite minimal, compared to if you just had it at random.

[00:32:02] **Jeremy:** How big do the files get? If I have a PMTiles of the entire world, what kind of size am I looking at?

[00:32:10] **Brandon:** Right now, the default one I distribute is 128 gigabytes, so it's quite sizable, although you can slice parts out of it remotely. So if you just wanted. if you just wanted California or just wanted LA or just wanted only a couple of zoom levels, like from zero to 10 instead of zero to 15, there is a command line tool that's also called PMTiles that lets you do that.


## Issues with CDNs and range queries

[00:32:35] **Jeremy:** And when you're working with files of this size, I mean, let's say I am working with a CDN in front of my application. I'm not typically accustomed to hosting something that's that large and something that's where you're seeking all over the file. is that, ever an issue or is that something that's just taken care of by the browser and, and taken care of by, by the hosts?

[00:32:58] **Brandon:** That is an issue actually, so a lot of CDNs don't deal with it correctly. And my recommendation is there is a kind of proxy server or like a serverless proxy thing that I wrote. That runs on like cloudflare workers or on Docker that lets you proxy those range requests into a normal URL and then that is like a hundred percent CDN compatible.

So I would say like a lot of the big commercial installations of this thing, they use that because it makes more practical sense. It's also faster. But the idea is that this solution sort of scales up and scales down. If you wanted to host just your city in like a 10 megabyte file, well you can just put that into GitHub pages and you don't have to worry about it.

If you want to have a global map for your website that serves a ton of traffic then you probably want a little bit more sophisticated of a solution. It still does not require you to run a Linux server, but it might require (you) to use like Lambda or Lambda in conjunction with like a CDN.


[00:34:09] **Jeremy:** Yeah. And that sort of ties into what you were saying at the beginning where if you can host on something like CloudFlare Workers or Lambda, there's less time you have to spend keeping these things running.

[00:34:26] **Brandon:** Yeah, exactly. and I think also the Lambda or CloudFlare workers solution is not perfect. It's not as perfect as S3 or as just static files, but in my experience, it still is better at building something that lasts on the time span of years than being like I have a server that is on this Ubuntu version and in four years there's all these like security patches that are not being applied.

So it's still sort of serverless, although not totally vendor neutral like S3.


## Customizing the map



[00:35:03] **Jeremy:** We've mostly been talking about how you host the map itself, but for someone who's not familiar with these kind of tools, how would they be customizing the map? 

[00:35:15] **Brandon:** For customizing the map there is front end style customization and there's also data customization. So for the front end if you wanted to change the water from the shade of blue to another shade of blue there is a TypeScript API where you can customize it almost like a text editor color scheme.

So if you're able to name a bunch of colors, well you can customize the map in that way you can change the fonts. And that's all done using MapLibre GL using a TypeScript API on top of that for customizing the data. 

So all the pipeline to generate this data from OpenStreetMap is open source. There is a Java program using a library called PlanetTiler which is awesome, which is this super fast multi-core way of building map tiles. And right now there isn't really great hooks to customize what data goes into that. But that's something that I do wanna work on. And finally, because the data comes from OpenStreetMap if you notice data that's missing or you wanted to correct data in OSM then you can go into osm.org.

You can get involved in contributing the data to OSM and the Protomaps build is daily. So if you make a change, then within 24 hours you should see the new base map. Have that change. And of course for OSM your improvements would go into every OSM based project that is ingesting that data. So it's not a protomap specific thing. It's like this big shared data source, almost like Wikipedia. 


## OpenStreetMap is a dataset and not a map

[00:37:01] **Jeremy:** I think you were involved with OpenStreetMap to some extent. Can you speak a little bit to that for people who aren't familiar, what OpenStreetMap is?

[00:37:11] **Brandon:** Right. So I've been using OSM as sort of like a tools developer for over a decade now. And one of the number one questions I get from developers about what is Protomaps is why wouldn't I just use OpenStreetMap? What's the distinction between Protomaps and OpenStreetMap? And it's sort of like this funny thing because even though OSM has map in the name it's not really a map in that you can't... In that it's mostly a data set and not a map. 

It does have a map that you can see that you can pan around to when you go to the website but the way that thing they show you on the website is built is not really that easily reproducible. It involves a lot of c++ software you have to run.

But OpenStreetMap itself, the heart of it is almost like a big XML file that has all the data in the map and global. And it has tagged features for example. So you can go in and edit that. It has a web front end to change the data. It does not directly translate into making a map actually.


## Protomaps decides what shows at each zoom level

[00:38:24] **Brandon:** So a lot of the pipeline, that Java program I mentioned for building this basemap for protomaps is doing things like you have to choose what data you show when you zoom out. You can't show all the data. For example when you're zoomed out and you're looking at all of a state like Colorado you don't see all the Chipotle when you're zoomed all the way out. That'd be weird, right? 

So you have to make some sort of decision in logic that says this data only shows up at this zoom level. And that's really what is the challenge in optimizing the size of that for the Protomaps map project.

[00:39:03] **Jeremy:** Oh, so those decisions of what to show at different Zoom levels those are decisions made by you when you're creating the PMTiles file with Protomaps.

[00:39:14] **Brandon:** Exactly. It's part of the base maps build pipeline. and those are honestly very subjective decisions. Who really decides when you're zoomed out should this hospital show up or should this museum show up nowadays in Google, I think it shows you ads. Like if someone pays for their car repair shop to show up when you're zoomed out like that that gets surfaced.

But because there is no advertising auction in Protomaps that doesn't happen obviously. So we have to sort of make some reasonable choice. A lot of that right now in Protomaps actually comes from another open source project called Mapzen. So Mapzen was a company that went outta business a couple years ago.

They did a lot of this work in designing which data shows up at which Zoom level and open sourced it. And then when they shut down, they transferred that code into the Linux Foundation. So it's this totally open source project, that like, again, sort of like Mapbox gl has this awesome legacy in that this company funded it for years for smart people to work on it and now it's just like a free thing you can use. So the logic in Protomaps is really based on mapzen.

[00:40:33] **Jeremy:** And so the visualization of all this... I think I understand what you mean when people say oh, why not use OpenStreetMaps because it's not really clear it's hard to tell is this the tool that's visualizing the data? Is it the data itself? So in the case of using Protomaps, it sounds like Protomaps itself has all of the data from OpenStreetMap and then it has made all the decisions for you in terms of what to show at different Zoom levels and what things to have on the map at all. And then finally, you have to have a separate, UI layer and in this case, it sounds like the one that you recommend is the Map Libre library.

[00:41:18] **Brandon:** Yeah, that's exactly right. For Protomaps, it has a portion or a subset of OSM data. It doesn't have all of it just because there's too much, like there's data in there. people have mapped out different bushes and I don't include that in Protomaps if you wanted to go in and edit like the Java code to add that you can.

But really what Protomaps is positioned at is sort of a solution for developers that want to use OSM data to make a map on their app or their website. because OpenStreetMap itself is mostly a data set, it does not really go all the way to having an end-to-end solution.


## Financials and the idea of a project being complete

[00:41:59] **Jeremy:** So I think it's great that somebody who wants to make a map, they have these tools available, whether it's from what was originally built by Mapbox, what's built by Open StreetMap now, the work you're doing with Protomaps. But I wonder one of the things that I talked about with Tom was he was saying  he was trying to build this mapping business and based on the financials of what was coming in he was stressed, right?

He was struggling a bit. And I wonder for you, you've been working on this open source project for five years. Do you have similar stressors or do you feel like I could keep going how things are now and I feel comfortable?

[00:42:46] **Brandon:** So I wouldn't say I'm a hundred percent in one bucket or the other. I'm still seeing it play out. One thing, that I really respect in a lot of open source projects, which I'm not saying I'm gonna do for Protomaps is the idea that a project is like finished. I think that is amazing.

If a software project can just be done it's sort of like a painting or a novel once you write, finish the last page, have it seen by the editor. I send it off to the press is you're done with a book. And I think one of the pains of software is so few of us can actually do that.

And I don't know obviously people will say oh the map is never finished. That's more true of OSM, but I think like for Protomaps. One thing I'm thinking about is how to limit the scope to something that's quite narrow to where we could be feature complete on the core things in the near term timeframe.

That means that it does not address a lot of things that people want. Like search, like if you go to Google Maps and you search for a restaurant, you will get some hits. that's like a geocoding issue. And I've already decided that's totally outta scope for Protomaps. So, in terms of trying to think about the future of this, I'm mostly looking for ways to cut scope if possible.

There are some things like better tooling around being able to work with PMTiles that are on the roadmap. but for me, I am still enjoying working on the project. It's definitely growing. So I can see on NPM downloads I can see the growth curve of people using it and that's really cool.

So I like hearing about when people are using it for cool projects. So it seems to still be going okay for now.

[00:44:44] **Jeremy:** Yeah, that's an interesting perspective about how you were talking about projects being done. Because I think when people look at GitHub projects and they go like, oh, the last commit was X months ago. They go oh well this is dead right? But maybe that's the wrong framing. Maybe you can get a project to a point where it's like, oh, it's because it doesn't need to be updated.

[00:45:07] **Brandon:** Exactly, yeah. Like I used to do a lot of c++ programming and the best part is when you see some LAPACK matrix math library from like 1995 that still works perfectly in c++ and you're like, this is awesome. This is the one I have to use. But if you're like trying to use some like React component library and it hasn't been updated in like a year, you're like, oh, that's a problem.

So again, I think there's some middle ground between those that I'm trying to find. I do like for Protomaps, it's quite dependency light in terms of the number of hard dependencies I have in software. but I do still feel like there is a lot of work to be done in terms of project scope that needs to have stuff added.


## You mostly only hear about problems instead of people's wins

[00:45:54] **Jeremy:** Having run it for this long. Do you have any thoughts on running an open source project in general? On dealing with issues or managing what to work on things like that?

[00:46:07] **Brandon:** Yeah. So I have a lot. I think one thing people point out a lot is that especially because I don't have a direct relationship with a lot of the people using it a lot of times I don't even know that they're using it. Someone sent me a message saying hey, have you seen flickr.com, like the photo site?

And I'm like, no. And I went to flickr.com/map and it has Protomaps for it. And I'm like, I had no idea. But that's cool, if they're able to use Protomaps for this giant photo sharing site that's awesome. But that also means I don't really hear about when people use it successfully because you just don't know, I guess they, NPM installed it and it works perfectly and you never hear about it.

You only hear about people's negative experiences. You only hear about people that come and open GitHub issues saying this is totally broken, and why doesn't this thing exist? And I'm like, well, it's because there's an infinite amount of things that I want to do, but I have a finite amount of time and I just haven't gone into that yet.

And that's honestly a lot of the things and people are like when is this thing gonna be done? So that's, that's honestly part of why I don't have a public roadmap because I want to avoid that sort of bickering about it. I would say that's one of my biggest frustrations with running an open source project is how it's self-selected to only hear the negative experiences with it.


## Be careful what PRs you accept

[00:47:32] **Brandon:** 'cause you don't hear about those times where it works. I'd say another thing is it's changed my perspective on contributing to open source because I think when I was younger or before I had become a maintainer I would open a pull request on a project unprompted that has a hundred lines and I'd be like, Hey, just merge this thing.

But I didn't realize when I was younger well if I just merge it and I disappear, then the maintainer is stuck with what I did forever. You know if I add some feature then that person that maintains the project has to do that indefinitely. And I think that's very asymmetrical and it's changed my perspective a lot on accepting open source contributions.

I wanna have it be open to anyone to contribute. But there is some amount of back and forth where it's almost like the default answer for should I accept a PR is no by default because you're the one maintaining it. And do you understand the shape of that solution completely to where you're going to support it for years because the person that's contributing it is not bound to those same obligations that you are.

And I think that's also one of the things where I have a lot of trepidation around open source is I used to think of it as a lot more bazaar-like in terms of anyone can just throw their thing in. But then that creates a lot of problems for the people who are expected out of social obligation to continue this thing indefinitely.

[00:49:23] **Jeremy:** Yeah, I can totally see why that causes burnout with a lot of open source maintainers, because you probably to some extent maybe even feel some guilt right? You're like, well, somebody took the time to make this. But then like you said you have to spend a lot of time trying to figure out is this something I wanna maintain long term? And one wrong move and it's like, well, it's in here now. 

[00:49:53] **Brandon:** Exactly. To me, I think that is a very common failure mode for open source projects is they're too liberal in the things they accept. And that's a lot of why I was talking about how that choice of what features show up on the map was inherited from the MapZen projects. If I didn't have that then somebody could come in and say hey, you know, I want to show power lines on the map.

And they open a PR for power lines and now everybody who's using Protomaps when they're like zoomed out they see power lines are like I didn't want that. So I think that's part of why a lot of open source projects eventually evolve into a plugin system is because there is this demand as the project grows for more and more features. But there is a limit in the maintainers. It's like the demand for features is exponential while the maintainer amount of time and effort is linear. 


## Plugin systems might reduce need for PRs

[00:50:56] **Brandon:** So maybe the solution to smash that exponential down to quadratic maybe is to add a plugin system.

But I think that is one of the biggest tensions that only became obvious to me after working on this for a couple of years.

[00:51:14] **Jeremy:** Is that something you're considering doing now?

[00:51:18] **Brandon:** Is the plugin system? Yeah. I think for the data customization, I eventually wanted to have some sort of programmatic API to where you could declare a config file that says I want ski routes. It totally makes sense. The power lines example is maybe a little bit obscure but for example like a skiing app and you want to be able to show ski slopes when you're zoomed out well you're not gonna be able to get that from Mapbox or from Google because they have a one size fits all map that's not specialized to skiing or to golfing or to outdoors.

But if you like, in theory, you could do this with Protomaps if you changed the Java code to show data at different zoom levels. And that is to me what makes the most sense for a plugin system and also makes the most product sense because it enables a lot of things you cannot do with the one size fits all map.

[00:52:20] **Jeremy:** It might also increase the complexity of the implementation though, right?

[00:52:25] **Brandon:** Yeah, exactly. So that's like. That's really where a lot of the terrifying thoughts come in, which is like once you create this like config file surface area, well what does that look like? Is that JSON? Is that TOML, is that some weird like everything eventually evolves into some scripting language right?

Where you have logic inside of your templates and I honestly do not really know what that looks like right now. That feels like something in the medium term roadmap.

[00:52:58] **Jeremy:** Yeah and then in terms of bug reports or issues, now it's not just your code it's this exponential combination of whatever people put into these config files.

[00:53:09] **Brandon:** Exactly. Yeah. so again, like I really respect the projects that have done this well or that have done plugins well. I'm trying to think of some, I think obsidian has plugins, for example. And that seems to be one of the few solutions to try and satisfy the infinite desire for features with the limited amount of maintainer time.


## Time split between code vs triage vs talking to users

[00:53:36] **Jeremy:** How would you say your time is split between working on the code versus issue and PR triage?

[00:53:43] **Brandon:** Oh, it varies really. I think working on the code is like a minority of it. I think something that I actually enjoy is talking to people, talking to users, getting feedback on it. I go to quite a few conferences to talk to developers or people that are interested and figure out how to refine the message, how to make it clearer to people, like what this is for.

And I would say maybe a plurality of my time is spent dealing with non-technical things that are neither code or GitHub issues. One thing I've been trying to do recently is talk to people that are not really in the mapping space. For example, people that work for newspapers like a lot of them are front end developers and if you ask them to run a Linux server they're like I have no idea.

But that really is like one of the best target audiences for Protomaps. So I'd say a lot of the reality of running an open source project is a lot like a business is it has all the same challenges as a business in terms of you have to figure out what is the thing you're offering.

You have to deal with people using it. You have to deal with feedback, you have to deal with managing emails and stuff. I don't think the payoff is anywhere near running a business or a startup that's backed by VC money is but it's definitely not the case that if you just want to code, you should start an open source project because I think a lot of the work for an opensource project has nothing to do with just writing the code.

It is in my opinion as someone having done a VC backed business before, it is a lot more similar to running, a tech company than just putting some code on GitHub.


## Running a startup vs open source project

[00:55:43] **Jeremy:** Well, since you've done both at a high level what did you like about running the company versus maintaining the open source project?

[00:55:52] **Brandon:** So I have done some venture capital accelerator programs before and I think there is an element of hype and energy that you get from that that is self perpetuating.

Your co-founder is gungho on like, yeah, we're gonna do this thing. And your investors are like, you guys are geniuses. You guys are gonna make a killing doing this thing. And the way it's framed is sort of obvious to everyone that it's like there's a much more traditional set of motivations behind that, that people understand while it's definitely not the case for running an open source project. 

Sometimes you just wake up and you're like what the hell is this thing for, it is this thing you spend a lot of time on. You don't even know who's using it. The people that use it and make a bunch of money off of it they know nothing about it. And you know, it's just like cool. 

And then you only hear from people that are complaining about it. And I think like that's honestly discouraging compared to the more clear energy and clearer motivation and vision behind how most people think about a company. But what I like about the open source project is just the lack of those constraints you know?

Where you have a mandate that you need to have this many customers that are paying by this amount of time. There's that sort of pressure on delivering a business result instead of just making something that you're proud of that's simple to use and has like an elegant design. I think that's really a difference in motivation as well.


## Having control

[00:57:50] **Jeremy:** Do you feel like you have more control? Like you mentioned how you've decided I'm not gonna make a public roadmap. I'm the sole developer. I get to decide what goes in. What doesn't. Do you feel like you have more control in your current position than you did running the startup?

[00:58:10] **Brandon:** Definitely for sure. Like that agency is what I value the most. It is possible to go too far. Like, so I'm very wary of the BDFL title, which I think is how a lot of open source projects succeed. But I think there is some element of for a project to succeed there has to be somebody that makes those decisions.

Sometimes those decisions will be wrong and then hopefully they can be rectified. But I think going back to what I was talking about with scope, I think the overall vision and the scope of the project is something that I am very opinionated about in that it should do these things. It shouldn't do these things. It should be easy to use for this audience. Is it gonna be appealing to this other audience? I don't know. 

And I think that is really one of the most important parts of that leadership role, is having the power to decide we're doing this, we're not doing this. I would hope other developers would be able to get on board if they're able to make good use of the project, if they use it for their company, if they use it for their business, if they just think the project is cool. 

So there are other contributors at this point and I want to get more involved. But I think being able to make those decisions to what I believe is going to be the best project is something that is very special about open source, that isn't necessarily true about running like a SaaS business.

[00:59:50] **Jeremy:** I think that's a good spot to end it on, so if people want to learn more about Protomaps or they wanna see what you're up to, where should they head?

[01:00:00] **Brandon:** So you can go to Protomaps.com, GitHub, or you can find me or Protomaps on bluesky or Mastodon.

[01:00:09] **Jeremy:** All right, Brandon, thank you so much for chatting today.

[01:00:12] **Brandon:** Great. Thank you very much.

