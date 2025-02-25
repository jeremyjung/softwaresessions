+++
title = "Prefetcher on Building PinkSea on the AT Protocol"

description = "Early internet aesthetics and decentralized oekaki"

[extra]
episode_url = "https://pinecast.com/listen/77c830bc-af3d-4337-a390-7e21c816fc72.mp3"
social_title = "Prefetcher on building PinkSea using ATProto"
social_description = "Early internet aesthetics and decentralized oekaki"
+++

[Kacper "prefetcher" Staroń](https://bsky.app/profile/prefetcher.miku.place) created the [PinkSea](https://pinksea.art/) oekaki BBS on top of the AT Protocol. He also made the online multiplayer game [MicroWorks](https://store.steampowered.com/app/1233410/MicroWorks/) with [Noam "noam 2000" Rubin](https://bsky.app/profile/noam2000.miku.place). He's currently studying Computer Science at the Lublin University of Technology.

We discuss the appeal of oekaki BBSs, why and how PinkSea was created, web design of the early 2000s, flash animations, and building an application on top of the AT Protocol.


## Prefetcher
- [Bluesky](https://bsky.app/profile/prefetcher.miku.place)
- [Github](https://www.github.com/purifetchi)
- [Personal site](https://nanoshinono.me/)
- [Microworks](https://store.steampowered.com/app/1233410/MicroWorks/)

## PinkSea and Harbor
- [PinkSea](https://pinksea.art)
- [PinkSea Bluesky Account](https://bsky.app/profile/pinksea.art)
- [PinkSea repository](https://github.com/shinolabs/PinkSea)
- [Harbor image proxy repository](https://github.com/shinolabs/harbor)
- [Harbor post from bnewbold.net](https://bsky.app/profile/bnewbold.net/post/3lgo3ri5m222e)
- [imgproxy](https://github.com/imgproxy/imgproxy) (Image proxy used by Bluesky)

## Early web design
- [Web Design Museum](https://www.webdesignmuseum.org/)
- [Pixel Art in Web Design](https://www.webdesignmuseum.org/exhibitions/pixel-art-in-web-design)
- [Kaliber10000](https://www.webdesignmuseum.org/gallery/kaliber10000-2003)
- [Eboy](https://www.webdesignmuseum.org/gallery/eboy-1999)
- [Assembler](https://www.webdesignmuseum.org/gallery/assembler-org-2001)
- [2advanced](https://www.webdesignmuseum.org/gallery/2advanced-studios-v1-2000)
- [epuls.pl](https://web.archive.org/web/20060613060019/http://www.epuls.pl/frameset.php?/) (Polish social networking site)
- [Wipeout 3 aesthetic](https://typeface.agency/on-how-the-designers-republic-sculpted-childhoods/)
- [Restorativland](https://geocities.restorativland.org) (Geocities archive)

## Flash sites and animations
- [My Flash Archive](https://bsky.app/profile/flash.nanoshinono.me) (Run by prefetcher)
- [dagobah](https://dagobah.net)
- [Z0r](z0r.de)
- [Juicy Panic - Otarie](https://flashmuseum.org/otarie/)
- [IOSYS - Marisa Stole the Precious Thing](https://archive.org/details/precious_thing)

## Geocities style web hosts
- [Neocities](https://neocities.org)
- [Nekoweb](https://nekoweb.org/)

## AT Protocol / Bluesky
- [PDS](https://atproto.com/specs/account)
- [Relay](https://atproto.com/guides/glossary#relay)
- [AppViews](https://atproto.com/guides/glossary#app-view)
- [PLC directory](https://web.plc.directory)
- [Decentralized Identifier](https://atproto.com/specs/did)
- [lexicon](https://atproto.com/guides/lexicon)
- [Jetstream](https://docs.bsky.app/blog/jetstream)
- [XRPC](https://atproto.com/specs/xrpc)
- [ATProto scraping](https://github.com/mary-ext/atproto-scraping) (List of custom PDS and did:web)

## Tools to view PDS data
- [PDSls](https://pdsls.dev)
- [atp.tools](https://atp.tools)
- [ATProto browser](https://atproto-browser.vercel.app)

## Posters mentioned
- [vertigris](https://bsky.app/profile/verti.blue) (Artist that promoted PinkSea)
- [Mary](https://bsky.app/profile/did:plc:ia76kvnndjutgedggx2ibrem) (AT Protocol enthusiast)
- [Brian Newbold](https://bsky.app/profile/bnewbold.net) (Bluesky employee)

## Oekaki drawing applets
- [Tegaki](https://github.com/desuwa/tegaki)
- [chickenpaint](https://github.com/thenickdude/chickenpaint)

## Group drawing canvas
- [Drawpile](drawpile.net)
- [Aggie](aggie.io)

## Other links
- [Bringing Geocities back with Kyle Drake](https://www.softwaresessions.com/episodes/bringing-geocities-back-with-kyle-drake/)
- [firesky.tv](firesky.tv) (View all bluesky posts)
- [ATFile](https://github.com/ziodotsh/atfile) (Use PDS as a file store)
- [PinkSky](https://pinksky.app) (Instagram clone)
- [front page](https://frontpage.fyi) (Hacker news clone)
- [Smoke Signal](https://docs.smokesignal.events) (Meetup clone)

--

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

## Intro

[00:00:00] **Jeremy:** Today I am talking to Kacper Staroń.  He created an oekaki BBS called PinkSea built on top of the AT protocol, and he's currently studying computer science at the Lublin University  of Technology.

We are gonna discuss the appeal of oekaki BBS, the web design of the early 2000s, flash animations, and building an application on top of the AT protocol. 

Kacper, thanks for talking with me today.

[00:00:16] **Prefetcher:** Hello. Thank you for having me on. I'm Kacper Staroń also probably you know me as Prefetcher online. And as Jeremy's mentioned, PinkSea is an oekaki drawing bulletin board. You log in with your Bluesky account and you can draw and post images. It's styled like a mid to late 2000s website to keep it in the spirit. 


## What's an oekaki BBS?

[00:00:43] **Jeremy:** For someone who isn't familiar with oekaki BBSs what is different about them as opposed to say, a photo sharing website?

[00:00:53] **Prefetcher:** The difference is that a photo sharing website you have the image already premade be it a photo or a drawing made in a separate application. And you basically log in and you upload that image. 

For example on Instagram or pixiv for artists even Flickr. But in the case of an oekaki BBS the thing that sets it apart is that oekaki BBSes already have the drawing tools built in. You cannot upload an already pre-made image with there being some caveats. Some different oekaki boards allow you to upload your already pre-made work.

But Pinksea restricts you to a tool called [Tegaki](https://github.com/desuwa/tegaki). Tegaki being a drawing applet that was built for one of the other BBSes and all of the drawing tools are inside of it. So you draw from within PinkSea and you upload it to the atmosphere. Every image that's on PinkSea is basically drawn right on it by the artists.

No one can technically upload any images from elsewhere.


## How PinkSea got started and grew

[00:01:56] **Jeremy:** You released this to the world. How did people find it and how many people are using it?

[00:02:02] **Prefetcher:** I'll actually begin with how I've made it 'cause it kind of ties into how PinkSea got semi-popular. One day I was just browsing through Bluesky somewhere in the late 2024s. I was really interested in the AT Protocol and while browsing, one of the artists that I follow [vertigris](https://bsky.app/profile/verti.blue) posted a post basically saying they'd really want to see something a drawing canvas like [Drawpile](drawpile.net) or [Aggie](aggie.io) on AT Protocol or something like an oekaki board. And considering that I was really looking forward to make something on the AT Protocol. I'm like, that sounds fun. 

I used to be a member of some oekaki boards. I don't draw well but it's an activity that I was thinking this sounds like a fun thing to do. I'm absolutely down for it. From like, the initial idea to what I'd say was the first time I was proud to let someone else use it. I think it was like two weeks. 

I was posting progress on Bluesky and people seemed eager to use it. That kept me motivated. And yeah. Right as I approached the finish I posted about it as a response to vertigris' posts and people seemed to like it.

I sent the early version to a bunch of artists. I basically just made a post calling for them. Got really positive feedback, things to fix, and I released it. And thanks to vertigris the post went semi-viral. 

The launch I got a lot of people which I would also tie to the fact that it was right after one of the user waves that came to Bluesky from other platforms. The website also seemed really popular in Japan. I remember going to sleep, waking up the next day, and I saw like a Japanese post about PinkSea and it had 2000 reposts and 3000 likes and I was just unable to believe it.

Within I think the first week we got like 1000 posts overall which to me is just insane. For a week straight I just kept looking at my phone and clicking, refresh, refresh, refresh, just seeing the new posts flow in. There was a bunch of like really insane talented artists just posting their works.

And I just could not believe it. PinkSea got I'd say fairly popular as an alternative AppView. People seem to really want oekaki boards back and I saw people going, oh look, it's like one of those 2000s oekaki boards! Oh, that's so cool! I haven't seen them in forever!


## The art stands out because it's human made

[00:04:58] **Prefetcher:** And it made me so happy every single time seeing it. It's been since November, like four months, give or take. And today alone we got five posts. That doesn't sound seem like a lot but given that every single post is hand drawn it's still insane.

People go on there and spend their time to produce their own original artworks. 

[00:05:26] **Jeremy:** This is especially relevant now when you have so much image generation stuff and they're making images that look polished but you're kind of like well... did you draw it?

[00:05:39] **Prefetcher:** Yeah. 

[00:05:40] **Jeremy:** And when you see people draw with these oekaki boards using the tools that are there I think there's something very human and very nostalgic about oh... This came from you. 

[00:05:53] **Prefetcher:** Honestly, yeah. To me seeing even beginner artists 'cause PinkSea has a lot of really, really talented and popular people (and) also beginner artists that do it as a hobby. Ones that haven't been drawing for a long time.

And no matter what you look at you just get like that homely feeling that, oh, that's someone that just spent time. That's someone that just wanted to draw for fun. And at least to me, with generative AI like images it really lacks that human aspect to it.

You generate an image, you go, oh, that's cool. And it just fades away. But in this case you see people that spent their time drawing it spent their own personal time. And no matter if it's a masterpiece or not it's still incredibly nice to see people just do it for fun. 

[00:06:54] **Jeremy:** Yeah. I think whether it's drawing or writing or anything now more than ever people wanna see something that you made yourself right? They wanna know that a human did this.

[00:07:09] **Prefetcher:** Yeah. absolutely.

[00:07:11] **Jeremy:** So it sounds like, in terms of getting the initial users and the ones that are there now, it really all came out of a single Bluesky posts that an existing artist (vertigris) noticed and boosted. And like you said, you were lucky enough to go viral and that carried you all the way to now and then it just keeps going from there,

[00:07:36] **Prefetcher:** Basically if not for vertigris PinkSea (would) just not exist because I honestly did not think about it. My initial idea on making something on ATProto and maybe in the future I'll do something like that would be a platform like [StumbleUpon](https://en.wikipedia.org/wiki/StumbleUpon) -- Something that would just allow you to go on a website, press a button, and it gets uploaded to your repo and your friends would be able to see oh -- you visited that website and there would be an AppView that would just recommend you sites based on those categories. 

I really liked that idea and I was dead set on making it but then like I noticed that post (from vertigris) and I'm like, no, that's better. I really wanna make that. And yeah. So right here I want to give a massive shout out to vertigris 'cause they've been incredibly nice to me. They've even contributed the German translation of PinkSea which was just insane to me.

And yeah, massive shout out to every single other artist that, Reposted it, liked it, used it because, it's all just snowballed from there and even recently I've had another wave of new users from the PinkSea account. So there are periods where it goes up and it like goes chill -- and then popular again.


## Old internet and flash

[00:08:59] **Jeremy:** Yeah. And so something that you mentioned is that some people who came across it they mentioned how it was nostalgic or it looked like the old oekaki BBSs from the early internet. And I noticed that that was something that you posted on your own website that you have an interest in that specifically.

I wonder what about that part of the internet interests you?

[00:09:26] **Prefetcher:** That is a really good question. Like, to me, even before PinkSea my interests lie in the early internet. I run on Twitter and also on Bluesky now an account called [My Flash Archive](https://bsky.app/profile/flash.nanoshinono.me), which was an archive of very random, like flash animations. And I still do that just not as much anymore 'cause I have a lot of other things to do.

I used to on Google just type in Flash and look through the oldest archived random folders just having flash videos. And I would just go over them save all of that or go on like the [dagobah](https://dagobah.net) or [Z0r](z0r.de) or swfchan. 'cause the early internet to me, it was really like more explorative.

'cause like now you have, people just concentrated in those big platforms like Twitter, Instagram, Facebook, whatever.

And back then at least to me you had more websites that you would just go on, you would find cool stuff. And the designs were like sometimes very minimal, aesthetically pleasing.

I'd named here one of my favorite sites, [Kaliber10000](https://www.webdesignmuseum.org/gallery/kaliber10000-2003) which had just fantastic web design. Like, I, I also spend a lot of time on like the [web design museum](https://www.webdesignmuseum.org/) just like looking at old web design and just in awe. 

My flash archive on Twitter at least got very popular. I kind of abandoned that account, but I think it was sitting at 12,000 followers if not more? And showed that people also yearn for that early internet vibe. And  to me it feels really warm. Really different from the internet nowadays.

Even with the death of flash you don't really have interactive experiences like it anymore. 'cause flash was supposed to be replaced by HTML5 and JavaScript and whatever but you don't really make interactive experiences  that just come packaged in a single file like flash.

You need a website and everything. In flash, it just had a single file. It could be shared on multiple sites and just experienced. That kind of propelled my interest. Plus I, I dunno, I just really like the old internet design aesthetics it really warms me (and really close..?)


## Flash loops

[00:12:01] **Jeremy:** The flash one specifically. Were they animations or games or was there a specific type of a flash project that spoke to you?

[00:12:15] **Prefetcher:** Something we call loops. Basically, it's sometimes animations. 'cause, surprisingly while I like flash games they weren't my main collection. What spoke to me more were loops. Basically someone would take a song, find a gif they liked, and they would just pair it together. Something like [YTMND](https://ytmnd.com) did. 

At least from loops I found some of my favorite musical artists, some of my favorite songs, a lot of interesting series, be it anime or TV or whatever. And you basically saw people make stuff about their favorite series and they would just share it online. I would go over those. 

For example, a good website as an example is [z0r.de](z0r.de), which is surprisingly still active and updated to this day. And you would see people making loops about members of that community or whatever they like. And you would for example see like 10 posts about the same thing.

So you would know someone decided to make 10 loops and just upload them at once. And yeah, to me, loops basically were like, I mean, they weren't always the highest quality or the most unique thing, but you would see someone liked something enough that they decided to make something about it.

And I always found that really cool. I would late at night just browse for loops and I'm like, oh, oh, this series, I remember it. I liked it (laughs)! 

But of course flash games as well. I mean, I used to play a lot when I was younger, but specifically loops, even animations and especially like when someone took like their time to animate something like really in depth.

My favorite example is, the [music video to a song by the band Juicy Panic called Otari](https://flashmuseum.org/otarie/). Someone liked that song enough that they made an entire flash animated music video, which was basically vectorized art of various series like Azumanga Daioh or Neon Genesis Evangelion as well, and other things. And it was so cool, at least to me, like a lot of these loops just basically have an intense, like immense feeling on me (laughs). I just really liked collecting them.

[00:14:38] **Jeremy:** And in that last example, it sounded more like it was a complete music video, not just a brief loop?

[00:14:45] **Prefetcher:** No, it was like a five minute long music video that someone else made.

[00:14:48] **Jeremy:** Five. Oh my gosh.

[00:14:49] **Prefetcher:** Yeah. You would really see people's creativity shine through on just making those weird things that not a lot of people have seen, but you look at it and it's like, wow.

## It's different than YouTube (Sharable single file, vectorized)

[00:15:01] **Jeremy:** It's interesting because you can technically do and see a lot of these things on, say, YouTube today, but I think it does feel a little different for some reason.

[00:15:16] **Prefetcher:** It really is. Of course I'm not denying on YouTube you see a lot of creative things and whatever. But first and foremost, the fact that Flash is scalable. You don't lose the quality. So be able to open, I don't know, any of the [IOSYS flash music videos for like their Touhou songs](https://archive.org/details/precious_thing) and the thing would just scale and you would see like in 4K and it's like, wow.

And yeah, the fact that on YouTube you have like a central place where you just like put something and it just stays there. Of course not counting reuploads, but with Flash you just had like this one animation file that you would just be able to share everywhere and I don't know, like the aspect of sharing, just like having those massive collections, you would see this flash right here on this website and on that website and also on this website.

And also seeing people's personal collections of flash videos and jrandomly online and you would also see this file and this file that you haven't seen it -- it really gives it, it's like explorative to me and that's what I like. You put in the effort to like go over all those websites and you just like find new and new cool stuff.

[00:16:32] **Jeremy:** Yeah, that's a good point too that I hadn't thought about. You can open these files and you have basically the primitives of how it was made and since, like you said, it's vector based, there's no, oh, can you please upload it in 1080 p or 4K? You can make it as big as you want.

[00:16:53] **Prefetcher:** Yeah.

## Web design differences, pixel art, non-responsive

[00:16:55] **Jeremy:** I think web design as well it was very distinct. Maybe because the tools just weren't there, so a lot of people were building things more from scratch rather than pulling a template or using a framework. A lot of people were just making the design theirs I think rather than putting words on a page and filling into some template.

[00:17:21] **Prefetcher:** Honestly, you raise a good point here that I did not think much about. 'cause like nowadays we have all of this tooling to make web design easier and you have design languages and whatnot. And you see people make really, in my opinion, still pretty websites, very usable websites on top of that.

But all of them have like the same vibes to them. All of them have like a unified design language and all of them look very similar. And you kind of lose that creativity that some people had. Of course, you still find pretty websites that were made from scratch. But you don't really get the same vibes that you did get like back then.

Like my favorite, for example, trend that used to be back on like the old internet is pixel art in web design. For example, [Kaliber10000](https://www.webdesignmuseum.org/gallery/kaliber10000-2003), or going off the top of my head, you had the [Eboy](https://www.webdesignmuseum.org/gallery/eboy-1999) or all the sites and then Poland, for example, ... (polish website) those websites use minimal graphics, like pixel graphics and everything to build really interesting looking websites.

They had their own very massive charm to them that, I don't know, I don't see a lot in more modern internet. And it's also because back then you were limited by screen size, so you didn't have to worry about someone being on a Mac with high DPI or on a 32x9 monitor like I am right now.

And just having to scale it up. So you would see people go more for images, like UI elements, images instead of just like building everything from scratch and CSS and whatnot. So, yeah, internet design had to accommodate the change. So we couldn't stay how it was forever 'cause technology changed. Design language has changed, but to me it's really lost its charm. Every single website was different, specific, the web design had like this weird form, at least on websites where it was like. I like to call it futuristic minimalism. They looked very modern and also very minimal and sort of dated.

And I dunno, I just really like it. I absolutely recommend checking, on the [web design museum](https://www.webdesignmuseum.org) fantastic website. I love them and the [pixel art in web design sub page](https://www.webdesignmuseum.org/exhibitions/pixel-art-in-web-design). Like those websites to me they just look fantastic.

[00:19:52] **Jeremy:** Yeah, and that's a good point you brought up about the screen sizes where now you have to make sure your website looks good on a phone, on a tablet, on any number of monitor sizes. Back then in the late 90s, early 2000s, I think most people were looking at these websites on their 4x3 small CRT monitors.

[00:20:20] **Prefetcher:** My favorite this website is best viewed with an 800 by 600 monitor. It's like ... what?

[00:20:28] **Jeremy:** Exactly. Even if you open your personal site now the design is very reminiscent of those times and it looks really cool but at the same time on a lot of monitors it's a small box in the middle of the monitor, so it's like --

[00:20:49] **Prefetcher:** I saw that issue, 'cause I was making it on a 1080p monitor and now I have a 32x9 monitor and it does not scale. I've been working on reworking that website, but, also on the topic of my website, I, I wanna shout out a website from the 2000s that still exists today.

'cause, my website was really inspired by a website called [Assembler](https://www.webdesignmuseum.org/gallery/assembler-org-2001). And Assembler, from what I could gather, was like a net art or like internet design collective. And the website still works to this day. You still had like, all of their projects, including the website that my website was based off of.

[00:21:28] **Jeremy:** Yeah, I mean there, there definitely was an aesthetic to that time. And it's probably, like you said, it's probably people seeing someone else's site in this case, what, what did you call it? Assem? Assembler?

[00:21:42] **Prefetcher:** Assembler.

[00:21:42] **Jeremy:** Yeah. You see someone else's website and then maybe you try to copy some of the design language or you look at the HTML and the CSS and I mean, really at the time, these websites weren't being made with a ton of JavaScript. There weren't the minifiers, so you really could view source and just pull whatever you wanted from there.

[00:22:06] **Prefetcher:** We also had those design studios, design agencies, notably [2advanced](https://www.webdesignmuseum.org/gallery/2advanced-studios-v1-2000) which check in now, their website still works, and their website is still in the same aesthetic as it was those 20 so years ago just dictating this futuristic design style that people really like.

'cause a lot of people nowadays also really like this old futurism minimalism for example a lot of people still love the [Wipeout 3 aesthetic](https://typeface.agency/on-how-the-designers-republic-sculpted-childhoods/) that was designed by one of my favorite studios overall [the designers republic](https://www.thedesignersrepublic.com). And yeah, it's just hard for me to explain, but it feels so soulful in a way.

[00:22:53] **Jeremy:** I think there are some trade offs. There's what we were talking about earlier with the flexibility of screen size. But there used to be with a lot of websites that used Flash, there used to be these very elaborate intros where the site is loading and there's these really neat animations.

But at the same time, it's sort of like, well, to actually get to the content, it's a bit much, but, everything is a trade off.

[00:23:25] **Prefetcher:** People had flash at their disposal and they just wanted to make, I have the tooling, I'm going to use all of the tooling and all of it.

[00:23:33] **Jeremy:** Yeah. Yeah. but yeah, I definitely get what you're saying where when I went to make my own website I made it very utilitarian and in some ways boring, right? I think we do kind of miss some of what we used to have.

[00:23:54] **Prefetcher:** I mean, in my opinion, utilitarian websites are just as fine. Like in some cases you don't really need a lot of flashy things and a lot of very modern very CPU intensive or whatever animations. Sometimes it is better to go on a website and just like, see, oh, there's the play button and that's it.

[00:24:17] **Jeremy:** Yeah. Well definitely the animations and the intro and all that stuff. I guess more in terms of the aesthetics or the designs. It's tricky because there's definitely people making very cool things now things that weren't even possible back then.

But it does feel like maybe the default is I'll pick this existing style sheet or this existing framework and just go with that.

[00:24:47] **Prefetcher:** A lot of modern websites just go for similar aesthetics, similar designs, which they aren't bad, but they are also very just bland. They, they are futuristic, they are very well designed. But when you see the same website. The same -- five websites have the same feel.

And this is especially, at least in my opinion, visible with websites built on top of NextJS or other frameworks. And it just feels corporate kind of dead. Like someone just makes a website that they want to sell something to you and not for fun.

[00:25:26] **Jeremy:** With landing pages especially it's like, wow, this looks the same as every other site, but I guess it must work.

[00:25:38] **Prefetcher:** It works. And it really cuts down on development time. You don't need to think much about it. You just already have a lot of well-established design rules that you just follow and you get a cohesive and responsive design system.


## Designing the PinkSea look and feel

[00:25:56] **Jeremy:** Let's talk about that in connection with PinkSea. What was your thinking when you designed how PinkSea would look and feel?

[00:26:06] **Prefetcher:** Honestly, at first I have to admit I looked at other websites. I looked at Bluesky first and foremost. I looked at, [front page](https://frontpage.fyi). I looked at [Smoke Signal](https://docs.smokesignal.events), and I thought that I might also build something that's modern and sleek and I sketched it out in an application and I showed it to some friends. 

One of them suggested I go for more like a 2000 aesthetic. I'm like, yeah, okay. I like that. As the website was built, I just saw more and more of how much I feel this could sit with others. Especially with the fact that it's an oekaki page an oekaki BBS and as you scroll through oekaki has a very distinct style to it.

And as you scroll and you see all of those, pixel shaded, all those dithered images, non anti-aliased pens and whatnot. It feels really really cohesive somehow with the design aesthetic. But of course, PinkSea in itself is a modern website. Like if you were to go to my [PinkSea repository](https://github.com/shinolabs/PinkSea). It's a modern website built up on top of [Vue3](https://vuejs.org), which talks via like [XRPC](https://atproto.com/specs/xrpc) API calls in real time and it's a single page app and whatever.

That's kind of the thing I merged the modern way of making sites with a very oldish design language. And I feel, in my opinion, it somehow just really works. And especially it sets PinkSea apart from the other websites. It gives it that really weird aesthetic.

You would go on it and you would not be like, oh, this is a modern site that connects with a modern protocol on top of a big decentralized network. This is just someone's weird BBS stuck in the 2000s that they forgot to shut down. (laughs) 

[00:28:00] **Jeremy:** Yeah. And I think that's a good reminder too, that when people are intentional about design, the tools we have now are so much better than what we used to have. There's nothing stopping us from making websites that when people go to them they really feel like something's different.

I know I did not just land on Instagram.

[00:28:27] **Prefetcher:** Yeah. And making PinkSea taught me that it's really easy to fall into that full string of thought that every site has to look modern. Because I was like, oh yeah, this is a modern protocol, a modern everything, and it has to look the part.

It has to look interesting to people and everything. And after talking with a bunch of friends and other people and just going, huh, that's maybe like the 2000s isn't as bad as I thought. And yeah, the website especially it's design people seem to just really like it.

Me too. I, I just absolutely love how PinkSea turned out it is really a reminder that you don't need modernness in web design always. And people really appreciate quirky looking pages, so to say, quirky like interesting. 

[00:29:23] **Jeremy:** I interviewed the, the creator of [Neocities](https://neocities.org) which is like kind of a modern version of [GeoCities](https://geocities.restorativland.org) and yeah, that's really what one of the aspects that I think makes things so interesting to people from that era is, is that it really felt like you're creating your own thing, and not just everything looks the same. The term I think he used is homesteading. You're taking care of your place and it can match your sensibilities, your style, your likes, rather than having to, like you said, try to force everything to be this, this sort of base modern, look.

## The old spirit of the internet is coming back

[00:30:08] **Prefetcher:** I mean Neocities and by extension also [Nekoweb](https://nekoweb.org/) are websites that I often when I don't have much to do -- I like just going through them because you see a bunch of people just make their own places. And you see that even in 2025 when we have those big social media sites.

You have platforms where you can get a ton of followers. You can get a ton of attention and everything. People to some extent still want that aspect of self-expression. They want to be able to make something that's uniquely theirs and you see people just make just really amazing websites build insane things on those old Geocities-like platforms using nothing but a code editor.

You see them basically just wanting thing to express, oh, that's mine and no one else has it. So to say that's why. Yeah. I feel like to some extent the old school train of thought when it comes to the internet is slowly coming back. Especially with the advent of protocols like ATProto. And you'll experience more websites that just allow people to make their own homes on the internet. 

Cause in my opinion, one of the biggest problems is that people do not really want to register on a lot of platforms. 'cause you already have this place where you get all of your followers, you have all of your connections, and then you want to move and then you'll lose all of your connections and everything.

But with something like ATProto, you can use the social graph of, for example, Bluesky. I want to add followers on PinkSea. So for example, you have an artist that has like 30,000 followers for example, I can just click import my following from Bluesky. And just like that they would already get all of the artists that they follow on Bluesky already added as followers on PinkSea.

And for example, someone else joins and they followed that big artist and they instantly followed them on PinkSea as well. I think that we are slowly coming back to the advent of people owning their place online. 


## PinkSea and ATProto (PDS)

[00:32:24] **Jeremy:** Yeah. So let's talk a little bit more about how PinkSea fits into ATProto. For people who aren't super familiar with ATProto, maybe you could talk about how it's split up. You've got the PDS, the relays, the AppView. What are those and how do those fit into what PinkSea is?

[00:32:48] **Prefetcher:** My favorite analogy, ATProto is a massive network, and at least me, when I saw the initial graph I was just very confused. I absolutely did not know what I'm looking at. But let's start with the base building block, something that ATProto wouldn't exist with.

And it's the [PDS](https://atproto.com/specs/account). Think of the PDS as like a filing cabinet. You have a bunch of folders in which you have files, so to say. So you have a filing cabinet with your ID, this is the DID part that sometimes shows up and scares people. It's what we call a [decentralized identifier](https://atproto.com/specs/did). Basically that identifier is not really tied to the PDS, it just exists somewhere. And the end goal is that every user controls their DID. 

So for example, if your PDS shuts down, you can always move to somewhere else. Still keep like, for example, that you are `prefetcher.miku.place`. But in that filing cabinet the PDS going back to it you have your own little zone, your own cabinets, and that has your identifier, it's uniquely yours. 

Every single application on the AT protocol creates data. They create data and they store the data in a structured format called a [record](https://atproto.com/guides/glossary#record). A record is basically just a bunch of data that explains what that thing is, be it a like, a post on Bluesky an oekaki on PinkSea and an upvote on front page, or even a pixel on place.blue.

And all of those records are organized into folders in your cabinet. And that folder is named with something we call a collection id. So for example, a like is, if I remember correctly, it's `app.bsky.feed.like`, so you see that it belongs to Bluesky. The `app.bsky` part. it's a feed thing, and the same way, PinkSea, for example, the oekaki and PinkSea uses `com.shinolabs.pinksea.oekaki` with `com.shinolabs` being the the collective that I use as a, pen name, so to say.

PinkSea being, well, PinkSea and oekaki just being the name. It's an oekaki. If you want to see that there are a lot of tools, for example, [PDSls](https://pdsls.dev) or [atp.tools](https://atp.tools) or [ATProto browser](https://atproto-browser.vercel.app), if you had to go into one of those and you would type in for example, prefetcher.miku.place, you would see all of your records, the things that, you've created on the AT protocol network. 


## Relay

[00:35:19] **Prefetcher:** So you have a PDS, you have your data, but for example, imagine you have a PDS that you made yourself, you hosted yourself. How will, for example, Bluesky know that you exist? 'cause it won't, it's just a server in the middle of nowhere. 

That's where we have a [relay](https://atproto.com/guides/glossary#relay). A relay is an application that listens to every single server. So every time you create something or you delete something, or for example, you edit a post, you delete an oekaki. You create a new, like -- Your PDS, your filing cabinet generates a record of that. It generates an event, something we call a commit. So, anytime you do something, your PDS goes, Hey, I did that thing. And relays function as big servers that a PDS can connect to. And it's a massive shout box. The PDS goes, Hey, I made this. Then the relay aggregates all of those PDSs into one and creates a massive stream of every single event that's going on the network at once. That's also where the name firehose comes from. 'cause the, the end result, the stream is like a firehose. It just shoots a lot of data directly at anyone who can connect to it. And the thing that makes AT Protocol open and able to be built on is that anyone can just go, I want to connect to [jetstream1.west.bluesky.network](https://docs.bsky.app/blog/jetstream).

They just make a connection to it and boom they just get everything that's happening. You can, for example, see that via [firesky.tv](firesky.tv). If you go to it, you would open it in your browser. Every single Bluesky post being made in real time right directly in your computer. So you have the PDSs that store data, you have the relay that aggregates every, like, builds a stream of every single event on the network. 


## AppViews

[00:37:26] **Prefetcher:** You just get records. You can't interact with it. You can see that someone made a new record with that name, but to a human, you won't really understand what a cid is or what property something else is. That's why you have what we call [AppViews](https://atproto.com/guides/glossary#app-view). An AppView, or in full an application view is an application that runs on the AT protocol network. It connects to the relay and it transforms the network into a state that it can be used by people.

That's why it's called an application view. 'cause it's a, a specialized view into the whole network. So, for example, PinkSea connects, and then it goes, hey, I want to listen on every single thing that's happening to `com.shinolabs.pinksea.oekaki`, and it sees all of those, new records coming in and PinkSea understands, oh, I can turn it into this, and then I can take this thing, store it in the database, and then someone can connect with a PinkSea front end.

And then it can like, transform those things, those records into something that the front end understands. And then the front end can just display, for example, the timeline, the same way Bluesky, for example -- Bluesky gets every single event, every single new file, new record coming in from the network. And it goes. Okay, so this will translate into one more like on this post. And this post is a reply to that post. So I should chain it together. Oh. And this is a new feed, so I should probably display it to the user if they ask for feeds. And it basically just gets a lot of those disjoint records and it makes sense of them all.

The end user has a different API to the Bluesky AppView. And then they can get a more specialized view into Bluesky.


## PinkSea does not store the original images, the PDS does

[00:39:26] **Jeremy:** And so in that example, the PDSs, they can be hosted by Bluesky the company, or they could be hosted by any person. And so PinkSea itself, when somebody posts a new oekaki, a new image, they're actually telling PinkSea to go create the image in the user's PDS, right? PinkSea is itself not the the source of truth I guess you could say.

[00:40:00] **Prefetcher:** PinkSea in itself. I don't remember which Bluesky team member said it, but I like the analogy that AppViews are like Google. So in Google, when you search something, Google doesn't have those websites. Google just knows that this thing is on that website. In the same vein, PinkSea, when you create a new oekaki, you tell PinkSea, Hey, go to my PDS and create that record for me. And then the person owns the PDS. So for example, let's say that in a year, of course I won't do it, but hypothetically here, I just go rogue and I shut down PinkSea, I delete the database. You still own the things. So for example, if someone else would clone the PinkSea repository and go here, there's PinkSea 2.

They can still use all of those images that were already on the network. So, AppViews in a way basically just work as a search engine for the network. PinkSea doesn't store anything. PinkSea just indexes that a user made a thing on that server. And here I can show you how to get to it somehow.

Those images aren't stored by PinkSea, but instead, I know that the image itself is stored, for example, on `pds.example.com`, and of course to reduce the load, we have a proxy. PinkSea asks the proxy to go to `pds.example.com` and fetch the image, and then it just returns it to the user.

[00:41:37] **Jeremy:** And so what it sounds like then is if someone were to create oekaki on their own PDS completely independently of Pink Sea the fact that they had created that image would be sent to one of the relays, and then PinkSea would receive an event that says oh, this person created a new image then at that point your index could see, oh, somebody created a new image and they didn't even have to go through the PinkSea website or call the PinkSea APIs. Is that right?


## Sharing PDS records with other applications

[00:42:14] **Prefetcher:** Yep. That is exactly right. For example, someone could now go, Hey, I'm making my own PinkSea-like application. And then they would go, I want to be compatible with PinkSea. So I'm using the same record. Or what we call a [lexicon](https://atproto.com/guides/lexicon), basically describe how records look like. I forgot to mention that, but every single record has an attached lexicon.

And lexicons serve as a blueprint. So a lexicon specifies, oh, this has an image, this has a for example, the tags attached to it, a description of the image. Validate that the record is correct, that you don't get someone just making up random stuff. 

But yeah, someone could just go, Hey, I'm making another website. Let's call it GreenForest for example. And GreenForest is also an oekaki website, but it uses, for example, [chickenpaint](https://github.com/thenickdude/chickenpaint) instead of tegaki but I want to be able to interoperate with PinkSea. so I'm also gonna use `com.shinolabs.pinksea.oekaki` the collection, the same record, the same lexicon. 

And for example, they have their own servers and the servers just create regular oekaki records. So for example, GreenForest gets a new user, they log in, create, draw their beautiful image, and then they click upload it.

So GreenForest goes to that person's PDS and tells the PDS, Hey, I want to make a new. `com.shinolabs.pinksea.oekaki` record. The PDS goes okay, I've done it for you. Let me just inform the relay that I did so, relay gets the notification that someone made that new PinkSea oekaki record. And so the main PinkSea instance, pinksea.art, which is listening in on the relay, gets a notification from the relay going, Hey, there is this new oekaki record. And PinkSea goes, sure, I'll index it. And so PinkSea just gets that GreenForest image directly in itself. And in the same vein, someone at PinkSea could draw something in tegaki -- their own beautiful character. And the same thing would happen with GreenForest. GreenForest would get that PinkSea image, that PinkSea record, and index it locally.

So the two platforms, despite being completely different, doing completely different things, they would still be able to share images with each other.


## Bluesky PDS stores other AppView's data but they could stop at anytime

[00:44:38] **Jeremy:** And these images, since they're stored in the PDS, what that would mean is that anybody building an application on ATProto, they can basically use Bluesky's PDS or the user's PDS as their storage. They could put any number of images in there and they could get into gigabytes of images.

And that's the responsibility of the PDS and not yourself to keep track of.

[00:45:12] **Prefetcher:** Yes, that can be the case. Of course, there is a hard limit on how big a single upload can be, which is, if I remember correctly, I don't wanna lie, I think it's 50 megabytes, I don't recall there being a hard cap on how big a single repository can be. I know of some people whose repositories are in the single gigabyte digits but this kind of is a thing scares app developers.

'cause you never know when Bluesky the company -- 'cause most people registering, are registering on Bluesky. We don't really know whether Bluesky, the company will want to keep it for free. Forever allow us to do something like that. You already have projects like, for example, [ATFile](https://github.com/ziodotsh/atfile), which just allow you to upload any arbitrary data just to store it, on their servers and they are paying for you.

So we'll never know whether Bluesky will decide, okay, our services are only for Bluesky if you want to use PinkSea you have to deal with it. Or whether they go, okay, if you want to use alternative AppViews you have to pay us in order to host them. So, that also leads me to the fact that decentralization is an important part of AT protocol as Bluesky themselves say that they are a potential adversary.

You cannot trust them in the long term. Right now they are benign right now, they're very nice, but, we never know how Bluesky will end up in a year or two. So if you want to be in the full control of your data, you need to sadly host it by yourself. And it's honestly really easy in order to do so.

There is a ton of really useful online content blogs and whatever. I think I've set up my PDS in 10 minutes on a break between classes and university. But to a person that's non-technical that doesn't know much I'd say around an hour to two hours 


## The liability and potential abuse from running a PDS

[00:47:14] **Jeremy:** Yeah, I think the scary thing for a lot of people is technical or not, is even if it's easy to set up, you gotta make sure it keeps running. You gotta have backups. And so it could be a lot.

[00:47:30] **Prefetcher:** Yeah. 

This is to be expected by the fact that you're in control of your data. Keeping it secure the same way, for your personal photos or your documents, for example, your master's diploma or whatever. And it's on you to keep your Bluesky interaction secure. On one hand, it's easier to get someone to do it, and I expect in the future we'll get people that are hosting public PDSes I sometimes thought of doing that for PinkSea, just like allowing people to register by PinkSea.

But, doing so as a person, you also have to be constantly on call for abuse. So if someone decides to register via PinkSea and do some illicit activities, you are solely responsible for it.


## PDS and AppView moderation liability

[00:48:17] **Jeremy:** So if they were to upload content that's illegal, for example, it's hosted on your servers so then it's your problem.

[00:48:27] **Prefetcher:** Yeah, it is my problem. 

[00:48:29] **Jeremy:** At least the way that it works now, the majority of the people, their PDS is gonna be hosted by Bluesky. So if they upload content that's breaks the law, then that's the Bluesky company's problem at least currently.

[00:48:44] **Prefetcher:** Yeah. That is something that Bluesky has to deal with. But I do believe that in the future we are going to have, more like independent entities just building infrastructure for ATProto, not even the relay it's just like PDSs for people to be able to join the atmosphere, but not directly via Bluesky. 

[00:49:06] **Jeremy:** I'm kind of curious also with the current PDSs, if it's hosted by Bluesky, are they, are they moderating what people upload to their PDSs?

[00:49:16] **Prefetcher:** Good question. Honestly, I don't think they're moderating everything 'cause, it's infeasible for them to, for example, other than moderate Bluesky to also moderate PinkSea and moderate front page and whatnot. So it's the obvious responsibility to moderate itself and to report abuse. I'd say that if someone started uploading illicit material, I do not think, and this is not legal advice, I do not think that they would catch on until some point let's say. 

[00:49:52] **Jeremy:** I mean, from what you were describing too, it seems like the AppViews would also, have issues with this because if, let's say someone created a PinkSea record in their PDS directly and the image they put in was not an oekaki image, it's instead something pretty illegal in the country that your AppView is hosted then, Wouldn't that go straight to the PinkSea users viewing the website?

[00:50:20] **Prefetcher:** Yes, sadly, this is something that you have to sign up as you're making an AppView and especially one with images. Sooner or later you are going to get material that you have to moderate and it's entirely on you. That's why, you have to think of moderation while you're working on an AppView. 

Bluesky has an insanely complicated, at least in my opinion, moderation system, which is composable and everything, which I like. But for smaller AppViews, I think it's too much to build the same level of tooling. So you have to rely more on manual work.

Thankfully so far the user base on PinkSea has been nothing but stellar. I didn't have to deal with any law breaking stuff, but I am absolutely ready for one day where I'll have to sadly make some drastic moderation issues.

[00:51:18] **Jeremy:** Yeah. I think to me that's the most terrifying thing about making any application that's open to user content.

[00:51:29] **Prefetcher:** I get it, sadly. I'm no stranger to having issues with people, abusing my websites. Because since 2016, my, first major project was a text board based off of, a text board in a video game called [DANGER/U/](https://va11halla.fandom.com/wiki/DANGEROUS_OPINIONS). It was semi-popular, during the biggest spike in activity in like 2017 and 2016, it had in the tens of thousands of monthly visitors.

And sadly, yeah, even though it was only text, I've had to deal with a lot of annoying issues. So to say the worst I think was I remember waking up and people are telling me that DANGER/U/ is down. So I log in the activity logs and someone hit me with two terabytes of traffic in a day.

There was a really dedicated person that just hated my website and just either spam me with posts or just with traffic. So, yeah, sadly I have experience with that. I know what to expect that's something that you sadly have to sign up for making a website that allows user content. 


## Pinksea is a single server

[00:52:42] **Jeremy:** To my understanding so far, PinkSea is just a single server. Is that right?

[00:52:47] **Prefetcher:** It is a single server. Yeah.

[00:52:48] **Jeremy:** That's kind of interesting in that, I think a lot of people when they make a project, they worry about scaling and things like that. But, was it a case where you just had a existing VPS and you're like, well hopefully this is, this is good enough?

[00:53:03] **Prefetcher:** I actually ordered a new one even though it's not really powerful, but my train of thought was that I didn't expect it to blow up. I didn't expect it to require more than a single VPS with 8 gigabytes of RAM and whatnot. And so far it's handling it pretty well. I do not expect ever to reach the amounts of traffic that Bluesky does, so I do not really have to worry about insane scalability and whatever.

But yeah. I thought of it always as a toy project until the day I released it and realized that it's a bit more than a toy project at this point. To this day, I just kind of think that that website even if it were popular, I would never expect it to have -- And in the best, most amazing case scenario, like a hundred posts a day. I do not have to deal with the amount of traffic that Bluesky does. So one VPS it is.

[00:53:59] **Jeremy:** Yeah, that makes a lot of sense. I mean the application is also mostly reads, right? Most people are coming to see the posts and like you said, you get a few submissions a day, but all the read stuff can probably be cached.


## Harbor image proxy

[00:54:15] **Prefetcher:** Yeah. The heaviest, thing that PinkSea requires is the [image proxy harbor](https://github.com/shinolabs/harbor), and that's something that right now only runs on that server. It's in Luxembourg. I think that's where my coprovider hosts it but yeah, that gets the most reads.

'cause in most cases, PinkSea, all it does, all you get is reads from a database, which is just, it's a solved problem. It's really lightweight. But with something like image proxying, you have this whole new problem. 'cause it's a lot of data, and you somehow have to send it -- it's enough for me to just host it locally on that PinkSea server and just direct people to it. But sooner or later, I can always just put it behind something like [Bunny CDN](https://bunny.net) or whatnot to have it be worldwide.

[00:55:09] **Jeremy:** So Harbor is something I think you added recently. How did the images work before and what is Harbor doing in its place?

[00:55:18] **Prefetcher:** Before I did what a lot of us currently do and I just freeload atop of Bluesky CDN 'cause Bluesky CDN is just open so far. But it's something that personally irked me. 'cause, I want PinkSea to be completely independent of Bluesky Corporation. I, I wanted to persevere even if Bluesky just decides to randomly, for example, close, the CDN to others or the relay to others or the PLC directory in the worst case scenario. 

So I wanted to make my own CDN more like proxy. You can't really call it a CDN because it's not worldwide. It's just a single server but let's just say image proxy. So Harbor whenever a person goes to PinkSea, they start loading in all of the images and every single image instead of going to, for example, the PDS or to `cdn.bluesky.app`. They go to `harbor.pinksea.art`, you get attached the identifier of the user and what we call a content identifier. 

Every single, thing uploaded to a PDS has an attached content identifier, which identifies it in a secure way so to say. So Harbor does in reality a really simple set of things. First and foremost, if the user has not seen it, like, not loaded it before first Harbor asks the local cache, do I have this file? If they do, if Harbor does, it just sends the file and it tells the browser, Hey, by the way, please don't ask me about this file for the next day. And in most cases, after one refresh, the user, all of the images load instantly because the web browser just goes, of those files were already sent. And Harbor asked me not to like, ask it more about the same file. 

So in the case of the image isn't in harbor's local cache, Harbor, first does a lot of those steps to resolve, the users identifier through their PDS, basically resolving that identifier, the DID to a DID document, which is a document basically explaining how that user, what is their, alias, what is their handle and where can we find them, which PDS. 

So we find the PDS and we then ask the PDS, Hey, send us this file for this user. The PDS sends it or doesn't, in which case we just throw an error and, Harbor just saves it locally and it sends it to the client.

It basically just that. But to my knowledge, it's the first non Bluesky image proxy that's deployed for any AppView. Which also caught the attention of [Brian Newbold](https://bsky.app/profile/bnewbold.net) one of the Bluesky employees and made me really happy.


## DID PLC Lookup



[00:58:14] **Jeremy:** The lookup when you have the user's, DID and you wanna find out where their PDS is that's talking to something called, I think it's the PLC directory?

[00:58:25] **Prefetcher:** Actually there are two different ways.

First is [PLC directory](https://web.plc.directory), PLC originally standed for a placeholder, and then Bluesky realized that it's not a placeholder anymore, and they stealthily changed it to public ledger of credentials. So we have PLC and we have web, the most common version is PLC.

The document, the DID document is stored on Bluesky controlled servers under the moniker of PLC directory. They expose a web API that basically just allows you to say, Hey, give me the document for did:plc, whatever. And, the directory goes, have it. And this is the less decentralized version.

You can host your own PLC directory and you can basically ask (their) PLC directory to just send you every single document and just you can have your local copy, which some people already do, you kind of sacrifice the fact that you are not in control of the document.

It's still on a centralized server, even if you control the keys. 'cause every single DID document also has a key. And that key is used to sign changes to the document. So technically, if you define your own set of keys, you can prevent anyone else from modifying your document, even Bluesky.

'cause every single document is verifiable back and forth. You can see the previous document and its key is used to sign the next document and the chain of trust is visible and no one can just make random changes to your identity, but yeah, it's still on Bluesky to control service and it's a point of contention.

Bluesky eventually wants to move it to a nonprofit standards organization, but we have yet to see anything come out of it, sadly.


## DID WEB lookup

The next method is web. And web instead of -- 'cause in did:plc, you have did:plc, and a random string of characters. 

[01:00:30] **Prefetcher:** Web relies on domains. So for example, the domain would already like be the sole authority of where the file is.

So for example, if I had did:web:example.com, I would parse the DID and I would see it's hosted at example.com. So I go to example.com, I go to /.wellknown/did.json which is the well-known location for the file. And I would have the same DID document as I would have if I used, for example, a PLC DID resolved via the PLC directory. the web method, you are in control of the document entirely. It's on your server under your domain. While it's the more decentralized version, it's just kind of hard for non-technical people to make them. 'cause it relies on a bunch of things. 

And also the problem is that if you lose your domain, you also lose your identity.

[01:01:23] **Jeremy:** Yeah. So unlike the PLC where it's not really tied to a specific domain, you can change domains. With the web way, you have to always keep the same domain 'cause it's a part of the DID and yeah, like you said, you can't let your renewal lapse or your credit card not work. 'cause then you just lose everything.

[01:01:49] **Prefetcher:** Yeah. You would still be able to change handles, but you would be tied for that domain to forever send your DID otherwise you would just lose it forever.

[01:01:57] **Jeremy:** Yeah, I had mostly only seen the PLC and I wasn't too familiar with the web, form of identification, but yeah that makes sense.

[01:02:06] **Prefetcher:** I think the web if I remember correctly, there is slightly over 300 accounts total on the entire network that use it. [Mary](https://bsky.app/profile/did:plc:ia76kvnndjutgedggx2ibrem) who is a person on Bluesky that does a lot of like, ATProto related things, has a [GitHub repository that basically gives insight into the network](https://github.com/mary-ext/atproto-scraping).

And on her GitHub repository, you can find the list of every single custom PDS and also how many DID webs there are in existence. And I think it was slightly over 300.

[01:02:38] **Jeremy:** So are you on that list?

[01:02:40] **Prefetcher:** My PDS Yeah. If you were to scroll down. I don't use a web DID 'cause I registered my account before when I was brand new to ATProto, so I didn't know anything. But if you had to scroll down, you would see pds.ata.moe, which is my custom PDS just running.

[01:02:55] **Jeremy:** Cool.

[01:02:57] **Prefetcher:** Yeah.


## Harbor image proxy can cache any image blob

[01:02:58] **Jeremy:** So something I noticed about harbor, you take the, I believe you take the DID and then you take the CID, the content identifier. I noticed if you take any of those pairs from the ATProto network, like I go find a image somebody posted on Bluesky, I pass that post DID and CID for the image into harbor.

Harbor downloads it and caches it. So it's like, does that mean anybody could technically use you as a ATProto CDN?

[01:03:38] **Prefetcher:** Yes, the same way anyone could use like the Bluesky CDN to for example, run PinkSea like I did. cause I do not know if there is a good way to check if a CID of an image or a blob basically. 'cause files on ATProto are called blobs. I do not think there is a nice way to check if that blob is directly tied to a specific record. But that also allows you to make cool, interesting things. 


## Crossposting to Bluesky talks directly to the PDS

[01:04:06] **Prefetcher:** 'cause for example, PinkSea has that, cross post to Bluesky thing. So when you create an image, You already have an option to cross post it to Bluesky, which a lot of people liked. 

And it was a suggestion from one of the early users of PinkSea. And the way it works is that when we create a PinkSea record, we upload that image, right? And then PinkSea goes, okay, I'm gonna use that same image, the same content identifier, and just create a Bluesky post. So Bluesky and PinkSea all share the same image. I don't upload it twice, I just upload it once. use it in PinkSea and I also use it in Bluesky. And the same way Bluesky its CDN, can just fetch the image. I can also fetch the image from mine, 'cause blobs aren't tied to specific records.

They just exist outside of that realm. And you could just query anything. Not even images. You could probably query a video or even a text file.

[01:05:04] **Jeremy:** So when you cross post to Bluesky, you're creating a record directly in the person's PDS, not going through bluesky's API.

[01:05:14] **Prefetcher:** No, I sidestep Bluesky's API completely. And, I basically directly talk to the PDS at all times. I just tell them, Hey, please, for me, create a `app.bsky.feed.post` record. And you have the image, the text, which also required me to manually parse text into rich text.

'cause like, Bluesky doesn't automatically detect for example, links or tags And you basically get -- like PinkSea creates a record directly with the link to the image. And all of those tags, like the PinkSea tag and whatever, And I completely sidestep. Bluesky's API. If Bluesky, the AppView would cease to exist, PinkSea would still happily create Bluesky crossposts for you.


## Other applications put metadata into Bluesky posts so they can treat them differently

[01:06:02] **Jeremy:** And since you're creating the records yourself, then you can include additional metadata or fields where you know that this was a PinkSea post, or originally came from PinkSea.

[01:06:13] **Prefetcher:** I could do that. I don't really do that right now 'cause I don't really have much of a reason other than adding a PinkSea hashtag to every single oekaki. But I, noticed, for example, I think it was [PinkSky](https://pinksky.app), interesting name, PinkSky, which is like (a) Bluesky Instagram client. 

Any single time you make a post via PinkSky it uses the Bluesky APIs. It's Bluesky, but it attaches a hidden hashtag like PinkSky underscore some random letters. In its feed building algorithm, it basically detects posts with that hashtag, that specific hashtag, and it builds a PinkSky only timeline.

'cause it's still a Bluesky post, but it has hidden additional metadata that identifies, Hey, it came from PinkSky. 

[01:07:02] **Jeremy:** It's pretty interesting how much control you have over what to put in the PDS. So, I'm sure there's a lot of interesting use cases that people are gonna come up with.

[01:07:14] **Prefetcher:** Yeah, of course. You still lose some of the data when you go through the Bluesky API. 'cause of course it stores the record and it's all in formats and whatnot. But you can attach a lot of metadata that can identify posts and build micro networks within Bluesky itself.

I see it like that.


## Bluesky CDN compression

[01:07:37] **Jeremy:** And I think, this might have been a post from you. I think I saw somebody saying that when you view an image from the CDN that the Bluesky CDN specifically, there's some kind of compression going on that that messes with certain types of art.

[01:07:55] **Prefetcher:** It's especially noticeable artists are complaining about it all the time, left and right. Bluesky is very happy with jpeg compression, by default, their CDN, -- like to every single image it applies a really not good amount of jpeg compression which is especially not small.

If you compare an image that's uploaded via PinkSea, view an image on PinkSea, and view the same image, which is, it's the same content id. It's the same blob. And you view it on Bluesky, it loses so much fidelity, it loses so much of that aliasing on the pen.

You just see everything become really blurry. And on top of that, when you upload an image via Bluesky itself, if I remember correctly, I don't wanna lie here, but they also downscale the image to 1024 pixels by default.

So every single image, not only big ones, and artists usually work with really big canvases, they get, downscaled and also additionally they get jpegified.

So for example, PinkSea directly uploads PNG files to the PDS. And for example, Harbor gives back the original file. It does no transformations on it, but Bluesky transforms all of them into JPEG compressed images and for photos, it's fine sometimes. 'cause I've also seen people just compare directly, downloaded images of the PDS versus images viewed on Bluesky.

But for art it's especially noticible. And people really (do) not like that.

[01:09:31] **Jeremy:** Yeah, that's kind of odd. 'cause if, if I understand correctly, then if you post directly to your PDS and Bluesky pulls it in you'll avoid that, that 1024 resizing. So your images will be higher quality?

[01:09:47] **Prefetcher:** I actually do not know. That's an interesting question. 

Cause I know that the maybe their CDN also does that 'cause that's what I've heard from others, that on upload the image gets processed and squashed down. So I don't know if doing it via an alternative AppView would change it or would Bluesky just directly reject this post? Because for example, PinkSea, I have built-in which I think I might change in the future -- PinkSea will reject your post if it's bigger than 800x800. 'cause then it'll notice that something is off. This could not have been made with PinkSea.

[01:10:26] **Jeremy:** Yeah, that's a good point I suppose we know at the very least, they have some third party and internal moderation tools that they feed the images through to, so they, they can do some automatic content tagging. But yeah, I, I don't know, like you said, whether, the resizing and all that stuff is at the CDN level

[01:10:50] **Prefetcher:** The jpegification is definitely at the CDN level. 'cause, 

Bluesky is actually running an open source image proxy. It's called [imgproxy](https://github.com/imgproxy/imgproxy). 

Brian Newbold talked about it a bit on that [harbor post](https://bsky.app/profile/bnewbold.net/post/3lgo3ri5m222e). And, yeah, so a lot of the compression, the end user things are done via image proxy, but that, downscaling, I don't know, you'd have to ask someone who's a bit more intimate with Bluesky's internals.

[01:11:19] **Jeremy:** Cool. yeah, I think we've, we've covered a lot. Is there, is there anything else, you wanted to mention or thought we should have talked about?

[01:11:26] **Prefetcher:** Regarding PinkSea I think I've mentioned a ton both the behind the scenes things and, the user things, the design principles. What I'd want to absolutely say, and it will sound cheesy, and, is that I'm eternally grateful to anyone who's actually visited PinkSea. It's definitely grown outta all of my like dreams for the platform, to the point where I'm sitting here just talking about it. I definitely hope that the future will bring us more applications (in) ATProto. I definitely have ideas on how to expand PinkSea, a lot of ideas, a lot of things I want to do, and I'm also a very busy person, so I never get around them. But yeah, think that's it, at least regarding PinkSea.

[01:12:15] **Jeremy:** Cool. Well, if people want to check out PinkSea or see what you're up to, where can they find you?

[01:12:22] **Prefetcher:** So PinkSea is at [pinksea.art](https://pinksea.art). That's the website and Bluesky Handle is at [pinksea.art](https://bsky.app/profile/pinksea.art) and me, well, search prefetcher on Bluesky, you'll probably find me. My tag is at [prefetcher.miku.place](https://bsky.app/profile/prefetcher.miku.place). all of my socials are probably there. I'm Prefetcher pretty much every single platform except for the platforms that already had someone called Prefetcher.

GitHub, [github.com/purifetchi](https://www.github.com/purifetchi) because Prefetcher was taken. And, yeah, hit me up. I'm always eager to talk. I don't bite.

[01:13:00] **Jeremy:** Very cool. Well, Kacper thanks. Thanks for taking the time. This was fun.

[01:13:04] **Prefetcher:** Thank you so much, Jeremy, for having me over. It was a pleasure.

