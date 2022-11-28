+++
title = "Jonathan Shariat on Tragic Design"

description = "Jonathan Shariat discusses how to avoid building harmful software"

[extra]
episode_url = "https://pinecast.com/listen/8b2cc5d8-3d06-4408-8415-8b856ca53b16.mp3"
+++

Jonathan Shariat is the coauthor of the book Tragic Design and cohost of the Design Review Podcast. He's currently a Sr. Interaction Designer & Accessibility Program Lead at Google.

This episode originally aired on Software Engineering Radio.

### Topics covered:

- How poor design kills in medical environments
- Causing harm with features meant to bring joy
- Considerations during the product development cycle
- Industry specific checklists and testing requirements
- Creating guiding principles for a team
- Why medical software often has poor UX
- Designing for crisis situations
- Why dark patterns can be bad in the long term

### Related Links

- [@designuxui](https://twitter.com/designuxui)
- [Tragic Design](https://www.tragicdesign.com/)
- [How Bad UX Killed Jenny](https://medium.com/tragic-design/how-bad-ux-killed-jenny-ef915419879e)
- [Design Review podcast](https://anchor.fm/designreview/)
- [Deceptive Design](https://www.deceptive.design/)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** Today I'm talking to Jonathan Shariat, he's the co-author of Tragic design. The host of the design review podcast. And he's currently a senior interaction designer and accessibility program lead at Google. Jonathan, welcome to software engineering radio.

[00:00:15] **Jonathan:** Hi, Jeremy, thank you So much for having me on.

[00:00:18] **Jeremy:** the title of your book is tragic design. And I think that people can take a lot of different meanings from that. So I wonder if you could start by explaining what tragic design means to you.

[00:00:33] **Jonathan:** Hmm. For me, it really started with this story that we have in the beginning of the book. It's also online. Uh, I originally wrote it as a medium article and th that's really what opened my eyes to, Hey, you know, design has, is, is this kind of invisible world all around us that we actually depend on very critically in some cases.

And So this story was about a girl, you know, a nameless girl, but we named her Jenny for the story. And in short, she came for treatment of cancer at the hospital, uh, was given the medication and the nurses that were taking care of her were so distracted with the software they were using to chart, make orders, things like that, that they miss the fact that she needed hydration and that she wasn't getting it.

And then because of that, she passed away. And I still remember that feeling of just kind of outrage. And, you know, when we hear a lot of news stories, A lot of them are outraging. they, they touch us, but some of them, some of those feelings stay and they stick with you.

And for me, that stuck with me, I just couldn't let it go because I think a lot of your listeners will relate to this. Like we get into technology because we really care about the potential of technology. What could it do? What are all the awesome things that could do, but we come at a problem and we think of all the ways it could be solved with technology and here it was doing the exact opposite.

It was causing problems. It was causing harm and the design of that, or, you know, the way that was built or whatever it was failing Jenny, it was failing the nurses too, right? Like a lot of times we blame that end user and, and it caused it. So to me, that story was so tragic. Something that deeply saddened me and was regrettable and cut short someone's uh, you know, life and that's the definition of tragic, and there's a lot of other examples with varying degrees of tragic, but, um, you know, as we look at the impact technology has, and then the impact we have in creating those technologies that have such large impacts, we have a responsibility to, to really look into that and make sure we're doing as best of job as we can and avoid those as much as possible.

Because the biggest thing I learned in researching all these stories was, Hey, these aren't bad people. These aren't, you know, people who are clueless and making these, you know, terrible mistakes. They're me, they're you, they're they're people. Um, just like you and I, that could make the same mistakes.

[00:03:14] **Jeremy:** I think it's pretty clear to our audience where there was a loss of life, someone, someone died and that's, that's clearly tragic. Right? So I think a lot of things in the healthcare field, if there's a real negative outcome, whether it's death or severe harm, we can clearly see that as tragic.

and I, I know in your book you talk about a lot of other types of, I guess negative things that software can cause. So I wonder if you could, explain a little bit about now past the death and the severe injury. What's tragic to you.

[00:03:58] **Jonathan:** Yeah. still in that line of like of injury and death, And, you know, the side that most of us will actually, um, impact, our work day-to-day is also physical harm. Like, creating this software in a car. I think that's a fairly common one, but also, ergonomics, right?

Like when we bring it back to something like less impactful, but still like multiplied over the impact of, multiplied over the impact of a product rather, it can be quite, quite big, right? Like if we're designing software in a way that's very repetitive or, you know, everyone's, everyone's got that, that like scroll, thumb, scroll, you know, issue.

Right. if, uh, our phones aren't designed well, so there's a lot of ways that it can still physically impact you ergonomically. And that can cause you a lot of problem arthritis and pain, but yeah, there's, there's other, there's other, other ways that are still really impactful. So the other one is by saddening or angry.

You know, that emotional harm is very real. And oftentimes sometimes it gets overlooked a little bit because it's, um, you know, physical harm is what is so real to us, but sometimes emotional harm isn't. But, you know, we talk about in the book, the example of Facebook, putting together this great feature, which takes your most liked photo, and, you know, celebrates your whole year by you saying, Hey, look at as a hero, you're in review this, the top photo from the year, they add some great, you know, well done illustrations behind it, of, of balloons and confetti and, people dancing.

But some people had a bad year. Some people's most liked engaged photo is because something bad happened and they totally missed. And because of that, people had a really bad time with this where, you know, they lost their child that year. They lost their loved one that year, their house burnt down. Um, something really bad happened to them.

And here was Facebook putting that photo of their, of their dead child up with, you know, balloons and confetti and people dancing around it. And that was really hard for people. They didn't want to be reminded of that. And especially in that way, and these emotional harms also come into the, in the play of, on anger.

You know, we talk about, well, one, you know, there's, there's a lot of software out there that, that, um, tries to bring up news stories that anger us and which equals engagement. Um, but also ones that, um, use dark patterns to trick us into purchasing and buying and forgetting about that free trial. So they charge us for a yearly subscription and won't refund us.

Uh, if you've ever tried to cancel a subscription, you start to see some real their their real colors. Um, so emotional harm and, uh, anger is a, is a big one. We also talk about injustice in the book where there are products that are supposed to be providing justice. Um, and you know, in very real ways like voting or, you know, getting people the help that they need from the government, or, uh, for people to see their loved ones in jail.

Um, or, you know, you're getting a ticket unfairly because you couldn't read the sign was you're trying to read the sign and you, and you couldn't understand it. so yeah, we look at a lot of different ways that design and our saw the software that we create can have very real impact on people's lives and in a negative way, if we're not careful. 

[00:07:25] **Jeremy:** the impression I get, when you talk about tragic design, it's really about anything that could harm a person, whether physically, emotionally, you know, make them angry, make them sad. And I think the, the most liked photo example is a great one, because like you said, I think the people may be building something that, that harms and they may have no idea that they're doing it.

[00:07:53] **Jonathan:** Exactly like that. I love that story because not, not to just jump on the bandwagon of saying bad things about like Facebook or something. No, I love that story because I can see myself designing the exact same thing, like being a part of that product, you know, building it, you know, looking at the, uh, the, the specifications, the, um, the, the PM, you know, put it that put together and the decks that we had, you know, like I could totally see that happening.

And just never, I think, never having the thought, because our we're so focused on like delighting our users and, you know, we have these metrics and these things in mind. So that's why, like, in the book, we really talk about a few different processes that need to be part of. Product development cycle to stop, pause, and think about like, well, what are the, what are the negative aspects here?

Like what are the things that could go wrong? What are the, what are the other life experiences that are negative? Um, that could be a part of this and you don't need to be a genius to think of every single thing out there. You know, like in this example, I think just talking about, you know, like, oh, well, some people might've had, you know, if they would have taken probably like, you know, one hour out of their entire project, or maybe even 10 minutes, they might've come up with like, oh, there could be bad thing.

Right. But, um, so if you don't have that, that, that moment to pause that moment to just say, okay, we have time to brainstorm together about like how this could go wrong or how, you know, the negative of life could be impacted by this, um, feature that that's all that it takes. It doesn't necessarily mean that you need to do.

You know, giant study around the impact, potential impact of this product and all the, all the ways, but really just having a part of your process that takes a moment to think about that will just create a better product and better, product outcomes. You know, if you think about all of life's experiences and Facebook can say, Hey, condolences, and like, you know, and show that thoughtfulness that would be, uh, I would have that have higher engagement that would have higher, uh, satisfaction, right?

So they could have created a better outcome by considering these things and obviously avoid the impact negative impact to users and the negative impact to their product. 

[00:10:12] **Jeremy:** continuing on with that thought you're a senior interaction designer and you're an accessibility program lead. And so I wonder on the projects that you work on, and maybe you can give us a specific example, but how are you ensuring that you're, you're not running up against these problems where you build something that you think is going to be really great, um, for your users, but in reality ends up being harmful and specifically.

[00:10:41] **Jonathan:** Yeah, one of the best ways is, I mean, it should be part of multiple parts of your cycle. If, if you want something, if you want a specific outcome out of your product development life cycle, um, it needs to be from the very beginning and then a few more times, so that it's not, you know, uh, I think, uh, programmers, uh, will all latch onto this, where they have the worst end of the stick, right?

Because a and Q and QA as well. Because, you know, any bad decision or assumption that's happened early on with, you know, the, the business team or, or the PM, you know, gets like multiplied when they talk to the designer and then gets multiplied again, they hand it off. And it's always the engineer who has to, has to put the final foot down, be like, this doesn't make sense.

Or I think users are going to react this way, or, you know, this is the implication of that, that assumption. So, um, it's the same thing, you know, in our team, we have it in the very early stage when someone's putting together the idea for the feature, our project, we want to work on it's right there. There's a few, there's like a section about accessibility and a few other sections, uh, talking about like looking out for this negative impact.

So right away, we can have a discussion about it when we're talking about like what we should do about this and the D and the different, implications of implementing it. That's the perfect place for it. You know, like maybe, maybe when you're a brainstorm. Uh, about like, what should we should do? Maybe it's not okay there because you're trying to be creative.

Right. You're trying to think. But at the very next step, when you're saying, okay, like what would it mean to build this that's exactly where I should start showing up and, you know, the discussion from the team. And it depends also the, the risk involved, right? Like, uh, it depends, which is attached to how much, uh, time and effort and resources you should put towards avoiding that risk it's risk management.

So, you know, if you work, um, like my, um, you know, colleagues, uh, or, you know, some of my friends were working in the automotive industry and you're creating a software and you're worried that it might be distracting. There might be a lot more time and effort or the healthcare industry. Um, those were, those are, those might need to take a lot more resources, but if you're a, maybe a building, um, you know, SaaS software for engineers to spin up, you know, they're, um, you know resources.

Um, there might be a different amount of resources. It never is zero, uh, because you still have, are dealing with people and you'll impact them. And, you know, maybe, you know, that service goes down and that was a healthcare service that went down because of your, you know, so you really have to think about what the risk is.

And then you can map that back to how much time and effort you need to be spending on getting that. Right. And accessibility is one of those things too, where a lot of people think that it takes a lot of effort, a lot of resources to be accessible. And it really isn't. It just, um, it's just like tech debt, you know, if, if you have ignored your tech debt for, you know, five years, and then they're saying, Hey, let's all fix all the tech debt. Yeah. Nobody's going to be on board for that as much. Versus like, if, if addressing that and finding the right level of tech debt that you're okay with and when you address it and how, um, because, and just better practice. That's the same thing with accessibility is like, if you're just building it correctly, as you go, it's, it's very low effort and it just creates a better product, better decisions.

Um, and it is totally worth the increased amount of people who can use it and the improved quality for all users. So, um, yeah, it's just kind of like a win-win situation.

[00:14:26] **Jeremy:** one of the things you mentioned was that this should all start. At the very beginning or at least right after you've decided on what kind of product you're going to build, and that's going to make it much easier than if you come in later and try to, make fixes then, I wonder when you're all getting together and you're trying to come up with these scenarios, trying to figure out negative impacts, what kind of accessibility, needs you need to have, who are the people who are involved in that conversation?

Like, um, you know, you have a team of 50 people who needs to be in the room from the very beginning to start working this out.

[00:15:05] **Jonathan:** I think it would be the same people who are there for the project planning, like, um, at, on my team, we have our eng counter counterparts there. at least the team lead, if, if, if there's a lot of them, but you know, if they would go to the project kickoff, uh, they should be there.

you know, we, we have everybody in their PM, design, engineers, um, our project manager, like anyone who wants to contribute, uh, should really be there because the more minds you have with this the better, and you'll, you'll tease out much, much more of, of of all the potential problems because you have a more, more, um, diverse set of brains and life experiences to draw from.

And so you'll, you'll get closer to that 80% mark, uh, that you can just quickly take off a lot of those big items off the table, right? 

[00:16:00] **Jeremy:** Is there any kind of formal process you follow or is it more just, people are thinking of ideas, putting them out there and just having a conversation.

[00:16:11] **Jonathan:** Yeah, again, it depends which industry you're in, what the risk is. So I previously worked at a healthcare industry, um, and for us to make sure that we get that right, and how it's going to impact the patients, especially though is cancer care. And they were using our product to get early warnings of adverse effects.

Our, system of figuring that like, you know, if that was going to be an issue was more formalized. Um, in, in some cases, uh, like, like actually like healthcare and especially if the, if it's a device or, or in certain software circumstances, it's determined by the FDA to be a certain category, you literally have a, uh, governmental version of this.

So the only reason that's there is because it can prevent a lot of harm, right? So, um, that one is enforced, but there's, there's reasons, uh, outside of the FDA to have that exact formalized part of your process. And it can, the size of it should scale depending on what the risk is. So on my team, the risk is, is actually somewhat low.

it's really just part of the planning process. We do have moments where we, we, um, when we're, uh, brainstorming like what we should do and how the feature will actually work. Where we talk about like what those risks are and calling out the accessibility issues. And then we address those. And then as we are ready to, um, get ready to ship, we have another, um, formalized part of the process.

There will be check if the accessibility has been taken care of and, you know, if everything makes sense as far as, you know, impact to users. So we have those places, but in healthcare, but it was much stronger where we had to, um, make sure that we re we we've tested it. We've, uh, it's robust. It's going to work on, we think it's going to work.

Um, we, you know, we do user testing has to pass that user testing, things like that before we're able to ship it, uh, to the end user.

[00:18:12] **Jeremy:** So in healthcare, you said that the FDA actually provides, is it like a checklist of things to follow where you must have done this? As you're testing and you must have verified these, these things that's actually given to you by the government.

[00:18:26] **Jonathan:** That's right. Yeah. It's like a checklist and the testing requirement. Um, and there's also levels there. So, I have, I've only, I've only done the lowest level. I know. There's like, I think like two more levels above that. Um, and again, that's like, because the risk is higher and higher and there's more stricter requirements there where maybe somebody in the FDA needs to review it at some point.

And, um, so again, like mapping it back to the risk that your company has is, is really important to understanding that is going to help you avoid and, and build a better product, avoid, you know, the bad impact and build a better product. And, and I think that's one of the things I would like to focus on as well.

And I'd like to highlight for your, for your listeners, is that, it's not just about avoiding tragic design because one thing I've discovered since writing the book and sharing it with a lot of people. Is that the exact opposite thing is usually, you know, in a vast majority of the cases ends up being a strategically great thing to pursue for the product and the company.

You know, if you think about, that, that example with, with Facebook, okay. You've run into a problem that you want to avoid, but if you actually do a 180 there and you find ways to engage with people, when they're grieving, you find people to, to develop features that help people who are grieving, you've created a value to your users, that you can help build the company off of.

Right. Um, cause they were already building a bunch of joy features. Right. Um, you know, and also like user privacy, like I, we see apple doing that really well, where they say, okay, you know, we are going to do our ML on device. We are going to do, you know, let users decide on every permission and things like that.

And that, um, is a strategy. We also see that with like something like T-Mobile, when they initially started out, they were like one of the nobody, uh, telecoms in the world. And they said, okay, what are all the unethical bad things that, uh, our competitors are doing? They're charging extra fees, you know, um, they have these weird data caps that are really confusing and don't make any sense their contracts, you get locked into for many years.

They just did the exact opposite of that. And that became their business strategy and it, and it worked for them now. They're, they're like the top, uh, company. So, um, I think there's a lot of things like that, where you just look at the exact opposite and, you, one you get to avoid the bad, tragic design, but you also see boom, you see an opportunity that, um, become, become a business strategy.

[00:21:03] **Jeremy:** So, so when you referred to exact opposite, I guess you're, you're looking for the potentially negative outcomes that could happen. there was the Facebook example of, of seeing a photo or being reminded of a really sad event and figuring out can I build a product around, still having that same picture, but recontextualizing it like showing you that picture in a way that's not going to make you sad or upset, but is actually a positive.

[00:21:35] **Jonathan:** Yeah. I mean, I don't know maybe what the solution was, but like one example that comes to mind is some companies. Now, before mother's day, we'll send you an email and say, Hey, this is coming up. Do you want us to send you emails about mother's day? Because for some people that's Can, be very painful. That's that's very thoughtful.

Right. And that's a great way to show that you, that you care. Um, but yeah, like, you know, uh, thinking about that Facebook example, like if there's a formalized way to engage with, with grieving, like, I would use Facebook for that. I don't use Facebook very often or almost at all, but you know, if somebody passed away, I would engage right with my, my Facebook account.

And I would say, okay, look, there's like, there's this whole formalized, you know, feature around, you know, uh, and, and Facebook understands grieving and Facebook understands like this w this event and may like smooth that process, you know, creates comfort for the community that's value and engagement. that is worthwhile versus artificial engagement.

That's for the sake of engagement. and that would create, uh, a better feeling towards Facebook. Uh, I would maybe like then spend more time on Facebook. So it's in their mutual interest to do it the right way. Um, and so it's great to focus on these things to avoid harm, but also to start to see new opportunities for innovation.

And we see this a lot already in accessibility where there's so many innovations that have come from just fixing accessibility issues like closed captions. We all use it, on our TVs, in busy crowded spaces, on, you know, videos that have no, um, uh, translation for us in different places.

So, SEO is, is the same thing. Like you get a lot of SEO benefit from, you know, describing your images and, and making everything semantic and things like that. And that also helps screen readers. and different innovations have come because somebody wanted to solve an accessibility need.

And then the one I love, I think it's the most common one is readability, like contrast and tech size. Sure. There's some people who won't be able to read it at all, but it hurts my eyes to read bad contrast and bad text size. And so it just benefits. Everyone creates a better design. And one of the things that comes up so often when I'm, you know, I'm the accessibility program lead.

And so I see a lot of our bugs is so many issues that, that are caught because of our, our audits and our, like our test cases around accessibility that just our bad design and our bad experience for everyone. And so we're able to fix that. And, uh, and it's just like an another driver of innovation and there's, there's, there's a ton of accessibility examples, and I think there's also a ton of these other, you know, ethical examples or, you know, uh, avoiding harm where you just can see it. It's an opportunity area where it's like, oh, let's avoid that. But then if you turn around, you can see that there's a big opportunity to create a business strategy out of it.

[00:24:37] **Jeremy:** Can, can you think of any specific examples where you've seen that? Where somebody, you know, doesn't treat it as something to avoid, but, but actually sees that as an opportunity.

[00:24:47] **Jonathan:** Yeah. I mean, I, I think that the, um, the apple example is a really good one where from the beginning, like they, they saw like, okay, in the market, there's a lot of abuse of information and people don't like that. So they created a business strategy around that And that's become a big differentiator for them.

Right. Like they, they have like ML on the device. They do. Um, they have a lot of these permission settings, you know, the Facebook. It was very much focused right. On, on using customer data and a lot of it without really asking their permission. And so once apple said, okay, now all apps need to show what you're tracking.

And, and then, um, and asked for permission to do that. A lot of people said no, and that caused about $10 billion of loss for, for Facebook. and for, for apple, it's, you know, they advertise on that now that we're, you know, ethical that, you know, we, we source things ethically and we, we care about user privacy and that's a strong position, right?

Uh, I think there's a lot of other examples out there. Like I mentioned accessibility and others, but like it they're kind of overflowing, so it's hard to pick one.

[00:25:58] **Jeremy:** Yeah. And I think what's interesting about that too, is with the example of focusing on user privacy or trying to be more sensitive around, death or things like that, as I think that other people in the industry will, will notice that, and then in their own products, then they may start to incorporate those things as well.

[00:26:18] **Jonathan:** Yeah. Yeah, exactly what the example of with T-Mobile. once that worked really, really well and they just ate up the entire market, all the other companies followed suit, right? Like now, um, having those data caps that, you know, are, are very rare, having those surprise fees are a lot, uh, rare.

Um, you know, there's, there's no more like deep contracts that lock you in and et cetera, et cetera. A lot of those have become industry standard now. Um, and so It, and it does improve the environment for everyone because, because now it becomes a competitive advantage that everybody needs to meet. Um, so yeah, I think that's really, really important.

So when you're going through your product's life cycle, you might not have the ability to make these big strategic decisions. Like, you know, we want to, you know, not have data caps or whatever, but, you know, if you, if you're on that Facebook level and you run into that issue, you could say, well, look, what could we do to address this?

What could we could do to, to help this and make, make that a robust feature? You know, when we talk about, lot of these dating apps, one of the problems was a lot of abuse, where women were being harassed or, you know, after the day didn't go well and you know, things were happening. And so a lot of apps have now dif uh, these dating apps have differentiated themselves and attracted a lot of that market because they deal with that really well.

And they have, you know, it's built into the strategy. It's oftentimes like a really good place to start too, because one it's not something we generally think about very, very well, which means your competitors. Haven't thought about it very well, which means it's a great place to, to build products, ideas off of. 

[00:27:57] **Jeremy:** Yeah, that's a good point because I think so many applications now are like social media applications, their messaging applications there, their video chat, that sort of thing. I think when those applications were first built, they didn't really think so much about what if someone is, you know, sending hateful messages or sending, pictures that people really don't want to see.

Um, people are doing abusive things. It was like, they just assume that, oh, people will be, people will be good to each other and it'll be fine. But, uh, you know, in the last 10 years, pretty much all of the major social media companies have tried to figure out like, okay, um, what do I do if someone is being abusive and, and what's the process for that?

And basically they all have to do something now. Um,

Um 

[00:28:47] **Jonathan:** Yeah. And that's a hard thing to like, if, if that, uh, unethical or that, um, bad design decision is deep within your business strategy and your company's strategy. It's hard to undo that like some companies are still, still have to do that very suddenly and deal with it. Right. Like, uh, I know Uber had a big, big part of them, like, uh, and some other companies, but, uh, we're like almost suddenly, like everything will come to a head and they'll need to deal with it.

Or, you know, like, Twitter now try to try to get, be acquired by Elon Musk. Uh, some of those things are coming to light, but, I, what I find really interesting is that these these areas are like really ripe for innovation. So if you're interested in, a startup idea or you're, or you're working in a startup, or, you know, you're about to start one, you know, there's a lot of maybe a lot of people out there who are thinking about side projects right now, this is a great way to differentiate and win that market against other well-established competitors is to say, okay, well, what are they, what are they doing right now that is unethical. And it's like, you know, core to their business strategy and doing that differently is really what will help you, to win that market. And we see that happening all the time, you know, especially the ones that are like these established, uh, leaders in the market. they can't pivot like you can, so being able to say, I'm, we're going to do this ethically.

We're going to do this, uh, with, you know, with these tragic design in mind and doing the opposite, that's going to help you to, to find your, your attraction in the market.

[00:30:25] **Jeremy:** Earlier, we were talking about. How in the medical field, there is specific regulation or at least requirements to, to try and avoid this kind of tragic design. Uh, I noticed you also worked for Intuit before. Uh, um, so for financial services, I was wondering if there was anything similar where the government is stepping in and saying like, you need to make sure that, these things happen to avoid, these harmful things that can come up.

[00:30:54] **Jonathan:** Yeah, I don't know. I mean, I didn't work on TurboTax, so I worked on QuickBooks, which is like a accounting software for small businesses. And I was surprised, like we didn't have a lot, like a lot of those robust things, we just relied on user feedback to tell us like, things were not going well. And, you know, and I think we should have, like, I think, I think that that was a missed opportunity, um, to.

Show your users that you understand them and you care, and to find those opportunity areas. So we didn't have enough of that. And there was things that we shipped that didn't work correctly right out of the box, which, you know, it happens, but had a negative impact to users. So it's like, okay, well, what do we do about that?

How do we fix that? Um, and if the more you formalize that and make it part of your process, the more you get out of it. And actually this is like, this is a good, a good, um, uh, pausing point bit that I think will affect a lot of engineers listening to this. So if you remember in the book, we talk about the Ford Pinto story and there isn't, I want to talk about this story and why I added it to the book.

Is that, uh, one, I think this is the thing that engineers deal with the most, um, and, and designers do too, which is that okay. we see the problem, but we don't think it's worth fixing. Okay. Um, so that, that's what I'm going. That's what we're going to dig into here. So it's a, hold on for a second while I explain some, some history about this car.

So the Ford Pinto, if you're not familiar is notorious, uh, because it was designed, um, and built and shipped and there, they knowingly had this problem where if it was rear-ended at even like a pretty low speed, it would burst into flames because the gas tank would rupture the, and then oftentimes the, the, the doors would get jammed.

And so it became a death trap of fire and caused many deaths, a lot of injuries. And, um, in an interview with the CEO at the time, like almost destroyed Ford like very seriously would have brought the whole company down and during the design of it, uh, and design meaning in the engineering sense. Uh, and the engineering design of it, they say they found this problem and the engineers came up with their best solution.

Was this a rubber block. Um, and the cost was, uh, I forget how many dollars let's say it was like $9. let's say $6, but this is again, uh, back then. And also the margin on these cars was very, very, very thin and very important to have the lowest price in the market to win those markets. The customers were very price sensitive, so they, uh, they being like the legal team looked at like some recent, cases where they have the value of life and started to come up with like a here's how many people would sue us and here's how much it would cost to, uh, to, to settle all those.

And then here's how much it would cost to add this to all the cars. And it was cheaper for them to just go with the lawsuits and they, they found. Um, and I think why, I think why this is so important is because of the two things that happened afterward, one, they were wrong. it was a lot more people it affected and the lawsuits were for a lot more money.

And two after all this was going crazy and it was about to destroy the company, they went back to the drawing board and what did the engineers find? They found a cheaper solution. They were able to rework that, that rubber block and and get it under the margin and be able to hit the mark that they wanted to.

And I think that's, there's a lot of focus on the first part because it's so unethical to the value of life and, and, um, and doing that calculation and being like we're willing to have people die, but in some industries, it's really hard to get away with that, but it's also very easy. To get into that.

It's very easy to get lulled into this sense of like, oh, we're just going to crunch the numbers and see how many users it affects. And we're okay with that. Um, versus when you have principals and you have kind of a hard line and you, and you care a lot more than you should. And, and you really push yourself to create a more ethical, more, a safer, you know, avoiding, tragic design, then you, there there's a solution out there.

Like you actually get to innovation, you actually get to the solving the problem versus when you just rely on, oh, you know, the cost benefit analysis we did is that it's going to take an engineer in a month to fix this and blah blah blah. But if, if you have those values, if you have those principles and you're like, you know what, we're not okay shipping this, then you'll, you'll find that.

They're like, okay, there's, there's a cheaper way to, to fix this. There's another way we could address this. And that happens so often. and I know a lot of engineers deal with that. A lot of saying like, oh, you know, this is not worth our time to fix. This is not worth our time to fix. And that's why you need those principles is because oftentimes you don't see it and it's, but it's right there at right outside of the edge of your vision. 

[00:36:12] **Jeremy:** Yeah. I mean, with the Pinto example, I'm just picturing, you know, obviously there wasn't JIRA back then, but you can imagine that somebody's having an issue that, Hey, when somebody hits the back of the car, it's going to catch on fire. Um, and, and going like, well, how do I prioritize that? Right? Like, is this a medium ticket?

Is this a high ticket? And it's just like, it's just, it just seems insane, right? That you could, make the decision like, oh no, this isn't that big an issue. You know, we can move it down to low priority and, and, and, ship it.

Okay. 

[00:36:45] **Jonathan:** Yeah. And, and, and that's really what principals do for you, right? Is they help you make the tough decisions. You don't need a principle for an easy one. Uh, and that's why I really encourage people in the book to come together as a team and come up with what are your guiding principles. Um, and that way it's not a discussion point every single time.

It's like, Hey, we've agreed that this is something that we, that we're going to care about. This is something that we are going to stop and, fix. Like, one of the things I really like about my team at Google is product excellence is very important to us. and. there are certain things that, uh, we're, you know, we're Okay. with, um, letting slip and fixing at a next iteration.

And, you know, obviously we make sure we actually do that. Um, so it's not like we, we, we always address everything, but because it's one of our principles. We care more. We have more, we take on more of those tickets and we take on more of those things and make sure that they ship before, um, can make sure that they're fixed before we ship.

And, and it shows like to the end user that th that this company cares and they have quality. Um, so it's one of it. You need a principal to kind of guide you through those difficult things that aren't obvious on a decision to decision basis, but, you know, strategically get you in somewhere important, you know, and, and like, like design debt or, um, our technical debt where it's like, this should be optimized, you know, this chunk of code, like, nah, but you know, in, in it grouping together with a hundred of those decisions.

Yeah. It's gonna, it's gonna slow it down every single project from here on out. So that's why you need those principles.

[00:38:24] **Jeremy:** So in the book, uh, there are a few examples of software in healthcare. And when you think about principles, you would think. Generally everybody on the team would be on board that we want to give whatever patient that's involved. We want to give them good care. We want them to be healthy. We don't want them to be harmed.

And given that I I'm wondering because you, you interviewed multiple people in the book, you have a few different case studies. Um, why do you think that medical software in particular seems to be, so it seems to have such poor UX or has so many issues.

[00:39:08] **Jonathan:** Yeah, that's a, complicated topic. I would summarize it with a few, maybe three different reasons. Um, one which I think is, uh, maybe a driving factor of, of some of the other ones. Is that the way that the medical, uh, industry works is the person who purchases the software. It's not the end user. So it's not like you have doctors and nurses voting on, on which software to use.

Um, and so oftentimes it's, it's more of like a sales deal and then just gets pushed out and they, and they also have to commit to these things like, um, the software is very expensive and, uh, initially with, you know, like in the early days was very much like it needs to be installed, maintain, there has to be training.

So there was a lot to money to be made, in those, in that software. And, and so the investment from the hospital was a lot, so they can't just be like, oh, can it be to actually, don't like this one, we're going to switch to the next one. So, because like, once it's sold, it's really easy to just like, keep that customer.

There's very little incentive to like really improve it unless you're selling them a new feature. So there's a lot of feature add ons. Because they can charge more for those, but improving the experience and all that kind of stuff. There is less of that. I think also there's just generally a lot less like, uh, understanding of design, in that field.

And there's a lot more because there's sort of like traditions of things. they end up putting a lot of the pressure and the, that responsibility on the end individuals. So, you know, you've heard recently of that nurse who made a medication error and she's going to jail for that. And sh you know, And oftentimes we blame that end, that end person.

So the, the nurse gets all the blame or the doctor gets all the blame. Well, what about the software, you know, who like made that confusing or, you know, what about the medication that looks exactly like this other medication? Or what about the pump tool that you have to, you know, type everything in very specifically, and the nurses are very busy.

They're doing a lot of work. There's a 12 hour shifts. They're dealing with lots of different patients, a lot of changing things for them to have to worry about having to type something a specific way. And yet when those problems happen, what do they do? They don't go in like redesign the devices. Are they more training, more training, more training, more training, and people only can absorb so much training.

and so I think that's part of the problem is that like, there's no desire to change. They blame the end, the wrong person, and. Uh, lastly, I think that, um, it is starting to change. I think we're starting to see like the ability for, because of the fact that the government is pushing healthcare records to be more interoperable, meaning like I can take my health records anywhere, that a lot of the power comes in where the data is.

And so, um, I'm hoping that, uh, you know, as the government and people and, um, and initiatives push these big companies, like epic to be more open, that things will improve. One is because they'll have to keep up with their competitors and that more competitors will be out there to improve things. Because I, I think that there's, there's the know-how out there, but like, because the there's no incentive to change and, and, and there's no like turnover and systems and there's the blaming of the end user.

We're not going to see a change anytime soon.

[00:42:35] **Jeremy:** that's a, that's a good point in terms of like, it, it seems like even though you have all these people who may have good ideas may want to do a startup, uh, if you've got all these hospitals that already locked into this very expensive system, then yeah. Where's, where's the room to kind of get in there in and have that change.

[00:42:54] **Jonathan:** yeah. 

[00:42:56] **Jeremy:** Uh, another thing that you talk about in the book is about how, when you're in a crisis situation, the way that a user interacts with something is, is very different. And I wonder if you have any specific examples for software when, when that can happen.

[00:43:15] **Jonathan:** yeah. Designing for crisis is a very important part of every software because, it might be hard for you to imagine being in that situation, but, it, it definitely will still happen so. one example that comes to mind is, uh, you know, let's say you're working on a cloud, um, software, like, uh, AWS or Google cloud.

Right. there's definitely use cases and user journeys in your product where somebody would be very panicked. Right. Um, and if you've ever been on an on-call with, with something and it goes south, and it's a big deal, you don't think. Right. Right. Like when we're in crisis, our brains go into a totally different mode of like that fight or flight mode.

And we don't think the way we do, it's really hard to read and comprehend very hard. and we might not make this, the right decisions and things like that. So, you know, thinking about that, like maybe your, your let's say, like, going back to that, the cloud software, like let's say you're, you're, you're working on that, like.

Are you relying on the user reading a bunch of texts about this button, or is it very clear from the way you've crafted that exact button copy and how big it is? And, and it's where it is relation to a bunch of other content? Like what exactly it does. It's going to shut down the instance where it's gonna, you know, it's, it's gonna, do it at a delay or whatever, like be able to all those little decisions, like are really impactful.

And when you, when you run them through the, um, the, the furnace of, of, of, uh, um, a user journey that's relying on, on a really urgent situation, you'll obviously help that. And you'll, you'll start to see problems in your UI that you hadn't noticed before, or, or different problems in the way you're implementing things that you didn't notice before, because you're seeing it from a different way.

And that's one of the great things about, um, the, the systems and the book that we talk about around, like, thinking about how things could go wrong, or, you know, thinking about, you know, designing for crisis. Is it makes you think of some new use cases, which makes you think of some new ways to improve your product.

You know, that improvement you make to make it so obvious that someone could do it in a crisis would help everyone, even when they're not in a crisis. Um, so that, that's why it's important to, to focus on those things. 

[00:45:30] **Jeremy:** And for someone who is working on these products, it's kind of hard to trigger that feeling of crisis. If there isn't actually a crisis happening. So I wonder if you can talk a little bit about how you, you try to design for that when it's not really happening to you. You're just trying to imagine what it would feel like.

[00:45:53] **Jonathan:** yeah. Um, you're never really going to be able to do that. Like, so some of it has to be simulated, One of the ways that we are able to sort of simulate what we call cognitive load. Which is one of the things that happen during a crisis. But what also happened when someone's very distracted, they might be using your product while they're multitasking.

We have a bunch of kids, a toddler constantly pulling on their arm and they're trying to get something done in your app. So, one of the ways that has been shown to help, uh, test that is, um, like the foot tapping method. So when you're doing user research, you have the user doing something else, like tapping or like, You know, uh, make it sound like they have a second task that they're doing on the side.

It's manageable, like tapping their feet and their, their hands or something. And then they also have to do your task. Um, so like you can like build up what those tabs with those extra things are that they have to do while they're also working on, uh, finishing the task you've given them. and, and that's one way to sort of simulate cognitive load.

some of the other things is, is really just, um, you know, listening to users, stories and, and find out, okay, this user was in crisis. Okay, great. Let's talk to them and interview them about that. Uh, if it was fairly recently within like the past six months or something like that. but, but sometimes you don't like, you just have to run through it and do your best.

Um, and you know, those black Swan events or those, even if you're able to simulate it yourself, like put your, put your, put yourself into that exact position and be in panic, which, you know, you're not able to, but if you were that still would only be your experience and you wouldn't know all the different ways that people could experience this.

So, and there's going to be some point in time where you're gonna need to extrapolate a little bit and, you know, extrapolate from what you know, to be true, but also from user testing and things like that. And, um, and then wait for a real data 

[00:47:48] **Jeremy:** You have a chapter in the book on design that angers and there were, there were a lot of examples in there, on, on things that are just annoying or, you know, make you upset while you're using software. I wonder for like our audience, if you could share just like a few of your, your favorites or your ones that really stand out.

[00:48:08] **Jonathan:** My favorite one is Clippy because, um, you know, I remember growing up, uh, you know, writing software, writing, writing documents, and Clippy popping up. And, I was reading an article about it and obviously just like everybody else, I hated it. You know, as a little character, it was fun, but like when you're actually trying to get some work done, it was very annoying.

And then I remember, uh, a while later reading this article about how much work the teams put into clubby. Like, I mean, if you think about it now, It had a lot of like, um, so the AI that we're playing with just now, um, around like natural language processing, understanding, like what, what type of thing you're writing and coming up with contextualized responses, like it was pretty advanced for the, uh, very advanced for the time, you know, uh, adding animation triggers to that and all, all that.

Um, and they had done a lot of user research. I was like, what you did research in, like you had that reaction. And I love that example because, oh, and also by the way, I love how they, uh, took Clippy out and S and highlighted that as like one of the features of the next version of the office, uh, software.

but I love that example again, because I see myself in that and, you know, you ha you have a team doing something technologically amazing doing user research, uh, and putting out a very great product, but he totally missing. And a lot of products do that. A lot of teams do that. And why is that? It's because they're, um, they're not thinking about, uh, they're putting their, they're putting the business needs or the team's needs first and they're putting the user's needs second.

And whenever we do that, whenever we put ourselves first, we become a jerk, right? Like if you're in a relationship and you're always putting yourself first, that relationship is not going to last long or it's not going to go very well. And yet we Do that with our relationship with users where we're constantly just like, Hey, well, what is the business?

The business wants users to not cancel here so let's make it very difficult for people to cancel. And that's a great way to lose customers. That's a great way to create, this dissonance with your, with your users. And, um, and so if you, if you're, focused on like, this is what the we need to accomplish with the users, and then you work backwards from.

You're you're, you're, you're, you're lower your chances of missing it, of getting it wrong of angering your users. and const always think about like, you sometimes have to be very real with yourselves and your team. And I think that's really hard for a lot of teams because we have we don't want to look bad.

We don't want to, but what I found is those are the people who actually, um, get promoted. Like, you know, if you look at the managers and directors and stuff, those are the people who can be brutally honest. Right. Um, who can say, like, I don't think this is ready. I don't, I don't think this is good. And so you actually, I, I, you know, I've done that in the front of like our CEO and things like that.

And I've always had really good responses from them to say, like, we really appreciate that you, you know, uh, you can call that out and you can just call it like, it is like, Hey, this is what we see this user. Maybe we shouldn't do this at all. Maybe. Um, and that can, uh, you know, at Google that's one of the criteria that we have in our software engineers and the designers of being able to spot things that are, you know, things that we shouldn't should stop doing.

Um, and so I think that's really important for the development of, of a senior engineer, uh, to be able to, to know that that's something like, Hey, this project, I would want it to work, but in its current form is not good. And being able to call that out is very important.

[00:51:55] **Jeremy:** Do you have any specific examples where there was something that was like very obvious to you? To the rest of the team or to a lot of other people that wasn't.

[00:52:06] **Jonathan:** um, yeah, so here's an example I finally got, I was early on in my career and I finally got to lead in our whole project. So we are redesigning our business micro-site um, and I got to, I got, uh, assigned two engineers and another designer and I got to lead the whole. I was, I was like, this is my chance.

Right? So, and we had a very short timeline as well, and I put together all these designs. And, um, one of the things that we aligned on at the time was like as really cool, uh, so I put together this really cool design for the contact form, where you have like, essentially, I kind of like ad-lib, it looks like a letter.

and you know, by the way, give me a little bit of, of, uh, of, of leeway here. Cause this was like 10 years ago, but, uh, it was like a letter and you would say like, you're addressing it to our company. And so it had all the things we wanted to get out of you around like your company size, your team, like, and so our sales team would then reach out to this customer.

I designed it and I had shown it to the team and everybody loved it. Like my manager signed off on it. Like all the engineers signed off on it, even though we had a short timeline, they're like, yeah, well we don't care. That's so cool. We're going to build it. But as I put it through that test of like, does this make sense for the, what the user wants answers just kept saying no to me.

So I had to go and back in and pitch everybody and argue with them around not doing the cool idea that I wanted to do. And, um, eventually they came around and that form performed once we launched it performed really well. And I think about like, what if users had to go through this really wonky thing?

Like this is the whole point of the website is to get this contact form. It should be as easy and as straightforward as possible. So I'm really glad we did that. And I can think of many, many more of those situations where, you know, um, we had to be brutally honest with ourselves with like this isn't where it needs to be, or this isn't what we should be doing.

And we can avoid a lot of harm that way too, where it's like, you know, I don't, I don't think this is what we should be building. Right.

[00:54:17] **Jeremy:** So in the case of this form, was it more like you, you had a bunch of drop-downs or S you know, selections where you would say like, okay, these are the types of information that I want to get from the person filling out the form as a company. but you weren't looking so much at, as the person filling out the form, this is going to be really annoying.

Was 

that kind 

[00:54:38] **Jonathan:** exactly, exactly. Like, so their experience would have been like, they come up, they come at the end of this page or on like contact us and it's like a letter to our company. And like, we're essentially putting words in their mouth because they're, they're filling out the, letter. Um, and then, yeah, it's like, you know, you have to like read and then understand like what, what that part of this, the, the page was asking you and, you know, versus like a form where you're, you know, it's very easy.

Well-known bam. You're, you're you're on this page. So you're interested in, so like, get it, get them in there. So we were able to, to decide against that and that, you know, we, we also had to, um, say no to a few other things, but like we said yes, to some things that were great, like responsive design, um, making sure that our website worked at every single use case, which is not like a hard requirement at the time, but was really important to us and ended up helping us a lot because we had a lot of, you know, business people who are on their phone, on the go, who wanted to, to check in and fill out the form and do a bunch of other stuff and learn about us.

So that, that, that sales, uh, micro-site did really well because I think we made the right decisions and all those kinds of areas. And like those, those general, those principles helped us say no to the right things, even though it was a really cool thing, it probably would have looked really great in my portfolio for a while, but it just wasn't the right thing to do for the, the, the goal that we had.

[00:56:00] **Jeremy:** So did it end up being more like just a text box? You know, a contact us fill in. Yeah.

[00:56:06] **Jonathan:** You know, with usability, you know, if someone's familiar with something and it's, it's tired, everybody does it, but that means everybody knows how to use it. So usability constantly has that problem of innovation being less usable. Um, and so sometimes it's worth the trade-off because you want to attract people because of the innovation and they'll bill get over that hump with you because the innovation is interesting.

So sometimes it's worth it and sometimes it's not, and you really have to, I'd say most times it's not. Um, and So you have to find like, what is, when is it time to innovate and when is it time to do the what's tried and true. Um, and on a business microsite, I think it's time to do tried and true. 

[00:56:51] **Jeremy:** So in your research for the book and all the jobs you've worked previously, are there certain. Mistakes or just UX things that you've noticed that you think that our audience should know about?

[00:57:08] **Jonathan:** I think dark patterns are one of the most common, you know, tragic design mistakes that we see, because again, you're putting the company first and the user second. And you know, if you go to a trash, sorry, if you go to a dark patterns.org, you can see a great list. Um, there's a few other sites that have a nice list of them and actually Vox media did a nice video about, uh, dark patterns as well.

So it's gaining a lot of traction, but you know, things like if you try to cancel your search, like Comcast service or your Amazon service, it's very hard. Like I think I wrote this in the book, but. Literally re researched what's the fastest way to delete it to, to, you know, uh, remove your Comcast account.

I prepared everything. I did it through chat because that was the fastest way for first, not to mention finding chat by the way was very, very hard for me. Um, so I took me, even though I was like, okay, I have to find I'm going to do it through chat. I'm gonna do all this. It took me a while to find like chat, which I couldn't find it.

So once I finally found it from that point to deleting from having them finally delete my account was about an hour. And I knew what to do going in just to say all the things to just have them not bother me. So th that's on purpose they've purposely. Cause it's easier to just say like fine, I'll take the discount thing.

You're throwing in my face at the last second. And it's almost become a joke now that like, you know, you have to cancel your Comcast every year, so you can keep the costs down. Um, you know, and Amazon too, like trying to find that, you know, delete my account is like so buried. You know, they do that on purpose and a lot of companies will do things like, you know, make it very easy to sign up for a free trial and, and hide the fact that they're going to charge you for a year high.

The fact that they're automatically going to bill you not remind you when it's about to expire so that they can like surprise, get you in to forget about this billing subscription or like, you know, if you've ever gotten Adobe software, um, they are really bad at that. They, they trick you into like getting this like monthly sufficient, but actually you've committed to a year.

And if you want to cancel early, we'll charge you like 80% of the year. And, uh, and there's a really hard to contact anybody about it. So, um, it happens quite often. If the more you read into those, um, different things, uh, different patterns, you'll start to see them everywhere. And users are really catching onto a lot of those things and are responding.

To those in a very negative way. And like, um, we recently, uh, looked at a case study where, you know, this free trial, um, this company had a free trial and they had like the standard free trial, um, uh, kind of design. And then their test was really just focusing on like, Hey, we're not going to scam you. If I had to summarize that the entire direction of the second one, it was like, you know, cancel any time.

Here's exactly how much you'll be charged. And on the, it'll be on this date, uh, at five days before that we'll remind you to cancel and all this stuff, um, that ended up performing about 30% better than the other one. And the reason is that people are now burned by that trick so much so that every time they see a free trial, they're like, forget it.

I don't, I don't want to deal with all this trickery. Like, oh, I didn't even care about to try the product versus like. We were not going to trick you. We really want you to actually try the product and, you know, we'll make sure that if you're not wanting to move forward with this, that you have plenty of time and plenty of chances to lead and that people respond to that now.

So that's what we talked about earlier in the show of doing the exact opposite. This is another example of that. 

[01:00:51] **Jeremy:** Yeah, because I think a lot of people are familiar with, like you said, trying to cancel Comcast or trying to cancel their, their New York times subscription. And they, you know, everybody is just like, they get so mad at the process, but I think they also may be assume that it's a positive for the company, but what you're saying is that maybe, maybe that's actually not in the company's best interest.

[01:01:15] **Jonathan:** Yeah. Oftentimes what we find with these like dark patterns or these unethical decisions is that th they are successful because, um, when you look at the most impactful, like immediate metric, you can look at, it looks like it worked right. Like, um, you know, let's say for that, those free trials, it's like, okay, we implemented like all this trickery and our subscriptions went up.

But if you look at like the end, uh, result, um, which is like farther on in the process, it's always a lot harder to track that impact. But we all know, like when we look at each other, like when we, uh, we, we, we talk to each other about these different, um, examples. Like we know it to be true, that we all hate that.

And we all hate those companies and we don't want to engage with them. And we don't, sometimes we don't use the products at all. So, um, yeah, it, it, it's, it's one of those things where it actually has like that, very real impact, but harder to track. Um, and so oftentimes that's how these, these patterns become very pervasive is the oh, and page views went up, uh, this was, this was a really, you know, this is high engagement, but it was page views because people were refreshing the page trying to figure out where the heck to go. Right. So um, oftentimes they they're less effective, but they're easier to track

[01:02:32] **Jeremy:** So I think that's, that's a good place to, to wrap things up, but, um, if people want to check out the book or learn more about what you're working on your podcast, where should they head?

[01:02:44] **Jonathan:** Um, yeah, just, uh, check out tragic design.com and our podcast. You can find on any of your podcasting software, just search design review podcast. 

[01:02:55] **Jeremy:** Jonathan, thank you so much for joining me on software engineering radio.

[01:02:59] **Jonathan:** alright, thanks Jeremy. Thanks everyone. And, um, hope you had a good time. I did.

</div>