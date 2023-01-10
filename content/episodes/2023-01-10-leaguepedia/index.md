+++
title = "Megan Cutrofello on Leaguepedia"

description = "Megan shares her experiencing building the League of Legends eSports Wiki"

[extra]
episode_url = "https://pinecast.com/listen/be69f622-8ffc-4646-828b-7b6517f54260.mp3"
+++

Leaguepedia is a MediaWiki instance that covers tournaments, teams, and players in the League of Legends esports community. It's relied on by fans, analysts, and broadcasters from around the world.

Megan "River" Cutrofello joined Leaguepedia in 2014 as a community manager and by the end of her tenure in 2022 was the lead for Fandom's esports wikis.

She built up a community of contributing editors in addition to her role as the primary MediaWiki developer.

She writes on her [blog](https://river.me) and is a frequent speaker at the [Enterprise MediaWiki Conference](https://www.mediawiki.org/wiki/EMWCon)

### Topics covered:

- When to use MediaWiki
- Visual vs code editor
- MediaWiki's rough syntax
- Templates and markup
- Limiting user input to simplify pages
- Choosing not to transliterate long player names in certain languages
- Handling mobile clients
- Building aliases for search results
- Creating a single source of truth
- Roster changes and caching
- Cargo (Query data in MediaWiki templates using SQL)
- Hiding implementation details from editors
- Optimizing for the editor, not a clean codebase
- Training your users to use workarounds
- MediaWiki only supports es5
- The wiki aesthetic
- Who is working on the wiki + onboarding
- Who is using the wiki
- The future of Leaguepedia
- How Megan got into wiki development
- Issues as opportunities to onboard

### Related Links

- [River Writes](https://river.me/) - Megan's Blog
- [Leaguepedia](https://lol.fandom.com/wiki/League_of_Legends_Esports_Wiki) - League of Legends esports wiki
- [MediaWiki](https://www.mediawiki.org/wiki/MediaWiki)
- [VisualEditor](https://www.mediawiki.org/wiki/VisualEditor)
- [VueJS in MediaWiki](https://www.mediawiki.org/wiki/Vue.js)
- [Open issue to support ES6 in MediaWiki](https://phabricator.wikimedia.org/T178356)
- [Whitespace programming language](https://en.wikipedia.org/wiki/Whitespace_(programming_language))
- [Lua](https://www.lua.org/)

### MediaWiki extensions
- [CharInsert](https://www.mediawiki.org/wiki/Extension:CharInsert) - Add code snippets into the MediaWiki editor
- [Semantic MediaWiki (SMW)](https://www.semantic-mediawiki.org/wiki/Semantic_MediaWiki) - Store and query data inside Wiki pages
- [Cargo](https://www.mediawiki.org/wiki/Extension:Cargo) - Replaced SMW at Leaguepedia

### Conference Talks
- [Usage of Cargo with Lua on LoL Gamepedia](https://www.youtube.com/watch?v=Me7Q_thzc98)
- [Mediawiker SublimeText plugin](https://www.youtube.com/watch?v=kkfyfZHN488)
- [Cargo/Lua Best Practices, and When Not To Use Them](https://www.youtube.com/watch?v=iy89cJIH4Sc)
- [MediaWiki Lua Tutorial](https://www.youtube.com/watch?v=-YbvRj7Bs-4)
- [Editing your wiki with Python is easier than you think](https://www.youtube.com/watch?v=w3HZbEmqSfI)

### Other podcast appearances
- [Between the Brackets](https://betweenthebrackets.libsyn.com/episode-26-megan-cutrofello)

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

[00:00:00] **Jeremy:** Today I'm talking to Megan Cutrofello. She managed the Leaguepedia eSports wiki for eight years, and in 2017 she got an award for being the unsung hero of the year for eSports. So Megan, thanks for joining me today. 

[00:00:17] **Megan:** Thanks for having me. 

[00:00:19] **Jeremy:** A lot of the people I talk to are into web development, so they work with web frameworks and things like that. And I guess when you think about it, wikis are web development, but they're kind of their own world, I suppose. for someone who's going to build some kind of a site, like when does it make sense for them to use a wiki versus, uh, a content management system or just like a more traditional web framework? 

[00:00:55] **Megan:** I think it makes the most sense to use a wiki if you're going to have a lot of contributors and you don't want all of your contributors to have access to your server.

also if your contributors aren't necessarily as tech savvy as you are, um, it can make sense to use a wiki. if you have experience with MediaWiki, I guess it makes sense to use a Wiki.

Anytime I'm building something, my instinct is always, oh, I wanna make a Wiki (laughs) . Um, so even if it's not necessarily the most appropriate tool for the job, I always. My, my first thought is, hmm, let's see, I'm, I'm making a blog. Should I make my blog in in MediaWiki? Um, so, so I always, I always wanna do that. but I think it's always, when you're collaborating is pretty much, you always wanna do MediaWiki 

[00:01:47] **Jeremy:** And I, I think that's maybe an important point when you say people are collaborating. When I think about Wikis, I think of Wikipedia, uh, and the fact that I can click the edit button and I can see the markup right there, make a change and, and click save. And I didn't even have to log in or anything. And it seems like that workflow is built into a wiki, but maybe not so much into your typical CMS or WordPress or something like that.

[00:02:18] **Megan:** Yeah. Having a public ability to solicit contributions from anyone. so for Leaguepedia, we actually didn't have open contributions from the public. You did have to create an account, but it's still that open anyone can make an account and all you have to do is like, go through that one step of create an account.

Admittedly, sometimes people are like, I don't wanna make an account that's so much work. And we're like, just make the account. Come on. It's not that hard. but, uh, you still, you're a community and you want people to come and contribute ideas and you want people to come and be a part of that community to, document your open source project or, record the history of eSports or write down all of the easter eggs that you find in a video game or in a TV show, or in your favorite fantasy novels.

Um, and it's really about community and working together to create something where the whole is bigger than the sum of its parts.

[00:03:20] **Jeremy:** And in a lot of cases when people are contributing, I've noticed that on Wikipedia when you edit, there's an option for a, a visual editor, and then there's one for looking at the raw markup. in, in your experience, are people who are doing the edits, are they typically using the visual editor or are they mostly actually editing the, the markup? 

[00:03:48] **Megan:** So we actually disabled the Visual editor on Leaguepedia, because the visual editor is not fantastic at knowing things about templates. Um, so a template is when you have one page that gets its content pulled into the larger page, and there's a special syntax for that, and the visual editor doesn't know a lot about that.

Um, so that's the first reason. And then the second reason is that, there's this, uh, one extension that we use that allows you to make a clickable, piece of text. It's called (https://www.mediawiki.org/wiki/Extension:CharInsert) CharInserts, uh, for character inserts. so I made a lot of these things that is sort of along the same philosophy as Visual Editor, where it's to help people not have to have the same burden of knowledge, of knowing every exact piece of source that has to be inserted into the page. So you click the thing that says like, um, insert a pick and band prefill, and then a little piece of JavaScript fires and it inserts a whole bunch of Wiki text and then you just enter the champions in the correct places. In the prefills of champions are like the characters that you play in, uh, league of Legends.

And so then you have like the text is prefilled for you and you only have to fill in into this outline. so Visual Editor would conflict with CharInserts, and I much preferred the CharInserts approach where you have this compromise in between the never interacting with source and having to have all of the source memorized.

So between the fact that Visual Editor like is not a perfect tool and has these bugs in it, and also the fact that I preferred CharInserts, we didn't use Visual Editor at all. I know that some wikis do like to use Visual Editor quite a bit, and especially if you're not working with these templates where you have all of these prefills, it can be a lot more preferred to use Visual Editor.

Visual Editor is an experience much more similar to editing something like Microsoft Word, It doesn't feel like you're editing code. and editing code is, I mean, it's scary. Like for, and when I said like, MediaWiki is when you have editors who aren't as tech savvy, as the person who set up the Wiki.

for people who don't have that experience, I mean, when you just said like you have to edit a wiki, like someone who's never done that before, they can be very intimidated by it. And you're trying to build a sense of community. You don't want to scare away your potential editors. You want everyone to be included there.

So you wanna do everything possible to make everyone feel safe, to contribute their ideas to the Wiki. and if you make them have to memorize syntax, like even something that to me feels as simple as like two open brackets and then the name of a page, and then two closed brackets means linking the page.

Like, I mean, I'm used to memorizing a lot of syntax because like, I'm a programmer, but someone who's never written code before, I mean, they're not used to memorizing things like that. So they wanna be able to click a button that says insert link, and then type the name of the page in the middle of the things that pop up there.

Um, so visual editor is. It's a lot safer to use. so a lot of wikis do prefer that. and if it, if it didn't have the bugs with the type of editing that my Wiki required, and if we weren't using CharInserts so much, we definitely would've gone for it. But, um, it wasn't conducive to the wiki that I built, so we didn't use it at all. 

[00:07:42] **Jeremy:** And the, the compromise you're referring to, is it where the editor sees the raw markup, but then they can, there's like little buttons on the side they can click and they'll know, okay, if I click this one, then it's going to give me the text for creating a list or something like that. 

[00:08:03] **Megan:** Yeah, it's a little bit more high level than creating a list because I would never even insert the raw syntax for creating a list. It would be a template that's going to insert a list at the very end. but basically that, yeah,

[00:08:18] **Jeremy:** And I, I know for myself, even though I do software development, if I click at it on a wiki and there's all the different curly brace tags, there's the square tags, and. I think if you spend some time with it, you can kind of get a sense of what it means. But for the average person who doesn't work with software in their day to day, do, do you find that, is that a big barrier for them where they, they click edit and there's all this stuff that they don't really understand?

Is that where some people just, they go, oh, I don't, I don't know what to do.

[00:08:59] **Megan:** I think the biggest barrier is actually clicking at it in the first place. so that was a big barrier to me actually. I didn't wanna click at it in the first place, and I guess my reasons were maybe a little bit different where for me it was like, I know that if I click edit, this is going to be a huge rabbit hole and I'm going to learn way too much about wikis and this is going to consume my entire life and look where I ended up.

So I guess I was pretty right about that. I don't know if other people feel the same way or if they just like, don't wanna get involved at all. but I think once people, click edit, they're able to figure it out pretty well. I think there's, there's two barriers or maybe three barriers. the first one is clicking edit in the first place.

The second one is if they learn to code templates at all. Media Wiki syntax is literally the worst I have encountered other than programming languages that are literally parodies. So like the white space language is worse (laughs https://en.wikipedia.org/wiki/Whitespace_(programming_language)) , but like it's two curly braces for a template and it's three curly braces for a variable.

And like, are you actually kidding me? One of my blog posts is like a plea to editors to write a comment saying the name of the template that they're ending because media wiki like doesn't provide any syntax for what you're ending. And there's no, like, there's no indentation. So you can't visually see what you're ending.

And there's no. So when I said the white sp white space language, that was maybe appropriate because MediaWiki prints all of the white space because it's really just like, PHP functions that are put into the text that you're literally putting onto the page. So any white space that you put gets printed.

So the only way to put white space into your code is if you comment it out. So anytime you wanna put a new line, you have to comment out your new line. And if you wanna indent your code, you have to comment out the indents. So it's just, I, I'm , I'm not exaggerating here. It's, it's just the worst. Occasionally you can put a little bit of white space. Because there's like some divisions in parser functions that get handled when it gets sent to the parser. And, but I mean, for the most part it's just, it's just terrible. so if I'm like writing an if statement, I'll write if, and then I'll write a commented out endif at the end, so once an editor starts to write templates, like with parser functions and stuff, that's another big barrier because, and that's not because like people don't know how to code, it's just because the MediaWiki language, and I use language very loosely, it's like this collection of PHP functions poured into this just disaster

It's just, it's not good! (laughs) And the, the next barrier is when people start to jump to Lua, which is just, I mean, it's just Lua where you can write Lua modules and then, Lua is fine. It's great, it has white space and you can make new lines and it's absolutely fine and you can write an entire code base and as long as you're writing Lua, it's, it's absolutely fantastic and there's nothing wrong with it anymore (laughs) 

So as much as I just insulted the MediaWiki language, like writing Lua in MediaWiki is great (laughs) . So for, for most of my time I was writing Lua. Um, and I have absolutely no complaints about that except that Lua is one index, but actually the one indexing of Lua is fine because MediaWiki itself is one indexed.

So people complain about Lua being one index, and I'm like, what are you talking about? If it's, if another language were used, then you'd have all of this offsetting when you go to your scripting language because you'd have like the first argument from your template in MediaWiki going into your scripting language, and then you'd have to offset it to zero and everyone would be like vastly confused about what's going on.

So you should be thankful that they picked a language that's one index because it saves you all of this headache. So anyway, sorry for that tangent, but it's very good that we picked a one index language.

[00:13:17] **Jeremy:** When you were talking about the, the if statement and having to put in comments to have white space, is it, cuz like when I think about an if statement in most languages, the, the if statement isn't itself rendering anything, it's like deciding if you're going to do something inside of the, if so. like what, what would that white space do if you didn't comment it out in the context of the if?

[00:13:44] **Megan:** So actually you would be able to put some white space inside of an if statement, but you would not be able to put any white space after an if statement. and there, most likely inside of the if statement, you're printing variables or putting other parser functions. and the other parser functions also end in like two curly braces.

And, depending on what you're printing, you're likely ending with a series of like five or eight, or, I don't know, some very large set of curly braces. And so what I like to do is I would like to be able to see all of the things that I'm ending with, and I wanna know like how far the nesting goes, right.

So I wanna write like an end if, and so I have to comment that out because there's no like end if statement. so I comment out an end if there, it's more that you can't indent the statements inside of the if, because anything that you would be printing inside of your code would get printed. So if I like write text inside of the code, then that indentation would get printed into the page.

And then if I put any white space after the if statement, then that would also get printed. So technically you can have a little bit of white space before the curly braces, but that's only because it's right before the curly braces and PHP will strip the contents right inside of the parser function.

So basically if PHP is stripping something, then you're allowed to have white space there. But if PHP isn't stripping anything, then all of the white space is going to be printed and it's like so inconsistent that for the most part it's not safe to put white space anywhere because you don't, you have to like keep track of am I in a location where PHP is going to be stripping something right now or not?

and I, I wanna know what statement or what variable or what template I'm closing at any location. So I always want to, write out what I'm closing everywhere. And then I have to comment that because there was no foresight to put like an end 

if clause in this white space, sensitive language.

[00:16:22] **Jeremy:** Yeah, I, I think I see what you mean. So you have, if you're gonna start an, if you have the, if inside these curly braces, but then, inside the, if you typically are going to render some text to the page, and so intuitively you would indent it so that it's indented in from the if statement. But then if you do that, then it's gonna be shifted to the right on, on the Wiki.

Did I get that right? 

[00:16:53] **Megan:** Yeah. So you have the flexibility to put white space immediately because PHP will strip immediately, but then you don't have flexibility to put any white space after that, if that makes sense.

[00:17:11] **Jeremy:** So, so when you say immediately, is that on the following line or is that 

[00:17:15] **Megan:** yeah, so any white space before the first clause, you have flexibility. So like if you were to put an if statement, so it's like if, and then there's a colon, all of the next white space will get stripped. Um, so then you can put some text, but then, if you wanted to like put some text and then another if statement nested within the first if statement.

It's not like Lua where you could like assign a variable and then put a comment and then put some more white space and then put another statement. And it's white space insensitive because you're just writing code and you haven't returned anything yet. 

it, it's more like Jinja (View templating language) than Python for, for an analogy.

So everything is getting printed because you're in like a, this templating language, not actually a programming language. Um, so you have to work as if you're in a templating language about, you know, 70% of the time , unless you're in this like very specific location where PHP is stripping your white space because you're at the edge of an argument that's being sent there.

So it's like incredibly inconsistent. And every now and then you get to like, pretend that you're in an actual language and you have some white space, that you can indent or whatever. it's just incredibly 

inconsistent, which is like what you absolutely want out of a programming language (laughs) 

yeah, it's like you're, you're writing templates, but like, it seems like because of the fact that it's using php, there's

[00:18:56] **Jeremy:** weird exceptions to the behavior. 

Yeah. 

[00:18:59] **Megan:** Exactly. Yeah. 

[00:19:01] **Jeremy:** and then you also mentioned these, these templates. So, if I understand correctly, this is kind of like how a lot of web frameworks will have, partials, I guess, where you'll, you'll be able to have a webpage, but it's made up of different I don't know if you would call them components, but you're able to build a full page that's made up of a bunch of different pieces.

So you could have a 

[00:19:31] **Megan:** Yeah Yeah that's a good analogy. 

[00:19:33] **Jeremy:** Where it's like, here's my table of contents, or here's my info box, or things like that. And those are all things that you would create a MediaWiki template for, and then somehow the, the data gets passed into those templates and the template decides how to, to render it out. 

[00:19:55] **Megan:** Yeah. 

[00:19:56] **Jeremy:** And for these, these templates, I, I noticed on some of the Leaguepedia pages, I noticed there's some html in some of them. I was curious if that's typical to write them with HTML or if there are different ways native to Media Wiki for, for, creating these templates.

[00:20:23] **Megan:** Um, it depends on what you're doing. MediaWiki has a special syntax for tables specifically. I would say that it's not necessarily recommended to use the special syntax because occasionally you can get things to not work out fantastically if people slightly break things. But it's easier to use it.

So if you know that everything's going to work out perfectly, you can use it. and it's a simple shortcut. if you go to the help page about tables on Wikipedia, everything is explained, and not all HTML works, um, for security reasons. So there's like a list of allowed, things that you can use, allowed tags, so you can't put like forms and stuff natively, but there's the widgets extension that you can use and widgets just automatically renders all html that you put inside of a widget.

Uh, and then the security layer there is that you have to have a special permission to edit a widget. so, you only give trusted people that permission and then they can put the whatever html they want there. So, we have a few forms on Leaguepedia that are there because I edited, uh, whichever widgets, and then put the widgets into a Lua module and then put the Lua module into a template and then put the template onto the page.

I was gonna say, it's not that complicated. It's not as complicated as it sounds, but I guess it really is as complicated as it sounds (laughs) . Um, so, uh, I, I won't say that. I don't know how standard it is on other wikis to use that much html, I guess Leaguepedia is pretty unique in how complicated it is.

There aren't that many wikis that do as many things as we did there. but tables are pretty common. I would say like putting divs places to style them, uh, is also pretty common. but beyond that, usually there's not too many HTML elements just because you typically wanna be mobile friendly and it's relatively hard to stay mobile friendly within the bounds of MediaWiki if you're like putting too many elements everywhere.

And then also allowing users to put whatever content inside of them that they want. The reason that we were able to get away with it is because despite the fact that we had so many editors, our content was actually pretty limited. Like if there's a bracket, it's only short team names going into it.

So, and short team names were like at most five or six characters long, so we don't have to worry about like overflow of team names. Although we designed the brackets to support overflow of team names, and the team names would wrap around and the bracket would not break. And a lot of CSS Magic went into making that work that, we worked really hard on and then did not end up using (laughsz) 

[00:23:39] **Jeremy:** Oh no. 

[00:23:41] **Megan:** Only short team names go into brackets.

But, that's okay. uh, and then for example, like in, uh, schedules and stuff, a lot of fields like only contain numbers or only contain timestamps. there's like a lot of tables again where like there's only two digit numbers with one decimal point and stuff like that. So a lot of the stuff that I was designing, I knew the content was extremely constrained, and if it wasn't then I said, well, too bad.

This is how I'm telling you to put the content . Um, and for technical reasons, that's the content that's gonna go here and I don't care. so there's like, A lot of understanding that if I said for technical reasons, this is how we have to do it. Then for technical reasons, that was how we had to do it.

And I was very lucky that all of the people that I worked with like had a very big appreciation with like, for technical reasons, like argument over. This is what's happening. And I know that with like different people on staff, like they would not be willing to compromise that way. Um, so I always felt like extremely lucky that like if I couldn't figure out a way to redesign or recode something in order to be more flexible, then like that would just be respected.

And that was like how we designed something. But in general, like it's, if you are not working with something as rigid as, I mean, and like the history of eSports sounds like a very fluid thing, but when you think about it, like it's mostly names of teams, names of players and statistics. There's not that much like variable stuff going on with it.

It's very easy to put in relational databases. It's very easy to put in fixed width tables. It's very easy to put in like charts that look the same on every single page. I'm not saying. It was always easy to like write everything that I wrote, and it's not, it wasn't always easy to like, deal with designs and stuff, but like relative to other topics that you can pick, it was much easier to put constraints on what was going to go where because everything was very similar across regions, across, although actually one thing.

Okay, so this will be like the, the exception that proves the rule. uh, we would trans iterate players' names when we, showed them in team rosters. So, uh, for example, when we were showing the hangul, the Korean player's names, we would show an English translation also.

Um, and we would do this for every single alphabet. but Hungarian players' names are really, really, really long. And so the transliteration doesn't fit in the table when we show the translation to the Roman alphabet. And so we couldn't do this, so we actually had to make a cargo table. Of alphabets that are allowed to be transliterated into the Roman alphabet, uh, when we have players names in that alphabet.

So we had, like, hangul was allowed and Arabic was allowed, and I can't remember the exact list, but we had like three alphabet, three or four alphabets were allowed and the rest of the alphabets were dis allowed to be transliterate into, uh, the Roman alphabet. and so again, we made up a rule that was like a hard rule across the entire Wiki where we forced the set of alphabets that were transliterated so that this tables could be the same size roughly across every single team page because these Hungarian player names are too long (laughs) 

So I guess even this exception ended up being part of the rule of everything had to be standardized because these tables were just way too wide and they were running into the info box. They couldn't fit on the side. so it's really hard when you have like arbitrary user entered content to fit it into the HTML that you design.

And if you don't have people who all agree to the same standards, I mean, Even when we did have people who agreed to all of the same standards, it was really, really, really hard. And we ended up having things like a table of which alphabets to transliterate. Like that's not the kind of thing that you think you're going to end up having when you say, let's catalog the history of League of Legends eSports,

[00:28:40] **Jeremy:** And, and so when, let's say you had a language that you couldn't trans iterate, what would go into the table. 

[00:28:49] **Megan:** uh, just the native alphabet. 

[00:28:51] **Jeremy:** Oh I see. Okay.

[00:28:53] **Megan:** Yeah. And then if they went to the player page, then you would be able to see it transliterated. But it wouldn't show up on the team page. 

[00:29:00] **Jeremy:** I see. And then to help people visualize what some of these things you're talking about look like when you're talking about a, a bracket, it's, is it kind of like a tree structure where you're showing which teams are facing which teams and okay, 

[00:29:19] **Megan:** We had a very cool, CSS grid structure that used like before and after pseudo elements to generate the lines, uh, between the teams and then the teams themselves were the elements of the grid. Um, and it's very cool. Uh, I didn't design it. Um, I have a friend who I very, very fortunately have a friend who's amazing at CSS because I am like mediocre at css and she did all of our CSS for us.

And she also like did most of our designs too. Uh, so the Wiki would not be like anything like what it is without her.

[00:30:00] **Jeremy:** And when you're talking about making sure the designs fit on desktop and, and mobile, um, I think when you were talking earlier, you're talking about how you have these, these templates to build these tables and the, these, these brackets. Um, so I guess in which part of the wiki is it ensuring that it looks different or that it fits when you're working with these different screen sizes 

[00:30:32] **Megan:** Usually it's a peer CSS solution. Every now and then we hide an element on mobile altogether, and some of that is actually MediaWiki core, for example, in, uh, nav boxes don't show up on mobile. And that's actually on Wikipedia too. Uh, well, I guess, yeah. I mean, being MediaWiki core, So if you've ever noticed the nav boxes that are at the bottom of pages on Wikipedia, just don't show up on like en.m.wikipedia.org.

and that way you're not like loading, you're not loading, but display noneing elements on mobile. but for the most part it's pure CSS Solutions. Um, so we use a lot of, uh, display flex to make stuff, uh, appropriate for mobile. Um, some media roles. sometimes we display none stuff for mobile. Uh, we try to avoid that because obviously then mobile users aren't getting like the full content.

Occasionally we have like overflow rules, so you're getting scroll bars on mobile and then every now and then we sort of just say, too bad if you're on mobile, you're gonna have not the greatest solution or not the greatest, uh, experience. that's typically for large data tables. so the general belief at fandom was like, if you can't make it a good experience on mobile, don't put it on the Wiki.

And I just think that's like the worst philosophy because like then no one gets a good experie. And you're just putting less content on the Wiki so no one gets to enjoy it, and no one gets to like use the content that could exist. So my philosophy has always been like the, the, core overview pages should be, as good as possible for both PC and mobile.

And if you have to optimize for one, then you slightly optimize for mobile because the majority of traffic is mobile. but attempt not to optimize for either one and just make it a good experience on both. but then the pages behind that, I say behind because we like have tabs views, so they're like sort of literally behind because it looks like folders sort of, or it looks like the tabs in a folder and you can, like, I, I don't know, it, it looks like it's behind (laughs) , the, the more detailed views where it's just really hard to design for mobile and it's really easy to design for pc and it just feels very unlikely that users on mobile are going to be looking at these pages in depth.

And it's the sort of thing. A PC user is much more likely to be looking at, and you're going to have like multiple windows open and you're gonna be tapping between them and you're gonna be doing all of your research at PC. You absolutely optimize this for PC users. Like, what the hell this is? These are like stats pages.

It's pages and pages and pages of stats. It's totally fine to optimize this for PC users. And if the option is like, optimized for PC users or don't create it at all, what are you thinking To not create it at all, like make it a good experience for someone? 

So I don't, I don't understand that philosophy at all. 

[00:34:06] **Jeremy:** Did you, um, have any statistics in terms of knowing on these types of pages, these pages that are information dense or have really big tables? Could you tell that? Oh, most of the people coming here are on computers or, or larger screens. 

[00:34:26] **Megan:** I didn't have stats for individual pages. Um, mobile I accidentally lost Google Analytics access at some point, and honestly I wasn't interested enough to go through the process of trying to get it back. when I had it, it didn't really affect what I put time into, because it was, it was just so much what I expected it to be.

That it, it didn't really affect much. What I actually spent the most time on was looking, so you can, uh, you get URLs for search results. And so I would look through our search results, and I would look at the URL of the failed search results and, so there would be like 45 results for this particular failed search.

And then I would turn that into a redirect for what I thought the target was supposed to be. So I would make sure that people's failed searches would actually resolve to the correct thing. So if they're like typo something, then I make the typo actually resolve. So we had a lot of redirects of like common typos, or if they're using the wrong name for a tournament, then I make the wrong name for the tournament resolve.

So the analytics were actually really helpful for that. But beyond that, I, I didn't really find it that useful.

[00:35:48] **Jeremy:** And then when you're talking about people searching, are these people using a search box on the Wiki itself And not finding what they were looking for? 

[00:36:00] **Megan:** Yeah. So like the internal search, so like if you search Wikipedia for like New York City, but you spell it C I Y T, , then you're not going to get a result. But it might say, did you mean New York City t y? If like 45 people did that in one month, then that would show up for me. And then I don't want them to be getting, like, that's a bad experience.

Sure. They're eventually getting there, but I mean, I don't want them to have to spend that extra time. So I'm gonna make an automatic redirect from c Y T to c i t Y 

[00:36:39] **Jeremy:** And, and. Maybe we should have talked about this a little earlier, but the, all the information on Leaguepedia is, it's about all of the different matches and players, um, who play League of Legends. so when you edit a, a page on Wikipedia, all of that information, or a lot of it I think is, is hand entered by, by people and on Leagueapedia, which has all this information about like what, how teams did in a tournament or, intricate stats about how a game went.

That seems like a lot of information for someone to be hand entering. So I was wondering how much of that information is somebody actually manually editing those things and how much is, is done automatically or programmatically. 

[00:37:39] **Megan:** So it's mostly hand entered. We do have a little bit of it that's automated, via a couple scripts, but for the most part it's hand entered. But after being handed, entered into a couple of data pages, it gets propagated a lot of times based on a bunch of Lua modules and the cargo extension. So when I originally joined the Wiki back in 2014, it was hand entered.

Not just once, but probably, I don't know, seven times for tournament results and probably 10 or 12 times for roster changes. It was, it was a lot. And starting in 2017, I started rewriting all of the code so that it was entered exactly one time for everything. Tournament results get entered one time into a data page and roster changes get entered one time into a data page.

And, for roster changes, that was very difficult because, for a roster change that needs to update the team history on a player page, which goes, from a join to a leave and it needs to update the, the like roster, change portal for the off season, which goes from a leave to a join because it's showing like the deltas over the off season.

And it needs to update the current team in the, player's info box, which means that the current team has to be calculated from all of the deltas that have ever occurred in that player's history and it needs to update. Current rosters in the team pages, which means that the team page needs to know all of the current players who are currently on the team, which again, needs to know all of the deltas from all of history because all that you're entering is the roster changes.

You're not entering anyone's current team. So nowhere on the wiki does it ever store a current team anymore. It only stores the roster changes. So that was a lot of code to write and deciding even what was going to be entered was a lot because, all I knew was that I was going to single source of truth that somehow and I needed to decide what was I going to single source of truth.

So I decided, um, that I was going to be this Delta and then deciding what to do with that, uh, how to store it in a relational database. It was, it was a big project. and I didn't have a background as a developer either. so this was like, I don't know, this was like my third big project ever. So, that was, that was pretty intense.

but it was, it was a lot of fun. so it is hand entered but I feel like that's underselling it a little bit.

[00:40:52] **Jeremy:** Yeah, cuz I was initially, I was a little confused when you mentioned how somebody might need to enter the same information multiple times. But, if I understood correctly, it would be if somebody's changing which team they're on, they would have to update, for example, the player's page and say like, oh, this player is on this team now.

And then you would have to go to their old team and remove them from the roster there. 

Go to the new team, add them to the roster there, And you can see where it would kind 

[00:41:22] **Megan:** Yeah. And then there's the roster, there's the roster nav box, and there's like the old team, you have to say, like the next team. Cuz in the previous players list, like we show former team members from the old team and you have to say like the next team. Uh, so if they had like already left their old team, you'd have to say like, new team.

Yeah, there's a, there's a lot of, a lot of places. 

[00:41:50] **Jeremy:** And so now what it sounds like is, I'm not sure this is exactly how it works, but if you go to any location that would need that information, which team is this player on? When you go to that page, for example, if you were to go to, uh, a teams page, then it would make a SQL query to figure out I guess who most recently had a, I forget what you called it, but like a join row maybe, or like a, they, they had the action of joining this team, and now, now there's a row in the database that says they did this. 

[00:42:30] **Megan:** it actually looks at the ten-- so I have an in in between table called tenures. And so it looks at the tenures table instead of querying all the way through the joins and leaves table and doing like the whole list of deltas. yeah. So, and it's also cached so you, it doesn't do the SQL query every time that you load the page.

So the only time that the SQL queries actually happen is if you do a save on the page. And then otherwise the entire generated HTML of the page is actually cached on the server. So you're, you're not doing that many database queries every time you load the page, so don't worry about that. but there, there can actually be something like a hundred SQL queries sometimes, when you're, saving a page.

So it would be absolute murder if you were doing that every time you went to the page. But yeah, it works. Something like that. 

[00:43:22] **Jeremy:** Okay, so this, this tenures table is, that's kind of like what's the current state of all these players and where they are, and then. 

[00:43:33] **Megan:** Um, the, the tenures table, caches sort of, or I guess the tenure table captures is a better word than caches um, every, join to leave historically from every team. Um, and then I save that for two reasons. The first one is so that I don't have to recompute it, uh, when I'm doing the team's table, because I have to know both the current members and the former members.

And then the second reason is also that we have a public api and so people can query that. 

if they're building tools, like a lot of people use the public api, uh, for various things. And, one person built like, sort of like a six degrees of Kevin Bacon except for League of Legends, uh, using our tenures tables.

So, part of the reason that that exists is so that uh, people can use it for whatever projects that they're doing. 

Cause the join, the join leave table is like pretty unfriendly and I didn't wanna have to really document that for anyone to use. So I made tenures so that that was the table I could document for people to use.

[00:44:39] **Jeremy:** Yeah. That, that's interesting in that, yeah, when you provide an api, then there's so many different things people can do that even if your wiki didn't really need it, they can build their own apps or their own pages built on all this information you've aggregated.

[00:44:58] **Megan:** Yeah. It's nice because then when someone says like, oh, can you build this as a feature request? I can say no, but you can (laughs) 

[00:45:05] **Jeremy:** Well you've, you've done the, the hard part for them (laughs) 

[00:45:09] **Megan:** Yeah. exactly. 

[00:45:11] **Jeremy:** So that's cool. Yeah. that's, that's interesting too about the, the caching because yeah, I guess when you think about a wiki, most of the people who are visiting it are just visiting it to see what's on there. So the, provided that they're not logged in and they don't need anything specific to them. Yeah, you should be able to cache the whole response. It sounds like. 

[00:45:41] **Megan:** Yeah. yeah. Caching was actually a nightmare with this in this particular thing. the, the team roster changes, because, so cargo, which I mentioned a couple times is the database extension that we used. Um, and it's basically a SQL wrapper that like, doesn't port 80% of the features that SQL has. so you can create tables and you can query, but you can't make, uh, like sub-select queries.

So your queries have to be like very simple. which is good for like most users of MediaWiki because like the average MediaWiki user doesn't have that much coding experience, but if you do have coding experience, then you're like, what, what, what am I doing? I can't, I can't do anything. Um, but it's a very powerful tool, still compared to most of what you could do with Media Wiki without this, basically you're adding a database layer to your software stack, which I mean, I, I, that's what you're doing, (laughs) 

Um, so you get a huge amount of power from adding cargo to a wiki. Um, in exchange it's, it's very performance. It's like, it's, it, it's resource heavy. uh, it hurts your performance a lot. and if you don't need it, then you shouldn't use it. But frequently you need it when you're doing, difficult or not necessarily difficult, but like intensive things.

Um, anytime that you need to pull data from one page to another, you wanna use something like that. Um,

So cargo, uh, one of the things that it doesn't do is it doesn't allow you to, uh, set a primary key easily. so you have to like, just like pretend that one row in the table is your primary key, basically. it internally automatically sets one, but it won't be static or it won't be the same every time that you rebuild the table because it rebuilds the table in a random order and it just uses an auto increment primary key.

So you set a row in the table to pretend to be your ran, to pretend to be your primary key. But editors don't know what, your editors don't understand anything about primary keys. And you wanna hide this from them completely. Like, you cannot tell an editor, protect this random number, please don't change this.

So you have to hide it completely. So if you're making your own auto increment, like an editor cannot know that that exists. Like this is back to when we were talking about like visual editor. This is like, one of the things about making the wiki safe for people is like not exposing them to the internals of like, anything scary like that.

So for example, if an editor accidentally reorders two rows and your roster change data like that has to not matter. Because that can't break the entire wiki. They, you can't make an editor like freak out because they just reordered two rows in, in the page. And you can't put like a scary notice somewhere saying, under no circumstances reorder two rows here.

Like, that's gonna scare people away. And you wanna be very welcoming and say like, it's impossible to break this page no matter how hard you tried. Don't worry. Anything you do, we can just fix it. Don't worry. But the thing is that everything's going to be cached. And so in particular, um, when I said I made that tenures table, one thing I did not wanna do was resave every single row from the join leave table.

So you had to join back to, sorry, I'm going to use, join in two different connotations. you had to join back to the join leave table in order to get like all of the auxiliary data, like all of the extra columns, like, I don't know, like role, date, team name and stuff. Because otherwise the tenures table would've had like 50 columns or something.

So I needed to store the fake primary key in the tenures table, but the tenures table is cached on the player page and the join leave table is on the data page, which means that I need to purge the cache on the player page anytime that someone edits the data on the data page. Which means that, so there's like some JavaScript that does that, but if someone like changes the order of the lines, then that primary key is going to change because I have an auto increment going on.

And so I had to like very, very carefully pick a primary key here so that it was literally impossible for any kind of order change to affect what the primary key was so that the cash on the player page wasn't going to be changed by anything that the editor did in unless they were going to then update the cash on that player page after making that change.

If that makes sense. So after an editor makes a change on the news page, they're going to press a button to update the cache on the player page, but they're only going to update the player page for the one line that they change on the news page. These, uh, primary keys had to be like super invariant for accidental row moves, or also later on, like entire moves of separating a bunch of these data pages into like separate subpages because the pages were getting too big and it was like timing out the server because there were too many stores to the database on a single page every time you save the page.

And anyway, it took me like five iterations of making the primary key like more and more specific to the single line because my auto increment was like originally including every single line I was auto incrementing and then I auto incremented only when that single player was was involved. And then I auto incremented only when that player and the team was involved.

And then I reset the auto increment for that date. So, and it was just got like more and more convoluted what my primary key was. It was, it was a mess. 

Anyway, this is just like another thing when you're working with volunteers who don't know what's going on and they're editing the page and they can contribute content, you have to code for the editor and not code for like minimizing complexity,

The editor's experience matters more than the cleanliness of your code base, and you just end up with these like absolute messes that make no sense whatsoever because the editor's experience matters and you always have to code to the editor. And Media Wiki is all about community, and the editor just becomes part of the software and part of the consideration of your code base, and it's very, very different from any other kind of development because they're like, the UX is just built so deeply into how you're developing.

[00:53:33] **Jeremy:** if I am following correctly, when I, when I think of using SQL when you were first talking about cargo and you were talking about how you make your own tables, and I'm envisioning the, the columns and the rows and, it's very common for the primary key to either be auto incrementing or some kind of GUID

But then if I understood correctly, I think what you were saying is that anytime an editor makes changes to the data, it regenerates the whole table. Is that did I get that right?

[00:54:11] **Megan:** It regenerates all of the rows on that page. 

[00:54:14] **Jeremy:** and when you talk about this, these 

data pages, there's some kind of media wiki or cargo specific markup where people are filling in what is going to go into the rows. And the actual primary key that's in MySQL is not exposed anywhere when they're editing the data. 

[00:54:42] **Megan:** That's right

[00:54:44] **Jeremy:** And so when you're talking about trying to come up with a primary key, um, I'm trying to, I guess I'm trying to picture 

[00:54:57] **Megan:** So usually I do page name underscore an auto increment. But then if people can rearrange the rows which they do because they wanna get the rows chronological, but some people just put it at the top of the page and then other people are like, oh my God, it's not chronological. And then they fix it and then other people are like, oh my God, you messed up the time zone.

And then they rearrange it again. Then, I mean, normally I wouldn't care because I don't really care like what the primary key is. I just care that it exists. But then because I have it cached on these player pages, I really, really do care what the primary key is. And because I need the primary key to actually agree with what it is on the data page, because I'm actually joining these things together.

and people aren't going to be updating the cache on the player page if they don't think that they edited the row because rearranging isn't actually editing and people aren't going to realize that. And again, this is burden of knowledge. People can't, I can't make them know that because they have to feel safe to make any edits.

It's bad enough that they have to know that they have to click this button to update the cache after making an edit in the first place. so, the auto increment isn't enough, so it has to be like an auto increment, but only within the set of rows that incorporate that one player. And then rearranging is pretty safe because they'd have to rearrange two pieces of news, including the same player.

And that's really unlikely to happen. It's really unlikely that someone's going to flip the order of two pieces of news that involve the same player without realizing that they're actually are editing that single player except maybe they are. So then I include the team in that also. So they'd have to rearrange two pieces of news, including the same player and the same team.

And that's like unlikely to happen in the first place. And then like, maybe a mistake happens like once a year. And at the end of the day, the thing that really saves us is that we're a wiki. We're not an official source. And so if we have a mistake once a year, like no one cares really. So we're not going for like five nines or anything.

We're going for like, you know, two (laughs) . Um, so 

[00:57:28] **Jeremy:** so 

[00:57:28] **Megan:** We were having like mistakes constantly until I added player and team and date to the set of things that I was auto incrementing against. and once I got all of those, it was pretty stable.

[00:57:42] **Jeremy:** And for the caching part, so when you're making a cargo query or a SQL query on one page and it needs to join on or get data from another page, it goes to this cache that you have instead of going directly to the actual table in the database. And the only way to get the right data is for the editor to click this button on the website that tells it to update the cache did I get that right? 

[00:58:23] **Megan:** Not quite. So it, well, or Yes, you did sort of, it goes to the actual table. The issue here is that, the table was last updated, the last time that a page was saved. And the last time the data got saved was the last time that the page that contains the parser function that generates those rows got saved.

So, let me say that again. So, some of the data is being saved from the data page where the users manually enter it, and that's fine because the only time that gets updated is when the users manually enter it and then the page gets saved. But then these tenures tables are stored by my lua code on the player pages, and those aren't going to get updated unless the player page gets blank edited or null edited, or a save action happens from the player page.

And so the way to make a, an edit happen from the player page is either to manually go there and click edit, and then click save, which is called a blank edit because. Blank edited, you didn't do anything but you pressed save or to use my JavaScript gadget, which is clicking a button from the data page that just basically does that for you using the api.

And then that's going to update the table and then the database table, because that's where the, the cargo parser function is that writes to the database and updates the tables there. with the information, Hey, the primary key changed, because that's where the parser function is physically located in the wiki because one of them is on the data page and one of them is on the player page.

So you get this disconnect in the cache where it's on two different pages and so you have to press a save action in both of them before the table is consistent again.

[01:00:31] **Jeremy:** Okay. It be, it's, so this is really all about the tenure table, which the user will never mod or the editor will never modify directly. You need your code running on the data page and the player's page to run, to update the The tenure table? 

[01:00:55] **Megan:** Yeah, exactly.

[01:00:57] **Jeremy:** yeah, it's totally hidden that this exists to the editor, but it's something that, that you as the person who put this all together, um, have to always be aware of, yeah.

[01:01:11] **Megan:** Right. So there was just so many things like this, where you just had to press this one button. I call it refresh overview because originally it was on a tournament page and you had to press, the refresh overview button to purge the cache on the overview page of the tournament. after editing the data and you would refresh, overview, to deal with this cache lag.

And everyone knew you have to refresh overview, otherwise none of your data entry is gonna like, be worth anything because it's not, the cache is just gonna lag. but every editor learned, like if there's a refresh overview button, make sure you press the refresh overview button, , otherwise nothing's gonna happen.

Um, and there is just like tons of these littered across the Wiki. and like to most people, it just like, looks like a simple little button, but like so many things happen when you press this button. 

so it is, it is very important.

[01:02:10] **Jeremy:** Are there, no ways inside of media wiki to if somebody edits one page, for example, to force it to go and, do, I forget what you called it, like a blank save or blank edit on another page?

[01:02:27] **Megan:** So that wouldn't even really work because, we had 11,000 player pages. And you don't know which one the user just edited. so it, it's unclear to MediaWiki what just happened when the user just edited some part of the data page. and like the whole point here is that I can't even blank edit every single player page that the data page links to because the data page probably links to, I don't know, 200 different player pages.

So I wanna link, I wanna blank it like the five that this one news line links to. so I do that, through like HTML attributes, in the JavaScript, 

[01:03:14] **Jeremy:** Oh, so that's why you're using JavaScript so that you can tell what the person edited because there isn't really a way to know natively in, in MediaWiki. what just changed? 

[01:03:30] **Megan:** there's like a diff so I could, like, MediaWiki knows the characters that got changed, but it doesn't really know like semantically what happened. So it doesn't know, like, oh, a link to this just got edited and especially because, I mean it's like templates that got edited, not really like the final HTML or anything.

So Media Wiki has no idea what's going on. so yeah, so the JavaScript, uh, looks at the HTML attributes and then runs a couple API queries, and then the blank edits happen and then a couple purges after that so that the cache gets purged after the blank edit.

[01:04:08] **Jeremy:** Yeah. So it, it seems like on these Wiki pages, you have the html, you have the CSS you have the ability to describe these data pages, which I, I guess in the end, end up being rows in in SQL. And then finally you have JavaScript. So it kind of seems like you can do almost everything in the context of a a Wiki page.

You have so many, so

many of these tools at your, at your disposal.

[01:04:45] **Megan:** Yeah. Except write es6 code. 

[01:04:48] **Jeremy:** Oh, still, still only es5. 

[01:04:52] **Megan:** Yeah, 

[01:04:52] **Jeremy:** Oh no. do, do you know if that's something that they are considering changing or

[01:05:01] **Megan:** There's a Phabricator ticket open. 

[01:05:05] **Jeremy:** How, um, how, how many years? 

[01:05:06] **Megan:** It has a lot of comments, oh a lot of years. I think it's since like 2014 or something 

[01:05:14] **Jeremy:** Oh yeah. I, I guess the, the one maybe, well now now the browsers all, all support es6, but I, I guess one of the things, it sounds like media wiki, maybe side stepped is the whole, front end ecosystem in, in terms of node packages and build tools and things like that. is, is that right? It's basically you can write JavaScript and there, yeah, 

[01:05:47] **Megan:** You can even write jQuery. 

[01:05:49] **Jeremy:** Oh, okay. That's built in as well.

[01:05:52] **Megan:** Yeah .So I have to admit, like my, my front end knowledge is like a decade out of date or something because it's like what MediaWiki can do and there's like this entire ecosystem out there that I just like, don't have access to. And so I like barely know about. So I have this like side project that uses React that I've like, kind of sort of been working on.

And so like I know this tiny little bit of react and I'm like, why? Why doesn't MediaWiki do this? 

Um, they are adding Vue support. So in theory I'll get to learn vue so that'll be fun.

[01:06:38] **Jeremy:** So I'm, I'm curious, just from the limited experience you've had, outside of, 

MediaWiki, are, are there like specific things, uh, in your experience working with React where you're, you really wish you had in inside of Media Wiki? 

[01:06:55] **Megan:** Well, really the big thing is like es6, like I really wish we could use arrow functions , like that would be fantastic. Being able to build components would be really nice. Yeah, we can't do that.

[01:07:09] **Jeremy:** I, I suppose you, you've touched a little bit on performance before, but I, I guess that's one thing about Wikis is that, putting what's happening in the back end, aside the, the front end experience of Wikis, they, they feel pretty consistent since they're generally mostly server rendered.

And the actual JavaScript is, is pretty light, at least from, from Wikis I've seen. 

[01:07:40] **Megan:** Yeah. I mean you can add as much JavaScript as you want, so I guess it depends on what the users decide to do. But it's, it's definitely true that wikis tend to load faster than some websites that I've seen.

[01:07:54] **Jeremy:** Yeah, I mean, I guess when you think of a wiki, it's, you're there cuz you wanna get specific information and so the goal is not to necessarily reproduce like some crazy complex app or something. It's, It's, to get you the, the, information. Yeah.

[01:08:14] **Megan:** Yeah. No, that's actually one thing that I really like about Wikis also is that you don't have the pressure to make them look nice. I know that some people are gonna hear that and just like, totally cringe and be like, oh my God, what is she saying? ? Um, but it's actually really true. Like there's an aesthetic that Wikis and Media Wiki in particular have, and you kind of stick to that.

And within that aesthetic, I mean, you make them look as nice as you can. Um, and you certainly don't wanna like, make them deliberately ugly, but there's not a pressure to like go over the top with like marketing and branding and like, you know, you, you just make them look reasonably nice. And then the focus is on the information and the focus is on making the information as easy to understand as possible.

And a wiki that looks really nice is a wiki that's very understandable and very intuitive, and one where you. I mean, one, that the information is the joy and, you know, not, not the presentation, I guess. So it's like the presentation of the information instead of the presentation of the brand. so I, I really appreciate that about wikis. 

[01:09:30] **Jeremy:** Yeah, that's a good point about the aesthetics in the sense of like, they have a certain look and yeah, maybe it's an authoritative look, , which, uh, is interesting cuz it's, like a, a wiki that I'll, I'll commonly go to for example, is there's the, the PC gaming Wiki. And when you look at how it's styled, it feels like very dated or it doesn't look like, I guess you could say normal webpages, but it's very much in line with what you expect a wiki to look like.

So it's, it's interesting how they have that, shared aesthetic, I guess. 

[01:10:13] **Megan:** Yeah. yeah. No, I really like it. The Wiki experience, 

[01:10:18] **Jeremy:** We, we kind of touched on this near the beginning, but sometimes when. I would see wikis and, and projects like Leaguepedia I would kind of wonder, you know, what's the decision between or behind it being a wiki versus something being like a custom CMS in, in the case of Leaguepedia but, you know, talking to you about how it's so, like wikis are structured so that people can contribute.

and then like you were saying, you have like this consistent look that brings the data to the user. Um, I actually, it gives me a better understanding of why so many people choose wikis as, as ways to present this information. 

[01:11:07] **Megan:** Yeah, a a lot of people have asked me over the years why, why MediaWiki when it always feels like I'm jumping through so many hoops. Um, I mean, when I just described the caching thing to you, and that's just like one of, I don't know, dozens of struggles that I've had where, MediaWiki has gotten in the way of what I need to do.

Because really Leaguepedia is an entire software layer on top of MediaWiki, and so you might ask why. Why MediaWiki? Why not just build the software layer on top of something easier? And my answer is always, it's about the community. MediaWiki lends itself so well to community and people enjoy contributing to wikis and wikis. Wikis are just kind of synonymous with community, and they always have been. And Wikipedia sort of set the example when they launched, and it's sort of always been that way. And, you know, I feel like I'm a part of a community when I say a Wiki. And if it was just if it were a custom site that had the ability to contribute to it, you know, it just feels like it's not the same.

[01:12:33] **Jeremy:** I think just even seeing the edit button on Wikis is such a different experience than having the expectation, well, I guess in the case of Leaguepedia, you do have to create an account, but even without creating the account, you can still click edit and you can look at the source and you can see how all this information, or a lot of it, how it got filled in.

And I feel like it's kind of more similar to the earlier days of webpages where people could right click a site and click view source and then look at the HTML and the css, and kind of see how it was put together. versus, now with a lot of sites, the, the code has been minified or there's build tools involved so that when you look at view source on websites, it just looks crazy and you're not sure what's going on.

So I, I, I feel like wikis in some ways are, kind of closer to the, the spirit of, like the earlier H

T M L sites. Yeah. 

[01:13:46] **Megan:** And the knowledge transfers too. If you've edit, if you've, if you've ever edited Wikipedia, then you know that like open bracket, open bracket, closed bracket. Closed bracket is how you link a page. and that knowledge transfers to admittedly maybe a little bit less so for Leaguepedia, since there, you need to know how all the templates work and there's not so much direct source editing.

it's mostly like clicking the CharInsert prefills. but there's still a lot of cross knowledge transfer, if you've edited one wiki and then change to editing another. And then it goes the other way too. If you edit Leaguepedia, then you want to go at it for the Zelda Wiki, that knowledge will transfer.

[01:14:38] **Jeremy:** And, and talking about the community and the editors. I, I imagine on Wikipedia, most of the people editing are volunteers. Is it the same with Leaguepedia in your experience? 

[01:14:55] **Megan:** Um, yeah, so I was contracted, uh, or I was not contracted. My LLC was contract and then I subcontracted. Um, it changed a bit over the years, um, as people left. Uh, so at first I subcontracted quite a few people. Um, and then I guess, as you can imagine, as, there was a lot more data entry that had to be done at the start.

And less had to be done later on, as I, expanded the code base so that it was more a single source of truth, and less stuff had to be duplicated. And I guess it was, it probably became a lot more fun too, uh, when you didn't have to edit, enter the same thing multiple times. but, uh, a bunch of people, uh, moved on over the years.

and so by the end I was only subcontracting, three people. Um, and everyone else was volunteer.

[01:15:55] **Jeremy:** And and the people that you were subcontracting, that was for only data entry, or was that also for the actual code?

[01:16:05] **Megan:** No, that wasn't for data entry at all. Um, and actually that was for all of my wikis, uh, because I was. Managing like all of the eSports wikis. or one of them was for Call of Duty and Halo, uh, to manage those wikis. One of them was for, uh, just the Call of Duty Wiki. and then one of them was for Leaguepedia to do staff onboarding.

Oh 

[01:16:28] **Jeremy:** okay. So this is, um, this is to help people contribute to all of these wikis. That's, that's what these, these, uh, subcontractors we're focusing on. 

[01:16:41] **Megan:** Yeah, 

[01:16:44] **Jeremy:** I guess that, that makes sense when we've been talking about the complexity, uh, what's behind Leaguepedia, but there's a lot that the editors, it sounds like, have to learn as well to be able to know basically where to go and how to fill everything out and Yeah. 

[01:17:08] **Megan:** So basically, for the major leagues, in League of Legends, um, we required some onboarding before you could cover them because we wanted results entered within like, about one to four minutes. of the game centering, or sorry, of the games ending. Um, so that was like for North America, Korea, China, Europe, and for the, like for some regions, like the really minor ones, like second tier leagues in, like for example the national leagues in Europe, second tier or something, we kind of didn't really care if it was entered immediately.

And so anyone who wanted to enter could just enter, uh, information. So we did want the experience to be easy enough that people could figure it out on their own. and we didn't really, uh, require onboarding for that. There was like a gradation of how much onboarding we required. But typically we tried to give training as much as we could.

Um, it, it was sort of dependent on how fast people expected the results and how available someone was to provide training. so like for Latin America, there was like a lot of people who were available to provide trainings. So even like the more minor leagues, people got training there. for example, But yeah, it was, it was very collaborative.

and a lot of people, a lot of people got involved, so, yeah. 

[01:18:50] **Jeremy:** And in terms of having this expectation of having the results in, in just a few minutes and things like that, is it, where are, are these people volunteers where they would volunteer for a slot and then there was just this expectation? Or how did that work? 

work 

[01:19:09] **Megan:** Yeah. So, um, a lot of people volunteered with us as resume experience to try and get jobs in eSports. Um, and some people just volunteered with us because they wanted to give back to the community because, we're like a really valuable resource for the community. And I mean, without volunteer contribution we wouldn't have existed.

So it was like understood that we needed people's help in order to continue existing. So some people, volunteered for that reason. Some people just found it fun to help out. so there's like a range of reasons to contribute.

[01:19:46] **Jeremy:** And, and you were talking about how there's some people who they, they really need this data in, in that short time span. you know, who, who are we talking about here? Are these like commentators? Are these journalists? I'm just curious who's, who's,

looking for this in such a short time span 

[01:20:06] **Megan:** Well, fans would look for the data immediately. sometimes if we entered a wrong result, someone would like come into our discord and be like, Hey, the result of this is wrong. you know, within seconds of the wrong result going up. So we knew that people were like looking at the Wiki, like immediately.

But everyone used the data, commentators at Riot. journalists. Fans, yeah. like everyone is using it.

[01:20:33] **Jeremy:** and since it's so important to, like you're mentioning Riot or the tournament organizers, things like that. What kind of relationship do you have with them? Do they provide any kind of support or is it mostly just, it's something they just use 

[01:20:54] **Megan:** I, so there is, um, I definitely talk to people at Riot pretty regularly. and we. we got like resources from them, so, they'd give us player photos to put up, and like answers to questions and stuff. but for the most part it was just something that they'd use.

[01:21:15] **Jeremy:** and, and so like now that unfortunately your, your contract wasn't renewed with Leaguepedia like where do you, I guess see the, the future of Leaguepedia but, but also all these other eSports wikis going, is this something that's gonna be more just community driven or, I'm, I guess I'm trying to understand, you know, how this, the gap gets filled.

[01:21:47] **Megan:** Yeah, I'm, I'm not sure. Um, they're doing an update to Media Wiki 1.39 next year. we'll see if stuff majorly breaks during that. probably no one's gonna be able to fix it if it does. Who knows? (laughs) um, yeah, I don't know. There's another site that hosts, uh, eSports wikis called Liquipedia

um, so it's possible that they'll adopt some of the smaller wikis. Um, I think it's pretty unlikely that they'll want to take Leaguepedia, um, just because it's too complicated of a wiki. but yeah, I, I, I don't know.

[01:22:31] **Jeremy:** it kind of feels like one of these things where I guess whoever is in charge of making these decisions may not fully understand the implications or, or what it takes to, to run such a, a large wiki. yeah, I guess it'll be interesting to, to see if it ends up being like you said, one, one big mess. 

[01:22:58] **Megan:** Yeah. I got them through the 1.37 upgrade by submitting like three or four patches to cargo, during that time and discovering that the patches needed to be made prior to the upgrade happening. So, you know, I don't think that they're going to update cargo during the 1.39 upgrade and it's cargo changes that have the biggest disruption.

So they're probably safe from that. and, and I don't think 1.39 has any big parser changes. I think that's later, but yeah, there'll probably still be like a bunch of CSS changes and who knows if anyone's going to fix the follow up from that. 

So, yeah, we'll see.

[01:23:46] **Jeremy:** Yeah, that's, um, that's kind of interesting to know too that, these upgrades to MediaWiki and, and to extensions like cargo, that they change so significantly that they require pull requests. Is that, like, is that pretty common in terms of when you do an upgrade of a MediaWiki that there there are these individual things you need to do and it's not just update package. 

[01:24:18] **Megan:** well the cargo change was the first time that we had upgraded in like two and a half years or something. so that one in particular, I think it was expected that that one wasn't going to go so smoothly. generally updates go not that badly. I say with rising intonation, (laughs) , um, if you keep up to date with stuff, it's generally pretty okay.

Cargo is probably one of the less stable ones just because it's a relatively small contributor base, and so kind of crazy things happen sometimes. Um, Semantic Media Wiki is a lot more stable. Uh, but then the downside is that if you have a feature request for SMW it's harder to get pushed through.

But cargo still changes a lot. The big change with cargo, like the big problematic change with cargo was a tiny bug fix that just so happened to change every empty string value to nil in Lua, 

You know, no big deal or anything, whatever.

[01:25:42] **Jeremy:** That, that's, uh, that's a good one right there. 

[01:25:47] **Megan:** I mean,

I I don't know how no one noticed this for like a year and a half or something man, 

It was a tiny bug fix. 

[01:26:02] **Jeremy:** Mm. 

[01:26:03] **Megan:** Like it was checked in as a bug fix and it really was a bug fix. I tracked down the guy who made the patch and I was like, I can't reproduce this bug. Can I just revert it? And he was like, I can't reproduce it either. 

[01:26:21] **Jeremy:** Oh, wow. (laughs) 

[01:26:23] **Megan:** And I was like, well, that's great. And I ended up just leaving it in, but then changing them back to empty string.

Um, when the extension was first released, null database values were sent to Lua as empty string due to a bug in the first place. Because null databases, null database values should just be nil in Lula. Like, come on here, . But they were sent as empty string.

And so for like five years, people were writing code, assuming that you would never get a nil value for anything that you requested from the database. So you can't make a breaking change like that without putting a config value that defaults to true. 

[01:27:10] **Jeremy:** Yeah. 

[01:27:11] **Megan:** So I added a legacy, nil value, legacy Lua, nil value as empty string config value or something, and, defaulted it to true and wrote in the documentation that it was recommended that you set it to false.

Or maybe I defaulted it to false. I, I don't remember what I set the default to, but I wrote in the documentation something about how you should, if possible, set this to false, but if you have a large code base, you probably need this . And then we set up Platform Ride to True, and that's the story of how I saved the shit out of our 1.37 upgrade this year.

[01:27:57] **Jeremy:** Oh yeah, that's, um, that's a rough one. Changing, changing people's data is very scary. 

[01:28:05] **Megan:** Yeah, I mean, it was totally unintended. and I don't know how no one noticed this either. I mean, I guess the answer is that not very many people do the kind of stuff that I do working with Lua and Cargo in this much depth. but a fairly significant number of fandom Wikis do, and this would've just been an absolute disaster.

And the semi ironic thing is that, I, I have a wrapper that fixes the initial cargo bug where I detect every empty string value and then cast it to nil after I get my data from cargo. So I would've been completely unaffected by this. And my wiki was the primary testing wiki for cargo on the 1.37 patch. So we wouldn't have caught this, it would've gone to live

[01:28:56] **Jeremy:** Wow. 

[01:28:58] **Megan:** So we got extremely lucky that I found out about this ahead of time prior to us QAing and fixed this bug

because it would've gone straight to live. 

[01:29:10] **Jeremy:** that's wild yeah, it's just like kind of catastrophic, right? It's like, if it happens, I feel like whoever is managing the wikis is gonna be very confused. Like, why, why is everything broken? I don't, I don't understand. 

[01:29:25] **Megan:** Right? And this is like so much broken stuff that it's like very difficult to track down what's going on. I actually had a lot of trouble figuring out what was wrong in the code base. 

Causing this error. And I submitted an incorrect patch at first, and then the incorrect patch got merged, and then I had to like roll back the incorrect patch.

And then I got a merge conflict on the incorrect patch. And it, it was, it was bad. It took me three patches to get this right. 

Um, But eventually, eventually I got there.

[01:30:02] **Jeremy:** Yeah. that's software, I guess , 

[01:30:06] **Megan:** Yeah. 

[01:30:07] **Jeremy:** the, the, the thing you were trying to avoid all these years. 

[01:30:10] **Megan:** Yeah, 

[01:30:13] **Jeremy:** you're in it now.

[01:30:14] **Megan:** It really was, that was actually the reason that I went in, I got into the Wiki in the first place, um, and into e-sports. Uh, was that after Caltech, I wanted to like get away from STEM altogether. I was like, I've had enough of this. Caltech was too much, get me away, (laughs) . 

And I wanted to do like event management or tournament organization or something.

And so I wanted to work in eSports. and that was like my life plan. And I wanted nothing to do with STEM and I didn't wanna work in software. I didn't wanna do math. I was a math major. I didn't wanna do math. I didn't wanna go to grad school. I wanted absolutely nothing to do with this. So that was my plan.

And somehow I stumbled and ended up in software. 

[01:31:02] **Jeremy:** Well, at least you got the eSports part. 

[01:31:05] **Megan:** Yeah, so that, that worked out. And really for the first couple of years I was doing like community management and social media and stuff. 

Um, and I did stay away from software for about the first two years, so it lasted about two whole years. 

[01:31:24] **Jeremy:** What ended up pulling you in? 

[01:31:26] **Megan:** Um, actually, so when, when I signed back with Gamepedia, our developer just sort of disappeared and I was like, well, shit, I guess that's me now. (laughs) 

So we had someone else writing all of our templates for a couple years, so I was able to just like make a lot of feature requests. and I'm very good at making feature requests.

If, if I ever have like, access to someone else who's writing code for me, I'm like, fantastic at just making a ton of like really minor feature requests, and just like taking off all of their time with like a billion tiny QA issues. 

[01:32:09] **Jeremy:** You you are the backlog, 

[01:32:12] **Megan:** Yeah, I really, um, I, there's another OSS project that I've been working on, um, which is a Discord bot and. We, our, our backlog just expands and expands and

[01:32:26] **Jeremy:** Oh yeah. You know what, I, I think I did look at that. I, I looked at the issues and, usually when you look at a, the issues for an open source project, it's, it's all these people using it, right? That are like, uh, there's this thing I want, but then I looked and it was all, it was all you. So I guess that's okay cuz you're, you're in the position to do something about it. 

[01:32:47] **Megan:** The, the part that you don't know is that I'm like constantly begging other people to open tickets too. 

[01:32:53] **Jeremy:** Really? 

[01:32:55] **Megan:** Yeah. Like constantly. I'm like, guys, it can't just be me opening tickets all the time. 

[01:33:04] **Jeremy:** Yeah. Yeah. If it was, if it was someone else's project, I would be like, oh, this is, uh, . 

I don't know about this. But when it's your own, you know, okay. It's, it's basically like, um, it's like a roadmap I guess.

[01:33:20] **Megan:** Yeah. Some of them have been open for, for quite a long time, but actually a couple months ago we closed one that had been open since, I think like April, 2020. 

[01:33:31] **Jeremy:** Oh, nice. 

[01:33:32] **Megan:** That was quite an event.

[01:33:34] **Jeremy:** Yeah, it's open source, So you can do whatever you want, right. (laughs) 

[01:33:41] **Megan:** We even have a couple good first issues that are actually good first issues. 

[01:33:46] **Jeremy:** Yeah. Not, not getting any takers? 

[01:33:49] **Megan:** No, we sometimes do. Yeah. I actually, we, so some of them are like semi-important features, but I like feel really bad if I ever do the good first issues myself because like somewhere else could do them. And so like, if it's like a one line ticket, I would just, I feel so much guilt for doing it myself. 

[01:34:09] **Jeremy:** Oh, I see what you mean. 

[01:34:10] **Megan:** I'm like, Yeah. so I just like, I can't do them. But then I'm like, oh, but this is really important. But then I'm like, oh, but we might get someone else who, and I just, I never know if I should just take the plunge and do it myself, so. 

[01:34:22] **Jeremy:** yeah. No, that's, that's a good point. It's, it's like, like these opportunities, right. For people to, and it could, it could make a big difference for them. And then for you, it's like, I could do this in 10 minutes or whatever. , 

Uh, I, I guess it all depends on how annoyed you are by the thing not being there,

[01:34:43] **Megan:** Right. I know because my entire background is like community and getting new people to onboard and like the potential new contributor is worth like 10 times, like, The one PR that I can make. So I should just like absolutely leave it open for the next year. 

[01:35:02] **Jeremy:** Yeah. Yeah, no, that's a, that's a good way of, of looking at it. I mean, I I think when you talk about open source or, or even wikis, that that sort of community aspect is, is so, so important, right? Because if it's just, if it's just one person, then I mean, it kind of, it lives or dies with the one person, right?

It, it's, it's so different when you actually get a bunch of people involved. And I think that's something like a lot of, a lot of projects struggle with

[01:35:38] **Megan:** Yeah. That's actually, as much as I'm like bitter about the fact that I was let go from my own project, I think the thing that I should, in a sense be the most proud of is that I grew my project to a place where that was able to happen in a sense. Like, I built this and I built it to a place where it was sustainable.

Although, we'll see how sustainable it was, (laughs) . but like I'm not needed for the day to day. and that means that like I successfully built a community.

[01:36:18] **Jeremy:** Yeah, no, you should be really proud about that because it's, it's not only like the, the code, right? Like over the years it sounds like you gradually made it easier and easier to contribute, but then also being able to get all these volunteers together and build a community on the discord and, and elsewhere.

Yeah, no, I think that's, I think that's really great to be able to, to do, do something like that. 

[01:36:50] **Megan:** Thanks. 

[01:36:53] **Jeremy:** I think that's, that's a good place to, to wrap up, but is there anything else you wanted to, to mention or do you want to tell people where to check out, uh, what you're up to?

[01:37:05] **Megan:** Yeah, I, I have a blog that's a little bit inactive for the past couple months, because I recently had surgery, but I, I've been saying for like five weeks that I will start, posting there again. So hopefully that happens soon. Uh, but it's river.me, and so you can check that out.

[01:37:27] **Jeremy:** Cool. Well, yeah, Megan, I just wanna say thanks for, for taking the time. This was, this was really interesting. the world of wikis is like this, it's like a really big part of the internet that, um, I use wikis, but I, I've never really understood kind of what's going on in, in terms of the actual technology and the community. so so thank you for, for sharing that. 

[01:37:53] **Megan:** Yeah. Thanks so much for having me. 

</div>