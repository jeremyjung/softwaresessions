+++
title = "Scott Hanselman on AI-assisted programming"

description = "I'm not vibing into production"

[extra]
episode_url = "https://pinecast.com/listen/7726eee4-43ad-409b-9d2d-21c130557ce2.mp3"
social_title = "Scott Hanselman on AI-assisted programming"
social_description = "I'm not vibing into production"
+++

Scott Hanselman is the the VP of Developer Community at Microsoft.

We discuss the ambiguity and non-determinism of agentic loops, expressing clear intent to steer models and the need for knowing fundamentals, and why saying you vibed something means you don't care.

This is an extended version of an interview posted on Software Engineering Radio.

## Related links

- [Scott Hanselman](https://www.hanselman.com)
- [Hanselminutes Podcast](http://www.hanselminutes.com/)
- [Scott and Mark Learn To](http://scottandmarklearn.to/)
- [Github Copilot](https://github.com/features/copilot)
- [Claude Code](https://code.claude.com/docs/en/overview)
- [Gemini CLI](https://geminicli.com)
- [Codex](https://chatgpt.com/features/codex)
- [OpenCode](https://opencode.ai)
- [Everything is a Ralph Loop](https://ghuntley.com/loop/)
- [Open Live Writer](https://openlivewriter.com)
- [LM Studio](https://lmstudio.ai)
- [Foundry Local](https://www.foundrylocal.ai)
- [Ollama](https://ollama.com)
- [Beads](https://github.com/steveyegge/beads)
- [OpenClaw](https://openclaw.ai)

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

## Intro

[00:00:00] **Jeremy:** and then do you have a, a hard stop time apart 

[00:00:02] **Jeremy:** from what we set?

[00:00:03] **Scott:** No, I'm chilling. I'm, uh, I'm gonna, after this I'm gonna go on Facebook Marketplace and buy a Mac mini

[00:00:09] **Scott:** So that's what you're, you're between me and my mac Mini. 

[00:00:12] **Scott:** Should be sitting on their porch.

[00:00:13] **Jeremy:** all right. yeah, I guess we'll get 

[00:00:15] **Jeremy:** started. 

[00:00:16] **Scott:** Alright, do it man.

[00:00:18] **Jeremy:** Today I am talking to Scott Hanselman. He's the Vice President of developer community at Microsoft. 

[00:00:24] **Jeremy:** And I last spoke to Scott back in 

[00:00:26] **Jeremy:** 2021 where we discussed NET

[00:00:29] **Scott:** Hey man, how are you?

[00:00:30] **Jeremy:** Pretty good. Today we're gonna talk about all these AI assisted development tools that are out there, and I think it's super overwhelming, I think for a lot of our listeners and for myself.

[00:00:43] **Jeremy:** So let's kind of give an overview of maybe the, the types of tools you have experience with. I think maybe we could start with just the chat bots, the, the ChatGPTs and the text box. you know, go back and forth on 


## Syntax highlighting and autocomplete

[00:00:59] **Scott:** I would even go farther back if I may. and like, not to put too fine a point on it, but like, let's go back to like 1975. 'cause I was thinking about this yesterday. I was trying to explain this to my wife and it's like when I started coding in like 80, 84, I went from assembly to C and people would be like.

[00:01:17] **Scott:** C? Come on, that's too high level, man. You gotta get down to the metal right? You're like, you're, you're, it's gonna rot your brain. C's gonna rot your brain. And then in the early nineties, we got color. And by that I mean we got syntax highlighting and they're like, oh, it's gonna rot your brain. And then we got, Stack Overflow and they were like, oh, you're gonna rot your brain.

[00:01:34] **Scott:** And now we got this. When we started thinking about AI augmented coding, it was next token prediction. You type A for loop, you hit space, and then it makes like ghost text and suggests. So that's the first thing. Then there was the chat bot. So just right before the chat bot, there was the ghost text. Uh, hey, you know, uh, here's, you know, we were, it would like interrupt you.

[00:01:57] **Scott:** And, um, they would have like next token prediction within the editor. And some people really like that 'cause it's like, oh, I know what I'm doing and then it's just gonna auto complete. So it was like auto complete on steroids. Then people went into chat, GPT and started asking questions, and then they would copy paste not from Stack Overflow, they'd copy paste from ChatGPT.


## The ambiguity loop is non deterministic

[00:02:17] **Scott:** Then the agentic loop started. And that's where things got interesting. And if you really want to sound smart in meetings, uh, just say agentic as many times as possible. And agentic loop sounds even smarter. But the idea was that why am I copy pasting this code from ChatGPT when I could just let the agent, the, the LLM run, build, look at the text, see a warning, fix the warning, and then, and then loop.

[00:02:43] **Scott:** And that's when we started getting into things like GitHub Copilot CLI and Gemini and Amp and OpenCode and, and Claude and all of those kind of things where it's LLM sees some tokens, gets the result, makes a judgment, and it's, I call it the ambiguity loop. Because this is what loops, this is what this is The thing about programming versus LLM programming.

[00:03:06] **Scott:** Programming is not ambiguous. Like it runs exactly as you wrote it. And if there's a bug, it's your fault. And if you want a for loop, you write the for loop, you do it in bash or power shall or whatever, and it does the thing. But an ambiguity loop is like, yeah, I don't really know. Like things could happen and we fool ourselves into thinking like regular expressions and stuff, kind of like handle ambiguity.

[00:03:28] **Scott:** But if you imagine this kind of slider bar of ambiguity between I'm parsing this binary and it's gonna work this way, and here's the way that the bites are packed. Versus the like, I don't know, man, it's unstructured data. What are you gonna do? LLMs are really good at ambiguity. Turns out the toil part of programming is really am ambiguous.

[00:03:49] **Scott:** Like I'm writing this, this bot on this other machine over here. I'm running what's called a Ralph Loop that we'll talk about later, and it's bumping into all kinds of little weird problems. And those little weird problems are just crap that I would have to go and Google or look on Stack Overflow. It's just ambiguity.

[00:04:04] **Scott:** So I'm running not a Ralph Loop, but an ambiguity loop that's like working that out because that's not the fun part of programming. The fun part of programming is like building stuff. So I think that these agents and why people are freaking out about them is because it's that same feeling that we got when Stack Overflow happened and we're like, oh, programming's over.

[00:04:21] **Scott:** Or when, when I got syntax highlighting and I was like, oh, it's, I don't have to do anything now that all the text is in color. Does that make sense? That's how I contextualize it across a historical context.

[00:04:32] **Jeremy:** Yeah, I think that's good to, to bring it back to the syntax highlighting and the auto complete, because I think nowadays that's very uncontroversial, right? People, they for the most part will accept like, oh, the syntax highlighting is there. It helps me.

[00:04:49] **Scott:** Yeah. That's a good way to put it.

[00:04:50] **Jeremy:** Point out what I'm looking for. The auto complete. I can quickly see is the suggestion something I want, yes or no? I think for the most part, people are, are on board. I think this ambiguity loop you're talking about is maybe a little bit I think people have more mixed feelings about is, is because of that what you're describing where it's like this slot machine, right? Like maybe it'll give you a good answer, maybe it won't. 


## One shot without specificity doesn't give good results

[00:05:16] **Scott:** Yes. And here's a really great, I had this internal conversation with this guy, like we're on teams and this is an internal guy. And he was so excited because he did a one shot. A one shot is when you type one prompt and then software pops out.

[00:05:29] **Scott:** He did a one shot and he cloned Minecraft. And you know, there's always this, there's this thing that, um, I think it's called, like there's a paper, I think it's like Project Unicorn or something like that, where like OpenAI cloned Minecraft. But forget about that result for a second. And think about the simple semantics of typing a prompt.

[00:05:49] **Scott:** Make me a clone of Minecraft that runs in the browser using ThreeJS. Which word in that sentence is doing the heavy lifting, the heavy semantic lifting. There's Minecraft. And there's ThreeJS because you're steering it and saying, use ThreeJS versus using Babel versus using whatever. But in that sentence, make me a clone means a copy of Minecraft means a lot.

[00:06:16] **Scott:** The word Minecraft semantically is effectively a 50 page spec. So I was trying to tell the guy, dude, that word is doing literally all the lifting, try explaining to it to give you a clone of Minecraft. Except you don't get to use the word Minecraft. Right. And now that would be effectively impossible. Now you go from, oh my gosh, I did a one shot of Minecraft to, this is a hot mess and I really need to be specific.


## The job of a programmer is to express understandable intent

[00:06:45] **Scott:** And you're gonna get, like you said, a roll of the dice. So we need to ask ourselves, when we are making these ambiguity loops, what is the job of the programmer? Well, it's to be specific. Because it's all about expressing your intent and making your intent understood. And I'm sure we would've loved in the sixties, seventies, and eighties to like just talk to the thing, but it wasn't specific enough.

[00:07:11] **Scott:** So we needed to be so specific then like put that electron in that register and we're gonna use assembly to do it. And now suddenly I can say, Hey, you know, computer, what's my blood sugar? And it knows to go into a rest API to get the tokens to go up to my Mongo database to bring all that kind of stuff down.

[00:07:29] **Scott:** 'cause suddenly the, the Lego pieces are, are, are high enough and the stack is deep enough that I can get what I want. And it might try it in Python one day, it might try it in JavaScript one day, but the result is I get to know what my blood sugar is. 'cause a rest, API is called. But that ambiguity loop shouldn't be something that we should take for granted because it's not gonna work every time.

[00:07:53] **Scott:** And that's why I think it's interesting to use the. The ambiguity loop to get me specific software that runs absolutely reliably because talking to chatGPT or talking to Claude, that's not a scripting language, right. It's effectively a pros compiler, and that's different. So I'm using it to make grounded scripts that I then run rather than just yapping at the thing and pretending that it's bash files.

[00:08:19] **Jeremy:** Yeah, in, in some ways it's like that shift you were talking about earlier where you went from writing assembly or machine code to writing compiled languages compiled down to that. And then we got to higher level languages like JavaScript, and then now we're one level. Even before that, we have our english prose that's helping us compile or generate the, the, high level language. 

[00:08:46] **Scott:** You know how people use like Lua or C Sharp and they put it, build it into like Unity apps. Right. And that's like, that's the scripting language for their game. That makes sense to me to embed an LLM would be to embed ambiguity, which they think, oh yeah, look, the NPCs are gonna be able to do stuff.

[00:09:04] **Scott:** But now they could do anything. They could say dumb stuff. They could go off the rails and the game could completely do something that you don't want it to do. That's what we don't want to do. We don't want to push out slop because rolling the dice is not software engineering.


## You can't one-shot a large app, you need to steer

[00:09:18] **Jeremy:** And I think maybe another important point is with that example where you said somebody tried to one shot, let's, let's write Minecraft. Right? My guess is that the end result was not actually Minecraft. It was probably something that resembled it a little bit, but 

[00:09:35] **Scott:** Yeah. I wish I could show you. It's actually, to be clear, it's super impressive. it's a full voxel world. It generates the voxels, it runs in the browser. the textures are all there.

[00:09:45] **Scott:** There's no crafting in mine. Um, but you know, you've got an inventory, it's. It's what you, it's Minecraft if you woke up from a dream and you're just like, oh, I had a dream. I was in Minecraft. So it's maybe like 60% of Minecraft, and that's pretty cool. But again, the spec lives entirely in the word Minecraft because if you said, make me a clone of fufu, and fufu isn't a thing, you're gonna just roll the dice and it's gonna go, it's gonna go insane.

[00:10:14] **Scott:** That's why it's not a reasonable demo to say, make me a space invaders. Make me a Pacman, make me a Donkey Kong. 'cause those words do all the heavy lifting.

[00:10:23] **Jeremy:** And I, I feel like, some of the higher levels people who are running these businesses, CEOs and things like that, they have this vision that. I'm gonna be able to ask this rather ambiguous thing and, and get a complete product, but to me it feels like we're not, we're not actually there. 

[00:10:41] **Scott:** Well, so. Like a, an example that I really like to use. Um, and then may I ask, do you have a car and do you, do you

[00:10:48] **Jeremy:** I do, yeah 

[00:10:50] **Scott:** Okay. Do you drive stick or do you have auto automatic, automatic. Do you know how to drive stick?

[00:10:54] **Jeremy:** I don't know it well enough to comfortably do it. 

[00:10:58] **Scott:** Okay. Do you feel that it is a personal failing, that you don't know how to drive stick.

[00:11:01] **Jeremy:** I do not.

[00:11:03] **Scott:** Okay. So take everything that we just talked about and now apply it to programming, right? Like, I could do assembler, but I couldn't do it without Googling anymore. Do I feel bad about that? No. Could I drive it in an emergency?

[00:11:15] **Scott:** Yes. Could you drive someone to the hospital and stick? Yes. You could probably make it happen if, if you were in a pinch. Here's the question though. What if you answered just now I don't have a car. I only know how to Uber. Then your relationship to the vehicle fundamentally changes. And if the vehicle breaks, you're gonna get outta that car.

[00:11:35] **Scott:** You're gonna leave that poor gentleman there, he's gonna have to fix that car, he's gonna have to repair it, and oil change and tires, and you're just gonna get in another Uber and fly away. But how deep is the stack for you to simply move your body from point A to point B and you have no control over how the guy's gonna get you there.

[00:11:52] **Scott:** So I think that there is value in driving stick occasionally, uh, trying to get somewhere without a GPS, because then the ambiguity has to be, and the responsibility is on you, the onus is on you. While, right now the idea like, Hey, send a stranger in a car with candy to pick me up. and I just like lean back that's the same thing, like asking an Uber to send you somewhere and asking, Claude code or GitHub copilot to make something for you.

[00:12:21] **Scott:** With no specificity. You're lucky. I mean, I hope you get to the airport. Good luck. You know what I mean?

[00:12:27] **Jeremy:** Well, I suppose in that example, the, the Uber or the Lyft, you're giving an address most likely. And it's, it's sort of this well-defined problem of I need to get this person to the airport, or I need to get this person Right. And I, I feel like that's a little different than me saying, telling an LLM, please build me a web browser or build me minecraft.

[00:12:53] **Jeremy:** Minecraft 

[00:12:54] **Scott:** that's fair. I think an example would be, uh, Hey, Uber, take me to the airport.

[00:12:59] **Jeremy:** Without specifying which one.

[00:13:01] **Scott:** Without specifying. And there's no ask user question.

[00:13:04] **Jeremy:** So I guess your point maybe is that it's somewhat unrealistic to say something so vague and not expect there to be a back and forth, to be clarifying questions, that kind of thing.

[00:13:14] **Scott:** Exactly. Exactly. Exactly. And I'm sure you've been in an Uber and you've told them, Hey, take the 405 because you are steering them. You're not driving the car, but you steered. And that's why we're finding steering in these CLI coding agents so delightful where it's like I, I, you're 90% in the direction I need you to go. Just get off on this exit. Yeah, those little moments matter specificity matters.


## Asking questions turned a complicated project into a browser extension

[00:13:40] **Scott:** I'll give you another example. My son is 18 and he has a, a Depop, so he sells like vintage clothing on Depop, which is like a marketplace for people to sell clothing.

[00:13:49] **Scott:** But he ships on a website called Pirate Ship. He doesn't use the beat Depop built in shipping. So I had this vision to make it so he didn't have to copy paste stuff back and forth. And I thought I was gonna do it with like playwright and I was gonna automate browsers and I was gonna build a whole like dashboard for him to do shipping.

[00:14:05] **Scott:** And I was basically using the, the, the copilot as a rubber duck. I was talking back and forth to it. I was talking to myself in the mirror. I'm not actually talking to an entity, I'm talking to myself. And in the brainstorming, just as if I called you and brainstormed. Uh, we, we, we, we realized that, oh, I don't want to write a playwright extension.

[00:14:25] **Scott:** I want a browser extension. So I wrote a browser toolbar for him, and I wouldn't have come up with that. I would've gone all the way down playwright automation and been wrong because of my own biases if I hadn't brainstormed. And a little bit of the ambiguity loop popped up and said, what a, have you thought about a browser extension?

[00:14:44] **Scott:** And it clicked. And then I went immediately. It's like, Hey, take me to JFK. You know, EWR has a direct flight. Have you thought about that? You're right. Let's do it. And that back and forth, as well as having a lot of experience and understanding the power of a browser extension turned out to be a really great experience.

[00:15:01] **Scott:** And now he's got one click shipping for his, uh, his little business.

[00:15:04] **Jeremy:** Very cool.


## Fundamentals are still important to get to the right solution

[00:15:05] **Jeremy:** I have, people ask me sometimes, is it, is it still worth learning how to code? Is it still worth learning all the specificity of, HTTP or how the browser works or databases? And I, I think what you're maybe implying is that having at least some background in these things will help guide you when you're asking these questions, when you're trying to come to a solution.

[00:15:33] **Jeremy:** If you don't have that background, you might not get there.

[00:15:38] **Scott:** I I, I acknowledge my position in history, my age where I grew up.

[00:15:43] **Scott:** I speak English, I'm a white guy on the West Coast. Like all those kind of things are the context in which I came up. I came up in a very interesting time in the eighties programming, so I don't wanna sound like old man who shakes fist cloud. Hey bro, why are you gatekeeping stuff? Right? But I see people saying, Hey man, I just vibed the great, the world's greatest new SaaS.

[00:16:02] **Scott:** Check it out. And they tweet local host 3000. And it's just like, (groan) right? So like, do you. Like buy your furniture at ikea? I do. Could you cut a board and did you take like probably W wood shop? Yeah. You know, would you build your own furniture? No. But you have an appreciation for building Ikea stuff. I think that's why Ikea makes you build it so that you don't feel like it just appeared in your house.

[00:16:28] **Scott:** I can't just like spawn up like Billy shelves. So that Yes. Without, while recognizing that it might sound like, hey, this old guy wants me to write everything in Assembler. Yes, yes, yes. Appreciating that oil changes are a thing. DevOps is a thing. Build loops are a thing. Um, and quality matters. So I would argue that it's not the death of software engineering, it's the death of toil and the only thing that matters now is taste and judgment.

[00:16:59] **Jeremy:** So where do you think that that balance is? What do you think people should be learning where they can use these tools effectively and they can still be building quality?

[00:17:12] **Scott:** I think if I were, and by the way, when I retire, I'm gonna go and teach, uh, high school computer science. That's my, my plan. I've got it all lined up, and I was a professor before, and I'll be a professor again. I don't think there's enough computer science history, and I don't think there's enough basics. I don't think anyone learned HTTP in college, right? They just kind of sat down. They did compilers. They learned Lex and yacc and then suddenly you're learning OSes and then you're writing apps, but you pick up HTTP and DNS and stuff like that.

[00:17:43] **Scott:** Maybe like I took a 400 level TCP/IP class, but as a general rule, you're not spending a lot of time learning how to do Kubernetes, uh, in school. I would, I think HTTP, DNS, NATS, like that's all bread and butter. That's, that's sociology, right? Like why do you learn about world history? So you can go and be like a corporate drone.

[00:18:06] **Scott:** You learn because it makes you a whole full person. So yeah, there is someone right now vibe coding their bachelor's degree in software engineering and I love that for them. But they're gonna get nailed just as people who don't learn about sociology and history and psychology are gonna get, are gonna get nailed.

[00:18:26] **Scott:** The Dunning Kruger effect is a real thing.


## Using LLMs differently based on your knowledge level

[00:18:28] **Jeremy:** Hypothetically, when you're teaching your computer science class, what would you tell your students in terms of using these AI assisted tools?

[00:18:39] **Scott:** I would say it is a funny two-faced thing because it is a senior engineer with infinite patience but it is a junior engineer with infinite energy.

[00:18:52] **Scott:** And the role that the LLM chooses depends on how you're coming at it. If I come at it as a .NET engineer. And I'm competent in C then it is a junior engineer with infinite energy and I need to point it exactly and I tell it what I want and it does the thing. But if I come at it as a Python developer, of which I am a novice or a medium, then it's more senior than I am.

[00:19:18] **Scott:** So I would be less likely to disagree if it makes a recommendation, right? So if it does something in .NET I'm like, no, don't use that. Use this. I will say, no, we're going to JFK. Trust me, this is how we're getting there. But if I've never been to that country, I've never been to that state, I don't know which airports the better.

[00:19:35] **Scott:** I'm gonna take the advice of the Uber driver. But it's the same LLM, it's the same model. And if you come at it with that sense of like, no, I know what I'm doing. Strong opinions weekly held, you're gonna have a much better experience. Additionally, the opening prompts matter, and I think that there's room for learning, uh, prompts.

[00:19:56] **Scott:** So if I were teaching the class, I would include a markdown file and skills that would force the, you know, user to like, oh, you just tried to vibe your entire final, here's some multiple choice questions. Here's some, you know, here's an exercise for the reader. I'm not gonna let them just, you know, one shoting your computer science final.

[00:20:14] **Scott:** Uh, you, you're doing yourself a disservice, I think if you do that.


## If you don't understand why the LLM did a thing then you should not feel comfortable shipping it

[00:20:18] **Jeremy:** Yeah, that's an interesting point about how the way you interact with the LLM is so different when you know the domain or you know the language Well, and I wonder if, in your opinion, if it's, let's say you don't know it well.

[00:20:34] **Jeremy:** Are, are you in, in a sense, sort of fated to get a result that's maybe not as good, like, because you didn't have that background because you couldn't steer it? 

[00:20:45] **Scott:** If you don't understand why it did a thing, then I would not feel comfortable shipping it. And that's where I think the, the limit is. Like if I were gonna do something, like, I'm like, I'm doing a bunch of Python stuff and I think I maybe a four outta 10 or five outta 10, but I know how their type system works versus TypeScript versus whatever.

[00:21:08] **Scott:** So I'm asking generic computer science questions like, you know, like, what's the python equivalent of a linter? Do I have enough guards for my exceptions? Like, that's not Python questions, that's just quality, that's just taste, you know, and I'll say, I'll challenge its assumptions. Like I, I built a blood sugar management system in Python a couple of days ago, and I've asked it like, should this be TypeScript?

[00:21:32] **Scott:** And it, and it, and I said, make me a pros and cons table about moving this to TypeScript. And it was like, no, I think this works. Python works great. And we kept it at Python. But then I had another thing that I was doing in, uh, in, in C\# and it was on .NET framework. And, uh, I thought it would just be fine on .NET framework.

[00:21:49] **Scott:** It said, no, no, we should move to .NET 10. Here's 10 reasons why. And it, it's a back and forth. I think too many people are trying to vibe code stuff in two or three shots while I'm doing stuff in 50 or 60. And having ongoing conversations, like I'm using, I've got, I'm, I'm gesturing right here. People can't see to my terminal, which has 13 tabs open and they're all doing something right now.

[00:22:13] **Scott:** And I use copilot, CLI, which is like claude code. It's a, an agent loop and it has infinite sessions. So it has this idea of like, that, that, that the context of like how long it can think about stuff. It doesn't exist in, in copilot cli. So I can just go dash, dash resume and pick up stuff I worked on a week ago.

[00:22:32] **Scott:** And it's like a hibernation, I just hibernated the agent, I brought it back. So it's remembering all the stuff and all the decisions I've been making on, and I'll say stuff like, you know, revisit our conversation from a week ago. Do you still think that's true? You know, go and look at this poll request. Go and look at the stack overflow.

[00:22:49] **Scott:** Go and look at this new tweet that someone that Simon Willison said. And given that new context, what do you think? So I'm constantly challenging it. Uh, and it's almost like I've got 13 engineers that are either working full time or they're just asleep and I wake 'em up and I ask 'em a question and then I go off and I do my thing.

[00:23:08] **Scott:** And it, it's really been like, I feel like an engineering manager with a lot of really cool little junior engineers with so much energy.


## Verify LLM's assertions with tests (Fear Driven Development)

[00:23:16] **Jeremy:** And for someone who isn't super familiar with the domain or with the language they're working in. How do you verify the assertions that the LLM is making? 

[00:23:29] **Scott:** I love that. I love that. So, because I'm not an expert in Python, but I wrote my blood sugar management system in Python.

[00:23:36] **Scott:** However, I am an expert in type one diabetes. So I thought to myself, how can I verify that this is valid, but I don't know the language? And it's, um, what I call fear-based development, right? It's FDD, fear driven development. I don't wanna screw this thing up. It's my blood sugar. And in the words of Bryan Lyles test all the fucking time, right?

[00:23:59] **Scott:** Always. So how many tests do I need before I don't feel scared? Uh, in this one here, it ended up being 270. That's just a number. But like, I needed about 70% code coverage across almost 300 tests, and it's on real data and it works. So that. That's CICD and it runs in GitHub actions and it runs locally. It does nothing until it tests.

[00:24:23] **Scott:** And I would again argue that that's about software engineering, not about Python. So as long as there's a test framework and a loop and that loop is verifiable, that's what's important. 'cause everyone's excited about like Ralph Loops, which we should talk about at some point. Ralph loops are great, but like if you have a million monkeys and they're typing in a million typewriters and you're hoping that they're gonna type Shakespeare, if you don't have a test that validates the Shakespeare, then you're just wasting monkeys and wasting typewriters.


## Write a few tests as examples and have the LLM write the rest

[00:24:52] **Jeremy:** And these tests, are you generally writing them yourself or is this something that the LLM is also writing? 

[00:24:59] **Scott:** So I will write four or five tests myself. Then I'll tell the LLM say, write me other tests on the boring stuff, like edge cases. And then, because we know that in software engineering, uh, one of the big problems is naming stuff.

[00:25:14] **Scott:** What, what the, what are the top, the top three issues in software engineering is naming stuff and off by one errors.

[00:25:19] **Scott:** So that's, that is, uh, the things I watch for. I know that it's edge cases, so I'll write a test. I'll have it, make me 10 more, and then I'll look for all the edge cases. And yes, it's true that I haven't deeply validated them.


## The code is your responsibility even if an LLM writes it

[00:25:33] **Scott:** And it is true that depending on the model you use, it'll comment tests out, it'll hide stuff from you. It'll pretend it'll, it'll, it'll gaslight you into thinking the tests work. And this is why it's so important that you understand, not you, but one, understand that you are, you are shipping this code. Like I always think it's funny when someone puts something up in the cloud and the cloud goes down and then they're mad at the cloud provider. Like, I get that you're mad at the cloud provider, but like, whose responsibility is it for that app is your responsibility? If you felt that strongly, you should have had it in two cloud providers, right?

[00:26:07] **Scott:** So if this thing fails, it's me. It's a hundred percent me. I'm not gonna blame copilot or Claude or whoever wrote that code. That's why when you check stuff in to GitHub, it says on behalf of, right, if, if I did something and my proxy did it for me, it's the buck. Buck stops here. So if this were production, production production, I would go in and double check it.

[00:26:31] **Scott:** And that's why like for example, the copilot CLI team, it's like seven or eight engineers and they're doing like, you know, 200 PRs a week. It's crazy. They're spending more time now reviewing than they are, writing code, but they will not ship slop. And if you look at another way, and I'm sorry I'm talking so much, but another way to think about it is when open source started and the open source supply chain started having all this flood of open source software, how do we deal with this?

[00:26:56] **Scott:** Code came from somewhere into the machine. Doesn't matter whether Jeremy wrote it or whether some kid wrote it and it got in via PR or whether an LLM code, it has gotta go through the same verification loops, the same security loops, the same testing loops, the same provenance loops, the same governance.

[00:27:14] **Jeremy:** Yeah, that, that makes sense to me. I mean, something that you sometimes hear people say with all these tools, the agents, the ability to generate code, they're saying, well, I am generating so much, I just don't, I just don't have time, or I just don't need to verify the output. And it sounds like in your case you're saying no.

[00:27:37] **Jeremy:** Ultimately, even though these tools are generating it, it still comes down to you need to review it because otherwise you don't know what's going on. 

[00:27:45] **Scott:** If I don't have time, then what are you making? Right. Like the point is to make a thing and ship a thing that you're proud of, so then you don't, ha we gotta go, we gotta go.

[00:28:03] **Scott:** Well then you don't care. You don't care about your customers, you don't care. Like, you have to understand the semantics or what are you even doing? I, I, I don't, I don't, I I just reject that. If it, if it's, now that said, there is this rise of toy fun personal apps, like using computer science history. To put this in context, it's, we're having a GeoCities moment, right?

[00:28:29] **Scott:** Where everyone's just making stuff. You know, there's this wonderful, uh, friend of mine on TikTok, named Rodney Norman. He's a comedian. He's got like crazy white hair, like the guy from like, like Professor Brown, and he's got a big, long beard. And he pops up on my for you page and he says, you know, you can just make stuff.

[00:28:45] **Scott:** You can just do stuff now. Yeah, that's what it feels like. I got a rocket ship strapped to my back and I'm just making stuff. That doesn't mean I'm gonna go and plug Stripe into it and start taking money for it and like taking people's money in real, real blood sugar. Do you see the difference? You, if you're shipping this, you better care if you're, if you're just playing Yeah. Play.

[00:29:05] **Jeremy:** Yeah, I mean, colloquially, right? People are saying, I vibe coded this 

[00:29:10] **Scott:** I don't say that anymore. If I vibe coded it, I don't care. You either are a vibe coder or you're an AI augmented software engineer, ai, augmented software engineer doesn't have good mouth feel, but like, bro, it's just vibes.

[00:29:23] **Scott:** No, I'm not vibing into production. That's not happening.

[00:29:27] **Jeremy:** Yeah, I, I think that's a good distinction to make too, where you were saying there's a lot of things that people are making just for fun. versus the things that people are, are relying on. And, to make something that's just a toy, that's just something neat for yourself. Um, may, may, maybe you don't need to look.

[00:29:48] **Scott:** Yeah, it's cool. 

[00:29:49] **Jeremy:** But if you're shipping a product, then it's ultimately it comes down to you and you really should be looking at what the code is.

[00:29:59] **Scott:** Have you ever heard of the, the Chinese room thought experiment?

[00:30:03] **Jeremy:** I have heard of it. Yeah. 

[00:30:04] **Scott:** Right. So like you imagine that you lock, I don't speak Chinese.

[00:30:08] **Scott:** You lock me in a room and I could be there for an infinite amount of time. You poke Chinese characters underneath the door, and then I poke Chinese characters out. And at some point in the future, through reinforcement learning, I will eventually either learn Chinese or I'll learn how to at least make the person on the other side of the door think that I know Chinese.

[00:30:30] **Scott:** So then the question is, if I can communicate with the person under the door, do I know Chinese? That's A thought experiment. Now, the people who made that experiment, they don't see a difference between that, but I do. Just because it passes all the tests doesn't mean it knows how to program. Right? Like you go to your mom's house and she's got a parrot, and your parrot's like, Hey how's it going Jeremy?

[00:30:51] **Scott:** You're like, oh my God, the parrot's so smart. How does a parrot know English? Right? Parrot starts swearing. Parrots, swearing, because your mom swears, right? Or the parrot who person who owned the parrot before, but the parrot is not smart, it's just parrot. So yeah, same thing. If the parrot starts coding python, I'm not gonna trust that parrot and then take parrot code and put it into production.

[00:31:13] **Jeremy:** Yeah, and I, I think too, what people may run into is whatever they build may look like it works initially, but there may be. Architectural problems that make it difficult to change, there could be more severe flaws that you just can't find because you don't know enough about what's happening. 

[00:31:31] **Scott:** You don't know what you don't know.

[00:31:33] **Scott:** And the first database migration or like the first scale issue and you're like, oh, we made a decision. Well actually we didn't make a decision. The ambiguity loop punted on a decision and now we're painted into a corner, an architectural corner.


## Windows Live Writer port

[00:31:48] **Jeremy:** So I think one of the things you mentioned is when you work on a project, it sounds like you, you have this plan or you have a lot of context that you're providing to the, the model. To start off, can you kinda walk through what are the kinds of things that you're, you're saying like, are you asking for specific architecture patterns, languages, ways to test that kind of thing? 

[00:32:16] **Scott:** Lemme think. Trying to think of an example. I'm looking at my tabs that are working right here. Okay. Here's one. So there's an application that is 20 years old.

[00:32:24] **Scott:** It's called. Windows Live writer. It's a blogging tool that we, and Microsoft released it in like 2006, and then we open sourced it later, and it's a mix of C\+\+, C\#, the ribbon control from office. the Internet Explorer, like the actual typing the blog post is actually the, a COM object from Internet Explorer and like it works, but it's janky and it needs to be modernized, so it's like 20-year-old software.

[00:32:52] **Scott:** That's an interesting technical problem because it's a, it's a brownfield tech pile of stuff, but I have a vision that we could get that running on .NET 10, which didn't exist with chromium or web A, you know, like WebView2 instead of Trident, which is the Internet explorer thing, we could update the ribbon control.

[00:33:11] **Scott:** Like you, you, I can see you're nodding. You're already getting, the spec is already in your head. So then the question is, how specific do you, do you express that intent to,to something like this? And arguably there's, there's gonna two ways to do it. There's the, the, the persistent loop, the Ralph loop, which is just like, do this make no mistakes, right?

[00:33:35] **Scott:** And, and, and then it just, like, that's just monkeys slapping, but verifiable loops with persistence. Is really, really interesting. So how do you verify that it works? What's changed contextually since this thing came out, 4K monitors happened, that wasn't a thing 20 years ago. Multiple DPI across multiple monitors.

[00:33:56] **Scott:** So like I know that that's a thing, so I put that in a spec. .NET is cross-platform, but this is a Windows app, so I'm not trying to get this thing to run cross platform. So that goes in the spec, it's C\+\+ and it uses COM. Uh, but I don't really need COM anymore for this because I'm gonna be switching over to Chromium.

[00:34:12] **Scott:** So I'll make a COM to JavaScript Bridge. Those little moments, make that loop, which, you know, I could have probably pointed a loop at it and it would fix it at some point, but it saves time. These are all these little architectural shortcuts where I'm anticipating that this is important or that's important. It found a, it found a reference to MySpace 'cause it had like an insert MySpace link.

[00:34:34] **Scott:** So like I said, go through the thing. If there's plugins for dead services, mark them as to-do keep track in the to-do of all the things that you've stubbed out, et cetera, et cetera, et cetera. I think I ended up basically dictating to the thing about a two and a half page spec, and I think we looped, I wanna say 20 times and it's running like it freaking works.

[00:34:59] **Scott:** Um, I'd say it's probably 70, 80% done and, and then now people are doing PRs against it and we've, revitalized this 20-year-old application. The question is, could we have done it by just saying, get this running on Windows. I think that the reinforcement and the, uh, that, that we, we would give a, an LLM to do that would be artificial because it doesn't know what success looks like.

[00:35:25] **Scott:** It might just say, oh, I got it running. But like, did you get it running? Did you post a blog post? Did the blog post work? Did you edit the blog post? So you gotta kind of think like a tester. Remember back in the day when like software testers were like, that was an actual job. It's a job again. So I feel like I'm talking to this engineer that's, you know, overseas or outsourced or insourced, and they're throwing code at me and I'm validating that code.

[00:35:51] **Scott:** So I make a plan that's about 80% of a plan, and I tell it, if you have questions, ask if you're making an architectural system, architectural decision, ask. And if there's a lack of clarity or the loop is unclear, then I will come up with a solution. Another example actually, because it's a Windows app, how's it gonna validate?

[00:36:11] **Scott:** Does it take a screenshot? Uh, does it like do debug got here debugging? Does it do interactive debugging? Those are all interesting things that are happening right now as well because it can't see unless it's multimodal. Like something like, um, like copilot CLI, I told it to take screenshots and compare it to the other one and see how close it was.

[00:36:33] **Scott:** So there's, there's anything you can do to make the plan clearer and make the loop tighter will, will cause it to be more successful.


## Defining success and giving tools to the model to verify (Debug View, screenshots to compare)

[00:36:40] **Jeremy:** And when you refer to these loops, I'm assuming a loop is the model attempting to write the code to accomplish what you asked for? Is it automatically looping on itself and it keeps trying or is it where it's prompting you and going like, okay, I, I gave my first try. Time for you to review. 

[00:37:02] **Scott:** That's a great question. So with this particular application, which is trying to bring back an old Windows app, it would get it to compile and think that was success. So I think no running it is success. So then it gets it running. It looks at the process tree and says, look, it has a PID. Success. I'm like, no.

[00:37:20] **Scott:** Well, it has to look good. Oh, okay, well then, and then you can kind of start upleveling. And then I realized I was running this app called debug view, which is effectively like the windows debug, spew kind of thing. And I was selecting the, the, the got here, debugging the debug right lines and pasting it back in.

[00:37:36] **Scott:** And after the third or fourth time, I'm like, it can run it. It then asks me, what do you see? It literally would, what do you see in the debug view? And I would copy paste it. I'm like, this is stupid. So then we made debug view an MCP server. Now I'm out of the loop, so I actually got myself out of the loop.

[00:37:54] **Scott:** So now it can compile, run, see the log, kill the PID build, and then the inner loop becomes simpler. So then I said, let me know and stop the loop when you have questions or you think you're done. And that's what's so kind of exciting about these, these loops is if they're clear and success is clear and verifiable, you can do really amazing stuff.

[00:38:20] **Jeremy:** So it sounds like as a part of your instructions, you're also giving it the tools. You're telling it how it should verify whether it actually did the thing. 

[00:38:31] **Scott:** Well, um, so like, I'm making a Windows Clawd bot now, now mot Malt bot, uh, windows Tray application. And, it declared success just right before we got on the call and it's like, yeah, it's working, it's great.

[00:38:44] **Scott:** And I looked at the tray and it says, connecting. And it's not connecting at all, right? It's completely. And I'm like, no, this isn't working. And it's like, no, no, it's working. I can see it's working. Look. And it shows me all the, it's very excited. And it's like, oh, and it's giving me rocket ships and an emoji.

[00:38:57] **Scott:** It's super excited that everything is, is working great. And then I realized that the UI is done. But the underlying stuff is not done. So I need to separate the UI from the business logic, build the core, which is much easier with these loops. So then once I get it, talking to the API, so it was my own mistake to tell it, you know, build this and I went UI down.

[00:39:23] **Scott:** That was foolish of me. It was, it was my own enthusiasm that that nailed me. So now I'm gonna go and refactor it, pull out the core, build the windows front end to the thing, get it connecting, and then layer that UI on top of that. 'cause that's way more verifiable.

[00:39:39] **Jeremy:** Yeah, I think it's a common experience with people who use these tools that there are times when they're, they're in a loop or they're, they're trying to come to a solution and each time they try, it's just not what you wanted or it's, it's saying it fixed it, but it really didn't, and. Are there specific strategies you have for, I guess, one, recognizing you're in this, you're, you're caught in this loop, it's not gonna get out. and how do you break it out of that, that cycle?

[00:40:12] **Scott:** 


## Models get caught in a loop when they are confused about what success looks like

[00:40:12] **Scott:** For me, it's always been that it is confused about what success looks like. You have to remember that an intern or a enthusiastic early in career engineer is very excited to be at the company.

[00:40:25] **Scott:** I'm so happy to be working with you, Jeremy. I'm gonna do whatever it takes, lie, cheat, steal, comment out tests in order to make sure that you don't fire me. These are reinforcement learned, large language models that are very, very excited to be here. And as such, just like, you know, the Devil Wears Prada, the, the interactions that they're gonna have with a salty old engineer like me are gonna be very interesting.

[00:40:49] **Scott:** Like, I guess I'm Meryl Streep in this, in this, uh, analogy, so I need to be very specific. Okay. Jeremy, I need you to do this. I need you to do it nicely. I want a half double decaffeinated, half calf with a twist of lemon, not two twists. You know what I mean? So you're, you need to be a little bit crisp with it.

[00:41:08] **Scott:** If you can give it test data, if you can give it verifiable test data, if you can say, build a harness, if it doesn't know what success is, it will make up success. Declare success. And then if you're not, whatever enough, senior enough, awake enough, to declare success and agree with it, then you're gonna get nailed.

[00:41:28] **Jeremy:** Yeah. And in the example you gave before, you had to tell it specifically to use this debug view tool and, and, give it that tool through the MCP server 

[00:41:40] **Scott:** And how would it, how would it know? Right. You gotta tell it that you have these tools available. It's gonna take a regular screwdriver and keep poking it into a Phillips screwdriver thing.

[00:41:48] **Scott:** It's like you got a Phillips right there, bro. Oh, you're absolutely right. I actually, I, I, I dunno if I can't show you 'cause we're on a audio podcast, but literally yesterday, I, I forgot that I had a whole test harness for my blood sugar thing and I had like another a hundred tests that I hadn't told it about and it was frustrated about something and I was like, oh, you know, go into this folder, I've got these tests.

[00:42:09] **Scott:** And it literally said, this is gold. Thank you so much. Now I see. You know, and then I was another totally unrelated thing, I was building a, a front end for, for Microsoft Loop. 'cause I wanted to like loop is like notion and I was building an API for it and then I found API documentation. I just paste it in, here's the URL for the documentation.

[00:42:29] **Scott:** And it was like, ah, now I have a plan. So it's just like giving it like a little breath of fresh air and it's like, ah, and now I'm re-energized. That's what these, these loops require. Ambiguity loops require specificity. That's what we are supposed to provide as software engineers.


## Context compaction, telling model when to remember things, writing notes for the model

[00:42:47] **Jeremy:** And as you have these longer loops or conversations, one of the things about these tools is they have, they have a context, and that context is only so large. And I, I wonder if you ever run into the issue of, I believe they call it context compaction, where eventually 

[00:43:07] **Scott:** Yeah. 

[00:43:07] **Jeremy:** The model has to kind of get rid of some of the, the context that you had before and, and if you've run into that and how you deal with that. 

[00:43:15] **Scott:** Yeah. So I just put in context here. I'm 73% into a 200,000 token context window. That is often a thing in these loops where it's, it's talking to you and it's talking. Then it kind of goes, huh, what? Oh, um. I don't remember, bro. What? And that's because it just compacted everything. Summarized it.

[00:43:38] **Scott:** And it doesn't remember an hour ago. That, happens a lot on these tools. It happens less so with, um, the infinite sessions that GitHub copilot CLI has because it does very, very active management of that window. But I've also, with any tool, found it to be very helpful to keep telling it, to save stuff.

[00:43:58] **Scott:** And I don't like to anthropomorphize these things. They're not people. But I have a context window and I also have a remarkable e ink, thing. And I sync to paper, like tell it to write stuff down as if it is a person. So, um, this big loop that I'm running on the, on the, on the Claude Bot over here. I said, every time you achieve something, write it down.

[00:44:22] **Scott:** And if you look at things like Steve Yegge's beads, uh, which is basically like a git focused to-do list that's distributed across multiple agents that are working on a swarm of problems. If everyone can agree on a ledger of the things that we're working on, those context windows matter less because if it wakes up, it's gonna go and say, what, what am I doing?

[00:44:44] **Scott:** What was I working on? Just like the movie Memento, when he forgets stuff, he tattoos it all over his body. He wakes up in the morning, he doesn't know who he is, and he gets caught up by looking in the mirror and seeing all the tattoos. So anytime anything interesting happens in his life, he tattoos it on himself to catch himself up.

[00:45:01] **Jeremy:** Do you ever end find yourself doing that manually where you yourself know what the context should be and you just go, here you go. Like this is, remember all this, or, yeah.

[00:45:12] **Scott:** Yeah. So. Context window management is not something I have been actively doing with the copilot CLI because of the sessions feature, but I still think it has a huge amount of value because it's not about their context, it's about your context when you Jeremy inherit the code later.

[00:45:27] **Scott:** Like for example, DPI, we were having a dots per inch issue with the open live writer and it was complicated. Like I spent a day messing around with DPI 'cause multi DPI multiple monitors is complicated. So I said, write down everything that we've learned so that no one has to ever deal with this again.

[00:45:44] **Scott:** And it made like a two meg, you know, mark down file, like it effectively wrote a chapter of a book about nuance and I'm running the Clawd Bot now, molt bot on Windows under WSL. And you know, every once in a while a Windowsism will come in and I said, regularly check for Windowsisms and remember it so that you never hit it again.

[00:46:06] **Scott:** And that's not thinking about the larger context window, that's just like put a post-it note on your monitor to remind you of this. And with any project, I'll end up having 10 or 15 of those that are secondary to the main plan. The main plan could be in, in something like beads, or it could be in GitHub actions, or it could be a markdown file with check boxes.

[00:46:30] **Jeremy:** And, and these, the main plan 

[00:46:33] **Jeremy:** and these additional notes that you provide, is there a way that consistently works across whether it's, GitHub co-pilot or it's Claude code or Gemini CLI Is is there like a, Hey, this is the markdown file you put it into, and all these things will understand it? 

[00:46:52] **Scott:** They're, they're all fighting right now, uh, about what the thing will be called.

[00:46:56] **Scott:** You know, like there's AGENTS.md and there's Skills md and like, um, you know how there's like a robots text, which is like the thing that your web browser, your website puts up in order to tell robots what to do. And then there's vLLMs.txt, which is literally a text file you put on your website in order to like tell OpenAI or whoever's scraping your website what to do about it.

[00:47:19] **Scott:** If you have an AGENTS.md, it's like a read me for agents. And then within that I'll say there is a docs folder, and within that docs folder here are the main subsystems and you're effectively building architectural context. And then if it finds itself doing a thing, then it will go and refer to the documentation.

[00:47:39] **Scott:** So I taught the Claude bot about my blood sugar, which is unique to me. Anytime I mention anything blood sugar related, it doesn't have to hold it in context. It just has to know, oh, there's a Post-it note with the details that I need to know, and then it pages it in, does the thing, and then it pages out.

[00:47:58] **Jeremy:** Something you mentioned earlier was you were referring to this Ralph, loop 

[00:48:02] **Jeremy:** What, what is that?


## Ralph Wiggum Loop

[00:48:03] **Scott:** Yeah, yeah. Oh, I'm sorry. So Ralph Loops are fun. So Ralph Wiggum is a character on The Simpsons, and he is a extremely naive and extremely persistent, funny little man. what we admire about Ralph is that he is persistent and he will never give up.

[00:48:24] **Scott:** And it is, designed for these continuous autonomous development cycles. And Ralph Wiggum um, the concept was, came up with, uh, a gentleman named Jeffrey Huntley, and he's basically trying to, do less, and this is a thing that I think we need to acknowledge as programmers, that we are ultimately very lazy.

[00:48:44] **Scott:** So if it can be automated, that's a good thing. So he's like, why am I doing this work? Let Ralph, let Ralph do it. So the Ralph Loop kind of embodies the spirit of this little character and the Simpsons, which is, I'm gonna stubbornly iterate, I'm gonna fail, but I'm never gonna give up until it succeeds. So a really great example of a Ralph Loop is not necessarily like, like the, the tech journalists will say, oh, you can just point it at some software and it'll clone it, and it, it will make like a Minecraft clone.


## Using the loop to reproduce bugs in GitHub issues

[00:49:15] **Scott:** It's not gonna be real, right? But, David Fowler, distinguished engineer in .NET had a really interesting problem where he had 400 issues in his GitHub repo for, uh, an application. And, it didn't have good reproductions of the bugs. And that's just one of those things. It's just technical debt and it, we don't know if they're bugs.

[00:49:36] **Scott:** It could be good bugs, we don't know. So he made a Ralph loop that said, spin through all 400 of these issues and reproduce them. If you get a good reproduction, keep track of that reproduction, then add that context to the issue. That is the very definition of toil and like what better thing than a Ralph loop to do that?

[00:49:57] **Scott:** And I think it came up with something like 384 good, solid repros. Right now the big problem with a Ralph loop is that it doesn't have like a task tracker. So that's where things get interesting. If you have a task list. And Ralph can then keep track and understand what success looks like, then you're gonna have a great experience with it.

[00:50:20] **Scott:** So I will do interactive work during the day, and then as I get towards the night, I'll be like, okay, what's a loop that it could work on overnight? Because I wanna wake up in the morning and have something successful happen. And it's also, uh, it sounds wasteful, but it's like shockingly cheap. you know, I'm a bit of an AI vegan, I don't do images and I don't do video.

[00:50:44] **Scott:** But next token prediction is becoming extremely inexpensive. And you could run a loop all night long and it might cost you like two bucks. So, if you have a problem that is Ralph Loop shaped. It can be an extremely powerful tool. I think though that people sometimes, uh, think that it is the only thing, or they'll take like vibe coding is fun to say.

[00:51:07] **Scott:** And now Ralph Loop is fun to say, but it's just another technique. It's another tool like, like CI/CD.


## It's a while loop that keeps reprompting the agent until success is reached

[00:51:15] **Jeremy:** And is this where people have, have built this, I don't know what you would call it, this harness that is going to manage and run the loop? 

[00:51:25] **Scott:** Well, so Jeffrey Huntley calls it a while true bash loop. So it's just like, while true. Uh, but you know, and the concept is very simple.

[00:51:33] **Scott:** It reprompts your agent a set number of times with the same prompt. And we mentioned before that it's an ambiguity loop. And if you ask it something a hundred times, you're not gonna get the same result a hundred times. And then you refuse to let the agent say it's done. But you have to identify what the stop condition is.

[00:51:57] **Scott:** And if the stop condition is unclear and it's done anything at all to try to wiggle its way out, you say, no, do it again. Like for example, all tests must pass, endpoints must be working, and then if it comments a test out and you can't comment, you can't change the tests or whatever, right? So you'll say, slash Ralph loop refactor this to whatever, and it all has to pass.

[00:52:22] **Scott:** And you have to go and say step, step, step. And when it's complete. When it's complete. When it's complete. But if you don't have a clean, if it doesn't have the ability to see something, if it can't see a log file, if it can't run a test, then that doesn't work. So that's why test harnesses matter so much in that context.


## Can use multiple models in the same loop

[00:52:38] **Jeremy:** So you're basically building your, your own while loop with a known stop condition that's going to call out to your, your model of choice. 

[00:52:48] **Scott:** Yes. Yeah. And, and then you can also mix and match models. So like, I'm on, I'm on copilot, I'll hit /model, I hit enter. I've got 14 models, so I might, you know, plan on Opus and if I wanna save money, I might then do the work on sonnet and then I'll have GPT 5.2 Codex review it just to kind of like mix it up.

[00:53:10] **Scott:** Um, you know, diverse teams are, are, are a good thing. So, uh, having only one model do it and then review it. Sometimes you can get a little bit of sycophancy. Um, it's nice to, to get fresh eyes and a way to do fresh eyes is throw another model at it so I can switch models, mid-conversation.


## How much does this stuff cost?

[00:53:28] **Jeremy:** And when you had mentioned it's cheaper than, than people think. When you said it costs $2 to run overnight, what, what model is that? Or, or in what case 

[00:53:38] **Jeremy:** is it that cheap? 

[00:53:39] **Scott:** So the, um, I run all these different tools. I've run, I run AMP and I'll run Charm and I'll run Toad and I'll run copilot CLI, and I'll run Claude on this machine over here that I'm gesturing to, to my right.

[00:53:51] **Scott:** It's got Claude code running, and on this machine here, I'm using GitHub copilot, CLI, um, I've got a Pro Plus account, when I select the models, it says, this is an expensive model. It's like a 3x model. So it uses so many premium requests. This other model like Haiku is a, uh, a one third model, which means I can do three times as many requests for the same cost.

[00:54:13] **Scott:** And, with my Claude Max subscription. I can estimate the amount of dollars that I spend a month, like 200 bucks versus how much I'm spending versus that, that day. And it might be two or $3. If you use a free tool like AMP code that's advertiser supported, they'll tell you the number of dollars that they're using.

[00:54:32] **Scott:** And then in any of these, you can go and say /session. And I can see I've used 63 premium requests and I've been in this session, this is a, a copilot session. I've been in this session for 133 hours. Remember I mentioned that idea of infinite sessions and I've used Claude, uh, Opus and it's used 64 million tokens.

[00:54:53] **Scott:** And that's within the context of my GitHub copilot account. And this stuff just gets cheaper and, and, and faster. And there's even local models, of course you could do that won't be quite as sophisticated, but if you wanted to do this work in airplane mode, you could do it as well.

[00:55:08] **Jeremy:** So if you take that example, you said it's been running for 133 hours. It's using claude's opus model. What's the, does it have like a dollar dollar amount attached to that?

[00:55:18] **Scott:** It doesn't have dollar. They use, everything's about tokens right now. And I think that we'll see the industry start moving towards tokens as a thing. Like, you know how, I don't know if your parents are technical or not, but mine aren't. But they know that five gigs is enough for their phones and I know that five gigs is enough for my phone for the morning, right?

[00:55:38] **Scott:** So like, you know, you, you get your Verizon or your T-Mobile and you say, I got 50 gigs and I got unlimited gigs or whatever. Token based pricing I think will be one of those things. And, you know, when you're running cloud code, it's got a little progress bar that's telling you how many tokens you have.

[00:55:54] **Scott:** That's, that's gonna be a, a thing. So just like people associate the number of gigs a month they use, they'll start associating the number of tokens. So it's less interesting to say it costs two bucks, but it's more interesting to say, well, I paid for a hundred million tokens and I'm halfway through the month.

[00:56:10] **Scott:** And I'm, you know, doing fine. I'm on pace to not use up all my bandwidth in quotes.


## Spending and how "one magical moment" makes it worth it

[00:56:17] **Jeremy:** So for your, your own personal projects, what does that that bill look like at the end of the month? 

[00:56:24] **Scott:** Well, so far I spend 200 on Claude and then I pay whatever the co-pilot, pro plus is, and those are the two that, oh, and then I have a subscription to, uh, open ai.

[00:56:36] **Scott:** So that's basically it. I mean, here's the thing, right? If you've, what do you value your time at, right? If, if you, if you just pick a number like a hundred dollars an hour and you say, my time's worth a hundred dollars an hour, which is a big number, and one magical moment once a month saves you a hundred bucks an hour.

[00:56:53] **Scott:** Like, you're like, oh my God, yes, I would, I would do that. it has definitely brought me more joy than Netflix. And the Netflix is 11.99 or whatever it is. All it takes is one amazing moment and you just go, oh wow, that was, I just paid for the whole thing.

[00:57:14] **Scott:** You know what I mean? My son just got a climbing gym membership yesterday with his own money. He's 18 and uh, it's $90 a month. And he's like, oh man, this sucks. I climbed for two hours, it's $45 an hour. And I'm like, no, dude, climb four hours a week. It's $16 an hour, it's five bucks an hour. And he's like, oh, my, my son.

[00:57:34] **Scott:** He is like, bro, you're right. I need to climb more. Like yeah, the more you use it, like the better dude. So like I'm, you know, what is it here? Copilot Pro plus is like 40 bucks and you get 1500 premium requests. And I've used, how many have I used here session? I've used 63. Right, and I've upgraded, I've upgraded open live writer

[00:57:59] **Scott:** it's not even, it's not even close. So yeah, I'm not, it's just, it's so valuable that it is a delight. So I honestly am not, I'm not thinking that much about it simply because, like I said before, I've got a rocket ship on my back. I'm getting, I'm busting out so much cool stuff and people might say it's a toy, this thing's a toy or that thing's a toy.


## Building projects you normally wouldn't have had time for

[00:58:20] **Scott:** But like there are toys that I was meaning to get to. Like I've got a podcast as well, you know, it's been going on for 20 years, but it's never had a backend admin site. I'd just been editing text files and like manually editing databases because I was like, ah, who's got a weekend to make a (pod) I don't wanna make a (pod)

[00:58:40] **Scott:** It took me 43 minutes to make a React website that does the backend admin for my podcast. That's worth, that's worth whatever my subscription is. So, Yeah. 

[00:58:52] **Scott:** Did not take, did not take any time at all to make that decision.

[00:58:55] **Jeremy:** Yeah. I mean, I think as developers, for whatever reason, a lot of us, we, we undervalue paying for tools.

[00:59:03] **Scott:** Oh my God. Developers would just love, like, I'm $99, never. I'll write my own, take nine hours to do it. You know what I mean? So, yeah, like, I mean, I'm sure that these, these AI companies are burning money and the pricing will figure itself out. This is just like when Netflix and streaming started and they couldn't figure out what the pricing is.

[00:59:22] **Scott:** But they're all trying to figure it out. And it's also gonna get faster. It's gonna get more environmentally friendly. We'll have more hybrid models, we'll have more local models. I can plug in Llama, I've got a 4080. I could do work on work locally. There's lots and lots and lots of options and it's only gonna get easier and, and, and hopefully cheaper.

[00:59:40] **Scott:** And that's important as well. I want this to be available like for everyone.


## Local models are not as good

[00:59:46] **Jeremy:** Yeah. One of the things you mentioned is that there are models you can run locally. 

[00:59:52] **Jeremy:** What's the, the state of that? How do they compare to the, the ones that you pay for from cloud services?

[00:59:59] **Scott:** It is challenging to get really good, deep, thoughtful plans from those local models, but if you have a good plan that was made by a big cloud model, you can then execute on that plan with some of the smaller ones.

[01:00:14] **Scott:** I think though that people don't realize that, these models in the cloud know more than just coding. They could go and translate Star Wars into Shakespeare, but I don't want that feature. Like, I don't need that. So when I download a model, I would like a Python optimized model that doesn't know how to do anything but Python.

[01:00:35] **Scott:** It doesn't, I don't care. It, it shouldn't have. How tall is Brad Pitt? Embedded in the model that's wasting space. So I think we're gonna see local models that are very specific and you can go on hugging face and find llama coding models, deep seek coding models that are specific to programming, specific programming languages or problems that I think would be really interesting, like save money, time and energy by solving it locally.

[01:01:02] **Scott:** Think of it as like a Redis cache for LLMs, but locally.

[01:01:07] **Jeremy:** Yeah. I, i, I also wonder, because there's so many things in these models, how much of that knowledge actually helps it code? 

[01:01:17] **Jeremy:** Because, you know, we have knowledge 

[01:01:19] **Scott:** don't That's a great 

[01:01:19] **Scott:** question 

[01:01:19] **Jeremy:** Outside of coding.

[01:01:21] **Scott:** They all know how tall Brad Pitt is and they insist on bringing it with me, you know, everywhere I go.

[01:01:27] **Scott:** But, um, a really fun way to test this is to just go and download like LM Studio or LM studio.ai. It's a delightful application, third party app, um, or, uh, you know, Foundry local or ollama. And then just throw a couple of problems at it. And if you like the answers, then maybe you can do some coding on an airplane.


## Restricting agent access to your computer (Tool, URL, Path)

[01:01:49] **Jeremy:** One thing we haven't really talked about is these agents or this ralph loop. I believe in a lot of cases it has full access to your computer. Is that, is that correct?

[01:02:03] **Scott:** That is 100% up to you. So, for example, if I were to fire up copilot, CLI or Claude in a, a folder on my machine, if I just made, you know, C:\\temp\\Jeremy\\Copilot, it'll say, do I have permission to open this folder?

[01:02:22] **Scott:** That's the same thing that you get when you open it in Visual Studio Code and it's like, do I trust this? Are we cool? No. So that's preventing it from accessing that, that data. So there's basically three things that a agent can do. Can it access a URL, can it access a tool or can it access a path? So by default it gets no tools, no paths, no URLs.

[01:02:45] **Scott:** And then every single time in a session it will ask you, can I do that? And it can be very annoying. And you say, yeah, you know, I'm gonna write a, you know, website for Jeremy, go and, uh, do this. And it'll be like, oh, can I, can I Google for stuff? Uh, yeah, go ahead. Fine. Okay, now I have access to Google. Um, okay, cool.

[01:03:04] **Scott:** Can I write the HTML file to the disk Is that cool? And it'll show you what it's about to write, and then you say yes. And then at some point you'll say, well, yeah, you can just write to the disk for the rest of the session. We're good. Stop asking me. And then you build up this knowledge base of what it's allowed to do and what it's not allowed to do.


## YOLO mode and the agent is running as you, so if you are an admin it's an admin

[01:03:20] **Scott:** What people are starting to do is they just go dash yolo. You only live once if you fire up an agent, --yolo or allow all tools and it's running as admin, it's running as you. So then you bring in things like sandboxes. You could use Windows Sandbox, you could use Docker Sandbox, you could use WSL. A lot of people are really enjoying WSL on Windows.

[01:03:46] **Scott:** And then you can unmount the drive, or you can use Docker and use volume mounting, but simply running it in a container. Isn't security, it's a, it's one layer of security, like a true sandbox. If you're gonna run this like a bank, you're gonna have auditable, governable, uh, layers of what it's allowed to do, what functions, what syscalls it can make, et cetera.


## Not running in YOLO mode while not at the computer

[01:04:09] **Scott:** So I think we are in kind of YOLO mode, but no, by default they do not have access to all of your stuff. But if you ran it in a loop in YOLO and went to sleep, like I've got a, I've got a 3D printer. Do you have a 3D printer,

[01:04:25] **Scott:** Like as a general rule, 3D print, 3D printer, people know not to leave the 3D printer on when they sleep.

[01:04:30] **Scott:** 'cause it could burn your house down. And there's always somebody that ends up doing that and they get spaghetti when they come home and it's just all over the place. And it could, you know, it could cause a problem. So I don't leave the house when the printer's going and I don't leave the house when I have a YOLO Ralph loop running.

[01:04:46] **Jeremy:** But in general, I suppose it sounds like when you are gonna use these tools, you do put it in YOLO mode and maybe hope for the best. 


## Allow all tools and internet but lock down the path and use git if it starts deleting things

[01:04:54] **Scott:** No. Well, if I'm standing in front of it and I'm actively doing it, usually I'll say like, allow all tools, because I know the tools that it has, I tend to lock them down by path. So for example, I'm in, d, GitHub, open live writer.

[01:05:11] **Scott:** It can go ham on anything from there down. Um, it can talk to anything on the web and it can talk to anything from there on that path down. And it can call any tool. I'm sure it could decide randomly to format my hard drive, but it's not running as admin. So that would fail. Um, I suppose it could randomly have a reason to go out and, you know, hit the internet somehow and do something problematic.

[01:05:36] **Scott:** But again, it's working on one specific thing. The loop that it's doing is looking at a log file, running a compiler and doing it. Again. That's different than Clawdbot. Or now called Moltbot which is a, basically Siri as a Ralph loop running on a, you know, a, a server somewhere or running in a, in a, in a background session.

[01:05:59] **Scott:** But yes, you don't know. But, giving it access to like your source code and having, you know, if it deletes it, then I'll just go and git reset and I'll get it, you know, I'll get it back. I've had it do dumb stuff. I've had it, push when I didn't want it to push. I've had it commit stuff and then I just undo and go back to running.

[01:06:18] **Scott:** I always run them in git. I wanna call that out though, like, I always have source control because if it makes a mistake, you back out.


## Agents make mistakes and even close themselves

[01:06:26] **Jeremy:** Yeah, because I was thinking of the example you gave earlier where I believe it was looking at processes and killing 'em and things like that. So to, to me it seems like it must have quite a bit of permissions if it's able to do that.

[01:06:40] **Scott:** Well, so when it runs as you, it has all the permissions that you have. So for example, the loop that I'm running over on this other machine, I, I told it that it can fire up the Windows app, save the PID of the app that it just ran. And it can kill that PID it can kill that process.

[01:06:55] **Scott:** That doesn't mean it couldn't accidentally kill all of the processes. And I have one time, two weeks ago had, uh, Claude code kill itself by doing a stop process. And it was a little bit too, you know, \*.\*. And then it woke up and it's like, what happened? How long? It literally said how long have I been out 

[01:07:14] **Jeremy:** Wow. 

[01:07:15] **Scott:** Which I thought was crazy. Uh, it, it, it literally is like, how long have I been awake, you know? And I was like, just, and I said, check the markdown files, see where you left off and keep going. And it, you know, it picked it up, but it basically bonked itself on the head with its own hammer. Um, and, and that's not a guarantee.


## Telling the model what it can do is not a real sandbox, need to run in a container or isolate it somehow

[01:07:32] **Scott:** So then the question is, is it a sandbox to put in a markdown file? Hey man, don't do that. No, it's not. That's obviously not a sandbox, so that's why running it in a container or you know, running it in WSL or whatever, you know, and that, that's non-specific of any operating system, if you decide to double click on a batch file and it does something stupid, I don't see that as being any different than running an agent.

[01:07:55] **Scott:** The only difference is the ambiguity, which gets us back to the beginning of the conversation. Ambiguity loops are ambiguous.

[01:08:03] **Jeremy:** Yeah, I mean, I could think of an example of if you're giving it access to the internet and maybe it downloads a utility, it think it's gonna help. 

[01:08:11] **Scott:** That, that's a 

[01:08:12] **Jeremy:** Yeah. And uh 

[01:08:14] **Scott:** Download a utility your company hasn't okayed and then suddenly you're in trouble.

[01:08:17] **Jeremy:** Right.

[01:08:18] **Scott:** Yep. Yeah, and I think that the difference between making a toy application that plays with your blood sugar in your spare time and working at a bank are different. So yeah, I would not go running anything like this, you know, in, in YOLO as admin in a bank

[01:08:35] **Jeremy:** Makes sense.

[01:08:35] **Scott:** That said. If it's your machine and you know what you're doing and you have this folder and down, there's a lot of power in this.

[01:08:42] **Scott:** And the nice part about it is that it's a slider bar of good, better, best. You don't have to say it's not, it's not between bother me all the time and yolo. You can give it and you can do this as a team, like the whole enterprise could roll out, here are the five approved tools, here are the six approved websites, here's the SKILLS.md that we're all gonna use.

[01:09:00] **Scott:** We check it all in with the repo and everyone's on the same page.


## Differences between models

[01:09:05] **Jeremy:** I think something you've alluded to during the conversation is you use different 

[01:09:10] **Jeremy:** agents and different models like there's Cloud Code or Gemini CLI or open I AI Codex. Are there specific strengths or or reasons that you use different agents or different models? 

[01:09:26] **Scott:** At this point? For me, as someone who wants to be an educated person that can go on a podcast with you and speak with some amount of. At least opinion, if not a little, tiny bit of authority. I try them all because I'm curious and I wanna understand them. For a lot of people it's just like Honda versus Toyota, like, which one did you like first? Uh, you'll have chat chats with people and be like, oh man, codex is amazing. Like, I get such great results with Codex. And then someone else think next to like, codex is trash and you there, it just depends on how you're talking to it.

[01:09:59] **Scott:** Honda versus Toyota. I, I find that Opus is really good at planning. I find that Sonnet is really inexpensive and really good at executing on a plan. I find that Codex is very slow, but very good at, reviewing code. I don't know if that's true for everyone. I believe that it is true for me. Uh, I'm playing with, you know, Gemini and things like that, so I'm always open to trying new things, you know, like I went to Chipotle for a very long time.

[01:10:28] **Scott:** I was very well known as a Chipotle guy. I have a shirt on right now that literally says, will code for tacos, but now I'm going to Qdoba more and more and more. So, strong opinions weekly held should be your perspective on models and like, I'm here, I just said /model in copilot CLI, and there's 14 models to choose from.

[01:10:48] **Scott:** You can turn them on and off based on what your organization has decided. So I see a lot of models because I have an individual subscription. You might log in and see four, and then you have to go in and turn on the ones you want for your enterprise, decide how much you wanna pay, and then your company might decide, or your CTO might say, oh, we're, we're A GPT shop.

[01:11:09] **Scott:** Oh, we're a cla a Claude shop. Well, with something like Claude Code, you get Claude models with some of the things like OpenCode or amp. You get an auto model, which is another interesting thing by the way. Some people, like you don't actually, when you order an Uber, say I want a Honda, you get whatever comes.

[01:11:26] **Scott:** You might say Uber black, or you might say whatever, but you don't really care that. I think we're gonna start seeing that more and more where it doesn't matter what model, you're gonna have an auto router and it won't say Claude Opus or GPT, it'll say auto, or it'll say Smart, or it'll say fast, or it'll say deep and then we'll do the right thing and you're not gonna worry about it as much.


## Statically typed languages better for LLMs?

[01:11:48] **Jeremy:** I had an interview with Bryan cantrill he's the CTO of Oxide computer.

[01:11:55] **Scott:** Yeah. Yeah. I was on ox oxide and friends. 

[01:11:57] **Jeremy:** Oh, nice. And one of the things he, he mentioned with working with large language models is he thought it was really advantageous to use strongly type languages like say rust, because the model is able to verify when things are not correct, just through that compile step and through the design of the language.

[01:12:23] **Jeremy:** I wonder in your impression, like whether you found that true for yourself. Like are there specific languages that work better when using these agents?

[01:12:35] **Scott:** That is a very good question. I think that is a good opinion by Bryan and as a general rule, I agree with it, but I would argue that in lieu of strong typing, one overcompensates with tests. So correctness is what Bryan is arguing for and that is valid. If I am using Python like I am for my blood sugar thing, having 200 tests make me worry less about how Python compiles or doesn't. With my .NET application, I have fewer tests, but I've got 419, I'm looking at this 419,000 lines of code and it all compiles that. But compilation doesn't equal correctness and strong typing doesn't guarantee correctness. So I would say I mostly agree with Bryan, but if you go back to fear-driven development, if you're afraid of the code, you don't have enough tests. So I write tests until I'm no longer afraid, regardless of language. I would say I am picking the right language for the environment, not picking a language based on whether it's strongly typed or not.

[01:13:48] **Jeremy:** Probably a similar philosophy to when you're writing the code yourself, even 

[01:13:53] **Jeremy:** before these tools.


## Writing more code in languages you don't know but fit the domain

[01:13:54] **Scott:** A hundred percent. Although I am finding myself writing more code in languages that I don't know because it's the right language. Like not everything has to be a, a, a .NET application that's like a complete self-contained cross-platform thing. Sometimes a hundred lines of Python is fine.

[01:14:16] **Jeremy:** Yeah. I think that would be an interesting shift for people because I, I think there does tend to be people who they know, let's say they know JavaScript, so they go, okay, I'm gonna write everything in JavaScript or Node or TypeScript and maybe this this removes some of the, the difficulty in getting started.

[01:14:38] **Scott:** 

[01:14:38] **Jeremy:** Let's say Python as an example, if you're working on something in the machine learning space, 

[01:14:43] **Scott:** Yep. 

[01:14:44] **Jeremy:** Even if you're not an expert in Python, these tools can,

[01:14:47] **Scott:** 

[01:14:47] **Jeremy:** help get you there.

[01:14:49] **Scott:** Well, like the, the, the, the, the blood sugar thing is meant to be a skill that is plugged into an agent. So you put it in, see users, Jeremy copilot skills or see users jeremy Claude skills. So I did it in Python because it's like one file, one markdown file, and one Python file. And you have Python. And I have Python.

[01:15:07] **Scott:** It works. I could have made it a .NET application. It would be larger, it would require a runtime. So that wasn't necessary. So I used Python for portability. Even though I don't know Python, I'm confident that it will work for you and it'll have a good experience. But you know, like I might have, I'm trying to think which one of these is a net application.

[01:15:25] **Scott:** like my, my live writer application, I wouldn't do it in anything but .NET 'cause that's what it's good at. So pick, pick the car brand that is gonna make your trip the most delightful. I'm definitely focused on delight right now.

[01:15:40] **Jeremy:** I think that's pretty good place to end it on, but is there anything else that you think we should have talked about or you wanna mention?

[01:15:48] **Scott:** I just think that it's a funny moment that we're in where people who are craftspeople are worried that the craft will go away. And I hope that it is just that the toil will go away, but the craft remains. I am having a blast. I hope I will be having a blast next this time next year. Maybe we'll chat and see how it turned out.


## Difference in how people think of the tools

[01:16:11] **Jeremy:** Yeah, I think it's so interesting how different people are reacting to these tools. You have some people where it seems like. This is amazing. I'm doing all these things, and then you have some people where it's like, I spend more time just trying to fix all the problems and this is not that helpful to me.

[01:16:32] **Jeremy:** And so there's this big disconnect I feel like, between how people think of these tools.

[01:16:38] **Scott:** Yeah, I think that's okay. Like if you love driving Stick and you have BMWs and you just, the, the joy of driving then don't take an Uber, right? But they're, they're solving different problems. Taking an Uber pick someone up who maybe can't drive, it enables them to do something that they could not do before.

[01:17:01] **Scott:** While driving stick shift around a track for fun at speed is different. So, yeah, I mean, I'm writing, like, I'm writing software for this robot over here. I'm writing software for my Commodore 64. and I'm writing software for Windows and Linux and Mac and, I'm using different tools in different languages in each each one.

[01:17:20] **Scott:** Some are more AI augmented because it matters more or less how much of myself I pour into the thing. But I feel like the result is so far quality software that helps people.

[01:17:35] **Jeremy:** Yeah, I think there's this mix of, for some people it's the effectiveness of the tool for them personally. And then I think there's the other part, like you're, you're describing the, the stick shift example. And I think what people kind of wonder is right now you can still get a car with a stick shift and, and drive it.

[01:17:58] **Jeremy:** And going into the future, if we are a person who wants to manually write the code, we want to craft it in a very specific way. Are we going to commercially still be able to continue to allow to be, do that.

[01:18:16] **Scott:** That is more of an economics problem than a tools problem. I subscribe to Trek economics, uh, which is the science and, uh, economics of Star Trek. It's an excellent book and worth looking up. And the whole point of Trek omics is that, craftsmanship matters. And just because you can say Tea Earl Gray Hot and it pops out of a door, that doesn't mean that you shouldn't make yourself a nice cup of tea sometimes on your own.

[01:18:45] **Jeremy:** All right. you mentioned you have a podcast, you actually have many podcasts. Um, if people wanna check out what you're up to, uh, where should they head?

[01:18:53] **Scott:** Go to hanselman.com, hanselman.com, my last name. If there is a tariff on podcasts, I'm afraid I will have to pay the tariff.

[01:19:00] **Scott:** Uh, I tend to yap and I apologize for that. But, Hanselminutes is my podcast you can get to at hanselman.com. It's been around over a thousand episodes over the last 20 years. And then I have a new podcast with Mark Russinovich, the CTO of Azure, where we learn something new every week. It's called Mark and Scott Learn to.

[01:19:15] **Scott:** So those are two that people can check out.

[01:19:18] **Jeremy:** Yeah, I highly recommend both of those. It's also amazing how long you've been doing Hanselminutes. I think it's been, you said over 20 years Right. 

[01:19:26] **Scott:** Yeah, it's been a minute. It's been a minute thou every Thursday for the last thousand plus episodes. And it, it, it, it tries to showcase faces that you maybe not ordinarily see.

[01:19:35] **Scott:** There's like the same three or four people that do the shows and, uh, I'm, I'm guilty of that, but there's a lot of cool people doing a lot of amazing work. I recently had, uh, a lady who is the IT manager of the Philadelphia Airport and I learned all about how airports run and like you don't see folks like that on a podcast.

[01:19:52] **Scott:** That's amazing. So yeah, definitely showcasing of people that are doing great work.

[01:19:57] **Jeremy:** All right. 

[01:19:58] **Jeremy:** We're good.

[01:20:01] **Scott:** I thought that was fun.

[01:20:02] **Jeremy:** Yeah, for sure. Me too. 

[01:20:04] **Scott:** See, if Grant tells me I broke into jail or anything, Grant's like, shut up. No, we don't talk about pricing. 

[01:20:11] **Jeremy:** You didn't have a chaperone last time. Things have changed.

[01:20:14] **Scott:** I don't know man. Dude you become important at work, it's like a whole thing. I accidentally became important at work.

[01:20:21] **Scott:** Scott, you are, you are free and clear. No jail for you. I, I mean, I had a great time listening, so, uh, I'm glad that I did. Cool. 


## These tools give new developers confidence to try things

[01:20:29] **Scott:** Well I know that we're still recording. You can use this as B roll if you want.

[01:20:33] **Scott:** But like, I was doing this talk internally recently for, the developer relations people and they're like, you know, what are we selling here man? What are we even selling, bro? Are we selling like tokens? Like we're trying to get people to use copilot. Like what's the thing? It's confidence transfer. I am confident that I could make whatever the (blank) I want right now.

[01:20:51] **Scott:** And it's amazing. I am. Just building stuff, and it's like, it's delightful. I feel like my 30 years of software is coming up to this moment where I can now make anything. But if a young person, an early career, early in career person, a new builder, a fresh builder, someone who just got outta school, just, just busted their ass for four years and just got a computer science degree, and they don't feel like they have that confidence, and they're like, oh, man, my job is over.

[01:21:18] **Scott:** I want to transfer my confidence to them. I want them to feel like, no, this is perfect. You entered at the perfect time. You know, computer science, you have a degree in computer science. You learn how to do this stuff manually. You know how to drive stick shift, and now we're gonna give you an Uber. You have the best of both worlds.

[01:21:36] **Scott:** And I want them to feel like that. And if, if, if a, if a copilot or a Claude makes someone feel dumb, we're doing it wrong. We have to let people know that this is a exoskeleton for your brain. But I don't want people to end up like the end of Wall-E where it's just like. In a chair and they're just bringing tacos to you, you know, via Amazon Prime.

[01:21:56] **Scott:** You've gotta do the work, you gotta know how the thing works, and if you do, you're gonna have a blast.

[01:22:02] **Jeremy:** 

[01:22:02] **Scott:** It does tickle a part of your mind, because I talked about taste. Like how do you know when it sucks or not? You just, I don't know. I mean, I just, I just know, bro. 

[01:22:12] **Scott:** You know what I mean? And, and that feeling of like, yeah, I know that, that, that feels right or that doesn't feel right. Developing that. I'll tell you one more story and then I'll get outta your way. Okay, so we're doing this new thing called a preceptorship. Most people have like internships and apprenticeships, and that makes the, the person who is less than they have a label, right?

[01:22:35] **Scott:** Jeremy, you're an apprentice. Work really hard and pull yourself out of apprentice world. My wife is a nurse and she is a nurse preceptor. A preceptor is a nurse trainer. They, she has an actual name tag that says preceptor. So if an, if a junior nurse says, Hey, um, I have a question, she's a safe person.

[01:22:56] **Scott:** They're not gonna like, flip the bozo bit and like fire her. Like, if an apprentice or an intern says something dumb in a meeting, they're gonna like, oh my God, I'm gonna lose my job. But if a nurse preceptor is there, they're a safe person to ask questions for. And, um, do you watch The Pitt? You know, No, no Oh, dude, so good. Okay. But you've seen like, er, you've seen like health shows, stuff like that. Okay. So. On the pitt. Like there's always a moment or any health movie like this where like some guy comes in and he is choking and he can't breathe and he's like, and somebody says, oh my god, quick Jeremy, do you have a pen?

[01:23:30] **Scott:** And then Jeremy hands me the pen and I pull the pen parts out and I have like a tube and I'm like, alright, I gotta stab this guy in the neck. You shove the neck and stab the guy in the neck and then he can breathe in his airway and he goes, I can breathe. Right. What they do on these shows is that they'll say, Jeremy, have you ever stabbed a guy in the neck with a pen?

[01:23:48] **Scott:** And you're like, no dude, it's my first day. I just got here. I'm a junior nurse, dude, this is your chance. Gives you the thing, you're like, Hey, you gotta put it by the third and fourth thoracic, whatever. And you go. And then at the end when the guy's alive and there's blood everywhere and the pen is like sticking out of his neck and they wheel him away, they say, Jeremy, how is that?

[01:24:06] **Scott:** That was amazing. I'm gonna be a doctor. I want that for freaking software engineers. Right sites down. Like that's how I grew up. Pair programming sites down. Oh man, Jeremy broke production. What are we gonna do? Time to learn everybody quick, grab a pen. You ever stabbed a whip server? I don't know the metaphor falls apart at this point, but you know, let's go and stab servers in the neck with a pen and learn and get excited and say, yeah, I can make stuff.

[01:24:37] **Jeremy:** That makes sense to me. I mean, like I, I remember when I was like tutoring in computer labs for some people, when they had a problem, what they really needed was the start to be kind of filled in. 

[01:24:50] **Scott:** Yep, exactly. 

[01:24:52] **Jeremy:** And I feel like a lot of these tools, if you're not sure how to get started or you're kind of scared of getting started, they can at least get you something.

[01:25:01] **Jeremy:** And then based on that, you're like, okay. Like I kinda, I kinda know how I can start filling in the rest or how I can start moving forward. Yeah.

[01:25:07] **Scott:** Exactly. Alright. Mac mini person is texting me. On Facebook

[01:25:12] **Scott:** Marketplace. They've left it on the porch so I gotta go. 