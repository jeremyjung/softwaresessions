+++
title = "The battle for your privacy on the web"

description = "Pete explains the ways standards committees, browser vendors, and extensions protect us from tracking on the web"

[extra]
episode_url = "https://media.transistor.fm/b75c6f76.mp3"
social_title = "The battle for your privacy on the web"
+++

Pete is the senior security researcher at Brave Software and the co-chair of the [W3C Privacy Interest Group](https://www.w3.org/Privacy/). 

We discuss:
- The differences between academic research and product development
- How websites track us with cookies, fingerprinting, and other techniques
- The surprising amount of data your browser gives up without a permission prompt
- What features should go in the browser vs being native only
- The confusion behind what incognito or private modes do
- The role of [EasyList](https://easylist.to/) and the underappreciated people behind it
- Building tools like [PageGraph](https://github.com/brave/brave-browser/wiki/PageGraph) to identify and rewrite tracking code
- Replacing resources at page load to preserve privacy without breaking websites
- Developing web standards at the W3C while preserving privacy
- Brave's plan to fund websites with ads instead of paywalls while preserving user privacy
- Getting involved in privacy and web standards

### Related Links
- [@pes10k](https://twitter.com/pes10k)
- [Personal Site](https://www.peteresnyder.com/)
- [Privacy Interest Group (PING)](https://www.w3.org/Privacy/IG/)
- [W3C Privacy Community Group](https://privacycg.github.io/)
- [Research at Brave](https://brave.com/research/)
- [SpeedReader: Fast and Private Reader Mode for the Web](https://brave.com/speed-reader/)
- [Detecting Filter List Evasion With Event-Loop-TurnGranularity JavaScript Signatures](https://brave.com/wp-content/uploads/2020/07/event-loop-signatures-sp-2021.pdf)
- [EasyList](https://easylist.to/)
- [uBlock Origin](https://github.com/gorhill/uBlock/)
- [Panopticlick](https://panopticlick.eff.org/)
- [Protecting Against HSTS Abuse](https://webkit.org/blog/8146/protecting-against-hsts-abuse/) (WebKit)
- [What’s the Difference Between First-Party and Third-Party Cookies?](https://clearcode.cc/blog/difference-between-first-party-third-party-cookies/)
- [Understanding Redirection-Based Tracking](https://brave.com/redirection-based-tracking/)
- [MediaDevices.enumerateDevices()](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/enumerateDevices) (Specifications give server all devices and labels without asking for permission)
- [CSS difficulty with adoption](https://en.wikipedia.org/wiki/Cascading_Style_Sheets#Difficulty_with_adoption) (CSS2 spec was written without an implementation causing problems)
- [What Are CSS Vendor or Browser Prefixes?](https://www.lifewire.com/css-vendor-prefixes-3466867)
- [FPRandom: Randomizing core browser objects to breakadvanced device fingerprinting techniques](https://hal.inria.fr/hal-01527580/document)
- [Brave Fingerprinting Protections v2: Farbling for Greater Good](https://brave.com/whats-brave-done-for-my-privacy-lately-episode-4-fingerprinting-defenses-2-0/)
- [PageGraph](https://github.com/brave/brave-browser/wiki/PageGraph)
- [Puppeteer](https://github.com/puppeteer/puppeteer)
- [Target: You Can’t Hide That Baby Bump From Us](https://digital.hbs.edu/platform-digit/submission/target-you-cant-hide-that-baby-bump-from-us/)
- [Brave Ads FAQ](https://support.brave.com/hc/en-us/articles/360026361072-Brave-Ads-FAQ)
- [LUMAscape](https://lumapartners.com/content/lumascapes/display-ad-tech-lumascape/)

Music by Crystal Cola: [12:30 AM](https://crystalcola.bandcamp.com/track/12-30-am) / [Orion](https://crystalcola.bandcamp.com/track/orion)

---

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy:** [00:00:00] In this episode of software sessions, I'm talking to Pete Snyder about the many ways websites track us. How ad blockers like uBlock Origin work. And the process of developing web standards with privacy in mind. We start by discussing his role as a senior privacy researcher at Brave software  

**Pete:** [00:00:18] Brave is kind of interesting or unique as a startup in that we have a proper research lab. I think our research team is seven or eight people right now. Those are people who do research in the form of published publications but also doing research that ties back into product in some way.

My research responsibilities are to figure out new ways that you can improve browser privacy, address tracking on the web, and solve the kinds of problems that Brave is interested in solving. I have one foot in engineering world and one foot in publishing world.

**Jeremy:** [00:00:48] Why is academic research important in this space?

**Pete:** [00:00:52] My gut feeling is that what's useful about academic research is that it changes the incentives and it gives you a chance to do things that are more novel and particularly things that are less tied to a short term ROI cycle. That is particularly useful for things that have watchdog functions over industry, things that are more difficult to monetize but more useful to average web users.

That's not to say there aren't people who try to build businesses around privacy or responsible computing but the incentives don't always work that way. What's really neat about doing a research focused computing career is you can do things that don't have to make somebody money in the short term. You can pick more oddball projects. The things that might not come to fruition right away.

**Jeremy:** [00:01:36] And is there a key difference in how you approach a problem when you're doing it in an academic context versus as a product for a company?

**Pete:** [00:01:46] Sure. So they go both ways. If I'm working for something at Brave the emphasis is on correctness and certainty. And knowing that when we ship it to 10 million people or whatever that it's not going to break and it's going to do what it says on the tin and that it's going to be a material improvement over the state of things before we ship that feature.

And that's really different than if you're trying to come up with a research project where.. sometimes good, sometimes bad, but the emphasis is not necessarily on a hundred percent correctness but is on novelty and doing something or figuring out some way to solve a problem in a way that it hasn't been tackled before.

And so you'll read research papers that say it works 95% of the time and that'll be sufficient or compelling for a research paper. But you wouldn't want to ship something that breaks 1 out of 20 websites if you're actually making a product. The goals are different, but also the success criteria are different.

**Jeremy:** [00:02:39] So it sounds like you can tackle things where it wouldn't be good enough for a product yet. But it's something that if you were working on it within the context of a company, they might say: Oh, we're not going to do that because it just doesn't seem like it's going to work.

**Pete:** [00:02:54] Yeah, exactly. So, maybe because certainty of success isn't there, or there isn't a one or two step obvious path to being a product. Maybe it conflicts with the current business goal or whatever else. But yeah, you have much more latitude in terms of products you can choose and kind of problems you want to tackle.

If you're writing research papers and not that I'm some incredible researcher or anything, but if you try to do successful research it doesn't reward you to solve that final 5% of the problem.

There's no benefit to getting no, not none, but there's a small benefit of going from 95% to 99% success or accuracy. On product you have to grind out as close to a hundred as you can get.

**Jeremy:** [00:03:37] And do you have examples of things where you worked on it in a research context and it actually became a part of a product?

**Pete:** [00:03:46] Sure. Yeah. So a couple of things. One is that.. so there's a research paper that we wrote at Brave called Speed Reader. Speed Reader is a different way of doing a reader mode in a browser. Right now, if you use any of the reader modes in popular browsers, you download the page, you render some subset of it.

You throw some JavaScript at it and it extracts sections that it thinks are useful, then it presents a new page to you. That's not a hundred percent correct. Chrome's DOM distiller does something slightly different, but to approximation you render the page and then you extract stuff out of it. Brave speed reader does something different.

It intercepts it at a network layer. It examines the text HTML. Does the analysis there and then feeds that back to the rendering engine. And so there's a bunch of nice benefits there. There's a privacy improvement in that you're executing less code talking with less third parties. There's an performance improvement as well in that you don't have to do the initial displaying and tear all that stuff down and build it back up. So that was the research paper that we published at. WWW 2018 2019. I don't remember, but either a year or two ago. And it's now in beta in Brave. That's maybe the oldest one. The most recent one was a project that I did last summer with a student from North Carolina, Quan Chen on figuring out ways that we can do blocking better.

Right now, if you're using a privacy tool in a browser in most cases you're downloading a big list of things that should get blocked. They look kind of like regular expressions. It says: Yes, block this. No don't black that, and it's a useful thing.

But it has the trade off of it's very easy to circumvent that. Somebody can just change the URL [and] move it to a different domain inline in the page, whatever else. And so the approach that we took from this paper is.. Let's not focus on the URL. Let's build signatures of the execution paths of these scripts and we can use that as the Oracle to identify this is known bad or known good. That machinery ended up being very complicated and it isn't something we want to ship to all of our users because of the performance hit. It's something that we use for generating filter lists that we should download to users regularly.

**Jeremy:** [00:05:40] Existing projects you were saying are just looking at a list of URLs. And you said using something like regular expressions to figure out if the URL it's pulling is on that list. The part I wasn't clear about is the new way that you were describing worked.

**Pete:** [00:05:57] Yeah. The alternative approach that we came up with is to instead.. Not care about where the code came from or even how the code is structured. So if it's obfuscated in some way, but instead to look at the DOM and JavaScript operations that the code executes and sequence those and use that as the identifying signature of the code.

There's some cleverness in there that makes that particularly difficult to do in JavaScript versus other languages. But at a high level, it was saying let's identify things based on their behavior, not on their source.

**Jeremy:** [00:06:28] And so would that be where the browser would have to load the script.. see how it would affect the DOM. And then based on that, you would determine whether or not this was something that was probably showing you an ad or trying to track you, that sort of thing?

**Pete:** [00:06:43] Yes. The way the project works toe to tip is.. There's these long, long, long lists of things that people previously have identified as being tracking related or ad related those are things like EasyList and EasyPrivacy and the uBlock Origin lists and all this kind of stuff.

And so you can throw those at the web and you get some kind of nice labeled data set of these things are tracking and ad related, these things are benign. So you can run those, execute those files or load those pages and get signatures of how that code operates in the page. And so now you have your ground truth signatures of this is what known bad code does. And this is what known good code does. Then you can run that stuff against a bunch of things that you don't know the labels of and you can rebuild those labels on top of this code that people have examined before. 

And so you can do a couple of things with that. You can either use that to build even more lists in an automated way. You can use it to do code rewriting since some parts are good and some parts are bad. You can use it for online blocking things like that.

**Jeremy:** [00:07:38] You're basically looking at things that people have identified as being bad behavior or tracking behavior. And you can load things that you haven't seen before and use that to instead of having a human curate the list you could have your code load things that it hasn't seen before and figure out.. Oh, this looks like this thing that I've seen before that somebody said was bad. And so I'm going to make a new list based on that.

**Pete:** [00:08:08] Yeah, exactly. For the Alexa 1000 or Alexa 10,000 like the most popular sites on the web, those have a lot of eyes on them. And so things that are tracking related get picked up pretty fast on those. But for the long, long, long tail of the web, that stuff is barely examined or at least, has a lot less eyes on it.

And so this is a way that you can use the the code that people have looked at to identify code that fewer people have looked at.

**Jeremy:** [00:08:32] On a broad sense, how deeply are people being tracked and do you think people are aware of just how deeply they're being tracked?

**Pete:** [00:08:41] So in the first case unimaginably. The amount of web surveillance and offline surveillance that people undergo.. unimaginable. Large amount. And then the second case, very little. You'll find these tools like Brave or the new version of Safari or Adblock plus or any of these.. uBlock Origin.

Good tools by people who are sincerely trying to reduce this stuff. And they'll put a little number in the URL bar and it'll say 10 trackers on this page or whatever. And you'll go to some new site and it'll have 95 or whatever. And that's just the known bad stuff. I think people have very little understanding of how atrocious the situation is.

**Jeremy:** [00:09:24] And what are some of the ways that people are being tracked by their browser?

**Pete:** [00:09:29] Oh. Well. In most cases, the tracking isn't being done by the browser. That's not necessarily the case. Chrome absolutely does observed things about what you're doing and sends it to the Google mothership. But in general the tracking isn't happening because of the browser itself.

But rather by things the browser is loading because of things the web pages tell it to do so. So there's a whole long tail of extremely boring everybody understands kind of things that have been around for 20 years to like more weirdo stuff. 

By far still the most common method people are tracked is just I drop a cookie. I drop a cookie on one site. I fetch the same image on another site. And so the cookie gets resent and that's my way of learning the same person visited site A and site B. 

Web browsers like Safari and Brave will never send third party cookies with a very small number of exceptions. Firefox and Edge have a kind of complicated system for determining when they send third party cookies but do a good job of not sending them to the worst offenders. Then things get slightly more sophisticated.

Instead of dropping cookies maybe what you'll do is throw storage into other places where people don't usually look for it. Right now there's at least four or five different APIs, six different APIs you can use to have persistent storage on the browser through JavaScript. Then there's a whole long tail of ways that things can get cached that also turn into persistent identifiers. That's maybe the second weirdest or second most understood. So then there's a whole bunch of places where the browser is implicitly keeping universal global state that you wouldn't necessarily think about as being a tracking vector, but anytime you have global state, you have the mechanism you need for tracking.

And the most frustrating example is something called HSTS tracking or HSTS cookies. It's an abbreviation for a header that a website can send you that says, Always automatically upgrade this request to an encrypted version, to an HTTPS version, even if I requested over HTTP.

Just in general what would happen is.. I make a request to some website I like, and it's going to be HTTPS. HSTS instructions are not respected over HTTP generally. But I make a request to a website I like it sends back this HSTS instruction that says good. Now that we have a secure conversation, I want you to never ever not communicate with me over a secure channel. So we got this one secure communication. We're going to use this as the kernel of trust to build the rest of our communication over.

And so, that instructs me every time I visit the site again, automatically the browser will know add an S to the HTTPS. And the same thing is true for any sub requests or in general, until people started coming up with counter measures, the same thing is true of any sub requests as well.

**Jeremy:** [00:11:59] If I understand correctly, you make a request to a URL and it tells your browser, in the future you try to go to this URL and you don't put in HTTPS to automatically go to HTTPS instead. And the part that I don't quite follow is how is that used to uniquely identify you?

**Pete:** [00:12:19] Oh, okay. Step one is I make a request to your website it's a secure connection. Then on your website you have 26 different images. You know, an a b c d an e and so my browser will make new requests for each of those images. And those images in this configuration are each hosted on different sub domains on your website.

A image off a.you.com that kind of thing. So now, if those are all requested over a secure channel, your server can decide I'm going to send the HSTS instruction or not for each request. So I'll get back to those images. And, I'll have, more or less 13 new HSTS instructions.

And those will be different for me than they will be for you for anybody else. Just flipping a coin enough times that's like the setting, the identifier step. And then now a week later or whatever you want to identify me again. I clear my cookies and everything, so I think I'm not identifiable but I come back to your site and now you'll have me request the same 26 images, but over HTTP, not a secure channel. And now my browser will upgrade more or less 13 of those images. Your server will look to see which 13 images got upgraded. And now that'll be unique to me versus everybody else in the world.

**Jeremy:** [00:13:28] I see. Wow. So it's a feature that had good intent, but the way that people are actually using it is they're building like a fingerprint right? They know for each URL which one they told you to upgrade to HTTPS and which ones not.

And like you said, so even if you clear your cookies or whatever the URLs that should be upgraded based on HSTS they're still stored in your browser.

**Pete:** [00:13:56] Yep. And so there's a long tail of these kinds of things where they were added to the web platform or to browsers or to the internet infrastructure for largely completely benign or really desirable reasons. But because of the way they've been implemented or because of the way clever people have misused them they become tracking vectors.

HSTS is not at all the only one. It's just the one that is kind of the most galling because it's supposed to be helping people's security and ends up hurting their privacy or can hurt their privacy.

**Jeremy:** [00:14:24] Right. So in the past you were talking about classic tracking that was making use of cookies. and that's something that gets stored in the user's browser. And my understanding is that for cookies in the past, you would go to a site and in order to track somebody while you're on that site you're making a request to another domain, right? To a tracking domain. And as you go from site to site, those other sites use a cookie from that same tracking domain. So that's what you consider a third party cookie. Is that correct?

**Pete:** [00:15:00] Yeah. So I would go to your site. Your site is benign.com your site includes an image from tracker.com. I get the request back from tracker.com. It tells me to save a cookie from tracker.com. I go to some new website, it also requests tracker.com and now tracker.com can link those, those views.

**Jeremy:** [00:15:16] And so now you were saying a lot of browsers like Brave  and Safari and Firefox are starting to block third party cookies. What are some of the ways that sites are working around that?

**Pete:** [00:15:30] So there's a long tail. Some people have been moving to these more esoteric tracking things. So HSTS tracking is one thing that people in the wild were doing particularly against Safari when Safari started blocking third party cookies. They've been moving to different types of identifiers in the browser.

So maybe I don't store something in a third party cookie, but I set a cookie on the first party cookie jar. And then I just append that to my request. So things like Google analytics do that. That's called riding on the first party cookie jar because even though the code is executed by say Google analytics or any number of other tracking scripts. It's actually living in your cookie jar, the cookie jar is associated with your origin. So those are two and then it just kind of gets more oddball from there. 

So there's, browser fingerprinting, if you're familiar with this, which is ways of finding like things that are semi identifying or semi unique in your browser, then build up enough of them. Very quickly, I can identify a large number of people uniquely. It's like, guess who, and you just split the population in half enough times, so that's done extremely commonly on the web. It's very, very common. 

And then there's a new kind of thing called bounce tracking. Not, it's not that new but increasingly common kind of thing called bounce tracking where, Different browsers will only let you set third-party state if you visited them in the first party context. And so websites will play these games where they'll just forward you through a long number of first parties before you get to where you want to go.

And now all these things can set third party cookies on in iFrames and things like that. I could go on and on. There's an endless number of ways these things are done, But getting rid of third party cookies is definitely an extremely helpful thing, but it's not the end all be all of web privacy.

**Jeremy:** [00:17:05] One of the things you mentioned was browser fingerprinting  what are some of the ways that, people's browsers get fingerprinted?

**Pete:** [00:17:12] Sure. At a high level browser fingerprinting is looking for a bunch of things that are going to be different between people's browsers. They don't have to be unique to a single person, but there'll be minor configuration differences or subtleties that are different between my browser and your browser and somebody else's browser.

For example, English is a very common language that's spoken on the web, and so if I know that's someone's language, maybe that identifies me. 1 out of 20 people speak English in the web or something like that. Yeah. Some number that's less than one or less than a hundred, I mean, a hundred percent.

And so then now I've cut out a large portion of the web and now I look at and see, is this person running a Mac? That's going to also cut the search space down. And I look at this person, how many devices do they have plugged into their machine? That'll shrink it down further. What are the kinds of peculiarities of their graphics card when their different drawing operations does it draw a line in a slightly different way than on a different graphics card.

That'll shrink it down further. Does this system have odd fonts installed. It'll shrink it down further, et cetera, et cetera, et cetera. And if you have enough of these kinds of things, you can pretty quickly put a lot of people in a bucket of size one.

**Jeremy:** [00:18:20] And one of the things you mentioned is that you can identify what devices are plugged into your computer and maybe what your graphics card is. What are some things you think people would find surprising about how much your browser is actually sending to the server that you're visiting?

**Pete:** [00:18:39] So it depends on the browser that you're using. But that's a good question. I expect people to be surprised that any webpage that you don't trust this is without a permission, websites can in some browsers enumerate all the devices you have installed, like the labels, the type, this kind of thing.

They can learn about what kind of network connection you're on, whether you're plugged in. If you're in Chrome, the most popular browser you can learn about, the kinds of network errors the person is observing, which can be very identifying if you're moving between networks and they have different kinds of DNS configurations. If somebody has a two factor authentication device, like a hardware key, you can learn some things about the hardware key, like the strength of it.

Even if you wouldn't expect a website can access that automatically. Those are just things the browser is intending for websites to be able to access. That's not like cleverness. That's just like, there is an API that will tell me specifically this. And then there's a long list of other things with a moderate amount of cleverness you can figure it out as well.

**Jeremy:** [00:19:36] I think a lot of people are familiar with the fact that when they go to websites, it'll ask for permission to use a microphone or to use GPS, things like that. For some of these other things that you're referring to, that it's able to figure out such as your, your devices that are connected, things like that.

Is that something where the person is giving permission or is that something that just just happens?

**Pete:** [00:19:58] Yeah, so that, that just happens. So I represent Brave on the W3C and I co-chair, one of the privacy groups on the W3C, the horizontal review group that reviews specs for privacy. And that's something that we're working with the working group that authors that spec, the media and capture media streams capture group to improve that API.

But that is just the way the API works in the standard right now. The website, says.. tell me about the devices the machine supports. It gets back a list of every device that the machine knows about that has like an AV component. And then the website now says, okay, I would like to access this one.

And then you get the permission dialogue. But without any permission you can learn all the devices and all the labels and the categories and this sort of thing. I should say that the spec looks like it's getting much better. That working group has been really, it has been good to work with and it's been, been really receptive to those concerns, but that is that's the way it ships right now in Chrome, Edge, Brave makes some modifications to it. I don't know about the other ones, but that's the way the spec standard is written.

**Jeremy:** [00:20:59] And that's interesting because you're saying the standard  is currently being written but a lot of these different browsers, they already have an implementation of it.

**Pete:** [00:21:09] Yeah. So this is another one of those good intentions that have turned out to have an unintended consequences kind of situations. So it used to be the case that you're running a web standard. A bunch of people would get together and work on the standard. And then when it was done, people were supposed to implement it.

And then, this is a rough history. I'm sure I'm going to get some of the details wrong but to a rough approximation something like CSS2 happened where you ended up with a standard that was basically unimplementable and it had all these kinds of subtleties that hadn't actually been worked out because nobody had implemented it yet.

There's other cases too and CSS2 might not have been the tipping point but it was definitely a famous example. Then there was a CSS21 standard that came out when people started implementing it, it had to get revised in certain ways to make it actually work in the world.

Hand-waving simplification, but people thought this is not great. We need to like, actually build these things as we're talking about them, to make sure that they work in the world. And so then you got into this kind of like prefix situation where I don't know if you, if you do.

If you're a web developer, you'll be familiar with like, until pretty recently, you had all these pre-fixed extensions like rounded corners, but WebKit rounded corners, and Microsoft rounded quarters and Mozilla Yeah. And you had similar things in, in the DOM.

And there's still some hangover at where a bunch of specs in most browsers  are implemented twice. Once WebKit prefix, things like that. And so understandably people thought this is not great. Now I have to write my code four different times. And so, right now, if you're trying to get a standard finished in the W3C, I'm less familiar with other standards organizations, but in the W3C, you need to have two working implementations, two independent implementations.

They don't necessarily need to be shipping like unflagged like the way it's supposed to work in the best cases like they're running in the browser and there's some flag that you flip or it's only enabled for some set of websites, but that's not always the case. Things are getting shipped as they're being designed in the standards body absolutely is like a little bit begging the question right? And that if you find out there's a problem during review with the spec well, now a whole bunch of websites have already started depending on that certain functionality and have it baked in that is a real pickle and something that we fight with a lot during these reviews. But, yeah, that's, the less than ideal situation that things have come to at this point, I think it's getting better, but that's generally how things are done right now.

**Jeremy:** [00:23:20] That's kind of interesting because it sounds like you have the W3C and you're planning on things that will go into the browser, but in order for them to become a standard, they need to already be in the browser. Which also means, like you said, that people are already using them. I wonder what is the negotiation or the back and forth in terms of, let's say Chrome is already using a certain feature and you say we'd like you to change this feature for this reason.

They'll say well, we already have thousands of sites that are using this. how are we going to change this? What does that, that back and forth look like?

**Pete:** [00:23:59] Yeah. So, the first thing to keep in mind is that the standards body is not a legal organization. The standards body can't make anybody do anything, they can say something's out of standard. They can remove it, but people listen to a standards body if they want to listen to a standards body and they don't, if they don't.

So in that sense, a standards body works by trying to make it mutually beneficial for people to go along with it and providing resources that maybe an organization wouldn't have if they weren't in the standards body and some benefit in terms of interoperability, that sort of thing to strengthen the platform in general.

So that being said, there's not an easy answer. Sometimes you can find clever games you can play with the way the existing APIs work that will reduce the amount of information exposed but without breaking the function signatures or the expected flow of the program. There's several different tiers of review in the W3C and some happen earlier than others.

What we've been trying to do is push review earlier in the process to try to catch these things while they're still in prototype stage, instead of, web scale stage. But yeah, there's no way that the standards body can go to mr and mrs. Google and say, you must do a thing or, Mr. and Mrs. Apple or whatever else. Unfortunately that's just the case.

**Jeremy:** [00:25:13] And you were saying, how you're the co-chair of the privacy interest group on the W3C. How much power would you say that that group has? Do you have examples of times where somebody has tried to push a feature through and you've rejected it on the basis of privacy and there's actually been changes made or the feature has been dropped all together?

**Pete:** [00:25:39] I should say in terms of power we're a subset of the W3C and the W3C at the end of the day has, the organization has maybe some moral authority or some, you know, people respect it. And so there's some soft in quotation marks power there.

And there's a lot of expertise that people respect in the W3C. And there's a lot of mutual interests between the browser vendors to have a web that is friendly for developers and friendly for users. So, there's no authority, but there is, web browsers are interested in sometimes what the W3C has because of these other reasons. So power is a funny word to use there through I take your point. 

To point out very specific changes that have been made. I'll talk about the WebRTC one the enumerate devices API, because that's the one we just mentioned before, so right now, partially because of interest among people in the working group, partially because of reviews that PING has done. PING is the privacy interest group. There's both immediate changes that look like they're going to go into the API.

None of this is a hundred percent. This is all in the GitHub issues right now. But this is the direction it looks like things are going, best guess. That there'll be a number of ways of shrinking the amount of information that websites can access by default. So it's things like, without a permission, maybe you don't see this person has 18 different microphones.

They just see there's at least one microphone. And then when the website asks for permission then they can learn about the number, the details, things like that. So that's a wonderful thing. I think the working group would agree that it's not the dream outcome, but it's dramatically better than what was there earlier.

And then we're also working with the working group. They're doing great work in terms of figuring out like where can we go to that's even better? And so that looks like it'll be the website doesn't see anything by default. If the website wants to see devices, they call a thing, the browser prompts you with a list of devices.

And then if you want to, that information gets passed. that's a example that comes to my mind. There's a long list of if it's of interest to your listeners too. I could also point you to the endless list of privacy issues that we raised and the back and forth that happens on them there.

But sometimes they're very large things like that. Sometimes they're very small things like you're leaking fingerprinting bits here and let's figure out a way to sort through that.

**Jeremy:** [00:27:44] One of the things I find interesting about your position is you work for brave, which is a browser vendor, and you have Microsoft with Edge. You've got Google with Chrome, Apple with Safari, and Mozilla with Firefox. And I would imagine that all of these different companies, they all have their own goals.

They all have their own things that they want. I wonder from your perspective, what are the kinds of roles that each of these companies play and where do they butt heads and where are they on the same page?

**Pete:** [00:28:19] I want to say things that I'm only very confident about. All these organizations and particularly the people that are sitting in these committees and these working groups that represent these organizations have an interest in the web.

They see there's something unique about the web that that is appealing and desirable and positive. That's not on other platforms. They may not a hundred percent agree on what those positive things are, but there's something that appeals to us about the web that doesn't exist on other platforms.

And so there's mutual interest there. I also think that all these people care about privacy, they care about making sure things are accessible to people with different needs on the web. They care about making sure APIs work well for people who speak different languages and come from different backgrounds and these sorts of things.

At the end of the day, people who choose to spend their time in these long meetings working with each other.. We have very similar interests and we're all pushing the same way. Where they differ is the prioritization of those interests. Brave is absolutely like, we think there's something super duper wrong, like kind of fundamentally wrong.

Yeah. Maybe that's too strong, but the web has really gone sideways and the privacy violations are endemic and really horrible. And like intolerable. I think other people would say, yes, privacy violations are bad, but also we want to make sure that we don't break the ecosystem that exists to fund the web as it exists today.

And so that's like privacy is just one among many different interests, including making sure advertising dollars self fund websites and things like that. And then I think there's other people who exist in other parts of that, on that spectrum and have different interests.

So I think we're all pushing the web in the same direction, are interested in making sure it flourishes, but what flourishing means probably differs between different people in different organizations.

**Jeremy:** [00:29:58] Something that sometimes comes up and maybe it's a little more front of mind because Apple's worldwide developer conference happened recently is that people have a perception of Safari not implementing a lot of features that other browser vendors either implement or want to implement. 

I think a lot of times they say that they're doing it in in the name of privacy. And on the other hand, you have developers who are saying, Oh, we want all of these different features because we want to be able to build a progressive web applications. We want to be able to build a websites that are similar to apps.

And I wonder from your perspective, how do you balance these two goals?

**Pete:** [00:30:40] So I think that's a really interesting example you brought up for a couple of reasons. I bet we're thinking about the same tweet that went around and the same people blowing off steam, and I can totally understand their frustrations. But I should say two things first before going into the guts of your question.

One is that, most of the things are not standards they are proposals. And so, as much as the web community, we like to treat them as standards because they're implemented in the popular browser. They are not standards, nobody's agreed to them, blah, blah, blah. They are proposals. Second thing is that, I think there was 16 or 17 or 18 different things on that list.

I don't remember the full thing, but I remember looking through it and thinking Brave takes the additional step of removing these things from chromium before we ship Brave. I am completely sympathetic to the idea in the vast majority of those cases, maybe all those cases, I just don't remember the full list that those are really privacy risking features.

And the permissions models around them are not well-defined. They haven't been well reviewed and the risk is really significant. Look, Apple's got more money than anybody knows what to do with Apple. Apple's not, not implementing cause they're lazy. They may be pursuing a different strategy.

But I also know that the people in those committees have sincere strong, heartfelt interest in privacy. So I understand the frustration of the web community, but I find the privacy story there compelling.

**Jeremy:** [00:31:58] And I think it's also maybe important to think about the fact that as soon as you put those into the browsers, it's going to be extremely difficult to remove them.

**Pete:** [00:32:08] Yeah. I mean the web congeals around any features that gets there. And the moment you put something in it becomes extremely difficult to pull it out. Something that we deal with at Brave a lot, because we think that the way a lot of APIs work is inappropriate and intolerable and we have to be very clever in the kinds of ways we can modify behavior that websites already expect to exist in a certain way.

**Jeremy:** [00:32:32] I think I know about the tweet you're referring to, and I don't remember all the specific features but, I wonder from your perspective, are these features that you think shouldn't exist or is it more that the way that people want to implement them now wouldn't be done in a privacy conscious way.

**Pete:** [00:32:50] Hmm, that's a good question. So I also don't remember the full list, but I can pull off some examples.  I think there's kind of three tiers. Some things just seemed like bad ideas that we should just not do, or at least not do without pretty fundamentally rethinking how they exist.

Some of these things are things because they make more sense as operating system features or native app features than they do websites. And some of these things, are things that, yeah maybe those would actually be very useful on the web. If we could figure out how to do them responsibly.

A lot of this stuff has its roots not in things that typical websites need to do, but like the union of a bunch of weird things that happened. One is like Firefox OS happened for awhile. And so a bunch of things got pushed into the web platform some of which got yanked out later, ChromeOS is another one, PWAs, things like this. 

And a lot of these things are really different from what we think about as websites. It's worth thinking about where are those lines and should they be firm or that sort of thing. A while ago, the example that sticks out of my head is there was a standard that got shipped in Gecko in Firefox and Chrome that allows websites to read the amount of ambient light in the room. 

The website could read it's very bright, it's very low, I don't remember the granularity, but any step in between. And of course the very first place this stuff got used was in tracking scripts to fingerprint people. Same with the battery API, there was an API that allowed websites to say, it's a full battery, low battery, that sort of thing.

You can imagine why that'd be a nice feature in an app. But you can also imagine it gets sucked into the fingerprinting scripts immediately and starts harming and targeting people. And so yeah there's definitely a part of the web that says let's just permission prompt everything, or use a number of different kinds of proposals that concerned me to restrict this stuff or allow it on the web in a responsible way. The web as it is without adding more functionality has so many deep privacy issues. I feel very nervous about pushing for new functionality unless privacy is really treated as a first class citizen in those standards.

**Jeremy:** [00:34:56] Yeah. And it sounds like where we're at now.. There's already so many different ways that you can be fingerprinted. And every time a new feature is added to the browser, it just gets more and more easy to track someone. 

**Pete:** [00:35:11] Yup. I think that's exactly right. And there's also cases where adding a new feature undoes a privacy protection somebody else has added in somewhere else. It's good to be very cautious before throwing new powerful features into the platform.

**Jeremy:** [00:35:23] Another thing that you had mentioned when we first talked about doing this interview was you had said that Brave is based on chromium. And you said that you had a somewhat semi adversarial relationship with upstream chromium. I wonder if you could elaborate on that?

**Pete:** [00:35:44] Sure that was kind of a silly in a goofball thing that way to put it. That's that misstates things too strongly. The chromium developers have been very receptive to questions that we have. And we've tried to upstream stuff we found to be a positive experience. 

But there are things where the vast majority of Chrome developers are Google employees. And of course Chromium is shipped in a lot of ways with Chrome in mind. I don't think it's a malicious thing, but it is the case and so there's a whole lot of stuff in the chromium code base that assumes Google. Which servers get talked to and account information stuff, and safe browsing things, and an incredibly long list of stuff that is just in the chromium code base but assumes Google including, and this is maybe this is what I had in mind when I said adversarial. Poor choice of words. There's a couple of features that Chrome ships that allow you to basically enable a feature only on certain origins and they call it field trials, this kind of thing.

So if the chromium folks want to test out any feature they can say only these three or four or five or whatever partner websites can use it. Sometimes that feature gets shipped, they'll ship a feature ungated, not flagged. And then they'll use this feature to turn it off.

So they'll ship some new experimental feature and then they'll say, but we're not gonna allow it on any sites. The field trials is zero or is empty. And so that's their way of making sure that sites don't get it. Well, if you're building a browser that wants to put firm lines between itself and Google data collection servers you don't get that information.

And so now all of a sudden, the weirdo experimental feature is enabled globally in Chrome or in your version of Chromium. A long list of things like that. There are also other choices in the platform that makes certain things that we would like to do difficult. I could go on those examples if it's of interest. I don't think that's adversarial that was a silly choice of words. But it does mean that there's different interests being pursued in the code base that are not always Brave's. It's not always as privacy focused as Brave, would like.

**Jeremy:** [00:37:40] I'm not sure if you would have an answer to this, but, when Brave was deciding, what rendering engine to use whether that's, Chromium's Blink or WebKit, or something else. Why, why make the decision to use chromium as a base?

**Pete:** [00:37:57] So this predates me at the company so I can only think through some of these things. I don't want to say something I'm not sure about. The early Brave folks considered a bunch of different engines and  Brave started as an Electron app. So basically when there is an extremely small number of developers at the company and it's extremely early days it was just everything was done on top of stock chromium. It allowed the company to iterate really quickly and try a bunch of new things and do some of the kinds of things that it knew it wanted to do that were easier to do at that level. Then trying to maintain a large patch set in this kind of stuff against Chromium.

And there's probably some path dependency on that. We're no longer an electron app. We're a proper chromium project. That's part of it. I don't know the particulars of why Electron was selected and not a Gecko option or not a WebKit option. I couldn't say exactly what tipped the scale on one versus the other.

**Jeremy:** [00:38:46] Something you mentioned was that private mode or incognito might be something interesting to talk about so could you elaborate on what you were thinking there?

**Pete:** [00:38:55] Like the battle of what like private browsing mode is and the incognito mode is and what that is supposed to do is I think nobody has a single story for what it actually is supposed to be.

In some browsers that basically means your storage doesn't persist after you close the browser. And that's all it means. The browser operates exactly the same way. Local storage operates the same way, et cetera, et cetera, except you have a separate cookie jar and a separate set of state that goes away when you close all your private browsing windows.

That was for a long time the textbook definition or the whatever was agreed on. But you can see over time in standards bodies and in implementations.. I think there's been some recognition that users have a different understanding, or at least some users have a different expectation of what private means.

And it can connotate something beyond just the state goes away. And so there's been a slow drip of new features. New privacy features into private browsing windows and major browsers. So Firefox by default if you enable a private browsing window you're in strict versus default mode for intelligent tracking protection, it does slightly different things.

Chrome changes the operation of some APIs that allow you to query your quota on storage to prevent sites from detecting whether you're in private browsing mode, et cetera, et cetera, things like this. But I think it's interesting because it seems like a recognition that users want more privacy in a machine and are desperate for whatever buttons are in front of them.

Even if what guarantees are being made by those buttons aren't totally clear.

**Jeremy:** [00:40:26] Yeah, that's a good point because when I think of private mode or incognito mode, I think of your first example where it just means that it's going to clear whatever was stored on the computer like cookies or your history, things like that. And what you're saying is that now the opinions have shifted to where maybe private mode should be blocking trackers or maybe it should be... I think the example you gave was preventing sites from finding out certain things about your computer or your browser. That's a perspective that I didn't realize people thought but that makes a lot of sense.

**Pete:** [00:41:05] And maybe this is a positive thing. It's become a little bit, eh, I'm not sure that's true. My impression I wouldn't go to war over it is, is that it's a little bit of testing ground for people to say, we know less people use private browsing mode than the typical mode.

So we can be slightly more experimental in the kinds of features we test out in private browsing mode for privacy related features. If that's the case, then it means more and more stuff gets turned on by default over the medium term. I think it's probably a good thing for the web

**Jeremy:** [00:41:34] One of the things that you had touched on earlier was when you're trying to preserve privacy, when you have features that are blocking certain things that could be used to track you or block certain features in the browser, one of the side effects of that is that it can break websites.

What are some, some common examples of where that can happen and how are, you know, you have brave, but browser vendors in general trying to to work around that?

**Pete:** [00:42:04] Sure. So the most common or goofball way that can happen is say, you're using some ad blockers you're pulling in some filter list and it says you should delete everything that says, Ad in the URL or whatever, right. /ad/ something like that. Some website for whatever reason has something that's not an ad in a URL or something like that.

Right now you're blocking something you don't intend. And there might be a script the page depends on for its execution. And given that the size of these filter lists, given that you could easily be considering hundreds of thousands, maybe even 200,000 rules if you're using a tool like Brave or uBlock Origin or something like that. The possibility for false positives is very high. So that's the simplest case that can happen. But then it gets more complicated. Brave by default blocks third party storage by default, there's a very extremely small number of exceptions that we make to unbreak websites.

But by default we just block all third party storage. So if you're in an iframe, you don't get to store stuff, you don't get cookies. If you're a third party request, stuff like that. And, the vast majority of cases that works just fine.

People don't usually care about the stuff that's going on in iframes on a page and when they do it doesn't usually need to touch storage, but you can imagine some places that'll break. Someone embeds a video and that video wants to store it's state or something like that.

That requires some cleverness in dealing with it. And then just a third example. Like when COVID started becoming a popular concern is that people want to look at maps and see where COVID was spreading. And so these sites would usually use things like, either rendering these maps via SVG or be a canvas operation, and brave, by default did no, no longer, but at the time was blocking certain canvas operations and SVG operations because we knew they were being used by fingerprinters. And all three of those cases have privacy protections that ended up breaking things that at least in these cases are privacy harming.

Probably even more so than my job doing privacy stuff at Brave is figuring out how to do that privacy stuff in a web compatible way or how to break less websites so people can use Brave without having to drop shields and drop those protections. And so each of those different things warrants a different response.

So one has been to adopt a strategy that the uBlock Origin project takes. The uBlock Origin project is fantastic and all credit to those folks. That project, it is really fantastic work.

Instead of just guessing, yes, I allow the resource or no, I block it. They'll also sometimes say replace it with some different thing that maintains the API signatures, but it actually nulls out the tracking behavior. And so that's been a really useful approach for unbreaking websites. 

If we can figure out what they expect, like the functions they expect to be in place but replace them with less painful stuff. And I can talk about our research project if it's of interest over the summer, actually with the student, Michael Smith, the student who's visiting from UCSD to leverage this, if that's of interest afterwards,  

**Jeremy:** [00:44:56] Are you replacing something in the JavaScript code that's running or are you replacing something that some browser API that is trying to get access to?

**Pete:** [00:45:06] Sometimes, sometimes both. So in the simplest cases like Google Analytics provides some functions or like triggered some events on load. And if you block Google analytics, it means some things will never load. And so instead of blocking Google analytics, You just, you say, here's the request for Google analytics.

Instead, I'm going to turn this thing that does nothing but trigger a load of it, but actually it doesn't touch network or anything like that. And so you're replacing the resource instead of requesting it. But you might also do things like, I see that some code that does something nasty or is inline so I don't get a chance to modify the request. I see it's inlined, so I want to somehow modify its behavior. And so I'm going to.. I mean, sometimes this stuff gets really gross, but I'm going to say overwrite some structure, the page expects to be there. I'm going to throw a stack trace. I'm going to look up and see if I'm in the inline code.

If I am, I'm going to take path a and otherwise I'm going to take path B all these kinds of gross things. The web is a messy place and there's a whole bunch of tricks like that, that have to get pulled. So we pull a bunch of that stuff from the uBlock Origin project, we generate some of our own, for fingerprinting stuff.

And this is something we've been able to pull from research that I'm really proud of us shipping, or I'm really glad about is in the same sort of way that uBlock Origin said it shouldn't just be yes or no. We should have some middle road that allows us to be more clever.

We've taken the same approach of fingerprinting protection. So instead of just saying yes, it's allowed or no, the API goes away. We now do something we call farbling where we break the assumption that websites have that.. That the features are going to operate in a fixed way across browsers by adding a little bit of noise to the API response.

So, if you're doing some canvas operations we'll with very low probability modify a pixel here or there or flip a bit like the lowest bit in the color channel for a pixel, that kind of thing. So instead of just blocking the API to protect people, we can instead have this more web compatible way where we still all the APIs do work, but we remove its identifiability by having it always do something different between sites, between sessions.

Something that we're working on right now. And we actually are working with a student from North Carolina, who's prototyping this for us over the summer. This is another research intern named Jordan Stock who's doing great stuff. We're looking into a third option for local storage for remote storage.

So instead of a frame, either yes. getting storage or no, not getting storage. We want this middle option where we can say the frame gets what looks like normal storage for the execution of the page. But by the time the top page for the top frame is closed, then that storage goes away. A lot of this stuff is just figuring out ways like the web compatibility game is, is figuring out a bunch of ways of breaking the binary choice and figuring out ways of sneaking more cleverness into the platform.

**Jeremy:** [00:47:43] So when you're referring to a frame and the local storage going away could you kind of elaborate what you mean by that?

**Pete:** [00:47:50] Oh, sure. So I'm on a website, like a typical website. you have your one frame, which is just this document object. And there's a bunch of like DOM structure that hangs off of that. But, one of those things off it might be an iframe, which is itself like its own contained document structure.

And that can be infinitely recursed or infinite. It can happen infinitely deep. And so, this is usually referred to as the first party and the third party. Or the first like the local frame and the remote frame. There's some overloading of terms. Because, yeah, some browsers like remote frames are also remote processes, in the way that an operating system understands.

But, typically yeah, the local frame is a frame that has the same, ETLD plus one, which means effective top level domain plus one, which is like the level of domain that you can register if you go to hover or whatever. And so all the frames that have the same ETLD plus one it's the top frame or local frames, anything else is a remote frame or a third party frame.

And so browsers will use this as like a.. some browsers will use this as a heuristic for saying local frames the user trusts. And so I'm gonna allow it to store cookies and local storage and this kind of thing. Remote frames deserve less trust. And so I'm going to block storage or I'm going to partition storage or I'm going to do something possibly clever with storage, not all browsers do that, but it's a increasingly common.

**Jeremy:** [00:49:05] I see, and I think you were explaining how you could have let's say an embedded iframe and it could use browser local storage, but maybe as soon as you click to another page, then that local storage goes away. Is that kind of what you were...

**Pete:** [00:49:22] Yeah. So that's the approach Brave is taking. So there's another privacy group in the W3C called the privacy community group, which is, kind of like the sibling group to the group I co-chair. So I co-chair the review group that reads everybody else's specs and tries to improve the privacy of what other organizations or what other working groups are working on. Privacy CG is where browser vendors go to introduce new features. And so brave is involved in both. There's a lot of overlap between the two. 

**Jeremy:** [00:49:50] earlier you were talking about how people could be fingerprinted. They could be identified by seeing how things render, whether that's on a canvas or SVG and what you were saying, the way that you were dealing with it, which I found was interesting is it sounded like you were adding additional information. So your video card might render something a certain way, but then you would add additional things that would make it render differently than the video card normally would. And that's how you would remove that as an identifying factor. I wonder also, you were mentioning about how you had a research project at UCSD and I didn't quite catch what, what exactly that was.

**Pete:** [00:50:35] Yeah. So in that order, the first one, the adding information parts, this, this approach came out of two research papers a while back. One is a paper called Privacator led by my current boss Ben Livshits who's a professor at Imperial in London. And the second paper was a paper called FP random fingerprint random. 

Both of those things introduced this technique or played with it. Brave is the first one who's productized it or included it in a popular shipping browser. But yeah the approach is to break the assumption that there's something unique about this browser that I can identify across sites.

And so we randomize some of these features or we add an extremely subtle amount of noise that'll confuse fingerprinters, but look indistinguishable to users. We do it in a way that's random, but deterministic under each first party under each session. So you close the browser, you get a new fingerprint and if you go to a new site, you get a fingerprint.

And so that prevents things from being linked. So it's been a nice way of taking academic research and figuring out a way to use it for a shipping, privacy protection.

**Jeremy:** [00:51:36] Cool. So that was something that, in your role at brave or I guess brave as a company decided that this was something to look into from a research perspective. And then because the research went well, you're able to move that over to the product side.

**Pete:** [00:51:50] Oh, well, I wish that was the case. I mean, so these are papers that preexisted at brave. It was a situation where we knew we had a problem. Most sites were breaking because of our fingerprinting protections. We didn't want to leave people less protected. And so research was one place we could start digging for a solution. 

So you asked about the project at UCSD this summer. There's a student who's visiting, Michael Smith, he's a fantastic student and a fantastic hacker. And so his project is, I mentioned before about the way uBO, uBlock Origin does these resources replacements. And so as you might imagine, these things are very difficult to generate. They take a lot of stepping into the debugger and manually figuring out how these large JavaScript blobs operate, particularly what, like what subset of the functionality you need to maintain to unbreak the pages. Extremely tedious and doesn't scale, it doesn't scale well. And so the approach that Michael and I are working on, Michael's doing the hard work. Is to see if we can automatically generate these things through a combination of browser instrumentation, a system we call page graph, which allows you to deterministically offline see the interaction of different elements of a page, 

AST analysis... AST is the abstract syntax tree or it's, it's a parsing step in, in executing JavaScript, or, parsing any language and then code rewriting to identify the parts that are privacy harming, rewrite, just those parts. And then we can programmatically generate these, these privacy preserving resource replacements in a way that can be automated instead of requiring the heroic amount of manual intervention that they currently do.

**Jeremy:** [00:53:23] So if I understand correctly currently when you use something like uBlock Origin and you go to a website and let's say that website loads a script that has privacy implications, has some issues with tracking, but the behavior is still needed for that website to work. uBlock Origin will replace parts of the JavaScript source code so that the site still works. But it blocks whatever kind of tracking behavior that it was going to have. Is that correct?

**Pete:** [00:53:53] Yeah, it's not that it fetches the resource and then does some rewriting on the fly. It just preloads like, this is the privacy preserving version of the Google analytics script, this kind of thing. Brave does the same thing. By the way, we had someone who worked with an intern last summer, Anton, who's now a full time employee at Brave and is phenomenal.

But yeah, brave does the exact same thing out of the box. So we preload all the same resource replacements and are generating our own and do this in the same way.

**Jeremy:** [00:54:23] And then in the research project that you're currently working on, the goal is for, the browser to be able to load these third party scripts and on the fly figure out if there's something, that should be blocked or changed in the script is, did I get that right?

**Pete:** [00:54:41] That's mostly it, so it's slightly different than that. And the reason it's different is that, so JavaScript because it's so dynamic, it's difficult to statically analyze. You have to execute it and see what it actually does in a lot of cases to deal with all sorts of corner cases or all sorts of aspects of the language, because things could get aliased and functions get bound and there's dynamic code execution through evals and stuff like that. 

And so the difficulty there is you hand me some Javascript. I can't reason about it in a fundamental way about saying these are the seven places to where it's going to write a cookie or do a network request or touch your local storage or whatever.

So that's one problem there. And the way we solve that is we have this heavily modified version of Brave that we call page graph, or that includes a feature we call page graph that allows us to among other things say, okay, these are the 18 parts of the JavaScript code that actually ended up touching local storage or doing a network request or whatever else.

And so we use that for de-aliasing the values of JavaScript then offline we can, once we have those, we can programmatically rewrite the code by analyzing where those places are and replacing those lines of code or those chunks of the file with privacy preserving alternatives.

And then at that point, we have our resource replacement automatically. So the process is offline and that we call the web and we will generate a whole bunch of these things beforehand that we can preload them in brave browser in the brave browser, or share them with the uBlock Origin project or anybody else.

But the appealing thing is if we do all this work over the summer and this research project is successful, which I think will be, we have a way of automatically doing the stuff that before it would take an extreme, a pretty awesome amount of manual, labor to do.

**Jeremy:** [00:56:28] And so it sounds like you have this special version of the brave browser and you could automate it to visit a bunch of websites. Pull all the scripts. And see what it does to the page. And then basically give you a list of, Hey, these are all the scripts that we think have issues.

And we saw what it did, and this is the part we need to remove or change. And then you can ship that to users, either in uBlock Origin or in the brave browser itself.

**Pete:** [00:56:57] Yeah. That's exactly right. And so most of that stuff already exists through fantastic tools that people like Google have made, puppeteer is a really fantastic system that Google has made that allows you to automate  browsers and interact with sites and understand what browsers are doing.

I mean, it's phenomenal, but it also doesn't answer all your questions. It's very difficult using puppeteer or using any system to understand this script modified this file. And that file then requested this image, and that image, whatever, you know, these complicated chains of interaction.

That's extremely difficult to understand online in puppeteer or particularly after the fact just looking at the end result of the page. And so page graph is this system that allows us to with extremely high fidelity trace every single one of these operations in the page and then stitch them together in a graph in the sense of like edges and notes, not as a PDF.

**Jeremy:** [00:57:49] Yeah, I think that's really interesting because I know one of your other, papers or presentations you have talked about Easy List, which is the list of trackers and ads that uBlock Origin and a lot of other systems use to decide what to block. And that sounds like a very time intensive process of you have all these different people that are visiting sites themselves and figuring out like, Oh, these are the things that should be blocked.

Whereas with your research now, it would be more like we could have just the computer go and browse the internet for us. Figure out what needs to be blocked and save a lot of time in the future in terms of figuring out what we need to block.

**Pete:** [00:58:33] Yeah, I think that's true. Although two complications there. And first I want to say that.. So EasyList is a fantastic project in there's a bunch of unrelated child projects. So there's EasyList. There's EasyPrivacy. There's a bunch of regional region specific EasyLists, this sort of thing. and, one the core maintainers of EasyList, who goes by the online handle Fanboy, is part of our team at Brave.

He's fantastic. He's a full time brave employee and his job at brave is to maintain filter lists both for Brave, but also to benefit the larger community. And so things like Easy Lists are on one hand, phenomenal, like  I think people just completely under appreciate how much there's four core maintainers of EasyList. And without these four people doing the things they do the web would be an infinitely more miserable place. And like the fact that like the web hangs on the evening, like the after hours jobs that these people have, until, at least until recently when they started being supported commercially is totally under appreciated and fantastic.

Those lists are also deeply imperfect they're full of heuristics. Like the ad example, like /ad/ examples. There's lots of heuristics, there's lots of stuff that gets broken. And there's lots of, in quotation marks, dead weight or rules that were useful five years ago, but now it's very difficult to know if they're still useful given the size of the web.

And so, it tends to just amass rules over time. None of that is the criticism of the maintainers who are fantastic or the community around them that contribute lists, but just the nature of the beast. Brave's approach. And some other researcher's approach has been to can we use these labels that these people have generated as high confidence things to start reasoning about the rest of the web.

So it wouldn't be a replacement, EasyList. You still need some human in the, in the cycle somewhere to make some of these assessments, but can we like force multiply what that person is able to do through automation or machinery or, machine learning or, you know, different types of, of, of tooling.

**Jeremy:** [01:00:24] Yeah, that makes a lot of sense. I thought it was really, surprising how few people were maintaining such a gigantic list. Like I think, you had said there were something like 300,000 entries, or I don't remember how many entries were on easy list, but it

**Pete:** [01:00:41] I think it's around 75 or I haven't looked recently. I know that Ryan's been doing some cleanup, but close to a hundred thousand in just EasyList. I think it's 70 something. And then there's EasyPrivacy and there's, you know, a long number of other lists too. So yeah, I couldn't tell you that the concatenated size, but large, very, very large.

**Jeremy:** [01:00:58] So you've been centered on the privacy side and the tracking side. And I wonder in your work, if you had any visibility on the people who kind of want all these things to happen, like the advertisers that want to be able to do the tracking, has this sort of tracking actually been really effective for them. And on the flip side, I wonder how much of these ads are even being seen by real people? Could there be ad fraud going on in terms of computers are just looking at these ads? And we're not the ones looking at these ads.

**Pete:** [01:01:37] Yeah. We're now stepping something out of my area and quadruple ironic quotation marks expertise. But I can, I can only share what I know, or my impression from working, doing what I do. Which is that yeah, absolutely. Fraud is completely endemic.

To the degree that people have no idea how much it is, but numbers that I've seen up for online ad fraud are anywhere from 10 to 50%. These are not numbers. You shouldn't hold me down to, but, but simply to understand the magnitude of the problem, like enormous and in the number of like middle players, that are in these markets, make it extremely difficult for any one party to understand what's going on. 

There's a phrase that gets thrown around called the Lumascape. And after this call, I can try to find you an image, but it's, it's this kind of like 18 step deep, like flow chart of how advertising markets worked. And that was five or six or seven years ago when that image was made.

But yeah, these they're extremely dense. And the vast majority of players in the markets you wouldn't recognize their name. Nobody would recognize their name unless you were an employee of that company. So, yeah, ad fraud is an enormous problem. And it doesn't seem like there's a way to, it's going to get better anytime soon.

Like this system seems like it's definitely on its way out and kind of getting worse. One thing that's really neat about Brave is that a number of the people who work at Brave have like histories in ad tech markets playfully have said they're repenting for... their work at Brave is their apology for what they did earlier.

One person who works BizDev.. Luke is like just a phenomenal dude and incredible at what he does, but he used to work in doing this kind of stuff, in terms of like helping to build tracking systems and understanding how they work and now, yeah, Luke, Luke is fantastic. Johnny Ryan is somebody who does policy work at brave, too.

He used to work at PageFair. He talks a lot to enforcers, like people on the political side, who do like, CPAA and, GDPR kind of things to make sure that regulators are actually enforcing these things. And his sense is that just the amount of fraud and the amount of tracking is, is, is just unimaginable.

And so, and so, yeah, the problem is, is well established. In terms of whether it's actually profitable I'm sure that's like very deeply debated. So I know that Google has some numbers that have said that if you remove like the behavioral component from tracking, you need to do just contextual tracking, so, or contextual ads.

So ads that know like where they appear, but not who their who's looking at them. Their numbers suggest that like the profits dropped by like 50% something along those lines. I don't remember the exact numbers, but, something on that magnitude I know some people are extremely skeptical of those numbers. And of course has Google is not an unbiased actor, but those are the numbers that they've shared.

And I know that these numbers on the other hand, that, that get pointed at you that says,  The amount gained by, marketers in the, and people who are placing ads, is negligible negligible to negative, when you removed the, behavioral compo component, because, there's so much fraud in the market that they ended up, like behavioral tracking actually ends up having a negative return.

So, so all that is to say is I, I, I deeply don't know. I know that the system relies on things that seem abhorrant to me, but, But there's a diversity of opinions. whether it's actually useful or useful for what it claims to do.

**Jeremy:** [01:04:45] From site to site, the sort of effectiveness in terms of the ads, you see how relevant they are, it can vary really wildly right. And, and we're never really sure Why certain ads are being shown to us. Right.  you know, the example that a lot of people will give is, on Amazon, right?

Where you buy something and then all of the suggested items are like, for the thing you bought and people kind of joke like, Oh, you know, this targeting isn't very good. But on the other hand, you have platforms like Instagram, where I've heard that the advertisements on there they're actually very effective.

They tend to show people things that they actually might be interested in buying and they actually go through and click. But it's interesting because like I was saying, I don't know why some things seem effective and why some things don't. It could be that they have tons of tracking information and they still do a bad job of what they show to you.

**Pete:** [01:05:44] I had the same uncertainty about this stuff. I imagine that, I mean, I shouldn't hazard a guess. I honestly don't know, the usefulness of these things, I'm, I'm really dubious or I'm really uncertain about it. I doubt it, but I couldn't say confidently that it's definitely not the case.

And I've heard the same kind of success stories and the same kind of, you know, catastrophe stories too. Two things here. One is that there's, This might be of interest. There's this kind of famous story of not success of tracking, but  the harm of it. I can send you a link to the story if it's of interest, but there's a famous case of a family getting advertisements from target.

These are paper advertisements from target. So the family starts getting advertisements sent to them for prenatal kind of stuff, cribs this kind of thing. And the father doesn't understand why this is happening and the parents don't understand what's happening.

It turns out that the daughter is pregnant, and has been looking up information about how to take care for the expected child. And advertisers knew it before the rest of the family knew it. Anyway. So, I guess that's a story where maybe it was effective, but also morally reprehensible.

And then the other thing I wanted to say is like, so this is maybe a chance to describe how brave does this differently than everybody else does. I think, one thing that I think is neat about brave is that brave does two things differently. One is that. There is no track, no information about you, your browsing ever leaves the device.

And so this has two benefits. One is that your device is gonna have a lot more information about you than any third party is because it sees every website you visit. So, it can do a better job of understanding what might actually be useful to you. And second is that Brave lifts the incentive structure.

So right now here on the web, the vast majority of ads are not going to be of interest to you. And all the ads come with this, like all these horrible side effects of hurting your performance. Violating your privacy, carrying the risk of malware, et cetera, et cetera, et cetera. And so nobody wants to look at it that's why ad blockers are popular.

Brave's approach is different. We'll pay you to look at ads like brave incentivizes you to look at ads that gives you a reason to look at ads. It gives marketers a reason to prioritize your attention. It breaks the privacy and performance harm and security risk.

And arguably can provide much better ads than, than some tracking based third party does. So I think there's something clever about what Brendan and Brian Bondy came up with.  in terms of the way that brave goes about these things compared to how other marketers have.

**Jeremy:** [01:08:05] We've been talking about how advertisers are using tracking to, to hopefully show you something that they think you'll be interested in, right. A lot of the research you're doing is to, to try and prevent a lot of that tracking.

So if you do that and you show someone banner ads, how are you going to be able to ensure that those, those ads are relevant to the person, when you can't track them?

**Pete:** [01:08:29] Two things, one is that brave will never, Brave, never puts an ad in the page. Like whenever you see an ad through Brave, it's very clearly not related to the page. It's in a notification to make sure that we are not putting ads against publishers who don't want them and for a whole bunch of other reasons, to prevent that kind of like, like brand confusion and all that other kind of nasty side effects about it. So brave doesn't track you in the sense that like your information never leaves your device. Brave if we wanted to, we couldn't learn anything about our users in any capacity like that.

No bits hit our servers that describe your browsing behavior. But like that you're on the device that the advice is constantly learning and saying, Oh, it looks like you're looking at shoes. Looks like you're looking at cryptocurrency. Looks like you're looking at, you know, airline flights or whatever it may be.

And so the device has a great deal of information that might be able to say, maybe you would like to see an ad about shoes, or maybe you would like to see it, an ad about, you know, vacations or whatever it may be. And so it's not tracking in the sense that like, nobody's looking at you.

It's your own device, seeing what your device already sees. but it does have the kinds of information that seems like it might be able to, actually show you stuff that you might want to see it. The other thing is you mentioned, users understanding why they're getting the ads they're getting and to be able to control it.

I mean, I think this is like a totally underappreciated concern in almost all of machine learning, where you have these extremely complex, deeply nested structures that are arrive at decisions that are completely opaque even to like machine learning experts, let alone to typical internet users.

People's lives are being guided by these unauditable black boxes. Brave's commitment is we are committed to allowing people to understand and to see the model to edit the model, to partition the model, to add into, or remove certain interests.

We're not at a threshold yet where, it makes sense to do that, but it is a commitment that Brave has made. It is absolutely in the plans and like, yeah, I mean, black boxes, like that terrify me and Brave is not going to become one of them.

**Jeremy:** [01:10:29] And you had mentioned how Brave the browser is not going to add ads to a site that doesn't have them. Does that mean that for sites that will have ads, that they would have some relationship with brave where they say that we want to show, ads in brave and that's what has to happen in order for advertising to show?

**Pete:** [01:10:50] Right now there's a couple different types of ads that Brave sends, the main one is there's notification ads. So, by default you see zero ads. You don't see anything, but if you say like, yes, I want to start getting paid to look at ads. You can say, show me, between one and five ads an hour and every, you know, one to five times an hour, you'll get a notification that looks like (fix transcript).

But say notification, you get, if you received an email or whatever, and it'll say maybe you're interested in shoes or, you know, whatever it might say, that's the predominant way that you see ads in Brave products. You also sometimes see advertising and get compensated for ads. Like if you open up the new tab page and you haven't disabled it, you may see an ad there and that you similarly get compensated for that.

I should say that for brave ads, the user gets 70% brave gets 30%. So it's like the inverse of the Apple app store. Right? Then there's the third tier of ad that brave considered, but does not ship and is working through the details on it. If we do ship it called publisher ads and that's when a website could affirmatively say yes, brave, please add ads in these locations on my website, Those, we don't do that now. if we ever did do it, it would be only with like the affirmative consent of the website.

But there's a bunch of difficulties there that have kept us from shipping. It mostly like privacy concerns of, we don't want the ad, the site hosting the ad to be able to learn about the user based on the ad that Brave places in the site. Like that would be a way of just really enabling a lot of the same tracking that's happening right now.

So we do not do publisher ads right now. We are thinking through ways that we might be able to do it in the future in a privacy preserving way. But right now the only ads that gets shown are notifications, new tab page.

**Jeremy:** [01:12:28] I see. So, the new tab page would be something very similar to when you create a new tab in Firefox and they have like a list of suggested sites. Something like that.

**Pete:** [01:12:39] Yeah. So right now, Like Chipotle advertised with Brave for a while. And so I think it was like one out of three times you opened up the new tab page. It would have a, you know, an image of a delicious burrito or whatever in the lower right hand corner, it would say Chipotle or whatever, like attractive images.

It's not executing code. It's not doing animations. It looks attractive. That kind of thing. But it's just an image. And if you don't like it, you can turn it off. But if you like it, then brave will pay you to look at it.

**Jeremy:** [01:13:01] Interesting. Yeah, it sort of reminds me a little bit of, back in the past, there were desktop applications that people could install and, I think they paid you. I don't remember if it was to click on the ads or, or just to see the ads. and this sort of sounds like a bit of, a modern kind of version of that.

**Pete:** [01:13:20] I think that's true. Although, I mean, a bunch of things distinguish it. One is that, like the bonzi buddies of the world, like ended up becoming malware vectors, two is that they didn't have the kind of information that would be useful to actually like send you the kinds of ads you were interested in.

They just pulled from a stock catalog. they were extremely obtrusive. I'm not aware of any ones that I paid you X like actual money or like a significant amount of money. I mean, but they might've existed. I couldn't say that they don't. One of the things that I want to say though, that I think is exciting to me about the Brave model is there is a sincere, honest question about like, how does content on the web get funded? And like advertising is not the only, but it's a significant part of how it content on the, on the web is funded currently.

Brave's approach is different, right now, if you enable ads by default, that money goes to the websites you visit. I have, those are configured to show me five bites an hour. And at the end of every month, brave keeps track on the browser, not on the server, but the browser keeps track of these are the, you know, this is the distribution of your viewing time across the sites that you visit.

And if you don't by default, brave, will just send your ad earnings to those sites. The sites that are involved like that are, are verified sites. They get revenue very similar to, or if not greater than, than the revenue that they would get for you looking at an ad that was an iframe on their page, but without the privacy harm, without all the nasty side effects.

So I think this can be a really powerful way of funding the open web, but without all the horrible stuff that's comes, comes with it currently.

**Jeremy:** [01:14:49] Yeah. I mean, I think that what you're seeing with a lot of news publications and even just people doing blogs and things like that is a lot of people are moving towards a subscription model, right. Where you pay me five bucks a month and, you can see my articles. And I think what's, what's tricky is that. You know, the web is so is so broad, right? You visit so many different sites a day. And so it's hard to imagine paying a monthly fee for every single site you visit. And yes, I'll be interested to see, see how that kind of model works out in the future.

**Pete:** [01:15:26] Yeah. And I should say too, that it's all in exploratory stages, but, but an idea that brave is considering and may prototype at some point is can we have some sort of like, if someone opts into the brave system, then, then brave can be the way that you just automatically pass through those paywalls.

Using the cryptocurrency, you could pay it in a, in brave is a way of saying, I don't want to have a subscription to a million different sites. If I'm in brave, then I just automatically do these, these invisible microtransactions to fund the sites that I'm viewing. I think there's something compelling about that.

**Jeremy:** [01:16:02] Yeah, for sure. everybody loves complaining about paywalls.

**Pete:** [01:16:07] Yeah, no joke.

**Jeremy:** [01:16:09] Cool. Well, I think that's a good place to start wrapping up. is there, is there anything else you think I should have asked or you wanted to mention.

**Pete:** [01:16:16] Nothing else comes to mind. I think this has been really enjoyable. I, well, actually, well, I can say two things. One is that, if you're any of your listeners are interested in privacy and web standards, like it it's a forum that could absolutely use more voices and more people who, Yeah, a greater diversity of opinion than people who work at browser vendors or ad tech companies.

And so if any of your listeners are interested in those sorts of things, I would encourage them to get involved. They can send me a message or they can just go to the issues themselves, but that would be fantastic. They have more people involved there. And the second one is, I imagine that a large portion of your listeners are people who write software for, for a living or, or who are considering careers in writing software for a living.

And a little bit soapboxy but you, yeah, that's a powerful thing and a privileged position for many people. And I would, it's worth thinking really, really well through like the morality of the kinds of causes you're spending your nine to five, like supporting.

**Jeremy:** [01:17:06] And where can people, if they want to see what you're working on currently, where can they check out what you're doing?

**Pete:** [01:17:12] Ah, so I have a website called peteresnyder.com where I have my publications and my research interests. a lot of the publications I work on at braid get published at brave/research. I write pretty regularly for the brave blog about new privacy features that are coming out in brave.

And I will. Be writing as an additional set of articles on the brave blog about, standards work in the direction that privacy interests in what standards also I'm on Twitter at PES10k.

**Jeremy:** [01:17:41] Cool. I think you gave everyone a lot to think about in terms of privacy and in terms of what's going on in their browsers. So thank you so much for talking to me today.

**Pete:** [01:17:50] Thank you very much, Jeremy. This has been super fun. I appreciate it.

**Jeremy:** [01:17:53] Thank you for listening to my chat with Pete. You can get show notes and a transcript for this episode at softwaresessions.com. The music in this episode was by crystal Cola. 

If you enjoyed the show, make sure to tell someone else about it. all right, I'll see you next time.

</div>