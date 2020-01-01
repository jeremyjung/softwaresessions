+++
title = "Rebuilding Fathom Analytics on Serverless Infrastructure with Jack Ellis"

description = "Jack Ellis shares his experience rewriting Fathom Analytics and migrating to AWS serverless infrastructure using Laravel Vapor."

[extra]
episode_url = "https://media.transistor.fm/7d0831ba.mp3"
+++

Jack is a software consultant with over 12 years of PHP experience.  He's currently working on [Fathom Analytics](https://usefathom.com/ref/SVQ3BG) and a [course on Serverless Laravel](https://serverlesslaravelcourse.com/).

### Jack Ellis
- [Personal Site](https://jackellis.me/)
- [@JackEllis](https://twitter.com/JackEllis)

### Fathom Analytics
- [Fathom Analytics](https://usefathom.com/ref/SVQ3BG) (SaaS, Affiliate link with $10 discount)
- [Fathom Lite](https://github.com/usefathom/fathom) (Open-source, original Golang version)
- [We rebuilt Fathom Analytics from the ground up and moved to Laravel Vapor](https://usefathom.com/news/moved-to-vapor)
- [How we built a GDPR compliant website analytics platform without using cookies](https://usefathom.com/news/anonymization)

### Laravel
- [Laravel](https://laravel.com/) (PHP web framework)
- [Laravel Vapor](https://vapor.laravel.com/) (Serverless provisioning and deployment tool)

### Hosting Providers
- [Digital Ocean](https://www.digitalocean.com/) (Host for Open-source version)
- [Heroku](https://www.heroku.com/) (Host for 1st rewrite)
- [AWS](https://aws.amazon.com/) (Host for 2nd rewrite)

### AWS Services Used
- [ElastiCache](https://aws.amazon.com/elasticache/) (Redis)
- [Elastic Load Balancing](https://aws.amazon.com/elasticloadbalancing/) (Handles web requests and triggers Lambda functions)
- [Relational Database Service](https://aws.amazon.com/rds/) (MySQL)
- [Simple Queue Service](https://aws.amazon.com/sqs/) (Message Queue)
- [Lambda](https://aws.amazon.com/lambda/) (Run functions without managing a server)

### Other Links
- [Things you should never do](https://www.joelonsoftware.com/2000/04/06/things-you-should-never-do-part-i/) (Post Jack mentions on never rewriting software)

Theme music 

### Timestamps

- [00:00:58] What's Fathom Analytics and how is it different from Google Analytics?
- [00:03:35] When was the project started?
- [00:06:00] Limiting what we know about our users
- [00:08:11] Tracking unique page views without cookies
- [00:11:50] The original Open Source Golang version of Fathom
- [00:14:06] The case for rewriting Fathom
- [00:17:46] The process of rewriting Fathom
- [00:20:49] Migrating from individual SQLite instances to multitenant MySQL
- [00:24:10] Working with DNS Caching, running the old and new application simultaneously while migrating
- [00:26:40] Moving from Digital Ocean, to Heroku, to AWS (using Laravel Vapor)
- [00:34:07] What's Laravel Vapor? (Provisioning and deployment tool for AWS serverless offerings)
- [00:37:06] Comparing how Fathom used Heroku vs AWS (Heroku Redis -> ElasticCache + SQS, Web/Worker Dynos -> SQS + Lambda functions)
- [00:40:25] Moving from Heroku Web/Worker dynos to Lambda functions
- [00:42:25] Using Elastic Load Balancer instead of API Gateway
- [00:44:01] Tracking load, downtime, maintaining availability
- [00:51:22] Walkthrough of what happens when a user visits a site running Fathom
- [00:52:50] Dealing with the AWS lambda cold start problem
- [00:54:04] Why serverless was a good fit and when to use it

Theme music is [12:30 AM](https://crystalcola.bandcamp.com/track/12-30-am) by Crystal Cola.

---

### Transcript

<div class="transcript">

**Jack** Happy to be here Jeremy

**Jeremy** So first to start off, For those who aren't familiar with Fathom could you kind of explain what it is and how it's different from something like Google Analytics? 

**Jack** Yeah So the biggest difference between Fathom and Google is that we're a simple privacy focused analytics platform. Emphasis on the simple. We all know how complex Google analytics is. 

Um so our aim is to be a one stop place that you can hop into click on a few filters and get all the data you need without having to go through all the different tabs and pages And then the second part of that is the privacy focused piece. 

A lot of people are losing trust in Google after all of the scandals they're having and people are wondering should we trust Google with our data? Does Google know too much? Should we opt for a platform where their business relies on privacy? I mean Google is fundamentally an advertising company let's not kill ourselves there. 

Um so in order for us to be a sustainable company we have to focus on privacy. And for a lot of people that's the kind of company they want to deal with. So yeah. 

**Jeremy** Yeah I think that's kind of a a trend lately where there's kind of more and more I don't know if you would call it backlash but Um a little bit of pushback in terms of the assumption that Hey companies taking all of our data and saving all of it and tracking us all over the web and all this stuff that this is kind of just a thing we have to accept and a thing that's like well there's nothing we can do about it but I feel like there's there's more and more products like Fathom where people are saying like well does it does it really have to be that way? 

**Jack** Yeah people are getting I mean I would call it a backlash. People are getting sick of big tech doing various things like this and I'm not talking about all big tech I mean I I'm definitely I'm not the anti-big tech guy I'm the anti Big tech doing shitty things guy that's who I am. 

So when we have Google who are doing I mean we're we're speculating at this point when the privacy scandals happen with Google we don't know about them until they hit the press right? So it's all speculation. And I have got to be careful with what I say but but the the um the overall theme is that people are losing trust in Google. For good reason. And um they don't want to keep sending data to Google And we're seeing people break away from Google man (?)  and everything else And I think it's a it's a good move. 

And there's a trend in privacy for good reason because all this Cambridge Analytica stuff for Facebook and and everything else people are becoming more concerned. 

**Jeremy** Right right And I think that's only gonna increase more and more because it seems like the the time til the next scandal seems to be getting more and more frequent. 

**Jack** Oh yeah you're right there. 

**Jeremy** So Fathom when when was it originally started? When was the project originally created? 

**Jack** Right You're testing my memory here. So um my partner Paul Jarvis tweeted out an idea back in 2018 this was before any of these privacy focused analytics platforms existed. He tweeted out a screenshot I mean he's a designer first right So he starts with the design. Uh it was a simple screenshot Um simple analytics and it blew up and loads of people were interested. People were replying, favoriting, or re-tweeting all of that jazz. And um and he was thinking wow there's clearly an interest for this kind of thing. And that's where it started really. 

And then it moved from screenshot on Twitter I forget if they built it or if they went straight to the landing page because I can say that Paul will usually start with when he's got an idea he'll pop a landing page to to see what the interest is. So it wouldn't surprise me if he put up a landing page first but I know that they had a lot of people in in the thousands sign up within 24 hours. 

Cause I was working with Paul on Pico at the time which which has recently been acquired by ghost as of few days ago actually. And if you know about that that's um we're working on Pico at the time And Paul was just telling me how crazy it was. 

So the original co-founder was Danny van Guten. Um the landing page would have gone up then they would have built the open source GitHub repo written in golang and release that. And then that blew up. And then the GitHub repo blew up. So um yeah that's how it all started really. And then we went on Product Hunt and got a ton of traction. People were self hosting it on Digital Ocean and everything else. And then yeah it blew up. 

**Jeremy** Yeah, so it sounds like Paul he just put out that tweet and put out that landing page and a ton of people were interested so he kind of realized like oh wow there really is a market here and just kind of ran with it. 

**Jack** Oh exactly. And it's an interest of his.   I mean I can't speak for Paul obviously but he would typically be scratching his own itch.  In this example he was sick of his analytics platform. He just wants to see the basics and um and then apparently loads of other people do too. And now we're there it's clear why. 

I mean I've I've used Google analytics analytics before and uh unless you're getting really heavy into the advanced marketing side of things you don't need Google analytics. You really don't. I know my apologies By the way I've got a I've got a fantastic cold going on so my my words emerging but um but yeah so unless you're doing you know targeted campaigns that sort of thing you don't need Google Analytics. You just don't. 

**Jeremy** Yeah It's  like most people they just want to know how many people are coming to my site and where are they coming from right? 

**Jack** Exactly, And maybe a few extra things. So how many people click play on my podcast? How many people join my newsletter? And the those are okay to track in aggregate. 

So our stance is that we are okay with tracking people on a non individual basis AKA We have 1000 people who looked at our site from the United States today. Um we're okay with that because we're not profiling individuals. We're not storing personal data. We don't need to be. So we focus on the trends rather than the this person did this this and this which is which kind of creepy if you think about it. 

**Jeremy** Yeah. So you're saying on Google Analytics you could maybe actually drill down to an individual person and see like where did they travel on my site? 

**Jack** Yeah and obviously this functionality is amazing. It's amazing functionality. But it's creepy. I'm not saying it's not useful to to know that in some cases but should you really be I've gotta be careful with thinking about exploiting your business knowing that much stuff about them without their consent. I mean now we've got the cookie banners which are just awful. Um so but at least the users know that they're being tracked beyond their wildest dreams So 

**Jeremy** Yeah Though I feel like you know when you make that cookie banner mandatory and you see it pop up people just tune it out now they're kind of like oh just click this away right? 

**Jack** Yeah it annoys people. And I'll tell you the funny thing we're seeing as well is some websites will actually block people from the EU because of GDPR. That's my favorite. Or they say we're not even going to try. Um I forget which website it was whether it was Forbes or something they have so much stuff going on and they just they just think we're not even going to try with this. 

**Jeremy** Yeah I I'm I'm sure it's changed by now but I remember when the GDPR first got put into effect the LA Times you would go to their their site from Europe and it would just say like sorry you can't you can't look at our stuff. 

**Jack** Yeah And it's crazy how much how much these websites do. I mean you just open developer tools and you have a look and you can see all the stuff that's firing and it's absolutely mind blowing. 

**Jeremy** Oh yeah for sure more than half of the payload of the page is just analytics rather than the actual content. 

**Jack** Yeah. Oh yeah Isn't that ridiculous? Yeah. 

**Jeremy** It's pretty wild. So I guess another thing that I'd kind of like to go into is one of the things that fathom does differently is I believe you don't use cookies right? 

**Jack** Yeah Yeah We're cookie free as of oh earlier this year we did a big article on it. Yeah That was a that was an interesting project.  It's not easy you know most people rely on cookies and going the cookie list way is hard Have you read the are you familiar with the article that I'm talking about? 

**Jeremy** Uh I am familiar with the article but  for our audience can you explain like at a high level sort of how it works?

**Jack** Yes, So we we landed on using  SHA  256 hashes to to identify users and the way we do it is that we've got And this is where it's quite quite hard to articulate how we do it that's why it's best best read in the article if you go to it. But and I suppose in a way the easiest way of explaining it is it's it's fingerprinting but we don't keep a historical log of the fingerprints. So a fingerprint will exist. You can't decrypt this I mean it's a it's a one way hash It's um crazy complex hash that you just can't break unless you've got the the chances of you cracking that hash are we've actually went into it with the computing power you'd need to crack these hashes and it's just ridiculous. 

But uh we will store the hash with a page view but then the minute the page view comes in again for the same user in the same database transaction we will remove the previous hash so that we have no way of building up a visitor log of the pages they viewed. And we don't have any sort of database transaction history or anything like that. 

So you can't build up a route that the user's taken. And that was important to us because even though we're obviously not going to do any of this we still don't want it to be possible to say we can see that user one did this this and this. We didn't want that. So we spent a long time going into making it impossible for us really because people have got to trust us. And yeah that was important to do. 

**Jeremy** Yeah And so essentially you're taking a fingerprint based off of the user's IP and some sort of other information 

**Jack** Yeah, so. Off the top of my head and I mean we've changed it since that article we'd already come out with quite a complex way in the first place but we introduced multiple salts now. So we chuck a salt in there that's kept for I believe about 24 hours. So we have no history of that salt. So the um the salt it changes by day. And I think we've now got it that the salt is different based on the last couple of digits of the IP or something like that. 

So you've got I think you know hundreds of different salts or probably thousands of different salts at this point. So it just gets ridiculously complicated And yeah and so yeah it's a fingerprint of those pieces. And uh honestly I can't remember it all off the top of my head but you can you can read about it on our blog on usefathom.com 

**Jeremy** For sure. Yeah We'll get a link to that in the show notes. And essentially though it's like you're taking certain pieces of information that are unique to the user whether that's the IP address or some kind of a fingerprint from the browser. And then you're applying a one way hash and making sure that you have no way of  going backwards and retrieving the information originally had.

**Jack** Yes And that last bit is the most critical piece of the whole equation because when you talk about fingerprinting if there's a way that you can Establish who these people are or you can reverse it to personal information. Then you get into very muddy waters. And uh we were clear from the start that we don't even though you know ethical company privacy focused company we still don't want to even be playing in that area. So it's absolutely critical that no one can get the data from the hash 

**Jeremy** Yeah I mean if you don't have it then you can't use it right?

**Jack** Exactly And that's just it. 

**Jeremy** The next thing I kind of want to go into is the very first version of uh Fathom that was made by Danny. You mentioned that it was written in in go how was that application built? Like was it a single service or um was it a bunch of separate applications Like how was that 

**Jack** Okay. So let's if we move away from the actual code base and talk about its existence in software as a service in the SAAS world the way that that was built there was a billing application and once you signed up it would provision and I believe it used puppet don't don't quote me on this but it had some sort of automation where it would create a directory and a handle or the DNS and everything like that. 

And I believe it would set up a SQLite file and then the compiled Go application and it would set that up across uh one of the I believe it was three um servers and then and then yeah And then you had a series of folders and they were spread across multiple servers. And that was yeah that was how it was done. 

Effectively he'd taken the open source version and just come up with a I mean I would say hacky way of deploying it and it worked. It worked fine. It just wasn't my way I mean we're now branching into into to my refactor and my rebuild here. But um I wouldn't have chosen to do it that way. Having it split across multiple servers so yeah that's how it existed in the first iteration. People would sign up then then it would be the open source version would just be provisioned and hosted for them on one of our servers. 

**Jeremy** And so would it be a separate instance for every customer? So you would take the open source version and let's say you know I had a website and I was a new customer I signed up then this whether it's puppet or some other provisioning tool would actually install a new instance of the software and create a SQLite instance for me? 

**Jack** Yeah that's right And it was um yeah that was pretty much it And I I'm about out of my depth talking about this because I only glimpse the code I glimpse the code enough to say I'm going to rebuild this. Um that's really about as far as I went so yeah automation was in place It set up multiple instances and it was spread across multiple servers. 

**Jeremy** Yeah And this was all running on Digital Ocean so these were hosted on just virtual machines. 

**Jack** Digital ocean and also why not 1&1  Surely not 1&1 It was some other some other server in the EU. 

**Jeremy** Hmm Interesting then you were kind of talking about how you made the decision to rewrite fathom and looking at what was there before what made you decide that this was the right move? 

**Jack** Yes So when I came on board it was really a case that I mean so they were having uptime issues at the time so they had to put out a lot of server fires and I wasn't I wasn't about that life. That's not something that I want to be involved in. So I came in and I thought well if we have any issues with provisioning When when new customers join any new setup any bugs or any uptime issues I wouldn't really be in a position to handle them because I'm not familiar with the setup. And um yeah And it would just be me having to learn about stuff to fix them. And I have no I have no doubts And people listening we're software engineers we are capable of learning anything. Um but it was really a case of how long will it take me to become productive within this this setup within this environment. And and for me it's going to be a few months. So I'm going to have to spend a few months to be able to do basic debugging and any improvements and that sort of thing. 

And that's just not realistic. I consult for clients full time so am I going to be learning about all of this setup and then doing that And it's just not realistic. So comparatively I could rebuild the entire thing using Laravel in the less time and I've got the experience already. So it's all good learning about something and then building it and saying Oh I've done it but you haven't got the experience. So you're then going to have to go through all this learning that you haven't had. Where as with PHP over is like over 13 years now I also I've seen all the bugs I've ever run into all the all the fun stuff. So it was it was a no brainer for me really. And uh I managed to rebuild it in I think less than two months I think it was something like that because I'm more productive in PHP and Laravel so. 

**Jeremy** Yeah that's that's actually an interesting point because you know a lot of times the narrative you hear around these types of conversations is people say like never never rebuild.  You should work with what's there because it's already working. But uh you brought up a good point that If you spend the time to learn that existing system even if you do figure it out you still don't have the the knowledge base of that that stack like 

**Jack** Oh yeah 

**Jeremy** You aren't necessarily an expert in Go. Even though you may have figured out enough to like okay how can I make some changes to this application. But you're still missing you mentioned like 13 years of PHP experience or Uh all of your experience with Laravel things like that. And those are the things that you you really wouldn't get if you had stuck with the existing application. 

**Jack** Exactly Jeremy Exactly. And I do I do remember an article I believe it was the CEO of stack overflow talking about how with your existing system you know the bugs you're going to create new bugs when you rebuild it and all that jazz. And honestly it depends where you are within your business or where you are with the software. 

If this was a product that had been live for five years. And it was huge. It was tremendous huge code base. I'd be thinking twice. We weren't dealing with a tremendous code base. We really weren't. I mean now it's definitely bigger now. We've got a lot more features and we're working on newer things. But back then it made more sense to rebuild it it was it was early days It was the first year of Fathom operating as a business. 

And yeah and obviously it's always a risk but um it was a calculated risk and I knew I could rebuild it quite quickly. And and let's be real reading Go when you when you are a programmer it's not it's not hard. So um I could read it and digest it and then converted to PHP and uh and then yeah and then I was more productive once that had been converted as expected. So it paid off. 

**Jeremy** Yes So um I kind of want to go into about how you were saying you were looking at the go and you're rewriting the code in PHP. Um was this sort of a a gradual process where you were replacing parts of the application and as you replaced them putting them in production? Or was it more like you rewrote the whole thing first. 

**Jack** So I rewrote the whole thing first Really. The biggest part of fathom is the data collection is the page view collection. Yeah The rest of it well you're taking me back down memory lane here. 

So the migration from the Go code base to the Laravel code base once it was built. So I rebuilt there were three versions. There's the first version which was the Golang version and then there's the second version which we're talking about now. And that is the first rebuild in Laravel. So I rebuilt the whole thing billing application and everything else. I then wrote some migration scripts to migrate all of the data out the SQLite files and into the new database. And that was bloody fun. Yeah Yes So that was interesting. So I migrated all the data and then the top of my head how did we do it. 

And then I believe we copied it So once it went live anything going to the old servers we would then go back and copy over to be processed by the the new servers off the top of my head is what I remember for that migration. And this migration was back early 2019 so I'm definitely less clear on what we did exactly here. But we avoided downtime by doing that. And there's always going to be DNS cache. Oh DNS cache. Yeah that's a that's good fun. But um we knew to go back to the page views table and copy them over. So um that's how we avoided the the downtime loss there. 

And we put up a notification in the dashboard and just said to people look the data's going to be slightly behind but we're not losing any of the data basically. So had a few people you know saying you know when's it going to be done? And that's fine. No one really cared as long as we keep the collection endpoint online and people's paid views aren't lost people don't care. The dashboard isn't as important as their their data being collected. So we had the flexibility there. 

**Jeremy** Yeah That's interesting  in a way it even though things are behind So in some ways you could consider that to be a form of um I don't know if you'd call it downtime but a period where things are not current Um but really the collection part never had downtime. 

**Jack** And let's let's be real here If you if your data was behind by six hours Or 12 hours to one day Do you really care that much? That's that's the question If you know your data's going to be there eventually cause remember we're dealing in transit. Most of our customers are looking at a seven day period or a month period. People aren't upset if they can't see their data for a few hours. Obviously that's not our aim That's not what I'm saying. But if we are doing a migration that's going to improve things speed things up most people are really chill So. 

**Jeremy** For sure, Yeah It's a little different than somebody who is like running a eCommerce site and you couldn't buy things for a few hours right?

**Jack** Oh that would be a completely different game. Yep. 

**Jeremy** So I kind of want to dive a little bit more into your migration from SQLite to MySQL because that sounds like quite an effort because you had individual uh SQLite instances for all your customers 

**Jack** that's right. 

**Jeremy** So how cause you're you're kind of moving from a separate install to I guess a multitenant single database right? 

**Jack** Yeah yeah exactly. Oh crikey. Okay. So I mean this this was you know obviously I joked that it was fun. Um the way we did it was that we crawled through all the directories of our customers. Okay? And then we we converted So we went through the SQLite we knew the database structure for the SQLite files and we went through all of the stats and all we did was migrate them into the new structure. So We had host names and path names. We wanted them centralized. We didn't want them to be say text entries in the page stats table. We wanted them to be reusable foreign keys for for obvious reasons. Um so we had to go through and then I think we migrated the host names in the path names and then we migrated the data into our new our new table format. 

So really it was just a it was a few loops If you think about it looping through the directories. And then once we're in a directory we loaded up the SQLite file and then we went through all of the tables and then just migrated it. And uh the the big complication was actually when so we had some users in the early days who didn't actually have site IDs. They just had a single site because fathom hasn't always supported multiple websites. So that was a bit more tricky. But you know it's just it's just a work around you know you just keep hacking at it. And And it worked and they migrated beautifully. We did have one customer who has a lot of user generated pages and it was in the I'd say probably in the millions So that was an interesting migration But uh apart from that no we got it done. 

**Jeremy** And it sounds like one of the the key differences is that you know in MySQL you had to put everybody in the same database. So did you have like a specific column I guess for the foreign key that I guess you mentioned the site IDs was that the main addition and the the rest of the schema was about the same? 

**Jack** Yeah So the big thing here is that everyone has their own sub domain. So it might be jeremy.usefathom.com jack.usefathom.com that was how you would distinguish between the two. So that was that was a good starting point. 

And then when they didn't have a site ID we just generated a site ID for them and that was absolutely fine. And that was an interesting thing as well as some people what we had to do the migration so that people didn't have to upgrade their embed code their JavaScript code. So some people  they were using their old URL which might've been the jeremy.usefathom.com But they weren't setting their site ID. So we had to be backward compatible. But I mean when you know all of these things We know how to build them the big thing was identifying the not the limitations but identifying the challenges before doing the migration. 

Once you identified the challenges and the issues it's easy. But that's the thought That's the hard part is to finding those those things in the first place. And once we did we um we ready to handle them. 

**Jeremy** Yeah, so was the schema in the new version basically the same other than you know that that one additional column? 

**Jack** It was very similar Let's just say that Very similar 

**Jeremy** Hmm And you had mentioned a little bit earlier about DNS caching can you kind of explain a little bit about why that's an issue and and sort of how you dealt with that? 

**Jack** Yeah. So the reason it's an issue is that it means that traffic for people with the old cache or from any cache for the old server their traffic would be sent to the old server rather than sent the new server And that means that any page views coming into the old server wouldn't be aggregated on the new server So we we'd be missing data.   

I mean we did talk about this and we were thinking - This is not a different version but we were thinking should we do some fancy thing that if data comes into the old server we send it to the new server via separate request. And we did talk about things like that but it gets ridiculous. 

And I think we always  opt for the simple solution and it was just let's just let it accumulate in the page views table and then we'll write a script to migrate it. You know bit by bit  in the cron job or something. And uh that ended up working beautifully And then once all the requests had stopped coming into the old servers we just turned them off. 

**Jeremy** Yeah So basically you have a Cron job and it just keeps migrating and migrating until uh eventually the DNS switches over to the new server and the old server just stops getting requests right? 

**Jack** Exactly. And honestly the majority of um requests did start going to the new server. Um but we still had a few going to the old server the DNS cache wasn't awful And you can um you can do things to reduce the testing my memory here again but you can do things to reduce the um the DNS cache so. 

**Jeremy** So at the time when you had both systems running did you have to keep basically running two production instances that are fully loaded  under the assumption that anybody could be talking to either one? 

**Jack** So the in in the migration we're currently talking about the version one to version two we had less customers so the scale wasn't as significant as it is nowadays. So um back then it wasn't as big of an issue and we were running on three VPSes so we weren't ready for scale anyway. 

If we are to talk about the migration from V2 to V3 Yes. We were fully provisioned with our old servers um because we don't know how many people are going to keep their DNS cache and everything else. So we had serverless provisioned on our new version and then we had our Heroku still fully scaled up through old version 

**Jeremy** Mm So you probably had an expensive bill that month. 

**Jack** Oh yeah And uh We had to obviously had the the database was a high availability we had to keep that online and yeah it was it was a fun build But those days are behind us So we're good. 

**Jeremy** So I want to talk a little bit about how you know you started on VPSes and you were saying like well you don't really want to have to manage servers So you moved on to using Heroku. So can you kind of talk a little bit about that decision and what was good and what were the challenges you faced with that? 

**Jack** Yeah So the way we started on the I said to Paul look How much would we pay for dev ops? And Paul actually got a quote of I think $1,000 a month for someone to do dev ops which is reasonable. But um for for a two person company did we really want to be paying $1,000 for someone to do dev ops Well absolutely not. So it's cheaper to go with Heroku because they do dev ops for us. So um it was yeah it was a really easy decision. 

Actually The um Heroku out of the door was really good you know provisioned Redis uh easy to scale dynos monitoring all this jazz If a dyno dies a new dyno gets reprovisioned and everything else I mean that's great. And it was it was great. The the we had done notifications set up so if we had too much load we could scale. And the database the high availability database was beautiful. If our database hardware failed it just rolled over to a standby instance You know and this is stuff we love. 

Yeah In terms of challenges predicting cost was obviously one because we did have cron jobs that ran to aggregate data that we couldn't necessarily predict with the costs. We also didn't have access to auto scaling unless we were to pay for the the performance dynos and they started $250 a month which I don't know why they do that. I mean maybe that's just the way of them pushing you into a higher tier. But um yeah really we weren't happy about that We felt that we should be able to have auto scale and no matter how much we're paying. And then also the tiers between the the add-ons. So the Redis we were paying a stupid amount for a tiny amount of space and I always had this ridiculous worry that we never actually encountered but I always thought what if we have so many page views that it exceeds our Redis our Redis storage and then we can't what do we do then. So and I I'd actually come up with this plan I was going to use the Redis Redis um add-on but then I was going to fall back to Uh SQS in the event that it was at maximum capacity. I thought I was all clever doing that. 

But um and then Vapor came out and Vapor solved all of these problems with scaling that we were thinking about with Heroku. And uh and that moved us to AWS well we were already on AWS with Heroku But um it moved us to Vapor. Which we had no idea Vapor was coming. So when it came it was a bit of a mind blowing experience Just announced that Laracon no one knew it knew it was coming Right. And uh and uh I said to Paul this solves all of our problems it really does. 

So that changed everything and now it felt like a fresh new start. And then we said well I I'd learned a lot I had learned um you know better ways to aggregate data better ways to um to do the data collection and everything else. So it seemed like it was an opportunity for another rebuild. And again we are still early early days And um if there's enough technical debt cause remember I built this in probably two months. It was pretty rushed. If there's enough technical debt to justify a rebuild that's when I say you should do it  it's a complicated trade off and it's always a risk But um having done it there's no regrets and it was the best move to make. 

**Jeremy** So this third rebuild that was actually a full rewrite It wasn't just like a a migration from Heroku to Vapor?

**Jack** No it was it was a full rebuild. I think it was just you know when you've got so many pieces that you you just look at it and you think I I can do so much better than this. 

And you know Paul was doing a new dashboard and with version two We actually had it. So it's a silly example but with the Ajax requests we had it so that All of the box data So the page view through the content data, the referral data, and then the live stats It came in a single request and that was much slower. 

In version three we broke it down into multiple requests that resolved in a stupid quick time. So um that was an example of what we did. But uh no honestly I think it was just I looked at everything I looked at the aggregation I looked at how the page views were collected and I just thought no We can do better than this. And uh we we changed how the jobs worked. We changed um, we changed loads of stuff I mean it was a fundamental overhaul to make it faster and just to make it a better system. And again we were still at the point where doing that was was likely going to be easier and cheaper on our time than than doing it with the current system. And I mean you're a software engineer. You know how it is modifying code can often take longer than rebuilding stuff which is very hard to explain to clients sometimes because as soon as you mention a rebuild everyone panics. 

But the thing with us is it's it's down to us. You know Paul trusts me to make the right decision with the architecture and the rebuilds and stuff and now I trust myself. So yeah the risk paid off is always a risk but it paid off. 

**Jeremy** And in this case It sounds like there was a lot of things that you wanted to change in terms of technical debt or just things that you saw like well we can do this a lot better. Do you think you would've still come to this decision if Laravel vapor that serverless solution wasn't in place Like would you have rewritten it? 

**Jack** No, we would have we would have modified the existing code base just because it's already working. Yeah Cause whenever you do a server migration or any sort of migration there's always a ton of stress. You're basically saying I want a ton of stress in my life My life's too easy Give me the stress. 

So um we would have carried on modifying it I think I would have modified the.. Cause in version two The way we did our aggregation was we actually locked rows So we went through some roads we locked them and then we processed all the locked rows and then removed them as they were processed. Um that doesn't scale too well. No shit Sherlock Right But it doesn't scale well. 

**Jeremy** Yeah So that was locking rows in your your MySQL database And you're running into a lot of uh lock contention I guess right? 

**Jack** Yeah well this wasn't so this wasn't a row level look in the typical sense  we wish we would have probably been a better way in hindsight but I actually just updated a column to lock them. It's a super scrappy basic way and this was built in under two months. But uh no it didn't it didn't scale well.  

And uh  what happened was if there were any rows that are locked. That means that the the task and the cron job doesn't run cause it says oh we're busy with the some are locked. So what does that mean. That means that if any any server issues happen you know an error, then the rows stay locked but they don't get processed. So we had one of those and just I had to debug that a few times and we were just running into more issues than it was worth you know. So um so then I said look I need to I've got a fresh set of eyes on this I'm just going to rebuild it. 

But no it's an interesting question which we are trying to rebuild Had Laravel Vapor not come out I yeah we probably wouldn't have done it. How things could have been.

**Jeremy** That's interesting. So it sounds like the release of this kind of this serverless platform you saw sort of the potential for a lot of things to change a lot of things to improve and specifically because of those features that's what really drove you to go like okay  this is worth rewriting. 

**Jack** Oh 100% yeah. We saw what was possible. And um you know and we don't want to be receiving emails saying we need to increase our scale cause we like marketing on the fact that hey we can literally handle billions of page views with version two. We could but we had to have some manual intervention for us to scale up you know how it is. Version three send us a billion page views We'll handle it You know so 

**Jeremy** yeah for sure  could you kind of briefly explain what Laravel vapor is for those who aren't familiar with it 

**Jack** Yeah So vapor is a serverless platform for PHP applications. Uh serverless being you don't have to manage any servers. Um auto scaling on demand There's no minimum provision It runs on AWS Lambda which is as you know serverless function as a service And um and yeah it focuses on the on AWS serverless offering. And what it does is it acts as effectively as a GUI for managing the infrastructure. 

So instead of you having to configure your Lambda functions and everything else vapor does it for you sets up the networks manages the firewall all of that stuff and you pay $39 a month which is an absolute steal. And it does it all for you. And we can just click around and not know anything about it and it's it's truly beautiful. 

**Jeremy** That's yeah that's that's interesting because it's sort of like having someone who's an expert in provisioning systems whether that's like puppet or Ansible or something but just having you know a service kind of take care of that for you. 

**Jack** Oh and I was so happy seeing this And uh it's funny cause I remember I'm pretty sure that uh Taylor Otwell got stick for not releasing it for free. And I'm thinking to myself it's $39 a month Are you absolutely crazy This is a bargain who wouldn't pay for this. And uh they're quick on the updates and and I just love it.  So I the other the other evening I wanted to create a new staging environment for our main application and all I have to do is run a command line say like vapor ENV staging and it creates a staging environment of the exact same set up as your production environment It does it in a few seconds. 

**Jeremy** That's fantastic 

**Jack** it's all configured via YAML files and yeah it's great It's a it's a game changer in the PHP world It really is. 

**Jeremy** So would you kind of say that somebody who was not too familiar with AWS could actually use vapor and it could set everything up and you wouldn't actually need to like know too much about how to navigate AWS console or how to deal with its API things like that? 

**Jack** Oh 100% I mean I'm my AWS knowledge is limited I'm I'm certainly no expert I obviously know my way around a little bit but um yeah it's it's the people that just want to focus on their applications and don't want to worry about the security configurations and and everything else because there are a lot of people that do worry that they haven't done their security configurations right. And that's the last thing you want is to make some stupid error with AWS So $39 a month they do it for you And uh I'm not paid to say this by the way I just I just absolutely love it 

**Jeremy** Yeah No I mean it sounds great to me cause like for for me as someone who I'm not super familiar with AWS but I've kind of gone around the console and played around a little bit and it's like it's super overwhelming There's like so much in there so much to learn just in the uh, the permission stuff alone. 

**Jack** Yeah The the IAM and  different users and a firewall yeah just no you can you can learn it but just for me no I'm good. 

**Jeremy** Yeah so I guess the next thing I'd like to sort of talk about is you know you did this big rewrite this big migration what were the things that you were moving from like to give you an example you know you had the Redis uh instancd in Heroku before I'm assuming you moved to ElasticCache another example would be you said you moved on to using Simple Queue Service So I'm kind of trying to get a picture of what are the you know services that you started using in place of other things that you had before. 

**Jack** Yeah You ask some good questions Jeremy I must say Um so yes. So for our queue cause whenever a page view comes in surprise surprise we don't hit the database right away. Who knew? We use the queue. Before we used Redis. Now we use Simple Queue Service which is pretty I mean I don't want to say infinitely cause that would technically be wrong and someone will tweet me giving me abuse. But we consider it to be infinitely scalable for our use case. So we don't worry about the Redis limit being hit. And then Simple Queue Service now handles all of our page views. Um and can can scale to ridiculous amounts. 

Um we used to have a few Redis instances We actually had Redis in our main API we had and this was our private API We had Redis for the um the caching of data like you know the typical cache you use in an application And then we add Redis for the queue And we were paying for each of those which just makes me laugh in hindsight. 

So now we just have Redis  which runs across our entire application And we store um sessions in one of the sections and then we store just generic cache in the other section. The reason we've done that is it just clears out the generic cache and not the sessions because obviously we don't want that. And then with regards to the the worker dynos yeah they just run on Lambda Vapor does something that uh To have a Simple Queue Service does something that again I don't know the details cause I don't need to know the details This is the beauty of it. But um it spins up Lambda in the background and uh Lambdas pretty much well Lambda has replaced our web dynos and and worker dynos So instead of paying a minimum amount each month for the dynos with Heroku we're now paying on demand for the Lambda Um invocations of executions whatever whatever they're called. 

**Jeremy** Yeah So I guess with um Heroku with those worker dynos was that sort of similar to having a Cron job I guess on a regular machine? 

**Jack** Um so the worker dynos actually would just listen to the queue. That's all they did. So they just then process the queue. The problem being that we'd have to pay $25 And and this sounds this does sound small talking nowadays but $25 a month that have to be  running 24/7. Comparatively Now Lambda isn't run unless they're are page views to be processed.

**Jeremy** So so you've set up uh within AWS that whenever something comes into the queue that triggers a Lambda function to be called and start processing the data 

**Jack** Yeah we didn't set anything  Vapor Did this all for us but that's what happens Yeah. 

**Jeremy** And for the initial request I'm trying to picture that when somebody goes to a website that has Fathom on it I'm assuming there's a piece of JavaScript that's  talking to your API is that correct? 

**Jack** That's correct, Yes. So the JavaScript file is uh they're  CloudFront  and then it calls our um our collection endpoint. 

**Jeremy** And so this collection end point when it was running on Heroku I'm assuming that there was  some kind of web server in front of it. How does that look like in the world of Lambda in a vapor 

**Jack** Yes I'll talk you through the differences. So with Heroku We actually had three applications We had the collector API and then I believe the to-do-do... The billing I think so the reason they were separate is because my logic was always if something happens with the API and it goes down for whatever reason I want them to be separate I want the collector to stay online. And so it made sense to have them as separate applications. 

The collector was also a separate code base again because if I push something if something managed to sneak into production I don't know how but if it did I don't want the collector to go offline. Again as I mentioned previously in the call we don't want things to go down our customers care about the data collection. We can afford some dashboard downtime we can't afford the collector downtime. 

So it actually run on a on lumen I don't know if you know lumen it's a micro framework for Laravel. So it ran on lumen separate separate code base and then it um yeah just queued things up and worked through them. 

And now coming from that into Vapor we have a single code base. But here's the cool thing about Vapor. We can have multiple environments for the same code base. So what does that mean it means that we can configure the Lambda runtime with the different memory and uh and a background worker memory. We can we give less memory to the um to the collector because it doesn't need as much. Whereas our heavier requests on the dashboard so say the background requests on the on the main application that the dashboard utilizes that needs a bit more a bit more RAM to do stuff. So we can reduce our costs by optimizing per environment which is a huge thing That's a big advantage of Lambda. So yeah So we moved from multiple code bases to one code base and we um we optimize based on the environment. 

**Jeremy** And in terms of when someone makes a request uh is it going through something like Amazon's API gateway or is there some other way that you're able to field the web requests?

**Jack** Well this is subject to change but at the moment it goes through their um Elastic Load Balancer. Um this may change I mean cause AWS API Gateway is expensive so we opted not to use that and we use just the Elastic Load Balancer which has been more than good enough for our needs. 

Maybe things will change because AWS just released the AWS API gateway pricing improvements meaning that we can I think it's $1 per million requests. So we'll see I honestly I don't think there's an advantage of using the API gateway over the load balancer. I haven't seen it yet. And I'm going to dive into this more cause I'm doing a course at the moment um on Serverless Laravel and I'm building up and I'm going to go into this because you sort of looking at it thinking well why would I use API Gateway?. Why wouldn't I just use the Elastic Load Balancer? So and I have not yet seen a reason but um subject to change of course but 

**Jeremy** Yeah Yeah Cause I mean it sounds like the main thing you're looking for is can I field a web request from you know my Javascript and then can that trigger a Lambda function right? 

**Jack** Yeah And and it I mean yeah the all the configuration from the request coming into the Lambda function I do nothing with um it's all done with Vapor I have no idea how they've done that Um and I don't need to know could I work it out? Yeah I'm sure I could work it out. Could I do it? Yes But I don't I don't need to know this but um it comes in it calls a Vapor function and then it chucks the page view in the queue and then all the magic's done.

**Jeremy** the next thing I'd like to  ask about is how do you  track the load on you know Redis and your database and things like that How do you figure out you know whether you're sized right 

**Jack** Okay So in in the Vapor dashboard we actually can monitor the Redis and when we were averaging I've just added a new node solely for redundancy. Um but the Redis uptime is pretty damn good I mean we haven't had any issues with that and we're averaging about 2-4% uh CPU load.  

And here's the thing though we can do a lot more with the caching and we're just getting into that. We're currently in a refinement Period of our product development and we're going to be doing a lot more caching. So I'm sure that that will go up But um yeah we monitor it from vapor. 

And then with with RDS you can actually set up you can set up alerts in vapor and they they just do things with AWS. So um if the CPU hits this and and everything else. So with the RDS yeah we've got some alert Um uh Alarms in place. 

But um yeah and this is another thing We opted for a fixed size RDS as opposed to a serverless RDS And one of the things that I do to avoid issues is I have limited the amount of background workers that run at any one time Okay. So imagine we get a huge influx of views. They would just queue up in um Simple Queue Service but we only have I think around 30 workers that run at any one time. 

The reason we do this is because I'd rather have a big backlog in uh Simple Queue Service than have Simple Queue Service running a thousand concurrent workers and just taking our database offline. And I actually experienced that when trying to do the migration I don't think I realized how powerful Simple Queue Service is and it took our Um it took our Heroku database offline. Um and I had to actually well we have high availability in place so it rolled over. But that was an interesting time to say the least.

**Jeremy** So in terms of like figuring out you know what the limit was  was it just sort of you you found that just during the migration or were there some tests you ran before to to figure out like what the limits of your database was? 

**Jack** Yes, a very good question. We started with Aurora and I didn't think it scaled fast enough when you've got sufficient load and not a huge issue but the the price that they charge for Aurora and they charge per uh what is it called Impl (?)  I/O I don't know if you're familiar with that. But I'm I'm Googling around I'm thinking how on earth I mean what is that? How can you even estimate the cost for that? Does that just mean per query? Does it mean.. And I just got way too deep with that and I'm not a a database ops guy I'm not a what do they call them the database The DBAs you know what I'm talking about I'm not I'm not that guy I'm not that girl so I can't I can't do that. Um so we actually just thought you know what let's just go with the fixed size database we'll overpay for it we over-provisioned it intentionally and we'll just roll with it. And um yeah we ended up with a bigger database and scaling It's easy and scaling is ridiculously quick. 

And then the first thing you're thinking about scaling a database is what about downtime? Well here's the thing  they will actually upgrade the standby database first and then they'll roll over to it And if there is any downtime we've actually built it in so that if the background worker tries to hit your database to insert the page view into the database and the database is offline it will then schedule it to not be retried for another I think five to 10 minutes. Which is which is great And then sure you build up a backlog but we store the timing of everything within the um initial payload that comes into SQS. So it's not like it's calculating the current time when it's processed because that would be a disaster. 

So um so yeah that's how we do it And then we can scale up the database to wherever we want and we'll live. But  the main database load is probably coming from the aggregation to be honest with you and um there's there's ways that we can optimize that still. cause all the page view collection does really is insert a um a record in so well a few records. 

**Jeremy** Yeah So it sounds like you have basically two instances of the database that are fixed and whenever you need to upgrade you  upgrade the um I guess you call it the standby right?

**Jack** That's right Yeah And it just is it's there and ready to be upgraded And we actually do that through AWS. Vapor does support scaling but I don't think um the Vapor supports  high availability out of the box for that I did go into AWS and set up but it's so easy I mean that's just a doddle so yeah. 

**Jeremy** And for Redis is that is that very similar Does Vapor AWS handle the availability for you? 

**Jack** Yeah I think so. Well I know it's obviously a managed service but in terms of if the Redis goes offline um I mean like I say it's a managed service so I'm not too concerned I'd imagine they'd spin something back up and then worst case our cache has to be regenerated Right. Um and that's not we've we've had our cache regenerated a few times and Yeah no concerns. We're not I mean you look at someone like Stripe for them to regenerate their cache is hilarious cause they've just got so much data. We're not at that point yet. And if we get when we get to that when we're at Stripe levels is a multibillion dollar company and a different story in lots of payment data. But that that is a different story Their cache cache is ridiculous and you see performance impact when their cache has to be regenerated for us Um for us it's you don't even notice it. 

**Jeremy** And how are you tracking downtime or failure between any of your services 

**Jack** Uh well I think we're not doing anything crazy I know Paul has monitoring but Paul hasn't received an alert in like a year I don't think so. Um I mean what have we got We've got RDS RDS is a managed service with a fail-over in place in another region. So that's handled. 

Um with Lambda Lambda serverless we don't have any servers to worry about There's not going to be the downtime. With redis I mean that's a good question about redis I've never thought is it possible for redis to go down Um I mean I don't think it is but Yeah that's something for me to look into but I don't I don't spend too much time worrying about that particular thing. 

And then what else do we have we have our email service but all emails are sent through queue worker which means they go into failed jobs So that's fine. And no there's we don't really stress about about that kind of stuff because we were pretty much apart from you know the database would consider ourselves to be pretty Serverless.

**Jeremy** Yeah I mean it's a you will occasionally see whether it's Google cloud or AWS It's not super common but sometimes you'll have an announcement that says like  Oh the instances in this region are down due to some problem And um yeah it it does happen 

**Jack** So we'll see what happens when when cause I mean when that happens then like half the internet's usually down. 

**Jeremy** Yeah that is that's true 

**Jack** So we'll have to see what happens when um when that when that arises But we've not seen it yet. But there is an argument you know why don't we have another region that our JavaScript file checks to see if the server loads If it doesn't we fire off to another region. There was an argument that we should do that and who knows Maybe we will You know you never say never. 

**Jeremy** Yeah for sure so one thing like through all of this that we haven't really talked about is when somebody embeds Fathom on their website um sort of what's the path that that call takes You know you said it talks to Elastic Load Balancer and that goes to a Lambda request and then where does it go from there 

**Jack** so it talks to the load balancer okay so the page view comes in goes through the load balancer hits a Lambda function and then it goes into straight into the queue. The queue then processes it and then the background worker the the Lambda function will insert it into a page views table. And then every five minutes we have a function that looks for finished page views or page views older than 15 minutes and it sums them up and inserts them into  page stats and referrer stats. All the other data like the country data the browser data is um inserted when the page view gets put into the page views table 

**Jeremy** Okay Yeah So it's kind of like making full use of all the different AWS services And like you said before you you don't have those individual instances or individual servers to manage anymore 

**Jack** And the re and the reason that we go into the page views table for the for the request is because we keep track of the average duration and that sort of thing So we do have to update a previous request whereas the um the browser stats and the country stats they're just they're just uh tallys just sums So we don't stress those. 

**Jeremy** And one thing that we also haven't talked about is you know you're relying on a lot of these  serverless functions And something that comes up often is  where you're trying to make a request but it takes time for 

**Jack** Oh cold starts. Yeah I mean so from the start Vapor had already solved that they had a parameter in the YAML file which was just warm up. And you put in how many uh functions you want warmed up and they do that for you. So they every 10 minutes they'll send requests to your server to keep them warm. 

However as of I think what nine days ago maybe AWS has released a new setting that allows you to to have what do they call it provision concurrency it's called  but um they yeah they released it. So um yeah probably going to be expensive but I don't know to be honest it's going to be tricky We're going to see how much it ends up costing but at the end of the day it's ridiculously valuable So 

**Jeremy** Yeah That's awesome I mean it sounds like you know you've you put a lot of thought into how to architect the system and how to make use of like all these serverless features you know to reduce  I guess system administration load on you and you know just kind of hand off as much as you can off to Amazon and off to Laravel. 

**Jack** Yes that's exactly it. So our time is worth more building the product than it is doing dev ops You know it's the equivalent of spending all of our time doing bookkeeping. Do we really want to be doing that? Well bookkeeping is not too bad. But let's say accounting like you know the tax returns and that kind of thing. We could do it. Hundred percent we could do. We could learn software engineers learn. You know we just learn quickly. Um everyone listening has learned all sorts of stuff over the years and we can pick stuff up very quickly but is our time best spent doing this. That's what it comes down to. So we want to maximize the amount of time we spend on the product and that's how we um we could get our product Like it is 

**Jeremy** and you know in kind of working in this sort of serverless environment going forward if you were working on a new project would you  move straight to serverless or are there any kind of reservations or things where you would say that well maybe we still need a more traditional application 

**Jack** Um there are definitely use cases where you wouldn't necessarily want to go serverless the big thing that we're serverless is it costs more um there I mean if you've got a basic blog why would you go serverless. Um yeah. It's There are there are lots of times you wouldn't need to go serverless. Um I mean there are infinite use cases where you wouldn't need to go I'd say it's personal decision I'd say it's also how business critical is your application. 

Um Yeah I do like putting out fires. I mean I've I've been woken up at 2:00 AM in the morning to fix a server. I don't like it It uh instant adrenaline in here and try and go try going back to sleep after that. So um it's not my cup of tea but some people don't really care if they have downtime. Um yeah And and also some people would rather hire someone to do dev ops or do it themselves and then they'll set up a a series of say five servers under a load balancer And they'll do that. 

And I'm not against that Really This is a personal preference This is me and Paul saying we don't want to spend any time doing servers. We will pay a premium to have this handled for us That's what it comes down to. And developers um We're funny because we quite often we get into this um and Taylor Otwell spoke about this on the indie hackers podcast our um of our pain threshold. We will spend five hours on something to save $5 or something which is just fun It's just brilliant. Yeah And we do that And uh yeah So but we've with this you know we have to focus on the product We can't get distracted by other things We just can't. 

**Jeremy** yeah obviously you were saying like if you're just making a blog or something really simple then yeah of course you can host it as a static site or something like that. Um but for an actual  Product  something that you hope to be a real business It sounds like at least your personal preference would be to to find out  how can I do this with serverless You know how can I do this without having to manage my own instances 

**Jack** personal preference Yeah and I'm not trying to piss anyone off and I'm not trying to say that serverless is the best and you should have to go serverless I wish you're not serious That's not where I'm going with this is really what's your appetite for server management And one of my clients I've just been speaking to about Vapor and serverless and they they're getting sick of servers. They've had a few server issues and they're just they're tired of it. For them They have business critical applications that they don't want to go offline. So they're saying serverless let's do it So yeah it depends on your appetite for server management I don't think that serverless is quote unquote better I just think it's a personal preference. 

**Jeremy** For sure so we've we've kind of talked a quite a bit about the different parts of Fathom and  went into building it Is there anything else that we missed or anything else you'd just like to mention 

**Jack** Mmm I don't think so I think one of the big big um one of the in my notes one of the big things moving from version two to version three we introduced a ton of automated tests. Test coverage wasn't good In version two we now test a minimum all of our business critical endpoints Um automatically during deployment we use Chipper CI and um all of all of our endpoints are tested prior to going live we didn't have in version two. So we also focused on testing version three So no I just I'd say anyone that's building with Laravel check out Laravel Vapor and yeah see if it fits in what you're into 

**Jeremy** Cool And um you had mentioned that you have a course coming on building with Laravel Vapor uh where can people go to Yeah 

**Jack** So I think it's yeah serverlesslaravelcourse.com Um I'm going to be sending out free tips and writing a few more articles and uh eventually I'll be releasing a course on how to use Vapor and a few of the underlying AWS pieces And then if you want simpler analytics then head to usefathom.com and a tip is if you go to our GitHub repository first look for the uh referral link cause you'll save $10 on your first invoice So 

**Jeremy** cool And if people want to kind of follow you or see what you're up to uh where should they head.

**Jack** Yeah So for my ramblings head to Twitter slash Jack Ellis 

**Jeremy** Very cool Well Jack it's been a pleasure talking to you about rebuilding Fathom 

**Jack** Yeah Cheers Jeremy.

</div>