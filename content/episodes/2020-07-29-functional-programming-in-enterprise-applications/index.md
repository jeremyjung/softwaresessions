+++
title = "Functional Programming in Enterprise Applications with Vladimir Khorikov"

description = "Vlad shares how he applies functional programming concepts in languages like C#"

[extra]
episode_url = "https://media.transistor.fm/14d8762c.mp3"
social_title = "Functional Programming in Enterprise Applications with Vladimir Khorikov"
embed_player = "yes"
embed_player_url = "https://share.transistor.fm/s/02abed28"
+++

Vlad is a Pluralsight course creator and the author of Unit Testing: Principles, Practices, and Patterns.

We discuss:
- Immutability
- Error handling
- Avoiding null
- Preventing invalid state
- Updating existing applications

This episode originally aired on Software Engineering Radio.

### Related Links
- [@vkhorikov](https://twitter.com/vkhorikov)
- [Enterprise Craftsmanship](https://enterprisecraftsmanship.com/)
- [Is Entity the same as Value Object?](https://enterprisecraftsmanship.com/posts/is-entity-same-as-value-object/)
- [Combining ASP.NET Core validation attributes with Value Objects](https://enterprisecraftsmanship.com/posts/combining-asp-net-core-attributes-with-value-objects/)
- [Error handling: Exception or Result?](https://enterprisecraftsmanship.com/posts/error-handling-exception-or-result/)
- [Applying Functional Principles in C#](https://www.pluralsight.com/courses/csharp-applying-functional-principles)
- [F# for Fun and Profit](https://fsharpforfunandprofit.com/)

---

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy:** [00:00:05] Hey, this is Jeremy Jung for Software Engineering Radio. Today. I'm talking with Vladimir Khorikov. Vladimir is the author of the book Unit Testing: Principles, Practices and Patterns he's a Microsoft MVP, and he's the author of many Pluralsight courses including Applying Functional Principles in C#, and today we're going to be talking about functional programming in enterprise applications. Vladimir welcome to Software Engineering Radio.

**Vladimir:** [00:00:28] Thank you for having me.

**Jeremy:** [00:00:29] The first thing I want to talk about is sort of what functional programming means to you, because it means different things to different people.
To you, what are the core principles of functional programming?

**Vladimir:** [00:00:41] If I were to describe functional programming in just a couple of words, I would say that functional programming is programming without hidden inputs and outputs. And that's basically it. And what I mean by hidden inputs and outputs is there are several examples of those. So the most,  prevalent example of a hidden output is immutability.

So let's say that you have a method that takes in some integer and then increments that integer by one. And what it can do is it can return that incremented integer back  as the return value, but. It can also mutate some global state with that integer. And by the way, by hidden, I mean that this information is not present in the method's signature.

So it's not present in the method arguments, and it is not present in their methods, return value. So in this example, when you, when you have this increment method if it, returns. A value, then it communicates what it does, pretty clearly. So it is honest about what it does. But if it instead mutates, global state, then this would be an example of a hidden output because that output is not present in the map at signature.

And to understand what this method does, you have to drill down to that method and to see what. What's actually going on, because it can this information is not present, in the, in the signature itself. So that would be an example of a hidden output. The hidden input is a similar to that. So instead of taking that integer as a parameter, as an argument. This method can also refer to some global state. So, for example, some static property or field, or it can refer to some external service to request that in integer and then incremented and then put in to some global state. So that would be an example of a hidden output.

Also reaching out to external systems such as the database or APIs would be that and also, the simple DateTime.Now would also be an example of hidden input because that input always changes. It basically refers to the systems low level, API, your, for example, windows API or Linux API to, to get, this input value so that's another example of, of a hidden input. Another example of a hidden output would be something like exceptions. So exceptions are hidden output because, when you throw an exception, and that exception is caught somewhere upper, the call stack. This exemption also is not present in the method's signature.

And,  you basically introduce another, Hidden pathway, for your, program flow that is not present in the method signature. So these are common examples of hidden inputs and outputs and functional programming is about avoiding those hidden inputs and outputs. If your mathematical function, your pure function would be something that, accepts a value, as an argument and returns a value and doesn't do anything other than that.

**Jeremy:** [00:04:06] Okay, so let's sort of break down a few of those. So. The first thing is  hidden outputs in terms of if you pass something into a function and the thing that you pass in becomes changed, then that in effect is a, hidden output because, there is no way of telling just from the method signature whether that behavior is possible.

**Vladimir:** [00:04:30] Correct. Yes.

**Jeremy:** [00:04:31] And so you're saying that the alternative to that is to make sure that the function is pure so that when you pass something in, if you are going to make a change, it would not be to what you passed in, but it would be something that you're returning back.

**Vladimir:** [00:04:50] Yeah. So instead of mutating the state of some existing object, what you need to do instead, in functional programming is you need to create a new object with the required properties. So instead of mutating the object that is passed in, you need to create a new object with new properties and return it back.

And with example, with a number increment that that's basically it, because when you increment the number by one and return it back, you're not, Changing the input parameter because it's a constant, you cannot change it. What you do instead is you create another number and return it back.

**Jeremy:** [00:05:26] And when we think about objects that we pass in, or we think about collections. a lot of times the objects and collections we work with are mutable, right? Like, we can have a list type in C sharp, for example, and we may want to add something to the list or remove something to the list. If we are instead creating a new list every time we want to change something, what are the performance implications of that?

**Vladimir:** [00:05:55] Well, yeah, definitely. So there are trade offs  to functional programming. And one of the most common tradeoffs to,  any immutability is this trade off of, Always creating new objects instead of mutating new ones. And, that's actually the reason why object oriented programming, has become so, so popular in the past.

Because if, you know, functional programming actually was introduced before object oriented programming. but why it didn't take off is because,  computers back then were not as powerful as now. And so it was very costly to do functional programming with all those memory allocations, with all those new object creation.

So it was very costly to do so. And what we had had instead is we started to operate  at the lower right level, of our programs. And we started to think of, , in terms of, memory allocations. So, but now we're kind of getting back to the roots and starting to,  to do more of what we did back then.

There are definitely trade offs here. And if your performance requirements for your application are strict, then there are some restrictions. So there are some limitations and probably you will not be able to implement some functional programming approaches.

But in most business line applications, that's not something you need to worry about. So if you write some framework, for example, an ASP.NET Application not application, but the server itself, Kestrel, then you do need to worry about that. But in most enterprise level applications you don't, so performance is not the biggest concern.

The biggest concern is usually the complexity and the uncontrollable growth of complexity. And, what functional programming allows you to do is it allows you to reduce that complexity at the expense of maybe not as performant code as you could have otherwise.

**Jeremy:** [00:07:56] So would you say that in the average application that the developer should default to making things immutable, is that a reasonable default for most developers?

**Vladimir:** [00:08:09] I would say so, yes. If it is possible, then you definitely need to default to creating immutable classes, immutable objects by default, it is not always possible and one of the limitations why is in object oriented languages it's pretty hard to create new objects based on the existing objects. So, for example, if you take F#, there is a really nice  language feature where you, where you can take data structure or an object, and, create a new object based on that,  existing object, but with the mutation, of, with the addition of new properties to that object. So you can say, for example, old object with, some property equals a new value and some other proper property equals other new value.

And what it will do it will not mutate the existing object, but it will create a new object with those two properties changed and then, but all the old properties they will remain the same. And this is a really nice feature that helps you to default to immutability. Unfortunately, in object oriented languages like C#, we don't have such features and so it's not always feasible to do so.

What I recommend you do instead is if you have some value, Or a simple class, you can wrap it into a value object, which is immutable. but for, for all other classes such as entities, like for example, a user or a company, that is usually something that you need to mutate, that is an example of an entity.

It has its own, inherent identity, such classes usually it's usually not feasible to make them immutable, but what you can do is you can keep them mutable, but put as much logic as possible to those immutable value objects. And this way  you can keep the separation between complexity and immutability.

So your objects will be either mutable or complex, but not both.  You  keep the separation between the complexity and, mutability because it is, when you combine the two, you start to have, these problems with the, the ever increasing complexity with unmanageable complexity.

**Jeremy:** [00:10:28] And you were referring to the concept of entities and  value objects. Is that right?

**Vladimir:** [00:10:34] Value object, yes.

**Jeremy:** [00:10:36] And so what, what is the distinction between those two? You were saying that a value object should be immutable and an entity could be mutable. Like how do you decide which is which is, which?

**Vladimir:** [00:10:48] Yeah.  these two concepts are, from the domain driven design, but they are actually applicable to an application in which even if you don't follow, domain driven design principles, it, it is handy to refer to your objects in this way anyway.  The main distinction between them is that an entity is something that is trackable, by your application has an internal, inherent identity.

An example I often give is, let's say you have a dollar bill, so you have money class, and this money represents a dollar bill. So this dollar bill  would be a value object in most systems because in most cases, you don't really care if you have the exact same dollar bill as you had before.

So let's say if you give someone a $1 bill and they give you back a also $1 bill. You don't care if it was the same piece of paper as before because for you, they are interchangeable. And that is  one of the most important properties of value objects. They are interchangeable, but that also depends on the domain model so on your context, for example, if you create a system that tracks those dollar bills, dollar notes, then in this case, the, those bills and those pieces of paper, they become entities because you do care about each individual a piece of paper. so you, for example, you can have the number on that dollar bill as the ID of your entity, and then you track, where it goes throughout its lifetime.

So it becomes an entity because it starts to have its own identity, its own identity, and you cannot exchange $1 dollar bill for another one because you do care about the history.

**Jeremy:** [00:12:42] Does this mean that pretty much anything that's an entity would also exist in some kind of permanent store, like a database?

**Vladimir:** [00:12:50] Yes, exactly. That's because you as I said you care about the history of that entity and what it usually manifests in as you need to persist that entity in the database. And then look after the changes in this entity.

**Jeremy:** [00:13:05] And you were kind of referring to the fact that these entities could act as wrappers to value objects. So I want to kind of give an example of, let's say I have a a ride sharing company, and I'm keeping track of my, my fleet of vehicles. So I have cars that are driving around the city and they're all reporting back to me, their position.

And each of my cars has an ID which parts of my, data would be an entity and which part would be a value object?

**Vladimir:** [00:13:38] Yeah. That's a good example of where you can apply this entity value, object separation. So the car itself would be an entity because you need to track it. That's, the primary indication that it is an entity. It has an  ID, and the position itself would be a value object because you can replace it with another object, with the same content and two positions of the same type and content, they are interchangeable for you. So yeah, that's a good example.

**Jeremy:** [00:14:08] And so the individual updates, they would have the ID of the vehicle and the actual position. That could be a value object. And as I'm receiving multiple updates from each of my vehicles, it's reusing the same ID. And, in my database, I might want to keep a history of, you know, all the locations that my car went.

So with those historical positions, would those be their own entity, or what would those be?

**Vladimir:** [00:14:41] So the positions themselves would not be their own entity in this case, what would be an entity is the historical record. So in this case, you wouldn't have the position itself as an entity with an ID, but you would still have some, let's say, vehicle history record or something like that, as another entity that would, also contain the position as a value object.

So, you will have this kind of nesting here where you still have the same value object, but the entity would be a different entity.

**Jeremy:** [00:15:15] I see. And so the reason that we have the value object is that it sort of tells our system that this concept of a location is identical, whether it's in the context of being an update, I'm getting from a vehicle versus, a historical position. They're really both the same concept, so I can use the same value object for both.

**Vladimir:** [00:15:40] Yes, exactly. it is much easier to reuse this position value object between these two concepts. And also, another reason why you wouldn't want to introduce a value object for these two positions is because it is much easier to keep consistency, in this way. So let's say you have other properties in your vehicle other than the position itself.

So yeah. Let's say vehicle has,  a license plate. And let's, let's say it has two numbers of its license plate, and it also has, two properties that display  the position of the vehicle. So X coordinate. And. Y coordinate let's say. Why you would want to introduce value objects  is to reduce complexity. Because when you have, those four properties as just four properties, then the number of permutations between them is higher. Then it would if you group, those properties into separate value objects.

So if you group the two properties that belong to the license plate into a value object, and you also group, the two coordinates into the position value object, then you will have only two properties inside that vehicle. And the number of permutations between them is much lower. It's just two, whereas the number of fermentation between the four objects is going to be  well, mu much larger, much larger number (laughs).

So, that's a good way to think of complexity of your system when you reduce, the number of properties that you need to keep in mind your software automatically becomes much simpler because it becomes much easier to keep the consistency because, for example, when you accept a position, what you need to do is you need to just, check the correctness of that position on its own without It's connection to other properties of the vehicle and the same for the license plate, you don't need to validate that license plate against the, the position coordinates. So yeah, the validation becomes simpler and just maintenance overall becomes much simpler too.

**Jeremy:** [00:17:46] And so it sounds like rather than having vehicle update type, for example, and making that object be responsible for it, the validations of the license plate and  the validations of the position information. Instead, you break out those concepts into their own objects so that those objects, when you create them, they validate whether or not it's valid.

And so as long as you can successfully create one. You pass it into the constructor for the vehicle update entity and you, you know that they're correct because, they were already validated before you passed them in.

**Vladimir:** [00:18:26] Yes, exactly, and that is one of the benefits of functional programming is that when you keep your objects immutable, your value objects immutable, you only need to validate those objects once. When you create them after that, you are, you can be sure that those objects remain in the consistent, in the correct state, so you don't need to validate them afterwards.

**Jeremy:** [00:18:49] Do you find that in development code wise, is it easier to reason about what's happening when you're creating these objects and then creating the entity and then passing these objects into the entity versus having a larger constructor for the entity?

**Vladimir:** [00:19:08] Well, it depends on the use case. So, yeah, usually what I like to do is I like to, Do it hierarchically. So you first create, lower level objects such as, as you said, value objects. Then if you have some other value object that consists of those lower level of value objects, you create that value object and then you pass that you, you kind of  create that structure where you go bottom up from the lower level objects to the higher level objects, and you create them sequentially one by one, and on the top at the top of that pyramid, you have the entity itself, which you can create just by passing those already validated value objects into that entities constructor.

And you don't need to do much else. So the entity itself becomes a much simpler to maintain.

**Jeremy:** [00:20:01] And these examples we've been giving the value objects, they've been able to validate themselves. Like for example, the position,  there's only a fixed set of numbers that are valid for the position, and so we could validate that without talking to an external store or a database or anything like that.

How about when you have a case where. To see if something is valid. You need to talk to an external API or talk to a database. Like for example, if there was some kind of, driver registration or like a license that's associated with the car and you needed to talk to,  some kind of. State API or,   city information to find out if that car update is valid, where, where would that exist in your application?

**Vladimir:** [00:20:50] Yeah. So there is kind of debate into where you should put this logic. I strongly recommend not putting it inside your domain model because your domain model shouldn't talk to any external systems. So you should make that domain model as functionally pure as possible.  Let me step back for a second and,  describe what I mean by that.

So what you want to do in your application, especially if you try to,  adhere to functional programming,  you don't actually want to make all your code immutable because that's usually impossible. when you create an application, you do want that application to mutate some state because otherwise that application would be useless.

For example, if you create a user or if you update the vehicle information, you do want to, you do want that information to be eventually updated. So the vehicle record and the database, it should be updated. What do you need to strive for is the so-called functional architecture. And this architecture is, where you have some sort of a sandwich between, where you first gather the information required for the business operation.

Then you delegate, that, information. So you pass that information. And delegate the work to the domain model. And then when the domain model, completes its work, you persist the results of that work to the database. And so what you can do here is you can make your domain model as purely functional as possible, and this way you kind of push the mutable operations to the edges of your system, to the edges of your business operation.

Because as I said, you cannot, skip those  mutable operations altogether, but you can kind of, work around them. and with this approach, with this functional architecture, what you achieve is you achieve the separation between, the two important concerns. So the domain model is responsible for your, domain logic.
And, I like to call it, immutable  and the rest of your system becomes mutable shell. So it is a dumb shell that is responsible for communicating with external systems. primarily. And so, the two responsibilities here are the domain modeling and orchestration and you don't want to mix them together because, when mixed together, they overcomplicate your code.

You know, you don't, you don't want to do that because, the code becomes much harder to maintain. So, yeah, so this is the functional architecture, this kind of sandwich where the beginning at the top of your business operation, it talks to external systems.

Then it passes control to your domain model, which is as purely functional as possible. And then  at the bottom,  all the decisions made by the domain model and communicates it to external systems, including your database. 

In some cases,  the flow of your domain logic itself depends on what kind of response you get from external systems. So in your, in your example, this response would be whether or not this vehicle. With this, number already exists in the database. And if it does, you cannot register a new vehicle with the same number.

What you can do is you can delegate some decisions to the controller,  for which you have to reach out to external systems such as the database because the alternative to that one would be to delegate this responsibility for communication with the database to the domain model itself. And this way you will keep the controller simple, but you will make the domain model impure. And that is, in my opinion, a worse option. even though you kind of keep the controller simple and you kind of keep all the domain logic inside the domain model, it's still not the best approach because you want to separate that domain model from this responsibility of communicating with external systems because, when, these two responsibilities are combined together, that's, when you start to have an over complicated code base.

**Jeremy:** [00:25:09] If I understand correctly, it sounds like anything that has to do with external systems, even if it's a part of validation, those calls should be made at the outside layer. Like for example, in your application controller or in an object that's receiving messages from an external system.

And, that is where you would make the call to check in your database to see if, for example, if this was an ID that already existed. Or if, you know, we needed to talk to some citie's registration system to see if this vehicle is licensed. We would do all of that outside of the, the value objects. We would do that more in our controller or in some area outside of all of the internal domain objects.

**Vladimir:** [00:25:59] Yes, that's correct. So, your, domain model you cannot delegate this responsibility of maintaining consistency that spans across the whole database. So you only need to delegate to our domain model. the consistency requirements that span, the objects themselves. So ideally it should stay within a single entity or, in domain driven design terms an aggregate an aggregate is a group of related entities.

If you're consistency requirements spans more than one aggregate or one entity, then yes, it's usually, it should be attributed to the controller itself. So, and, they check for uniqueness, let's say user, email, uniqueness or vehicle number uniqueness. That's an example of such a validation. Yes.

**Jeremy:** [00:26:49] Let's say you have a value object that is a, vehicle and before we checked with the database, we didn't know if it was a valid new vehicle or not because we didn't know if it was already existing or if it's truly new. And at the controller we make a request to the database and we find out that this vehicle doesn't already exist yet, so it's a valid request to create a new vehicle.

Would we then need to create a new type that says like, this is a valid, vehicle creation request, because if we hadn't done that check yet, then we, we wouldn't actually know if it was valid yet. I don't know if that makes sense?

**Vladimir:** [00:27:32] Yeah, it does. so what you're talking about is you want to have, let's say an idempotent request that would either create a new vehicle or update an existing one if it already exists. Correct.

**Jeremy:** [00:27:46] Sure. Yeah.

**Vladimir:** [00:27:47] Yeah. I wouldn't create a new request, for that. So, if it is a requirement, if it is a business requirement to do that in one go, which it sounds like it is here, then I would just attribute this logic to the controller.

So first check, if this vehicle with this ID exists, and then, go from there, either update its position. using this value object or create a new vehicle using the same value object. So, in this case, you will work with the same position with your object anyway, because you will use it for creation and for update of the vehicle position.
And so it's just a matter of,  what to do next when you see if the vehicle exists or not.

**Jeremy:** [00:28:36] And so after we've completed this validation and we've created our value object, then when we persist it to our database, that would also be in the controller. Is that correct?

**Vladimir:** [00:28:47] Yes. So the creation  of the vehicle. That part would be the domain logic part. So if we are talking about the sandwich architecture, again, the functional architecture, then at the first, the top part of the sandwich would be reaching out to the database to see the vehicle exists.

The middle part for the main model part would be the creation of new vehicle or, the update of the, the update of the existing vehicle. And then the bottom part would be a saving that vehicle to the database. Yes.

**Jeremy:** [00:29:22] And I want to kind of step back to, at the start of our conversation, you were talking about hidden inputs and hidden outputs. And one of the things that you were talking about as being a hidden output is, a exception. For example, like if there's an error that occurs. You may not know, that an exception is something that can return,  Walk us through like why that's an issue or if that is an issue.

**Vladimir:** [00:29:53] The issue here is not the exception per se. But how you use those exception . So if you use those exceptions for validation, then it does become an issue. what I'd like to see with regards to exceptions is that exceptions are for exceptional situations only. And what I mean by that is situations that you did not expect to happen in your application.

Validation is by definition, an expected, situation. Because you do expect your clients or your users to enter incorrect values or send you incorrect data and so on. And so when you validate that data, you do expect it to be sometimes at least to be incorrect. And so, what you can do is you can, for example, validate that data and then if it is incorrect, you can throw an exception saying that this data is incorrect. But, it has the drawback of, of this hidden output that I mentioned earlier where you create   another another path in the program flow that is not, that is not present in the method signature.

So let's say if you have a method a void method, that accepts some data and then throws an exception, you, you cannot be sure what it does,  so you cannot be sure how you react to these exceptions, because it could be that these exceptions are caught at the method that now call this validate method, but it could also be several layers upward the call stack, and so it becomes much harder to debug this application and much harder to understand what it does.

Whereas with something like a result type, what you could do is you can explicitly return the result of the validation from that method and this, this way, you will make the signature honest. So an honest signature is something I like to also refer to a purely. Purely functional method would have an honest signature because it will tell you explicitly what it does, what it, what inputs it has and what outputs it produces.
The drawback with the result type is that you often need to write more code, because without them, you can basically just, make several validations, call several validate methods, and then if something is wrong, you will catch an exemption in the catch part of your application. But with the result, you have to, process each output separately. So you have, the first result, which you need to process and the second one and so on. And also another issue here is that, it becomes, at least in  object oriented programming languages like C#. It becomes simpler to, omit that result because there is nothing preventing you to just forget about it and ignore it. And yeah, that, that could be an issue. And that is one of the trade offs of this functional programming approach. but again, I think, the benefits of this approach, overweight the costs because you're becoming much more explicit. In the values, those methods for return.

And it is much more maintainable in the long run. And by the way, this issue with, the ignorable outputs, it is only present in OOP languages, like C#. For example. If you take F#, you cannot just ignore an output, which is none, which is non void or unit in F# terms, you have to pipe it into special function, ignore.

So you can always see that you are ignoring something because you're seeing that, the return value is piped into that, ignore method.

**Jeremy:** [00:33:44] For those who aren't familiar with result types, can you kind of give a brief explanation of what they are.

**Vladimir:** [00:33:51] Yeah, sure. So a result is an explicit representation of some operation. So let's say, when you perform some operation, let's say you're trying to, save. Something in an external system. let's say that you want to update your profile on Facebook and you're using a Facebook API for that.

And, so you're, you're doing some API calls to the Facebook API and this operation, obviously may fail. And one of the ways to to deal with that failure is, as I said before, is to use exceptions, but that's not the best way to deal with that because I, it is not often obvious where exactly you process those failures.

A better way would be to catch those potential exemptions from that API at the lowest level possible, and then wrap them into an explicit structure such as a result class and the result classe is a simple structure that tells you whether or not this operation succeeded. So it has. such fields as is it a failure or is it a success?
And if the operation was supposed to return a value, then you can also make this result, class generic. And if it is successful, it can also contain a value, that will contain the result of the operation.

**Jeremy:** [00:35:12] The benefit of using the result type is that your function signatures, they become very explicit in telling you that this call that you're going to make, it could succeed or it could fail. And this result type is going to tell you,  whether it succeeds or fails and that way, you know, to write code to, to account for both cases.

**Vladimir:** [00:35:33] Exactly. Yes.

**Jeremy:** [00:35:34] One of the things about exceptions is that when an exception occurs, there's a lot of information that's kind of embedded with it generally a full stack trace, for example, whereas with a result type, you may not have any additional information on why something failed. how do you deal with that or, or are there cases where you would say it does make sense to use an exception instead?

**Vladimir:** [00:35:59] Yeah.  I'm not saying that you shouldn't use exceptions at all because there are use cases for them, and one of those use cases is, well, actually the only use case is where you have an, a situation that you cannot, you don't know how to deal with. And for example. if that Facebook API returns an error that you didn't expect.

so let's say that when you wrote the software, you expected some set of return values, return errors, some set of errors from the Facebook. Let's say that the user doesn't exist, but if it returns some other error, some obscure error, you don't necessarily know how to deal with that error.

And in this case, because you don't know how to deal with that, it is preferable to throw an exception. This would be an example of an unexpected situation for which exceptions are preferable.  because exceptions represent unexpected situations in code, you shouldn't catch them.

you should only catch them  at the topmost level of your call stack. And the only way,  you should react to them is to just log, what exactly happened. And then, basically crash the application. Or if it's some background process, you need to just restart all over again.

Because otherwise if you are if you're trying to continue working  after this exception took place what you can run into is you can run into an inconsistent state where your program entered some, state where it. It's kind of still working, but, it may become inconsistent and even save some data into the database where it will become much harder to deal with because you want to avoid that inconsistency as much as possible and  as soon as that inconsistency takes place, you want to stop everything, basically crash your application. And that would be the only use case for exceptions. And so in this case, you do still have the call stack, which you can then log somewhere and deal somewhere somehow later.

But. If it is an expected situation, let's say that the Facebook API returned that this user doesn't exist, then you do know how to deal with that and you basically don't need the exception,  stack because you can just, process this, error from the Facebook. Turn it into a result object, and then,  return back to the caller and that caller then can in turn show some friendly error message to the user.

**Jeremy:** [00:38:42] So, so basically when you're working with external API APIs, like  the Facebook API, you may make a HTTP request, and maybe it times out and the HTTP library that's built into C#, I believe it would throw an exception. and what you're saying is that you would know ahead of time that I expect that there may be times where my request times out or it fails, I'm going to catch this exception and then I'm going to return a result type that kind of explains what the failure was, rather than, just throwing that exception and catching it somewhere else.

**Vladimir:** [00:39:19] Yes, but that depends on whether or not you know how to deal with that, even if you expect some time out.  Yeah, let's say that the Facebook API, calls to that API may time, time out from time to time. So you need to see whether or not you can deal with those errors. Because if you cannot, then even if you expect those situations to happen, you basically cannot do anything about them.

And so you need to throw an exception anyway and that could be because let's say, the Facebook API is essential for this operation, and you cannot proceed without a response from Facebook. But if it is not essential, let's say if a user updates its profile and you want to update its Facebook profile as well simultaneously, but if you cannot do that, then still fine you can proceed further.

So in this case, you can see you that this facebook call  was a failure, but you know, that it is not essential for this business operation and you can just ignore that result and move on.  And another example, let's say you write an ORM such as entity framework, and, in this ORM. The lack of connection to the database would be an exceptional situation because  you cannot do anything about that.

And you don't know,  how the user of your library will react to that exception. And so in this case, because you as a library writer, you do not know how to deal with that exception. You also need to throw an exception and then the library or a user such as yourself or myself, we can decide whether or not this operation was essential for us and whether or not we can proceed, with that exemption or not.

So let's say that when you're trying to save something to the database, it is preferable to do that. Say, for example, when you try to log something into the database. So it is preferable to that the log is successful, but if it's not, then not a big deal. And so in this case, you also need to,  to catch and that exception that the library throws and then transform it into a result class and then process it, upper the call stack.

But if it is essential for your application, let's say you're saving not a log entry, but the user itself, then even if you know that this ORM can throw an exception, you cannot do anything about that, and so you shouldn't process that exception. You should basically allow it to pop up to the upper layers where it will be logged and the application will crash.

**Jeremy:** [00:41:58] Another thing that you sometimes talk about in the context of functional programming is this idea of how object oriented languages, they usually have a null,  concept where. Instead of returning the object, you expect you return a null. And that could be because you couldn't find the element it could be any number of reasons. What are the drawbacks of returning a null?

**Vladimir:** [00:42:25] Yeah, it's a common $1 billion mistake that all object oriented programming languages have in them. And that is the problem we have now is that, they make all your code dishonest because what, . What they do with your code. Let's say that you return a user from some method, and that user is a class.

So in C# classes are nullable. all classes are nullable, so they, you can return not an object of that class, but now that would be a valid program from the compiler perspective. the problem with that is that you cannot differentiate between nullable user and the non-nullable users and where you can, see a method that returns that user.

What it actually does, it returns a special, class, which you can call user or null because it may be either a user or null. And so when you want a non-nullable user, you, there is no way for you to do that. because all, as I said, all classes are nullable by default. and yeah, that's the problem because that introduces another hidden output that you cannot see just by looking at the method signature.

**Jeremy:** [00:43:36] One of the things that you've, done as a way to kind of push back against that as this concept of a maybe or an optional type, could you explain what those are and how they're used?

**Vladimir:** [00:43:47] Yep. I think what I did, in this course, yeah, I'm trying to remember, it was several years ago. Yeah. So what you can do instead is there is a good tool, it's called fody null guard that you can use to basically inject null checks in all your methods and properties. And what it will do is it will check all input arguments for nulls for you and also it will check output, return values for nulls as well. And it's a very good tool. I tried to use it, in as many of my projects as possible, but it's not always possible, let's say that. And what it does is it. Helps you to approximate your code to this world where nulls do not exist.

So, if you try to return a null, where your method returns a user, your method will automatically throw an exception because of this automatic checks for nulls. And to avoid that, you will need to use a maybe or an option as in F#. So, and Maybe is a special struct that you can use to explicitly tell the clients of your code which parts of your,  inputs or outputs can be null.

And because it is a maybe it itself can not turn into a null because it is struct and structs in C sharp are not nullable. And it becomes sort of a nice trick, to avoid, these null problems. Because if you want to make your return value, your user nullable, you have to wrap it with a maybe of user and you cannot do that otherwise because if you try to return null without that Maybe your method will throw an exception.

But if you, if you do use the Maybe, then your null will be automatically transformed into an instance of that Maybe type and your code will, will proceed.  The validation here is not as strict  as in functional programming languages because, this issue with the null it will not be caught at the compile time.

But still it's close enough because,  even though the compiler will see this code as valid, I mean the code where you return a user, but, return null instead, but it will still fail at runtime. So you will have sort of, close to functional guarantees. here as well.

**Jeremy:** [00:46:17] Sounds like it's similar to the result type in the sense that with the result type we were saying we would wrap an object in a result, and what that would do to the method signature is it would say that this function you're going to call it could succeed or it could fail.

And similarly, this Maybe type, it sounds like it's wrapping your object. It's wrapping your response and telling you that your response could have something in it or it could have nothing in it, and it's making it explicit as a part of the return type.

**Vladimir:** [00:46:48] Yes, exactly. So, the, the maybe type  it gives you the same benefits of the result type. So it makes the, method explicit. But in addition to that, if you use it, these Fodi null guard library, it also gives you some guarantees, some runtime guarantees that you will not actually have a null. Where you return a non Maybe user.

So if you return just user, then you have this guarantee that it will actually be a non-null instance. Because if you try to return null, then the application will throw an exception.

**Jeremy:** [00:47:21] Something that C# added recently in C# 8 is it added non nullable reference types. So it has a compiled type check,  to see if you could possibly be using something that's null, is that a good substitute for this Maybe type or kind of what are your thoughts on that feature?

**Vladimir:** [00:47:42] It's a nice move in to the right direction, but I don't think that it is a good enough substitute because those checks they will only give you compile warnings. So they are not compile errors, but that's not a big issue because you can turn those warnings into errors by setting up a couple of things in Visual Studio.

The main issue here is that, it doesn't catch all those situations where you may have nulls. And so you still may have some issues with nulls even though,  C# 8 will tell you that everything is fine. So that's basically my concern with that, that it's not as strict as they might be type.

**Jeremy:** [00:48:27] It kind of gives you some protection, but there are some cases it doesn't catch. So it may give you this false sense of security.

**Vladimir:** [00:48:36] Yes, exactly.

**Jeremy:** [00:48:37] Another thing that you bring up in some of your courses is that. When data is coming in from an outside source, like let's say, you have a API and somebody sends you data via JSON, or you get data via a message queue, you tend to create a separate DTO, a data transfer object rather than use the entities or the value types that you've created internally.

Why do you make the decision to do that?

**Vladimir:** [00:49:11] Yeah, that's a very important thing to do in my opinion, because, you need to maintain the separation between data contracts and your domain model. And this is important because if you are using the same domain classes,  and as, as these input data structures, then you may fall into several problems.

So let's say that you  you have a controller that is responsible for user creation and, one way to represent that data that clients send you when they try to register a new user. one way to do that would be to use the same user domain objects. Object as you have in the domain model.

So let's say that it has a username or password and maybe some other properties that map one-to-one to the properties that the client sent you. The issue here, the first issue here is the security hole, potential security hole. Because, you may introduce some properties in the future to your domain class that you don't want the client to set. So let's say that you introduce a flag saying that this user is an admin. let's say it's a boolean isAdmin flag. And if you introduce it to your domain model, then, it, it becomes a potential security problem because now your clients can send this flag as well, and it will be deserialized into that domain model.

And if you save it. as as-is into the database, then, you will basically create another admin in your system without knowing that. And so that's one another problem here is that. When you use your domain classes like that, you are setting those, domain classes in stone, so to speak, because you often need to maintain backwards compatibility with the clients.

And what it means is you cannot refactor those classes as often as you may need. So let's say that, for example, you,  your user has a name property and you want to split it into first name and last name. But because you want to maintain backwards compatibility, you can not just do that because the old clients of your application will break because they will not know that split they will not know about it and they will continue to send you just one name. And in this case, it becomes problematic because now you have to maintain sort of the old name property. But you also need to add the first name and the last name and then somehow correlated between the two maybe transform name into first and last name user using some rules.

And you don't want to do that. Instead, what you need to do is you need to have a separate layer of data contracts. DTO data transfer objects  where you have as many versions of those data contracts as you as you want. So if you decide to split the name into first and last names. You don't need to modify the old DTO.

You can create a new endpoint that accepts a new. DTO, version two, let's say, that we'll have the first and the last name, and then you will do the conversion between these two end points. So the first endpoint  that still has the first version of the DTO. You can do the conversion between your domain model and the old data structure there.

And so in this way, you are free to modify to refactor your domain model without looking back to  how how it makes incompatible or backward compatible changes for your clients. and so you, you sort of. Decouple that data contract from your internal domain model. You want the internal domain model to move as fast as you want, so you want to be able to refactor it, but you want to keep the data contracts backward compatible.

**Jeremy:** [00:53:06] It's almost like the difference between when you have a class, you have a public interface, and then you have the private implementation. And when you. Use data transfer objects, you expose an interface that you want to keep the same, but you want to be able to modify how that's handled internally in your system.

And so having these DTOs, it makes sure that you can make as many changes as you want internally in your system without affecting what your API looks like to the outside.

**Vladimir:** [00:53:41] Yes, exactly. It's a good analogy. Yes.

**Jeremy:** [00:53:43] The one thing I can think about as far as DTO is and converting them to internal domain objects. One of the things about that is it sounds like you could potentially have a lot of conversion code.  How should you sort of plan for that and where should that exist in your application?

**Vladimir:** [00:54:02] So, my view has evolved since that course. I think what I did is I created, extension methods on top of, result, and it's still a good way to do that. Let's say that, when you create a user, you need to validate, his first last name, let's say an email, and let's say a couple of other properties.

And what you can end up with is a lot of code that does validation. So you are creating a value object first, and then you need to make sure that the user with the same email doesn't exist in the database, and then you need to create another value object and validate it . And so it creates a lot of, if else statements that clutter your code base.

What you can do instead is you can follow the so-called railway oriented approach, which was introduced by Scott Wlaschin. and so what I did is I basically adopted this approach from F# to C#. and you can introduce extension methods that will drastically simplify all those if statements, It will help you to reduce the number of line codes by a factor of three, and without losing any readability. And for simple validations, it's still a good approach, but, there is a nice, way of dealing with validation in asp.net and that is validation attributes.

And what I did in that course, I said that validation attributes is nice, but they kind of don't play well with value objects. And so if you want to really adhere to domain driven design principles or functional principles, then you need to switch from those annotations to this railway oriented approach.

But you actually can combine the two. So you can combine the approach with annotations and still have this validation logic in Value Objects. So one of the biggest disadvantages of having those validations in annotations is that you are duplicating that validation. So you want to keep those validation rules inside your domain model because it is part of your domain model it is essential part of it. when you put let's say regular expression validation attributes on top of your DTOs you are duplicating those rules between the two parts of your system. So now you have a value object with the same rules and, and also, that same rule that exists in the data annotations.

So to combine the two, you can actually create your own custom annotations that would delegate,  those checks to the value objects, but still would work exactly the same way as the regular annotation attributes, meaning that you can declaratively put them on top of your DTO properties and they will work, very well.

So you will still reduce the, number of validation code lies lines drastically, but you will still keep this nice declarative approach that you had with annotations. And I have a blog post on my website, we can link it in show notes where I showed this approach in detail.

**Jeremy:** [00:57:25] Just to make sure I understand correctly, so what you're describing is in ASP.NET. When you have a model for  a DTO, you can put annotations on it. You can have your property and above the property, you could say something like, the max length is 50 so this person's name can't be more than 50 and what ASP.NET is able to do is if you were to create a form and  you used that property in the form, if somebody typed in a name and they put in 80 characters, ASP.NET, using that annotation would be able to automatically, sort of create an error and you would be able to put that next to the field. And I think what you're saying that you can do is that you can keep those sort of validation rules inside the domain objects that you create, or I think you called them the value object, and you're able to still write an annotation that just refers to the validation that exists in your value object rather than using the builtin, data annotations.

**Vladimir:** [00:58:37] Yes. Yes, exactly. And that's a nice way to combine the two because it sort of combines the best of the two worlds. You still have your validation rules in one place.

**Jeremy:** [00:58:48] What's your approach to, when you have a code base, that has exceptions and it passes back nulls  the calls to the database are sort of mixed in with the objects.

Like how do you start that process of bringing in more functional concepts or just bringing in more concepts that are easier to follow and to understand?

**Vladimir:** [00:59:09] Yeah, that's a great question. And yeah, it's a tough one it depends a lot on the specifics of that project on specifics of the team and the management. It's one thing if this project doesn't,  evolve much and it's just some project in the maintenance mode where you don't need to introduce a lot of new features in this case, I actually don't recommend that you do much because it will be, it will most likely will not pay off in the long run.

But if it is a project that is actively developed, then it's a different story, and in this case, you need to come up with some refactoring approach, some refactoring strategy, there are a couple of approaches here. In Domain Driven Design, for example, Eric Evans wrote a great piece where he talked about, so this approach that involves bubble contexts. And so a bubble context is something that you create inside a legacy code base that adheres to all the good principles. So you have a nice separation between the domain logic and the orchestration and your domain logic is ideally, purely functional and, because you, you cannot refactor the whole application at once.

And I actually don't recommend that you rewrite your application either because it's, it's not a good idea in most cases. You still want to start somewhere. And where you can start is by creating these bubble contexts. Let's say that you have some new feature or you need to modify an existing feature, and this feature is somewhat not too connected to the other system.

And so you can start to isolate this functionality into the bubble context and surround that bubble context with an anti-corruption layer and that anti-corruption layer, it's basically a repository that converts your good and clean domain model into the database with this messy legacy structure and converts back into your nice and clean domain model.

And what you can do is you can start expanding that bubble context. You can gain territory,  more and more with new features with new, refactorings. And eventually what you want to do is, come to this point where your bubble context becomes the main part of your application. And, it's the legacy part that is surrounded by the anti-corruption layer.

This pattern is also called a strangler pattern where you strangle, these legacy part, and cut off slices of functionality from that part and transform it and refactor them, into your bubble context.

You need to first define the building blocks of your domain model. And those building blocks are usually value objects. So the , easiest to create classes in your application, let's say as simple as an email value object or as simple as a customer name value object. And so, when you do that, you can put, domain logic that relates to those email and customer names to those value objects. start using these value objects from the rest of your system, and then, start, from there so you can build a hierarchy of objects. So let's say that you have another object that consist of, those smaller building blocks, smaller value objects. So you do that. And then, as I said previously, you can proceed to your entities and refactor that entity. So instead of separate properties on the entity, you can start to have, properties, defined as value objects. And so, you are attributing more and more logic from that entity to those value objects. And the entity itself becomes simpler. And then, from that level, you step even further and push the domain logic down from controllers to those entities. Because what you usually have in such legacy systems is the anemic domain model where your domain logic is separated from the domain data. So data is separate from the logic and that we can talk about it a bit too.

But the main drawback in this system is that it's hard to maintain encapsulation. It's hard to maintain consistency, inside. the domain data, because it's separated from the logic that works upon that data. and the logic itself is usually like in something like services. And so you can push that logic from services down to entities.

And so what you have it's sort of a cascade of a logic that you push further and further down. And the more down you can push it, the better because the easier it will be to work with. And the problem with the anemic domain model is that, well there is actually a nice, dichotomy between,  anemic domain models and functional programming because, anemic domain model it's about separating data from functions or from operations that work upon that data. But functional programming is kind of the same. So it's also about separating data from operations that work upon that data. The big difference between the two is that in functional programming though, the data is immutable and it is a big deal because it's impossible to corrupt immutable data. So it's basically impossible to come up with something that you cannot change. but anemic domain models, although they exhibit similar properties to the functional approach. The biggest,  difference is that it is mutable that data inside domain models is mutable and you can never know who mutates that data and how they do that. And so it becomes impossible to enforce restrictions on everyone whom mutated that data with, with such an environment.

**Jeremy:** [01:05:18] Given all the things we've talked about, if people want to kind of see an example of a lot of these things in action, are there any code bases that they can take a look at that are open source or any good examples that you can point them to?

**Vladimir:** [01:05:35] So, if we are talking about C-sharp, then I would recommend my Pluralsight course. it's called, applying functional principles in C or something like that. I actually have a trial code for Pluralsight side, so if you want just reach out to me. We can put my email address.

So they will give you a, I think it's 30 days, unlimited access to Pluralsight, so you can watch all my courses and more during that time. Also if we're talking to F#, I would highly recommend Scott Wlaschin's books on this topic. So he. Has a great site it's called F# for fun and profit, and it has a section with books in it where one of the books is basically the collection of them articles from the site itself.

But the other book is that it is about Domain Driven Design combined with the functional approach, and it's really great book. It, it explains how to do the Domain Driven Design in a functional programming language like F#.

**Jeremy:** [01:06:38] And, where should people go if they want to see more about what you're working on and follow you?

**Vladimir:** [01:06:45] The best place is to go to my website. It's called enterprise craftsmanship.com. And yeah, you will find all the links there.

**Jeremy:** [01:06:55] Cool. Well, Vladimir thank you so much for coming on the show.

**Vladimir:** [01:06:59] Thank you for having me. 

**Jeremy:** [01:07:00] I hope you enjoyed the conversation with Vlad. You can get the show notes and a transcript for this episode at softwaresessions.com.   Alright see ya.

</div>