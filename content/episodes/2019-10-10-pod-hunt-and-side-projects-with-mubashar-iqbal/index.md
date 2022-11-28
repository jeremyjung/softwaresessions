+++
title = "Pod Hunt and Side Projects with Mubashar Iqbal"

description = "Mubs shares strategies for building successful side projects, how they differ from professional projects, and explains how he built Pod Hunt, an app for discovering podcasts."

[extra]
episode_url = "https://pinecast.com/listen/77ee3936-9f04-4b1f-b23a-c54d3dc9818c.mp3"
+++

Mubs is an amazingly prolific creator.  He's built 85 side projects which are all listed on his website and was Product Hunt's Maker of the Year in 2016.  His output is inspiring and he offers great advice on how to approach building side projects of your own.

### Mubs
- [Personal Site](https://mubs.me/)
- [@mubashariqbal](https://twitter.com/mubashariqbal)
- [List of Projects](https://iworkedon.com/@mubashariqbal)

### Side Projects
- [Pod Hunt](https://podhunt.app/)
- [Hacker News Day](https://hackernewsday.com/)
- [Will Robots Take My Job?](https://willrobotstakemyjob.com/)

### Pod Hunt Stack
- [Laravel](https://laravel.com/)
- [Laravel Forge](https://forge.laravel.com/)
- [Tailwind CSS](https://tailwindcss.com/)
- [VueJS](https://vuejs.org/)
- [MySQL](https://www.mysql.com/)

### Timestamps
- 01:14 - What's Pod Hunt?
- 03:42 - How are people using Pod Hunt?
- 08:42 - Why Pod Hunt isn't a native app yet
- 11:25 - How long to build the prototype?
- 15:50 - Pod Hunt's Stack
- 16:55 - Why Pod Hunt isn't a Single Page Application
- 22:18 - No CDN yet
- 23:24 - MySQL as the datastore
- 24:24 - Laravel Forge for hosting
- 28:13 - What's Hacker News Day?
- 34:06 - Choose a side project that solves your own problem
- 40:43 - The difference between projects for fun vs money
- 50:20 - Will Robots Take My Job?

---

## Transcript

[Click here to help me correct the transcript on GitHub!](https://github.com/jeremyjung/softwaresessions/edit/master/content/episodes/2019-10-10-pod-hunt-and-side-projects-with-mubashar-iqbal/index.md)

<div class="transcript">

**Jeremy** This is Jeremy Jung and you're listening to Software Sessions. 

Today, I'm speaking with Mubs. 

A lot of people talk about working on side projects, but I don't know anyone with as many as Mubs. he's even got a website called Iworkedon.com that showcases all 84 of his projects. 

That kind of output is incredible. Welcome to the show Mubs. 

**Mubs** Thanks. Thanks for having me on and it's soon to be 85.

**Jeremy** Soon to be 85.. Are you going to announce what that is here?

**Mubs** I mean I can it's actually funny because I did a podcast interview with Courtland Allen of Indie Hackers last week and we were talking about Pod Hunt and stuff like that and it gave me an idea of a really quick little hack thing. 

You know, just to kind of see if I can improve my experience around Hacker News.  So it took me about three hours to work on it, so yeah, I'll probably push that out tomorrow.

**Jeremy** 3 hour turnaround time.  I usually can't get a single-issue down in three hours. 

**Mubs** I mean I can talk a little bit about it if you want or we can talk about it afterwards as well. 

**Jeremy** Why don't we start with Pod Hunt first because you mentioned it a little bit earlier. What is Pod Hunt? And why did you decide to create it? 

**Mubs** Yeah, Pod Hunt is my attempt and lots of people have tried as well to solve the problem of podcast discovery. 

According to the most recent stats that I found there was something like 850,000 podcasts out there 450,000 active podcasts and active means that they published an episode in the last ninety days. So when there's that much content out there, it's not really organized any particular way and it's very hard to find good stuff to listen to and so, you know, so other people have tried to solve this problem as well. 

I took a slightly different approach to it in that Pod Hunt puts focus on the individual episodes not on like the overall podcast itself. 

So as an example, let's say you're a big fan of The Joe Rogan podcast it's number 1, number 2 on the charts. But even with Joe Rogan, he's put out something like 500 episodes now and which one of those 500 episodes are you going to listen to? 

So yeah, it can be awesome to find a good podcast but then you still got to hunt down the episodes that you are going to find interesting and so Pod Hunt is kind of it's a website where anybody can become a part of the community and you can submit episodes and then other people will upload those episodes and then that gives you a good way to find new episodes and find the ones that other people think are worth listening to as well. 

**Jeremy** A new set of podcast people vote on every day. So every day you go to the website. There's going to be a new set?

**Mubs** Yeah, and that was another reason to make it like that daily leaderboard. 

When I went to a few of the other attempts to solve the problem and it's like oh, these are the best podcasts and you'd come back one day and you'd see an awesome list and be like, that's fantastic. 

You'd come back a week later a month later. And it's the same list. Right? Like it's the same top podcast and I'm like well, yeah, but I wanted something new and so focusing on episodes gives us that ability to see what was published in the last day, in the last week, and it gets submitted and so every time you come because we reset the leaderboard every day you get something new and something original hopefully and something interesting that you can listen to it as well. 

**Jeremy** How do you see people currently using it? Are they typically going to the website and listening to podcasts from there or they importing that day's podcast into their own player. What do you see most people doing? 

**Mubs** I think it's a little bit of a mixture. 

So we have a feed essentially that you can add to your podcast player of the top five episodes that are voted on every day. So you don't actually have to come back to the website at all. You can just add that feed to your player and then every day you get this random sampling of the top five episodes that you can listen to. 

We also have a weekly emailing list as well. So if you don't want to come back to the website everyday once a week we'll email you the list of the top 10 podcast from the previous week as well. So we have a few different ways that people can stay kind of looped in in terms of what's good and what's not as well. 

I mean some people come back every day because they're just die hard podcasting fans and they want to see what's in here every day and they want to submit stuff as well. And then other people I think it's just more of a casual thing whenever they're looking for a new podcast. 

They say oh, what was that site I could use to find new podcasts and they kind of hop in again. I think we're also seeing a little bit of traction on social media as well. I think at last count we had about 430 followers on Twitter as well. And we tweet out any new episodes that get submitted as well. 

So people are kind of finding different ways to kind of stay in the loop about what's new. I think still the majority of people are listening to podcasts in some kind of app, whether it's the podcast app from Apple or from Spotify or something like that. So finding it on Pod Hunt and if they're not listening straight away they'll just kind of add that to their player list and then they'll listen to it whenever they have some spare time. 

**Jeremy** You're thinking they add the specific episode or you think they're adding the feed usually?

**Mubs** I think I mean most players aren't ready. You can't really add an individual episode in a lot of instances as well. So you have to follow the podcast itself. I know Breaker I think allows you to add an individual episode to your list. I think Listen Notes allows you to do that as well. But the vast majority of players they still focus on the whole entire podcast angle of things. 

That is a feature that I want to add on to Pod Hunt itself in that you can actually mark and pick individual episodes is something that you want to listen to and then we can kind of do the same thing that we do with the top 5 list and you can have a personalized these are the things that I want to listen to and it will kind of automatically appear in your player as well. 

**Jeremy** I think a lot of people feel the podcast overload, in terms of trying to find out what to listen to and  it seems like maybe with something like Pod Hunt we could get to the point where people are subscribing to this Pod Hunt feed and they get some choices that they'll probably enjoy and they can add, you know their own picks to the feed and maybe you don't necessarily have to subscribe to an individual podcast you subscribe to the one Pod Hunt feed and you can go in and kind of influence what things show up in there. Is that your vision? 

**Mubs** I think yeah, I think longer term it's more than just like what's popular but also you should be able to filter it down to like let's say you like an entrepreneurship podcast. So you like technology podcasts or whatever it is. So they'll be a way that you can follow a  category of podcast as well as individual people as well. 

So let's say you want to follow me for some reason. I don't know why you would but if I'm on a podcast now, it will automatically appear in this feed that you've kind of set up. So all of the topics that you follow all the people that you follow and even individual podcasts let's say there's one podcast that you know that you want to listen to every episode of as well or at least if it's on Pod Hunt right now because that's that's the other filter that happens automatically right? 

Because you could say that you want to follow the Indie Hackers podcast the episodes from that podcast will only appear in this customized feed if that episode appears on Pod Hunt. You're already kind of filtering even though you're following Indie Hackers if nobody submits that episode it won't actually appear anywhere, right? So you're already adding a quality filter. Hopefully Pod Hunt is that quality filter so you can subscribe to a podcast where it might not appear if nobody actually likes any of those episodes. 

**Jeremy** Yeah, that's cool. I mean it's like the the core value proposition of Pod Hunt might become, you know, this RSS feed that gives you exactly what you want. So, that'd be awesome. 

**Mubs** Yeah, I mean ultimately long-term I think it may well become like an app as well. 

So, you know you can log into the website log into your app. And then as you like things they will automatically get added to the player as well, you know things like that. 

I was building a quick MVP to see if people would like this approach to finding podcasts and things like that and so its much easier to build and iterate on that on the web then it is to build and iterate on something like an iPhone app instead. 

I started with that just because it was something that I mean it's been tried in the past, but it's been like a number of years since anybody tried this kind of approach and so I wanted to see is this something worth pursuing? I mean are there going to be enough people interested in this that it's then worth spending the weeks and months that it takes to build an iPhone app or Android app or whatever. 

And also understanding what features people are actually looking for as well, it's much easier to show people a website and say what do you think of this versus can you go and install this app on your phone and then run it and then tell me what you think, you know, it becomes much harder to do all that kind of stuff. 

And so yeah, so that was the idea because I mean I spoke to a few people and they're like if it's not a app, I'm not interested and I'm like well, that's fantastic. I love that you think apps are everything but really in terms of kind of iterating and kind of trying new things experimenting you can't really beat the web in my experience. 

**Jeremy** Yeah, so that's a trend that goes beyond just Pod Hunt but maybe into side projects in general that it's much easier to get a website going than it is a native app. 

**Mubs** Oh, yeah, absolutely even with this little idea that I spoke about there's no way I could build an entire app in three hours and submit it to the Apple Store and to Google Play and all those kind of fun things as well. 

I mean, I literally had a website up and running that I could use myself in like under an hour and it was great, you know, and even to put it on a server and have it so other people could access it. You know that took that little bit of extra time but there's no way that would have happened if I was trying to build an app. 

You know, especially with quick little side projects like this, obviously my personal friends probably would have been okay installing it but if I put it out there on the store it's very unlikely that you would just randomly find it and install it. 

If I link to it somewhere and then you get the SEO benefits, people might just search for it and find it and things like that. And then yeah and like I said, I think I've been doing web stuff for over 20 years. I've got a lot of experience in that so it's very easy for me to kind of spin stuff up. And I can have it launched in a hurry.

**Jeremy** Yeah, so let's go a little bit more into that. How long did it take you to build the initial prototype? 

**Mubs** So Pod Hunt I started working on it on July the 25th in about a week I had something that I could like share with some close friends to say look: This is what I've been working on, you know, it's not published yet. 

But yeah, it kind of works and so they could submit episodes and I could submit episodes and we got to see how the voting stuff worked and all that kind of stuff. I think I did the soft launch the week after that. So basically after about two weeks after I started it. 

I did kind of a soft launch where I just sent out some tweets and things and said, hey, I've been working on this. I think I said, I'm working on something if you like podcasts can you just kind of let me know and I sent them a link so they could find out. 

I didn't want it to be out there publicly yet because it was still closed soft-launched and I think in about a month I used that time to get feedback from people about stuff I needed to fix and improve so about a month after I started working or just after that. 

**Jeremy** Were there any like major features that you added between the soft launch and the month later or was it pretty similar and just kind of more polish that sort of thing? 

**Mubs** It was more just changing the user experience. 

So things like the the process of submitting an episode changed a lot in-between. 

When I first did the soft launch to when I did the actual launch just the whole like onboarding experience changed a lot as people were in there kind of adding themselves to the site or just signing onto the site and then submitting episodes it was mostly just around that cuz obviously you got two core experiences on the website. 

One is to submit an episode and one is to see the the leaderboard itself. 

I think basically the submission process was the hardest because there's just a lot of steps to it, you know, you kind of have to pick the podcast that you want to submit from you have to pick the specific episode that you want to submit and then you have to provide the information about that episode as well. 

Like why are you submitting it and then kind of who was in it as well. So who is the host of the podcast and if they have any guests on the podcast that that kind of stuff as well. And so collecting all that information is kind of a multi-step thing. And so just kind of making sure that was really obvious and clear about why you were doing the things that you were doing along the way was something I think made once I launched it was much easier for people to understand what was happening and submit episodes. So I think that helped with the uptake early on as well. 

**Jeremy**  I've noticed a trend with a lot of your side projects is you launch very quickly and it seems like that gets you feedback really quickly as well. So I guess is that one of your main goals with your side projects? 

**Mubs** Yeah, I think that's that's the main reason I like to launch quick and often and then launch over and over again week after week month after month to just have more small launches when you add a new feature when if it's significant enough, but it's mostly to get the product in the hands of the user so that they can tell you what's wrong. What's you know, what's awesome and kind of what else they're looking for as well because my experience has been that other people have said this but people don't really know what they want until they see it and sometimes they don't know what they don't want until you show them what you've built and then they tell you I don't want that.  

And even with screenshots, I've noticed some people put together screenshots and wire frames and things like that, but it's still very hard for people to understand. When I complete this form I put this information here. It's going to actually impact what the next form looks like, right? So understanding what the implications are selecting this and then moving on to the next step you can show the screenshots and people think they understand it. But it's never that easy, right? 

**Jeremy** Yeah for sure.  the next thing I guess I'd like to talk about is what stack did you use to build Pod Hunt? 

**Mubs** Yeah, so it's again because it's a website. It's very lean. I mean most of my side projects now are using the Laravel PHP  framework. It's very much like Ruby on Rails, but I'm a long time PHP person. I think I built my first PHP site in 2000 so I've been using PHP for a long time on and off. I mean I built stuff in Node and Python and Ruby on Rails and all that kind of stuff as well, but PHP has just kind of always been there. So I'm very very happy with it and very comfortable with it. And then on the front end I'm using the Tailwind CSS framework and it's using some VueJS and some just vanilla JavaScript as well. 

**Jeremy**  Is it a single page application or? 

**Mubs** No, actually, it's not I tend not to for MVPs do single page applications, especially for something like Pod Hunt because ultimately I want Pod Hunt to be a monster in the SEO space like every episode every person, you know, I want Pod Hunt to rank well for that and so doing a single page app makes it where you have to do extra work so that the search engines can index everything and make sure everything is okay on that side of things. 

The reason I went with Vue is the individual voting element right like so each podcast episode that's made next to it. There's a little up arrow, which you can vote on and stuff like that and obviously you have to maintain State like is user logged in have they voted on this already have they not voted on it. And so you're going to cancel the vote they have voted and stuff like that. And so trying to manage that in vanilla JavaScript or something was going to be pretty hard and also, you know that particular element in terms of has the user upvoted that I don't really care if the search engines can index that information because I don't want them to and so using Vue for those individual elements kind of made some sense because it was much easier to reuse those because I've got the same element on the home page, but when you look at the episode, it's the same element so you can sort of upvote that particular thing as well. 

So it made it easy to reuse some some core parts of the experience. And having it as a Vue component just made it so that it was all isolated and stuff and easy to kind of shift around as well. 

**Jeremy** Yeah, so it's not a single page application but there are certain pages where for example when you upvote something. It's not a full page refresh.

**Mubs** Right. So yeah, like on the homepage you can upvote all of the episodes and it just happens instantly. It's not going to refresh the page each time you up vote something and again and that's just for the normal reasons. 

Like as you scroll down I don't want you to have to upload something and then it refreshes the page. Then you got to scroll back to where you were so kind of stuff like that. So just to kind of maintain the experience as well. 

You can do that with just normal JavaScript or with jQuery as well. But using Vue, it just made it easier to maintain the state of everything. So it's easier to know if your user is logged in or if they voted and you know, because I like that because things like just changing the color when you actually upvote it it changes the color of it so that you know that you've already upvoted it and kind of things like that and and using a Vue component there just made that really easy without having to you know, track lots of different states and lots of different things for every episode. 

**Jeremy** Yeah, I mean I actually like that approach personally. I think it's pretty pragmatic because then you don't have to worry about sort of the server-side rendering aspect and SEO and that sort of thing but you still get to take advantage of some of this modern tooling to make it not so complicated when you want to have just like some interactivity on the page. 

**Mubs** Yeah, and I think still you know, I'm a big fan on the web and stuff as well so, you know, just the idea that you can come to the website and use it. Even if you have JavaScript turned off like the website, It'll still work. You still want, you know, obviously you won't be able to upvote things and things like that, but the web still works because that was my other concern is like what if I build this as a single page app like what happens on if somebody's on their iPhone on a safari browser, this is a Chrome browser Mozilla Firefox browser. All those things is like well is  (unintelligible)   is that it? 

Well it's you know, because obviously I said if the JavaScript isn't working you can still see the episode you can still see all the information about the app so you can see the table to see who's in the lead every day. Even if you can't upvote that stuff at least it all still works the core experience still works. 

With a SPA if something goes wrong because of some browser issue or whatever then basically the whole site isn't working at all. And again, this is a you know, fun little side project thing. I don't have hours and hours and hours to make sure I isolate every individual issue right? So it's like I'm trying to get the most bang for the amount of time that I have and just having it  (unintelligible)  with some progressive enhancements so that you can add some functionality on top of that I think is the best 

**Jeremy** Definitely and I think one of the nice things too is that you know, when you're switching pages you get a reload of your application, right? So you don't have to worry about the persistent state somehow getting a bug there as you move from page to page. 

**Mubs** Absolutely, you know and I built SPAs in the past as well and you know where it makes sense as well. I'm not against them but especially, you know, especially if you're targeting SEO stuff again, you can make it work, but it's but you have to do extra work, right? And again, I'm trying to I'm trying to keep the amount of work I have to do to a bare minimum as well. 

**Jeremy** Right. Um, so are you using any other managed services like for example a CDN in front of it for scaling purposes? 

**Mubs** Not yet. And again, it gets a little bit tricky because obviously if you're if you're logged in and you have to have that state of who's logged in who can vote and who's already upvoted it kind of breaks the CDN. Anyway, unless you do everything client side, which is why a lot of people end up once you have to go to a certain scale SPAs make more sense because scaling is its own expense and kind of things like that. So right now, you know, it's small enough and fast enough. I don't have to worry about that yet. Obviously, it's hopefully at some point it will become a problem and I know I'll have some I don't have to think about that. I think there's going to be little parts, I can I can cache and kind of you know offload to this CDN and things like that so that before I have to be super concerned about like moving the whole thing into SPA. 

**Jeremy** How about the the data store for the project? What are you using for that?

**Mubs** Yeah again, just try to keep it simple. Just a MySQL database. It's not like this, you know noSQL stuff it's you know, it's because it's meant to be a leader board and things like that actually having a list of things. Actually. It was more helpful in this case. I just being able to run a quick query that said, you know order it by this particular attribute and stuff like that. So scanning those tables and things were a lot was was pretty quick and and you know, the sort of relationships are pretty obvious as well. Like, you know, you got a podcast an episode a user who can upload stuff so it was all kind of fairly obvious stuff. And I'm not worried about just like randomly adding fields on to records because I know a podcast is a podcast what the attributes I know what episode is and what the attributes of the episode are. I'm not going to randomly gonna be concerned about new kind of attributes appearing like that. 

**Jeremy**   I guess the other thing I would ask is. Where is this all being hosted? 

**Mubs** So yeah the Laravel Community has this thing called Laravel Forge that a lot of people use to kind of manage their hosting. So Forge was actually written by. Taylor Rockwell who is actually the the writer of the framework itself as well and it's kind of a it's kind of a ops layer that sits in between your GitHub repositories and wherever you want to host, so they support things like Linode and AWS and Digital Ocean and all those kind of things and it's a really really cool interface that just allows you to by the you know, click of the mouse basically spin up a virtual server it installs things like, you know nginx for you MySQL for you and configures things in in in a way that can optimize them for hosting. And then it will clone your repo down into the server and kind of spin up everything in terms of configuring nginx and PHP and MySQL so they can all talk to each other and can understand all that kind of stuff so you can go from not having anything and having a GitHub repo with all of your code in it that you've pushed to having a site live in under 20 minutes. 

**Jeremy** That's that's actually really cool because it seems like you're getting sort of the user experience of using a SAAS, but it's actually being hosted on just like a regular VM, right? 

**Mubs** Yeah, exactly and it's up to you. Like like I said, it supports a few options in terms. It obviously doesn't support everybody. Although you can actually just run a script on a kind of any VM that you want as well as long as so you can say you want to add a VM and it will say if it's not in the list of the supported providers where you kind of hook up your API, so they can automatically add a new VM if you want to but you can take this script execute it on the server once you've spun it up and then it will install the software for you and then kind of connect back into into Forge so that you can manage it still through Forge even though you know, it couldn't figure it out for you automatically. 

**Jeremy** Right and but if it is one of the supported formats than let's say you use Digital Ocean or Linode you wouldn't have to create a VM and you know install nginx and install MySQL and all that which is probably the last thing you want to think about when you're trying to get a side project done, right? 

**Mubs** Right. Absolutely. And yeah, and you know, it's so in in the Forge site you you actually see ya. So once you picked, you know who you're going to host it with once they know they can actually so they will ask you like, okay what size instance would you like to make so you can create small one if you want it or large one or you can. Even I think with a with AWS and Digital Ocean you can even configure load balancers as well and sort of all sorts of options like that so that you can actually spin up depending on what your needs are. If it's just gonna be a quick little side project. You probably just need the one server but if it's if it's a more significant application then you might have. Two web servers and have a load balancer in front of it all that kind of stuff and you can kind of do all of that through their interface as well. 

**Jeremy** Cool. So, how about we circle back to the project related to Hacker News you were mentioning before? 

**Mubs** Yes, so yeah, I was talking to yeah, I was on another podcast we're talking about like the the leaderboard that Product Hunt right? It's obviously very inspired by Product Hunt as well in terms of the way that they reset their leaderboard every day. And and I was saying how I really found that really easy to you know, I could come back every day and I see this like this short list of things that were popular during that particular day and and I'd mention that you know, I that's one of the things I find really stressful about Hacker News like I come to Hacker News every day well not even every day anymore, but I come to Hacker News I just see this long stream of of right?

well have I seen that before was that from yesterday was that from the day before and so my idea was well, maybe I can turn the idea of this like segmented leaderboard. Based on the day that it was submitted and just apply that same approach to Hacker News right. Can I can I turn that long list of awesome news into something that's a little bit easier to consume. And and so yeah, I did some quick looking around and I was and Hacker News has an API that you can use the pull down all of the all the posts and you have any up votes they have and all sorts of stuff and when obviously when they were submitted and things like that. And so yes, I built a quick little page. It's really it's literally just one page where there's a there's a process that talks to the API and pulls down. I think it just pulls down the 500 most recent items according to what their so if you went to Hacker News we show you all five hundred posts essentially in the order that they appear on kind of Hacker News. And then I use that information to say okay now I want to segment that list based on when those five hundred things were actually submitted. So if they were submitted today then they're in one list and if there was somebody yesterday they're in in a second, let's say you can kind of see based on each day what the popular news was for each of the was what was popular yesterday what's popular today? And you can go back as far as you far as you want as well. 

**Jeremy** I see. 

**Mubs** So like I said, really really really simple really one page kind of thing. Yeah. I just basically I had to write the thing that queried the API to go and fetch the information and then you built a really simple little single page of that queried that table based on when it was submitted and then ordered it by by the appropriate kind of attributes as well. So and then like I said it didn't take me very long. But it but I've been using it for the last couple of days myself now and it's bit. It has been kind of interesting that I don't have to worry about like and I don't have to scan like the entire list to see what's new and what's not new because I can just say okay I know I came yesterday what's been popular since then right? Like I can just kind of say Well since. Today what was submitted and what's popular and so just seeing it broken down by when it was submitted is actually making it a little bit easier to consume that information as well. 

**Jeremy** And I'm assuming you're doing something similar to pod hunt where maybe you only show the top 10 or top certain number per day. 

**Mubs** yes. Well and I have the same thing I have on Pod Hunt is well, where so you see the sort of top 10 and then there's like a link at the end at the end of the top 10 that says that there's you know, there's 60 more or you know, it's 80 more and you can expand that if you want to. To see all of that as well. But yeah, so yeah, so the same idea that on one screen you can kind of so the way I have things set up is on one screen. I can see both today yesterday and the day before and I can see roughly depending on how long the the sort of titles are and things like that. I could see between 10 and 15 stories. And so just by scanning the one page I can see what was popular in those three days. So even if I come back like every other day, it's not like I have to worry about um, maybe I miss stuff because I didn't scan back far enough to see what was popular now. I can just kind of see on one screen I can see what's popular for the past three days instantly. 

**Jeremy** Yeah, so basically similar to Pod Hunt where you go to the page you get what let's say you want to see an article for today you just get a very short list you don't have to kind of scroll through and figure out like you were saying which ones have I seen which ones have I not seen. 

**Mubs** Right. Yeah. Yeah. I mean there's ways to add more functionality to it as well in terms of you know, I can maybe you can highlight a I can remember when was the last time I visited the page right? And then I can I can apply different styling to things that were new since I came. And things like that as well. So there's ways to kind of add more functionality to it. But yeah again, it's one of those things where it's like well build the MVP. What's the core functionality the core functionalities? Like let's segment that list. So you're not having to worry about having this stuff. And what was popular yesterday? I don't know because I have to scroll down the page three now of Hacker News to what was popular, you know, so that long ago I could see it on one page. So that's the core experience and then put it in the hands of people see what they say and if people like it and and in and if I continue to use it everyday, then I'll add more that functionality as well. 

**Jeremy** Yeah, I mean, it sounds like for both this side project and for Pot Hunt you kind of took something that was an issue for you and you figured out a way how can I save myself some time and you just decided to work on it. 

**Mubs** Yeah, and I mean I find that the best approach to you know, in terms of your finding ideas for things to work because a lot of people always reach out to me and be like, oh, yeah, and they're like, I don't know what to build. I know they're like I want to do a side project, but I don't know what to I don't know what app to build and usually my answer is like, well, you know what's causing you pain every day. What's the thing that you do either when you're having fun or in your work that you like aah I wish there was an app that where I can use to automate this or if there was something that had this information in one place. I could aggregate or something you could aggregate so that they will be easy to find it. Yeah that that if you can solve one person's problem. That's fantastic. And if that one solving that one problem might be a hundred other people who have the same issues or maybe a thousand other people were having the the same issue as well 

**Jeremy** Yeah, definitely. 

**Mubs** And then you can find that audience as well. 

**Jeremy** Yeah, I mean, that's a good approach because like you said if it kept solving the problem for you, then you would at least be motivated to work on it for yourself, right? 

**Mubs** Right. And yeah, and that's that and that's I think the other the sort of other reason that people stop working on things, you know, even if in some cases people do find something to work on but they never quite get to the launch or even if they launch and their like wow, you know, I didn't really I don't really like this thing. I don't really need it every day and I don't use it every day and then you kind of lose interest in it and it's kind of falls away by the side versus if it's something that you know, if it's going to be solving a problem for you and it's gonna be something that you're going to use. It's much easier to stay motivated and and kind of stay interested in it as well. 

**Jeremy** Definitely the next thing I kind of like to ask is how do you decide how to timebox your side projects? 

**Mubs** I tried not to I mean obviously I'm a little bit, you know, I mean, obviously I. I'm able to do things pretty fast. Now. I've been doing this for long enough where you know, I'm not really spending a lot of time learning things and kind of figuring stuff out. It's normally it's like I know what problem I want to solve and I kind of have a good idea of how I want to solve it as well. And so my main thing is I think my main approach in this kind of situation is you know, while you're excited while you're motivated about something do as much as you can. And then the more progress you make because you're excited about something the more likely you are to continue to work on it. Right so and you know, and then obviously like I said because I'm able to build things so quickly. I don't really have to worry about like, I'm not spending six months on something and I haven't launched it yet and it's starting to become a pain like why haven't I launched it yet things like that. And so yeah, that's where I think. Time boxing comes in because you like okay. Now I'm gonna give myself a certain window where I have to build something launch it because otherwise I'm just wasting time and wasting cycles and things like that. This is you know, kind of my approaches. Well, you're build it as fast as I can launch it, even if it's not ready launch it and so, you know, obviously it's hard to know when is the right time to launch and and that's that's the other thing I tell people too is like I mean when I say launch something. You know, it's not like I'm doing a massive party and launching it and like getting lots of press or anything like that. Like I'm launching it. You know, I'm sharing it with friends and their friends are sharing with their friends and things like that. So it's kind of a very low-key very soft launch that you're using to get feedback and then the minute that you can get the feedback to improve it then I think. At that point naturally you get to the point where it's like, well this feels like it's ready for something more significant in terms of a launch strategy as well. And then you can kind of figure out what's the best approach to kind of launch it more officially but as you know, I think yeah people have to get away from the idea of I got to launch it. It has to be big success it has to have this massive launch because. We just don't work like that anymore. It's not like you know. I mean, I still remember the days when companies would ship you software on on on CDs and floppy disks and things like that. And that was how you installed new software. And so this idea of a release made a lot more sense and a launch made a lot more sense. Now, I can update your website every time you come even if you come once a day if you come once an hour, there's a pretty good chance that I've launched something new in the time that you've visited the sites. So yeah, so launches happen a lot more often than you think now and so this idea of a launch is still important, but it's not like this be all end all either. 

**Jeremy** Yeah, and it sort of seems like you know, you you work on something because you are enjoying that experience or you're getting good feedback. And because you release so quickly you're sort of able to stay in that cycle rather than getting stuck and you know deciding like oh, I don't really feel like working on this because it feels so far out. 

**Mubs** Yeah, and I think you know and that's again that's yeah choosing what to work on I think is really important, you know having that good product founder fit I think is really important as well because if you pick something just because oh it's like a hot industry and I think I can build something. And you know kind of catch the wave as it were. Yeah, and you might be able to but it's not something that's going to be passionate about it, you know, especially with side projects, right? Like you've already worked 8 hours in your whatever your day job is or if your school or whatever having the energy in the motivation to work on something for another two or three hours after that after you get home. Yeah, I think that to me is the hardest thing but I like finding the the passion to come before and then so picking something that's going to give you that energy and that lifts to actually work on it is way more important than picking like what the hot industry is this week. 

**Jeremy** Definitely. I mean that definitely makes sense in terms of you know, figuring out something that you really enjoy doing. So do you think your thinking changes though, when a project transitions from not making money to making money? 

**Mubs** To some degree. I mean at some point. A project stops being a side project well, hopefully at some point a project stops being a side project, right? So and I think at that point you do have to treat it, you know, just the the amount of attention that you give it the amount of attention that it requires will change to an obviously depending on what kind of product it is in terms of if you're charging customers. You know a monthly fee to kind of use it and things like that. They expect a certain amount of functionality a certain amount of responsiveness as well. And so, you know, so it changes the dynamic of kind of your relationship with the project as well. 

**Jeremy** in your previous work when you make something that is going to charge money. Is that something you typically do from the start or is that something that you sort of have a free product and see where it goes from there. 

**Mubs** I think it depends on the product itself. Right? Like it depends. I mean, I with something like Pod Hunt. I knew that the core of the product had to be free right like people aren't going to pay to find new episodes that they're gonna listen to but obviously if you got some kind of SASS for Enterprise business then yeah absolutely you would charge, you know, kind of right from the beginning I think in many ways. For a side project you actually want to charge right from the beginning just because it will lower the support costs that you're going to incur right like just because if you've got a free tier you got lots of people signing up to try it and see what it's all about and trying to figure it out that can cost you a lot of time to kind of support all those people and to respond to their questions and kind of everything like that and you know and plus you don't know how serious they are, right. They're just kind of kicking the tires and kind of seeing. If it's something that's kind of interesting or not. What you want is you want people who are serious so that so that the so that the time you're spending is actually has the potential to give you the ROI that you're interested in as well. And so yes, I think I think for those kind of projects I would absolutely charge right from the beginning. 

**Jeremy** And this is like a very conscious decision. You're making when you're choosing the project right? Whether you think this is something that you want to make money on or it's just for fun. 

**Mubs** Yeah, absolutely. And yeah, and I think you I think that's the other thing right from the beginning whenever I start a side project or a project of any kind is understanding why right? Like I mean, I built a lot of projects where it's. It's purely for one is purely for fun that I'm like this thing will never make money and I understand that and that's cool. But also understanding the well, okay that project might lead to you know a new relationship or it might lead to just growing my network or followers. It might mean more people on my emailing list or whatever happens. To me. It doesn't have to be about charging customers, but you still have to understand why you're building. It is just a manager expectations. Right? Like it's not like I'm going to build this in it and I'm suddenly going to become the next Mark Zuckerberg, you know, good luck with that if you're building something you nights and weekend and you're spending an hour a night on it like good luck. 

**Jeremy** Yeah, I guess another thing I kind of like to ask is, you know, you're in your day job you you're a director of engineering for an agency, right? And when you approach a project at work versus a side project, how do you approach things? 

**Mubs** It's mostly just about. Time usually right like I know well and one obviously when I'm doing agency work. I'm doing work for a client. They have a certain criteria certain achievement a certain goal that they want to achieve already. So yeah, they kind of take some of that that that sort of expectations of you because they can really tell you what they want the functionality to be what they want. What the. The things to be and obviously I'm usually working on my own either like, you know, I've been working a team from anywhere from five to 20 people, you know, so so obviously having the different skill sets involved. I don't do any of the design work on kind of any of those projects. We typically have a front-end engineering team backend engineering team as well to kind of. Kind of build all the different aspects of it as well. So, you know when it comes to that, you know, you're kind of managing the project more kind of in those instances. This is obviously when I'm doing stuff on the side. It's like well, you know, what's the itch that I want to scratch right? Like what's the thing I want to do with this thing. And and like I said, how do I get to somewhere where I can launch it as fast as I can versus obviously. I mean, I know it's some of the projects I've done on my. day job have been year-long projects and so expectations and things are completely completely opposite there 

**Jeremy** yeah, yeah that that's an interesting point because you know like you were saying before with. Personal projects you're like, you know, let me see if I can ship in a week or two weeks and let me just keep getting feedback. Where with the agency work. I would guess it's like, you know, you're delivering a final product to your agency. And you know, that's that's what they're going to show to the public, right? 

**Mubs** Yeah, and I mean, I mean obviously it depends again. It depends on the client and think that we've done smaller projects in that as well. And we worked in an agile way as well on some projects as well. So we're shipping stuff to the client, you know every few weeks still so it's not like we're just doing the whole the old classic waterfall approach where you start the project in one year later. Here's your application, but it's but it's still I mean still it's just like I said, it's more like you're managing the sort of your managing the the the Sprints and things like that in kind of more organized way and you're still figuring out what can you do in those few weeks and things like that, but but the long-term vision and the long term expectations are obviously much higher in something like that. Just because I said there's more people involved. There's there's just lots of different expectations in there and and frankly, I mean also approach. the building of the application itself in a slightly different way as well like I you know, you kind of as I think about what I do for my clients is more understanding and realizing that you need to have maintainability and and scale and those kind of things in mind as you kind of work on those things. This is my side projects. I'm I'm really not worrying about that kind of stuff because one I don't know if it's an idea that people really want. Two I don't really worry about scale because who's going to use this thing anyway, and so yeah, so the sort of the so attitude changes because I'm not too concerned about the long-term and the maintainability and the scalability and all that kind of stuff because because that that's gonna be a nice problem to have at some point versus versus versus the agency work, which is like this project that I'm building, you know in theory. We'll be live for five six years. Hopefully at least and so you think about like okay, how do I build a project that will live that long with the code that I'm obviously, we'll continue to add to it stuff like that. But but the core of it will be the same for a long long time, hopefully. 

**Jeremy** Yeah, so I guess for the side project you can release quicker because you don't need to have a five-year plan for the support for example.

**Mubs** I was gonna say I mean, it's basically then MVP right like so the idea is to launch it to see what people think about it and chances are within six months to a year. If it's a project that has legs. You'll probably scrap what you built and start over and then actually build the version 1 and that will be the thing that will have its legs. Right? So so yeah, so so the idea is and that's the other reason that you kind of iterate fast is that you just you just like I had this feature. It sucks. Nobody used it. I'm just going to scrap it right like you kind of move fast like that. Try it. See if it works if it succeeds you kind of you kind of add to it. If it fails you just rip it out and start over. And so yeah, so so the things that you're trying to do at the same you're trying to build software but the sort of approach and and the way that you kind of you kind of focus on like what's the thing that you're trying to focus on and you know in my case on my side project. It's like well, let's see what the users actually want and. Obviously, it's like what can I do in that hour or two in kind of each evening that I have versus I've got eight hours every day to work on this. 

**Jeremy** For sure. So the thing I want to kind of close out with is probably the most popular side project you ever made is the project where you wrote a page about whether robots will take your job. I guess really briefly. Could you explain what that page was? And 

**Mubs** I got contacted by somebody I never met I still have never met this person Timitar lives in Bulgaria. In I believe about two years ago. He just reached out to me randomly online and was like, Hey, I've seen, you know, all the all the stuff that you built. It would be cool if we can work on. something and I was like absolutely would love to and so we're trying to figure out like what we were going to we were like well, let's start small. Let's build something really quick and easy just so that we can see if we like to work together if we like to work on the same kind of things and so he's like, oh, yeah absolutely. Sounds good. I found this research paper. That was written by some researchers at the Oxford University in 2013. That did a study of about 750 jobs or 745 I think it was and they looked at the attributes of those jobs at the skills that you need to have and they did a analysis of in 2023 would Ai and Robotics be able to do that particular job instead of a human. And so they publish this thing and it was in a PDF. It was about 300 pages long with all of the how they how they analyze everything and you know, it was just kind of a long thing and at the end they had this table which was like for every job they they come out assigned a percentage to the the the likelihood of that that job would be would be automated away. So we basically took that last bit of a report which had just that 700 jobs in it and we kind of extracted that out of the report and we built a little really simple site where you just type in the name of the of the job that you're interested in. We looked up the we looked up the percentage likelihood of that of that job you wanted and we showed you that and we show you some other stats about that particular job that we pulled from the US. Gee, I don't know what the agency is in the US that has that has the information about but we found basically for all those jobs how many workers they were in the workforce and what the what the expect if there was any more of those it's gonna be less of those over the next 20 years. So we just and what the average salary was and sort of sort of that kind of stuff and we just kind of packaged all that up into a really nice little site that looked really good because he was a designer and I was the developer on that particular site. And so we built this thing in about two weekends. Just you know, just kind of working casually with the time zones and stuff trying to work all that stuff out as well and we launched it and in the first week that it was live it'd done four  million page views.  

**Jeremy** Wow, that's incredible. 

**Mubs** It was kind of insane. Yeah, we launched on product. Um and by the end of the day it been on like and it being on MSN and I think it was on The Next Web and then we found out like just by because the traffic just kept coming in waves waves and waves of more traffic and we're like then we found out it was on like TV stations all over the country is on radio stations as well. It was on like Barstool Sports, which I didn't really know was that that popular but we got like millions of page views because it was on Barstool Sports and then it made it to the top of a couple of really popular subreddits as well. We got a lot of traffic from there as well. So yeah, that was the that was pretty awesome. It was a pretty awesome site to 

**Jeremy** Yeah. So the one thing I thought was interesting is if you go to the site one of the entries on the front page is for computer programmers and it says 48 percent thinks AI is going to replace computer programmers. So where do you think that leaves us? 

**Mubs** Well, if you think about it, it's kind of happening a little bit. Anyway, right now is not necessarily will robots right in terms of AI and things like that. But if you look at the no code movement that's happening right now. I mean, I know it's still human beings but like computer programs are being replaced by people who can't actually code. So I think it's a very good likelihood that there will be a lot of movement, especially in this space now. I mean, I think ultimately still the the rate of growth in terms of the market in terms of the things that need to be built and things that need to be coded will still outgrow the pace of jobs being, you know handled by somebody else. So I think as a computer programmer, I think I think my job is safe. I think I think there's severe need for somebody like me, but I think purely because the market is still continuing to grow there needs to be more programmers over the next 20 years than less and that's I think part of the reason that this no code movement is happening and the whole AI shift is happening is because I don't think we can keep up with the demands that are out there. So so, you know building these tools and things that allows non-technical people to be able to do some of the things that we do now is a necessity just because yeah because there just aren't enough programmers 

**Jeremy** Yeah. Yeah, and it's you also have there's some kind of research being done on things like automated program repair where program will actually be able to read its own code and try to identify problems while it's running. So I don't know how how far off that is, but there's definitely more things coming down the pipeline. 

**Mubs** Yeah, and like I said, it's you know, and there's this whole thing with automation is not you know, I don't think we're all just going to sit on our asses from you know, for the next hundred years not have to do anything because AI and Robotics are going to take over the world or anything like that. But but you know, it's just going to be a shift in the way that you know, and and when we first put forth at this website we can get asked the same question a fair bit too and it makes you think about well this happened during the Industrial Revolution as well. Right? Like if there was, you know, people are out working and yeah, then they went to work in factories. And and now you know now that we've got the software Revolution having to start working in factories of people working, you know more in software and things like that. I think even as we see the shift of AI things like that coming in, there's just going to be a skill shift as long as you can you can retrain yourself a little bit. I think there will always be work out there that still needs to happen by humans as well 

**Jeremy** Yeah, well, hopefully we'll all be ready for that. So I think that's a good place to wrap up if anybody wants to follow you or check out check out some of your other projects. Where should they look? 

**Mubs** Yeah, I mean I'm pretty active on. Twitter so, it's Twitter sure, Mubashar Iqbal which is my full name. And then as you said there's Iworkedon.com that has the the full list all on my 84 soon to be 85 side projects as well. 

**Jeremy** Very cool well Mubs. Thank you so much for joining us today. 

**Mubs** Absolutely. Thanks for having me on.

</div>