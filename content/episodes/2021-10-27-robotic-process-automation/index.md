+++
title = "Robotic Process Automation"

description = "Alexander Pugh discusses why and when to use Robotic Process Automation (RPA)"

[extra]
episode_url = "https://pinecast.com/listen/a4f0ba14-b507-4937-95af-4705477e1533.mp3"
+++

Alexander Pugh is a software engineer at Albertsons. He has worked in Robotic Process Automation and the cognitive services industry for over five years.

This episode originally aired on Software Engineering Radio. 

### Related Links
- [Alexander Pugh's personal site](https://itsokayitsofficial.io/)

#### Enterprise RPA Solutions
- [Automation Anywhere](https://www.automationanywhere.com)
- [UiPath](https://www.uipath.com/)
- [blueprism](https://www.blueprism.com/)

#### Enterprise "Low Code/No Code" API Solutions
- [appian](https://appian.com/)
- [mulesoft](https://www.mulesoft.com/)
- [Power Automate](https://powerautomate.microsoft.com/en-us/)

#### RPA and the OS
- [Office primary interop assemblies](https://docs.microsoft.com/en-us/visualstudio/vsto/office-primary-interop-assemblies)
- [Office Add-ins documentation](https://docs.microsoft.com/en-us/office/dev/add-ins/)
- [Task Scheduler for developers](https://docs.microsoft.com/en-us/windows/win32/taskschd/task-scheduler-start-page)
- [The Component Object Model](https://docs.microsoft.com/en-us/windows/win32/com/the-component-object-model)
- [The Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** Today, I'm talking to Alexander Pugh. He's a solutions architect with over five years of experience working on robotic process automation and cognitive services. 

Today, we're going to focus on robotic process automation. 

Alexander welcome to software engineering radio. 

[00:00:17] **Alex:** Thank you, Jeremy. It's really good to be here. 

[00:00:18] **Jeremy:** So what does robotic process automation actually mean? 

[00:00:23] **Alex:** Right. It's a, it's a very broad nebulous term. when we talk about robotic process automation, as a concept, we're talking about automating things that humans do in the way that they do them. So that's the robotic, an automation that is, um, done in the way a human does a thing.

Um, and then process is that thing, um, that we're automating. And then automation is just saying, we're turning this into an automation where we're orchestrating this and automating this. and the best way to think about that in any other way is to think of a factory or a car assembly line. So initially when we went in and we, automated a car or factory, automation line, what they did is essentially they replicated the process as a human did it. So one day you had a human that would pick up a door and then put it on the car and bolt it on with their arms. And so the initial automations that we had on those factory lines were a robot arm that would pick up that door from the same place and put it on the car and bolt it on there.

Um, so the same can be said for robotic process automation. We're essentially looking at these, processes that humans do, and we're replicating them, with an automation that does it in the same way. Um, and where we're doing that is the operating system. So robotic process automation is essentially going in and automating the operating system to perform tasks the same way a human would do them in an operating system.

So that's, that's RPA in a nutshell, 

**Jeremy:** So when you say you're replicating something that a human would do, does it mean it has to go through some kind of GUI or some kind of user interface?

[00:02:23] **Alex:** That's exactly right, actually. when we're talking about RPA and we look at a process that we want to automate with RPA, we say, okay. let's watch the human do it. Let's record that. Let's document the human process. And then let's use the RPA tool to replicate that exactly in that way.

So go double click on Chrome, launch that click in the URL line and send key in www.cnn.com or what have you, or servicenow hit enter, wait for it to load and then click, you know, where you want to, you know, fill out your ticket for service. Now send key in. So that's exactly how an RPA solution at the most basic can be achieved.

Now and any software engineer knows if you sit there and look over someone's shoulder and watch them use an operating system. Uh, you'll say, well, there's a lot of ways we can do this more efficiently without going over here, clicking that, you know, we can, use a lot of services that the operating system provides in a programmatic way to achieve the same ends and RPA solutions can also do that.

The real key is making sure that it is still achieving something that the human does and that if the RPA solution goes away, a human can still achieve it. So if you're, trying to replace or replicate a process with RPA, you don't want to change that process so much so that a human can no longer achieve it as well.

that's something where if you get a very technical, and very fluent software engineer, they lose sight of that because they say, oh, you know what? There's no reason why we need to go open a browser and go to you know, the service now portal and type this in when I can just directly send information to their backend.

which a human could not replicate. Right? So that's kind of where the line gets fuzzy. How efficiently can we make this RPA solution? 

[00:04:32] **Jeremy:** I, I think a question that a lot of people are probably having is a lot of applications have APIs now. but what you're saying is that for it to, to be, I suppose, true RPA, it needs to be something that a user can do on their own and not something that the user can do by opening up dev tools or making a post to an end point.

[00:04:57] **Alex:** Yeah. And so this, this is probably really important right now to talk about why RPA, right? Why would you do this when you could put on a server, a a really good, API ingestion point or trigger or a web hook that can do this stuff. So why would we, why would we ever pursue our RPA?

There there's a lot of good reasons for it. RPA is very, very enticing to the business. RPA solutions and tools are marketed as a low code, no code solution for the business to utilize, to solve their processes that may not be solved by an enterprise solution and the in-between processes in a way.

You have, uh, a big enterprise, finance solution that everyone uses for the finance needs of your business, but there are some things that it doesn't provide for that you have a person that's doing a lot of, and the business says, Okay. well, this thing, this human is doing this is really beneath their capability. We need to get a software solution for it, but our enterprise solution just can't account for it. So let's get a RPA capability in here. We can build it ourselves, and then there we go. So there, there are many reasons to do that. financial, IT might not have, um, the capability or the funding to actually build and solve the solution. Or it it's at a scale that is too small to open up, uh, an IT project to solve for. Um, so, you know, a team of five is just doing this and they're doing it for, you know, 20 hours a week, which is uh large, but in a big enterprise, that's not really. Maybe um, worth building an enterprise solution for it. or, and this is a big one. There are regulatory constraints and security constraints around being able to access this or communicate some data or information in a way that is non-human or programmatic. So that's really where, um, RPA is correctly and best applied and you'll see it most often.

So what we're talking about there is in finance, in healthcare or in big companies where they're dealing with a lot of user data or customer data in a way. So when we talk about finance and healthcare, there are a lot of regulatory constraints and security reasons why you would not enable a programmatic solution to operate on your systems. 

You know, it's just too hard. We we're not going to expose our databases or our data to any other thing. It would, it would take a huge enterprise project to build out that capability, secure that capability and ensure it's going correctly. We just don't have the money the time or the strength honestly, to afford for it.

So they say, well, we already have. a user pattern. We already allow users to, to talk to this information and communicate this information. Let's get an RPA tool, which for all intents and purposes will be acting as a user. And then it can just automate that process without us exposing to queries or any other thing, an enterprise solution or programmatic, um, solution.

So that's really why RPA, where and why you, you would apply it is there's, there's just no capability at enterprise for one reason or another to solve for it. 

[00:08:47] **Jeremy:** as software engineers, when we see this kind of problem, our first thought is, okay, let's, let's build this custom application or workflow. That's going to talk to all these API APIs. And, and what it sounds like is. In a lot of cases there just isn't the time there just isn't the money, to put in the effort to do that.

And, it also sounds like this is a way of being able to automate that. and maybe introducing less risk because you're going through the same, security, the same workflow that people are doing currently. So, you know, you're not going to get into things that they're not supposed to be able to get into because all of that's already put in place.

[00:09:36] **Alex:** Correct. And it's an already accepted pattern and it's kind of odd to apply that kind of very IT software engineer term to a human user, but a human user is a pattern in software engineering. We have patterns that do this and that, and, you know, databases and not, and then the user journey or the user permissions and security and all that is a pattern.

And that is accepted by default when you're building these enterprise applications okay.

What's the user pattern. And so since that's already established and well-known, and all the hopefully, you know, walls are built around that to enable it to correctly do what it needs to do. It's saying, Okay. we've already established that. Let's just use that instead of. You know, building a programmatic solution where we have to go and find, do we already have an appropriate pattern to apply to it? Can we build it in safe way? And then can we support it? You know, all of a sudden we, you know, we have the support teams that, you know, watch our Splunk dashboards and make sure nothing's going down with our big enterprise application.

And then you're going to build a, another capability. Okay. WHere's that support going to come from? And now we got to talk about change access boards, user acceptance testing and, uh, you know, UAT dev production environments and all that. So it becomes, untenable, depending on your, your organization to, to do that for things that might fall into a place that is, it doesn't justify the scale that needs to be thrown upon it.

But when we talk about something like APIs and API exist, um, for a lot of things, they don't exist for everything. And, a lot of times that's for legacy databases, that's for mainframe capability. And this is really where RPA shines and is correctly applied. And especially in big businesses are highly regulated businesses where they can't upgrade to the newest thing, or they can't throw something to the cloud.

They have a, you know, their mainframe systems or they have their database systems that have to exist for one reason or the other until there is the motivation and the money and the time to correctly migrate and, and solve for them. So until that day, and again, there's no, API to, to do anything on a, on a mainframe, in this bank or whatnot, it's like, well, Okay. let's just throw RPA on it.

Let's, you know, let's have a RPA do this thing, uh, in the way that a human does it, but it can do it 24 7. and an example, or use cases, you work at a bank and, uh, there's no way that InfoSec is going to let you query against this database with, your users that have this account or your customers that have this no way in any organization at a bank.

Is InfoSec going to say, oh yeah. sure. Let me give you an Odata query, you know, driver on, you know, and you can just set up your own SQL queries and do whatever they're gonna say no way. In fact, how did you find out about this database in the first place and who are you.

How do we solve it? We, we go and say, Okay. how does the user get in here well they open up a mainframe emulator on their desktop, which shows them the mainframe. And then they go in, they click here and they put this number in there, and then they look up this customer and then they switch this value to that value and they say, save.

And it's like, okay. cool. That's that RPA can do. And we can do that quite easily. And we don't need to talk about APIs and we don't need to talk about special access or doing queries that makes, you know, Infosec very scared. you know, a great use case for that is, you know, a bank say they, they acquire, uh, a regional bank and they say, cool, you're now part of our bank, but in your systems that are now going to be a part of our systems, you have users that have this value, whereas in our bank, that value is this value here. So now we have to go and change for 30,000 customers this one field to make it line up with our systems. Traditionally you would get a, you know, extract, transform load tool an ETL tool to kind of do that. But for 30,000 customers that might be below the threshold, and this is banking. So it's very regulated and you have to be very, very. Intentional about how you manipulate and move data around.

So what do we have to do? okay. We have to hire 10 contractors for six months, and literally what they're going to do eight hours a day is go into the mainframe through the simulator and customer by customer. They're going to go change this value and hit save. And they're looking at an Excel spreadsheet that tells them what customer to go into.

And that's going to cost X amount of money and X, you know, for six months, or what we could do is just build a RPA solution, a bot, essentially that goes, and for each line of that Excel spreadsheet, it repeats this one process, open up mainframe emulator, navigate into the customer profile and then changes value, and then shut down and repeat.

And It can do that in one week and, and can be built in two, that's the, the dream use case for RPA and that's really kind of, uh, where it would shine.

[00:15:20] **Jeremy:** It sounds like the. best use case for it is an old system, a mainframe system, in COBOL maybe, uh, doesn't have an API. And so, uh, it makes sense to rather than go, okay, how can we get directly into the database?

[00:15:38] **Alex:** How can we build on top of it? Yeah,

[00:15:40] **Jeremy:** we build on top of it? Let's just go through the, user interface that exists, but just automate that process. And, the, you know, the example you gave, it sounds very, very well-defined you're gonna log in and you're going to put in maybe this ID, here's the fields you want to get back.

and you're going to save those and you didn't have to make any real decisions, I suppose, in, in terms of, do I need to click this thing or this thing it's always going to be the same path to, to get there.

[00:16:12] **Alex:** exactly. And that's really, you need to be disciplined about your use cases and what those look like. And you can broadly say a use case that I am going to accept has these features, and one of the best ways to do that is say it has to be a binary decision process, which means there is no, dynamic or interpreted decision that needs to, or information that needs to be made.

Exactly like that use case it's very binary either is, or it isn't you go in you journey into there. and you change that one thing and that's it there's no oh, well this information says this, which means, and then I have to go do this. Once you start getting in those if else, uh, processes you're, you're going down a rabbit hole and it could get very shaky and that introduces extreme instability in what you're trying to do.

And also really expands your development time cause you have to capture these processes and you have to say, okay. tell me exactly what we need to build this bot to do. And for, binary decision processes, that's easy go in here, do this, but nine times out of 10, as you're trying to address this and solution for it, you'll find those uncertainties.

You'll find these things where the business says, oh, well, yeah. that happens, you know, one times out of 10 and this is what we need to do. And it's like, well, that's going to break the bot. It, you know, nine times out of 10, this, this spot is going to fall over. this is now where we start getting into, the machine learning and AI, realm.

And why RPA, is classified. Uh, sometimes as a subset of the AI or machine learning field, or is a, a pattern within that field is because now that you have this bot or this software that enables you to do a human process, let's enable that bot to now do decision-making processes where it can interpret something and then do something else.

Because while we can just do a big tree to kind of address every capability, you're never going to be able to do that. And also it's, it's just a really heavy, bad way to build things. So instead let's throw in some machine learning capability where it just can understand what to do and that's, you know, that's the next level of RPA application is Okay. we've got it. We've, we've gone throughout our organization. We found every kind of binary thing, that can be replaced with an RPA bot. Okay.

Now what are the ones that we said we couldn't do? Because it had some of that decision-making that, required too much of a dynamic, uh, intelligence behind it. And let's see if we can address those now that we have this. And so that's, that's the 2.0, in RPA is addressing those non-binary, paths. 

I would argue that especially in organizations that are big enough to justify bringing in an RPA solution to solve for their processes. They have enough binary processes, binary decision processes to keep them busy.

Some people, kind of get caught up in trying to right out the gate, say, we need to throw some machine learning. We need to make these bots really capable instead of just saying, well, we we've got plenty of work, just changing the binary processes or addressing those. Let's just be disciplined and take that, approach.

Uh, I will say towards RPA and bots, the best solution or the only solution. When you talk about building a bot is the one that you eventually turn off. So you can say, I built a bot that will go into our mainframe system and update this value. And, uh, that's successful.

I would argue that's not successful. When that bot is successful is when you can turn it off because there's an enterprise solution that addresses it. and, and you don't have to have this RPA bot that lives over here and does it instead, you're enterprise, capability now affords for it. And so that's really, I think a successful bot or a successful RPA solution is you've been able to take away the pain point or that human process until it can be correctly addressed by your systems that everyone uses. 

[00:21:01] **Jeremy:** from, the business perspective, you know, what are some of the limitations or long-term problems with, with leaving an RPA solution in place?

[00:21:12] **Alex:** that's a, that's a good question. Uh, from the business there, isn't, it's solved for. leaving it in place is other than just servicing it and supporting it. There's no real issue there, especially if it's an internal system, like a mainframe, you guys own that. If it changes, you'll know it, if it changes it's probably being fixed or addressed.

So there's no, problem. However, That's not the only application for RPA. let's talk about another use case here, your organization, uses, a bank and you don't have an internal way to communicate it. Your user literally has to go to the bank's website, log in and see information that the bank is saying, Hey, this is your stuff, right?

The bank doesn't have an API for their, that service. because that would be scary for the bank. They say, we don't want to expose this to another service. So the human has to go in there, log in, look at maybe a PDF and download it and say, oh, Okay.

So that is happens in a browser. So it's a newer technology.

This isn't our mainframe built in 1980. You know, browser based it's in the internet and all that, but that's still a valid RPA application, right? It's a human process. There's no API, there's no easy programmatic way to, to solution for it. It would require the bank and your it team to get together and, you know, hate each other. Think about why this, this is so hard. So let's just throw a bot on it. That's going to go and log in, download this thing from the bank's website and then send it over to someone else. And it's going to do that all day. Every day. That's a valid application. And then tomorrow the bank changes its logo. And now my bot is it's confused.

Stuff has shifted on the page. It doesn't know where to click anymore. So you have to go in and update that bot because sure enough, that bank's not going to send out an email to you and saying, Hey, by the way, we're upgrading our website in two weeks. Not going to happen, you'll know after it's happened.

So that's where you're going to have to upgrade the bot. and that's the indefinite use of RPA is going to have to keep until someone else decides to upgrade their systems and provide for a programmatic solution that is completely outside the, uh, capability of the organization to change. And so that's where the business would say, we need this indefinitely.

It's not up to us. And so that is an indefinite solution that would be valid. Right? You can keep that going for 10 years as long, I would say you probably need to get a bank that maybe meets your business needs a little easier, but it's valid. And that would be a good way for the business to say yes, this needs to keep running forever until it doesn't.

[00:24:01] **Jeremy:** you, you brought up the case of where the webpage changes and the bot doesn't work anymore. specifically, you're, you're giving the example of finance and I feel like it would be basically catastrophic if the bot is moving money to somewhere, it shouldn't be moving because the UI has moved around or the buttons not where it expects it to be.

And I'm kind of curious what your experience has been with that sort of thing.

[00:24:27] **Alex:** you need to set organizational thresholds and say, this is this something this impacting or something that could go this wrong. It is not acceptable for us to solve with RPA, even though we could do it, it's just not worth it. Some organizations say that's anything that touches customer data healthcare and banking specialists say, yeah, we have a human process where the human will go and issue refunds to a customer, uh, and that could easily be done via RPA solution, but it's fraught with, what, if it does something wrong, it's literally going to impact.

Uh, someone somewhere they're their moneys or their, their security or something like that. So that, that definitely should be part of your evaluation. And, um, as an organization, you should set that up early and stick to it and say, Nope, this is outside our purview. Even we can do it. It has these things.

So I guess the answer to that is you should never get to that process, but now we're going to talk about, I guess, the actual nuts and bolts of how RPA solutions work and how they can be made to not action upon stuff when it changes or if it does so RPA software, by and large operates by exposing the operating system or the browsers underlying models and interpreting them.

Right. So when we talk about something like a, mainframe emulator, you have your RPA software on Microsoft windows. It's going to use the COM the component operating model, to see what is on the screen, what is on that emulator, and it's gonna expose those objects. to the software and say, you can pick these things and click on that and do that.

when we're talking about browser, what the RPA software is looking at is not only the COM the, the component object model there, which is the browser, itself. But then it's also looking at the DOM the document object model that is the webpage that is being served through the browser. And it's exposing that and saying, these are the things that you can touch or, operate on.

And so when you're building your bots, what you want to make sure is that the uniqueness of the thing that you're trying to access is something that is truly unique. And if it changes that one thing that the bot is looking for will not change. So we let's, let's go back to the, the banking website, right?

We go in and we launch the browser and the bot is sitting there waiting for the operating system to say, this process is running, which is what you wanted to launch. And it is in this state, you know, the bot says, okay. I'm expecting this kind of COM to exist. I see it does exist. It's this process, and it has this kind of name and cool Chrome is running. Okay. Let's go to this website. And after I've typed this in, I'm going to wait and look at the DOM and wait for it to return this expected a webpage name, but they could change their webpage name, the title of it, right. They can say, one day can say, hello, welcome to this bank. And the next day it says bank website, all of a sudden your bot breaks it no longer is finding what it was told to expect.

So you want to find something unique that will never change with that conceivably. And so you find that one thing on the DOM on the banking website, it's, you know, this element or this tag said, okay, there's no way they're changing that. And so it says cool the page is loaded. Now click on this field, which is log in.

Okay. You want to find something unique on that field that won't change when they upgrade, you know, from bootstrap to this kind of, you know, UI framework. that's all well, and good. That's what we call the happy path. It's doing this perfectly. Now you need to define what it should do when it doesn't find these things, which is not keep going or find similar it's it needs to fail fast and gracefully and pass on that failure to someone and not keep going. And that's kind of how we prevent that scary use case where it's like. okay. it's gone in, it's logged into the bank website now it's transactioning, bad things to bad places that we didn't program it for it, Well you unfortunately did not specify in a detailed enough way what it needs to look for.

And if it doesn't find that it needs to break, instead of saying that this is close enough. And so, in all things, software engineering, it's that specificity, it's that detail, that you need to hook onto. And that's also where, when we talk about this being a low-code no-code solutions that sometimes RPA is marketed to the business.

It's just so often not the case, because yes. It might provide a very user, business, friendly interface for you to build bots. But the knowledge you need to be able to ensure stability and accuracy, um, to build the bots is, is a familiarity that's probably not going to be had in the business. It's going to be had by a developer who knows what the DOM and COM are and how the operating system exposes services and processes and how.

JavaScript, especially when we're talking about single page apps and react where you do have this very reactive DOM, that's going to change. You need to be fluent with that and know, not only how HTML tags work and how CSS will change stuff on you in classes, but also how clicking on something on a single page app is as simple as a username input field will dynamically change that whole DOM and you need to account for it. so, it is it's, traditionally not as easy as saying, oh, the business person can just click, click, click, click, and then we have a bot. You'll have a bot, but it's probably going to be break breaking quite often. It's going to be inaccurate in its execution.

this is a business friendly user-friendly non-technical tool. And I launch it and it says, what do you want to do? And it says, let me record what you're going to do. And you say, cool.

And then you go about you open up Chrome and you type in the browser, and then you click here, click there, hit send, and then you stop recording. The tool says, cool, this is what you've done. Well, I have yet to see a, a solution that is that isn't able to not need further direction or, or defining on that process, You still should need to go in there and say, okay, yeah.

you recorded this correctly, but you know, you're not interpreting correctly or as accurate as you need to that field that I clicked on.

And if you know, anybody hits, you know, F12 on their keyboard while they have Chrome open and they see how the DOM is built, especially if this is using kind of any kind of template, Webpage software. It's going to have a lot of cruft in that HTML. So while yes, the recording did correctly see that you clicked on the input box.

What it's actually seen is that you actually clicked on the div. That is four levels scoped above it, whereas the parent, and there are other things within that as well. And so the software could be correctly clicking on that later, but other things could be in there and you're going to get some instability.

So the human or the business, um, bot builder, the roboticist, I guess, would need to say, okay, listen, we need to pare this down, but it's, it's even beyond that. There are concepts that you can't get around when building bots that are unique to software engineering as a concept. And even though they're very basic, it's still sometimes hard for the business user to, they felt to learn that.

And I I'm talking concepts as simple as for loops or loops in general where the business of course has, has knowledge of what we would call a loop, but they wouldn't call it a loop and it's not as accurately defined. So they have to learn that. And it's not as easy as just saying, oh Yeah.

do a loop. And the business will say, well, what's a loop.

Like I know, you know, conceptually what a loop could be like a loop in my, when I'm tying my shoe. But when you're talking about loop, that's a very specific thing in software and what you can do. And when you shouldn't do it, and that's something that these, no matter how good your low code, no code solution might be, it's going to have to afford for that concept.

And so a business user is still going to have to have some lower level capability to apply those concepts. And, and I I've yet to see anybody be able to get around that in their RPA solutions.

[00:33:42] **Jeremy:** So in your experience, even though these vendors may sell it as being a tool that anybody can just sit down and use but then you would want a developer to, to sit with them or, or see the result and, and try and figure out, okay, what do you, what do you really want this, this code to do?

Um, not just sort of these broad strokes that you were hoping the tool was gonna take care of for you? Yeah.

[00:34:06] **Alex:** that that's exactly right. And that's how every organization will come to that realization pretty quickly. the head of the game ones have said, okay, we need to have a really good, um, COE structure to this robotic operating model where we can have, a software engineering, developer capability that sits with the business, capability.

And they can, marry with each other, other businesses who may take, um, these vendors at their word and say, it's a low code meant for business. It just needs to make sure it's on and accessible. And then our business people are just gonna, uh, go in there and do this. They find out pretty quickly that they need some technical, um, guidance to go in because they're building unstable or inaccurate bots.

and whether they come to that sooner or later, they, they always come to that. Um, and they realize that, okay, there there's a technical capability And, this is not just RPA. This is the story of all low-code no-code solutions that have ever existed. It always comes around that, while this is a great interface for doing that, and it's very easy and it makes concepts easy.

Every single time, there is a technical capability that needs to be afforded. 

[00:35:26] **Jeremy:** For the. The web browser, you mentioned the DOM, which is how we typically interact with applications there. But for native applications, you, you briefly mentioned, COM. And I was wondering when someone is writing, um, you know, a bot, uh, what are the sorts of things they see, or what are the primitives they're working with?

Like, is there a name attached to each button, each text, field, 

[00:35:54] **Alex:** wouldn't that be a great world to live in, so there's not. And, and, as we build things in the DOM. People get a lot better. We've seen people are getting much better about using uniqueness when they build those things so that they can latch onto when things were built or built for the COM or, you know, a .NET for OS that might, that was not no one no one was like oh yeah, we're going to automate this.

Or, you know, we need to make this so that this button here is going to be unique from that button over there on the COM they didn't care, you know, different name. Um, so yeah, that is, that is sometimes a big issue when you're using, uh, an RPA solution, you say, okay. cool. Look at this, your calculator app. 

And Okay. it's showing me the component object model that this was built. It that's describing what is looking at, but none of these nodes have, have a name. They're all, you know, node one node, 1.1 node two, or, or whatnot, or button is just button and there's no uniqueness around it. And that is, you see a lot of that in legacy older software, um, E legacy is things built in 2005, 2010.

Um, you do see that, and that's the difficulty at that point. You can still solve for this, but what you're doing is you're using send keys. So instead of saying, Okay.

RPA software, open up this, uh, application and then look for. You know, thing, this object in the COM and click on it, it's going to, you know, it can't, there is no uniqueness.

So what you say is just open up the software and then just hit tab three times, and that should get you to this one place that was not unique, but we know if you hit tab three times, it's going to get there now. That's all well and good, but there's so many things that could interfere with that and break it.

And the there's no context for the bot to grab onto, to verify, Okay. I am there. So any one thing, you could have a pop-up which essentially hijacks your send key, right? And so the bot yes, absolutely hit tab three times and it should be in that one place. It thinks it is, and it hits in enter, but in between the first and second tab, a pop-up happened and now it's latched onto this other process, hits enter. And all of a sudden outlook's opening bot doesn't know that, but it's still going on and it's going to enter in some financial information into oops, an email that it launched because it thought hitting enter again would do so. Yeah.

That's, that's where you get that instability. Um, there are other ways around it or other solutions.

and this is where we get into the you're using, um, lower level software engineering solutioning instead of doing it exactly how the user does it. When we're talking about the operating system and windows, there are a ton of interop services and assemblies that a, uh, RPA solution can access.

So instead of cracking open Excel, double-clicking on Excel workbook waiting for it to load, and then reading the information and putting information in, you can use the, you know, the office 365 or whatnot that, um, interop service assembly and say, Hey, launch this workbook without the UI, showing it, attach to that process that, you know, it is.

And then just send to it, using that assembly send information into it. And the human user can't do that. It can't manipulate stuff like that, but the bot can, and it it's the same end as the human users trying. And it's much more efficient and stable because the UI couldn't afford for that kind of stability.

So that would be a valid solution. But at that point, you're really migrating into a software engineering, it developer solution of something that you were trying not to do that for. So when is that? Why, you know, why not just go and solve for it with an enterprise or programmatic solution in the first place?

So that's the balance. 

[00:40:18] **Jeremy:** earlier you're talking about the RPA needs to be something that, uh, that the person is able to do. And it sounds like in this case, I guess there still is a way for the person to do it. They can open up the, the Excel sheet and right it's just that the way the, the RPA tool is doing it is different. Yeah.

[00:40:38] **Alex:** Right. And more efficient and more stable. Certainly. Uh, especially when we're talking about Excel, you have an Excel with, you know, 200,000 lines, just opening that that's, that's your day, that's going to Excel it, just going to take its time opening and visualizing that information for you. Whereas you, you know, an RPA solution doesn't even need to crack that open.

Uh, it can just send data right directly to that workbook and it that's a valid solution. And again, some of these processes, it might be just two people at your organization that are essentially doing it. So it's, you know, you don't really, it's not at a threshold where you need an enterprise solution for it, but they're spending 30 minutes of their day just waiting for that Excel workbook to open and then manipulating the data and saving it.

And then, oh, their computer crashed. So you can do an RPA solution. It's going to be, um, to essentially build for a more efficient way of doing it. And that would be using the programmatic solution, but you're right. It is doing it in a way that a human could not achieve it. Um, and that again is. The where the discipline and the organizational, aspect of this comes in where it's saying, is that acceptable?

Is it okay to have it do things in this way, that are not human, but achieving the same ends. And if you're not disciplined that creeps, and all of a sudden you have a RPA solution that is doing things in a way that where the whole reason to bring that RPA solution is to not have something that did something like that. And that's usually where the stuff falls apart. IT all of a sudden perks their head up and says, wait, I have a lot of connections coming in from this one computer doing stuff very quickly with a, you know, a SQL query. It's like, what is going on? And so all of a sudden, someone built a bot to essentially do a programmatic connection.

And it is like, you should not be who gave you this permissions who did this shut down everything that is RPA here until we figure out what you guys went and did. So that's, that's the dance. 

[00:42:55] **Jeremy:** it's almost like there's this hidden API or there's this API that you're not intended to use. but in the process of trying to automate this thing, you, you use it and then if your, IT is not aware of it, then things just kind of spiral out of control.

[00:43:10] **Alex:** Exactly. Right. So let's, you know, a use case of that would be, um, we need to get California tax information on alcohol sales. We need to see what each county taxes for alcohol to apply to something. And so today the human users, they go into the California, you know, tobacco, wildlife, whatever website, and they go look up stuff and okay, let's, that's, that's very arduous.

Let's throw a bot on that. Let's have a bot do that. Well, the bot developers, smart person knows their way around Google and they find out, well, California has an API for that. instead of the bot cracking open Chrome, it's just going to send this rest API call and it's going to get information back and that's awesome and accurate and way better than anything. but now all of a sudden IT sees connections going in and out. all of a sudden it's doing very quickly and it's getting information coming into your systems in a way that you did not know was going to be, uh, happening. And so while it was all well and good, it's, it's a good way for, the people whose job it is to protect yourself or know about these things, to get very, um, angry, rightly so that this is happening.

that's an organizational challenge, uh, and it's an oversight challenge and it's a, it's a developer challenge because, what you're getting into is the problems with having too technical people build these RPA bots, right? So on one hand we have business people who are told, Hey, just crack this thing open and build it.

And it's like, well, they don't have enough technical fluency to actually build a stable bot because they're just taking it at face value. Um, on the other hand, you have software engineers or developers that are very technical that say, oh, this process. Yeah. Okay. I can build a bot for that. But what if I used, you know, these interop services, assemblies that Microsoft gives me and I can access it like that.

And then I can send an API call over here. And while I'm at it, I'm going to, you know, I'm just going to spin up a server just on this one computer that can do this. When the bot talks to it. And so you have the opposite problem. Now you have something that is just not at all RPA, it's just using the tool to, uh, you know, manipulate stuff, programmatically.

[00:45:35] **Jeremy:** so, as a part of all this, is using the same credentials as a real user, right. You're you're logging in with a username and password. if the form requires something like two factor authentication or, you know, or something like that, like, how does that work since it's not an actual person?

[00:45:55] **Alex:** Right. So in a perfect world, you're correct. Um, a bot is a user. I know a lot of times you'll hear, say, people will be like, oh, hi, I have 20 RPA bots. What they're usually saying is I have 20 automations that are being run for separate processes, with one user's credentials, uh, on a VDI. So you're right.

They, they are using a user's credentials with the same permissions that any user that does that process has, that's why it's easy. but now we have these concepts, like two factor authentication, which every organization is using that should require something that exists outside of that bot users environment. And so how do you afford for that in a perfect world? It would be a service account, not a user account and service accounts are governed a little differently. A lot of times service accounts, um, have much more stringent rules, but also allow for things like password resets, not a thing, um, or two factor authentication is not a thing for those.

So that would be the perfect solution, but now you're dragging in IT. Um, so, you know, if you're not structurally set up for that, that's going to be a long slog. Uh, so what would want to do some people actually literally have a, we'll have a business person that has their two factor auth for that bot user on their phone.

And then just, you know, they'll just go in and say, yeah.

that's me. that's untenable. So, um, sometimes what a lot of these, like Microsoft, for instance, allow you to do is to install a two factor authentication, application, um, on your desktop so that when you go to log in a website and says, Hey, type in your password.

Cool. Okay. Give me that code. That's on your two factor auth app. The bot can actually launch that. Copy the code and paste it in there and be on its way. But you're right now, you're having to afford for things that aren't really part of the process you're trying to automate. They are the incidentals that also happen.

And so you have to build your bot to afford for those things and interpret, oh, I need to do two factor authentication. And a lot of times, especially if you have an entirely business focused PA um, robotic operating model, they will forget about those things or find ways around them that the bot isn't addressing, like having that authenticator app on their phone.

that's, um, stuff that definitely needs to be addressed. And sometimes is only, found at runtime like, oh, it's asking for login. And when I developed it, I didn't need to do that because I had, you know, the cookie that said you're good for 30 days, but now, oh, no. 

[00:48:47] **Jeremy:** yeah. You could have two factor. Um, you could have, it asking you to check your email for a code. There could be a fraud warning. There's like all sorts of, you know, failure cases that can happen. 

[00:48:58] **Alex:** exactly. And those things are when we talk about, uh, third-party vendors, um, third-party provider vendors, like going back to the banking website, if you don't tell them that you're going to be using a bot to get their information or to interface with that website, you're setting yourself up for a bad time because they're going to see that kind of at runtime behavior that is not possible at scale by user.

And so you run into that issue at runtime, but then you're correct. There are other things that you might run into at runtime that are not again, part of the process, the business didn't think that that was part of the process. It's just something they do that actually the bot has to afford for. that's part of the journey, uh, in building these. 

[00:49:57] **Jeremy:** when you're, when you're building these, these bots, what are the types of tools that, that you've used in the past? Are these commercial, packages, are these open source? Like what, what does that ecosystem look like?

[00:50:11] **Alex:** Yeah, in this space, we have three big ones, which is, uh, automation anywhere UI path and, blue prism. Those are the RPA juggernauts providing this software to the companies that need it. And then you have smaller ones that are, trying to get in there, or provide stuff in a little different way. and you even have now, big juggernauts that are trying to provide for it, like Microsoft with something like power automate desktop.

So all of these, say three years ago, all of these softwares existed or all of these RPA solution softwares existed or operated in the same kind of way, where you would install it on your desktop. And it would provide you a studio to either record or define, uh, originally the process that was going to be automated on that desktop when you pushed play and they all kind of expose or operate in the same way they would interpret the COM or the DOM that the operating system provided. Things like task scheduler have traditionally, uh, exposed, uh, and they all kind of did that in the same way. Their value proposition in their software was the orchestration capability and the management of that.

So I build a bot to do this, Jim over there built a bot to do that. Okay. This RPA software, not only enabled you to define those processes, But what their real value was is they enable a place where I can say this needs to run at this time on this computer.

And it needs to, you know, I need to be able to monitor it and it needs to return information and all that kind of orchestration capability. Now all of these RPA solutions actually exist in that, like everything else in the browser. So instead of installing, you know, the application and launching it and, and whatnot, and the orchestration capability being installed on another computer that looked at these computers and ran stuff on them.

Now it's, it's all in the cloud as it were, and they are in the browser. So I go to. Wherever my RPA solution is in my browser. And then it says, okay, cool. You, you still need to install something on the desktop where you want the spot to run and it deploys it there. But I define and build my process in the provided browser studio.

And then we're going to give you a capability to orchestrate, monitor, and, uh, receive information on those things that you have, those bots that you have running, and then what they're now providing as well is the ability to tie in other services to your bot so that it has expanded capability. So I'm using automation anywhere and I built my bot and it's going, and it's doing this or that.

And automation anywhere says, Hey, that's cool. Wouldn't you like your bot to be able to do OCR? Well, we don't have our own OCR engine, but you probably as an enterprise do. Just use, you know, use your Kofax OCR engine or Hey, if you're really a high speed, why don't you use your Azure cognitive services capability?

We'll tie it right into our software. And so when you're building your bot, instead of just cracking open a PDF and send key control C and key control V to do stuff instead, we'll use your OCR engine that you've already paid for to, to understand stuff. And so that's, how they expand, what they're offering, um, into addressing more and more capabilities.



[00:53:57] **Alex:** But now we're, we're migrating into a territory where it's like, well, things have APIs why even build a bot for them. You know, you can just build a program that uses the API and the user can drive this. And so that's where people kind of get stuck. It's they they're using RPA on a, something that just as easily provides for a programmatic solution as opposed to an RPA solution.

but because they're in their RPA mode and they say, we can use a bot for everything, they don't even stop and investigate and say, Hey, wouldn't this be just as easy to generate a react app and let a user use this because it has an API and IT can just as easily monitor and support that because it's in an Azure resource bucket.

that's where an organization needs to be. Clear-eyed and say, Okay. at this point RPA is not the actual solution. We can do this just as easy over here and let's pursue that. 

[00:54:57] **Jeremy:** the experience of making these RPAs. It sounds like you have this browser-based IDE, there's probably some kind of drag and drop set up, and then you, you, you mentioned JavaScript. So I suppose, does that mean you can kind of dive a little bit deeper and if you want to set up specific rules or loops, you're actually writing that in JavaScript.

[00:55:18] **Alex:** Yeah. So not, not necessarily. So, again, the business does not know what an IDE is. It's a studio. Um,

so that's, but you're correct. It's, it's an IDE. Um, each, whether we're talking about blue prism or UiPath or automation anywhere, they all have a different flavor of what that looks like and what they enable.

Um, traditionally blue prism gave you, uh, a studio that was more shape based where you are using UML shapes to define or describe your process. And then there you are, whereas automation anywhere traditionally used, uh, essentially lines or descriptors. So I say, Hey, I want to open this file. And your studio would just show a line that said open file.

You know, um, although they do now, all of them have a shape based way to define your process. Go here, here. You know, here's a circle which represents this. Uh, let's do that. Um, or a way for you to kind of more, um, creatively define it in a, like a text-based way. When we talk about Java script, um, or anything like that, they provide predefined actions, all of them saying, I want to open a file or execute this that you can do, but all of them as well, at least last time I checked also allow you for a way to say, I want to programmatically run something I want to define.

And since they're all in the browser, it is, uh, you know, Javascript that you're going to be saying, Hey, run this, this JavaScript, run this function. Um, previously, uh, things like automation anywhere would, uh, let you write stuff in, in .NET essentially to do that capability. But again, now everything's in the browser.

So yeah, they do, They do provide for a capability to introduce more low level capability to your automation. That can get dangerous. Uh, it can be powerful and it can be stabilizing, but it can be a very slippery slope where you have an RPA solution bot that does the thing. But really all it does is it starts up and then executes code that you built.

[00:57:39] **Alex:** Like what, what was the, the point in the first place? 

[00:57:43] **Jeremy:** Yeah. And I suppose at that point, then anybody who knows how to use the RPA tool, but isn't familiar with that code you wrote, they're just, they can't maintain it 

[00:57:54] **Alex:** you have business continuity and this goes back to our, it has to be replicable or close as close to the human process, as you can make. Because that's going to be the easiest to inherit and support. That's one of the great things about it. Whereas if you're a low level programmer, a dev who says, I can easily do this with a couple of lines of, you know, dot net or, you know, TypeScript or whatever.

And so the bot just starts up in executes. Well, unless someone that is just as proficient comes along later and says, this is why it's breaking you now have an unsupportable business, solution. that's bad Juju. 

[00:58:38] **Jeremy:** you have the software engineers who they want to write code. then you have the people who are either in business or in IT that go, I don't want to look at your code.

I don't want to have to maintain it. Yeah. So it's like you almost, if you're a software engineer coming in, you almost have to fight that urge to, to write anything yourself and figure out, okay, what can I do with the tool set and only go to code if I can't do it any other way.

[00:59:07] **Alex:** That's correct. And that's the, it takes discipline. more often than not, not as fun as writing the code where you're like, I can do this. And this is really where the wheels come off is. You went to the business that is that I have this process, very simple. I need to do this and you say, cool, I can do that.

And then you're sitting there writing code and you're like, but you know what? I know what they really want to do. And I can write that now. And so you've changed the process and while it is, and nine times out of 10, the business will be like, oh, that's actually what we wanted. The human process was just as close as we could get nothing else, but you're right.

That's, that's exactly what we needed. Thank you nine times out of 10. They'll love you for that. But now you own their process. Now you're the one that defined it. You have to do the business continuity. You have to document it. And when it falls over, you have to pick it back up and you have to retrain.

And unless you have an organizational capacity to say, okay, I've gone in and changed your process. I didn't automate it. I changed it. Now I have to go in and tell you how I changed it and how you can do it. And so that, unless you have built your robotic operating model and your, your team to afford for that, your developer could be writing checks bigger than they can cash.

Even though this is a better capability. 

[01:00:30] **Jeremy:** you, you sort of touched on this before, and I think this is probably the, the last topic we'll cover, but you've been saying how the end goal should be to not have to use the RPAs anymore 

And I wonder if you have any advice for how to approach that process and, and what are some of the mistakes you've seen people make

[01:00:54] **Alex:** Mm Hmm. I mean the biggest mistake I've seen organizations make, I think is throwing the RPA solution out there, building bots, and they're great bots, and they are creating that value. They're enabling you to save money and also, enabling your employees to go on and do better, more gratifying work. but then they say, that's, it that's as far as we're going to think, instead of taking those savings and saying, this is for replacing this pain point that we had to get a bot in the first place to do so.

That's a huge common mistake. Absolutely understandable if I'm a CEO or even, you know, the person in charge of, you know, um, enterprise transformation. Um, it's very easy for me to say, ha victory, here's our money, here's our savings. I justified what we've done. Go have fun. Um, and instead of saying, we need to squirrel this money away and give it to the people that are going to change the system. So that, that's definitely one of the biggest things.

The problem with that is that's not realized until years later when they're like, oh, we're still supporting these bots. So it is upfront having a turnoff strategy. When can we turn this bot off? What is that going to look like? Does it have a roadmap that will eventually do that?

And that I think is the best way. And that will define what kind of processes you do indeed build bots for is you go to it and say, listen, we've got a lot of these user processes, human processes that are doing this stuff. Is there anything on your roadmap that is going to replace that and they say, oh yeah you know, in three years we're actually going to be standing up our new thing.

We're going to be converting. And part of our, uh, analysis of the solution that we will eventually stand up will be, does it do these things? And so yes, in three years, you're good. And you say, cool, those are the processes I'm going to automate and we can shut those off. 

That's your point of entry for these things not doing that leads to bots running and doing things even after there is a enterprise solution for that. And more often than not, I would say greater than five times out of 10, when we are evaluating a process to build a bot for easily five times out of 10, we say, whoa, no, actually there's, you don't even need to do this.

Our enterprise application can do this. you just need retraining, because your process is just old and no one knew you were doing this. And so they didn't come in and tell you, Hey, you need to use this.

So that's really a lot of times what, what the issue is. And then after that, we go in and say, Okay.

no, there's, there's no solution for this. This is definitely a bot needs to do this. Let's make sure number one, that there isn't a solution on the horizon six months to a year, because otherwise we're just going to waste time, but let's make sure there is, or at least IT, or the people in charge are aware that this is something that needs to be replaced bot or no bot.

And so let's have an exit strategy. Let's have a turn-off strategy. 

When you have applications that are relatively modern, like you have a JIRA, a ServiceNow, you know, they must have some sort of API and it may just be that nobody has come in and told them, you just need to plug these applications together.



[01:04:27] **Alex:** And so kind of what you're hitting on and surfacing is the future of RPA. Whereas everything we're talking about is using a bot to essentially bridge a gap, moving data from here to there that can't be done, programmatically. Accessing something from here to there that can't be done programmatically.

So we use a bot to do it. That's only going to exist for so long. Legacy can only be legacy for so long, although you can conceivably because we had that big COBOL thing, um, maybe longer than we we'd all like, but eventually these things will be. upgraded. and so either the RPA market will get smaller because there's less legacy out there.

And so RPA as a tool and a solution will become much more targeted towards specific systems or we expand what RPA is and what it can afford for. And so that I think is more likely the case. And that's the future where bots or automations aren't necessary interpreting the COM and the DOM and saying, okay, click here do that.

But rather you're able to quickly build bots that utilize APIs that are built in and friendly. And so what we're talking about there is things like Appian or MuleSoft, which are these kind of API integrators are eventually going to be classified as RPA. They're going to be within this realm.

And I think, where, where you're seeing that at least surfaced or moving towards is really what Microsoft's offering in that, where they, uh, they have something called power automate, which essentially is it just a very user-friendly way to access API. that they built or other people have built.

So I want to go and I need to get information to service now, service now has an API. Yeah. Your, IT can go in and build you a nice little app that does a little restful call to it, or a rest API call to it gets information back, or you can go in and, you know, use Microsoft power automate and say, okay, I want to access service now.

And it says, cool. These are the things you can do. And I say, okay, I just want to put information in this ticket and we're not talking about get or patch or put, uh, or anything like that. We're just saying, ah, that's what it's going to do. And that's kind of what Microsoft is, is offering. I think that is the new state of RPA is being able to interface in a user-friendly way with APIs. Cause everything's in the browser to the point. where, you know, Microsoft's enabling add ins for Excel to be written in JavaScript, which is just the new frontier. Um, so that's, that's kind of going to be the future state of this. I believe. 

[01:07:28] **Jeremy:** so, so moving from RPAs being this thing, that's gonna click through website, click through, um, a desktop application instead it's maybe more of this high, higher level tool where the user will still get this, I forget the term you used, but this tool to build a workflow, right. A studio. Okay. Um, and instead of saying, oh, I want this to click this button or fill in this form.

It'll be, um, I want to get this information from service now. And I want to send a message using that information to slack or to Twilio, or, um, you're basically, talking directly to these different services and just telling it what you want and where it should go.

[01:08:14] **Alex:** That's correct. So, as you said, everything's going to have an API, right? Seemingly everything has an API. And so instead of us, our RPA bots or solutions being UI focused, they're going to be API focused, um, where it doesn't have to use the user interface. It's going to use the other service. And again, the cool thing about APIs in that way is that it's not, directly connecting to your data source.

It's the same as your UI for a user. It sits on top of it. It gets the request and it correctly interprets that. And does it the same thing with your UI where I say I click here and you know, wherever it says. okay. yeah. You're allowed to do that. Go ahead. So that's kind of that the benefit to that.

Um, but to your point, the, the user experience for whether you're using a UI or API to build up RPA bot, it's going to be the same experience for the user. And then at this point, what we're talking about, well, where's the value offering or what is the value proposition of RPA and that's orchestration and monitoring and data essentially.

we'll take care of hosting these for you. we'll take care of where they're going to run, uh, giving you a dashboard, things like that.

[01:09:37] **Alex:** That's a hundred percent correct. It's it's providing a view into that thing and letting the business say, I want to no code this. And I want to be able to just go in and understand and say, oh, I do want to do that. I'm going to put these things together and it's going to automate this business process that I hate, but is vital, and I'm going to save it, the RPA software enables you to say, oh, I saw they did that. And I see it's running and everything's okay in the world and I want to turn it on or off. And so it's that seamless kind of capability that that's what that will provide. 

And I think that's really where it isn't, but really where it's going. Uh, it'll be interesting to see when the RPA providers switch to that kind of language because currently and traditionally they've gone to business and said, we can build you bots or no, no, your, your users can build bots and that's the value proposition they can go in.

And instead of writing an Excel where you had one very, very advanced user. Building macros into Excel with VBA and they're unknown to the, the IT or anybody else instead, you know, build a bot for it. And so that's their business proposition today. 

Instead, it's going to shift, and I'd be interested to see when it shifts where they say, listen, we can provide you a view into those solutions and you can orchestrate them in, oh, here's the studio that enables people to build them.

But really what you want to do is give that to your IT and just say, Hey, we're going to go over here and address business needs and build them. But don't worry. You'll be able to monitor them and at least say, yeah okay. this is, this is going.

[01:11:16] **Jeremy:** Yeah. And that's a, a shift. It sounds like where RPA is currently, you were talking about how, when you're configuring them to click on websites and GUIs, you really do still need someone with the software expertise to know what's going on. but maybe when you move over to communicating with API, Um, maybe that won't be as important maybe, somebody who just knows the business process really can just use that studio and get what they need.

[01:11:48] **Alex:** that's correct. Right. Cause the API only enables you to do what it defined right. So service now, which does have a robust API, it says you can do these things the same as a user can only click a button that's there that you've built and said they can click. And so that is you can't go off the reservation as easy with that stuff, really what's going to become prime or important is as no longer do I actually have an Oracle server physically in my location with a database.

Instead I'm using Oracle's cloud capability, which exists on their own thing. That's where I'm getting data from. What becomes important about being able to monitor these is not necessarily like, oh, is it falling over? Is it breaking? It's saying, what information are you sending or getting from these things that are not within our walled garden.

And that's really where, it or the P InfoSec is, is going to be maybe the main orchestrator owner of RPA, because they're, they're going to be the ones to say you can't, you can't get that. You're not allowed to get that information. It's not necessarily that you can't do it. Um, and you can't do it in a dangerous way, but it's rather, I don't want you transporting that information or bringing it in.

So that's, that's really, what's the what's going to change. 

[01:13:13] **Jeremy:** I think that's a good place to wrap it up, but, uh, is there anything we missed or anything else you want to plug before we go?

[01:13:21] **Alex:** No. Uh, I think this was uh pretty comprehensive and I really enjoyed it. 

Alex thanks for coming on the show

[01:13:28] **Alex:** No, thank you for having me. It's been, it's been a joy.

[01:13:31] **Jeremy:** This has been Jeremy Jung for software engineering radio. Thanks for listening. 

</div>