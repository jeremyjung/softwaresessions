+++
title = "Testing"

description = "Jason Swett discusses when and how to write tests within the context of smaller applications"

[extra]
episode_url = "https://media.transistor.fm/2c5eadba/6efa9b85.mp3"
+++

Jason Swett is the author of the Complete Guide to Rails Testing. We covered Jason's experience with testing while building relatively small Ruby on Rails applications. 

Our conversation applies to just about any language or framework so don't worry if you aren't familiar with Rails.

### A few topics covered:
- Listen to advice but be aware of its context. Something good for a large project may not apply to a small one
- Fast feedback loops help us work quicker and tests are great for this
- If you don't involve things like the database in any of your tests your application may not work at all despite your tests passing
- You may not need to worry about scaling at the start for smaller or internal applications
- Try to break features into the smallest pieces possible so they can be checked in and reviewed quickly
- Jason doesn't remember the difference between a stub and a mock and doesn't think it's that important


### Related Links:
- [Code with Jason](https://www.codewithjason.com/)
- [The Complete Guide to Rails Testing](https://www.codewithjason.com/complete-guide-to-rails-testing/)
- [Code With Jason Podcast](https://www.codewithjason.com/podcast/)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** today I'm talking to Jason Swett, he's the author of the complete guide to rails testing, a frequent trainer and conference speaker. And he's the host of the code with Jason podcast. So Jason, welcome to software sessions. 

[00:00:13] **Jason:** Thanks for having me. 

[00:00:15] **Jeremy:** from listening to your podcast, I get a sense that the size of the projects you work on they're, they're relatively modest.

Like they're not like a super huge thing. There, there may be something that you can fit all within your head. And I was wondering if you could talk a little bit to that first, so that we kind of get where your perspective is and the types of projects you work on are.

[00:00:40] **Jason:** Yeah. Good question. So that is true. Most of my jobs have been at small companies and I think that's probably typical of the typical developer because most businesses in the world are small businesses. You know, there's, there's a whole bunch of small businesses for every large business. And so most of the code bases I've worked on have been not particularly huge.

And most of the teams I've worked on have been relatively small And sometimes so small that it's just me. I'm the only person working on the application. I, don't really know any different. So I can't really compare it to working on a larger application. I have worked at, I worked at AT&amp;T so that was a big place, but I was at, AT&amp;T just working on my own solo project so that wasn't a big code base either.

So yeah, that's been what my experience has been like.

[00:01:36] **Jeremy:** Yeah. And I, I think that's interesting that you mentioned most people work in that space as well, because that's basically where I fall as well. So when I listened to your podcast and I hear you talking about like, oh, I have a, I have a rails project where I just have a single server and you know, I have a database and rails, and maybe I have nginx in front, maybe redis it's sort of the scale that I'm familiar with versus when I hear podcasts or articles, you know, I'm reading where they're talking about, oh, we have 500 microservices or we have 200 instances of the application.

That's, that's not a space that I've, I've worked in. So I, I found it helpful to, to hear, you know, from you on your show that like, Hey, you know, not everybody is working on these gigantic projects.

[00:02:28] **Jason:** Yeah. Yeah. It's not terribly relatable when you hear about those huge projects.

And obviously, sometimes, maybe people earlier in their career can get the wrong idea about what's applicable to their situation. I feel like one of the most dangerous kinds of advice is advice that's good advice, but it's good advice for somebody else.

And then I've, I've. Been victim of that, where I get some advice and maybe it's genuinely good advice, but it's not good advice for me where I am doing what I'm doing. And so, I apply the advice, but it's not the right thing. And so it doesn't work out for me. So I'm always careful to like asterisk a lot of the things I say where it's like, Hey, this is, this is good advice if you're in this particular situation, but maybe not for everybody.

And really the truth is I, I try not to give advice these days because like advice is dangerous stuff for that very reason.

[00:03:28] **Jeremy:** so, so when you mentioned you try not to give advice and you have this book, the complete guide to rails testing, would you not describe what's in the book as advice? I'm kind of curious what the distinction is there.

[00:03:42] **Jason:** Yeah, Jeremy, right after I said that, I'm like, what am I talking about? I give all kinds of advice. So forget, I said that I totally give advice. But maybe not in certain things like like business advice or anything like that. I do give a lot of advice around testing and various programming things.

So, yeah, ignore that part of what I said.

[00:04:03] **Jeremy:** something that I found a little bit unique about rails testing was that a lot of the tests are centered around I guess you could call it like a full integration test, right? Because I noticed when working with rails, if I write a test, a lot of times it's talking to the database, it's talking to if, if I.

Have an API or I have a website it's actually talking to the API. So it's actually going through all the layers and spinning up a database and all that. And I wonder if you, you knew how that work, like each time you run a test, is it creating a new database? So that each test is isolated or how does all that stuff actually work?

[00:04:51] **Jason:** Yeah, good question. First. I want to mention something about terminology. So I think one of the most important things for somebody who's new to testing to learn is that in our industry, we don't have a consensus around terminology. So what you call an integration test might be different from what I call an integration test.

The thing you just described as an integration test, I might call an acceptance test. Although I happen to also call it an integration test cause I use that terminology too, but I just wanted to give that little asterisk for the listener, because if they're like, wait, I thought an integration test was this.

And not that anyway, you asked how does that work? So. It is true that with those types of rails tests, and just to add more terminology into the mix, they call those system tests or system specs, depending on what framework you're using. But those are the tests that actually instantiate a browser and simulating user input, exercise, the UI of the application.

And those are the kinds of tests that like show you that everything works together. And mechanically how that works. One layer of it is that each test runs in a database transaction. So when you, you know, in order to run a certain test, maybe you need certain records like a user. And then I don't know if it's a scheduling test, you might need to create an appointment and whatever. All those records that you create specifically for that test that's happening inside of a database transaction. And then at the end of the test, the transaction is aborted. So that none of the data you create during the test actually gets persisted to the database. then regarding the whole database, it's not actually like creating a new database instance at the start of each test and then blowing it away.

It's still the same database instance is just the data inside of each test is not being persisted at. 

[00:07:05] **Jeremy:** Okay. So when you run. What you would call, I guess you called it an acceptance test, right? Where it's going, it's opening up your website, it's clicking through the website, creating records, things like that. That's happening in a database instance that's created for, I guess, for all your tests that all your tests get to reuse and rails is automatically wrapping your test in a transaction.

So even if you're doing five or 10 database queries at the end of all, that they all get rolled back because they're all within the same transaction.

[00:07:46] **Jason:** Exactly. And the reason why we want to do that. Is because of a testing principle that you want your tests to be runnable in any order. And the key thing is you want your tests to be deterministic. So deterministic means that the starting state determines the in-state and it's the same every time, no matter what.

So if you have tests a, B and C, it shouldn't be the case that you can run them in the order, ABC, and they all pass. But if you do it CBA, then test a fails because it should only fail. If something's actually wrong, it shouldn't fail for some other reason, like the order in which you run the tests. And so to ensure that property of deterministic newness we need to make it so that each test doesn't leak into the other tests.

Cause imagine if that. Database transaction. thing didn't happen. And it's, it's only incidental that that's achieved via database transactions. It could conceivably be achieved some other way. That's just how this happens to work in this particular case. But imagine if no measure was taken to clean up afterward and I, I ran a test and it generated an appointment.

And then the test that runs after that does some tests that involves like doing a count of appointments or something like that. And maybe like, coincidentally, my second test passes because I've always run the tests in a certain order. and so unbeknownst to me, test B only passes because of what I did in test a that's bad because now the thing that's happening is different from what I think is happening.

And then if it flipped and when we ran it, test B and then test a. It wouldn't work anymore. So that's why we make each test isolated. So it can be deterministic.

[00:09:51] **Jeremy:** and I wonder if you've worked with any other frameworks or any other languages, and if you found that the approaches and those frameworks or languages is similar to rails, like where it creates these, the transaction for you, does the rollback for you and all of that.

[00:10:08] **Jason:** Good question. I have to plead ignorance. I've dabbled a little bit in testing and some other languages or frameworks, but not enough to be able to say anything smart about it. 

[00:10:22] **Jeremy:** Yeah, I mean in my experience and of course there are many different frameworks that I'm not familiar with, but in a lot of cases, I I've seen that they don't have this kind of behavior built in, like, they'll provide you a way to test your application, but it's up to you if you want to write code that will wrap everything in a transaction or create a new database instance per test, things like that.

That's all left up to you. so I, I think it's interesting that that rails makes that decision for you and makes it to where you don't really have to think about that or make that decision. And for me personally, I found that really helpful.

[00:11:09] **Jason:** Yeah, it's really nice. It's a decision that not everybody is going to be on board with. And by that decision, I mean the general decision of rails to make a lot of decisions for you. And it may not be the case that I agree with every single decision that rails has made, but I do appreciate that that the rails team or DHH, or whoever has decided that rails is just going to have all these sensible defaults.

And that's what you get. And if you want to go tweak that stuff, I guess you can, but you get all this stuff this way. Cause we decided what we think is the best way to do it. And that is how most people use their, their rails apps. I think it's great. It eliminates a lot of overhead and then. Use some other technologies, I've done some JavaScript stuff and it's just astonishing how much boiler plate and how many, how much energy I have to expend on decisions that don't really matter.

And maybe frankly, decisions that I'm not all that equipped to make, because I don't have the requisite knowledge to be able to make those decisions. And usually I'd rather just have somebody else make those decisions for me. 

[00:12:27] **Jeremy:** we've been talking about the more high level tests, the acceptance tests, the integration tests. And when you're choosing on how to test something, how do you decide whether it should be tested that, that level, or if it should be more of a unit level tests, something, something smaller

[00:12:49] **Jason:** Good question. So I want to zoom out just a little bit in order to answer that question and come at it from a distance. So I recently conducted some interviews for a programmer job. I interviewed about 25 candidates, most of those candidates. Okay. And the first step of the interview was this technical coding exercise. most of the candidates did not pass. And maybe, I don't know. Five or six or seven of the candidates out of those 25 did pass. I thought it was really interesting. The ones who failed all failed in the same way and the ones who passed all passed in the same way. And I thought about what exactly is the difference.

And the difference was that the programmers who passed, they coded in feedback loops. So I'll say that a different way, the ones who failed, they tried to write their whole program at once and they would spend 15, 20 minutes carefully writing the program. And then at the end of that 20 minutes, they would try to run it.

And unsurprisingly to me the program would fail like on line 2 of 30, because nobody's smart enough to write that much code and have the whole thing work. And then the ones who did well. They would write maybe one line of code, run it, observe what happens, compare what they observed to what they expected to see, and if any corrections were needed, they made those corrections and ran it again.

And then only once their expectations were satisfied, did they go and write a second line and they would re repeat that process again, that workflow of programming and feedback loops I think is super important. And I think it's what distinguishes, Hmm. I don't exactly want to say successful programmers from unsuccessful programmers, but there's certainly a lot to do with speed.

like, think about how much slower it is to try to write your whole program, run it and see that it fails. And then try to find the needle in the haystack. It's like, okay, I just wrote 30 lines. There's a problem somewhere. I don't know where, and now I have to dig through and find it It's so much harder than if you just write one line and you see a problem and you know, that, that problem lines in that line, you just wrote.

So I say all that, because testing is just feedback loops automated. So rather than writing a line and then manually running your program and using your own judgment to compare what you observed to what you expected to see you write a test that exercises your code and says, I expect to see this when this happens.

And so the kind of test you write now to answer your question will depend first on the nature of the thing you're writing. But for like, if we take kind of the like typical case of, let's say I'm building a form that will allow me to create a customer in a system. And I put in the first name, last name and email address of the customer. that's a really basic like crud functionality thing. There's not a lot of complexity there. And so I am, to be honest, I might just not write a test at all and we can get into how I decide when to write a test and when not to, but I probably would write a test. And if I did, I would write a system spec to use the rails are spec terminology that spins up a browser.

I would fill in the first name field with a first name, fill in the last name field with the last name, email, with email click, the submit button. And then I would assert that on the subsequent page, I see some indicator of success. And then if we think about something that. Maybe more involved, like I'm thinking about some of the complicated stuff I've been working on recently regarding um, coming up with a patient's balance in the medical system that I work on.

That's a case where I'm not going to spin up a browser to check the correctness of a number. Cause that feels like a mismatch. I'm going to work at a lower level and maybe create some database records and say, when I, when I created this charge and when I create this payment, I expect the remaining balance to be such and such.

So the type of test I write depends highly on the kind of functionality.

[00:17:36] **Jeremy:** So it sounds like in the case of something that's more straight forward, you might write a high level test, I guess, where you were saying I just click this button and I see if the thing I expected to be created is there on the next page. And you might create that test from the start and then just start filling in the code and continually running that test you know, until it passes.

But you also mentioned that in the case of something simple like that, you might actually. Choose to forego the tests and just take a look you know, visually you open the app and you click that same button and you can see the same result. So I wonder if you could talk a little bit more about how you decide, like, yeah, I'm going to write this test or no, I'm just going to inspect a visually

[00:18:28] **Jason:** Yeah. So real quick before I answer that, I want to say that it's, it's not one of the tests is straightforward or the feature is straightforward that determines which kind of test I write, because sometimes the acceptance test that I write, which spins up a browser and everything. Sometimes that might be quite an involved test and in complicated feature, or sometimes I might write a lower level test and it's a trivially simple one.

It has more to do with um, What's, what's the thing that I care about. Like, is it primarily like a UI based feature that, that is like the meat of it? Or is it like a, a lower level, like calculation type thing or something like that? That's kind of what determines which kind of right. But you asked when would I decide not to write a test.

So the reason I write tests is because it's just like cost prohibitive to manually perform testing, not just in monetary terms, but like in emotional pain and mental energy and stuff like that. I don't want to go back and manually test everything to make sure that it's still working. And so the ROI on writing automated tests is almost always positive, but sometimes it's not a positive ROI.

And so when I don't write it down, It's if these conditions are true, if the cost of that feature braking is extremely low. And if the I'll put that if, if the consequences of the feature breaking are really small and the frequency of the usage is low and the cost of writing the test is high, then I probably won't write a test.

For example, if there's some report that somebody looks at once every six months and it's like some like maybe a front desk person who uses the feature and if it doesn't work, then it means they have to instead go get the answer manually. And instead of getting the answer in 30 seconds, it takes them five.

Extremely low cost to the failure. And it's like, okay, so I'm costing somebody, maybe 20 bucks once every six months, if this feature breaks. And let's say this test is one that would take like an hour for me to write. Clearly it's better just to accept the risk of that feature breaking once in a while, which it's probably not going to anyway. So those are the questions I ask when I decide and, and to, to be clear, it's not like I run through all those questions for every single test I write in the vast, vast majority of cases. I just write the test because it's a no-brainer that it's, that it's better to write the test, but sometimes my instincts tell me like, Hey, is this really actually important to write a test for?

And when I find myself asking that, then I say, okay, what's the consequences of the breakage? How hard is this test to write all that. 

[00:21:46] **Jeremy:** So you talked about the consequences being low, but you also talked about maybe the time to write the test being high. What are the types of tasks that, that take a long time to write?

[00:21:58] **Jason:** Usually ones that involve a lot of setup. So pretty much every test requires some data to be in place data, either meaning database, data, or like some object structure or something like that. Sometimes it's really easy sometimes to set up is extremely complicated. and that's usually where the cost comes in.

And then sometimes, sometimes you encounter like a technical challenge, like, oh, how do I like download this file? And then like inspect the contents of this file. Like sometimes you just encounter something that's like technically tricky to achieve. But more frequently when a test is hard to write it's because of the setup is hard.

[00:22:49] **Jeremy:** and you're talking about set up being, you need to insert a whole bunch of different rows into your database or different things that interact with one, another things like that.

[00:23:02] **Jason:** Exactly. 

[00:23:03] **Jeremy:** when you're testing a system and you create a database that has all these items in it for you to work with, I'm assuming that what's in your test database is much smaller than what's in the real database. So how do you get something that's representative so that if you only have 10 things in your tasks, but in production, there's thousands of them that you can catch that, Hey, this isn't going to work well, once it gets to production,

[00:23:35] **Jason:** Yeah. that's a really interesting question. And the answers that I don't like, I usually don't try to make the test beta test database representative of the production database in terms of scale, obviously like the right data has to be there in order to exercise the test that it has to be true. But I don't, for example, in production at this moment I know there's some tens of thousands of appointments in the database, but locally at any given time, there are between zero and three or, or So appointments in any particular test, that's obviously nowhere near realistic, but it's only becomes relevant in a great, great minority of cases with, with regard to that stuff, the way I approach that is rather to So I'm thinking about some of those through the, for the first time right now, but obviously with performance in general premature optimization is usually not a profitable endeavor. And so I'll write features without any thought toward performance. And then once things are out there and perform it in production observe the bottlenecks and then fix the bottlenecks, starting with what's the highest ROI.

And usually tests haven't come into the picture for me. It's cause like, okay. The reason for tests again is, so you don't have to go back and do that manual testing, but with these performance improvements, instead of tests, we have like application performance monitoring tools, and that's what tells me whether something needs an issue or people just say like, Hey, this certain page is slow or whatever.

And so tests would be like redundant to those other measures that we have that tell us if there's performance.

[00:25:38] **Jeremy:** Yeah. So that sorta touches on what you described before, where let's say you were writing some kind of report or adding a report and when you were testing it locally, it worked great generated the report. Uh, Then you pushed it out to production. Somebody went to run it and maybe because of an indexing problem or some other issue It times out, or it doesn't complete takes a long time, but I guess what you're saying is in a lot of cases, the, the consequences of that are not all that high.

Like the person will try it. They'll see like, Hey, it doesn't work. Either you'll get a notification or they'll let you know, and then that's when you go in and go like, okay, now, now we can fix this.

[00:26:30] **Jason:** Yeah. And I think like the distinction is the performance aspect of it. Because like with a lot of stuff, you know, if you don't have any tests in your application at all, there's a high potential for like silent failure. And so with the performance stuff, we have other ways of ensuring that there won't be silent failure.

So that's how I think about that particular.

[00:26:56] **Jeremy:** I guess another thing about tests is when you build an application, a lot of times you're not just interacting with your own database, you're interacting with third-party APIs. You may even be connecting to different pieces of hardware, things like that. So when you're writing a test, how do you choose to approach that?

[00:27:23] **Jason:** yeah, good question. This is an area where I don't have a lot of personal experience, but I do have some there's another principle in testing that is part of the determinism principle where you don't want to involve external HTTP requests and stuff like that in your tests. Because imagine if I run my test today, And it passes, but then I run my test tomorrow and this third-party API is down and my test fails the behavior of my program didn't change. The only thing that's different is this external API is down right now. And so what I do for, for those is I'll capture the response that I get from the API. And I'll usually somehow um, get my hands on a success response and a failure response and whatever kind of response I want to account for.

And then I'll insert those captured responses into my tests. So that then on every subsequent run, I can be using these canned values rather than hitting the real API.

[00:28:37] **Jeremy:** I think in your um, the description of your book, you mentioned a section on, on stubs and mocks, and I wonder what you're describing here, which of those two things, is it? And what's the difference?

[00:28:53] **Jason:** Yeah. it's such a tricky concept And I don't even trust myself to say it right every time that I want to remind myself of the difference between mocks and stubs. I have to go back to my own blog posts that I wrote on it and remind myself, okay, what is the difference between a mock and a stub? And I'll just say, I don't remember.

Because this isn't something that I find myself dealing with very frequently. It's something that people always want to know about at least in the rails world. But I'll speak for myself at least. I don't find myself having to use or wanting to use mocks and stubs very much.

I will say that both mocks and stubs are a form of a testable. So a mock is a testable and a stub is a testable and a testable. It's like a play on stunt double instead of using a real object or whatever it is, you have this fake object. And sometimes that can be used to like trick your program into behaving a certain way or it can be used to um, gain visibility into an area that you otherwise wouldn't have visibility into.

And kind of my main use case for mocks and stubs when I do use them, is that when you're testing a particular thing, You want to test the thing you're interested in testing. You don't want to have to involve all the dependencies of the thing you're testing. And so I will like stub out the dependencies.

So, okay. Here's an example. I have a rare usage of stubs in my, in my uh, test suite and dear listener. I'm going to use the word stub. Don't give too much credence to that. Maybe. I mean, mock, I don't remember. But anyway, I have this area where we determine a patient's eligibility to get a certain kind of medicine and there's a ton that goes into it and there's all these, like, there's, there's these four different, like coarse-grained determinations and they all have to be a yes in order for it to overall be a yes.

That they can get this medicine. It has to do with mostly insurance. And then each one of those four core course grain determinations has some number of fine grain determinations that determines whether it is a yes or a no. If I weren't using mocks and stubs in these tests, then in order to test one determination, I would have to set up the conditions.

This goes back to the setup, work stuff we talked about. I'd have to set up all the conditions for the medicine to be a yes. In addition to, to the thing I'm actually interested in. And so that's a waste because that stuff is all irrelevant to my current concern. Let me try to speak a little bit more concretely.

So let's say I have determinations ABC. When I'm interested in determination, a I don't want to have to do all the setup work for determinations, B, C, and D. And so what I'll do is I'll mock the determinations for B, C and D. And I'll say for B, just have the function returned true for C same thing, just return true for D return.

True. So it'd like short circuits, all that stuff and bypasses the actual logic that gives me the yes, no determination. And it just always gives me a yes. That way. There's no setup work for B, C, and D. And I can focus only on.

[00:32:48] **Jeremy:** And I think it may be hard to say in this example, but would you, would you still have at least one test that would run through and do all the setup, do the checks for ABC and D and then when you're doing more specific things start to put in doubles for the others, or would you actually just never have a full test that actually did the complete setup?

[00:33:14] **Jason:** well, here's how I'm doing this one. I described the scenario where I'm like thoroughly testing a under many different conditions, but stubbing out B, C and D. They don't have another set of tests where I thoroughly test B and stub out a C and D. And so on. I have one thorough set for, for each of those. If you're asking whether I have one that like exercises, all four of them, No.

I just have ones for each of the four individually, which is maybe kind of a trade off. Cause it's arguable that I don't have complete confidence because I'm never testing the four together. But in the like trade off of like setup?

work and all that, that's necessary to get that complete con confidence and the value of that, like additional, because really it's just like a tiny bit of additional con confidence that I would get from testing all those things together.

In that particular case, my judgment was that that was not worth 

[00:34:19] **Jeremy:** yeah. Cause I was thinking from their perspective of sometimes I hear that people will have a acceptance test that covers sometimes you hear people call it the happy path, right. Where they everything lines up. It's like a very straightforward case of a feature. But then all the different ways that you can test that feature, they don't necessarily write tests for those, but they just write one for the, the base case.

And then, like you said, you actually drill down into more specifics and maybe only test a, a smaller part there, but it sounds like in this case, maybe you made the decision that, Hey, doing a test, that's going to test all four of these things, even in the simplest case is going to involve so much setup and so much work that, that maybe it's not, not worth it in this case.

[00:35:13] **Jason:** Yeah. And I'd have to go back and refresh my memory as to like what exactly this scenario is for those tasks. Because in general, I'm a proponent of having integration tests that makes sure multiple things work together. Okay. You might've seen that Gif where it says like um, two unit tests, zero integration tests, and there's like a cabinet with two doors.

Each door can open on its own or, or maybe it's drawers. Each drawer can open on its own, but you can't open both drawers at the same time. And so I think that's not smart to have only unit tests and no integration tests. And so I don't remember exactly why I chose to do that eligibility test with the ABC and D the way I did.

Maybe it was just cost-prohibitive to do it altogether. Um, One thing that I want to want to comment on regarding mocks and stubs, there's a mistake that's made kind of frequently where people overdo it with mocks and stuff. They misunderstand the purpose. The purpose again is that you want to test the thing you're testing, not the dependencies of the thing.

But sometimes people step out the very thing they're testing. And so they'll like assert that a certain method will return such and such value, but they'll stub the method they're testing so that the method is guaranteed to return the same value and that doesn't actually test anything. So I just wanted to make, mention that as a common mistake to avoid 

[00:36:47] **Jeremy:** I wonder if you could maybe give an example of when you, you have a certain feature and the thought process you're going through where you decide like, yes, this is the part that I should have a stub or a mock for. And this is the part where I definitely need to make sure I run the code.

[00:37:07] **Jason:** Well, again, it's very rare that I will use a mocker stub and it's not common that I'll even consider it for better or worse. Like we're talking about. The nature of rails tests is that we spin up actual database records and, and test our models with database data and stuff like that. In other ecosystems, maybe the testing culture is different and there's more mocks and stubs.

I know when I was doing some coding with angular, there was a lot more mocking and stubbing. But with rails, it's kind of like everything's available all the time and we use the database a lot during testing. And so mocks and stubs don't really come into the picture too much. 

[00:37:56] **Jeremy:** Yeah. It's, it's interesting that you, you mentioned that because like I work with some projects that use C-sharp and asp.net, and you'll a lot of times you'll see people say like you should not be talking to the database in your tests. And you know, they go through all this work to probably the equivalent of a mock or a stub.

But then, you know, when I, when I think about that, then I go like, well, but I'm not really testing how the database is going to react. You know, are my, are my queries actually valid. Things like that, because all this stuff is, is just not being run. in some other communities, maybe they're they have different ideas, I guess, about, about how to run tests.

[00:38:44] **Jason:** Yeah, And it's always interesting to hear expressions. Like you should do this or you shouldn't do that, or it's good to do this. It's bad to do that. And I think maybe that's not quite the right way to think about it. It's more like, well, if I do this, what are the costs and benefits of doing this? Cause it's like, nothing exactly is a good thing to do or a bad thing to do.

It's just, if you do this, this will happen as a consequence. And if you don't this won't and all that stuff. So people who don't want to talk to the database in their tests, why is that? What, what are the bad things they think will happen if you do that? The drawbacks is it appears to me are it's slow to use the database in any performance problem.

Usually the culprit is the database. That's always the first thing I look at. And if you're involving the database and all of your tests, your tests are going to be much slower than if you don't use the database, but the costs of not talking to the database are exactly what you said, where you're like, you're not exercising your real application, you're missing an entire layer and maybe that's fine.

I've never tried approaching testing in that way. And I would love to like, get some experience like working with some people who do it that way. Cause I can't say that I know for an absolute fact that that doesn't work out. But to me it just makes sense to exercise everything that you're actually using when the app runs.

[00:40:18] **Jeremy:** what's challenging probably for a lot of people is that if you look online for how to do testing in lots of different frameworks, you'll get different answers. Right. And it's not clear what's gonna fit your situation right? And you know, to, to give an example of, we've been talking about how rails will it, it predominantly focuses on tests that, that talks to the database and it wraps everything in a transaction as we talked about before, so that you can reset the state and things like that.

I've also seen in other frameworks where they'll say like, oh, you can run a database test, but you use this in-memory version of the database instead of actually talking to a real MySQL or Postgres instance, or they'll say, oh, for this test we're going to use SQLite in place of the Postgres database you're actually using in production.

And it, it makes the, the setup, I suppose, easier. Um, And maybe it makes the tests run quicker, but then it's also no longer the same as what you're really running. So there's like a lot of different approaches that, that people describe and take. And I think it can be hard for, for people to know, like what, what makes sense for me.

[00:41:42] **Jason:** Yeah. And this is another area where I have to plead ignorance because again, I don't have experience doing it the other way. Logically, I feel like my way makes sense, but I don't have empirical experience doing it the other way. 

[00:41:57] **Jeremy:** we've talked a little bit about how there's cases where you'll say I'm not going to do this thing because it's going to take a lot of time and I've weighed the benefits. And I wonder if you could give some examples of things where you spent a lot of time on something, and then in hindsight, you, you realize like this really wasn't worth it.

[00:42:18] **Jason:** I don't think I have any examples of that because I don't think it tends to happen very much. I really can't emphasize enough how old, the case where I choose not to write a test for something is like a one in 5,000 kind of thing. It's really not something I do frequently. The mistake is overwhelmingly in the opposite direction.

Like somebody may, maybe I will get lazy and I'll skip a test and then I'll realize, oh yeah, This is why I write tests because it actually makes everything easier. And uh, we get pain as as a consequence when we skip tests. So that's usually the mistake I make is not writing a test when I should, rather than writing a test when I should not have 

[00:43:08] **Jeremy:** So since then, in general, you, you said that not writing it is, is the, the mistake. How do you get people in the habit of. Of writing the tests where they feel like it's not this thing that's slowing them down or is in the way, but is rather something that's helping them with that feedback loop and is something that they actively want to do.

[00:43:33] **Jason:** Yeah. So to me, it's all about a mindset. So there's a common perception that tests are something extra. Like I've heard stories about, like somebody gives a quote for a project and then the prospective client asks like, well, how much, if we skip tests, how much less would that be? And it's like, oh, it wouldn't be less.

It'd be like five times more because tests are a time saver. So I want to try to dispel with that notion. But even so it can be hard to bring oneself, to write task because it feels like something that takes discipline. But in my case, I don't feel like it takes discipline. Because I remind myself of a true fact that it's actually the lazy and easy way to code is to code using tests.

And it's the harder, more laborious way to write code. Not using tests because think about what's, what's the alternative to not writing tests. Like we said earlier, the alternative is to manually test everything. And that's just so painful, especially when it's some feature where like, I'm sure you have experience with this, Jeremy, you, you make a code change.

And then in order to verify that the thing still works, you have to go through like nine different steps in the browser. And only on that last step, do you get that answer you're after. That's just so painful. And if you write a test, you can automate that. Some things that might present friction in that process, or just like a lack of familiarity with how to write tests and maybe a um, a lack of an easy process for writing tests.

And just to briefly touch on that, I think something that can help reduce that. Is to write tests in the same way that I write code in feedback loops. So we talked about writing one line, checking, writing, another line, checking that kind of thing. I write my tests in the same way. First I'll write the shell of the test and then I'll run just the shell, even though it seems kind of dumb to just run the shell cause you know, it doesn't do anything. I do that just to demonstrate to myself that I didn't like make some typo or something like that. I'm starting from like a clean baseline. And then I'll write one line of my test. Maybe if I'm writing a system spec, I'll write a line that creates a user of rum that I know that nothing's going to happen when I run the test, but I'll run it just to see it run and make sure there's no errors.

And then I'll add a line that says, log the user in and then I'll run that. And so on just one line at a time. There's this principle that I think is really useful when working, which is to separate the deciding what to do from the actually doing it. I think a lot of developers mixed those two jobs of deciding what to do and doing it in the same step.

But if, if you separate those, so you'd like, decide what you're going to have your tests do. And then after that, so like maybe I'll open my test and I'll write in comments what I want to achieve, not in technical terms necessarily, but I'll just write a comment that says, create a user, right? Another comment that says, log in another comment that says, click on such and such.

And then once I have those, there, I'll go back to that first line and convert that to code. Okay. My comment that says, create a user, I'll change that to the syntax that actually creates a user and again, using the feedback loop. So I'll run that so that I can, you know, once I'm, once I'm done writing all those comments that say what the test does, I'm now free to forget about it.

And I don't have to hold that in my mental Ram anymore. And I can clear my mental RAM. Now all my mental RAM is available to bring, to bear on the task of converting my steps that I already decided into working syntax. If you try to do both those things at the same time, it's more than twice as hard. And so that's why I try to separate.

[00:48:04] **Jeremy:** So that's interesting. So it's like you're designing, I guess, the feature, what you want to build in the context of the test first it's would that be accurate?

[00:48:19] **Jason:** that certainly can be the case. So much of this is context dependent. I very regularly give my self permission to be undisciplined and to go on exploratory spikes. And so if I have like very, if I have a really vague idea about what shape a feature is going to take, I give myself permission to forget about tests and I just write some code and I feel cause there's two reasons to write code.

You know, a code is not only a work product code is also a thinking. so I would let go into a different mode, I'll say, okay, I'm not trying to create a work product right now. I'm just using code as a thinking medium, to figure out what I'm even going to do. So that's what I'll do in that case. And then maybe I'll write the test afterward, but if it's very clear, what the thing is that I'm going to write, then I'll often write the test first again, in those two phases of deciding what it's going to be and the deciding how it works.

And I won't do a thing where, where, like I write 10 test cases and then I go through one by one and write code to make them pass. Usually I'll write one test, make a pass, write a second test, make it pass and so on. 

[00:49:38] **Jeremy:** okay. So the more exploratory aspect, I guess, would be when. You're either doing something that you haven't done before, or it's not clear to you what the features should be is, is that right?

[00:49:58] **Jason:** Yeah, like maybe it's a feature that involves a lot of details. There's like a lot of room for discretion. It could be implemented in more than one way. Like how would I write a test for that? If I don't even know what form it's going to take? Like there's decisions to be made, like, what is the, the route going to be that I visit for this feature?

What am I even going to call like this entity and that entity and stuff like that. And I think that goes back to my desire to not juggle and manage. Multiple jobs at the same time. I don't want to, I don't want to overly mix the design job with the testing job. Cause testing can help with design, but design in like a code structure sense.

I usually don't want to mix testing with like UI design and not even UI design, like, like design in the highest sense. Meaning like what even is this thing? How does it work? Big picture wise and stuff like that. That's not the kind of design that testing helps with in my mind of the kind of design that testing helps with again, is the code structure.

So I want to have my big picture design out of the way before I start writing my test. 

[00:51:21] **Jeremy:** and in terms of the big picture design, is that something that you keep all in your head or are you writing that down somewhere? I'm just wondering what your process is.

[00:51:34] **Jason:** Yeah, it can work a number of different ways in the past. I've done usability testing where I will do some uh, pen and paper prototypes and then do some usability testing with, with users. And then I will um, convert those pen and paper prototypes to something on the computer. The idea being pen and paper prototypes are the cheapest to create and change.

And then the more you cement it, the more expensive it gets to change. So only once I'm fairly certain that the pen and paper prototypes are right. Will I put it into something that's more of a formal mock. And then once I have my formal mock-up and that's been through whatever scrutiny I want to put it through, then I will do the even more expensive step of implementing that as a working feature.

Now having said all that, I very rarely do I go through all that ceremony. Sometimes a feature, usually a feature is sufficiently small, that all that stuff would be silly to do. So sometimes I'll start straight with the the mock-up on the computer and then I'll work off of that. Sometimes it's small enough that I'll just make a few notes in a note-taking program and then work off of that.

What is usually true is that our tickets in our ticketing system have a bulleted list of acceptance criteria. So we want to make it very black and white. Very yes, no. Whether a particular thing is done and that's super helpful because again, it goes back to the mixing of jobs and separating of jobs.

If we've decided in advance that this feature needs to do these four things. And if it does those four things it's done and it doesn't need to do anything more and if it doesn't meet those four criteria, then it's not done then building the thing is just a matter of following the instructions. Very little thinking is involved.

[00:53:45] **Jeremy:** depending on the scope of the feature, depending on how much information you have uh, you could either do something elaborate, I suppose, where, you know, you were talking about doing prototypes or sketches and, and so on before you even look at code or there could be something that's not quite that complicated where you have an idea of what it is and you might even play with code a little bit to get a sense of where it should go and how it should work.

But it's all sort of in service of getting to the point where you know enough about how you're going to do the implementation and you know enough about what the actual feature is to where you're comfortable starting to write steps in the test about like, these are the things that are going to happen.

[00:54:35] **Jason:** Yeah. And another key thing that might not be obvious is that all these things are small. So I never work well, I shouldn't say never, but in general, I, don't work in a feature. That's going to be like a week long feature or something like that. We try to break them down into features that are at most like half.

And so that makes all that stuff a lot easier. Like I use the number four as an example of how many acceptance criteria there might be. And that's a pretty representative example. We don't have tickets where there's 16 acceptance criteria because the bigger something is the more opportunity there is for the conceive design to turn out, not to be viable.

And the more decisions that can't be made, because you don't know the later step until the earlier decision is made and all that kind of stuff. So the small size of everything helps a lot.

[00:55:36] **Jeremy:** but I, I would imagine if you're breaking things into that small of a piece, then would there be parts that. You build and you tasked and you deploy, but to the user, they actually don't see anything. Is that the appraoch?

[00:55:52] **Jason:** definitely, we use feature flags. Like for example, there's this feature we're working on right now, where we have a page where you can see a long list of items. The items are of several different types right now. You just see all of them all the time, but depending on who you are and what your role is in the organization, you're not going to be interested in all those things.

And so we want people to be able to have check boxes for each of those types to show or hide those things. Whereas checkbox feature is actually really big and difficult to add. And so the first thing that I chose to do was to have us add just one single check box for one type. And even that one, single checkbox is sufficiently hard that we're not even giving people that yet.

We coded it so that you get the check boxes and that one checkbox is selected by default. When you uncheck it, the thing goes away, but it's selected by default so that we can feature flag that. So the checkbox UI is hidden. Everything looks just the way it did before. And now we can wait until this feature is totally done before we actually surface it to users.

So it's the idea of making a distinction between deployment and release. Cause if we try to do this whole big thing, it's, it's gonna take weeks. If we try to do the whole thing, that's just too much risk for something to go wrong. And then like, we're going to deploy like three weeks of work at once.

That's like asking for trouble. So I'm a huge fan of feature flags. 

[00:57:35] **Jeremy:** Interesting. So it's like the, it's almost like the foundation of the feature is going in. And if you were to show it to the user well, I guess in this case, it actually did have a function right at you. You could filter by that one category. 

[00:57:52] **Jason:** oh, I was just going to say you're exactly right. It wouldn't be a particularly impressive or useful feature, but what we have is complete it's it's not finished, but it is complete. 

[00:58:06] **Jeremy:** I'm not sure if you have any examples of this, but I imagine that there are changes that are large enough that I'm not sure how you would split it up until you, you mentioned like half a days worth of time. And I, I wonder if either have examples of features like that or a general sense of how, what do you do if you, you can't figure out a way to split it up that small.

[00:58:34] **Jason:** I have yet to encounter a feature that we haven't been able to break up into pieces that are that small. So, unfortunately, I can't really say anything more than that because I just don't have any examples of exceptions 

[00:58:49] **Jeremy:** For, for people listening, maybe that should be a goal at least like, see if you can make everything smaller, see if you can ship as little as possible, you know, maybe you don't hit that half a day mark, but at least give it a, give it a try and see what you can do.

[00:59:10] **Jason:** yeah. And the way I care would characterize it, maybe wouldn't be to ship as little as possible at a time, but to give a certain limit that you try not to go over. And it's, it's a skill that I think can be improved with practice. You learn certain techniques that you can use over and over. Like for example, one way that I split things up sometimes is we will add the database tables in one chunk. And we'll just deploy that, cause that presents a certain amount of risk, you know, when you're adding database tables or columns or anything like that, like it's always risky when you're messing with the structure of the database. So I like to do just that by itself. And it's kind of tidy most of the time because because it's not something that's like naturally visible to the user is just a structural change.

So that's an example of the kind of thing that you learn as you gain practice, breaking bigger things up into smaller pieces. 

[01:00:16] **Jeremy:** so, and, and that example, in terms of whatever issue tracking system you use, what, what would you call that? Would you just call that setting up schema for X future features, or I'm just kinda curious how you characterize that.

[01:00:35] **Jason:** yeah, something like that. Those particular tickets don't have great names because ideally each ticket has some amount of value that's visible to the user and that one totally doesn't, it's a purely nuts and bolts kind of thing. So that's just a case where the name's not going to be great, but what's the alternative can't think of anything better. So we do it like that. 

[01:01:02] **Jeremy:** you feel like that's, that's lower risk shipping something that's not user-facing first. Then it is to wait until you have at least like one small thing that, you know, is connected to that change.

[01:01:19] **Jason:** Yeah. I had a boss in the past who had a certain conception of the reason to do deployments. And, and her belief was that the reason that you deploy is to deliver value to the user which is of course true, but there's another really good reason to deploy, which is to mitigate risk. The further production and development are able to diverge from one another, the greater, the risk.

When you do a deployment. I remember one particular time at that job, I was made to deploy like three months of work at once and it was a disaster and I got the blame because I was the one who did the work. And quite frankly, I was really resentful that that had. And that's part of what informs my preference for deploying small amounts of work at a time.

I think it's best if things can be deployed serially, like rather than deploying in patches, just finish one thing, deploy it, verify it, finish the next thing, deploy it, verify it. I have the saying that it's better to be a hundred percent done with half your work than halfway done with a hundred percent of your work. For, for the hopefully obvious reason that like, if, if you have 15 things that are each halfway in progress, now you have to juggle 15 balls in your head. Whereas, if you have 15 things you have to do, and then you finish seven of them, then you can completely forget about those seven things that you finished and deployed and verified and all that.

And your mental bandwidth is freed up just to focus on the remaining work. 

[01:03:10] **Jeremy:** yeah, that, that makes sense. And, and also if you are putting things out bit by bit, And something goes wrong, then at least it's not all 15 things you have to figure out, which was it. It's just the last thing he pushed out.

[01:03:26] **Jason:** Exactly. Yeah. It's never fun when you deploy a big delta and something goes wrong and it's a mystery. What introduced the problem? It's obviously never good if you deploy something that turns out to be a problem, but if you deployed just one thing and something goes wrong, at least you can. Roll it back or at the very least have a pretty decent idea of where the problem lies. So you can address it quickly. 

[01:03:56] **Jeremy:** for sure. Well I think that's probably a good place to leave it off on, but is there anything else about testing or just software in general that you, you thought we should've brought up?

[01:04:09] **Jason:** Well, maybe if I can leave the listener with one thing um, I want to emphasize the importance of programming and feedback loops. It was a real eye-opener for me when I was interviewing these candidates to notice the distinct difference between programmers, who didn't program and feedback loops and programmers, who do I have a post about it?

I'm just, it's just called how to program and feedback loops. I believe if anybody's interested in the details. Cause I have like. It's like seven steps to that feedback loop. First, you write a line of code, then you do this. I don't remember all seven steps off the top of my head, but it's all there in the blog post.

Anyway, if I could give just one piece of advice to anybody who's getting into programming, it's a program in feedback loops. 

[01:05:00] **Jeremy:** yeah, I think that's been the, the common thread, I suppose, throughout this conversation is that whether it's. Writing the features you want them to be as small as possible. So you get that feedback of it being done. And like you said, taking it off of your plate. Then there's the being able to have the tests there as you write the features so that you get that immediate feedback, that this is not doing what the test says it should be doing.

So yeah, it makes it, it makes a lot of sense that basically in everything we do try to get to a point where we get a thumbs up, we get at, this is complete. The faster we can do that, the better we'll we'll all be off. Right.

[01:05:46] **Jason:** exactly. Exactly. 

[01:05:50] **Jeremy:** if people want to check out your book, check out your podcast, I think you even have a, a conference coming up, right? Uh, where, w where can they learn about that.

[01:06:02] **Jason:** So the hub for everything is code with jason.com. So that's where I always. Send people, you can find my blog, my podcast, my book there. And yeah, my conference it's called sin city ruby. It's a Ruby conference. This will only be applicable dear listener, if you're listening before March 24th, 2022. But yeah, it's, it's happening in Las Vegas.

It's going to be just a small intimate conference and it's a whole different story, but I kind of put on this conference accidentally. I didn't intend to do a conference. I just kind of uh, stumbled into it, but I think it will be a lot of fun. But yeah, that's, that's another thing that I have going on. 

[01:06:49] **Jeremy:** What, what was it that I guess. Got you into deciding this is, this is what I want to do. I want to make a conference. 

[01:06:58] **Jason:** Well, it started off as I was going to put on a class, but then nobody bought a ticket. And so I had to pivot. And so I'm like, okay, I didn't sell any tickets to this class. Maybe I can sell some tickets to a conference. And luckily for me, it turns out I was right because I was financially obligated to a hotel where I had reserved space for the class.

So I couldn't just cancel it. I had to move forward somehow. So that's where the conference came. 

[01:07:28] **Jeremy:** interesting. yeah, I'm, I'm always kind of curious. How people decide what they want to attend, I guess, like, you know, you said how you didn't get enough signups for your class, but you get signups for a conference. And you know, the people who are signing up and want to go, I wonder to to them, what is, what is it about the going to a conference that is so much more appealing than, than going to a class?

[01:07:54] **Jason:** Oh, well, I think in order to go to a class, the topic has to be of interest to you. You have to be in like a specific time and place. The price point for that kind of thing is usually much higher than for, for a conference. Whereas with a conference it's affordable to individuals, you don't have to get your boss's permission necessarily, at least not for the money. It's more of like a, you don't have to be a specific kind of person in a specific scenario in order to benefit from it. It's a much more general interest. So that's why I think I've had an easier time selling tickets to that. 

[01:08:31] **Jeremy:** Mm, mm. Yeah, it's, it's more of a I wanna get into a room with a bunch of people and just learn a bunch of cool stuff and not necessarily have a specific specific thing you're looking to get out of it, I guess.

[01:08:46] **Jason:** Yeah. There's no specific outcome or anything like that. Honestly, it's mostly just to have a good time. That's the main thing I'm hoping to get out of it. And I think that is the main draw for people they want to, they want to see their friends in the Ruby community form relationships and stuff like that. 

[01:09:07] **Jeremy:** Very cool. Jason good luck with the conference and thank you so much for coming on software software sessions.

[01:09:13] **Jason:** Thanks a lot. And uh, thanks for having me. 

</div>