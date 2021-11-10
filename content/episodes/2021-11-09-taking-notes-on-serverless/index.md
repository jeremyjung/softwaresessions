+++
title = "Taking Notes on Serverless"

description = "Swizec Teller shares his experience with serverless technology, taking notes, and sharing information with his team"

[extra]
episode_url = "https://media.transistor.fm/49cc2fd4/bc911df4.mp3"
+++

Swizec is the author of the Serverless Handbook and a software engineer at Tia.

### Swizec
- [Swizec's personal site](https://swizec.com/)
- [Serverless Handbook](https://serverlesshandbook.dev/)
- [Serverless Framework](https://github.com/serverless/serverless)

### AWS
- [Lambda](https://aws.amazon.com/lambda/)
- [API Gateway](https://aws.amazon.com/api-gateway/)
- [Operating Lambda](https://aws.amazon.com/blogs/compute/operating-lambda-performance-optimization-part-1/) (The cold start problem)
- [Provisioned Concurrency](https://aws.amazon.com/blogs/compute/new-for-aws-lambda-predictable-start-up-times-with-provisioned-concurrency/)
- [DynamoDB](https://aws.amazon.com/dynamodb/)
- [Relational Database Service](https://aws.amazon.com/rds/)
- [Aurora](https://aws.amazon.com/rds/aurora)
- [Simple Queue Service](https://aws.amazon.com/sqs/)
- [CloudFormation](https://aws.amazon.com/cloudformation/)
- [CloudWatch](https://aws.amazon.com/cloudwatch/)

### Other serverless function providers
- [Gatsby Cloud Functions](https://www.gatsbyjs.com/products/cloud/functions/)
- [Vercel Serverless Functions](https://vercel.com/docs/concepts/functions/serverless-functions)
- [Netlify Functions](https://www.netlify.com/products/functions/)
- [Cloud Functions for Firebase](https://firebase.google.com/docs/functions)

### Related topics
- [Jamstack](https://jamstack.org/)
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)
- [What is a Static Site Generator?](https://www.netlify.com/blog/2020/04/14/what-is-a-static-site-generator-and-3-ways-to-find-the-best-one/)
- [What is a CDN?](https://www.cloudflare.com/learning/cdn/what-is-a-cdn/)
- [Keeping Server-Side Rendering Cool With React Hydration](https://aboutmonica.com/blog/server-side-rendering-react-hydration-best-practices)
- [TypeScript](https://www.typescriptlang.org/)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** Today, I'm talking to Swiz Teller. He's a senior software engineer at Tia. The author of the serverless handbook and he's also got a bunch of other courses and I don't know is it thousands of blog posts now you have a lot of them.

[00:00:13] **Swizec:** It is actually thousands of, uh, it's like 1500. So I don't know if that's exactly thousands, but it's over a thousand.

I'm cheating a little bit. Cause I started in high school back when blogs were still considered social media and then I just kind of kept going on the same domain.

Do you have some kind of process where you're, you're always thinking of what to write next? Or are you writing things down while you're working at your job? Things like that. I'm just curious how you come up with that. 

[00:00:41] **Swizec:** So I'm one of those people who likes to use writing as a way to process things and to learn. So one of the best ways I found to learn something new is to kind of learn it and then figure out how to explain it to other people and through explaining it, you really, you really spot, oh shit. I don't actually understand that part at all, because if I understood it, I would be able to explain it.

And it's also really good as a reference for later. So some, one of my favorite things to do is to spot a problem at work and be like, oh, Hey, this is similar to that side project. I did once for a weekend experiment I did, and I wrote about it so we can kind of crib off of my method and now use it. So we don't have to figure things out from scratch.

And part of it is like you said, that just always thinking about what I can write next. I like to keep a schedule. So I keep myself to posting two articles per week. It used to be every day, but I got too busy for that. when you have that schedule and, you know, okay on Tuesday morning, I'm going to sit down and I have an hour or two hours to write, whatever is on top of mind, you kind of start spotting more and more of these opportunities where it's like a coworker asked me something and I explained it in a slack thread and it, we had an hour. Maybe not an hour, but half an hour of back and forth. And you actually just wrote like three or 400 words to explain something. If you take those 400 words and just polish them up a little bit, or rephrase them a different way so that they're easier to understand for somebody who is not your coworker, Hey, that's a blog post and you can post it on your blog and it might help others.

[00:02:29] **Jeremy:** It sounds like taking the conversations most people have in their day to day. And writing that down in a more formal way. 

[00:02:37] **Swizec:** Yeah. not even maybe in a more formal way, but more, more about in a way that a broader audience can appreciate. if it's, I'm super gnarly, detailed, deep in our infrastructure in our stack, I would have to explain so much of the stuff around it for anyone to even understand that it's useless, but you often get these nuggets where, oh, this is actually a really good insight that I can share with others and then others can learn from it. I can learn from it. 

[00:03:09] **Jeremy:** What's the most accessible way or the way that I can share this information with the most people who don't have all this context that I have from working in this place. 

[00:03:21] **Swizec:** Exactly. And then the power move, if you're a bit of an asshole is to, instead of answering your coworkers question is to think about the answer, write a blog post and then share the link with them.

I think that's pushing it a little bit.

[00:03:38] **Jeremy:** Yeah, It's like you're being helpful, but it also feels a little bit passive aggressive.

[00:03:44] **Swizec:** Exactly. Although that's a really good way to write documentation. One thing I've noticed at work is if people keep asking me the same questions, I try to stop writing my replies in slack and instead put it on confluence or whatever internal wiki that we have, and then share that link. and that has always been super appreciated by everyone.

[00:04:09] **Jeremy:** I think it's easy to, have that reply in slack and, and solve that problem right then. But when you're creating these Wiki pages or these documents, how're people generally finding these. Cause I know you can go through all this trouble to make this document. And then people just don't know to look or where to go. 

[00:04:30] **Swizec:** Yeah. Discoverability is a really big problem, especially what happens with a lot of internal documentation is that it's kind of this wasteland of good ideas that doesn't get updated and nobody maintains. So people stop even looking at it. And then if you've stopped looking at it before, stop updating it, people stop contributing and it kind of just falls apart.

And the other problem that often happens is that you start writing this documentation in a vacuum. So there's no audience for it, so it's not help. So it's not helpful. That's why I like the slack first approach where you first answered the question is. And now, you know exactly what you're answering and exactly who the audiences.

And then you can even just copy paste from slack, put it in a conf in JIRA board or wherever you put these things. spice it up a little, maybe effect some punctuation. And then next time when somebody asks you the same question, you can be like, oh, Hey, I remember where that is. Go find the link and share it with them and kind of also trains people to start looking at the wiki.

I don't know, maybe it's just the way my brain works, but I'm really bad at remembering information, but I'm really good at remembering how to find it. Like my brain works like a huge reference network and it's very easy for me to remember, oh, I wrote that down and it's over there even if I don't remember the answer, I almost always remember where I wrote it down if I wrote it down, whereas in slack it just kind of gets lost.

[00:06:07] **Jeremy:** Do you also take more informal notes? Like, do you have notes locally? You look through or something? That's not a straight up Wiki. 

[00:06:15] **Swizec:** I'm actually really bad at that. I, one of the things I do is that when I'm coding, I write down. so I have almost like an engineering log book where everything, I, almost everything I think about, uh, problems I'm working on. I'm always writing them down on by hand, on a piece of paper. And then I never look at those notes again.

And it's almost like it helps me think it helps me organize my thoughts. 

And I find that I'm really bad at actually referencing my notes and reading them later because, and this again is probably a quirk of my brain, but I've always been like this. Once I write it down, I rarely have to look at it again.

But if I don't write it down, I immediately forget what it is.

What I do really like doing is writing down SOPs. So if I notice that I keep doing something repeatedly, I write a, uh, standard operating procedure. For my personal life and for work as well, I have a huge, oh, it's not that huge, but I have a repository of standard procedures where, okay, I need to do X.

So you pull up the right recipe and you just follow the recipe. And if you spot a bug in the recipe, you fix the recipe. And then once you have that polished, it's really easy to turn that into an automated process that can do it for you, or even outsource it to somebody else who can work. So we did, you don't have to keep doing the same stuff and figuring out, figuring it out from scratch every time.

[00:07:55] **Jeremy:** And these standard operating procedures, they sound a little bit like runbooks I guess. 

[00:08:01] **Swizec:** Yep. Run books or I think in DevOps, I think the big red book or the red binder where you take it out and you're like, we're having this emergency, this alert is firing. Here are the next steps of what we have to check.

[00:08:15] **Jeremy:** So for those kinds of things, those are more for incidents and things like that. But in your case, it sounds like it's more, uh, I need to get started with the next JS project, or I need to set up a Postgres database things like that. 

[00:08:30] **Swizec:** Yeah. Or I need to reset a user to initial states for testing or create a new user. That's sort of thing.

[00:08:39] **Jeremy:** These probably aren't in that handwritten log book.

[00:08:44] **Swizec:** The wiki. That's also really good way to share them with new engineers who are coming on to the team.

[00:08:50] **Jeremy:** Is it where you just basically dump them all on one page or is it where you, you organize them somehow so that people know that this is where, where they need to go. 

[00:09:00] **Swizec:** I like to keep a pretty flat structure because, I think the, the idea of categorization outlived its prime. We have really good search algorithms now and really good fuzzy searching. So it's almost easier if everything is just dumped and it's designed to be easy to search. a really interesting anecdote from, I think they were they were professors at some school and they realized that they try to organize everything into four files and folders.

And they're trying to explain this to their younger students, people who are in their early twenties and the young students just couldn't understand. Why would you put anything in a folder? Like what is a folder? What is why? You just dump everything on your desktop and then command F and you find it. Why would you, why would you even worry about what the file name is? Where the file is? Like, who cares? It's there somewhere.

[00:09:58] **Jeremy:** Yeah, I think I saw the same article. I think it was on the verge, right?

I mean, I think that's that's right, because when you're using, say a Mac and you don't go look for the application or the document you want to run a lot of times you open up spotlight and just type it and it comes up.

Though, I think what's also sort of interesting is, uh, at least in the note taking space, there's a lot of people who like setting up things like tags and things like that. And in a way that feels a lot like folders, I guess 

[00:10:35] **Swizec:** Yeah. The difference between tags and categories is that the same file can have multiple tags and it cannot be in multiple folders. So that's why categorization systems usually fall apart. You mentioned note taking systems and my opinion on those has always been that it's very easy to fall into the trap of feeling productive because you are working on your note or productivity system, but you're not actually achieving anything.

You're just creating work for work sake. I try to keep everything as simple as possible and kind of avoid the overhead.

[00:11:15] **Jeremy:** People can definitely spend hours upon hours curating what's my note taking system going to be, the same way that you can try to set up your blog for two weeks and not write any articles. 

[00:11:31] **Swizec:** Yeah. exactly.

[00:11:32] **Jeremy:** When I take notes, a lot of times I'll just create a new note in apple notes or in a markdown file and I'll just write stuff, but it ends up being very similar to what you described with your, your log book in that, like, because it's, it's not really organized in any way. Um, it can be tricky to go back and actually, find useful information though, Though, I suppose the main difference though, is that when it is digital, uh, sometimes if I search for a specific, uh, software application or a specific tool, then at least I can find, um, those bits there 

[00:12:12] **Swizec:** Yeah. That's true. the other approach I'd like to use is called the good shit stays. So if I can't remember it, it probably wasn't important enough. And you can, especially these days with the internet, when it comes to details and facts, you can always find them. I find that it's pretty easy to find facts as long as you can remember some sort of reference to it.

[00:12:38] **Jeremy:** You can find specific errors or like you say specific facts, but I think if you haven't been working with a specific technology or in a specific domain for a certain amount of time, you, it, it can be hard to, to find like the right thing to look for, or to even know if the solution you're looking at is, is the right one. 

[00:13:07] **Swizec:** That is very true. Yeah. Yeah, I don't really have a solution for that one other than relearn it again. And it's usually faster the second time. But if you had notes, you would still have to reread the notes. Anyway, I guess that's a little faster, cause it's customized to you personally.

[00:13:26] **Jeremy:** Where it's helpful is that sometimes when you're looking online, you have to jump through a bunch of different sites to kind of get all the information together. And by that time you've, you've lost your flow a little bit, or you you've lost, kind of what you were working on, uh, to begin with. Yeah. 

[00:13:45] **Swizec:** Yeah. That definitely happens.

[00:13:47] **Jeremy:** Next I'd like to talk about the serverless handbook. Something that you've talked about publicly a little bit is that when you try to work on something, you don't think it's a great idea to just go look at a bunch of blog posts. Um, you think it's better to, to go to a book or some kind of more, uh, I don't know what you would call it like larger or authoritative resource. And I wonder what the process was for, for you. Like when you decided I'm going to go learn how to do serverless you know, what was your process for doing that? 

[00:14:23] **Swizec:** Yeah. When I started learning serverless, I noticed that maybe I just wasn't good at finding them. That's one thing I've noticed with Google is that when you're jumping into a new technical. It's often hard to find stuff because you don't really know what you're searching for. And Google also likes to tune the algorithms to you personally a little bit.

So it can be hard to find what you want if you are, if you haven't been in that space. So I couldn't really find a lot of good resources, uh, which resulted in me doing a lot of exploration, essentially from scratch or piecing together different blogs and scraps of information here and there. I know that I spend ridiculous amounts of time in even as deep as GitHub issues on closed issues that came up in Google and answer something or figure, or people were figuring out how something works and then kind of piecing all of that together and doing a lot of kind of manual banging my head against the wall until the wall broke.

And I got through. I decided after all of that, that I really liked serverless as a technology. And I really think it's the future of how backend systems are going to be built. I think it's unclear yet. What kind of systems is appropriate for and what kind of kind of systems it isn't.

It does have pros and cons. it does resolve a lot of the very annoying parts of building a modern website or building upon backend go away when you go serverless. So I figured I really liked this and I've learned a lot trying to piece it together over a couple of years.

And if combined, I felt like I was able to do that because I had previous experience with building full stack websites, building full stack apps and understanding how backends work in general. So it wasn't like, oh, How do I do this from scratch? It was more okay. I know how this is supposed to work in theory.

And I understand the principles. What are the new things that I have to add to that to figure out serverless? So I wrote the serverless handbook basically as a, as a reference or as a resource that I wish I had when I started learning this stuff. It gives you a lot of the background of just how backends work in general, how databases connect, what different databases are, how they're, how they work.

Then I talked some, some about distributed systems because that comes up surprisingly quickly when you're going with serverless approaches, because everything is a lot more distributed. And it talks about infrastructure as code because that kind of simplifies a lot of the, they have opposite parts of the process and then talks about how you can piece it together in the ends to get a full product. and I approached it from the perspective of, I didn't want to write a tutorial that teaches you how to do something specific from start to finish, because I personally don't find those to be super useful. Um, they're great for getting started. They're great for building stuff. If you're building something, that's exactly the same as the tutorial you found.

But they don't help you really understand how it works. It's kind of like if you just learn how to cook risotto, you know how to cook risotto, but nobody told you that, Hey, you actually, now that you know how to cook risotto, you also know how to just make rice and peas. It's pretty much the same process.

Uh, and if you don't have that understanding, it's very hard to then transition between technologies and it's hard to apply them to your specific situation. So I try to avoid that and write more from the perspective. How I can give somebody who knows JavaScript who's a front end engineer, or just a JavaScript developer, how I can give them enough to really understand how serverless and backends works and be able to apply those approaches to any project.

[00:18:29] **Jeremy:** When people hear serverless, a lot of times they're not really sure what that actually means. I think a lot of times people think about Lambdas, they think about functions as a service. but I wonder to you what does serverless mean? 

[00:18:45] **Swizec:** It's not that there's no server, there's almost always some server somewhere. There has to be a machine that actually runs your code. The idea of serverless is that the machine and the system that handles that stuff is trans is invisible to you. You're offloading all of the dev ops work to somebody else so that you can full focus on the business problems that you're trying to solve.

You can focus on the stuff that is specific and unique to your situation because, you know, there's a million different ways to set up a server that runs on a machine somewhere and answers, a, API requests with adjacent. And some people have done that. Thousands of times, new people, new folks have probably never done it.

And honestly, it's really boring, very brittle and kind of annoying, frustrating work that I personally never liked. So with serverless, you can kind of hand that off to a whole team of engineers at AWS or at Google or, whatever other providers there are, and they can deal with that stuff. And you can, you can work on the level of, I have this JavaScript function.

I want this JavaScript function to run when somebody hits this URL and that's it. That's all, that's essentially all you have to think about. So that's what serverless means to me. It's essentially a cloud functions, I guess.

[00:20:12] **Jeremy:** I mean, there been services like Heroku, for example, that, that have let people make rails apps or Django apps and things like that, where the user doesn't really have to think about the operating system, um, or about creating databases and things like that. And I wonder, to you, if, if that is serverless or if that's something different and, and what the difference there might be. 

[00:20:37] **Swizec:** I think of that as an intermediary step between on prem or handling your own servers and full serverless, because you still have to think about provisioning. You still have to think of your server as a whole blob or a whole glob of things that runs together and runs somewhere and lives or lifts somewhere.

You have to provision capacity. You have to still think about how many servers you have on Heroku. They're called dynos. you still have to deal with the routing. You have to deal with connecting it to the database. Uh, you always have to think about that a little bit, but you're, you're still dealing with a lot of the frameworky stuff where you have to, okay, I'm going to declare a route. And then once I've declared the route, I'm going to tell it how to take data from the, from the request, put it to the function. That's actually doing the work. And then you're still dealing with all of that. Whereas with full serverless, first of all, it can scale down to zero, which is really useful.

If you don't have a lot of traffic, you can have, you're not paying anything unless somebody is actually using your app. The other thing is that you don't deal with any of the routing or any of that. You're just saying, I want this URL to exist, and I want it to run that function, that you don't deal with anything more than that.

And then you just write, the actual function that's doing the work. So it ends up being as a normal jobs function that accepts a request as an argument and returns a JSON response, or even just a JSON object and the serverless machinery handles everything else, which I personally find a lot easier. And you don't have to have these, what I call JSON bureaucracy, where you're piping an object through a bunch of different functions to get from the request to the actual part that's doing the work. You're just doing the core interesting work.

[00:22:40] **Jeremy:** Sort of sounds like one of the big distinctions is with something like Heroku or something similar. You may not have a server, but you have the dyno, which is basically a server. You have something that is consistently running, 

Whereas with what you consider to be serverless, it's, it's something that basically only launches on when it's invoked. Um, whether that's a API call or, or something else. The, the routing thing is a little bit interesting because the, when I was going through the course, there are still the routes that you write. It's just that you're telling, I guess the API gateway Amazon's API gateway, how to route to your functions, which was very similar to how to route to a controller action or something like that in other languages.

[00:23:37] **Swizec:** Yeah. I think that part is actually is pretty similar where, I think it kind of depends on what kind of framework you end up building. Yeah, it can be very simple. I know with rails, it's relatively simple to define a new route. I think you have to touch three or four different files. I've also worked in large express apps where.

Hooking up the controller with all of the swagger definitions or open API definitions, and everything else ends up being like six or seven different files that have to have functions that are named just right. And you have to copy paste it around. And I, I find that to be kind of a waste of effort, with the serverless framework.

What I like is you have this YAML file and you say, this route is handled by this function. And then the rest happens on its own with next JS or with Gatsby functions, Gatsby cloud functions. They've gone even a step further, which I really like. You have the slash API directory in your project and you just pop a file in there.

And whatever that file is named, that becomes your API route and you don't even have to configure anything. You're just, in both of them, if you put a JavaScript file in slash API called hello, That exports, a handler function that is automatically a route and everything else happens behind the scenes.

[00:25:05] **Jeremy:** So that that's more of a matter of the framework you're using and how easy does it make it to, to handle routing? Whether that's a pain or a not.

[00:25:15] **Swizec:** Yeah. and I think with the serverless frameworks, it's because serverless itself, as a concept makes it easier to set this up. We've been able to have these modern frameworks with really good developer experience Gatsby now with how did they have Gatsby cloud and NextJS with Vercel and I think Netlify is working on it as well.

They can have this really good integration between really tight coupling and tight integration between a web framework and the deployment environment, because serverless is enabling them to spin that up. So easily.

[00:25:53] **Jeremy:** One of the things about your courses, this isn't the only thing you focus on, but one of the use cases is basically replacing a traditional server rendered application or a traditional rails, django, spring application, where you've got Amazon's API gateway in front, which is serving as the load balancer.

And then you have your Lambda functions, which are basically what would be a controller action in a lot of frameworks. and then you're hooking it up to a database which could be Amazon. It could be any database, I suppose. And I wonder in your experience having worked with serverless at your job or in side projects, whether that's like something you would use as a default or whether serverless is more for background jobs and things like that.

[00:26:51] **Swizec:** I think the underlying hidden question you're asking is about cold starts and API, and the response times, is one of the concerns that people have with serverless is that if your app is not used a lot, your servers scale down to zero. So then when somebody new comes on, it can take a really long time to respond.

And they're going to bail and be upset with you. One way that I've solved, that is using kind of a more JAM Stacky approach. I feel like that buzzword is still kind of in flux, but the idea is that the actual app front-end app, the client app is running off of CDNs and doesn't even touch your servers.

So that first load is of the entire app and of the entire client system is really fast because it comes from a CDN that's running somewhere as close as possible to the user. And it's only the actual APIs are hitting your server. So in the, for example, if you have something like a blog, you can, most blogs are pretty static.

Most of the content is very static. I use that on my blog as well. you can pre-render that when you're deploying the project. So you, you kind of, pre-render everything that's static when you deploy. And then it becomes just static files that are served from the CDN. So you get the initial article. I think if you, I haven't tested in a while, but I think if you load one of my articles on swizec.com, it's readable, like on lighthouse reports, if you look at the lighthouse where it gives you the series of screenshots, the first screenshot is already fully readable.

I think that means it's probably under 30 or 40 milliseconds to get the content and start reading, but then, then it rehydrates and becomes a react app. and then when it's a react app, it can make for their API calls to the backend. So usually on user interaction, like if you have upvotes or comments or something like that, Only when the user clicks something, you then make an API call to your server, and that then calls a Lambda or Gatsby function or a Netlify cloud function, or even a Firebase function, which then then wakes up and talks to the database and does things, and usually people are a lot more forgiving of that one taking 50 milliseconds to respond instead of 10 milliseconds, but, you know, 50 milliseconds is still pretty good.

And I think there were recently some experiments shared where they were comparing cold start times. And if you write your, uh, cloud functions in JavaScript, the average cold startup time is something like a hundred milliseconds. And a big part of that is because you're not wrapping this entire framework, like express or rails into your function. It's just a small function. So the server only has to load up something like, I don't know. I think my biggest cloud functions have been maybe 10 kilobytes with all of the dependencies and everything bundled in, and that's pretty fast for a server to, to load run, start no JS and start serving your request.

It's way fast enough. And then if you need even more speed, you can go to rust or go, which are even faster. As long as you avoid the java, .net, C-sharp those kinds of things. It's usually fine.

[00:30:36] **Jeremy:** One of the reasons I was curious is because I was going through the rest example you've got, where it's basically going through Amazon's API gateway, um, goes to a Lambda function written in JavaScript, and then talks to dynamoDB gives you a record back or creates a record and, I, I found that just making those calls, making a few calls, hopefully to account for the cold start I getting response times of maybe 150 to 250 milliseconds, which is not terrible, but, it's also not what I would call fast either.

So I was just kind of curious, when you have a real app, like, are, are there things that you've come across where Lambda maybe might have some issues or at least there's tricks you need to do to, to work around them? 

[00:31:27] **Swizec:** Yeah. So the big problem there is, as soon as a database is involved, that tends to get. Especially if that database is not co-located with your Lambda. So it's usually, or when I've experimented, it was a really bad idea to go from a Vercel API function, talk to dynamo DB in AWS that goes over the open internet.

And it becomes really slow very quickly. at my previous job, I experimented with serverless and connecting it to RDS. If you have RDS in a separate private network, then RDS is that they, the Postgres database service they have, if that's running in a separate private network, then your functions, it immediately adds 200 or 300 milliseconds to your response times.

If you keep them together, it usually works a lot faster. ANd then there are ways to keeping them. Pre-warned usually it doesn't work as well as you would want. There are ways on AWS to, I forget what it's called right now, but they have now what's, some, some sort of automatic rewarming, if you really need response times that are smaller than a hundred, 200 milliseconds.

But yeah, it mostly depends on what you're doing. As soon as you're making API calls or database calls. You're essentially talking to a different server that is going to be slower on a lambda then it is if you have a packaged pserver, that's running the database and the server itself on the same machine.

[00:33:11] **Jeremy:** And are there any specific challenges related to say you mentioned RDS earlier? I know with some databases, like for example, Postgres sometimes, uh, when you have a traditional server application, the server will pool the connections. So it'll make some connection into your data database and just keep reusing them.

Whereas with the Lambda is it making a new connection every time? 

[00:33:41] **Swizec:** Almost. So Lambdas. I think you can configure how long it stays warm, but what AWS tries to do is reuse your laptops. So when the Lambda wakes up, it doesn't die immediately. After that initial request, it stays, it stays alive for the next, let's say it's one minute. Or even if it's 10 minutes, it's, there's a life for the next couple of minutes.

And during that time, it can accept new requests, new requests and serve them. So anything that you put in the global namespace of your phone. We'll potentially remain alive between functions and you can use that to build a connection pool to your database so that you can reuse the connections instead of having to open new connections every time.

What you have to be careful with is that if you get simultaneous requests at actually simultaneous requests, not like 10 requests in 10 milliseconds, if you get 10 requests at the same millisecond, you're going to wake up multiple Lambdas and you're going to have multiple connection pools running in parallel.

So it's very easy to crash your RDS server with something like AWS Lambda, because I think the default concurrency limit is a thousand Lambdas. And if each of those can have a pool of, let's say 10 requests, that's 10,000 open requests or your RDS server. And. You were probably not paying for high enough tier for the RDS server to survive that that's where it gets really tricky.

I think AWS now has a service that lets you kind of offload a connection pool so that you can take your Lambda and connect it to the connection pool. And the connection pool is keeping warm connections to your server. but an even better approach is to use something like Aurora DB, which is also an on AWS or dynamo DB, which are designed from the ground up to work with serverless applications.

[00:35:47] **Jeremy:** It's things that work, but you have to know sort of the little, uh, gotchas, I guess, that are out there. 

[00:35:54] **Swizec:** Yeah, exactly. There's sharp edges to be found everywhere. part of that is also that. serverless, isn't that old yet I think AWS Lambda launched in 2014 or 2015, which is one forever in internet time, but it's still not that long ago. So we're still figuring out how to make things better.

And, it's also where, where you mentioned earlier that whether it's more appropriate for backend processes or for user-facing processes, it does work really well for backend processes because you CA you have better control over the maximum number of Lambdas that run, and you have more patience for them being slow, being slow sometimes. And so on.

[00:36:41] **Jeremy:** It sounds like even for front end processes as long as you know, like you said, the sharp edges and you could do things like putting a CDN in front where your Lambdas don't even get hit until some later time. 

There's a lot of things you can do to make it where it is a good choice or a good I guess what you're saying, when you're building an application, do you default to using a serverless type of stack? 

[00:37:14] **Swizec:** Yes, for all of my side projects, I default to using serverless. Um, I have a bunch of apps running that way, even when serverless is just no servers at all. Like my blog doesn't have any cloud functions right now. It's all running from CDNs, basically. I think the only, I don't know if you could even count that as a cloud function is w my email signup forms go to an API with my email provider.

So there's also not, I don't have any servers there. It's directly from the front end. I would totally recommend it if you are a startup that just got tens of millions of dollars in funding, and you are planning to have a million requests per second by tomorrow, then maybe not. That's going to be very expensive very quickly.

But there's always a trade off. I think that with serverless, it's a lot easier to build in terms of dev ops and in terms of handling your infrastructure, it's, it takes a bit of a mind shift in how you're building when it comes to the actual logic and the actual, the server system that you're building.

And then in terms of costs, it really depends on what you're doing. If you're a super huge company, it probably doesn't make sense to go and serverless, but if you're that. Or if you have that much traffic, you hopefully are also making enough money to essentially build your own serverless system for yourself.

[00:38:48] **Jeremy:** For someone who's interested in trying serverless, like I know for myself when I was going through the tutorial you're using the serverless framework and it creates all these different things in AWS for you and at a high level I could follow. Okay. You know, it has the API gateway and you've got your simple queue service and DynamoDB, and the lambdas all that sort of thing.

So at a high level, I could follow along. But when I log into the AWS console, not knowing a whole lot about AWS, it's creating a ton of stuff for you. 

And I'm wondering from your perspective for somebody who's learning about serverless, how much do they need to really dive into the AWS internals and understand what's going on there. 

[00:39:41] **Swizec:** That's a tough one because personally I try to stay away as much as possible. And especially with the serverless framework, what I like is configuring everything through the framework rather than doing it manually. Um, because there's a lot of sharp edges there as well. Where if you go in and you manually change something, then AWS can't allow serverless framework to clean up anymore and you can have ghost processes running.

At Tia, we've had that as a really interesting challenge. We're not using serverless framework, we're using something called cloud formation, which is essentially. 

One lower level of abstraction, then serverless framework, we're doing a lot more work. We're creating a lot more work for ourselves, but that's what we have. And that's what we're working with. these decisions predate me. So I'm just going along with what we have and we wanted to have more control, because again, we have dev ops people on the team and they want more control because they also know what they're doing and we keep having trouble with, oh, we were trying to use infrastructure as code, but then there's this little part where you do have to go into the AWS console and click around a million times to find the right thing and click it.

And we've had interesting issues with hanging deploys where something gets stuck on the AWS side and we can take it back. We can tear it down, we can stop it. And it's just a hanging process and you have to wait like seven hours for AWS to do. Oh, okay. Yeah. If it's been there for seven hours, it's probably not needed and then kills it and then you can deploy.

So that kind of stuff gets really frustrating very quickly.

[00:41:27] **Jeremy:** Sounds like maybe in your personal projects, you've been able to, to stick to the serverless framework abstraction and not necessarily have to understand or dive into the details of AWS and it's worked out okay for you. 

[00:41:43] **Swizec:** Yeah, exactly. it's useful to know from a high, from a high level what's there and what the different parts are doing, but I would not recommend configuring them through the, through the AWS console because then you're going to always be in the, in the AWS console. And it's very easy to get something slightly wrong.

[00:42:04] **Jeremy:** Yeah. I mean, I know for myself just going through the handbook, just going into the console and finding out where I could look at my logs or, um, what was actually running in AWS. It wasn't that straightforward. So, even knowing the bare minimum for somebody who's new to, it was like a little daunting. 

[00:42:26] **Swizec:** Yeah, it's super daunting. And they have thousands, if not hundreds of different products on AWS. and when it comes to, like you mentioned logs, I, I don't think I put this in the handbook because I either didn't know about it yet, or it wasn't available quite yet, but serverless can all the serverless framework also let you look at logs through the servers framework.

So you can say SLS function, name, logs, and it shows you the latest logs. it also lets you run functions locally to an extent. it's really useful from that perspective. And I personally find the AWS console super daunting as well. So I try to stay away as much as possible.

[00:43:13] **Jeremy:** It's pretty wild when you first log in and you click the button that shows you the services and it's covering your whole screen. Right. And you're like, I just want to see what I just pushed. 

[00:43:24] **Swizec:** Yeah, exactly. And there's so many different ones and they're all they have these obscure names that I don't find meaningful at all.

[00:43:34] **Jeremy:** I think another thing that I found a little bit challenging was that when I develop applications, I'm used to having the feedback cycle of writing the code, running the application or running a test and seeing like, did it work? And if it didn't, what's the stack trace, what, what happened? And I found the process of going into CloudWatch and looking at the logs and waiting for them to eventually refresh and all that to be, a little challenging. And, and, um, so I was wondering in your, your experience, um, how you've worked through, you know, how are you able to get a fast feedback loop or is this just kind of just part of it. 

[00:44:21] **Swizec:** I am very lazy when it comes to writing tests, or when it comes to fast feedback loops. I like having them I'm really bad at actually setting them up. But what I found works pretty well for serverless is first of all, if you write your backend a or if you write your cloud functions in TypeScript that immediately resolves most of the most common issues, most common sources of bugs, it makes sure that you're not using something that doesn't exist.

Make sure you're not making typos, make sure you're not holding a function wrong, which I personally find very helpful because I have pretty fast and I make typos. And it's so nice to be able to say, if it's completely. I know that it's at least going to run. I'm not going to have some stupid issue of a missing semi-colon or some weird fiddly detail.

So that's already a super fast feedback cycle that runs right in your IDE the next step is because you're just writing the business logic function and you know, that the function itself is going to run. You can write unit tests that treat that function as a normal function. I'm personally really bad at writing those unit tests, but they can really speed up the, the actual process of testing because you can go and you can be like, okay.

So I know that the code is doing what I want it to be doing if it's running in isolation. And that, that can be pretty fast. The next step that is, uh, Another level in abstraction and and gives you more feedback is with serverless. You can locally invoke most Lambdas. The problem with locally running your Lambdas is that it's not the same environment as on AWS.

And I asked one of the original developers of the same serverless framework, and he said, just forget about accurately replicating AWS on your system. There are so many dragons there it's never going to work. and I had an interesting example about that when I was building a little project for my girlfriend that sends her photos from our relationship to an IOT device every day or something like that.

It worked when I ran SLS invoke and it ran and it even called all of the APIs and everything worked. It was amazing. And then when I deployed it, it didn't work and it turned out that it was a permissions issue. I forgot to give myself a specific, I am role for something to work. That's kind of like a stair-stepping process of having fast feedback cycles first, if it compiles, that means that you're not doing anything absolutely wrong.

If the tests are running, that means it's at least doing what you think it's doing. If it's invoking locally, it means that you're holding the API APIs and the third-party stuff correctly. And then the last step is deploying it to AWS and actually running it with a curl or some sort of request and seeing if it works in production.

And that then tells you if it's actually going to work with AWS. And the nice thing there is because uh serverless framework does this. I think it does a sort of incremental deploys. The, that cycle is pretty fast. You're not waiting half an hour for your C code pipeline or for your CIO to run an integration test, to do stuff.

One minute, it takes one minute and it's up and you can call it and you immediately see if it's working.

[00:47:58] **Jeremy:** Basically you're, you're trying to do everything you can. Static typing and, running tests just on the functions. But I guess when it comes down to it, you really do have to push everything, update AWS, have it all run, um, in order to, to really know. Um, and so I guess it's, it's sort of a trade-off right. Versus being able to, if you're writing a rails application and you've got all your dependencies on your machine, um, you can spin it up and you don't really have to wait for it to, to push anywhere, but, 

[00:48:36] **Swizec:** Yeah. But you still don't know if, what if your database is misconfigured in production?

[00:48:42] **Jeremy:** right, right. So it's, it's never, never the same as 

production. It's just closer. Right? Yeah. Yeah, I totally get When you don't have the real services or the real databases, then there's always going to be stuff that you can miss. Yeah, 

[00:49:00] **Swizec:** Yeah. it's not working until it's working in production.

[00:49:03] **Jeremy:** That's a good place to end it on, but is there anything else you want to mention before we go?

[00:49:10] **Swizec:** No, I think that's good. Uh, I think we talked about a lot of really interesting stuff.

[00:49:16] **Jeremy:** Cool. Well, Swiz, thank you so much for chatting with me today. 

[00:49:19] **Swizec:** Yeah. Thank you for having me.

</div>