+++
title = "Object Relational Mappers with Julie Lerman"

description = "Julie discusses the role of object relational mappers and their trade-offs, micro-ORMs, the rise of specialized databases, and Entity Framework"

[extra]
episode_url = "https://pinecast.com/listen/cff05b0f-3352-4976-bc8a-164e1f99f496.mp3"
social_title = "Object Relational Mappers"
social_description = "Julie discusses the role of object relational mappers and their trade-offs, micro-ORMs, the rise of specialized databases, and Entity Framework"
+++

[Julie](https://twitter.com/julielerman) is a software consultant with a focus on Domain Driven Design, a Pluralsight course author, and a Microsoft Regional Director.

Related Links:
- [@julielerman](https://twitter.com/julielerman)
- [The Data Farm (Julie's blog)](http://thedatafarm.com/)
- [Entity Framework](https://docs.microsoft.com/en-us/ef/)
- [Dapper](https://github.com/StackExchange/Dapper)
- [Automapper](https://automapper.org/)
- [Hibernate](https://hibernate.org/orm/)
- [NHibernate](https://nhibernate.info/)
- [Pluralsight Courses](https://app.pluralsight.com/profile/author/julie-lerman)

This episode originally aired on Software Engineering Radio.

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

**Jeremy:** [00:00:00] Today I'm talking to Julie Lerman. She's a frequent conference speaker, an independent consultant and a Pluralsight course author. Today we're going to talk about her experience working on ORMs and Entity Framework. 

Julie, welcome to software engineering radio.

**Julie:** [00:00:16] Hey, Jeremy. Thanks so much for having me.

**Jeremy:** [00:00:18] For those who aren't familiar with ORMs what are they and why do we need them?

**Julie:** [00:00:23] The first thing is the definition so ORM stands for object relational mapper. It's a software idea and implementation in many aspects for taking the concepts that we describe as classes and transforming them into the structure of a relational database. So you can get the data in and out easily.

So the ORM takes care of that mapping and the transformation. So you don't have to worry about writing SQL. You don't have to worry about getting structured results from a database that are in rows and columns and then transforming them back into object instances. So the ORMs do that for you.

**Jeremy:** [00:01:15] Some of the most popular languages used are object oriented. Why do we continue to store our data in a relational database when it's so different from our application code?

**Julie:** [00:01:26] There's certainly a lot of reasons for relational databases compared to document databases, object databases. Relational databases for their structure and normalization and tuning, and it's different kinds of storage needs I think than when you're storing documents. Sometimes I think more about getting the data back out. Finding data. 

It's one thing to be able to store it in a way that makes sense. But then when you need to pull data together and create relationships that aren't naturally in those documents unless you have prepared and designed something like a document database for every possible scenario.

There's also the whole concept of event sourcing where if you're just storing the events then you can actually re-persist that data in different structures so that it's easier for the various ways you might access it. Also, relational databases have been around for a long time and it's interesting that even with the popularity and extreme power of these other kinds of nonrelational databases, the NoSQL databases, relational databases are still, I can't say the source off the top of my head but I've used them in conference slides. They update their data monthly, but I can see these graphs where it shows that it was still about 70% of systems out there are using relational databases and in a lot of cases, so much legacy data, too, right. That's all going to be in relational databases.

**Jeremy:** [00:03:18] Relational databases, they give us the ability to request just the data we need that matches a certain condition or we can combine different parts of our data and get just a specific thing that we need.

If we were dealing with a bunch of arrays of objects or documents it might be harder to query for a specific thing does that sort of match...?

**Julie:** [00:03:45] Yeah, especially that unplanned data access and. Another interesting thing. And it's one of those things that I think you have to like, stop and think about it, to realize the truth in it, which is that most systems, most of the work you're doing the database is reading the database much more than creating  and storing data.

That's the bigger problem. Getting the data back out and having the flexibility to do weird things whereas something like a document database depending on how you split it up and keys and everything, it's just more designed. A relational database is a little easier to get at that weird stuff.

**Jeremy:** [00:04:37] You mentioned ad hoc queries. So with a relational database you can store all your information and then you can decide later what queries or information you want to get out, whereas you had hinted at with a document database you have to think upfront about what queries you want to make. Could you elaborate a little bit on that?

**Julie:** [00:05:02] I don't want to be generalizing too much, because there's all kinds of other factors that might come in especially when talking about huge amounts of data for like machine learning and things like that. There's pros and cons to both of them.

And like I mentioned with event sourcing ways to have your cake and eat it too. When I look for example at documentation for Azure CosmosDB, that's the document database that I have the most familiarity with. One of the most important documents is that upfront design and that design bleeds into how you're modeling your data in your application so that you can store it fluidly into the document database. So it's really, really important. Now I don't want to conflate this with the beauty of a system like document database, how that aligns so much more nicely for persistence.

And most of your getting data in and getting data out when we're talking about domain driven design. Where you don't want to worry about your persistence, just focus on the domain and then we can figure out how to get the data in and out right? We've got patterns for that.

But it is interesting if something like a document database more naturally aligns with your objects right? So that flows nicely in. However, it's still really important to be considerate of how you're breaking up that data in the way you store it. What your graphs are going to be. Maybe it's easy to get it in this way. But then what about when you're getting it out? What about different perspectives that you have? I want to be really careful about, comparing and contrasting the document DB versus relational DB. I want to stop at some level of that because there's always going to be debate and argument about that.

However one of the nice things about an ORM is it does take away some of that pain. That we normally would have when we're writing applications and writing that data access layer where we have to say, okay, I want this. Now I have to figure out the SQL statement, or call a stored procedure, or however I'm going to do it.

Whether I'm getting data in or getting data out and then I have to transform my objects into the SQL right? Or I get data back. And then I have to read through that data and instantiate objects and stuff, all the values into those objects. That's the stuff that the ORM can...

Repetitive. Like Bull (bleep). Right. Writing all that stuff. So that's what the ORMs do. I think the next big question that comes up then is yeah, but my SQL is always going to be better than some generic thing that an ORM is going to build for me. Right? The general advice for that is for many cases what the ORM doesthe performance will be just perfectly fine. And then there's going to be the cases where the performance isn't good. So then you can use your own stored procedures, use your views.

But a lot of the ORMs, certainly the one I focus on, which is Microsoft's Entity Framework, has the ability to also interact with stored procedures and views and do mappings to views and things like that. So people don't realize that, right. But maybe 80% of the SQL that entity framework is going to write whether it's for queries or for pushing data into the database. Maybe 80% of that is perfectly fine. And then 20% of that, do performance testing, go yeah. I can do better. I can do better and fix those up.

**Jeremy:** [00:09:27] I want to step back a little and walk through some of the features of ORMs that you had mentioned. Uh, one of them was not necessarily having to write SQL so you have some alternative query language that the ORM is providing. So what are some of the benefits of, that?

Like why would somebody not just jump straight to SQL and would instead use this SQL-like query language?

**Julie:** [00:09:57] well, Again, I'd have to kind of focus on .NET and I know you do a little bit of .NET programming so you probably are familiar with LINQ the query language that's built into .NET, into C-sharp and the .NET languages. It's a much, simpler expression than SQL, and it's much more code like and if you were writing a SQL string to put in to your application, we want to use stored procedures and views, but let's say you're just writing raw SQL, right? You're writing a string. And you're crossing your fingers that you got it right, right? That there's no typos, but also that you've written it correctly, but if you're using something like LINQ, which is part of the language, then you've got all the advantages of the language syntax and IntelliSense and here's my object what are my methods that are available all popping up. 

You don't have to worry about magic strings. I think that's really key and you don't have to know SQL concepts really. So with entity framework at the very beginning the team actually came out of Microsoft research. The team that had created that started with a SQL like language to do it. But then LINQ was also created at Microsoft by the C sharp team. And then, LINQ was originally created for objects. So you can use that for writing queries just across your objects. I wouldn't say LINQ was evolved, but a LINQ version that applied to entity framework was created.

And there was also LINQ to SQL which was a much lighter weight ORM that was also created within Microsoft, so you're using almost the same LINQ. A lot of things are shared some are more specific to entity framework. 

There's another benefit. I use LINQ for all kinds of things in my code, not just for the database interaction with Entity Framework, I use LINQ just when I'm working with arrays. Working with data in objects in memory. So I've also got this common syntax. I already know how to use it. There's just some special features of it that are specific to using entity framework.

So there's all kinds of benefits and the best benefit was it enabled me to essentially forget SQL. I forget how to write T-SQL. If I have to write raw T-SQL, I have to Google it after all these years of coding but I don't mind.

**Jeremy:** [00:12:39] With LINQ this was a query language that was already built into C# and also VB.NET. All of the languages that run on the .NET runtime, and so the developer may already be familiar with this query language. And they can apply it to making queries to a database rather than having to learn SQL which would be an entirely new language to the developer.

**Julie:** [00:13:19] Yes. And not just that, but I don't have to learn T-SQL (Microsoft SQL Server) and O-SQL (Oracle) and P-SQL (Postgres). There's all kinds of different database providers for entity framework. And the same for other ORMs. I feel a little bad just focusing on EF, but that's my area of expertise.

But the providers are the ones that do that transformation. So entity framework iterates over the query a few times and creates a query tree. And then the query tree is passed on to the provider, which then does the rest of the transformation into its particular SQL. So, I actually go back and forth between SQL server, SQLite and PostgreSQL. SQL server's what I'm most familiar with but I can use SQLite and Postgres and there's a lot of generic, common stuff right? 

So as a matter of fact the way LINQ for entity framework is built. That's just one thing and then the providers figure it out. So if you need something that's really specific to SQL server that doesn't work in Postgres or something in Postgres that doesn't work in SQLite there might be an extension that lets you tap into that particular thing. Or call a stored procedure. Except you wouldn't do that in SQLite because they don't have stored procedures. 

Interestingly tapping back to talking about document databases. There is a provider for Azure CosmosDB. So we've got an object, relational mapper. That maps to a non-relational database. So the reason that exists is because there was a lot of people that said I really am familiar with entity framework. I've been using it for years. We're going to be using CosmosDB. Can I just use that? So that exists.

And Azure has a SQL I'll just say SQL language for accessing but there's other APIs that are used also it's not all SQL, but because it has the SQL construct the providers kind of already know how to build SQL.

So it's just, we'll build the SQL that Azure works. So it's not solving the problem that we have with relational databases, which is that we've got this rows and columns structure and we need to do this translation all the time. The problem it was solving that provider is solving by linking entity framework and the document database is I already really know how to use entity framework.

And here I am just, I'm just doing some queries and persisting some data. Why do I have to learn a whole new API?

**Jeremy:** [00:16:27] You're saying that even with a document store, you might be able to use the same query language that's built into your ORM. With a relational database you have joins and things like that allow you to connect all your tables together and do all these different types of queries.

Whereas with a document database, I usually associate those with not having joins. Is that also the case with this document database that you're referring to with, with CosmosDB?

**Julie:** [00:17:02] I've written only tiny little minimal SQL for accessing it used to be called document DB, cosmos DB directly. I can't off the top of my head remember how that SQL works that out. If you've got to pull multiple documents together. I don't know, but what's nice is that in your code you don't have to worry about that stuff. Oh God, inner joins and outer joins and all like, Oh my God, I can't, I can't write that stuff anyway. So LINQ makes sense to me. I know it really well. So I don't have to worry about that.

**Jeremy:** [00:17:43] It sounds like at a high level, you get this query language that's built in to the language. Is more similar to the other code you would write. And you also get these compile time guarantees, auto-completion, what things you're allowed to call versus SQL, where, like you were saying, it's you have this giant string you hope that you got right. And don't really know until you query. So there's a lot of benefits with an ORM. You were also talking about how when you don't have an ORM you have to write your own mapping between after you've done your SQL query, you get some data that's in the form of just a set of records. And you have to convert those into your objects that are native to your application. And so basically the ORM is taking care of a lot of the you could say repetitive or busy work that you would normally have to do.

**Julie:** [00:18:47] To be fair, there are mappers. There are programs that are mappers or APIs that are mappers like auto mapper for .NET. So the connection string, like I don't have to worry about creating connections and all that kind of stuff, either with the ORM, but something like auto mapper, you can have a data model that really matches your database schema, and you can have a domain model that matches the business problem you're trying to solve. And then you can use something like auto mapper to say, okay, like here's what customer looks like in my application. Here's what customer looks like in this other data model. That's going to go to my data, but that map matches my database really easily.

And auto mapper let's you say this goes with this, this goes with that blah, blah, blah, blah, blah. So yeah. that stuff does exist. And, and there are also other lighter much... entity framework is a big thing. It does a lot. There are certainly lighter weight ORMs that they don't do as much, of that take away as much of that work.

However, if you need to squeak every little millisecond out of your performance, there's an open source ORM called dapper and it was built by the team that writes stack overflow because they definitely needed to squeak every millisecond of performance out of their data access. There was no question about that. 

So with dapper, it takes care of some of the stuff, some of that creating the connections and materializing objects for you, but you still write your own SQL because they needed to tightly control the SQL to make sure. Because it's more direct it doesn't have lots of things happening in between that entity framework does. And there's lots of dials in entity framework where you can impact how much work it's doing and how much resources it's using.

**Jeremy:** [00:21:09] So my understanding with, whether you would use entity framework versus one of these smaller ORMs, or more basic mapper is, it sounded like performance. And so it sounds like maybe you would default to using something like entity framework and then only dropping down to something like dapper, if you were having performance issues. Is, is that where your perspective comes from?

**Julie:** [00:21:41] Not sure if I would wait until I'm having performance issues. I think people sometimes will make that decision in advance, but an interesting plan of attack so that you can benefit from the simplicity of using entity framework. So you don't have to write the SQL, et cetera, is for example, using a CQRS pattern.

So you're separating the commands and the queries separating pushing data into the database and the queries. Cause it's usually the queries where you need to really, really focus on the performance and worry about the performance. Some people will use CQRS and let entity framework take care of all the writing and let dapper take care of all the readings.

So they're designing their application. So things are not, not the business logic, but the layer of the application that's taking care of the persistence. So designing it so that those are completely separate. So, Oh, I'm doing writing. So we're spinning up dapper and we're going to, or actually the other way around, I'm writing. So I'm going to spin up an entity framework context and say, go ahead and save changes or I'm doing a query and I'm writing my own SQL because I trust it. So now I'm going to spin up dapper and execute that SQL, let it create the create my objects for me.

**Jeremy:** [00:23:10] It sounds like it might be better to decide that up front figuring out, what is the amount of load I'm going to get in my application. What are the types of queries I'm going to be using for writing and reading data? And then from there, figuring out, should I use dapper? Should I use entity framework?

**Julie:** [00:23:35] Yeah, and there's some amount of testing and exploration, you would need to do proof of concept stuff. I think you might want to do first because I think entity framework query performance surprises people a lot. Like it's a lot better than people presume it's going to be. 

So yeah, I would definitely do some proof of concept before going that route cause it's certainly a lot easier to just use one thing all the way through.

However, if you've got things, applying separation of concerns and broken up, then it's not as traumatic to say for this bit... It is running a little slowly and, let's just use dapper. But if it's separated out, then it's easier to just say, yeah, let's just change over to that bit in our infrastructure.

**Jeremy:** [00:24:30] Are there workloads in a general sense that you would say that entity framework performs worse than others? For example, An app with a heavy write workload. Would that be an issue in entity framework? Are there examples of specific types of applications?

**Julie:** [00:24:52] I don't know if it's workload, compared more to structure you know schema. Um, or what it is you're trying to get at. you know, sometimes it's, how your model is designed, right? So there are just some places that any frameworks not going to, just not going to be able to do something as well as your own SQL. I had an example, this was years ago. So entity framework was not in its infancy, but it was like EF4 and I had a client who had gone down kind of a not great path of implementing entity framework in their software that's used across a big enterprise. They had created one big, huge model for everybody to use.

So that one model was responsible for no matter what you were doing, you had to use that model. Just pulling that model into memory was a lot of work for entity framework, but it created a lot of problems for the teams who were stuck using that. Because of the way they had set that up, they had this common query that would only return one piece, one row. They were looking for one row, but because of the way they had designed this model entity framework had to go through all kinds of hoops to create the SQL, to get at this one piece of data to, to write this query. And it was taking, it was in Oracle taking two minutes to execute. And they're like, what do we do? And I looked at it and I said, Just write a stored procedure. It's too late to change this model because everything's dependent on it.

So just write a stored procedure and the stored procedure took nine milliseconds. So like, okay we can pay you for the whole three days. You can go home now if you want, that was worth it.

**Jeremy:** [00:26:46] And so it sounds like that's not so much the choice of not using entity framework as it is-- you're still using entity framework, but you're using it to make a request to a stored procedure in the database. Similarly to how you could probably send raw SQL from entity framework.

**Julie:** [00:27:05] Yes. So you can still take advantage of that. So we're still using entity framework and saying, Hey, I don't want you to write the SQL, just execute this for me. And so that's still taking advantage of the fact that it knows it's SQL Server. It knows what the connection string is, et cetera.

It's not writing the query now there's we can take advantage of views in the same way and can actually map our objects to views and have it so we're still executing the view. And it's gonna still materialize the data for us, which is really nice.

**Jeremy:** [00:27:44] Yeah. So when you were talking about deciding whether or not to use entity framework, when you use entity framework, you could still be using a mix of the LINQ query language. Maybe raw SQL commands. Like you said, views, stored procedures. It's not this binary choice where you're saying, I'm going to write everything myself or I'm going to leave everything to Entity Framework.

**Julie:** [00:28:11] Absolutely. I mean that's the way we approach programming overall. Right? So I've got all of these wonderful arrows in my quiver to choose from. And, I'm not stuck with one. I just leverage using my knowledge and my experience. I'm making a decision, Hey, right tool for the job right. I guess that's what we've been saying for decades, not just programming, using the right tool for the job, but just because you want to use Entity Framework, doesn't mean you have to use it all the way through, but I think that's like, again using, using C# for this and maybe I'll use NodeJS or maybe I've got some really complex mathematical thing to do, for this particular thing I'll use F# or some other functional programming language.

**Jeremy:** [00:29:08] So we did a show back in 2007 about ORMs and I know that you've had a lot of experience both working with ORMs and probably working with applications without them just writing SQL directly. And so I would imagine there's been a lot of changes in the last decade, or maybe even couple decades.

What are some of the big things that you think have changed with ORMs in the last, 10 or 20 years?

**Julie:** [00:29:40] I think something we've been talking about, which is [that]NoSQL databases have reduced the need for ORMs right? Just slice that right off the top. There's so many scenarios where people don't need relational databases to solve that. So this is interesting, right? Because I'm not sure that the answer is. 

About what's happened with the ORMs... I think the answer is more what's evolved with the way we persist data and the way we perceive data. Machine learning, right? The idea of event sourcing, right? Talk about right tool for the job. Like here's my data, but for this scenario, it's going to be more effective and efficient for me if that data is stored in relational for this scenario, it'd be more effective if it's stored as documents, right? For this scenario, it'd be more effective if it's text, like just a text file. Oh, I forgot XML. Just kidding or JSON. Right? 

I think that's what's impacted ORMs [more] than the ORMs themselves. And entity framework is still going strong and evolving, and very, very wide use, in the .NET space. Some of the ones that were more popular are not really around anymore or haven't been updated in awhile. 

Dapper gets its love of course from the stack overflow team. So I really think it's more about the change in how we store data that's just reduced people's need for ORMs. But still whatever that resource was 70% of the applications are still using relational.

And then there's the people, like, no matter what, like we will never use an ORM. We will always write our own SQL. They have beautiful stored procedures and views and finely tuned databases. And they'll write the SQL for you these people. Just don't ask me to do it cause I'll probably never write SQL that's as good as entity framework with its algorithms and command trees can figure out on my behalf but there are plenty of database professionals who can definitely do that.

**Jeremy:** [00:32:37] For somebody who is working with a relational database and let's say they worked with entity framework or they worked with hibernate, or any number of ORMs a decade ago.. Is there anything that's changed where you would say, Hey, this is different. Maybe you should give this a second look?

**Julie:** [00:32:59] I apologize for not being able to speak to hibernate, like  how that has evolved, but when Entity Framework first came out and this was very different than NHibernate, the .NET version of hibernate, Entity framework did not have any appreciation or respect for our objects.

It was really designed from the perspective of storing relational data and it wasn't testable. It just didn't have any patterns. Interestingly, I spent a lot of time researching how entity framework aligns with good model design based on how we design domain driven design aggregates, and some of the, things that we put in place to protect our entities from people doing bad things with them. So Entity Framework at the beginning did not give us any way to do that. It didn't just lock your data access in to entity framework, the whole framework.

It locked your entire application in. All your entities and your classes had to be completely tied to entity framework in order for entity framework... Now that's all decoupled, right? So entity framework also we had this big visual modeler that in order to create the model, you had to start with an existing database.

Now it's like, look, here are my classes I don't want to design a database. I'm designing software. Right. I'm solving business problems. I have my domain model. So you build your domain model and then say, Hey, entity framework. Here's my domain model. Here's my database. Oh. And by the way, I know that by default, you're going to want this to go there and this to go there.

But I need to tell you there's a few things I want you to do a little differently. So we have all of that and we tell.. entity framework has nothing to do with our domain logic. So it's gotten better and better and more respectful of our code, our domain logic, and our domain business logic and code, and staying out of the way.

And that's been a big deal for me as somebody focused on domain driven design, which is. As I'm building my software I do not want to think about my data persistence, right. Has nothing to do with my domain. I like to joke unless I'm building the next Dropbox competitor right? So data persistence has nothing to do with my domain.

So I. Look to see how well as each iteration of entity framework comes out. I look and do some experiments and research to see how well it's defaults understand or map correctly, like get my data in and out of my database without me having to tweak Entity framework's mappings, but more importantly, without me having to do anything to my domain classes in order to satisfy entity framework and with each iteration it's gotten better and better and better, which is nice. 

Now, one bit of pushback I had in the early days when it was talking about entity framework and DDD was well, you're mapping your domain directly to the database using entity framework. You shouldn't do that. You should have a data model and map that, but what's interesting is entity framework becomes the data model, right? The mappings of the entity framework become the data model.

So I'm not doing it directly. That is the data model. So it is solving that problem. It's giving me that separation and there are still some design, some aggregate patterns that, entity framework, for example, won't satisfy in terms of the mappings, or maybe just some problems, some business problems or storage problems that you have. There are some times when it just makes sense to have something in-between even if the entity framework is still in-between that, like I have a specific data model, cause it just handles it differently. So you don't have to change how your, your domain I'm very passionate about that. Don't change the domain to make entity framework happy. Never, never, never, never.

**Jeremy:** [00:37:45] Could you give a specific example of before the objects you would have to create in order to satisfy entity framework? What were you putting into your objects that you didn't want to put in?

**Julie:** [00:38:01] That I didn't want to, I don't want to, well, one of the things that Entity Frameworks mappings could not handle is if you want it to completely isolate or encapsulate a collection in your entity. In your class, if you want to completely encapsulate the collection entity framework couldn't see it. Entity framework only understood for example, collections, but maybe you want to make it so that you can only iterate through it and enumerate through it. But if it was an IEnumerable, which is so that's what you would do, like in your class, you would say, Oh, I'm going to make it an IEnumerable so nobody can just add things to it and go around my business logic, which is, if you want to add something, I have to go over to this business logic to make sure all your invariants are satisfied or whatever else needs to happen.

So entity framework literally could not see that. And so, yeah. We struggled with, finding ways to work around that adding stuff, or just giving it up and saying, okay, I'm exposing this here, please. Don't ever use it that way please. But you know, you have to tell the whole team don't ever use it that way.

Right. But with Entity Framework Core 3 they changed that. So you can write your class the way you want to, and you can use the patterns that we use to encapsulate collections and protect them from abuse, misuse, and still entity framework is able to discover them and understand how to do all the work that it needs to do.

So that's just an example.

**Jeremy:** [00:39:50] What you wanted to do in your domain object is make this collection be an IEnumerable, which makes it so that the user of that class is not allowed to add items to it?

**Julie:** [00:40:03] Right. Developers using it. Add or remove

**Jeremy:** [00:40:08] right. Add or remove. And, uh, so you wanted to be able to control the API for the developers. Say that you want to receive this object and you can, you can see what's in it, but you can't add or remove from it.

**Julie:** [00:40:24] Well, you can, but not directly through that property. Right. You'd have to use a method that has the controls. I refer to it as a ADD DD ADD driven design, right? Because I am a control freak. I want to control how anybody's using my API.

**Jeremy:** [00:40:44] You wanted to control how people use the API, but if you did that within your object, then entity framework would look at that. IEnumerable and say, I don't know what this is, so I can't map this.

**Julie:** [00:40:56] It just completely ignores its existence.

So that was one evolution of Entity Framework that you can do that now. And all kinds of other things.

**Jeremy:** [00:41:09] Are there any other specific examples you can think of, of things that used to be either difficult to do or might frustrate people with entity framework [that] are addressed now?

**Julie:** [00:41:20] Along those same lines of encapsulating properties, right? So, and encapsulated collections was really, really hard. Like it wasn't hard. It was impossible. But if you want it to either encapsulate properties or not even expose properties, you didn't want to expose them all at all and you just wanted to have private fields.

You couldn't do anything like that either, but now with the, more modern, EF Core, you could literally have an object, a type defined with fields, no properties exposing those fields outside of the API. But you can still persist data. Entity framework is still aware of them or depending on how locked down, like if you made them totally private you'll have to tweak the configuration in Entity Framework, you have to tell Entity Framework, Hey, this field here, I want you to pay attention to it. Right. So there's some conventions where it will automatically recognize it. 

There are some ways of designing in your type that Entity Framework won't see it, but you can override that and tell entity framework about that. So I think that's a really interesting thing, because a lot of scenarios where people want to design their objects that way. And you know, again, just so much of that is about protecting your protecting your API from misuse or abuse but not putting the onus on the users of your API, right.

The API will let you do it. You're allowed to do and it won't let you do what you're not allowed to do.

**Jeremy:** [00:43:04] You had mentioned earlier another big difference is that it used to be, that you would create your database by writing SQL, and then you would point entity framework to that to generate your models?

**Julie:** [00:43:17] Oh, yes. The very first iteration, that was the only way it knew how to build a model. Oh, wait, there was a way to build the model, a data model in the designer. That's right. But then everything's dependent on that model or on the database instead of no, I want to write my domain logic and then, now Entity Framework. Not everybody has a brand new project, right. But say you get a brand brand new project and there is no existing database. So you can ask entity framework to generate the database based on the combination of its assumptions from reading your types. And extra configurations you add to entity framework and create the database.

So I hear all the DBAs going. Yeah. Oh no, no, no, no, no. That's not how it works. But this is the simple path. Like, so first you can have it create the database and then as you make changes to your domain Entity Framework has this whole migrations API that can figure out what has changed about your domain and then, figure out what SQL needs to be applied to the database in order to make those changes. So that's, that's one path. A twist on that path of course, is you can create that stuff. Instead of having those migrations, create the database or update the database, you can just have it create SQL and hand it to the professionals and say, this is sorta what I need.

If you can do this and then just make it the way you want it to be, just long as the mappings still work out. But the other way is if you do have a greenfield application and you do have a database already, you can reverse engineer, just like we did at the very beginning, but it's a little different.

But you can reverse engineer into a data model, which is, your classes. And a context, the entity framework configuration. So the classes are I refer to those as a stake in the ground. Because then you can just take those classes and make them what you want them to be. And then just make sure that you're still configuring the mapping so everything lines up. So there are two ways to go still, but at the beginning, There was this, I forgot even that the designer had, the entity data model designer had a way to design a model visually and then create both the database and the classes from it. But that, that went away really quickly.

So it was essentially point to the database, the whole huge database and create one whole huge data model from it. And that's how everything would work now.

A) we don't do that. And also we still don't have one big, huge data model. Right. Separation of concerns again. So we have a data model for this area of work and a data model for that area of work. And they might even point back to their own own databases. Right. And start talking about microservices and et cetera.

**Jeremy:** [00:46:35] Yeah. So if I understand correctly, it used to be where you would either use this GUI tool to build out your your entities or your database, or you would point entity framework at an existing database that already had tables and

**Julie:** [00:46:53] And all of that UI stuff is gone. Some third party, providers make some UI stuff, but as far as the entity framework is concerned, you know, Microsoft is concerned. We've got our classes and we've got our database. There's no UI in between.

**Jeremy:** [00:47:12] It sounds like the issue with that approach was that it would generate your domain models, generate your classes, but it would do it in a way that probably had a whole bunch of entity framework specific information in those classes? 

**Julie:** [00:47:30] In your classes. Yeah. So much dependencies in your classes. Now, none of that, they started moving away from that in the second version of the entity framework. Which was called EF4 not 2, but

it's cause it was aligning with .NET 4, but now we've now we've got EF Core, which came along with .NET Core, which is cross platform and lightweight and open source.

**Jeremy:** [00:48:00] So it sounds like we're moving in the direction from having these domain models. These classes have all this entity framework specific stuff to creating just basic or normal classes. Like the kind of code you would write if you weren't thinking about entity framework or weren't thinking about persistence specific issues.

And now with current ORMs, like entity framework core, those are able to map to your database, without, I guess the term could be polluting all your classes.

**Julie:** [00:48:38] And to be fair, entity framework was the evil doer at the beginning of entity framework. Right. hibernate didn't do that, nhibernate didn't do that. They totally respected your domain classes and it was completely separate. There was a big, well, I'll just say a big stink, made, by the people who had been using these kinds of practices already. And were using tools like hibernate and Entity Framework came around and said: Oh, here's the new ORM on the block from Microsoft. Everybody needs to use it. And they looked at, and they're like, But, but, but, you know, because entity framework was inserting itself into its logic into the domain classes.

And, the Entity Framework team got a lot of big lessons from the community that was really aware of that. And it wasn't right. I was, it was all new to me. I had never used an ORM before, so it was like, la di da, this is cool. This is nice. And you know, all these other people were like going, this is terrible. Why is Microsoft doing this? I don't understand. So eventually it evolved and I learned so much. I learned so much because of them. I mean, these are really smart people. I have a lot of respect for, so I was like, okay, they obviously know what they're talking about. So I gotta, I gotta figure that out. That's how I ended up on the path of learning about DDD. Thanks to them.

**Jeremy:** [00:50:09] So it sounds like there's been three versions of entity framework. There's the initial version that tried to mix in all these things into your domain models. Then there was the second version which you said was called entity framework 4 that, that fixed a lot of those issues. And then now we have Entity Framework Core.

I wonder if you could explain a little bit about. Why a third version was created. And what are the key differences

**Julie:** [00:50:40] Yeah. So this is, this was when Microsoft also at the same time, it had taken .NET Framework and rewritten it to be cross platform and open source and use modern software practices. And at the same time, the same thing was done with entity framework. They kept many of the same concepts, but they rewrote it because the code base was like 10 years old and also just in old thinking. 

So they rewrote it from scratch, keeping a lot of the same concepts. So people who were familiar, you know, who've been using Entity Framework they wouldn't be totally thrown for a loop. and so rewrote it with modern software practices, much more, open API in terms of flexibility and open source.

And because it was also part of .NET Core cross-platform. So that was huge. And then they've been building on top of that. So Entity Framework, the original Entity Framework. So I think it's interesting how you say there were three. So the first iteration of entity framework, and then this next one where they really, honored separation of concerns.

So that was EF4 through EF6 and then they kind of went to a new box with EF Core and served with the EF Core 1 and then 2 and 3 and, no 4. And now it's 5. So skipping a number again. So EF6 is still around because there's millions of applications that are using it. and they're not totally ignoring it.

As a matter of fact, they brought EF6 on top of .NET core. So EF6 is now cross-platform, but it's still in so many applications and they've been doing little tweaks to it, but EF Core is where all the work is going now.

**Jeremy:** [00:52:39] And it sounds like Core is not so much a dramatically different API for developers, but is rather an opportunity for them to clean up a lot of technical debt and, provide that cross platform capability, at least initially.

**Julie:** [00:52:57] And enable it to go forward and to do more, be able to achieve more, functionality that people have wanted, but was just literally wasn't possible with the earlier stack.

**Jeremy:** [00:53:12] Do you have any examples of a big thing that people had wanted for a while? They were finally able to do?

**Julie:** [00:53:19] And this is really, really specific now because this is about entity framework with the newest version, EF Core 5 that's coming out. One thing that people have been asking for since the beginning of EF time was when you're eager loading data. So there's a way of bringing related data back in one query.

There's actually two ways, but there's one way called a method called include. So including is so that you can bring back graphs of data instead of bringing, you know, go get the customers. Now, go get their orders. And now we need to merge them together in memory in our objects. So the include method says, please get me to customers and their orders and include, transforms that into like a join query or something like that brings back all of that different data and then builds the objects and make sure they're connected to each other in memory.

That's a really important thing to be able to do. The problem is because it was all or nothing, whatever relation, whatever related data you were. Okay. Bringing back in that include method, you would just get every single one. So, you know, if you said customer include their orders, there was no way to avoid getting every single one of their orders for the last 267 years.

**Jeremy:** [00:54:42] You're able to do an include, so you're able to join a customer to their orders, but in addition to that also have some kind of filter, like a where.

**Julie:** [00:54:52] On that child data, I'll say quote, you know, I'm doing air quotes, that child data, that related data. So we could never do that before. So we had to come up with other ways to do that.

**Jeremy:** [00:55:04] Yeah. So it was, it was possible before, but the way you did it was maybe complicated or convoluted.

**Julie:** [00:55:12] And it writes good SQL for it too, better than me. Maybe not better than, many of my really good DBA friends, but definitely better than I would.

**Jeremy:** [00:55:25] Probably be better than the majority of developers who know a little bit of SQL, but, uh, are definitely 

**Julie:** [00:55:33] Not DBAs yeah. I mean, that's one of the beauties of a good ORM, right?

**Jeremy:** [00:55:39] I guess it, it, um, doesn't quite get you to being a DBA, but it, um, levels the playing

**Julie:** [00:55:46] Well, I can hear my DBA friends cringing at that statement. So I will not agree with that. It doesn't level the playing field, but what it does is it enables many developers to write pretty decent SQL how's that how's that my DBA friends?

**Jeremy:** [00:56:10] I guess that's an interesting question in and of itself is that we're using these tools like ORMs that are generating all this code for us and we as a developer may not understand the intricacies of what it's doing and the SQL it's writing. So I wonder from your perspective, how much should developers know about the queries that are being generated and about SQL in general, when you're working with an ORM? 

**Julie:** [00:56:42] I think it's important. If you don't have access to a data professional it's important to at least understand how to profile and how to, recognize where performance could be better and then go seek a professional. But yeah, profiling is really important. So if you've got a team where you do have a DBA somebody who's really good with and understands they can be doing the profiling, right. Capturing it. And there's, you know, whether, if they're using SQL server, they might just want to use SQL server profiler there's all kinds of third party tools.

There's some capability built into visual studio. If you're using that, or there, there's all kinds of ways to profile, whether you're profiling the performance across the application, or you want to hone in on just the database activity, right? Because sometimes if say there's a performance problem, is it happening in the database? Is it happening in memory? Is entity framework trying to figure out the SQL? Is it happening in memory after the data has, you know, the database did it really fast? The data's back in memory now, entity framework is chugging along for some reason, having a hard time materializing all these objects and relationships.

So it's not just about not always about profiling the database. And there are tools that help with that also.

**Jeremy:** [00:58:18] You have the developers writing their queries in something like entity framework. And you have somebody who is more of an expert, like a DBA who can take a look at how are these things performing. And then if there are issues they can dive down into those queries, tell the developer, Hey, I think you should use a stored procedure here or a view.

**Julie:** [00:58:44] Yeah. Or even kind of expand on that. Unless you're solo or a tiny little shop, this is how you build teams. You've got QA people. You've got testers, you've got, data experts. You've got people who are good at solving certain problems. And everybody works together as a team. I'm such a Libra. Why can't we all get along?

**Jeremy:** [00:59:10] Yeah. And it sounds like it takes care of a lot of the maybe repetitive or tedious parts of the job, but it does not remove the need for, like you said, all of these different parts of your team, whether that's, the DBA who can look at the queries or maybe someone who is more experienced with profiling so they could see if object allocation from the ORM is a problem or all sorts of different, more specific, issues that they could dive into.

A lot of these things that an ORM does, you were saying it's about mapping between typically relational databases to objects and applications and something you hear people talk about sometimes is something called the object, relational impedance mismatch. And I wonder if you could explain a little bit about what people mean by that and whether you think that's a problem

**Julie:** [01:00:11] Well, that is exactly what ORMs are trying to solve, aiming to solve.  The mismatch is the mismatch between the rows and columns and your database schema and the shape of your objects. So that's what the mismatch is, and it's an impedance for getting your data in and out of your application.

So the ORMs are helping solve that problem instead of you having to solve it yourself by reading through your objects and transforming that into SQL, et cetera, et cetera, all those things we talked about earlier. I haven't heard that term in such a long time. That's so funny to me.

It's funny that, we talked about it a lot when, and like in the EF world, it was like, what's EF4 it's to take care of the impedance mismatch, duh. Okay. Yeah. We never said duh. Just kidding. But we talked about that a lot. At the beginning of entity framework's, history, and yeah, I haven't had anybody bring that up in a long time.

So I'm actually grateful you did.

**Jeremy:** [01:01:15] So maybe, we've gotten to. The point where the tools have gotten good enough where people aren't thinking so much about that problem because ideally entity framework has solved it?

**Julie:** [01:01:28] Entity framework and hibernate and dapper.

**Jeremy:** [01:01:32] I think that's a good place to wrap things up. If people want to learn more about what you're working on or about entity framework or check out your courses where should they head?

**Julie:** [01:01:46] Well, I spend a lot of time on Twitter and on Twitter. I'm Julie Lerman and I have a website and a blog. Although I have to say, I tweet a lot more than I blog these days. but my website is thedatafarm.com and I have a blog there and of course look me up on Pluralsight.

**Jeremy:** [01:02:08] Cool. Well, Julie, thank you so much

**Julie:** [01:02:11] Oh, it was great. Jeremy, and you asked so many interesting questions and also helped me take some nice trips into my entity framework past to remember some things that I had actually forgotten about. So that was interesting. Thanks.

**Jeremy:** [01:02:26] Hopefully... Hopefully good memories.

**Julie:** [01:02:28] All good. All good.

**Jeremy:** [01:02:31] All right, thanks a lot Julie.

**Julie:** [01:02:31] Yep. Thank you.

</div>