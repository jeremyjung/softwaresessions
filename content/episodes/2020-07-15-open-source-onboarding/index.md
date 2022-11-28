+++
title = "Open Source Onboarding with Brian Douglas"

description = "Brian talks about unintentional gatekeeping in open source, making projects more approachable, and how new contributors should get started"

[extra]
episode_url = "https://pinecast.com/listen/d12bc9a1-2f1e-409c-a99e-c5ee0e3a74bf.mp3"
social_title = "Open Source Onboarding with Brian Douglas"
+++

Brian is a Senior Developer Advocate at GitHub and was previously a Developer Advocate at Netlify.

We discuss:
- Unintentional gatekeeping 
- Formal onboarding for your projects
- The value of discord communities for newcomers
- Streaming issue triage and programming on twitch
- How Open Sauced helps developers get involved with open source

Music by Crystal Cola: [12:30 AM](https://crystalcola.bandcamp.com/track/12-30-am) / [Orion](https://crystalcola.bandcamp.com/track/orion)

### Related Links
- [@bdougieYO](https://twitter.com/bdougieYO/)
- [Open Sauced](https://opensauced.pizza/)
- [ExpressJS Triager Guide](https://github.com/expressjs/express/blob/master/Triager-Guide.md)
- [GraphiQL](https://github.com/graphql/graphiql)
- [Babel's contributing guide](https://github.com/babel/babel/blob/master/CONTRIBUTING.md) (Gives suggestions on familiarizing yourself with codebase)
- [Webpack's funding page](https://opencollective.com/webpack)
- [SE Unlocked episode with Dan Abramov](https://www.software-engineering-unlocked.com/episode-13-bad-tests-dan-abramov/)
- [Explore GitHub](https://github.com/explore)
- [Changelog Nightly](https://changelog.com/nightly)
- [Code Triage](https://www.codetriage.com/)
- [Figma](https://www.figma.com/)
- [Discord](https://discord.com)

### Twitch Streams
- [bdougieYO](https://www.twitch.tv/bdougieYO)
- [jlengstorf](https://www.twitch.tv/jlengstorf)
- [Noopkat](https://www.twitch.tv/noopkat)
---

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy:** [00:00:00] This is Jeremy Jung and today I'm talking to Brian Douglas, he's a senior developer advocate at GitHub, the host of JAMstack radio and the creator of open sauced, an application to help new contributors to open source. 

Brian welcome to Software Sessions.  

**Brian:** [00:00:14] Hey Jeremy, thanks for having me on.

**Jeremy:** [00:00:16] The first thing I want to get into is. What's the biggest barrier for people getting into open source?

**Brian:** [00:00:23] Yeah, that's a good question. I think the barrier for open source is something I found or discovered right off the bat. I've been developing for over seven years now, seven years ish. And getting into open source can be daunting, especially if you don't know where to get started.

So I think the biggest barrier is actually onboarding and it's just knowing is a CONTRIBUTING.md, the proper place to go to or is there some other secret channel somewhere or a Slack group or something else where you could actually get a relationship with the project? I think a lot of us leverage a lot of these tools that are open source, and go years of leveraging them without even knowing who's contributing to them, who's powering it.

What community is involved in the project. So just knowing where to start is usually the hardest part. I think that we do a good job as a developer community. There are guides on how to contribute, like open a pull request, manage your commits and stuff like that.

But there's no guide of how to say hello when it comes to giving your first open source contribution.

**Jeremy:** [00:01:27] Not knowing where to start, even if there is a CONTRIBUTING.md and there's issues out there. People are like, I don't know which one to pick up. I don't know who to talk to first. It's just awkward, I guess.

**Brian:** [00:01:38] Yeah. Each project is different. So there's no centralized CONTRIBUTING.md file everybody is sourcing from so where one project can be, could say, okay, CONTRIBUTING.md, git clone, git, check out a new branch, git push origin. And then that's it. And some of them don't even have contributing MDs.

Some of them are just READMEs. Then you go to the README and there could be missing information. Some projects don't have READMEs. Some projects have READMEs and websites and documentation and Slack groups. So not knowing the balance of how to actually get involved in the project.

And I think what it really comes down to is if I started a new job the first thing I'm gonna get is a step by step okay. Here's your laptop. Here's how to do this thing. Here's how to clone the repo. Here's who to talk to. A lot of projects don't have that. Like they don't have like area owners, plugin owners, who's on the review team. Who's on the triage team. How big is the contributing group? 

You can go into the GitHub repo and discover it all. But it'd be nice if someone just gave you a piece of paper or one file to get all that information. I think we've sort of grown out of the CONTRIBUTING.md and we need something else.

**Jeremy:** [00:02:49] When you are looking at an open source project, there's all these different issues whether it's bugs or feature requests. And it can be hard to know which things are suited for your skill level. And what do you think is the solution for that for somebody trying to pick out that issue that would work for them.

**Brian:** [00:03:08] Yeah. And I mean, the easy answer is they have labels like good first issue and like documentation. If some people don't know this, if you go to any GitHub repo, so like github.com/nodeJS/node. Or node/node, I think is what it is /contribute. So if you add /contribute on the URL you can see all the issues that are available for up for grabs and you can leverage them and jump into.

I don't actually recommend doing all that first and going to labels. I think the very first step is actually talking to a person. So the quickest place that you can find communication synchronous of like, Hey, I'm looking to contribute. I've been using this thing for six months on this project. I just want to give back. I had this idea for a feature like open issue, like ask questions on the issue, or even like now we have a feature at GitHub called discussions. In addition to that go into the discussion, but also limit the amount of back and forth you have to do asynchronous. And just go directly to the source, which is the person who is on-call already to chat with you.

A lot of projects have discords now. So find the discord link and then jump in there and say hello, because your experience is going to be completely different when you're actually talking to somebody and asking questions synchronously in discord.

The chat scrolls so it doesn't matter if you say a random question or you ask a question that's been asked a hundred times. Someone will give you a link, but it's better to do that than to be the person on the issue asking the same question for the fourth time. Or asking the wrong question at the wrong time.

I think that's a little daunting as well. If you don't know how the project, the underlying secret sauce of the project is actually laid out for you.

**Jeremy:** [00:04:45] When I think about open source, I think about communication being asynchronous, right? Going through issues, emails, mailing lists, things like that. And you're saying if you're first starting out, actually the best thing would be to, to find more synchronous communication, find that discord room or gittir, or, whatever it is, where you can actually have a conversation with someone.

**Brian:** [00:05:10] Yeah. And to be fair I'm catering this more towards a beginner opensource contributor. If you're experienced, do the regular thing, reference the issue, open up the PR, and no need to look for a synchronous communication if you know how to solve the problem.

GitHub itself is like 50 million developers worldwide. There's not 50 million developers doing open source. Let's just be clear on that. So there's a big difference between the users on GitHub who are just shipping code, like normal building websites for their companies or mobile apps or whatever it is to the people actually contributing the code that's powering all that stuff and powering GitHub as well. 

I'm using this term called unintentional gatekeeping. I've been thinking about this a lot and I want to write a blog post on this because it's around the flow of information. So if I happen to be in the right Slack channel or the right discord, I have more information than the person who's not there.

Because there's more information flowing through there than there are publicly on issues, because issues are treated as like a statement of work. You're declaring that this is the way it's working or declaring that it's broken and next steps to reproduce it or whatever it is.

And same thing with PRs. Like you're declaring this is the work I've done. This is the next steps. You review it. It's very robotic. But when you have that relationship that's built in a Slack channel and like, this is similar if you go to meetups or if you happen to know somebody from college or high school or whatever it is very similar. That relationship is like a relationship that helps give you that extra edge.

And I think when we talk about things like tech, there's definitely a lot of conversation about diversity, especially today. so when we have diversity of backgrounds, diversity of culture, where people coming from, you tend to find a lot of the, especially newer, smaller startups have a mono cultured diversity.

And people are well aware but there are VCs who are telling us it doesn't matter when you first start out just build a product, get all your friends in the same room. Build only the culture fits and stuff like that. And then let's move on and then we'll figure it out when the company is like much bigger and it has like much bigger issues.

So I say all this because it's opportunity for people to become quote unquote of the culture of the open source project by just being in a room like this being in the room and listening. And if you find out that maintainer or the contributors are not your cup of tea you can just move away and move to another project or fork the project and create a new project that's similar but has a different culture.

Like, open source a lot of these things are MIT licenses, no limitation for you to try things out and maybe copy code and create your own project and see if there's growth in that approach. I don't recommend that. But if that's your approach, definitely try it out.

**Jeremy:** [00:07:56] Another thing that I often hear when people talk about wanting to get into open source is they have trouble finding someone to mentor them or help them through the process. I wonder what are your thoughts on how we can improve that experience?

**Brian:** [00:08:13] Yeah, this is more on the maintainer. Individuals who are managing the projects. I mentioned the onboarding experience. There's obviously opportunity for them to have better onboarding. Have some clear steps of what your expectations are for people to contribute to the project. Not just how to clone it and open a PR but more of like, how do you report an issue?

Is there a template for reporting issues that can guide the person into actually asking the right question as opposed to free for all and then your issues turn into stack overflow which is not the best place to ask questions is GitHub issues. Like you could do that, but stack overflow it's an entire platform built for that reason. So how do you kick people from issues to stack overflow instead? 

We didn't talk about what sort of code, right. But, I do a lot of JavaScript and there's this one library called express JS. it just builds quick servers for your websites and web apps and ExpressJS actually did ship something really recently, I think back in April, they merged in this new quote unquote feature or a guide, which is called the triager guide. Are you familiar with this at all?

**Jeremy:** [00:09:16] I'm not.

**Brian:** [00:09:17] Yeah. So, basically what they're doing is they're instead of saying, Hey, We have a lot of issues go ahead and pick one up and like merge it. Or not even merge it just open the PR and we'll go back and forth for like weeks or months.
And then we eventually merge it. 

Instead, they're saying if you want to intro into express, you don't have to know anything about express. You don't have to use express. We have this role called the triage role and it's literally a team in the org that you can join if you just raise your hand and your job is to triage issues.

So if someone provides an issue. If they don't provide reproduction steps, you kick it back and say, Hey, can you provide reproduction steps? So if you don't know how to do it, then the maintainer probably won't know how to do it. Or maybe they do, but that's a lot of time for them. 

So joining like a triage role or having an opportunity to do that, to label issues, to mark things as ready for review or ready to contribute or whatever or good first issue or whatever it is like that's-- express has a lot of issues and there's a lot of time spent trying to figure out is this valid or is this not?

They're actually taking help from the open source community, giving them a badge, which is the triage role in the project. So it shows up on their profile. That was great for prospective employers. Like, Hey, you're in the org, we're using express, you have access to the maintainers. Maybe we can get our features on there.

That's eye opening and it's eye opening that I have not seen that at all until very recently. So me personally, for my project, I just launched a triage role. Cause I want people to be able to have an introduction into my project, which is a react app without needing to know react, like all you have to do is know how to answer questions or how to find information.

If you don't, there's other people on the team that can help guide you. And we have a discord as well that can guide you to actually getting things shipped.

**Jeremy:** [00:11:02] I've noticed when you watch people's livestreams for coding and who work on open source projects-- a lot of the time they spend is actually on issue triage. Is on looking through all these GitHub issues, figuring out which ones are valid and which ones are not. And so I think that's an interesting idea of getting people started there so that they get to see the process of open source without necessarily needing to jump straight into the technical details. That's an interesting path to get more involved.

**Brian:** [00:11:36] Yeah, I like it. I'm curious of, what Twitch streamers you watch too as well cause I've been trying to collect the list of myself. But I like watching people do open source, actually. I think right now, Jason Lengstorf is doing some open source right now on his Twitch stream,  I'll catch the VOD later.

But, yeah, I think that's actually a good thing you brought up to you as well. Cause I've been doing some Twitch stream myself and trying to figure out what is the purpose for live coding on Twitch? Is it to give webinar type tutorials like screencasts, is it to interview like what we're doing on a podcast or do that as a Twitch stream and where I found my niche or what I like to do on Twitch streams is actually do exactly that triage issues.

I'm actually gonna be live streaming later today. And I've been doing some sketch, some UI building. I'm not a designer. At all. But I took a course last fall and learned how to use sketch to build some UI templates to not have to rely on somebody else to actually get me across the goal line for our shipping projects.

So I'm going to spend 90 minutes building out some UI, and actually trying figma for the first time too as well. Cause figma, it's sort of like the GitHub for designers. I'm not sure if that's the summary of their product. I don't work there, but, yeah. So basically I'll be doing figma.

I'll be building some UIs and some wireframes. Just sort of figure out the next steps, cause I've got a backlog of features I want to add to my project, but I don't know how to tell people that this is how we're going to work on it. Cause I have a whole I think 17 contributors at this point I was going to say team, but they're contributors. We do have teams in squads or whatever. But yeah, so it's easier for me to get everything in my head and the vision for the project out onto like a UI. And let individuals know. 

But my question, I first asked, like, I'm curious, who are you watching on Twitch?

**Jeremy:** [00:13:19] Yeah, so I  just, dabble a little bit. One of the people that I find interesting is, Suz Hinton and sometimes it's like issue triage type stuff, but also sometimes she works on more hardware type projects, in sort of the intersection between working with JavaScript, but actually working with, physical hardware and actually wiring stuff up. I don't watch a lot of streams but things that are interesting for me is being able to see someone's thought process. Cause often when you watch a streamer they're talking through their process and what they're thinking and whether it's doing triage or whether it's working on a bug or a feature. You get to see how somebody works in a way that you wouldn't from a screencast. With a screen cast or a lecture they're very well prepared. They've been practicing, whatever they're trying to teach, whereas in a stream it's more this is something that they haven't done before, and you're just going through that process with them.

**Brian:** [00:14:25] yeah, Suz Hinton, I guess. Is it nope cat or no op cat?

**Jeremy:** [00:14:30] Yeah, noopkat, I think that's right. Yeah.

**Brian:** [00:14:32] Yeah. Yeah. Not hearing the word said out loud. I say noop and nope. noop. I interchange it's like

**Jeremy:** [00:14:38] They're probably all right.

**Brian:** [00:14:41] Yeah. So I've actually watched Suz and I like her style and I like the projects that she works on too as well. I've yet to catch her live in a while.
So I don't know if she stopped streaming. 

But yeah, similar to yourself I like seeing the thought process and the people walking through how to build things. Because at the moment a lot of us are working from home. Especially in the state of California. And we're not sitting next to our coworkers anymore and asking those questions.

I think twitch has in the last three months it's sort of exploded with live coders, and live coders as in the general people who live stream and code at the same time. Because I think a lot of people will just figure it out, like, Hey, I need to have community and I'm not getting it through my team Slack channel. So it's been an interesting transition as far as like a whole other culture that's growing on Twitch at the moment.

**Jeremy:** [00:15:35] For sure. And then for yourself as the person who is doing the streaming, what do you  get out of it and what are you looking for?

**Brian:** [00:15:43] Yeah, I mean, it just comes down to community. I started the stream, mainly because I wanted to have a place to start throwing my ideas out there for the project I'm working on right now, which is open sauce and I started streaming two years ago.

I'd heard of people doing live coding on Twitch, but it wasn't very popular at all. Only a handful of people were doing it and I even talked to some people at Twitch about it. Some people who were familiar with this space and were knowledgeable and so I started doing it, but I didn't really have the proper equipment. 

I had my Mac and I was just streaming from my Mac. And nowadays you gotta have proper lighting and step up the game a bit and a green screen as well which I'm sort of sitting in front of it at the moment.

I was doing that but I sort of fell off because my daughter was born just a couple months after that. So I took time off from work but also took time off from coding, just to enjoy some paternal leave. 

But anyway fast forward to very recently which is a couple of months ago I started streaming again focused on trying to build an open source project and just have a place to write code consistently cause my day job is developer advocate and I don't have any long standing projects that I work on a regular basis. 

A lot of stuff I work on it just sort of ships complete and then we don't touch it unless there's something broken. So once I get done with the actual shipping something, I just move on to the next thing. So there's nothing that I can feel proud of that I continue to work on. Or where I do like the latest and greatest things like Vue JS or whatever. I shipped Vue projects, but I move on and they just work until I have to do maintenance on it. 

So I wanted to have a consistent place where I could just talk about a story of a project that I was working on, which again, I keep mentioning it, which is open sauced. And since then I've actually built a community of quite a few developers interested in the same problem I'm trying to solve which is open source onboarding.

 **Jeremy:** [00:17:32] Let's get a little bit into open sauce. We were talking about a lot of different troubles that people have when they're trying to get into open source.  How is open sauce trying to address those?

**Brian:** [00:17:42] Yeah, you tee'd it up for me earlier with the whole trouble getting into open source, it's onboarding. So we're building a platform to provide structured onboarding for open source projects. So like me connecting with maintainers and projects to add a simple YAML file to the project.

So that way anybody who navigates to the project on open sauce, can have a good, like step by step process of who to talk to, how to get involved in the project, where to go for the synchronous communication. 

The other thing is that tracking projects is something you can do on GitHub, but it's not really built for that. At least today, like hopefully GitHub gets on board. And puts open sauce or adopts a lot of the features that we're sort of building. But the goal is not to track projects you're already a part of or even track projects that that you're working on. 

It's more tracking projects that you want to quote unquote stalk. So like a GitHub star is a thing sort of like you hit a star, like, or whatever on a project. And it goes into like a list. And usually most people just forget about that list because you just add a star, like that's about it. It's like sort of Instagram. You just add a like, and you move on and that's what GitHub stars have become.

So it's hard to track things that you're interested in based on stars. You could watch projects, but then when you start watching projects it becomes a basically signal to noise ratio. So then with a very popular project, you don't know what you're looking at. So then you fall off immediately, cause this is too much information or not enough information, one or the other.

Yeah, so basically there's not a lot of tools. So I think a couple of years ago, actually, when we met a couple of years ago, I had just shipped a little side project for myself, which is essentially bookmarking issues. Issues that I wanted to work on GitHub. 

So my day job is at GitHub. I've actually seen internally this feature be built a couple of times, but we sort of backed away from it cause it didn't really solve the right problem. And so as soon as I joined GitHub, I was like, Oh, maybe I won't work on this thing anymore. So I took a bit of a break and then noticed that we weren't shipping it.

So I just picked it up recently, but essentially you could find the project you're interested in. Find the issues that you're interested in and mark them to save. And then manage the note taking. So if you want to take notes on like this is the maintainer to talk to, this is an example that I can leverage to solve problems or help triage things, even like-- 

So I was trying to contribute to the graphiql opensource project graphiql. It's like a little playground to test out GraphQL queries and trying to contribute to that was actually pretty hard. There was a lot of context I'd missed. And at the time the project itself was transitioning from Facebook's org to the GraphQL foundation.

But also pretty much everybody who was becoming maintainers on the project were actually transitioning in and owning the project. So there's a rough transition into that, moving from org to org, but also the maintainer is becoming acclimated to the project as well.

They were all familiar with it, but now they own it. So they are all trying to figure out the best practices and how to clean it up. So at that time that's when I was trying to contribute. So I was looking at the issues and I'm like, man, I think I could solve this one, but I'm not finding the bug's actually invalid because it seems to be fixed.

So they had a ton of old issues that were just sitting there that were invalid from that because the transition cause they had fixed a bunch of stuff. They were still getting acclimated. No one went through and closed out a bunch of old issues and to close out a bunch of issues automatically with no reason or question sends the wrong signal to the users. So they just sat. And I tried, I tried working on an issue that was invalid. 

And I discovered that when I commented on the issue with my thought process, the maintainer or one of the maintainers came back to me and was like, Hey, this is actually invalid. All that backstory, I just told you, he told me right there on the issue.
And he's also like, Hey, we also have the discord, that you should come and chat with if you want to work on anything else. And I was like, Oh, okay. That's weird. Like in the repo, there was nothing about a discord. They since added it. But then I was able to get all that context, the conversation and the questions, like, what is happening with this project? Like where can I help out all in discord. So that's like, that's sort of the summary. 

That story is a summary of what I'm trying to accomplish. No one, like myself needs to go into a project and be confused with skills. Like knowing that they can actually do something. To fix problems, but they don't know where to start and they don't know how to approach it because the way I do code at GitHub is different than the way GraphiQL is doing it in their repo.

So that's the high level goals with some other features that we're trying to work on, but, we're always taking ideas. If you go to opensauce.pizza, that's the actual website that's live github.com/opensauced that also exists for anybody who wants to contribute or just ask questions.

Open ideas, open the cool ideas, or bad ideas. It doesn't matter. Open up a discussion. We'd love to hear what problems they're facing in open source.

**Jeremy:** [00:22:39] Do you envision this being something where the list of projects is curated or is it more somebody can pick any project on GitHub?

**Brian:** [00:22:48] There are projects that do curation for open source projects. So GitHub has the explore feature. You can sign up for a newsletter, you get a bunch of projects every night or every week. I forget what the cadence is. And then change log has a nightly, the most popular projects. Here's a list of them, check them out. And then there's like also code triage was another project too, as well. Where you can also be curated a list of like Ruby projects or JavaScript projects as well. We do want to have curation as a feature. Like this is more there's a repo that you're using or a library that you're using. Add the library or the repo just the URL to open sauce to your dashboard. And this is all login through GitHub. It's using your own data. The backend is all the open source repo. 

So when you log in, you click the create the repo button, it starts tracking all your notes and all the issues in the repo itself, all open source. So once you've done that, then you have a nice tracking issue to then say, okay, I've looked at this issue, look, this issue, doesn't work, invalid or whatever. I closed this. We also track your contributions as well. So if you do any sort of PRs they'll show up in the list, but also in addition to that, it also tracks your issue contributions. So if you comment on an issue, it shows that in the list as well. So that in the eyes of open sauce, nontechnical contributions are contributions. That's another thing that I stand on, which is just because you don't have a green square for that day. Doesn't mean you didn't do anything.

The platform itself, the answer to your original question-- No curation today, curation in the future, maybe it is on the roadmap. It's not actually realized in a plan. But the focus really is around if I already know the project I want to get involved in, can I just take it to open sauce and get all the information I need, digested.

So I can just click the steps one, two, three, even to hammer down on that onboarding experience, like there's a project called babel they do transpiling for JavaScript for different versions. Like one of the best things you can do if you want to contribute to Babel is use Babel.

I did mention triaging is another thing you can do, but if you already know how to do it and you're ready to start-- use Babel use Babel plugins, build a Babel plugin, like try going that far and seeing actually how it actually works under the hood and how you interact with the actual babel core library.

So that's a recommendation and that's like a recommendation I'm actually trying to work with that team. Hopefully. I talked to him months ago, but I haven't really picked up the conversation because I wanted to focus on actually getting a dashboard working. But I would like to see as an onboarding experience, if it's like a Webpack or if it's Babel or something else, as part of my onboard experience, build a simple tool or clone or a hello world to actually get my brain wrapped around it.

So that way you can confidently go in there and answer questions around, how is this broken for this user? And how can I fix it in the context of what I know?

**Jeremy:** [00:25:39] So it sounds like coming up with-- I'm not sure what you would call it, almost like an exercise of before you contribute to this project here's a well-defined thing that you can build so you have an idea of how to tackle a real problem.

**Brian:** [00:25:56] Yeah. Yeah. And I think it's easier for some projects than others, But I think that's on the maintainer to say, Hey, here's the contributor guide. But in addition to the contributor guide, here's the actual action items to do to get yourself up to speed. So whether it's build something on your own or just clone one of the example repos and walk through that, those are all possibilities. 

But it's up to the maintainer, not everybody has to have the same sort of step or guides or not everybody's working on projects on the web. But as long as you have the steps, that's all that matters. So if someone actually knows what the step is to actually get started, that's helpful.

And like, we're talking about at the moment we're currently in like a existential crisis or at least America is. And there's a lot of people who have been underserved by their leaders and their community leaders and even the higher level of government. And like you go into cities. And there's a different, this like take like LA County. LA has one of the largest police forces in the United States. LA has one of the worst public school systems in the United States. I know we're talking about a political issue so I won't go too deep in that, but really what it comes down to is like actually information sharing.

So if somebody who is in LA County, and working towards life skills or just like growing their career or whatnot. If they have to go to the public school system there they're going to miss out on a lot. Like there's going to be a lot of information they just don't know. And if you happen to be just one County over, which is Orange County, then you're in such a better experience. And it's such a much better step up. 

And I think that it comes down to like, if I want to contribute to open source and I wanted to level up my skill in my career am I getting the right information by contributing to this project? Or even using this project? I think that should be a decision that we should make as far as contributing to projects.

If there are not people going in there and contributing and it's that free form, like free flowing information. And there happens to be few people who are managing the project whether it's good or bad that should be eye opening. Cause then you have one or two points of failure, like one person gets sick or has a kid, or takes time off. Then it's down to the one person left over to actually contribute. And there's nobody else in this entire developer community that has knowledge to actually contribute back. 

This is maybe not popular to talk about but Facebook has a lot of open source projects that we are leveraging entire products our features our companies on. Yeah, but the only people who work on that are technically Facebook employees. So is that really open source? And I know things like React, they do have contributors outside, but the individuals making all decisions are internal Facebook employees.

And I know they have the best interest in the open source community. I'm picking on them because they just happen to be the example I have on top of my head, but it didn't seem like information is really flowing in back and forth. And maybe I could be corrected too. I'm happy to be corrected on that. And if there's information on the react community that allows people to onboard a lot easier than I'm all for hearing it.

I'll probably do my research after this podcast cause I pulled it out of thin air and picked on them without having any sort of backing statement. But anyway, regardless, there are projects that do not have information flowing that we're supporting or we're leveraging in our projects. So whether it's react or not, we should take a hard look on, is there a proper onboarding for anybody to basically jump in there and get things done?

**Jeremy:** [00:29:37] Yeah, I think that's an interesting point in terms of when you have companies, whether it's Facebook or any other company you have people who are being paid to work on these open source projects and ultimately the company that's paying, they want to get something that's of value to their own company. And, whether it's a benefit to the rest of the open source community is it may or may not be front of mind. So I think that that's an interesting sort of, I don't know if you'd call it a problem, but a discussion to have. How much control do companies have over the software we use and is it too much, and on the flip side, it's like, if it's not companies doing it, then it's volunteers doing it. Maybe that's an issue too, right? Like that we're relying on so much software that's being worked on by people for free.

**Brian:** [00:30:36] That's the thing that I like discussing too as well, which is not just a onboarding decentralization of open source, like future. This might be counterintuitive to everything I said before, but when you talk about working for free, there is money being funneled into open source.

And again, I apologize for picking on projects that people love and leverage in their, their projects day to day, but look at a project like Webpack and I only pick on them cause I know them and I use them. And, I know the maintainers as well, but you see the project is making half a million dollars a year, just in open collective.

So that's the one location that I've looked at it and I can sort of cite today cause I've just looked at it recently. But that actually pays contributors to contract, to help solve and squash bugs. So like when you look at that, that's awesome. Actually, hats off to them and I think we should see more of that. I don't think that's a bad thing just to be clear. 

But what about projects like rollup or parcel or all these other bundlers and packagers and stuff like that? Those are all valuable projects, but they're not getting the same sort of funding. Are we voting by the dollars that we donate as well?
And, that's another question that was asked and like, I'm not here to say that's wrong or bad. I'm happy to fund other people doing open source. Cause I think it's more about not about true open source. Like the Richard Stallman, like open source, everything type of deal. 

Basically what I'm getting at is that we should put our dollars where our mouth is, but also we should put our money in the things that are actually providing value and providing information and providing access to all developers as well. The best thing about this is that you have all these bootcamp grads, all these college students, coming out the gate, leveled up, and ready to ready to ship day one, which is great.

There's no month long process of like, Oh, you're only stuck to doing bugs or reading articles. You can actually ship code day one because you have the GitHub account while you're in college, you have access to all open source technology. So if you want to build a quick website or a Minecraft server, whatever it is how to interact, like with stack overflow in forums and answer questions to get your job done.

And, that information sharing has exploded the ability for us to grow our developer community. To be able to hire developers and train them quick. And like all bootcamp grads are only two years behind from anybody else because they just need two years of experience to actually get up to speed because the web, the mobile, everything like code changes quickly. Well, not all code not all code's the same, but I can speak for the web. The web moves quickly. So you're only two years behind the last person.

 **Jeremy:** [00:33:19] Yeah, I think that's really great that more people are getting exposed to the idea of what open source is and having the skills to be able to contribute. And what I also think is interesting is Dan Abramov, who's on the react core team and he's also the creator of Redux.

He was talking on a podcast and he was saying he has all these projects that he no longer maintains that he used to work on and he feels a little guilty about it. But he was also saying that if somebody comes in and takes over those projects, some of them, when he was working on them, he was working on them at Facebook.

So he was getting paid to work on them. And when you have somebody come in, who's coming in on a volunteer basis. I'm not sure the word he used. It's it's almost like they've been tricked, I guess is what he was saying is. I was working on this thing, getting paid for by my employer and somebody else is coming in and taking that on for free. And so there's this interesting imbalance in terms of the people who are getting paid to work on it and the people who aren't.

**Brian:** [00:34:25] I mean, it's a challenge cause there's a lot of people actually able to-- GraphiQL founder or sorry, maintainer I was talking to, he's getting paid full time to work on GraphiQL. So there isn't a balance. Like he definitely is a knowledge holder, but I think that's a testament of like I spent at least two minutes, dogging Facebook, but also it's a testament to Facebook that they actually value putting open source maintainers there full time, to support the community and also even open sourcing it in general. 

Like there was a time when I first got into programming where you didn't open source stuff, just because like, it didn't make any sense. I talked to people at Pinterest and they open source somethings like they had a very similar front end framework, which they called Denzel. And like, maybe it was open source. I don't remember, but I'd never even heard of it until I talked to someone at Pinterest. 

Facebook put the time into actually promoting it, putting a conference on and actually getting people to care about it and saying like, Hey, this is actually the way to do it. They get value because then it's easier to get hired at Facebook. Despite the fact that they don't actually use React in their interviews, but it is a leg up, like you're knowledgeable that Facebook is hiring and hiring React developers or JavaScript developers, or we're even doing JavaScript at Facebook.

So I would say that the value that the person who's sliding up against, Dan and working with them and getting feedback from him, he's actually getting mentorship directly from Dan. And I would say that's not a monetary value. That experience that relationship that you get is invaluable to be quite honest.

And I said, I was talking about the whole LA County and the information sharing, like the more, the information is shared, the more value it's going to be like, the information I've gotten for free from just doing open source, it'd be involved in the community and going to meetups, is invaluable. I would not be here today without it. 

But if I relied on someone to tell me that or me reading my own blog posts or me figuring that out myself, I would not be here today. So I would say like, yes, it would be nice to have a six figure salary to work on open source every day and triage a bunch of issues. That'd be amazing. But also the fact that Dan's accessible, and makes himself accessible, I think, is what it makes the biggest difference. Dan he is a figurehead for the React community. But the fact that I can go to React. Open up a PR and get Dan or Brian Vaughn or somebody else from the team, to actually review my stuff and give me feedback and tell me what's up and make me feel comfortable. That's a big deal.

**Jeremy:** [00:36:57] For sure. the way we learn the quickest is when it's from somebody who knows more than us, or has come before us, is able to teach us. And like you said, I think that can be really invaluable for sure.

**Brian:** [00:37:07] Yep.

 **Jeremy:** [00:37:08] Another thing I want to talk about is you've been a developer advocate for GitHub and previously for Netlify. And I know in the past you had mentioned you had been a little hesitant to take on the developer advocate role because you were really interested in coding and engineering work.

Have you ever thought about going back into a more engineering focused role or what keeps you in the advocacy role?

**Brian:** [00:37:37] So what keeps me there is my paycheck. So I'm paid as a senior developer. That was the whole deal for me to go to, GitHub. And, that's helpful. 

Also. I love community. I love interacting with the community and having opportunities to be out there. I missed being able to just put on my headphones and just write some code all day, go to lunch, come back, write some code all day and then have maybe a meeting once a week, do a standup once a day. I do miss that. And I do miss that solidarity time, but also, I mean, I am a pretty outgoing person and happy to have those conversations. 

So like there isn't a balance, of doing that. And I think a lot of devrel folks, they  come and go, not like they don't quit devrel, but they do go work on a project for awhile just to get back in the right head space, to be able to actually talk about devrel.

Like one of my biggest fears from doing developer advocacy full time is that not working on a project full time on a regular basis your skills start to not keep up because I had mentioned you're only two years behind in the last thing that came out. So if you're not constantly trying new things out and seeing what's out there, then it might be harder to get an engineering job later on.

I've mostly give up on the dream of climbing the engineering ladder. And I've only made that decision recently, because I think I get a better feeling around writing code when it's my own code, but also open source. So another reason why I even have open sauce is because it was a project for me to have long standing code, like learn how to write, test, learn how to use hooks in React when everybody was transitioning, like I had a project the ability to leverage and there's no pressure to ship there's no PM pushing me to like, Hey, we should have had this last week. 

Like I get to basically instead of sit and write code, I watch a lot of tech videos.
I do a lot of screencasts. I do a lot of Twitch videos as well, so I have more freedom and less pressure to ship things. Mainly because I don't have a project that needs to be shipped constantly. So I tend to build, and I like the pattern as developer advocacy and I recommend this for anybody, like build a project that you can actually use to leverage your skills and keep that going.

So whatever it is, if it's your sourdough bread making app or whatever it is to tell you when to feed your starter, Which I mean, I mentioned that because I actually want to build that, but, anyway, like build something like that so that way you can leverage and talk about on a regular basis and I think most devrel folks, they have that app for them. And I think open sauce is mine. So yeah. I guess the original question was like, yeah, I do have feelings around  doing full time engineering, but I'm actually pretty content with my role today and my access to information and leveling up my skillsets.

I am not spinning up Kubernetes clusters or even know how to do that. I've done it before, but like, it's going to take me a bit to refigure that out. Like just give me the one that's working on your repo and I'll go from there. And that's my approach to code, it's write it quick, get it done. And maybe write a test.

**Jeremy:** [00:40:41] Yeah, that's cool. You may not day to day be diving in really deep on coding every day, but you keep that for yourself for your own personal project. So that you keep your skills up and plus you get to work on your own terms at your own pace. So you don't lose that joy or the the fun of just building things.

**Brian:** [00:41:04] Yeah, and I mean, to be clear too. I do have projects that I do maintain. It's just that these are projects that I only maintain like twice a year for updates and I'm just basically having the dependabot, update them for me. And then every now and then we'll add a new feature or answer a question or something like that, but all closed source stuff to make my devrel a lot easier.

**Jeremy:** [00:41:26] Cool. I know we're running up on time. And I just wanted to ask you one more question. Five years ago you were a new developer. you moved from Florida to the Bay area. You attended a lot of meetups and community events, and now you're on the other side, you're the one giving talks, giving presentations and talking to new developers. How do you feel like things have changed?

**Brian:** [00:41:52] Yeah, I mean, it's changed a lot. And I think asking the question now at the time that we're in currently, I envision it's gonna change even more in the next year. But I would say when I first got the programming, jQuery was definitely a legitimate place to put all your JavaScript. CoffeeScript is probably the next level above it. And they were pretty legit things to use. I know a lot of JavaScript developers from 10 years ago probably are cringing for me saying that but you didn't have to know a whole lot. I think we had a lot of stuff that we just took for granted and we've seen a lot of security vulnerabilities because of that.

So I think now-- I feel like the developer space is just leveled up in being educated in things like security, progressive web apps. So with that being said there's a lot to learn. So you can't be counted on to know everything. And that's the other thing about being a developer advocate. It's like no one knows everything.

There's no pressure for me to get back in the engineering full time so I can know everything. Cause no one does, no one's perfect at backend orchestrating of servers and spinning them up in containers. And even on the front end doing CDNs, like no one's really expert on that.

And I think people are really focused on things like the JAMstack where you can just pick and choose and leverage tools and free accounts that get your stuff mostly done. I think that's been a big change as well. And I think I've rode the wave in that change where I now have an entire project where I have no database.

My database is literally github.com and could I have done that as easily five years ago? Probably? I roughly did it four years ago but four years ago as a junior developer. So like that goes to show we're transitioning the way that if you wanted to build something on top of a third party API or whatever, like there's a lot of tools for you to use free and I think there's a lot of VCs and a lot of founders and a lot of open source projects that are really looking at the space and looking at this sort of mock regurgitation of developer tools and how anybody has access to anything. And it's been super fascinating to see that.

**Jeremy:** [00:43:53] Cool. Well, I know you got to get off to a meeting, so I just wanna say thanks for chatting with me today, Brian.

**Brian:** [00:43:58] Cool. Thanks, Jeremy. Looking forward to seeing what comes out.

**Jeremy:** [00:44:02] I hope you enjoyed the chat with Brian. If you're interested in getting an open source, you can check out the show notes at softwaresessions.com. I've got links to Brian's project, open sauced and a link to where he does his Twitch streams. The music in this episode is by Crystal Cola. Alright, I'll see you next time.

</div>