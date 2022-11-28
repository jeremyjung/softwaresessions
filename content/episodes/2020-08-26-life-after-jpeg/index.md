+++
title = "Life after JPEG with Henri Helvetica"

description = "Henri talks web performance and how WebP could become the main image format of the web."

[extra]
episode_url = "https://pinecast.com/listen/8587e324-111b-4512-a61e-b4bf45a1b0ac.mp3"
social_title = "Life after JPEG"
social_banner = "027-henri-helvetica.png"
social_description = "How WebP could become the main image format of the web"
+++

Henri is a frequent conference speaker and organizer of the Toronto [Web Performance](https://www.meetup.com/Toronto-Web-Performance-Group/) and [JAMStack](https://twitter.com/JAMstackTORONTO) meetups.

We discuss:
- Managing images with features like lazy loading and the picture tag 
- Handling varying network conditions on mobile
- Making designers a part of the performance conversation
- The WebP image format that could replace JPEG and PNG
- Ways the GIF can be an MP4 in disguise
- How lighthouse has given websites a visible target for performance
- What we can learn from "lite" news sites

### Conference Talks
- [A Decade of Disciplined Delivery](https://www.youtube.com/watch?v=HC1eVj5cQOo)
- [Shape Of The Web](https://www.youtube.com/watch?v=SeV_Pqw5egU)
- [Moving Pictures: A Snapshot At the Future of Web Media](https://www.youtube.com/watch?v=TSjAiwFMB34)

### Related Links
- [@HenriHelvetica](https://twitter.com/HenriHelvetica)
- [Cloudinary](https://cloudinary.com/)
- [Picture tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture)
- [Network Information API](https://developer.mozilla.org/en-US/docs/Web/API/Network_Information_API)
- [WebP](https://developers.google.com/speed/webp)
- [Responsive images done right: a guide to picture and srcset](https://www.smashingmagazine.com/2014/05/responsive-images-done-right-guide-picture-srcset/)
- [Use srcset to automatically choose the right image](https://web.dev/use-srcset-to-automatically-choose-the-right-image/)
- [Mozilla: Improving JPEG Image Encoding](https://blog.mozilla.org/blog/2014/07/15/improving-jpeg-image-encoding/) (Mozilla explains why they want to stick with JPEG in 2014)
- [The Great JPEG 2000 Debate: Analyzing the Pros and Cons to Widespread Adoption](https://cloudinary.com/blog/the_great_jpeg_2000_debate_analyzing_the_pros_and_cons_to_widespread_adoption)
- [How JPEG XL compares to other image codecs](https://cloudinary.com/blog/how_jpeg_xl_compares_to_other_image_codecs)
- [Serve images in next-gen formats](https://web.dev/uses-webp-images/)
- [JPEG XR](https://jpeg.org/jpegxr/)
- [High Efficiency Image File Format](https://nokiatech.github.io/heif/)
- [Using HEIF or HEVC media on Apple devices](https://support.apple.com/en-us/HT207022)
- [AVIF for Next-Generation Image Coding](https://netflixtechblog.com/avif-for-next-generation-image-coding-b1d75675fe4)
- [AV1 & Media Codecs](https://research.mozilla.org/av1-media-codecs/)
- [WebP is now supported on Safari 10](https://groups.google.com/a/webmproject.org/forum/#!msg/webp-discuss/J8HLhTaklYE/RAtX14MEAQAJ) (WebP support was added in a Safari beta but then removed)
- [Safari 14 Beta Release Notes](https://developer.apple.com/documentation/safari-release-notes/safari-14-beta-release-notes) (4 years later, WebP is officially added to Safari)
- [HTTP Archive Almanac: Image format usage](https://almanac.httparchive.org/en/2019/media#image-formats) (Shows the relatively small footprint of WebP)
- [Native image lazy-loading for the web](https://web.dev/native-lazy-loading/)
- [How To Defer, Lazy-Load And Act With IntersectionObserver](https://www.smashingmagazine.com/2018/01/deferring-lazy-loading-intersection-observer-api/)
- [How Medium does progressive image loading](https://jmperezperez.com/medium-image-progressive-loading-placeholder/)
- [Above the fold in web design](https://en.wikipedia.org/wiki/Above_the_fold#In_web_design)
- [An update on mobile CPUs and the Performance Inequality Gap](https://twitter.com/slightlylate/status/1233275220275818498)
- [Web Page Test](https://www.webpagetest.org/)
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)
- [CNN lite](http://lite.cnn.com/)
- [NPR text only](https://text.npr.org/)
- [User Timing API - Measuring User Experience Performance](https://www.keycdn.com/blog/user-timing)

### People mentioned during this episode

- [@burkeholland](https://twitter.com/burkeholland)
- [@kornelski](https://twitter.com/kornelski)
- [@andydavies](https://twitter.com/andydavies)
- [@patmeenan](https://twitter.com/patmeenan)
- [@slightlylate](https://twitter.com/slightlylate)
- [@souders](https://twitter.com/souders)

Music by Crystal Cola: [12:30 AM](https://crystalcola.bandcamp.com/track/12-30-am) / [Orion](https://crystalcola.bandcamp.com/track/orion)

---

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy:** [00:00:00] Hey, this is Jeremy Jung and you are listening to software sessions. This episode, I'm talking to Henri Helvetica. He's a freelance developer with a focus on performance engineering.  He's also involved in the Toronto web performance and JAMstack meetup groups. And we discuss why images and performance are so tightly tied together. 

We also went deep into what life after JPEG might look like with the introduction of formats, like web P. And we talk about tools that can help you during your web performance journey. 

Henri is a big runner so i asked him if he started his day with a run.

**Henri:** [00:00:36] Thank you for the introduction. And good morning. And with regards to a run, I wanted to first thing in the morning, and as we were talking about, getting up early just moments ago, I have my alarm set for 6:30.

I tend to sort of open my eyes up around quarter to six, and figure out like how this run is going to go, but it was raining this morning. so I was a little upset, went and looked outside. The rain stopped by 7:00 AM. I was thinking, okay, maybe I should head out now. And as I was getting ready to head out, the rain started again and I thought to myself, okay, it's not going to happen simply because I knew I was doing this podcast.

So I want to be back in time and fresh. And, and afterwards, I think I'm going to watch, this, Microsoft event they have online, MS create. yeah, run does not look good today.

And it's funny. I was speaking to Burke, Holland from Microsoft. He said that he sent the clouds my way, knowing that it would force me to stay in.

**Jeremy:** [00:01:34] They are a big cloud company, right?

**Henri:** [00:01:36] That's a good one. I like that.

That was good. I'm going to have to keep that one.

**Jeremy:** [00:01:42] You're, you're pretty deep into the web performance space. What are some of the biggest mistakes you see people making on the front end?

**Henri:** [00:01:52] I mean, web performance I, I consider it a bit of a dark art. There's lots involved and, and much of it may not seem, very clear to the sort of like average developer at times. but with any auditing that takes place, whether it be web performance or accessibility or, UX, overall, you're always going to have some low hanging fruit, and, One of those fruits  is, image management. and I think that, you tend to find a lot of people sort of disregarding the importance of making sure that images are set properly, as a resource loading on your page. and. It's important for a number of reasons. most notably is the fact that it's always, absolutely going to be the heaviest resource on your page. Okay. Barring video. and you know, video in the last say couple of years, specially, especially this year has become a lot more prominent. So I mean, that's a bit of a different conversation, because, you know, you could quite often find pages with no videos. So I didn't want to go too deeply into that topic, but, you know, you will find images 99.9% of the time and images are challenging. Image management has become a lot more complicated, for a number of reasons. Retina screens brought in a particular challenge with regards to how to select the right image. and then you also have more than ever people are really paying attention to, connectivity, understanding that, connectivity may vary along like a five minute period, what was 4G at the start of your walk might suddenly downgrade to like very poor 4G or even like moderate 3g. Then you might go  into your home and back out. And so you have  varying conductivity that, ultimately the site doesn't care about. It's like, Hey, just load this image.

You have these things to take in consideration and you luckily have some very brilliant engineers out there that are trying to make these accommodations. So, I would certainly say, images, Have been, are, and potentially will continue to be, one of the bigger challenges in terms of a low hanging fruit.

**Jeremy:** [00:04:15] I want to go a little more into images. If you have the most basic case. Let's say you're not building a single page application. You're building a traditional, like just a document website. What are some of the ways that you should be treating images? you mentioned retina, how do we ensure we're only sending retina assets to people with retina devices? Should we be loading images in a lazy fashion? Like what are some of the best practices there?

**Henri:** [00:04:47] The ultimate best practice, at this point, and it's a bit of a cop out, but, it would be to, outsource the work. and I say that simply because I think it's, it's become, enough of a challenge that there are some companies out there that are solely set up to do that work for you?

Obviously people like Cloudinary and there's a bunch of others as well, that have been very upfront and outspoken in their need to let people know that this is the kind of work that they do. And, that's their specialty now.

Barring that, there are a number of ways you can, look at, managing images. Obviously I'd say, one of the earliest revelations that came along the way when dealing with images and dealing with a retina, non retina, when we had and obviously, formats as well. picture tag srcset, and the ability to  pinpoint what you wanted to send under what conditions.

And, that was fantastic at the time. And, and everyone felt like, okay, we've, we've come up with a great solution, but along the way as well. What ended up happening is that you had these ever growing blocks of code. And I believe it was Brad frost once, posted, I think a screenshot of a code block just to handle, retina, not retina, et cetera.

And it was so huge. He just sat there and was like, I'm not going to do this, there's no way, I need this massive block of code just to serve a couple of images under the right conditions. Things like that came about, and obviously as much as they did work, there was a sense that, things need to be a bit more simplified.

I mean, people are still working on that, but I mean, what that also didn't do is. take in consideration, things like network conditions. And so you can have like this amazing, beautifully scripted block of code for images, but that still didn't take into consideration whether or not you were getting proper, bandwidth and, good, round trip times and whatnot. And that's where things like, network information API came around and whether or not you want to serve a particular images under particular conditions. And that's where it starts to get pretty complicated. 

**Jeremy:** [00:07:23] And this code you were referring to, this is all JavaScript?

**Henri:** [00:07:27] Oh no no. Th th this is all just like classic HTML. I mean, we've not, we've not even gone into the JavaScript element yet, But, no this is all just like straightforward HTML that was there for you to sort of manage, images as best as possible.

And, and like I said, the code block could just grow very quickly. If you want to just have like all your options covered, right. or conditions should I say? but again, none of that really delved into the idea that, Oh, we have variant network conditions too. And that sort of threw like an additional curve ball into, what seemed like very simple rudimentary work, you know, loading up an image of a cat, but, it's not the case anymore.

**Jeremy:** [00:08:15] In CSS, for example, there are things like media queries where we could say, the device's screen is this size. So I'm going to send them this type of image. are, are these the types of things you're talking about when you're talking about serving different images to different browsers and devices?

**Henri:** [00:08:34] With regards to different browsers specifically, the picture tag was actually a bit of a revelation there because we had situations where at one point. There was kind of like a fractured, landscape of, image support. you may remember, at the time when web P was starting to, make its way into the conversation.

Even though the webp is like 11 years old, but I feel like, you know, even to this day, a lot of people, like webp what's that I'm not sure. And I remember a couple of years ago when I went on this sort of like image, you know, format management discussion, at conferences, there were people who had no idea what the webp was.

To go back, in history, when the web P was really started to be introduced by Google and, supporting, browsers with the blink engine, there was a moment in time where, Mozilla felt that, we had not extracted all we could out of a JPEG. So their sentiment was that, a sudden introduction of a web P might've been premature.

And in fact, there was a, a blog post that it described their decision into maintaining their sort of support, and additional research into, getting, better compression over the JPEG. A blog post that has since vanished, but I think if you go to the Wayback machine, you might be able to find it. And then on top of that you had the idea that the JPEG and JPEG 2000 and JPEG XR were sort of still out there floating around for people who want to experiment and really, really dive in a little more, because at the time you had CDN companies like say Akamai that we're working with, big retailers and, they had obviously a lot invested in making sure that, they could squeeze all the data they could, out of, certain assets like images. So you could have say a website, like, I remember in one of my talks, I gave this example like forever 21, I could talk about a company that's, gone bankrupt. So it's not like I have stock in that company.

**Jeremy:** [00:10:44] Yeah. They're not going to come get you now.

**Henri:** [00:10:46] Exactly, exactly. Right. It's like, here's a couple of pennies, man. Let me give me some, give me some stock. but, I, I, remember in my talk, I showed that, in devtools in different browsers you saw, you know, the JPEG 2000 being served and you saw the JPEG XR being served. You saw obviously, in Mozilla's case, a JPEG being served.

Now I believe in Chrome. you were getting the webp. So the picture tag definitely helped with that, you know, with people who really want to be, very focused and, and trying to serve the best, format and most compressed. option possible, you know, very, disciplined delivery of assets because that's what it is at the end of the day. Trying to be as disciplined as possible and trying to find the absolute best possible, solution to, to sort of lessen the load.

**Jeremy:** [00:11:38] Is WebP kind of the equivalent of a JPEG. It's another lossy, image format, but is perhaps more efficient 

**Henri:** [00:11:46] So the WebP is a very interesting format. So, history. WebP came from, a video format. So the WebP is actually a product of the WebM. Some of the more interesting and more, data efficient, image formats are all actually stemming from video, which is really interesting.

So, the HEIC, which came from the HEVC, and, and then very future conversation, AV1 birthed the AVIF. AVIF and again, that's video to still image, but let's get back to the WebP it was made for the web, essentially. Visual fidelity it may not be the best format, but in terms of what is best for the web resources being transmitted down the wire, the WebP makes a great case. and I'll list a couple of features real quickly, obviously a very aggressive codec compression is 10, 20, 30%, better than PNGs. And better than JPEGs. Their chroma subsampling, is locked at 420. So for those who may or may not know chroma subsampling, basically it has to do with, it's sort of like the removal of certain colors that, may not be super perceivable to the eye.

And so the fidelity remains to an extent, and essentially they removed some data that you probably, you know, yeah the average person wouldn't really catch. And it also had transparency, which made it obviously a lot more attractive because obviously the JPEG didn't have that.

And, at one point, actually, and I've mentioned this a few times and you know, I was lucky enough to have a conversation with a Chrome PM. just about four years ago, he had mentioned to me The web P they had specifically the PNG format in their sites, as the felt that, feature for feature, they're aligned well enough that they felt that they could replace every PNG on the net  with a webp.

I also say that because the WebP came in two flavors lossless and lossy. Obviously the lossy one being the most attractive, but there is also a lossless option. So for those who really want to hang on to that fidelity and they, they refuse to let them go. There's a lossless format as well.

So, the WebP on paper was an attractive format. But early on, some of the challenges, was encoding, was support. For people who are just so used to PNGs and JPEGs and, and God forbid GIFs, the majority of the software out there had just endless support for those three, even SVGs, but the WebP not the case. There was some work involved in trying to get the WebP into sort of like the ecosystem, but it wasn't going to happen without some of the more proper software outfits not supporting it. Say for example, Photoshop, there's a bit of a potentially outdated plugin that's been around and now not even supported by the original company that put it out, for Photoshop. And, you can sort of go through the litany of other sort of popular software, outfits that may or may not be supporting it to this day.

**Jeremy:** [00:15:15] In terms of the best practice for images, you said there's a picture tag that will let you use a different format depending on the user's browser. So if you were using Chrome now, I suppose that it could send the user a WebP. but if they were using Safari, maybe it would have to send them a JPEG or PNG.

**Henri:** [00:15:39] Yeah, it's funny you should mention Safari. I can go back and finish up my WebP story. Web P was slowly gaining and I do mean slowly gaining some recognition, I don't want to list it as popularity, but some recognition.

Mozilla had doubled down in the JPEG. You had the WebP, JPEG, for sure. And then whatever else you wanted to use that was on the fringes of popularity, like the JPEG 2000 and the JPEG XR, 2000 being supported by Apple, and XR being supported by Microsoft. Then a significant moment in format history, Mozilla had a moment of clarity and they reopen, the bug to provide support to the WebP. And which was a bit of a, you know, I don't want to say a shocker. But, had sort of decided that, Hey, you know what, we probably need to do this.

So they reopened, that bug, again in history, and sort of significant in a sense that for like a week, webkit, specifically Safari supported webp. And it was like a very bizarre moment. And he got pulled ASAP. It was like grand opening, grand closing, literally.

And I could send you that link and this had an article about it. that was like, you know, no knew what was going on. But at one point we'll say about a year to two years ago, I think. First of all, you had Chrome and Blink engine supporting webP. You had Mozilla who had finally announced that, it was in nightly. Also somewhere in between, Edge had moved over to Chromium and they sort of quietly announced that they had WebP support. So, at the top of 2020, you had three of the four majors all supporting WebP and then hell froze over about a month and a half ago, at WWDC at Apple headquarters.

And they announced WebP support for, Safari 14. So basically in about a couple of years, you went from one to four of the majors supporting web P. and it is significant in a sense that, A well known, image researcher, developer, engineer, Cornell. I can never pronounce his last name, but, so I won't, but, I'm a big fan of his work. He's actually the author of imageoptim. image, optimization tool. He put out this tweet saying that he felt some point next year, WebP could essentially be the only format you need. and it actually does make some sense, because if you're going to have the four majors on board and, and all the other browsers who are running off the blink engine, You know, we could, we could see the, the web P format climb significantly in, in presence on the web.

Because as of right now, if you go to the HTTP archive, WebP is still in relatively trace amounts, on the web. and again, for a number of reasons from like tooling to developer, knowledge. It's going to be pretty interesting to see what happens.

**Jeremy:** [00:19:09] WebP it sounds like it's going to be able to replace JPEGs and PNGs because it has that lossless option. How about, how about GIFs? Are we going to be able to have animated pictures in WebP?

**Henri:** [00:19:22] The big WebP proponents will tell you yes. And, I mean, I'm going to go back to that statement you made with regards to, why the WebP is going to be, replacing the JPEG and the PNG part of the reason and I think specifically why it feels it can replace a P because I think essentially people will still reach out to the PNG as a lossless format for that transparency element, and no other image format out of the classic four, had that as a lossy option. So now back to what you were saying with respect to the animated GIFs, As much as I'm not a huge fan of the animated GIF, we have to live with the fact that people love them. 

**Jeremy:** [00:20:13] and they definitely love them.

**Henri:** [00:20:15] they absolutely like imagine Twitter with no animated gifs. it's almost like it'd be like empty but it's, it is interesting because, For the most part, the animated GIF has been replaced by the MP4. Quite often when you go into dev tools and, and look at, The entrails of this GIF, you believe you sent off a, it's actually an MP4 now, that was done for a number of reasons, specifically, storage because, MP4 versus GIF in terms of storage, huge difference in terms of size and, and some of these GIF farms realized that very early and, you know, you can have, storage costs, balloon out of control, just cause, you know, you want to carry a GIF. That was part of it. I've actually never, I mean, I shouldn't say never, I've seen an animated WebP once. Like I'm assuming it probably loops as well.

So on paper, yes. There would be probably an argument for that to take place, but also for that to take place, the services that are out there, giving you these GIFs will have to on their own, do the encoding. So you can sort of like drag this, this animated, image, and hopefully it will be a WebP that'll be the one, early challenge.

And, and again, I get back to the idea that we as just everyday persons have the, the tools and the encoding capabilities either on our phones or our computers to just say, Oh yeah, I want WebP. So there is a bit of a developer education that's going to have to take place, let alone consumer education right? You know, the average person knows what a GIF is. Devs don't know what WebPs are. So I don't, I don't imagine, individuals will. So there's going to be that I think hurdle along the way. But on paper yeah, it would be, it would be, probably an apt replacement.

**Jeremy:** [00:22:25] That is interesting about how you mentioned a lot of the times where we would usually use a GIF. We now use an MP4, because that makes me wonder when. Someone is in a discord room, for example, and there's animated images everywhere. even if somebody thinks they're using GIFs, those may actually all be MP4s.

Is that, is that right?

**Henri:** [00:22:47] Absolutely. I'll tell you a quick story. I remember, one of my earliest talks on images. I'd mentioned that and the next day. I ran into a developer, and a speaker actually, who was, at my talk. And, he mentioned how they didn't believe me. And they went into dev tools.

And, it was like, So, for everyone who didn't see that I just made this sort of like a mind blown face. and, and they told me that like, Hey, I was suspicious of that comment and I went into dev tools and they had no idea. 

**Jeremy:** [00:23:27] Yeah. 

**Henri:** [00:23:29] I actually felt good for a minute, you know, but, but yeah, that's, what's happening.

And, and again, we're talking about, The availability to still have, the animation, but to save on storage, and even though, a gift may have that classic choppy look and feel, and you're like, Oh, that's gotta be a GIF, but it's just the choppy look and feel as an MP4,  it's being done, because they do have the capabilities.

Now getting back to that WebP conversation, whether or not they'll be able to, get all that encoding done. and, and, and suddenly, you know, their terabytes or petabytes of GIFs are going to be turning into, WebP. I'm not sure, but we'll see.

**Jeremy:** [00:24:15] Yeah, but it sounds like if they're being turned into MP4 files to the end user, it really doesn't matter.

**Henri:** [00:24:24] Ultimately that is, the challenge, right. as developers, we're making sure that, you know, we are disciplined as possible, but the end user doesn't care, is it looping? Does it work? can I post it on my page? That's it, very early in fact, there was a situation where, Facebook who have been, very aggressive in, exploring performance, opportunities and how to save, data, Quite often they're very early adopters.

There was a point where they were starting to serve webp and they found out people were often just dragging stuff to the desktop to share either with friends or somehow. And they're realizing that, the WebP was being supported in the browser, but nowhere else. And so there, there were some complaints.

And then at one point, I think they were trying to do something a Chrome where when you drag the WebP out of a window, it would be encoded into like PNG a by the time we got to your desktop little things like that. But what that described is the user experience had to be absolutely seamless.

People do not care. And they just want to know that the images went from their window to the desktop, or they could just share it with a friend, you know, an iMessage or whatever it is and that's it, that's always part of the challenge, right? Making sure that, that the users can have like a very seamless experience in sharing, in social media,

**Jeremy:** [00:25:54] Yeah, that's interesting because it reminds me of an iPhone in a lot of cases, if you take a photo, it's not. A JPEG, it's a HEIC format and you send that to someone, who can't open it. And you're kind of like what the heck is going on.

**Henri:** [00:26:10] Absolutely. it's funny, you should mention that because I remember when  Heath and you know, that whole ecosystem, was being introduced, at this one WWDC. It might've been two years ago and you just saw Twitter, just kind of not explode, but just going through this, like, what's HEIF, what's HEIF or what's going on?

Hey, Hey, and I remember I gave a talk within like two weeks about HEIF and. Nothing happened. Even within the, Apple ecosystem, that format wasn't even supported by Safari. I think it may have been supported by, maybe image capture, but it had limited support outside of the iOS ecosystem now.

I don't want to sort of like get into like the iOS business, but, if you take your phone and you go into say, a timed shot, like three, 10 seconds, whatever it comes up as a JPEG, which is weird. And I believe the front facing camera, I don't think does a HEIC shot either, but. If you do the, normal sort of like, backside camera shot, that's not burst. I believe it comes up as a HEIC. it's like super weird. and it's very bizarre because now you're talking about, them adopting HEIC or HEIF being the only ones. And now. Providing support for webP, which is super interesting, but that may also have, to do with the fact that, there are patents around, HEIF, and HEIC, and that's something that I've, I've come to sort of, discover.

And, and, and why the support for, open source formats like WebP, and a few of the others, like, AVIF that I talked about, are, are significant, because I think the opportunities are there to sort of bypass those royalty payments.

**Jeremy:** [00:28:06] The current encodings that we use now are any of those, patent encumbered, like are the browser vendors paying royalties for those?

**Henri:** [00:28:16] With respect to the WebP certainly not, None of the browsers are supporting HEIC. So there's probably no payments there that's part of the reasons why, I believe, some of the future, formats that are patented maybe challenged, they'll still make some money, but I don't think that they'll see the sort of windfalls that they have in the past. Just cause there's so much support behind, open source, formats, you know, I'll give you a quick example. Let me know if I'm going off course here because I have all this stuff racing through my head. so AV1 it's an open source video format and AVIF is the sort of, the image format that's, born from AV1.

AV1 is being supported by two to three dozen companies, all companies that have a very vested interest in video. And, all the browser vendors are in because actually Chrome, Mozilla and Cisco were three of the founding partners in this.

And Apple and Safari joined. Does that mean that Apple and Safari specifically is going to support AVIF?  Not necessarily, but at least we see the early interest. and I don't see why Safari won't keep a very close eye on that now there are some people out there who would make the argument that they won't.

Okay. I get it. but the fact that they joined the consortium very early, I think is, is, Hopefully telling, of their interests. So that being said, there will be support, I think, longterm for open source, formats. although, there's, there's one particular format, sort of like lurking in the background right now, which is called the JPEG XL.

And this is another open source format a couple of years ago. when the JPEG was celebrating an anniversary, I think it was the 25th anniversary actually. the, JPEG.org, the organization, put out a call for paper, to sort of see what was out there. See if people were interested in, in, sort of like improving the JPEG, as it stood, because again, 25th anniversary, the JPEG was a little long in the tooth and it's like, what else can we do? so a couple of companies came together. Seven submissions were made actually. Two were picked.

And the two companies that, were selected, were Cloudinary and Google. And Cloudinary had played around with this one format called FUIF, which is a free universal image format. And, Google had been toying around with this one format called PIK. PIK was in the background working because they had also believed that the JPEG was getting a little old and can use some updates. Long story short, the two, projects kind of came together into one and it became like the JPEG XL. and it's been moving along. you could actually, play with it right now. but. Again, not to get into the entails. it's not been adopted by a single browser yet, but they're certainly working on it.

And in the fact that I think you have two image powerhouses, coming together, I think there may be something bubbling, on that end, and the JPEG is, being touted as like the one format for all your needs. So imagine, potentially, the WebP with the added idea and support that would also be able to replace something like an SVG, which is very interesting because the SVG as a vector format has particular features that a raster format can never have. But the JPEG XL feels like boom. You know, they have that covered. And a few other features that, you know, I don't want to get into the entrails too, too, too much, but, it's, it's kind of fun out there right now, you know?

**Jeremy:** [00:32:16] It's interesting because we've had the same formats in the browser for such a long time. We've had the JPEG the GIF the PNG, SVG, seems after all these decades, we're finally getting to the point where we might start seeing, new, new formats take over.

**Henri:** [00:32:36] Yep. And you know, people have to realize that, there's, you know, there are so many things that, that go into, having, so many updates say in the last three or four years or five, part of it's like computing power, there's so much, that goes into, being able to, have these formats readily available. Early days of, of the web P one of the challenges was the fact that it was CPU intensive.

But you know, again, you're talking about the WebP being 11 years old in, you know, in six years, CPU power can change quite a lot from a handheld device to, to your laptop. Right. So who knows what you know is taking place on the enterprise side. but you know, it's funny, you should mention the fact that the formats are all old.

In, in my talks, I mentioned this quite often and just want to remind people that, you know, like you said, the GIF, the SVG, the PNG and JPEG. You're looking at easily, like a hundred years, which is crazy, you know, like I, I joke around in my talks that it's like older than the Rolling Stones, but, that's very important.

We've had HTTP1 and 1.1 For like almost 30 years almost. And, in the last three or four, we've gone H2 and now we're talking H3. If you're looking at the early days of web, you know, no one knew that the web was going to be consumed, in greatest amounts on handheld devices, and handheld devices with moderate power.

I think we're lucky enough that, we have like some iPhones and high end Androids and whatnot, but the average individual is looking for a deal and the deals happen with moderate devices and they have particular, CPU hurdles and, you know, we've needed to make some changes along the way.

Formats being one of them and, protocols being the other, but that's a separate story.

**Jeremy:** [00:34:38] I would think that currently a lot of the devices have dedicated hardware to decode specific image formats, like for example, H264 and, and maybe now that things like web P are gonna be in the browser, there would be dedicated hardware to, to decode that as well.

**Henri:** [00:34:56] And, and these are things that will probably come along. but you know, you still have the fact that you have an absolute trusty in what I like to call the workhorse in, in the JPEG that's always going to be there. I mean the JPEG again, by far, the, the, the best support out there, it's the one that's being delivered, by digital cameras by, you know, Our phones.

So I mean, there's less of a concern, but eventually yes, you do want some hardware decoding. Like, for example, when I brought up the, the AV1 I remember, a speaker from, a talk from an engineer at YouTube, talking about, you know, them experimenting with the AV1 and then realizing that something about like 10 to 12% of their users run very old devices and they had no idea.

And so these are things that you have to take in consideration. And so, if they're finding out that they're on old devices through, you know, trying to serve, you know, next generation video, They're still going to be on these old devices being served next generation, still images.

These are, again, part of these curve balls that engineers are being, pitched, quite often

**Jeremy:** [00:36:18] Yeah, so it seems like this, I guess, dream that we had of. Hey, everything is going to be moving to web P or maybe everything will be moving to AV1 is probably not going to become true for actually quite some time, because like you said, there are still going to be a significant percentage of people who they need to use the old formats because of their old devices or because they're, they're buying low cost devices.

So it doesn't seem like we're going to be able to get away from. The image tag that goes here, we'll give you the JPEG. We'll give you the webp and so on. Yeah.

**Henri:** [00:36:56] Yeah, that, that, that's definitely going to be, you know, it it's like that rough transitional period right where, everything's being supported by everything you needed. And then now you have to get into that transition where it's like, okay, well, you know, maybe it's the hardware that needs to change. Okay. Now we have to make sure that people know that they should request a web P and things like that.

So along the way to nirvana. we have to get a bunch of things sorted out so that, from a user standpoint to a developer standpoint, to like, a hardware, so yeah, I mean, it it goes past browser support. and obviously that's one of the hurdles that's without a doubt. but, once you have the browser support,  that you need, you know, you still have this sort of like the few legs to, go down and, and make sure that, you can have that sort of like perfect situation where it's like, okay, boom.

Now we have like the support that we want. We have the browsers, and then we have the education and that, that, that needs to take place.

**Jeremy:** [00:38:07] We've been talking a lot about things that are, that are coming and I want to bring us back to some of the things that that developers can do now to improve performance or at least improve, perceived performance.

And one of the things we had mentioned earlier, was the concept of image, lazy loading. Like, should we be loading all the images on page load? Or should it be as the user scrolls? And I wonder from your perspective, how should web developers approach that and what are the tools they should use for that?

**Henri:** [00:38:43] I would say you, you actually should be lazy loading. I mean, ideally in an ideal world, you know, you don't, request resources that you're not going to see. and, a while back, I don't know if I could dig this up, but there was a study, sort of indicating that, something like two thirds of, of, of resources were below the fold, on average, and then, on top of that, only about one out of two, users went to the bottom of the page.

So yeah, so you ended up having a bunch of resources below the fold that, quite possibly aren't going to be, needed.

So the advent of lazy loading came about again, you know, wanting to make sure that you're not hampered by a page having to load say 10 megs of resources, just so that you can look at the, first sort of like page and a half of, of information. So that being said, lazy loading became a bit of a priority.

And as you may know, Chrome has natively, added, lazy loading as of right now, I believe in stable, if not for sure canary, and obviously there's some libraries out there that would, that would help you out with, with, that process as well.

And again, I get back to the idea of being disciplined as a developer. And making sure that, Hey, did you want to snack because, I can give you a snack or I can take you to all you can eat, you know? And the all you can need is what we don't need since you only want a snack. So, if that analogy made sense, but, but yeah, I mean, it's, it's super important, you know?

I mean, for example, I think I tweeted this a couple of days ago. someone who's at an agency, sent me a, a site that they had just, pushed and it'd gone live and I'm like, okay, let me take a quick look. You know, it was like 11 megs on, on first load. it was like 99 images. 89 of them were lostless, and everything loaded in one shot.

And it was a fairly long, fairly long page. I mentioned this to them in a quick communication, like, hey, there's a bunch of other issues, but you guys should be using some lazy loading, you know, because again, it's the idea of whether or not, a, a individual is going to go to right down to the bottom of, the page, and, on average that's not the case.

And lazy loading is going to help you manage those assets. for the best user experience possible,

**Jeremy:** [00:41:08] So with that particular page, as an example, it sounds like one of the things that they should do is conditionally load. different qualities of images based on the device you're using. And the other thing would be to do some form of lazy loading so that you, you don't load every image on the page, but instead you load them as the user gets close to them. and this is all being done just through HTML tags? Like there's no JavaScript?

**Henri:** [00:41:39] So barring the native, implementation. you could actually there are a couple of ways that you can set that up now, prior to  the native implementation of lazy loading, we were using the intersection observer API, and what that was essentially, it was kind of like, 

I describe it as like fake lazy loading. so you could actually indicate, you actually set up, through intersection observer, sorta like how far from the viewport you want particular assets to load, and that became, native to the browsers before Lazy loading. Now it had uses beyond images, but, people were starting to use that for images specifically.

That was certainly available now on, you know, outside of using JavaScript, I can't believe you were able to set that up. however, you had mentioned, potentially using, Images, I think you'd mentioned images in a, low quality. Did you mention that at some point?

**Jeremy:** [00:42:48] Yeah. So if you are on, let's say you're on a phone and the device size is small. Maybe you don't need that full 4K resolution image. so it sounded like there was some way within just using HTML that you would be able to, select different images for different devices.

**Henri:** [00:43:11] Oh, so, we're talking about maybe using the, network information API potentially, we're getting into, I guess, JavaScript, not so much HTML, but, you know, you could actually start to conditionally, provide, particular, image qualities.

Depending on the network conditions, obviously now, what that could be is, I don't know, let's talk about baseball, you know, you may have a front page where it's like major league baseball under a crisis, you know, and then you have like a bunch of players, like, on the page in an image, but that might be under ideal conditions, say 4G powerful phone, whatever.

But just say they're under less than ideal network conditions instead of, of, of having the image of the players. You might throw up, the MLB logo. Three colors, made it at SVG. It might be two kilobytes instead of like the 43 that it was for the image of the players.

So the net info API is going to allow you to do, stuff like that. Certainly. there was a point as well, and this was again, a JavaScript implementation where, I mean, if you do, what sort of people know from medium, where they give you that sort of blurred, image, and then it does this little swap to give you something a bit more, high quality.

I mean, people have their say about that. Some love it. Some don't because it's actually an extra request. Et cetera, et cetera, et cetera. Facebook also played, aggressively with that where they're actually, I think their, their, blurred image was like one or two kilobytes or something. And then they would swap in the proper image that was more of a user experience situation because they wanted to let people know that, Hey, this image here coming up.

You can stick around, but you know, that sort of blurred image gave the user just the information they needed to know. Hey, there's an image, I can wait the extra, like half second for it to load up. Instead of giving you like this blank page.

**Jeremy:** [00:45:19] This has all been specifically with images. Are there any other, common mistakes, either on that particular page or on other websites that you often see?

**Henri:** [00:45:31] I mean, in terms of, additional sort of challenges, like some of the challenges you'll see, it's sort of like, a bigger user experience, issue. So in terms of, prioritizing what needs to load, on the first load. So above the fold, and these are things that you're pretty much going to see, Once the page loads, but at a particular level so that's why the film strips are very important. So you can see sort of like a frame by frame level of what's loading on the page, and then you can make some adjustments. I mean, in terms of, another low hanging fruit, I'd probably say, the next one might be making sure that you keep your requests down.

And again, that partly has to do a bit with some lazy loading, because at that point, you can make sure that, you're not loading, like say, you know, making these 300 requests in one shot when really you can just keep it at like a hundred, 150, I dunno. But you'll know only when you see the page load yourself.

I think that's certainly important. And I'm talking about low hanging fruits here. I don't want to get into the deep, entrails that, that, you know the good people like Andy Davies and Patrick Meenan, get into. but yeah, I mean, these, I think are some of the, immediate decisions that you can make.

Just making sure that, you know, your, your first load is as quick as possible. And that's by keeping some of the requests down and make sure that you're not, you're not stuffing, that first load with like a bunch of, you know, I shouldn't say needless, resources, but some resources are probably, on the fence on whether or not they should be right there. you could sort of, you know, have them load below the fold, and still deliver the information that you, you, planned on, on providing.

**Jeremy:** [00:47:20] In the case of the first load. Would that usually be because when you first load the page there's scripts that are running, or there's images that are loading, that aren't really content, I guess, that aren't really text somebody needs to read and things it's like that. And those are the things that you would load, later, somehow I guess this is what you're saying?

**Henri:** [00:47:43] So, it's a great question because this is the kind of conversation I've had with, with, designers, and which is why I always believe that designers should certainly be, aware of the performance conversation, because you know, they'll sit there and make this, have this page mock up and they're like, boom, boom, boom, boom, boom, boom.

This is going to look amazing. But really and truly, I think part of that push pull is what is the most important here? what. what kind of asset, what information can we have come in below the fold? You know, what, what can come in a little later in a load? because again, all that research, is around  the snap of the finger, making sure that page loads up right away, the user can kind of scan to see what's going on.

And then at that point start to like make the way down the page. You do not want that page to load and have this sort of like blank space. And then that turns into that blank stare. And then, who knows what happens after that? you really want that information to be like, boom, cattle prod.

It's right there. It's like, okay, they're scanning the headline, looking at a couple of photos and then they start to load up the rest. And that little bit of time as seemingly insignificant is sometimes a world to a page and when it comes to loading resources,

**Jeremy:** [00:49:09] So that's almost bringing it to, being a part of the design is can you make a page where. you don't have to load all the sort of surrounding images and surrounding chrome, just to see the content. And even before you talk about performance, it's, it's more of a, when somebody first gets to this page, how do we make sure they see what they need to see?

**Henri:** [00:49:30] Absolutely. Absolutely. And, you know, you bring this up just a week or two or week after, I've I've listened to, or watched, an amazing talk. it was, actually, with regards to cnn.com, during 9/11, you know, and it was phenomenal how, the sort of tech lead, talked about how the stripped the, page bare in order to just keep the details that they needed, because they actually had tried one version of the page, what they felt was, sort of like the essentials.

And then they kept stripping. It kept stripping, it kept stripping it, and eventually it just became one image, a logo and text. Now, granted, you know, that's also because you're under so much sort of, sort of stress from all the traffic, but the idea remains that what do you need to deliver in terms of information?

What is going to load as quickly as possible? That's what we're going to go with. In essence, almost 20 years later, you know, we're still dealing with that because now, even though we don't get that sort of like 9/11 level stress to a site, but you still have the fact that you have devices and varying networks and you know, it'll never translate again from like, that kind of traffic to, you know, a network being that throttled.

But the fact remains that, we can predict that they're going to be on their device. It's going to have various, a network connectivity, varying power as a handheld. And so you try and do the best to manage that element. And the fact that you do have like a team of developers and designers who have sometimes, dueling opinions.

**Jeremy:** [00:51:27] As a user, and maybe this is more common amongst developers, we sometimes like to see the lite pages,  you gave the example of CNN or NPR, where they just give you the content. And, those are often in separate versions from the normal site, but you're sort of saying, can we take some of the lessons that we're applying to those, those lite sites and just apply it to our design in general?

**Henri:** [00:51:53] Absolutely. And, Someone who had heard me talk about the idea that lite sites existed. and I brought up the fact that lite.cnn.io, is upright now. And you can go check it out and it'll have the same information as cnn.com, but CNN.com will have all the media images and videos and, and X, Y, and Z and ads.

Whereas the lite site is (pssh)  text, not a single image. And apparently, this became a bit of a standard after 9/11 and that site is up all the time. And again, I keep mentioning 9/11 because obviously that was like a very unique situation, but the fact remains that in times of hurricanes, any kind of like meteorological, crisis, or anything like that.

Storms, whatever you want. These sites are still going to be very important because that infrastructure is going to be down and you won't be able to access sites as, as readily as, as possible. and, the fact that you have a site with just bare bones info is fantastic.

**Jeremy:** [00:53:00] Another thing I want to talk a little bit about is, Chrome being slow or being a memory hog is kind of this running joke. And I'm wondering in your perspective, is that the fault of Chrome or is it the types of applications and websites that developers are putting on it?

**Henri:** [00:53:20] I mean, it, this is mildly above my pay grade. you know, I keep it a number of windows open as well. there's probably a little bit of both going on. and applications have never been more demanding that's without a doubt. and in turn that's a testimony to the fact that browsers have never been more capable with a bunch of features, you know? I've been a big proponent and fan of, browser engineers because, I should pull this up,  but someone, on Twitter said that the browser is by far. the greatest piece of software out there.

I think there's a strong case for that to be absolutely true. I've gone out and said that, on your phone, through your browser, you could probably please just take care of everything. You need to do banking. you can save money, you can go out and make money. I mentioned that you could find a date, buy clothes for that date, rent the car for the date, order food for the date, all through a browser, and if you had told us that like 10, 15 years ago, people would be like, yeah, whatever.

But in 2020, today, July 19th, it's happening. And, browsers have to make these sort of, accommodations, you know, so, whether or not Chrome is to blame in terms of like being a memory hog, I'll let you know the engineers debate that, but  I think you must tell the story that the browser is basically a bit of like a Swiss army knife right now.

We have made demands, from the browser that have generally been met. And, I think we've benefited from that, 10 fold, and, and again, If you didn't have a laptop or anything like that, the browser on your device would be able to, to save you.

And, you know, we could have had this, this conversation on the browser, on the phone, let alone that, you know, the fact that we actually are having it on a desktop right now, you know, so, you know, kudos to the engineers out there. I'm not slamming you guys.

**Jeremy:** [00:55:31] Yeah, it's, it's pretty, it's pretty incredible just what you can do in the browser and the fact that it has become so extensive that now we have electron right. Where people are making websites basically designed to be desktop applications.

**Henri:** [00:55:47] Yeah. I mean, I don't know if you saw someone, yesterday the day before. I think recreated, either MacOS 8 or some Mac application in electron. It was pretty fascinating, you know, so, but yeah, absolutely.

**Jeremy:** [00:56:02] And what makes a lot of this possible is, is JavaScript, right? And there's a lot of different JavaScript frameworks that people use, like React and Vue and so on. And from your perspective, what are the additional things you should be thinking about from a performance perspective when you're working in, in heavy JavaScript, code bases?

**Henri:** [00:56:25] You know, on demand. That's it, you mean the world without JavaScript although it can, it can exist, you know, it would be challenging. and I think we have to accept that it's definitely here to stay and it's here to, I mean, I shouldn't say here it's here to stay. I don't think it was ever not invited.

I just think that, there was a sort of like this liberal use of JS and, you know, without really under standing how powerful it was and, how caustic it could be a to the experience, the user experience, Thank the Lord for people like Alex Russell, who are out there to remind us of the fact.

But that that's, that's really it. And I think that, as, more and more frameworks come around, the idea is to not really. shun, their availability, because again, you know, people are spending some time to research and create a library, or a framework that they feel that they need.

It's when it's being used and deployed. can we use it as efficiently as possible? That's it at the end of the day, name the resource. Someone's out there, using it liberally. Can you make sure that, in employing this, this resource, you could just, send it down the wire.

Or make use of it  in the most disciplined fashion. And that's what it comes down to in the end. And that is the research that needs to take place. when, using these resources, especially JavaScript, like I said, and like you mentioned, between its availability and everything that it can do for us,

**Jeremy:** [00:58:05] You, you talk about being in dev tools all the time. Are there specific parts of dev tools or, or tools outside of dev tools that you use to try and identify areas where there's performance problems?

**Henri:** [00:58:20] So, Dev tools  I mean, auditing a site can seem a little boring at times because. You are essentially looking for very, specific details, I personally love dev tools because, as scary as it can look at times, and there's still many parts of it that, you know, I tend to forget, or I get lost, in, but, It will provide a lot of the information that you need, on a pages, health, and, and what's taking place, on the page now with respect to tools in particular that I like, again, I'll say it, I love dev tools.

Obviously, it would be impossible to, do a, proper performance audit without having something like web page test handy, webpagetest.org, a product of, the great mind of Patrick Meenan a tool that's been called the, the Cadillac of performance. And, and again, not the prettiest to the naked eye, but, a treasure trove of, of detail and information.

And, Patrick Meenan has done, incredible work in, in making that available. so yeah, webpagetest.org is certainly, something, you need to keep around. I'm going to throw in, lighthouse. And I say that specifically, because, if you take lighthouse version one, two, right through to version six, there's been very considerable amount of, of work and research that has gone into what we are seeing right now in lighthouse, in terms of the information that you provided, the recommendations, and, the links they provide with the recommendations, they'll tell you, it's like, Hey, we see. In these sort of like 10 resources that you might be able to save X amount of, of kilobytes of megabytes, even, if you do this, and that has helped in what I believe, is yeah, a maturation in, understanding performance.

And what you're also seeing right now, through lighthouse is people working, to reach the, mythical score of a hundred. you know, you have people sharing. Their performance scores and all the other audits that, it takes in consideration, sharing them on Twitter, you know, saying that, you know, I have 89 right now.

I'm totally working on the rest. This was not happening like prior to lighthouse. you know, having a, performance conversation was kind of like  speaking to like a wall of bricks, but now, people are just, openly and willingly sharing, you know, their scores, which means that they are looking into ways of improving, their sites performance, whether or not they get into the deep entrails, separate story.

But, Google has been able to create this, platform where, Not all the low hanging fruits, but low to mid will sort of give you a good idea of what it's like to look after performance. So, I would say certainly dev tools, certainly webpage  And, and again, I think lighthouse has been, very important in sort of raising the bar of performance.

**Jeremy:** [01:01:48] Yeah, I think lighthouse is interesting because it almost gamifies it. You get this score, like you said, you can post it in a tweet and say like, Hey, look at, look at the score I got. There's also a target, for people who make frameworks and things like that. Where, if you have a static site generator, you could say, Oh, the default template that you get from my generator, it's going to get you this score in lighthouse. So I think it's, it is very powerful to have that, that target or that goal that everybody can see. Yeah.

**Henri:** [01:02:23] Yup. Absolutely. And, it has been gamified and, I know that term is used, quite often. and I definitely agree. I mean, I don't want to make it sound like it's. Like a game game game. but it is something that people have been able to sort of like, you know, look at and say, okay, this is where I want to be.

You know, like this is the 10 second, hundred meter. That's how I qualify. I've been running 10 fives. We're going to get it down to 10 soon. So, I, I'm seeing these, these conversations come out of, of individuals. I least expected to sort of, talk about, when that kind of adoption, takes place, I think it needs to be sort of, discussed and to an extent, applauded.

**Jeremy:** [01:03:07] I think in, in your work, it seems like you have a pulse on a lot of the different APIs that are available in the browser. Are there any that you think are being under utilized things that people could be using that they aren't?

**Henri:** [01:03:24] The thing about some of these API APIs, quite a few, are likely being underutilized, but what is underutilized ultimately? I think the bigger picture is, can you look at your personal goals with this particular site? are they being met and if they're not, what are the avenues.

To you meeting this goal that you have in mind. and then you'll step back and look at all your options. And, you know, for every particular API that's available there's probably a bit of a downside, some of it might be sort of like complexity of use, you know, cause some are just not used quite often because it requires a bit more work and sometimes people are like, Oh, I don't feel like spending an afternoon having to do this. You know, I get back to the idea around animations, right. it could be the animated GIF. It could be potentially an MP4 it could actually be. animated CSS, but that CSS, the SVG animation is going to take a bit more work and you're like, eh, or are you going to just jump in and just say, Oh, F it, I'm just going to use this GIF for this animation, even though by the naked eye, you could tell that it could have been done in CSS, right?

So the same thing is happening with particular APIs where it's like, eh, using it on a page. It's probably going to take a little bit of work, which means if there's a mistake, it's like, I don't want to go in there and having to do all this, like, and debugging X, Y, and Z. You start to look at some of these other options that might be a little easier.

And then that might even mean that you might rewrite a particular part of the page cause it's like, eh, you've suddenly discovered that, you know, you could kind of strip this out and make it a bit more bare and make it easier overall to sort of manage. so, that's part of the challenge with APIs. In fact, I remember, I think it was Steve Souders who said that user timing API.

So, yeah, it was the user timing, API, a great tool. developer adoption, not so great because it just meant that there was a bit more work taking place. And a lot of developers, they found didn't want to get into that. And so that's why you start to have some of these other tools like speed curve.

That'll sort of like show you what needs to be improved and where you can sort of, make some of these improvements. and hopefully, without the sort of, challenges of having to sort of like refactor, some code, when most developers don't want to.

**Jeremy:** [01:05:58] Right. I think it's sort of a general belief that you only do the things that you need to, and, if you have a simpler way of doing it, where you import some package from NPM, let some JavaScript library, do it for you, then you'll do it until it becomes a problem.

**Henri:** [01:06:15] Yep. Absolutely. And that's where, you know, the whole idea of, I'm sure you remember this sort of a sudden push for a vanilla JavaScript because people were just jumping in and grabbing all these libraries to do some of the simplest, work and people importing in particular library of, you know, like a hundred, 200k library could have been like 30 K of just vanilla JavaScript.

You know, so, as you said people just don't like to do the heavy lifting

**Jeremy:** [01:06:42] Yeah, I mean, I think we can all identify with, if we don't have to do the work, then we don't want to do the work.

**Henri:** [01:06:49] And that's it. I mean, and I never fault developers for that. That's where we're at, you know, trying to make sure that people can sort of do a bit of the work and get some the reward without going heavily into the entrails.

**Jeremy:** [01:07:02] For sure. I think that's a good place to start wrapping up, but are there any other things you, you think I should have asked or anything you thought we should have talked about?

**Henri:** [01:07:13] I mean, not really. It's just, you know, again, this is a, it's just a fun conversation and, hopefully not to the audiences detriment sometimes, you know, my mind starts to run in these different directions the minute, make a one statement and I'm like, Oh, oh, oh. I kind of want to mention this too.

I mean, we did spend a bit of time on the images side, but, it, it is something that I've found fascinating, over the last few years. And, you know, I've followed quite a few, developers and engineers who have, been deep into that research. So anyone who wasn't into images, I certainly do want to apologize.

But, if you are, I hope you enjoyed it and enjoyed that little, the triggering from my, my Bluetooth. That's telling me that, dude, it's kinda like Oh man, what's his name? the comedian he had the wrap it up box.

**Jeremy:** [01:08:03] Oh, really? No, I hadn't heard of that.

**Henri:** [01:08:06] Oh man. why am I forgetting his name? Oh, anyways, whatever.

**Jeremy:** [01:08:10] Yeah, it's trying to play you off the stage.

**Henri:** [01:08:12] Exactly, exactly. It's like the big hook keeps missing my neck. But you know, again, there's so many things around performance that that, can be discussed. You know, I recently listened to a podcast, which featured an engineer from Facebook and they were talking for an hour about, HTTP3 and QUIC and I thought that was fascinating. And, and that's some of the heavy duty lifting that's taking place, But. For very obvious reasons. And it's certainly going to play well into the future, especially, this future that we have right now, that's going to be heavily laden with media, you know, images and certainly video.

For obvious reasons who are working from home now, students are going to be learning from home. So there's going to be a lot of streaming taking place. And that's the, the next hurdle in dealing with media management and dealing with performance.

**Jeremy:** [01:09:02] Yeah, I think my hope as a developer is that these new things, whether they be HTTP3, or they be the new video codecs new formats, I'm hoping that we get APIs or get supporting libraries that makes it almost transparent to us. That makes it so that, I just say, I want to post this video and somebody else, like probably the people who are on that podcast have done the hard work of making sure that goes over the right transport.

Gets encoded in the right video format, split up if it needs to get split up that sort of thing. that's, that's my hope anyways.

**Henri:** [01:09:43] Yeah. I mean, it's certainly everything that we'd like to see, because, as it becomes a seamless and like you said, effortless for us, ideally, that can be sort of, also, transmitted down to, the user. I mean, because ultimately they're the ones, having to, you know, follow along, the online class.

They're the ones who have to do the, live, remote, you know, yoga, you know, workshop or whatever it is. I think there are a lot of discoveries that are going to take place in the next little while, because, the, the fact that our world is going to be, about us consuming a lot more video content.

This was predicted to be happening two to three years from now. Obviously this pandemic, basically, cut that into like a third, we are more than ever dependent on the transmission of video across the net. And I think it's incredible that even our conversation is taking place right now in such a clear and seamless fashion, back to school, is about like a month from now, we're about to see the net just they're going to be pulling carts, you know? And, it's very interesting to see how that's going to take place because you know, we're talking about the pandemic hitting like mid-March and there was still confusion as to how this was going to play off of the rest of the year. Now it's like, we're getting ready for what might be an entire year of remote everything.

let's see what happens.

**Jeremy:** [01:11:16] For sure. This is another big test for the web.

**Henri:** [01:11:21] Yep. Totally. You know, the web is just there, like wiping its forehead, like, Oh my God, like what just happened? And how am I going to make it, make my way through this? So, no man, it's, it's super interesting and I'm sure we're going to, you know, maybe a year from now have another discovery, and some engineering feat that's hopefully going to make things better for everyone involved.

**Jeremy:** [01:11:46] For sure. If people want to see what you're doing next, I know you do a lot of conference talks and things like that. Where should they check you out? 

**Henri:** [01:11:55] I would say exclusively, Twitter, you know, I'm a big fan of the platform, so, Henri Helvetica. So H E N R I and Helvetica, as you know it to be spelled. I'm planning to have this 1.0, 2.0, release of work that I've wanted to do probably in September. So, I've shared this privately with a few people but, a blog is coming.

I'm probably going to do a series of short YouTube videos talking about little things from browsers to a short podcast on performance, but a light conversation again, as we just did, but probably a little shorter. But yeah, Twitter is certainly the place to find me, whether it be, in public or in my DMs as well.

**Jeremy:** [01:12:44] Awesome. I'm looking forward to seeing the YouTube channel and the podcast.

**Henri:** [01:12:49] Absolument and Jeremy, man, I definitely want to thank you for A) Your patience. Because like I said, my AV hurdles, weren't the most fun. So this is a conversation that's long in the making and thanks for having me on the show.

**Jeremy:** [01:13:04] Yeah, thanks for coming on. It's been a real pleasure Henri.

**Henri:** [01:13:07] Merci Merci. And when I get my thing going, I'll be sure to ping you to have you as a guest. Cause I'll tell you about this other little project I have as well.

**Jeremy:** [01:13:17] Nice, I'm looking forward to it. 

**Henri:** [01:13:19] Yeah, man, it's going to be fun.

**Jeremy:** [01:13:20] That's going to do it for this episode. If you're interested in learning more about web performance, we have all the tools and APIs we discussed in this episode, in the show notes. And if you have questions, I'm sure that Henri would love to hear from you. 

The music in this episode was by Crystal Cola. Thanks again for listening and I'll see you next time.

</div>