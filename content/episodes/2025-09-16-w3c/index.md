+++
title = "Francois Daost on the W3C"

description = "How features end up in the browser"

[extra]
episode_url = "https://pinecast.com/listen/c5f0d89e-620b-4549-a890-44992ded800b.mp3"
social_title = "Francois Daost on the W3C"
social_description = "How features end up in the browser"
+++

Francois Daost is a W3C staff member and co-chair of the Web Developer Experience Community Group.

We discuss the W3C's role and what it's like to go through the browser standardization process.


## Related links

- [W3C](https://www.w3.org/)
- [TC39](https://tc39.es/)
- [Internet Engineering Task Force](https://www.ietf.org/)
- [Web Hypertext Application Technology Working Group (WHATWG)](https://whatwg.org/)
- [Horizontal Groups](https://www.w3.org/guide/process/horizontal-groups.html)
- [Alliance for Open Media](https://aomedia.org/)
- [What is MPEG-DASH? | HLS vs. DASH](https://www.cloudflare.com/learning/video/what-is-mpeg-dash/)
- [Information about W3C and Encrypted Media Extensions (EME) ](https://www.w3.org/press-releases/2016/eme-factsheet/)
- [Widevine](https://www.widevine.com/)
- [PlayReady](https://learn.microsoft.com/en-us/playready/)
- [Media Source API](https://developer.mozilla.org/en-US/docs/Web/API/Media_Source_Extensions_API)
- [Encrypted Media Extensions API](https://developer.mozilla.org/en-US/docs/Web/API/Encrypted_Media_Extensions_API)
- [requestVideoFrameCallback()](https://developer.mozilla.org/en-US/docs/Web/API/HTMLVideoElement/requestVideoFrameCallback)
- [Business Benefits of the W3C Patent Policy](https://www.w3.org/2004/03/pp-points-20040210.html)
- [web.dev Baseline](https://web.dev/baseline)
- [Portable Network Graphics Specification](https://www.w3.org/TR/png-3/)
- [Internet Explorer 6](https://en.wikipedia.org/wiki/Internet_Explorer_6)
- [CSS Vendor Prefix](https://developer.mozilla.org/en-US/docs/Glossary/Vendor_Prefix)
- [WebRTC](https://webrtc.org/)

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

## Intro

[00:00:00] **Jeremy:** today I'm talking to Francois Daoust. He's a staff member at the W3C. And we're gonna talk about the W3C and the recommendation process and discuss, Francois's experience with, with how these features end up in our browsers.

[00:00:16] **Jeremy:** So, Francois, welcome 

[00:00:18] **Francois:** Thank you Jeremy and uh, many thanks for the invitation. I'm really thrilled to be part of this podcast.


## What's the W3C?

[00:00:26] **Jeremy:** I think many of our listeners will have heard about the W3C, but they may not actually know what it is. So could you start by explaining what it is?

[00:00:37] **Francois:** Sure. So W3C stands for the Worldwide Web Consortium. It's a standardization organization. I guess that's how people should think about W3C. it was created in 1994. I, by, uh, Tim Berners Lee, who was the inventor of the web. Tim Berners Lee was the, director of W3C for a long, long time.

[00:01:00] **Francois:** He retired not long ago, a few years back. and W3C is, has, uh, a number of, uh. Properties, let's say first the goal is to produce royalty free standards, and that's very important. Uh, we want to make sure that, uh, the standard that get produced can be used and implemented without having to pay, fees to anyone.

[00:01:23] **Francois:** We do web standards. I didn't mention it, but it's from the name. Standards that you find in your web browsers. But not only that, there are a number of other, uh, standards that got developed at W3C including, for example, XML. Data related standards. W3C as an organization is a consortium.

[00:01:43] **Francois:** The, the C stands for consortium. Legally speaking, it's a, it's a 501c3 meaning in, so it's a US based, uh, legal entity not for profit. And the, the little three is important because it means it's public interest. That means we are a consortium, that means we have members, but at the same time, the goal, the mission is to the public.

[00:02:05] **Francois:** So we're not only just, you know, doing what our members want. We are also making sure that what our members want is aligned with what end users in the end, need. and the W3C has a small team. And so I'm part of this, uh, of this team worldwide. Uh, 45 to 55 people, depending on how you count, mostly technical people and some, uh, admin, uh, as well, overseeing the, uh, the work, that we do, uh, at the W3C.


## Funding through membership fees

[00:02:39] **Jeremy:** So you mentioned there's 45 to 55 people. How is this funded? Is this from governments or commercial companies?

[00:02:47] **Francois:** The main source comes from membership fees. So the W3C has a, so members, uh, roughly 350 members, uh, at the W3C. And, in order to become a member, an organization needs to pay, uh, an annual membership fee. That's pretty common among, uh, standardization, uh, organizations.

[00:03:07] **Francois:** And, we only have, uh, I guess three levels of membership, fees. Uh, well, you may find, uh, additional small levels, but three main ones. the goal is to make sure that, A big player will, not a big player or large company, will not have more rights than, uh, anything, anyone else. So we try to make sure that a member has the, you know, all members have equal, right?

[00:03:30] **Francois:** if it's not perfect, but, uh, uh, that's how things are, are are set. So that's the main source of income for the W3C. And then we try to diversify just a little bit to get, uh, for example, we go to governments. We may go to governments in the u EU. We may, uh, take some, uh, grant for EU research projects that allow us, you know, to, study, explore topics.

[00:03:54] **Francois:** Uh, in the US there, there used to be some, uh, some funding from coming from the government as well. So that, that's, uh, also, uh, a source. But the main one is, uh, membership fees.


## Relations to TC39, IETF, and WHATWG

[00:04:04] **Jeremy:** And you mentioned that a lot of the W3C'S work is related to web standards. There's other groups like TC 39, which works on the JavaScript spec and the IETF, which I believe worked, with your group on WebRTC, I wonder if you could explain W3C'S connection to other groups like that.

[00:04:28] **Francois:** sure. we try to collaborate with a, a number of, uh, standard other standardization organizations. So in general, everything goes well because you, you have, a clear separation of concerns. So you mentioned TC 39. Indeed. they are the ones who standardize, JavaScript. Proper name of JavaScript is the EcmaScript.

[00:04:47] **Francois:** So that's tc. TC 39 is the technical committee at ecma. and so we have indeed interactions with them because their work directly impact the JavaScript that you're going to find in your, uh, run in your, in your web browser. And we develop a number of JavaScript APIs, uh, actually in W3C.

[00:05:05] **Francois:** So we need to make sure that, the way we develop, uh, you know, these APIs align with the, the language itself. with IETF, the, the, the boundary is, uh, uh, is clear as well. It's a protocol and protocol for our network protocols for our, the IETF and application level. For W3C, that's usually how the distinction is made.

[00:05:28] **Francois:** The boundaries are always a bit fuzzy, but that's how things work. And usually, uh, things work pretty well. Uh, there's also the WHATWG, uh, and the WHATWG is more the, the, the history was more complicated because, uh, t of a fork of the, uh, HTML specification, uh, at the time when it was developed by W3C, a long time ago.

[00:05:49] **Francois:** And there was been some, uh, Well disagreement on the way things should have been done, and the WHATWG took over got created, took, took this the HTML spec and did it a different way. Went in another, another direction, and that other, other direction actually ended up being the direction.

[00:06:06] **Francois:** So, that's a success, uh, from there. And so, W3C no longer works, no longer owns the, uh, HTML spec and the WHATWG has, uh, taken, uh, taken up a number of, uh, of different, core specifications for the web. Uh, doing a lot of work on the, uh, on interopoerability and making sure that, uh, the algorithm specified by the spec, were correct, which, which was something that historically we haven't been very good at at W3C.

[00:06:35] **Francois:** And the way they've been working as a, has a lot of influence on the way we develop now, uh, the APIs, uh, from a W3C perspective.

[00:06:44] **Jeremy:** So, just to make sure I understand correctly, you have TC 39, which is focused on the JavaScript or ECMAScript language itself, and you have APIs that are going to use JavaScript and interact with JavaScript. So you need to coordinate there. The, the have the specification for HTML. then the IATF, they are, I'm not sure if the right term would be, they, they would be one level lower perhaps, than the W3C.

[00:07:17] **Francois:** That's how you, you can formulate it. Yes. The, the one layer, one layer layer in the ISO network in the ISO stack at the network level.


## How WebRTC spans the IETF and W3C

[00:07:30] **Jeremy:** And so in that case, one place I've heard it mentioned is that webRTC, to, to use it, there is an IETF specification, and then perhaps there's a W3C recommendation and

[00:07:43] **Francois:** Yes. so when we created the webRTC working group, that was in 2011, I think, it was created with a dual head. There was one RTC web, group that got created at IETF and a webRTC group that got created at W3C. And that was done on purpose. Of course, the goal was not to compete on the, on the solution, but actually to, have the two sides of the, uh, solution, be developed in parallel, the API, uh, the application front and the network front.

[00:08:15] **Francois:** And there was a, and there's still a lot of overlap in, uh, participation between both groups, and that's what keep things successful. In the end. It's not, uh, you know, process or organization to organization, uh, relationships, coordination at the organization level. It's really the fact that you have participants that are essentially the same, on both sides of the equation.

[00:08:36] **Francois:** That helps, uh, move things forward. Now, webRTC is, uh, is more complex than just one group at IETF. I mean, web, webRTC is a very complex set of, uh, of technologies, stack of technologies. So when you, when you. Pull a little, uh, protocol from IETFs. Suddenly you have the whole IETF that comes with you with it.

[00:08:56] **Francois:** So you, it's the, you have the feeling that webRTC needs all of the, uh, internet protocols that got, uh, created to work


## Recommendations

[00:09:04] **Jeremy:** And I think probably a lot of web developers, they may hear words like specification or standard, but I believe the, the official term, at least at the W3C, is this recommendation. And so I wonder if you can explain what that means.

[00:09:24] **Francois:** Well. It means it means standard in the end. and that came from industry. That comes from a time where. As many standardization organizations. W3C was created not to be a standardization organization. It was felt that standard was not the right term because we were not a standardization organization.

[00:09:45] **Francois:** So recommend IETF has the same thing. They call it RFC, request for comment, which, you know, stands for nothing in, and yet it's a standard. So W3C was created with the same kind of, uh thing. We needed some other terminology and we call that recommendation. But in the end, that's standard. It's really, uh, how you should see it.

[00:10:08] **Francois:** And one thing I didn't mention when I, uh, introduced the W3C is there are two types of standards in the end, two main categories. There are, the de jure standards and defacto standards, two families. The de jure standards are the ones that are imposed by some kind of regulation. so it's really usually a standard you see imposed by governments, for example.

[00:10:29] **Francois:** So when you look at your electric plug at home, there's some regulation there that says, this plug needs to have these properties. And that's a standard that gets imposed. It's a de jure standard. and then there are defacto standards which are really, uh, specifications that are out there and people agree to use it to implement it.

[00:10:49] **Francois:** And by virtue of being used and implemented and used by everyone, they become standards. the, W3C really is in the, uh, second part. It's a defacto standard. IETF is the same thing. some of our standards are used in, uh, are referenced in regulations now, but, just a, a minority of them, most of them are defacto standards.

[00:11:10] **Francois:** and that's important because that's in the end, it doesn't matter what the specific specification says, even though it's a bit confusing. What matters is that the, what the specifications says matches what implementations actually implement, and that these implementations are used, and are used interoperably across, you know, across browsers, for example, or across, uh, implementations, across users, across usages.

[00:11:36] **Francois:** So, uh, standardization is a, is a lengthy process. The recommendation is the final stage in that, lengthy process. More and more we don't really reach recommendation anymore. If you look at, uh, at groups, uh, because we have another path, let's say we kind of, uh, we can stop at candidate recommendation, which is in theoretically a step before that.

[00:12:02] **Francois:** But then you, you can stay there and, uh, stay there forever and publish new candidate recommendations. Um, uh, later on. What matters again is that, you know, you get this, virtuous feedback loop, uh, with implementers, and usage.

[00:12:18] **Jeremy:** So if the candidate recommendation ends up being implemented by all the browsers, what's ends up being the distinction between a candidate and one that's a normal recommendation.

[00:12:31] **Francois:** So, today it's mostly a process thing. Some groups actually decide to go to rec Some groups decide to stay at candidate rec and there's no formal difference between the, the two. we've made sure we've adopted, adjusted the process so that the important bits that, applied at the recommendation level now apply at the candidate rec level.


## Royalty free patent access

[00:13:00] **Francois:** And by important things, I mean the patent commitments typically, uh, the patent policy fully applies at the candidate recommendation level so that you get your, protection, the royalty free patent protection that we, we were aiming at.

[00:13:14] **Francois:** Some people do not care, you know, but most of the world still works with, uh, with patents, uh, for good, uh, or bad reasons. But, uh, uh, that's how things work. So we need to make, we're trying to make sure that we, we secure the right set of, um, of patent commitments from the right set of stakeholders.

[00:13:35] **Jeremy:** Oh, so when someone implements a W3C recommendation or a candidate recommendation, the patent holders related to that recommendation, they basically agree to allow royalty-free use of that patent.

[00:13:54] **Francois:** They do the one that were involved in the working group, of course, I mean, we can't say anything about the companies out there that may have patents and uh, are not part of this standardization process. So there's always, It's a remaining risk. but part of the goal when we create a working group is to make sure that, people understand the scope.

[00:14:17] **Francois:** Lawyers look into it, and the, the legal teams that exist at the all the large companies, basically gave a green light saying, yeah, we, we we're pretty confident that we, we know where the patterns are on this particular, this particular area. And we are fine also, uh, letting go of the, the patterns we own ourselves.


## Implementations are built in parallel with standardization

[00:14:39] **Jeremy:** And I think you had mentioned. What ends up being the most important is that the browser creators implement these recommendations. So it sounds like maybe the distinction between candidate recommendation and recommendation almost doesn't matter as long as you get the end result you want.

[00:15:03] **Francois:** So, I mean, people will have different opinions, uh, in the, in standardization circles. And I mentioned also W3C is working on other kind of, uh, standards. So, uh, in some other areas, the nuance may be more important when we, but when, when you look at specification, that's target, web browsers. we've switched from a model where, specs were developed first and then implemented to a model where specs and implementing implementations are being, worked in parallel.

[00:15:35] **Francois:** This actually relates to the evolution I was mentioning with the WHATWG taking over the HTML and, uh, focusing on the interoperability issues because the starting point was, yeah, we have an HTML 4.01 spec, uh, but it's not interoperable because it, it's not specified, are number of areas that are gray areas, you can implement them differently.

[00:15:59] **Francois:** And so there are interoperable issues. Back to candidate rec actually, the, the, the, the stage was created, if I remember correctly. uh, if I'm, if I'm not wrong, the stage was created following the, uh, IE problem. In the CSS working group, IE6, uh, shipped with some, version of a CSS that was in the, as specified, you know, the spec was saying, you know, do that for the CSS box model.

[00:16:27] **Francois:** And the IE6 was following that. And then the group decided to change, the box model and suddenly IE6 was no longer compliant. And that created a, a huge mess on the, in the history of, uh, of the web in a way. And so the, we, the, the, the, the candidate recommendation sta uh, stage was introduced following that to try to catch this kind of problems.

[00:16:52] **Francois:** But nowadays, again, we, we switch to another model where it's more live. and so we, you, you'll find a number of specs that are not even at candidate rec level. They are at the, what we call a working draft, and they, they are being implemented, and if all goes well, the standardization process follows the implementation, and then you end up in a situation where you have your candidate rec when the, uh, spec ships.

[00:17:18] **Francois:** a recent example would be a web GPU, for example. It, uh, it has shipped in, uh, in, in Chrome shortly before it transition to a candidate rec. But the, the, the spec was already stable. and now it's shipping uh, in, uh, in different browsers, uh, uh, safari, uh, and uh, and uh, and uh, Firefox. And so that's, uh, and that's a good example of something that follows, uh, things, uh, along pretty well. But then you have other specs such as, uh, in the media space, uh, request video frame back, uh, frame, call back, uh, requestVideoFrameCallback() is a short API that allows you to get, you know, a call back whenever the, the browser renders a video frame, essentially.

[00:18:01] **Francois:** And that spec is implemented across browsers. But from a W3C specific, perspective, it does not even exist. It's not on the standardization track. It's still being incubated in what we call a community group, which is, you know, some something that, uh, usually exists before. we move to the, the standardization process.

[00:18:21] **Francois:** So there, there are examples of things where some things fell through the cracks. All the standardization process, uh, is either too early or too late and things that are in spec are not exactly what what got implemented or implementations are too early in the process. We we're doing a better job, at, Not falling into a trap where someone ships, uh, you know, an implementation and then suddenly everything is frozen. You can no longer, change it because it's too late, it shipped. we've tried, different, path there. Um, mentioned CSS, the, there was this kind of vendor prefixed, uh, properties that used to be, uh, the way, uh, browsers were deploying new features without, you know, taking the final name.

[00:19:06] **Francois:** We are trying also to move away from it because same thing. Then in the end, you end up with, uh, applications that have, uh, to duplicate all the properties, the CSS properties in the style sheets with, uh, the vendor prefixes and nuances in the, in what it does in, in the end.

[00:19:23] **Jeremy:** Yeah, I, I think, is that in CSS where you'll see --mozilla or things like that?


## Why requestVideoFrameCallback doesn't have a formal specification

[00:19:30] **Jeremy:** The example of the request video frame callback. I, I wonder if you have an opinion or, or, or know why that ended up the way it did, where the browsers all implemented it, even though it was still in the incubation stage.

[00:19:49] **Francois:** On this one, I don't have a particular, uh, insights on whether there was a, you know, a strong reason to implement it,without doing the standardization work. 

[00:19:58] **Francois:** I mean, there are, it's not, uh, an IPR (Intellectual Property Rights) issue. It's not, uh, something that, uh, I don't think the, the, the spec triggers, uh, you know, problems that, uh, would be controversial or whatever.

[00:20:10] **Francois:** Uh, so it's just a matter of, uh, there was no one's priority, and in the end, you end up with a, everyone's happy. it's, it has shipped. And so now doing the spec work is a bit,why spend time on something that's already shipped and so on, but the, it may still come back at some point with try to, you know, improve the situation.

[00:20:26] **Jeremy:** Yeah, that's, that's interesting. It's a little counterintuitive because it sounds like you have the, the working group and it, it sounds like perhaps the companies or organizations involved, they maybe agreed on how it should work, and maybe that agreement almost made it so that they felt like they didn't need to move forward with the specification because they came to consensus even before going through that.

[00:20:53] **Francois:** In this particular case, it's probably because it's really, again, it's a small, spec. It's just one function call, you know? I mean, they will definitely want a working group, uh, for larger specifications. by the way, actually now I know re request video frame call back. It's because the, the, the final goal now that it's, uh, shipped, is to merge it into, uh, HTML, uh, the HTML spec.

[00:21:17] **Francois:** So there's a, there's an ongoing issue on the, the WHATWG side to integrate request video frame callback. And it's taking some time but see, it's, it's being, it, it caught up and, uh, someone is doing the, the work to, to do it. I had forgotten about this one. Um,

[00:21:33] **Jeremy:** 


## Tension from specification review (horizontal review)

[00:21:33] **Francois:** so with larger specifications, organizations will want this kind of IPR regime they will want commit commitments from, uh, others, on the scope, on the process, on everything. So they will want, uh, a larger, a, a more formal setting, because that's part of how you ensure that things, uh, will get done properly.

[00:21:53] **Francois:** I didn't mention it, but, uh, something we're really, uh, Pushy on, uh, W3C I mentioned we have principles, we have priorities, and we have, uh, specific several, uh, properties at W3C. And one of them is that we we're very strong on horizontal reviews of our specs. We really want them to be reviewed from an accessibility perspective, from an internationalization perspective, from a privacy and security, uh, perspective, and, and, and a technical architecture perspective as well.

[00:22:23] **Francois:** And that's, these reviews are part of the formal process. So you, all specs need to undergo these reviews. And from time to time, that creates tension. Uh, from time to time. It just works, you know. Goes without problem. a recurring issue is that, privacy and security are hard. I mean, it's not an easy problem, something that can be, uh, solved, uh, easily.

[00:22:48] **Francois:** Uh, so there's a, an ongoing tension and no easy way to resolve it, but there's an ongoing tension between, specifying powerful APIs and preserving privacy without meaning, not exposing too much information to applications in the media space. You can think of the media capabilities, API. So the media space is a complicated space.

[00:23:13] **Francois:** Space because of codecs. codecs are typically not relative free. and so browsers decide which codecs they're going to support, which audio and video codecs they, they're going to support and doing that, that creates additional fragmentation, not in the sense that they're not interoperable, but in the sense that applications need to choose which connect they're going to ship to stream to the end user.

[00:23:39] **Francois:** And, uh, it's all the more complicated that some codecs are going to be hardware supported. So you will have a hardware decoder in your, in your, in your laptop or smartphone. And so that's going to be efficient to decode some, uh, some stream, whereas some code are not, are going to be software, based, supported.

[00:23:56] **Francois:** Uh, and that may consume a lot of CPU and a lot of power and a lot of energy in the end. So you, you want to avoid that if you can, uh, select another thing. Even more complex than, codecs have different profiles, uh, lower end profiles higher end profiles with different capabilities, different features, uh, depending on whether you're going to use this or that color space, for example, this or that resolution, whatever.

[00:24:22] **Francois:** And so you want to surface that to web applications because otherwise, they can't. Select, they can't choose, the right codec and the right, stream that they're going to send to the, uh, client devices. And so they're not going to provide an efficient user experience first, and even a sustainable one in terms of energy because they, they're going to waste energy if they don't send the right stream.

[00:24:45] **Francois:** So you want to surface that to application. That's what the media, media capabilities, APIs, provides.


## Privacy concerns

[00:24:51] **Francois:** Uh, but at the same time, if you expose that information, you end up with ways to fingerprint the end user's device. And that in turn is often used to track users across, across sites, which is exactly what we don't want to have, uh, for privacy reasons, for obvious privacy reasons.

[00:25:09] **Francois:** So you have to balance that and find ways to, uh, you know, to expose. Capabilities without, without necessarily exposing them too much. Uh,

[00:25:21] **Jeremy:** Can you give an example of how some of those discussions went? Like within the working group? Who are the companies or who are the organizations that are arguing for We shouldn't have this capability because of the privacy concerns, or 

[00:25:40] **Francois:** In a way all of the companies, have a vision of, uh, of privacy. I mean, the, you will have a hard time finding, you know, members saying, I don't care about privacy. I just want the feature. Uh, they all have privacy in mind, but they may have a different approach to privacy.

[00:25:57] **Francois:** so if you take, uh, let's say, uh, apple and Google would be the, the, I guess the perfect examples in that, uh, in that space, uh, Google will have a, an approach that is more open-ended thing. The, the user agents has this, uh, should check what the, the, uh, given site is doing. And then if it goes beyond, you know, some kind of threshold, they're going to say, well, okay, well, we'll stop exposing data to that, to that, uh, to that site.

[00:26:25] **Francois:** So that application. So monitor and react in a way. apple has a more, uh, you know, has a stricter view on, uh, on privacy, let's say. And they will say, no, we, the, the, the feature must not exist in the first place. Or, but that's, I mean, I guess, um, it's not always that extreme. And, uh, from time to time it's the opposite.

[00:26:45] **Francois:** You will have, uh, you know, apple arguing in one way, uh, which is more open-ended than the, uh, than, uh, than Google, for example. And they are not the only ones. So in working groups, uh, you will find the, usually the implementers. Uh, so when we talk about APIs that get implemented in browsers, you want the core browsers to be involved.

[00:27:04] **Francois:** Uh, otherwise it's usually not a good sign for, uh, the success of the, uh, of the technology. So in practice, that means Apple, uh, Microsoft, Mozilla which one did I forget?

[00:27:15] **Jeremy:** Google.

[00:27:16] **Francois:** I forgot Google. Of course. Thank you. that's, uh, that the, the core, uh, list of participants you want to have in any, uh, group that develops web standards targeted at web browsers.


## Who participates in working groups and how much power do they have?

[00:27:28] **Francois:** And then on top of that, you want, organizations and people who are directly going to use it, either because they, well the content providers. So in media, for example, if you look at the media working group, you'll see, uh, so browser vendors, the ones I mentioned, uh, content providers such as the BBC or Netflix.

[00:27:46] **Francois:** Chip set vendors would, uh, would be there as well. Intel, uh, Nvidia again, because you know, there's a hardware decoding in there and encoding. So media is, touches on, on, uh, on hardware, uh, device manufacturer in general. You may, uh, I think, uh, I think Sony is involved in the, in the media working group, for example.

[00:28:04] **Francois:** and these companies are usually less active in the spec development. It depends on the groups, but they're usually less active because the ones developing the specs are usually the browser again, because as I mentioned, we develop the specs in parallel to browsers implementing it. So they have the.

[00:28:21] **Francois:** The feedback on how to formulate the, the algorithms. and so that's this collection of people who are going to discuss first within themselves. W3C pushes for consensual dis decisions. So we hardly take any votes in the working groups, but from time to time, that's not enough.

[00:28:41] **Francois:** And there may be disagreements, but let's say there's agreement in the group, uh, when the spec matches. horizontal review groups will look at the specs. So these are groups I mentioned, accessibility one, uh, privacy, internationalization. And these groups, usually the participants are, it depends.

[00:29:00] **Francois:** It can be anything. It can be, uh, the same companies. It can be, but usually different people from the same companies. But it the, maybe organizations with a that come from very, a very different angle. And that's a good thing because that means the, you know, you enlarge the, the perspectives on your, uh, on the, on the technology.

[00:29:19] **Francois:** and you, that's when you have a discussion between groups, that takes place. And from time to time it goes well from time to time. Again, it can trigger issues that are hard to solve. and the W3C has a, an escalation process in case, uh, you know, in case things degenerate. Uh, starting with, uh, the notion of formal objection.

[00:29:42] **Jeremy:** It makes sense that you would have the, the browser. Vendors and you have all the different companies that would use that browser. All the different horizontal groups like you mentioned, the internationalization, accessibility. I would imagine that you were talking about consensus and there are certain groups or certain companies that maybe have more say or more sway.

[00:30:09] **Jeremy:** For example, if you're a browser, manufacturer, your Google. I'm kind of curious how that works out within the working group.

[00:30:15] **Francois:** Yes, it's, I guess I would be lying if I were saying that, uh, you know, all companies are strictly equal in a, in a, in a group. they are from a process perspective, I mentioned, you know, different membership fees with were design, special specific ethos so that no one could say, I'm, I'm putting in a lot of money, so you, you need to re you need to respect me, uh, and you need to follow what I, what I want to, what I want to do.

[00:30:41] **Francois:** at the same time, if you take a company like, uh, like Google for example, they send, hundreds of engineers to do standardization work. That's absolutely fantastic because that means work progresses and it's, uh, extremely smart people. So that's, uh, that's really a pleasure to work with, uh, with these, uh, people.

[00:30:58] **Francois:** But you need to take a step back and say, well, the problem is. Defacto that gives them more power just by virtue of, uh, injecting more resources into it. So having always someone who can respond to an issue, having always someone, uh, editing a spec defacto that give them more, uh, um, more say on the, on the directions that, get forward.

[00:31:22] **Francois:** And on top of that, of course, they have the, uh, I guess not surprisingly, the, the browser that is, uh, used the most, currently, on the market so there's a little bit of a, the, the, we, we, we, we try very hard to make sure that, uh, things are balanced. it's not a perfect world.

[00:31:38] **Francois:** the the role of the team. I mean, I didn't talk about the role of the team, but part of it is to make sure that. Again, all perspectives are represented and that there's not, such a, such big imbalance that, uh, that something is wrong and that we really need to look into it. so making sure that anyone, if they have something to say, make making sure that they are heard by the rest of the group and not dismissed.

[00:32:05] **Francois:** That usually goes well. There's no problem with that. And again, the escalation process I mentioned here doesn't make any, uh, it doesn't make any difference between, uh, a small player, a large player, a big player, and we have small companies raising formal objections against some of our aspects that happens, uh, all large ones.

[00:32:24] **Francois:** But, uh, that happens too. There's no magical solution, I guess you can tell it by the way. I, uh, I don't know how to formulate the, the process more. It's a human process, and that's very important that it remains a human process as well.

[00:32:41] **Jeremy:** I suppose the role of, of staff and someone in your position, for example, is to try and ensure that these different groups are, are heard and it isn't just one group taking control of it.

[00:32:55] **Francois:** That's part of the role, again, is to make sure that, uh, the, the process is followed. So the, I, I mean, I don't want to give the impression that the process controls everything in the groups. I mean, the, the, the groups are bound by the process, but the process is there to catch problems when they arise.

[00:33:14] **Francois:** most of the time there are no problems. It's just, you know, again, participants talking to each other, talking with the rest of the community. Most of the work happens in public nowadays, in any case. So the groups work in public essentially through asynchronous, uh, discussions on GitHub repositories.

[00:33:32] **Francois:** There are contributions from, you know, non group participants and everything goes well. And so the process doesn't kick in. You just never say, eh, no, you didn't respect the process there. You, you closed the issue. You shouldn't have a, it's pretty rare that you have to do that. Uh, things just proceed naturally because they all, everyone understands where they are, why, what they're doing, and why they're doing it.

[00:33:55] **Francois:** we still have a role, I guess in the, in the sense that from time to time that doesn't work and you have to intervene and you have to make sure that,the, uh, exception is caught and, uh, and processed, uh, in the right way.


## Discussions are public on github

[00:34:10] **Jeremy:** And you said this process is asynchronous in public, so it sounds like someone, I, I mean, is this in GitHub issues or how, how would somebody go and, and see what the results of

[00:34:22] **Francois:** Yes, there, there are basically a gazillion of, uh, GitHub repositories under the, uh, W3C, uh, organization on GitHub. Most groups are using GitHub. I mean, there's no, it's not mandatory. We don't manage any, uh, any tooling. But the factors that most, we, we've been transitioning to GitHub, uh, for a number of years already.

[00:34:45] **Francois:** Uh, so that's where the work most of the work happens, through issues, through pool requests. Uh, that's where. people can go and raise issues against specifications. Uh, we usually, uh, also some from time to time get feedback from developers and countering, uh, a bug in a particular implementations, which we try to gently redirect to, uh, the actual bug trackers because we're not responsible for the respons implementations of the specs unless the spec is not clear.

[00:35:14] **Francois:** We are responsible for the spec itself, making sure that the spec is clear and that implementers well, understand how they should implement something.


## Why the W3C doesn't specify a video or audio codec

[00:35:25] **Jeremy:** I can see how people would make that mistake because they, they see it's the feature, but that's not the responsibility of the, the W3C to implement any of the specifications. Something you had mentioned there's the issue of intellectual property rights and how when you have a recommendation, you require the different organizations involved to make their patents available to use freely.

[00:35:54] **Jeremy:** I wonder why there was never any kind of, recommendation for audio or video codecs in browsers since you have certain ones that are considered royalty free. But, I believe that's never been specified.

[00:36:11] **Francois:** At W3C you mean? Yes. we, we've tried, I mean, it's not for lack of trying. Um, uh, we've had a number of discussions with, uh, various stakeholders saying, Hey, we, we really need, an audio or video code for our, for the web. the, uh, png PNG is an example of a, um, an image format which got standardized at W3C and it got standardized at W3C similar reasons. There had to be a royalty free image format for the web, and there was none at the time. of course, nowadays, uh, jpeg, uh, and gif or gif, whatever you call it, are well, you know, no problem with them. But, uh, um, that at the time P PNG was really, uh, meant to address this issue and it worked for PNG for audio and video.

[00:37:01] **Francois:** We haven't managed to secure, commitments by stakeholders. So willingness to do it, so it's not, it's not lack of willingness. We would've loved to, uh, get, uh, a royalty free, uh, audio codec, a royalty free video codec again, audio and video code are extremely complicated because of this.

[00:37:20] **Francois:** not only because of patterns, but also because of the entire business ecosystem that exists around them for good reasons. You, in order for a, a codec to be supported, deployed, effective, it really needs, uh, it needs to mature a lot. It needs to, be, uh, added to at a hardware level, to a number of devices, capturing devices, but also, um, uh, uh, of course players.

[00:37:46] **Francois:** And that takes a hell of a lot of time and that's why you also enter a number of business considerations with business contracts between entities. so I'm personally, on a personal level, I'm, I'm pleased to see, for example, the Alliance for Open Media working on, uh, uh, AV1, uh, which is. At least they, uh, they wanted to be royalty free and they've been adopting actually the W3C patent policy to do this work.

[00:38:11] **Francois:** So, uh, we're pleased to see that, you know, they've been adopting the same process and same thing. AV1 is not yet at the same, support stage, as other, codecs, in the world Yeah, I mean in devices. There's an open question as what, what are we going to do, uh, in the future uh, with that, it's, it's, it's doubtful that, uh, the W3C will be able to work on a, on a royalty free audio, codec or royalty free video codec itself because, uh, probably it's too late now in any case.

[00:38:43] **Francois:** but It's one of these angles in the, in the web platform where we wish we had the, uh, the technology available for, for free. And, uh, it's not exactly, uh, how things work in practice.I mean, the way codecs are developed remains really patent oriented.

[00:38:57] **Francois:** and you will find more codecs being developed. and that's where geopolitics can even enter the, the, uh, the play. Because, uh, if you go to China, you will find new codecs emerging, uh, that get developed within China also, because, the other codecs come mostly from the US so it's a bit of a problem and so on.

[00:39:17] **Francois:** I'm not going to enter details and uh, I would probably say stupid things in any case. Uh, but that, uh, so we continue to see, uh, emerging codecs that are not royalty free, and it's probably going to remain the case for a number of years. unfortunately, unfortunately, from a W3C perspective and my perspective of course.

[00:39:38] **Jeremy:** There's always these new, formats coming out and the, rate at which they get supported in the browser, even on a per browser basis is, is very, there can be a long time between, for example, WebP being released and a browser supporting it. So, seems like maybe we're gonna be in that situation for a while where the codecs will come out and maybe the browsers will support them. Maybe they won't, but the, the timeline is very uncertain.


## Digital Rights Management (DRM) and Media Source Extensions

[00:40:08] **Jeremy:** Something you had, mentioned, maybe this was in your, email to me earlier, but you had mentioned that some of these specifications, there's, there's business considerations like with, digital rights management and, media source extensions. I wonder if you could talk a little bit about maybe what media source extensions is and encrypted media extensions and, and what the, the considerations or challenges are there.

[00:40:33] **Francois:** I'm going to go very, very quickly over the history of a, video and audio support on the web. Initially it was supported through plugins. you are maybe too young to, remember that. But, uh, we had extensions, added to, uh, a realplayer.

[00:40:46] **Francois:** This kind of things flash as well, uh, supporting, uh, uh, videos, in web pages, but it was not provided by the web browsers themselves. Uh, then HTML5 changed the, the situation. Adding these new tags, audio and video, but that these tags on this, by default, support, uh, you give them a resources, a resource, like an image as it's an audio or a video file.

[00:41:10] **Francois:** They're going to download this, uh, uh, video file or audio file, and they're going to play it. That works well. But as soon as you want to do any kind of real streaming, files are too large and to stream, to, to get, you know, to get just a single fetch on, uh, on them. So you really want to stream them chunk by chunk, and you want to adapt the resolution at which you send the stream based on real time conditions of the user's network.

[00:41:37] **Francois:** If there's plenty of bandwidth you want to send the user, the highest possible resolution. If there's a, some kind of hiccup temporary in the, in the network, you really want to lower the resolution, and that's called adaptive streaming. And to get adaptive streaming on the web, well, there are a number of protocols that exist.

[00:41:54] **Francois:** Same thing. Some many of them are proprietary and actually they remain proprietary, uh, to some extent. and, uh, some of them are over http and they are the ones that are primarily used in, uh, in web contexts. So DASH comes to mind, DASH for Dynamic Adaptive streaming over http. HLS is another one. Uh, initially developed by Apple, I believe, and it's, uh, HTTP live streaming probably. Exactly. And, so there are different protocols that you can, uh, you can use. Uh, so the goal was not to standardize these protocols because again, there were some proprietary aspects to them. And, uh, same thing as with codecs.

[00:42:32] **Francois:** There was no, well, at least people wanted to have the, uh, flexibility to tweak parameters, adaptive streaming parameters the way they wanted for different scenarios. You may want to tweak the parameters differently. So they, they needed to be more flexibility on top of protocols not being truly available for use directly and for implementation directly in browsers.

[00:42:53] **Francois:** It was also about providing applications with, uh, the flexibility they would need to tweak parameters. So media source extensions comes into play for exactly that. Media source extensions is really about you. The application fetches chunks of its audio and video stream the way it wants, and with the parameters it wants, and it adjusts whatever it wants.

[00:43:15] **Francois:** And then it feeds that into the, uh, video or audio tag. and the browser takes care of the rest. So it's really about, doing, you know, the adaptive streaming. let applications do it, and then, uh, let the user agent, uh, the browser takes, take care of the rendering itself. That's media source extensions.

[00:43:32] **Francois:** Initially it was pushed by, uh, Netflix. They were not the only ones of course, but there, there was a, a ma, a major, uh, proponent of this, uh, technical solution, because they wanted, uh, they, uh, they were, expanding all over the world, uh, with, uh, plenty of native, applications on all sorts of, uh, of, uh, devices.

[00:43:52] **Francois:** And they wanted to have a way to stream content on the web as well. both for both, I guess, to expand to, um, a new, um, ecosystem, the web, uh, providing new opportunities, let's say. But at the same time also to have a fallback, in case they, because for native support on different platforms, they sometimes had to enter business agreements with, uh, you know, the hardware manufacturers, the whatever, the, uh, service provider or whatever.

[00:44:19] **Francois:** and so that was a way to have a full back. That kind of work is more open, in case, uh, things take some time and so on. So, and they probably had other reasons. I mean, I'm not, I can't speak on behalf of Netflix, uh, on others, but they were not the only ones of course, uh, supporting this, uh, me, uh, media source extension, uh, uh, specification.

[00:44:42] **Francois:** and that went kind of, well, I think it was creating 2011. I mean, the, the work started in 2011 and the recommendation was published in 2016, which is not too bad from a standardization perspective. It means only five years, you know, it's a very short amount of time.


## Encrypted Media Extensions

[00:44:59] **Francois:** At the same time, and in parallel and complement to the media source extension specifications, uh, there was work on the encrypted media extensions, and here it was pushed by the same proponent in a way because they wanted to get premium content on the web.

[00:45:14] **Francois:** And by premium content, you think of movies and, uh. These kind of beasts. And the problem with the, I guess the basic issue with, uh, digital asset such as movies, is that they cost hundreds of millions to produce. I mean, some cost less of course. And yet it's super easy to copy them if you have a access to the digital, uh, file.

[00:45:35] **Francois:** You just copy and, uh, and that's it. Piracy uh, is super easy, uh, to achieve. It's illegal of course, but it's super easy to do. And so that's where the different legislations come into play with digital right management. Then the fact is most countries allow system that, can encrypt content and, uh, through what we call DRM systems.

[00:45:59] **Francois:** so content providers, uh, the, the ones that have movies, so the studios here more, more and more, and Netflix is one, uh, one of the studios nowadays. Um, but not only, not only them all major studios will, uh, would, uh, push for, wanted to have something that would allow them to stream encrypted content, encrypted audio and video, uh, mostly video, to, uh, to web applications so that, uh, you.

[00:46:25] **Francois:** Provide the movies, otherwise, they, they are just basically saying, and sorry, but, uh, this premium content will never make it to the web because there's no way we're gonna, uh, send it in clear, to, uh, to the end user. So Encrypting media extensions is, uh, is an API that allows to interface with, uh, what's called the content decryption module, CDM, uh, which itself interacts with, uh, the DR DRM systems that, uh, the browser may, may or may not support.

[00:46:52] **Francois:** And so it provides a way for an application to receive encrypted content, pass it over get the, the, the right keys, the right license keys from a whatever system actually. Pass that logic over to the, and to the user agent, which passes, passes it over to, uh, the CDM system, which is kind of black box in, uh, that does its magic to get the right, uh, decryption key and then the, and to decrypt the content that can be rendered.

[00:47:21] **Francois:** The encrypted media extensions triggered a, a hell of a lot of, uh, controversy. because it's DRM and DRM systems, uh, many people, uh, uh, things should be banned, uh, especially on the web because the, the premise of the web is that the, the user has trusts, a user agent. The, the web browser is called the user agent in all our, all our specifications.

[00:47:44] **Francois:** And that's, uh, that's the trust relationship. And then they interact with a, a content provider. And so whatever they do with the content is their, I guess, actually their problem. And DRM introduces a third party, which is, uh, there's, uh, the, the end user no longer has the control on the content.

[00:48:03] **Francois:** It has to rely on something else that, Restricts what it can achieve with the content. So it's, uh, it's not only a trust relationship with its, uh, user agents, it's also with, uh, with something else, which is the content provider, uh, in the end, the one that has the, uh, the license where provides the license.

[00:48:22] **Francois:** And so that's, that triggers, uh, a hell of a lot of, uh, of discussions in the W3C degenerated, uh, uh, into, uh, formal objections being raised against the specification. and that escalated to, to the, I mean, at all leverage it. It's, it's the, the story in, uh, W3C that, um, really, uh, divided the membership into, opposed camps in a way, if you, that's was not only year, it was not really 50 50 in the sense that not just a huge fights, but the, that's, that triggered a hell of a lot of discussions and a lot of, a lot of, uh, of formal objections at the time.

[00:49:00] **Francois:** Uh, we were still, From a governance perspective, interestingly, um, the W3C used to be a dictatorship. It's not how you should formulate it, of course, and I hope it's not going to be public, this podcast. Uh, but the, uh, it was a benevolent dictatorship. You could see it this way in the sense that, uh, the whole process escalated to one single person was, Tim Burners Lee, who had the final say, on when, when none of the other layers, had managed to catch and to resolve, a conflict.

[00:49:32] **Francois:** Uh, that has hardly ever happened in, uh, the history of the W3C, but that happened to the two for EME, for encrypted media extensions. It had to go to the, uh, director level who, uh, after due consideration, uh, decided to, allow the EME to proceed. and that's why we have a, an EME, uh, uh, standard right now, but still re it remains something on the side.

[00:49:56] **Francois:** EME we're still, uh, it's still in the scope of the media working group, for example. but the scope, if you look at the charter of the working group, we try to scope the, the, the, the, the updates we can make to the specification, uh, to make sure that we don't reopen, reopen, uh, a can of worms, because, well, it's really a, a topic that triggers friction for good and bad reasons again.

[00:50:20] **Jeremy:** And when you talk about the media source extensions, that is the ability to write custom code to stream video in whatever way you want. You mentioned, the MPEG-DASH and http live streaming. So in that case, would that be the developer gets to write that code in JavaScript that's executed by the browser?

[00:50:43] **Francois:** Yep, that's, uh, that would be it. and then typically, I guess the approach nowadays is more and more to develop low level APIs into W3C or web in, in general, I guess. And to let, uh. Libraries emerge that are going to make lives of a, a developer, uh, easier. So for MPEG DASH, we have the DASH.js, which does a fantastic job at, uh, at implementing the complexity of, uh, of adaptive streaming.

[00:51:13] **Francois:** And you just, you just hook it into your, your workflow. And that's, uh, and that's it.


## Encrypted Media Extensions are closed source

[00:51:20] **Jeremy:** And with the encrypted media extensions I'm trying to picture how those work and how they work differently. 

[00:51:28] **Francois:** Well, it's because the, the, the, the key architecture is that the, the stream that you, the stream that you may assemble with a media source extensions, for example. 'cause typically they, they're used in collaboration. When you hook the, hook it into the video tag, you also. Call EME and actually the stream goes to EME.

[00:51:49] **Francois:** And when it goes to EME, actually the user agent hands the encrypted stream. You're still encrypted at this time. Uh, encrypted, uh, stream goes to the CDM content decryption module, and that's a black box well, it has some black, black, uh, black box logic. So it's not, uh, even if you look at the chromium source code, for example, you won't see the implementation of the CDM because it's a, it's a black box, so it's not part of the browser se it's a sand, it's sandboxed, it's execution sandbox.

[00:52:17] **Francois:** That's, uh, the, the EME is kind of unique in, in this way where the, the CDM is not allowed to make network requests, for example, again, for privacy reasons. so anyway, the, the CDM box has the logic to decrypt the content and it hands it over, and then it depends, it depends on the level of protection you.

[00:52:37] **Francois:** You need or that the system supports. It can be against software based protection, in which case actually, a highly motivated, uh, uh, uh, attacker could, uh, actually get access to the decoded stream, or it can be more hardware protected, in which case actually the, it goes to the, uh, to your final screen.

[00:52:58] **Francois:** But it goes, it, it goes through the hardware in a, in a mode that the US supports in a mode that even the user agent doesn't have access to it. So it doesn't, it can't even see the pixels that, uh, gets rendered on the screen. There are, uh, several other, uh, APIs that you could use, for example, to take a screenshot of your, of your application and so on.

[00:53:16] **Francois:** And you cannot apply them to, uh, such content because they're just gonna return a black box. again, because the user agent itself does not see the, uh, the pixels, which is exactly what you want with encrypted content.

[00:53:29] **Jeremy:** And the, the content decryption module, it's, if I understand correctly, it's something that's shipped with the browsers, but you were saying is if you were to look at the public source code of Chromium or of Firefox, you would not see that implementation.


## Content Decryption Module (Widevine, PlayReady)

[00:53:47] **Francois:** True. I mean, the, the, um, the typical examples are, uh, uh, widevine, so wide Vine. So interestingly, uh, speaking in theory, these, uh, systems could have been provided by anyone in practice. They've been provided by the browser vendors themselves. So Google has Wide Vine. Uh, Microsoft has something called PlayReady. Apple uh, the name, uh, escapes my, uh, sorry. They don't have it on top of my mind. So they, that's basically what they support. So they, they also own that code, but in a way they don't have to. And Firefox actually, uh, they, uh, don't, don't remember which one, they support among these three. but, uh, they, they don't own that code typically.

[00:54:29] **Francois:** They provide a wrapper around, around it. Yeah, that's, that's exactly the, the crux of the, uh, issue that, people have with, uh, with DRMs, right? It's, uh, the fact that, uh, suddenly you have a bit of code running there that is, uh, that, okay, you can send box, but, uh, you cannot inspect and you don't have, uh, access to its, uh, source code.

[00:54:52] **Jeremy:** That's interesting. So the, almost the entire browser is open source, but if you wanna watch a Netflix movie for example, then you, you need to, run this, this CDM, in addition to just the browser code. I, I think, you know, we've kind of covered a lot.


## Documenting what's available in browsers for developers

[00:55:13] **Jeremy:** I wonder if there's any other examples or anything else you thought would be important to mention in, in the context of the W3C.

[00:55:23] **Francois:** There, there's one thing which, uh, relates to, uh, activities I'm doing also at W3C. Um. Here, we've been talking a lot about, uh, standards and, implementations in browsers, but there's also, uh, adoption of these browser, of these technology standards by developers in general and making sure that developers are aware of what exists, making sure that they understand what exists and one of the, key pain points that people, uh.

[00:55:54] **Francois:** Uh, keep raising on, uh, the web platform is first. Well, the, the, the web platform is unique in the sense that there are different implementations. I mean, if you, 

[00:56:03] **Francois:** Uh, anyway, there are different, uh, context, different run times where there, there's just one provided by the company that owns the, uh, the, the, the system. The web platform is implemented by different, uh, organizations. and so you end up the system where no one, there's what's in the specs is not necessarily supported.

[00:56:22] **Francois:** And of course, MDN tries, uh, to document what's what's supported, uh, thoroughly. But for MDN to work, there's a hell of a lot of needs for data that, tracks browser support. And this, uh, this data is typically in a project called the Browser Compat Data, BCD owned by, uh, MDN as well. But, the Open Web Docs collective is a, uh, is, uh, the one, maintaining that, uh, that data under the hoods.

[00:56:50] **Francois:** anyway, all of that to say that, uh, to make sure that, we track things beyond work on technical specifications, because if you look at it from W3C perspective, life ends when the spec reaches standards, uh, you know, candidate rec or rec, you could just say, oh, done with my work. but that's not how things work.

[00:57:10] **Francois:** There's always, you need the feedback loop and, in order to make sure that developers get the information and can provide the, the feedback that standardization can benefit from and browser vendors can benefit from. We've been working on a project called web Features with browser vendors mainly, and, uh, a few of the folks and MDN and can I use and different, uh, different people, to catalog, the web in terms of features that speak to developers and from that catalog.

[00:57:40] **Francois:** So it's a set of, uh, it's a set of, uh, feature IDs with a feature name and feature description that say, you know, this is how developers would, uh, understand, uh, instead of going too fine grained in terms of, uh, there's this one function call that does this because that's where you, the, the kind of support data you may get from browser data and MDN initially, and having some kind of a coarser grained, uh, structure that says these are the, features that make sense.

[00:58:09] **Francois:** They talk to developers. That's what developers talk about, and that's the info. So the, we need to have data on these particular features because that's how developers are going approach the specs. Uh. and from that we've derived the notion of baseline badges that you have, uh, are now, uh, shown on MDN on can I use and integrated in, uh, IDE tool, IDE Tools such as visual, visual studio, and, uh, uh, libraries, uh, linked, some linters have started to, um, to integrate that data.

[00:58:41] **Francois:** Uh, so, the way it works is, uh, we've been mapping these coarser grained features to BCDs finer grained support data, and from there we've been deriving a kind of a, a batch that says, yeah, this, this feature is implemented well, has limited availability because it's only implemented in one or two browsers, for example.

[00:59:07] **Francois:** It's, newly available because. It was implemented. It's been, it's implemented across the main browser vendor, um, across the main browsers that people use. But it's recent, and widely available, which we try to, uh, well, there's been lots of discussion in the, in the group to, uh, come up with a definition which essentially ends up being 30 months after, a feature become, became newly available.

[00:59:34] **Francois:** And that's when, that's the time it takes for the, for the versions of the, the different versions of the browser to propagate. Uh, because you, it's not because there's a new version of a, of a browser that, uh, people just, Ima immediately, uh, get it. So it takes a while, to propagate, uh, across the, uh, the, the user, uh, user base.

[00:59:56] **Francois:** And so the, the goal is to have a, a, a signal that. Developers can rely on saying, okay, well it's widely available so I can really use that feature. And of course, if that doesn't work, then we need to know about it. And so we are also working with, uh, people doing so developer surveys such as state of, uh, CSS, state of HTML, state of JavaScript.

[01:00:15] **Francois:** That's I guess, the main ones. But also we are also running, uh, MDN short surveys with the MDN people to gather feedback on. On the, on these same features, and to feed the loop and to, uh, to complete the loop. and these data is also used by, internally, by browser vendors to inform, prioritization process, their prioritization process, and typically as part of the interop project that they're also running, uh, on the site

[01:00:43] **Francois:** So a, a number of different, I've mentioned, uh, I guess a number of different projects, uh, coming along together. But that's the goal is to create links, across all of these, um, uh, ongoing projects with a view to integrating developers, more, and gathering feedback as early as possible and inform decision.

[01:01:04] **Francois:** We take at the standardization level that can affect the, the lives of the developers and making sure that it's, uh, it affects them in a, in a positive way.

[01:01:14] **Jeremy:** just trying to understand, 'cause you had mentioned that there's the web features and the baseline, and I was, I was trying to picture where developers would actually, um, see these things. And it sounds like from what you're saying is W3C comes up with what stage some of these features are at, and then developers would end up seeing it on MDN or, or some other site.

[01:01:37] **Francois:** So, uh, I'm working on it, but that doesn't mean it's a W3C thing. It's a, it's a, again, it's a, we have different types of group. It's a community group, so it's the Web DX Community group at W3C, which means it's a community owned thing. so that's why I'm mentioning a working with a representative from, and people from MDN people, from open Web docs.

[01:02:05] **Francois:** so that's the first point. The second point is, so it's, indeed this data is now being integrated. If you, and you look, uh, you'll, you'll see it in on top of the MDN pages on most of them. If you look at, uh, any kind of feature, you'll see a, a few logos, uh, a baseline banner. and then can I use, it's the same thing.

[01:02:24] **Francois:** You're going to get a baseline, banner. It's more on, can I use, and it's meant to capture the fact that the feature is widely available or if you may need to pay attention to it. Of course, it's a simplification, and the goal is not to the way it's, the way the messaging is done to developers is meant to capture the fact that, they may want to look, uh, into more than just this, baseline status, because.

[01:02:54] **Francois:** If you take a look at web platform tests, for example, and if you were to base your assessment of whether a feature is supported based on test results, you'll end up saying the web platform has no supported technology because there are absolutely no API that, uh, where browsers pass 100% of the, of the, of the test suite.

[01:03:18] **Francois:** There may be a few of them, I don't know. But, there's a simplification in the, in the process when a feature is, uh, set to be baseline, there may be more things to look at nevertheless, but it's meant to provide a signal that, uh, still developers can rely on their day-to-day, uh, lives.

[01:03:36] **Francois:** if they use the, the feature, let's say, as a reasonably intended and not, uh, using to advance the logic.

[01:03:48] **Jeremy:** I see. Yeah. I'm looking at one of the pages on MDN right now, and I can see at the top there's the, the baseline and it, it mentions that this feature works across many browsers and devices, and then they say how long it's been available. And so that's a way that people at a glance can, can tell, which APIs they can use.

[01:04:08] **Francois:** it also started, uh, out of a desire to summarize this, uh, browser compatibility table that you see at the end of the page of the, the bottom of the page in on MDN. but there are where developers were saying, well, it's, it's fine, but it's, it goes too much into detail. So we don't know in the end, can we, can we use that feature or can we, can we not use that feature?

[01:04:28] **Francois:** So it's meant as a informed summary of, uh, of, of that it relies on the same data again. and more importantly, we're beyond MDN, we're working with tools providers to integrate that as well. So I mentioned the, uh, visual Studio is one of them. So recently they shipped a new version where when you use a feature, you can, you can have some contextual, uh.

[01:04:53] **Francois:** A menu that tells you, yeah, uh, that's fine. You, this CSS property, you can, you can use it, it's widely available or be aware this one is limited Availability only, availability only available in Firefox or, or Chrome or Safari work kit, whatever.

[01:05:08] **Jeremy:** I think that's a good place to wrap it up, if people want to learn more about the work you're doing or learn more about sort of this whole recommendations process, where, where should they head?

[01:05:23] **Francois:** Generally speaking, we're extremely open to, uh, people contributing to the W3C. and where should they go if they, it depends on what they want. So I guess the, the in usually where, how things start for someone getting involved in the W3C is that they have some kind of a technology in mind.

[01:05:41] **Francois:** They have some kind of pet project, something that they care about. And so they find the right GitHub repository in this case probably, and they start a discussion with people who are actually develoPNG the spec. And they may be feedback, it may be negative feedback, but it may be a, Hey, I had this idea So there are different places where you can raise ideas.

[01:06:01] **Francois:** Um, so I don't know where to point at a single place. I guess I mean, there's probably a contact email, but it doesn't make a lot of sense. Um, and, uh, and that's usually how things start. And then, uh, and then when people get involved, some of them will like it and, uh, it's always a pleasure with someone, uh, enjoys interacting, uh, on, on standards and will find ways to, encourage, uh, their, their contributions.

[01:06:27] **Francois:** Uh, of course if they represent, uh. Companies, there will come a time where, uh, the, the process is going to kick in for patent reasons for different, uh, uh, different things and for membership fees. because again, that's how the W3C, the budget, uh, from the BFC, come from membership fees. and, and so, uh, things will kick in and, uh, we'll get to the next level.

[01:06:52] **Francois:** But, uh, initially it's really about just come find a feature you that doesn't work for you, uh, where you find something that looks clunky in one of the spec. If you read the spec, it's, uh, not always a fan fancy read, but, uh, and report, uh, report a bug, not in the implementation, but in the spec.

[01:07:10] **Francois:** Um, and start or propose a new idea to the, to the group that develops the specification you like. Um, and we'll take it from there, and we're very happy to have that feedback.

[01:07:22] **Jeremy:** So maybe find the, if there is an existing specification, go find the, the GitHub repository where that's located. if you have something that you want implemented newly, maybe find the working group that would be related and start from there.

[01:07:41] **Francois:** Absolutely.

[01:07:42] **Jeremy:** Francois, thank you so much for, for chatting with me today. I think we, we covered a lot about the, the W3C and, and how it relates to all the things that we use in our browsers every day. So thank you.

[01:07:53] **Francois:** Thanks a lot for the invitation again. It's been a pleasure.
