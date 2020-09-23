+++
title = "Building the Lucky Web Framework in Crystal with Paul Smith"

description = "Paul discusses how strict compile time guarantees inspired him to create Lucky using the Crystal programming language"

[extra]
episode_url = "https://media.transistor.fm/3338b381.mp3"
social_title = "Building the Lucky Web Framework in Crystal"
social_description = "The benefits of compile time guarantees and conversational error messages"
+++

Paul Smith is a Software Engineer at GitHub and the creator of the Lucky web framework. He previously worked at heroku and thoughtbot and has experience building applications using Rails and Phoenix. He's also the creator of the [Bamboo e-mail package](https://github.com/thoughtbot/bamboo) and the co-creator of the [ExMachina test data package](https://github.com/thoughtbot/ex_machina) for Elixir.

We discuss:
- The tradeoffs of object oriented and functional programming
- How a lack of compile time guarantees slow down ruby and elixir development
- Creating conversational error messages
- Ways fast languages can change how you write applications
- Writing templates with Crystal instead of HTML
- Choosing what to include in a web framework
- The Crystal community and ecosystem

### Related Links
- [@paulcsmith](https://twitter.com/paulcsmith)
- [The Crystal programming language](https://crystal-lang.org/)
- [The Lucky web framework](https://luckyframework.org/)
- [HTML2Lucky](https://luckyhtml.herokuapp.com/)
- [AlpineJS](https://github.com/alpinejs/alpine)

This episode originally aired on Software Engineering Radio.

---

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

Jeremy: Today I'm talking with Paul Smith.

Paul is the creator of the lucky web framework and he currently works at GitHub. Today, we're going to talk about the crystal programming language and the Lucky web framework. Paul, welcome to Software Engineering Radio. 

Paul: Thank you so much. Happy to be here.

Jeremy: There are a lot of languages for software developers to choose from. What excited you about crystal? 

Paul: Yeah, that's really interesting because when I first saw Crystal, I actually was not interested at all. It basically looked like Ruby to me. And so I just think, okay, so it's a faster Ruby. And typically if I want to learn a new language and want something that feels really different that pushes the boundaries on things.

I started getting more interested in compile time guarantees. I worked at Thoughtbot previous to Github and previous to Heroku and people were starting to get really into typed languages. Some people were starting to get into Haskell, which is the big one that is probably one of the more type safe but also hard to use languages.

But also Elm, which has a good focus on developer happiness and productivity and explaining what's going on. And as they were talking about, how they were writing fewer tests and it was easier to refactor, it started becoming clear to me that that's something I want. One of the things somebody said was, if the computer can check the code for you let the computer do that rather than you or rather than a test. So I started to get really interested in that. I was also interested in elixir which is another fantastic language. I did a lot of work with elixir. I built a library called bamboo, which is an email library. And another called ex machina, which is what a lot of people use for creating test data. I was really into it for awhile.

And at first I'm like, wow, I love functional. And then I realized a lot of the stuff I like about this I can do with objects. I just need to rethink things so that it uses objects rather than whatever random DSL.

Jeremy: You've got this big bucket of functions and you got to pass in all the parameters whereas, I feel like if you have those instance variables available in the object, then the actual functions can be a lot simpler in some ways.

Paul: Totally. That's a huge focus and making the object small so that it doesn't have too much. But that's how I began to feel with elixir is that I'm like, I just have 50 args and most of them I don't care about. I want to look at what's important to this method, to this method it's this argument, but with functions you're like, which things important. Is the first thing? Probably not. That's probably just the thing I'm passing everywhere. And so I liked that ability to focus in and know this object has these two instance variables everywhere.

Jeremy: It's interesting to get your perspective because it seemed like you were pretty deep into elixir if you had created, bamboo and ex machina and stuff like that.

Paul: Yeah. I was like way gung ho and then I started missing objects. And luckily with Crystal and Ruby, you still get a lot of the functional stuff. You can pass blocks around. That's functions. You can use functions. But it's not the other way in Elixir, you can't use objects. It just doesn't exist.

And then the type safety. I still run into so many errors and it was so frustrating. I don't want to do that.

The main benefit I got out of Elixir compared to Rails which is what I had been using and still use a lot of was speed. That was really big. In terms of bugs caught, about the same. Mostly because it's still for the most part a dynamically typed language with very few compile time guarantees. I'd still get the nil errors. I'd still mess up calls to different functions and things like that. And so that's where I ran into Crystal. It has the nice syntax I like from Elixir and Ruby. It's also very, very fast. Faster than Go in some benchmarks.

So it's quick. Plenty fast for what I need. 

And it has those compile time guarantees like checking for nils. That's a huge one. And it also makes the type system very friendly. So it does a lot of type inference. And very powerful macros so you can reduce some of the boilerplate.

And so that's when I started getting into Crystal was seeing Elixir I still got a lot of these bugs that I was running into with Rails, but I liked the speed but I don't want to use Haskell and Elm doesn't exist on the backend. So I started looking at crystal.

Jeremy: Sounds like there's this spectrum. You have Ruby and you have Elixir, where you don't necessarily specify your types so the compiler can't help you as much. And then you've got Haskell, which is very strict. You have a compiler that helps you a lot. Then there's languages in-between for example Java and C and things like that. They've been around for quite some time. How does crystal compare to languages like those ? 

Paul: Yeah, that's a great question cause I did look at some of those other ones. TypeScript for example is huge. Kotlin was another one that I had looked at because it's Java but better basically. That's the way it's pitched. And so far everyone that's used it has basically said that. And also looking at Rust, what it came down to was how powerful was the type system. 

So crystal has union types which can be extremely helpful and it catches nil. Java does not have a good way to do that. Kotlin does but also boilerplate and the macro system.. Crystal's is extremely powerful. Elixir also has a very powerful macro system.

But Crystal's is type safe, which is even more fantastic. So basically what that let me do with Lucky was build even more powerful type safe programs. And we can get into that once we talk about lucky and how that was designed. But basically with these other languages, a lot of what we do in Lucky just simply wouldn't be possible or wouldn't be possible without a significant amount of work and duplication.

Jeremy: You covered a few things there. One of the things was macros, what are macros? 

Paul: Yeah. This is like a confusing thing. It took me a while to get what it is. But in Ruby they have ways of metaprogramming. That are not done at compile time for most compiled languages. You need macros to de-duplicate things and basically what a macro does is it generates code for you.

The way I think about it is basically you've got a method or a macro but it looks like a method. It has code inside of it. And it's like you're copy pasting whatever's inside of that macro into wherever you called it from. So in other words, Rails has has_many, has_many :users, has_many :tasks that's generating a ton of code for you.

So that's how Ruby does it. Crystal has_many would be a macro and it would literally generate a ton of code. And copy paste that into wherever you called it. It's just a way to reduce boilerplate.

Jeremy:  In the case of dynamic languages, like Ruby, when you talk about Metaprogramming, that's having a function that is generating code at runtime. And the macro is doing something similar except it's generating that code at compile time. Is that the distinction? 

Paul: That's the way I look at it. there are people much smarter than me that probably have a more specific answer about what the differences are but in my mind and in practical usage that's what it comes down to.

Jeremy: Let's say there's a problem in that code, what do you get shown in the debugger? 

Paul: Debugging macros is definitely harder than debugging your regular code for that exact reason. It is generating code. So what crystal does, uh, there's different ways of doing this, but I like Crystal's approach. It'll show you the final result of the code and it'll point to the line in the generated code that caused the issue and tell you which macro generated it.

Now, it's still not ideal because that code isn't code you wrote, it's code that the macro generated but it does allow you to see what the macro generated and why it might be an issue.

Part of that can be solved by writing error messages and error handling as part of the macro. So, in other words, making sure, if you're expecting a string literal, you can have a check at the top that checks for it to be a string literal. I wouldn't use them by default, but it's great for, I think a framework where you have a lot of boilerplatey things that you're literally typing in every single model or every single controller, and that people get used to. It's well tested. It has nice error messages. In my own personal code though, I pretty much never used macros. They're only in the libraries that I write.

Jeremy: Another thing you mentioned is how crystal helps you detect Nils or nulls. How does the language do that?

Paul: It actually uses union types for that. Some languages that have this, they'll have an optional type, which is basically a wrapper around whatever real type, like an optional string, optional int, and you have to unwrap it. The way Crystal does it is you would say string or nil, and there's a little bit of syntactic sugar.

So you can just say string with a question mark at the end. But that gets expanded to string or a nil type. Um, so then within that method, the compiler knows that this could be a string, could be a nil, and there's a little bit of sugar there where the compiler, if you say, if whatever variable you have, it's going to know that within that if it is not nil and in the else it is.

So there's a little bit of sugar there as well. But that's basically how they handle it. And there are ways to force the compiler [to] just say, Hey, this thing is not nil you can call not nil on it. I would avoid that because maybe the compiler's right and it really is nil. Or maybe you change the method later and then it can become nil and you're going to get a runtime error there.

But it does have those escape hatches. Cause sometimes you just need the quick and dirty and you can if you need to.

Jeremy: As long as you don't tell the compiler that then you will actually have a compiler error. If you have a method that takes in some type of object or a nil. And then you don't account for the fact that it could be nil. Then the compiler won't let you compile, is that correct?

Paul: That is correct. So for example, if you just had a method that's print_email and it accepts a user or nil, now, I'm not saying I would do that, but let's say that it does. And you just tried within that method to do user.email to print the user's email. Um, it's going to fail and tell you that nil does not have the method, email.

And so you need to handle that. And then you're forced to either do an if or you can use try, which is basically a method that says call a method on this object. Unless it's nil, if it's nil, just return nil. But yes it forces you to do that.

Jeremy: And in crystal, how do you handle errors? Because a lot of different languages have exceptions or result types.  What's the the main way in crystal?

Paul: I'd group it into two types of errors where you have runtime exceptions still because things do break. Not everything is in a perfect world. Inside your type system, databases go down, redis falls over or whatever. So you still have runtime exceptions and then you have the compile time errors, which we just talked about.

But in terms of how those runtime exceptions are handled I don't want to say exactly the same as Ruby cause there probably are some subtle differences, but extremely similar to Ruby and that you're not passing around errors. It's not like Go where you are explicitly handling errors at every step.

You raise it and you can rescue that error like a try catch in other languages and you can also just let it bubble up and rescue at a higher level which I personally prefer. Because not every error is something that I care about and forcing me to handle every single error everywhere means that it is harder as a reader of the code to tell which errors I should care about because they're all treated as equal.

So I like that in crystal I can say this particular error, this particular method, I want to handle in a special way. And somewhere up above the stack. I can just say anything else. Just print a 500, log it, send it to Sentry (an error monitoring SaaS).

Jeremy: Yeah, so it's very similar to Ruby or any other language that primarily relies on exceptions. Java probably falls into the same category.

Paul: Probably. I haven't used it in quite some time, but I imagine it would be similar.

Jeremy: You had mentioned that crystal is pretty fast compared to other languages. What are the big benefits you've gotten from that raw speed?  

Paul: The biggest benefit I would say is not having to worry so much about rendering times. In rails for example you can spend a ton of time in the view, even though everyone says databases are slow, they're not that slow. In something like Rails ActiveRecord (Rails ORM) takes a huge amount of time to instantiate every single record.

So how does this play out in real life? You could in lucky if you wanted to load a thousand records and print them on the page and probably do that in a couple hundred milliseconds maybe which is a totally reasonable response time. Same thing in rails would be many seconds, which is not reasonable in my opinion.

And this can be really helpful partly because it just means your apps are faster, people are getting the response quickly. But also because you have a lot more flexibility. I've built internal tools where they want to have the ability to search all of the inventory or products or whatever else and they want to have like a select all or be able to select everything.

And in rails you can't just render all 1000 products cause it basically falls over. And you can try and cache stuff but then that gets complicated. So you have to paginate. But when you paginate that makes it hard to select things across multiple pages, then you need some kind of JavaScript to remember which ones you selected across pages, and it just balloons the complexity, right?

If you know: Hey, we only have 800-900 products, we're not going to suddenly have 20,000 in Lucky. You just render them all, put them all on the same page, give them all check boxes, and it's in the user's hands in 200 milliseconds and you're done. You just removed most of that complexity. 

So those are some of the ways that speed is playing out. And I think one key difference there is some people think speed is just about scalability. How many people can be using this? The speed improvements I care about are the ones where even if you have one request per day, I want that request to be insanely fast. And so that's what you're getting with Lucky and Crystal.

Jeremy: When you talk about web applications with Lucky being a web framework. A lot of people point out that a lot of the work being done is IO. It's talking to the database, it's making network calls. But I guess you're saying that rendering that template, those are things that having a fast language it really does make a big difference.

Paul: It does. Yeah. I think the whole database IO thing, a lot of times that's what people say when they're working with a slow language. If you have a fast one. It's not as big of a deal. Cause this was the same with Phoenix and Elixir. I loved how quickly it could render HTML. That was huge.

Jeremy: And like you said, that opens up options in terms of not having to rely on caching or pagination or things like that.

Paul: Yeah. This is huge. An example from work. We just announced GitHub Discussions. I'm on that team. And one of the big things we were trying to get working was performance of the discussions show page. You could have hundreds of comments on that page. And we were finding that most of the time taken was actually spent rendering the views and calling methods on the different objects to render things differently in the seconds. And we can't cache those reliably because there are so many different ways to show that data. If you're a moderator, you get certain buttons. If you're an unverified user like someone who just signed up, you see a different thing. If you're not signed in you see a different thing, and so you can't reliably cache those, and we had a lot of cool techniques to get that down, but this is something that if this were written in lucky, it just would not have been an issue.

Jeremy: And GitHub in particular is written in Ruby, is that correct?

Paul: It is. Yeah. It's using Ruby on Rails, and I'm not trying to knock Rails. I really love Rails. I've been using it for 12 years. I like Ruby. But hey, if there's something that could be even better, I'm open to that.

Jeremy: You have used Rails for 12 years. How would you say that your productivity compares in Ruby versus in crystal?

Paul: I think that's tricky. It's better and worse. And what I mean by that is... I think crystal I'm more productive. And crystal, you do have compile times and we can talk about that. They're not the fastest, they're not the slowest, but I do find that I can write more code and then compile once, and it just tells me where the problems are and I have a lot more confidence and I spend a lot less time banging my head on like, why isn't this thing working?

And it's because I passed the wrong type somewhere. However, Ruby has a massive ecosystem, so there are things that exist in Ruby that I would have to rewrite in Crystal. And so that for sure, no matter how productive I am in Crystal, is not as productive as requiring the gem and then just using it.

So the hope with Lucky though is that we're building up enough things that you don't have to be rewriting everything. And the community is also really stepped up and writing a number of libraries that are super helpful for web development. For example somebody just wrote webdrivers.cr, which makes it so that it can automatically install the version of Chrome driver that matches the version of Chrome that you have installed.

So you don't have to manage that at all. That's something that was in Ruby for awhile, and will be in Lucky, probably in the next release. So yeah, I think it's better. It's one of those things that will get better with time.

Jeremy: So in terms of the language productivity crystal sounds like a net positive but it's more in the the community aspect and how many libraries are available that's where a lot more time is taken.

Paul: I think so. And then just the initial ramping up it is a new language and so there aren't as many stack overflow questions and answers and there aren't as many tutorials. So there's definitely some things there. But like I said, those are things we're working on especially for Lucky try and make sure we have really good guides, really good error messages.

We tried to borrow a little bit from Elm. Not specific error messages, but just the idea that an error message should raise something human readable and understandable and if possible help guide them in the right direction of what they probably want to do. Or at least point them to documentation to make it easier. So we're trying to help with that as much as we can.

Jeremy: I want to move next into your experience building Lucky. You were a Rails developer for many years. Are there any specific major pain points in Rails or in your previous web development experience that you wanted to address with Lucky?

Paul: Yeah. There were some more specific than others. Some easier to solve. In the sense that the solution works or it doesn't. And others that are a little bit more abstract. So I'll talk about some of the specific things. I often said that I'm into type safety. I don't think that is quite true. Especially if you haven't used Lucky, it just doesn't click what that means or why it matters. Cause you just think like, Oh, so  don't tell me if I pass an integer instead of a string. Like who cares? I'm not seeing those kinds of errors.

What I'm most interested in is compile time guarantees, whether that's with a type or some other mechanism. and that's there not just to prevent bugs, but to help you as a developer to spot problems right away. And give you a nice error so you know what to do about it. So, for example, one of the things that I've seen in basically every framework I've ever used, regardless of whether it is type safe or not, is that you need to use an HTTP method, a verb and a path.

So, for example, if you want to delete a user, you would have /users/1 to be the ID. The tricky part is you have to have the HTTP method delete for it to do the delete action. But sometimes you forget that you use a regular link and you wonder why the heck it just keeps showing you this thing instead of deleting it or the particularly insidious one is when you have an update and a create. One uses post one uses put, if you have an update form and you forget to put the method put, you get all kinds of routing errors cause it says, Hey, this doesn't exist. And you went, well why? Why doesn't this exist? I can see it right here. I've got the route, I've got everything.

Oh it's cause I forgot to put the HTTP method is a PUT. And it just wastes time. So that's one of those things where we wanted compile time guarantees in Lucky. And so I don't want to go too in depth here, but basically what we did was we made every controller into a single class that handled the routing and also the response.

Jeremy: If I understand correctly when you have a page and you want to link to a specific user on that page. Then you would use this function link and you would pass in the class that corresponds to showing a user, and then you would pass parameters into that function. Like, for example, the id of the user.

And if you didn't do that. Then you would have an error at compile time.

Paul: Correct.

Jeremy: You wouldn't need to start the website and then go to the page and have it explode, which I guess is typically what you would expect from most web frameworks.

Paul: Or what's worse, it wouldn't explode. It would just generate the wrong link and you would have to remember to click that link or write an automated test that clicks that link. And so it's really easy for bugs to sneak in, and this just completely prevents that class of bug. As well as just makes life easier because if you forget a parameter while you're developing from the start, instead of just generating something with like a nil ID, it's going to say, Hey, you forgot this.

It just saves a lot of debugging time, and I think it's also more intuitive if you've ever used Rails Helpers or Phoenix, help any of these... man the conventions. Like is it singular, is it plural? Does it have the namespaces or not have the namespace? In lucky that it's gone. You just call the action, the one that you created, you call that exactly as is.

Jeremy: It sounds like this is maybe a little more explicit? 

Paul: Yeah, it's a little more explicit, but I hesitate. I've heard a couple of things in the programming community. One Rails started as convention over configuration, which that was huge because you had to learn the convention, but at least once you did, you knew how about other rails projects were. And then another one I hear is explicit over implicit.

I don't buy into either of those in particular. Because sometimes implicit is better, sometimes explicit is better. I don't hear anyone arguing to bring back the old objective C where you had to manually reference and dereference memory. That is technically more explicit. But does anyone want to do that? No. So I don't think explicit over implicit, you have to think about it. Everything needs to be judged in its own context. And what I think is even better than convention over configuration is intuitive over conventions. Meaning you don't even think about it.

There doesn't need to be a convention. Because you're literally just calling the thing that you created like anything else, there's nothing special about that. It's a class just like any other class and you call a method on it, just like any other method.

I think it's tricky because I think it's also easy to say explicit over implicit and make your code super hard to follow. And it's like, yes, it's more explicit, but also I just wrote 20 lines of code instead of 1. And those 20 lines could differ because I do it differently than the other guy or girl.

Jeremy: Another thing about Lucky that's a little different is that for templating instead of having somebody write HTML and embedding language code in it you instead have people write Crystal code.

So could you explain why you made that decision and what the benefits are?

Paul: Yeah, sure. So a lot of things actually with Lucky I did not want to do, or were definitely not how I started doing things. And it just moved in that direction based on the goals. And I think that's part of what makes Lucky, different is that we don't say, here's how I want to do it.

We say, here's what I want to do and I want it to be easy, simple, and bug free. So. What we started with was using templating languages, just like you'd use in almost anything where you write your HTML and then you interpolate values in it. At the time I wrote Lucky, and this may be changed now you could not use a method that accepted a function or a block is what it would be called in Crystal and have that output correctly in the template. I think it just blew up. I don't remember this was two years ago, three years ago. 

The other problem I was having was it's not just a template. Any bigger size framework also has partials or fragments or includes or whatever you want to call it. It also has layouts where you can inject different HTML in different parts of your HTML layout, and those are all things that a person has to learn when they're learning your framework. What are these methods called for.

Generating a partial or calling a partial or injecting stuff in different layers of the layout. And it's also more stuff that I have to write. And with Lucky, like there was already a lot to write. They were building the ORM and the automated test drivers and the router and like everything. So I can't afford to just do stuff like everyone else does it if it's not pulling its weight.

So eventually. I started experimenting with building HTML using classes and regular Crystal methods. Some of the requirements for me when I was building it was it had to match the structure of HTML and it had to be very easy to refactor. Meaning I can pull something out into a new method and it just works.

So easy refactoring. And then I also need to be able to do layouts with it. The reason for that is Elm also uses code to generate HTML. However, it is not approachable to a newcomer. If you have a designer and they pull it up and try and look at what that generates... No way. I mean. I'm a programmer, I still don't know what it generates without really looking through Elm. And that's partly because you are generating data objects. So arrays of arrays. Or maps or whatever else. so I didn't want that. It has to be approachable to people and look and be structured like HTML.

And so we were actually able to do that. I don't know if I need to go into huge detail but basically you can say, Hey, I want a div. Inside of that, I want an H1. Underneath that I want another div. And you're not building arrays and maps and anything else. What that provides is actually a lot of things that I did not think of.

One, super easy refactoring. If you have a link in a particular page and you don't want to copy that over and over and over, extract a method and you call it like any other method, there's nothing to learn. It's just a method. Like anything else, it can accept arguments just like anything else. Your conditionals work.

You can extract that into a component, which is basically another class and it tells you explicitly here's what I need to run. And it renders the thing. You always have the correct closing tag. I have been bitten so many times by shifting stuff around. And forgetting a closing tag and my whole page looks wonky and I have to go through layers of indentation.

That just doesn't happen if you forget an end so you would have a do end when you're creating these blocks, it blows up. It's like, Hey, you're missing one. And the coolest part is you just add an end in there and you've run the crystal formatter and it re-indents everything perfectly. And then on top of that if that wasn't enough I just loved how easy it was to refactor and use. You don't have to split up your code from your template. Like in rails, you would have a helper. So you've got like, here's your template, but then you might have a helper, a totally separate file. If you've got something that pertains to just that page, you can just extract a method.

It's right there. But this also made it so we can do layout without any special work. Your layout is basically a class. You would say, here's my class with the head. It renders the head renders HTML body or whatever. And then it calls a content method or a sidebar method or whatever else, and your page.

So if you wanted to render a list of users, inherit from that class and implement a content method or a sidebar method. And so when that's rendered out, it just calls those methods. So we got all of that for free. If you look at our view rendering code, it's 50 lines. Because basically we use a macro and give it a list of tags like paragraph, H1, H2, whatever and generate a bunch of methods.

And that's basically it. So from an implementation perspective, it's extremely simple. Plus, you get all these niceties around... refactoring is super easy. It's super easy to tell what a page needs to render at the top of the page. You just say I need a user. I need a paginator. I need a current user.

So you know what that page needs. You don't get that with a template. and you get all the power of crystal for rendering layouts however you want. That all basically came for free. So it was kind of a happenstance that templates weren't working and this has worked out better. 

A lot of people when they see this they're like, what the heck is this? I hate it. And I always just say, just give it a try. Just give it a try for a little bit. So far. One person has said like, okay, I don't like it, and you can use templates if you want. We've actually built that in, but everybody else is like, now that I've used it, I love it.

Jeremy: What it sounds like is in a lot of, JavaScript frameworks, for example, like React, there's this concept of components. And so you can create what looks like new HTML tags, but really has some other HTML in it. Let's say you have a a list of businesses and maybe you have a component that would have all the business details in it. It sounds like in the case of Lucky, you can do the same thing. It's just that your component would be in the form of a Crystal class. And so there isn't any new syntax. And you're not mixing, different languages. You're not mixing HTML and JavaScript. Instead, everything is just using Crystal.

Paul: Exactly. You have two options. You can extract a private method cause sometimes it's just a small thing you want to extract only used by one page. Just do a method. If not. Extract a class. And the cool part about all of this is that you don't need to restructure anything. Meaning you can start with everything in one method, in your content method, and then you can pull out just a little bit into a private method.

And then if that's not enough cool, pull that out into a class so you're not forced into just pulling out classes all over the place if you don't need one.

It really worked out really well because it also makes testing easier. You can pull out a class component that just does one thing and you can instantiate just that component and test just that HTML. And once again, this is very easy because it's a class. You call it and run it like any other class.

And so that's been a big goal of Lucky is try to reduce and this also comes down to the whole convention over configuration is how do we just make it so there is no convention. It's just intuitive. Like if you know how to extract and refactor a crystal class, you know how to extract and refactor stuff for a page in Lucky automatically. Of course there's still some degree of learning and experimentation, but it's the same paradigms. if you want to include methods in multiple pages, use a module just like any other module. So that was very much a goal. 

And that's part of other parts of lucky, for example, querying in something like Rails. The model is for creating, updating, reading, everything. In Lucky you do create a model and we use macros to actually generate other classes for you, but you have a query object that is a class. 

Jeremy: What am I passing into my query object? What does that look like? 

Paul: Let's say you have a user by default, it generates a User::Base query. So basically you have this new object namespace under the model. And by default, the generators generate another file.

And basically what that does is it creates a new class called UserQuery. That inherits from that UserBase query class. What you would do in your controller action or anywhere, say UserQuery.new by default. That just gives you a new query that would query everything in the database. Unless of course you overrode initialize and did something else. Then it would use that scope. So if you want to further filter down you would call for example, if you wanted the name to be Paul, it would be UserQuery.new.name("Paul"). Because Lucky generates methods for every column on the model with compile time guarantees if you typo that method it's going to blow up. If you've renamed the column later it's going to blow up. If you accidentally give it nil, it's going to blow up and tell you to use something else, but that's how you would do it.

You say dot name is Paul. Or we also have type specific criteria and methods. You can do things like .age.gt(30). And so you have this very flexible query language that's all completely type safe. So in your scopes, if you wanted to do something like recently published for a post, inside that method, you would do something like published_at.gt(1.week.ago).

And you can chain that. So you could do PostQuery.new.recently_published.authored_by("Paul") or whatever. So that's basically how it works. You just have these methods that are chained, that you can build upon in pretty much any way you want.

Jeremy: In a lot of applications people use JavaScript frameworks, whether its React or Vue or angular, what does integrating with JavaScript libraries and frameworks look like in Lucky?

Paul: I think easier than a lot in the sense that you can generate a Lucky project with different modes. So when you initialize a project you can use just the command line with some flags, or the default is to walk you through a wizard which will say, do you want API only? In which case it won't even have HTML pages or the default, which is a full app.

What that does is it generates a Webpack config for you. It sets up your public assets and images so that they can be copied and fingerprinted. And so out of the box that already has a basic webpack set up for you that handles CSS. It handles most of your ES6 JavaScript type stuff that people typically like.

That's just handled out of the box. If you want to include React or Vue you would include that just like any other Webpack project in terms of building it. And it's actually a little simpler. We use Laravel mix on top of Webpack, which is basically a thin JavaScript layer that calls Webpack underneath the hood.

If you want a full single page app. That's also totally supported. You would basically have just one HTML page that has the basic HTML and body tags and within that mount to your app. So whatever that is for your language in Vue, it might be, just a tag that's like main app.

And then in your JS you would initialize that tag with your app. And we have fallback routing so that you can do client side routing if you want. It's not particularly well-documented, which is the biggest problem. Some people are helping with that cause a number of people have done React and Vue.

Hopefully those will be fleshed out a little bit more, but it's totally supported. In the longterm though, we've got plans to make it so you don't even need those types of frameworks quite as much. Since we already have class components and a bunch of other things I'm working on a way to add type safe interactivity to HTML.

So you're not writing the Javascript, you're writing Crystal for the most part, and it can interface with Javascript and you can use React and Vue inside of it. But a lot of your simple (unintelligible) if anything like that is going to be handled client side, but written with Crystal and server interactions will also be sent over an Ajax request but will also be type safe when you call the actions and do all the HTML rendering similar to Livewire for Laravel or Live View by Phoenix. But with some differences that's not done yet, but it will be, and I think it's going to be really exciting. I've got a proof of concept up locally and it's really awesome.

Jeremy: We had a previous episode on Live View and I think the possibilities of things like that are really interesting of being able to not have to have this separation between your JavaScript front end and your server backend yet still be able to have the interactivity people expect.

Paul: Yeah, I think it could be cool. And that's also where speed comes into play. When you're doing interactions like that, you don't want to wait even a hundred, even 50 milliseconds is noticeable for those types of interactions. And so Phoenix... also [a] really fast, template language. Basically it gets compiled down to Elixir, and so that helps a lot.

I do think there's some big flaws that I've seen in some other implementations. Well, I don't want to say flaws, that sounds a little overly harsh, but things that are just deal breakers for me. And one of those is some clientside interactions have to be instantaneous. If I click on my avatar on the top right, I expect the menu that has settings and log out to be instant.

If there's any kind of latency in the network and it takes 200 milliseconds, even. That's going to be a weird interaction and it's going to feel like your app is broken. And of course that's exacerbated by people not in your country. This is another problem. People are doing these things, deploying servers in their own country.

Put a VPN in front of your computer in Australia or even the UK, 400 milliseconds. You can't do that for a settings menu or for opening a modal. And so there needs to be some way to do those interactions instantaneously. Livewire by Laravel, the same guy that wrote it, built Alpine JS.

WIt looks a little bit like Vue, but it doesn't have a virtual DOM it operates with the DOM that you generate. That's what it uses for client side interactivity. So you can do the server side stuff, which I mean, if latency's there if you're submitting a comment there's no way around it.

You've got to hit the server. But if you're opening and showing something in a menu, a tab, a modal. That's instantaneous and is handled by Alpine. So Lucky is actually going to use that along with our own server rendered stuff to do client side interactions instantaneously.

Jeremy: Alpine, it's a JavaScript front end framework similar to Vue without the virtual DOM, and it sounds like what you're planning is to be able to write Crystal code and have that generate Alpine code. Is that right? 

Paul: That's correct. Cause it's mostly in line and it can't do everything. But most of what I want from client side interactions are typically super simple things. I want to open and close something. I want to show tabs. And those are things that Alpine's incredibly good at because you don't need a separate JavaScript file.

We can just generate something that says, it uses X as it's kind of modifier X dash click toggle the thing. True or false, toggle open to true or false and X if or X show and then if it's open or not. Those are things that we can very easily generate on the backend and make type safe because we can say,  this has to be a boolean and here's the action.

And all those things are then type safe, but you can still do JavaScript if you want, so you can still use JavaScript functions in there with your Alpine if you need to.

Jeremy: Yeah. That just sounds like the distinction between that and like a live view or a live wire is that my understanding is with those solutions you're shipping over basically diffs in your HTML, and that's how it's determining what to change. Whereas you're saying like, you may still have some of that but there's certain interactions where you just want to run JavaScript locally on the person's client, and you should still be able to do that even if you are doing this sort of sending diffs over the wire, for other things.

Paul: Yeah. Exactly. Alpine's made for that. The biggest key differentiator between Livewire live view is the type safety, all those nice things that you get in lucky you're going to get also for your client side interactions. So if you have an action and you have a typo or something, it's going to blow up.

It's going to tell you if you forget something, if you've missed the wrong type. I mean, and this is something that's very hard in the front end world because you either have to run an automated test to make sure you catch these or the worst. You have to open up the console. Because like, why isn't this working?

I don't know. Now I have to dig into the console. It's not even where you typically want to see logs, and so being able to shift that to where you're used to seeing errors and before you even have to open the browser, I think that's going to be a huge deal.

Jeremy: I think on the server side, testing is pretty well understood in terms of,  especially if you have API end points, or you have  just regular server code, like people know how to test that. But on the client side, there's like so many different ways of doing it.

It feels like, and a lot of them involve spinning up browsers and, um, it can get kind of complicated and so, yeah, it'll be interesting to see if you can shift more of that to the, the server environment that a lot of people are used to.

Paul: Yeah, I think it will be cool. We'll see how it goes and yeah, I do think there's definitely complexity that comes with moving it to Javascript, especially if you have a single page app cause then you need to spin up an API. You need the the server and an API. When you use your Cypress tests or whatever, or a lot of people mock the API, which sometimes is fast, but can get out of sync, in which case you lose confidence in your tests.

So having it in one spot, is I think really great. And we do have the capability to run browser tests that's built into lucky because I think it is still good to have at least a couple smoke tests for your critical paths. To test the happy path. Um, but I mean if you can write fewer of those, that's great cause they take forever to run.

Jeremy: For sure. Yeah. Um. In lucky, there's a lot of features that in other frameworks would be not usually be included. Like for example, there's authentication. you have this setup check script to see if your app has all of its dependencies, things like that.

I wonder if you could sort of explain sort of how you decided what sorts of features should exist in the framework versus being something that you'd leave to the user to decide.

Paul: I think things If there's no downside for one thing, if there's no downside, only upside and almost everyone would benefit from it, I want to include it. So that's, for example, the system checks script. Um, we also have a setup script and that's what we tell people to use. Instead of saying like, first installed yarn and then run your migrations and blah, blah, blah.

No our documentations don't even mention that. It's like run script set up. Um, and the idea there is, it serves as kind of a best practice. It kind of pushes you into things to say like, Hey, put stuff that you need in here. Then we lay it on the system check, which also runs before setup. And also every time you boot the development environment, um, where it'll check, Hey, do you have a process manager?

Which you need. It'll check whether Postgres is installed and running, because that's required. so if you go back to kind of that criteria, it's useful to pretty much everyone. Meaning like, if Postgres isn't running and the app's not going to work, everyone would need to know that. Um, and it doesn't really have a downside.

If you don't want it for whatever reason, you just delete it. Or stop running it, that's not a huge downside. That's like,  one click. So that's part of why that's included. I don't like spending time on things that aren't delivering actual real value.

So I don't like spending time figuring out why my local environment is not working or why it was working and now suddenly isn't. And with something like a system check that makes teams happier in the sense that, let's say all of a sudden ads somebody adds a new search capability and it requires elastic search, and I do git pull from master, do my feature as soon as I boot the app, if they've added something to system check that says, Hey, you need elastic, it's going to tell me it's not going to just blow up.

It's going to be like, Hey, you need elastic search now. Install that and run it. These are the types of things that I really think are gonna save, a lot of time in terms of auth. that's another one of those where it's like, so many people want it and it should be easy and simple and not like five different ways to do it, but not everyone wants it, which is why, we made it optional.

You choose in the wizard, like if you don't want auth, fine. I guess that most people generate it with off. I know I do cause I need it. And the thing is, we also changed how auth  works in the sense that it's mostly generated code. It's not just a bunch of calls to some third party library. So what that means is it is easy to modify.

So if you want to add email confirmations or invitations or anything else like that. You're not mucking around in some third party library. It's code generated in your app that you can see and modify. So it doesn't lock you into anything. It's very flexible and it helps you get off the ground running.

And that's why that was included. Uh, and I'm sure we're going to have other stuff that may be included or at least an option of being included in the future.

Jeremy: Yeah. I think, one of the conversations that people are having now is  particularly in the JavaScript ecosystem.

you end up pulling in a lot of different dependencies. You end up having to make a lot of different decisions. And so it's interesting to sort of see,  lucky kind of move back and in the direction of say, a rails of trying to kind of include the things that you think probably most people building an app are going to need. 

Paul: Yeah, it's a little more in that direction. I think on the flip side, rails is starting to include so much that people are starting to get mad almost, and it's like so much that you're like, what is this? What is happening. So we want to strike a balance there. And so part of that is being very careful about what is included.

I think some of the things that are included in rails could just as easily be added after the fact, meaning, 20 minutes of work and you can add it. Those are the types of things I probably would not include in lucky if it's 10 20 30 minutes to,  add it and modify your app. And only 50% of people even want it.

We're probably going to just say, here's a guide on how to do it and make it easy, but not do that as a generator, if that makes sense.

Jeremy: What's an example of something like that that would be pretty easy to add in after the fact and doesn't necessarily need to be included?

Paul: Um, well, in rail six, it's coming up. They have this action mailbox thing that handles inbound emails. I'm pretty sure by default that is included. I could be wrong, so don't quote me on that. But I've been seeing a lot of Twitter stuff lately of people being super pissed about it, so I think it's there.

Um, that's something I definitely wouldn't include because I think I've written one app ever that uses inbound emails. I mean github does too, but I have not written that and a lot just don't have that. So it's odd to include it, especially given the fact that it's not particularly hard to set up yourself. I think based on what I've seen, or action text is another one where it has ways of making rich text editing easier. That might be something too where. It could be added on later that I think, at least as a little bit more merit, because I think it's fairly common for at some point to be like, we need a rich text editor.

Um, but those are the kinds of things that I would probably push off. And it's not a best practice either. Meaning I think it's smart that it has active record by default and chooses a database for you. Um, because it's best practice to just use active record. Right. And you're gonna have the best time using active record.

Cause that's what everyone uses. So including that makes sense. But yeah, something like action mailbox is like what's the benefit in including it

Jeremy: Yeah. Just because the majority of people who are writing applications, they'll never need that inbound email feature. Uh, as opposed to, your example of authentication, like probably the majority of applications people are building will have authentication in them.

Paul: Exactly. Yeah. And it's something that's hard to add, meaning um it touches so many parts of your application. And because we are generating stuff, it's not easy to add after the fact. but stuff that. Is easy to add and easy to remove that. Another criteria is how easy is it to remove it? So we include a few default CSS styles, but super easy to remove.

It's basically like you go to your application dot CSS, it's like delete everything below this line. You delete it and it's like you're done. But it's nice because it makes it look decent and not like a horrific, ugly thing when you start your app, but it's easy to remove. And so that's something, for example, that we also include by default.

Jeremy:  That's also, I think the distinction between something that's generated code and, or configuration that the user can see. Um, I mean, I think your. Set up scripts and your system checks, scripts. Uh, one of the things that makes those kind of more straightforward is the fact that they are in your code base and they're their bash scripts, right?

So, if you want to modify it or you want to remove it, they're, they're kind of right there. Whereas something like a action text or action mailbox is probably in like. the rails gem, right. It's in the library, so you don't even see it in your code base. I guess that would be the distinction there.

Paul: Yeah. Or you might, but you don't know why it's there or what it does. Or. Yeah. Another concern is how many things does it hook into? so for example, one of the big things is, like I said, do default styles. How many places does that hook into things? Just one, you go to your, your main CSS file and delete it, but there's a way to do that that I don't particularly like.

I've seen some people, for example, use bootstrap or any framework. It doesn't matter what it is. The problem with those is it also modifies the generated HTML and the scaffold. Cause by default it's adding classes like column three, medium button, blah, blah, blah, blah, blah. If you don't want to use bootstrap, you have to remove bootstrap and manually go through all of the generated HTML files to remove the bootstrap classes.

And so that's like a key difference too is how easy is it to remove. And we've really want to only add things that are easy to remove or really hard to add.

Jeremy: What, what is the, uh, adoption of lucky look like? Do you know of people using it in production currently?

Paul: Yeah. I don't have exact numbers. Um, which I think is good because it. Reduces anxiety a lot. Not knowing is like, is it going up? Is it going down? But people are using it in production. a lot from the very early days of crystal, one of our core team members, um, Jeremy, he's been using it at work for two and a half, three years.

And they've had great success with it. They replaced some of their rails and microservices with lucky, uh, originally for the performance boost. And I think this is common. They stay for all the nice type safety and the reliability they get. Um, it's hard to explain with just words, but then you use it and you see an error and we try and make them nice.

Not all of them are. But we try and make it nice and people go, Oh, this is nice. Or people are annoyed that they see this compiler error and then realize, Oh, wait, actually did catch a block. So, but they're having great success. Um, big performance boost. like something like they reduced their number of servers by like 70%, and their response times got cut down 60 or 70%.

So yeah, they're having great success and then a few other people are building client projects using lucky. I don't know what they are. Some people, there's just not, they can't say to the public, unfortunately. But yeah, people are using in production, which is really exciting.

Jeremy: Looking at, the crystal community, what does that look like?  is a pretty active what are your thoughts on the community?

Paul: Yeah, it's quite active. Um, they've got sponsors, quiet, quite a few corporate sponsors, so they're making decent money to help fund development. They're aiming for 1.0, I don't know exactly when, but they did a blog post. I'm saying it's going to be soon, and I've talked to them in person about it, but I don't know how much  I was supposed to say, but soon.

Um, which is fantastic because then you're not going to have to deal with the breaking changes, which have definitely been happening the last two years. And I think it's good because the language is improving and changing things. But once 1.0 hits, people are going to be able to jump in and they're not going to have to update their apps every 3 months or whatever.

Um, but yeah, a lot of participation, and the sponsorship money goes a long way. A lot of the development is based in Argentina and the dollar is super strong over there. so meaning if you've got corporate sponsorship in dollars over here, that goes a really long way towards the development. Um, and they're all super nice.

I've talked to a lot of them in person. Um, super nice, super smart guys. The community itself in terms of forums and chats, that's where I'm a little hesitant. It's, it's active, but I think not particularly welcoming for newcomers. just really strong personalities, very smart, but very strong personalities, and I would say.

It may be better to come to the lucky chat rooms. We're very strict about our code of conduct and not about nitpicky things, but just in general that,  you talk to people with respect and empathize, and we're not the type of people where you come with a question and we're like, well, did you Google it?

We're going to try and help you. And so I think it's a very welcoming community. And even if you're not using lucky. Feel free to hop on our chat room. Um, if you go to the lucky website, there's a link.

And uh, yeah, we're pretty nice over there. So things are moving forward. We're trying to get to around the same time as crystal. Um, maybe a little after, but I think that'll be a big milestone.

Jeremy: it's interesting talking about the community. Because I think when you think about Ruby one of the big parts that attracts people is not just the language or the framework, but it's,  having an inclusive community, having people that are really friendly. It's good to hear that, lucky is striving to do that. Why is there that divide?

Paul: Uh, I'm not entirely sure. I mean, part of it is I am a sensitive person, and so I am kind of trying to create the community that I want, which may be actually way more, upbeat and positive just because, I want new people to feel comfortable. and I think maybe part of it is, with crystal, they don't have that much time, I think, is part of it. And so it's easier to brush stuff off. Some of it could be just that they don't care about the same things that I personally do.

There's nothing actively bad going on. It's just I prefer things rather than to just be okay or average. I want it to be exceptional. And a place where it's just like, don't worry, you can say something. If it's, you feel it's dumb. We're not going to be like, pile on.

We're going to be like, Hey, it's fine and here's maybe an alternative. so yeah, I mean, go to the crystal rooms. I still do. I still get help. There's a lot of really smart people. Um, you just gotta put on like a little thicker skin and be prepared for like, why do you want to do this? Have you tried this other thing?

Have you done this other thing? In a way it's a good thing because they're making sure that like you've tried your different options and you're not just asking to do something that's a horrible idea, but it can make people, I think, feel like their ideas getting attacked or whatever.

Um, so that's what I mean by part of it is just like, if you're sensitive, that's gonna come off as probably harsher than it was intended. Um, but you can still get a lot of help.

Jeremy: Yeah, I guess it's just trying to find the right level of, yeah. I don't know what the word would be, but, yeah. Making people feel comfortable.

Paul: Yeah, I do have a really high bar for that because like I am sensitive and I grew up when I learned to program all online with books and with forums. And I remember how hard it was as a new developer that didn't know best practice and people would be like, why are you even trying to do that?

It's so stupid. And it's like, dude, I've been programming for like six months, calm down. And, I think it's common. I think, I mean, that happened in the Ruby forums happened in the rails forums. it's a common thing, I think across the internet and various communities. So it may not even be that Crystal is particularly bad.

It's probably a lot like most communities, but we just want ours to be exceptional. Um, in terms of making people feel welcome and  if someone has a bad idea and air quotes bad because maybe it's a great idea and we just don't have the context, but if it is a bad idea, we're not going to say, why are you doing that?

Blah, blah, blah. First, let's help you solve your problem and then talk about how might this be better? Maybe there's a better way to do it. And. It just feels a lot better. People are more accepting to have your feedback when you're not just immediately jumping on them and say, why are you even trying to do that? I think that's important.

Jeremy: Yeah. I mean, I think that probably applies to really all projects, right? Like they could all kind of stand to learn from some of that. And Kind of see it from the other person's perspective who doesn't have sort of all the. The same knowledge that you know you've been building up and maybe they can bring you a new perspective as well that you didn't, you didn't even think about.

Paul: Yeah, totally. I mean, we've changed stuff in lucky a lot of stuff that I was pretty sure about and they asked if it could be done differently, shared their use case, and it's like, Oh yeah, I made a mistake. And so it's good for everyone. Like if you show a little bit of vulnerability and openness, you're much more likely to learn.

And you're much more likely to learn new and novel things because the people with, the strongest opinions are often the ones that have that opinion based on some principle they read about or a talk or something else. It's the quiet people that are like, Hey, can we try doing this like a little differently?

And you're like, Whoa, I've never thought of this. Because no one else has, but you're new. You came up with this great new, innovative idea and he felt comfortable sharing because we're not just shooting people down constantly and so yeah, I wish more communities did that in general because it's mutually beneficial.

Jeremy: That's a good place to start wrapping up. Where should people go if they want to learn more about lucky?

Paul: First place, luckyframework.org. That's the main website. It has guides. it has blog posts that you can follow or subscribe to with new announcements. Uh, and it has a link to our chat room as well as the github. So that's where I'd go. Feel free to hop on the chat room anytime. Um, we're all really helpful, and try and be nice. And so like, people shouldn't hesitate to run in there if they have problems. Um. If there's stuff that's confusing. Um, feel free to open an issue on lucky. We have a tag that's like, improve error experience. So we're, we have dedicated stuff just to do that. Yeah. In fact, if you start a lucky project, then you get a compile time error when you first start or are fresh on a project, it says, Hey, if you're still stuck, go to our chat room and ask for help. 

Everyone should feel free to do that.

Jeremy: Very cool. and how can people follow you and see what you're up to.

Paul: @PaulCSmith on Twitter. Probably the best way to do it right now. Maybe one day I'll have a blog or something, but right now it's Twitter.

Jeremy: Cool. Well, uh, Paul, thank you so much for coming on the show.

Paul: Yeah. Thanks for having me. I really enjoyed it.

</div>