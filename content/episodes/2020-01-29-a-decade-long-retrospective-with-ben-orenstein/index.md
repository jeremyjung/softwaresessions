+++
title = "A decade long retrospective with Ben Orenstein"

description = "Ben Orenstein reflects on a decade of programming, teaching, conference speaking, and his latest role as the CEO of Tuple."

[extra]
episode_url = "https://media.transistor.fm/d13ee068.mp3"
+++

Ben is the CEO of [Tuple](https://www.tuple.app), a pair programming application for remote developers.

He currently co-hosts [The Art of Product](https://artofproductpodcast.com/) with Derrick Reimer.

We talk about:
- His first crazy programming job
- Why you should speak at conferences
- The trade-offs of remote work
- Why great coworkers should be the #1 priority for new developers 
- How these are "the good old days" of Tuple
- Ben's favorite smash bros character
- ...and much more!

### Ben Orenstein
- [Personal Site](https://www.benorenstein.com/)
- [@r00k](https://twitter.com/r00k)

### Podcasts
- [The Art of Product](https://artofproductpodcast.com/)
- [Giant Robots](https://giantrobots.fm/) (Ben hosted this podcast until episode 240)

### Other Links
- [Tuple](https://www.tuple.app) (Remote pair programming application)
- [Refactoring Rails](https://www.refactoringrails.io/) (Ben's video course)
- [How to talk to developers](https://www.youtube.com/watch?v=l9JXH7JPjR4) (Fantastic talk for anyone giving presentations)
- [Upcase](https://www.upcase.com/) (Rails, vim, and tmux video tutorials. Previously run by Ben while he was at thoughtbot.)

---

### Transcript

This is a lightly edited machine transcription.  You can help me edit it at [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy** Today I'm joined by Ben Orenstein, the CEO of Tuple, a pair programming application for remote developers. He also previously worked at the thoughtbot software consultancy and has a lot of conference speaking and developer education experience. Ben, I wanted to talk to you about your career going from programmer to CEO of a company and software development in general over the last 10 years. So thank you for joining me.

**Ben** Yeah, my pleasure. And I have to say it's, it's kind of weird to have someone talk about my career as like this long thing, or like I've been in the industry long enough to see like these macro changes happening. Uh, it's, it's weird getting old enough where that is possible.

**Jeremy**  That means that we're both still healthy enough for that to happen right?

**Ben** Yes. No, it's, it's a privilege, if anything.

**Jeremy**  the first thing I'd like to start with is just some trends of the last decade and you can kind of go into what your opinion is on it or if you have any other kind of thoughts to add on to that 

**Ben** Okay.

**Jeremy** So the first one I would like to ask is there is  kind of this trend of people going, I need to be a full stack developer. And so what's your opinion on, you know, specializing on one thing, like being really good at backend versus being really good at front end versus this whole concept of full stack.

**Ben** I think the good news there is that it kind of doesn't matter. And so if you really enjoy working across the different boundaries, then that is something that some places will be totally into and want to recruit you. And if you want to get hyper focused, and because you just are like nuts for Postgres, you can totally find work doing that too. I suspect it's getting harder and harder to really be fullstack as the, each layer gets kind of more complicated. Um, but it's nice that you can sort of make either work.

**Jeremy** And how about you know, I know your background is in working in Ruby, um, but kind of lately there's been a lot of talk about, uh, adding static type checking to Ruby and sort of this conversation between, is it better for a language to be dynamic versus static? what are your, your thoughts on that?

**Ben** I think, at the end of the day, there's no way that brains are going to get way better at helping us make correct programs. So we might be able to write programming languages that make it slightly easier for our brains to effectively hold lots of things in our head or to catch errors and things like that.

But I think eventually there's just no way where computers aren't better at checking these things and paying attention to these sort of things. And so today's dynamic and today's static languages, it still feels like the pros and cons are kind of equal ish. So I think you can basically, you know, there's, there's nice things about static languages and there's nice things about dynamic languages and it's not clear to me that anyone has one

exactly. Uh, and it's, it would be a reasonable choice to pick either, I think, um, particularly based on what you're trying to do. But I think over the long term, uh, outsourcing the thinking and the checking and the correctness to a computer feels like it has to be the future.

**Jeremy** Mm. So that kind of ties into a question in terms of,  how do you know when you should stick with what you know versus, okay, it's time to jump on to a new language or a new stack.

**Ben** Um, I think that can kind of just be a personal decision actually. And so you can kind of, again, because we're fortunate enough to be in a world where there's a lot of demand, you can kind of do what makes you happy. So you could still write COBOL full time. And make a lot of money cause there's so few COBOL programmers and so much COBOL code.

So if you want it to like not update your tech stack from what it was in the 70s or whenever, that was a thing that's totally still like feasible as a career path. And so if you just decide that Ruby is the last language you want to learn, you can, that is, that will totally work. I'm convinced you can make it to retirement, uh, without having to pick up a new language cause there'll be so much Ruby to, to maintain.

and, and it would be also fine to write new Ruby. Uh, but my, my guess is that. most people would be somewhat bored by that. And I think they also will be well-served. Like if you are, if you're staying up to date and learning new things and pushing yourself, I think that can lead to a lot of positive professional growth.

And if your target company is something more startupy, the latest stuff is more likely to be in use so that you probably want to move yourself in that direction. But if you don't care about that and then you can kind of not worry about it. Like I, for example, I, I basically don't know Javascript.

Like, I get that it's a thing. I know it's important. I know how widespread it is. I almost can't write a line of JavaScript and it turns out I've had a pretty decent development career without that. And so if I want it to go, there's, it keeps you from doing certain things, but, uh, I've been able to more or less ignore it because I don't really want to learn it.

And it's been fine. It turns out.

**Jeremy** And  you've been ignoring JavaScript, but in terms of the backend, are you at the point where you're thinking to yourself, okay, if I was going to start coding again, um, I would write it in another language.

**Ben** Mmm. when I think about doing side personally, I am still writing some code. Not a ton, but some and it's, it's all Ruby right now.  I am tempted by other languages and frameworks quite a bit. Um, I think clojure is beautiful. It's like one of the best design languages that I'm aware of. Um, I would love to write like a substantial thing in clojure.

Uh, but whenever I have a sort of new side project idea and like, okay, do I want to maximize the chances that I actually ship this thing or do I want to use it as a learning opportunity for a new technology? And I find that pretty much every time I do the technology thing, I don't really get very far.

And so I think if I'm going to pick up a new, like a large new tech stack at this point, it's going to have to be a really concerted effort. Like I'd probably need to like book a house somewhere and just like, all right, for this next, and this, this is the thing I've done in the past, um, with, with a friend or a couple of friends is like, all right, we want to learn.

This thing, let's, let's just go do this and nothing, nothing but this for like a week straight to kind of get our feet wet.

**Jeremy** how about When you're building, you're designing an application. Um, you know, over the last decade, there's kind of been this back and forth between, um, you know, we started with monoliths, then we kind of went to a service oriented architecture. Then now people were talking about microservices and now people are going back to monoliths and it's kind of like, where do you sort of lie on that spectrum of like, how should people decide what they should do?

**Ben** Um, it would be hard to give prescriptive advice for the entire world, uh, based on no context. Um, I will say that I think it's a pretty reasonable strategy to start with a monolith and then later refactor to other services if you find that the, Pros and cons work out in your favor substantially.  there's a lot of simplicity to be gained by having all your code in one place and you're sacrificing quite a bit of that to go to any sort of external services, uh, particularly microservices.

And so I think it's just important to go into it with your eyes open and, and, and understand the pros and the cons. And I think actually that's like my meta answer or like my higher level answer for basically everything in, in software development is. That pretty much every approach is a particular set of pros and cons to it.

And so the trick is understanding what those are and matching the choices to your situation.

**Jeremy** kind of similar to that. When you're deciding whether to use something like say AWS directly or use a service on top of that, like say Heroku or now or something like that, what are kind of the different, I guess, decision points or criteria you're looking at?

**Ben** Well for me, I've basically been a Heroku convert since I discovered it like eight years ago or something. Um, and it's because for me, the, the, the part of the stack that I like focusing on is like application level and, and messing around with servers and SSH into things is just not my particular cup of tea.

And so I'm, I'm happy to, to pick that the trade offs that those services involve, but like, it's. It's not the same for everyone. And we're now, we're not quite there. Um, but we are now paying more to Heroku then, you know, would be ideal in a perfect world. Um, like we have at least a four figure Heroku bill now.

And so it's like, okay, I can start to see why people, you know, use more of their own things. Eventually, like you start to say, okay, maybe we can manage this ourselves at the, and the trade offs start to make sense as the price gets high enough.

**Jeremy**  you know, with tuple, um, you said you're using Heroku and you've got a pretty high bill and whatnot.  Um, how about. SAAS services, like for example, there are services for, customer chat or for authentication or for databases, like for example, Firebase or Auth0, that sort of thing.

Um, sort of what are the things you look at kind of, you know, as the CEO of the company when you're deciding, okay, we should just kind of build it ourselves, or we should use one of these, these services.

**Ben** um, I don't know that I have a general rule. I think I tend to choose to use someone else's thing rather than build ourselves. I've seen, um. How quickly a, Oh, we can build a simple version in, you know, two days. I've experienced the reality of coming back to that simple version over and over and over and over again and pouring more and more work into it and ending up with something that's like, you know, 60% as good as if we'd paid for someone who specializes in it.

So my default is probably to try to use something that someone else is going to build and maintain. And, and that's true for like, you know, open source requirement, like dependencies and other paid services. Um, but. Every so often you really just do need the simple version and you actually can get by and it's kind of hard to predict when that's true.

So I don't know that I have a great rule for that.

**Jeremy** Yeah, I mean, specifically with Tuple, I believe, I remember hearing that, you know, you wrote your own authentication, or rather you use the devise gem, which is kind of like a rails, um, library for authentication. So I'm kind of wondering is, you know, are there certain things like for example, authentication or managing your users where you would say like, this is kind of the type of thing that I would prefer to keep, you know, within my own app?

**Ben**   Uh, authentication, I think of using device as like, not writing our own authentication. It's pretty much, it's someone else's code to me. Um, and like for, for sure, especially around like password hashing and things like that, like, I don't want to go anywhere near any of that. Um. I'm not even, I can't, I'm having trouble.

We had, like, we wrote our own user management stuff, but it's, you know, it's pretty simple and there's always this layer you have to write. So we use Stripe for, for billing, but there's always a sort of intermediate level of like, okay, well you still need to have some stuff locally and kind of sync it back to Stripe and handle failures in this way and all this.

Um, so we ended up writing some of our own billing code. Uh, but for the most part, we're actually, we've been relying pretty heavily on external things and, and pushing dependencies away from us. Like we're trying to be really good at making a great remote pair programming app and not great at the rest of it and letting other people that are good handle those things.

**Jeremy** For sure. Just because the remote pair programming aspect is really about sending someone's screen, and that's really kind of heavily. seeped in, web RTC and, um, low latency programming and stuff like that, that you can't just go in and buy something because if you could, then somebody would have already made the app.

**Ben** Exactly. It's the core competency and it's the thing that we, you know, we'll spend years getting, making better and better and have already spent a lot of time on, and that's what people are paying us for. And no one's really paying us for like a, a wonderful authentication backend. Like they don't, it needs to be secure.

It needs to work, but it's not a differentiator.

**Jeremy** One of the the reasons I ask is because sort of there's, there's this trend I think particularly within sort of the JavaScript community of, of saying like, okay, you know, maybe I don't need a back end. I could just use Firebase and maybe I don't need to have server side code for my authentication because I can use, I believe there's like Auth0 and I think Okta is another one.

Um, I'm kind of, you know, wondering, it's like, do you feel like in future projects or future work of yours that you would move in that direction? Or is there kind of like always going to be this set of certain things that you're wanting going gonna keep in your own code base?

**Ben** Um, I've never moved those particular things out of a code base I worked on and said, you know what? We've got to stop storing data and use Firebase instead.

Um, but Heroku, has really nice hosted Postgres, so it's like, I have really kind of actually used another person to, to handle that. Um, authentication.

I sort of don't even really understand what it means to not have authentication in your own app. Exactly. I'm not, like, I don't really get what Auth0 does, um, to be honest. So I don't know, but maybe, who knows?

**Jeremy** One of the things I'd like to do is kind of go back to  the start of your career.  So I was wondering if you could kind of talk about your experience starting as a, as a new software developer.

**Ben** Sure. Um, so it really kind of actually begins, at, college for me. So I majored in computer science, uh, but I also majored in like being a really terrible student. And, uh, the second major won. And so I did not graduate. I was a bit too immature and like kinda terrible at tackling large projects and breaking work down and not procrastinating and all this, uh, just had horrible, like academic skills.

Um, so, uh, did not graduate. Uh, which actually is, you'd imagine made it tough to jump into, uh, programming as a career. So I, I had to sort of work my way in from the sides. I started at like in IT consulting, like fixing networks and things like that. Uh, I eventually found this entry level programming job and it was great because it was entry level and they were willing to accept me without a degree.

And I got in and I got hired. And after just a couple of weeks, I realized like, this place was kind of the strongest, not invented here company, I've, I've ever even heard of, to the point that they, like they wrote their own email client, they wrote their own. Um, originally they used to write their own operating system to run on the mainframes that the software that the then like they programmed to run the software.

Eventually they start using windows, but they wrote their own, when I, when I left, they were getting ready to write their own version control. It was like a, it was, they were their own programming languages as well. Um, so there was like this weird not invented here thing.

And so I was learning these proprietary one company, uh, tools and languages, uh, and also just kind of a, a dearth of, uh good software engineering practices. So I was reading about, you know, how do you run a good software engineering team and what are, what are the things you should be doing? And we were doing so few of them.

Um, so it was hard. Um, and I, I was extremely demotivated by it and I was playing with Ruby on the side, uh, on the, like the nights and weekends, and I was using this really bad language at work and I was using this beautiful language on the side. And I was like, man, I have to, this is great that I've got, I'm in the right field now.

Like I'm, I'm glad I'm programming. This is, this is what I want to do, but this, this particular company is terrible. and it was funny because at the time I thought I was a terrible worker because I was so demotivated and I was like, Oh man, I am horrible at work. And it turned out actually that I was just de-motivated by the circumstances and so that was like affecting my work.

Uh, but I, I was able, , to turn the nights and weekends Ruby on Rails work into, uh, my next job, which was wonderful, uh, by just, just having done enough, like just kind of like making a couple play apps and teaching myself and, , just sort of self study, that I found someone passed along a job listing and they were looking for an entry level rails person.

And it turns out that I had just enough to kind of get me in the door there. And that was really where the, the curve at my career started.

**Jeremy** And, you know, for you, while you were at that job, when you first started, you said you thought that you personally were just not a good developer or and so was it really doing research outside of work that really kind of taught you like, Oh, this is.

This is what I really want to be doing, and I'm not, you know, it's not me, basically.

**Ben** Ah, I didn't know it wasn't me at the time. Um, I knew that there was this other, there was a better way to do it and there were better tools, and so that was frustrating, but I didn't realize how much that frustration was affecting my own productivity. Um, and I like I, yeah, I didn't, I didn't figure that out for a while.

I think I was kind of, until I got into this better circumstance, uh, with better tools and better coworkers and just better everything. And I was super motivated and I was very productive and I was like, Oh yeah, it wasn't, it wasn't just a constant, it was actually a variable.

**Jeremy** and for someone who finds themselves in that kind of position, you know, find themselves in a job where they feel like they're not productive, they're not motivated. Um, what would you tell that person to kind of make them realize, like, you know, it's, maybe it's just time to move on. Maybe it's not, it's not, you.

**Ben** I mean, I guess it's, it's hard to see in the moment is the thing. It's, like I said, I didn't figure it out until I left. I guess it depends on if the other stuff, like if things outside work appeal to you. Like I, I was having fun working on Ruby on the side, uh, and that felt enjoyable and fulfilling.

And so, um, that I guess was probably a good clue that a lot of my dissatisfaction was the circumstance and not just that programming in general. Uh, I don't know if I have like general tips on that though.

**Jeremy** working in that environment, what did it sort of teach you about when you look for that next job? Um, you know, were there certain things that you look for during the interview process or kind of in the job posting, that sort of thing?

**Ben** I feel like every job I have teaches me new questions to ask before I take the next job. Uh, and I don't know if there's a great way,  to get those without the firsthand experience. Although maybe I should, I'm realizing I should probably write a blog post about some of these things, uh, because you, you sort of don't realize the axes along which companies and jobs can vary until you've seen multiple points along the axis.

Um like, Oh, I didn't even think there would be somewhere that wouldn't let me work on side projects until I went somewhere. And they were like, Oh, we own everything that you do on the side. It's like, what? I had no idea that to even think about that before, until you're telling me to sign this, uh, this document here, and I say, and it becomes a whole fight.

Um, so yes, every single job has changed how I approached the next one.

**Jeremy** Yeah. I mean that's a, that's a good point. Cause I was, in a previous discussion, I was talking to Cassidy Williams and she was saying, you know. When she was working at Amazon, they basically told her, um, you can work on a side project, but it has to be with Amazon employees. And, uh, it was, you know, there's kind of all these sort of restrictions that it's sort of like, yeah, you don't really think about, um, until you see them.

**Ben** Totally. Yeah. I think, unfortunately, the list of things that I would, I would ask about are mostly from sort of scar tissue of bad experiences

**Jeremy** you know, in your, your next job, uh, you said you kind of started as an entry level Ruby on Rails developer. Um, what were your responsibilities then? Was it just taking, you know, tickets out of a backlog and you were working on code or was there kind of more of a, um, you know, role of figuring out what's the right thing to build.

**Ben** definitely the latter, which was great. We, I was on a really small team. It's just three of us, and we were sort of this independent. Um, skunk works kind of team inside a healthcare organization, uh, but as we were sort of the tech people that could come in and build custom software. And so we,  uh, accomplished kind of the first main goal for which the group was established pretty early on.

And so we kind of just suddenly had time and we were, our salaries were already paid by this grant that had come in. And so we could just kind of drop into a department and talk to them about what their process looked like. Um, and. Like one of my favorite projects was we went and met with their clinical trials department and the clinical trials department had an enormous spreadsheet that 80 people edited simultaneously, uh, and, and like giant  uh file cabinets full of papers that they would use to check for deadlines and things like that. And it was like, wow, we're going to be able to help you so much with such a simple app. And so I got to be a part of that whole thing just from, you know, from conception, conception of this idea. And that was, that was wonderful.

That's the, that's the kind of thing that I really, really enjoy.

**Ben** In that particular case, it was kind of easy because like the pain was so clear. Like they would tell us like, we have all these deadlines we have to hit. And so every Monday we go through every piece of paper and look for the due date, and we check it and we make sure it's not coming up soon, and then we move it to the bottom of the stack.

And it was like, well. I am going to blow your mind or it's like, you know, just attaching a series of documents to a single clinical trial was like a, a huge benefit for them so that anyone could like click it and, and view the document and attach new ones and put it, put a new version, like track track versions was also a huge thing for them.

Um, like, show me all the due dates across all the trials. Oh my gosh. That's, wow. What an innovation.

Um, so it was, and that was kind of like a nice springboard into this work cause it's not always so clear. I think, um, people that are in desperate need of fairly simple custom software are kind of the ideal sweet spot of development.

I think a lot of the times it's a little bit more subtle what you're going to have to build to make people happy.

**Jeremy** For sure. And I feel like sometimes, um, you know, that Excel spreadsheet that people have sometimes that that actually does work just fine.

And, and it's, it's sort of like that balance between, um, in your case, it sounded like building custom software, you know, was like a really big. Game changer for them.

**Ben** Yeah. Right. Yeah. The problem they had was not Excel. The problem they had was that they were, they had 80 people editing it at the same time.

**Jeremy** Right, right.

**Ben** Um, and that there were just things that Excel was not super well suited for. And so Excel alone is not necessarily a smell that there's a product there, although it's probably a decent, you know, it's, it's a good initial sign, uh, but it's an Excel plus pain is kind of more what you're looking for.

**Jeremy** Yeah. I guess pain. Just pain in general, right? It's usually a, is a good sign.

**Ben** Yup. But, Excel or something like it combined with pain is even better because there are lots of pains that are not good app ideas.

And one sign, one sign that a pain is not a good business idea is that people have not tried to solve it with something else already. So I was like, Oh yeah, no, we totally agree.

This does suck. Like, Oh, like what have you done to try to fix that? Oh, nothing. Okay. Well, there you go. Um, it's not actually a problem. It's just fun to complain about. Uh, but, Oh, like this thing is terrible. Like, Oh, we've done so far. Well, we have this enormous Excel spreadsheet, and we mail it around.

Okay, there we go. That's, now we're on to something.

**Jeremy** Yeah.  following that job. was your job basically, or the title, was that basically just a software engineer or was there

any, okay.  you know, in jobs after that you kind of started to take on more responsibilities, right? beyond just as a software engineer, um, what was kind of the next position you took and sort of how did it compare to the previous one?

**Ben** so my next job after that was at thoughtbot, which is a Ruby on Rails consultancy. Uh, we were based in Boston, and. I started off as a consultant there, like one of the web developers. And so I was building Rails apps for other companies. But along the way, I very much got the bug of trying to build a product for people on the internet, something that people would buy from me.

And I decided to make a screencast for developers, Rails developers who use Vim cause I got really good with Vim and I got I got a very sort of tailored, set of plugins and processes and workflows for uh, writing rails apps in Vim and my coworkers really appreciated it when I was like, kind of giving them tips during pair programming.

And so I was like, I bet I could sell it. Screencast teaching these things. And so I spent a few weekends and, um, put together something and then put it up for sale and started making money, uh, and like pretty quickly, like sold like a thousand dollars worth of, uh, $9 screencasts. And I was like, Oh my gosh, this is amazing.

And, uh, around this time thoughtbot my employer was that, does, this is all on the side that I did that. And then my employer was also selling educational content. So they were like doing, uh, workshops in person and charging big money for them. And every time they did, people would ask, Hey, like could, could I take this remotely, or could I watch a recording of it for some cheaper price? And so eventually they did record those workshops and put them up for sale. And so they were making some money from educational products. Um, I worked out a revenue share deal where I put my screen cast on the thoughtbot, you know, collection of products.

And, uh, we, we sort of split the revenue from that. Uh, and then one day I went to the CEO and I said, um, I think thoughtbot should make a. Um, recurring revenue model, put all the educational stuff underneath it and produce way more content and create this like large community of, of people that are trying to learn to be better rails developers.

And he said, okay, go ahead and do it. And so that actually became my new job and I ended up kind of more or less starting a company inside the company. And that was called up case. And that, uh, I ran that for some number of years. Uh, and that was, uh, really my kind of first major foray into like building a, a a thing, like a proper, like business.

Uh, and it was a super formative, it was exactly what I wanted to do because I was, I was still really enjoying programming, and I, and I love teaching programming, but the. Amount of skill I had in programming versus the amount of skill I had in like how do you make a business, uh, was completely different.

And I wanted to bring those more in line. And so this let me actually focus on that and learn those things while still drawing a developer salary, which is pretty wonderful. Like the risk is, was basically nothing, um, to me personally. Um, and more or less to thoughtbot. Uh, so it was a very nice like learning laboratory for those, those new skills.

**Jeremy** And how big was the team you were working with and kind of what were, how were people's roles delineated.

**Ben** Pretty small. Um, it was just me for a while. Uh, we eventually hired a full time producer who helped us, like make videos and podcasts. And then we would occasionally, when, when thoughtbot consultants were free, like when they weren't booked on clients, we'd like bring them onto the project. And so occasionally the team would get as big as four or five, but it was usually more like two to three.

**Jeremy** you, you know, you're kind of talking about how the team would grow and shrink, um, you know, where the roles that people, where they like designers or were they like programmers or what, what was the type of kind

**Ben** It was a mix. It depended on what we were trying to do. So upcase was we were selling content and so. That the easy answer to what should we do now is make more content generally. And so a lot of the times we were spending quite a bit of hours, like putting together the next, the next course or the next, like weekly screencast or or 

something like that. Which by the way is something I will never sign up for again, I hope, we basically one day like decide like we should, we should do a one like a weekly screencasts, a short one, and that will like keep people subscribed to the service cause they're paying every month. So they want to see new stuff.

So let's, um, let's have a recurring, uh, production of this thing, which is just like this never ending, like content treadmill that you now can't get off of because your revenue is tied to this promise that you've made. Um, so I, uh, I will not do that again. I, I think, I think, I hope I've learned my lesson from that.

**Jeremy** Yeah. And so like, later on you wrote a course on refactoring rails, kind of on your own and sold a video course. Right. What, what were sort of the, the lessons that you took from working on Upcase to kind of what you decided to do then?

**Ben** Hmm. Um, I'm not sure. It'd be hard to tease apart exactly what came from upcase and, and, and what didn't. At that point. I had a lot of experience making rails focused educational content and selling it. And so it was kind of like, it was kind of just like the work I had been doing only more independent, so, so tons of overlap really.

**Jeremy**  are there other screencasts that you've watched previously or other educational material that you looked at and or certain trends where you felt like these kinds of things aren't really built the way that I would like them to be. And so that you sort of adjusted what you built to reflect, you know, what you would want to see?

 **Ben** not that much. I don't consume that much other like educational content for programming. I would say the closest thing to an answer to that is that I, I really love showing code like live coding. Basically. It's like when I, when I do technical talks, I try to have some, at least some live coding component because I think it makes it more interesting.

I think the risk keeps the talk feeling more exciting to people and also you can learn a ton by watching people actually work. So there's the, there's the topic I'm teaching you at the time, but you're picking up lots of other little things, just like how do you get your cursor from here to here? How, like what part do you edit first?

Like what do you do when the test fail? What were you looking at? What files you opening, how you arrange the pains of your editors so you can see different things. And so I just think that's, it's such a rich. Um, vein that it's kind of wasteful or kind of a missed opportunity if you don't actually show live coding when you're teaching developer topics to some extent.

Uh, and so I made sure that for my course, basically every topic I demonstrate is, mostly like me taking uh, okay, here's some rails code that I wrote and it ha exhibits this problem, or we have this goal and then I'm going to refactor it live for you in the video.

**Jeremy** Yeah. I mean, I could say for myself, when I went through refactoring rails, I think what struck me was. Like the combination of, like you said, the, the live coding, but also in a lot of courses you'll basically be having slides and you'll be looking at someone talk and it's kind of just concepts, but you're not really seeing the code at the same time.

And to me, I really liked that you kind of just jumped right into the code and that you also had, um, sort of the code, uh, written down separately so that if you need to review, you could just look at that quickly rather than have to look through 30 slides again and find the thing that you were interested in.

**Ben** Thanks.  I'm glad that worked well for you.

**Jeremy** another thing I'd like to ask you about is, you know, in the past you used to give a fair amount of conference talks and they're very high energy, they're very kind of unique in their presentation style. And I sort of wanted to get your opinion on when someone is deciding to make a conference talk, like what is kind of the reason they should be doing this. Like what makes something a great conference talk versus something they should just make as a blog post or a post on YouTube or something like that.

**Ben** That's a great question and I liked the way you phrased that because that is actually my complaint of most talks is that most conference talks would be better as a blog post. Because you could skim it and take it in very quickly. And the information density is much higher. And so to me, every talk should be forced to kind of justify its existence as a talk and not a blog post or a YouTube video that you can watch it.

2x or something like that. , and so I tried to take the opportunity, of talks to do talk specific things, uh, like talk to the audience a lot or have the audience do weird things or, , take questions during the talk, like it let people heckle me and try to respond. And,  that sort of thing. Like to me a talk is a performance.

It is not so much conveying information. Like, I do want to teach people things, but you have to realize that like your first goal is kind of performance. You're on stage. You are, you have a responsibility to your audience to not be boring, uh, in a way that a blog post does not. Exactly. Because the blog post is kind of, you know, the result of a Google search.

And so someone is seeking out this information and they want to skim it and get it quickly that the talk it experiences like you have chosen to spend some of your precious life, uh, sitting here watching me. And so I take the responsibility of making it entertaining and interesting. Uh, very seriously.

**Jeremy** One of the things that kind of strikes me is that, yeah, a lot of times I'll be sitting in a conference talk and the actual information may be useful, but I'm just kind of bored. Right.

**Ben** Yeah, totally. And bored people don't learn is the thing. Like now in particularly, you're competing with, everyone has a laptop and so it's like, well, okay, your talk has to be more interesting than the internet. So get to work, you know? Yeah. You had to do some stuff like plan some crazy stuff. You're going to have to do some things, plots, and stops to, to actually be more interesting than that.

**Jeremy** Yeah. And like,  there was one where you're able to get the room to sing happy birthday to someone. So, um, definitely, definitely unique.

**Ben** Yeah, I, I'm pretty much always trying to think of like, okay, with this talk, what kind of thing can I do that will get people to close their laptops? Like what? What gets people to actually snap out of the, you know, browsing and not actually paying attention, stupor and pay attention to what I'm saying.

**Jeremy** and, unless I've missed them somehow it seems like in the last few years, um, you kind of haven't given as many talks. Is there a reason why you stopped giving them 

**Ben**  um, so I got a little bit burnt out on traveling so much for talks. At first it was great cause it was like a great way to like, do like company-sponsored travel. And so I was just like, every month I was somewhere else. And I really enjoyed that for a while. And then I got kind of burnt out on traveling around quite so much.

that was only a small part of it. I would say that the bigger thing is just that I moved less out of the tech world and more into the business world. And there are just fewer conferences targeted at people that are doing the things I'm doing Mo most of these days. Uh, and so. Um, I do still give some talks at like MicroConf, which is a conference for like, people that are mostly starting, like bootstrap software companies.

Um, and so like, my, my skills and my knowledge are more appropriate there, but I'm, I'm not nearly as up on the latest, coolest, you know, programmer advice and,  tech stuff as I was before.

**Jeremy** And what would you say is like the primary role of a conference? Like why, why should somebody go to a conference and why should they speak at a conference?

**Ben** That's another good question. for first of all, if you can speak, you probably should. Speaking is a great hack.  the return on investment, I think for speaking at a conference can be really, really tremendous. Particularly, let's say you're, you're sort of introverted and you don't want to go and quote unquote network with people.

If you give a talk, people will come up to you. They will network with you. Like they'll come like there's an already an established conversation going. So it's a great way if you can stomach the being up on stage,  then you can  not have to go seek out people, which is wonderful. Um, but. It's interesting to think about like what, what is the role of a conference?

Like what, what should you be getting out of it? To me, I think the most useful things are our friendships actually. So I keep going to this, to MicroConf. This conference I mentioned mostly because of the people that I met there. And so a lot of the things that I've learned and the good ideas I've taken out, um.

Are from conversations with people, not during talks, but in fact just kind of like the hallway track of, of hanging out with people and then conversing with them later. And I have friends that friendship that are now several years old. and it's because of those, those sort of chance meetings. And so the, the talks sure, like maybe you learn something at a talk.

Sure. But like, they're going to be recorded and so you can go watch that later. But to me it's hard to re replicate the experience of being in a room where a lot of people have the same interest. And so you have, you know what you're gonna talk about. Like you have a, the conversation topic is pretty much already there and that's, that's, I find that really valuable.

**Jeremy** that's really interesting because it's sort of like you're giving the talk, but. That talk is almost just like this sort of excuse or this framework for people to come up to you, so it's actually benefiting you a lot more. and, not necessarily just the audience. Yeah.

**Ben** Yeah. Hopefully. I mean, hopefully it is useful too like, if you give a bad talk, it people aren't gonna want to come talk to you nearly as much. So, you know, I try to do a good job anyway, but yes, I'm certainly getting something out of it. And there's a, there's a crazy, there's this phenomenon I experienced a couple of times, especially in the tech world where if you give a talk about a thing a couple times, you become the, the whatever guy pretty fast.

I spent one year, I think where I gave a VIM talk at like six or seven conferences. And then I was the VIM guy for like three years or four years after that. Uh, just based on that work right there. So it's, if you want to estab, it's a really nice tool for kind of establishing expertise in something that people will attribute to you even more expertise than you might, uh, deserve.

**Jeremy** but I guess the thing is, is that, you know, the process of preparing for that talk probably makes you more of an expert than you were to begin with as well. Right.

**Ben** Absolutely. Yup. Yeah. It's not all smoke and mirrors.

**Jeremy** another thing I want to kind of talk about is while you were at thoughtbot, but also now, um, you know, you've been running podcasts for how long has it been now?

**Ben** Something like five years

**Jeremy** So what is kind of the biggest benefit you feel like you've gotten out of podcasting.

**Ben** Um, I'm not sure what the biggest is, but there've been a few big ones for sure. Uh, the first was I started when I was at thoughtbot for awhile. The podcast I hosted was an interview show. And so we had on interesting people from the industry and I didn't even think about how good that would be for me networking wise at the time.

And, and I didn't realize it for several months. Then I was like, wait a minute, I have the email addresses and have had a conversation with like all these, like fairly prominent people in our world. so that's great. By the way, actually, maybe one of the best things. I think, honestly, it's just that you have an excuse to have a conversation with someone.

it's flattering and useful to have someone on a podcast. I'd like to be invited to a podcast because you don't have to prep. You get to have a long conversation. Uh, and, and everyone wins, right? Like your audience wins. The person on coming on wins, the host wins. It's just all, it's a very positive interaction.

And so if you had emailed me and said, Hey, like, do you want to talk for an hour? In a couple of weeks from now I'd be like, ah, like maybe, but it probably not. But if you're like, Hey, do you wanna come on my podcast? It's like, yeah, definitely. That sounds great. Um, so it's, it's a good, uh, it's, it's a nice to have uh even a small podcast just for the easy excuse of inviting someone on and having a chat with them.

but then beyond that, , like today, I would say the most value, I don't really have very many guests on my podcast. these days. Uh, but I still get quite a bit of a value out of it because, uh, on it, I talk with my cohost about what it's like to start software companies and what we're doing week to week.

And we're not even exactly trying to  to teach people things. We're just talking about what we're doing. But people learn stuff anyway. Like they, they follow the story. They sort of see the lessons you're learning in real time. Uh, and that it kind of, it gets them on our side. Like having an audience, like a lot of my, um, accustomed the customers for tuple first heard about us through the podcast.

**Jeremy** yeah. It kind of kind of goes in with the trend lately of a lot of people talking about how you should, you should learn out in the open. Right. And I think like, , maybe, what are things that you can do that don't really require a lot of extra work for yourself, but that other people can learn from right?

**Ben** Yup, totally. And again, like I think that point that there's a point there that I think is really good, which is you don't even necessarily have to distill what you've learned or turn like turn it into lessons. Exactly. Like I, I don't, we don't sit down and say, okay, what are the, what are 10 bullet points of advice based on what we've learned recently?

We just talk about what we, what we're working on and what the results are. And people can form their own conclusions and learn lessons that you aren't even seeing, by the way, which is funny too. So it's that, that is one great thing about working in public is that it's, it can be useful to without much editing or without much attempts to kind of make it meta useful.

**Jeremy** and like, when you personally listen to a podcast, what are, what are you sort of hoping to get out of it.

**Ben** Kind of that actually, um, the podcasts I enjoy the most these days are, not teaching podcasts. They are talking about what the people are doing in detail, sharing numbers and explicit tactics and advice or not advice, but just like things are doing. Um, and I really, that's like my, those are my favorite these days.

and I, I found this really clearly. Like I've noticed, I have a couple of podcasts to listen to, which are  frequently the host or hosts talking about what they've, what they're doing and what the numbers are and what's been working in and what they're frustrated about or struggling with.

Uh, and I really enjoy those episodes. And then sometimes they do episodes like, um, uh, 10 business books you should read this year. And I always find, I hate those episodes. I find them so much less useful. And so it's like when, oddly enough, sometimes I find that when people start trying to teach and trying to distill, I like it even less.

**Jeremy** Hmm. because it's sort of less, um, it feels less real, I guess. You know, it kind of, somebody kind of prepared, these are the things I'm going to teach you. Um, but it's not just kind of like, these are the thoughts that are coming out of my head and these are, this is what I really believe and feel.

Right. Mmm.

**Ben** yeah. And the conclusions that you've drawn from your own experience are maybe corrected or maybe not. And so if you decide, if you distill your experience down and then into a series of lessons, maybe I should listen to them and maybe I shouldn't. But if I listen to your experiences and draw my own conclusions and, uh, have like a useful model in my head based on what happened to you, uh, that, that feels better to me.

**Jeremy** Yeah. That kind of reminds me of something that I hear often is that like the people who are kind of in the best position to, to teach others are those who are kind of learning as they go. At the same time, you know, not so much like looking back, um, these are the things that  that you should do.

**Ben** Yeah. I will say this is not to totally dismiss that kind of, Publishing, I guess, uh, like if I learn a useful thing while I'm writing some code, that's a great blog post. Like if you discovered something like a cool method or an interesting technique, or if a shorter version of whatever, like that's a great thing to just write up and say, Hey, I found this thing today.
I learned this thing. That's a great tweet. That's a great whatever. Um, for me, Podcast. I guess this advice I think applies mostly to podcasts and also just kind of my personal proclivities. Like some people probably want the extremely tactical, I've distilled it down for you advice. It's just for me. I feel like as I get a little further along in my knowledge in various fields, I want less tactical advice and more kind of real world what's going on with you.

**Jeremy** and sort of like What is the things you should think about when you're deciding what kind of form that your posts should take? Like whether it should be something on Twitter or it should be a blog post or something you talk about on, you know, your podcasts.

Like what are you kind of thinking about when you make that decision.

**Ben** Um, for me, it's, I don't, I don't have a framework for it or anything. I'm, I'm pretty uh haphazard, I guess with that, I tweet occasionally when it feels like it's a tweet shaped tweet, tweet sized insight, I guess. Uh, and then  most of the rest falls into my podcast, cause I don't actually write almost any blog posts these days, which is not ideal, but it's true.

Um, you kinda can't go that wrong. And I feel like, like just whatever, I think the answer is kind of like whatever you're going to do. Like maybe it's best as a blog post, but if you won't actually write the blog post, but you will write a tweet, then do that.

**Jeremy** For sure. Yeah. I mean, I, I've noticed for, myself, like if I'm looking for tactical information, like you're saying before,  you know, blog posts are really great, just because you can kind of skim through it and see like, okay, this is the thing that,  that I wanted to figure out or wanted to do.

Um, but at the same time, you know, when you listen to podcasts. , just kind of hearing people talk and kind of go back and forth on a problem that's similar to yours or maybe something that you might run into the future, even if you don't pick out like a specific insight at that moment. I kind of feel like sometimes it helps you, uh, you know, inform your decisions when you do run into something in the future.

You kind of remember, even if you don't remember specifically, it came from that podcast. Um, you know, you kind of are a little better equipped for whatever you're dealing with. Yeah,

**Ben** Yeah. I think our brains are pretty wired for stories, and so if you hear something in a story, I think it's more likely to stick in your head and be accessible later versus a sort of factual blog posts is probably like, I've, I've written factual blog posts and then forgotten that I had written them and like discovered them in Google searches later.

So I know that information does not hang around.

**Jeremy** I kind of wanted to talk a little bit about, you know, currently now you're the CEO at Tuple, right? And I wanted to talk about what that change has been like for you from going to working for, you know, a company like thoughtbot, um, to running your own company. Like what have been the biggest challenges or changes, you know, that sort of thing.

**Ben** Um, I don't know what the biggest challenges have been exactly. it's been, I mean, it's been a positive change. It's been great. Like I'm super glad I did it. I've wanted to do it for a long time. And when we came up with the idea for Tuple and did some research into it, it was like, I just had this feeling like if I don't try this, I'm going to really regret it.

And so I, I'm super glad we took the plunge. There are a constant and changing set of challenges, but that's actually what I enjoy in life, typically is like, I, I like to solve new problems and discover new things. Stretch myself. And so I, it's hard to think of any like one like, Oh, it's way harder because of X.

It's, it's, it's, it's harder for a bunch of reasons. Like the stability is maybe the biggest thing in the early days. Um, we are now like sustainably profitable, which is awesome. So, uh, but in the early days, like I was just burnt. We were all burning cash every month and watching our net worths go down, and that was stressful.

So that was, um, that was the biggest change, that challenge at first, I would say. Ah, now what is it, I don't know now is maybe the deciding like it's probably still like, it's actually, um, I would say the biggest consistent challenge is, mental state management. So like for me, being less reactive to good things and bad things and trying to stay calm and sort of focused, uh, is a consistent hard part. Like when there's less at stake, it's easier, like at thoughtbot I didn't really get that stressed, honestly. Uh, I get more stressed now, um, because the stakes are higher and it's like, well, this is so cool. I don't want it to go away and I help, I don't steer the ship into the iceberg. And they're just like more ways to, for the company to get hurt or die. Uh, then like for your full time job to go away and in which case you just get another one, so whatever, but you can't just make a new company necessarily. Uh, so yeah, I would say that it's, the mental side of things are much more challenging.

**Jeremy** kind of knowing that you don't have this, I guess safety net if things don't work out on whatever project you're working on. Um, if you're working for a company, they'll just kind of move you onto another project. Right.

**Ben** Yeah. Unless you're like really high up inside an organization, I think it's hard for you personally to do that much damage. But with a three person startup, uh, we're on the CEO, I'd certainly could hurt us.

Uh, so it's this, the stakes feel a bit higher there and it's like, yeah. And, and this is, I own a third of the company, so it's like, if I, if I screw this up, I've really hurt myself a lot actually.

And it gives me a great lifestyle. Like, I don't want this to go away. I want to keep doing this for a long time. It's actually really fun. So that's that, that that part of it feels a little more stressful.

**Jeremy** How about like, access to specific resources? You know, when you work at a large company, , you have all these employees that you have access to, , you have services like, health care or whatever that your company takes care of for you.  are there any things that you kind of miss in particular that you're, you're kind of thinking like, Oh, it'd be so much easier if I had this same thing that I had back at my company.

**Ben** Not really, actually. and it's, it's, it's interesting to me that the answer is not really. Um, I think you can get a lot done with a small team and then the occasional consultant, some of the back office stuff, uh, is a little annoying. Um, but like, we were fortunate enough to live in like Massachusetts, so there's like a good, healthcare answer here.

Like health insurance was pretty painless for all of us to get and pay for. Yeah, I don't, what do I miss? I dunno. Not much. Really. Um, which is man. We're pretty lucky. And it's, it's funny, like we, we work out of my, uh, one of my cofounders, like second bedrooms in his condo and so, but like, which sounds like, Aw, man, like that's, you know, you're doing the scrappy startup thing and it's kind of like you're suffering, but you know, you, you make it work and it's like, actually, no, it's great.

Like we have a kitchen, so we make lunch sometimes and we have like a comfy couches and we sit and play video games occasionally, and it's just, it actually, I don't feel like I'm deprived for in any way really.

**Jeremy** Yeah. That's awesome. I mean, in some ways it kind of sounds like a, what people might think of,  people who went to school or went to college, you know, this experience of just working with friends, hanging out in an apartment, that sort of thing. It kind of sounds a little bit like that.

**Ben** Yeah. Uh, it's, I've, I've said before before that I think, I think we're in the good old days right now. Like it's just the three of us were working out of a second bedroom. We're scrappy we're light, like we make decisions pretty fast. We, we move pretty fast. I think. The future is something we look back and go, wow, I  remember it was just just the three of us and we didn't have an office and there was no payroll really, and they're just like, just like a simple or simpler time.

It's, I'm trying to appreciate what we have now and like there, there are downsides for sure, but I feel like this is kind of, we're in a kind of a, a special time actually.

**Jeremy** and that kind of makes me wonder, you know. As you think about potentially growing the company, um, you know, how do you plan to try and keep that feel? Or do you think you can keep that feel?

**Ben** Um, I don't know. I haven't done it before, so we'll see. Um, I have guesses. Uh, my first guess is that we should try to add people really slowly, like . And first of all, I'd be reluctant to add people. I have friends that have businesses that have employees and they say like, there's a, it's nice to add more people cause you can sort of do more things, but you're adding a ton of overhead.

Uh, so like, you know, wait to hire your first employee for a while and that, that resonates a lot. Uh, just so just like keeping what we have for as long as possible until it really hurts and we feel like we can have a lot of benefit by giving it up, is sort of the first. Order of business. Beyond that, I'm not sure everyone wants to do it.

Everyone wants to keep that sort of a fast startup execution ability, and yet everyone more or less loses it. Um, so it's clearly very hard. Uh, so I don't, I don't know. Uh, I don't think it's a solved problem. I think it's something we'll have to work on a lot and learn lots of lessons.

And there just seemed to be, there seems to be this phenomenon as like that, that as a company grows in order to execute a given plan that works and loses the ability to execute new plans. I think because you're busy servicing, like the current plan that has always worked and it's hard to cannibalize it and, and whatnot.

and then there's just also just like the geometric explosion of communication directions as you grow this, there's a lot of challenges. There's a lot of things that make that, that are hard about that. And so I think it's like a multidimensional problem.

**Jeremy** Yeah. I mean, that's, that's interesting because, uh, you know, right now you're a team of three. So I would imagine that, you know, most of your communication is in person, face to face. Right. And so, I guess in your previous experience, you know, How did you kind of keep in communication with either your clients or your coworkers?

You know, was it like email? Or was it chat, like how did you kind of keep it all together in a, in a larger environment?

**Ben** Um, definitely a lot of chat. Like thoughtbot was a Slack company when I left and that was where most of the communication happened, it seemed like,

Yeah. As uh, as scattered as that is. I think that was, well, that was sort of like the, probably the biggest piece of it was chat combined with maybe like GitHub issues and, and things like that.

**Jeremy** and, and sort of, you know, a trend kind of in the last few years is more and more people are talking about, um, working remote or the benefits of working remote. Um,  you're in this environment where you're able to have everybody in the same room, uh, and you're able to have this really, you know, high level of communication in person.

Um.  in terms of the future of work are, are more people going to come back to that environment or do you think kind of like this remote thing is going to pick up more and more.

**Ben** I think I agree with, um, Alex McCall here. Where remote will become more and more popular and it will also have substantial downsides. I think it, it has, like, there's a lot of benefits to remote work. There's some serious drawbacks to it. Uh, I think it will prove enduringly popular despite its drawbacks because of its, its substantial benefits.

But I don't, I wouldn't call it an unalloyed good. I think there are, yeah. So, you know, it's, it's, I think it's, I think it is somewhat inevitable, but also like we'll be dealing with the ramifications of it.

**Jeremy** yeah. And for your own company, you know, let's say for your next hire, would you ensure that there's somebody who could work with you guys? You know, locally?

**Ben** I think so. Yeah. So my first choice is to work on in person teams. Um, and part of that is, is just my personality, that I am very extroverted and I, I get my most energy working in person with people and talking to them and all that. So I think. Given my proclivities, I would want that. Uh, and because again, I think there are drawbacks to remote stuff.

Then again, we, we make a tool to make programming remotely less painful. So like we're, we're trying to make it better and I'm happy to be part of the solution. Hopefully, you know, to like set some of the drawbacks of remote work like that. The positives are great. Awesome. Um, one thing that is crappy about working remote is that it's kind of lonely and I have found that a short like pairing session, um, with somebody is like, actually really like, boosts my mood substantially.

Just having like a quick call with them a quick, a tuple session is like actually kind of awesome. So like a surprising mood. Improver Uh, it's kind of nice to, like, I try to be honest about like, you know, what, what my preferences are, but also like, we're sort of on this mission of like, let's, let's make it so that if you do choose this, and we all, like, we work mostly in person, but we also work from home or we go, I was, uh, I spent a month,  traveling, uh, this last summer.

And so I was working remotely. So like, we, even though that we're generally in person, company, we still have remote, you know, several times a month. So I think everyone's kind of moving to that model. So when you are remote, what are you gonna do? So that's, we try to have a good answer to that.

**Jeremy** Yeah, that's an interesting point because it's kind of like as more people are doing remote work and more people are getting, um, like you said, lonely or just kind of feeling more disconnected, you know, maybe what we are going to see is more tools like Tuple, more tools that kind of make people feel like, um, they have maybe not 100% the same as face to face, but you know, getting closer.

Right.

**Ben** Yep. Yeah. I'd be shocked if that did not be true, become true.

**Jeremy** Yeah. Cool. Yeah, that's a, that's an interesting insight. kind of looking back at, you know, your work where you were just a software engineer to now being the CEO of a company, ,  are there things that you sort of miss about, you know, the type of work you used to do, or are you kind of all in on, you know, 

**Ben** Pretty all in on the CEO thing. Um, I really enjoy it. Uh, overall I don't really have any complaints. I do love programming still, and I still actually get to do some programming, which is cool. Uh, I probably should do less and less with time, and I suspect I will. Um, so I, I think I will miss programming more and more as it becomes less and less a part of my, uh, day to day.

but what I really enjoy most of all is just like the acquisition of new skills. And so giving up programming is, um, made up for by getting to learn and practice new things and figure out new problems.

**Jeremy** were there any like  I guess, critical decisions you can remember over the past decade that you feel like really shaped, you know, where you got to, , today.

**Ben** yes, I would say that probably the biggest thing is that I got interested in teaching. not just programming, but like helping other people get better at it too. And so like when I sit, I gave my first talk at railsconf in like 2009 or something. And, it was. A big moment for me, I think because it turned out I loved it.

Uh, and it also like raised my profile substantially. And so suddenly, like I, I got like a hundred new Twitter followers after my talk. Uh, and that basic trend has continued to where it's like, I, I tend to make a lot of things and teach. I try to teach a lot. And in return I attract people that like learning things.

And then every so often I'm like, Hey, I have this thing and it costs money. And there's this big group of people that are, that know me and trust me from the other stuff, and they are willing to buy it. And that uh reality has let me do a lot of things like what I'm doing now. I don't think. I'm not sure we would've made it, uh, to profitability if I had not been building this audience this whole time and had this like large group of people that I could say, Hey, I made a thing.

I think you actually will like it. And they go, Oh yeah, that's Ben. I know. He makes good stuff. We should try it. Um, so I'm very, very glad I got into this early because I think that's the hard, the hardest part is just like how long it takes to, to build up these, this group of people, but it's probably had more impact on my life than almost anything else professionally.

**Jeremy** mm. And, and what are sort of the things that you've done over the years to kind of maintain, you know, relationships with, with people, with, with friends and fellow developers to, to kind of keep this going.

**Ben** Um, I wouldn't say I've done an amazing job of it, honestly.  let's say Twitter and my podcasts are kind of like my best answer to this. Um, I put out a weekly podcast for like, like I said, six or seven years, I think now. , I think that's PR and there's something special about the spoken word, like hearing someone actually talk about their story in their own with their own voice.

That I think builds a connection that's, that's pretty real. Um, and so those are the main touch points. Like, I don't have a weekly newsletter. I don't have a active blog. Um, I tweet sometimes, but not that much. Uh, but the, the podcast to me doesn't feel like work. And so I put it out every week and it's kind of the, it's the best.

There's a sort of core group of people that have been listening to it for a long time or like that, pick it up and listen to all of it. Uh, and I think that's, that's probably been the best vehicle for that.

**Jeremy** and for somebody who kind of. They, they want to build up, you know, a set of people that they can count on or that they can learn from and things like that. What would your advice be to them?

**Ben** Like someone that wants to build a professional network, you mean? Or,

**Jeremy** , yeah, let's, let's go with that.

**Ben** my best source of that I think has been,   first of all trying to work somewhere with great people. Like I, I think especially in the early days, working somewhere that has great coworkers is more important than working somewhere than other benefits, like a lot of money or a mission that you love or, or something like that.

and then I would say actually like, like I touched on before, conferences have been also a really good source for me. I've just like meeting like friends, like professional friends that I've, I've wanted to stay in touch with.

**Jeremy** Yeah, so it seems like it's a combination of finding some kind of public outlet, right? Whether that's writing blog posts or getting on Twitter or doing conference talks. Right. 

**Ben** It definitely helps. Yeah. If you're putting stuff out there that let people find you and realize that you are sort of kindred spirits and that you should have a conversation that's, that's useful. I think.

**Jeremy** and then being very intentional, I guess, about your career choices, trying to find people to work with that, you know, you really get along with and you can really all kind of,  

**Ben** Yup, totally. And I've learned more from,  talented and generous coworkers than, than any anything else. Like any YouTube series or you know, courses or whatever, like does nothing quite like sitting with someone, uh, who's better at something than you are and having them teach you how to do it. That's just, humans have been learning that way for thousands of years, millions of years maybe.

And it's a, it works real well.

**Jeremy** for sure. I mean, I think that's one of the things that. Whether it's software development or really any position, you know, the, the human connection. Just like working with people, learning with people, and just, you know, just having fun, right? Like that's such a huge component to whether you're going to have a good time or you're going to have a bad time in this, in this industry right?

**Ben** Yup. Yeah. Quality of coworkers are important for like your learning, but also your happiness for sure.

**Jeremy** Cool. Well, that's probably a pretty good place to start wrapping up.  is there anything in this coming year that you're kind of looking forward to

**Ben** yeah, I think it's going to be an awesome year. So,  2019 was our first year, like actually in business. I'm just like, we had, we had zero customers in January of 2019 and now we have hundreds. And so we've, we've gotten past the like, okay, we can, we afford to keep running this? And the answer is yes.

And like now it's like, okay, we're, we're making some money. We're on a good trajectory. And like, what, what can we do with this thing? Like, we have this sort of interesting opportunity and can we keep it growing? Can we keep making the app better and better? Uh, I'm just really excited to kind of. Get to like version two of the company, like it feels like we kinda just hit one point now where it's like, okay, the software is pretty good, the business model seems to work.

Um, but we're sort of doing scrappy versions of a lot of things and now it's like, okay, now we can actually take the time to invest and like really go back and do more things with more quality. Um, and, um, I'm excited for all that opportunity.

**Jeremy** Yeah. It's kind of like this move from almost like the scrappy startup to, you're almost becoming like a established player, I guess, if, if that's a good way to put it.

**Ben** Yeah. Well, we'll see. I would say we're not there yet, but, uh, who knows. 

**Jeremy** Yeah. Yeah. That's exciting. , and, , good luck to you in the future with tuple.

**Ben** Thanks very much. I appreciate it. And thanks for your, uh, your good questions.

**Jeremy** Oh, thank you. finally like, for people who want to check out Tuple or kind of see what you're up to, where should they head?

**Ben**  Tuple is just tuple.app. If you are interested in a remote pair programming app that works on MacOS , for me, um, I have, I host a podcast called the art of product. Uh, if you want more stuff like this, uh, that would probably be the way to go. Uh, and if you like Twitter, uh, I'm, r00k on Twitter.

**Jeremy** Cool. And the very last question I have for you is. 

**Ben** Oh man. Um, that's a great question and I applaud your, your research for it. Um, I'm probably gonna go with link overall. Yup. Classic link. Yeah. I started off with young link, played a lot of him. Uh, but I think big link is a little bit better fit for me.

**Jeremy** Very cool. Yeah. He's got a lot of tools. He's got the, the boomerang. The bombs. Yeah. Pretty cool. Well, thank you so much for, for joining me today, Ben.

**Ben** Yeah. My pleasure. Thanks for having me on.

**Jeremy** Notes of the show?

**Ben** Notes of the show can be found at softwaresessions.com.

**Jeremy** Thanks for listening.

</div>