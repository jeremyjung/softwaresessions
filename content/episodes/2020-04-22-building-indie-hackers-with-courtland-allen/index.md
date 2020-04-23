+++
title = "Building Indie Hackers with Courtland Allen"

description = "Courtland Allen talks about the technical details of building Indie Hackers"

[extra]
episode_url = "https://media.transistor.fm/ab7a382f.mp3"
+++

Courtland Allen is the founder of Indie Hackers, a community for people who want to start bootstrapped and profitable businesses. It was acquired by Stripe in 2017. 

We discuss:

- Why a SPA was the wrong choice
- Caching strategies
- Using firebase and algolia
- Fighting spam
- Why he hasn't hired another engineer
- Focusing on the right problems
- Being a part of Stripe

Related Links:

- [Indie Hackers](http://www.indiehackers.com/)
- [@csallen](https://twitter.com/csallen)
- [Stripe](https://www.stripe.com)
- [How to Build a Life You Love by Quitting Everything Else with Lynne Tye of Key Values](https://www.indiehackers.com/podcast/086-lynne-tye-of-key-values) (One of Courtland's favorite podcast episodes)
- [Ember](https://www.emberjs.com/) (SPA framework)
- [Ember fastboot](https://ember-fastboot.com/) (Server Side Rendering)
- [Firebase](https://firebase.google.com/) (Authentication provider and NoSQL database)
- [Algolia](https://www.algolia.com/) (Provides search for posts)
- [Render](https://render.com/) (Web Host)
- [Dribbble](https://dribbble.com/) (Site to find design inspiration)
- [Egghead](https://egghead.io/) (Developer video courses, got started selling zip files of videos to mailing lists)
- [Balsamiq](https://www.balsamiq.com) (Wireframing tool, added inspirational quotes to their loading screen so that people wouldn't complain about loading time)
- [Dan Luu](http://danluu.com/) (Popular tech blog with no styling)


Music by Crystal Cola: [Orion](https://crystalcola.bandcamp.com/track/orion)

---

### Transcript

<div class="transcript">

**Jeremy** Today, I'm talking to Courtland Allen, the founder of indie hackers. Courtland. Can you explain what it is?

**Courtland**  Sure. Indie Hackers is an online community for people who want to start bootstrapped and profitable internet businesses. We've got a podcast where I'll interview these indie hacker founders and ask them how they came up with their ideas, how much money they're making, how they got to where they are today.
We've also got the same thing on our website, about 450 interviews with founders who've shared the revenue numbers and basically all the behind the scenes information about how they do what they do. And then we've got a community forum where these founders and other people who aspire to be indie hackers and start their own companies go to ask each other questions and share advice and tips and strategies just to help each other out.

So the kind of common thread is pretty much everybody's working with the goal of freedom. Most people who are indie hackers don't like having regular jobs. They don't like having a boss. They don't like having an upper limit to how much they can get paid. They don't like having to work regular schedules.

And so they want the freedom to work from wherever they want. The freedom to earn as much money as they want, the freedom to work on whatever project they creatively choose to decide to work on, and the freedom to work with the people that they want. So a lot of it is just about independence and freedom.

**Jeremy** Yeah. And like, if you actually go look at the site now, like you said, there's all sorts of things going on. Like there's the, the forum, there's the interviews. people can post their products, um, the revenue they're making and all sorts of things. From the very beginning. Um, it was a lot simpler than that right? So, so how did indie hackers like first start off?

**Courtland** Yeah. At first, it just started with the interviews on the website, so I knew I wanted to be an indie hacker. Um, of course that word, the term didn't exist yet, but I had read stories on other websites about these software engineers who are like, Hey, you know, I'm tired of working for Google. I'm tired of working at startups.
I want to make my own startup, but I don't want to go the traditional Silicon Valley route. I want to build my own thing. I want to charge money for it. I don't want to raise money from investors. And they would every now and then share their stories on various websites, like hacker news or on Twitter or on some news websites.

And I was trying to come up with an idea of my own. And so I basically devoured these stories. I was reading them everywhere. I could find them, but it was really hard to find them because these people just don't get a lot of press if you're not making $1 billion, if you're not a unicorn company, uh, the tech press doesn't really want to write about you.

And so it's hard for others to emulate what you're doing cause they can't even find out about you. So in the middle of doing all this research myself, I came up with sort of the meta idea that, Hey, I can tell there other people like me who are also searching for this information. I can see them in the comments asking the same kind of questions I'm asking.

I'm trying to do the same kind of research that I'm doing. What if my idea was to create sort of the central hub online to make all this information easy to find. And so that was the Genesis of indie hackers. It started off as just a blog where I would find these people and I would interview them and I would ask them all the specific questions.

That people like me wanted answered. I think if you're just sort of reading these stories for entertainment, you didn't really care what kind of questions and information was shared. It was just entertaining to you. But if you're like me and the millions of other people who wanted to be indie hackers, you really cared about specific stuff, like how much money is this person making that puts their entire story into context.

How do they come up with the idea? Because you're trying to come up with an idea and you want examples. How do they find their first customers? Because that's often the hardest part. Finding customers and. Usually if you're a software engineer or someone who can build something, you're comfortable in that arena, but you're not necessarily comfortable with marketing and business and all that kind of stuff.
So I asked everybody the same set of questions, and I launched the site with just 10 interviews, and it wasn't for another three or four months and many dozens of interviews before I started adding other resources like the podcast and the community forum, et cetera.

**Jeremy** And what I think attracted a lot of people to the site is the fact that there were specifics, right? Specific numbers in terms of how much money you were bringing in, how much you were spending. So I think, today in sort of our conversation, I want to also go into the specifics of, you know, how you built indie hackers.

So, you know, going back to that first, page that just had the 10 interviews. you know, what was that builtin? Was it just, you know, HTML and CSS or, you know, kind of, how'd you first get started?

**Courtland** Yeah. So I'd started a bunch of different companies in the past and none of them succeeded the way I wanted them to. And for every single one I realized I'd made the same mistake that a lot of other software engineers make, which is that I underestimated how much time and effort would go into this thing.
And so part of the criteria I use to decide to build indie hackers compared to some other ideas I had was, this is just a blog. It's not that complex to build. I'm not going to waste six, 12 months of my time building all this infrastructure before I can even get my product out and have people using it.

Uh, I could literally sign up for a medium account today or a blogger account today and have a blog going in like two seconds. Um, and so sort of my compromise to myself since I am a developer and I do like building stuff. Was that since it's such a simple, simple website to build. I would allow myself the luxury of building it from scratch on my own.

So I ended up building my own blogging software for indie hackers, which, uh, only took a couple of weeks while I was also doing the interviews. So those first few weeks, I think it was like three weeks between when I came up with the idea, and when I launched it, I was doing almost nothing besides building the blogging software and designing it, and also emailing literally hundreds of people to try to get them to do an interview.

And so when I first launched, basically, indie hackers was hosted on AWS, I was using elastic Beanstalk, which is sort of their scaling service to make sure your server doesn't crash if you get on hacker news, which was my plan for launching it. And I had done custom front end using obviously HTML and CSS.

I was using Ember JS as my front end JavaScript framework. So indie hackers is a single page app, um, and not much else was going on besides that. One thing I did put a lot of time into was the design. I knew that one of the biggest things you want to do if you have a content based website, is differentiate yourself.

When people come visit your website, you don't want them to think, Hey, this looks like every other website I've seen. Otherwise, they're not going to remember you when they come back and they're not going to become a loyal subscriber. They're not going to remember like, Hey, this really good content was on this specific website.

So I saw that all the other blogs were, you know, white with black text. I made indie hackers dark blue with white text. And I tried to put really bright colors and vivid colors on there, and instead of making the homepage look like a blog, I created like a different square with a bright icon for every single different interview that I did.
Just so when you came back to the site, it would instantly stand out as something that was memorable to you. And also with the name itself, I wanted to not describe my website, but the people that my website was sort of promoting and the people like me who wanted to basically create their own path to freedom through their own startup.

So I called it indie hackers, which was sort of a made up term at the time, but it sort of caught on. So there are a lot of considerations, not just technical, but also uh strategic early on that I thought would pay dividends down the road.

**Jeremy** That's definitely one of the things I noticed when I first went to indie hackers is that the look was very distinctive. I think there's a lot of people who know how to build backend software.  And you know, maybe toy around with HTML a little bit, but they don't really have that design sense.

Like, where did that come from for you? Like, how are you able to come up with a design that, that actually looks really great?

**Courtland** In terms of a design that looks different, I think. That's simple. Just look at what everybody else is doing and do the opposite. I think people are, we're sort of like a, we're like herd animals you know, we take a lot of comfort in copying what other people do especially when there's uncertainty. 

If there's something that you're not good at, your default instinct is to look around and what everybody else is doing. If you want to stand out, you need to ignore your instinct and do the opposite of what everybody else is doing. Even if every other website is super slick and looks professionally designed, honestly, maybe just make a really rough, shoddy website that looks like it's not professionally designed and embrace it. And even call it out and talk about it.

I think the worst thing you can do is if you're not great at design, is try to make a super slick design cause then it's just gonna look inferior to everybody else's. Cause obviously you're not going to beat them at their own game if you're not good at that game.

If you do want to become a good designer. My advice is practice. It's no different than becoming a good developer. It's no different than becoming a good basketball player. It's just put in the reps and practice design a hundred websites. Pay attention to why yours looks worse than others. Go on dribble, look up some good designs.
Try to recreate them from memory and after you put in some reps, it doesn't matter if you have a naturally good eye for design, you'll get better.

**Jeremy** You're saying like, in order to get those reps in order to practice, maybe you do start with copying with those other people made and then somehow you just get this intuition in terms of what will work when you do something different.

**Courtland** That's exactly what it is. 

Intuition I think we tend to believe it's something that you're born with, but it's the exact opposite. And intuition is something that you develop through repeated experience and practice. And so if you want to become a really good designer or really good, anything, you need a ton of practice and eventually some of the things that require conscious effort for you to think about upfront and that aren't obvious.
Will sort of be burned into the circuitry of your brain and become second nature to you, and you will be able to sort of build off those things without wasting any brain power, even having to think about them. In other words, it'll become intuition. And so that's how you get good at being a designer or pretty much anything else.

But again, like if you're trying to start something new and it's your first time you're probably not going to be a good designer right out of the gate. You should probably focus on your strengths. You know, there are things that I'm not good at. I definitely didn't build those into the strategies for indie hackers.

If I wasn't a good designer, I would not have tried to differentiate or tried to make a really slick design. I would have differentiated by having a really crappy, bare bones design.

**Jeremy** Do you have any good examples of people who when they first launched a product, uh, and you know, they didn't have those design skills, they made something that either looked really bare bones or like looked really dated, but that  was part of the message of the product?

**Courtland** You know, I think. In the developer space in particular, a lot of developers just make really bare bones looking stuff, or sometimes they'll just eschew the design altogether. So Joel Hooks, for example, runs a website called egghead, and I don't want to hate on egghead's design egghead looks great, but when he first built egghead, like he didn't even have a website, he went on YouTube.
He found a guy who had been producing some really great developer content on YouTube. He's formed a partnership with them and said, Hey, can I package these all into a zip file? And send them an email to your list and, you know, charge people for it. And the guy's like, no one's ever going to pay for this, but go ahead and you can try it.

And he did it. And he knew that because his target audience was developers, like he didn't need a sleek website. Developers don't care that much about the glitz and the glamour. They just want the thing, right? They, they're more than happy to get a zip file with a bunch of educational videos in them. And so I think, you know, that's an extreme example where someone just basically bypassed design altogether because he knew his audience and what was going on.

Whereas if you're, say, trying to start a bank. Are you trying to open a restaurant? Well, those are very trust-based businesses. People have to trust that you're going to keep their money safe. They have to trust that you're not going to poison them with their food. So essentially they're looking at all these little idiosyncrasies or looking at, uh, everything you do to determine is it top notch quality, because that's sort of a clue as to whether or not they can trust you.

And if you have like a really broken ugly banking website, you look a little sketchier. If you have a really dirty website, you look a little less trustworthy. A restaurant and look a little bit less trustworthy. So I think you have to determine, you know, who your audience is and what you're doing, and then figure out what, where do I need to shine here?

What's important and what's not? And it's not the same for every industry. It's not the same for every company.

**Jeremy** Actually, it kind of reminds me of, I had a conversation with Ben Orenstein previously, and I remember hearing on a podcast with him, he had mentioned that, they were looking for products. Um, I don't remember if it was for forms or for something else. And, what their team had done is they basically looked at the landing pages of each of these products.

And there were certain ones where that landing page just looked sketchy. And they're like, Oh, well, I don't feel like we can pick this one, just cause it looks 
like it's kind of questionable. So that's, that's interesting. 

And it also reminds me of, um, there's a, blog by a guy named Dan Luu and it's just danluu.com. And if you go there, There's no styling. It's just text. 

But the content is really good and it goes really deep into different topics. It's a good reminder if the content is something that people really want to see they're not gonna worry about the fact that there's no styling.

**Courtland** No, not at all. And I think even as a creator, sometimes when you can make these conscious decisions about what you're not going to focus on. It really frees you up to do better on the things that you do focus on because there's only so much time in the day and you only have so much motivation and willpower.

A lot of people won't get started on a project or they'll never take it to completion because there's so many blockers. They have to do this right, and they have to do that right, and it just adds up to a ton of work. But if you can just say, Hey, screw it. I'm going to be like Dan Luu and have a minimally designed blog.

I'm literally not going to have any styles whatsoever. I'm just going to type, and that's an entire set of responsibilities that's no longer in your way. Which means you can put more effort into the content and doing more research and writing really well, and it means you're more likely to actually take this project to completion instead of starting on something and never quite finishing like so many people do.

Because you get lured into this state where you believe every single thing has to be amazing, and you have to do all the things on everybody's checklist everywhere you usually, you don't have to, you have to focus and choose what to ignore and what to focus on.

**Jeremy** It kind of reminds me of browsing hacker news over the years, there's been so many posts on people saying like how I started my blog and you know, it's all about, how they cobbled together like three or four different services and generate their page and how they style it and set everything up.

And it's like. I feel like a lot of people, by the time they've gone through all of that, you know, it could be like, it could be months later, right. Where they may never finish cause they're just like, Oh, I never, never looked quite the way I wanted it to. So I just gave up.

**Courtland** Yeah, totally gave up, was way too hard. And like, honestly, sometimes people do this for fun. Sometimes they just want to learn the newest frameworks or, uh, programming environments or languages and they just want to play around. And when I started, indie hackers, like in my mind, there was no guarantee that I was going to succeed.

And a lot of it was fun for me. Like I made some technical choices that I regret, uh, in hindsight because I just wanted to play around with Ember JS and I wanted to play around with the server side rendering for it. And in hindsight, it wasn't the best choice for a website that scales, but it was what I was really familiar with and what I had fun doing.

And who's to say if I had made a better choice that it would have stuck with it in the end.

**Jeremy** Yeah. So let's kind of go into, I guess a few of those choices to start, one of the things you mentioned is that from the very beginning when indie hackers was just the interview pages basically like a regular blog, you started with a single page application.
 
Is that like a decision that if you were making it now, would you still go that route?

**Courtland** Definitely not. I mean, this was, let's see. It was like the middle of maybe early 2016 when I was making these decisions. Very different JavaScript environment than what we live in today. I mean, Angular was still very relevant. Ember was kind of in its prime. React hadn't quite won yet. In the way that it has now Vue I don't know if it was even on the scene at the time and single page apps are all the rage. That was how you built web applications. 

And for me, I just wanted indie hackers to be incredibly fast and snappy. And once you load it, I just didn't want you to have to spend very much time switching between pages. And to be fair, like for the first few months of indie hackers existence, it was totally fine.

The website loaded almost instantaneously. I was doing some server side rendering. So even the initial load didn't really have any perceptible. Uh, you know, if you open Gmail, this sort of like this blank screen where it's loading and it's firing up all the JavaScript Indie hackers didn't have that because of the server side rendering.

Also search engines could pick up the content. So I felt pretty confident for awhile. Of course, fast forward to today, three, three and a half years later, almost 4 years later and indie hackers is way bigger than it was back then. And there's way more going on. And as you said, there's the interviews and the podcast there's a whole directory of products. There's a meetups feature, there's an article section, there's a newsletters section, there's the forum, which has groups and all sorts of different
views in it. And there's just a ton of JavaScript to load. And so the initial loading time, in my opinion, is way too slow now because you have to load basically every part of the app or none of it.

And yeah, once you're in the website and you navigate around it's fast, but it's not, in my opinion, the right choice for a site like this.

**Jeremy** One of the things that I often hear is people say like, you got to get the time down for first load, right? Like if people have to wait around too long they're just going to bounce cause it takes too long. 

But I wonder in your experience, I don't know if you've monitored how long it takes for people to get to the page and things like that because it seems like even though there is that initial loading time you still have a huge community. You still have a ton of people who are making indie hackers work. And so I wonder from your perspective, how big a difference does it make having that extra couple seconds of loading time?

**Courtland** I mean, the thing is like. I can't really map out the counterfactual. You know, I wish I could go back and build a different world and in that world I did it differently and see, okay, well how many visitors does indie hackers get now? I'm pretty sure the number would be much higher. Just because of research I've seen done, you know, Amazon was calculating something like every 10th of a second of loading speed they shave off the site they sell however million dollars of goods. That's probably true for most other websites on the internet. That being said, It's hard to tell like what people's experiences are. If you're on like a mobile phone on like 3g or something. Your experience using indie hackers is very different than if you're connected to, you know, land line or something in your apartment on your desktop computer.

And so for me, indie hackers loads pretty quick. For most people, it's pretty quick and they don't really care about it. Then there's different browsing habits, habits that contribute. So for example, if you're just browsing around the website, it's usually pretty snappy. If you have a habit of opening things in new tabs, well that means you have to fire up a new tab, which means you have to go to the website from scratch, which means you're going to get the loading screen again, right?

And so if you're in that situation, it's going to be more annoying for you, and you're going to be constantly running into this. So I think it just comes down to sort of, you know, you're a personal way that you browse the website. And for me it's constantly a balancing act. There are times where, I mean there've been weeks where I've done nothing but focused on performance improvements and there are weeks where I figure, you know, I might as well be spending my time on content, are contributing to the forum, are building new features.

And so I usually try to keep an eye on it, keep an eye on complaints, keep an eye on this, the loading speed stats. And if things get too bad, then go back and hit up performance.

**Jeremy** Cause it's like one of the things I remember is that the site used to have where you would first go to the site and it would take long enough where you would show like a quote right? And so you'd read the quote and then take time for the site to load and then it would come up. And then now it's loading fast enough where I guess you don't need to show the quote.

I'm kind of wondering like, is there any way to know like. Are there less people who bounce, you know now that they don't need to see that quote? Or do they miss the quote?

**Courtland** So it's, it's actually, that's a trick I learned from one of my podcast guests, Peldi Guilizzoni who runs a company called balsamiq. But they have kind of a drag and drop tool for mocking up user interfaces. And it just takes a while for their tool to load in your browser. And so what they started doing is they're like well our loading screen is boring. Why don't we put a an inspirational design quote or something on the loading screen. So people have something to do because there's you know there's the actual loading speed but then there's also the perceived loading speeds. And if you can show something of value to people when they show up to your website they might not care that much that you know the main thing hasn't loaded yet. And so they did that and it worked like instantaneously all the complaints they are getting of people saying Hey this tool takes too long to load I don't have six seconds to wait for it to load were now saying, Hey, your your tool loads too fast. I didn't have time to finish reading this quote. Uh, which is kind of the complaint that they wanted.

Like, okay, great. People are now complaining about the other thing. That's fine. So I was like yeah I could do that for indie hackers as well. And so I changed it from server side rendering. To, uh, basically having this load in quote, and I got the exact same complaints, Hey, why is this loading quote disappearing so, so quickly? I randomized it so every time you loaded the site it'd be like one of uh 99 different quotes that came from different indie hackers interviews And there'd be a link to the interview. Um and I've since moved back I reimplemented server side rendering. So now for most pages on the website there just is no quote. It's not that it's loading so fast you don't see the quote. It's that the response comes back from the server just is the appropriate HTML and CSS for the homepage. It's the same if you visit any post on the website. If you open it up there's no quote. So there's certain pages on the site that I pre-render on the server. And then there's other pages on the site that I don't and if you load those up you'll still see the quote. 

**Jeremy** One of the things that I wonder about is when you go to the site like you have a few different data stores I believe right? You've got Firebase and you've got Algolia right? 
 
For those who aren't familiar with those can you explain a little bit about what each one does and what its role is in the site? 

**Courtland** Yeah. So Firebase is basically I mean they brand themselves as a development platform. They're really a database, or at least the feature that I'm using of theirs is the realtime database. It's no different than really any other database other than the fact that it's NoSQL So you kind of determine your own schema of how you're going to store your data and that it's also real time.

So it's pretty easy to make it so your browser can basically listen in on any node in Firebase and see you want to change updates in real time. For example, if you go to indiehackers.com/start It's kind of like a start here page to tell people how to get started. And there's a counter at the top and every time anyone takes one of our actions for how to get started, that counter updates in real time cause we're just watching a node in Firebase that has the number and your browser's just watching it and will update in real time.

So Firebase is just a realtime database. That's where pretty much all the data for indie hackers lives in fact 100% of the data for indie hackers lives inside that database. Algolia is basically a platform for searching. And so if you want to create, let's say, a search engine feature for your website where people can search things, well, that's actually kind of complex, especially if you have lots of content.

If you want to be able to search through or filter search results.  It's basically a database but you need to structure your database in a certain way and have all these indexes to allow for fast searching et cetera. And if you don't want to build that from scratch, you can use Algolia. And so a lot of the data in our Firebase database, we also push into our Algolia indicies and that enables a lot of the different features on the site, but most relevantly sort of our global search. 

So if you've got indie hackers up, up top, there's a search icon and you click that and you can search through any of the posts on the website. And Algolia has features that'll like highlight. The texts that you search for and the search results, and that'll help us, you know filter search results by the most replies and the most upvote or the most relevant et cetera so I don't have to build any of that code from scratch I just plug it into Algolia and let it run.

**Jeremy** So is it basically where there is some integration between Algolia and Firebase where you tell Algolia like I don't know if schema is the right word but this is how the data is laid out in Firebase and then Algolia just kind of figures out how to make the search and indexes work?

**Courtland** Yeah I've got some code that basically watches our Firebase database and automatically let's say you make a post in indie hackers whenever there's a new post in any hackers it pings Algolia with that post information and says, Hey, here's a post to put it in the post index in Algolia. Now the post index in Algolia gets that post Algolia does all its special sauce to make sure that that posts can be searched for and it can be filtered in different ways or shorted in different ways.
And so now when you go to the global search on the website and search for, I don't know how to set up an email marketing campaign or whatever the post is about, it'll show up. So the searches you do on the site actually are pinging the Algolia index whereas when you're just reading the forum you're just looking at directly the data from Firebase.

**Jeremy** So there there isn't like a direct connection between the two You actually wrote some software to to push data into Algolia

**Courtland** Yeah, you have to build that bridge yourself.

**Jeremy** Interesting. The search example I think that probably makes sense to a lot of people. One of the things I'm curious about is when you click on a post I noticed in the network request it's also getting like the posts and a bunch of additional data from Algolia rather than going straight to Firebase. What's the thinking behind that and how do you choose where to pull data from?

**Courtland** So there's some limitations with the Firebase real time database. Um specifically you can only really sort a node by one variable at a time in Firebase. So I can say find posts but sort them by the date that they are created. And that's it. 

Whereas Algolia is extremely versatile in how you can search and sort, you can have numerous sorts and numerous filters at the same time in Algolia. And so when you open a post, one of the things that we do is we show you related posts. We say, Hey, here's more posts from this author, and there's also more related posts on the website. That would be very hard to do in Firebase. I'd have to make lots and lots of different requests. I'd have to pull like tons of posts from the database filter by user, et cetera.

Whereas with Algolia, I can say like, Hey, here's a post. It's made by Dan Luu, find other posts that are from the same author, sort them chronologically, and then also only slice out, filter it to those that have above, you know, 20 up votes. And then those will be the ones who recommended a sidebar. And so, uh, basically the post itself, it just comes from Firebase and the recommended posts comes from a relatively complex query we do to Algolia to find posts that we think are high quality that are from the same user and or about the same topic.

**Jeremy** That's interesting cause it makes it seem like Firebase the querying capabilities are actually really limited If you only get like a single parameter.

**Courtland** Firebase actually I think maybe six to nine months after I built in the hackers came out with a completely different product besides just the real time database which basically replaces the real time database that everybody uses.

And it's a little bit more versatile has a lot more features. But again, it's one of those things where you're like, well, I had already, a ship had already sailed for me I had already made my choice. So it was too late for me.

**Jeremy** That's the kind of thing where when you're using a service from another company you can't always predict what they're going to decide to do.
 
**Courtland** Yeah you can't. But I mean ultimately like Firebase works Even if I was using the newer product cloud firestore I would still have, Algolia and Algolia has its use cases that are still pretty good. And so it's one of those things where like you know I wish they had come out with it earlier but at the same time it's fine.

**Jeremy** And one of the things you're mentioning about Firebase being a realtime database is that where like every user who comes to indie hackers they're opening like a WebSocket connection to Firebase?

**Courtland** Yep. All the data to Firebase is transmitted through a WebSocket connection. So obviously that enables some real time functionality, which I barely make use of on indie hackers, to be honest. Um, but of course there's other advantages to firebase just not, you know not limited to the real time nature of it.

**Jeremy** What's like an example of where you use the real time functionality?

**Courtland** So one of the examples that I gave earlier was this sort of start here page where you can kind of, we've got some counters, in fact, pretty much every example for where I use it, are counters on the site where we're counting different things that are happening. There's only a few pages like that, but I kinda like the idea that on those pages, the site feels alive.

It feels like you're doing things with other people. It's not just sort of a static website. So the start here page, the idea there is that we started, we launched this in January of this year on January 1st and the idea is, Hey, it's a new decade. It's 2020. Uh, let's count how many people start a new project.

Um, so far the number is up to 6,987 and we count you as having started if you do one of any six steps. And so each of those steps, we also have counters set up for people who've done that. For example, 559 people have posted, um, about finding a cofounder. And so, okay, if you're looking for a cofounder, you partner up with somebody that that counts as starting.

And so like, if I look at this page for long enough, I'll see that number tick up every day. Every hour is more people do it. And it kind of gets the sense of this website, or this page in particular isn't just about. You know, getting started yourself, but it's also realizing that this is bigger than you when you can see other people right now doing this thing, and hopefully that inspires you to get started.

So I think a lot of it has to do with just what kind of feeling you want people to have when they're visiting your website. For most of the website, it's totally fine that it's static. Like when I'm on the homepage, I don't necessarily need to see the upvote counts changing in real time. Every time somebody upload something, it's fine.
It's cool just to get a snapshot. That being said, one of the things that indie hackers has really transitioned into since it started uh early on it was just a static blog. You know it never updated unless I updated things. If I made a new post that was it. which meant we were able to take a little bit more advantage of caching.
It was just easier. Whereas now it's a little bit more like a social media website. It's more like a forum where the content is driven by users. I don't know when someone's going to make a post, I don't refresh or change anything in the code. It's all done in the database, which means caching is harder because I don't know when things are going to be uploaded, et cetera.

And you want the homepage to be fresh. I don't want it to be stale, so I don't want you to load the homepage and see a bunch of old upvote counts from the last time our cache was updated two hours ago or a day ago or something. And so I've had to sort of figure out how to get a caching strategy to work so that the website's performant and the home page loads quickly while also being fresh and showing you the most recent upvote counts, which is again, not that easy to do with a single page app.

**Jeremy** Yeah. So like what's been your approach there with caching? How do you decide which things you cache. How do you communicate to your CDN? What does what does that look like for indie hackers?

**Courtland** Yeah it's different depending on the page. So the homepage has its own kind of special treatment. It's by far the most trafficked page on indie hackers. It also has the most sort of independent bits of things that change because there's just upvotes and comment counts at all the different posts you see on the homepage. And so with that we basically have got my server set up which does server side rendering for the single page app. 

The problem with that is if I just let users hit that directly it's really slow. It takes a long time for the Ember app to spin up on the server to generate the HTML and respond. And if a lot of people did that the server would probably fall over. And so I've just got kind of a a script on the server that runs every 15 seconds where the server pings itself It basically hits the server side rendering code generates the app with the most recent upvote counts et cetera. It gets all the HTML et cetera and then it saves a copy of that HTML on the server. And then when any user visits the homepage what they do is they just get served that copy of the HTML. And so the HTML files being updated to every 15 seconds and so essentially every post to the homepage isn't actually hitting a CDN It's going directly to the server which is just serving the static HTML file which is never going to be more than 15 seconds out of date. The reason I set that up it's just because the homepage is so highly trafficked but it needs to be fresh. 

Other pages for example a post on indie hackers I actually don't let your request hit the server. It is cached at the CDN level and essentially what I do is in the same way that I watched the database to see when there's a new post made so I can submit that data to Algolia.

I also watch to see if there's an update to a post or a new comment on a post, and then I'll purge that particular URL from my CDNs cache. And so that way post pages can stay cached for as long as they need to as long as there's no update. But if there is an update I can basically break the cache. The new request will go through and repopulate the cache with the updated version of that page and it'll look fresh and be snappy and fast. 

And then there's some other pages where essentially I don't do any caching whatsoever. These are the cases the pages that show like the loading quote because those are just basically hitting the server and the server in that case is not doing the server side rendering, which is too slow. It's just returning to you the empty HTML file, which has a little bit of JavaScript in there that'll use Ajax to load a random quote basically and show it while the app spins up on your machine.

So there's different strategies for different pages depending on how highly trafficed they are and how often they update. 

**Jeremy** The strategy you were referring to where you go to the homepage and every 15 minutes you're generating this HTML. Is this something that you kind of created yourself or is this something that's built into to Ember?

**Courtland** So yeah it's every 15 seconds. So it's quite a lot of different versions of the homepage. Um it's not built into Ember at all. I mean Ember has the server side rendering but beyond that it's kind of up to you to figure out how to use it. And so by default You know, any request that comes to your server Ember is gonna fire up the server side rendering if you have it configured. 

If you want to do what I did, basically I just have sort of an if branch. So the Ember server-side rendering module is called fastboot and I basically say, okay, if the request is coming from the server itself, then basically fire up fastboot and generate this response and then save the response as an HTML file on the server.

Whereas if the response is coming from anyone else, basically a visitor from the web, then skip fast boot and just go straight to this HTML file that's saved in this location and serve that instead.

**Jeremy** Oh that's so fast boot doesn't have to run every time.

**Courtland** Exactly. Exactly It only runs when the server's sort of regenerating the homepage for itself.

**Jeremy** That's interesting because it's like when I think of server side rendering the server is always rendering for every single person who's visiting the page. Did you find that in terms of just the number of servers you would need that it would just became way too expensive to do it that way rather than try to build up this caching thing yourself?

**Courtland** Yeah so I eventually moved off of AWS. I had Elastic Beanstalk. It was kind of constantly scaling the servers up and down in response to load. It was just a lot to manage. I'm not a super expert at doing that kind of stuff. There are a few times where the site went down. It was on hacker news. Um, I just didn't, I guess elastic beanstalk just hadn't been configured properly or something. It didn't spin up servers fast enough or couldn't spin up enough and it just was too much load. 

There were issues with deploying the code where the code would be deployed to multiple different machines at different times. Different people got different versions of the website.

So I just wanted something that was significantly simpler. So now I'm hosted on render.com. It's super simple. I love their user interface. I only have one server. It's pretty beefy, and I don't really do any sort of auto scaling. And I kind of rely on these caching techniques we've been discussing to make sure the site doesn't go down, and it hasn't a single time since I switched to render and sort of doing things this way. 

**Jeremy**  So like the only thing that's running on an actual machine that's managed by you I guess is basically the infrastructure for the homepage and to render the HTML and provide that to the user.

**Courtland** Yeah pretty much I mean it's the thing is like, it's hard to separate the homepage from any other page because it all lives in the single page app. Instead of, that just depends on what route you visit. You'll get that page, but you're really loading everything. And then it's just kind of at the CDN level.

I intercept some requests for some caching and at the server level later you know determine whether or not to show you the homepage or to let the requests go through and hit the the fast boot server side rendering code.

**Jeremy** And then like all the things that your webpage eventually calls whether it's Algolia or Firebase or I'm not sure what other services you're using. Those are all managed services so you don't actually have to handle any scaling challenges for those.

**Courtland** Yup exactly And all those can be called directly from the front end. So typically if you have a database what will happen is you really don't access the database on the front end you access it from your server because you need the credentials to access it. Whereas Firebase is basically sort of a JavaScript client that comes down and as a user, you authenticate directly with Firebase through that client, and then you're on the front end of the website making requests directly to Firebase for the data that you need. 

And so again I don't really have to do very much on the server side. Once you load the app you've got everything you need to directly request all the data you need.

 **Jeremy** It's always from the browser so that if I'm creating a new post for example I'm not gonna talk to your server running at Render I'm just going to talk directly to Firebase.

So does that mean that within Firebase there's also like permissions in terms of determining where you can create a post or how many you can create that sort of thing?

**Courtland** Exactly. So Firebase handles our authentication. You're authenticated basically directly your indie hackers account is basically a Firebase account. And we've got some permission set up in Firebase. They have a UI for doing this, for saying, okay, which types of accounts can write to which nodes? What can they write?

Can they edit, can they delete, et cetera. So we have this giant file basically that defines all of our security rules and permissions for Firebase and make sure that, you know, you can't go on any hackers and delete somebody else's posts, even if you don't use our user interface with start issuing, you open up the JavaScript console and sort of issuing Firebase commands directly. You'll be rejected if you try to delete someone else's post or update it or or do anything like that.

**Jeremy**  One of the things about indie hackers is it's a social site. You have a lot of user generated content and because of that that means you also have people who may just be bots or maybe just are there to spam. What are ways that you're able to address that problem?

**Courtland** Yeah so there's.. There's a lot spammers who have at various points in time attempted to use indie hackers to their benefit. Probably the most interesting one was one day I woke up and there was like 2000 people on the site in our real time Google analytics traffic, and I was like, Holy crap, what happened?

I noticed they're all hitting one post. And this post was something like, you know, Argentina versus Brazil live-streaming soccer match. And what was happening is there was like some sort of soccer match going on and this spammer knew that this was happening and they hosted some website for live streaming, but their website didn't have any google juice, basically google didn't respect their website, and they knew indie hackers did. 

So they came to indie hackers made a post that just linked to their website. Our posts showed up as number one on Google. Thousands of people across the world were searching for how they could stream the soccer match, hit our posts, click the link, went to that guy's website.

And so that's one of, of many dozens of scams and things that spammers have done on indie hackers. And sometimes it's really hard to figure out why people are doing this. It's not so much bots. The ones that we have issues with today are mostly humans. They're actual people who are making really low quality spam posts on the site.

And we've got like, I don't know, probably many dozens by this point different mechanisms to catch those people, to try to prevent them from signing up in the first place, to filter them out, to prevent them from making posts after they join, to make it really quick and easy for us to delete their posts or shadow ban them or delete their accounts. And it's interesting to see. The way I can tell they're humans and not bots it's cause they tried to get around it. So for example recently we made it so like if you're brand new to the site like you can't really put a link in your post or you definitely can't put multiple links and we'll kind of show you different warnings saying like, Hey, you're brand new. You need acquire more reputation, et cetera. Uh, and the spammers will literally just like change their link. They'll like, try to take out the periods like www, WW without the dot, you know, et cetera. 

And so I've got like all this like regex code to catch that. It's actually very rewarding cause it's much easier for me to, uh, to make these rules than it is for them to sort of bypass them. And, but I get to see all their different attempts to, to try to figure it out. And now a lot of people have resorted to like trying to change their username on the website to a URL since they can't can't make a post with the URL.

Uh so it's kinda like playing whack-a-mole you know just like figure out what I need to do to fix things. They try to figure out a way around it. Um but what's bizarre to me is like no one is clicking these posts. No one like it's not working. I can see how many clicks these links are getting and the answer is zero. So my theory, uh, at this point is like, a lot of these are people working at companies who don't really care, who are literally paid by others to post spam.

A lot of them are, um, in India or Eastern Europe or Indonesia. Where they're probably working for a very small amounts of money just to hit up certain lists of websites and just post the same spam. Um, and I can even see in sort of the refer where a lot of spammers come from, they'll come from websites like openallurls.com where it's just like a text field and they can post a bunch of URLs and click one button and open them all in different tabs one of the many URLs that And so like that's one signal I can use to say, okay, if you're coming from this website, you're almost certainly a spammer.

**Jeremy** Yeah.

**Courtland** there's a lot of stuff like that. A lot that happens on the front end a lot.

**Jeremy** Every time somebody creates an account do you have code that's almost like building a little profile on you know how likely are you to be a spammer?

**Courtland** Yup. Exactly. What are all the different variables that go into this person? This is the person that will certainly spam, or sometimes we can basically just shadow ban you before you do anything and you'll never even know you're shadow banned. You're making posts and no one can see them.

 **Jeremy** How much of your time or you know your team's time do you actually have to spend with uh manual moderation and how much just kind of gets taken care of by all this infrastructure you put together?

**Courtland** So for the longest time I was basically the only person doing any of this. I'm still the only person writing code for indie hackers but now we have the wonderful Rosie Sherry. Who actually was somebody I interviewed early on in the first few months of indie hackers' existence.

She has her own community of software testers called ministry of testing And she joined us as our community manager So the homepage of indie hackers is entirely curated by her. She sees all the different posts. She decides which ones go to the homepage, except for a handful of users who have permission to automatically post to the homepage. Um, and I've also built some internal tools that make it easy for her to review some of the more gray area, questionable spam, or we're not quite sure if this is spam or maybe users have reported something that's not spam but they don't like it and she can make sort of a judgment call. Which has been great because now I don't have to do it. She's excellent at doing it. And the interface that I built for that is pretty easy to repurpose for other things cause it's basically just a list where you go down the list and you click you know yes or no spam or not banned or not banned et cetera et cetera.

**Jeremy** Nice. You're basically the only developer of indie hackers. A few months ago you were talking about bringing on another engineer and going through an interview process for that. What happened with that?

**Courtland** Yeah We decided not to hire another engineer for purely like internal budgeting reasons. Like how are we going to spend our money is this what we need in order to grow.  

Coincidentally we're in this, facing this huge recession that's basically I don't know if it's accurate to say it's already started but it's certainly coming as a result of this coronavirus pandemic. Uh and so maybe this would have had to happen anyway? 

Maybe it was like a good move that I couldn't have foreseen at the time but we just decided not to. Right now I mean if you think about indie hackers' goals our goal is always to become bigger to become more influential to affect more people. And I think you know if you build something that you think is good your directive is always basically to grow, right? 

It's always this balance between making what you're doing better and having it reach more people. And, you know, at the current point in time, I think indie hackers can always get better.

There's so many bugs on the website. There's some performance issues to fix. There's so many features I want to build. That list is inexhaustible. And I spent quite a lot of time last year and the year before just kind of running myself ragged, trying to burn through this list as fast as I possibly could.

But at some point it just becomes incremental, you know, all of these changes are just incremental. Like Facebook has, I don't know how many hundreds or thousands of engineers, but how much better has Facebook really gotten subjectively as a user over the years? At some point, it's kind of just incremental changes and you don't really notice most of them.

So for me, I think mostly what I've been focusing on now is. Less, how can I improve the site and change the nature of it to make it better. And instead, how can I bring this to more people? You know, what's easier? Making indie hackers twice as good or having indie hackers reach twice as many people. And I think I've crossed the threshold where like reaching twice as many people is a more worthwhile goal.
And so a lot of what I spend my time on now isn't even coding. It's just marketing type stuff or strategy type stuff. It's improving the podcasts have better interviews, that get shared more and are more helpful and educational to people. It's doing a better job moderating the forum and having better tools for that.

So I think at some point you know we might bring on more engineers. We might grow the team. but right now it's mostly about finding a really good formula for growing the site in a repeatable way that doesn't plateau, that isn't too slow, and that we can feel sort of comfortable that you know we've got this engine for growth and it's working well.

 **Jeremy** You know when you look at a lot of tech companies usually the goal is to grow and grow and grow And you look at so many companies that have huge engineering staffs and it's really interesting you know to see you kind of go in the other direction and take a look at kind of what you have now and say like is the important thing to make my product better? Or is the more important thing is to improve the content you know increase the number of people who are there it's like a very different way of looking at it.

**Courtland** I think that balance is always there. It's just it, depending on the amount of resources at your disposal, sometimes you don't have the ability to do both at the same time. Or do you have to switch between one and the other? And if you're an indie hacker, if you're a solo founder and maybe you're a team of two or three, just working on something ambitious. You really have to focus and you have to be realistic about how much time you have to spend on any given task. 

Because if you try to do everything, what's gonna happen is you're just going to do everything poorly. You know, if I try to do, you know, like the best podcast in the world and also like the best website in the world, and also like grow really fast and also like the best forum and like, I'm just gonna have like a mediocre version of all of that.

And so what I've had to do is really focus on one at a time. And try to implement sort of permanent infrastructural improvements to have it so that the improvements I make to any of those cases last and they're permanent before I move on to something else. And so for us right now, you know, when you think about growing a website, you really want to create, you know, what I will call a machine for growth, a repeatable process for why your website is going to keep growing and why more growth will feel more growth in the future.

And once you have that in place, um, some would call it product market fit, but I'm not sure that's the best, the most accurate way to describe it. But once you have that in place. You kinda got to keep fueling it, but you can then focus on other things. And I think it doesn't quite make sense to scale up your team before you find that because having more people doesn't really help you find that faster.

In fact, it probably, it probably hurts and it probably makes your communication overhead way higher and it's harder to strategize and execute on plans and you have more people. But once you know what's working and you know exactly what you need to do, I think that's when you want to scale up. So companies like Facebook, you know, they found their mechanism for growth years and years ago, and they had more than enough funding to do lots of things at the same time.

Whereas with indie hackers, I've been sort of successively growing the platform, hitting a plateau, figuring it out, growing it again, hitting a plateau, figuring it out. And so now I'm at a place where it's like, okay, well it's plateaued at a point. That's great. You know, it's seven or eight times bigger than it was just a few years ago.
But also. You know, what's the next mechanism and can I come up with a mechanism where the community is really powering the growth of the website rather than me having to invest manual effort constantly every six months or 12 months to figure out what the next way is to push past the current plateau.

**Jeremy** I really liked the idea of what you're saying, where, you know, you're starting at just by yourself and you're finding out where are these walls I'm hitting where it's like, You know, Hey, I need help with managing the community, so, you know, I'm going to bring in Rosie or  I'm spending time, you know, every week, editing my podcast and there's other things that I could be doing that are kind of more specific to my skills. So I'll bring in Bradley, right? Who's editing your podcasts.

**Courtland** Yeah, he's been editing since like the fourth episode. He just repeatedly emailed me and said, Hey, like I could edit your podcast, and I was telling him, Hey, no, I got it. I want to learn how to do it. Back in those days, I had the time cause I was doing many fewer things and he sorta won me over. He proved that he could do a better job at editing than I ever could.

And it saved me countless hours since then. So yeah, being able to hire and outsource jobs to people who are really good and really motivated to do good work there is, is a lifesaver.

 **Jeremy** One of the things that's interesting too about indie hackers is that, you got acquired by Stripe, I believe. Was it about a year ago or how long has it been?

**Courtland** Three years ago.

**Jeremy** Three years ago. Oh my gosh. 

And the way that you kind of describe. the way that you're growing, it really matches with what somebody might think of in terms of somebody who is an indie hacker, who is a bootstrapper, who is gradually figuring out, okay, what's the next step? Who can I hire next to, to help me out? And yet, you have this giant company that has so many engineers, so many people, involved with it. 

Do you lean on them in order to get any engineering advice or product advice or kind of, what's the relationship between you and Stripe?

**Courtland** Yes. Stripe and I have a, I mean, Stripe owns indie hackers. Just to be clear, indie hackers is part of Stripe. They bought indie hackers, the whole kit and caboodle, all of it is part of Stripe. 

That being said, the way we operate inside of Stripe is very independent. I generally report to the CEO every few months or so. He sort of checks in on what I'm doing. Uh, all of Stripe's resources are available to me. If I wanted to go to the design team, I could say, Hey, I need this design. And they would definitely help out. If we want to go to the marketing team, it can say, Hey, I'm trying to figure this out, and they would help out.

But for the most part, I really don't. I mostly run indie hackers independently kind of the same way I ran it before. We have a budget within Stripe to sort of run the site and grow it with a goal of, of again, like balancing these two variables.

How good can indie hackers be? How effective can it be at getting people to start new companies and helping those companies succeed, but also how many people can it reach and sort of multiplying those two variables together to get the biggest numbers possible. I think it's, it's interesting in a way that, I would almost compare indie hackers to a high growth startup where we're not making money.

It's no longer a goal to like, you know, generate revenue. Before I joined Stripe, I was making about seven, $8,000 a month at the site. Since I joined Stripe, we got rid of all the ads, all the sponsors, all the affiliate links, everything we were doing to make money. And it just makes $0 dollars it just purely burns cash.

But it has this positive impact on the people who come by it. And I think a resulting positive impact on Stripe because a lot of the people who start these companies will end up becoming Stripe customers at some point in the future. So my mandate now is basically to grow and to have an impact on the world and not really worry about revenue.

And in that way, I'm much more like a funded startup than I am like a bootstrapper who's got to figure out how to pay the bills and generate revenue in order to survive.

 **Jeremy** When you're talking about like having a budget for indie hackers, if you were to say, go to someone at Stripe and ask for some design advice or ask the infrastructure team to host indie hackers, like would that go into your budget or would that be kind of like, you know, "free"?

**Courtland** Yeah, that'd be free. I mean, no one would really, I mean, that's kind of a personal sort of thing that I would do. Um, and the design team at Stripe, like I respect them. Immensely. I looked up to them for so many years before I ever joined Stripe, so it's super cool to be able to work with them. And I've talked to a few people and they've given me lots of pointers about how I could design the site better and prove different things, but it's not part of like our budget, our budget is more so just like the money that we spend, how we are able to hire people like Bradley and Rosie to help out with indie hackers, uh, my own salary, my brother's, et cetera.

 **Jeremy** You know, when you were talking about hosting, you used to host on AWS and then you moved to render. Did you ever consider, pushing off the responsibility of that onto, you know, a team at Stripe or on the Stripe infrastructure?

**Courtland** No, because I think one of the easiest and best things about being independent is you move fast. You know, there's a reason why when I joined Stripe, I wasn't like, how do we get a ton of engineers onto this? And you know, mix indie hackers into the Stripe infrastructure. Stripe was a very mature company compared to indie hackers, and the hackers at the time was literally just me. Stripe at the time that I joined was over 600 people. And when you have organizations of that different size, you execute at different speeds like Stripe, and also has different responsibilities. For example, indie hackers is not managing anybody's money. We're not a tool that's powering businesses. We're not like crucial infrastructure for the web.

Stripe is. And so there are all sorts of checks and balances and security protocols and procedures that Stripe needs to adhere to. That quite frankly, would just be a complete waste of time for me to worry about with indie hackers. Uh, and so, you know, the strategy isn't so much how do I mix in with Stripe and use all their resources, et cetera.

It's the exact opposite. How do I stay as independent as possible? How do I retain my ability to move quickly and be agile and make decisions on the fly, um, despite being part of Stripe? And I think that's, you know, been one of the biggest successes with any hackers so far is that there hasn't been any sort of negative effect of, uh, you know, a slowing down of indie hackers or a compromising of indie hackers values because, , of joining Stripe and vice versa, there's never, never really been any sort of negative effect in terms of Stripe where, uh, indie hackers has exposed them to risk et cetera, as being, you know, part of the company. We've been able to sort of keep things independent despite being the same. and I've been able to sort of rely on my advantages there that I'd had before joining Stripe without losing them. And I think I've seen a lot of other acquisitions where that's not been the case.

There's been too much of an obsession with how do we combine these two things, you know, how do we get synergy? And I think it's much harder to get those kinds of synergistic things going than people think. Because there's usually costs, there's lots of unforeseen costs. That are hard to predict. And we've done a pretty good job of avoiding those, although I do think we could do a little bit better job taking advantage. You know, I, I probably should rely on the Stripe design team a little bit more. I'd probably should rely on marketing a little bit more, but so far so good.

**Jeremy** You were talking about how a lot of acquisitions don't go quite the way people expect and that reminds me of, one example I can think of is there was a pair programming application called Screenhero and they got bought by Slack and you know, Slack is the text chat that businesses all over use.

So it seems like it would make a lot of sense to like, okay, let's bring this screen sharing application, this pair programming application, put it into Slack. It's going to be great. but my understanding is what happened is they got brought into Slack and then Slack has this massive code base, right?

And they're trying to slot this custom application they built, into Slack, but these code bases they're completely different. And so trying to get their product that worked into this existing code base that has so many other features and the stakes are so much higher they ended up not being able to make it work. And, I think that's a good reminder that like even things that like makes sense on surface when you actually try and do it, then there's actually a pretty good reason why things don't work out the way you expect.

**Courtland** And there's just so many different ways for partnerships and acquisitions to happen. I've talked to dozens of founders whose companies have gotten acquired or they've been through that process since I joined Stripe and just founders are looking for advice or how do I navigate this? What was it like for you, et cetera.

And as far as I can tell, they're all different. They're all so unique. And there's some, you know, general principles that sort of, um, you know, you can sort of zoom out and apply it to lots of different situations. But you know, they know in that particular example, like that was a very technical integration they wanted to pull off. It really depended on the code base as being workable or compatible in some way. And you know, maybe there's some diligence that either side could have done before that acquisition to figure out if this is viable or maybe they just had to try it, you know, and see if it would work or not. Or maybe different people could have made it work.
You know, it's impossible to say from the outside looking in, but with indie hackers and Stripe. There's absolutely no reason to combine the code basis. There's no advantage. There's no point. Indie hackers is not part of the Stripe core product. It's a different brand. It's a different website. Uh, and that's worked to our advantage.

**Jeremy** And so like, how many years have you been running indie hackers? Like when did you first start?

**Courtland** I started it in July of 2016 so about four years now.

**Jeremy** And looking, you know, over those four years, you know, was there a specific time or a specific thing you were working on where like, that was the most fun period for you?

**Courtland** Hmm. You know, there's a, it's always fun when things are going well. It's always fun when the site is growing. Whenever there's a lot of traffic coming in, uh, whenever I see people getting the most out of the site I think that's the most fun stuff. 

And I also think change is the most fun whenever I'm doing different things.
And so when I first started the podcast, I thought that was super fun cause it was new to me and I didn't think I would like having a podcast. And at times I don't, but at times I love it. And when I first started it, that was great. Um, recently I've really loved the podcast. I've gone to have a lot of interesting, fascinating conversations with different people and really just indulge in it.

Um, where there've been other times, for example, where I've really been focused on the website. And I really haven't been able to put as much time or thought into the podcast as I possibly could. And then I didn't feel great releasing like, you know, episodes that I didn't think were top notch and so were sort of a drag, but that was excited about other things.

The indie hackers meetups have been a tremendous source of excitement for me for the last year and a half. We didn't have meetups when any hackers first started. And then around July of 2018 I believe we had like our first sort of official meetup where this is an indie hackers sanctioned meetup, and it was in San Francisco.
And since then, we've had, literally thousands of groups of people all over the world and hundreds of countries who've gotten together for no other reason that they're all indie hackers and they want to talk to each other and meet each other. 

And I can basically fly to any country, put up a little notice on the  website, like, Hey, let's do a meet up or join the meetup that's already there and get to meet a whole bunch of people who speak my language and have the same interests and who like each other. Um, so now, like whenever I travel anywhere, that's the first thing I do is I figure out what's going on with the indie hackers meetups in the area. And that's super fun. And I'm not sure that'll ever get old. Basically means I can go anywhere and make friends instantly.

Uh, and I think it's not just me. Anyone can do that. Anybody can go to indiehackers.com. Look at the meetups on the home page, start their own meetup. It can be anything from like. Hey, you know, I want to get coffee. Does anyone want to come work at this coffee shop with me too? Like, Hey, let's have speakers come in and rent out a space and do presentations. I've been to two person meetups. I've been to 150 person meetups. So I think that's been a super exciting thing. 

Moving the forum to the homepage was very exciting for me too, because the initial vision for indie hackers was really just to be this blog, and now it's much more of a social living, breathing community.

And there's a very definite point in time where, you know, there was a before and after, there was the forum on some back page where it was kind of hard to find and only a few people were on it to the point where the forum became the homepage. And it's the main feature of indie hackers. And it's the main thing that people sort of visit and read when they come to the site.

And also, you know, I recorded a podcast episode with my, one of my best friends, Lynne Tye, and we did a couple takes in my apartment. And we got it really good  and her episode is, I think the second most popular episode of the podcast. People loved it. They could tell that we were friends and she had just such a great story and so it was super fun watching her business grow as indie hackers was growing and then get to sort of combine forces and do a podcast episode. That went really well.

**Jeremy** And it seems like, you know, one of the big things is really just building this community, right? Interacting with people, having people that are in the same situation as you who are into the same things as you. Um, which is always a good time. 

One of the other things I wanted to ask is you know, throughout this period, is there anything that was like a slog or was like a thing that you really didn't want to work on or didn't really feel, but you had to do it anyways.

**Courtland** Oh, tons of stuff. That's entrepreneurship. I mean, just chronologically, the very beginning, trying to get those first interviews when nobody knew who I was and they're like, why is this random guy emailing me, asking me to share my revenue numbers and my business strategy? I mean, that was like one yes for every like 15 emails, lots of nos, lots of who are you?

Lots of ignored emails and like, you know, I don't care who you are. It's probably not fun. Sending lots of personalized cold emails to everybody. So that was just like literally a slog. and that continued for a while actually. I mean, even after the site launched, I started getting lots of inbound requests, but I always had this background anxiety that the requests were going to run out, that I wasn't gonna be able to find enough people.

Back then, I was publishing sometimes five or six new interviews a week. I calmed down on that and sort of doing fewer, uh, cause people couldn't even read that many. But, um, that was a huge slog starting the podcast for, for kind of similar reasons. I wasn't very confident that I could be a good podcast host.

I was afraid of how I would sound. I didn't like the sound of my own voice. Uh, it just seemed like so much work just to get a single episode out compared to, you know, doing an interview over email was a slog for quite a while until I launched the podcast. I think I started working on it in November of 2016 it didn't launch until March of the next year just to get three episodes out because there was so much work for me.

Other than that, I, I think it's been, you know, mostly good. There's always paperwork and there's always like administrative stuff and taxes and accounting and that kind of stuff is never fun. Um. You know, fighting spam. Uh, it's fun once you have the tools in place and you can fight effectively, but before you do, it's constant.
It's constant fear someone's just going to win and destroy your website. So, uh, you know that wasn't fun either.

**Jeremy** And like, as people come to the site and you make changes over the years, like there's going to be things that they like and things they don't like. you know, one of the examples I can think of is. When you first started with the interviews, people came for the interviews, they loved the numbers, they love hearing people's stories, and then they kind of got deemphasized like they kind of got hidden a little bit. And I know a lot of people freaked out. How do you listen to feedback and figure out what to listen to versus, you know, what, what's kind of more just noise?

**Courtland** Yeah. I mean, listening to your users, no matter what you're doing is extremely important because those are the people who use our app. 
Those are the people who you're, you're trying to serve, right? If you're not doing things that make them happy, you're doing it wrong. But at the same time, your users aren't strategists. They're not tacticians. They're not. I mean in my case, they literally are founders. So, uh, they actually do have a lot of good, you know, strategic advice. But no one really knows what your goals are to the degree that you do. And so you always have to sort of take user feedback and filter it through a lens of, okay, what am I trying to accomplish here? And does this help me get there? 

With the interviews, for example, I think people will tend to be resistant to change. "You know, the interviews aren't on the homepage anymore." "Indie hackers is changing and bring back the old indie hackers." But at the same time, we're still doing just as many interviews as we've done in the past now requires one extra click to get there. Or you could just bookmark the interviews page and be straight there. The interviews, newsletters, the same as it's always been. 

So ultimately like, the sort of initial pushback you might have when you make a change sometimes just fades. I don't think I've gotten a single complaint about the interviews being deemphasized in years.

So, uh, I think a lot of it just comes down to realizing, you know, what you can ignore. And what you can list, what you should listen to and for the advice you do listen to, like how do you listen to you? Do you just literally do what everybody is saying? Well, that doesn't work because you're going to have people saying contradictory things.
And even if everybody's in unison saying the same thing, like, is that really the best advice for you? Um, with the interviews in particular, you know, it's, it's an interesting phenomenon because they're very helpful in two ways. They're helpful for people who are just getting started and they're not really sure how to navigate this landscape of.

Basically, what is it like to be an indie hacker? How do I get started? And they can just browse through the interviews, read the new ones, and get like a really good snapshot of all of these different perspectives and hopefully find a couple that resonate with them. But here's the thing, like, people eventually graduate from reading the interviews. Nobody that I've ever met has sat down and read every single interview from the beginning to the end, all 450.

After 20-30 interviews, you kind of get it and you're like, that's fine right? Which means it's kind of hard to rely on the interviews. Purely for growth because it has literally 100% churn. Eventually everybody graduates and moves on. 

So, um, you know, that's one of the underlying factors that like you'll consider as a person creating your website, that reader is, well, they'll just think, Hey, I'm in this phase where I love these interviews. I want to keep reading, et cetera. But they're not thinking ahead to like, well, am I always going to love the interviews? And like what are the implications for the site and its ability to help people and solve problems as a whole? If like this is on the homepage, you have to put that kind of thought in because your users aren't going to.

**Jeremy** You, you listen to them, but then you have to put it into the context of, you know, the strategy you have and the plan you have to see if it makes sense. What do you think is the difference between, the interviews, I totally agree with you where  after a certain point it's not going to provide value to them maybe. But I feel like the podcast is very different, I feel like there probably are people who have listened from the very start and have gone to the very end. What do you think is different between those two things?

**Courtland** Several differences. Number one, the podcast is more passive, just because the format is audio. All you really need the willpower to do is press play. And then guess what? It's playing. And now you just have to, you actually take some action. You have to put an effort to stop it from playing. You have to press pause.
And so people sort of work this into their life as sort of a matter of habit. You know, when I'm cooking, I press play on the podcast. When I'm walking to work or driving to work, I press play on the podcast. But the interviews, you literally have to sit down, open your email, click the link, and then power through every sentence you read is more conscious effort.

Um, and so if you're getting diminishing returns from what you're reading, if you're getting diminishing returns from what you're hearing, cause you've already read it before. It just at some point, the equation doesn't balance out and you no longer feel like it's worth the effort you're putting in. You know, you'll look at something else.
The other thing is I think the podcast is a little bit more novel. And so what I tell a lot of founders is no matter what you're doing, whether or not you're putting out a podcast, you're doing interviews, you're building a web application or a mobile app. 

Basically, you should think of yourself as solving a problem for people. And everything about your business is going to be determined by the properties of that problem. How many people have that problem will constrain how big you can grow, how frequently people have that problem, will constrain how frequently they use your app or your website or your podcast or whatever, how fast that problem is growing will constrain how fast you're able to grow and so on and so forth.

It's like 15 or 16 different properties of any problem you're solving that dictate sort of what you do to solve it and how people are going to react to what you do. And I think one of the things that the podcast solves for people is this kind of ever-present desire to know what's new, what's going on, what's happening in the world.

The interviews on the website don't quite solve that. They solve a subtly different problem, which is like, how do I get started? You know, what does it look like to be an indie hacker? Um, a good analogy would be like going to school. If you go to school to get a degree in computer science, your problem is that you don't have a degree in computer science and you want to learn how to code.

But at some point, you get the degree and you learn, and now the problem is solved and like you're not going to keep going to school like you've solved the problem. It's, it's over. Um, whereas if you want to know what's new in the world, maybe you're going to read hacker news or you're subscribed to the New York times or you browse Twitter, but you're never going to stop wanting to know what's new in the world. You'll probably want to know what's new in the world until the day that you die. And so you won't graduate from these platforms. You won't churn. Um, because they're solving a very different problem. That itself doesn't really have an end date. 

So I think the podcast is kind of similar. If you look, look at why people listen.
Uh, I would guess that the people who listen because they want to learn what it's like to be an indie hacker are much more likely to churn as listeners and the people who are listening because they want to know what's new, what's the latest and greatest, and what are people working on now.

**Jeremy** I would also say too, is that when I listened to a podcast, it feels a lot more personal as well, right? Because we get to hear you, we get to hear your guests, and you know, there's this storytelling process. it's a form of entertainment, right? Like beyond just, what's the advice that's being shared.

**Courtland** Yeah. I think about this as the forum as well. Right? Entertainment is something that like . Generally speaking, you're never going to not want, you know, you're never going to come at you and your life and be like, you know what? I've got all the fun I've ever needed to have in my entire life and I'm done done.

**Jeremy** That's enough.

**Courtland** Yeah. It never, it's when it's one of those perennial problems that never ends as does. Wanting to know what's new, as does, needing to eat, et cetera, et cetera. Do you need to do your taxes? So, you know, I think the forum right now is a little bit too educational. It's a little bit too ad hoc, you know, help me solve this problem or post your own problem and not quite as entertaining and quite as, as.
Newsworthy is it could be to sort of facilitate the perennial browsing habits. And I also think a lot about, you know, the sort of competing forms of behavior, you know, if someone's not reading indie hackers, what are they doing right now? 

Um, you know, we've seen like sort of a dip in traffic and the different traffic has been caused by people reading about the coronavirus in other words, the problem that they were solving by reading indie hackers has now been supplanted with the solution of reading about the coronavirus.

And for those people, a lot of it had to do with like what's going on in the world. Like, you know, what's happening. And their priority is switched to this much bigger flashier problem with the coronavirus. And so I've been thinking a lot about, well, you know, if that's competing with us or if people are looking at Instagram instead, or people are looking at Facebook instead, you know, in my opinion, indie hackers is a more helpful website.

It's a more beneficial to you. It kind of helps you change your life for the better. It's more proactive than watching people post modeling photos on Instagram. Um, or, or reading about the coronavirus that you really can't contribute to. And so a lot of it has to do with, well, you know, what can I do to develop a longer lasting habit, even if that is being more entertaining and more newsworthy. If it's also in the context of you learning other things about starting your own business, then it's more productive than Instagram in the end. And that's sort of, it.

 **Jeremy** It'd be really great if you could get to the point where you know, it's very clear that looking at Instagram or looking at tik tok or whatever is very addicting and it's very entertaining. Um, but being able to capture some of that while educating, you know, like with indie hackers, I think that'd be, that'd be awesome.

I think it's a good place to to start wrapping up but is there anything you wanted to mention or you think I should have asked?

**Courtland** I mean I think my message for people listening is if you're technical which I assume you are if you're listening to this podcast if you're developer you can start a business. You already have all the skills learning how to code, learning how to build things. That's the hardest skill to acquire. Learning how to talk to people how to market what you're doing and find an audience is not easy to do but you 100% can learn how to do that pretty quickly just by trying. And so I would encourage you to try building and releasing something to the world. Go on indie hackers, check out the podcast. It's a very easy way to listen to how other developers are doing this.

Start small with something really simple. That's doable. Don't try to work on your most ambitious plan all up front. It's very hard to do that. But if you start something really simple, put it out. See if you can make a few dollars. And eventually build a path for yourself to basically become financially independent.

I think it's a worthwhile endeavor, and I'm pretty sure the future we're moving to is one where many millions of people are living the sort of lifestyle where they work for themselves wherever they want, whenever they want, on whatever they want. And I think developers are better positioned to start doing this than anybody else.

**Jeremy** It's really exciting to to be a developer just because we we have so much power in terms of what we're able to create you know by ourselves or with tools online or just being able to connect with people online. Like there's so many things that we can do that are super difficult if you need to to build like a physical product or get something manufactured where you need so much more money you need so many more connections and so on and so forth. Whereas for software it's go and build it and you learn how to market it and sell it and maybe you can make a living out of it.

If people want to follow you Courtland where should they check you out?

**Courtland** I am on Twitter twitter.com/csallen I'm also on indie hackers indiehackers.com/csallen and I again I highly recommend checking out the podcast that's at indiehackers.com/podcast  

**Jeremy** Awesome. Well Courtland thank you so much for joining me today  

I hope you enjoyed the chat with Courtland. You can get the transcript for this episode at softwaresessions.com. All right. See ya.

</div>