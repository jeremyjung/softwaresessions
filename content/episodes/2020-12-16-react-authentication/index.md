+++
title = "React Authentication with Ryan Chenkie"

description = "Ryan discusses the tradeoffs of sessions vs JSON web tokens, common mistakes to avoid, and his experience creating video courses."

[extra]
episode_url = "https://pinecast.com/listen/b025511f-6599-40ae-9a7a-51ab1fcc5a92.mp3"
social_title = "React Authentication"
social_banner = "034-ryan-chenkie.png"
social_description = "Sessions vs JSON web tokens, mistakes to avoid, and creating video courses"
+++

[Ryan](https://twitter.com/ryanchenkie) is the author of [Advanced React Security Patterns](https://reactsecurity.io/) and [Securing Angular Applications](https://ryanchenkie.com/securing-angular-applications/). He picked up his authentication expertise working at [Auth0](https://auth0.com/). Currently, he's a GraphQL developer advocate at [Prisma](https://www.prisma.io/).

Related Links:
- [@ryanchenkie](https://twitter.com/ryanchenkie)
- [React Security](https://reactsecurity.io/)
- [Stop using JWTs for Sessions](http://cryto.net/~joepie91/blog/2016/06/13/stop-using-jwt-for-sessions/)
- [What are cookies and sessions?](https://stackoverflow.com/questions/11142882/what-are-cookies-and-sessions-and-how-do-they-relate-to-each-other)
- [Learn how HTTP Cookies work](https://flaviocopes.com/cookies/)
- [JSON Web Token Introduction](https://jwt.io/introduction/)
- [Refresh Tokens: When to Use Them and How They Interact with JWTs](https://auth0.com/blog/refresh-tokens-what-are-they-and-when-to-use-them/)
- [Critical Vulnerabilities in JSON Web Token Libraries](https://auth0.com/blog/critical-vulnerabilities-in-json-web-token-libraries/)
- [RS256 vs HS256: What's the difference?](https://stackoverflow.com/questions/39239051/rs256-vs-hs256-whats-the-difference)


Music by [Crystal Cola](https://crystalcola.bandcamp.com/).

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy:** [00:00:00] Today, I'm talking to Ryan Chenkie. He used to work for Auth0 and he has a new course out called advanced react security patterns.

I think authentication is something that often doesn't get included in tutorials, or if it's in there, there's a disclaimer that says, this isn't how you do it in production. So I thought it would be good to have Ryan on and maybe walk us through what are the different options for authentication and, how do we do it right?

Thanks for joining me today, Ryan.  

**Ryan:** [00:00:30] Yeah, glad to be here. Thanks for inviting me.

**Jeremy:** [00:00:33] When I first started doing development, my experience was with server rendered applications. like building an app with rails or something like that.

**Ryan:** [00:00:42] Yep.

**Jeremy:** [00:00:42] And the type of authentication I was familiar with there  was based on tokens and cookies and sessions. And I wonder if for people who aren't familiar, if you could just walk us through at sort of a basic level, how that approach works.

**Ryan:** [00:01:01] Sure. Yeah. so for those who have used the internet for, for a long time, the web, I should say for a long time, And who might be familiar with like the typical round trip application, which, which many of these still exist. A round trip application is one where every move you make through the application or the website is a trip to the server that's responsible for rendering the HTML for a page for you to see and on the server things are done. Data is looked up and HTML is constructed which is then sent back to the clients to display on the page. 

That approach is in contrast to what we see quite often these days, which is like the single page application experience, where if we're writing a react or an angular or Vue application it's not always the case that we're doing full single page, but in a lot of cases, we're doing full single page applications where all of the JavaScript and HTML and CSS needed for the thing gets downloaded initially, or maybe in chunks as movements are made.

But let's say initially is downloaded and then interacting with data from the server is happening via XHR requests that that go to the server and you get some data back. So it's different than the typical round trip approach, In the roundtrip approach. And what's historically done, what is still very common to do and it's still a very legit way to do auth is you'll have your user login. So username and password go into the box. They hit submit. And if everything checks out, you'll have a cookie be sent back to the browser, which lines up via some kind of ID with a session that gets created on the server.

And a session is an in memory kind of piece of data. It could be in memory on the server. It can be, in some kind of like store, like a Redis store, for example, some kind of key value store, could be any of those things. And the session just points to a user record, or it holds some user data or something.

And it's purpose is that when subsequent requests go to the server, maybe for new data or for a new page or whatever, that cookie that was sent back when the user initially logged in is automatically going to go to the server. That's just by virtue of how browsers work cookies go to the place from which they came automatically.

That is how the browser behaves. The cookie will end up at the server. It will try to line itself up with a session that exists on the server. And if that is there then the user can be considered authenticated and they can get to the page they're looking for or get the data, the data that they're looking for.

That's the typical setup and it's still very common to do. It's a very valid approach. Even with single page applications. That's still a super valid approach and some people recommend that that's what you do, but there are other approaches too these days.

There are other ways to accomplish this kind of authentication thing that we need to do, which I suspect maybe you want to get into next, but you tell me if we want to, if we want to go there.

**Jeremy:** [00:04:03] You've mentioned how a lot of sites still use this cookie approach, this session approach, and yet I've noticed when you try to look up tutorials for working on react applications or for SPAs and things like that. I've actually found it uncommon, at least, it seems like usually people are talking about JSON web tokens that are not the cookie and session approach.

I wonder, if you had some thoughts on, on why that was.

**Ryan:** [00:04:37] Yeah, it's an interesting question. And I've thought a lot about this. I think what it comes down to is that especially for front end developers who might not be super interested in the backends, or maybe they're not concerned with it. Maybe they're not working on it, but they need to get some interaction with a backend going.

It's a little bit of a showstopper, perhaps, maybe not a showstopper. It's a hindrance. There are road blocks put in place if you start to introduce the concept of cookies and sessions because it then necessitates that they delve a little bit deep into the server. I think for front end developers who want to make UIs and want to make things look nice on the clients but they need some kind of way to do authentication.

If you go with the JSON web token path, it can be a lot easier to get done what you need to get done. If you use JSON web tokens maybe you're using some third party API or something. And they've got a way for you to get a token, to get access to the resources there.

It becomes really simple for you to retrieve that token based on some kind of authentication flow, and then send it back to that API on requests that you make from your application and all that's really needed there is for you to modify the way that requests go out. Maybe you're using fetch or axios or whatever you just need to modify those requests such that you've got a specific header going out in those requests. So it's not that bad of a time, but if you're dealing with cookies and sessions, then you've got to get into session management on the server. You've got to really get into the server concepts in some way if you're doing cookies and sessions.

I think it's just more attractive to use something like JSON web tokens, even though when I think when you get into, like, if you look at companies that have apps in production and, and like, especially like with organizations that have lots of applications, maybe internally, for example. And they're probably doing single sign-on. Maybe they've got tons of React applications, but if they're doing single sign-on, especially there's going to be some kind of cookie and session story going on there. So yeah, I think all that to say ease of use is probably a good reason why in tutorials, you don't see cookies and sessions, all that often. 

**Jeremy:** [00:06:51] It's interesting that you bring up ease of use because, when you look at tutorials, a lot of times, it just makes this assumption that you're going to get this JSON web token. You're going to send it to the API to be authenticated. But there's a lot of other pieces missing.

I feel like to to make an actual application that's secure and going through your course for example, there's the concept of things like, the fact that with a JWT, a JSON web token, you can't, invalidate a token. Like you can't force this token to no longer be used because it got stolen or something like that.

Or, there's strategies that you discuss. Like you have this concept of a refresh token alongside the JSON web token and going through the course and, and I'm looking at this and I'm going like, wow, this, this actually seems like pretty complicated. This seems like I have to worry about more things than, just holding onto a cookie.

**Ryan:** [00:07:50] Totally. Yup. Yeah, I think that's, that's exactly right. I think that's one of the selling features of JSON web tokens is especially if you're coming from maybe like maybe if you're newer to the concept, let's say one of the compelling reasons to use them is that they're pretty easy to get started with for, for all the reasons that I went into just a second ago.

But once you get to the point where you've got to tighten up security for your application, you need to make sure that users aren't going to have these long lived tokens and be able to access your APIs indefinitely. And you want to put other guards in place. It requires that you do a bit of gymnastics to create all these things to protect yourself, that cookies and sessions can just do for you if you use this battle-tested well trotted method of authentication and authorization and that's one of the big arguments against JSON web tokens.

There's this really commonly cited article, which if I'm doing training, I'll drop, in any session that I'm doing, I can probably get you the link, but it's joepie.

I think I'm going to Google that joepie, JWT. That's what I always Google when I need to find this. The title is Stop using JWTs for Sessions. So this guy. Sven Sven Slootweg, I think is his name. He, he's got a great article, a great series of articles actually about why it is not a great idea to use JSON web tokens.

And I think there's a lot of validity to what he's saying. It essentially boils down to this-- that by the time you get to the point where you've got a very secure system with JSON web tokens. you will have reinvented the wheel with cookies and sessions and without a whole lot of benefit. I think he's making the case for this in situations where let's say you've got like a single page react application and you've got an API that is controlled by you that is your own first party API. That's just responsible for surfacing data for your application in those situations. You might think you need JSON web tokens, but you would be able to do a lot with cookies and sessions just fine in those situations. Where JSON web tokens have value I think is when you have different services, in different spots, on different domains that you can't send your cookies to because they're on different domains.

Then JSON web tokens can make sense. At that point, you're also introducing the fact that you need to share your secrets for your tokens amongst those different services. Other third-party perhaps services or domains that you don't control would need to know something about your tokens. I don't know if I've ever seen that actually in practice where you're sharing your secret, but in any case you would need to, to be able to validate your tokens at those APIs.

And so that becomes a case for why JWTs makes sense because cross domain requests, you won't be able to use cookies for that. So there's trade-offs but ultimately if you've got an application front end app and your own API, I think cookies and sessions make a lot of sense.

**Jeremy:** [00:10:50] I think that for myself and probably for a lot of people, there is no clear I guess you could say decision tree or how do you choose which of the two to use? And I wonder if you had some thoughts on, on how you make that decision.

**Ryan:** [00:11:05] Yeah. Yeah. It's interesting. It's certainly a whole plethora of trade offs that you would need to calculate in some way. It's one of the things that I see people frustrated with the most, I think, especially when you see articles like this, where they say stop using JWTs. The most common refrain that I've seen in response to these articles is that it is never explained *what* we should do then.

Like there's always these articles that tell you not to do something but they never offer any guidance about what you should do. And this article that I pointed out by Sven he says that you should just use cookies and sessions. So he does offer something else you can use.

But I think what it comes down to is you need to, I think first ask yourself, what's my architecture look like. Do I have one or two or a couple or whatever, front end applications backed by an API? Do I have mobile applications in the mix? Maybe communicating with that same API and where's my API hosted is it under the same domain or different domain? Another thing is like, do I want to use a third party provider? If you're rolling your own authentication, then sure. Cookies and sessions would be sensible, but if you're going to go with something like, Auth0 or Okta or another one of these identity providers that lets you plug in authentication to your application, they almost all rely on OAuth, which means you are going to get a JSON web token or a different kind of access token.

It doesn't necessarily need to be a JSON web token, but you're going to get some kind of token and instead of a cookie and session, because they are providing you an authentication artifact that is generated at their domain. So they can't share a domain with you, meaning they can't do cookies and sessions with you.

So the decisions then come down to like, whether you want to use third party services, whether you want to have support multiple domains to, to access data from you know, it would be things like, are you comfortable with, your sessions potentially being ephemeral? Meaning like, if you're going to go with cookies and sessions and you are deployed to something that might wipe out your sessions on like a redeploy or something, I would never recommend that you do that.

I would always recommend that you use like a redis key value store or something similar to keep your sessions. You would never want to have in-memory sessions on your server because these days with cloud deployments, if you redeploy your site, all your sessions will be wiped.

Your users will need to log in again, but it comes down to how comfortable are you with, with that fact, and then on the flip side, it's like, how comfortable are you with having to do some gymnastics with, with your JSON web tokens, to invalidate them potentially. 

One thing that comes up a lot when I'm with the applications I've seen that are using JSON web tokens is somebody leaves the company. Or somebody storms out in the middle of the day cause they're upset about something and they've been fired or whatever, but they have a JSON web token that is still valid. The expiry hasn't expired yet. So theoretically, they could go home or something. If they have access to the same thing on their home computer, or maybe they're using a laptop of their own. Anyway, if they still had access to that token, they could still do some damage if they're pissed off right. Something like that. And, unless you put those measures in place ahead of time, you can't invalidate that token.

You could change up the secret key that validates that token on your server, but now all your users are logged out, everyone has to log back in. So yeah, man, it just comes down to like a giant set of trade-offs and the tricky part about it... I think a lot of the reason that people get frustrated is just that all of these little details are hard to know ahead of time.

And that's one of the reasons that I wanted to put this course together is to help enlighten people as to the minutia here. Cause it's a lot of minutiae, like there's a lot of different details to consider when making these kinds of decisions.

**Jeremy:** [00:15:13] I was listening to some of the interviews, and an example of something that you often see is people go like, okay, let's say I'm going to use JWTs but I don't know where to store it. 

And then in your course, you talk about it's probably best to store it in a cookie and make it HTTP only so that the JavaScript can't get to it and so on and so forth. And then you're talking to, I think it was Ben (Awad). And he's like, just put it in local storage what's the big deal? In general in tutorials that you see on the internet, but in this course, it's like, you're getting these mixed messages of like, is it okay to put it here? Or is it not?

**Ryan:** [00:15:55] Yeah, it's interesting, right? Because I mean, maybe it's just like this common tack that bloggers and tech writers have, where, when they write something, I find this often and I like to go contrary to this, but what I find often, a lot of people are like, do this and don't do this. I'm giving you the prescription about what to do. 

Whereas I like to introduce options and develop a conversation around trade-offs and stuff like that. But I think where we see a lot of this notion that you're not supposed to put them in local storage or you're supposed to put them in a cookie or whatever, it's because we see these articles and these posts and whatever about how it's so dangerous to put it in local storage and you should never do it.

And there's this pronouncement that it should be off limits. And the reality is that a lot of applications use local storage to store their tokens. And if we dig a little bit beneath the surface of this this blanket statement that local storage is bad because it's susceptible to cross-site scripting... If we dig a little bit deeper there what we find is that yes, that is true. Local storage can be (cross-site) scripted. So it's potentially not a good place to keep your tokens. But if you have cross-site scripting vulnerabilities in your application, you've arguably got bigger problems anyway. Because let's say you do have some cross site scripting vulnerability that same vulnerability could be exploited to allow somebody to get some JavaScript on your page, which just makes requests to your API on your behalf and then sends the results to some third party location. 

So yeah, maybe your tokens aren't being taken out of local storage, but if your users are on the page and there's some malicious script in there, it can be running requests to your API, your browser thinks it's you because it's running in the browser in that session. And you're susceptible that way anyway. So yeah, the argument there to say local storage is not a big deal is because yeah, cross-site scripting bad, but I mean, you're not going to take your tokens out of local storage and be like, ah, I don't have to worry about cross-site scripting now. I'm good. You still have to manage that. So and that's the other thing too, like there's so many different opinions on this topic about what's right and what's wrong. Ultimately, it comes down to comfort level and your appetite for putting in measures that are hopefully more secure things like putting it in a cookie or keeping it in browser state. But maybe with diminishing returns. There's maybe some point at which putting all that extra effort into your app to take your tokens out of local storage might not be worth it because if you don't have that vulnerability of cross-site scripting anyway then maybe you are okay.

**Jeremy:** [00:18:40] And just to make sure I understand correctly. So with a cross site scripting attack, that would be where somebody is able to execute JavaScript on your website, usually because somebody submitted a form that had JavaScript code in it. And what you're saying is when you have your token stored in a cookie, the JavaScript can't access it directly, which is supposed to be the benefit. But it can still make requests to your API. Get information that is private in the JavaScript, and then start making public requests that don't need the token to other URLs?

**Ryan:** [00:19:20] Pretty much. Yeah. So if you put your token in a cookie and it's got to be an HTTP only cookie, you need to have that flag set, then JavaScript can't access it. Your browser won't let you script to that cookie, cause like you can with regular cookies, you can do `document.cookie` and you can get a list of cookies that are stored in that browser session, I guess you would say, or for that domain or whatever.

So yeah, you're right. You got it right. If someone is able though, to get some cross-site scripting, let's say you are keeping your token in a cookie. Someone gets some malicious script onto your page. They can start scripting things such that it makes your browser request your API on behalf of the user, without them clicking buttons and doing whatever, just says, make a post request, make a get request, whatever to the API... results come back. And then they just send them off to some storage location of theirs. I've never seen that in practice. In theory that can happen. It might be interesting to, to make a proof of concept of that. I mean, in theory all of that flow checks out but I've never actually seen it be done but theoretically possible. I'd be willing to bet a lot that it's happened in practice in some fashion.

**Jeremy:** [00:20:39] So following the path of your course, it starts with cookies, it goes to JWTs. And then at the end of the advanced course, it goes back to cookies and sessions. And, so it sounds like if you're going to be implementing something yourself and not using a third party service, maybe implicitly you're saying that implementing cookies and sessions probably has a lesser chance of you messing things up if you go that route. Would you agree with that?

**Ryan:** [00:21:12] Yeah, I think so. I think if you, especially like, if you follow the guidance, put forth by the library authors of these things, like maybe you got an express API. If you use something like `express-session`, which is a library for managing sessions. and you follow the guidance. You've got a pretty good chance of being really secure. I think, especially if you implement something like cross-site request forgery. If you have a CSRF token, that is, we can get into CSRF if you like, but if you have that protection in place, then you're in pretty good shape.

You're using a mechanism of authentication that has been around for a long time. And it has had a lot of the kinks worked out. JSON web tokens have been around for a while, I suppose in technology years, but it's still fairly new. Like it's not something that's been around for a long, long, long time, maybe 2014 or something like that I want to say. And really just into popular usage man in the last like four years probably is how long that's been going on. So not as much time to be battle-tested. 

I've heard opinions before about like, man, we're going to see in a few years' time... So this plethora of single page apps, that's using JSON web tokens, we're going to see all sorts of fallout from that. I've heard this opinion be expressed where people who are not fans of JWTs are able to see their potential weak spots. They say like, people are gonna figure out how to hack these things really easily and, and just, you know, ex expose all sorts of applications that way. So, yeah. TBD on that. I suppose, but it's certainly there's potential for that.

**Jeremy:** [00:22:46] And so I wonder how things change when, cause I think we're, we're talking about the case where you've got an application hosted on the same domains. So, let's say you've got your react app and you've got your backend, both hosted behind the same URLs basically, or same host name. Once you start bringing in, let's say you have a third party that also needs to be able to talk to the same API. How does that change your thinking or does it change it at all?

**Ryan:** [00:23:22] Well, I suppose it depends how you're running things. I mean, Anytime that I've had to access third party APIs to do something in my applications. It's generally a call from my server to that third-party server. So in that flow, what it looks like is a request to come from my react application to my API that I control and the user would be validated as the request enters my application. And if it passes on through, if it's valid, then a request can be made to those third parties. 

For example, if you're using third parties directly from the browser, I can't think of too many scenarios where you would be calling your API and third parties using the same JSON web token. I don't know that that would be a thing. In fact, that's probably a little bit dangerous because then you're sharing your secret key for your token with other third parties, which is not a great idea. When third parties are in the mix, generally, it's a server to server thing for me.

But you know, maybe there's a way that you validate users both at your API and at the third party using separate mechanisms, separate tokens or something like that. I don't know. I haven't employed that set up strictly from the browser to multiple APIs. For me, it's always through my own server, which is arguably, probably the way you want to do it anyway, because you're probably going to need some data from your server that you need to send to that third party and you're probably going to want to store data in your server that you get back from that third party in some scenarios. So I don't know if you go from your own server, you're probably better off I think.

**Jeremy:** [00:25:02] And let's say you're going from your own server and you need to make requests to our API. Does that mean that from your server side code you're receiving the cookie and then you send requests from then on using that cookie even though you're a server application?

**Ryan:** [00:25:23] Well in those scenarios. So this is interesting. This is where, people argue that JSON web tokens are a good fit for this scenario when you have servers to server communication. That article that I mentioned, about how you should just use cookies and sessions and stop using JSON web tokens.

The argument boils down to the fact that JSON web tokens are not meant for sessions. They're not meant to be a replacement to a session. And that's how people often use them is like a direct one for one replacement to sessions. But that's not what they are. Tokens are an artifact that is produced at a point in time that you have proven your identity, that they're basically like a receipt that you proved your identity.

And it's like, I don't know how to think about this. Maybe like when you go to an event or something and you get a stamp on your hands so that you can leave and then come back in, it's kind of like that. And then by the time that stamp washes off. It's expired. So you can't get back in that kind of thing right? So it's a point in time kind of thing. Whereas like a session would be more so like if you wanted to leave and come back from that event and every time you came back, it's like, Hey I was here just a second ago. Can you go to the back and just check with your records and make sure that I'm still valid or whatever. And then they do that and then they let you in, I don't know, maybe a bad analogy, whatever, but the point is that cookies and sessions versus tokens. It's a different world. It's not, they're not interchangeable, but people use them as if they are. 

So this article argues that a good use case for JSON web tokens is when you have two servers needing to communicate with one another needing to prove between one another, that they should have access to each other, and maybe they need to pass messages back and forth between one another. That's the sort of the promise of JSON web tokens is that you can encode some information in a token easily, send it over the wire and have it be proved on either end that the message hasn't been tampered with.

That's really the crux of it with JWTs. So getting back to your question there, yeah, that's a good use of that. It's a good use case for, for tokens is if you need to communicate with a third party API, you wouldn't be able to do that necessarily with cookies and sessions.

I mean, I don't know of a way to send a cookie between two servers. Maybe there's something there. I don't know of it. But yeah, JSON web tokens easily done because you just send it in the request header. So they go easily to these other APIs. And that, I mean, if you look at integrating various third party APIs, it's generally like, they're going to give you an access token.

It might not be a JWT, but they're going to give you an access token and that's what you use to get access to those APIs. So yeah, that's how I generally put it together myself.

**Jeremy:** [00:28:23] It sounds like in that case you would prefer having almost parallel types of authentication. You would have the cookie and session set up for your own single page application talking to your API. But then if you are a server application that needs to talk to that same API... Maybe you use, like you were saying some kind of API key that you just give to that third party, similar to how when you log into to GitHub or something and you need to be able to talk to it from a server, you can request a key. And so that that's authenticating differently than you do when you just log in the browser.

**Ryan:** [00:29:07] Yeah I think that's right I think the way to think about it is like if you've got a client involved. Client being a web application or a mobile application, that's a good opportunity for cookies and sessions to be your mechanism there. But then yeah, if it's server to server communication, It's probably going to be a token.

I mean, I think that's generally these days anyway, the only way you'd see, see it be done. I think like most of the third party services that I plug into, but the access tokens, they give you aren't JSON web tokens, from what I've seen, but if you're running your own third party services, for example, and you want to talk from your main API, perhaps to other services that you have control of then a JSON web token might be a good fit there, especially if you want to pass data encoded into the token to your other services. Yeah, that's what I've seen before.

**Jeremy:** [00:29:59] And I wonder in your use of JSON web tokens, what are some common things that you see people doing that they should probably reconsider?

**Ryan:** [00:30:11] Yeah. Well, One is that it's super easy to get started with JSON web tokens. If you use the HS 256 signing algorithm, which is kind of the default one that you see quite often, that is what we call a synchronous way  of doing validation for the token, because you sign your token with a shared secret.

So that shared secret needs to be known by by your server. And whichever other server you may be talking to so that you can validate the tokens between one another. If your API is both producing the token, so signing it with that secret and also then validating it to let your users get access to data. Super common thing to do, maybe not such a big deal because you're not sharing that secret around, but as soon as you have to share that secret around between different services, things start to open up for potentially that secret getting out and then whoever has that secret is able to sign new tokens on behalf of your users and use them at your API, and be able to get into your API.

So the recommendation there is to instead use the RS-256 signing algorithm or some other kind of signing algorithm, which is more robust. It's an asynchronous way of doing this meaning that there's then like a public private key pair at play. And, it's kind of like an SSH key.

You've got your public side and your private side. And so, if you want to be able to push stuff to GitHub, for example, you provide your public side of your key, your private side lives on your computer, and then you can just talk to one another. That is the better way of doing signing, but it's a bit more complex.

You've got to manage a JSON web key set. There's various complexities to it. You've got to have a rotating set of them, hopefully, various things to manage there. So yeah, if you're going to go down the road of JSON, web tokens, I'd recommend using RS 256 it's more work to implement, but it's worthwhile.

One thing that's interesting is that for a long time, eh, I can't remember if this is something that's like in the spec or not, but there's this big issue that surfaced about JSON web tokens, years back a vulnerability, because it was found out that if you, I think if you said the algorithm, so there's this header portion of the token, it's like an object that describes things about the token.

And if you set the algorithm to none I believe it is, most implementations of JSON web token validation would just like accept any token I think that's how it worked is like you could set the algorithm to none and then whatever token you sent would be validated, something like that. And so that issue has been fixed at the library level in most cases. But I think it's probably still out in the wild, in some respects, like there's probably still some service out there that is accepting tokens with an algorithm set to none. Not great. Right? Like you, you don't want that to be your situation. yeah. So watch out for that.

Other things that I can think about would be like, Don't store things in the token payload that are sensitive because anyone who has the token can read the payload, they can't modify it. They can't modify the payload and expect to, to make use of the modified payload, but they can read what's in it.

So you don't want secret info to be in there. If you're going to do a shared secret, make sure it's like a super long strong key, not some simple password. I think because JSON web tokens are not subject to, so I guess I'll back up a little bit. If you think about trying to crack a password and trying to brute force your way into a website, by guessing someone's password, how do you do that?

Well, you have a bot that is going to send every iteration, every variation of password I can think of until it succeeds. If you've got your password verification and things set up properly, you're going to use something like Bcrypt which inherently is slow at being able to decode or being able to verify passwords because you want to not allow for the opportunity that bots would be trying to guess passwords the slower you make it within reason so that a human doesn't have a bad time with it.

The more secure it is because a bot isn't going to be able to crack it. But if somebody has a JSON web token, they can run a script against it that does thousands and thousands of iterations per second, arguably, or however fast their computer is. And this is something that I've seen in real life in a demo is somebody who is able to crack adjacent web token with a reasonably strong secret key in something like 20 minutes, because they had lots of compute power to throw against it.

And they were just guessing, trying to guess various iterations of secret keys and it was successful because, you know, there's no limitation there on how fast you can try to crack it. So, and as soon as you do that, as soon as you crack it and you have that secret key, a whole world of possibilities for a hacker opens up because then they can start producing new JSON web tokens for their, for this application's users potentially, and get into their systems, very, sneakily.

So. Yeah, make sure you use a long, strong key or use RS 256 as your algorithm. That's my recommendation. I think.

**Jeremy:** [00:35:25] I think something that's, that's interesting about, this discussion of authentication and JSON web tokens is that in the server rendered space. When you talk about Rails or Django or Spring, things like that, there is often support for authentication built into the framework. Like they, they take care of, I try to go to this website and I'm not logged in.

So I get taken to the login page and it takes care of, Creating the session cookie and putting it, putting it in the store and it takes care of, the cross site request, forgery, issues with, with a token for that as well. And, and so in the past, I think people could, could build websites without necessarily fully understanding what was happening because the framework could kind of take care of everything.

And why do we not have that for say react or, or for Vue things like that?

**Ryan:** [00:36:25] Yeah. Well, I think ultimately it comes down to the facts that these, you know, these libraries like react and Vue are, are client side focused. I think we're seeing a bit of a shift when we think about things like next JS, because there's an opportunity now. if you have a full kind of fully featured framework, like next, where you get a backend portion, you get your API routes.

There's an opportunity for next, I hope they do this at some point in the future. I hope they take a library like next there's this library called next auth. very nice for integrating authentication into a next application, which is a bit tricky to do. It's it's surprisingly a little bit more tricky than you would think, to do.

If they were to take that and integrate it directly into the framework, then that's great. They can provide their own prescriptive way of doing authentication. And we don't need to worry about it as much, maybe, you know, a plugin system for other services, like Auth0 would be great. but the reason that we don't see it as much with react, vue, angular, et cetera, is because of the fact that they don't assume anything about a backend.

If you're going to talk about having something inbuilt for authentication, you need to involve a backend. that's gotta be a component. So yeah, that's, that's that's I think that's why.

**Jeremy:** [00:37:35] I think that, yeah, hopefully like you said, as you have solutions like, like next that are trying to. hold both parts, in the same place that we, we do start to see more of these, things built in, because I think there's so much, uncertainty, I guess, in terms of when somebody is building an application, not knowing exactly what they're supposed to do and what are all the things they have to account for.

so, so hopefully, hopefully that becomes the case.

**Ryan:** [00:38:06] I hope so, you know, next is doing some cool things with like I just saw yesterday. I think it was that there's an RFC in place for them to have like first-class tailwind support, which means like you wouldn't have to install and configure it separately. Tailwind CSS would just, come along for the ride with next JS.

So you can just start using tailwind classes, which I think would be great. Like, that'd be, I it's one of the least favorite things about, starting up a next project for me is configuring tailwind. So if they do, if they extend that to be something with off. Man. That'd be fun. That'd be good,

**Jeremy:** [00:38:37] at least within the JavaScript ecosystem, it felt like, people were people, well, I guess they still are excited about building more minimal libraries and frameworks and kind of piecing things together. and, and getting away from something that's all inclusive, like say a rails or a spring or a Django.

And it almost feels like we're maybe moving back into that direction. I don't know if that.

**Ryan:** [00:39:02] Yeah. Yeah, I get that sense for sure. I think that there's a lot of people that are interested in building full stack applications. you know, it feels like there was this. Not split. That's not the right way to put it, but there's, there was this trend, four or five years ago to start kind of breaking off into like being a front end developer or a backend developer, as opposed to like somebody who writes a server rendered app.

In which case you have to be, you have to be both just by the very nature of that. so there's specialization that's been taking place, and I think a lot of people now. You know, there's people like me who instead of specializing in one or the other, I just did both. So I call myself a full stack developer.

and now there's this maybe trend to go to, to, to, to go back to like being a full stack developer, but using both sides of the stack as they've been sort of pieced out now into like a single page app plus, some kind of API, but taking that experience and then melding it back into the experience of a full-stack developer.

I think we're seeing that more and more so. Yeah. I don't know. I think also like if you're. If you're wanting to build applications independently, or at least if you want to have like your head around how the whole thing works cohesively, you kind of need to, to be, you know, you need to have your head in, in, in all those areas.

So I think there's a need for it. And I think the easier it's made while we're still able to use things like react, which everybody loves you know, all the better

**Jeremy:** [00:40:29] Something else about react is something I liked about the course is, more so than just learning authentication. I feel like you, you, in some ways, teach people how to use react in a lot of ways. Some examples I can think of is, is how you use, react's context API to, to give, components access to requests that, that have the token included, or using your authentication context, that state to be able to know anywhere in your app, whether, you should be logged in or whether you're, still loading things like that. I wonder if there's like anything else within react specifically that you found, particularly useful or helpful when you're trying to build, an application with authentication.

**Ryan:** [00:41:20] Yeah. In React specifically. so I come from mostly doing angular work, years back to focusing more on react in the last few years. It's interesting because angular has more, I would say I would argue angular brings more out of the box that is helpful for doing authentication stuff or helping with authentication related things than something like react.

And, and maybe that's not a surprise because react is this maybe, maybe, maybe you think of reacting to the library as opposed to a framework. And angular is a framework that gives you lots of. Lots of features and is prescriptive about them. in any case, angular has things built in like route guards so that you can easily say this route should not be accessed unless some condition is met.

For example, your user is authenticated. It has its own HTTP library, which is to send requests to a server X XHR request. And it gives you an interceptors layer for them so that you can put a token onto a header to send that. React is far less prescriptive.

It gives you the option to do whatever you want. but some things that it does do nicely, I think which help for authentication would be like the react dot lazy function to lazily load routes in, in your application or at least lazily load components of any time. That's nice because one of the things that you hopefully want to do in a single page app, to help both with performance and with, with security is you don't want to send all of the stuff that a user might need, until they need it.

So an example of this would be like, if you've got, let's say you've got like a marketing page. And you've got your application, maybe under the same domain, maybe under different sub domains or something like that. and you've got like a login screen. There's no reason that you should send the code for your application to the user's browser before they actually log in.

And in fact, you probably shouldn't even put your login page in your react application, if you can help it. if you do have it in your application, you, at the very least you shouldn't ship all of the code for everything else in the application until the user has proved their identity. So to play this out a little bit, if the user did get all of the code for the application before they log in, what's the danger of that?

Well, there's hopefully not too much. That's dangerous because hopefully your API is well-protected and that's where the value is. That's where your, you know, your data is it's protected behind a, an API that's guarded, but the user then. Still has access to all your front end code. Maybe they see some business logic or they see they're able to piece together things about your, your application.

And, and a good example of this is do you follow, Jane Wong on, on Twitter? She finds hidden features in apps and websites through looking at the source code. I don't know how exactly how she does it. I'd love to talk to her about how she does it. I, I suspect that she'll like pull down the source code that gets shipped to the browser.

She'll maybe look through it and then maybe she'll, she'll run that code in her own environment and, and change things in it to coax it, to, to show various, to render various things that normally wouldn't render. So she's able to do that. And see secrets about how about those applications. So imagine that playing out for something, some situation where like, You in your front end code have included things that are like secret to the organization that really shouldn't be known by anybody definitely recommend you don't do that.

That instead you, you hold secret info behind an API, but the potential is still there. If it, if not that, then at least the user is figuring out how your application works. They're really getting a sense of how your application is constructed. So before you even ship that code to the browser, the user users should be authenticated.

before you send things that an admin should see versus like maybe a regular user, you should make sure they're an admin and reacts lazy loading feature helps with that. It allows you to split your application up into chunks and then just load those chunks when, when they're needed. so I'd like that feature aside from that, it's kind of like, you know, one of the downsides of react I suppose, is like, for other things like guarding routes, for attachment tokens, this kind of thing, you kind of have to do it on your own.

So yeah, react's lazy loading feature, super helpful for, you know, allowing you to split up your application. But aside from that other features, you know, it's kind of lacking, I would say in react, there's not, not a ton there to, to help you.

You kinda have to know those things on your own. Once you do them a couple of times and figure it out, it becomes not so bad, but still some work for you to do.

**Jeremy:** [00:46:04] Yeah. Talking about the hidden features and things like that. that, that's a really good point in that. I, I feel like a lot of applications, you go to the website and you get this giant, bundle of JavaScript. And,  in a lot of cases, a lot of companies are using things like feature flags and things like that, where there'll be code for something, but the user just never gets to see it.

And that's, that's probably how you can just dig dig through and find things you're not supposed to see.

**Ryan:** [00:46:19] Yep. Exactly. You just pull down the source code that ends up in the browser and then flip on those feature flags manually, right? That's probably how she does it, I would assume. And it's very accessible to anybody because, as I like to try to, hammer home in my courses is that the browser is the public client.

You can never trust it to hold secrets. you really need to to take care of not to expose things in the browser that shouldn't be exposed.

**Jeremy:** [00:46:44] I wonder, like you were saying how in react, you have to build, more things yourself. You gave the example of how angular has a built-in way to, to add, tokens, for example, when you're, you're making HTTP requests, I wonder if you, if you think there's there's room for some kind of library or standard components set that, you know, people could use to, to have authentication or authorization in a react or in a vue, or if that's just kind of goes against the whole ecosystem.

**Ryan:** [00:47:18] Yeah, I think there's room for it, I wouldn't be surprised actually, if you know, some of the things that I show in my course, how to build yourself. If that exists in a, an, an independent library. I think where it gets tricky is that it's often reliance on the context. And even on the backend, that's, that's being used to make those things really work appropriately.

So. I guess a good example is like the Auth0 library that's allows you to build off into a react application. It's very nice because it gives you some hooks that, are useful for communicating, with Auth0 to, for instance, get a token and then to be able to tell if your user is currently authenticated or not.

So they give you these hooks, which are great, but, but that's reliant on like a specific service. A specific backend, a session being in place Auth0 stores, a session for your users. That's how they're able to tell if they should give you a new token. I mean, I love to see that kind of stuff.

Like if there's, you know, things that are pre-built to help you, but I just. I don't know if there's like a good way to do it in a, in a sort of general purpose way because it is quite context dependent, I think.

But I, I might be wrong. Maybe there's value. In having something that, I mean, I suppose if you created something that you could have like a plug-in system for, so something may be generic enough that it gives you these useful things. Like whether the user is currently authenticated or, if a route should be guarded or something like this.

If you had that with the ability to plug in your context, like, I'm using Auth0 or I'm using Okta, or I'm using my own auth. Whatever, maybe that maybe, maybe there's opportunity for that. that might be interesting.

**Jeremy:** [00:49:03] Would definitely save people a lot of time.

**Ryan:** [00:49:05] Yeah. Yeah, for sure. And that's why I love these prebuilt hooks by Auth0, for sure. When I'm using Auth0 in my applications, it certainly saves me time.  

**Jeremy:** [00:49:14] The next thing I'd like to ask you about is you've got a podcast, the entrepreneurial coder and, sort of in parallel to that, you've been working a quote unquote, normal job, but also been doing a lot of different side things. And I wonder, whether that's the angular security book or recording courses for egghead like how are you picking and choosing these things and, and what's your thought process there?

**Ryan:** [00:49:43] Yeah, that's a good, good question. I have always been curious about business and entrepreneurial things and, and, and selling stuff, I suppose. I would say now I haven't been in business for a super long time, but I, I have been in business for a while now. and what I mean by that is, Yeah, you can take it back to like 2015 when I started at Auth0 at the same time that I was working there, I was also doing some side consulting, building applications for clients. And so since that point, I, you know, I I've been doing some side stuff. it turned into full time stuff back in 2017. I left Auth0, late 2017 to focus on, on consulting.

Then 2020, mid 2020, I realized that the consulting was good and everything like that. And I mean, I still do some of it, but it's, it's difficult when you're on your own as a consultant to be learning. And, and that's something that I really missed is that I found that my learning was really stagnating.

I learned a ton at Auth0 because I was sort of. Pushed to do so it was necessity of my job. As a, as a consultants building applications. I mean, sure. I needed to learn various things here and there, but I, I really felt that my learning had stagnated. And I think it's because I wasn't surrounded by other engineers who were doing things and learning from them and sort of being pushed to, to learn new stuff.

So yeah, an opportunity came up. With, with Prisma, who I'm now, now, working at I'm working at Prisma and it was a, it started everything kind of fell into place to make sense for it. For me. I mean, I, I don't think I would take just, just any job. It was really a great opportunity at Prisma that presented itself.

And I said, you know, I, I do miss this whole learning thing, and I do want to get some more of that. So, that's, that's probably the biggest reason that I decided to join up with a company again. So all that being said, the, the interest in like business yeah. And interest in doing product work,  like a course, this react security course, or my angular book, that came out of just some kind of like, I don't know, man, like some kind of desire. I don't know when exactly it sort of sprouted, but this desire to create a product, to productize something, productize my knowledge and to create something out of that and offer it to the world and offer it, in a way where, you know, I could be, be earning some, some income from it. And you know, there there's various people I could point to that have inspired me along that journey, the, the most prominent one is probably Nathan Barry. I don't know if you're familiar with Nathan Barry. He's a CEO of convert kit and I've followed his stuff for a long time. And he was very, always very open about, his, eBooks and his products that he creates.

And that that really inspired me to want to do something similar. And so, in trying to think of what I could offer and what I could create, authentication and, identity stuff kind of made sense because I acquired so much knowledge about it at Auth0. And I was like, you know, this probably makes sense for me to to bundle up into something that is consumable by people and I, and hopefully valuable. I sense that it's been valuable as certainly the response to the products has told me that it has been valuable. So yeah, I think that's the genesis there. And then the. interest in business stuff I think I've just, I don't know. I've always been curious about, especially about like online business, maybe, maybe less so with like traditional brick and mortar, kind of business, but, but, but online business in particular, it just the there's something alluring to it because like, if you can create something and offer it for sale, there's no, there, I'm sure there are better feelings, but I was about to say there, there's no better feeling than to wake up to an email saying that you've made money when you're you've been sleeping right. And that's, it's a cool feeling for sure. so. Yeah, I think that's, that's probably where that comes from.

**Jeremy:** [00:53:34] And when you first started out, you were making courses for egghead and frontend masters, does that feel like very distinctly different than when you go out and make this react security course?

**Ryan:** [00:53:49] Yeah. Yeah, definitely. Yeah. For a few reasons. I think that the biggest and probably the overarching thing is that when you do it on your own, you create your own course, the sense of ownership that you have over it is makes it a different thing. I'm in tune quite deeply with the stuff I've created for like react security.

And even though I've done what three, I think front-end masters courses, you know, I've been out to Minneapolis a bunch of times. I know the people there, quite well it's. There, isn't the same sense of like, ownership over that material, because it's been produced for another organization when it's your own thing.

It's, it's like your baby, and you care more deeply about it. I think so. So yeah, that's been, it's a different experience for sure. For that reason. I think too, there's the fact just the, you know, getting down to the, the technicalities of it. There's, there's the fact that you are responsible for all of the elements of production.

You know, you might look at a course and be like, okay, it's just a series of videos, but there's tons of stuff that goes into it. In addition to that, right. There's like all of the write-ups that go along with each video. There's the marketing aspects like of. You know, putting the website together and all, and not only that, like the there's, the lead-up, the interest building lead up over the course of time through building an email list that, and you collect email addresses through blog posts and social engagement.

It was building up interest on social over the course of time, like tweeting out valuable tidbits. there's just this whole complex web of things that go into putting your product together. Which means that you need to be responsible for a lot of those things, if you want it to go well, that you don't really need to think about if you're putting it on someone else's platform.

So there's, trade-offs either way definitely trade-offs. But, I mean, it depends what I want to do, but I think. If I were to do a product with some size to it, it would be I'd want to do my own, my own thing for sure.

**Jeremy:** [00:55:48] Are there specific parts of working on it on your own what are the parts (that) are just the least fun?

**Ryan:** [00:55:57] Yeah, the parts that are the least fun. I suppose for me, it's like, probably editing, editing the videos is the least fun. I've got this process down now where it doesn't take super, super long, but it's still, It's a necessity to, to the process that is always there, editing videos and, and the way that I. I dunno, I'd probably do it in a I I probably put this on myself, but I, the way that I record my videos, I editing takes quite a while. yeah, I, I think that is not such a great part about it. what else? I guess there's like the whole aspect of like, if you, if you record a video and you've messed something up and the flow of things doesn't work out, then you have to like rethink the flow.

There's any anytime I've got to do anytime I've got a backtrack, I suppose that that takes the wind out of my sails for a little while. Yeah, those are the two that stand out the most. I think.

**Jeremy:** [00:56:51] Yeah. I noticed that during some of the videos you would, make a small mistake and correct it like you would say, Oh, we needed these curly braces here. I was curious if that was a mistake you made accidentally and you decided, Oh, you know, it's fine to just leave it in. Or if those were intentional.

**Ryan:** [00:57:10] Definitely no intentional mistakes. I'd love to post a video sometime on a raw video that isn't edited because you'd laugh at it. I'm sure it's like, inevitably in every video, there's what it looks like. If you, if you were to see it unedited is a bunch of like starts and stops for a section till I finally get through and then a pause for awhile and then a bunch of starts and stops to get to the, to the next section.

So like, "In this section we're going to look at", and I don't like the way that I said it. So I start again "in this section, we're gonna look at" and then there's like five of those until I finally get it. And so my trick with editing is that I will edit from the, the end of the video to the start so that I don't accidentally edit pieces of the video that I'm just going to scrap.

Anyway, that's what I did for a long time. When I first started, it's like, I'd spend like 10 minutes editing a section, and then I get further along and I'm like, Oh, I, I, I did this section in a better way later and now I have to throw it, all that editing that I just did. So if I edit from the back to the to the front, it, it means that I can find the final take first, chop it when I start to take and then just get rid of everything before it right.

So yeah, there's, there's definitely no intentional mistakes, but sometimes like, if there's. If there's something small, like it's, Oh, I I mistyped a variable or something like that. I'll often leave that in. Sometimes it's a result of like, if I do that early on in the video, and then I don't realize it until the code runs like a few minutes later.

I'm just like internally. I'm like arggh! But I don't want to go and redo the video. Right. So I'm just like, okay, I'll, I'll leave that in whatever. And some of, some of those are good. I think in fact, I arguably, I probably have my videos in a state where they're, they're a bit too clean, like, cause I've heard a lot before where people don't mind seeing mistakes.

They actually kind of like when they see you make mistakes and figuring out how to. How to troubleshoot it, right?  

**Jeremy:** [00:59:02] The, Projects that you've done on your own have been learning courses, right. Or they've been books or courses. And I wonder if that's because you, specifically enjoy making, teaching material, or if this is more of a testing ground for like, I'll, I'll try this first. And then I'll, I'll try out, a SAAS or something like that later.

**Ryan:** [00:59:22] Right. Yeah. I definitely enjoy teaching. Would say that I, am passionate about teaching. maybe I'm not the most passionate teacher you'd come across. I'm sure there are many others that are more passionate than I am, but I enjoy it quite a bit. I mean, and I think that's why I like the kind of work that I do.

The devrel work that I do at Prisma. You know, I enjoy being able to offer my experience and have others learn from it. So at this point, like if I'm making courses or books or whatever, and I don't know if I'll do another book. I mean, writing, writing a book is a different thing than, than making a a video-based course.

And, and I don't know if I would do another one but in, in any case, I don't think it's a proving ground. I'll do other courses regardless of what other sort of things I make. But speaking of SAAS, that is an area that I'd like to get into, for sure. As time wears on here, I'd love to start and I've got a few side projects kind of simmering right now that that would be in that direction.

So yeah, I think that that's, that's an ideal of mine is getting to like a SAS where you started hopefully generating recurring revenue more, you know, more. More predictable recurring revenue, as opposed to, you know, of course it's a great, because you build up to a launch, hopefully you have a good launch.

It's a pretty good amount of money that comes in at launch time, but then it goes away and maybe you have some sales and you generate revenue as time goes on. But, less predictably than perhaps you would in a SAAS if you have one. So yeah, that's kind of where my head's at with that right now.

**Jeremy:** [01:00:51] I'm curious you, you mentioned how you probably wouldn't do another book again. I'm curious why that is and, and how you feel that is so different than a video course.

**Ryan:** [01:01:02] Yeah, I think, I think it's because I enjoy creating video based courses more than I, I enjoy writing. I like both, but writing less so. And I also think that there's this perception when you go to sell something, but if it's a book it's worth a certain price range, and if it's a video course, it's worth a different price range that is higher.

I don't think that those perceptions are always valid because I think the value that can come from a book, if it's on a technical topic that is going to teach you something, you know, if you pay $200, $250, $300 for that book, which is in our world, that's a PDF. Right. I think it's perfectly valid. I think that, people have this blocker though, when it comes to that internally, they're like, there's no way I'm going to pay that much for a PDF, but the same information in a video course, people are often quite, amenable to that. So there's that. 

I happen to enjoy creating video courses more than I do books. I think that's the reason that I probably wouldn't do a book again. And a book is a book is harder to do than a video course. I think writing a book is, is a difficult, is a difficult thing. For whatever reason. I, I couldn't tell you like technically why or specifically why, but I sense, I've heard this from a lot of people that making a book is harder than making a video course. Yeah.

**Jeremy:** [01:02:28] Yeah, I have noticed that it feels like everybody who tries to write a book, they always say it was way harder than they thought it was going to be. And it took away longer. 

**Ryan:** [01:02:36] Yeah, for sure.

**Jeremy:** [01:02:37] I do agree with the value perception. I don't know what it is, but maybe it's just the nature of the fact that, there's so much, you can just go online and see in blog posts and stuff that maybe for some reason, people don't value it as much when it's all assembled and, writing form.

But like the pitch, even your course on the landing pages, you say like, yeah, you can technically find all this information online, but you know, just think about how much time you're going to spend looking for it and not knowing whether or not it's, it's valid or not.

**Ryan:** [01:03:14] Yep. Absolutely. That's the big, the big sell I think, with, with, online education, rather than having you assemble all that knowledge yourself over the course of time, the value proposition is I will give it to you. I will show you my lessons learned and give it to you succinctly in a nicely. Kind of a, you know, collated fashion.

**Jeremy:** [01:03:34] Another thing that, I enjoyed about the course is that it was very to the point, sometimes you'll see an advertisement for a video course and they'll say like, Oh, it's got 20 hours of content, but it's like, the fact that it's long doesn't mean you learn more.

If anything, you would think you would want to spend less time to learn the same amount of material. So, yeah. I definitely appreciated that as well as the fact that you've got the transcripts underneath the video.

**Ryan:** [01:04:05] Oh, that's good to hear. That's awesome. Yeah.

**Jeremy:** [01:04:07] Cause it's like, I could watch a video and then get to the end and like, maybe I'll remember some things, but other things I won't. And then to, to pick it up, I have to go watch the video again. whereas when you've got that, that transcript, that's pretty helpful.

**Ryan:** [01:04:23] That's great to hear. Yeah, I was, I wanted to make a point of including transcripts, you know, for accessibility reasons, for sure. But, but also because you know, something that I have realized as time has gone on is that people do appreciate the, the written form. I always thought that maybe it's a little bit weird to read something that is like, the narration of a video, because it doesn't translate perhaps super well if it's in, in, in print, but I think, everything that I've heard about the transcripts has been positive. Like, like you've said, so I'm glad to hear that, people seem to like them.

**Jeremy:** [01:04:54] The last thing I'll ask is. I guess when authoring courses, or even just when you're releasing a product on your own, what are like some things that you think are really good ideas and what are some things that, you've realized like, Oh, maybe, maybe not so much.

**Ryan:** [01:05:09] Yeah. So, what I'd offer there is. it's a good idea to try to validate what you, want to create as a product. If you, if you're going for, if you're going for a sale, like right. If you want to, if you want to sell the thing, if you want to make a decent amount of money, it's a really good idea to try to validate it early on and you can do that without much effort. I think by doing smaller things ahead of time, it's things like creating couple of videos for YouTube see what the response is there. offer tidbits on places like Twitter and see what people, how people respond to them. One of the ways that I validated these courses was by doing just that, like tweeting out kind of small, valuable pieces of content, writing blog posts, and seeing how people responded to them.

And then the, like the biggest thing, though, for me for this particular course was I created the free, intro course, the react security fundamentals course. And after I saw, you know, the number of people signing up for it, I was like, okay, I think there's enough volume here. A volume of interest to tell me that if I was able to offer a sale to even a small percentage of that, that list that it would be worthwhile.

The other thing that I, would recommend is that you, that you build up an email list, you find some way to get in touch with your. audience and keep in touch with them. And that's, that's often through email. if you can build up an email list and offer valuable things to them over the course of time, they will have you in mind, they will feel some need for reciprocity when it comes time to, for you to offer something for sale, do all those things.

well before you go to release your course, the last thing I want for anyone is to release the course and nobody is there to, to buy it. And, you know, unfortunately I think a lot of people. have the assumption that if they just, you know, create it, put it up on the internet, it'll sell somehow. But the reality is you almost certainly need to have develop an audience beforehand.

At least if you do, that's the way that, you know, you can make a meaningful sort of, I guess, a impact, but also be. financial results from going down that road. So build that audience, I think is, is the key there.

**Jeremy:** [01:07:18] Cool, that's a good place to, to start wrapping up, if people want to check out your course or see what you're up to, where should they had?

**Ryan:** [01:07:26] Sure. Yeah. Thanks so much that you can go to react security.io, and I'll get you some links, to put in the show notes or whatever, but react security.io. There's a link there for. The advanced course. you can check me out on Twitter. I'm at @ryanchenkie on Twitter and, where else I've got a YouTube channel that's my name? Ryan Chenkie has my name on YouTube. I've got some sort of free stuff there. Yeah. Check those places out, you know, kind of find your way around.

**Jeremy:** [01:07:50] Cool. Well, Ryan, thank you so much for chatting with me today.

**Ryan:** [01:07:54] Thanks for having me. This has been great. I was happy to be able to do this.

**Jeremy:** [01:07:58] Thanks again to Ryan Chenkie for coming on the show. I'll be taking a short break and there will be new episodes again next month. i hope you all have a great new year and I'll see you then.

</div>