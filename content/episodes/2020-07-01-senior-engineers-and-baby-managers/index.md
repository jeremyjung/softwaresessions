+++
title = "Senior engineers and baby managers with Lauren Tan"

description = "Lauren shares her thoughts on the roles of senior engineers, technical leads, and managers."

[extra]
episode_url = "https://media.transistor.fm/b303bd57.mp3"
social_title = "Senior engineers and baby managers with Lauren Tan"
embed_player = "yes"
+++

Lauren is a Software Engineer on the React Organization's Web Core team at Facebook and was previously an Engineering Manager at Netflix.

We discuss:
- Getting started in software development
- Being empowered to say "no" as a senior engineer
- The vagueness of a technical lead role
- Why becoming a manager is not a promotion
- Leaving management to become an engineer again
- Avoiding clever abstractions in code

If you enjoy this discussion with Lauren, be sure to check out her [episode on the Changelog](https://changelog.com/podcast/386).

Music by Crystal Cola: [12:30 AM](https://crystalcola.bandcamp.com/track/12-30-am) / [Orion](https://crystalcola.bandcamp.com/track/orion)

### Related Links
- [@sugarpirate_](https://www.twitter.com/sugarpirate_)
- [Personal Site](https://www.no.lol)
- [The Engineer / Manager Pendulum](https://charity.wtf/2017/05/11/the-engineer-manager-pendulum/)
- [Should I Become a Tech Lead?](https://www.no.lol/2019-03-09-should-i-become-a-tech-lead/)
- [Does it Spark Joy?](https://www.no.lol/2020-01-17-does-it-spark-joy/)
- [Changelog Episode - Engineer to Manager and Back Again](https://changelog.com/podcast/386)
- [Dan Abramov's Redux twitter post](https://twitter.com/dan_abramov/status/1191495127358935040)

---

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

<!-- Intro -->

**Jeremy:** [00:00:00] Hey, this is Jeremy. Usually when software developers are talking career progression, it moves in the direction from being a software engineer to becoming an engineering manager. And today I'm talking to Lauren Tan who moved in the opposite direction. She was an engineering manager at Netflix, and she recently made the decision to become a software engineer at Facebook. 

We discuss why she made that decision and the differences between being a software engineer, a technical lead and an engineering manager. We also discuss what it means to be a senior software engineer and the ways that you can increase your impact and your influence in a software engineering role. I really enjoyed the conversation with Lauren and I hope you do as well.

Hey Lauren, thanks for joining me today.

**Lauren:** [00:00:42] Hi Jeremy. It's such a pleasure to be here. Thanks for having me.

<!-- Origins -->

**Jeremy:** [00:00:45] If we look back at 2015, you're moving from Australia to Boston, you're starting your first senior developer role at the dockyard consultancy. How did you get into this position where you decided that i'm going to leave this country I live in and I'm going to start this senior developer role in Boston?

**Lauren:** [00:01:03] A long time ago. I never really planned to leave Australia, let alone come to America. And I kind of traced his back to essentially how I got my career started in technology where really what started as a hobby creating silly applications then. 

In fact, one of my earliest introductions to programming was through excel and making elaborate spreadsheets and writing Visual Basic or VBA. It was something that I never really planned to do. The long story short is after college, I started a startup called The Price Geek with one of my classmates.

And at the time I was getting really interested in essentially exploring more of this hobby that I had of programming and potentially exploring the idea of turning that into a career. So the year or two that I worked on that startup was really fun. We learned a lot about product development, about the business side of things, how to manage your money and how to get funding and financing.

That was all really interesting. And near the end of the startup when we were basically throwing in the towel I realized that I enjoyed it so much and despite the fact that my degree was in finance and not computer science, I enjoyed it so much that I thought to myself, wow, it would be amazing if I could keep programming as a career.

So I was very fortunate to get a first job in Australia as a software engineer. And I had started writing a bunch of blog posts and started sharing them on Twitter and on medium. And slowly but surely, I got people reading it. And there was a point where one of the creators of that JavaScript framework that I was writing about got in touch with me to say: Hey, would you be interested in coming to speak at one of our conferences? And of course, I was totally taken aback because first of all, I had never even been to a tech conference at that point, let alone speak at one. So I had totally no idea what I was doing. But I was convinced by them to apply. So I did and I'm very grateful that they did that. 

And doing all of this essentially, I started to get the attention of some of the people working in America. The CEO of that consultancy DockYard reached out to me and asked if I would be interested in working there. And at the time they were pretty well known in the field of building Ember applications, Ruby on Rails applications. And so I thought it would be pretty interesting to go and work there and learn from some of the people that I really looked up to in that community. And that was the start of my career in Boston. And really it was a difficult decision to move. I think moving anywhere it's difficult but the move from Melbourne to Boston was exceptionally hard because it's a totally different country. It's so far away. My family and my friends would be not even in the same time zone anymore in opposite ends of the world really. So that was particularly difficult. And of course the Boston weather, it's terrible. And part of the reason why I was like, I need to maybe live somewhere else is because of the terrible Boston winter that I experienced in 2015.

**Jeremy:** [00:04:33] That makes a lot of sense how you ended up in California.

**Lauren:** [00:04:36] Right. I was like-- I need to go somewhere warm.

**Jeremy:** [00:04:40] One of the other guests I'm going to have on, Swyx-- he often talks about learning in public, which you were doing with your blog posts which got you noticed. 

So I think that's good advice for software developers in general that putting yourself out there and sharing knowledge can really make these opportunities come to you.

**Lauren:** [00:05:01] I think it can, but I also want to say that I think that developers that learned their craft during the time that I started I think we were very fortunate in the sense that the web was a bit of a simpler place back then. People would build applications just literally using HTML, CSS, and vanilla JavaScript back then. You might just consider using jQuery or Backbone, or MooTools even.

A single page application really wasn't the norm. I think today is a very different world because software development-- I don't know if it's gotten more complex, but I think at least in the world of front end development it's gotten much more difficult to just get started.

Not saying that you can't build an app with just HTML, CSS, and vanilla JavaScript. But if you want to get a job doing it, then there is a bit of a higher bar I think. So I will say learning in public can be very helpful. But I also don't want to lie and disguise the fact that the environment has changed.

Times have changed and things are getting slightly more complicated and complex to build and that just means that there's a bit of a higher hill to climb.

**Jeremy:** [00:06:18] If you are going to make a site, you have so many options you have React, Vue, Ember, Svelte. There's all these different frameworks and do I use Javascript? Do I use TypeScript?  It's definitely a lot more-- I don't know how you'd describe it. Intimidating, I guess.

**Lauren:** [00:06:39] It shows the evolution of how front end development has improved in a way. It's like, it's a mindset shift I think in the industry where previously, like 10 years ago it was still okay to just build what people might call enriched documents. Really documents sprinkled with some interactivity. But these days you're often building interactive applications that warrant a framework like react or angular or svelte or Vue. So I think maybe the problems that we're trying to solve have also changed that warrant more complex solutions.

Because I don't think the answer is to say like: Oh, we just need to get rid of all the complexity. The complexity exists for a reason. I think if I had advice for someone who was coming up in the industry, I would say, don't get intimidated by all these different technologies. And honestly, it probably doesn't really matter in the grand scheme of things which one you pick as long as you pick one and then you don't shut yourself off to learning from the others as well.

Because frameworks will come and go, but the knowledge that you acquire from using these frameworks will hopefully stay with you for a long time. And so those are much more transferable than knowing every single detail about the React API or something like that.

**Jeremy:** [00:07:56] Yeah, I think that's good advice. And I also wonder, when you started-- you had experience building applications in things like Rails. There are a number of frameworks where you can build a front end using primarily server side code, not necessarily build a single page application. People starting out, is that still something they should look at or do you think they should jump straight to single page applications?

**Lauren:** [00:08:24] I feel like it depends on your goal and hopefully if you're learning to program, hopefully you also have a project or some kind of motivation for learning those technologies. You should hopefully use the right tool for the job. And if you're building something that really doesn't require a lot of interactivity, then maybe a single page application is overkill, even though it might be beneficial for you to learn.

So I think it depends on your goal. If your goal is purely just for educational purposes, then by all means, choose the fanciest technology stack and learn away. But if you're actually trying to get a project going off the ground, I feel like it's probably not that useful to bike shed on like, do we use Svelte or do we write our own thing, or do we just use server side rendered templates?

I think those are all fun as technologists to debate and think about. But they're just in my opinion obstacles for actually trying to do what you're trying to set out to do. So that's a bit of a roundabout way of saying that I think it depends on your goals. Is it to learn or is it to build something that you know you can get out the door really quickly. And depending on what goal you have, I think my suggestion would be slightly different.

I think fortunately, if your goal is mainly just to learn, then any one of those single page application frameworks are great to pick up. My only suggestion would be, again, like not to tie yourself too closely to just one framework, even though one may seem like the incumbent. The one that every company is hiring for and that's fine.

Maybe you start there, but don't let that limit you from learning everything else. Because again, like there are a lot of concepts from the different frameworks that often make their way into other frameworks as well.

**Jeremy:** [00:10:17] That kind of reminds me of how when you first started, you were very focused on Ember. And now you're deeply involved in React you don't have to feel like you're tied to just the one you start with.

**Lauren:** [00:10:29] Absolutely. And I think in the tech community there are a lot of these people who say: Oh, you know, don't bother learning a framework. Just learn the fundamentals. In spirit, I agree with that principle. I think that you should learn the fundamentals. But I also agree that actually learning a framework first is not a bad thing. In fact, it helps you.

Sometimes you don't need to peel away all the layers of abstraction straight away because that can be very overwhelming. And I think single page applications, there are a lot of tutorials online that you can follow and you can get something working. And that is your basis for starting to then peek under the hood to say: Oh, how actually does that work?

Why did I use a component here instead of make a component that does this other thing. I think of it more like the onion of knowledge really. I don't know what a good analogy is but like an onion in the sense that there are layers that you peel away and you slowly understand what the frameworks and the languages are doing.

And in fact, I see even today, like my career and the stuff that I'm doing is continually peeling the layers. Maybe today I may not be working on writing an application anymore. I might be working on the infrastructure that powers the tools that allow this application to be made.

But I wouldn't have been able to have gotten here if I had not been building applications before. So you go deeper and deeper. But you can't go deeper without a strong foundation. So my advice is start with what's comfortable. Start with something that's easy to learn and use that as a foundation for going deeper into the technologies and the areas of programming that you're interested in.

Because maybe you'll find that front end development is not for you and maybe you'll realize that actually I prefer back end development. And that's perfectly fine. There's no one path in this industry which is pretty cool. So I would say keep it broad, learn as much as you can, and then follow what interests you and what excites you.

**Jeremy:** [00:12:35] A lot of people when they're learning, it's hard to stay motivated unless you're building something that you can see. I think in that respect if using a framework like React or Phoenix or Rails-- if it's going to get you to the point of being able to see something working that will keep you motivated, keep you moving, then it makes a lot of sense to start there.

**Lauren:** [00:12:57] Yeah. I totally agree. There are a lot of great concepts in these frameworks that will apply in other areas as well. Again, whether you use this framework or that framework or no framework, there are still a lot of programming patterns that you can learn. Which is why if I were to start learning how to code again, I would still start from the same place. I would still pick a framework and go with that and then figure out how it works.

**Jeremy:** [00:13:22] I want to take us back to your time at DockYard. I believe your title was senior developer. What do you think made you a senior developer or did you feel like one at the time?

**Lauren:** [00:13:34] I think that's a great question. I think my general  viewpoint on this is that I don't think we have agreed upon standards for what we deem senior, and I don't want to be the gatekeeper of what determines someone as a senior engineer. But I certainly didn't feel like a senior developer, at least in my definition of what I thought a senior developer should be at the time.

And at the time, I think I had a fairly naive impression of what a senior developer was and my thought was all about the senior developer is essentially the person who is the best programmer. Who knows every single API by heart. Is a genius at all the internals of every library that they use. And they're just technical, technical, technical chops.

But interestingly, the more I worked there and the more I interacted with others, people who had the same title. The more I realized that my viewpoint of what makes somebody a senior developer or engineer was totally off. And today I feel like the technical chops are just a small part of the skillset and the tool set of a senior engineer.

And if that's the only thing that you're bringing to the table, then-- it's not necessarily a bad thing, but I think you're doing yourself a disservice by not flexing those other muscles. Which is a huge lesson I learned when I took on the role of a manager. But yeah, I definitely didn't feel like I was a senior developer back then.

Maybe today I feel more like a senior developer but I think everyone has this different definition. But at least in my definition, I think I feel pretty confident in saying that. Yes, I am actually a senior developer.

**Jeremy:** [00:15:22] So what would you say were the key differences then? Because you were saying that it's beyond just the technical aspect, but what are those pieces that make you feel comfortable saying that you're senior now?

**Lauren:** [00:15:36] First of all, it was the mindset shift for myself that I can't pinpoint a specific point in time where it happened. But I certainly recognize it today where I essentially no longer feel the need to rush into writing code. Whereas in the past the moment you get a project, you're like-- all right, I need to write this proof of concept. You just focus on writing code and that's all like for you, your impact is all about the raw output of your keyboard essentially. 

And that was the wrong mindset to have because what I learned over the years in working on different projects and in different companies is that oftentimes the most impactful things were not actually the result of code.

It could be a conversation that you have with your customer or your client to find out the assumption that you had made was incorrect. And if there's something you can ask in a question and you can get an answer to in 30 minutes or you could spend days and weeks building something and then you bring it back and showing it to them and then they tell you why this is not what I wanted.

I learned that lesson very painfully because I was one of those people who would just rush into writing code. My viewpoint was if I don't have to talk to anyone then I'm succeeding. But that was totally incorrect and it was a tough lesson to go through, but I think a lesson that I sorely needed. It's definitely affected the way I operate today.

I think today I don't shy away from talking to people. In fact, I will go out of my way sometimes to have conversations with people even when it's going to disrupt the time that I enjoy of writing code because I know how impactful conversations like that can be especially when you're trying to do things that are maybe not very certain or get more context or even prioritize things. 

I think another aspect of being a senior developer is knowing when to say yes to things and when to say no to things. I don't think there's a decision tree for when to say no or yes. I think it's very much based on intuition and your understanding of the context and the problems you're trying to solve. And also organizational challenges that may happen, but prioritization is something I feel like we don't often talk about. Because again, if your mindset is all about my impact is based on the pure output of my coding, then you're not going to be in a position where you can say, hold on-- before I go and just jump straight into writing some code, let me actually speak with my manager and challenge the idea of like, wait, hold on. Is this actually the best way to do it? Do we even need to write any code to solve this problem? Maybe it's an organizational problem. If I were to distill it down I think it's the realization that my output is not just code anymore.

And I think that for me was the point where I could say to myself: I am a senior engineer. Even though maybe I'll join a company and not immediately be an expert in all of the proprietary tools that they have, which is expected. How can you, how can anyone be an expert when you haven't used those technologies. And there's certainly no expectation I think that any company you join you will be immediately the foremost expert on something that they do within the company. So the thing that you bring from position to position or project to project is really those core skills of your understanding of fundamental programming, things that are transferable, but also the organizational chops that are also equally if not more important than those foundational skills.
 
**Jeremy:** [00:19:34] Earlier in your career like at DockYard did you feel like you had the authority to ask those questions like to challenge your manager, go directly to the customer. Was there anything that was stopping you from doing that then?

**Lauren:** [00:19:34] I think there were a number of challenges for sure. The agency relationship with customers makes it a little bit difficult because as an agency or a software consulting company you are not always in a position to question or challenge the client because at the end of the day, the client's paying you to build something very specific and sure, maybe you can point out the flaws in their plan or deficiencies but ultimately the contract that you signed states that you have to deliver a certain product by the end of a certain timeline. 

That was probably the systemic challenge there, but I think I also didn't feel empowered to do that anyway, even if that wasn't the case. I think there were a number of challenges, but certainly I was, maybe not having the right examples either too. Like for example, maybe if some of the more senior people in the company were doing that and setting a good example, then I think others would have followed as well. But I don't really feel like we were necessarily in a position to do so.

So I think that made it more complex. And I think once I started joining a companies like Netflix or Facebook where I currently work. I think that dynamic and the expectations also changed because now I'm in a position where my job is not just to blindly output code just because someone said so, but to be a problem solver.

And so I think it's a very different relationship. And I think if you are in a software consulting role or a software agency role then a lot of what I'm saying may not necessarily apply because you're not always in a position to go and question your client or customer.

Maybe you might find a customer that is awesome enough to let you do that and  be receptive of the feedback as well. But that's not often the case, especially on projects where it's like super tight deadline, just deliver something in two to three months. So context is everything.

**Jeremy:** [00:21:42] Yeah. That's an interesting point about how when you're working at an agency, you're ultimately telling the customer: I will do this thing for you. It's written down in a contract, whereas for a more traditional company, it's really dependent on the culture of that company and maybe that's something that when you're interviewing or learning more about that company, you would want to figure out how much agency or how much control will you have as an engineer being in that company.

**Lauren:** [00:22:14] Yeah. I think that's a great point. And it's a question I will often ask when I've done interviews as an interviewee in the past is ask people, especially the engineers on the team that are interviewing me for examples of times where they were empowered to say no to certain things. And I think the way that the answer those questions will tell you a lot about the culture of the company. 

I often find as a meta point asking for examples in interview questions to your interviewers are actually always for me, very helpful in trying to reverse engineer what the culture is really like versus what it's advertised. Because sometimes, and it's not ideal, but there's often a disconnect between what is stated and what really happens. And I think there's no better way to learn that than to ask for examples.

**Jeremy:** [00:23:08] What are some questions you would ask to reverse engineer that?

**Lauren:** [00:23:14] Oh, I have so many. The things that come to mind are, like I just mentioned-- can you share an example of a time where you were empowered to say no, or, tell me about a time where you disagreed with a manager and, you were given the autonomy or freedom to go and explore that solution that you were proposing. The things along those lines where it gives the interviewer a chance to show that the culture is truly what they say they claim it is. If I think of more later I'll bring them up as well. Or I can share some thoughts in writing later as well.

**Jeremy:** [00:23:52] When you ask those kinds of questions, reading people's body language or just the way they respond you can infer a lot of information, beyond what's being said.

**Lauren:** [00:24:06] Yeah. Especially in the times where maybe that person is unable to give you an example and instead they'll talk about it more generally, which for me is a bit of a smell. It means that maybe they don't practice what they preach. And I think what you just said is very important.

I think the way that the person answers that question tells you a lot, even if you don't come out right and say like: "No, I am not empowered to say no." I think it just tells you a lot, like just how the person answers what they say, what they don't say, is also important. But I mean, I also say that with the somewhat small caveat that there may be a chance that maybe that person just hasn't had that occur to them. Maybe not that they have not been empowered to say no and they just have never had to say no. It's not necessarily a bad mark, I would say. So a lot of judgment applies to how you interpret those answers. But again, they can be so subjective. So I don't know if there's a clear cut way to say like, "Oh, this company is definitively bad or good."

And then I think to make things more challenging, depending on the size of the company you're going into a lot of the culture will really depend on the immediate team that you're on. And in fact probably the manager that you have is a bigger indicator of the culture than the general company-wide culture. 

So it really depends. But if you have the hiring manager in your interview panel and you're given time to ask questions, then I would definitely bring lots of really hard questions and really get a sense of whether this manager will be the right person to support you in your career.

And, sort of going off on a tangent here, but I think my own experience being a manager has also taught me that there are lots of different kinds of managers and it's not like one is better than the other. I think there is some kind of matching that you have to do on your own as you understand what kind of support you need.

For example. If you're still early in your career, maybe you do need a manager who is very technical, who can give you a lot of technical feedback, that can help you grow in your career, at least technically. But maybe once you get more senior in your career, maybe that kind of manager would no longer be as beneficial to your career as for someone who is earlier in their career.

And instead, maybe you might look for someone who is more of a sponsor. Someone who goes out and finds really difficult problems and says, "Hey, can you solve this?" And maybe that's what you need in your career. So I think spending the time to introspect and think about if I had the perfect manager, what would they be like?

And then go backwards from there and say what questions do I need to ask in order to determine if this manager would be that person? And obviously it's not perfect, you can never really know for sure until you start working with them. But it can at least give you more confidence if you're interviewing at lots of different places and you're trying to make a decision on where you ultimately land.

**Jeremy:** [00:27:17] Yeah. That's an interesting point about finding a manager fit. After DockYard, you moved to Netflix as a senior software engineering lead. In that role, what were you looking for in a manager?

**Lauren:** [00:27:34] So I joined Netflix, not as a lead per se. It wasn't an official title, but more so unofficial title after a period of time. I guess LinkedIn probably doesn't capture that very accurately. In terms of what I was looking for in my manager at that point when I had just joined the company, I did think I was at the point when I joined Netflix that I really wasn't necessarily looking so much for just raw technical chops.

I wasn't looking for a manager who was a better coder than me. I think the thing that I was excited about was Netflix's culture of freedom and responsibility and context, not control and all those things that they write on their culture memo. And I can actually safely say that pretty much most of it, if not all of it is true and they do apply in practice.

So I was very excited about going into a company where the culture was so different than anything I had ever experienced. And I wanted to learn what I had started to think about would define me as being at the level that I wanted to be. You know, like not someone who is only good at programming, but also someone who brings a lot of impact to the team that they work on, whether it's a contribution in the form of code or contribution in the form of an architecture document, or even a comment or some feedback that you've given someone. Because when I first joined, I didn't feel like I was in that position yet.

But about a year and a half, I don't remember exactly I did start to feel like I was getting the hang of the culture and also the technology at Netflix where I was then very comfortable when my manager came to me and said: "Hey, would you like to be the lead for the team?" to say yes.

I was like, yeah, absolutely. In fact, I already felt like I was operating like a lead. So this was more just a recognition that I was already operating at that capacity. So I think that my manager at the time was definitely very supportive and they looked out for opportunities for me.

And they were never really prescriptive about certain things like they may have had different opinions from me from time to time but they weren't afraid to say, you know what go try what you think is right. And then let's compare notes and see what turns out to be better.

And that was always very encouraging because it creates this almost psychological safety of going and trying different things that people don't necessarily immediately agree with. Like if you can prove that something is better with a prototype or a document or whatever it might be that you're given the autonomy and flexibility in the space to go and explore that and then come back and say, you know what? This was either a good idea, or a bad idea, or unconclusive. But I think that was, for me, something that I really enjoyed about that part of my career.

**Jeremy:** [00:30:36] And it sounds like your manager gave you the opportunity to explore having more influence, having more control over the types of work you were doing, and how you were doing it and at that time in your career, that's really what you were looking for.

**Lauren:** [00:30:55] Yeah. I think I don't recall when, but there has definitely been times where I've had what I would call the programmers midlife crisis. Where you start questioning what you're doing and the way that you've been doing things and the purpose and starting to look up from the keyboard and like, hold on a minute.

I can get this project done, but is this really the right thing to be doing? And I think the more senior you get, the more that urge will come to you and you start thinking more about, Hm. The moments where you say to yourself like, hold on a minute, something feels off.

And I think the turning point for a lot of people will be when you'll start turning those thoughts into action and instead of just saying, hold on a minute in your mind and then just continuing anyway, you start actually going forward and talking to people and say, hold on, here's something that doesn't sit quite well with me. Let's talk about it. 

And in fact, I think one of the things I started to recognize once I was operating in that lead capacity even though maybe I didn't have the title just yet, was that actually I was spending less time coding.

And initially it felt kind of awkward. I was like, why am I in all these meetings? Why am I feeling like my output has dropped a lot? And it was true. If the only output that you're measuring is my code, then it definitely dropped quite a lot. But in terms of the impact I was having on the team and the projects that I was on I think definitely outweighed that. It wasn't a net loss because oftentimes when you have someone who's operating in a lead capacity, it means that in a way, they're giving away those problems that are maybe more difficult to solve. And allowing others to learn about them and, not hogging all the difficult pieces to themselves which sometimes the tech leads might do instead of giving opportunities to others to grow, which is actually a responsibility for a tech lead. So I think going back to your question of what did I need from my manager at the time, I think it was definitely being put more so than a lot of other things it was being put in an environment where I could really flex those nontechnical skills and understand, and almost in a way, create the environment you know? Like if a manager is like a gardener, then creating the right conditions in the environment so that I could not just thrive, but also evolve and grow and, broaden my branches. It's a weird analogy.

**Jeremy:** [00:33:38] And, we've stepped around it but I think the the title of someone being a lead to a lot of people is a little fuzzy. Some people think a lead is the same thing as a manager. And it sounds like what you're saying is in your case, a lead was someone who is able to ask questions to figure out what should actually be built. They're able to decide who should work on these things after you've decided what needs to get built, and we haven't mentioned this, but potentially help the people who are building these things if they get stuck. Would you say those are the three primary things that a lead does?

**Lauren:** [00:34:21] Um, at a high level, I think that's pretty accurate. To be a bit more granular, I would say it also depends on the kind of tech lead that you want to be, or, or maybe another way to put this might be the tech lead that your team needs. Because the truth is, at least from my perspective, just like managers have different archetypes. I would also say that tech leads had to have different archetypes and it really just depends on the kind of project that you're working on. I would say though, as a minimum for me, at least from the technical side of things, yes. Even though I wasn't writing a lot of code anymore as a lead, I was still reviewing a lot of code.

In fact, I think I would probably say I reviewed more than I wrote code. I think that was also part of the dawning realization that-- Hey, you know what? You can contribute in forms that aren't just you writing the code and then slowly universe expanding of like, Oh, if I step back just a little bit, I start to see the forest of what impact as an engineer is. And it was the realization that I had been only just focusing on this technical tree and not growing all these other skills that are also really important. So I think tech leads are typically the people who are seen as the best engineer who gets pushed into the lead position.

But I would say that tech leads are interesting in the sense that you're not a manager, you typically don't have reports, and you don't have any authority so to speak, over anyone. So all you really have typically, I feel is the influence that you've earned throughout your career in that company.

And that kind of social capital, if you will, that people will start to listen to you because you've been around, you know your way around, and you've proven that you can handle large projects and things like that and grow other engineers. So I think for me being a tech lead in some ways can be actually more challenging in some ways than a manager because it's blurring the lines I guess. 

I think as a tech lead you're in this awkward gray zone between engineer and manager and you're not quite one. You're not quite a manager. You're obviously still an engineer, but you're in a position of greater influence and greater not really authority, but more respect typically is given to you.

And so you're in this awkward position. Where it again, it comes down to what your team needs. And maybe like for example, if I was to join a new team and I was the tech lead for that team and if it was a team of one or two people, then obviously the expectations and the way I would do my job would be very different from me joining as a tech lead on a team of 12 engineers. It's a very different set of variables that you have to learn how to tweak. 

And again, it just depends on the makeup of the team as well. So like if I joined a team of 12 very junior engineers then also my approach would be very different versus if I joined a team of 12 extremely senior engineers. It all is very fuzzy. I don't think there's one, there's no one way to do your job as a tech lead, or as an engineer, as a manager. And maybe it sounds like a bit of a cop out answer, but I do think that a lot of questions can be distilled down to the age old answer it depends. 

Obviously just saying it depends and nothing else is a bit of a cop out. But I can say that there are different circumstances and some may require as a tech lead more involvement from you at the architecture level. Maybe some less or maybe some where you, instead of worrying too much about architecture, maybe the problems are more around organizational challenges or headcount or constraints I would imagine things like that the tech lead should be doing as well. 

Like that example I shared with you of joining a team and being one of two engineers. Maybe one of the first things of my job would be to point out to leadership that-- Hey, I've just joined this project and it's clearly very ambitious, but there's only two of us and the deadline-- that the timeline that we're gonna work on is way too unrealistic.

So I actually need to campaign my manager to say, this is why we need another two engineers or one engineer on this project. And so that's why I think it's a bit tricky. Cause it really depends on the team that you're on.

**Jeremy:** [00:39:05] That's a really good point in terms of the size and the experience and the actual project that you're tackling. I think that's why people have so much trouble understanding what it is a tech lead does. Because from what you're describing, it's a completely different job from person to person.

**Lauren:** [00:39:24] Yep. Yeah. It's very context dependent because you're straddling the line between manager and engineering and individual contributor. And so you have to sometimes wear the manager hat even though you're not a manager, and sometimes you have to wear the engineer hat.

But I think knowing when to switch hats is really important. And if the expectation that maybe someone else has set for you is that you are wearing the technical hat most of the time, then that's the expectations that you work towards. But I think for most companies, especially the bigger ones, I think there is an expectation that you also wear the project management hat, the organizational hat where you go and raise problems like that as well.

**Jeremy:** [00:40:10] So we've been talking about tech leads and managers and how the role of a tech lead is so fuzzy. After your role as a lead at Netflix, you moved on to becoming a manager.

What would you say are the key differences between being a manager and a tech lead? How did your job change, how did your role change?

**Lauren:** [00:40:33] So I do want to make the distinction that even though I said earlier that as a tech lead, you're in-between a manager and an individual contributor. I do want to say there are a lot of manager specific things that tech leads don't get exposed to.

It was definitely a big jump even going from tech lead to manager, let alone like as a non tech lead engineer to manager. And I think a lot of those challenges were in the forms of essentially problems which I never really thought about. 

Like, maybe I would have said-- we need more people on this project. But I wouldn't have then gone on to say, all right, I need to spend the next three months looking for the perfect hire to join the team. Because that was the job of the manager, to really think about the people and the conditions of the overall team that they're supporting.

Whereas as a tech lead your sphere is slightly more constrained to maybe a project or two purely more in terms of the results of said project, whereas I think as a manager, the expectations become more at the organizational level and your success is really determined by the work that your team ultimately does or doesn't do.

Maybe it sounds kind of subtle when I describe it that way, but I will say that it was definitely a very different job when I went on to become a manager. The first of which is I think a very false conclusion that I may have harbored a long time ago and I think a lot of people share the same sentiment as well. Which I want to go on record and say I kind of disagree with that. And that view is essentially that becoming a manager is a promotion. In some ways, maybe it is a promotion, like maybe financially you might get paid more and you might have more opportunities to have certain kinds of impact depending on the company that you're in.

But I will say for the most part having that mindset that management is a promotion is not the right one to have because I think it disguises the fact that when you go from engineering to manager you're basically going from very senior engineer who was very good at their job to going to become a baby manager who knows nothing about their job.

So it is very different. They're like two definitely distinct tracks and all the skills that you've used. Like, 99% of them, you've used to be successful as an engineer are probably not going to translate that well to being a manager. Like you're not going to be expected to write as much code or to even do code reviews instead your role is really more to ensure that you have the right people on your team, and also the right environment where those people can thrive and do their best work and achieve the goals that have been set out for your team and even shape those goals that your team should be working on. So it was definitely a very different career change.

And I think even though I had expectations going in, that it'd be very different. It was a totally different experience doing it, if that makes sense. Like I was expecting one thing. I knew it would be different, but I didn't realize it'd be that different. And I remember as a manager, I was spending so many hours just looking through LinkedIn or reaching out to people on Twitter, and asking them like, "Hey, would you want to come work on my team?"

Because as a manager, your biggest lever for impact is getting to pick who is in the team and it may sound like a very-- it may sound simple, right? Like you're just hiring, but I would say it's actually a very very high leverage activity. If you find that person who fills out a gap in your team where maybe there's a certain skill set or a certain technology, skill or organizational skill that your team doesn't have that you want to have, and you're able to fill that position and not just do that, but keep them there as well for-- well not keep them there but, to create an environment where that person is happy staying for awhile, then you've really done a great job because now you have a strong, solid dream team that has the capabilities of doing awesome work that you need, that you want to achieve the vision that you have for your team. And then you also have to balance that with the often difficult work of what is often called talent retention, but I don't really like that term because I don't think so much about retaining people because that sounds to me like they're constantly trying to escape and then you're just trying to hold them back.

I think it's more about creating an environment where people are attracted and they want to stay not because they're handcuffed. But because they choose to stay, because you're a great manager and the team is good. That the work is impactful. If anyone listening is also going through that transition or you've just become a manager, I'll say that I think for me the biggest challenge I had to overcome in the initial couple of months of making this transition was really understanding that it was a completely different job and then changing all the things that I did for that new reality and not trying to go back to the things and the skills and activities that I had been relying on as a tech lead.

**Jeremy:** [00:46:10] You gave a few examples of what a manager does that wouldn't go to a tech lead like hiring and if your team needs more resources, making that pitch to get more money, and also creating an environment where people want to stay there. Are there any other specific examples for the types of things that would only be a manager's role versus something that a tech lead would do?

**Lauren:** [00:46:36] Yeah. So this is not going to be an exhaustive list for sure, but I can at least point out the things that are not immediately obvious, not unless someone explicitly says it. But I will say actually, depending on the company, I think one of the biggest jobs of a manager is actually the flip side of hiring, which is firing.

And that's a really tough one. You never go into a team or hire someone or work with someone on your team expecting that you'll need to one day fire them. But as a manager, that is the thing that you think about on a constant basis, not because you just like firing people just to fire people or again, I don't know, maybe at certain companies where they do things like stack ranking and there's an expectation that, yeah, I don't know. I've been fortunate not having worked in companies like that. But if you are a manager, I would say that you're often the person who does a lot of unglamorous things like that. To me at least, it seems unglamorous to me. The hard work of recruiting and hiring and speaking to candidates and selling them on your team.

And if you do write code it's most likely going to be the very boring parts of the code base. Like adding tests or writing a little script that does a certain thing. So you're not going to be working on those things that you thought were exciting or the things that may have even attracted you to software engineering in the first place.

So very different job. And, there is going to be so many other things that you may not be aware that managers have to do. Like, I don't really like how people will phrase this, but a lot of managers will say like they provide air cover or they shield their team from shit.

I think there's some truth to that in the spirit of what that means. But I think there are obviously different ways of approaching it. And personally for me, instead of thinking it like that, like I'm shielding my team from shit, I think it's more about maybe there is shit coming towards our way. But my job as a manager is to also not make that shit before it comes to my team, if that even makes sense. And so that often means talking to people in different positions, different parts of the company, people who are higher, like a VP or a director and convincing them that this path isn't the right one.

And the truth is that a lot of individual contributors won't see that. Not because they are ignorant but because if your manager is doing a good job of that, you just don't see it. And sometimes managers can be a bit flippant, I think. And to say that, Oh yeah, I shield all the shit, so you don't have to, which I think is, again, like in spirit it, it captures the outcome of what, what that is. But I think it also doesn't quite accurately portray how the manager goes about doing it cause there are many different ways that yes, maybe you can just shield and keep your team unaware of everything, but that's not necessarily a great way to run your team as well because your reports will not necessarily trust you very much if you're always being very dishonest and like not telling them the truth, because of your desire to shield them from shit.

Instead maybe the better approach is to let people know that. You know what, there are rocky things that are coming. They're things that the company that we work at doesn't do so well, and that's okay. We'll figure it out. But not to completely hide it, I think. I think that's the part which I am not a big fan of.

It's a bit of a cop out to me if the manager just keeps things from their team because of that mindset or because of that belief that by doing so, they are helping your team, when in fact, I think it's actually making the team worse off.

<!-- continue editing here -->

**Jeremy:** [00:50:25] That's an interesting perspective because ultimately, if you are shielding your team and the things that they're being shielded from are just shifting elsewhere in the organization, that's not really solving the root problem.

**Lauren:** [00:50:39] Right. Yeah, and I think it can also be very powerful for managers to point out areas which need help. And then instead of feeling like the manager has to solve all of those problems I think we-- we talk a lot about the management parts of the job, but not the leadership parts of the job.

Leadership is really more about influence and the way you conduct yourself and how others perceive your behavior versus management, which is more like-- I think a role that you play. So things like hiring and firing are obviously the role of a manager.

But getting people excited about a vision and getting people to do certain things even though you're not explicitly bending their arm to do it is a part of the job that is not often talked about or even taught-- like how do you do that? It's not something that you can just read a book and do. It's something that over time and trial and error and maybe some intuition you build that up over time.

A realization that I had over the past two and a half years when I was a manager was that leadership is not solely within the domain of the manager. It sounds silly to say this, I had to be a manager in order to realize this. But it wasn't as evident to me until I became a manager that, Hey, hold on. There's a lot of things that I'm doing as a manager that I didn't have to be a manager to do these. So when I started to think about the different parts of the job that I was doing, I started to realize that, hold on, there's the parts that I like, right? A lot of the leadership side of things I really enjoyed.

And then the other parts which I maybe didn't enjoy as much. And I realized like, Oh, hold on. Actually I don't necessarily have to be a manager to practice these skills. That was actually the realization that I needed to maybe go back to be an engineer again.

But I certainly don't regret the time I spent as a manager cause I was exposed to so many different kinds of problems that I'd never ever had to face as an engineer. Hiring, having to let people go. Dealing with the sometimes unreasonable demands of different organizations that we were working with and balancing that all.

And another thing that maybe managers don't talk about is oftentimes people will come to you with problems that you can't solve. And these are maybe personal problems, emotional problems. And if you're a very empathetic person, then I think the job of a manager gets really difficult because people come to you with lots of problems that you can't solve. And if you're an engineer, you probably want to try and solve all the problems and it can be very frustrating.

I guess I'll sum it up all by saying that being a manager is a totally different job from being an engineer, even a tech lead. It's totally different. It's not a promotion. I don't consider it a promotion. And I think if anybody chooses to do it, I think you learn a lot and hopefully you enjoy that transition as well.

But personally for me, I didn't enjoy it. That doesn't make being a manager bad. It just means that it wasn't for me.

**Jeremy:** [00:54:00] And now that you're at Facebook as a software engineer again, What's the thing that you enjoy most about being a software engineer as opposed to being a manager?

**Lauren:** [00:54:11] I think when it came down to it. It was really a reflection of why was I in the tech industry in the first place. And I think the simple way to put it is that I mentioned earlier at the start of this conversation that programming started out as a hobby for me. And it was something that I would spend all my free time just working on.

I would have these shower thoughts essentially of programming. And I realized I've been so fortunate that I was able to turn something that was purely a hobby into a full time career. And when I was reflecting at the end of 2019 about the next couple of years of my career, I did really start to think that there was a lot of programming in being an engineer that I really missed.

And also me realizing that other part, which I mentioned earlier, which is that there's a lot of things I was doing as a manager that they were not things that only managers could do. But you may have to become a manager to learn the skills, which just sounds kind of weird.

But I think it was that realization that Hey, one, I can go back to do what I love, which is programming. And two, I can also bring back all these lessons that I've learned as a manager and basically supercharge myself as an engineer and be so much more impactful. 

Not because I'm going to write all the code and solve all the problems, but because I know how to inspire. I know how to influence. I know how to communicate. I know how to get things done and get other people to help out with those problems. And I think that was for me, the realization that I could have my cake and eat it too, I guess. And I think that I'm very fortunate in that.

I think at Facebook they think very heavily about career paths as an engineer, as a manager. And I think the company does a pretty good job at stating that one is not superior to the other. In fact, there's more or less an identical leveling track for engineers and managers and also very similar in terms of compensation. 

So there's not a penalty for you if you become an engineer. It's not like you're going back. It's seen more as you are just hopping over to the other parallel track. And one of the blog posts that I want to call out here that really helped me think about my career this way is a blog post by Charity Majors called the engineer/manager pendulum.

And she does an amazing job of articulating this hidden career path of jumping between the engineering track and a management track every couple of years. And she does a way better job than I think I can to explain why it's an interesting career path to take, but it certainly inspired me to start thinking more critically about what I wanted out of my job.

And then finally mustering the courage to go and interview again because I don't actually know anyone that I can think of who actually enjoys interviewing. I don't. I think it's one of those evils that we put up with. So there is some courage you have to muster up often just to interview and go look elsewhere.

But I think her blog posts really spurred me to take action on it.

**Jeremy:** [00:57:34] The interviewing problem is-- that sounds like maybe a job for a manager?

**Lauren:** [00:57:43] Yes. I think, yes, it is part of the manager's job, but I think as engineers, we can also do a lot to at least point out the problems.

Maybe we're not the ones to fix them, but we can at least say, Hey, this interview panel that I'm on-- I've looked at the other interviewers on the panel and you can call out things that aren't quite right, that don't sit right to you.

Maybe the panel is very undiverse or maybe the interview goes on for like eight whole hours. There are things like that you can still do to influence that process and even influence the questions that get asked. I haven't been a part of an interview panel here yet, but if I understand it correctly, I think that engineers have a lot of influence over the kinds of questions that set a standard for the different interviews that we have.

And so that's one way as well, to have a lot of impact and influence over the interview process. And make sure that the questions that we're asking are relevant, realistic, but also ensures that we keep that standard of engineering quality that we want, which is always a fine balance to strike.

I could probably talk to you for another whole two hours just on the topic of interviewing, so I won't go into that right now.

**Jeremy:** [00:59:01] Yeah. It's definitely something that everybody has an opinion and everybody agrees it needs to be better, but for some reason we as an industry just haven't gotten there yet.

**Lauren:** [00:59:12] I think my short answer to this is that I don't think there is a perfect solution. Which is why we haven't as an industry adopted something that's better. It's a process that is very lossy and there's just no way to really tell in a short frame of time what a person will be like working on a job.

And there are many ways to solve it. None of which I think is better than another. So that's all I'll say about that topic. Don't get me started.

**Jeremy:** [00:59:43] Yeah, I think that anybody listening to this maybe the big takeaway would be regardless of what your role is, even if you are just a regular software engineer, look for what are the places where you can ask questions, whether that's what type of work you're doing, whether the technology you're using is right, or do you have the right people to do it?

What are ways that you can really improve your team situation without necessarily having to change titles.

**Lauren:** [01:00:16] Yeah. I think that's a great way to put it. The way I would try to summarize my learnings over the years is really that it comes down to ultimately for me, it all stems from this root. And I think the root of this is all of that. Realizing that your job is not to write code. Code is merely a side effect of your job.

I think your job is really to solve problems and there are many ways to solve problems and I think realizing that is, to me, step zero in terms of growing more senior in your career. And, the other thing I'll say to that is also as you get more senior things will get more ambiguous. And you have to learn how to deal with that uncertainty and ambiguity and accepting that sometimes there isn't an answer.

And that's okay.  I think those are the two big lessons that I've learned.

**Jeremy:** [01:01:10] That's interesting because I think as engineers, a lot of people feel like as they learn more things will get less ambiguous. But it sounds like as you progressed in your career, things are actually getting more ambiguous and that's how you know you're progressing.

**Lauren:** [01:01:24] Exactly. Yeah. I think even in the code I write. Cause like I think you can see it sometimes. I've seen this in myself as well. When you're not a junior engineer anymore but you're not really senior and you kind of know enough to be dangerous and you start dreaming up these-- I'm very guilty of this in my past of writing these weird abstractions that you think will save you a lot of time. But when you look at them in a couple of months, you realize this was totally the wrong abstraction to have picked and it's actually slowing the team down.

That is often because again, you're trying to feel your way around and explore and learn, and write better code in your mind. But I find myself these days, it's like trying to write the simplest possible code and delaying the point of abstraction as much as possible and writing a lot of comments about all right--
This could be better, but I'm not gonna make it more abstract right now because this is just a one off case and we don't actually know for sure if it's going to happen again. So that's, I think, the part of recognizing the ambiguity of things. And there are a lot of things that have subtly changed about my behavior.

I used to be all about talking about best practices and talking about, Oh, this is an anti pattern, or, so and so said, we shouldn't do it this way. Or you try to read the tea leaves of someone's tweets into Oh yeah, Dan Abramov says, don't do this. So this is now law and we cannot break this law. 

But I think a painful but necessary part of growth I think is realizing that nothing is really an absolute, *only the Sith deals in absolutes* and being comfortable with that. Like, again, I was saying like there's often maybe no best answer, but picking the right tool for the job, the right solution, it takes a lot of patience and communication together with your team.

**Jeremy:** [01:03:20] For sure. Yeah. Dan Abramov's example is actually really funny cause he is the creator of Redux, right? And he has this tweet where somebody is describing like how somebody put Redux into their application because Dan said to do it and he replies to the tweet and says *this is the reason I'm going to hell*.

**Lauren:** [01:03:41] Yup. Yeah. Dan Abramov is a really smart person and someone I really enjoy working with. I think it's all part of our growth of realizing that the things that maybe we all believed were best practices a year ago are probably now anti-patterns, which is why I just shy away from saying this is the best practice and we must do it this way. And taking a more case by case basis to things. 

And again, this all ties back to being comfortable with ambiguity, right? Because if you don't have these laws, so to speak. Then you're introducing a lot of ambiguity in your code because now maybe people have a lot of uncertainty about, Oh, do I use this in this situation or that?

And instead of you saying, Oh, you should always use this thing. You're now saying, right, let's evaluate it on a case by case basis. And that's okay. Maybe it's going to slow it down a little bit but in the long run, it actually makes us faster and more resilient to change. Especially if product requirements change and suddenly all the abstractions that you dreamed up are now totally irrelevant.

It's a very interesting industry to be in. I think software it's, it's changing all the time. The way we build software also has to reflect that. And instead of trying to build these very rigid architectures and constructs-- which maybe in certain scenarios are warranted.

Like if you're writing code that will never be updated for the next 30 years, then it probably makes sense to get it right from day one. But if it's something that's constantly being improved and evolved, then maybe you don't, you don't jump into pouring the concrete where the concrete doesn't belong just yet.

**Jeremy:** [01:05:22] Yeah, I think that's a good note to end it on. Where can people follow you?

**Lauren:** [01:05:27] The best place to follow me will be on Twitter. My handle is *sugarpirate_*. You can also follow me on LinkedIn, or add me on Facebook but Twitter is probably your best bet if you're trying to get ahold of me.

**Jeremy:** [01:05:42] Lauren, thank you so much for chatting with me today.

**Lauren:** [01:05:44] Yes. And thank you Jeremy. It was really fun talking to you. And see ya everyone!

**Jeremy:** [01:05:47] That's it for my chat with Lauren, You can get show notes and a transcript for this episode at softwaresessions.com. And if you enjoyed the show, let someone else know about it. The music in this episode is by Crystal Cola. See you next time.

</div>