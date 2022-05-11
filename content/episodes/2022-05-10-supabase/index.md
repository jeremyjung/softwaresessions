+++
title = "Supabase"

description = "Ant Wilson shares what it's like to build Supabase"

[extra]
episode_url = "https://media.transistor.fm/033bcc78/587f963a.mp3"
+++

Ant Wilson is the co-founder and CTO of supabase.

We discuss the product and how it was built.

Thie episode originally aired on Software Engineering Radio.

### A few topics covered:
- Building on top of open source
- Forking their GoTrue dependency
- Relying on Postgres features like row level security
- Adding realtime support based on Postgres's write ahead log
- Generating an API layer based on the database schema with PostgREST
- Creating separate EC2 instances for each customer's database
- How Postgres could scale in the future
- Monitoring postgres
- Common support tickets
- Permissive open source licenses

### Related Links
- [@antwilson](https://www.twitter.com/antwilson)
- [Supabase](https://supabase.com/)
- [Supabase GitHub](https://github.com/supabase)
- [Firebase](https://firebase.google.com/)
- [Airtable](https://www.airtable.com/)
- [PostgREST](https://postgrest.org)
- [GoTrue](https://github.com/netlify/gotrue)
- [Elixir](https://elixir-lang.org/)
- [Prometheus](https://prometheus.io/)
- [VictoriaMetrics](https://victoriametrics.com/)
- [Logflare](https://logflare.app/)
- [BigQuery](https://cloud.google.com/bigquery)
- [Netlify](https://www.netlify.com/)
- [Y Combinator](https://www.ycombinator.com/)

### Postgres
- [PostgreSQL](https://www.postgresql.org/)
- [Write-Ahead Logging](https://www.postgresql.org/docs/current/wal-intro.html)
- [Row Security Policies](https://www.postgresql.org/docs/current/ddl-rowsecurity.html)
- [pg_stat_statements](https://www.postgresql.org/docs/current/pgstatstatements.html)
- [pgAdmin](https://www.pgadmin.org/)
- [PostGIS](https://postgis.net/)
- [Amazon Aurora](https://aws.amazon.com/rds/aurora/)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** Today I'm talking to Ant Wilson, he's the co-founder and CTO of Supabase. Ant welcome to software engineering radio.

[00:00:07] **Ant:** Thanks so much. Great to be here. 

[00:00:09] **Jeremy:** When I hear about Supabase, I always hear about it in relation to two other products. The first is Postgres, which is a open source relational database. And second is Firebase, which is a backend as a service product from Google cloud that provides a no SQL data store.

It provides authentication and authorization. It has a functions as a service component. It's really meant to be a replacement for you needing to have your own server, create your own backend. You can have that all be done from Firebase. I think a good place for us to start would be walking us through what supabase is and how it relates to those two products.

[00:00:55] **Ant:** Yeah. So, so we brand ourselves as the open source Firebase alternative

that came primarily from the fact that we ourselves do use the, as the alternative to Firebase. So, so my co-founder Paul in his previous startup was using fire store. And as they started to scale, they hit certain limitations, technical scaling limitations and he'd always been a huge Postgres fan.

So we swapped it out for Postgres and then just started plugging in. The bits that we're missing, like the real-time streams. Um, He used the tool called PostgREST with a T for the, for the CRUD APIs. And so

he just built like the open source Firebase alternative on Postgres, And that's kind of where the tagline came from.

But the main difference obviously is that it's relational database and not a no SQL database which means that it's not actually a drop-in replacement. But it does mean that it kind of opens the door to a lot more functionality actually. Um, Which, which is hopefully an advantage for us. 

[00:02:03] **Jeremy:** it's a, a hosted form of Postgres. So you mentioned that Firebase is, is different. It's uh NoSQL. People are putting in their, their JSON objects and things like that. So when people are working with Supabase is the experience of, is it just, I'm connecting to a Postgres database I'm writing SQL.

And in that regard, it's kind of not really similar to Firebase at all. Is that, is that kind of right?

[00:02:31] **Ant:** Yeah, I mean, the other thing, the other important thing to notice that you can communicate with Supabase directly from the client, which is what people love about fire base. You just like put the credentials on the client and you write some security rules, and then you just start sending your data. Obviously with supabase, you do need to create your schema because it's relational.

But apart from that, the experience of client side development is very much the same or very similar the interface, obviously the API is a little bit different. But, but it's similar in that regard. But I, I think, like I said, we're moving, we are just a database company actually. And the tagline, just explained really, well, kind of the concept of, of what it is like a backend as a service. It has the real-time streams. It has the auth layer. It has the also generated APIs. So I don't know how long we'll stick with the tagline. I think we'll probably outgrow it at some point. Um, But it does do a good job of communicating roughly what the service is.

[00:03:39] **Jeremy:** So when we talk about it being similar to Firebase, the part that's similar to fire base is that you could be a person building the front end part of the website, and you don't need to necessarily have a backend application because all of that could talk to supabase and supabase can handle the authentication, the real-time notifications all those sorts of things, similar to Firebase, where we're basically you only need to write the front end part, and then you have to know how to, to set up super base in this case.

[00:04:14] **Ant:** Yeah, exactly. And some of the other, like we took w we love fire based, by the way. We're not building an alternative to try and destroy it. It's kind of like, we're just building the SQL alternative and we take a lot of inspiration from it. And the other thing we love is that you can administer your database from the browser.

So you go into Firebase and you have the, you can see the object tree, and when you're in development, you can edit some of the documents in real time. And, and so we took that experience and effectively built like a spreadsheet view inside of our dashboard. And also obviously have a SQL editor in there as well.

And trying to, create this, this like a similar developer experience, because that's where Firebase just excels is. The DX is incredible. And so we, we take a lot of inspiration from it in, in those respects.

[00:05:08] **Jeremy:** and to to make it clear to our listeners as well. When you talk about this interface, that's kind of like a spreadsheet and things like that. I suppose it's similar to somebody opening up pgAdmin, I suppose, and going in and editing the rows. But, but maybe you've got like another layer on top that just makes it a little more user-friendly a little bit more like something you would get from Firebase, I guess.

[00:05:33] **Ant:** Yeah.

And, you know, we, we take a lot of inspiration from pgAdmin. PG admin is also open source. So I think we we've contributed a few things and, or trying to upstream a few things into PG admin. The other thing that we took a lot of inspiration from for the table editor, what we call it is airtable.

And because airtable is effectively. a a relational database and that you can just come in and, you know, click to add your columns, click to add a new table. And so we just want to reproduce that experience again, backed up by a full Postgres dedicated database. 

[00:06:13] **Jeremy:** so when you're working with a Postgres database, normally you need some kind of layer in front of it, right? That the person can't open up their website and connect directly to Postgres from their browser. And you mentioned PostgREST before. I wonder if you could explain a little bit about what that is and how it works.

[00:06:34] **Ant:** Yeah, definitely. so yeah, PostgREST has been around for a while. Um, It's basically an, a server that you connect to, to your Postgres database and it introspects your schemas and generates an API for you based on the table names, the column names. And then you can basically then communicate with your Postgres database via this restful API.

So you can do pretty much, most of the filtering operations that you can do in SQL um, uh, equality filters. You can even do full text search over the API. So it just means that whenever you obviously add a new table or a new schema or a new column the API just updates instantly. So you, you don't have to worry about writing that, that middle layer which is, was always the drag right.

When, what have you started a new project. It's like, okay, I've got my schema, I've got my client. Now I have to do all the connecting code in the middle of which is kind of, yeah, no, no developers should need to write that layer in 2022.

[00:07:46] **Jeremy:** so this the layer you're referring to, when I think of a traditional. Web application. I think of having to write routes controllers and, and create this, this sort of structure where I know all the tables in my database, but the controllers I create may not map one to one with those tables. And so you mentioned a little bit about how PostgREST looks at the schema and starts to build an API automatically.

And I wonder if you could explain a little bit about how it does those mappings or if you're writing those yourself. 

[00:08:21] **Ant:** Yeah, it basically does them automatically by default, it will, you know, map every table, every column. When you want to start restricting things. Well, there's two, there's two parts to this. There's one thing which I'm sure we'll get into, which is how is this secure since you are communicating direct from the client.

But the other part is what you mentioned giving like a reduced view of a particular date, bit of data. And for that, we just use Postgres views. So you define a view which might be, you know it might have joins across a couple of different tables or it might just be a limited set of columns on one of your tables. And then you can choose to just expose that view. 

[00:09:05] **Jeremy:** so it sounds like when you would typically create a controller and create a route. Instead you create a view within your Postgres database and then PostgREST can take that view and create an end point for it, map it to that.

[00:09:21] **Ant:** Yeah, exactly (laughs) . 

[00:09:24] **Jeremy:** And, and PostgREST is an open source project. Right. I wonder if you could talk a little bit about sort of what its its history was. How did you come to choose it? 

[00:09:37] **Ant:** Yeah.

I think, I think Paul probably read about it on hacker news at some point. Anytime it appears on hacker news, it just gets voted to the front page because it's, it's So awesome. And we, we got connected to the maintainer, Steve Chavez. At some point I think he just took an interest in, or we took an interest in Postgres and we kind of got acquainted.

And then we found out that, you know, Steve was open to work and this kind of like probably shaped a lot of the way we think about building out supabase as a project and as a company in that we then decided to employ Steve full time, but just to work on PostgREST because it's obviously a huge benefit for us.

We're very reliant on it. We want it to succeed because it helps our business. And then as we started to add the other components, we decided that we would then always look for existing tools, existing opensource projects that exist before we decided to build something from scratch. So as we're starting to try and replicate the features of Firebase we would and auth is a great example.

We did a full audit of what are all the authorization, authentication, authentication open-source tools that are out there and which one was, if any, would fit best. And we found, and Netlify had built a library called gotrue written in go, which did pretty much exactly what we needed. So we just adopted that.

And now obviously, you know, we, we just have a lot of people on the team contributing to, to gotrue as well.

[00:11:17] **Jeremy:** you touched on this a little bit earlier. Normally when you connect to a Postgres database your user has permission to, to basically everything I guess, by default, anyways. And so. So, how does that work? Where when you want to restrict people's permissions, make sure they only get to see records they're allowed to see how has that all configured in PostgREST and what's happening behind the scenes?

[00:11:44] **Ant:** Yeah, we, the great thing about Postgres is it's got this concept of row level security, which actually, I don't think I even rarely looked at until we were building out this auth feature where the security rules live in your database as SQL. So you do like a create policy query, and you say anytime someone tries to select or insert or update apply this policy.

And then how it all fits together is our auth server go true. Someone will basically make a request to sign in or sign up with email and password, and we create that user inside the, database. They get issued a URL. And they get issued a JSON, web token, a JWT, and which, you know, when they, when they have it on the, client side, proves that they are this, you, you ID, they have access to this data.

Then when they make a request via PostgREST, they send the JWT in the authorization header. Then Postgres will pull out that JWT check the sub claim, which is the UID and compare it to any rows in the database, according to the policy that you wrote. So, so the most basic one is you say in order to, to access this row, it must have a column you UID and it must match whatever is in the JWT.

So we basically push the authorization down into the database which actually has, you know, a lot of other benefits in that as you write new clients, You don't need to have, have it live, you know, on an API layer on the client. It's kind of just, everything is managed from the database.

[00:13:33] **Jeremy:** So the, the, you, you ID, you mentioned that represents the user, correct. 

[00:13:39] **Ant:** Yeah. 

[00:13:41] **Jeremy:** Is that, does that map to a user in post graphs or is there some other way that you're mapping those permissions?

[00:13:50] **Ant:** Yeah. When, so when you connect go true, which is the auth server to your Postgres database for the first time, it installs its own schema. So you'll have an auth schema and inside will be all start users with a list of the users. It'll have a uh, auth dot tokens which will store all the access tokens that it's issued.

So, and one of the columns on the auth start user's table will be UUID, and then whenever you write application specific schemers, you can just join a, do a foreign key relation to the author users table. So, so it all gets into schema design and and hopefully we do a good job of having some good education content in the docs as well.

Because one of the things we struggled with from the start was how much do we abstract away from SQL away from Postgres and how much do we educate? And we actually landed on the educate sides because I mean, once you start learning about Postgres, it becomes kind of a superpower for you as a developer.

So we'd much rather. Have people discover us because we're a firebase alternatives frontend devs then we help them with things like schema design landing about row level security. Because ultimately like every, if you try and abstract that stuff it gets kind of crappy. And maybe not such a great experience. 

[00:15:20] **Jeremy:** to make sure I understand correctly. So you have GoTrue, which is uh, a Netlify open-source project that GoTrue project creates some tables in your, your database that has like, you've mentioned the tokens, the, the different users. Somebody makes a request to GoTrue. Like here's my username, my password go true.

Gives them back a JWT. And then from your front end, you send that JWT to the PostgREST endpoint. And from that JWT, it's able to know which user you are and then uses postgres' built in a row level security to figure out which rows you're, you're allowed to bring back. Did I, did I get that right?

[00:16:07] **Ant:** That is pretty much exactly how it works. And it's impressive that you garnered that without looking at a single diagram (laughs) But yeah, and, and, and obviously we, we provide a client library supabase JS, which actually does a lot of this work for you. So you don't need to manually attach the JJ JWT in a header.

If you've authenticated with supabase JS, then every request sent to PostgREST. After that point, the header will just be attached automatically, and you'll be in a session as that user. 

[00:16:43] **Jeremy:** and, and the users that we're talking about when we talk about Postgres' row level security. Are those actual users in PostgreSQL. Like if I was to log in with psql, I could actually log in with those users.

[00:17:00] **Ant:** They're not, you could potentially structure it that way. But it would be more advanced it's it's basically just users in, in the auth.users table, the way, the way it's currently done. 

[00:17:12] **Jeremy:** I see and postgrest has the, that row level security is able to work with that table. You, you don't need to have actual Postgres users.

[00:17:23] **Ant:** Exactly. And, and it's, it's basically turing complete. I mean, you can write extremely complex auth policies. You can say, you know, only give access to this particular admin group on a Thursday afternoon between six and 8:00 PM. You can get really, yeah. really as fancy as you want. 

[00:17:44] **Jeremy:** Is that all written in SQL or are there other languages they allow you to use?

[00:17:50] **Ant:** Yeah. It's the default is plain SQL. Within Postgres itself, you can use

I think you can use, like there's a Python extension. There's a JavaScript extension, which is a, I think it's a subsets of, of JavaScripts. I mean, this is the thing with Postgres, it's super extensible and people have probably got all kinds of interpreters.

So you, yeah, you can use whatever you want, but the typical user will just use SQL. 

[00:18:17] **Jeremy:** interesting. And that applies to logic in general, I suppose, where if you were writing a rails application, you might write Ruby. Um, If you're writing a node application, you write JavaScript, but you're, you're saying in a lot of cases with PostgREST, you're actually able to do what you want to do, whether that's serialization or mapping objects, do that all through SQL.

[00:18:44] **Ant:** Yeah, exactly, exactly. And then obviously like there's a lot of awesome other stuff that Postgres has like this postGIS, which if you're doing geo, if you've got like a geo application, it'll load it up with a geo types for you, which you can just use. If you're doing like encryption and decryption, we just added PG libsodium, which is a new and awesome cryptography extension.

And so you can use all of these, these all add like functions, like SQL functions which you can kind of use in, in any parts of the logic or in the role level policies. Yeah.

[00:19:22] **Jeremy:** and something I thought was a little unique about PostgREST is that I believe it's written in Haskell. Is that right?

[00:19:29] **Ant:** Yeah, exactly. And it makes it fairly inaccessible to me as a result. But the good thing is it's got a thriving community of its own and, you know, people who on there's people who contribute probably because it's written in haskell. And it's, it's just a really awesome project and it's an excuse to, to contribute to it.

But yeah. I, I think I did probably the intro course, like many people and beyond that, it's just, yeah, kind of inaccessible to me. 

[00:19:59] **Jeremy:** yeah, I suppose that's the trade-off right. Is you have a, a really passionate community about like people who really want to use Haskell and then you've got the, the, I guess the group like yourselves that looks at it and goes, oh, I don't, I don't know about this.

[00:20:13] **Ant:** I would, I would love to have the time to, to invest in uh, but not practical right now. 

[00:20:21] **Jeremy:** You talked a little bit about the GoTrue project from Netlify. I think I saw on one of your blog posts that you actually forked it. Can you sort of explain the reasoning behind doing that?

[00:20:34] **Ant:** Yeah, initially it was because we were trying to move extremely fast. So, so we did Y Combinator in 2020. And when you do Y Combinator, you get like a part, a group partner, they call it one of the, the partners from YC and they add a huge amount of external pressure to move very quickly. And, and our biggest feature that we are working on in that period was auth.

And we just kept getting the question of like, when are you going to ship auth? You know, and every single week we'd be like, we're working on it, we're working on it. And um, and one of the ways we could do it was we just had to iterate extremely quickly and we didn't rarely have the time to, to upstream things correctly.

And actually like the way we use it in our stack is slightly differently. They connected to MySQL, we connected to Postgres. So we had to make some structural changes to do that. And the dream would be now that we, we spend some time upstream and a lot of the changes. And hopefully we do get around to that.

But the, yeah, the pace at which we've had to move over the last uh, year and a half has been kind of scary and, and that's the main reason, but you know, hopefully now we're a little bit more established. We can hire some more people to, to just focus on, go true and, and bringing the two folks back together. 

[00:22:01] **Jeremy:** it's just a matter of, like you said speed, I suppose, because the PostgREST you, you chose to continue working off of the existing open source project, right? 

[00:22:15] **Ant:** Yeah, exactly. Exactly. And I think the other thing is it's not a major part of Netlify's business, as I understand it. I think if it was and if both companies had more resource behind it, it would make sense to obviously focus on on the single codebase but I think both companies don't contribute as much resource as as we would like to, but um, but it's, it's for me, it's, it's one of my favorite parts of the stack to work on because it's written in go and I kind of enjoy how that it all fits together.

So Yeah. I, I like to dive in there. 

[00:22:55] **Jeremy:** w w what about go, or what about how it's structured? Do you particularly enjoy about the, that part of the project?

[00:23:02] **Ant:** I think it's so I actually learned learned go through, gotrue and I'm, I have like a Python and C plus plus background And I hate the fact that I don't get to use Python and C plus posts rarely in my day to day job. It's obviously a lot of type script. And then when we inherited this code base, it was kind of, as I was picking it up I, it just reminded me a lot of, you know, a lot of the things I loved about Python and C plus plus, and, and the tooling around it as well. I just found to be exceptional. So, you know, you just do like a small amounts of conflig. Uh config, And it makes it very difficult to, to write bad code, if that makes sense.

So the compiler will just, boot you back if you try and do something silly which isn't necessarily the case with, with JavaScript. I think TypeScript is a little bit better now, but Yeah, I just, it just reminded me a lot of my Python and C days.

[00:24:01] **Jeremy:** Yeah, I'm not too familiar with go, but my understanding is that there's, there's a formatter that's a part of the language, so there's kind of a consistency there. And then the language itself tries to get people to, to build things in the same way, or maybe have simpler ways of building things. Um, I don't, I don't know.

Maybe that's part of the appeal.

[00:24:25] **Ant:** Yeah, exactly. And the package manager as well is great. It just does a lot of the importing automatically. and makes sure like all the declarations at the top are formatted correctly and, and are definitely there. So Yeah. just all of that tool chain is just really easy to pick up.

[00:24:46] **Jeremy:** Yeah. And I, and I think compiled languages as well, when you have the static type checking. By the compiler, you know, not having things blow up and run time. That's, that's just such a big relief, at least for me in a lot of cases,

[00:25:00] **Ant:** And I just loved the dopamine hits of when you compile something on it actually compiles this. I lose that with, with working with JavaScript. 

[00:25:11] **Jeremy:** for sure. One of the topics you mentioned earlier was how super base provides real-time database updates. And which is something that as far as I know is not natively a part of Postgres. So I wonder if you could explain a little bit about how that works and how that came about.

[00:25:31] **Ant:** Yeah. So, So Postgres, when you add replication databases the way it does is it writes everything to this thing called the write ahead log, which is basically all the changes that uh, have, are going to be applied to, to the database. And when you connect to like a replication database. It basically streams that log across.

And that's how the replica knows what, what changes to, to add. So we wrote a server, which basically pretends to be a Postgres rep, replica receives the right ahead log encodes it into JSON. And then you can subscribe to that server over web sockets. And so you can choose whether to subscribe, to changes on a particular schema or a particular table or particular columns, and even do equality matches on rows and things like this.

And then we recently added the role level security policies to the real-time stream as well. So that was something that took us a while to, cause it was probably one of the largest technical challenges we've faced. But now that it's in the real-time stream is, is fully secure and you can apply these, these same policies that you apply over the CRUD API as well.

[00:26:48] **Jeremy:** So for that part, did you have to look into the internals of Postgres and how it did its row level security and try to duplicate that in your own code?

[00:26:59] **Ant:** Yeah, pretty much. I mean it's yeah, it's fairly complex and there's a guy on our team who, well, for him, it didn't seem as complex, let's say (laughs) , but yeah, that's pretty much it it's just a lot of it's effectively a SQL um, a Postgres extension itself, uh which in-in interprets those policies and applies them to, to the, to the, the right ahead log.

[00:27:26] **Jeremy:** and this piece that you wrote, that's listening to the right ahead log. what was it written in and, and how did you choose that, that language or that stack?

[00:27:36] **Ant:** Yeah. That's written in the Elixir framework which is based on Erlang very horizontally scalable. So any applications that you write in Elixir can kind of just scale horizontally the message passing and, you know, go into the billions and it's no problem. So it just seemed like a sensible choice for this type of application where you don't know.

How large the wall is going to be. So it could just be like a few changes per second. It could be a million changes per second, then you need to be able to scale out. And I think Paul who's my co-founder originally, he wrote the first version of it and I think he wrote it as an excuse to learn Elixir, which is how, a lot of probably how PostgREST ended up being Haskell, I imagine.

But uh, but it's meant that the Elixir community is still like relatively small. But it's a group of like very passionate and very um, highly skilled developers. So when we hire from that pool everyone who comes on board is just like, yeah, just, just really good and really enjoy is working with Elixir.

So it's been a good source of a good source for hires as well. Just, just using those tools. 

[00:28:53] **Jeremy:** with a feature like this, I'm assuming it's where somebody goes to their website. They make a web socket connection to your application and they receive the updates that way. How have you seen how far you're able to push that in terms of connections, in terms of throughput, things like that?

[00:29:12] **Ant:** Yeah, I don't actually have the numbers at hand. But we have, yeah, we have a team focused on obviously maximizing that but yeah, I don't I don't don't have those numbers right now. 

[00:29:24] **Jeremy:** one of the last things you've you've got on your website is a storage project or a storage product, I should say. And I believe it's written in TypeScript, so I was curious, we've got PostGrest, which is in Haskell. We've got go true and go. Uh, We've got the real-time database part in elixir.

And so with storage, how did we finally get to TypeScript?

[00:29:50] **Ant:** (Laughs) Well, the policy we kind of landed on was best tool for the job. Again, the good thing about being an open source is we're not resource constrained by the number of people who are in our team. It's by the number of people who are in the community and I'm willing to contribute. And so for that, I think one of the guys just went through a few different options that we could have went with, go just to keep it in line with a couple of the other APIs.

But we just decided, you know, a lot of people well, everyone in the team like TypeScript is kind of just a given. And, and again, it was kind of down to speed, like what's the fastest uh we can get this up and running. And I think if we use TypeScript, it was, it was the best solution there. But yeah, but we just always go with whatever is best.

Um, We don't worry too much uh, about, you know, the resources we have because the open source community has just been so great in helping us build supabase. And building supabase is like building like five companies at the same time actually, because each of these vertical stacks could be its own startup, like the auth stack And the storage layer, and all of this stuff.

And you know, each has, it does have its own dedicated team. So yeah. So we're not too worried about the variation in languages.

[00:31:13] **Jeremy:** And the storage layer is this basically a wrapper around S3 or like what is that product doing?

[00:31:21] **Ant:** Yeah, exactly. It's it's wraparound as three. It, it would also work with all of the S3 compatible storage systems. There's a few Backblaze and a few others. So if you wanted to self host and use one of those alternatives, you could, we just have everything in our own S3 booklets inside of AWS.

And then the other awesome thing about the storage system is that because we store the metadata inside of Postgres. So basically the object tree of what buckets and folders and files are there. You can write your role level policies against the object tree. So you can say this, this user should only access this folder and it's, and it's children which was kind of. Kind of an accident. We just landed on that. But it's one of my favorite things now about writing applications and supervisors is the rollover policies kind of work everywhere.

[00:32:21] **Jeremy:** Yeah, it's interesting. It sounds like everything. Whether it's the storage or the authentication it's all comes back to postgres, right? At all. It's using the row level security. It's using everything that you put into the tables there, and everything's just kind of digging into that to get what it needs.

[00:32:42] **Ant:** Yeah. And that's why I say we are a database company. We are a Postgres company. We're all in on postgres. We got asked in the early days. Oh, well, would you also make it my SQL compatible compatible with something else? And, but the amounts. Features Postgres has, if we just like continue to leverage them then it, it just makes the stack way more powerful than if we try to you know, go thin across multiple different databases.

[00:33:16] **Jeremy:** And so that, that kind of brings me to, you mentioned how your Postgres companies, so when somebody signs up for supabase they create their first instance. What's what's happening behind the scenes. Are you creating a Postgres instance for them in a container, for example, how do you size it? That sort of thing.

[00:33:37] **Ant:** Yeah. So it's basically just easy to under the hood for us we, we have plans eventually to be multi-cloud. But again, going down to the speed of execution that the. The fastest way was to just spin up a dedicated instance, a dedicated Postgres instance per user on EC2. We do also package all of the API APIs together in a second EC2 instance.

But we're starting to break those out into clustered services. So for example, you know, not every user will use the storage API, so it doesn't make sense to Rooney for every user regardless. So we've, we've made that multitenant, the application code, and now we just run a huge global cluster which people connect through to access the S3 bucket.

Basically and we're gonna, we have plans to do that for the other services as well. So right now it's you got two EC2 instances. But over time it will be just the Postgres instance and, and we wanted. Give everyone a dedicated instance, because there's nothing worse than sharing database resource with all the users, especially when you don't know how heavily they're going to use it, whether they're going to be bursty.

So I think one of the things we just said from the start is everyone gets a Postgres instance and you get access to it as well. You can use your Postgres connection string to, to log in from the command line and kind of do whatever you want. It's yours.

[00:35:12] **Jeremy:** so did it, did I get it right? That when I sign up, I create a super base account. You're actually creating an two instance for me specifically. So it's like every customer gets their, their own isolated it's their own CPU, their own Ram, that sort of thing.

[00:35:29] **Ant:** Yeah, exactly, exactly. And, and the way the. We've set up the monitoring as well, is that we can expose basically all of that to you in the dashboard as well. so you can, you have some control over like the resource you want to use. If you want to a more powerful instance, we can do that. A lot of that stuff is automated.

So if someone scales beyond the allocated disk size, the disk will automatically scale up by 50% each time. And we're working on automating a bunch of these, these other things as well.

[00:36:03] **Jeremy:** so is it, is it where, when you first create the account, you might create, for example, a micro instance, and then you have internal monitoring tools that see, oh, the CPU is getting heady hit pretty hard. So we need to migrate this person to a bigger instance, that kind of thing.

[00:36:22] **Ant:** Yeah, pretty much exactly. 

[00:36:25] **Jeremy:** And is that, is that something that the user would even see or is it the case of where you send them an email and go like, Hey, we notice you're hitting the limits here. Here's what's going to happen. 

[00:36:37] **Ant:** Yeah.

In, in most cases it's handled automatically. There are people who come in and from day one, they say has my requirements. I'm going to have this much traffic. And I'm going to have, you know, a hundred thousand users hitting this every hour. And in those cases we will over-provisioned from the start.

But if it's just the self service case, then it will be start on a smaller instance and an upgrade over time. And this is one of our biggest challenges over the next five years is we want to move to a more scalable Postgres. So cloud native Postgres. But the cool thing about this is there's a lot of.

Different companies and individuals working on this and upstreaming into Postgres itself. So for us, we don't need to, and we, and we would never want to fork Postgres and, you know, and try and separate the storage and the the computes. But more we're gonna fund people who are already working on this so that it gets upstreamed into Postgres itself.

And it's more cloud native. 

[00:37:46] **Jeremy:** Yeah. So I think the, like we talked a little bit about how Firebase was the original inspiration and when you work with Firebase, you, you don't think about an instance at all, right? You, you just put data in, you get data out. And it sounds like in this case, you're, you're kind of working from the standpoint of, we're going to give you this single Postgres instance.

As you hit the limits, we'll give you a bigger one. But at some point you, you will hit a limit of where just that one instance is not enough. And I wonder if there's you have any plans for that, or if you're doing anything currently to, to handle that.

[00:38:28] **Ant:** Yeah. So, so the medium goal is to do replication like horizontal scaling. We, we do that for some users already but we manually set that up. we do want to bring that to the self serve model as well, where you can just choose from the start. So I want, you know, replicas in these, in these zones and in these different data centers.

But then, like I said, the long-term goal is that. it's not based on. Horizontally scaling a number of instances it's just a Postgres itself can, can scale out. And I think we will get to, I think, honestly, the race at which the Postgres community is working, I think we'll be there in two years.

And, and if we can contribute resource towards that, that goal, I think yeah, like we'd love to do that, but yeah, but for now, it's, we're working on this intermediate solution of, of what people already do with, Postgres, which is, you know, have you replicas to make it highly available.

[00:39:30] **Jeremy:** And with, with that, I, I suppose at least in the short term, the goal is that your monitoring software and your team is handling the scaling up the instance or creating the read replicas. So to the user, it, for the most part feels like a managed service. And then yeah, the next step would be to, to get something more similar to maybe Amazon's Aurora, I suppose, where it just kind of, you pay per use.

[00:40:01] **Ant:** Yeah, exactly. Exactly. Aurora was kind of the goal from the start. It's just a shame that it's proprietary. Obviously. 

[00:40:08] **Jeremy:** right. 

Um, but it sounds, 

[00:40:10] **Ant:** the world would be a better place. If aurora was opensource. 

[00:40:15] **Jeremy:** yeah. And it sounds like you said, there's people in the open source community that are, that are trying to get there. just it'll take time. to, to all this, about making it feel seamless, making it feel like a serverless experience, even though internally, it really isn't, I'm guessing you must have a fair amount of monitoring or ways that you're making these decisions.

I wonder if you can talk a little bit about, you know, what are the metrics you're looking at and what are the applications you're you have to, to help you make these decisions?

[00:40:48] **Ant:** Yeah. definitely. So we started with Prometheus which is a, you know, metrics gathering tool. And then we moved to Victoria metrics which was just easier for us to scale out. I think soon we'll be managing like a hundred thousand Postgres databases will have been deployed on, on supabase. So definitely, definitely some scale. So this kind of tooling needs to scale to that as well. And then we have agents kind of everywhere on each application on, on the database itself. And we listen for things like the CPU and the Ram and the network IO. We also poll. Uh, Postgres itself. Th there's a extension called PG stats statements, which will give us information about what are, the intensive queries that are running on that, on that box.

So we just collect as much of this as possible um, which we then obviously use internally. We set alerts to, to know when, when we need to upgrade in a certain direction, but we also have an end point where the dashboard subscribes to these metrics as well. So the user themselves can see a lot of this information.

And we, I think at the moment we do a lot of the, the Ram the CPU, that kind of stuff, but we're working on adding just more and more of these observability metrics uh, so people can can know it could, because it also helps with Let's say you might be lacking an index on a particular table and not know about it.

And so if we can expose that to you and give you alerts about that kind of thing, then it obviously helps with the developer experience as well.

[00:42:29] **Jeremy:** Yeah. And th that brings me to something that I, I hear from platform as a service companies, where if a user has a problem, whether that's a crash or a performance problem, sometimes it can be difficult to distinguish between is it a problem in their application or is this a problem in super base or, you know, and I wonder how your support team kind of approaches that.

[00:42:52] **Ant:** Yeah, no, it's, it's, it's a great question. And it's definitely something we, we deal with every day, I think because of where we're at as a company we've always seen, like, we actually have a huge advantage in that.

we can provide. Rarely good support. So anytime an engineer joins super base, we tell them your primary job is actually frontline support.

Everything you do afterwards is, is secondary. And so everyone does a four hour shift per week of, of working directly with the customers to help determine this kind of thing. And where we are at the moment is we are happy to dive in and help people with their application code because it helps our engineers land about how it's being used and where the pitfalls are, where we need better documentation, where we need education.

So it's, that is all part of the product at the moment, actually. And, and like I said, because we're not a 10,000 person company we, it's an advantage that we have, that we can deliver that level of support at the moment. 

[00:44:01] **Jeremy:** w w what are some of the most common things you see happening? Like, is it I would expect you mentioned indexing problems, but I'm wondering if there's any specific things that just come up again and again,

[00:44:15] **Ant:** I think like the most common is people not batching their requests. So they'll write an application, which, you know, needs to, needs to pull 10,000 rows and they send 10,000 requests (laughs) . That that's, that's a typical one for, for people just getting started maybe. Yeah. and, then I think the other thing we faced in the early days was. People storing blobs in the database which we obviously solve that problem by introducing file storage. But people will be trying to store, you know, 50 megabytes, a hundred megabyte files in Postgres itself, and then asking why the performance was so bad.

So I think we've, we've mitigated that one by, by introducing the blob storage.

[00:45:03] **Jeremy:** and when you're, you mentioned you have. Over a hundred thousand instances running. I imagine there have to be cases where an incident occurs, where something doesn't go quite right. And I wonder if you could give an example of one and how it was resolved.

[00:45:24] **Ant:** Yeah, it's a good question. I think, yeah, w w we've improved the systems since then, but there was a period where our real time server wasn't able to handle rarely large uh, right ahead logs. So w there was a period where people would just make tons and tons of requests and updates to, to Postgres. And the real time subscriptions were failing. But like I said, we have some really great Elixir devs on the team, so they were able to jump on that fairly quickly. And now, you know, the application is, is way more scalable as a result. And that's just kind of how the support model works is you have a period where everything is breaking and then uh, then you can just, you know, tackle these things one by one. 

[00:46:15] **Jeremy:** Yeah, I think any, anybody at a, an early startup is going to run into that. Right? You put it out there and then you find out what's broken, you fix it and you just get better and better as it goes along.

[00:46:28] **Ant:** Yeah, And the funny thing was this model of, of deploying EC2 instances. We had that in like the first week of starting super base, just me and Paul. And it was never intended to be the final solution. We just kind of did it quickly and to get something up and running for our first handful of users But it's scaled surprisingly well.

And actually the things that broke as we started to get a lot of traffic and a lot of attention where was just silly things. Like we give everyone their own domain when they start a new project. So you'll have project ref dot super base dot in or co. And the things that were breaking where like, you know, we'd ran out of sub-domains with our DNS provider and then, but, and those things always happen in periods of like intense traffic.

So we ha we were on the front page of hacker news, or we had a tech crunch article, and then you discover that you've ran out of sub domains and the last thousand people couldn't deploy their projects. So that's always a fun a fun challenge because you are then dependent on the external providers as well and theirs and their support systems.

So yeah, I think. We did a surprisingly good job of, of putting in good infrastructure from the start. But yeah, all of these crazy things just break when obviously when you get a lot of, a lot of traffic

[00:48:00] **Jeremy:** Yeah, I find it interesting that you mentioned how you started with creating the EC2 instances and it turned out that just work. I wonder if you could walk me through a little bit about how it worked in the beginning, like, was it the two of you going in and creating instances as people signed up and then how it went from there to where it is today?

[00:48:20] **Ant:** yeah. So there's a good story about, about our fast user, actually. So me and Paul used to contract for a company in Singapore, which was an NFT company. And so we knew the lead developer very well. And we also still had the Postgres credentials on, on our own machines. And so what we did was we set up the th th the other funny thing is when we first started, we didn't intend to host the database.

We, we thought we were just gonna host the applications that would connect to your existing Postgres instance. And so what we did was we hooked up the applications to, to the, to the Postgres instance of this, of this startup that we knew very well. And then we took the bus to their office and we sat with the lead developer, and we said, look, we've already set this thing up for you.

What do you think. know, when, when you think like, ah, we've, we've got the best thing ever, but it's not until you put it in front of someone and you see them, you know, contemplating it and you're like, oh, maybe, maybe it's not so good. Maybe we don't have anything. And we had that moment of panic of like, oh, maybe we just don't maybe this isn't great.

And then what happened was he didn't like use us. He didn't become a supabase user. He asked to join the team. 

[00:49:45] **Jeremy:** nice, nice.

[00:49:46] **Ant:** that was a good a good kind of a moment where we thought, okay, maybe we have got something, maybe this is maybe this isn't terrible. So, so yeah, so he became our first employee. Yeah. 

[00:49:59] **Jeremy:** And so yeah, so, so that case was, you know, the very beginning you set everything up from, from scratch. Now that you have people signing up and you have, you know, I don't know how many signups you get a day. Did you write custom infrastructure or applications to do the provisioning or is there an open source project that you're using to handle that

[00:50:21] **Ant:** Yeah. It's, it's actually mostly custom. And you know, AWS does a lot of the heavy lifting for you. They just provide you with a bunch of API end points. So a lot of that is just written in TypeScript fairly straightforward and, and like I said, you never intended to be the thing that last. Two years into the business.

But it's, it's just scaled surprisingly well. And I'm sure at some point we'll, we'll swap it out for some I don't orchestration tooling like Pulumi or something like this. But actually the, what we've got just works really well.



[00:50:59] **Ant:** Be because we're so into Postgres our queuing system is a Postgres extension called PG boss. And then we have a fleet of workers, which are. Uh, We manage on EC ECS. Um, So it's just a bunch of VMs basically which just subscribed to the, to the queue, which lives inside the database.

And just performs all the, whether it be a project creation, deletion modification a whole, whole suite of these things. Yeah. 

[00:51:29] **Jeremy:** very cool. And so even your provisioning is, is based on Postgres.

[00:51:33] **Ant:** Yeah, exactly. Exactly (laughs) . 

[00:51:36] **Jeremy:** I guess in that case, I think, did you say you're using the right ahead log there to in order to get notifications?

[00:51:44] **Ant:** We do use real time, and this is the fun thing about building supabase is we use supabase to build supabase. And a lot of the features start with things that we build for ourselves. So the, the observability features we have a huge logging division. So, so w we were very early users of a tool called a log flare, which is also written in Elixir.

It's basically a log sync backed up by BigQuery. And we loved it so much and we became like super log flare power users that it was kind of, we decided to eventually acquire the company. And now we can just offer log flare to all of our customers as well as part of using supabase. So you can query your logs and get really good business intelligence on what your users um, consuming in from your database.

[00:52:35] **Jeremy:** the lock flare you're mentioning though, you said that that's a log sink and that that's actually not going to Postgres, right. That's going to a different type of store.

[00:52:43] **Ant:** Yeah. That is going to big query actually. 

[00:52:46] **Jeremy:** Oh, big query. Okay. 

[00:52:47] **Ant:** yeah, and maybe eventually, and this is the cool thing about watching the Postgres progression is it's become. It's bringing like transactional and analytical databases together. So it's traditionally been a great transactional database, but if you look at a lot of the changes that have been made in recent versions, it's becoming closer and closer to an analytical database.

So maybe at some point we will use it, but yeah, but big query works just great. 

[00:53:18] **Jeremy:** Yeah. It's, it's interesting to see, like, I, I know that we've had episodes on different extensions to Postgres where I believe they change out how the storage works. So there's yeah, it's really interesting how it's it's this one database, but it seems like it can take so many different forms. 

[00:53:36] **Ant:** It's just so extensible and that's why we're so bullish on it because okay. Maybe it wasn't always the best database, but now it seems like it is becoming the best database and the rate at which it's moving. It's like, where's it going to be in five years? And we're just, yeah, we're just very bullish on, on Postgres.

As you can tell from the amount of mentions it's had in this episode.

[00:54:01] **Jeremy:** yeah, we'll have to count how many times it's been said. I'm sure. It's, I'm sure it's up there. Is there anything else we, we missed or think you should have mentioned.

[00:54:12] **Ant:** No, some of the things we're excited about are cloud functions. So it's the thing we just get asked for the most at anytime we post anything on Twitter, you're guaranteed to get a reply, which is like when functions. And we're very pleased to say that it's, it's almost there. So um, that will hopefully be a really good developer experience where also we launched like a, a graph QL Postgres extension where the resolver lives inside of Postgres.

And that's still in early alpha, but I think I'm quite excited for when we can start offering that on the on the hosted platform as well. People will have that option to, to use GraphQL instead of, or as well as the restful API.

[00:55:02] **Jeremy:** the, the common thread here is that PostgreSQL you're able to take it really, really far. Right. In terms of scale up, eventually you'll have the read replicas. Hopefully you'll have. Some kind of I don't know what you would call Aurora, but it's, it's almost like self provisioning, maybe not sharing what, how you describe it.

But I wonder as a, as a company, like we talked about big query, right? I wonder if there's any use cases that you've come across, either from customers or in your own work where you're like, I just, I just can't get it to fit into Postgres.

[00:55:38] **Ant:** I think like, not very often, but sometimes we'll, we will respond to support requests and recommend that people use Firebase. they're rarely

like if, if they really do have like large amounts of unstructured data, which is which, you know, documented storage is, is kind of perfect for that. We'll just say, you know, maybe you should just use Firebase.

So we definitely come across things like that. And, and like I said, we love, we love Firebase, so we're definitely not trying to, to uh, destroy as a tool. I think it, it has its use cases where it's an incredible tool yeah. And provides a lot of inspiration for, for what we're building as well. 

[00:56:28] **Jeremy:** all right. Well, I think that's a good place to, to wrap it up, but where can people hear more about you hear more about supabase?

[00:56:38] **Ant:** Yeah, so supeabase is at supabase.com. I'm on Twitter at ant Wilson. Supabase is on Twitter at super base. Just hits us up. We're quite active on the and then definitely check out the repose gets up.com/super base. There's lots of great stuff to dig into as we discussed. There's a lot of different languages, so kind of whatever you're into, you'll probably find something where you can contribute. 

[00:57:04] **Jeremy:** Yeah, and we, we sorta touched on this, but I think everything we've talked about with the exception of the provisioning part and the monitoring part is all open source. Is that correct? 

[00:57:16] **Ant:** Yeah, exactly.

And as, yeah. And hopefully everything we build moving forward, including functions and graph QL we'll continue to be open source.

[00:57:31] **Jeremy:** And then I suppose the one thing I, I did mean to touch on is what, what is the, the license for all the components you're using that are open source?

[00:57:41] **Ant:** It's mostly Apache2 or MIT. And then obviously Postgres has its own Postgres license. So as long as it's, it's one of those, then we, we're not too precious. I, As I said, we inherit a fair amounts of projects. So we contribute to and adopt projects. So as long as it's just very permissive, then we don't care too much.

[00:58:05] **Jeremy:** As far as the projects that your team has worked on, I've noticed that over the years, we've seen a lot of companies move to things like the business source license or there's, there's all these different licenses that are not quite so permissive. And I wonder like what your thoughts are on that for the future of your company and why you think that you'll be able to stay permissive.

[00:58:32] **Ant:** Yeah, I really, really, rarely hope that we can stay permissive. forever. It's, it's a philosophical thing for, for us. You know, when we, we started the business, it's what just very, just very, as individuals into the idea of open source. And you know, if, if, if AWS come along at some point and offer hosted supabase on AWS, then it will be a signal that where we're doing something.

Right. And at that point we just, I think we just need to be. The best team to continue to move super boost forward. And if we are that, and I, I think we will be there and then hopefully we will never have to tackle this this licensing issue. 

[00:59:19] **Jeremy:** All right. Well, I wish you, I wish you luck.

[00:59:23] **Ant:** Thanks. Thanks for having me. 

[00:59:25] **Jeremy:** This has been Jeremy Jung for software engineering radio. Thanks for listening. 

</div>