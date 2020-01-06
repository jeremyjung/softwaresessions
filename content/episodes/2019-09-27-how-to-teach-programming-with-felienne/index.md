+++
title = "How to Teach Programming with Felienne"

description = "Felienne discusses teaching programming to kids by saying code out loud, the user experience of spreadsheets, the role of a computer science education, and her experience as a professor, conference speaker, and podcaster."

[extra]
episode_url = "https://media.transistor.fm/515168b3.mp3"
+++

Felienne is an associate professor at Leiden University who brings a unique perspective on programming education backed by scientific research.  She also runs the [Programming Education Research Lab (PERL)](https://perl.liacs.nl/) in order to study the best ways to teach programming.

### Felienne 
- [Personal Site](https://www.felienne.com/)
- [@Felienne](https://twitter.com/Felienne)
- [Publications](http://www.felienne.com/publications)
- [Software Engineering Radio Podcast](https://www.se-radio.net/)

### Strange Loop Keynote
- [How to Teach Programming (and other things?)](https://www.youtube.com/watch?v=g1ib43q3uXQ)

### Related Research Papers 
- [How is Programming Taught at Code Clubs](http://perl.liacs.nl/2019/09/26/how-is-programming-taught-at-code-clubs/)
- [The Effect of Reading Code Aloud on Comprehension: An Empirical Study with School Students](https://pure.tudelft.nl/portal/files/52671807/Paper_camera_ready_final_withLink.pdf)
- [Code Phonology](https://www.felienne.com/archives/5947)
- [Why Minimal Guidance During Instruction Does Not Work](http://www.cogtech.usc.edu/publications/kirschner_Sweller_Clark.pdf)
- [Cognitive Architecture and Instructional Design: 20 Years Later](https://link.springer.com/article/10.1007%2Fs10648-019-09465-5)
- [Papers by Brianna Morrison](https://www.brianamorrison.net/papers)

### Bonus
- [St. Louis City Museum](https://www.citymuseum.org/)

### Timestamps
- 00:56 - Spreadsheets as programming
- 04:57 - When do you build software vs use what's already there?
- 10:14 - Direct instruction vs independent learning
- 20:28 - How should you start teaching kids?
- 24:39 - Is teaching kids different than older students?
- 30:15 - Using rote memorization and saying code out loud
- 35:15 - What is the role of Computer Science education?
- 40:42 - Teaching IDEs, Git, Debugging, and Code Review
- 45:43 - Problems with teaching Open Source
- 49:12 - Incorporating live coding into university lectures
- 56:18 - Podcasting and conference speaking

---

## Transcript

[Click here to help me correct the transcript on GitHub!](https://github.com/jeremyjung/softwaresessions/blob/master/content/episodes/2019-09-27-how-to-teach-programming-with-felienne/index.md)

<div class="transcript">

**Jeremy** Today I'm here with Felienne. Felienne is an associate professor of computer science at Leiden University. And she's really passionate about programming education. This includes everything from promoting the power of spreadsheets to researching how to improve programming education for kids. Felienne. Welcome. 

**Felienne** Thank you Jeremy. 

**Jeremy** So the first thing I wanted to talk about is you have a reputation for being really into spreadsheets. Why are you so passionate about spreadsheets? 

**Felienne** Spreadsheets are the best programming language in the history of computing really people laugh if I say that but it's very true spreadsheets are such a good programming language. So people can just pick them up and dive straight in Imagine doing that for Java first you have to install Eclipse, which is not easy and then you open an IDE. What do you do? What do you even enter? Whereas if you open a spreadsheet, you know what to do with it. The concept is so intuitive. You just start with data and then a little calculation. Oh, I need more. Hey, maybe I need a pivot table. Maybe I need Visual Basic nowadays. You can also script with JavaScript which is a little bit easier and closer to what more people might know than Visual Basic. So it just this the threshold of starting is so low. It's so easy to get in and then build bigger things. I actually think programming language could learn quite a bit from how the excel user interface is designed 

**Jeremy** hmm. So that's kind of like the I guess you could call it the onboarding experience where somebody you show them a spreadsheet and you don't have to necessarily even tell them anything. They can kind of start to figure it out on their own and see like, oh, you know, I want to add numbers here. I want to do these kind of calculations. It's sort of so intuitive that they don't need to go through some complicated tutorial. I guess that's that's one of the big things for you. Hmm. Do you know sort of the history of how people first got into spreadsheets? Like how did we come to that being a good solution? 

**Felienne** Yeah so I know a story. I don't know if it's true, but I can tell you the story. I know so I know the creators of visicalc. This was one of the first spreadsheet solutions. They were in a lecture about accountancy. On the Blackboard. Imagine this big university lecture hall with a very big Blackboard and a professor that was doing. Financial calculation so he was manually creating a spreadsheet updating a number

**Jeremy** on the Blackboard. 

**Felienne** and then going to another example

**Jeremy** Yeah. Mm hmm

**Felienne** on the Blackboard and updating the value there and it was it was a financial calculations was like, oh, let's say we sold 500 trucks today. Oh that's this amount of moneys. And what is our interest rate? And what is our capital we have to subtract. 

**Jeremy** Yeah. 

**Felienne** but he was doing that on a Blackboard and as as the legend tells those two guys from visicalc they knew Computing they knew programming and they were like wow, you could do this with a computer and it would be so much easier and this apparently is how the first spreadsheet solution was created. 

**Jeremy** Interesting. So it's mapping like something you physically do into just doing that same thing on a computer. 

**Felienne** Absolutely. It's very much based on this idea of bookkeeping that you do in already in rows and columns. 

**Jeremy** that's true. 

**Felienne** a closeness of mapping between a real situation outside of the computer bookkeeping and an application on the computer 

**Jeremy** Yeah and I would guess that we've had sort of this idea of rows and columns for hundreds or thousands or who knows how many years right and taking all of those sort of experiences people have built something that really works for them and all we did was put that on a computer

**Felienne** Yeah, absolutely this and this idea of rows and columns goes way back in my thesis. I had an example of a stone tablets of I don't know 3,000 before Christ where rows and Columns of the I think it was Pythagorean triplets. We're on the stone tablet in those rows and columns spreadsheet like format. it is really very old 
**Jeremy** a spreadsheet on a tablet but a stone tablet. Yeah. Wow, that's crazy. So another thing is early in your career. You sort of came to the realization you you worked at a financial company, right? 

**Felienne** Yeah I did an internship 

**Jeremy** Okay. I believe you were tasked to build a domain specific language to help them do their job right and but you decided that they actually didn't need to have a new language or a new program built for them. And so what I wanted to go into is is how did you come to that decision? How did you decide that what they had was good enough. 

**Felienne** So maybe first let me explain why I what I initially thought because I think that's interesting too because when I was in university. I very much was told that non-programmers needed programmers to do anything. I'm not really sure if this is still taught in University, but I think this is still an image that is in the minds of many programmers that non-programmers cannot do anything. They don't even know how to double-click whatever they really need us to-do-do programmers to the rescue. That was my image. So my idea was not oh I'm going. To see what they're doing or to be interested in that. I was just like, oh I can it was from a place of wanting to help them. It was very much oh I can build something and they will be so happy because they don't know how to do anything of course, and then I started to look what are they already doing and they were doing quite powerful things which spreadsheets creating investment models and forecasting all sorts of budgets. But they do know how to use computers. They do they maybe don't do it in our way the pro pro pro textual programming language way, but I find this very empowering and it was also empowering for them. So I don't need IT. I actually don't really like those people because they always takes forever I go there and ask for an application and then six months later they've built it and it's not what I want. So I don't need that I can do it myself so that I think made me think okay. Suppose, I would build a domain specific language for finance. It has to compete with what they already have. It has to be better than an Excel with some scripting and some macros. That's clearly not possible. 
**Jeremy** it's sort of you you realize that hey these these people are way more competent than we give them credit for. You know, they they know sort of their their domain. They know how to use a computer. They know how to use a spreadsheet to get what they want. And so why am I inserting myself in and saying I'm going to build you something it's going to be great, but you got to wait for half a year to do it, right? Yeah, that's. Like I think on a broader scale past just spreadsheets what are sort of key things you think people should look for when they're deciding on whether or not they need to build something new?

**Felienne** Yeah, that's a very very good question. Of course is not known easy. Answer to that. I think in many cases. Some Python scripts or some spreadsheets or some small things might already be a solution to many business problems. And this is also something non-programmers know I know many places where some people have hacked some stuff together with a few scripts and it actually really works. So I think the. The Guiding principles should really be to have a good conversation with people that are going to use your tools and also take into account that requirements might change a lot. So you need to make something. Is easy to change by them or by you? And you also need to have the time and we have time now to build something. But do you have time every month to make some changes Financial calculations can change very often. So this empowering the user to make new changes should really be at the center of your design and often of course it isn't there's oh tell me what you need. Oh, this is what you need. Here it is. Yeah, but that was what I needed six months ago 

**Jeremy** Right

**Felienne** now I need something else. 

**Jeremy** Yeah, so as programmers, you know for us I guess it's probably easier to build something that's very rigid that the user can't change right but you're saying that what's actually better for the user is something that they can change on their own which may not be custom software. 
**Felienne** Yeah, absolutely. I once chatted with his CTO of SAP and he said that the most used button in the SAP software is the export to excel button because SAP is is quite a rigid system and it's be quite expensive to to get an extra report in so what users do if it doesn't support the report they wanted dump their data into Excel and they run their analyses there and then maybe they'd manually upload it back through the system or they just have this shadow thing.

**Jeremy** Yeah. Yeah, SAP is an interesting example because I think sap itself is very customizable, but maybe not easily. So I guess. 

**Felienne** And probably not by end users

**Jeremy** right not by end-users. 

**Felienne** because they wouldn't know how to but also because you just can't you need to hire a consultant to to tweak all the right buttons for them

**Jeremy** Right, so they have built it to be easy for a consultant maybe to configure but but definitely not for the end user. Right cool. The next thing I'd like to talk about is, you know, one of your big missions I think is to improve programming education for kids. One of the things that I think really distinguishes sort of your experience from other people's is when it comes to programming for kids or Just programming in general. I think a lot of people. They have opinions but they don't necessarily back it up with any real data. And so I wanted to kind of talk about your research in that field. Like what are the sort of specific things that you learned and the things that you research in the papers and so on.

**Felienne** Very true. I think there's there's a big case of survivorship bias in programming. So most people that made it into programming are people that told themselves programming as a young age in my talk yesterday. I talked about the stack Overflow survey of 2019 if you look at their data. I chose that 85% of programmers have learned programming before the age of 19. So before college, probably and a big part of that is going to be self taught because many high schools across the world do not yet teach programming.

**Jeremy** right. 

**Felienne** So everyone that's in programming to generalize a bit many people in programming have taught themselves and clearly this is possible because we have all done it but that very much shapes the image of Education. Most people don't have an image of how a programming lesson should look like because they've never been in a programming lesson the programming lessons they did was probably like I learn programming. I had a book with basic listings and type them into the computer maybe people that are a little bit younger than me. Now, they look at YouTube but it's basically the same thing they look at the program. They copy it. Maybe they'll listen to the explanation on YouTube or they teach each other in a group of friends. So then we think oh, It was good enough for me to just have a book. Why wouldn't that be good enough for everyone, but clearly there's a big part of privilege there because my parents had a computer and they let me use that computer clearly I make mistakes and I wiped my dad's hard drive maybe twice but at least I can remember ones that I did he was very scared he was like, oh be careful with the computer because he needed it for work and still he let me play on it. So not everyone has a computer and not everyone has parents that say oh, oh, it's okay. If you destroying my computer, worst case, we buy a new one. So there's lots of privilege also and being able to teach yourself having enough free time having enough enough trust from parents, but also fitting the image of someone that likes programming because. If you're if you're a white boy, you say oh, what did you do all weekend Peter? Well, I was up all night programming then most people say okay that that seems like a thing you would do whereas if you're let's say a black girl and you say oh I spent all weekend programming. You will definitely get a different reaction from adults. Sadly. That's the way of the world. So maybe people saying is that really for you? What were you making wouldn't you rather be? Horseback riding or dancing. So that's also very much part of it that some kids are encouraged to that do that self-learning. It's fits what people think they should do and other kids are to a lesser extent 

**Jeremy** So I guess it's your sort of thing that a lot of people who learn to it was self-taught and it's because they sort of had I guess the privilege of having the computer or having people to support them. But that doesn't necessarily mean that that's the right way or the best way to teach it, right? 

**Felienne** Yeah. In fact, it's probably not the best way there's quite some research that says that exploratory teaching or inquiry learning is not very effective. If you want to look into this yesterday my talk. Also, I mentioned the paper by a Dutch psychologist Paul Kirchner and the papers called why minimal guidance doesn't work. And that's sort of says it all minimal Guidance just having kids explore stuff. It doesn't work and he studied as a meta-study. So it looks at other studies across Fields across ages of children and they will say well we try to things we explain it to kids or we have them figure it out themselves. And yeah, it was more efficient if we just explain it to them

**Jeremy** Hmm. So how did they how did they perform that study? How did they measure which kids did better? And and how did they treat the kids differently to see who performed better? 

**Felienne** Yeah, so here's another study is a meta-study so I can give you an example of one of the studies. He talks about in his paper. That's a paper by Jones Weller. And in that paper, they had two groups of children sold the same algebra equations, but the first group just got the algebra equation. So very typical like X is 4X plus 7. What is inks traditional algebraic equation and the other group got something like a recipe? So they say oh if you have something of this shape, which can always do is all you can move something to the other side of the equal sign, but then it has to be negative or you may divide both sides by the same thing. So they got a recipe and then they compared on a set of algebraic equation. Who solves them best quickest and with fewer errors and then the group that got the recipes did Banner it's sort of what you expect because they got the recipe, but the interesting thing is they did way way better. So they solve the problems and 20% of the time of the first group. That's pretty spectacular and also they did better on new algebra equations that looked really different from. From the recipe but of course the things that were in the recipe like move stuff through the other side of the equal sign that stuff you need for anything so they can learn that from the recipes and apply that in new problems 

**Jeremy** I think that's that's typically how people learn math right is they when they're in either? It's a. Teacher explaining or whether it's in the textbook. They will walk through a problem right in the textbook or what, you know on the on the Blackboard or whiteboard whatever and then show you kind of this is how you solve a problem and then they'll give you like a whole bunch of problems to solve, you know, probably for homework or something like that. Right? And so so this study is about math right for programming. Is there a specific. Towards programming or how did 

**Felienne** yes. I know there are some studies around programming that. Example that I gave in math that idea of a recipe is actually called a worked example, and I know their studies know by heart, but we can put them in the show notes later and they're also papers that have looked at the worked example effect for programming and it was also present 

**Jeremy** And so there's this work effect example, could you kind of explain how they ran the tests? Like, how did they sort of come to the conclusion or how you would I guess, you know, we could use say JavaScript or python teaching someone that is an example. Like how did they sort of run the study? 

**Felienne** so I don't know these worked example papers by heart. Brianna Morrison is one of the people that has worked on this. I don't know them by heart, but typically studies in education are ran in a similar fashion where half of the group gets an intervention and the other half is a control group and then you can measure who does best. So I imagine that these studies to were ran in a similar 

**Jeremy** way.

Mmm, okay. You also have a few studies of your own right and one of those I believe you were saying it had to do with surveying code clubs people. I guess maybe you could kind of go into that and explain 

**Felienne** Yeah, absolutely. So one of the reasons I go very interesting and interested in programming education is I was teaching in a Code Club myself on Saturday afternoon every weekend. And the kids were not making as much progress as I thought they could theoretically make I was thinking of me as a 10 year olds like. Why don't you work on this for six hours during the week? Why is it this this one hour? So they were not really making  programs and then I got interested in why aren't  they making programs? And then I chatted to a bunch of people at many developers conferences also people that run their own clubs and I saw that they were all doing it in the same way that I was doing it mimicking my own childhood experience. Hello kids. Here's some books here some tutorials pick a computer. Go have fun. I'm in the back drinking coffee feeling very good about Community doing community service. 

**Jeremy** Yeah, so unguided 

**Felienne** education. Exactly. But of course just asking a few people, you know, that's not really scientific. So we set out to do a big survey across the around the world and we asked people on Twitter for example and mailing lists and the coder Dojo coder clubs those are groups of clubs that your Club can be part of internationally. So we ask those people to send out our survey and we got a hundred responses. And then we could actually see. Okay. So how is programming taught at code clubs? That's also the title of our paper by the way, and one of the things we found in surprisingly is that 71% of the code clubs that we sampled indeed uses this Independent Learning style where each child works on their own projects and if they have questions, they ask the teacher but it is not direct front front facing instruction where

**Jeremy** Right. Hmm. 

**Felienne** a teacher explains something so it's very much. un-school like. 

**Jeremy** are these kids coming in with no programming knowledge or kind of I guess what are the club's look like? 

**Felienne** good question. I think we ask this in the survey, but I don't know by heart. There's probably a difference between some clubs where kids have experience and some clubs where kids do not have experience. One thing that we found that I do know by heart is that many of the club's had mostly boys half of the club had more than half boys, so that is one of the issues also we know that if you have lower self-efficacy, you have lower self confidence then exploratory teaching is even worse for you than if you already have some background knowledge and some confidence because if you're adding a few things and you're not worried that you look foolish you can ask questions. Whereas if you have nothing you don't even know how to ask a question and if you ask a question and maybe people will say. That's a stupid question. How can you not know that?

**Jeremy** Right. 

**Felienne** so that's that's even more detrimental for a specific group girls that's already underepresented. 

**Jeremy** Mmm-hmm. So for the students that it was more of a guided learning whether this is the study or whether this would be your own experience. How would you start teaching kids? Like what would you start teaching them as far as programming goes? 

**Felienne** Yeah, so that's that's of course a very interesting question. And we as a field not just we my research group. We don't really know yet. So for mathematics, we're sort of the jury's sort of out we know we do addition and subtraction and a multiplication sort of builds up upon each other before program. We have what do you do first Loop or condition or a variable they are orthogonal in a sense. They don't really depend on each other and the issues with a loop is that the instruction pointer goes back up in a sense. Whereas first you've taught the children oh the the compiler reads from top to bottom and then now you go back that is hard but for condition not all lines are executed that is hard you have to mentally in your brain.

**Jeremy** It's a lot. 

**Felienne** but a variable also has has lots and lots of different complications misconceptions is how we call them ways that you can misunderstand the variable. There's so much research about how you can misunderstand variable if you have lots of experience already with mathematics, you might think that a variable Can Only Hold one value. because in a proof in Mathematics you say oh Delta is 0.1. You don't go in the middle of your proof. Haha. Now Delta's 12. It's just it's not really a variable. It's more a constant in the scope of a problem or proof. So if you come from a math background, you might think that the variable Can Only Hold one value and some children think that some children think that if variables are created. They have a default value. They are always zero for example. It make sense. We could have made programming languages in such a case that everything starts with an N value. I mean Tony hoare has said that null values were his billion dollar mistake so variables should have an initial value by default. It's not it's not wrong thinking in a sense that that could be the way it works. So variables also have lots of issues. So where would you start it is not easy. 

**Jeremy** So you're still still trying to work on that problem, 

**Felienne** so that I can tell you what we do now and I teach in python in high school and in Netherlands High School start at 12, so they are bit younger than people might typically expect from the American system and there we start with variables and then conditions and then Loops. That's the order we have now because variables allow you to build many interesting things initially. So that's nice and conditions keep the mental model alive that the code goes from top to bottom which is really something that students struggle with so I want to train that as much as possible before I have to break it with a for loop so that that I can say, okay remember how everything's goes from top to bottom. It is almost true. Do not forget it. It's just it was a tiny lie not a big lie. 

**Jeremy** Yeah. 

**Felienne** But I don't know if that's the best way in these type of things are very hard to measure if you have a small intervention like you use JavaScript and you use Python for three weeks that is easy to measure but if you have such a trajectory you have five weeks of a variable and then five weeks of a loop, maybe five weeks of a condition you get a very very long running study and then there's lots of risk of contamination because the students if it's in one school, maybe they talk to each other if you have ideally you would have randomized groups, but then that means they're in the same school. So then they might learn from each other. You cannot prevent them from chatting with each other. 

Whereas if you say we do one group in one school and one group in the other school schools are different. 

**Jeremy** Yes, absolutely, 

**Felienne** teachers are different conditions are different for both schools.

**Jeremy** Absolutely. Mmm. 

**Felienne** So the bigger the idea is that you want to test the harder it is to do it in it in a pure way. I mean, ideally I would kidnap 300 children lock them in my University and teach them for 10 years and then measure the difference, but my Ethics Committee will not let me. 

**Jeremy** You might get some amazing programmers though,

**Felienne** yeah. Yeah, or they will all be traumatized.

**Jeremy** Mmm that too. Yeah, so. How would you compare you know this experience of teaching high schoolers to you know, someone who's older do you think it's the same should you follow the same process or do you think it's different depending on how young you are?

**Felienne** That's a very good question. So there's quite some research that says that. If people learn a new skill, then they will fall back to behaving like a baby basically you have the development levels of Piaget. And the lowest level is called the sensorimotor level. Imagine a baby has no hypothesis of the world just grabbing stuff to figure stuff out there Neo-Piagetism says that if you're learning a new skill, you will basically behave like a baby and I recognize that in programming. So if I learn a new programming language. I did an Elm Workshop a while ago and I hadn't done Elm before I look at Elm. I'm like, oh, I see something an equal sign that make I grabbed onto it like a baby. I'm like, I see something I know I am unable to read a whole program or even a line of Elm at once because it's too much. So I really recognize that sensorimotor level of I can see tiny pieces I am I I do not see everything at once. Whereas I see a Python program of a hundred lines. I can scan in a more or less see what's going on. So I think that hypothesis is very true. And I think that the most things that we know that work for young kids also work for. Learners if they're novices if they really at the beginning of their career.

**Jeremy** Right. Okay, 

**Felienne** So that would argue for there's no difference but there's quite some differences in my experience between teaching high school or Elementary schoolers and undergrads, but that more has to do with their self image and their image of each other. Because if an eight-year-old is confused. They will tell you they will be like I hate this I do not understand anything you said to me they will tell you especially if it's in a Code Club, they come there voluntarily they didn't they do not have to come back. They'll just say I'm never going back to your stupid Club. I hate this which is it hurts, but it is very useful. They will they will assume it's about you they will they will have not internalized that if they don't learn it's about them. Whereas undergrads especially if you're teaching it in a good school, then they will have this self image of being smart. So and often they go to high school through High School. Not studying a lot because they're just smart kids and then they come into a computer science program and everyone is smart. So if they don't understand something they'll just go home and cry in their dorm. They will not tell you that they hate your stupid lecture and that they're never coming back if they're never coming back. They just do that. So in that sense it's really very very different because you do not get that feedback. You can ask a group of undergraduates. Have you understood everything and then you're like yes teach. We understood everything. Thank you for the lecture. So that's very different and we know especially again talking about minority students. We know that girls already at the age of eight or nine have internalized this programming and technology is not for me and this is very much true also for all the older you get as a girl in this world the harder it gets because the more you have been exposed to. Books and TV shows and ads saying not for you programming. It's not for you. It's only for white boys. So that makes it even harder if you're older to ask questions. I've had this I told an undergrad course where a female student asked a stupid quote-unquote question that she might have known before had she also been programming for 10 years and then the whole lecture halls like how can you not know this? 

and then, they will never ask a question again.  that is really an issue and it has nothing to do with those cognitive levels of understanding. It just has to do with what the world has already thrown at them.

**Jeremy** You think we can sort of change that culture or change that perception? 

**Felienne** Yeah, it's very hard. As I said, it's so much survivorship bias of most people that are here have learned in that way. I think code boot camps. Is it there they like everything have some pros and cons. I have some issues but one of the things definitely beneficial about Boot camps is that they are bringing in people that learn programming when they were 20 or 30 or 40 and they're coming into the community. We are recording this at the strange Loop conference and I spoke to many people this weeks ago. I came into programming as a boot camp that dilutes the self Learners in a sense. So that changes the population and that will also change the way people view education because people that went through a boot camp have an image of how they learn programming it might be last year. So they have a really good image.

**Jeremy** Mmm. 

**Felienne** So that is definitely one of the things that might change your opinion, but also I like to think that the things I say in talks like rote memorization is really important if you're learning programming. I hope that also changes people's perspective to a certain extent that if they start teaching their children or other people's children that they think oh, maybe I shouldn't just hand out the basic listings. Maybe I should just explain the basic elements the important syntactic pitfalls and the important concepts explain it to all the kids. So then also kids that are nervous to ask a question or they just have no background have a fair chance of getting the information. 

**Jeremy** I kind of want to go a little bit more into the rote memorization. So I think a lot of people are familiar from school rote memorization trying to remember how to spell words or or things or the multiplication tables things like that. What does rote memorization look like in the context of programming?

**Felienne** That's a really good question. We don't know exactly we've tried some things but the most important thing for now I think is first as programming community to accept the fact that rote memorization might be a thing that will actually work in programming. So first I want to spend a little bit of time explaining why it works so well, so why do we make children spell out letters is because they then automate spelling the letters and that frees up mental room to then read words at once after a while you don't have to do. Bo-o-k anymore. You can just do it at once and then even with sentences the same is true for tables of multiplication. Why do you have why do we have people still rote memorize 7 times 6 we have a calculator on your iPhone. But the fact that you can do 7 times 6 is 42 at once that frees up mental room to make bigger calculations that if you see seven times six anywhere you're like, oh that's 42 I can do it. So that's the value of rote memorization. It isn't necessarily that you have to memorize all these values because yes, you can look up you can look it up with Google. It is that it allows you to build bigger program build bigger structures. In the same way, we think that it will work for programming because if it doesn't take you any mental effort to write a for Loop, if I am in python I tell this to my high schoolers if I sneak into your room in the middle of the night and I wake you up. What do you say for I in range open bracket for closing brackets colon. They can do this and I tell them you have to be able to do this just like the tables of multiplication. Why because they're solving a problem and their brain is already full with oh I have to reverse an array. There's almost no space then it should take them zero effort to produce the Syntax for a for Loop because then that takes no effort and then oh nested Loops that takes no effort because it's just a loop which they know inside another loop it's really all about. Having we talked about that in my keynote yesterday chunks having these elements in your brain that you can easily access with no or hardly any mental efforts and then of course people in programming will say yeah because you can Google the syntax. Yes, but if you're in the middle of everyone knows his feeling like you're in a middle of a problem and it's very annoying if you have to then look something up or then your compiler says oh this is wrong. And of course if you're an expert you can you can keep it in your brain you're like. Oh, I missed the closing brackets without losing everything. But especially if you're a beginner a compiler telling you there's a spelling error or syntax error. It will just break the whole house of cards in your brain. So that's that's why we think that rote memorization of syntax is really very important. And we do this in almost a drill style where kids have to have to be able as I said if I shake them awake in the middle of the night to produce python syntax by voice. 

**Jeremy** Yeah, so I think that was also one of the things you mentioned in your keynote was the importance at least within a classroom setting of having the students actually say the syntax right which I thought was interesting.

**Felienne** Yeah, so one of the things how do you do rote memorization? Well doing this vocally is a thing that works really well also for math. We do two tables of multiplication. We say them aloud there. You could also do it in silence, but it's easier. I'm more effective. If you do this aloud we suspect the same thing is true for programming. So we need we did a study where half of the group read code aloud with us in this multiplication table all the group at one style and the other group then they'll do that and the first group did better on the syntax that test at the end of the lesson lecture series. 

**Jeremy** Yeah, so basically applying things that we have used for Generations but applying it to programming and it turns out it works.

**Felienne** It's not very surprising. But then again it's also cool because it goes against what people in programming believe in general because I believe oh, it's not about syntax. You can just look that up. It should be fun. You should solve problems. So it is on one side is not very surprising. But it also forces us as programming community to accept that. Yeah, we are like everyone else it's not like like programming is this magical thing. That's really different no, it's just like math and just like language. 

**Jeremy** Yeah, earlier you were talking about how boot camps are bringing in a lot of people who, you know weren't programming as a kid, you know, they're coming in getting more sort of direct instruction things like that. I wanted to sort of go into what you think the role of traditional Computer Science Education is now that there are so many options whether that's a boot camp or that's an online course or self study that sort of thing. 

**Felienne** That's a very good question and it's very hard to of course to talk about that if you're also a university professor in computer science departments, because many of the things I say are like about my own students and colleagues, but I think in general everywhere in the world computer science programs are struggling with who are we. Teaching who do we want our students to be at the end of the course because many universities especially initially early in programming education. They were educating scientists computer scientists. So and now it's a people are Computer Scientists, but they're actually a programmer so much many programs are still very much developed. Also the program at Leiden where I teach too instruct people to be a scientist. So they need to know about algorithms and data structures because that's what you need for science. I know there are professors that say, oh we don't teach the use of an IDE because they can learn to use an IDE if they go through industry. Whereas on the other hand industry wants people that just know programming. They want people to know front end development and they do want them to know IDE and code reviews and refactoring skills. And then there is this tension between wanting to teach scientists and the scientific matters and reproducibility and stuff that's important in science and just quickly getting programmers in industry and I think many programs across the world is as I said also my own program have this sort of schizophrenic view of yeah, but it shouldn't be too much practice. We want we still want them to be a scientist whether if you look at the statistics, I don't know. I don't have the numbers. 20% maybe of computer science graduate students go to do a PhD and and and and even fewer, of course really go on to science. Then after the PHD many people with a PhD they still go into industry. So most of our graduates actually go into industry, where's the programs are leaning towards creating scientists still. So maybe that's not an answer to what is the role of University programs, but that's my answer of the why is there a problem? We also want to recruit scientists we want to teach for that but industry has requests from University so I do think there's still tremendous value in getting a University degree. I still have lots of use for the things I learned in University I took like five compiler courses. I know I should have taken a history and philosophy course, but I was like, oh, I love compilers, but it's very very nice because we were talking about chunks. If I see a problem I can think oh, this is a problem that needs its own programming language. It's a tool. I know I can use and that's a very valuable skill. So I'm so very happy about my education and I think it told me many things but I can see how boot camps also have value especially in a time where some professions are not in that demand anymore maybe at one point you will have self-driving cars and then taxi driver and truck drivers need to do something else and there's a huge shortage in programmers. So it's great if they can go to a six-month Boot Camp and find a job that they like and that pays well. I don't think it's the one or the other 

**Jeremy** Yeah, um, what do you do? You think that the because you were saying that maybe 20% of the students that go through your program end up going into higher education right getting phds for the students who, you know plan to go into industry right after school, you know, would you still recommend that they go for you know, a full computer science program? 

**Felienne** Yeah would be weird if I said no, but I guess it was a very much depends on where you live and what your personal situation is because going through University, especially a new us could be very very expensive. So it might not be worth it in the country where I live tuition is two thousand Euros a year 

**Jeremy** Wow, 

**Felienne** that that's 

**Jeremy** really cheap. 

**Felienne** We think is pretty expensive. It used to be cheaper when I was in university, but that's a way different equation than the thing. So in the Netherlands, I would say yeah. Sure. Yeah. Yes, absolutely and also in our situation expectations are different because most people will expect that you went to University because why wouldn't you it's not that expensive so it very much depends on where you are and. 

**Jeremy** Yeah, so it's yeah, I guess that's a that's an interesting point that if education is, you know, pretty inexpensive, you know, very accessible than like you said why wouldn't you do it and I think you know here in the US. You could go to university and you could end up, you know, by the time you get out. You could have a hundred grand in student debt, right? And so that's yeah, that's a that's a perspective. I hadn't really thought about that, you know other countries, maybe the decision decision isn't as hard to make. 

**Felienne** At least it's a different decision 

**Jeremy** Another thing I kind of am curious about is do you think that because you were saying that industry is expecting certain things like how to do how to use an IDE or how to do code review how to do Version Control. Do you think that these Concepts should be taught in University? 

**Felienne** Yeah. and not just because industry but also because science I also want my PhD students know about Version Control because it's a very handy skill if you're writing a script. For example, we had another paper where we we downloaded 250,000 scratch programs and we wrote a static source code analysis tool to analyze those programs so that's pretty engineering work. So I want that script also to be Version Control because at one point you're looking at the paper like hey, that's a weird value. Let me look up the data set and let me look up the code that actually produce this value. So lots of scientists of computer science is also engineering work. So I think those skills are not just valuable because people need them in industry. Everyone needs if you're programming you need Version Control, you need good command of an IDE stupid stuff like the shortcut for quickly commenting out a number of lines of code. I have this in my exam. I ask any exam. What is the shortcut for commenting out code? I got some shit from some people because they're like, yeah, it's it shouldn't be a button course about what buttons do use but this is a tool again that you can use because if you're debugging a hard program because like I don't know what to do. I want to comment out these 10 lines. 

 If that means you have to go in front of every line and put a hashtag there. Then you're not going to do that. It's not going to be the first thing you try because it will take much effort. But if you know, you can select the lines and you can do command question mark then it takes way less energy. So that means that that's a tool you can. Grab from your toolbox more easily so stuff like that. It's just not because industry tells me I need to do this but because it's just a valuable tool for programming whatever you will do with programming 

**Jeremy** Yeah, and I definitely agree and what I would also kind of ask is so you because you were saying at your University now you teach all these things right when you went through school yourself. Let's say when you did undergraduate did they teach any of these kinds of Concepts? 

**Felienne** not really. 

**Jeremy** mmm. 

**Felienne** I wish I had made notes of going to University now. I wish I had a diary of all the things they taught me because I want to say no they never showed me but I don't know 100% 

**Jeremy** Right. 

**Felienne** definitely I ended up at the end of undergrad or let's say the end of my masters definitely knowing about Version Control knowing about refactoring support and knowing about all these IDE tricks and the putting breakpoints. I don't think we learned something like breakpoints. I don't think I learned that I know we had one course that was like a project course and I think there were some Version Control. It was still subversion because I'm that old.

**Jeremy** Yeah. 

**Felienne** I don't know if I learned this like from a teammate that already knew this or from the lecture but breakpoints and debugging certainly there wasn't of course in it. 

**Jeremy** Yeah, I mean I in my own experience when I did a bachelor's program they did not teach Version Control. They did not teach debugging they did not teach the IDE. It was kind of sort of the fundamental concepts like you would learn about data structures or compilers and so on. And they actually, you know, they in some people would think this is a good thing. You know, they said oh you can use whatever language you want. But because they did that they also weren't able to really teach to a specific language. And so I think it's I don't know. I don't know how you sort of balance giving students the freedom to do what they want. But at the same time also be able to give them the tools so that you know, they can they know what to do. 

**Felienne** And especially about the programming language because there's also some research that shows that the programming language, you know also influences the choices you make there's a super cool study by a German guy called Lutz Prechelt and he had students implement a tree algorithm in and then students with a background in different programming languages and then all the Python students are like sure you use a hash map and all the Java students are like no you use a dictionary or something like that. So they use different data structures because and it's not just because a programming language doesn't support them because programming languages anything supports a tree it is because the culture of the one programming language says hashmap. That's the thing you would always use any other programming languages dictionary that's what you typically pick. So teaching a course without a programming language is also sort of weird because there is a relationship between a programming language and a data structure that you might not be aware of otherwise, 

**Jeremy** I also think maybe even teaching a little bit about the concept of Open Source and having people understand these libraries that you're using kind of where they come from and you can actually look at the source for them that sort of thing. I kind of wonder if maybe if that should be discussed in studies. 

**Felienne** Yeah. So on the one hand side, I want to say yes, we want to teach students about open source, but on the other hand side open source is such a toxic community. I mean Linux and Richard stallman and they're all quite terrible and not just that they're terrible. I mean that's already terrible, but they continue to be terrible for decades women and black people continue to point out. How terrible they are. There was this, you know Stallman was in the news on Twitter again this week for defending Epstein. No one I know that's not a white man is surprised they're like, yeah, we've been saying he's an asshole forever and same thing with Linus Torvalds. They're assholes but not only do they remain in the community. They are defended by basically everyone. So for that reason, I would be very very reluctant to teach open source because I know what I will be exposing my female students to I wouldn't feel very happy about 

**Jeremy** I guess even you know, well, I guess one of the things I would say is maybe one of the reasons why you know, there is this level of toxicity is maybe because of the people who are contributing right? And I wonder like. You know, should we be educating so that we can get more people, you know who are different right 

**Felienne** yeah, that's this is the very good question. And this is almost a question of institutional change in general. Like should we bring in more women? So that other women after them have an easier job should we take this institution whether it's Academia or industry or open source. Should we take it as it is and try to change it a little bit by having a front group of people changing the culture slightly or should we just say well this thing was just shit from the beginning let's burn it to the ground and build something new. I don't know. It's very hard because many of those institutions which has existed for a long time but changing the fundament of something is really very hard. Putting it on people to say. Oh let's let's all go in to open source to change it a little bit it will take lots and lots of energy. So for me looking at open source has never been worth it because I look at I see how it is and I don't feel it. I got enough shit for just being a female professor in computer science department. I don't need that extra shit, but I totally see what you're saying that yeah. We wanted it to change. Only saying it's shit, might not change anything, but can't fight anything. I guess you just have to make changes pick your battles. 

**Jeremy** I guess the next thing I would ask is, you know, you've been teaching for how long now? 

**Felienne** 6 years in university. 

**Jeremy** So how would you say that your teaching style or what you choose to teach has changed over the years. 

**Felienne** All that's a great question. I should write a blog post about that. So definitely the direct instruction approach of explaining stuff that I'm doing. Modeling so telling students. Hey, I'm making this decision now and that's because such and such. I'm also relying more and more on live coding in class. So right around having slides with syntax. I was preparing for a course a new python course last week and I was like, oh everything I'm preparing is just code snippets. I don't have. I don't have slides. I have a bunch of slides like these are the deadlines and administrative administrative stuff but then all my explanation it's all in the brow it's all in the IDE, so it's just use a code snippet. This is how you run it. This is a variable and that allows me to interact immediately with the code and that also allows me to from the beginning show them IDE short cuts. For example. 

This is how you start your code. We use Visual Studio code. This is how you start your code. It is of fn f5. You start the code with a keyboard shortcut so you don't have to right click run the code. So then they can see this is how Felinne it uses the IDE. Oh, I don't need that line. I will comment it out command question mark so they picked that up and it also allows if students have a question great questions, like what was this. This was such a great question. Oh, yeah, this was about refactoring. So I was showing how to refactor a variable name and then one of the students says, can you also refactor a string constant? 

**Jeremy** Oh, yeah. 

**Felienne** Can you right click it and then refactor it? I was like that's a good question. Let's see what happens if we try it so you immediately react to that and I thought it was very interesting and then he said Oh, I thought it was a stupid question. I was like no, it's a great question. I can imagine several scenarios where you want to refactor your string constants because you've changed the name of something. You also want the labels to go with that to also change so it's like no it doesn't work like that, but. In a while, you can build your own programming language and you can make something where it does work like that so that live coding is very valuable, but I wouldn't necessarily recommend this to beginning teachers beginning professors because you need to be really quite knowledgeable about the programming language and about your programming tools. Which is not that easy if you're an academic, maybe you don't have that much programming experience. Or you need to make room in your schedule to learn all the tools? And sometimes you'll make mistakes. I have tried to implement bubble sort and then in a course and then I made a stupid mistake. It was something wrong with my my Loop condition and then it just broke and then you're like now what do I do? And then of course one student says yeah, maybe you should change that into a bigger and larger than equals or something and I go oh that's it. Well thank you. 

**Jeremy** Yeah. 

**Felienne** you move on but you also need that self-confidence. So it's not a thing. I don't think it's bad. I didn't do that six years ago. I think it was a good decision. But once you can do it, you can really teach many things in that context 

**Jeremy** and. I guess in doing so did you actually do you actually practice sort of what you're going to do in class, you know, as far as the live coding session or is it more you just know what you're going to do and so you just do it?

**Felienne** Yeah, so I do practice a bit. So I have this all these files are all small files and you're like file one underscore and then the name of what I'm do. So I there is a line a buildup in what I'm going to do.

**Jeremy** I see. 

**Felienne** So there is some I run all the code before and I put some I hide some code snippets in the back of the in the underneath of the file. At the end. some new lines so they don't see it. But if I'm really stuck I'm like, okay, I'm stuck. I'm just gonna get this code snippet from my secret stash. So you need some preparation. But of course also if you makes slides you need some preparation. 

**Jeremy** I kind of. I guess it goes both ways in terms of when I think when you make mistakes, I think maybe the students will see a little bit of themselves as well. You know, or they'll see your thought process 

**Felienne** and if I make a tiny mistake and I sort of know what I did wrong, then I it's definitely a learning opportunity for the students because and I can just vocalize and say okay, I'm stuck. I also don't know what to do. So what am I going to do? Okay, I'm just gonna comment out everything except for the first line. Okay, that's it works next line or okay, I'm gonna put a breakpoint in there and inspect the variable so it can definitely be a learning experience. 

**Jeremy** Yeah. 

**Felienne** this is something we don't talk about I think many you describing your experience very representative of many undergrad programs where they say oh, this is data structures, but you don't really get experience in practice practical stuff. So of course about hey, I'm stuck. What do you do now that that's lacking in many undergrad programs. So that isn't this situation is an opportunity where you can say, okay, everything is broken. 

**Jeremy** Yeah. Yeah. I mean it's um, I guess it depends on the language. But yeah, like you said live coding I think is really helpful just to see someone solve something right or walk through a process. I also think that REPLs are really helpful to is like being able to type something in and see immediately. You know what the result is supposed to be. So yeah to me. It makes a lot of sense to you know to have live coding and you know, not just do slides because ultimately that's what the person will be doing when they go back and they work on their project or their homework. They're going to be going through the same things you are. 

**Felienne** Yeah, definitely and actually one hybrid thing I use this is for teaching in a high school that we have slides that are online on slides.com. Super nice. They're not paying me to say this and that you can make slides, but you can also embed code in the slides. So we actually embed from a website called. REPL.it That this is a REPL in the browser. We embed code within the slides so you can have a slide and you click to the next slide and then there's Python and you hit run within the slides and it runs there you can change the code in the slide and it runs.

**Jeremy** That's really cool. 

**Felienne** so that's I prepared lesson materials for another teacher in high school. That's not a computer science graduate he has a math degree so he knows some things but not all and he uses those slides and that works really well because it's a nice combination of he doesn't have to know everything because some stuff is in the slides but the students still get this experience of seeing code running and they can ask questions. Like Hey, will this do he also doesn't know but that's fine because they can try sort of together. So I think specifically in the context if you're not a very experienced computer science person yourself, you know an experienced programmer, then you can also have this hybrid form of some live coding than it's not that scary. 

**Jeremy** I guess the next thing I'd like to talk about is so we're both host on the software engineering Radio podcast. You've been podcasting for I think over three years, right? Yeah. So what what excited you or what got you interested in podcasting? 

**Felienne** So one of the things is really cool as you get to meet amazing people. It's so cool. You just send someone an email like hey, can I interview you for my podcast and they'll say yeah sure. Well, I have one and a half hour to chat with you about what I'm an expert in. 

clearly that's a great great opportunity

**Jeremy** definitely

**Felienne** to talk to people that otherwise you wouldn't talk to and it's also a really good way to make me learn stuff because we do lots of preparation for a show you have to ask the right questions. You're not gonna get an expert on say, okay. Tell me about your topic.

**Jeremy** Yeah.

**Felienne** Oh, that's interesting. Let me think of a new question about that. But you have to prepare so very often we get books for example from Publishers. We want to interview someone about that book. You read the book. You ask really you think really good 

**Jeremy** questions

**Felienne** Yeah.

You ask them so it's really a learning opportunity.

**Jeremy** I guess is it similar to the reason why you give conference talks?

**Felienne** It's also because one of the reasons I like giving conference talks is I like to like for people to know about my work The normal way that scientists make sure people know about that works is you write a paper and then maybe a journalist reads your paper. like a science journalist and they write a book about it. It ends up in someone else's talk. That's very indirect. So I like to speak about my work because. I mean, my best cited paper has 161 citations. My keynote yesterday. There are maybe two thousand people in the audience. So clearly this is a good investment of my time. So I wouldn't say it's the same because conference talks are really about me tell talking about me or my work whereas the podcasting is more me being a student again. So tell me more about this. I am so interested. 

**Jeremy** That's really cool it's like the conference talk is where you're the expert and you're kind of telling people. Hey, this is what I learned and the podcast is the opposite. It's you telling you know the expert. Hey teach me about this thing that you you know a lot about 

**Felienne** Absolutely yes it's like being a student again, which is a good uh good experience. If you're a teacher and you're like, ah learning is hard. It's good to remember that 

**Jeremy** that's really cool. 

**Felienne** and also, of course. We get to pick our own topics and our own guests. So being on the podcast, especially at software engineer radio it's a pretty big podcast. So if you are a host you can also shape what people listen to you have a decision on who is being interviewed. For example, I try to interview with female hosts often because I think those are voices we don't hear enough. So it also helps me shape the community because we have a pretty big. Really big audience. So that's also nice to be able to help shape the what community looks like and who we see or listen in this case as experts. 

**Jeremy** so over the course of these three years. What have you learned in terms of interviewing people or what do you do differently now?

**Felienne** So that's also a great question. I don't think I do many things differently because those shows are all really all about the expert. So the basic setup is always like. Who are you? Why are you excited about this tell me more in-depth. So I don't think I play a big role in those interviews, of course behind the scenes. I have my ideas on my questions, but in a sense is really very much about centering the other person. So I don't think I have changed that much because every show is different

**Jeremy** the the topics you decide to tackle? You know, have you noticed any kind of Trend in the things you choose or is it? 

**Felienne** Yeah, so many have been about education or a related topic. So we've I did one on code schools on boot camps. So that's I think an interesting topic is very close to what I'm interested in. I'm also very interested in code quality. So I also did some shows on testing refactoring Martin Fowler. So sorry Michael Feathers so stuff like that is really interesting to me and I know a lot about the research on that so that is what I like. And also I think I've had lots of scientists in my show because as I said people don't really read your papers, so if you have an opportunity to get a scientist to speak to directly through the podcast. So I've also had a few scientists at the really interesting thing is like with image recognition and very recently genetic programming automatic programming repair is a super cool technique that I think not enough programmers know about this technique. So then I'm like, oh everyone wants to do this and I try to do that through SE Radio 

**Jeremy** Definitely. Yeah, the automatic program repair. I listen to the episode and I thought wow this sounds like magic. 

**Felienne** Yeah, it's like, oh the program is fixing 

**Jeremy** Yeah, that's awesome. Is there anything else that you you think we should have talked about or that you're excited to dimension? 

**Felienne** No, I think we covered most things. 

**Jeremy** Very cool Felienne. Thank you so much for joining me today. 

**Felienne** Thank you for having me.

</div>