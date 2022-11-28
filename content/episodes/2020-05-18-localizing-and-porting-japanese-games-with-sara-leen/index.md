+++
title = "Localizing and Porting Japanese Games with Sara Leen"

description = "Sara Leen shares what it's like to localize, port, and modernize games"

[extra]
episode_url = "https://pinecast.com/listen/7e5f82a7-d5f1-43ab-85d5-5e98ea7694c5.mp3"
social_banner = "020-sara-leen.jpg"
social_title = "Localizing and Porting Japanese Games"
social_description = "Learn about scripting, reverse engineering, and rewriting games!"
+++

Sara Leen is a localization programmer for XSEED Games on titles like Ys, Trails in the Sky, and Corpse Party. She got her start reverse engineering and fan translating games. 

We discuss:

- What makes games different
- How games store and encode text
- Rewriting Corpse Party (and not being able to run it for a year!)
- Porting and modernizing games
- Reverse engineering raw assembly

This episode originally aired on Software Engineering Radio.

Related Links:

- [@SaraJLeen](https://twitter.com/SaraJLeen)
- [Personal Site](http://sara.wingdreams.net/)
- [Corpse Party PC Programming Blog](https://www.xseedgames.com/2016/05/02/corpse-party-pc-programming-blog/)
- [Trails in the Sky Second Chapter Localization Blog 5](https://www.xseedgames.com/2015/10/30/the-legend-of-heroes-trails-in-the-sky-second-chapter-localization-blog-5/)
- [Mojibake](https://en.wikipedia.org/wiki/Mojibake) (Garbled text when text is decoded using the wrong encoding)
- [Shift JIS](https://en.wikipedia.org/wiki/Shift_JIS) (Japanese character encoding used in older games)
- [Hot Soup Processor](https://en.wikipedia.org/wiki/Hot_Soup_Processor) (Obscure programming language used for Corpse Party)
- [XSEED Games](http://xseedgames.com/)

Music by Crystal Cola: [12:30 AM](https://crystalcola.bandcamp.com/track/12-30-am) / [VHS Skyline](https://crystalcola.bandcamp.com/track/2-30-am-vhs-s-k-y-l-i-n-e)

---

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy:** Hey, this is Jeremy Jung. This episode, I'm talking to Sara Leen, a localization programmer for XSEED Games. Sara has over a decade of experience localizing games from Japanese to English. And we talk about how games are different than other types of software, storing and extracting text, porting games to different platforms, and rewriting a game from scratch. 

A game written in an obscure programming language called... can you guess it? Hot Soup Processor.

Pretty good right? This was a fun episode and I hope you enjoy it.  

**Jeremy:** [00:00:35] The first thing I want to start with is you have experience with building other types of software. I was kind of taking a look at your resume. What makes games different than working on a typical software application?

**Sara:** [00:00:48] With games, there's a lot of things that you have to worry about that you otherwise wouldn't like the frame rate of the application becomes very important. For example, you need to make sure that the timers of the application are coded just so that the game will always run at a steady pace. And there are various applications of timers like delta time that are usually used to ensure this goes perfectly smooth.

**Jeremy:** [00:01:17] When you talk about timers, I've heard of this concept called a game loop. Is that what you're referring to?

**Sara:** [00:01:27] Essentially a game is made of graphics, audio, and input. But all of these have to be checked every frame. And so you have your timer going so that it is basically looping through the game 60 times a second or whatever other frame rate your game is running at a lot run at 30. There will be various steps in this process, like game logic and drawing the various models. And of course you have to keep the sound system updating.

**Jeremy:** [00:02:01] As opposed to a web application where a lot of things are in response to something, right? Somebody's going to a webpage, clicking a button. With a game it sounds like there is this consistent loop that's tied to the frame rate. Is that correct?

**Sara:** [00:02:20] Right. And instead of reacting to things, you are occasionally checking the state of course so many times per frame and you will still have to respond to the user input but it's all going to be one part of this large set of functions.

**Jeremy:** [00:02:38] So you're in this loop and let's say somebody was pressing a button on their controller or moving their mouse that would affect the state. And when you're in that loop it's going to look at that state to determine what to do next in the loop?

**Sara:** [00:02:58] Yes, exactly. For example, in your input system you are usually going to be saving every frame, the state of the input system at the moment, like is this button being pushed? Is this button being pushed? Was this button pushed last frame and by comparing it against the previous frame. You know what the user is doing right now, and then many parts of the game logic will have various branches that check exactly what the user is inputting and what the current context is.

It's certainly more complex than the idea of I push a button and it calls this function.

**Jeremy:** [00:03:34] That sounds like like an entirely different model of thinking. The structure of the application has to be almost completely different.

**Sara:** [00:03:42] Absolutely.

**Jeremy:** [00:03:43] In terms of skillsets working on a game versus working on a regular application.  What parts are really different and which parts are kind of the same?

**Sara:** [00:03:54] Regardless of what you're working on you're going to be working with a lot of external APIs, but these are probably going to be entirely different for a game versus other software. 

For example, you need to be familiar with APIs like DirectX and OpenGL and all of these typically have different ways of handling graphics, handling audio, handling input.

There's also SDL of course that you could use and depending highly on the programming language as well there may be different ways of handling certain things that would be different from handling a normal application.  

But most importantly you need to be familiar with graphics and audio APIs above all. I think those are typically less important when you're working on normal software because you're more concerned about how to build your window and how to get all of the elements displaying in the proper positions.

**Jeremy:** [00:04:51] With a typical application the actual act of rendering to the screen is abstracted away from you so you don't have to worry about how to draw to this screen. It's more like, I want a button or I want a window and something else is handling that for you.

**Sara:** [00:05:08] Yes, that's pretty much it. And when it comes to video game graphics, you have to consider a lot of different things like differences between graphics cards. Can this graphics card handle square textures or does it need a different shape?  As well, of course, as being concerned with the quality of how it's drawing. Like is this texture supposed to be filtered? Will this graphics card filter it correctly? The APIs simplify that, but you're working at a lower level.

**Jeremy:** [00:05:36] And when you were giving examples of APIs you were talking about DirectX and OpenGL and SDL.  How low a level are we talking? If I wanted to draw something to the screen at the most base level what kind of work am I looking at?

**Sara:** [00:05:55] Well, for SDL in particular this is somewhat of a simplified process because it handles all of the initialization of devices and such for you. 

But with DirectX and OpenGL, you have to actually get the list of devices you have to initialize each process that you need. Like you need Direct3D, you need DirectInput, you need DirectSound, and then you have to make sure that you have all the device information that you need, including stuff like the current resolution or the capabilities of the device. Device capabilities is a big thing when it comes to that. 

And then to actually draw the image, you are going to need to create a texture buffer. You're going to need a back buffer for the screen, and then you will have to load the texture and you will have to draw the texture to the buffer and then present that to the screen.

**Jeremy:** [00:06:53] When you refer to the buffer, at kind of a high level, can you kind of explain what that's doing?

**Sara:** [00:06:58] Essentially you have the screen that you're drawing to, and you usually don't want every single draw command to go directly to the screen. It's better to have a buffer that you can operate with so that you can display things in the correct order at all times. You can have them on the correct Z level, and of course, any sort of processing you need to do, you can do before it's drawn to the screen. And so everything goes onto the buffer after it's ready more or less.

**Jeremy:** [00:07:29] And when something is in the buffer is that what you plan to actually have the video card render? Or is that after it's already been rendered?  Where is that in the stage?

**Sara:** [00:07:43] Well, rendering is basically the last step of presentation, but it depends. If you are drawing something 3D naturally you are going to have to do some processing on that via the graphics card. And the APIs allow for things like that, but typically rendering to the screen itself is always going to be the very last step of the frame.

**Jeremy:** [00:08:06] And then elsewhere in your application even though you're putting things into the buffer, you're deciding that there are certain frames that you don't need to render?

**Sara:** [00:08:17] Yeah, and of course that depends highly on the game, but often there may be no difference. So you don't really need a new frame or there might be a case where the game is overall running a little too slow. So skipping some of these frames will get you more CPU cycles free to work with.

**Jeremy:** [00:08:36] We were talking about the loop earlier where all the logic is happening at a set rate, but in terms of the way people see the game of how smooth it is, you may have the game logic running at the same rate, but only choose to render certain frames in the buffer so that it still runs the same it's just that it's a little choppier?

**Sara:** [00:09:03] Yeah and essentially you need your game logic working at the highest that your gameplay can really go. But when it comes to the graphics, it's a little more arbitrary for sure. There are situations where you might intentionally want your game logic running at 120 frames per second and then the player input and such will still come at that speed regardless of the actual refresh rate of the display.

**Jeremy:** [00:09:32] Interesting. I want to talk a little bit about how games can have a lot of binary assets. Typical software development you would use git as a version control system. Would you use the same for games or is there a different system that's more suitable?

**Sara:** [00:09:49] Well naturally, this depends on the company. Quite a few do use git and simply store the binary assets even though there is no real comparison system for them. There are also various internal systems that companies may use that are specially made for handling their specific assets. Essentially version control is not that different in the gaming industry. It just occasionally uses different applications.

**Jeremy:** [00:10:22] And so when somebody uses git even with the binary assets, it's not an issue. You just can't see the diffs properly.

**Sara:** [00:10:32] No, it's typically not a big deal because it's not difficult to look at two different pictures and visually compare them. And generally you're going to be changing the binary assets less as development goes on rather than more, whereas the code that's always going to be changing.

**Jeremy:** [00:10:52] The title you use is localization programmer. What would you say is the main role of a localization programmer?

**Sara:** [00:11:02] Essentially, when a game is being localized from one language to another obviously the goal is that you get all of the text inserted and you make sure that it all looks correct. At base levels this is generally the accepted position of a localization programmer. You are getting all of the texts into the game. You are making all of the code work with the correct fonts and other asset changes that you may need that are different from the original language. However there are a lot of things in this process that you wouldn't normally need as a skill. For example, if you are working with Japanese games, all of the comments and everything are going to be in Japanese of course.

**Jeremy:** [00:11:43] When you're translating games, do you usually have access to the original source code?

**Sara:** [00:11:49] I usually do, but there are plenty of cases where we are working on a game and the original developer is actually the one to handle the localized version. It depends a lot on how much other companies feel they are able to release to other parties, whether it's because of rights issues or they're just kind of nervous about their code quality, which I mean, I would be.

**Jeremy:** [00:12:12] And when you get access to the code do you usually have access to the original developers or are you on your own?

**Sara:** [00:12:21] I would say that completely varies. You never know exactly, but it's usually going to be the same with each partner. Like, they will usually be more than happy to help you if they have the developers on hand to help you. But game companies are constantly developing new titles themselves.

So when someone like me is working on a game, we may not have as much access to the developers or they would be working on the game.

**Jeremy:** [00:12:48] You were talking earlier about being able to extract text or bring text into the game. What are some examples of ways that the text would already be stored and how would you bring that out?

**Sara:** [00:13:03] This also varies a lot and it's very interesting. Many games use script files, essentially lists of commands for their events, et cetera. And in these cases, as long as you know the format of the script file, you're usually going to be fine. But some games like to hard code their text, and yet others have been in binary formats that have been compiled in some way, assembled rather.

And when that happens, you often have to take a look at the code and figure out exactly what this format is, which may or may not be documented, and basically do the process in reverse unassemble it.

**Jeremy:** [00:13:46] The first example you gave was script files. So would that be a plain text file and you could replace that text with instead of Japanese put in English?

**Sara:** [00:13:57] Essentially, yes, like when there's a script file format, you're going to see various commands, like there will be message and then it will have the text for a message box, that kind of thing. And when that is the case, it's usually pretty easy to change since it is just text. But you might run into some encoding issues.

**Jeremy:** [00:14:17] By encoding issues, would that be where let's say you replaced the Japanese with English and then the game itself tries to load the texts from the script file and it can't due to a different text encoding?

**Sara:** [00:14:29] Not so much that as you might get garbled text, what in the fan community that I used to work in, we would call cave speak.

**Jeremy:** [00:14:38] Could you explain what you mean by that?

**Sara:** [00:14:40] Imagine that you are playing a game in Japanese, but your system doesn't have Japanese fonts loaded. The font not being there for Japanese, you might instead see jibberish like ekvgh, that kind of thing. And that is cave speak. 

If the encoding is very specific for the game or the font simply doesn't have other symbols, you might get complete jibberish in what font was already there. In Japanese, it's called mojibake.

The way that encodings work of course, is that the text is interpreted from its binary or hexadecimal format into characters we can understand. And since there's a lot of different encodings out there, sometimes you don't know exactly what you're going to get. So, for example. If a game was made for an older system, it may have a completely custom encoding where a value like "2" means "a" and in this situation just replacing the text you have no idea what the game's going to output. You're going to have to change it all yourself.

**Jeremy:** [00:15:55] So the original text in the script files, or perhaps you're talking about the binary files, they're not necessarily using a standard encoding like ASCII or Unicode. They may have made up their own encoding format.

**Sara:** [00:16:12] Yes, and this certainly varies. When it comes to Japanese, you'll usually be able to find that it's in the standard Japanese encoding Shift JIS. And Shift JIS largely supports English letters, but because Japanese text tends to include characters that are all the same width, it doesn't often account for the fact that in English you have very thin letters like the letter I. And so when you simply insert the text into those games you might get a situation where all of the letters are spaced really far from each other. And that does not look good.

**Jeremy:** [00:16:52] You were talking about how there's the example of script files or the example of code being hard coded or even binary files. What is the end result you'd like to get this text out for a translator to work on?

**Sara:** [00:17:25] Typically the text you want to get into an Excel sheet because that's the industry standard for translation and keeping texts like that. Sometimes the developer will provide this themselves and that will of course, make the process of translation a little easier because somebody like me can work while the game is being translated but usually it's more a case of what is the translator comfortable working with?

Are they comfortable working with script files? Do they need an Excel sheet? Most of them do and that's fine. But obviously this results in more steps. You need to create a tool chain to both extract the text and get it into a sheet, and then you have to make the call of whether you can get that text directly back into the game or if you would need to include more information, like the exact lines it's from.

**Jeremy:** [00:18:21] The simplest would be the script file where you might build a tool to convert the script files to rows in an Excel spreadsheet. A translator works on that to translate it to English. They give the spreadsheet back to you and you run some kind of application to convert their spreadsheet back into the script files.

**Sara:** [00:18:43] Yes, exactly. Although granted if a game is very small, you might just do it all by hand.

**Jeremy:** [00:18:49] In terms of these script files are the lines of dialogue or the text-- are they in their original context? If somebody in a game was having a conversation would all of the sentences be grouped together or is it sometimes just spread all over the place?

**Sara:** [00:19:14] This varies a lot. Sometimes you won't even know which character is speaking unless you actually play through the game while you're working on the script. And obviously this poses some interesting challenges because in general, Japanese is not as context heavy and context apparent as English is.

You can't always tell who's talking just by the tone of their voice, so to speak.

**Jeremy:** [00:19:41] Going back to when you have something where the text is hard coded. Is that a case where you basically have to do it by hand or have you found a process to deal with that?

**Sara:** [00:19:53] There are a variety of ways that this can be approached too, which is part of the beauty of games. It's an art form. But what I personally like to do is simply make something that extracts all of the apparent strings, like surrounded by quotes from all of the code and gives that information along with the line number. And just like with any other script, you can usually automate this.

**Jeremy:** [00:20:20] So you create your own version of a script even though they didn't exist originally.

**Sara:** [00:20:29] Yeah. And then you have this list of all the strings in the game, and you can easily put those into a sheet.

**Jeremy:** [00:20:37] When you work on localization, how much of the code base or the game engine do you feel like you need to understand?

**Sara:** [00:20:45] It depends on the scope of the task, but typically I would say that I don't need personally to understand much of the game to start working on it, but by the time that the project is finished, I should understand almost everything except for the raw graphics the APIs being used. Even then, I might need to depending on how the game is functioning and whether we need to do something differently, like making an older game use widescreen.

**Jeremy:** [00:21:15] And what's your strategy when you first start work on a project? You get the source files and you need to find out where the text is stored and how it's stored. What's your strategy for figuring that out?

**Sara:** [00:21:30] First I will look through all the files I received and make sure that the text isn't somewhere extremely obvious. And if it's inobvious, I will then start looking at the source code and getting it to compile. And I will look through that to see exactly what files it's loading. And from there I can usually figure out where the text is stored.

**Jeremy:** [00:21:52] In terms of when you get a project, do you just look at the code or do you figure out how to to run it and all that first?

**Sara:** [00:22:01] Usually I prefer to start by looking at the code itself and getting that to compile, but typically a developer will provide a working copy of the game that you can use to see exactly how everything functions. I do like to know what kind of game I'm working on and the basics of the gameplay, the basics of the setting, because that will help me motivate myself to work on it. It will help me get into the right mindset for it.

**Jeremy:** [00:22:31] You were talking about how there were easier ways of localizing in terms of script files and the hardest being hard coded or binary.  What are some ways that if a developer is making a game that they can facilitate the easiest localization?

**Sara:** [00:22:51] The easiest localization would definitely be first you want to make script files for everything, whether it's just the list of strings that the game is using, or a proper script file for all the events. And then you want to make sure that the game is capable of loading a different sets of these based on what language is currently in use.

And if the game is already capable of loading different folders or different files for different versions of the scripts then it shouldn't be too hard to localize, but you also need to make sure that there are easy ways to work with the graphics and of course, absolutely all of the assets can be loaded differently based on language.

Another problem of course, is when it comes down to stuff like fonts. Because to make a very pretty looking font, you probably want to make the font graphical rather than using a true type or open type font. And of course, the challenge with that is including every character you could need for every language as well as issues like the font could be badly spaced in certain languages and to make a game as easy to localize as possible, you probably want to use Unicode and Unicode fonts and just include everything you possibly can.

**Jeremy:** [00:24:17] And because unicode has most languages used in the world, then you won't have the text and encoding problems.

**Sara:** [00:24:25] Exactly. You would completely skip that step. You wouldn't need to worry about the fonts. You would just be able to put whatever language you need and you won't get tripped up by stuff. Like in Japanese games Shift JIS is the encoding used right? And if you try to insert accents like an E with the little dash over it. It will instead draw a Japanese symbol if you don't change the encoding.

**Jeremy:** [00:24:52] You were talking about graphical fonts, so would that be a raster image, like a giant PNG or a JPEG that has all the different characters on it? 

**Sara:** [00:25:06] Yes, exactly. Usually this also has some sort of table containing the geometry of the font so that you can draw it with proper spacing and everything.

**Jeremy:** [00:25:18] And then when you're talking about assets, that would be like textures. For example, if you had a sign in the game, that would be something that somebody would have to go into Photoshop and have a different version for each language?

**Sara:** [00:25:34] Yes, and ideally you want to keep all of the original layered versions of this with the text on a separate layer, because that will make it as easy as possible to change the text that's on it. But of course that isn't always available. So when it's not, you need somebody who's actually able to remove the text and put something new in.

There's also things like title screens of course, and any sort of special menu texts you have like that's drawn in a different font or has a special design.

**Jeremy:** [00:26:06] Because something in Japanese versus something in English can look significantly different when you're doing a logo. So you need someone with the artistic expertise to be able to recreate something that looked like the other thing, right?

**Sara:** [00:26:22] Yes. And of course Japanese logos are often written entirely in Japanese, so you will want to come up with a localized title for these games and then put it in the correct localized language, and that will involve basically designing a new logo that looks similar. It gets the same point across which is the big thing in localization. You want to get the point across.

**Jeremy:** [00:26:47] One of the games you worked on was a game where you decided that the game's code needed to be rewritten. Can you talk a little bit about what the game is and why you decided that you needed to rewrite the game?

**Sara:** [00:27:00] Well, in this case, we are talking about a game called Corpse Party. Corpse Party's origins were as an RPG maker game on an obscure Japanese computer (PC98). Obscure over here at least. And when the developers revisited it many years later, they decided to remake it in a programming language called Hot Soup Processor or HSP for short. HSP was taught in many Japanese schools because it was free and it was made for people wanting to get into things like this.

Now Hot Soup Processor resembles basically the child of Java and C and in this way, everything is a little different. I wouldn't even compare it to C, honestly more like BASIC. And as a result, your game looks more like a scripting language than a programming language. And the bigger problem is that you don't have as much control over the graphics and sound APIs for games that are coded in HSP, and so to do many things with the graphics properly or get the timers right it may be better to change over to something else. Especially if you're going to put this game on something like Steam, because Steam does not have a version of their API for Hot Soup Processor. I know. Shocking.

**Jeremy:** [00:28:30] About it being like BASIC, is there a high reliance on GOTO statements?

**Sara:** [00:28:38] Unfortunately, yes, there is.

**Jeremy:** [00:28:40] Was this statically typed? What was it like to kind of work in that language?

**Sara:** [00:28:49] Well, when it comes to typing. You don't always know what type it's going to be. You don't know if this variable is necessarily an integer or if it's a float, and the compiler of the scripts largely doesn't care, and obviously that means you can run into some typing issues because you have completely misunderstood what a variable actually was. That definitely gave me some headaches.

**Jeremy:** [00:29:16] So it's sort of like Javascript or Ruby where you can define a variable and that variable, you could put in a string, you could put an a number, you could put in pretty much anything and there isn't really a way to check. I guess it just runs through the interpreter and then you find out at runtime whether something's going to blow up.

**Sara:** [00:29:37] Pretty much, I definitely would compare it to Ruby in that regard.

**Jeremy:** [00:29:42] What was your strategy for rewriting a game? Were you porting function by function? How did you get started?

**Sara:** [00:29:50] Of course, I started by just copying all of the code and then I began rewriting each function one at a time. Trying my best to understand the purpose of each function as I was going along. I knew what some of them did already because we actually inserted the translation before all of this, but the thing is that I was never going to be sure exactly what functions relied on each other and what variables were needed and how exactly they needed to be typed until everything was already basically put together. And so I honestly was pretty scared during this process at times because I had no idea if it was going to work until it worked.

**Jeremy:** [00:30:36] You were rebuilding it function by function but because it wasn't really clear which functions relied on other functions you couldn't run the game. There wasn't this iteration of getting part of it working and moving on to the next part, you had to build everything and then you found out if there were issues?

**Sara:** [00:30:58] Yes, exactly. Because for the most part with games, you are not building the code level by level. You are programming something that will be able to run all of the levels.

**Jeremy:** [00:31:09] Wow, that sounds terrifying.

**Sara:** [00:31:11] It is.

**Jeremy:** [00:31:12] Were you able to on a function by function level, have an idea of  what the function was supposed to return so you could at least test certain functions?

**Sara:** [00:31:26] Yes. There were definitely cases like that. However, the most complex parts of the game are often more in the graphics and audio engines and such if you're working at this kind of level. And I wasn't always sure how the graphics functions worked. No fault to the developers, just that it was so much.

**Jeremy:** [00:31:46] Since you didn't quite understand how the graphics functions worked, when you rewrote that portion of the game did you take a different approach rather than trying to recreate what they had done?

**Sara:** [00:31:59] Well, I initially tried to recreate what they'd done, although for certain API functions, et cetera, I basically took my best guess and so when the game was finally running, it definitely didn't look or sound right. At first, there were problems, and these were entirely problems with how I had understood the code rather than anything to do with the game itself of course.

**Jeremy:** [00:32:24] How long did it take from getting the code to actually being able to run the game at all?

**Sara:** [00:32:31] The original version of the game pretty much worked out of the box and compiling it I just needed the version of the HSP tools that the game had been made for. But when it came to actually making my version of the game run it took about a year.

**Jeremy:** [00:32:50] Wow. So a year before you could launch the game. That's intense.

**Sara:** [00:33:00] Believe me, I hated myself for a lot of that project. I was like, why didn't I just use the original code? Why did I put myself through this? But the result was that the game runs very well.

**Jeremy:** [00:33:12] One of the common pieces of advice people get when they work on software is quick iteration in terms of build the thing, see if it works, then you can build the next thing. But in this case it seems like that wasn't possible to do.

**Sara:** [00:33:32] Yeah. Unfortunately. With games everything is going to be more tangled and depending on the way you approached creating the game you can end up with either something that's very clean and parts don't depend too much on each other, more abstracted, or it can be a plate of spaghetti. And just like any application, this is a matter of designing the application before you start building it.

**Jeremy:** [00:34:01] Something you managed to do when you rewrote the game was make it platform agnostic.  What are some examples of ways that when you write a game, you make something that can be easily run on different platforms?

**Sara:** [00:34:15] Regardless of the platform, you are going to be dealing with different graphics and audio API APIs. Because you're not going to run DirectX on a PS4 and essentially the approach you need to take with this is mostly related to creating wrapper functions for all of the graphics stuff you need to do so that you can easily change these functions and not have to change any other part of the code. 

For example, you want to have functions for drawing a sprite. You want to have functions for drawing some text, and you want these to be things that you can easily change the contents of without changing any part of the actual games code directly.

**Jeremy:** [00:35:00] And the parts that are going to be different from platform to platform, would you say that's the graphics, the sound, the input that sort of thing?

**Sara:** [00:35:10] Yes. Basically everything that deals with IO.  Aside from the fact that on pretty much any platform you're going to be able to use, fopen() without any issue.

**Jeremy:** [00:35:21] When you rewrote the game, I think you had said that when you got the original version of the game, you had replaced the text. Was that hard coded into the game or was that through scripting files?

**Sara:** [00:35:34] Mostly scripting files, but it took me quite a bit of effort to understand these scripting files. There definitely was some hard coded text in the game. Mostly related to the menu functions. Chapter names for example that you would encounter in the menus were hard coded

**Jeremy:** [00:35:52] And did your rewrite load in the original script file format?

**Sara:** [00:35:58] Yes, actually. Although interestingly enough with this particular game, all of the original scripts were in Japanese. Even the commands and this is not common. It does happen, but usually the commands and such will be roughly in English because when you're working with programming, you're going to be writing some of it in English no matter what language you speak.

But since all of these scripts were completely in Japanese, I decided to replace all of the commands such that the game could still load the original format, but it was using something sort of new in that the script commands were simply translated.

**Jeremy:** [00:36:37] And when you refer to a script command could you give an example of what some of those would be?

**Sara:** [00:36:42] Stuff like message, wait, display picture. Move character to the left, stuff like that, or check a variable. 

It's a lot like programming. It's just that you are working in a language that is created for the game and is being used by the game without compilation usually. 

Sometimes there's assembly involved, but when you assemble the script like this, you are just converting the commands to one, two, three, et cetera to make sure that you know what the commands are without having to use as much text and space.

**Jeremy:** [00:37:19] So it's kind of like an enum, is that a good example?

**Sara:** [00:37:24] Yeah. Essentially

**Jeremy:** [00:37:25] And those commands would use the English letters but they would be written in Japanese words?

**Sara:** [00:37:33] They were actually written in Shift JIS full Japanese.

**Jeremy:** [00:37:36] Wow.

**Sara:** [00:37:37] I never encountered any other project that did that, although I understand it must've made the script files really easy to understand for them.

**Jeremy:** Yeah. It's interesting how we sort of make the assumption when we look at code that there's going to be English in it. I guess sometimes you get surprised.

**Sara:** [00:37:55] Yeah, for the most part, there aren't many programming languages where you can do everything in another language, but if you're creating the language yourself, obviously you have plenty of control over that and you can do anything. 

Even though we sort of take for granted that there's going to be English there it doesn't have to be, and I find that extremely interesting.

**Jeremy:** [00:38:17] I don't know that it happens very often, but I think a lot of languages do support Unicode for variable names and stuff like that, I just am not sure how many people actually take advantage of that.

**Sara:** [00:38:28] Yeah. When it comes to seeing localized variable names and source that are not in the normal character set? I would say I hardly ever see it. I can only think of one occasion and you will usually instead find that it is written in English characters, but is in that language, which in the case of Japanese is what they call Romaji.

So you would have the Japanese written entirely in letters. And you find that a lot when you're localizing Japanese games.

**Jeremy:** [00:39:01] You said after a year you were able to run the game, but there were bugs or there were different issues. How were you able to track down what bugs were in the game? Was it a completely manual process where you just had to keep playing and keep trying things?

**Sara:** [00:39:19] Essentially, as well as having testers within the company also handle that sort of testing, what is called quality assurance. Of course, we just call it QA. But by having people iterate through the game many times we would find all of the bugs with it, essentially like you would any other program. You just have to have people using it.

**Jeremy:** [00:39:41] Were there any bugs or odd behavior in the original version that the game was relying on that you had to reproduce?

**Sara:** [00:39:51] I wouldn't say there were any bugs that I had to reproduce, but since I had copied the game's code as closely as possible, some of the original bugs did carry over initially and I was later able to fix a lot of them.

**Jeremy:** [00:40:08] We've been talking about the process of making games and rewriting games. What is the language that you rewrote the game in?

**Sara:** [00:40:18] C++

**Jeremy:** Is that pretty typical for the projects you work on?

**Sara:** I would say that the vast majority of professional games are written in C++

**Jeremy:** [00:40:31] What makes that the default choice that people would go to?

**Sara:** [00:40:38] Frankly, it is widely supported. You have C++ compilers for consoles. You have them for computers, you have them for all kinds of different devices. Whereas you create a game in Ruby, you have no idea if you're going to be able to put that on a PlayStation.

**Jeremy:** So it's just the fact that everybody's using it and there's so many tools, so much support.

**Sara:** [00:41:04] Yeah, exactly. As well as the fairly robust standard libraries and since these are available on so many platforms, it's just always been the choice ever since it came to be. Originally back in the days of like the Nintendo Entertainment System, games were primarily written in raw assembly. But obviously that's not very practical, especially for the scale of games these days.

So it eventually changed to C and then C++. There have been efforts to adopt C# in more platforms, but it's kind of a slow going because it's just so deep-rooted.

**Jeremy:** Typically when I hear about C# and games it's within the context of the Unity engine. It seems like that would make it easier for people to get started and work on projects but I don't know what the trade offs are relative to C++.

**Sara:** [00:41:58] Typically, I would say that C++ simply is the most easy to optimize compared to other options like this because of the nature of how it's compiled. Whereas with C#, they take a more native approach where all of the code is managed code, and the native code is easier to optimize, whereas the managed code that makes up most of C# simply isn't something you can optimize much beyond how it's handled for everything.

It's a global optimization, whereas optimization specific to various functions in games are better than global optimization in a case like this. The trade off is simply performance. How much you can pull out of the system before it starts choking.

**Jeremy:** [00:42:50] And one of the big differences between the two languages is that C# has a a garbage collector. For games, is that something that's seen as not desirable?

**Sara:** [00:43:02] Rather than having garbage collection, you need to handle all of the games memory very, very strictly. You need to know exactly how much memory everything is going to take at any given time. The reason for this is because consoles typically have much more severe memory limitations than a computer does, and if you start running over that memory, you just don't have a program running anymore. It's problematic. 

Whereas on PC, there are things like virtual memory to pick up if you end up running out of memory somehow, and as a result, if you have any sort of garbage collection, you're going to be wanting to do it yourself. Frankly, all memory that you're locating, you should be doing yourself. You should have your own memory manager in the game.

**Jeremy:** You said it's probably true for all platforms, but on consoles it's more important just because of the memory restrictions.

**Sara:** [00:43:58] Yes. And of course that is also why when you are porting a game to a console, you have to be very considerate of things like memory space and of course video RAM. It was more important back in the older days of systems like the Super Nintendo and the Nintendo 64 but it still remains important today. If you start running out of memory on console, there's nothing you can do about it.

**Jeremy:** [00:44:27] You've ported some games from low spec hardware like the PlayStation Portable to the PC. What are some of the unique challenges related to porting a game?

**Sara:** [00:44:38] First of all, when it comes to games on an older system or a weaker system such as the PlayStation Portable the game is made exactly for the hardware specifications and you are at the mercy of those specifications at first. For example, the PlayStation Portable, its resolution is quite small. It is something like 480 by 272 and while that is almost 16:9 it's not quite. 

When it comes to PC games people want options. They want the ability to use different resolutions and customize their controls and the original game is probably not going to have supported this and more importantly if you're working in a game at a low resolution like that, that is not going to look good on a PC screen.

With these projects we take as many of the original PSD assets and such as we can and just redo the games assets in HD and that obviously results in a much prettier game. 

But that also assumes that you actually made the assets in a higher resolution to begin with. Otherwise, they're going to have to be remade, and that is a whole different ballpark of problems.

**Jeremy:** [00:46:00] Yeah, their resolution is so low that if you were to use the original assets, they would just look super blurry or blocky if you were to port it straight to the PC.

**Sara:** [00:46:10] Exactly right. And frankly, that would make the game look a lot worse as a whole and less people would play it because at that point you're just playing something that looks old and you don't want it to look old because you're creating a new version of it. You want it to look new and shiny and sparkly.

**Jeremy:** [00:46:30] How does the process of porting a game differ from your experience rewriting Corpse Party? How much of it is a rewrite versus something different?

**Sara:** [00:46:43] When you're porting the game, hopefully it's in a language that you can still use. And if that's the case then the first step is going to be ripping out all of the stuff that you can't use. 

For example, when you're working on a console you have to use the console developer's development kit in everything. You have to use their software and while usually this supports the same programming languages that you would be able to use on PC anyway, you won't be able to use most of the graphics functions and the audio functions and you're just going to have to do all of that over instead of copying like I did when I was porting, one language to another.

I instead had to basically take guesses at what all of these functions did and then reproduce them to my best. And occasionally this would result in something I didn't understand, just like when I was working on the original corpse party game, but more often I would find that I missed a functionality and that something wouldn't change color when it was supposed to or something wouldn't play from the correct speaker or things like that.

One of the latest issues that I got when I was working on my first port last minute was that I realized there were audio files that were supposed to be looping and cross fading. And I had forgotten to implement any of this because I didn't realize what it was. When it comes to porting to PC, there are two main concerns. One is making sure all the functionality is correct in the first place. The second is making sure that the game runs well on a PC because there are different threading models and different timer models that simply don't convert well to a PC. That's the case with changing platforms in general.

You want to make sure that everything runs as it should, even though it's on a different platform, which I know I'm just speaking in circles there, but at the same time, you have to realize if you just put a game directly on PC and you don't change anything it is going to run a lot slower than it could because it was optimized for something else.

**Jeremy:** [00:49:04] When you talk about different threading models, could you give an example of something running on a console versus on a PC? What are these different threading models or different choices you'd be looking at?

**Sara:** [00:49:18] Well, for example let's say that you are programming a game that is working on a Nintendo Wii. You will find that you have to handle the graphics at this time and the audio at this time and threading is often a better choice when it's available for simple performance reasons. 

However, it's also the case that a lot of older games don't use any sort of threads at all. Everything is just a single thread going through that single game loop and you have to deal with the results as they come. But when it comes to a PC game, you of course want threads. You want to be able to use more of the CPU and instead of using the exact CPU number and types that you have on the console like that, you have this audio and this CPU and this console happens to have a dedicated audio processor, stuff like that. You want to use something more general on a PC that'll work on anything.

**Jeremy:** [00:50:20] So in terms of concurrency models on a console, the software development kit for that console may already have ways that you're required to do certain things. Like you were saying, a certain way to do graphics, a certain way to do audio, and once you bring it to PC, then you have more control over how you do concurrency, how you do graphics. And so you may choose to do it completely differently than how it originally worked.

**Sara:** [00:50:52] Yes, and I think in many cases that's preferable because obviously concurrency in something like a game is best used for optimization and making sure that everything runs smoothly without any hitches. But on a console, you are optimizing to such a specific scenario that this optimization does not carry over well and is actually harmful when you are copying it directly to a PC.

**Jeremy:** [00:51:18] Are there any specific APIs for example OpenGL that you would choose when you want to make something that you can consistently use across platforms?

**Sara:** [00:51:29] I would choose OpenGL or possibly SDL because surprisingly SDL exists for quite a lot of platforms. That said, I would say that Vulkan is becoming something that would be very useful in that sort of way.

**Jeremy:** [00:51:43] In terms of the projects that you've worked on, the example you gave with PlayStation Portable, were those games using some APIs specific to the console to do graphics, rendering, audio, that sort of thing?

**Sara:** [00:51:59] Yes. The APIs for these things are typically provided by the development kit and whether they resemble an existing API or not is pretty much up to the console creator's choice. For example, if you're working on a Nintendo 3DS, you can probably use OpenGL straight up with just a few changes. Although the optimization is still going to be a nightmare by comparison because it is completely different.

**Jeremy:** [00:52:26] When you're working on one of these ports have you ever had to go the other way around where you had a less constrained environment and then had to move it to a more constrained environment?

**Sara:** [00:52:40] So far, I would say no, because for the most part, PC is about the least constrained you'll get. But I still try to make sure that when I'm working on a game, it'll run on as many systems as possible, and that means trying to make it run on a toaster if I could. And when your PC is a potato, you don't really expect a fully 3D game to work right.

But sometimes they can. Sometimes if you are very careful about the way you optimize the game and take a lot of constraints in what you're doing, you will make a game that looks a lot better than it should on an older PC. And I try to make that a goal of mine. I try to make sure that these games run in older environments, Up until last year I was even making a point of supporting Windows XP with all of my games and that would be more of an issue at times than you would think.

**Jeremy:** [00:53:36] What's an example of something that you would have to do specifically for such an old operating system?

**Sara:** [00:53:42] For supporting old operating systems you essentially are limited when it comes to your compilers and your libraries. You can't use newer versions of libraries because they weren't made for older systems. The windows kernel changed very dramatically with Windows Vista and it's only been evolving more and more since.

And you are limited to using this older version of the kernel that is largely still supported, but there's often behaviors that are just a little different between a system and you won't expect them. Like you might be trying to get the size of your window rectangle and it will be off by one. Small things like that. Or you'll be drawing text and Vista might support outlining the text and XP might not.

**Jeremy:** [00:54:32] So there's subtle bugs or small features that don't exist. So when you have to take into account whether you'll have those or not it just makes everything more complicated.

**Sara:** [00:54:44] Yes, exactly. And you don't always have the ability to expect it because often the functions will look the same, but the behavior is simply different.

**Jeremy:** [00:54:56] And these are operating system level calls that you're referring to?

**Sara:** [00:55:01] Yes, largely. Although there is also the matter of APIs for things like graphics that don't exist on older operating systems. For example, you can't use DirectX 10 or later on XP.

**Jeremy:** [00:55:15] One of the things about porting is we were talking about the things that you can't reuse. Are you able to use most of the core game loop and the logic as-is without modification?

**Sara:** [00:55:27] Well, for the most part, most of the game code is going to stay intact like that. You will have to alter stuff like the coordinate calls for various textures because all of a sudden you're worried about different resolutions. Games running on consoles generally run on a single resolution that is their target. And if you are using a different resolution on your TV, the console is scaling the output to that. 

But when you are working on PC, you need to account for that and you need to account for different aspect ratios because while it's easy to say, Oh, I'm going to make my game this resolution, you might upset the people who have ultra wide monitors or the people who are still using old 4:3 monitors. They exist and ideally you want to support all of these scenarios as smoothly as you can. When you're creating a game, you can account for this better than if you're working on a game that already exists.

**Jeremy:** [00:56:23] It sounds like a lot of work in terms of finding the sections of code that are expecting a specific resolution, a specific aspect ratio. And earlier you were talking about how your assets may change as well, because you need UI elements that can be rendered at a much higher resolution or at a different shape. It seems like there's a lot of work that needs to go into it.

**Sara:** [00:56:51] Yes. A lot of the games that I worked on earlier in my career were older games that were made for 4:3 and in the process of working on these I realized obviously these games need to be widescreen, and so there were a lot of different approaches that could be taken. I could have converted the entire game to widescreen, but then what about the purists?

So I made this approach where I could arbitrarily in the code set any graphic to be aligned to the left or right of the screen or the center. Essentially by dividing the screen into regions that were still 4:3. So for example, I would draw a UI element that was always in the bottom right of the screen on the right, and when the aspect ratio increases, this would still be drawn on the right of the screen in the corner.

And by separating out HUD elements like this it gives a fairly consistent experience between different platforms without having to limit the user to a specific aspect ratio.

**Jeremy:** [00:58:00] You've worked on a lot of different games that have been made a long time ago or more recently. What are some of the big differences code-wise you've seen in the oldest projects you've worked on versus the newer ones?

**Sara:**[00:58:15] Well, I actually got my start in fan translation, working on things in assembly, disassembly rather. And obviously the challenges for that are very apparent. You're working with very raw code that you don't have any information on. But as I've gone along, I worked on various Japanese indie games as well as Japanese professional titles.

As the time has gone along, I feel that on average these games are more abstracted and more object oriented. And back then there was very little object orientation. There were just these loops and loops upon loops. Nowadays, you'll have various objects that might be inherited from other objects.

So a video game's character might be a single generic object that has most of the basic behaviors. And then on top of that, you will have the class for the player character or the class for a dragon. And they have their own unique stuff to them. And obviously the game loop has changed a lot over the years as a result of things like this.

**Jeremy:** [00:59:27] I think that matches how software development in general has evolved because there used to be primarily procedural code, right? And now we're seeing more object oriented code, more code related to functional programming. Maybe that parallels the general software community.

**Sara:** [00:59:49] Yes, I believe so, yeah. In this regard, the evolution does seem pretty parallel. The only limiting factor is that adoption of new programming languages is very slow.

**Jeremy:** [01:00:01] I'm not even sure what they would have used before C++

**Sara:** [01:00:07] C. But before that, they really did just program games in basic assembly. And occasionally in BASIC.

**Jeremy:** [01:00:15] You worked on fan translations where you would have to reverse engineer the code. You said that was assembly?

**Sara:** [01:00:27] Yes. Because when it comes to these games that are already compiled and you're working on them as a fan, you're not going to have any access to the source code ever. 

So there are two options available to from there. You can either learn how to work with the code that's already compiled by learning the assembly and learning how to debug this.

Or you can in some cases to an extent decompile the code if it was made in an existing framework that's well understood like .NET or some other programming languages that exist. But usually you're going to be working with the raw assembly when you're working as a fan and you need a strong understanding of the processor that the game was developed for and the exact sort of quirks to expect.

**Jeremy:** [01:01:18] When you're working as a fan you somehow have to determine where the text is in that game right even though everything is raw assembly. How would you even know where to start?

**Sara:** [01:01:35] Well, initially you would have a debugger that works with the game and you would have to step through step by step until you actually see the texts being drawn. And then you basically start stepping back from there to see how the text was loaded. And so it's all a process of finding first something that uses the function you need to edit and then working your way back.

**Jeremy:** [01:02:01] That sounds very, very time consuming.

**Sara:** [01:02:05] It absolutely is, but it's an interesting process because you learn a lot about how different styles are used in different things.

**Jeremy:** [01:02:16] Not only would you have to to find the text but you would have to find a way to re-insert it without the application breaking.

**Sara:** [01:02:26] Yeah, and in some cases the text would be stored in the application itself, but usually it's going to be in some sort of container you don't have any specifications for. And then it might be in some encoding you don't know. It might even be encrypted and obviously all of the functions for you to fix that are right there, but how do you put it back in? It's easier to extract something than it is to create an archive that works exactly as the one before.

**Jeremy:** [01:02:55] That's interesting. You have these files where you don't know how they're encoded but you're looking through the assembly code to maybe get a hint for how they were generated so you can modify or generate them yourself.

**Sara:** [01:03:09] Exactly. And when it comes to compressions and encryptions. It definitely is much easier to get a file that's already encrypted or encoded or compressed open than it is to make a new one because you have to worry about the size of the file. You have to worry about getting the optimization of the compression right. You mess up one part of the encryption key and everything's wrong.

**Jeremy:** [01:03:36] That sounds like pretty intense work for a fan project.

**Sara:** [01:03:40] Yeah. I actually got my start working on just simple script engines in games like Furcadia of all things when I was young. But as it went along I discovered things like emulation and all these interesting games in a language I didn't understand. And all I could think was how could these games be English? Is there a way? And sure enough, there actually was.

**Jeremy:** [01:04:05] That's really impressive and very cool. For somebody who's interested in modifying or localizing games, How would you recommend someone today get started?

**Sara:** [01:04:20] Well, I would find a project that you like on something like GitHub and simply try changing things and improving things in that first. Make it your own. Essentially with something like this, you need to get comfortable working in other people's code. It's not about learning to program a program yourself. It's about learning to be comfortable in other shoes and being able to cope with the decisions they make.

**Jeremy:** [01:04:52] I feel like general software development, a lot of it is also that right? So many of the projects people work on they're not brand new. They're something that a team has been working on for years and you're coming into that environment, living with the decisions that were made, and figuring out where to go from there.

**Sara:** [01:05:16] Yes. With normal game development, you'll find all sorts of tutorials that teach you how to build a basic platform and game engine or such, but it won't necessarily tell you why it's built that way, and you can make games that way, but you can't really work with somebody else's games from tutorials like that.

It has to all be about putting in the footwork yourself and just trying. You just have to try and you just have to keep doing it until it gets right. Just like any other skill.

**Jeremy:** [01:05:43] After all the years of experience you've had are there certain things that you do really differently now than what you did before?

**Sara:** [01:05:55] Oh, definitely. For one, I used to do absolutely everything by hand even stuff like text. I used to copy the text and paste it into files as I needed it and rinse and repeat. And when I was working as a fan translator, sometimes early on I would change the pointers for the text manually when I needed more space.

And that is just an awful idea. Automate as much as you can, make sure that whatever you're doing, you're doing it the easiest way you can. But at the same time, don't sacrifice quality for this. But typically you won't.

**Jeremy:** [01:06:38] So basically find the things that you are doing that are repetitive. Identify the things that you can automate and build that script or build whatever functionality you need.

**Sara:** [01:06:52] Yes, exactly. Because if you're spending a lot of time pulling the text out or something like that, you obviously don't need to be. There are cases where you might want to do that, like if there's exactly one or two hard coded strings or just a single menu, but if the project you're working is at any sort of scale that makes that an hours long job? Do not do it manually. Please.

**Jeremy:** [01:07:20] I think that applies broadly as well. How much pain do you need to feel before you just automate it and write that script. 

**Sara:** [01:07:32] Yes, exactly. The beauty of being a programmer is you shouldn't need to do much math because you can make the program do it for you.

**Jeremy:** [01:07:40] Cool. I think it's a good place to start wrapping up, but is there anything else that you thought we should have mentioned or talked about?

**Sara:** [01:07:50] I suppose another thing I would like to mention is if you're getting into localization programming for a specific language, like Japanese to English or something like that you should probably try to learn as much of the languages you can along the way. So not just the programming language, but the actual language as well.

If you are working on Japanese games a lot, knowing Japanese makes your work so much easier.

**Jeremy:** [01:08:15] What are some of the ways that you've found that knowing the language really helped you a lot?

**Sara:** [01:08:21] Even though all of the texts for a programming language is just gonna be in like ASCII, you're going to be dealing with the fact that all of the comments are going to be in another language. A lot of the function names are going to be in another language. You're going to see a file named Zako and you're not going to know that means a small fry enemy.

**Jeremy:** [01:08:42] Yeah, so just helping you get as many hints and context as you can.

**Sara:** [01:08:49] Exactly. Because when you're working on someone else's code in another language, you are not going to be working with documentation you can necessarily read. All of the documentation is absolutely going to be in that language.

**Jeremy:** [01:09:03] I guess code comments as well if those exist.

**Sara:** [01:09:07] They do usually.

**Jeremy:** [01:09:09] For people who are interested in checking out what you're working on or what you're up to how can they follow you?

**Sara:** [01:09:17] First of all, obviously you should keep up with XSEED's work in general if you want to keep up with what I'm doing. But I also have Twitter @SaraJLeen and I also occasionally do Twitch streams, not of programming, but of games in general.  And my Twitch username is @saralene. Sort of a corruption of my name.

**Jeremy:** [01:09:45] You work in a very unique field of software development and I really enjoyed the conversation. Sara. Thank you so much for sharing your experience, translating and porting games.

**Sara:** [01:09:55] Thank you for giving me a chance to talk about the technical side of things.

**Jeremy:** Yeah, it was really fun thanks again for coming on the show.

**Sara:** My pleasure.

**Jeremy:** That's it for my chat with Sara. I hope you check out some of her projects like Corpse Party and Trails in the Sky. She put in a lot of work to make sure they run well on old PCs so don't worry if you've got a slow computer. As usual, a transcript for this episode is available at softwaresessions.com.  Alright. See ya.

</div>