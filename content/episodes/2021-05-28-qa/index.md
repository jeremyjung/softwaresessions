+++
title = "Quality Assurance Testing"

description = "Michael and Maxwell of Aspiritech discuss exploratory testing, dropping old tests, accessibility, and how QA can influence product usability and documentation"

[extra]
episode_url = "https://media.transistor.fm/3c2740d6/c8aeac62.mp3"
+++

Michael Ashburne and Maxwell Huffman are QA Managers at Aspiritech.

This episode originally aired on Software Engineering Radio. 

Related Links:
- [Aspiritech](https://www.aspiritech.org/)
- [Section 508 Test for Accessibility](https://www.section508.gov/test)
- [ANDI Accessibility Testing Tool](https://www.ssa.gov/accessibility/andi/help/install.html)
- [Windows Hardware Compatibility Program](https://docs.microsoft.com/en-us/windows-hardware/design/compatibility/)
- [Audio over Bluetooth](https://habr.com/en/post/456182/)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy:** [00:00:00] Today I'm joined by Maxwell, Huffman and Michael Ashburn. They're both QA managers at Aspiritech. I'm going to start with defining quality assurance. Could one of you start by explaining what it is?

**Maxwell:** [00:00:15] So when I first joined Aspiritech, I was kind of curious about that as well. One of the main things that we do at Aspiritech  besides quality assurance is we also, give meaningful employment to individuals on the autism spectrum. I myself am on the autism spectrum and that's what, initially attracted me to the company.
quality assurance in a nutshell is making sure that, products and software is not defective. That it functions the way it was intended to function.  

**Jeremy:** [00:00:47] how would somebody know when they've, when they've met that goal? 

**Michael:** [00:00:50] It all depends on the client's objectives. I guess. quality assurance testing is always about trying to mitigate risk. There's only so much testing that is realistic to do, you know, you could test forever and never release your product and that's not good for business. It's really about, you know, balancing, like how likely is it that the customer is going to encounter defect X, how much time and energy would be required to, to fix it?

Overall company reputation, impact, there's all sorts of different metrics. Uh, and every, every customer is unique really they, they get to set the pace, 

**Maxwell:** [00:01:30] does the product work well?  is the user experience frustrating or not? that's always a bar that I look for. One of the main things that we review in the different defects that we find is customer impact.

and how much of this is going to frustrate the customers. And when we're going through that analysis, is this cost effective or not. The client they'll determine it's worth, the cost of the, uh, quality assurance and of the fix of the software to make sure that that customer experience is smooth.

**Jeremy:** [00:02:03] When you talk to, to software developers, now, a lot of them are familiar with things like they need to test their code right. They have things like unit tests and integration tests that they're running regularly. where does quality assurance fit in with that? Like, is that considered a part of quality assurance is quality assurance something different?

**Michael:** [00:02:24] we try to partner with our clients, because the goal is the same, right. It's to release a quality product that's as free of defects, as, you know, as possible.

We have multiple clients that will let us know these are clients typically that we've worked with for a long time that have sort of established a rhythm. they'll let us know when they've got a new product in the pipeline and as soon as they have available, Uh, software requirements, documentations specs, user guides, that kind of thing.
They'll provide that to us, to be able to then plan. Okay. You know, what are these new features? Uh, what defects have been repaired since the last build or, you know, it all depends on what the actual product is. And we start preparing tests even before there may be, uh, A version of the software to test, you know, now that's more of a, what they call a waterfall approach where it's kind of a back and forth where, you know, the client preps the software, we test the software.

If there's something amiss, the client makes changes. Then they give us a new build. but we just as well, we work in, uh, iterative design or agile is a popular term, of course, where. We have embedded testers, that are, you know, on a daily basis, interacting with, uh, client developers to address, you know, to, to verify certain parts of the code as it's being developed.

Because of course the problem with waterfall is you find a defect and it, it could be deep in the code or some sort of linchpin aspect of the code. And then there's a lot of work to be done. To try to fix that sort of thing. Whereas, you know, embedded testers can identify a defect or, or even just like a friction point as early as possible.
And so then they don't have to, you know, tear it all down and start over and it's just, Oh, fix that, you know, while they're working on that part, basically.

**Jeremy:** [00:04:18] so I think there's two things you touched on there. One is. the ability to bring in QA early into the process. And if I understand correctly, what you were sort of describing is. even if you don't have a complete product yet, if you just have an idea of what you want to build, You were saying you start to generate test cases and it almost feels like you would be a part of generating the requirements generating. Like, what are the things that you need to build into your software before uh, the team that's building it necessarily knows themselves did that I sort of get that.

**Maxwell:** [00:04:55] I've been in projects that we've worked with the product from cradle to grave. a lot of them haven't gotten all the way to a grave yet, but, um, some of them, the amount of support that they're offering. It's reached that milestone in its life cycle, where they're no longer going to, um, address the defects in the same way.

They want to know that they're there. They want to know what exists. But then now there are new products that are being created, right? So we are, um, engaged in embedded testing, which is, which is testing, certain facets of the code actively, and making sure that it's, doing what it needs to do.

And we can make that quick patch on that code and put it out to market. And we're also doing that at earlier stages with, in, in earlier development where before it's an even, fully formed design concepts, we're offering suggestions, and recommending that, you know, this doesn't follow with the design strategy and the concept design.
so that part of embedded testing or unit testing, can be involved at earlier stages as well. For sure.

**Michael:** [00:06:08] Of course, those, you have to be very, careful you know, we wouldn't necessarily make blanket recommendations to a new client, a lot of the clients that we have, we have been with us for several years. And so. You know, you develop a rhythm, common vocabulary, you know, you know, which generally speaking, which, goals weigh more than other goals and things like that from, from client to client or even coder to coder.

it's only once we've really developed that. shared language that, you know, we would say by the way, you know, such and such as missing from blankety blank, say great example with a bunch of non words in it, but I think you get the picture.

**Jeremy:** [00:06:48] when you're first starting to work on a project, you don't know a whole lot about it, right? you're trying to, to understand how this product is supposed to work and, what does that process look like? Like what should a company be providing to you? What are the sorts of meetings or conversations you're having that, that sort of thing.

**Michael:** [00:07:08] we'll have an initial meeting with a handful of people from both sides and just sort of talk about both what we can bring to the project and what their objectives are. and, and, you know, the, the thing that they want us to test, if you will. And, if we reach an agreement that we want to move forward, then the next step would be like a product demo, basically, we would come together and we would start to fold in, you know, leads and some other analysts, you know, people that were, might be a good match for the project say, and we always ask, our clients.

And they're usually pretty accommodating. if we can record the meeting, you know, now everyone's meeting on Google meet and virtually and so forth. And so, uh, that makes it a little easier, but a lot of our analysts have everyone has their own learning style. Right. You know, some people are more auditory, some people are more visual.

So we preserve, you know, the client's own demonstration of what it's either going to be like, or is like or is wrong or whatever they want us to know about it. and then we can add that file to our secure project folder and anybody down the road that's being onboarded. Like that's, that's a resource an asynchronous resource that they can turn to right? A person doesn't have to re demonstrate the software to onboard them,  or sometimes, you know, by the time we're onboarding new people, the software has changed enough that we have to set those aside actually. And then you have to do a live in person kinda deal.

**Maxwell:** [00:08:32] and you really want to consider, individuals on the, on the spectrum, the different analysts and testers they do have different learning styles.  We do want to ask for as many different. resources that are available, to, accommodate for that, but also to have us be, the best enabled to be the subject matter experts on the product.

so what we've found is that what we're really involved in is writing test cases and, and, and rewriting test cases to humanize the software to really get at, what are you asking this software to do that in turn is what the product is doing. a lot of the testing we do is black box testing, and we want to understand what the original design concept is.

So that involves the user interface, design document, right? early stages of that, if available, or just that, dialogue that Michael was referring to, to get that common language of what do you want this product to do? What are you really asking this code to do? having recordings, or any sort of training material, is absolutely essential. To being the subject matter experts and then developing the kind of testing that's required for that.

**Michael:** [00:09:48] And all sorts of different clients have different, different amounts of testing material, so to speak I mean, everything from, you know, a company that has their own internal, test tracking software and they just have to give us access to it. And the test cases are already there to, a piece of paper, like a physical piece of paper that they copied the checklist into Excel.

And now, like, these are the things that we look at, but of course there's always a lot more to it than that, but that at least gives us a starting point to sort of to build off of and, you know, testing areas and sections and, you know, sort of thematically related features, things like that. And then we can, we develop our own tests, on their behalf, basically.

**Jeremy:** [00:10:29] And when you're building out your own tests, what, what would be the, the level of detail there? Would it be a high level thing that you want to accomplish in the software and then like absolute step by step, click by click, 

**Michael:** [00:10:42] You know, I hate to make every answer conditional, right. But it sort of depends on the software itself and what the client's goals are. one of our clients, uh, is developing a new, screen-sharing app that's for developers both work on the same code at the same time, but they can take turns, typing, controlling the mouse, that sort of thing.

and although this product has been on the market for awhile, we started out with one of those checklists and now have hundreds of test cases based on, both features that they've added, as well as weird things that we found like, Oh, make sure sometimes you have to write a test case, uh, that tests for the negative, like the, the absence of a problem, right?

So you can make sure X connects to Y and the video doesn't drop or. If you can answer the connection, on, before the first ring is done and it successfully connects anyway, or, or, you know, any host of, of options. So our test cases, for that project, we have a lot of, uh, screen caps and stuff because a picture's worth a thousand words as the cliche goes.

but we also try to describe, describe the features, not just, you know, present the picture with an arrow, like click here and see what happens. Because again, everyone has sort of different data processing styles and some would prefer to read step by step instructions rather than try to interpret, you know, some colors in a picture.

And what does this even mean out of context?

**Maxwell:** [00:12:08] and lots of times you'll end up potentially seeing test cases they seem like they could be very easily automated. Cause literally they're written all in code. and the client will occasionally ask us to do a test cycle scrub or they'll ask us, okay, well, what can be automated within this?

Right. But one of the key things we really look at is, is to try to humanize that test case a little more away from that just basic automation, lots of times that, that. Literally involves asking, what are you trying to get out of this out of this test case? cause it's fallen so much into the, into the weeds that you no longer can really tell what you're really asking it to really do So lots of times we will, we will help them automate them. But also just give it the proper test environment. and the, and the the proper steps, you'd really be amazed. How many test cases just do not have the proper steps get an, an actual expected result. And if it's written wrong at that basic manual level, you're not adding value.

so that's one thing that we, that we really have found it's added value to the clients and to their test cycles.

**Michael:** [00:13:21] A lot of people ask about automation because it's a very sexy term right now. And it certainly has its place. Right. But uh you can't automate new feature testing. it has to be an aspect of the product that's mature. Not changing from build to build. And you also have to have test cases that are mature, that you know, every little virtual or otherwise, you know, T is crossed and I is dotted, or else you end up having to do manual testing anyway, because the computer just goes oh
it didn't work. Because that's really all the, you know, the automated process can do is either it passes or it doesn't. And so then we have to come in and, and we have clients where we do plenty of that. Like, okay, they ran through the tests and these three failed figure out why, and then they go in and start digging around and, Oh, it turns out this is missing or this got moved in the latest update or something like that.

**Jeremy:** [00:14:12] that's an interesting, perspective for testing in general, where it sounds like when a feature is new, when you're making a lot of changes to how the software works. that's when, manual testing can actually be really valuable because as a person, you have a sense of what you want and if things kind of move around or don't work exactly the way you expect them to, but you kind of know what the end goal is. you have an idea of like, yes, this worked or no, this didn't. and then once that's solidified then that's when you said it's easier to, to shift into automatic testing. for example, having, an application, spin up a browser and click through things or, or trigger things through code, things like that.

**Michael:** [00:14:58] And you have to, you know, you have to get the timing just right. Cause the computer can only wait in so many increments and you know, if it, if it tries to click the next thing too soon and it hasn't finished loading, you know, then it's all over. but that's actually the, the, the discernment that you were sort of referring to the, the, using your judgment when executing a test.

that's where we really, we really do our best work and we have some analysts that specialize in exploratory testing, which is where you're just sort of looking around systematically or otherwise. I personally have never been able to do that very well. uh, but that's critical because those, those exploratory tests are always where you turn up the weirdest combination of things.

Oh, I happened to have this old pair of headphones on and when I switched from Bluetooth to. manual plug, you know, just disconnected the phones or the, you know, the conference call altogether you know, and who does that. Right. But, you know, there's all, all sorts of different kinds of combinations and, and, and who knows what the end user is going to bring. He's not going to necessarily buy all new gear, right. When he gets the new computer, the new software, whatever.

**Jeremy:** [00:16:05] I feel like there's been a. Uh, kind of a trend in terms of testing at software companies, where they, they used to commonly have, in-house testing or in-house QA, it would be separated from development.

And now you're seeing more and more of, people on the engineering staff, on the developing staff being responsible for testing their own software, whether that be through unit tests, integration tests, Or even just using the software themselves, where you're getting to the point where you have more and more people are engineers that maybe have some expertise or some knowledge in tests and less, so people who are specifically dedicated to test. and so I wonder from your perspective you know, a QA firm or just testers in general? Like what their role is in, in software development going forward.

**Maxwell:** [00:16:55]  having specialized individuals that are constantly testing it and analyzing the components and making sure that you're on track to make that end concept design come to life really is essential. And that's what you get with the quality assurance. It's like a whole other wing of your company that basically is making sure that everything you are, that you are doing with this, product and with this software, is within scope.

and you can't be doing anything better as well. that's the other aspect of it, right? cause lots of times when we find a component and we found something, that we've broken or we've found a flaw in the design we look at, what that means.
bigger picture um, with the overall product. and we try to figure out all right, well, does this part of the functionality... is it worth it to fix this part of the functionality? is it cost-effective right. So lots of times quality assurance.

it comes right down to the, to the cost-effectiveness of the different, patches. and lots of times it's even the safety. of the, uh, product itself. it all depends on what exactly you're, you're designing, but I can give you an, an example of a, of a product that, that we were, that we were working with in the past, where we were able to get a component to overheat, obviously that is a critical defect that needs to be addressed and fixed.

that's something that can be found. as you're just designing the product. But to have a specialized division, that's just focused on quality assurance. They're more liable, they're more inclined. And that is what their directive is, is to find those sorts of defects. And I'll tell you the defects that we found that overheated this, this product, it was definitely an exploratory, find it was actually caught.

Off of a test case that was originally automated. so we definitely, we're engaged in every aspect or a lot of the aspects of the, of the engineering departments with this, uh, products. but in the end it was exploratory testing.

It was out of scope of what they had automated then ended up finding us. That's where I really see quality assurance in this, in this field within software engineering, really gaining respect and gaining momentum in understanding that, Hey, these are, these are really intelligent, potentially software engineers themselves.
That their key focus is to, is to testing our product and making sure that it's a design that, that is within the scope.

**Michael:** [00:19:36] It's helpful to have a fresh set of eyes too you know, if a person's been working on a product for, you know, day in, day out for months on end, inevitably there will be aspects that become second nature. may allow them to effectively like skip steps in the course of testing, some end result when they're doing their own testing, but you bring in, you know, a group of a group of analysts who know testing, but don't know your product other than generally what it's supposed to do and you sort of have at it and you find all sorts of interesting things that way.

**Jeremy:** [00:20:13] Yeah, I think you brought up two interesting points. one of them is the fact that. Nowadays, there is such a big focus on, automated testing as a part of a continuous integration process, right? Somebody will write code they'll check in their code, it'll build, and then automated tests will see that it's still working.

But those tests that the developers wrote, they're never going to find things that there were never a test written for. Right. So, I think that whole exploratory, testing aspect is interesting. and then Maxwell also brought up a good point uh, it sounds like QA can also not just help find what defects or issues exists, but they can also help. grade how much of an issue those defects are so that, the developers they can prioritize. Okay. Which ones are really a big deal that we need to fix, uh, versus what are things that, yeah, it's, I guess it's a little broken, but it's not, not such a big deal.

**Maxwell:** [00:21:14] in a broader sense, there are certain whole areas of design right now. Uh, Bluetooth is a really, uh, big area that we've been working in. I'm the QA manager for the Bose client at, Aspiritech and Bluetooth is really a big thing that, that is, that is involved in all of their different speakers.

So obviously if we, if we find anything, anything wrong with, with a certain area, you know, we want them to consider what areas they might want to focus more manual testing and less automation on. Right. and we're always thinking about, feature specific in that sense, um, to help the clients out as well.

and analysts that are on the spectrum, they really have. it's fascinating how, how they tend to be very particular about certain defects. and, and they can really find things that are very exploratory, but they don't miss. the, uh, forest for the trees in the sense that they still maintain, the larger concept design, funnily enough, where they can let you know, you know, is Bluetooth really the factor in this, that should be fixed here or is it, or is it something else? to, it leads to different, to interesting avenues for sure.

**Michael:** [00:22:32] Yeah, Bluetooth is really, A bag of knots in a lot of ways, you know, the different versions, different hardware vendors, we work with zebra technologies and they make barcode printers and scanners and so forth.
And you know, many of their printers are Bluetooth enabled. but you know, the question is, is it Bluetooth 4 to Bluetooth, 4 is it, backwards compatible.

And, uh, a certain, uh, rather ubiquitous, computer operating system is notorious for having trouble with Bluetooth management, whether it's headphones or printers or whatever. and in that instance, because we want to, you know, we're not testing the computer OS, we're testing the driver for the printer. Right. 

So, part of the protocol we wound up having to build into the, into the test cases is like, okay, first go in deactivate, the computer's own, resident internal hardware, Bluetooth, then connect to this, you know, third party USB dongle, install the software, make sure it's communicating, then try to connect to your printer For a long time, an analyst would run into some kind of issue.

And the first question is always, are you using the computer Bluetooth? Or is it a third-party Bluetooth and is discoverable on, is it a Bluetooth, low energy because you don't want to print using Bluetooth low energy because it'll take forever. Right? 

And then the customer thinks, Oh, this isn't working. It's broke. You know, not even knowing that there's. Multiple kinds of Bluetooth and yeah. It's, uh, it's hairy for sure.

**Jeremy:** [00:24:00] Yeah. And then I guess, as a part of that, that process, you're finding out that there isn't necessarily a problem in the customer's software. but it's some external case so that, when you get a support ticket or a call, then, you know, like, okay, this is another thing we can ask them to check. Yeah.

**Maxwell:** [00:24:18] Absolutely. And then that's something that we are, that we've been, you know, definitely leveraged for, to help out, to try to resolve customer issues that come in as well, and try to set up a testing environment that mimics that. And, and we've occasionally. integrated that to, to become part of our manual testing and some automated scenarios as well.

so that, so those have been interesting scenarios having to buy different routers and what, and what have you. And once again, it gets back to the cost-effectiveness of it. You know, what is, what is the market impact? Yes. This particular AT&T router or what have you, um, might be having an issue. but you know, how many, how many users in the wind, the world are really running the software on this.

Right. and that's something that, everyone needs to, you know, that every company should consider when they're, considering, uh, you know, a a patch, um, in the, in the software.

**Jeremy:** [00:25:14] and something you, you also brought up is. As a, as a software developer, when there is a problem. One of the things that we always look for is we look for a reproducible case, right? Like, what are the steps, um, you need to take to have this bug or this problem occur. And it sounds like one of the roles might be.
we get in a report from a customer saying like this part of the software doesn't work. Um, but I'm not sure when that happens or how to get it to happen. And so, as a QA, uh, analysts, one of your roles might be taking those reports and then building a repeatable, um, test case.

**Michael:** [00:25:55] Absolutely. There's lots of times where clients have said we haven't been able to reproduce this, see if you can. And you know, we get back to them after some increment of time. And, sometimes we can, and sometimes we can't, you know, sometimes we have to buy special, uh, like headphones or some kind of, you know, try to reproduce the investment that the client was using.
Uh, in case there was some magic sauce interaction going on there.

**Maxwell:** [00:26:21] our analysts on the spectrum. they are so particular in writing up defects, all the little details. and that really is so important in quality assurance is documentation for the entire process. that's one area where I think quality assurance really helps development in general is making sure that everything is documented that it's all there on paper and the documentation is, is solid and really sound. Um, so for a lot of these defects, we've actually come in and I think up the standard a little bit where you can't have the defect written where, you know, the reproducibility is one out of one.

And it turns out this was a special build that the developer was using that no one else in the company was even using. It's a waste of time to track this defect down. And that's based on the fact that it was a poorly written up report in the first place.
so it can be fun to have to. Track down all the various equipment you need for it. And analysts are really well-suited for writing those up and, and, uh, and investigating these different defects that are errors that we, that we find sometimes they're, sometimes they're not actually defects. They're just errors in the system. 

**Michael:** [00:27:34] uh, tell them about like The Bose guide that Bose wound up using the guide that we had made internally.

**Maxwell:** [00:27:40] Yeah. There have been, so many guides that we've ended up creating that have been like terminal access, shortcuts, uh, just different, different ways to, you know, access the, uh, system, from a tester perspective that have, that have absolutely helped, just documenting all these things that engineers end up using to test code. Right. But lots of times these shortcuts Aren't well documented anywhere. so what quality assurance and what the Aspiritech has done, is we come in and we really create excellent training guides for how to, how to check the code.
Um, and, and what all the various commands are that have to be inputted and how that translates to what, the more obvious user experiences, which is, I think a lot of times what ends up being lost. it ends up all being code language and you don't really know what the user experiences, it's nice to, to be able to, To have found that, that the guides that we've created when we show them to the clients, because really we created them to make life easier for us and make the testing easier for us to make it more translatable. 

When you see all this different code that some of us are very well versed in. but other analysts might not be. As well-versed in the code or that aspect of it. Right. but once you humanize it and you, and you sort of say, okay, well, this is what you're asking the code to do. then you have that other perspective of, I actually can think of a better way that we could Potentially do this. so we've brought a lot of those guides to the clients and they've really been, they've really been blown away, at how well documented All of that was, um, all the way down to the level of the, uh, GUIDs of all the systems. We have very good inventory tracking, and even being able to test and run, internal, components of the system. and that's why I bring up the a G U I D S so a lot of the testing that we end up doing, or I wouldn't say a lot, but a portion of it is the sort of tests that installers would be running this sort of functionality that only installers of systems would be, would be running. So, it's still, it's still black box testing, but it's behind the scenes of what the normal user experiences. Right. It's sort of the installer experience for lack of a better word.

And even having that well-documented and finding errors. In, in those processes have been quite beneficial. I, I remember one scenario in which there was an emergency update method that we had to test, right. And this is, this was a type of method where if someone had to run it, they would take it into the store and a technician would run it right. So basically we're, we're running software quality assurance on a technicians test for a system and the way a technician would update the system. And what we found is that what they were asking the technician to do was a flawed and complex series of steps. it did work. But only one out of 30 times, and only if you did everything in a very particular timing.

And it just was not something that was user-friendly, for the, a tech technician. So it's the kind of thing that we ended up finding. And lots of times it requires the creation of a guide because they don't have guides for technicians, to end up to end up finding a defect like that.

**Michael:** [00:31:21] and the poor technician, you know, he's dealing with hundreds of different devices, whatever it is, you know, whatever the field is, whether it's phones or speakers or printers or computers or whatever. And, you know, this guy is not working with the same, software day in and day out. The way we have to sometimes again, because the developer is sort of building the, the tool that will do the stuff, you know, we're, we're dealing with the stuff it's doing. And so in a lot of ways, uh, we can bring our own level of expertise to a product. Uh, we can surpass, you know, the developer even, it's not like a contest, right.

but just in terms of, you know, how many times is a developer installing it for the first time, like Maxwell was saying, what, when we do out of box testing, we have to reset everything and install it fresh over and over and over and over again. And so, so we wind up being exposed to this particular, you know, series of steps that the end user might only see a couple of times, but you know, who wants their brand new shiny thing, especially if it costs hundreds of dollars, you know, you don't want to have a lot of friction points in the process of finally using it.

You know, you just kind of want it to just work as effectively as possible.

**Jeremy:** [00:32:45] if I understood correctly in, in Maxwell's example, that would be, you had a physical product, like let's say a pair of headphones or something like that, and you need to upgrade, the firmware or. Perform some kind of reset. And that's something that like you were saying, a technician would normally have to go through, but, as QA, you go in and do the same process and realize like, this process is really difficult and it's really easy to make a mistake or, um, just not do it properly at all.

and then, so you can propose like either, you know, ways to improve those steps or just show the developers like, Hey, look, I have to do all these things just to, you know, just update my firmware. Um, you might want to consider like, making that a little easier on, on your customers. Yeah.

**Maxwell:** [00:33:32] Absolutely. And the other nice thing about it, Jeremy is, you know, we don't look at it at a series of tests like that as lower level functionality. just because, um, you know, it's more for a technician to have run it. It's actually part of the update testing.

So it's, so it's actually very intricate. as far as the design of the, of the product. We find a defect in how this system updates. It's usually going to be a critical defect. Um, we don't want the product to ever end up being a boat anchor or a doorstop. Right. So that's so that's, so that's what we're always trying to avoid.

and in that scenario, it's one of those things where then we don't exactly close the book on it once we, once we figure out, okay, this, this was a difficult scenario. For the technician, we resolve it for the technician. And then we look at, bigger scope, how does this affect the update process in general?

You know, does this affect the, uh, customers testing, that suite of test cases that we have for those update processes. you know, it can, it can extend to that as well. Uh, and, and then we look at it in terms of automation too. Uh, to see if there's any areas where we need to fix the automation tests.

 **Michael:** [00:34:46] it can be as simple as power loss during the update at exactly the wrong time. the system will recover if it happens within the first 50 seconds or the last 30 seconds, but there's this middle part where it's trying to reboot in the process of updating its own firmware. And if the power happens to go out, then. You're out of luck

that does not make for a good, reputation for the client. that, I mean, the first thing a customer that's unhappy about that kind of thing is going to do is tell everybody else about this horrible experience they had.

**Maxwell:** [00:35:20] Right. And I can think of a great example, Michael, we had found a ad hoc defect. They had asked us to look in this particular area. There was a very rare customer complaints of update issues. but they could not find it with their automation. we had one analyst that amazingly enough, was able to pull the power.
At the right exact time in the right exact sequence. And, and we reported the ticket and we were able to capture the logs for this incident. And they must have run this through 200,000 automated tests and they could not replicate what this human could do with his hands. Um, and it would have really amazed them after we had found it.
cause they really had run it through that many automation tests, but it does, it does happen where you find those.

 **Jeremy:** [00:36:10] we we've been talking about, uh, in this case you were saying this was for Bose, which is a very, large company. And I think that. When the average developer thinks about quality assurance, they usually think about it in the context of, I have a big enterprise company. Um, I have a large staff, I have money to pay for a whole bunch of analysts, things like that.

I want to go back to where Michael, you had mentioned how. one of your customers was for a, uh, a screen-sharing application. we had an interview with Spencer Dixon who's the CTO at Tuple. I believe that's the product you're referring to. So. I wonder if you could walk us through, like for somebody who has a business that's I want to say they're probably maybe four or five people, something like that.

what's the process for them, bringing on a dedicated analysts or testers. given that you're coming in, you have no knowledge of their software. What's the process there like?

**Michael:** [00:37:13] first of all, not to, not to kiss up, but the guys at Tuple are a really great bunch of guys. They're very easy to work with. we have like an hourly cap, per month, you know, to try to not exceed a certain number of hours. That agreement helps to manage their costs. They're very forthcoming. and they really have, folded us in to their development process. You know, they've given us access to their, uh, trouble ticket, uh, software.

We use their internal instant messaging application, to double-check on, you know, expected results. And is this a new feature or is this something that's changed unintentionally? so when we first started working with them, there was really only one. person on the project. and this person was in essence, tasked with turning, the Excel checklist of features into suites of test cases.

And, you know, you, you start with Make sure X happens when you click Y and then you make that the title of a test case. And, you know, once you get all the easy stuff done, then you go through the steps of making it happen. They offered us a number of very helpful sort of starting videos that they have on their website for how to use the software, by no means are they comprehensive.

 but it was enough to get us comfortable, you know, with the basic functionality and then you just wind up playing with the software a lot. they were very open to giving us the ramp up time that we needed in order to check all the different boxes, uh, both ones on their list. And then new ones that we found because, you know, there's, there's more than one. connection type, right? That can be just a voice call or there can be the screen sharing and you can show your local video from your computer camera, so you can see each other in a small box. And, you know, what order do you turn those things on?

And, which one has to work before the next one can work? Or what if a person changes their preferences in the midst of a call and, you know, these are things that, fortunately Tuple's audience is a bunch of developers. So, uh, when their clients, their customers report a problem, uh, the report is extremely thorough because they know what they're talking about.

And so the reproduction steps are pretty good, but we still, sometimes we'll run into a situation, that they've shared with us. It's like, we can't, we can't make this one happen. And I don't know. I mean, The getting back to the Bluetooth, like they've even had customers where, uh, I guess one headset used a different frequency. Uh, than another one, even though they were on the same Bluetooth version. And when he changed this customer, I shouldn't say he, the customer, whoever whomever, they are, uh, they changed from one headset to another and you know, the whole thing fell apart and it's like, how do you even, you know, cause you don't go to the store and look on the package and see, Oh, this particular, uh, you know, headphone uses 48 kilo Hertz for their, you know, At the outset. I didn't even know that that was a thing that could be a problem. Right. It just, you figured Bluetooth has its band of the telecom spectrum and, but, you know, anything's possible. So they gave us time to ramp up, you know, cause they knew that they didn't have any test cases and uh, over time now, there's a dedicated team of three people that are on the project regularly, but it can expand to as many as six, you know, because it's a sharing application, right?

So you tend to need multiple computers involved, And yeah, we've really, we've really enjoyed a relationship with Tupelo and our, and our eagerly awaiting, uh, if there would be windows version, because there's so many times when we'll be working on another project even, and, you know, talking with the person and saying, Oh, I wish I could, you know, we could use Tuple cause then I could click the thing on your screen and you could see it happen instead of just, you know, um, they are working on a Linux version though.

I don't think that's a trade secret. So that's, that's in the pipeline. We're excited about that. And these guys, they pay their bills in like two days. No customers do that. They're, they're really something.

**Jeremy:** [00:41:14] I mean, I think that's a, a sort of a unique case because it is a screen sharing application, you have things like headsets and webcams and, you're making calls between machines. So, I guess if you're testing, you would have all these different laptops or workstations set up all talking to one another.
So yeah, I can imagine why it would be really valuable to have, people or a team dedicated to that.

**Michael:** [00:41:40] And external webcams. And you know, whether you're, you're like my Mac mini is a 2012, so it doesn't have the three band audio. port, right. It's got one for microphone and one for headphone. So that in itself is like, well, I wonder how many of their customers are really going to have an older machine, but, it wound up being an interesting challenge because then I had to, if I was doing a testing, I had to have a microphone sort of distinct from the headphones.

And then that brings in a whole other nest of interactivity that you have to. Account for maybe the microphones USB based, you know, all sorts of craziness.

 **Jeremy:** [00:42:19] I'm wondering if you have projects where you not only have to use the client, but you also have to, to set up the server infrastructure so that you can run tests internally. I'm wondering if you do that with clients and if you do like, what's your process for learning? How do I set up a test environment? How do I make it behave like the real thing, things like that.

**Maxwell:** [00:42:42] So the production and testing equipment is what the customers have right. It's basically to, to create that setup, we just need the equipment from them and the user guides and the less information, frankly, the better in those setups, because you want to mimic what the customer's scenario is, right? You don't want to mimic too pristine of a setup. and that's something that we're always careful about when we're doing that sort of setup. As far as more of the integration. and the, uh, sandbox testing bed, where you're testing a new build for regressions or what, or what have you, that's going to be going out. we'd be connected to a different server environment. 

**Michael:** [00:43:24] And with zebra technologies, they're their zebra designer, printer driver. Uh, they support windows 7 windows 8.1 windows 10 and windows server 2012, 2016, 2019. And in the case of the non server versions, both 32 bit and 64 bit, because apparently windows 10 32 bit is more common in Europe, I guess, than it is here.

And even though, you know, windows 7 has been deprecated by Microsoft, they've still got a customer base, you know, still running, you know, don't fix what ain't broke. Right. So why would you update a machine if it's doing exactly what you want, you know, in your store or a business or whatever it is. And so we make a point of, of executing tests in all 10 environments.

It, it can be tedious because windows 7 uh, 32 and 64 have their own quirks. So we always have to test those too, you know, windows 8 and windows 10. They're fairly similar, but you know, they keep updating windows 10 and so it keeps changing. and then when it's time, for their printer driver to go through the, uh, The windows logo testing, they call it that's like their, their hardware quality labs, hardware certification, uh, that Microsoft has, which in essence means when you run a software update on your computer, uh, if there's a new version of the driver, it'll download it from Microsoft servers.

You don't have to go to the customer website and specifically seek it out. So we actually do, uh, certification testing for zebra, uh, with that driver in all of those same environments and then submit the final, package for Microsoft's approval. And that's, uh, that's actually been, uh, sort of a job of ours if you will, for several years now.
And that it's not something you take lightly when you're dealing with Microsoft and actually this sort of circles back to the, the writing, the guides, Because, you know, there are instructions that come with the windows hardware lab kit, but it doesn't cover everything obviously. And we wound up creating our own internal zebra.
Printer driver certification guide and it's over a hundred pages because we wanted to be sure to include every weird thing that happens, even if it's only sometimes, and be sure you set this before you do this, because in the wrong order, then it will fail. And he won't tell you why and all sorts of strange things.

And we've of course, uh, when we were nearing completion on that guide. Our contact at zebra was actually wanted, wanted a copy. Um, cause you know, we're not they're only a QA vendor obviously. and so if there's anything that would help and they have other divisions too, you know, they do, uh, uh, they have a browser print application that allows you to print directly to the printer from a web browser without installing a driver and that's a whole separate division and, you know, but overall, all these divisions, you know, have the same end goal as we do, which is, you know, sort of reducing the friction for the customer, using the product.

**Jeremy:** [00:46:31] That's an example of a case where it, it sounds, you said it's like a hundred pages, so you've got these, these test cases basically ballooning in size. And maybe more specifically towards, the average software project, as development continues, new features get added, the product becomes more complex.

I would think that the number of tests would grow, but I would also think that it, it can't grow indefinitely. Right. There has to be a point where. it's just not worth going through, you know, X number of tests versus the value you're going to get. So I wonder how you, how you manage that as things get more complicated, how do you choose what to drop and what to continue on with?

**Michael:** [00:47:15] it obviously depends on the client, in the case of zebra to use them again, You know when we first started working with them, they put together the test suites. We just executed the test cases, as time went by, They began letting us put the test suites together. Cause you know, we've been working with the same test cases and you know, trying to come up with a system.

So we sort of spread out the use instead of it always being the same number of test cases, because what happens when you get, when you execute the same tests over and over again, and they don't fail. That doesn't mean that you're you fixed everything. It means that your tests are worthless. Eventually. so they actually, a couple of summers ago, they had us go through all of the test cases, looking at, uh, the various results to evaluate like, okay, if this is a test case that we've run 30 times and it hasn't failed for the last 28 times, is there really any value in running it at all anymore?

Uh, so long as that particular functionality isn't being updated because they update their printer driver every few months when they come out with a new line of printers, but they're not really changing the core functionality of what any given printer can do. They're just adding, like model numbers and things like that.

So when it comes to like the ability of the printer to generate such and such a barcode on a particular kind of media, like that only gets you so far. but when you have, you know, uh, some printers have RFID capability and some don't, and so then you can, you get to kind of mix it up a little bit, depending on what features are present on the model.

So deprecation of, worn out test cases, uh, does help to mitigate, you know, the ballooning, test suite. I'm sure. I'm sure Bose has their own approach

**Maxwell:** [00:49:02] Absolutely. there are certain features then might also fall off entirely, where, you'll look at how many users are actually using a certain feature. like Michael was saying, you know, there might not be any failures on this particular feature, plus it's not particularly being used a lot.

So, so it's a good candidate for being automated. Right. so also we'll look at cases such as such as that. and we'll go through a test cycle scrubs. we've had to do, um, a series of, update matrixes that we've had to, um, progressively. look at how much of the market has already updated to a certain version.

so if a certain part of the market, if 90% of the market has already updated to this version, You don't you no longer have to test from here to here as far as your update testing. So that's another way in which you can, which you slowly start to reduce test, test cases and coverage.

but you're always, you're always looking at that with risk assessment in mind. Right. And, and you're, and you're looking at, you know, who are the end users that, you know, what, what's the, what's the customer impact. If we're, if we're pulling away. Um, or if we're automating this set of test cases.

so, you know, we go about that very, uh, carefully, but, we've been gradually more and more involved in helping them assess, what test cases are the best ones to be manually run? cause those are the ones that we end up finding defects in time and time again.

so those, so those are the areas. that we've really helped rather than having, you know, cause lots of times clients will, if they do have a QA department you know, the test cases will be written more in an automation type language. So it's like, okay, why don't we just automate these test cases to begin with?

And it'll be very broad scope where they have everything is written as a test case, for the overall functionality. And it's just way too much as you're pointing out Jeremy and as features grow. It just, that just continues on. it has to be whittled down in the early stages to begin with.

but that's how we, that's how we help out. to finally, you know, help manage these cycles to get them in a more reasonable, manual testing, cadence, right. And then having, having the automated section of test cases have that be, you know, the larger portion of the overall coverage as it should be in general.

**Jeremy:** [00:51:29] so it sounds like there's this, this process of you working with, uh, the client figuring out, what are the test cases that. don't or haven't brought up an issue in a long time, or, the things that get the most or the least use from customers, things like that, you, you, you look at all this information to figure out what are the things that for our manual tests we can focus on, um, and try to push everything else. Like you said, into some automated tests.

**Michael:** [00:51:59] So if, over time, we're starting to see these trends with older test cases or simpler test cases. You know, if we notice that there's a potential we'll bring that to the, to the client's attention.

And we'll say, we were looking at this batch of tests for basic features and we happened to notice that they haven't, failed ever or in two years or whatever. Would you consider us dropping those, at least for the time being, see how things go. and you know, that way we're spending less of their time.

So to speak, you know, on the whole testing process, because as you pointed out, like the more you build a thing, the more time you have to take, you know, to test it from one end to the other. but at the same time, uh, a number of our analysts are, um, OAST 508 trusted tester certified for accessibility testing, using screen readers and things like that.

uh, it's interesting how many web applications, you know, it just becomes baked into the bones. Right. And so, you know, you'll be having a team meeting talking about. yesterday's work. Um, and somebody will mention, you know, when I, when I went to such and such page, you know, because this person happened to use, a stylus to change the custom colors of the webpage or something like that.

Um, they'll say, you know, it really, it was not very accessible and there was light green, there was dark green, there was light blue, like I can, you know, and so I used my style sheet to make them. Red and yellow and whatever. and you see enough of that kind of stuff. And then that's an opportunity, to grow our engagement with the client, right?

Because we can say by the, by, you know, we noticed these things, we do offer this as a service. If you wanted to fold that in or, you know, set it up as like a one-time thing, even, you know, it all depends on, how much value it can bring. The client, right. you know, we're not pushing sales, trying to, Oh, we'll always get more whatever.

Um, but it's just about, when you see an opportunity, for, improvement of the client's product or, you know, uh, helping, uh, better secure their position in the market or, you know, however, however it works or could work to their advantage. You know, we sort of feel like it's our duty. To mention it as their partner.

we also do data analysis, you know, we don't just do QA testing. I know that's the topic here, of course. but that is another, another way where, you know, our discerning analysts can find, one of our products or one of our clients rather. we do monthly, uh, call center. Like help desk calls.

we analyze that data in aggregate and, you know, they'll find these little spikes, you know, on a certain day, say over there or a clutch over a week of people calling about a particular thing. And then we can say to the, to the client, you know, did you push a new feature that day or was it rainy that day?

Or, you know, I mean, it could be any, and maybe the client doesn't care, but. But we see it. So we say it and, and let them decide what to do with the information.
**Jeremy:** [00:55:08] The comment about accessibility is, is, um, is really good because it sounds like if you're a company and you're building up your product and you may not be aware of the accessibility issues, um, you have a tested by someone who's using a screen reader, you know, sees those issues with contrast and, and so on.

And now the developer, they have like these, these specific, actionable things to do and potentially even, um, moved those into automated tests to go like, okay, we need to make sure that these UI elements have this level of contrast, things like that.

**Michael:** [00:55:45] Yeah. And there's different screen readers too. you know, the, the certification process, like with the government to become a trusted tester uses one particular screen reader named Andy it's an initialism. Um, but there are others and, you know, then it's on us to become familiar with, you know, what else is out there because it's not like everyone is going to be using the same screen reader, just like not everyone uses the same browser

**Maxwell:** [00:56:10] I think the clients realize that, yeah, we do have a good automation department, but is it well balanced with what they're doing manual QA wise? And I think that's where we often find that there's a little bit lacking that we can provide extra value for, or we can boost what is currently there.

**Michael:** [00:56:28] Our employees are quality assurance analysts. They're not testers. They don't just come in, read the script, then, Pokemon go afterwards. we count on them to bring that critical eye, you know, and they're, and everyone's own unique perspective. Uh, when they go to use any given product, you know, Pay attention to what's happening.

You know, even if it's not in the test case, you know, something might, you know, flash on the screen or there might be this pause before the next, uh, thing kicks off that you are waiting for. And that happens enough times and you kind of notice, like there's always this lag right before the next step, you know, and then you can check that out with.

The developer, like, is this lag, do you guys care about this lag at all? And you know, sometimes we find out that it's unavoidable because something, you know, something under the hood has to happen before, the next thing can happen.

**Maxwell:** [00:57:20] and even asking those questions, we've found out fascinating things like, you know, why is there this lag every time when we run this test, you know, we never want to want to derail a client too much. You know, we're always very patient for the answer. And sometimes we don't, you know, we might not get the answer, but I think that that does help build that level of respect between us and the developers, uh, that we really care what their, what their code is doing. And we want to understand, you know, if there is a slight hiccup what's causing that slight hiccup, it's, it's, it ends up being fascinating for our analysts as we are learning the product.
And that's what makes us wanna want to really learn, um, exactly what that, what the code is doing.

**Michael:** [00:58:02] though I'm not a developer. Um, when I first started at Aspiritech, I worked on Bose as well, and I really enjoyed just watching their code, scroll down the screen. As you know, the machine was booting up or the speaker was updating because you can learn all sorts of interesting things about what's happening, you know, that you don't see normally. 

There's all sorts of weird inside jokes, uh, in terms of like what they call the command or, you know, Oh, there's that same spelling error where it's only one T or, you know, things that you kind of, you kind of get to know the developers in a way, you know, like, Oh, so-and-so wrote that line.

We always wondered. Cause there's only this one T and that word was supposed to have two teeth, you know, and they say, Oh yeah, we keep giving him a hard time about that. But now we can't change it because, so we have fun.

**Jeremy:** [00:58:52] If people want to learn more about, what you guys are working on or about Aspiritech where should they head?

**Maxwell:** [00:58:58] www.aspiritech.org. is our, is our website, head to there, uh, give you all the information you need about us. 

**Michael:** [00:59:06] We also have a LinkedIn presence, uh, that we've been trying to leverage lately and, uh, talk to our current clients. I mean, they've really, they've really been our biggest cheerleaders and the vast majority of our, of our work has come from client referrals. was, is an example of that too.

You know, they were referred by a client who was referred, you know, we're very proud of that. You know, it speaks volumes about, about the quality of our work and the relationships that we build and, and, uh, you know, we have very little customer turnover in addition to very little staff turnover and that's because we invest in these relationships and then it seems to work for both sides.

**Jeremy:** [00:59:46] Michael, maxwell, thanks for coming on the show

**Maxwell:** [00:59:49] thank you so much, Jeremy. It's great talking to you.

**Michael:** [00:59:52] Thanks for having us

</div>