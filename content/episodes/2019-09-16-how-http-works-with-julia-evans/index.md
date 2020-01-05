+++
title = "How HTTP Works with Julia Evans"

description = "Julia Evans explains all things HTTP, the need for intermediate level educational materials, the importance of fundamentals, writing to an audience, the zine format, and working on education professionally."

[extra]
episode_url = "https://media.transistor.fm/c5d70ee3.mp3"
+++

Julia Evans is best known for her zines and blog posts that break down technical topics in a friendly way.  She has written educational material on everything from Linux system calls to working with managers.

She joins us to talk about what she learned while writing her latest zine: [HTTP: Learn your browser's language](https://wizardzines.com/zines/http/).

### Julia Evans
- [Personal Site](https://jvns.ca/)
- [@b0rk](https://twitter.com/b0rk)

### Zines
- [HTTP: Learn your browser's language](https://wizardzines.com/zines/http/)
- [Wizard Zines](https://wizardzines.com/)

### Other references
- [Mozilla Developer Network](https://developer.mozilla.org/en-US/)
- [netcat](http://netcat.sourceforge.net/)

### Timestamps
- 0:50 - Why write a zine about HTTP?
- 1:21 - What's a header that could break your site?
- 2:50 - What does HTTP look like?
- 5:58 - What headers are most important?
- 8:39 - Response Codes
- 12:26 - Authentication
- 14:57 - Cookies
- 18:37 - Using browser development tools
- 19:46 - Caching and CDNs
- 25:46 - Referrer Header and Hotlinking images
- 27:34 - Resuming file downloads 
- 30:00 - URLs
- 32:11 - Why webpages show different languages
- 34:34 - Same Origin Policy / CORS
- 43:42 - Compression / GZIP
- 45:58 - Intermediate Programming Education
- 49:35 - Picking topics for blogs and zines
- 57:10 - Picking an audience to write to
- 59:54 - Types of educational material (zines, books)
- 64:03 - Why Julia likes the zine format
- 65:53 - Working on education full time

---

## Transcript

[Click here to help me correct the transcript on GitHub!](https://github.com/jeremyjung/softwaresessions/edit/master/content/episodes/2019-09-16-how-http-works-with-julia-evans/index.md)

<div class="transcript">

**Jeremy** Today I'm speaking with Julia Evans. Julia makes fantastic zines that breakdown technical topics in a really friendly way and she also has a lot of great blog posts. It's always like exciting to see new content from Julia. And so I'm really excited to talk to her today about her current work writing a Zine about HTTP. So thanks so much for joining us today.

**Julia** I'm so excited to be on the show. Thanks for having me.

**Jeremy** The first thing I want to ask is what got you excited about writing about HTTP, like I think a lot of people know a little bit about HTTP, but what got you really excited about diving into the you know, the deep end.

**Julia** Like, one time I started learning about HTTP was when I was working on the team that kind of handled like the Content Delivery Network at work and I had to start dealing with like okay, wait, if we don't set these HTTP headers exactly, right the site will go down. This is like kind of scary. Wait. How does HTTP work there's like a lot more to this than I thought, you know, and I'm like starting to deal with some of those like nitty-gritty details. I was like, oh this is really cool. Like there's like a lot to this protocol. It does a lot.

**Jeremy** And so like what are some examples of like a header that you might set and just like if you didn't set it right you said the whole site goes down. 

**Julia** Yeah, well, okay an example where something where the whole site could go down I think the Strict Transport Security is kind of an interesting example of a header. Where like so the Strict Transport Security header forces your site to use HTTPS, which is a good thing in a lot of ways, right? Because like we live in 2019, you can encrypt everything we have Let's Encrypt. You should just make everything HTTPS, but what that means is if you ever kind of like screw up your TLS Cert. It means you can never go back to the HTTP version of the site, right? So if the TLS does break for some reason you have no recourse and browsers will just refuse to use the HTTP version of your site. So it's just like a little bit of a it's something to pay attention to it, you know, like you need to make sure you're ready to commit to https for eternity.

**Jeremy** Which I think we're I think we're getting there right? 

**Julia** No I think so. I did it for my personal site. I was like, oh, okay no HTTPS forever I can do it. Like it's fine. I think I think it's a fine thing to do, but you just have to have to know that that's what you're committing to right 

**Jeremy** Yeah it's so it's like basically you're saying you you're telling the browser. Hey, like when you come talk to me, you have to use HTTPS. But like if my HTTP is broken like my certs are broken, then it's just the site's totally down. 

**Julia** Then the site's totally down. Yeah, exactly. 

**Jeremy** Yeah, so I guess maybe we should back up a little bit when we're talking about the HTTP protocol. I think a lot of people don't really understand what's actually being sent like they I think they understand that you go to a website and you know, it's like making requests and there's stuff coming back. But like what does that actually look like? 

**Julia** Yeah, totally. So let's talk about HTTP request first. So I think a lot of people have heard about like, oh like a get request or post request. So the first thing to know about HTTP request is just that every HTTP request has a method which is usually get or post right when you type a URL in your browser. That's a get request. And requests have they have a method right like get they have headers which is sort of what we were talking about with Strict Transport Security which are just like extra information you're saying to the server which is like, hey, my browser is Firefox, right? And then there's a body sometimes so get requests don't usually have a body but post requests where you're sending like JSON where like you might have done that with an API probably post requests usually have a body where you're actually sending like some data to the server. 

**Jeremy** Right right over over the network like if we take it just a little step lower I guess is the HTTP request. Is that writing over TCP you know does is it just text or is it binary? What does that look like? 

**Julia** So HTTP 1.1 Which is The version that I think most people are most familiar with it's like what we've been using sort of for the last 10 years or something is a plain text protocol over TCP. So literally if you go into your terminal and you type like nc netcat is a tool to open up a TCP connection, maybe type like nc example.com 80 and you just type like get slash HTTP slash 1.1 enter host: example.com and enter enter. It'll send off an HTTP request and then it will send you back an HTTP response. And that's it. Like you can it's like it's like you're literally a protocol that you can like type with your hands which I find so charming and wonderful. I'm like I can just look at this. It's so simple. Wow, and it's the whole web like what could be better, you know, 

**Jeremy** Yeah, and it's literally yeah, it's just text. It's like text separated by line breaks, I guess 

**Julia** Yeah, yeah exactly. 

**Jeremy** So you don't even have to like prettify it or whatever. It's just kind of like oh, this is just these are the headers 

**Julia** yeah technically there it's like a \r\n like there's two line breaks but a lot of the time if you just put a \n it'll be okay, it'll work anyway, even even if that's not like what the spec says but yeah. Yeah, it just line breaks. 

**Jeremy** the things we were talking about earlier is how there's all these different headers and things like that. What are the ones that you think are most important for people to understand? 

**Julia** Yeah, totally so for. Responses, let's say I think one of the more important headers is the content type header and and also for requests actually. Okay, let's talk about HTTP APIs  because I think that usually when you're in a browser and you're making requests, you're not worrying so much about the headers that you're sending right like your browser just does it you're like who cares like, you know? I'm your browser sending all these all these headers on your behalf. But when you're using an HTTP API, you often are controlling the headers that you're sending directly, right? And you might not might be like, okay, what do I need to set? And there's they're actually like generally only two headers you can set when you're using an HTTP API. So there's this header called content type. And so let's say we're making a post request to like the twilio API or the Instagram API or something in that post request. You're going to be sending a body which could be either JSON or it could be something called. It's called like form URL encoded usually you'll use JSON and if you don't set the content type to match the body of your request, like, do you know if like if it's JSON and you don't set like content type application/json the server would be like, I don't know what you're sending me. Oh, like I'm not I can't deal with this. Right? Like it really needs you to like say what the content type is explicitly. So I think that's an important header to know about and this is like very top of mind for me because I was just like integrating with an API the other day like just like some random API and I was like, yeah content type application/json and I tried it without it and it did not work. So yeah, it's like and like you only need to do this if you're because a lot of the time you have like a library that you use right if you're using some API. But sometimes you don't have a library like this this one I was using just like didn't have a library. So I was like, okay great. Let's just we're gonna add some headers manually, you know. 

**Jeremy** So I'm curious when the server says like, oh, no, I don't understand that is that is that nginx or is that like the application server? Like which part is, you know is rejecting you. 

**Julia** It can it can be both. So in that case I would guess that it's the application server. 

Because it's sort of like about the content type of the request. You can also definitely have nginx reject the request for example, like if it was like a time out like you'll see like 503 request like timeout which will which will typically be from like nginx like look. I tried to send your request to the server. It didn't reply. I don't know what happened like like 504 Gateway timeout I give up, right? 

**Jeremy** So that was another thing I kind of wanted to ask like when you look at response codes. What are what are some common response codes that by understanding what they mean like it really helps you debug like when you're talking to an API what's actually wrong? 

**Julia** Yeah, so there's four kinds of response codes. There's the ones that start with two the ones that start with three the ones that starts with four and the ones that start with five, right? So this is pretty simple. They're they're categorized in really nice. Sorry, but the two ones like 200 mean like success. Everything is great. the three ones are all redirects basically, so they're like go to this other website. These are not the droids you're looking for. I don't know right like the four ones are like a client error so basically the four ones are telling you like. It's your fault. So for example, when I was making the request to the API, and I didn't set the content type. It was like, I don't understand what you're talking about. It was like 400 like bad request or something and it was like, I don't know you screwed up like try again 

**Jeremy** This is your fault 

**Julia** Yeah. I think like 403 unauthorized is another example of like you didn't authenticate correctly 404 not found is like look you asked for this URL. It's not there but it's your fault that it's not there right you should have asked for a URL that that was there. 404s are kind of like blaming you and in different ways 

And then the 500s are the server's fault you have like 500 internal server error, which is sort of a generic like something went wrong usually in the application code and on the server and just like. You know, like there was an exception something like that. 

**Jeremy** Yeah, I mean, I think that's really a great way to look at it like basically if it starts with a 4 it's your fault and if it starts with a 5 then it's the server's fault.
 
**Julia** Yeah, and it's not totally true. Like if there's a 404 it very well could be the server's fault 

**Jeremy** Mmm, that's true. 

**Julia** like and the same with like an unauthorized error. Like maybe you screwed up your application code right? Like your your authentication code like but that's kind of the semantics of it. Like that's what it means. 

**Jeremy** Yeah, I mean like yeah, I've kind of come across like you said like, oh the 500 internal server error and then another one I've seen is like 502 like a bad gateway and I'm not sure like what cases you've seen it in but for me like I found this like. If I have nginx in front of an application and nginx can't talk to the application a lot of times I end up getting the bad gateway like so do you know kind of like the deeper meaning behind that like, what is it? What is it supposed to be telling you? 

**Julia** I think it's just what you said. That's my understanding is like nginx couldn't. I meant we could we could we could we could look it up

**Jeremy** we have the internet. 

**Julia**  The official thing says server error response indicates that the server while acting as a Gateway or proxy received an invalid response from the Upstream server. So yeah, I don't know it just like something is wrong with the server right like like nginx is like look something wrong. I think a lot of a lot of these error codes are a little bit general, you know, it's like received an invalid response 

**Jeremy** It's like thanks. You're just telling me I'm wrong, right? 

**Julia** Yeah. Yeah, and I think the reality is like there's a lot of different software doing a lot of different things and we're like returning the same error codes it's and so it's hard to tell like just from an error code like exactly what went wrong. Like I think it could be that there's like a firewall problem, right? 

**Jeremy** Yeah, that would be a firewall problem from say nginx to whatever server is trying to talk to ya.

**Julia** exactly. I don't know if that would be a 502 like it's a little.

**Jeremy** probably be a five something, right.

**Julia** yeah, but yeah, it would be a five something.

**Jeremy** When you think of authentication with APIs, like how does that actually work? Like are you putting things into the headers or like, you know am I putting my username and password in there like what's going on there?

**Julia** Yeah, so usually you use an API key that you'll get from the API like a secret key. Well, I guess there's two kinds right? There's like OAuth, which I don't really want to get into.

Largely because I do not have it swapped into my head how OAuth works honestly and OAuth is also like sort of you're logging in on behalf of someone else right? It's not like you're authenticating to the API yourself, but if it's like if you're just doing like if you're for example using the Twitter API and you just want to post tweets to your account, you can just use an API key you don't need to do like OAuth So yeah, and then there's two places you can put that API key to it depends on the API basically like you have to look at the docs but it can either be in the header.

So there's this authentication authentication authorization header. I you just basically like put the API key in that header. You need to base64 encode it but like every Library will just do that for you. Like you'll just feel like you know, but yeah, it just like the authorization header and then like a base64 encoded version of your own.

Of your API key and then the other way is some apis like I was just using an API that it was actually like just part of the request body. So you just include your the API key in your request body instead of putting it in a header, which is like, you know fine,

**Jeremy** Yeah, how about when people are first logging in, you know, they have to put in a username and password is that also usually put into the header?

**Julia** Yeah, yeah, that's also in like an authorization header. It's just like you take the username and password and concatenate them together the colon and then base64 the whole thing and then you put that into header into the authorization. It's like authorization basic and then the base64 encoded version of like username:password

**Jeremy** Okay, so when people talk about HTTP basic authentication or is it authorization, that's what they're talking about.

**Julia** Yeah, that's what they're talking about. Yeah, it's just in the header and like like you'll see that pop up in your browser sometimes right where it's like log into this website that that's what that is. Your browser is just like putting that into a head.

**Jeremy** Okay, so if you opened up like the browser development tools and you took a look at the header, you could decode the base64 string and just see your username and password.

**Julia** Yeah, exactly. It's not like secured at all. Like it's just like plaintext

**Jeremy** Hmm. Okay. Another thing I kind of wanted to ask about is is cookies. So I know I know we're all accustomed to going to web pages and getting warned like this site uses cookies, but it's like. What is that? What does that actually mean like what's going on there?

**Julia** Right and it's interesting because there's sort of two different kinds of cookies. Right? Like there are like so the most common if it's a use case where cookie is like like the basic thing that they're for is actually like keeping you logged in right? Like it's like you log into like your email and then when you go back to your email and load another page you don't log in every single time.

Like you stay locked in even when like if you reload the page five hours later, and that doesn't just happen. Right like the way that works. Is that the server set's a cookie, which is like some kind of session token for you and then you. Every time you browser goes back to that side. It'll it'll send the cookie back and cookies are really dumb in a way.

Like it's really like the server sends like the set-cookie header which with the cookie and then every time you browse respects that site it just sends it back right? It's like here are the cookies you sent me here the cookies he sent me and it doesn't really like it doesn't know what they are.
Right? It just like name equals value and it just sends sends it all back.

**Jeremy** You're saying the the server keeps sending back the cookie that you sent to it.

**Julia** No, it's the other

**Jeremy** Oh the other way around. Okay, okay.

**Julia** Yeah, yeah, the server sets a cookie once and then your browser will send it back every time I visit the website which is how the server knows who you.

Because like the first time you login it sets like the login cookie, right? And then every time you browser goes back it sends a cookie and it's like in the service like okay that's Julia.

**Jeremy** Yeah, so every time you like click on a different link your browser is sending the cookie to the server again over and over again. There's no like there's no kind of like cache or anything. It's just you always send it.

**Julia** Yeah, yeah, because otherwise, there's no way for the server to know right because it's getting an HTTP request which is like get like slash tweets and if there weren't that cookie header, there would be no way for it to know who you are.

Or that you are already logged in like because there's nothing else in that request that it could use its not quite true because actually like the JavaScript on the page can use like local storage to get information from your browser instead or to get cookies.

But just on like like if you wanted the server to know without the JavaScript having to make like a separate Ajax request. Yeah, you basically have to use cookies.

**Jeremy** Yeah, so I'm sort of curious about that because like when people are building say a single page application or an application that uses JavaScript, you know to talk to APIs there's kind of a lot of talk about like should you use cookies or should you use local storage for the the authorization token? And I'm kind of wondering like what how do you decide like where should you put it?

**Julia** That's a great question. I honestly am not a front-end developer and I'm like pretty reluctant to weigh in. on like frontend best practices. Like like the main thing in this zine on the cookies page. I was like look the main thing you have to know is if you're designing a login system of cookies.

It's real complicated and you need to be careful that your security and like I'm not I do not have space on this page to tell you just like please go read You know like use a framework which already implements some best practices. I don't know

**Jeremy** Good luck.

**Julia** Just like don't design it yourself without like thinking about it or like that Consulting anyone because it's complicated, you know, like security's hard to get right.

**Jeremy** cool, you know all these things that we're talking about whether it's the status codes or the headers and that sort of thing. What's the best way for someone to sort of see what's happening like when they go to websites and actually see the headers going back and forth.
What would you recommend they start with?

**Julia** Okay, so I'm proud of all browsers in the developer tools you have this network tab which is the best thing and so amazing and it just lists every request that happened. So I'm looking at one right now and it says like a status 200 method get domain developer dot mozilla.org/whatever and then it has all of the response headers and all of the request headers and I can just see everything that happened right there in my browser.

And you can see all the cookies. You can just see everything. It's beautiful.

**Jeremy** Yeah, it kind of blew my mind a little bit. When you you go to a web page and you have the network tab open and just like oh my God, there's like 40 requests and it's filled with stuff

**Julia** Yeah, it's true. There's almost like a million requests.

**Jeremy** another thing like I wanted to kind of go into is like when I first started playing with developer tools and things like that.

One of the status codes you'll see a lot is I believe it was a is it a 304. It's it like where something. I guess. It's already cached or like you already have it and I was kind of wondering if we could go into sort of how that works. Like, how does the server know like? Oh, you already got this and I don't need to send it again. again.

**Julia** Right. Yeah, so your browser has a lot of things cached because like for example, let's say you're on like you know twitter.com and there's like all this CSS right like megabytes of CSS, 

**Jeremy** Yeah. 

**Julia** Maybe maybe not but like, you know, a lot of people have a lot of JavaScript and CSS and you don't want to have to redownload it every time you load the page because it takes forever. Right especially if you're on a slow connection, so your browser caches the JavaScript and the CSS and but what that means is that it needs to have a way to ask the server like hey has this been updated right? There's a couple ways to do that. The main the main way is that when a server let's say like Twitter send sends you JavaScript it'll send an e-tag header for that JavaScript and the e-tag is just like an identifier for the JavaScript. 

It's typically like a hash like an md5 sum or something of just like the contents of that file so it'll be like, okay e-tag like. F e a 1 2 3 right and your browser is like okay sweet. This file the e-tag is F e a 1 2 3 and it will save it in its cache and then the next time it request that page, right? Like for example the next time you click on something it'll send send another request to the server and be like hey, I want this. And it'll send a get request with the if none match header, which is basically saying with with the e-tag of the like resources it already has so to be like, okay get like slash whatever.js. If none match F e a 1 2 3, and then if that's the current version of the resource, the server will reply and say. Like 304 not modified, which means it's fine. Just use the version you already have and like the three like we talked about that before it's like a redirect right and it's kind of funny because it's not really a redirect but it's like what the spec says like. Oh, it's like a quote-unquote redirect to the cache. Right? 

**Jeremy** Hmm, it's a redirect but it's not actually returning anything to you, right? 

**Julia** Yeah, yeah, exactly. So but anyway just saying use use what use what you have already. 

And a lot of like so I think most people won't Implement them that themselves like this like 304 not modified thing. Like they won't write code to do that. And what you'll typically do is you'll host like your CSS or JavaScript on like a Content delivery Network like fastly or cloudflare cloudfront or you know, whatever akamai and then they'll take care of that for you. So like they'll set the e-tag to like the hash of the thing and then it'll send a 304 not modified if it hasn't been modified. 

**Jeremy** And is that used just from say the browser to the server or is that also used from like the content delivery Network to like your application server? 

**Julia** That's a good question. I don't know if content delivery networks send like if none match to check if they already have it because I think it's sort of less important like. because CDNs usually don't make as many requests for cache resources because like you'll send like let's say you're sending them some CSS and you're like, okay cache this for, you know, 60 seconds or 2 minutes or however long you want to cache it for but it won't send you another request for two minutes, right? So if it just request the resource again, like two minutes later, it's not that big of a deal,  

**Jeremy** so maybe we can go into that a little bit. So you're saying there's a cache control header. So the if I understand correctly  the user makes a request and let's say they want an image and then this the CDN would make a request to the application server. And would it be the application server returning? What was the header called again? Sorry. 

**Julia** Cache Control. There's so many headers! We can do a taxonomy later.

**Jeremy** and it's like, you know this image I'm giving you you don't need to ask me for it again for another five days or something and then it's actually the CDN that is keeping track of the fact that doesn't need ask again. Is that right? 

**Julia** Yeah, exactly. Yeah or your browser like your browser will also look at the cache control header and be like, okay, I won't ask about this again for another five days.

**Jeremy** Mmm, okay, and okay, so it's like both the browser and the CDN both make use of cache control headers. 

**Julia** Yeah, yeah, which is what another reason to be careful about setting them because if you set your cache control header for too long, then people aren't going to ask you like the browser isn't going to ask you again for the resource. So that might have an old version.

**Jeremy** Okay, so it doesn't even make the request like with the example of the e-tag the browser were asked but in the case of cache control the browser goes like no, I'm good. Like I got the right thing.

**Julia** Yeah, it said it was good for five days. So it's only been three days.

**Jeremy** Yeah, and I believe I believe you. 

**Julia** Yeah, and that's that's another example of how you can sort of like break your website. Right? Like if you expect like these things to be updated but then they're being cached. 

**Jeremy** so if someone like I know sometimes I'll go to a site and I'm like, hey, I'm not seeing the thing. I expect to see and someone will just tell me like, oh just you know, just hold Ctrl shift R and like force it to refresh. So like is that sort of saying ignore the cache control or what does that 

**Julia** Exactly. Yeah, that's saying ignore everything that's been cached and like refetch everything that's telling the browser to do that, but you could that only works for your browser,

**Jeremy** right and everybody else looking at the site is still seeing the old thing.

**Julia** exactly.

**Jeremy** Got it. So another thing I was kind of curious about is I was looking at a some of your Twitter posts about headers that show information like oh this this HTTP request that came from fastly or this came from cloudflare and I'm kind of wondering like what is the reason for having headers that are specific to a CD CDN

**Julia** That's a good question. I think it's helpful for debugging. Like for example, let's say there's something wrong with what the CDN did you can say like because you'll have these headers like X-fastly-request-ID fastly is a CDN and then there's some long ID and then if you have an issue you could say like, oh fastly this is the request ID.

I had a problem with can you look into this? Like if you're like emailing your support team and your customer of fastly

**Jeremy** I see hmm

**Julia** yeah, I would assume that's the reason that they put that in

**Jeremy** so it's like they they put in like an ID that you can use to send to their support team or something like that. If Something is wrong.

**Julia** Yeah, yeah, if you're not like their customers that aren't going to be emailing their support team I don't think it's that useful because it just took some internal ID that they use.

**Jeremy** Right, right. How about the the referer header? Like do pages actually behave differently depending on what's what's put in there? 

**Julia** They can so I think it was it was a popular thing like maybe in the mid-2000s. So what what the what the referer header does is it tells you which like if a site links to your site, it'll tell you like which site sent it. So people that use a lot use this a lot actually for like marketing tracking for example, like they'll be like, okay this person came to my page from you know, this other blog post or from like Twitter so you can sort of like track where are people coming to your site from if you if like you have an e-commerce site, But then another sort of funnier way people used to use it is they just do it this big thing about hot linking right where someone would just include an image in their site right? And then it would like and not host on their own server Maybe because they want to save bandwidth. I think this was the when bandwidth on the internet was more scarce and it's not like I think it's such a big deal. So then people would be like Oh, I'm gonna put like a rude image. If  like it's not the referrer isn't from my site. 

**Jeremy** Yeah. Yeah. I kind of remember that where it's like yeah people would use like free image hosting services or things like that and they would try to embed it in like a forum post or something. 

**Julia** Yeah, and then the free image service would just be like, oh this was hot link. You can't see this image because of that. 

**Jeremy** Okay, cool. Another thing I'd like to ask is are there any like headers that people wouldn't expect or kind of weird that that you found while you're researching this. 

**Julia** Are there weird headers? That's a good question. I was mostly thinking about normal headers. 

**Jeremy** That makes that that's practical. Yeah. 

**Julia** What's a weird header. I think one kind of fun header that I like is the range header, you know the range header?

**Jeremy** I don't. 

**Julia** So have you ever done like wget --continue on a file?

**Jeremy** I haven't but I can kind of guess what it does. 

**Julia** Yeah, and it okay. So sometimes I'll download like large like ISOs right and I think especially like back in the days when the internet was slow, like you'd be down a living like a seven hundred megabyte like, you know CD image and then if you get stuck in the middle, it sucks because like, you know, you need to like wait another like three hours. I used to download ISOs on dial-up anyway, so it took a long time. 

Anyway, the point the point is that um, there's this range header that you can send to a lot of servers servers and it'll say like, okay just start this download like 200 megabytes in so you tell it sort of like which byte to start the download at and then you'll just be like, okay give me everything like from 200 megabytes to the end of the request and so  get. Which is this program that lets you download files um supports this uh with the --continue flag where it'll just like look at the current file size and then request everything that sort of like from that on and then append it start appending it to the end of the file. 

I think it's a cool little feature of HTTP that's actually supported by tons of servers, even though I think it's basically useful for continuing downloads of large files. 

**Jeremy** Yeah, that's that's pretty cool. Because I know like in the in web browsers originally it was where you would want to download a file and let's say you're downloading like a Linux ISO and it didn't finish like it failed halfway through and then it would just be like, oh download failed. You gotta start all over. What I've noticed like, you know, maybe more recently is, you know, you're in Firefox or Chrome or whatever. Sometimes it actually lets you click resume download if it gets disconnected, so I'm kind of thinking maybe that uses the range headers. 

**Julia** That that that's my guess because it seems unlikely that it's just like kept the connection open for some reason like for like an hour like yeah, it's probably using the range header. Yeah. 

**Jeremy** Yeah, that's um, that's pretty cool. That's like. I don't know. That's that's very practical I guess. another thing I kind of want to ask about is the the URL like when you you type in a URL to go to a website, I think like. What I don't quite understand is when I do like posts and slash you know myzines or something like that, you know, I have the domain but then I have like this sort of directory structure. I guess you could call it after that. Is that something that like is that happening at the network level or is that just the server is pulling that part out and just figuring out from there? 

**Julia** Yeah, so when you send an HTTP request. There's everything after sort of after slashed right you have like whatever.com slash like, I don't know each DP whatever like what am I? I'm at developer.mozilla.org/en-US/docs/web/status/502 right and there could be like question mark blah equals blah like everything after the slash just gets sent to the server as a string right and like. So at the network level it has it doesn't care within the path. It could be like they don't have to be slashes right there could be you know, I don't know some other character like like it doesn't care. Um, and then it's the server's job to say like, okay that means you know, and it actually could mean anything to the server right? Because like if it's serving like a file directory, it might be like service over subdirectory. I'm if it's an api it's probably a different route, right? How do I based on like whatever/whatever. Yeah, but it's from from like the network perspective. It's just a string including the query string query parameters and everything. 

**Jeremy** I see so everything before the slash it's um it's exactly the same. 

**Julia** Yeah, yeah everything before it. Well everything before the slash is like the domain and the port and then everything after the slash is just sent in like a long string to the server for it to do whatever it wants with and typically it'll like do the same things right like service will like parse out the query parameters and give it to you in some kind of like dictionary, right?

**Jeremy** the query parameters being like where you have like a question mark and then like a key equals value sort of thing. 

**Julia** Exactly. Yeah. 

**Jeremy** Okay. Another thing I've noticed is sometimes if I'm in say another country and I go to a website, you know, I'll go to a website expecting it to be an English and I'll get back like oh, it's everything is in Spanish. I don't understand like what happened and is is that related to headers at all? 

**Julia** Um, it's sort of related to headers. I would say in a way it's not because. When you like your browser, I can actually look at my developer tools right now, but I'm pretty sure that my browser it is sending an accept language header, which is like hey, accept language en-US right. Which is like I want a website in English and it's not going to send a different header just because I'm in Spain if that makes sense. Like it shouldn't start sending me responses in Spanish, but I think that what servers will typically do is to look at your IP address and then do geolocation and then send you stuff in a different language even if your browser technically sent it the header asking for English. 

Which I don't personally understand like I'm like you're Google you should be able to figure out the accept language header. Like why do you think I want a Spanish site just because I'm in Spain?

Like there must be some reason for it, but I personally do not get it.

**Jeremy** Yeah. Oh that's interesting. So it's like if you really did live in Spain or something then when you install your browser, I guess I guess would you install a specific browser or a specific version for your language? I'm kind of actually curious like what?

**Julia** I feel like it might ask you maybe like what language do you want? I don't know like I mean maybe the reality is that browsers do not set the accept language header while. And a lot of people do have the accept language accept header set to English, even if they're in a different country and so it's more practical to do based on geolocation.

Like I'm sure they did it for a good reason. But anyway, it's not because of the headers this time actually, but if you do set like if you make a request to like twitter.com and said like except language like Spanish like en-ES ES you will get a website in Spanish like you'll get twitter.com in Spanish.

**Jeremy** so I guess that means someone must be sitting the header, right?

**Julia** Yeah, exactly. Someone must be setting it. I'm like confused about at this whole issue.

**Jeremy** Yeah, yeah. Yeah, so I guess there's yeah there's different ways of going about it and we're not sure which one they're using. But okay cool. I guess another thing maybe we should go into is I think a lot of people when they're trying to build a website they run into issues with with CORS where 

**Julia** Yeah..! Yeah...!

**Jeremy** And they're like, why doesn't anything work? And so maybe you could maybe you could go into a little bit about what that is. 

**Julia** Let's talk about that. Okay, so I think often people think of the issue as being with CORS, but I'm gonna do a little bit of like a well actually and be like actually the issue is the same origin policy. So let's talk about the same origin policy for a second. 

So basically the same origin policy is a policy that browsers have which is to protect you like as a browser user. What it does is it says it says okay. Let's say you're on a website that has some JavaScript on it. 

And that website is trying to make a request to another domain. That's not so An Origin is just like some like domain.com like api.clothes.com or something and it includes a subdomain. So like api.clothes.com and clothes.com are not the same 

**Jeremy** Oh they're not 

**Julia** Even though they're, they're not the same origin. Yeah, so it has to be it has to be the same protocol like HTTPS is not the same origin as HTTP. It has to be the same port and has to be exactly the same domain and subdomain like it's really strict If you try to make it if some JavaScript tries to make a request to a different origin, I would like I think the way to think about it is that by default it's not allowed. So it's not like expect that it should be allowed and then there are some cases where it's not allowed. It's actually we're like expect that it should be not allowed and then there are some cases where it's allowed. 

**Jeremy** Okay, and this is just for JavaScript? 

**Julia** Yeah, it's actually any request from the page, but typically people run into this problem with JavaScript because if you're just including an image from another site, right like like we talked about hot linking right? That's one of the cross-origin request thats is allowed. It's just like it if you just include some JavaScript like it like. script src, or you just like like just include some CSS or if you include an image those things are okay. They're on like the small list of allowed things. But if you're making a request with JavaScript like to an API, that's not allowed to another origin. 

**Jeremy** And that's the same origin policy. 

**Julia** That's the same origin policy and then CORS is actually the thing that lets you make cross origin requests. So it's actually the good thing. Like uh yeah CORS CORS is like a set of headers that that make it possible to make cross-origin requests. There's like so like the same origin policy is what's stopping you and CORS is what like a thing that you can do to make it to make it okay. So yeah CORS CORS is not in your way CORS is a good thing. So we can talk about CORS and like how it lets you make requests. So let's say you're trying to make a post request to some API. 

Which is something you might want to do, right? Oh, you want to talk about something different first. Do you want to talk about why the same origin policy exists? 

Is that that useful because it's not obvious that I had to think about it for a while because well like wait, why can't I just make requests because you can make a request to those websites from your server, right?

Like if you're trying to make requests from an API, you can just do it from your server. So why can't you do it from the browser? Right? Like why is the browser so mad about cross-origin requests Right? And why is it like no same typically right be like, why is it so serious? So there's two reasons the browser is so strict about this.

One of them is that the browser will send your cookies on cross-origin requests So for example, like let's say some JavaScript makes a request to another server.

It actually will make the request like if it's making a get request and it will make the request with your login cookies.

**Jeremy** Hmmm the login cookies for your origin or for the site you're making the request

**Julia** For the site you're making the request to 

**Jeremy** Oh Okay.

**Julia** Right, and so you don't just want any JavaScript to be able to make a request with your like as you when you're logged in

**Jeremy** basically impersonate you.

**Julia** Right, you're like use your own login

**Jeremy** Yeah.

**Julia** But yeah, like that's actually not. Okay. And and and I mean you say, okay.

Well then just don't include the login cookies then right, but it's actually a second reason which is you could be on some kind of private Network like a corporate Network like I've had at work in the past which is like, okay, you're on like you have some secret company corporate Network and then if you like, oh, let's just make a request to like go like steal money, dot you know, whatever.

And like it may not need any login cookies to do that. But because it's on like a private Network that it doesn't have access to it's still something that you need to be protected from so it's really because like your like browser is actually like. Sort of it potentially in a privileged location, right?

And so your browser isn't just going to let anyone make any requests like from your computer. So so it's actually important like which is I think good to keep in mind because you could be like uh Why are you like, why are you doing
this 

**Jeremy** So it's like I mean your computer technically, you know, it has access to the cookie and it can talk to this this private site, but the browser is basically stopping another website from accessing that stuff on your private Network, I guess.

**Julia** Exactly. Yeah, but if you want to get around this you can so so which is CORS CORS stands for cross origin request sharing. I believe reads cross-origin resource sharing. So it's that it's that sharing things across. origins Which your browser by default it's not like you do. Okay. So let's talk about a get request I guess.

So, let's say you want to like let's say you have two websites on like your corporate private Network or something and you want them to be able to make requests to each other. So what you can do is on on responses, so. The CORS stuff happens on kind of a Target server that you're trying to make the request to right because obviously I guess like the JavaScript asking for the site can't be like I have access right because it's like it could just lie, right.

So so the server on the other side needs to be like, okay. No, this site has access it's fine. So it when it sends back a response, it can add this header called Access Control allow origin, which is the origin of the site that the JavaScript is on. That's allowed to make the request. So that's kind of it.

**Jeremy** So the sorry the access control allow origin that's coming back from where?

**Julia** It's coming back from the server with the resource that's being

**Jeremy** Okay.

**Julia** So yeah, like like if it's like api.Whatever.com like that's like your API that you want to allow like what a specific site access to you could return like Access Control, Allow origin like my other website.com.

**Jeremy** and is this done for like the whole domain like as your browser asks, like hey, can I access your site from this other origin? And that's for like everything on that site or is it like scope to specific urls?

**Julia** It's scoped to the origin. Yeah, so it's everything on the domain and subdomain. Yeah, so you I don't I don't believe I could be wrong, but I don't believe you can do just one URL.

**Jeremy** I see.

**Julia** Which is why you have to be careful about how you structure your site I guess and is also actually one like example of this, you know, how GitHub pages are at like something.github.io Like it's pretty important. That's a different origin than like github.com right? Because you could imagine that like GitHub allows like some things like like certain kinds of requests from github.com and it's not allowing like other JavaScript that it doesn't control on github.com. Right? Like you're on like myuser.github.io and everyone actually has their own subdomain, so they all have their own origin. So they're all isolated from each other.

**Jeremy** Okay, so if you have a subdomain that's considered a completely separate origin.

**Julia** Yeah, which is why it's good to use subdomains If you're trying to isolate isolate people instead of like like if you're doing like a shared hosting site, you should probably give them subdomains because then it'll be different Origins. 

**Jeremy** Okay, because otherwise, it would be like, you know, you could make a website that basically when somebody goes to your GitHub Pages site, it makes requests to like their actual GitHub account and goes like Oh, I'm just gonna like delete your Repos or something like that

**Julia** yeah, exactly. Exactly. 

**Jeremy** That seems bad. 

**Julia** And then you can kind of see like the rabbit hole of browser security from there right like but. 

**Jeremy** Yeah, that's it. That's interesting it's kind of like the browser is like acting as your guardian, I guess going saying like no you can't do this because this is this is dangerous. Don't do that Julia, right? 

**Julia** Yeah, and it's right. 

**Jeremy** Very cool sort of the next thing. I kind of don't want to go into as more in a general sense about your thoughts on. Education in you know, programming things like that, but I guess before I do that, is there anything on HTTP specifically that you think we should have talked about? 

**Julia** I wonder if it would be fun to talk about compression really quickly. I think I just really love that like did you know that most things that are sent on the internet are compressed. 

**Jeremy** So is that like the like I often hear gzip? Is that what you're talking about? 

**Julia** Yeah, yeah, they're gzipped. So like if you request some JavaScript, it's good. It's almost certainly going to be compressed to save bandwidth and I just think it's really nice like that. Like there you go. Because your browser will send this header which is like accept encoding gzip which is like if you compress it, I get it it's fine. And then the server will just compress it and like even if your application itself like Server doesn't compress it. Usually there's some proxy server in the middle like nginx will just be like, okay, I'll just compress it. 

**Jeremy** Because why wouldn't you right? 

**Julia** Yeah because why wouldn't you right and it's something you can just do on the Fly it's not a big deal. 

**Jeremy** And that's all like transparent to you like because when you open up the network tab in the browser, it's showing you the raw headers and all that stuff, but that's because the browser has already decompressed the gzip. 

**Julia** Yeah, yeah exactly. Well the headers won't be compressed.

**Jeremy** Oh the header. Okay. So the headers are always plain text and it's just the content that gets compressed. Okay, interesting. Yeah. 

**Julia** Yeah, yeah, and then the browser will show you the uncompressed content, even though like usually like very often the content will actually have been compressed 

**Jeremy** Right, right. Oh, that's cool. It's kind of like another thing the browser takes care of 

**Julia** There's so many things the browser is so wonderful. Um Yeah in http2 actually headers are compressed, but that's 

**Jeremy** then it's completely binary then in http2. Hmm. Okay, so no more no more using netcat to talk to servers. 

**Julia** no, it's kind of sad but there's a lot of advantages.

**Jeremy** Yeah, it's always cool when you have something that uses a text-based protocol like for example with like another example I can think of is redis is it's all just in text so, you know, you can telnet to a redis server and kind of play around and see how it works. So I always thought that was pretty cool. 

**Julia** Yeah, I love I love plain text. 

**Jeremy** Cool. 

**Julia** Let's talk about education.

**Jeremy** Okay. Yeah, so I guess you know you've talked about before how you wish there were more intermediate materials for developers out there like, you know you searched online and there's just tons of like, oh, you know how to how to start as a new programmer and like how to do your first thing which is really which is really awesome. 

**Julia** Right, how to get started with python like how to learn JavaScript? 

**Jeremy** and then but like for you know myself and I'm like I want to learn about like, oh how to how to use a CDN or something. Like there's something like a, you know, then it may be another step further. It's I find it a little difficult or like I find it. There's not as many resources out there. So I'm kind of curious like what you would like to see more of or you know, what are your hopes for that space? 

**Julia** Yeah, so I think the way I think about the work I do because I think that's sort of most of what I write about sort of that intermediate space is kind of like what I started learning more about HTTP. I had a couple of great co-workers like I have a coworker named ray who'd worked with CDNs a lot and I would be just like Ray. How is HTTP header formed?

**Julia** what are these headers? Like how how do I and a lot of it is sort of simple stuff, like nothing we talked about in this like episode so far is really bad like complicated right? It's just like things that you don't know because no one told you like about like the range header or whatever like it's not that important, but it's cool to know that and it could be useful and like you just need someone to have told you one time. Um and and so I think like the work I'm trying to do is sort of like to be that like co-worker. There's just like hey you need to know about this like little thing it'll be useful to you. I don't know if that if that makes sense?

**Jeremy** Yeah, I mean like I think that's one of the things that you know, really draws a lot of people and myself included to to your material because it's it sort of gives us a window into these things that like you said you you wouldn't even know that you need to look into or could like really save you a lot of time unless you have like a colleague or a friend who could tell you like. Yeah, I've seen that problem and you know, you can you can fix it with this way by knowing just a little bit more about the thing you're working on. 

**Julia** Yeah. Yeah, I think a lot about it too in terms of sort of fundamentals right? Like because the reason I'm so excited to write about HTTP is that. It's like the protocol that runs the entire web 

**Jeremy** that seems important 

**Julia** like it's and like that's that's all. And it's not really that hard to learn about but if you don't know it, you can really end up sort of stuck right because if you have a problem with caching and you don't know that you have a problem with caching or you don't know that your browser is caching stuff. Like what are you supposed to do? Right? Like I think that there are a few of these fundamental things, especially I think protocols that are also aren't really. taught like in a lot of places, like certainly. I didn't learn about http in school, you know, like I really learned about it on the job.

And so I kind of want to collect some of these like fundamental things and be like look this is it like it's not it's not that much to know you just need to learn it and then you'll be not not set. But like you'll have the foundation because like you're not going to memorize the whole HTTP protocol right? Like like we were talking you were like, what's 502 and I was like wait like yeah. I don't remember but the point is that like if you have that Foundation, then you can go to like mdn the Mozilla developer Network and just look up what you need to know and then. Like that's what like I think being a wizard sort of is right it's the ability just like know where to look look up the answer and get it done. 

**Jeremy** Yeah, and when you're deciding on topics to to write about or dive deeper into is it where you'll be working on something at work and then you'll kind of hit a wall and then you just kind of start doing research or like how do you end up picking, you know the specific topics? 

**Julia** Yeah, so when I blog it will typically be that it'll be like like around this thing at work and then I was curious about it. And then like these are things that I learned when I write zines it's a little bit different because I guess because they're bigger topics. And I usually write down things. I already know about but I try to write about things that I consider really fundamental. So I've learned a lot about like sort of Unix command-line tools, which are like, I like I feel like they're like in my fingers at this point, right? Like it's like really what you need to know.

I've written about like kind of Concepts in Linux like like permissions and like, you know file descriptors and stuff like that. And then http is also something that I kind of consider fundamental and I kind of want to like I think next I might write about databases like relational databases. So I think that's really fundamental and it's something that I think a lot of people don't like there's some things about transactions for example that I think are not well understood by many people, you know, including me honestly, like I'm going to need to learn a few things to write about databases and like indexes right. It's like if I think there's just like a lot a few things to know about databases that are truly not obvious.

**Jeremy** I think like you know with a lot of these things whether it's you know, HTTP or it's the Unix calls of it's databases. I think a lot of people they kind of they stay at more of the higher level, you know level of knowledge. Like if you're working with a database, you know, maybe you're working through an orm and you're like, why is my thing slow and it's you know, like you said, Understanding more about indexes or understanding more about like, oh, I have all these transactions and they're all locking the database and nothing can get done like going just a little bit deeper, you know, it can it can help so much. 

**Julia** Yeah, and I think like if you want to be a great developer, I feel like you do need to understand some of these concepts like for example, if your front end developer, I think like I'm not a front-end developer, but my impression is that a lot of these things about HTTP we're talking about are kind of fundamental to front end development right? Because like your site performance is very important, which means that caching is important right or like security is important, which means that you need to kind of understand the basic security of the model like model of the browser. I think just in order to like communicate well with your security team, right? About like why you're doing certain things and you do it like you need to know like you can't just set access control allow origin * like why that's not okay.

Like I think they're just like some fundamental things that you need to know to be able to like work productively with like experts who maybe are experts in browser security at your company, even if you aren't yourself that person I think having having a foundation is a big deal

**Jeremy** Yeah, so I guess from it from your perspective like the foundation's you're thinking of would be protocols. You said the Linux system calls databases. Are there anything else that you think like, you know people could you know, they could invest like a little bit more time and they could really get a big benefit out of it? 

**Julia** That's a great question. Let me think about it. I'm still I I I only I work on things. One thing I've been writing about recently is debugging which I think is a different kind of foundational skill, right, which is not like a technical skill in another way and in the same way, I think like I mean I have this other zine which is about like how to work with your manager, which I personally also think is a foundational skill, like as someone who has a job. 

**Jeremy** Something we sometimes forget, right? 

**Julia** Yeah. Yeah, but I'm definitely still working on the list. I think it's obvious. I don't know what you think are like other foundational 

**Jeremy** Yeah, I mean mmm. It's kind of hard to say it also sort of depends on what type of projects you work on I think. 

**Julia** Yeah. 

**Jeremy** Like one thing I never really thought about too much and kind of actually some of your articles kind of made me look a little bit closer is yeah just the system call concept of you know, hey were writing we're writing code in a high-level language. But actually this is like doing all these operating system-level calls and if we understand like Hey, what calls is it making and how often is it doing? How much time is it taking? You know that really helps with trying to figure out why something is slow, right? But if you are like let's say a front end developer and you're just working sort of in the JavaScript ecosystem, you know HTML CSS. Maybe that part isn't so important, you know, so. 

**Julia** yeah, yeah, and then like you might almost be a little more algorithm focus in a way because I feel like like because like front-end performance is so important like I feel like or just like I guess the browser model in general right because there's so much more to like what a browser is doing.

**Jeremy** Yeah, yeah.

**Julia** Security and I feel like a good understanding of the browser environment is really key. 

**Jeremy** Yeah, I guess like I would be sort of curious like because I'm not too deep into front-end either but I'm wondering if in your impression if you do a lot of work in the browser, you know is is it important to understand a little bit about how the browser itself works or about how the JavaScript runtime works or is that like maybe too deep like just kind of curious? 

**Julia** I would guess that it's more about sort of the interface that the browser exposes to you and less about what it's doing internally. So sort of just like because because browsers have all these capabilities and they're always getting new ones. Right? Like there's like the music API and the like local storage like we talked about right?

I think just being like aware of what all those different interfaces are and like what they let you do seems important. I think of things a lot in terms of interfaces right like HTTP is an interface. The browser has all these interfaces. 

**Jeremy** Yeah, so that's that's kind of a that's kind of an interesting perspective where it's um you are you are going like one level deeper, but it's about sort of the API is available to the browser. Yeah. 

**Julia** yeah and just like how you can expect them to behave.

**Jeremy** Right. Yeah. Yeah, that makes a lot of sense. Yeah, I think like yeah definitely like the blog post and the zines are doing I think are helping people to just get a better awareness of like of the sort of foundational Concepts. And I mean, I know myself like I went I studied computer science, but a lot of what I learned in school. Is is not like these things even though I think they're they're super important. But umm

**Julia** I didn't learn any of this in school, even though I also studied computer science, but like I. 

**Jeremy** Yeah, it's yeah, we just like, you know, we learn about data structures and algorithms and things like that, but it's like I didn't learn about system calls or I didn't learn about how databases work all this stuff. So. Yeah, you know I didn't I when I was in school, I was the one who would like you would have a folder and then I would make a copy of the folder and say like oh this is version 2 right? It's like and then I started working and I was like, oh why like why didn't they teach us anything? 

**Julia** Yeah, I think one of my friends tipped me off at school and was like you need to be learning this. 

**Jeremy** yeah, that that could be a whole other discussion sort of the Gap. Yeah, but so. One of the things um I also kind of wanted to ask you about is one of the things I find really interesting about your posts is I feel like you really you really know your audience in terms of what to explain and what not to explain because I. You know looked up tutorials on things and you know, I'm trying to get a basic concept of like oh, how do I for example, let's say I'm in Python and how do I interact with C code from python or something like that? And you know, I'm looking up tutorials and I make it a tutorial that kind of goes into like explaining like you didn't know anything like yeah, and 

**Julia** Right. I get so frustrated. 

**Jeremy** like, you know, I just want to know the thing I came here, but you know, I have to get through three pages of like oh, this is how a var this is what a variable is and like so I'm kind of curious like how do you make decisions like that on on what to focus on and what not to. 

**Julia** Yeah, so my Approach is always to sort of focus on my past self and like, okay, what did I not know like a year ago or two years ago or five years ago about this that I wish someone would have told me and that's not what a variable is, right? Because I knew fiveyears ago what a variable is. And I think it sort of like a keeping that focus and not because um and that often like sometimes it doesn't exactly work because I won't explain something because I'm like, well, I knew that and someone will be like well, I don't know that and then I'll be like, okay, I'll add that too. But I sort of I think try to start with sort of a minimal approach. I've just like well what didn't I know and what do I wish I would have known and I think that resonates with a lot of people. Because I think often people aim it aim their stuff at an audience of nobody like, you know, like they don't have any real person in their mind who would benefit from this and so starting with someone who could be like literally yourself. I think it's better than like, oh, I don't know. Maybe someone would want to explain this way. I don't who right? 

**Jeremy** Yeah. Cuz I think I think you know, some people really get caught up on that where they're not sure like, oh, you know, I want to I want to reach as many people as possible. So I should explain absolutely everything but then I kind of wonder if you know in some cases when you do that the people who could really use the information that you know, you've got buried in your post. They won't find it because they'll kind of get hung up on the things that they don't care about so much. 

**Julia** Yeah, exactly and maybe the people who are starting at a more basic level can't really deal with the more advanced information because like you haven't you probably haven't explained literally everything.

**Jeremy** because if you answered every absolutely everyone who says like I don't understand this thing and you added it to the post then you know, eventually you would have a 300-page book, right? 

**Julia** Yeah, yeah exactly. 

**Jeremy** Another thing I find interesting about, you know, you're posting your zines is that you know, they're they're relatively, you know, they're relatively small so that it's kind of easy to to read it in one sitting and go like, okay, like I learned a thing and you know, I can kind of keep this in my head. So I'm kind of curious like from your perspective, you know, do you see this kind of you know short form writing being more common like because you know in the past there were you you would have a reference text, you know, you would have your two hundred three hundred page book and go like, oh go read this and then you can start learning python or then you can start writing python or something, but I think that's like getting harder and harder for people to do right? 

**Julia** Yeah, and I think the reason I started doing it that way is partly that at that's realistically not the way that I work. Like books are great. I know and I know some people do learn a lot from. I mean I did I learned to program from a book way back, but then I didn't I don't think I read any programming books after that. You know, like I just read the one book and then that was it. I'm sure I've read other books, but I can't think of one off the top of my head except the managers path by Camille Fournier, which is amazing and also relatively short. Okay, but yeah, I think the reality of how I work most of the time is I want to get like some sort of like basic ideas. I'd like how to think about something and then afterwards like once I have a framework for how to think about it, then I'll just go look up information as I need it and I feel like that's how many people work these days. You know, like you want to know like maybe like how okay like what's the basics of like what our HTTP headers and what are the methods like how does this work? I'm like, what's up with browser security? Oh my God, and then like. And then once you have all of that you can just be like, okay. I want to know what the 304 HTTP Response Code means again. I'll just look that up. Right and you don't like you're not going to look up up in a book also because it's 2019 right here. Like I don't know. I don't think it's. Useful though I do think that actually reference books are amazing in a way because I don't want to I don't want to slam reference books because I have this reference book called The Linux programming interface that explains like every like we're talking about sort of interfaces in the browser interface. This is like the Linux interface and it's like everything that Linux can do for you and it's like 800 pages and is incredible and like whenever I want to know something I do actually look it up in that book. But again, it's like so I think reference books can be incredibly valuable and I'm really happy that. The author of that book took the time to write it because it's incredible and it's like a gift like to 

**Jeremy** Yeah, but maybe like maybe it's better not to start straight from the reference text. 

**Julia** Yeah, because I've only read like 15, 10% of that book and every time I go to it, it's perfect and it's exactly what I need. But like, you know, I'm probably not going to read it all the way through. 

**Jeremy** it's kind of like I feel sort of the same way about docs as well where a lot of times like all the information is there but if you're just trying to get started you're kind of like I don't know what to look at first, right? This is like the docs becomes a lot more useful once you have sort of a basic context of what you're trying to do and sort of what the high-level pieces are. And then that's when you can kind of dive in and get exactly the piece of information you're looking for. 

**Julia** Yeah, and I think people just really learning a lot of different ways like because you need to sort of do some things interactively, right? You need to play around which is I think where like tutorials can be really great where the like let's walk you through like exactly what to type on your computer and then you need to kind of like get a framework for how to think about the thing and then you like the reference docs and like it's not like this one right way. I think people need need like a whole like web of different kinds of materials. I'm currently excited about interactive things and I have like a project. I'm working on I'm so excited!

**Jeremy** What would you like to see more from other people, you know, would it be like short posts or zines or video courses like kind of what resonates with you?

**Julia** I think I really love the zine format. I would like to see more of that because I just think it's like a great like size to explain something like really important like you kind of explain not the whole thing but you can explain like enough of it, but people kind of get an idea and it's also more. Okay, so I. What I love about the zine is that it's a physical thing actually, you know, like you like you can like print it out and like give it to someone and then they'll like read it on the bus. I'm like people will actually read physical things.

**Jeremy** Yeah, it's like a novelty now, right? 

**Julia** Yeah, it is like a novelty and I think it just a really lovely thing and so maybe what I would like to see more of is physical things that are real and that you can go read on the subway in your hands 

**Jeremy** Yeah, and I think like I can imagine like you're saying yes, someone reading a zine on the Subway or something, but it's a little harder to picture, you know you with the Linux programming interface book on the Subway?

**Julia** yeah. Yeah, exactly and you can almost like trick someone into learning things. This is kind of how I think about it. Like even though it's not it's not supposed to be a trick but like sometimes I'll just be like here look at this and they'll be like, oh like I was you know out and then I was bored and then I picked this up then I learned something cool, you know and like. It's like it's like a nice thing to like thrust on people. 

**Jeremy** Yeah, and it's kind of like, you know, you have like the really cool covers and stuff and they just like the little pictures and stuff when you open it up and you're like, oh, you know, this is kind of fun and you're like you get to the end you're like, oh I learned about I learned about HTTP or I learned about how the internet works.

**Julia** Yeah 

**Jeremy** That's pretty cool. I think like maybe the last thing I'd like to ask is you know, you started out writing ziens as kind of a hobby. But but recently you sort of transitioned into do, you know it being more of a business and I was kind of wondering like how has writing them. I guess you could call it professionally been working out for you. Yeah. 

**Julia** It's been amazing. I yeah, it's been really astonishing. I think I was really. Like it was sort of a difficult transition to make because I think it's hard to like sometimes like value your own work and feel like it's okay to charge for this 

But I think it's really helped me spend more time on them because I'm like, okay, this is like like I think I feel more of a responsibility if it makes sense now that I'm trying to do things like this does need to be like really good. And I think like my this HTTP zine is 28 pages, which is the longest they'll ever be definitely 28 is maximum. I think I think it helps me like if it makes it easier to pay people to like like pay illustrators or whatever and yeah, it's amazing. I make a living from it, which is outstanding and like very surprising. And that I'm very happy about or like very grateful for what else? 

**Jeremy** I mean, I guess is there anything you didn't expect when you know, you tried you made this decision. 

**Julia** I think I didn't expect it to be so successful if that makes sense. Like I think I'd sold some things before and I'd make like a like a few thousand dollars like and I was like, okay, I'll start selling that but it won't like be that big of a deal or it won't be that successful and it's been like way more successful like as a business than I thought it would have. And I was like, oh like because I think I have this I've had this idea sometimes because like like working as a software developer that like writing software is the most important thing and it's the only thing that sort of valuable and that sort of doing education work isn't valuable if that makes sense, even though I love doing education work and I personally think it's valuable and like like other people don't value it and I can't really make money doing it. And what I learned is that that's not true.

You know like it is super valuable. You can definitely make money doing it. I like definitely make more doing this right now than I did in my first job. 

I think it really made me see like in a very clear way that it's like valuable work and like why I don't know. It's like why would teaching people something be less valuable than doing the thing? 

It's a strong bias in our culture probably.

**Jeremy** Yeah, I mean it's basically like someone makes educational material and other people learn from it. It's like kind of like you're teaching all of them and they're all getting better at the same time. And you know, you just have to make that one thing right and you can touch like know a million people or whatever which I think is like, that's really awesome. Yeah. 

**Julia** Like it kind of scales in the same way that software does.

Because you just write it once and then all these people learn from it in the same way that you like write software once and then it does the thing like a bajillion times

**Jeremy**  yeah, and I think like a lot of people they kind of under I don't know if they underestimate but they sort of they don't always realize how much time they save when they either talk to an expert or they get access to, you know, a resource like a Zine or a blog post or whatever, you know, sometimes you could be struggling with something for a week or whatever and because you read you know, like just one Zine or just one blog post. It's like all that is, you know, you're done and like a couple hours so. 

**Julia** Yeah, I remember like once at work. I had this issue and I was literally Never Gonna figure it out except that I happen to have read a blog post the week before that described that exact issue and I was like thank God. I read that blog post because I was literally Never Gonna figure it out. Like it was impossible. It was like a weird TCP thing. 

**Jeremy** Yeah. That's really cool. So like given, you know the importance of education and how much you enjoy it. Have you have you thought about dedicating more time towards that versus just as a software engineer. 

**Julia** Yeah, that's right now that's the only thing I'm doing actually I yeah, I don't have a job right now as of like 

**Jeremy** it sounds weird to say but that actually sounds really exciting. 

**Julia** No, it's very exciting it's fun! I think I think I'm going to try to spend a year on it. I still need to write it up. Like I want to talk about it a little more on my blog. But yeah, I've of a bunch of projects. I'm excited about and I was because I was like well, like look, I'm so excited about education. 

What if I just like spend spent a little more time on it for a while to see how I feel about it? And I think that like when you make like a transition like that, it can feel like a huge commitment. Right? But it's like literally not you know, it's okay. Let's just try this for a year and see you see how it goes and like what I make and yeah. So far, I've finished one Zine like I think I finish this HTTP zine today. So I guess by the time this podcast goes goes out. It'll be out. 

**Jeremy** Congratulations! That's that's really cool. Yeah, I'm really excited to see what you come up with because myself and sort of the community as a whole I think really enjoys the material you put out and it's really super accessible and like you said it kind of brings into picture like, okay, what are the fundamentals that I should know that I may not know I should know and so I'm really excited to see that more that come from you and you even mentioned like getting into more interactive stuff, which I think. That sounds really cool. 

**Julia** Thank you. Yeah, and I'm very excited. It's nice to have the time. 

**Jeremy** So is there anything else that you think I should have asked or that you're sort of excited to talk about? 

**Julia** No, we talked about very many things that I'm excited about. 

**Jeremy** All right, Julia. Well, I think that's going to do it for us. So thank you so much for coming on the show. 

**Julia** Thanks for having me.

</div>