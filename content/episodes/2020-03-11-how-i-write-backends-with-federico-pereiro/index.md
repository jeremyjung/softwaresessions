+++
title = "How I write backends with Federico Pereiro"

description = "Federico describes how he creates understandable and stable backends for web applications."

[extra]
episode_url = "https://pinecast.com/listen/b74cd879-7f89-42d8-b3b0-24e51a14ad36.mp3"
+++

Federico has been writing backends for web applications since 2012 and is the co-founder and chef of alto;code.  He wrote a post on GitHub named "How I write backends" that summarizes his process.

We discuss:

- His current stack
- Redis as a primary data store
- Reducing the number of layers in your software
- How duplicating input validation makes code harder to understand
- Integration tests over unit tests
- Minimizing dependencies
- Why you should never normalize alerts

### Federico Pereiro
- [Personal Site](http://www.federicopereiro.com/)
- [How I write backends](https://github.com/fpereiro/backendlore)
- [Our company](http://altocode.nl/)
- [ac;pic, our pictures application](https://github.com/altocodenl/acpic)
- [ac;tools, our backend services](https://github.com/altocodenl/actools)

### Related Links:
- [Fred Brooks & The Mythical Man Month](https://en.wikipedia.org/wiki/The_Mythical_Man-Month) (conceptual integrity)
- [Steve Yegge - Code's worst enemy]( http://steve-yegge.blogspot.com/2007/12/codes-worst-enemy.html)
- [Steve Yegge - Platforms rant](https://gist.github.com/chitchcock/1281611) (no backdoors, all services talking through the wire as if they were external actors)
- [Book of Hook - Suffer no jankiness]( http://bookofhook.blogspot.com/2012/08/suffer-no-jankiness.html)
- [Taiichi Ohno & the Toyota Production System](https://en.wikipedia.org/wiki/Taiichi_Ohno)
- [Auto-activation in software](https://github.com/fpereiro/teishi#auto-activation)

---

### Transcript

You can help edit this transcript at [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy** This episode. I'm talking to Federico Pereiro about his post on writing backends. It got a ton of attention on Hacker News and GitHub and I wanted to chat with him about it. 

Federico, welcome to software sessions. 

**Federico** Hello, Jeremy. Thank you so much for having me.

**Jeremy** You've talked about how simplicity is very important to you.  what does that, that mean to you when somebody says, software simplicity?

**Federico** Yeah, it's a, it's a great question and hopefully I won't spend the an entire hour talking about this. This is definitely a favorite subject of mine. Simplicity is the way I try to approach all software from all angles. It's always about simplicity.  I've been thinking about what it means for me, at least right now, it boils down to two things.

And the two ideas that I take from different authors. So the first idea is that of a conceptual integrity. And I take that from Frederick Brooks. Who wrote, um, a very famous software development book called the mythical man month in the 60s, which I think for many, still like the Bible of, software development, uh, as a, as a project as an enterprise.

So basically Frederick Brooks essentially says that conceptual integrity is let's say, the core feature of any software system, what he really wants to see in it. And, uh, it boils down to having a few concepts that can describe the entire piece of software you're trying to build and how those concepts interlock with each other at different levels of scale.

And it's very related to how an architect or a group of architects can really understand the entire system and hold it in their heads. So I feel like that's one side of simplicity that is very important. And if I had to really narrow it down, it would be like the idea that I can understand the system in my head without records to paper or even to the code.

And then of course in the details, I will have to get into the code and to the documentation as well. But. I understand the system and others can understand the system.

**Jeremy** You know, you're talking about the concepts that you're going to have in your head without even looking at the code, without even looking at, you know, documentation. Could you give me an idea of like, if you had an application, what are those concepts?

**Federico** Hmm. It's a good question. Let me think. I really have to think about this so. Actually let me give you an example  from a tool that I'm writing right now, I'm writing, um essentially a lightweight framework for creating the front end of a web application, and I'm really trying to narrow down the core concepts that I'm going to be using. I'm seeing that it boils down to two things:

It boils down to event listeners then to events themselves, and then to views. Like for now, I'm thinking that those three concepts essentially can describe all the aspects  of the front end of an application to make it a bit more concrete. Let's say you are working on a shopping cart, right?

You have the concept of some HTML and CSS that you're looking at the screen. So that's basically the view. The view is HTML and CSS, and then, through both event listeners and events themselves, I can model anything. Like for example, getting product information from the server, adding an item to the cart, changing the number of items for a particular thing you have in the cart.

Removing something from the cart, sending a transaction to the server saying, Hey, I want to buy this. So essentially I know that the details are going to be, , perhaps a bit tangled, and I'm not going to be able to hold them in my head. But I can understand that the big parts, the big concepts through which I can describe the parts of the system.

I don't know if that makes sense.

**Jeremy** Uh, so you have the individual things you're talking about, like you're giving the example: the shopping cart, adding items,  checking out, things like that. And what you're saying is that when you're building the application,  you may not know all the individual actions that are gonna happen, but you know how you're gonna accomplish that. Like you said, like each of those things would be an event and then you would have, you know, these event listeners that would, react to each of those actions. So that sort of high level concept, just knowing that you think is, you know, those concepts that you want to be able to hold in your head.

**Federico** Exactly. And through those concepts that you call in your head, that would be at the level of the tool itself. Right? If we're talking about a specific code for an application, then the example would have to be different. Uh, I would have to go like one level down if you want in terms of abstraction and say, for example, this, uh, the shopping cart has, the concepts would be adding something to the cart, taking it out.
I mean, like we would have to go one level down. But the idea is that, uh, the, there's a lot of detail into the documentation and in the code, but you can grasp the system at the conceptual level. And the conceptual view can take you very far. And the conceptual view gives you the skeleton on which you can put metaphorically the meat of the application on top.

You can understand an approach to system in, in that way.

**Jeremy** It sounds like knowing those kind of high level concepts, you should be able to easily go into the code and, and find those details you're looking for without needing some kind of design document or something like that.

**Federico** Mm hmm or perhaps the design document and the documentation are great compliments to it.  It gives you the starting point and it also gives you a rope in case you're feeling like you're sinking into the quick sand. Sometimes I really get anxious when I'm like going deep into a code base, even my own code bases.
So I really feel like, eh, having always the strong concepts that are properly articulated are always a way to take stock of where I am and just make me able to understand the system in a fraction of the time that it would take me to understand another system that has a weak conceptual integrity.

**Jeremy** Can you give me an example of a project where you felt like the complexity was kind of getting out of hand and you, you couldn't keep those concepts, you know, all in your head?

**Federico** Not that long ago I was working, uh. with a certain team on a, on a web application and uh, I felt that there was a lack of conceptual integrity in that. I think at the application level conceptual integrity would mean what are the main entities in our system and how do they interact with each other?

The low hanging fruit of how the entities would work with each other it was worked out, but there were a lot of, um, interactions between the entities that were not really properly specified.  it was actually hard to think about the implications of,  making a change here and the implication is not even at the software level, but more like an application logic layer. Like would this make sense if this was possible or not should we allow this operation or forbid it? And I felt that there was not enough time devoted to understanding how the the entities of the system, which are essentially the pieces of the system will interact with each other at an application level.

And I cannot go more into detail because I don't want to give you like specific details about the company and whatnot. But the feeling was that I didn't have the conceptual integrity. And when I was asking around. Eh, the other people that were working on the code before me didn't have it either, and I felt that was actually hampering the the efforts into advancing eh with a clear and steps on firm ground, let's say.

**Jeremy** So if I understand correctly, when you would make a change, it wasn't clear what the consequences of that change were is that kind of what you're describing?

**Federico** Exactly. You felt, eh, also that things were branching out a lot, like the possibilities, I changed something in an entity and it can affect two or three other entities. It also generated the feeling that, you really could not estimate how much a certain task would take because yes, you could implement a small task, but you didn't know how many new tasks you would create because of that task you already did.

Like how much more work you're going to create by the work you just did. I don't know if that makes sense. So software destined to expand fractally a lot of the time. And I feel like that's why Fred Brooks insisted so much on conceptual integrity because if you outline the concepts well, how they articulate with each other, you have much more of an intuition of where the problem areas are going to be and where you are.

Not to expect many surprises.

**Jeremy** When you would make a change, it wasn't clear where else in the application you would have to also make changes or what you might also break elsewhere in the application.

How would you sort of properly specify those entities? Would that be a part of just the design process of writing the code, or would that be kind of, you know, written down somewhere in some form of documentation?

What does that look like to you?

**Federico** To me, the idea, if we're talking about the application layer, eh, an application itself,  I really like to, to think about the entities in terms of the operations, you can perform with them eh over them. So I guess it's not that different from object oriented programming, except that I just a face it through more of an API paradigm or there's a server listening to get and post requests essentially.

Each entity has a number of routes. to get information or to post information and in some cases to perform other types of operations. So my idea is first to write these, basic interactions. Uh, well, I was going to say on paper, but it's a on a text file right. And then,  the idea is that first you go with the, with the more obvious things, and then you try to see how certain routes which I call, the interesting routes  which are actions or events, or methods,  those routes usually lie at the intersection of two or sometimes even three entities.

And these are the places where it makes a lot of sense.  to spend time and design, to think about the implications, to see how they overlap with each other. And, uh, when you have a certain sense of clarity of what's going to happen there, and by no means is going to be final, then you can actually write some code and write some tests, but you are going to at least understand what are you trying to do?

And that's going to inform your first iterations. So. , a documentation first approach, but very lightweight it's like just describing what the end point would be doing, , and then just, implementing it, sitting back or perhaps taking a walk around your office or house, or perhaps around the block and thinking if those pieces actually make sense and fit with each other.

And the other thing is that, eh, the 80 20 principle, there's going to be a very few end points that are going to represent most of the value of your application and also perhaps overlapping, perhaps not. There's a few end points that are going to be the hardest ones to write, eh? So you think about what's important and you think about what's hard and eh, you pay attention to those areas chiefly. The rest is going to be relatively straightforward.

**Jeremy** So you sort of start from, you could almost call it like this API first approach where you're figuring out what are all the actions that my uh application is going to have, and you're building out these routes, I guess it sounds like similar to when you have maybe like a, a rest type design.

And it seems like you're putting a lot of thought into what are the actions going to be in my application, and how are those actions going to interact with all the different entities, which I guess would be either objects or things that you store in your database. And that's really where everything starts and you try to have all that done before you start writing code.

**Federico** Eh Yes, to a certain extent. I would just write it and say, yeah, I think this should have this shape and whatnot, and perhaps I won't even document the entire shape. What I then do is I start writing the end point and at the top of the end points, I write the validations for the payloads that we're going to receive.

I tried to be pretty thorough with the validation because I find that it's immensely clarifying of your thoughts to really think about which inputs are valid and which inputs are not, and not just validation to a shallow extent, but try to deeply validate what an end point or what a function actually receives, because a, that's essentially defining the domain of the function from a mathematical perspective.

And, and then from the domain, you say, okay, these are all the possible families of inputs I have for this route, for this endpoint, for this function it's the same thing at least for me in this, uh, scenario. And then,  what am I going to do with this? Because if I receive an input that I deem valid, I need to create an output that will also be valid right?

Then, the function if received, if it receives a valid input, has the responsibility to produce a valid output. So yeah, I just document a little bit. Then I get into the API or write the validation, and then pretty quickly you want to write a few tests. First to make sure that you cannot give invalid inputs uh, to the end point. 

And then you write a few tests to cover the main use cases for the end points if you're storing a, a user check that the user name is at least four characters long, so you can write a test and try to see if you can send an empty username or a, like a, an empty string for the username, like it's really pedestrian and low level, but, uh, that also takes you to the next step and the next step. And, uh. I feel that that approach works well.

**Jeremy** In terms of something like that example, like this username check, is that something that you would typically put into its own, uh end point or its own route, or was that something that you would embed in something that's kind of doing more? Like, for example, if you have an account creation requests.  Have that validation in there or would it or would it be separate?

**Federico** No, the validations, I would do it and I would have a signup route. That's how I've been doing it. And, uh, the signup route performs the validation of the username and password and a few more fields. And, uh, although perhaps there's a bit of repetition of code, uh, here and there. Um, not much though I like having the validations for each route written within the route itself, at the top. I feel like if the routes are well-designed, then the overlap is going to be a small, uh, you might want to define a few helper functions. Like, for example, if you have a lot of places where a user can send you an email field, like a, an email string, then yes, you might have a function, which is a helper too.

So the final, what is valid email or not, and then you can use that in different,  endpoints. But, uh, usually yes I write the validation at the top of each route and the, that logic is like embedded within the route itself.

**Jeremy** It sounds like you do testing, kind of like outside in, you would make a request to do a signup, for example, using an HTTP call and seeing if the signup, you know, successfully completed.  And not necessarily having tests for the individual validations. Like, for example, that helper function that's going to check, you know, whether an email is valid or something like that.
Instead, you would have that be, I guess, implicitly checked by,  a more high level, endpoint, right?

**Federico** Yes. Yes, to put it in a certain way would be like. The proof is in the pudding, right? So like the pudding being the API you expose, so you expose the API, then you should test the API through  and whatever is embedded within the,  an API endpoint, whether it is the validations or the results they produce, you should judge them by the results.

Besides this, just generating the least amount of code, I think,  because if you add the unit test to the end to end tests, then it's more code. Eh, at least more tests.  I feel like it's the real deal in terms of that,  end-to-end tests,  test what you are exposing. I feel like to test things that you are not exposing it's a bit artificial because it can give you a false sense of confidence  if the tests are passing mostly because of that, because perhaps that test is passing as a unit test, but then there's something between the, the internal function and the outer parts of the route where there's a bug there that can be triggered by a real request.

I just validate what I expose. In the case of applications, I validate through hitting the end points. In the case of tools, I just validate by hitting  the main functions that I expose in a, in a tool, in a library and the internals are going to be tested implicitly.
Through a coverage of most, if not all of the cases I can think about. Does that make sense?

**Jeremy** Yeah, that, that makes sense.  When you have these end-to-end tests, these tests that are making an HTTP request, testing the full API. do you have any trouble  if there is a failure or there is a bug narrowing down where in your code that the actual, you know, failure is occurring.

**Federico** Oh, great question. And this is how I do it, and it mostly works for me. So there's, there's a principal, , called, um, auto-activation. It comes from, eh, the Toyota production system, which is something a bit weird to be talking about in terms of software, , but the, these people at Toyota and particularly this, um.
I believe engineer called Taichi Ono,  who was the architect of the system, one of the two pillars of the whole system for Toyota and the quality revolution within the company, which eventually became  I believe six Sigma and other things were derived from there.  I need to do some fact checking there probably.

It was immensely influential and like, one of the two pillars,  one of them was just in time and the other one was auto-activation and auto-activation the name is a bit paradoxical, but the idea is that you have an automatic machine processing, for example, a loom with some fabric. So the machine should be able to detect when there's an issue, eh, with the incoming fabric, or when with the outgoing fabric, and if there's an issue there, whether in the input or in the output,  the machines should automatically stop the operation. So the machine stops and that has two effects.
First of all, the machine  doesn't produce a faulty, output. Like if it detects a fault, the output, it stops right there. Second of all, the operator, those that are walking around the plant. , see that there's an abnormal event taking place. So that immediately brings the thing to their attention, and they just go to the machine and figure out what's going on. And by figuring out what's going on, they go deep into it. They don't just say, Oh, the loom was threadbare. So the machine just gave up because it was too fidgety. No they tried to ask why three or five times until they find the root cause of the problem and then eliminate it.  eh, when I read that, it just blew my mind. And I thought, this definitely has to be applied to software as well. So the way that I applied is twofold from the perspective of tests. whenever a test fails, the whole tests suite fails and it stops right there, it doesn't go any further.

So any tests can be a showstopper. That already tells you, okay, this particular test failed. Then when I go to the code, that's why I write the validations. so thoroughly at the top of each end points. And also if I'm writing a tool or a library, I write the validations at the top of each function that I expose.

So the validations are very detailed in that if something is not right, eh, then the function is going to stop and return you an error message that would tell you exactly what's wrong there in the input. So by doing that,  you catch the error as soon as possible from the perspective of the implementation and also from the perspective of the test.

So in that way, the errors cannot go very far. You tend to catch them if not at the root, perhaps one or two steps removed from the root, but not six steps removed from the root.  I find that that actually works both conceptually and in practice.

**Jeremy** Yeah. And so it sounds like   you believe most of the bugs or the errors or problems are coming in from bad input and bugs that occur kind of further down the line are less common.

**Federico** Considerably less common. and also because if you're assuming that something is a string, then if you check that it's a string, you're not going to get an eh, like no such method match because you passed an undefined, right, which is a typical type of error, like a type error, so like this roots out most,  type errors, but also range errors.

And when you define quite strictly the inputs that you can allow, you start to think about the corner cases immediately, even before you're writing the implementation of the route.

You're starting to think. Do I really need to pass the username? Just to give you a stupid example, I guess perhaps they don't need to pass their username here. Perhaps it's implied that I don't need it. So when it, it makes you think quite hard about what the end point or the function is going to do if you think about the domain of fit.

So I would say that it forces you to have quite clear thinking already before getting into the implementation of the endpoint itself. And that's perhaps were empirically most of the value is, and most of the prevention of the bugs happen.

**Jeremy** You have all this input validation, this very strong input validation at the API level. Does that mean that further into the application you don't perform,  much validation because you're very confident that by the time it gets to functions deeper in the application of that the data is correct?

**Federico** That is exactly right. Yes. I try to validate things only once. The exceptions tend to be, when you have a one tool that relies on the next tool, uh, because in those cases you might be doing double validations, but as much as possible, uh, I really try to validate things once.

And then never again. And I also tend to not use too many layers, eh, in the app itself. Like most of the application logic I have within the route itself, uh, and then perhaps there's the database layer below it, but the database layer should already be tested because it's the tool. So essentially once that code execution goes past the validation.

So at the top of the route then, yes, whatever happens below has to be a valid output based on the input you just gave me, so there's not going to be a nested, eh validation of sorts.

**Jeremy** That's an interesting point because I've heard talk about sometimes people say like, you need to do defensive programming, you know, you you need to make sure that your, your function is going to be safe regardless of the inputs. But,  if you're pretty confident because of that strong layer, that can save a lot of duplicate code or just more code in general.

**Federico** Mm hmm and I really love your questions, which are really taking me where I want to go, so to speak. So let me just do a small fork.  I really believe in specifying everything and outlining everything, but not doing it twice and not because of performance. Performance is extremely overrated.

Everything is so fast and nowadays both software and hardware, it's like it's so fast. We don't really have to care about it anymore except in very specific circumstances that you're usually lucky to have because it means you have a very interesting product with a lot of users at the same time.

But, uh, it's not about performance. It's about adding these extra checks add noise in, in the eye of the person that is working on the system. This reminds me of  a blogger, the name of the blog i think is, book of hook, and he has an article, uh, named suffer no jankiness. And the idea is that, eh, he was commenting on the best coders he worked with, including John Carmack from ID and basically like Carmack would tolerate nothing that was unknown to him. 

So there was a super small bug and he would like say, no, no, I need to understand exactly what's going on here. I'm not going to tolerate this. So he would spend there one or two days, which for intensive for John Carmack would be like someone else's a month perhaps in terms of productivity, but he would like find the root cause of what was going on there.

And going back to what you asked me, I feel like with defensive programming is if you're doing a check twice and you are owning the code, or perhaps a small team is honing the code, that second check you're doing, either you need it and that's the proper place to do it. And if that's not the proper place to do it, do it at the top or wherever it has to be done, or you know that it has been done.

So don't do it again. So if you add these defensive layers, you're actually just obfuscating what is coming you're obfuscating the data flows, and you're adding extra code that is going to obfuscate your understanding of, of the code itself. So I feel like that's what, that's the damaging part of it.

And this brings me to tangent that I was talking about and goes back to what I discussed at the beginning. I told you that with simplicity. I saw  first of all, the conceptual integrity concept from Fred Brooks. And there's also, uh, another software engineer developer that has been super influential in me.

His name is Steve Yegge Y E G G E. And he used to work at Amazon at Google, and he had this set of software rants and like, I loved them. I highly recommend them. And, uh, one of  his rants that really got to me was,  code's, worst enemy. And uh, they basically code's worst enemy,  is the amount of lines.

And he speaks from the experience of him himself working on a game called Wyvern that apparently was very popular. And he spent like a decade of his life on this and he realized that the game was too big not just twice as big as he wanted it to be. It was like. 10 or a hundred times bigger that what he wanted to really build and maintain.

And there was a super painful realization to him and the catalyst for most of his writing. And I read that when I was just starting out as a programmer and I became, uh, a fanatic about the reduction of code size in terms of lines and just counting the lines of code, not to the point of doing golfing with the code.

But yes, to the point of really questioning the necessity of writing something or not, including, for example, double validations. So to me, like size is also a metric of simplicity. And the tricky part is not just the size of your tools, it's the size of the combination of your tools. And your application logic because you might have zero lines in your tools because you use vanilla JS or like no frameworks, but then you spend the tens of thousands of lines in your application code doing, developing your own tools kind of adhocly.

So that would not be an overall approach that reduces, um, complexity or lines of code. Eh, you could also go the other way around, which I see a lot, which is we're going to use all the frameworks now, all the tools. And so our code is going to be super short. So perhaps your code is super short, your application code, but you're relying on hundreds of thousands of,  of lines of code and perhaps even more realistically are relying on perhaps 120 functions, from 20 different libraries. So the overall amount of code that you have on the system is still very large. You're just hiding it behind the wall of the library or the tool. So I feel that's what I am trying to achieve in terms of simplicity practically is to reduce or minimize the lines of code from the total lines of code, both in my tools and in the application code itself.

**Jeremy** Do you weigh the lines of code in external dependencies differently? Like when you bring in, express or you bring in Django or rails that sort of thing,  there can be a lot of code in there. Do you treat it differently than your own code?

**Federico**  Yeah. I think you have to to a certain extent, but, uh, to what extent multiplied, eh, like, I don't know. What's the multiplier really?  if you really start going down this train of thought, you go crazy. Because, for example, I used nodeJS, right? So. Am I going to count the lines of code in nodeJS? Am I going to count the lines of code in V8, which is the Javascript engine on which node JS run. So or the operating system underlying. So you go crazy, eh? So the idea is not to take this too far, but I think it really makes sense to put attention into this, both in your own code and one level below it.

Let's say.  if you choose to use rails and you like rails, then go ahead with rails and don't go too crazy about,  the lines of code in rails. But, How many libraries do you use on top of rails? So, for example, just to talk about what I know with node, I really try not to use many libraries at all.

Uh, I just have my own set of tools that is relatively small and I understand well. And,  for some projects I use express for some other projects, I use,  seven or eight hundreds,   line, eh, server layer that I wrote myself. And there's not much else there. So I tried to minimize it, and perhaps not explicitly count, the lines of code in the dependencies. But yes, the amount of dependencies perhaps.

**Jeremy** It's interesting that, you know, you're using node, which is kind of known for this sort of explosion of dependencies, right. Known for somebody importing an NPM package and that package, having  thousands of lines of code in its own dependencies and so on and so forth.

Uh, And it seems like you're trying to avoid that I guess.

**Federico** To the utmost extent, but, uh, again, like I have exceptions, I, for example, use the AWS SDK for node, right. I use it usually for S3  and that, I think it's a five megabytes, 10 megabytes of code that I'm importing there, and I don't even want to know what I'm bringing in there.

But at the same time, I feel that I use three or four S3 functions and then, I don't use anything else there. And, uh, the rest of my code is unaffected by those dependencies. So I feel like the impact of that complexity on the rest of my code is much less than if I was importing a lot of code and I was using it all over my application.

**Jeremy** Yeah. And maybe also the. confidence you have in that library, right? You're kind of making the assumption that this is a AWS SDK provided by Amazon.  It's probably, you know, been very well tested, very reliable, and so hopefully you don't need to understand the internals.

**Federico** Yes. You would want to believe that. Uh, yes, and of course. It's a factor in what you, decide. But, uh, like I was always quite suspect  of the mainstream libraries, and I feel like,  time has kind of given me like the right to be paranoid. Not super paranoid, but like, yes, careful, like really never take authority at face value.
 especially coming from big corporations, never. Yeah.

**Jeremy** That's a good point. Specifically with AWS, I think I've heard of their SDK in certain languages is better than others. So you might get lucky or you might,  you might not.

**Federico** Mm hmm. Definitely. And in the end, there's always, eh, we'd call that the someone, somewhere somehow principle, which is like no matter what problems are abstracted to you, and you have the ability to use the solution, someone somewhere somehow had to implement that solution. And that solution might not be.  the best solution may not even be a good solution.

And in the end, you need to find out for yourself.  so like you cannot just take that at face value. I mean, at certain point you do have to, but over time, if you're developing a skill in a core area, you can question things a bit more and more. Not to topple them down, but just to to understand them more and to just feel whether they are solid and they stand on their own, or perhaps they do not.

**Jeremy** I want to go back to how you arrived at the current stack you used today. So that being, you know, Node, Nginx,  the local file system. What was sort of the trajectory of, I guess, your software development career where you know, you settled on those things.

**Federico** Yeah, I would say it's the result of both being lazy and lucky, let's say.  lazy, because most of those technologies, I pretty much almost started with and lucky because I would say that most of those technologies, uh, stood the test of time, so to speak.  I started about 10 years ago doing a HTML, CSS and a little bit of Javascript.

So when I started trying to build back ends a couple of years after that. I think it was early 2012  I knew JavaScript. I knew a little bit of Python, and I said, is there a way to do a backend in Javascript? And then nodeJS was already around. It wasn't mainstream. It wasn't huge, but it was definitely around. It was uh one or two Google searches away. So I, I just started using it and I absolutely loved it. And, uh, I basically stayed with it and then I've never really had the recent to move away from it. And then I had some exposure to rails, I had some exposure to PHP. but,  uh, like, node, just felt much better or much nicer to me, and I really didn't know why.

But,  eventually with time I saw certain things there that I really liked about it, and I could defend node, versus other options, but really I was quite lucky in that I just picked node first and then eh quite lazy in that I was never really actively thinking, is this the global optimum for me? Or perhaps there's something better that I have never tried.

So that definitely happened to me with node, and it also definitely happened to me with Redis because I never particularly liked uh Mongo DB. I really felt that the, the API was a quite complex to understand and I felt it was always changing and, uh, I also didn't like relational databases much, I felt like the, the relational paradigm was quite constraining.

Now that, um, I spent programming a few more years, I really understand why they exists and the fact that it's actually wonderful. But at the time I was really thinking, this is way too complex and I don't understand way anybody would need that, you know? Like it was, I was very, very ignorant and very arrogant, eh, and eh, but like I didn't like the relational one.

And I didn't like noSQL. I had heard some horror stories from other noSQL databases, and then it just ran into Redis, which is a, a no SQL database, if you want to call it that, is essentially a server that is very well written and it implements data, data structures in memory. So you have lists hashes, uh, sets, sorted sets, and a few others.

And I felt that it was conceptually beautiful and in practice it was so easy to get started and just started using it. And at the same time it could take you very, very far in what you could model with it. And also in terms of the sheer performance of it. And also over time, I was very lucky that redis became mainstream, essentially. So people still don't consider it. Uh, most people don't consider it as the main database for a project, but now it really became part of the mainstream toolset. And, uh, I guess I was lucky that, uh, I liked it early on, eh, and then it just basically kept on being valid, let's say.

And, then with regards to nginx, I'd started using it because it made HTPs much easier. And, uh, and yeah, that's, that's pretty much it then as for Ubuntu, uh, I guess it's an easy distribution to install in your computer. I started using Ubuntu back in 2005, and since I was using it on my own computer, it would be nice perhaps that my server also was running the same distribution, so I would have to learn less comments.

So I guess a very lazy approach.

**Jeremy** Well, it seems to have worked so far right.

**Federico** So far. So far

**Jeremy** Your usage of Redis is a little interesting because a lot of times people think of Redis as something to be used for, for caching and not necessarily a primary data store.  What has been your experience with, with Redis as a primary data store do you find that you're one of the few people using it or is there actually like a pretty large community of people who are also doing that?

**Federico** I think it's hard to tell, eh? I definitely feel it's not a majority position to use it as the main data store. And at the same time, the objections that I find that I hear about it  they don't withstand a conversation with two or three questions going back and forth.

Eh, so the most people's fears about Redis are, I wouldn't say completely unfounded, but they are not. , well researched, let's say, and  perhaps for a very good reason. People tend to be quite conservative in their choice of database. And perhaps because I have such an emphasis on simplicity and a lot of the systems I'd be able to just build for myself, I tend to value perhaps going with less conventional approach that is more clear over a more conventional approach that is perhaps conceptually less clear.

But, uh, there's definitely some people out there that are using Redis for. Nontrivial tasks that are not just caching, but also involve computation and in some cases even, eh, data storage as well. Then I kind of put some details on this  in a section in the backend lore, um, article.

So like, I don't think Redis would be a great database for all types of applications. Like definitely if you're handling financial transactions or healthcare. You probably want a relational database where each transaction is committed to disk,  before getting the, okay, like something that is really compliant with the acid, , guarantees of a database.

But for most of the applications I have worked with in my life for this seems to be a nice choice. I wouldn't say all of them, but most of them, and the reason, perhaps not many people do it, is because they never really consider the possibility of actually doing things in Redis. And the main thing that scares people, and I can understand the scare but doesn't mean that you have to give into it, is the fact that Redis runs in memory instead of running and on the disc.

**Jeremy** One of the things you, you kind of just mentioned is that. If you were working with financial data, you might consider a relational database due to the,  you know, the ACID guarantees.

Are there other projects or other scenarios you've, you've found where,  using a relational database makes more sense, whether that's related to joins or other features of the database.

**Federico** Yes. That's also a good point, eh I guess if you're handling a system with a millions of records and, uh, all those records are deeply interrelated, and this type of scenario is actually what made a. Codd, design relational databases, like, uh, like working with, uh, with large systems, for example, of inventories then yes, relational makes a lot of sense because if we're going to implement this in redis, you would have to create your own indexes.

Just to give you a, an example, like if you store a million users in Redis in hashes in Redis hashes,  you can not even say, give me the user that has this email. You have to store a separate collection of emails linking back to the user. So you basically have to do your links yourself in Redis. There's a few ways in which you can do that actually efficient ways you can, for example, you say sorted sets to do searches on, on ranges where word are alphabetical ranges or numeric ranges, but you need to do the indexes yourself,  whereas in a relational database, you get that quote unquote for free. I mean, you get it as part of the standard toolkit of searching and joining. Still in our relational database you can not just search anything. You need to actually know which columns you're going to index. You need to understand how you're going to structure the joins and the foreign keys. So I wouldn't say it's free in a relational database, but it definitely can be easier, especially  if you don't know beforehand what types of queries you're going to have to face.

So in redis you're a bit more hard coded. You need to add the indexes yourself.  whereas in the relational database, I feel like you have much more flexibility for on the fly, the finding new queries on your existing data.

**Jeremy** It sounds like if you have a pretty good idea of what data you're going to have and how you're going to be querying it. Then using Redis is, um, it's not too bad in the sense that you do have to create these indexes, but you can do that as long as you know ahead of time. Whereas if you have, like you said, interrelated data and you're not quite sure what information you're going to want to query by then using a relational database kind of gets you in a better position to be able to accommodate that with, you know, less work, I guess on your part.

**Federico** Definitely, and it's actually very funny to actually reach this conclusion because the reason I started with Redis in the first place is that I felt that it was more flexible, but it's very funny to see that actually, you do need to know more beforehand if you're designing with Redis than if you're designing with a relational database.

**Jeremy** So another part that I thought that was interesting about your, your backend post was how you use a local file system or you use,  a local file system on another server.

Could you kind of explain sort of how you use that and, why you do that?

**Federico** Yes, sure.  first of all, I use S3. Always, now I would say by default, unless there's a hard requirement or like people really like some people, the signing the app really don't care about their the files for more than a few hours. I would say other than that, I always use S3 by default, so I really don't have to concern myself with the data durability, eh, in terms of files,  that's part of my goal too.

With that said. I like serving and holding files locally for a number of reasons.  the first of them is speed.  if you have, uh, the files, whether on the same server as the API you're serving them, or in a bit of a bigger architecture, if you had them on a. Separate server, eh, that is still like relatively close to the other one.

The speed at which you can serve files, particularly with node JS, which is extremely performance for doing this type of operation of serving a static file. The performance goes up and, uh, by going up, it means. With a small server, you can deal with hundreds, even perhaps thousands of requests per second and not really have to worry about it that much.

Whereas if you have S3, then node, will do the best it can. But because the request might take 20 milliseconds, perhaps 30, there starts to be a lot of queuing there.  so performance is one reason. Cost is another one. S3 is cheap for storing data, but it's relatively expensive for retrieving it.

If you have potentially an, I wouldn't say an unlimited amount, but if you don't know how much data is going to be downloaded from your server. Then you have an unlimited financial downside of using S3 because it's 9 cents, the gigabyte. So you get super successful and you get a one terabyte that's 90 bucks.

I mean, it's not the end of the world, but, uh, you don't know how much it is. So if you serve them locally and you can actually do it, then. The cost is essentially zero, unless you're like a rate limited or like actually if they limit your bandwidth, eh, in the server, the cloud service that you use, which is usually not the case.

So I feel like a, you, you have a big saving there  and then the third one, which is only for cases where you store a lot of files, I don't like the way that S3 works with the large buckets the admin of S3 in particular is not very good. Uh, so I feel that sometimes it's nice to have your own FS layer with the own metadata on the files.
So that you can query your files faster, for example, by username, sorry,  file name, or by the last date modified. So I'd rather have that information locally and just query it efficiently rather than depend on the query mechanisms that S3 provides me.

**Jeremy** So are you using the local file system as kind of almost like a cache? And then after you store it in the local file system, you'll put it into S3, so that you don't lose it.  but the first place you'll go to is the local file system?

**Federico** It would go to the file system and to S3 and unless it's in this three successfully, I am not going to consider the transaction successful. So just to be super clear, for example, I'm building an application for managing pictures. So I'm uploading a picture from my browser to the server. So the server will reply with a 200 code unless it, the file is properly stored on S3.

So, but the reads are going to come from the file system directly.

**Jeremy** And would it be a case of like when somebody is getting their photo back, it would try to go to the local file system first, and then only if that failed, you would go out to S3?

**Federico** Yes.  I mean, there's three ways you can do it. You can put this stuff only on S3 you can put them on both S3 and the file system and always serve from the file system. Or you can just try to keep the last 10,000 or a hundred thousand files accessed on the file system, which will be the cache approach.

And I am lately inclining myself towards the approach where all the files are going to be in the local file system, which creates, of course, the challenge of handling potentially terabytes of files, which would have to be distributed across a number of servers, but I feel like I'd rather deal with that problem then with the problem of having the things only on S3.

**Jeremy** And when you're doing this local, File system approach. I believe in your posts, you mentioned how you have a separate server that stores these files and then you build some kind of web service layer on top of that. Could you kind of explain like why you took that approach.

**Federico** Sure. the thing is  if you're accessing the local file system, then you definitely don't need a. Any layer between the API running on that server and accessing that local file system. But, uh, if you need to separate,  the file system from the API because essentially you have a lot of files, then,  you need to create the communication channel between the, the APIs in node and the file system on that server. And I would or I wouldn't feel comfortable with any sort of direct file system access through the network. Eh, I remember reading briefly about network file systems and how they were quite brutal or hard to implement. Uh, so I never really went through that path and instead I just tried to basically create a separate proper layer that communicates through the network in the same way that the, the front end of an application talks to the, the server, to the, to an API.

I thought the API also has to be able to talk properly to a file system server. Like to have a services approach and, uh, avoid the backdoors at all costs. Steve Yegge also has, uh, an amazing rant about the platforms and essentially, he basically says that Amazon web services evolved from the idea that there should be no backdoors and all services should interact with each other as if they were external services.
And I think that's beautiful advice because if you have no backdoors, then. And there's a lot of security issues you can side step for sure. You also have to think about a lot of other things. You need to think about the authentication between the API node server and this file system server layer. Eh, so you need to solve that problem, but there's not going to be a backdoor.

Eh, the communication is going to be done securely. Over the wire. And, uh, that's, I feel like that's really a resilient, uh, and skillful way to see the problem. So in that case, just to sum up this, uh, answer, I feel like if you're not going to serve files from your local file system, then you need to treat the file system as a service.
And if it's a service. To me, it's an API and then you're talking through it through, through the wire, and then you're just going to use HTTP and you can even use the same authentication mechanisms as you would use between the client and the server.

**Jeremy** That goes into my next question of when do you decide to split something into a separate service? Like do you have some kind of process that you follow in that decision?

**Federico** I would, the principal would be let your problems, dictate your solutions. So for example, if you have an app and you don't think you're going to have more than. 30 or 50 gigabytes of data for the foreseeable future, eh, like you're like way below that, and you also don't think you're going to go past, I don't know, two thousand five thousand requests per second, which is a lot because a thousand requests per second I think is a hundred requests, 100 million requests per day.
So like a, it's amazing to have already had level of traffic. So unless you really feel you have a lot of traffic or a lot of data. You can go very, very far with just having a single API server, serving files from its own file system, and then having S3 as a backup in case something happens to that server.

So you can go a long way with that. However, if you start to have either more traffic or more likely more data, then yes, you need to figure out a way to solve the problem of not being able to fit everything on a single server. And so that takes you to the direction of splitting things into services. And definitely having a file service is something that I'm realizing I'm needing.

And I have some design work done to that effect, but I haven't implemented yet. So I will probably be working on this. Uh, this year.  I have worked with  a file service in the past many years ago.  It also worked quite well because again, we had a significant amount of data and we could not rely having all the data on just a single API servers.

**Jeremy** It sounds like the decision is very much focused on performance. what would you say to the fact that. You know, when you split things up into services, they run on separate machines. So you have to add this additional,  layer of HTTP traffic, right? you are starting to build a distributed system, you have a lot more network traffic, you have like some additional complexity, how does that factor into your decision?

**Federico** Well, it's a good question because when you start thinking in terms of services, talking through HTTP over the wire, then. When incoming HTTP requests from a client can become, I would say dozens that will be a nightmare, but perhaps five or six HTTP requests of all your services communicating for example, the architecture I'm thinking about now I'm going to need essentially six core services. Like eh one for authentication, one for files. Probably a database as a service as well, that's super tricky and I still don't, don't want to get too much into detail with that one. And then,  one for logs, one for server, like monitoring, like how's the health of the server, and one for statistics.

So there's potentially at least six services running in the background.  at least two or three of them are going to be activated by any incoming requests on an API. So  it's going to require more machines, but in the end, you need more machines.

That's why you're setting up services in the first place. Right. that's the big reason for which I am thinking of isolating this functionality into its own services, which is I cannot hold everything in one place, so I'm going to split. So in the end, if you need to split it into several servers, the several servers need to communicate with each other, and then as long as you implement things eh relatively straightforwardly, I don't think that performance really should be an issue.

The main issue there would be to have. Conceptual integrity, again, to understand how that request that comes from the client to the server generates its own sequence of requests. , you could say a dance or a conversation amongst servers on the backend. And, uh, I guess that's where the, where the art lies, right?
In creating something that is elegant and scalable. And understandable and still gets the job done and can scale. I wouldn't say to a big scale, but like for me, I would be feel very happy if I could say that it can handle let's say a hundred terabytes and I dunno, eh, 50,000 requests per second. I will be very happy with the system that it could do that.

So my, my two requirements would be, well, those on one end and the other end being able to understand what's going on there.

**Jeremy** And more kind of at the service to service level without needing to go look into the code or look at the documentation and understand that when this type of request comes in, it's going to get, you know, these four or five services you can know that without needing to actually dive into documentation or code.

**Federico** Yes. Ideally, yes.

**Jeremy** One of the things you mentioned in terms of services you are thinking of creating in the future related to logging and monitoring and things like that.  How do you currently handle logging and how do you currently handle monitoring?

**Federico** Yeah. Right now, for my own, uh. Apps, which are, have very small traffic,  I'm taking care of them in a very artisanal sort of way. Still artisanal scale. I have very bones implementations of the services. I have a centralized log server that is just a node server that is listening to requests.

And then like the, the two or three apps I have running are basically sending their logs to that centralized log through the wire. that's essentially how it's working now. And I have a very basic,  frontend to actually query those logs. So that's, that's a very verbose implementation of a centralized logging service.

And eh to saner person listening to this. I would recommend probably use a logging service that exists already. You don't have to roll your own, but eh, I do think that having a a central place to store your logs is a, a great time saver, eh, and also it makes things a bit safer in that if you're logging service, storing the stuff to S3, then your logs are not going to be lost on a server restart or if your server goes down. You'll still have access to the logs to the last minute. For many reasons I think it's a very good idea. And also because you don't have to be logging in manually through ssh to to different servers and seeing what's wrong there, especially in an emergency.

The second part of this is the notifications, which are also very crude at this stage,  and I'm sure that the logging solutions out there have better ways of doing it, but certain types of logs,  send emails, and I get those emails and I respond to them if I have to. so I have a very crude mechanism.
First of all, of centralizing the logs, and second of all of making certain logs, trigger notifications. Despite being very crude, I think that's going to be pretty much the essential flow of any system. Uh, you need a place to gather things, and then you need like some logic that tells you, Hey, if this happens,  sound the alarm.

**Jeremy** How do you balance between logging things that you believe are errors or exceptions and still wanting to keep information that's not necessarily an error, but you might need to look back later to help debug something.

**Federico** Oh, that's a great question. Eh, before like years ago, I thought, Oh, we can log everything, and I realized that's a bad idea for two reasons. First of all. It's creepy, eh, you're, you're getting all the full history of what your users are doing. Even if you're not looking at it, I don't think it's morally right to actually do that.
 I'm not passing judgment on anyone that is doing it because that's a blanket statement. I have to look at the details of what someone else will be doing. So I don't want to offend anyone in that regard because I might not know what they're doing. But at least to the extent that I'm writing my own applications. I really don't want to track everything that a user is doing. Definitely not. I do want to track a few things. However, the second reason I don't want to do that is because if you track every transaction, and if you have an unreal amount of users and traffic that can easily go into gigabytes, and then perhaps terabytes of logs which are mostly useless.
So I feel that it's good to track. Usually only the abnormal, which is essentially errors. And to track also the auth flows without, of course, storing their passwords in plain text, eh, which is very important not to do, eh, when you're logging, for example, the requests. 

So basically to recap, I store all the errors and I store all the user flows, taking out, of course, the passwords or the tokens, or the the secrets, let's say, because the auth flows are important to understanding the future, eh, security issues, or like the patterns of attacks that you might experience. And it's also something that is a functionality to the user to see where have I logged in from in the past. So that's valuable information for the user.

And on the other hand, errors are going back to what we discussed earlier about this, uh, the machines in Toyota that are auto activated. When there's an error, you need to take notice and see what's going on. eventually there's going to be certain types of errors, like there's all the time bots trying to hit a vulnerabilities on your app.
 I get emails from those daily and I almost learn to ignore them, but not completely. But I feel that's still valuable information because of the, IPs you see there or the patterns you see there. So I might not be in a position to make, do something about the data now, but I might be in a position to do something about that later, perhaps sharing with others.

So I feel that's worth registering. And one more thing that is worth registering, which is a subset of what I said, but when a client has an error, when the javascript, eh executing on a browser has an error. I send the error itself with as much contextual information as possible to the server, and then the server sends it to the centralized logging thing, and then the centralized logging thing sends me an email.
So there's a flow from the javascript braking on the, on the UI and me and my cofounder getting an email and I think that's super important and that has helped us detect uh bugs that we wouldn't have heard of otherwise.

**Jeremy** So basically it sounds like you focus on the JavaScript errors in the front end, any errors on the backend, whether that's an exception or or something like that.
And then the authentication flows because it's like pretty important. If somebody can't log in for some reason or somebody is trying to attack your, your application and then anything more than that, I guess you've changed from before you thought like, I need to keep everything because I might need it later to kind of, now you're saying probably I won't actually need it. It sounds like.

**Federico** Yes. And what I do sometimes, and that brings me also to this statistic service that I have a bare bones implementation of right now, is that. I do, for example, one to track certain metrics because it's fun to track them or because it also gives you a perspective of how much your users are using an app. So for example, there's ways to track how many unique users you have in a period of time without really having to, eh, have a list of which users were active.

You can, you can add a counter through, uh, I think it's a bloom filter I can't remember, eh, you can kind of see if the user was there or not without having to store the user name itself that's a performant and like non obtrusive way to detect how many users use your application.

And also you can have counters, for example, in the picture application I'm building. I can count how many new pictures are uploaded to the system, eh? Or how many pictures were rotated, let's say, or different operations. And then you have a counter bound for a period of time. So perhaps in the last hour, we had so many uploads in the last day, we had so many uploads.

So I think that's good to track, but you don't need to know that at this particular moment, this particular user upload this particular picture that I rather not, not have that eh, for, for these reasons I outline

**Jeremy** You posted on how you write back ends on hacker news and  you got a lot of response, a lot of feedback.  what are the things that, you know, people have told you or the feedback you've received that are things that you're excited to, to look into or try in the future?

**Federico**  Well, first of all, I was never expecting this level of interest. I was super. Happy, overwhelmed, confused.  It was a quite the ride for me but yeah, it was super positive.  I would say the most valuable feedback I got were further questions.
it was amazing how places where I wasn't very clear, eh, someone came and asked and they asked me about, uh, for example, how do I partition databases, how I perform migrations and databases, or like, do you use sticky sessions, uh, to see which requests should go to which server? Like specific questions, either through email or through the comments in hacker news or through issues.

They were great to clarify my thinking and I'll start a dialogue with, with many of these people to whom I am very, very, very grateful. So the questions I would say were the best, eh, the best feedback I could get. Then I learned eh definitely a few things. I didn't know that she could run Redis inside the Amazon web services that Amazon web service offer you their own Redis as a service. I didn't know that. I should probably be ashamed about that one, but I just didn't know. 

Also, someone said, why do you use node, you can just write all your application logic in nginx, and I just said, no, you cannot, and sorry, and that person and when I reply that I felt so sure about what I was saying. He just said, I was thinking, who is able to write an application on nginx configuration?

It's impossible, and then the person says, no, you can do it with this tool. And then lo and behold, they went and checked and it's actually possible. And it's actually not that crazy. I think it's called open resti. So the idea is that you have a set of Lua modules that extend nginx configuration, and you can do like quite a few things, and interact for example with SQL databases. And I would say, Oh, that's crazy. But I just looked a little bit more, and it looks pretty elegant. And actually Lua I had a very pleasant experience working with, because it's the language for performing programmatic Redis transactions. So in the end I was absolutely wrong and I learned something new there, so that was amazing.

Then,  yeah, I got a few suggestions about alternative things. I definitely got some validation from people that said. Definitely. I've been doing also this for awhile and I use a similar approach, and this has worked for me, which for me was a relief because I, especially getting all that exposure, like saying perhaps I'm just saying stupid things.

And a lot of people that know better are silent, eh. So to at least have some validation is, is nice. and then in terms of particularly going off the deep end, I had, um, a few doubts about how to implement them.  CSRF, which are a cross site request forgery tokens, whether they were needed or not.

And, uh, the last couple of days I have been involved in a great discussion, both in hacker news and in an issue in the, in the repository or in the document in GitHub,  about, uh, how to implement them, whether they're necessary or not. So the feedback there has been amazing, and I'm still like going through it, but yeah, I'm definitely learning a lot about very specific topics where I had like a, let's say, the fog of war or something just uh, unknowns there. And, um, it's really helping me clarify my thinking.

**Jeremy** Yeah. That's, that's fantastic. It's great that, you know, you shared your experience, but then also, you know, we can get the experience of the internet as a whole.

**Federico** It was absolutely beautiful and I wasn't expecting it. Again, there was something I felt like I just had to put down pretty much for my own future reference, and it was just beautiful to see how it evolved. Then people took it into their own hands.

**Jeremy** Yeah. Yeah. you know, we're, we're going to start wrapping up, but before we do, is there anything that you'd like to mention or think, you know, that I should have asked or,

**Federico** Yeah. A piece of advice perhaps I would just, uh, probably have to put on the backend lore is that, one very important piece of knowledge I learned there is to never normalize errors or alerts. So like when you're used to getting emails, eh, that something is failing and it's, uh, the boy that cried Wolf. Then at some point when the Wolf comes, you're going to be way less responsive it's super important to.
either not get the, the alerts if you shouldn't be getting them like solve, perhaps the those low level problems or turn off those particular alerts. Or at the very least have a hierarchy of errors and notifications because you really want to know when something is off. And that brings me back to the concept of auto activation there.  It's really important to never normalize the, Oh, yes, this, this stupid thing is failing again. And it's not my responsibility because, uh, perhaps it's something else. This time and this time it's your responsibility and you want to know that as soon as possible. 

**Jeremy** I understand that, that feeling well of like expecting certain errors to happen and having to have this sort of heuristic, you know, in your mind of like, okay, does this, does this error matter or not? And that's just kind of wastes a lot of mental energy.

**Federico** It does. It's dangerous, eh? I mean, most of the time it's a just trivial. But if you're dealing with systems and they're responsible for them, it's, it's downright dangerous.

**Jeremy** Yeah, no, that's, that's definitely good advice.
For people who want to check out your post or check out what you're working on,  at your company, uh, where should they head.

**Federico** So the name of my company is altocode, and, uh, we actually are building our software, eh. In public, which is we're putting it in GitHub and it's open sourced. And a while we are hoping to charge a fee for the service. We are still giving away the software for free and we are putting all our best practices into the code itself.

So the pictures application I was mentioning, the name of it is, uh, ac;pic and uh, it's open source and like in the, like all the practices that I mentioned in backend lore all the practices are there, implemented in actual functioning code, eh, on the repository.

So that's a, let's say, a live example of these practices and, and you can just check it out in GitHub. I can of course send you the the link later. So that's, that's a place to look for, for the code itself. And I'm super open to feedback and questions and, uh, yeah, people pointing also factual errors. It's all very welcome.

**Jeremy** Cool.  Federico, thank you so much for joining me on software sessions.

**Federico** It was a real pleasure. Thank you.

**Jeremy** Thanks again to Federico for coming on the show. You can get show notes for this episode at softwaresessions.com. If you haven't seen Federico's posts on writing back ends, we've got a link to it in the show notes.
Okay. I'll see you next time.

</div>