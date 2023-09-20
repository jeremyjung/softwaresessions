+++
title = "Daniel Zingaro and Leo Porter on learning to program with LLMs"

description = "CS professors discuss how teaching and assessing students will change"

[extra]
episode_url = "https://pinecast.com/listen/3e9982f1-eb95-40e8-a6b0-410c3b14de9c.mp3"
social_title = "Daniel Zingaro and Leo Porter on learning to program with LLMs"
social_description = "CS professors discuss how teaching and assessing students will change"
+++

Dr. Daniel Zingaro and Dr. Leo Porter are co-authors of the book [Learn AI-Assisted Python Programming](https://www.manning.com/books/learn-ai-assisted-python-programming).

Leo will teach an introductory computer science course this quarter at UCSD using this book. We discuss how tools like GitHub Copilot let people new to programming focus on breaking down problems instead of language syntax.

Dr. Zingaro is an Associate Professor of Computer Science at University of Toronto Mississauga and Dr. Porter is an Associate Professor at University of California San Diego.

This episode was originally posted on Software Engineering Radio.

### Topics covered:

- Making programming more accessible
- Teaching problem decomposition instead of language syntax
- The importance of reading and testing untrusted generated code
- The rise of throwaway or one-off code
- Concerns about relying on commercial tools
- Rethinking how to assess students

### Related Links

- [Learn AI-Assisted Python Programming](https://www.manning.com/books/learn-ai-assisted-python-programming)
- [Leo Porter](https://leoporter.ucsd.edu/)
- [Daniel Zingaro](https://www.danielzingaro.com/)
- [GitHub Copilot](https://github.com/features/copilot)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

Note the timestamps and audio for this transcript will not completely match.

## Intro

[00:00:00] **Jeremy:** Today I'm talking to Dr. Leo Porter. He's an associate teaching professor of computer science at the University of California San Diego, and he co-founded the computing education research laboratory there.

I'm also joined by Dr. Daniel Zingaro who is an associate teaching professor of computer science at the University of Toronto. And he's also the author of the book, learn to Code by Solving Problems and the Book, Algorithmic Thinking. They are co-authors of the book, learn AI Assisted Python programming.

Leo and Dan, welcome to Software Engineering Radio.

[00:00:37] **Leo:** Thank you for having us, Jeremy. I really appreciate your podcast, so thanks. Great to be here.

[00:00:41] **Dan:** Thanks Jeremy.

## Writing a book for Leo's CS1 class

[00:00:43] **Jeremy:** The first thing we could start with is, is why this book? And, and why now? How did you decide on like, okay, this is the thing we need to do now.

[00:00:51] **Leo:** So, uh, this is Dan. Uh, so Dan, um, like really early when LLMs first kind of were coming out and being seen on the scene for programming, uh, he started playing with them, uh, for programming projects. And I think Dan really quickly realized that they'd had this, a big impact on how we teach programming. so he reached out to me, uh, and said, I really need to give em a try.

And, uh, after I played with them for a little while, I had the exact same realization that this is gonna change, uh, how we teach programming, uh, in a pretty dramatic way. So having realized that, having realized that we had to change our, uh, introductory CS1 courses, we knew we needed to do that, but in order to teach that class, we'd have to have a book that we could assign our students that that would go along with the class.

And so we knew we had to change the class, but we also knew we had to have a book for it. And given the, the timeline to write books, we started in the book first. Um, and so that's how it got started.


## LLMs for Syntax, Humans for breaking down problems

[00:01:45] **Dan:** I guess we figured out that our course had to change first, before we knew exactly, um, how it had to change. One thing we, um, learned early on was that the kinds of assignments we give in our introductory courses, they're just solved by, by these tools like ChatGPT and copilot.

So, uh, we knew something had to change, and then it is just a matter of figuring out what. And so we spent, um, quite a bit of time with these tools and we started to realize that what's gonna change is the skills that our students need to learn, uh, to be effective using these tools. So like b before these tools, we would spend a lot of time teaching syntax.

Um, and students struggle quite a bit with learning syntax, which I mean, it's very, it's, it's very frustrating, right? Cuz you can't even do anything until you get the syntax right? And you're getting all these errors like missing colons and, you know, mismatched braces and stuff like that. Uh, so it's actually good, that, the LLMs are doing the syntax for the students.

But you know, just because that skill's, uh, not needed as much, uh, doesn't mean that there aren't still skills for students to learn. So instead of syntax, other things become more important. Uh, so for example, uh, Leo and I, realize that reading code is gonna be extremely important even more so than before.

I think if, if that, if that's even possible. Uh, and that's because sometimes you're gonna get back code that just doesn't work. And so we realized that students are gonna need to be able to read, the response that they get to see if the code looks reasonable, or not, right? And then if the code, uh, I is unreasonable, then they need to read more code, uh, and look at other solutions, right, that they get from the, uh, LLM.

Uh, there are other, uh, things they can do as well, like messing around with the prompt and so on. But they're gonna need to be able to read code, uh, throughout the process. And then, so we just kind of kept on using these tools and documenting the skills that students are gonna need.

And we just kinda realized that all the skills students are gonna need are skills we would want to teach anyway. So like, uh, one more example is testing, right? So, students may now not have, uh, an understanding of every last detail of, you know, the Python language like they would before. And so then that makes testing even more important, right?

Than it was they need to verify that the code they're getting is correct. And so they have to be very good at writing test cases. and, and, you know, similar, similar for debugging, we need our students to have strong debugging skills, again, even potentially stronger than before, right? Because if the code isn't working, they need to first determine what the code is doing to be able to fix it. And then I guess one more I'll mention is problem decomposition. And this is a big one. I think this is gonna come up a couple times probably in our talk today, but LLMs struggle when you give them tasks that are too large and students need to know how to break problems down into small components so that, that, LLM can solve each one and, you know, have a good chance of getting it right.

[00:04:56] **Leo:** Yeah, I, I think, um, kind of to, to piggyback off of that, you, you may be hearing these skills and saying, oh, these are absolutely essential skills. Every software engineer should know, uh, these are being taught right now. Right? Um, and the answer is not really, like these aren't core topics in a lot of introductory CS classes because so much time is spent on syntax.

And so fairly early on when we kind of realized these skills would be so essential, Uh, we got really excited because these are skills we want to teach in our classes, and the LLMs are now giving us the ability to do that more.

[00:05:27] **Dan:** Mm-hmm.

[00:05:28] **Jeremy:** I think that's interesting about the syntax comment because you were saying how reading is gonna be more important than ever because you have LLM generating the code. Um, and you need to understand that code that's being generated and understand that it does what it, uh, you think it does.

And so I wonder if when you say you spend less time on syntax, is it because you feel like they're gonna generate this code and they're sort of organically gonna pick up syntax that way versus having to focus on it at the start? I'm just trying to picture what you see changing there. 

[00:06:05] **Dan:** Yeah, Jeremy. So, uh, I, I was, I guess speaking specifically about syntax errors, which don't generally happen when you're using LLMs, and I also agree with you, you need to know what the code is doing, but, um, you can do that without worrying about each specific piece of syntax. Like, um, you're gonna need to know what the keywords do for sure, but, missing, you know, brackets and colons and, uh, oh, there needs to be like a blank line here.

indentation, uh, a lot of this kind of thing. Is done for the most part, correctly by the LLMs. So yeah, I agree with you. You need to be able to identify the structures. So in our, in our book actually, Leo and I have, um, a couple of chapters on reading code and, I don't think we ever break breakdown, a line of code into its individual tokens.

We do talk about the main structures, like ifs and loops and functions and all that. but compared to other books, I, I think or other, uh, other ways of teaching where you would focus on the micro level, we try to focus on the line level now, cuz we want our students to be able to grasp what each line is doing, I guess more than each token.

[00:07:27] **Leo:** Yeah, maybe to, to add to that a bit, it's almost, uh, if you think about the advent of block-based languages, it was to make sure that the, essentially the, the author can't make syntax mistakes, right? Is the whole purpose of kind of block-based languages. And they're, they're huge for introductory programming, especially in like K through 12.

in a sense, LLMs do this because they'd never give you back wrong syntax, or they almost, almost never give you back wrong syntax. And so it takes away that kind of cognitive burden of making sure you handle the, the token level. as uh Dan was saying 


## LLM generated code needs test cases to catch logical errors

[00:08:00] **Jeremy:** I, I'm curious, so you said the syntax is correct, but what are the, the typical mistakes you see coming back from these LLMs?

Is it a, a logical mistake or is it ever something that. Actually doesn't compile. I'm, I'm kind of curious what your experience has been.

[00:08:19] **Leo:** I think the, uh, more common errors that we've been seeing are logical. So it misinterprets the prompt that you're giving it. It essentially tries to solve a problem that's different than what you're trying to solve. It may have bugs in it, so it is in fact trying to solve the right problem, but it, it's off by one, um, is maybe replicating some mistake that it found in, in the large code base.

And so most mistakes are gonna be you need to write test cases, run it. That mistake is then gonna show up when the test cases catch it, and then you'll have to try to fix it. if the students can read the code, uh, if we train them well to read the code, often you'll look at the response. And if the response is just not even trying to solve the right problem, you can usually pick that up pretty quick.

Uh, and I think, I think the students will be learn to do that and then they can just say, okay, this is clearly not the right answer. And, and use the different tools in say vscode to find another answer, and then pick one that's right or change their prompt to get a response that's right. Go through that whole flow.

But then some point or other it will give an answer that looks right. And then I think all of us as software engineers know that even the code looks right, it may not be. And so then they have to actually write the test cases, get some level of confidence that's actually working right before they'll know.

And so sometimes, sometimes, you know, really quick is that it's just clearly wrong at solving the wrong problem. And sometimes it looks right, but it actually has some bugs that need to be fixed.

[00:09:49] **Dan:** I guess one thing that struck me is how much a change in the prompt can, can matter. Uh, Leo, you know, um, we've, we've seen this over and over again where we'll write a prompt. It seems fine to us. And then we'll realize, oh, there are actually two different ways of interpreting this. and, uh, the ambiguity of, of English strikes again, right?

And so it's just amazing to me how clarifying the prompts, how many times that fixes the code. Not always. We've definitely have examples where that's not the case, but, um, more, more often than not, in my experience, changing the prompt, uh, appropriately has a bigger than, than, um, anticipated effect on the, on the code.

It's amazing.

[00:10:36] **Leo:** And for thinking of the prompt, uh, in terms of like doc strings for functions, uh, adding the test cases certainly help. Um, sometimes it is, surprising sometimes that you can add the test cases to the prompt and it'll still give you back code that does not actually pass that test case because it, vscode and copilot doesn't actually run the code that comes back from the LLM.

Uh, but I do find the test cases do tend to help with the quality response you get back.

[00:11:01] **Jeremy:** As a part of your prompt, you're asking it to implement some functionality, and you're also asking it to write these tests for that same functionality?

[00:11:11] **Leo:** Oh no, sorry. I, I, it's more the, um, doc test kind of format. So it, it, um, you're writing, let's say you, you've written your function signature and then you have the description of the function in a doc string. And then at towards the end of the doc string, I'm articulating the test cases that I intend to use.

Um, and the articulating the test cases that I intend to use helps it come with a better prompt. Um, I haven't found it to be great at writing test cases. I haven't spent a ton of time with this, but the time that I have spent, it tends to want to do almost like a brute force search of all possible inputs, uh, as opposed to doing, okay, well here's a couple common.

Here are the edge cases. Now I can feel fairly good about it. It doesn't seem to have that, um, intuition yet.

[00:11:55] **Jeremy:** 

[00:11:55] **Leo:** For the most part, we're writing the test cases our ourselves, and we're gonna be teaching the students how to write the test cases

themselves 

[00:12:01] **Dan:** Yeah,

Yeah. So Leo and I have actually made a conscious decision to have students write test cases from scratch. Even though you could play around with the LLM and have it, you know, try to generate test cases, whether it's flawed or not, we still want students to do this from scratch. We think that writing test cases is a skill we want our students to have.

[00:12:23] **Jeremy:** Sometimes what these models will generate, like you were saying, has logical errors. And hopefully if you're writing the test cases, you've put some thought into 'em, and your test cases are actually checking the correct behavior.

So then you have the LLM generate the implementation. It's running against tests where you know what the correct answer should be. And so if it generates something that's incorrect, you've, you've kind of caught it. You're not totally relying on it. Telling you everything is, is good, you know? Um, It's confidence in something that's like you personally can't see.

It's just what the machine gave you.

[00:13:05] **Dan:** Maybe it takes away one layer of uncertainty too, Jeremy, right? Like, so the code could be wrong, right? And then if it generates test cases, okay, the test cases could be wrong too. And maybe you get unlucky and two wrongs make a right and then your test cases pass for the wrong reason. So yeah, we really wanna hone this skill in our students.

And, and like Leo said earlier, these intro courses used to be so full of low level syntax concerns that we, we didn't do testing properly. I mean, you know, we all try to cover testing, but I think we're gonna be able to cover it a lot more, detailed now.


## LLMs could encourage students to test more since their output is untrusted

[00:13:41] **Leo:** And I, I think we're enthusiastic about, uh, how students will approach testing when you're working with the LLM is what we. This is fairly anecdotal, but uh, when they interact with us talking about testing, often students aren't testing their code because they wrote it. And so of course it's Right. Right.

This is like this really famous, uh, kind of bug in human thinking, right? Is that if you write it, of course the computer's gonna interpret what you're saying, right? Um, and so students tend to trust their code in a way that professional software engineers never would. and I think because it's coming from this third party that you know is wrong, it's coming from the LLM that can, that can often make mistakes.

I think they're gonna be more inclined to actually engage in those testing practices. Uh, kind of knowing about the fallibility of the LLM,

[00:14:27] **Jeremy:** You're shifting the order. I mean, there is test driven development that some people practice, but I feel like probably what's most common is you write the implementation yourself and then, then you'll go and see like, oh, did this thing I, I wrote.

Did it do what I thought it should do? Um, whereas this is kind of flipping it, where it's the large language model is gonna write my code, so I'm just gonna start with the test and then I'll ask it to, to write me the code. And maybe that will kind of make test driven development be the default. 

[00:15:02] **Leo:** So yeah, I, I, I think that students may wanna engage more in kind of test driven development because they wanna think more about, uh, what exactly should this function be doing? Uh, how should behave, what kind of inputs and output should it expect? And then it can kind of write the prompt to co-pilot or whatever LLM is using, uh, to express those inputs and outputs.

Well, they're more apt to get good answer from the LLM and they've kind already got their test cases worked out as well, so they can immediately just go right into the testing agency if the prompt came back right.


## Using LLMs at the function level instead of a broader scope

[00:15:35] **Jeremy:** And you mentioned writing a prompt to implement a specific function. Have you found that they work well at the function level? But if you try to ask it to build something more broad, that that's kind of when it has problems? 

[00:15:53] **Dan:** So, I think in general, LLMs do work best at the function level. We have tried to get it to generate bigger apps, collections of functions, and it can work, but sometimes it does, uh, it does do worse.

But also we want students to do the problem decomposition for themselves and break up the problem into individual functions. Even though maybe the LLM could work, uh, with, uh, bigger chunks of code, we want students to do it. And one reason is so that they can customize what they get from the LLM. So, in the book, we have a bunch of examples where you could probably just throw it at the LLM and get an answer and, you know, eventually get it to work.

But I think at that point, making changes to it might be trickier than it would be if you knew, uh, the architecture of what you were, what you were building. So in the book, we have a bunch of top-down design diagrams, and we want students to understand what they're building at that level, like at the function level instead of, like we said earlier, instead of like at the token level or the line level.


## Potential issues with outsourcing high level design to an LLM

[00:17:03] **Jeremy:** And so like in this example, you're thinking more from a, a learning perspective. You want the student to look at the big picture, figure out, okay, what are all the different functions or parts of my application? Break that down and then feed those individually. To, um, these large language models. I, I'm wondering from like, let's say you're a, a professional software engineer and your interest is more in I want to make the thing and less so, in I want to learn how to make the thing.

in that case, do you feel like you could feel confident in, in giving the large language model a larger piece of the design, or do you still feel like it's good to have that overall structure done by the, the developer and then just be very targeted about how you use the large language model?

[00:18:03] **Leo:** I think that's a tricky question because we haven't worked with these tools heavily in a professional programming setting. I think often when we're thinking about large design of software, you're gonna be working on teams, talking with other members of the team about the interfaces and things like that.

And so I'd be pretty hesitant to to outsource that, that thinking to the, the l lm cuz you, the communication between the teams still has to happen. Uh, even if it weren't for that. Um, I kinda think of it as a probabilities. So essentially whenever you ask co copilot or any of these LMS to, to do a task, the more it has to right, get the kind of more likely it's gonna make a mistake.

Um, and so, uh, that's kind of why I like the functional level. It seems like I. Partially because it's not that much code that tends to write. Um, so you help to avoid kinda the probabilistic problem, but also because it's learned on a huge code base that has lots and lots of functions that have been implemented.

It tends to do well at that, that solving the function kind of task.

[00:19:10] **Jeremy:** Yeah. And I, I think the way you put it as outsourcing that designer, that decision is, is interesting because yeah, if you are working on a team and whether it's in code review or just in a discussion, often people will ask, well, well, why did you do it this way? Or Why, why is this the, you know, the good way to design it?

And if you kind of handed that off to an l l m, maybe your answer is, I don't know. It's just what it it told me, which (laughs) 

[00:19:39] **Dan:** Yeah.

[00:19:42] **Leo:** That isn't an answer I want to u use talking to my boss. Right. Well the chat GPT told me I should have it this way. That doesn't seem like a good answer.


## Choosing GitHub Copilot for CS1

[00:19:50] **Jeremy:** I think we, we've kind of been talking in more a general sense of working with LLMs and you've mentioned how you're gonna be teaching introductory computer science courses this coming, quarter or semester. And so when you teach these classes, what tools are you gonna recommend your students use?

And yeah, maybe you could go into that a bit.

[00:20:13] **Leo:** Absolutely. So we're gonna be recommending, um, At least, at least for my class, I'm gonna be recommending that they use, uh, vs code with copilot. Um, I just like the integration of the IDE with the, uh, interactions with the LLM uh, I think it avoids just a whole bunch of copy pasting from another interface into your IDE to then, uh, run it.

I think it also reduces the barrier of them kinda immediately getting the code and then testing it right there in the environment. I'm sure any of the other tools would work, it's just, that seems to have worked well for us, uh, when we were writing the book. And that's, that's actually the technique we recommend in the book as well.

Um, so that would be the primary tool for the students writing the code. 

In addition to having them using copilot with, uh, in the IDE for a lot of the code generation, depending on where things are at with copilot x, um, which is right now, um, available through wait list. Uh, if that's, that's available publicly, I think we're gonna be recommending that because it has a copilot chat feature, uh, which can be really nice to interact with.

And, uh, the main use that, that we're gonna be encouraging students to use, whether it be co-pilot chat or a ChatGPT is in just a conversation with the LLM about, particularly modules and libraries. So if you are diving into, merging PDFs, which, uh, Dan did a great job in one of the chapters in our book talking about, if you wanna dive into that, well, what libraries should we be using in Python for that.

Uh, and we found that the LLMs do a really good job at this, of actually saying, here are the different libraries you could use. Here are the pros and cons of them. These are the ones that, uh, need to be actually have additional install done. Or these ones that come in with, vanilla Python. they're actually really good at kind of giving you the what you should use for the various libraries.

Um, and so that's, that's one other way that we were gonna be encouraging the students to use the LLM.


## Types of questions to ask the LLM

[00:22:07] **Dan:** Yeah. So whenever the students or the junior programmer, doesn't know how or doesn't think they can, uh, do something in base Python, we have them interact with the chat and, and ask. So another example that comes to mind from the book is we have a chapter writing some games.

And so for most games, including the two that, uh, we've got in the book, you need to be able to generate random numbers, right? So how do you do that? And so in the past you would've used a search engine stack overflow or something, and you would've found, some sample code and you would've pasted it in to your file and made variable name changes and things like that.

And so what we do now is we ask chat, okay, I need to generate some random numbers. How do I do it? And then it will come back to you with a few options, and then you can systematically work through those options if you like. Uh, and you can ask, okay, is this one built into Python or not? And then it will tell you, oh, this one's not.


## We don't need to memorize API docs

[00:23:11] **Dan:** And you say, oh, well, okay, so like, how do I install this? And then no, does it work on all OSS or just Windows? Right? So, uh, we guide the reader through these questions that you could have, uh, to help you make a decision. Um, and I think what I like the most about this is not having to learn. APIs, like yet another api.

Like I don't, I don't think I have room, you know, in my, like, brain for any more APIs. And, and what's cool is I, I've forgotten like every API that, uh, we've used in the book. So we have like examples of emerging PDFs and, uh, removing duplicate images from directories, uh, from like people's phones, and, and stuff like that.

And I don't know, I don't know which library it's using. Uh, and I'm, I'm totally okay with that, right? Like I just, I, I wanted to get the job done. I wanted to write a tool, and the tool got written and it used some sort of library and it worked great. And I didn't have to look through the documentation for that library and figure out like, which functions do I have to call and things like that.

So, I, I know it, it can be fun, you know, it could be fun to really learn an API well, but a lot of people, they don't want to program for programming sake. Like, they just wanna get work done, right? So, you know, while I, I, I fully admit to, enjoying programming just for the sake of programming. I do a lot of competitive programming problems just for fun.

You know, it's like Sunday morning and it's like, Hey, yeah, I got like an hour and I got an hour to work on something. Let me work on this little competitive programming problem. But, uh, a lot of people, they're not motivated by that. They're motivated by consequences of code. And this is one thing about LLMs that I'm very excited about, is you can just, make a lot more progress, without having to learn what these, people may believe is just useless knowledge, right?

Like, does it really matter how I should invoke this api Right, to merge PDF files? I mean, the answer for many people is no. Like, they just want the result to happen. And I love how we can kinda match what they, uh, deem important, right? With the LLMs, it's like a new level of abstraction, for for many people.


## LLMs make building software possible for more people

[00:25:28] **Leo:** There's a couple of audiences that come to our introductory classes, and what Dan's talking about here is one of the things I'm most excited about with this, and that's the students who come and take just one. Programming class. I know it's probably a different audience than, uh, a lot of the people listening right now.

Um, but the people who just take one programming class, it's required for, for their major. They, I just wanted to explore it a little bit, but they, they don't go into this as a, as a career. I think a lot of those students right now, uh, if you ask them a year later to program something, do any of these tasks that we're talking about right now, I doubt they're able to, even if they did really well in that class.

Uh, and that's really disappointing, right? If they've taken a programming class, they should be able to, to do something with that, a year or even five years later. And I really believe that if you teach them the skills of interacting with these LLMs, they'll be able to do these tasks later. They'll be able to come back and go, you know, I don't remember any of the Python syntax.

I don't remember, uh, even how to get started with this. But you know what, I'm just gonna ask, uh, copilot, how do, how do I go about merging these PDFs, having this directory? And then, uh, the copilot chat comes back and says, oh, you might use this and that. And then they go, oh, I remember, I remember how to, how to write these functions.

And I just said, you have to go over a prompt. I think they could really do it. And that, that's a bit of a game changer, right? That means a larger portion of our society will be able to, uh, write code and using a useful way. And I'm just really excited about that. I think it's gonna be really nice, uh, after the changes happen.


## More people might stick with Computer Science

[00:26:58] **Jeremy:** I can totally see in the context of someone who's, not seeing it as a career, or someone who is like, hasn't done it in a while. It could be. These tools can be incredibly useful, right? Or it can even get you interested in this field at all, right? Like a lot of people, they, they struggle through the syntax and then they decide like, oh, this is not for me.

Even though like they had something really cool they wanted to build and, and maybe these kind of tools can, can get them over that hump.

[00:27:31] **Leo:** Exactly. I think there's a population of students, um, and it varies a bit by demographics, who come to computer science, with really the best motives in mind, right? They wanna make their goals in their life are to make the world a better place, and they want to achieve those goals. And if you spend the first three quarters or three semesters working with them and all they're seeing is syntax and they're not actually solving anything meaningful, um, it starts to create this disconnect of what their goals are for their life and what they think the goals of are, are career are.

Of course as, as, as a computer science, I wanna say, stick it out. You know, if you, if you go into the fourth, fifth class, you'll start seeing how these are really useful tools that can make society a better place. But it'd be really nice to front load that and have them solving useful problems much earlier and seeing that, uh, computer science, uh, can be used in really nice ways.


## Efficency can be taught later

[00:28:26] **Jeremy:** And, and so within the, the context of. People who are studying computer science will eventually, who may become professional software developers, things like that. Something more long term where it becomes more of a craft, the, the code that comes back from these large language models. Sometimes it could be something that's like not maybe the most easy to read or it may be doing something inefficiently.

And I'm wondering from your perspective how users of these tools should, should think about that and, and recognize when that's a problem.



[00:29:06] **Dan:** We in, in, in the first couple of courses, typically in the CS program, um, we don't spend much time on efficiency. the reason is that there's just so much to learn early on, and, um, we worry about overwhelming people with, know, too much, for them to, to process it at once. And we don't wanna prevent students from becoming interested, by.

Giving them all of these requirements early on. So typically we, you know, we push efficiency, down the, down the road into like a data structures course, for example. But your question points to another reason why, we've decided to teach some of the skills we teach early on. So if, if a student, you know, came up to Leo or, or me and said, Hey, you know, like I wanna generate efficient code, how do I do it?

My answer would, would be, so like, get, get familiar with programming first, but you are learning the skills necessary where you'll be able to look at code later because you know how to read it still, right? It's not, uh, something that you don't understand. You're gonna, you're gonna know it. We're gonna spend lots of time on code reading, and so later I think we can just teach efficiency the way we always did.

Um, so, you know, doing, uh, time complexity analysis on, on the code and they're still gonna understand what the code is doing. So, um, I, I, I don't think this is going to, this is going to change much in, in the earliest courses.


## LLMs can expose students to different types of code

[00:30:35] **Leo:** To the, to the point about code readability, I might add that, uh, certainly they're gonna get back some, some code that's maybe not the best style and it may not be as readable. Uh, but what's kinda interesting is that students aren't exposed to a lot of different styles kind of in our existing courses, right?

They, they see the code that they write and they see the code that the professor writes and gives them, and there's not much else. And so, I mean, we're gonna need data and we're gonna need research to, to, to know this for sure, but it, it, I suspect them seeing lots of different code styles and having to read those different code styles may actually inform them better than we do now about what makes code more readable.

Uh, and then they might be able to employ that as they go forward.

[00:31:21] **Jeremy:** And, and when you're saying they're gonna read different styles and things like that, are you referring to code they're gonna see from the LLM or are you talking about them reading just other code bases in their classes or their professional work?

[00:31:39] **Leo:** Oh, I'm sorry. Yeah, I was referring to the code. They'll see from the LLM Right 

[00:31:43] **Jeremy:** Oh I see 

[00:31:43] **Leo:** LLM will come back in all these different ways. They'll have different styles and they'll, uh, have different approaches to solving it. Right? Sometimes they'll, uh, come back with like this one line 

Lambda expression thing that solves it, and they'll have no idea how that works.

And they'll, they'll ask for a different answer and they'll get, uh, a much more, uh, user-friendly first, uh, first programing experience kind of code back. And they'll be able to understand that and go, okay, this is the kind of code that I wanna see. Not this thing that was completely non-readable. 

[00:32:11] **Dan:** Yeah, Leo, I just thought of something. So, uh, so you know, by default you can get it to give you 10, uh, code segments to solve the problem, right? So it'd be kind of cool, if we ask students about each of them, right? Each of the 10, which ones are right, which ones have bugs, which ones have good style, which ones have bad style, it's like a built-in learning opportunity right there.

So yeah.

[00:32:34] **Leo:** Oh, it's true. Yeah. And, and so the 10 things that, uh, Dan I was referring to is if you do control, enter in vs code when you're working with a copilot, it'll give you back 10. Possible responses. And you're totally right Dan. You could just say of these 10, how readable are they? Are they right? Um, there's lots of fun things you can do to ask students questions.

[00:32:51] **Dan:** and often many of them are right with just subtly different ways of, of, of, of solving the problem. I mean, I'll, I'll admit to having some fun looking through all of the suggestions just to kind of see what the variability is and when there's a lot of variability. I really like it because, uh, like Leo said, it exposes people to different styles they may not have seen before.

And, um, may it may, it may, um, encourage you to ask questions, right? Like, why does this one work? Right? I've tested it. It doesn't look like it should work. Why does it work? I feel like that's the beginning of a pr pretty powerful learning experience right there.

[00:33:30] **Jeremy:** Yeah, that makes sense to me because I, I think about how when a lot of people are doing software development before all these LLMs, they will search on the internet and go, okay, what's an existing answer for this thing I'm trying to do?

They'll find a post on Stack Overflow and they'll find the accepted answer and it'll be like, okay, this is it. This is the solution. Whereas, at least in this case, it seems like you can go like, okay, well here's, here's 10, 10 potential solutions, and at least you get a little bit more exposure to, um, what are the different ways you could do it.

[00:34:06] **Leo:** Exactly, and, and it's nice for 'em to see these different options. And I think there is, for professional software engineers seeing that stack overflow post, like, here's the accepted answer, integrating that into your code isn't a big jump for, for a lot of us. Um, but I do wanna stress that for the intro students, it often is a really big jump.

Uh, just the, oh, how do I change around this? Oh, this was the interface for this function, but I'm been asked to have this other interface with a function and, and they really can struggle in that domain. And so I think copilot and these LLMs are nice in that they give back answers that are more tailored to the existing code that they're working with, um, and will reduce that barrier of them trying to incorporate the answer.


## Optimization can come later, most code is straightforward

[00:34:50] **Jeremy:** So it seems kind of overall, when you're talking about people who are using programming in a more professional capacity, the code style and efficiency that will probably be taught very similarly to however it is now, where you basically have to get exposed to different styles and types of code, get exposed to the algorithms and and that will allow you to read the answers you get back better.

So the answers you get back from the LLM with the knowledge you gain from these later courses, you'll be able to tell like, oh, okay, this is, this. Level of complexity, or this has like, you know, exponential, performance implications, that kind of thing.

[00:35:43] **Leo:** So I think the performance piece is really important. Um, and I appreciate your, you bringing it up. I think, I'm, I'm kind of curious, uh, uh, what percentage of the time professional programmers are really spent, uh, are spending optimizing, uh, the code that they write?

Um, I suspect a lot of the code that's written, uh, is pretty straightforward. Uh, you, you already know how to work with the database you're working with. You already know how to write the queries for that. You're, you're, you're just, uh, you're still doing something that, that's certainly thought provoking, but it's not the hard work of, oh, how am I gonna write design the right algorithm for this to get the exact best runtime?

And so I think there are some times that that does matter, but those may be the times that the LLMs aren't as helpful and there's still gonna be a, a pretty big need for programmers who know how to do that, uh, themselves.

[00:36:33] **Jeremy:** Yeah. I mean, I, I think that of course this is gonna vary from industry to industry, but Dan, you were talking about learning APIs and I feel like a lot of jobs are learning APIs and gluing them together.

[00:36:49] **Dan:** Yeah. Um, I would agree, but I wonder what can happen if some of that's automated. Right? So maybe, people who are gluing APIs together will be able to. Get even more done, right? Incorporate even more, APIs in the same amount of time that they've been doing it. Now, I don't, I don't know if that job changes as dramatically as it, it seems, um, I guess there's this tension between people, having to change jobs or become more efficient in the current job.

And, you know, obviously I, I hope it's the latter and there is some recent evidence that it could end up being, the latter, just more productive people overall, building, know, bigger software in incorporating more APIs than, than before and, and not overloading yourself. So, we'll, we'll see, you know, how it, how it all, um, how it all turns out.

But I'm, I'm hopeful that we'll just be doing our jobs better.


## Reading code as a skill

[00:37:51] **Jeremy:** In that, that context, sometimes people will say that the, the reading of code and comprehending code can sometimes be more difficult than writing the, the code. And in fact, can sometimes take you more time, like, let's say you've built out a project and now you need to add new features.

Well, to add the feature, you have to understand the, the code base that existed before and so. When we talk about LLMs and the context of not programming, but just general writing, people talk about the fact that it's easy to generate more writing, right? We can generate more documents, blog posts, more articles, that sort of thing.

And with code, it sounds like it'll be similar, right? Where it'll be easier for us to write more code, generate more code. Um, but I wonder if either of you have thought or, or think it's a concern that we'll be generating so much code that now we'll have so much we won't be able to even have the time to understand all of it, 

[00:38:55] **Leo:** I haven't thought much about the generating so much code that you can't understand. I mean, I think if, if we're generating code, I, I'm really hoping someone's testing and making sure it works right and stuff. And so I guess it depends on what kind of, uh, what level of the interface are we, we looking at.

Um, but I have thought about a fair bit about the, the, what you described early on in your question, which was. Diving into a big code base, figuring out what needs to be changed and changing it, that is a really common task, especially for like new software engineers, uh, in their, their first jobs. Right.

And it is also one that's really well documented in the, the education literature, uh, education literature, uh, that we aren't teaching them to do. Like we almost always are giving them, uh, right, these functions are really well defined or, uh, write the code all from yourself, but we rarely ever give them large code bases to learn from.

Now I don't think diving into a large code base and trying to understand how it works is the right thing for like an intro class. And then we're mainly talking about, uh, students first learning your program here. Uh, but I am encouraged that we are teaching code reading as kind of a first level skill when I think current programming courses teach code reading right?

In parallel with writing. So a lot of the writing's happening very early before they even know how to read well. Um, and so I think there's some optimism here that if we teach code reading first and make it a core skill, they'll be better set up in the later classes to maybe take on those large projects where they tackle the exact problem you're describing, which is also the exact thing they're gonna have to do when they get to, to their jobs.


## The amount of code we throw away may increase exponentionally

[00:40:37] **Jeremy:** Yeah, it, it also kind of, I wonder sometimes when you're writing code, you'll write it in a certain way because it's tedious to write a lot of code, right? Like you'll, you'll make something generic in such a way where you can reuse it, and maybe reduce the amount of lines of code. But then when you have something, generate that code, maybe it'll be a solution that.

Is a lot more code than you would've written personally, and it works. But, by nature, the fact that it was easy to generate, you chose that solution versus one that, that maybe was more generic and um, had less code. I, I'm not sure if that makes sense, but I'm kind of curious if the use of these models will sort of change maybe how we write code

[00:41:30] **Dan:** I'm kind of wondering if the amount of code we throw away is going to increase exponentially. Because, because, um, you spend time working on something, you're probably gonna keep it. But I, I wonder because, uh, Jeremy, like what you said, it's, it's so easy to generate code now. so I, I've had this thought where, what, not sure how, how, um, how much I believe myself here, but, uh, should we be storing the, the prompt, like not the dot py file, right?

Like just store the prompt and then if you do have to regenerate the code later, maybe you gotta make some tweaks or something. You just change the prompt and then, and then rerun it. So, because, because, because code is, um, It's not there yet, but it's, it's becoming free, right? It's becoming, you can generate as much of it as you want.

And so I, I wonder how much, how much of it is, so there's, there's a lot of code already that you write once, and you run it once and then, and then you get rid of it or lose it or whatever. And I wonder if that, that practice will increase. So it's like, okay, you know, I wanna do this data analysis.

Okay. So you write a prompt, you get some code, you generate some graph, and then you just don't even think about it. You just get rid of it, and then maybe later you want another similar analysis and you just do it again. Right. So I kind of wonder, because there's maybe less ownership now of code, right?

You didn't like sweat as much to write the code. So maybe, maybe more of it gets thrown away.

[00:43:03] **Leo:** I, I completely see what you're saying, Dan. So you have the prompt and you had it perform some form of data analysis and you wanna tweak it to do a slightly different data analysis. Uh, I wouldn't go into the, I mean, right now if I wrote the code from scratch, I would go into the code and find that one spot that I need to change and I would tweak it.

But if I'm just generating the code, I would just tweak the prompt and then get a new piece of code that does exactly what I want there without having to, to

[00:43:26] **Dan:** yeah. You know, how, how, it can take a, a long time to re-familiarize yourself with a program that you wrote six months ago. You know, it's like, oh, I, I called this variable temp one. Like, what's this for again? Right. you know, maybe, yeah,

[00:43:41] **Leo:** Wait, I think we've all been there.


## Keeping the prompt instead of the code

[00:43:43] **Dan:** Uh, but yeah, I don't know. It's just, just a thought I've been having.

It's like, it, so, so when, when, now when, when I hear people talking about code maintenance, for example, like using, you know, good variable names and consistent style and stuff, in my head I'm thinking, well, you know, is, is the code the artifact now? Is it still the artifact? And right now, you know, of course it is.

But, um, but, you know, fast forward a little while, maybe, maybe some of what I just said, uh, sort of becomes true eventually.

[00:44:11] **Leo:** That's getting to perhaps kind a larger issue about what is the interface that we're, we work with as programmers. I've been thinking about this a lot, uh, just because I, I teach my, my background's. I have a PhD in computer architecture, and so I teach the classes that do machine code and assembly code, and they're, they're, they're core classes for computer scientists because you need to know how computers work.

And, um, I think that's a core component, understanding that, But we don't start by teaching the students machine code. Like no one wants to learn how to program a machine. Um, at least I can't imagine anyone wanting to learn that. Um, and we've kind of cognitively picked Python or Java right now, the most common two programming language to learn from.

Because they're easy to learn, they're easy to, to read. The code tends to be more understandable when you read it. It tends to be a little bit more forgiving when you write it. Um, and so we picked these because we think they're nice interfaces. They're, they're convenient for programmers and they're convenient for, for new learners.

And it just seems to make sense that the LLM may be that next step of interface that we start choosing. The, the catch is because it can be wrong. It's not like a compiler. A compiler is deterministic. It's gonna be, uh, shy of that. Maybe one time in your career you find a compiler bug, like the compiler's always right.

This time the LLM isn't always right and so I, I'm not sure how this is all gonna play out. Um, you can imagine the LLM as the new interface and all we ever store is, is code prompts and we don't ever even see the code, perhaps as one scenario. And the other is we, we do in fact still interact with the LLMs and still interact after the code.

Um, but I think it's too early to kind of know where this is all gonna fall. But, um, we could see some big shifts, I think, in the field over the next few years.

[00:45:52] **Jeremy:** Yeah, I think that's pretty interesting to think about what, what Dan had mentioned where yeah, you could check in your prompt and maybe a set of test cases for the app that's supposed to come out and yeah, maybe that's your alternative to the actual source code. Um, especially for things that, like you were saying, are, are used not that frequently or maybe you only use it once and so the, um, the quality of the actual code is.

Maybe less so important in terms of readability and things like that. And as long as you can reliably reproduce that thing, yeah, maybe, maybe that does make sense.

[00:46:39] **Leo:** The reliable reproduction could be the tricky part. And you there may be even saying that you, you start doing where you tag don't, don't try to reproduce this. Like, we actually spend a whole bunch of time on this. It's super optimized. Like, don't think the LLMs gonna give you this answer again. So, uh, keep the code along with the prompt.

Keep the code too. Don't, don't scratch that because the LLMs not gonna do better. Um, and then in some cases you're like, yeah, the LLM's gonna do a pretty good job on this and

[00:47:07] **Dan:** Yeah. Leo, maybe we have to Maybe we have to distinguish between code that you can just get out of an LLM no problem. And code that people have spent time working on. I like that. Yeah. Yeah,

[00:47:21] **Leo:** some you're like, hashtag don't change. 

[00:47:23] **Dan:** Humans were here. 

[00:47:25] **Leo:** exactly.


## The concerns about relying on commercial tools

[00:47:27] **Jeremy:** Yeah. this is the 30th iteration of this code we generated and we verified that this one's good. So just, just, it's a interesting, interesting future. We, we might be heading into, so, so one thing you, you mentioned a little bit earlier is that the tools that you're gonna recommend to your students, it sounds like it's primarily going to be GitHub copilot and GitHub copilot X for the, the chat interface.

And one thing about these tools is these are tools by commercial companies, right? These are tools by OpenAI and Microsoft. They're tools that you have to pay a subscription fee to use. You have to send your code to a commercial server. And I wonder if that aspect concerns you at all. The, the fact that the foundations that our students are learning on is kind of reliant on these companies and these cloud services.

[00:48:31] **Leo:** I think it's an amazing question. Uh, I think to some degree these are the tools that professional software engineers are using, and so we need, there's, there's a bit of an obligation as instructors to teach them the tools that they're gonna be using as professionals going forward. I think right now they're free.

Uh, to use for, for education's sake. and so as long as that stays the case, I'm a little, more comfortable with it. If it started to move to a pay model for education, I think there could be some really big problems with equity. and I think it's not just true for, for computer science, but I'll start with computer science.

I mean, if it's computer science and we start making it where you would have to pay to get access to these models or use these models, then whether we tell the students they can use it or not, they still can use them. And so there's gonna be some students that, the wealthier students who may have access to these, who are being able to learn better from these, being able to solve better homeworks with these, that's super scary.

And you could imagine the same thing for even just K through 12 education, right? If you're thinking about them writing essays for homeworks or anything else, if it's a pay model, then the students who have, uh, the money will pay for it and get access to these tools. And the students who don't, won't.

You could imagine the, all these kind of socioeconomic, uh, divides that already exist, only being exacerbated by these tools if they switch to this pay model. Um, so that has me very worried. Um, and there's some real ethical issues we have to think about when we're, we're using them. Yeah. Um, the other ethical issue I kinda wanna mention is just the, the copyright and the notion of ownership.

Um, and I think it's important for us as instructors to engage students in the conversation about what it means to create content and intellectual property and how these models are built and what they're building off of. Um, and just engage in that ethical conversation with the students. I don't think we as a society have figured this out.

I don't, I think there's gonna be some time both legally and ethically before we have the right answers. but at the very least, you need to talk to the students about, uh, these challenges so they know what's going on and they can engage in the debate.

[00:50:45] **Dan:** Yeah, just to underscore that, Leo, this is the reason we're doing research on the first version of the course that Leo's teaching. We need research on the impact of LLMs, on students. especially, we need to know if students benefit from this, in what ways they benefit. How are these benefits distributed across demographic groups?

We have a long and sad history in, computer science of inequities, in who takes our courses, who succeeds in our courses. we're very aware of this and it's, uh, unacceptable to make that situation, uh, worse than it already is. So, um, we're, we're gonna be carefully doing our research on this, uh, first offering of the course.


## A downside is students might bypass fundamentals

[00:51:30] **Jeremy:** So we've mostly been talking about the benefits of using these tools in classes and in education. we just mentioned the possible inequities if you don't have access to those things, I, I wonder if from either of you, if there are negatives you see to this technology, whether that's the impact on what people learn or in anything else.

Like are there downsides you see to the use of this technology? 

[00:52:04] **Dan:** Yeah. So in addition to, uh, the important, uh, inequity concerns that, uh, we just talked about, I have a concern about students using the tools in ways that. Don't help them learn the skills we think they need. So it's a, it's a, it's a power tool and you can, uh, you can get pretty far, I think with, without, um, being systematic in, in how you work with it and without testing, without debugging, um, it's, you know, it's, it's kind of magic right now.

And so I can imagine, a lot of students just taking off at, you know, a hundred miles an hour. and so I'm one, one of, one of, uh, the things we have to worry about in these initial courses is, convincing students that there really are principles to using this technology. You can't just type something and get an answer and then go party.

and, and, and so that, that is one of my concerns. That's one of the negatives. It's super powerful. And, like, like, so before you, you can't just type some Python and make it work and, but now you can sort of type in whatever you want and kind of get something back. and so part of our job as educators is to help students use these tools, in in a way that.

Will ensure their long-term success with, with these tools, right? So, I, I'm not saying that they can't just do whatever they want and, and make some of their first assignments work. I, I think they could, I think they could be like un principled with the prompts and just throw it in there and get code and, you know, submit that, submit that code.

But, uh, we're, we're going, you know, we're going for longer term, uh, effectiveness here, right? We have students who may not take another CS course. We need to keep them in mind. We have students who are gonna wanna eventually be software engineers, uh, security experts, PhDs in computer science, right? So we have a number of audiences that we're talking about, and we think they all need to know the fundamental skills of programming still.

Even though, you know, they have this, this power tool at their expense now.

[00:54:07] **Leo:** Speaking of the fundamental skills for programming, I, because of my, my hardware background, I'm this huge fan of teaching mental models in classes. Like what is the mental model of computation? Like, how, how do you imagine the computer is executing as you write the code? And, uh, ideally a professional computer scientist should be able to take, okay, well this is kind of the, my interpretation, this is my mental model for when I'm working at Python.

If I really, really wanna drill this down, I can turn that into assembly. And if I really had to and turn to machine and even think about how this is working within the cash subsystems and virtual memory and all these things, I want 'em to be able to play those things out. We are changing the first class, and I think the first class is gonna be doing some things much better than before, like teaching problem decomposition and things like that.

I'll, I'll mention that in a second, but, we are doing some things better. but we may not be teaching at how is the computer working as well. And so you can't just change one course and think the rest of the curriculum's gonna work. And so I think the entire curriculum's gonna need to adjust some, um, in, in a way of just adapting to these LLMs.


## Rethinking how to assess students

[00:55:10] **Leo:** Um, the second piece for things getting potentially more challenging, uh, is instructors, we're in a good place right now as instructors, uh, in terms of how we assign and grade homework. Um, so grading, uh, this probably isn't gonna be a shock, is not one of our favorite things to do as faculty. I mean, it's actually really important.

Uh, it's, it's central to us understanding how our students have learned, but it's generally not the most favorite thing that we do. And what a lot of instructors have done, myself included, is for much the introductory sequence. We have created assignments that can be entirely auto grade. So we define functions incredibly well.

Like, write a really good description, this is exactly what it needs to do, and the students write that one piece of code and, uh, whether we like it or not. That is exactly when copilot does very well, and the LLMs do really well. And so the LLMs are gonna solve those very easily already. So we have to fix our assignments just like it, it's a given.

Um, but it means that we're probably gonna have to rethink how we do assessment. Um, and so we're probably gonna be writing assignments that are much more open-ended and we're probably gonna have to be grading those, uh, putting more care and time integrating those potentially by hand. Uh, but I think these are all good things for the community and for the field.

Um, but you can imagine how it's gonna be a bit of a, a shift for faculty and, and may take some time, uh, to be adopted as a result.

[00:56:41] **Jeremy:** And, and so if you're shifting to homework that is more broad in scope, has more code, needs more human eyes on it, how how does that scale within the educators side? Right. You were, you were talking about how you've got, um, things that could be auto graded before and then now you're letting somebody generate this whole project.

How does that work from your end?

[00:57:09] **Leo:** I, I think there's a few things that are at play. Um, we, at, at large institutions like Dan and I are at, we have kind of armies of, uh, instructor assistants, instructional assistants that help us, uh, and so we can engage 'em in, in various tasks. And so, uh, one of the roles they heavily have now is helping students in the labs solve these auto grade assignments.

and so you can imagine they will still be in the labs helping the students with these creative assignments, but now they're gonna have to have potentially a larger role in assessing the success of those. Um, there's been some really creative work, uh, in, in assessment and so I'll, I'll, I'll mention a couple of the ones, but there's, I, I'm sure I'm gonna be omitting some.

But, uh, one is, Students could complete their project, and then they have to record a short video of them explaining the code that was in their project and how it worked, and you actually assess them on that video and their explanation of the code and how it works. Right? Because those can be perhaps shorter than trying to go through a really big project and, and see how it works.

Um, there's a tool out of a UIUC, um, called Prairie Learn that helps with, um, uh, these are still auto graded, but uh, it helps with the, the test setting where you can write questions and have them, uh, graded kinda in a, in a exam or homework setting. the, the neat feature of that is that it can be randomized and so you don't have to worry as much about students kind of leaking information to each other about, test content from quarter to quarter.

And so, because the randomization, they have to learn, actually learn the skills, and so you can, um, kinda engage with 'em in these test centers. And so right now a big grading burden on, on faculty is exams. And so you can actually give more exams, give more frequent feedback to the students and with, without the same grading burden.

and so that, that's the other kinda exciting assessment piece.

[00:59:01] **Dan:** 


## Current assessment is not effective

[00:59:01] **Jeremy:** In the different types of assessments, like the example of the video you gave, I'm just thinking to myself, well, the person could ask copilot or ChatGPT to give 'em a script, right? And they can rehearse that when they, um, send you a video.

[00:59:18] **Leo:** I think, but I think that's, um, I think this is a philosophical shift in assessment that's kind of been gaining momentum over the years and that's that the assignments are all formative and they should all be. Pretty low stakes and the students should be doing them for the process of learning. and then, and, and it's unfair in some ways. There's a, there's a lot of things right now where you kind of grade them on, were you present at this time?

Did you, did you meet this deadline at this time? Which if you're thinking about the, a diverse population of students, like you can imagine like a, a working mother who's also trying to do this, grading them on where you here at this time doesn't feel very equitable to me. And so there's this whole movement for grading for equity that shifts much of the assessment onto the exams.

And so, yeah, the students could, uh, find multiple ways to cheat on the homeworks, but that's not the point of the homework and the homework's just to learn. It's a small scale, the grade, so. But you still then have those kinda controlled environments where they're taking these tests and that's where the grade actually comes from.

Um, it's gonna take some time to make that shift, at, at, at least at a number of schools, my own included assess that those ho take home assignments are a huge portion of the grade. And students will love that because they can get all this help. And they can, especially with the auto graders, that they don't even write their own test cases.

They just use the auto graders, the test cases. Right. Um, which is really depressing. Um, and they go to the, the, the instructional staff. The instructional staff tends to, to give away the answers. That's actually a paper that we, uh, published a few years ago. Um, and so the students love this high stakes, but tons of help version of assessment, but that may not actually measure their, their level of knowledge.

And so it's gonna take a little bit of adjustment, for students and for faculty to do the shift, uh, to where the, as assess the, the exams are the


## Give students something interesting to build and don't worry about cheating

[01:01:09] **Dan:** Yeah. Also, I'm, I'm not convinced that cheating is gonna be a problem here. it's very possible, for example, that students cheat on our previous assignments because the assignments were not authentic. Um, you know, in industry you're never going to, no one's gonna come up to you and say, Hey, like, from scratch, you know, write this exact function, takes two lists and determines, you know, how many values are equal between them.

It's like, it's like, that's not gonna happen, right? You're gonna be doing something that has some sort of business purpose. And I kind of wonder, um, and this, this will, you know, this will play out, um, one way or another in the next, in the next, uh, few months. But I kind of wonder if we give students authentic tasks.

Now you're cheating yourself right out of doing some, some something of value, right? Like before you were. You were probably cheating yourself out of a learning opportunity, but how, how can, you know, how can students know that? Right. The assignments boring, right? It's like, write all these functions and then something, something happens because of the magic, you know, starter glue code we wrote.

So I don't, I don't know. I feel like if you give students opportunities to learn what they want to learn, um, there's, I don't, I don't know. I don't, I just don't think there's a reason to cheat. And, and also, I mean, um, I, I've been much happier in my career recently when I don't worry about it. So it's like, okay, I've got a bunch of students, some of them are gonna cheat, some of them are not.

And I'm here to talk to the ones who, who wanna learn. So, I don't know. A lot of people were on some email lists, for example, and a lot of people seem to be panicking about it. And I, I kind of think, you know, buddy, you had a huge cheating problem before. I don't think it's gonna become worse now that you're giving students authentic work to do.

Right? They, they all want to be using, uh, you know, programming to, you know, to do their jobs better or make their lives better, or the world better. They don't wanna waste their own time. But if you give them a decontextualized task, it's like, it's super tempting to just cheat, right? Because what's the point?

Right? And so, um, I, I, I'm, I'm very hopeful. I, I, I am not convinced that that cheating is gonna be a problem.

[01:03:23] **Jeremy:** Yeah, that's a good point, and I think it's very motivating for any student or anybody who's learning a thing to, to be able to see a clear, connection to like an actual thing that I made, versus I'm writing functions to pass these test cases is like not very, not very interesting, uh, intellectually.

So I think if you structure the, the projects where it's like, oh, am I gonna actually make this thing that does this thing That seems pretty cool, then yeah, that's definitely more motivating

to, to actually go through with it.

[01:04:00] **Dan:** Like, just off the top of my head, imagine if every student had to make a landing page, like a website who's gonna cheat? Like what? I want a landing page. Like, 

I, I want that. And, and all student and students are gonna want that too. And so it's like, well, okay. Like I, I, I may as well make it right. Like this has a, this has a purpose.

So, Leo. Leo, I'm curious, you've been, you've been, uh, patiently listening to, to that. I'm curious what you think about 

[01:04:29] **Leo:** Oh, I, I, I, I can't agree more. I think the, um, I mean, we can leverage the research, right? The computing and context is kinda this well established thing that if you teach computing in a context that's meaningful to the students, they tend to learn more and engage more, and wanna stay in the major more. Um, and I think we're just gonna be able to do, we do this right?

We, for convenience sake, and because of the scale of the number of students that we've had in our classes, we've kind of moved away from that and gone to these auto graded nots of exciting assignments. And I think we're, this is the impetus we need to go back to fun, creative, interesting assignments that the students are gonna put time and care into because they want to, not because they have to.


## Problem Decomposition

[01:05:10] **Jeremy:** So it, it sounds like through our discussion, you're, you're really excited about, bringing large language models into the classroom and kind of what that means for you and your, your students. And I wonder if there's anything we didn't really touch on or maybe something that was unexpected that you think is gonna make a really big difference, to you and your students.

[01:05:33] **Leo:** I think one of the things that we haven't touched on yet that I'm, I'm really excited about is, the piece of problem decomposition. And so over the years, because of this trend towards auto grading, uh, what's happened is, all the cognitive work of taking a, a big, computing task and breaking into smaller pieces, deciding what classes should exist, what functions should exist, all those interfaces, all that work that I think is really interesting and exciting.

It is now done for students because the auto grading structure just makes it so you have to have these functions and they just code the functions. and so I think that's really concerning just from a software engineer in perspective, that students are, are learning how to program without learning those core abilities as, as software engineers to take a large problem, break it down, figure out what the right interfaces are, and that's a lot of, that's actually more art than science, I'd argue.

And so the more time you have to practice it, the better. And I am incredibly excited that LLMs are kind of forcing our hand to make us step back, give larger programming tasks to them, and teach them the process of problem decomposition explicitly in a way that, in a way that we've never really, never done before.

I think that's, uh, that's a good place to, to wrap it up on so if people want to hear more about your upcoming book or maybe even enroll in in your class, Leo, where can they get some more information? I. 

Both Dan and I have active LinkedIn pages and we're happy to have folks, uh, follow us there. Manning Publishing is the, publisher for our book. Um, and so we have that book out on early access right now. Um, it should be available, uh, entirely electronically by August in time for the start of the fall quarter.

Um, and then it should be out in print, uh, shortly thereafter. 

[01:07:25] **Jeremy:** Cool. Well, this has been an interesting discussion. I mean, large language models are kind of that's the thing right now. Everybody's trying to, to stuff it into every single product. And I think getting both of your perspective on where it fits in in education has been, has been very interesting.

So thank you. Thank you very much for coming on the show 

[01:07:46] **Leo:** Thank you Jeremy, for inviting us and for running such great podcast. We really appreciate it.

[01:07:52] **Dan:** Thanks Jeremy. 

</div>