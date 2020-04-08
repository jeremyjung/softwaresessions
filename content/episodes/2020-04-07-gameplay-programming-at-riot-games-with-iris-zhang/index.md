+++
title = "League of Legends Gameplay Engineering with Iris Zhang"

description = "Iris shares her experience working on backend services and gameplay at Riot Games"

[extra]
episode_url = "https://media.transistor.fm/ab7a382f.mp3"
+++

Iris Zhang is a gameplay engineer at Riot Games on the League of Legends Champions Engineering team. She previously worked on backend services at Microsoft.

We discuss:

- Working at Microsoft and Riot Games
- Finding a role and team that fits you
- Backend services vs gameplay engineering
- Building features, testing, and debugging gameplay
- Using internal tools to create game logic

### Related Links:
- [Personal Site](http://www.iriszhang.com/)
- [@riotnyanbun](https://twitter.com/riotnyanbun)
- [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) (Book used by Microsoft team)
- [Spring Framework](https://spring.io/) (Java web framework used by League of Legends)
- [Chef](https://www.chef.io/products/chef-infra/) (Deployment tool used at Riot)
- [Hazelcast](https://hazelcast.com/) (Cache that Riot Games switched to)
- [What it's like to work on League of Legends](https://builtin.com/media-gaming/riot-games-technologists-working-league-of-legends)
- [Sylas](https://na.leagueoflegends.com/en-us/champions/sylas/) (Champion that can steal ultimates)
- [Clash](https://na.leagueoflegends.com/en/featured/clash#/) (Public facing mode worked on by backend team)

Music by Crystal Cola: [12:30 AM](https://crystalcola.bandcamp.com/track/12-30-am) / [Orion](https://crystalcola.bandcamp.com/track/orion)

---

### Transcript

<div class="transcript">

**Jeremy** This is Jeremy Jung and you're listening to software sessions. This episode I'm talking to Iris Zhang, a gameplay programmer on the league of legends team at riot games.

I grew up playing video games, and one of the reasons why I got interested in software development is because I wanted to make a game. Now, I never got to that point but Iris is one of the few people who made that dream come true.

So I thought it would be fun to talk to somebody who made that jump. Someone who used to work on backend services and mobile apps who made the switch to games. Here's Iris.

**Iris** I actually started playing league of legends I want to say nine or 10 years ago now, back in 2011 or so when I was working as a high school teacher in Philadelphia. And it was a really stressful job. I don't know if you've heard of Teach for America.

They send young college grads to high need schools. And League of Legends was sort of my way of coping with my job, so to speak. I always grew up liking games and playing games. I played smash brothers with my friends all throughout middle and high school. And then, I got really obsessed with like text-based RPGs in high school especially, but I never considered it as a career. Uh, seriously until a game, like league of legends got very big, and I saw that people could make a career out of it. And, when I finally quit my job, I took a bit of a break from working in general, but I was really inspired by games like that, and I really thought that I could make a career out of it.

So that's when I decided I would give it a shot.

**Jeremy** How did you get your, your start or how did you decide what your next step should be?

**Iris** Right. Well, at that point it was definitely a pipe dream. So I started by taking, local classes. I think I was in Philly at the time, so I took some classes in computer science at the local college and I really enjoyed it. And then I decided to take it more seriously by enrolling in a post baccalaureate program at Columbia University in New York City. And that's when it got really serious. I wanted to get the credits I needed to get a master's degree in computer science. My family background is Chinese and my parents were pushing me really hard if I were to make a career change, it has to be through academia or through like a degree.
And they were sort of really onboard with the idea at the time too.

**Jeremy** It looked like you were actually doing work in games development and in mobile development when you started your masters.

**Iris** Yeah, that's right. Because I was already enrolled in my post baccalaureate program, I ended up finding a job through the jobs board at Columbia. It was a startup, like somebody had wanted to create an educational game for kids for the iPad. And they were just looking for people to help them sort of get that first prototype out the door.

And I, I just jumped on the opportunity. I just thought it was, it was so much fun. I get to make games and make a little money on the side while I pay my tuition. And thankfully the, the program at Columbia was like flexible enough that I could do both sort of part time.

**Jeremy** What would you say were like the big or lessons that you learned by going through the master's program that you might not have learned just working in industry?

**Iris** Yeah, that's a great question. At one point I had done five credits of my master's degree and I was I really didn't know if I wanted to finish it out. I felt like I was learning more from, my work at that point. to be honest, I'm still very, very glad that I finished because I think that academia still exposes you to fields in computer science that a normal like bootcamp or just like doing your job, at a startup or wherever. I don't think that really exposes you to the wide range of possibilities. That is computer science. and I'm really glad I made that choice in the end because I think it was in my. second to last semester that I took a class in computer graphics and that really cemented, the career that I had envisioned for myself, which was working somewhere in game development, adjacent to graphics or in graphics itself.

**Jeremy** It wasn't necessarily always just the technical skills you were learning, but it was getting exposure to people who worked in different fields.

**Iris** Yeah, definitely um, though the technical skills I think are also very important. Like, I actually know somebody who didn't do the full master's program, and all they did was they took the baccalaureate degree and just started their own startup with that. And I think that worked for him because he only needed the fundamentals.
And like learning the fundamentals is basically just a few classes like data structures and algorithms and advanced C plus plus.
So, with those classes under your belt, you're pretty much past the bar as far as like, yes, I can now start working as a software engineer.

But if like you wanted to be a serious computer scientist in the future, or get into fields that are more specialized, like machine learning or graphics or computer vision, or even research in the future, like I think that finishing out the degree unlocks those doors for you.

**Jeremy** So like a, generalist or like web programming or something like that. Maybe the degree isn't quite as important, but when you're getting more specialized or you're getting into more research type fields, then that degree is a lot more important.

**Iris** Yup. Exactly.

**Jeremy** Did you also find that having that degree, not even talking about the technical aspect, but having that, paper, did that open doors for you that otherwise wouldn't have been there?

**Iris** Yeah, definitely. I don't think I would've been able to, get my first job. post graduating without having that degree without saying like, I was going to be graduating with a degree. So when I was on campus, I was part of a student group called women in computer science and they sent me to Grace Hopper conference, in 2016 and that's where I met Microsoft recruiters. And that's how I got my first job post grad.  I don't think that would have been possible if I weren't in the middle of like getting my degree at the time.

**Jeremy** There's a lot of talk I think within tech about, sort of, the barriers are being removed in terms of education, but I do feel like when you have that degree, people will see you differently when you're going through an interview process, some companies, they may not even, consider you unless you have that degree.

**Iris** Yeah. It unfortunately, for better or for worse, opportunities are still quite gated and, companies especially, you know, what they call the FAANG, companies or whatever, they seem to recruit very heavily from schools like Columbia or schools that have top computer science programs in general.
And like where they show up and like where they recruit. Like only schools like that have the, have the money really to like send you to those conferences or to host companies like that to come to their campus and to recruit.

**Jeremy** You started at Microsoft, you were working on, Azure, I believe, on backend services. Did it kind of align with what you were expecting or what was your overall feeling on that, that position?

**Iris** Yeah. It was really interesting because I had no idea what to expect. When I graduated Columbia, I had worked at one startup making,  iPad games, and I had worked at another startup called paperless post in New York city, and that's where I got exposure to , iOS development. At that point, I had really no, backend services experience.

For some reason, this team made me an offer and I was like, I just want to try this out and see if I like it or not. and I don't know what the reputation now is in, in school, but I remember when I was there, I had this impression that the backend devs were the most serious. They were, the developers developer, you know, like they had, all the hard problems like, to solve.

Whereas like client work, like iOS and a web dev or any kind of UX work was considered lesser, or like, Oh, like that's easy. Anyone can do that, but like backend that's very serious. So it was kind of like a challenge to myself too, that I can do it and prove myself in this field. So I kind of just went for it.

I was on a team of about, 18 engineers and we were divided into three pods essentially, and each of its pod kind of, manage its own work. But, we shared the same backlog of tasks. And I think the whole entire team struggled as a whole to, figure out what processes were most efficient for planning our work.

Aside from that too, as an individual contributor, I felt very, I felt very like I was a cog in this big machine that was Microsoft in this product. I was working on this product called Azure Information Protection. It's a service that runs inside of both outlook and it's available as a third party API for people to call. It's basically an end to end encryption service for documents from Microsoft documents, like text files, word files, emails, whatever. And I felt very separated from the actual end product  and what that was, I feel like I spent most of my time trying to understand business logic and like how this product was actually being used because I was so far removed from, from it as a developer.

And the, the development that I was doing was very, very specific, like, fix this particular error message that was showing up erroneously, in this backend call. Like, things like that, or like, fix this integration test. that's breaking, you know, like two times, two out of three times that we run it for whatever reason.

I think I probably spent the first three months, like, just fixing our tests framework. So the work itself was quite specific Like I felt like I lost a lot of agency over my work actually. Going from somewhere where I could like play around with buttons all the time and like see immediately the results of, what I was coding.

Instead, I was like, I have no idea what I did today. Then make, you know, this one error log, like now it just like error output correctly.

It was my first exposure to backend work and I think I would have felt very differently if I was on a team that had more agency. But yeah, a lot of the struggle for me was like losing that visual aspect of programming 

**Jeremy** yeah, because the projects that you had worked on previously, whether it's a an iOS application or it's a game, it sounds like it's the sort of thing where you make a change and then it's small enough where you can run that project and see exactly the change that you made.

**Iris** Exactly.

 **Jeremy** Like you were saying, you know, you feel like kind of like a cog, right, where you're fixing up this little thing, but, you don't really have the big picture. And so it's kind of hard to stay, stay motivated. 

**Iris** Yeah, absolutely. There were a lot of positives of that first job like understanding how a team like that works at that scale and working with very, very excellent developers who had very high standards for how code should be and how services should be managed and operated and observed.

That was something that I think will always stay with me. Like I, don't know if you've heard of the book clean code, but that was something that was like drilled into me at Microsoft and pretty much like nothing will pass code review unless it like stuck very strongly to those standards. And I think teams are different too.

Like I think my team was particularly a stickler for things like that and it gave me a really good understanding of testing frameworks too. Like I, I learned The difference between unit tests and integration tests and end to end tests and what all those functions serve. and then also what a really good, CDCI like pipeline looks like, because at the time Microsoft was still, a lot of teams had their own bespoke solutions, but they had all moved to this thing called one build at Microsoft. And just seeing that work across all different teams at Microsoft with all different products and having a work so seamlessly, like that really spoiled me actually for the future.
Yeah.

**Jeremy** So, so it sounds like big takeaways or the big things that you did learn were, how to test things and why you test things, how to work with, continuous integration where you check in your code and things kind of get built and tested on their own. and also, I guess just how to build things with reliability in mind, cause I'm assuming what you were working on, if it didn't work, then, people would be freaking out. So they, you know, they had a very strict process there.

**Iris** Yeah. It was very strict process. It exposed me to like what good looks like as far as engineering tools and engineering management.  I'm comparing it now to like every place where I've worked at Microsoft definitely had the most mature tools when it came to engineering

**Jeremy** Yeah. And before, at the smaller companies you worked at was it kind of you know, you would write some code and then you'd run it at your desk and just check it in and just hope things were good?

**Iris** That was the case at my startup, it was not the case at paperless. Like they did also have CDCI I think we use Jenkins. and everything was checked in through GitHub and, Oh, we, we had testing frameworks there too, but it was all on a much smaller scale, much, much smaller.
And if things would go would go wrong. Like. Those are third party applications, so we would just, you know, call them. Whereas at Microsoft, everything was in house, the people we'd call up were just people who are in the next building over  (laughs) 

**Jeremy** After the experience working on smaller projects and then working at Microsoft your next step was working at Riot. Knowing that you were working on a large backend project and you kind of weren't too happy about the fact that you couldn't really see the things that you were working on and the end product, what made you decide that you wanted to go to Riot and, and work on backend services there?

**Iris** Uh, remember how he said, like 10 years ago I started playing league of legends? Well, it was, it was no longer a pipe dream  (laughs) .

So, I think. I had clicked on a LinkedIn ad one day,  that riot had put out and I didn't really think anything of it. It was just a click to like, share my resume. And then I had a message from a recruiter, my inbox thing, like, Hey, we'd like to invite you to apply for Riot.

And I was like, Whoa, this is. This is real. This is happening. so yeah, I just like sort of on a whim, went through that process. At the same time, I was getting agitated with, my team at Microsoft and I was really, I was looking for a change.  Not really because of the work and the product that I was working on.

I think I could have been motivated to stay because I did feel like I was learning a lot and like seeing what good looked like. At the same time though, um. The dynamics on my team were not the healthiest. and at the time, I think Microsoft was undergoing a cultural transformation, starting with Satya, the CEO, trying to instill values like growth mindset in a lot of the teams.

But, it was still not there like leadership was preaching, these things, but middle management and depending on the team that you, you're, you were on, like that wasn't the reality of the day to day. So we still had some very toxic senior, I would say engineers. Just, I don't know. They had a lot of ego. They could not listen to feedback. And it was not an open feedback culture. Like any sort of feedback that you had, you had like you went through the manager and the manager would go take it to that person and they may or may not even take it very well. If they didn't like it would have come out in a team meeting, like in front of everybody instead of like done privately.

So things weren't great and I just ultimately decided that instead of staying at this team where I didn't feel like I would have much of an influence to, to change the culture. , I wanted to join a company where I felt the culture fit  me better.  So I think that's why ultimately I went with riot even though like it was still backend work. I also really loved the product and understood it, so that was a huge motivator as well. It was just sort of a woodwind in that scenario.

**Jeremy** Let's say you would make a change on the back end team, is that something that you could visibly see in the game or is it kind of more like you just knew that you had done something?

**Iris** Yeah. It was much of that, again, exactly how you describe on a backend team, you don't really feel like you have an impact on the end customer in our case, the player, and it's kind of painful. Really because, one of the, cultural values of Riot is player experience first.

So it's like you really care about the players, as a backend developer, if you mess up something for the player, nobody can log into the game anymore. So that really sucks. But also it's like you don't really get that many opportunities to ship a feature and say like, Hey, we had a hand in this feature.

One of the cool projects that my coworkers. I heard from them because they've worked on it that they will have worked on on this back end team with something. I don't know if you're familiar with league, but like you can level up until as a summoner. You know, you can acquire experience until you're level 30.

And so they worked on the project to undo that level cap and make it like infinite. So now you can go beyond level 30.  So that was a huge backend project for them. And they had a lot of fun doing that. 

And then there was another project that, people were working on called clash and clash is like a 5 v 5 tournament style. Like you get four of your friends together and you play, and then you get like rewarded for how well you do in the tournament. And it's like a Saturday, Sunday thing and unfortunately that project kind of crashed and burned once in 2016. And like they tried to do it once in 2017 They're finally beta testing it in regions. And now it's like 2020, so they're finally shipping it  (laughs) . 

But yeah. Um, so it's like projects like that, that only come around once every few years or so. Really. aside from that, it's like if you mess up, then players can't log in, but otherwise your work is pretty invisible still. You are still just managing like, looking at errors and trying to figure out what happened. Why couldn't people log in? Why couldn't people buy their skins? Why couldn't you know... things like that

**Jeremy** You don't really get celebrate new features very often, but what you experience is when something bad happens.

**Iris** Exactly 

**Jeremy** You don't get to experience the joy of the wins.

**Iris** Yeah 

**Jeremy** That's a bummer.

**Iris** Definitely. It definitely takes a special kind of person to enjoy being a backend dev,  in speaking with lots of back and devs over the years at Riot and at Microsoft and, in general, what, what I hear people talk about enjoying the most is like The detective aspect of, programming, the on call and being that like first responder type person.

As a backend developer on league of legends. In many ways, we played the SRE role more than we did the software engineer role. Um,  we, we did have features that we had to deliver on and tickets that we had to close. But for the most part, I would say we were mostly firefighting. Like the on-call burden was pretty heavy.
and diagnosing. Properly. What went wrong with our services? Was like, I would say more than 40% of the job.

**Jeremy** Yeah, that's pretty high. And it sounds like, you know, the stakes are pretty high too, so it sounds, it could be pretty stressful.

**Iris** Yeah. It was incredibly stressful. In comparison to my on-call at Microsoft league of legends on call is, Oh, I would not wish that upon anyone  (laughs) .

**Jeremy** So, you were working on a product that you really liked, but the actual work like you said, it was firefighting. You didn't really get to see the end results other than, trying to fix a problem. Even though you were working in games, you kind of had some of the same, issues that you had back at Microsoft.

**Iris** Yeah. And in many ways, Riot is a less mature tech company than Microsoft is, obviously, because it's not a tech company. At the end of the day, it's a game company. We're, we're in the business of making games, not tech tools. And calling back to what I was saying about Microsoft and how the tech tools are incredibly mature, like when we were debugging something, everything went into like a tracer that would post the logs into a system that I could easily query and find exactly the correlation ID of the particular call that like results in this error and then isolate it to all the other service calls that cause this particular, error. 

But at riot, we were like manually parsing through logs. Like there were, there was nothing. Our tools are very immature and we just like didn't have the infrastructure in place to properly diagnose anything.

And so, I learned a ton about like VMs and I, I learned a ton about how like Docker instances work and like all these things, mostly because like, I had to manually, navigate all of the hardware  (laughs)  that was like hosting our services and like deploying it myself through this like weird Merlin...

We call it Merlin. It was like, just like literally something we wrote on top of chef 
for league of legends. Um, and so like, doing all of that yourself, it ends up being. Quite painful. and it's not as fun to like, play detective when you feel like you are limited by the tools that you have.

**Jeremy** You're logging into production servers and when you're trying to track down a bug, you know, you have to find the right server and then.
Find which server from that, you know, to get to the next step and you're kind of jumping from server to server to, to kind of trace what happened?

**Iris** Yes, exactly. And a lot of times it was, it wasn't entirely clear, like what service went down, so trying to hunt down like the particular server and the host that,  was a troublesome one. Like that in itself took a long time. Whereas I think, uh, Microsoft, like all of that would have been traced already and then like dumped to you in a bug or ticket that like landed on your desktop.

Like, Oh, okay, I don't have to go hunting for those things. All those things are already like known to me. I just have to go look at the problematic node or whatever.

**Jeremy** Right. Can you kind of give an idea of the types of code bases you were working on, like when you were trying to troubleshoot what types of applications where these?

**Iris** So league of legends, the backend service is mostly a monolith that's written in Java and Spring. What we call the platform was like the monolithic platform that you would log into when you start the client for league of legends. And that just like it had so much crud in it in terms of like what it would do.

We had tried to separate out the services into its own microservices. I think that's like a trend that like every tech company, every company that uses tech has like migrated towards in, in recent years. Unfortunately with league of legends because I think it was written really quickly and people wanted it out the door they just put everything into one monolith. 

And so I think parts of the store were still in the platform. Parts of accounts were still on the platform. matchmaking, like, like queuing up with your friends was in there and like all these different things had its hand in the platform.

And so we were in charge of managing the platform, but really what we were in charge of, well it's like trying to figure out, what issues happened and what service and like relaying that down to the teams that actually own the services and then like trying to break apart the parts of platform that like should exist as its own service though we never really got to that part.

It's like that was always the North Star. But like, we didn't quite get there. I'll give an example of one project that I, I worked very long term on. It was a project to migrate all of the services, all of the things within the platform to use a different caching server than the one we had already in the game.

I won't like get into like nitty gritty details of it, but the reason being was like, we didn't want a relationship with this third party caching service anymore. So that was the only reason why we needed to write this migration thing. And migrations in backend services is usually a huge pain in the ass.

Because like, everything is just so coupled with that third party service so we had to write like an intermediate layer so that we could easily switch between one service and the other caching service. And then I learned a lot about caching, so that was cool.

But at the end of the day, it's like, ooh, what a project.

**Jeremy** Yeah. Were you trying to also make sure that you could use the old calls to talk to your new service, or were you also having to change all the existing code to talk to this new service?

**Iris** Uh, well, it had to be switchable on the fly.

So because our services like we expect it to be up constantly running. If we switch from one to the other, we want to make sure that  if it can happen without a restart of the service we should try to write it in that way.

I don't know if you're familiar with the service hazelcast, but that's like what we were trying to switch it to. and hazelcast was like, advertises itself as like a drop in replacement for this particular cache that we had been using. And it's also open source so it would be free for us to use, um, and we'd only have to pay for support.

So that was like a huge win in our books. But yeah it was a lot and all of our testing around doing this project was making sure that those original calls, once we switched a particular cache over to hazelcast, that like those calls still worked and that it scaled appropriately to scaling is another issue that backend developers have to deal with. Um, nothing works unless it's at scale for a backend developer 

**Jeremy** Especially at the scale of, league of legends.

**Iris** Yeah, exactly

**Jeremy** Did you reach a point  the work you were doing, you sort of decided like, Hmm, maybe this is, maybe this is not for me and I want to go find something else to do. How was that process for you?

**Iris** Yeah. So at some point I began to, internally, reach out to people, working on gameplay, because I had a feeling that my passion didn't lie in backend. In speaking with people who did like it, I really don't care about services at scale. it didn't really satisfy me that like a request like now, 50,000 people can concurrently request a service  (laughs) like that. That seems to like really excite some people. And I just was not a developer who was very excited about that. 

So, the things that I was excited about and like, I harken back to my game dev days and, my, iOS app days is like, I really love delighting end users and players with like visual things that like, feel buttery, smooth, whether that's like a button click or whether that's like something in the game that like delights them and excites them. It just looks really cool. The visual aspect of programming was something that I really had missed.

And thinking back to the graphics course that I took at Columbia too. Um, what really excited me about that was just how I miss resource constrained environments and programming. Like with a managed code like Java and most backend services, you don't really care about memory at all. At least locally on the host. It's like you have, you have loads of memory that's not an issue. Like you, you care about serving like you care about network calls and making sure that network calls are, as fast as possible. and that you, you minimize network calls. But that's, that's happening at scale. That's not really happening on the scale of the device.

And that's something I missed really from my mobile days too. It's like having that, memory constrained device,  and working with memory management

**Jeremy** So when you switched roles, you joined the, the champions engineering team, could you kind of explain what that team works on?

**Iris** Sure. We are embedded on a team of VFX artists, animators. Concept, artists, character artists, and game designers. We are working on the tools that enable other creatives to create the best champs.

**Jeremy** Can you give an example of a tool that you might work with to, to help a designer or to to help an artist?

**Iris** Yeah, absolutely. So, League of Legends uses its own proprietary game engine, and we also have a few proprietary tools. one of those we call Riot editor. It's The one tool that most artists interface with at Riot,  to make league. And this tool has a whole bunch of tools, embedded in it.

For example, we have, animation station where animators are playing animation tracks and editing those tracks within the tool. And then there's also particle town where VFX artists are designing the particles that are used in the game. Game designers use this thing called a block builder.

It's like a drag and drop programming language that designers can use to build the game logic for the champions.  And so as game engineers, we have to be very familiar with all of these tools.

We also own the code, for these tools and improve upon it so that we enable people to, create even more complicated champions.

**Jeremy** In this case, it sort of sounds like your users are really the internal staff at Riot. Like you're building these tools for them to build the game with right?

**Iris** That's right. Though. as engineers, the work is divided such that we actively own a champion in development. And so. We are intimately familiar as well with the gameplay of the champ and the it's kit and like what it should look like and feel like. And that way we are empowered to actually propose like solutions about how to design the champion, but given the limitations of our tech, or we could say like, Oh, we think we could push tech to do this thing, whether it's in the engine or whatever. Whether it's through tools or through the engine or through, block builder or whatever.

**Jeremy** Could you give an example of something where you can either give people more options because you can push the tech, or where you actually push back and say, no, we can't do this because of these technical reasons?

**Iris** Yeah, I have two examples. One where we really pushed the tech and one where we are like, nope, we cannot do this.

So for example I don't know if you're familiar with the game, but there was a champion that was recently I think he was in the past six months or so, that came out called Sylas, in League of Legends.

And Sylas is a champion that that steals spells from other champions in the game. And for a champion like this to exist, all of the spells and all of the champions within league of legends had to be basically (laughs) rewritten to use an external, like a meta system so that Sylas could steal their ultimate spell. 

And so this, this took a lot of effort from engineering to like propose a solution. They basically had to migrate all of the data from old champions over to this solution, while also keeping in mind that like, this is such a big chunk of work that like, it had to be timed correctly and scoped correctly in order to do it.

But, they were so excited for this new possibility that it was decided, like, yes, this is worth the engineering effort to overhaul all of the champions in league of legends just to enable this. 

Another example: I'm working on a champion right now. I'm not at Liberty to say what they're all about, because it hasn't been announced yet. But one of the parts of the champion, that was requested of him from the tech side was we wanted to show like another UI bar on his health bar that would show like a timed spell effect. 

**Jeremy** This is above the character?

**Iris** Yeah, this is above the character and champions already have like health bars and they have mana bars but now we wanted to show like an additional thing and we had to push back and be like, unfortunately, UI is one of the hardest things that we can change in league of legends. And if it's only going to be used by one champion, it's just not worth engineering effort to write something like this.

So I had to convince the designer and the artists and the animator like, we need to think of a different solution to indicate that time to spell, whether it's through VFX or through animation, like I think there's a different way we can address that problem. So the designer had to go back to the drawing board and think about new ways to to solve this problem.

**Jeremy** Yeah, that's, that's really interesting because the assumption that I had and probably many other people do is that you would have a game designer and they would just say like: This is what I want done. Go build it. But you're saying it's actually more of a collaborative process of going back and forth: Hey, this is what I want.
And you saying something like: Well, we could do it, but it's going to take this long. And then there has to be like a negotiation. It sounds like.

**Iris** Yeah, absolutely. It wasn't always that way. I think in the champions world,  engineers were often treated as a service, essentially like a service oriented approach where the designer would literally come with a design and the engineer is just responsible for implementing that. There was no input either way. But now we have moved to the world where we are embedded on the team. Therefore we're there at the beginning of the process. During the champions ideation, we are there and prototyping and trying to like investigate the possibility of tech. And I think we, yeah, we prefer this model honestly. Cause like as engineers like, our time is precious. Like we should like guard against just completely out there requests.  (laughs)

**Jeremy** From the very beginning is everybody kind of getting into a room and sort of starting initial conversations and going from there?

**Iris** Exactly. Yeah. And the earlier we are a part of that process, the better cause. Like, sometimes like we can come up with a tech solution that maybe other people haven't even thought of or thought was possible.

**Jeremy** That's really cool because it, really sounds like it gives you that, connection to these things that are going into the game. The decisions you make you absolutely see in the end product.

**Iris** Yeah, absolutely. I will say the major difference between working on a gameplay team at Riot as compared to a backend team is like, working on a backend team is basically like working at Amazon or working at Microsoft  (laughs). But in, in like a game company. Right. Um, and maybe you lack the tools, but like, it really does feel like you're part of a software team and your decisions are basically, oh, how do I scope these engineering tasks?

Whereas now I would say 55% of my day isn't actually coding anymore. It's actually like talking with designers and artists to figure out like, what is, what is it that you want? Like help me help you achieve what it is that you want. 

**Jeremy** That's really cool. You were talking about how working on backend services was, was very similar to working at Microsoft, working at Amazon.  How is gameplay programming different than the backend web development you were doing?

**Iris** Yeah, it's actually, it's way different.  When you're working with tools now and game code, a lot of it is more dependent on your understanding of 3D math it's not just implemented business logic anymore. You actually have to have a pretty solid understanding of the game, and what is going on in the game otherwise, the business logic will make no sense to you.

And it's so complicated, like you really can't be clueless about how the game works. Otherwise the code would just make no sense to you at all. So that's kind of. I would say the biggest hurdle, but also why the requirement that you must play the game is one that makes sense to me.  And then aside from that, the programming, I will say is pretty wild, wild west.

Like we do try to like follow standards. we use C plus plus across the game engine with a smattering of Lua. we're trying to move away from Lua actually  (laughs) , and convert most of that over to C plus plus.  There are pretty strict standards, with C plus plus, I think, we're debating right now whether we should,  keep using our own proprietary, formatter or the clang formatter, and things like that.

So, there there are way less, I would say, game programmers at Riot than there are like backend services programmers at Riot. Um, so we are a small community, but we're getting there in terms of like setting best practice and standards and things like that.

**Jeremy** It's an interesting contrast from, you know, your time at Microsoft where you said people were really into clean code and these processes and I guess games in general I feel like are probably more loose, I would think.

**Iris** Yeah. It's more about like what can you push the code to do and less about like how does your code look and how is it going to integrate into everything else? Because truthfully, I do a lot of prototyping. A lot of that is throwaway work that's not going to make it into the actual code base of the game itself.

And then, the code base is behind animation, behind VFX, behind graphics and shaders behind, the actual gameplay itself. All of that is so different. There's no way any one person could become an expert in any of these things. So over time, people start to gravitate towards a particular field of expertise.

For me, I think I'm going to gravitate towards graphics cause that's what I love. But, Yeah. There's, there's really no one person who is an expert at gameplay. It's, such a wide variety of things.

**Jeremy** You had worked on some game projects previously, it sounds like the skill sets needed here were, were pretty different. How did you get started, contributing? Like how much did you have to learn and to even just work on your first bug or your first feature?

**Iris** Yeah. Actually, that's interesting because when I applied to this position, I was worried about that. I was worried that I wouldn't be able to contribute as much, but what I actually found was I took to it relatively quickly. Because I had that past experience working on games, but also because at the end of the day, code is code like code kind of works one way and not the other.

So all of my skills, learning how to debug, knowing how to dig around and unfamiliar code base and familiarize yourself with it. Those skills will help in any situation including gameplay. 

**Jeremy** You have a feature, like having an ability that takes away other champions spells, for example. how do you even get started? Like knowing where to look within the code base. If you can't understand everything from the start how do you even get pushed into the right direction? 

**Iris** Yeah, absolutely. So, first you lean on your non-engineering experts people who are familiar with their craft. A lot of the tech designers and tech artists at Riot are fairly technical themselves. And the only thing is they don't have access to the code, but they can read it and then they can point you in the right direction and generally they'll tell you like: Oh, this is related to that system. And you can just like do a search of the code base of that system and you'll probably find that thing that you're looking for. Um, I also work on a team of four other engineers, and so as a team, we were able to help each other with our tasks all the time.

**Jeremy**  At Microsoft for example, you were talking about how there is a big focus on, on testing. How does testing in a gameplay environment work?

**Iris** Yeah, that is very interesting. There are very few tests now, and I think there's more of a reliance on our QA.  But it's a back and forth collaboration. We have a very strong relationship with QA.  Basically, when a champion is designed and has been scripted by the designer, we actually do a process where QA will take the champion at that point and run them through a whole bunch of tests, like manual tests. They actually hire vendors to help them do this, and then they'll serve us up all of the bugs. And so we'll have like a giant list of like bug backlogs and now it's on me as engineer to go through and like try to figure out what's going on in this. So it's actually a very collaborative, multi-disciplinary process for testing.

**Jeremy**  When I think about traditional backend or front end development, if there's a bug, there's the ability to debug, right? To like kind of step through the code.
Um, are you able to also do that with like a running league of legends game?

**Iris** Yes, we absolutely are in, in fact, the tool that designers use to script the, the game logic block builder actually has the ability to step through that thing too, to debug like: Oh, okay, this is the code that is now running. Even though it looks like a drag and drop interface you can still debug through that too. 

**Jeremy** Hmm. So this, block builder, you were saying it's kind of like writing a script and, is that defining like the behavior of, of spells and different actions in the game?

**Iris** That's right

**Jeremy** And they can, they can load those in, without ever having to actually modify source code? That's pretty cool. Do you have like an example of when you would have a bug and what your approach would be to narrowing down how to fix it?

**Iris** Yeah, absolutely. I'll give an example. We are in the process of trying to redo like an existing champion in the game right now. So I've been tasked to like help them fix the bugs before this champion re-releases. So he came back with a bug where he creates like a clone of himself and that clone could do damage to other enemies.

And then the turret for some reason  we have towers in the game that like hit you. And for some reason it wasn't aggroing correctly onto this champion when his clone was doing damage. So somewhere in the logic he was creating a clone. This clone was not affecting the turret logic the way we want it to. So, when I received this bug, the first thing I do is I try to repro it within league of legends. Once I can repro it, I start to put break points on where I think in the code this might affect and I could do it either from script, so I could start with the script. And I did think it was like a scripting thing.

Our scripter our block builder actually allows us to put debug statements into the code, into, the game. So like, when things are happening, like a whole bunch of debug statements, will just start like popping up in the game. and that will tell you like the logic flow of like, what's actually happening.

And you're like, Oh, okay. So this thing happened, this thing. Didn't happen, but it should have happened. Why is that? And then from there you can attach the league of legends client to the process that is running in like your visual studio when you're debugging like C plus plus.

And now you're like taking it to actual game code game engine code and figuring out like, well, what's happening here? And from there, hopefully you can narrow down where in the code in the logic flow. It's breaking down and make the change.

**Jeremy** It sounds like the way you might narrow down something on a front end application, it's just that it happens to be 3D game running at 140 frames a second or whatever.

**Iris** Exactly. Yeah.  (laughs)  obviously all games have this, but league of legends is especially server deterministic, so there's a game server running. There's also a game client running, and sometimes your bug is happening in the server other times it's in the client. But for the most part it's usually the server because league of legends is very server deterministic.

**Jeremy** Right the server has to be the source of truth since it's a multiplayer game.

**Iris** Exactly.

**Jeremy** Do you have a way of sort of setting up, I'm going to have these champions on this team, these champions on this team, and these are the conditions of, know, the currently playing games. So, that you can try and get your, your perfect reproduction scenario?

**Iris** Absolutely. we have this in house tool called launcher, and we can actually launch, multiple instances of the game simulating different players. that's why we need our machines to be quite powerful as we need to make sure we have the memory to be able to do that  (laughs)  because,  a lot of issues actually happen.

Not on the, like, you know, multiple players playing level. But because league is such a complicated game with so many champions, so many items, combinations of whatever, a lot of issues actually happen on the data layer. And so we have a really complicated way of managing data within the game, like what all loaded in, like who are the characters that are playing, like what items do they get and whatever. Like all these things have to be loaded up to the right, data layer. so to speak. And so when content creators like changed stuff, in data future, for example, like that's like the stuff that's going into like future versions of the game.

Or we could like switch layers and say, okay, let's look at what's on release right now. Like what's out there in the, in the world and look at, well, what changed between now and then? Like somebody checked in something into this data layer that like messed everything up. So yeah that's how how we narrow those down.

**Jeremy** Back to the detective story, I guess.

You know, now that you've been working in the industry for a while, and you've kind of seen a lot of different types of  development, a lot of different sizes of companies. you know, in the future, what are going to be the most important things you look for in a role, both technical and culture wise?

**Iris** Yeah, that's a great question. I think that at this stage in my career,  I'm more concerned about culture than I am about, tech stack. Although that is also very important to me as somebody who, likes the visual aspect of programming. I think that as long as that's there it comes down to culture. 

I think about the times where I willingly switched out of a company, like I started actively looking, even though I already had a job, and the only time I did so was mostly because I felt like the culture of the team that I was on was starting to not satisfy me in any way. That's one thing that I do appreciate about Riot is that on both of the teams I was on I was really appreciative of the culture that they have fostered.

And for me, a good culture looks like everybody is very receptive to feedback and there is an open feedback culture and senior engineers and junior engineers, feel comfortable giving each other, open feedback. This is something that was really important to me too.

On my old team, we had these meetings called safety and belonging and basically it sounds like you sit around in a circle and talk about your feelings where really that, that was it. And like that was, that was kind of like the key to sort of, making sure everybody on the team felt comfortable with each other, expressing vulnerabilities.
And we never really talked about work at these meetings. It was always about like each other as humans. And as we talk to each other more and became comfortable with each other as human beings, we noticed that in our work, we just felt more comfortable giving each other the hard feedback of like, Hey, like you're slacking off today. Or like that was a really bad code review. And like some people are just not comfortable with doing that until you get to know someone. Well, that's just human nature.  Um, the fact that we're able to get to that point was like really important to me. Whereas like I contrast it to like my experience at Microsoft where like any sort of feedback had to go through someone's manager and that was like very
oppressive.

**Jeremy** Yeah. that makes a lot of sense because you know, for myself, the most important thing is really the people. Like you can have work that's okay, maybe not the best, but as long as the people are good, then you know, you can still have a good time and it can still be a good experience.

Whereas the opposite, I feel is not true.

**Iris** Yes, definitely. And, I'm very thankful for each manager that I have had at Riot and I mean even at Microsoft, I think I lucked out. I had a really good manager. I think that's also really important is to have a manager that you feel really has your back in everything And is like looking out for your best interest, not their best interests.
 
**Jeremy** These are the kinds of things that I feel like you find out after you join a team. Do you think there's anything that you would look for or ask during the interviewing process or the recruitment process?

**Iris** I think these are things that will come up during their interview process, hopefully, I would look for cultural interviews. Unfortunately I think a lot of tech companies don't even do cultural interviews or if they do it's like a very quick one at the very end to see if you're a culture fit.

And that's always kind of a red flag for me. I always feel like you ought to make sure that the person joining your team will really, really fit. And I liked that Riot put a huge emphasis on cultural fit.  In fact, I think I did just as many cultural interviews as I did tech interviews. That's something that's super important.

At other companies, I feel like I've often just been run through the gamut with tech interviews and at the very end, they leave 20 minutes for you to ask questions about the company. It's like, oh, okay. But if that were the case, I mean, some things I would ask is like, how do you measure your engineers?

Like, what is the performance management look like and how do you know you've done a good job or a bad job? And like, as far as like leadership goes, how do you measure leadership?  How do you measure that they're doing their job effectively?
Cause like how you manage managers is actually very indicative of how like people on the front line are going to be treated as well.

**Jeremy** Definitely. I think it's a good place to start wrapping up, but are there any other, things you thought we should've talked about or I should have asked?

**Iris**  Nope I think that that's great and I'm happy to wrap it up here 

**Jeremy** Cool. And where can people follow you if they want to see what you're up to?

**Iris** On Twitter. My name is @RiotNyanbun

**Jeremy** Iris, thank you so much for chatting with me today.

**Iris**  Yeah. You too, Jeremy. Thank you for your time. 

**Jeremy** I hope you enjoyed the conversation with Iris. Show notes for this episode are at softwaresessions.com. I'll see you next time.

</div>