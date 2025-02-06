+++
title = "Tom Macwright on Shutting down Placemark"

description = "Challenges running a bootstrapped solo business"

[extra]
episode_url = "https://pinecast.com/listen/be669bcb-838b-4d14-93d2-bc211d77f314.mp3"
social_title = "Tom Macwright on Shutting down Placemark"
social_description = "Challenges running a bootstrapped solo business"
+++

Tom MacWright is a prolific contributor in the geospatial open source community. He made geojson.io, Mapbox Studio, and was the lead developer on the OpenStreetMap editor. He's currently on the team at [Val Town](https://www.val.town).

In 2021 he bootstrapped a solo business and created the Placemark mapping application.

He acquired customers and found steady growth but after spending two years on the project he decided it was financially unsustainable. He open sourced the code and shut down the business.

In this interview Tom speaks candidly about why geospatial is difficult, chasing technical rabbit holes, the mental impact of bootstrapping, and his struggles to grow a customer base.

If you're interested in geospatial or the good and bad of running a solo business I think you'll enjoy this conversation with Tom.


## Related Links

- [Tom's blog](https://macwright.com)
- [Placemark Play](https://play.placemark.io)
- [Placemark GitHub](https://github.com/placemark/placemark)
- [Placemark archive](https://www.placemark.io)
- [geojson.io](https://geojson.io)
- [Valtown](https://www.val.town)
- [Datawrapper (Visualization tool)](https://www.datawrapper.de)

## Geospatial Companies mentioned
- [Mapbox](https://www.mapbox.com)
- [ArcGIS](https://www.arcgis.com)
- [QGIS](https://qgis.org)
- [Carto](https://carto.com)

--

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

# [00:00:00] Introduction

**Jeremy:** Today I'm talking to Tom MacWright. He worked at Mapbox as a, a very early employee. He's had a lot of experience in the geospatial community, the open source community. One of his most recent projects was a mapping project called Placemark he started and ran on his own.

So I wanted to talk to Tom about his experience going solo and, eventually having to, shut that down. Tom, thanks for agreeing to chat today.

**Tom:** Yeah, thanks for having me.


## [00:00:32] Tools and Open Source at Mapbox

**Jeremy:** So maybe to give everyone some context on, what your background was before you started Placemark. Um, let's talk a little bit about your experience at, at Mapbox. What did you work on there and, and what would you say are like the big things you learned from that experience?

**Tom:** Yeah, so if you include the time that I was at Development Seed, which essentially turned into Mapbox, I kind of signed the paper to get fired from Development Seed and hired at Mapbox within the same 20 seconds. Uh, I was there for eight and a half years. so it was a lifetime in tech years. and the company really evolved from, uh, working for Human Rights Watch and Amnesty International and the World Bank and doing these small, little like micro websites to the point at which I left it.

It had. Raised a lot of money, had a lot of employees. I think it was 350 or so when I left. and yeah, just expanded into a lot of different, uh, try trying to own more and more of the mapping stack. but yeah, I was kind of really focused on the creative and tooling side of it. that's kind of where I see a lot of the, the fun and programming is making these tools where, uh, they can give people the same kind of fun like interaction loop that programming has where you, you know, you do a little bit of math and you see the result and you're able to just play with, uh, what you're working on, letting people have that in other domains.

so it was really cool to figure out how to get A map design tool where somebody changes the background color and it just automatically changes that in your browser. and it covered like data editing. It covered, um, map styling and we did, uh, three different versions of that tool over the years.

and then Mapbox is also a company that was, it came from, kind of people who are working on the Howard Dean campaign. And so it was pretty ideological and part of the ideology was being pretty hardcore about open source. we hired a lot of people who were working on open source projects before and basically just paid them to work on the open source projects, uh, for their whole time there.

And during my time there, I just tried to make as much of my work, uh, open as possible, which was, you know, at the time it was, it was pretty great. I think in the long term it's been, o open source has changed a lot. but during the time that we were there, we both kind of, helped things like leaflet and mapnik and openstreetmap, uh, but also made like some larger contributions to the open source world.

yeah, that, that's kind of like the, the internal company facing side. And also like what I try to create as like a more of a, uh, enduring work. I think the open source stuff will hopefully have more of a, a long term, uh, benefit.

## [00:03:40] How open source has changed (value capture by large companies)

**Jeremy:** When I was working on a project that needed offline maps, um, we couldn't use Google Maps or any of the, the other publicly available, cloud APIs. So yeah, we actually used a, a tool, called Tile Mill that I, I hadn't known that you'd worked on, but recently found out you did.

So that actually let us pull in OpenStreetMap data and then use this style, uh, language called carto to, to basically let us choose what the colors would be and how the different, uh, the roads and the buildings would look. What's kind of interesting to me is that it being open source really let us, um, build something we otherwise wouldn't have been able to do.

But like, at the same time, we also didn't pay Mapbox any money. (laughs) So I'm, I'm kind of curious, like, if it's changed, like what the thinking was in terms of, you know, we pay for people to build all these things. We make it open source. but then people may just not ever pay us, you know, for all these things we did.

**Tom:** Yeah. Yeah. I think that the main thing that's changed since the era of tilemill is, the dominance of cloud platforms. Like back then, I think, uh, Mapbox was still using, we were using like a little bit of AWS but people were still just on like VPSs and, uh, configuring things in cPanel and sometimes even running their own servers.

And the, the danger of people using the product for free was such a small thing for us. especially when tile Mill was also funded by the Knight Foundation, so, you know, that at least paid half of my salary for, or, well, sorry, probably, yeah, maybe half of my salary for the first year that I was there and half of three other people's salaries.

but that, yeah, so like when we built Tile Mill, a few companies have really like built on those same tools. Uh, there's a company called Carto coincidentally, they had the same name as Carto CSS, and they built on a lot of the same stack they built on mapnik. Um, and it was, was...

I mean, I'm not gonna say that it was all like, you know, sunshine and roses, but it was never a thing that we talked about in terms of like this being a brutal competition between us and these other startups.

Mapbox eventually closed source some stuff. they made it a source available license. and eventually Mapbox Studio was a closed source product. Um, and that was actually a decision that I advocated for. And that's mostly just because at one point, Esri, Microsoft, Amazon, all had whitelisted versions of Mapbox code, which, uh, hurts a little bit on a personal level and also makes it pretty hard to think about.

working almost like it. You don't want to go to your scrappy open source company and do unpaid labor for Amazon. Uh, you know, Bezos can afford to pay for the labor himself. that's just kind of my personal, uh, that I'm obviously, I haven't worked there in a long time, so I'm not speaking for the company, but that's kind of how it felt like.

and it yeah, kind of changed the arithmetic of open source in this way that. It made it less fun and, more risky, um, for people I think.


## [00:07:11] Don't worry about the small free users

**Jeremy:** Yeah. So it sounds like the thinking was if someone on a small team or an individual, they took the open source software and they used it for their own projects, that was fine. Like you expected that and didn't worry about it. It's more that when these really large organizations like a, a Microsoft comes in and, just like you said, white labels the software, and doesn't really contribute significantly back.

That's, that's when it, the, the thinking sort of shifted.

**Tom:** Yeah, like a lot of the people who can't pay full price in USD to use your product are great users and they're doing cool stuff. Like when I was working on Placemark and when I was like selling. The theme for my blog, I would get emails from like some kid in India and it's like, you know, you're selling this for a hundred dollars, which is a ton of money.

And like, you know, why, why should I care? Why shouldn't I like, just send them the zip file for free? it's like nothing to me and a lot to them. and mapping tools are really, really expensive. So the fact that Mapbox was able to create a free alternative when, you know, ArcGIS was $500 a month sometimes, um, depending on your license, obviously.

That's, that's good. You're always gonna find a way for, like, your salespeople are gonna find a way to charge the big companies a lot of money. They're great at that. Um, and that's what matters really for your, for the revenue. 


## [00:08:44] ESRI to Google Maps with little in-between

**Jeremy:** That's a a good point too about like the, my impression of the, the mapping space, and maybe this has changed more recently, but you had the, probably the biggest player Esri, who's selling things at enterprise prices and then there were, or there are like a few open source options. but they feel like the, the barrier to entry feels a little high.

And so, and then I guess you have stuff like Google Maps, right? That's, um, that's very accessible, but it's pretty limited, so. There's this big gap, it feels like right between the, the Esri and the, the Google Maps and open source. It's, it's sort of like, there's almost like there's no sweet spot. guess May, maybe it's just because people's uses are so different, but I'm, I'm not sure, um, what makes maps so unique in that way

**Tom:** Yeah, I have come to understand what Esri and QGIS do as like an extension of what CAD is like. And if you've used CAD software recently, it's just as crazy and as expensive and as powerful. and it's really hard to capture like the people who are motivated enough to make a map but don't want to go down the whole rabbit hole.

I think that was one of the hardest things about Placemark was trying to be in the middle of those things and half of the people were mystified by the complexity and half the people wanted more complexity. Uh, and I just couldn't figure out how to get it to the right in between spot.


## [00:10:25] Placemark and its origins in geojson.io

**Jeremy:** Yeah. So let's, let's talk a little bit about Placemark then, in terms of from its start. What was your, your goal with Placemark and, and what was the product itself?

**Tom:** So the seed of the idea for Placemark, uh, is this website called geojson.io, uh, which is still around. And, Chris Fong (correction -- Whong) at, at Mapbox is still, uh, developing it. And that had become pretty useful for a lot of people who I knew in the industry who were in this position of managing geospatial data but not wanting to boot up ArcGIS uh, geojson.io is based on, I just tweeted, I was like, why?

Why is there not a thing where you can edit data on a map and have a GeoJSON representation and just go Back and forth between the two really easily. and it started with that, and then it kind of grew to be a little bit more powerful. And then it was just a tool that was useful for everyone. And my theory was just that I wanted that to be more useful.

And I knew just like anything else that you build and you work on for a long time, you know exactly how it could be so much better. And, uh, all the things that you would do better if you did it again. And I was, uh, you know, hoping that there was something where like if you make that more powerful and you make it something that's like so essential that somebody's using every day, then maybe there's some some value in that.

And so Placemark kind of started as being like, oh, this is the thing where if you're tasking a satellite and you need a bounding box on a specific city, this is the easiest way to do that. Um, and it grew a little bit into being like a tool for collaborating because people were collaborating on it.

And I thought that that would be, you know, an interesting thing to support. but yeah, I think it, it like tried to be in that middle of like, not exactly Google my Maps and certainly a lot, uh, simpler than, uh, QGIS or ArcGIS

**Jeremy:** something I noticed, so I've actually used geojson.io as well when I was first learning how to put stuff on a map and learning that GeoJSON was a format that a lot of things were using, it was actually really helpful to, to be able to draw, uh, polygons and see, okay, this is how the JSO looks and all that stuff.

And it was. Like just very simple. I think there's something like very powerful about, websites or applications like that where it, it does this one thing and when you go there, you're like, oh, okay, I, I, I know what I'm doing and it's, it's, uh, you know, it's gonna help me do the, this very specific thing I'm trying to do.


## [00:13:16] Placemark use cases (Farming, Transportation, Interior mapping, Satellite viewsheds)

**Jeremy:** I think with Placemark, so, one question I would have is, you gave an example of, uh, someone, I think you said for a satellite, they're, are they drawing the, the area? What, what was the area specifically for?

**Tom:** the area of interest, the area where they want the, uh, to point the camera.

**Jeremy:** so yeah, with, with Placemark, I mean, were there, what were some of the specific customers or use cases you had in mind?

'cause that's, that's something about. Um, placemark as a product I noticed was it's sort of like, here's this thing where you can draw polygons put markers and there's all these like things you can do, but I think unless you already have the specific use case, it's not super clear, who uses it for what.

So maybe you could give some examples of what you had in mind.

**Tom:** I didn't have much in mind, but I can tell you what people, what some people used it for. so some of the more interesting uses of it, a bunch of, uh, farming oriented use cases, uh, especially like indoor and small scale farming. Um, there were some people who, uh, essentially had a bunch of flower farms and had polygons on the map, and they wanted to, uh, mark the ones that had mites or needed to be watered, other things that could spread in a geometric way.

And so it's pretty important to have that geospatial component to it. and then a few places were using it for basically transportation planning. Um, so drawing out routes of where buses would go, uh, in Luxembourg. And, then there was also a little bit of like, kind of interesting, planning of what to buy more or less.

Uh, so something of like, do we want to buy this tract of land or do we wanna buy this tract of land or do we wanna buy access to this one high speed internet cable or this other high speed internet cable? and yeah, a lot of those things were kind of like emergent use cases. Um, there's a lot of people who were doing either architecture or internal or in interior mapping essentially.

**Jeremy:** Interior, you mean, inside of a building 

**Tom:** yeah.

yeah. 

**Jeremy:** Hmm. Okay.

**Tom:** Which I don't think it was the best tool for. Uh, but you know, people used it for that.

**Jeremy:** Interesting. Yeah. I guess, would people normally use some kind of a CAD tool for that, or 

**Tom:** Yeah. Uh, there's CAD tools and there are a few, uh, companies that do just, there's a company that just does interior maps especially of airports, and that's their whole business model. Um, but it's, it's kind of an interesting, uh, problem because most CAD architecture work is done with like a local coordinate system, and you have like very good resolution of everything, and then you eventually place it in geo geospatial space.

Uh, but if you do it all in latitude and longitude, you know, you're, you're moving a door and it's moving the 10th or 12th decimal point, and eventually you have some precision problems.

**Jeremy:** So it's almost like if you start with latitude and longitude, it's hard to go the other way. Right? you have to start more specific and then you can move it into the, the geospatial, uh, area.

**Tom:** Yeah. Uh, that's kind of why we have local projections for towns is that you can do a lot of work just in that local projection. And the numbers are kind of small 'cause your town's small, relatively. 

**Jeremy:** yeah, those are kind of interesting. So it sounds like just anytime somebody wants to, like you gave the example of transportation planning or you want to visually see where things are, like your crops or things like that, and that, that kind of makes sense. I mean, I think if you just think about paper maps, if somebody wants to sketch something out and, and sort of track the layout of something, this could serve the same purpose but be editable.

and like you said, I think it's also. Collaborative so you can have multiple people editing the same, um, map. that makes sense. I think something that I believe I saw on your website is you said though that it was, it's like an editing tool, but it's not necessarily a visualization tool.

Uh, I'm kind of curious what you, what you meant by that.


## [00:17:39] An editing tool that allows you to export data not a visualization tool

**Tom:** Yeah, I, when you say a map, I think there's, people can interpret that as everything from raw data to satellite imagery and raster data. and then a lot of it is like, can I use this to make a choropleth map of the voter turnout in our, in my country? and that placemark did a little bit, but I think that it was, it was never going to be the, the thing that it did super well.

and so, yeah, and also like the, the two things kind of, don't mesh all that well. Like if you have a scale point map and you have that kind of visualization of it and then you're editing the points at the same time and you're dragging around these like gigantic points because this point means a lot of population, it just doesn't really make that much sense.

There are probably ways to square that circle and have different views, but, uh, I felt like for visualizations, I mean partly I just think data wrapper is kind of great and uh, I had already worked for observable at that point, which is also, which I think also does like great visualization work. 

**Jeremy:** Would that be the case of somebody could make a map inside a placemark and then they would take the GeoJSON and then import that into another visualization tool? Is that what you were kind of imagining people would do?

**Tom:** Yeah. Yeah, exactly.

**Jeremy:** And I could see from the customer's perspective, a lot of them, they may have that end, uh, visualization in mind. So they might look for a tool that kind of just does both. Right.

**Tom:** Yeah. Yeah. Certain people definitely, wanted that. And yeah, it was an interesting direction to go down. I think that market was going to be a lot different than the people who wanted to manage and edit data. And also, I, one thing that I had in mind a lot, uh, was if Placemark didn't work out, how much would people be burned?

and I think if I, if I built it in a way that like everyone was heavily relying on the API and embeds, people would be suffer a lot more, if I eventually had to shut it down. every API that you release is really a, a long-term commitment. And instead for me, like guilt wise, having a product where you can easily export everything that you ever did in any format that you want was like the least lock in, kind of.

**Jeremy:** Yeah. And I imagine the, the scope of the project too, you're making it much smaller if you, if you stick to that editing experience and not try to do everything.

**Tom:** Yeah. Yeah. I, the scope was already pretty big. as you can tell from the open source project, it's, it's bigger than I wish it was. the whole time I was really hoping that I could figure out some niche that was much more compact. there's, I forget the name, but there's somebody who has a, an application that's very similar to Placemark in.

Technical terms, but is just a hundred percent focused on planning septic systems. And I'm just like, if I just did this just for septic systems, like would that be a much, would that be 10,000 lines of code instead of 40,000 lines of code? And it would be able to perfectly serve those customers. but you know, that I didn't do enough experimentation to figure that out.

Um, I, that's, I think one thing that I wish I had done a lot more was, pivot and do experiments.

**Jeremy:** that septic example, do you know if it's a, a business in and of itself where it can actually support one person or a staff of people? Or is it, is that market just too small?

**Tom:** I think it's still a solo bootstrapped project. yeah. And it's, it's so hard to tell whether a company's doing well or not. I could ask the person over DM.


## [00:21:58] Built the base technology before going public

**Jeremy:** So when you were first starting. placemark. You were, you were doing it as a solo, developer. A solo entrepreneur, reallyyou worked on it for quite a while, I think before you announced, right? Like maybe a year or so?

**Tom:** Yeah, yeah. Almost, almost a year, I think, maybe, maybe 10 months in the dark.

**Jeremy:** I think that there's, there was a lot of overlap between the different directions that I would eventually go in and. So just building a collaborative editor that can edit map data fairly quickly and checks all the boxes of being able to import and export things, um, that is, was a lot of work. and I mean also I, I was, uh, freelancing during part of it, so it wasn't a hundred percent of my time.

**Tom:** But that, that core, I think even now if I were to build something similar, I would probably still use that work. because that, whether you're doing the septic planning application or you're doing a general purpose kind of map editor or some kind of social application, a lot of that stuff will be in common.

Um, and so I wanted to really get, like, to figure out that problem space and get a few solutions that I could live with. 

**Jeremy:** The base. libraries or technologies you were gonna pick to get the map and have the collaborative aspect. Those are all things you wanted to get settled first. And then you figured, okay, once I have this base, then I can go find the, you know, the, the, the customers or, or find the specifics of what I'm gonna build.

**Tom:** Yeah, exactly.

**Jeremy:** I I think you had said that going forward when you're gonna work on another project, you would probably still start the same way.


## [00:23:51] Geospatial is a tough industry, no public companies

**Tom:** if I was working on a project in the geospatial space, I would probably heavily reference the work that I already did here. but I don't know if I'll go back to, to maps again. It's a tough industry. 

**Jeremy:** Is it because of the, the customer base? Is it because like people don't really understand the market in terms of who actually needs the maps? I'm kind of curious what you feel makes it tough.

**Tom:** I think, well there are no, there are no public mapping companies. Esri is I think one of the 10 largest private companies in the us. but it's not like any of these geospatial companies have ever been like a pure play. And I think that makes it hard. I think maps are just, they're kind of like fonts in a way in which they are this.

Very deep well of complexity, which is absolutely fascinating. If you're in it, it's enough fun and engineering to spend an entire career just working on that stuff. And then once you're out of it, you talk to somebody and you're just like, oh, I work on this thing. And they're like, oh, that you Google maps.

Um, or, you know, I work at a font type like a, you know, a type factory and it's like, oh, do you make, uh, you know, courier in, uh, word. It's really infrastructure, uh, that we mostly take for granted, which is, that's, that means it's good in some ways. but at the same time, I, it's hard to really find a niche in which the mapping component is that, that is that useful.

A lot of the companies that are kind of mapping companies. Like, I think you could say that like Strava and Palantir are kind of geospatial companies, both of them. but Strava is a fitness company and Palantir is a military company. so if you're, uh, a mapping expert, you kind of have to figure out what, how it ties into the real world, how it ties into the business world and revenue.

And then maps might be 50% of the solution or 75% of the solution, but it's probably not going to be, this is the company that makes mapping software. 

**Jeremy:** Yeah, it's more like, I have this product that I'm gonna sell and it happens to have a map as a part of it. versus I'm going to sell you, tools that, uh, you know, help you make your own map. That seems like a, a harder, harder sell.

**Tom:** yeah. And especially pro tools like the. The idea of people being both invested in terms of paying and invested in terms of wanting to learn the tool. That's, uh, that's a lot to ask out of people.


## [00:26:49] Knowing the market is tough but going for it anyways

**Jeremy:** I think the things we had just talked about, about mapping being a tough industry and about there being like the low end is taken care of by Google, the high end is taken care of by Esri with ArcGIS. Uh, I think you mentioned in a blog post that when you started Placemark you, you, you knew all this from the start.

So I'm kind of curious, like, knowing that, what made you decide like, I'm gonna, I'm gonna go for it and, you know, do it anyways.

**Tom:** uh, I, well, I think that having seen, I, like I am a co-founder of val.town now, and every company that I've worked for, I've been pretty early enough to see how the sausage is made and the sausage is made with chaos. Like every company doesn't know what it's doing and is in an impossible fight against some Goliath figure.

And the product that succeeds, if it ever does succeed, is something that you did not think of two or three years in advance. so I looked at this, I looked at the odds, and I was like, oh, these are the typical odds, you know, maybe someday I'll see something where it's, uh, it's an obvious open blue water market opportunity.

But I think for the, for the most part, I was expecting to grind. Uh, you know, like even, even if, uh, the odds were worse, I probably would've still done it. I think I, I learned a lot. I should have done a lot more marketing and business and, but I have, I have no regrets about, you know, taking, taking a one try at solving a very hard to solve problem.

**Jeremy:** Yeah, that's a good point in that the, the odds, like you said, are already stacked against you. but sometimes you just gotta try it and see how it goes,

**Tom:** Yeah. And I had the, like I was at a time where I was very aware of how my life was set up. I was like, I could do a startup right now and kind of burn money for a little while and have enough time to work on it, and I would not be abandoning an infant child or, you know, like all of the things that, all the life responsibilities that I will have in the near future.

Um. So, you know, uh, the, the time was then, I guess,


## [00:29:23] Being a solo developer

**Jeremy:** And comparing it to your time at Mapbox and the other startups and, and I suppose now at val.town, when you were working on Placemark, you're the sole developer, you're in charge of everything. how did that feel? Did you enjoy that experience or was it more like, I, I really wish I had other people to, you know, to kind of go through this with,

**Tom:** Uh, around the end I started to chat with people who, like might be co-founders and I even entertained some chats with, uh, venture capital people. I am fine with the, the day to day of working on stuff alone of making a lot of decisions. That's what I have done in a lot of companies anyway. when you're building the prototype or turning a prototype into something that can be in production, I think that having, uh, having other people there,

It would've been better for my mentality in terms of not feeling like it was my thing.

Um, you know, like feeling detached enough from the product to really see its flaws and really be open to, taking more radical shifts in approach. whereas when it's just you, you know, it's like you and the customers and your email inbox and, uh, your conscience and your existential dread. Uh, and you know, it's not like a co-founder or, uh, somebody to work with is gonna solve all of that stuff for you, but, uh, it probably would've been maybe a little bit better.

I don't know. but then again, like I've also seen those kinds of relationships blow up a lot. and I wanted to kind of figure out what I was doing before, adding more people, more complexity, more money into the situation. But maybe you, maybe doing that at the beginning is kind of the same, you know, like you, other people are down for the same kind of risk that you are. 

**Jeremy:** I'm sure it's always different trade offs. I mean, I, I think there probably is a power to being able to unilaterally say like, Hey, this is, this is what I wanna do, so I'm gonna do it.

**Tom:** Yeah.

## [00:31:52] Spending too much time on multiplayer without a business case

**Jeremy:** You mentioned how there were certain flaws or things you may not have seen because you were so in it.

Looking back, what, what were some of those things?

**Tom:** I think that, uh, probably the, I I don't think that most technical decisions are all that important, um, that it never seems like the thing that means life or death for companies. And, you know, Facebook is still on PHP, they've fought, fixed, the problem with, with money. but I think I got rabbit holed into a few things where if I had like a business co-founder, then they would've grilled me about like, why are we spending?

The, the main thing that comes to mind, uh, is real time multiplayer, real time. It was a fascinating problem and I was so ready to think about that all the time and try to solve it. And I think that took up a lot of my time and energy. And in the long term, most people are not editing a map. At the same time, seeing the cursors move around is a really fun party trick, and it's great for marketing, but I think that if I were to take a real look at that, that was, that was a mistake.

Especially when the trade off was things that actually mattered. Like the amount of time, the amount, the amount of data that the, that could be handled at. At the same time, I could have figured out ways to upload a one gigabyte or two gigabyte or three gigabyte shape file and for it to just work in that same time, whereas real time made it harder to solve that problem, which was a lot closer to what, Paying customers cared about and where people's expectations were?

**Jeremy:** When you were working on this realtime collaborative functionality, was this before the product was public? Was this something you, built from the start?

**Tom:** Yeah. I built the whole thing without it and then added it in. Not as like a rewrite, but like as a, as a big change to a lot of stuff.

**Jeremy:** Yeah, I, I could totally see how that could happen because you are trying to envision people using this product, and you think of something like Google Docs, right? It's very powerful to be typing in a document and see the other cursors and, um, see other people typing.

So, I could see how you, you would make that leap and say like, oh, the map should, should do that too. Yeah.


## [00:34:29] Financial pressures of bootstrapping, high COL, and healthcare

**Tom:** Yeah. Yeah. Um, and, you know, Figma is very cool. Like the, it's, it's amazing. It's an amazing thing. But the Figma was in the dark for way longer than I was, and uh, Evan is a lot smarter than I was. 

**Jeremy:** He probably had a big bag of money too. Right.

**Tom:** Yeah.

**Jeremy:** I, I don't actually know the history of Figma, but I'm assuming it's, um, it's VC funded, right?

**Tom:** Uh, yeah, they're, they're kind of famous for just having, I don't think they raised that much in the beginning, but they just didn't hire very much and it was just like the two co-founders, or two or three people and they just kept building for long time. I feel like it's like well over three years.

**Jeremy:** Oh wow. Okay. I think like in your case, I, I saw a comment from you where you were saying, this was your sole source of income and you gotta pay for your health insurance, and so you have no outside investments. So, the pressures are, are very different I think.

**Tom:** Yeah. Yeah. And that's really something to on, to appreciate about venture capital. It gives you the. Slack in your, in your budget to make some mistakes and not freak out about it. and sadly, the rent is not going down anytime soon in, in Brooklyn, and the health insurance is not going down anytime soon.

I think it's, it's kind of brutal to like leave a job and then realize that like, you know, to, to be admitted to a hospital, you have to pay $500 a month. 

**Jeremy:** I'm, I'm sure that was like, shocking, right? The first time you had to pay for it yourself.

**Tom:** Yeah. And it's not even good. Uh, we need to fix this like that. If there's anything that we could do to fix entrepreneurship in this country, it's just like, make it possible to do this without already being wealthy. Um, it was, it was a constant stress.


## [00:36:29] Growth and customers

**Jeremy:** As you worked on it, and maybe especially as you, after you had shipped, was there a period where. You know, things were going really well in terms of customers and you felt like, okay, this is really gonna work.

**Tom:** I was, so, like, I basically started out by dropping, I think $5,000 in the business bank account. And I was like, if I break even soon, then I'll be happy. And I broke even in the first month. And that was amazing. I mean, the costs were low and everything, but I was really happy to just be at that point and that like, it never went down.

I think that probably somebody with more, uh, determination would've kept going after, after I had stopped. but yeah, like, and also The people who used Placemark, who I actually chatted with, and, uh, all that stuff, they were awesome. I wish that there were more of them. but like a lot of the customers were doing cool stuff.

They were supportive. They gave me really informative feedback. Um, and that felt really good. but there was never a point at which like the, uh, the growth scale looked like, oh, we're going to hit a point at which this will be a sustainable business within a year. I think it, according to the growth when I left it, it would've been like maybe three years until I would've been, able to pay my rent and health insurance and, live a comfortable life in, in New York.

**Jeremy:** So when you mentioned you broke even that was like the expenses into the business, but not for actually like rent and health insurance and food and all that. Okay. Okay. can you say like roughly how much was coming in or how many customers you had?

**Tom:** Uh, yeah, the revenue initially I think was, uh, 1500 MRR, and eventually it was like 4,000 or so. 

**Jeremy:** And the growth was pretty steady.


## [00:38:37] Bootstrapping vs fundraising

**Tom:** Um, so yeah, I mean, the numbers where you're just like, maybe I could have kept going. but it's, the other weird thing about VCs is just that I think I have this rich understanding of like, if you're, if you're running a business that will be stressful, but be able to pay your bills and you're in control of it, versus running a startup where you might make life changing money and then not have to run a business again.

It's like the latter is kind of better. Uh, if stress affects you a lot, and if you're not really wedded to being super independent. so yeah, I don't know between the two ways of like living your life, I, I have some appreciation for, for both. doing what Placemark entailed if I was living cheaply in a, in a cheap city and it didn't stress me out all the time, would've been a pretty good deal.

Um, but doing it in Brooklyn with all the stress was not it, it wasn't affecting my life in positive ways and I, I wanted to, you know, go see shows at night with my friends and not worry about the servers going down. 

**Jeremy:** Even putting the money aside, I think that's being the only person responsible for the app, right? Probably feels like you can't really take a vacation. Right.

**Tom:** Yeah, I did take a vacation during it. Like I went to visit my partner who was in, uh, Germany at the time, and we were like on a boat, uh, between Germany, across the lake to Switzerland, and like the servers went down and I opened up my laptop and fixed the servers. It's just like, that is, it's a sacrifice that people make, but it is hard.

**Jeremy:** There's, there's on call, but usually it's not just you 24 7.

**Tom:** Yeah. If you don't pick up somebody else 


## [00:40:28] Financial stress and framing money spent as an investment

**Jeremy:** Yeah, yeah, yeah, I guess at what point, because I'm trying to think. You started in 2021 and then maybe wrapped up, was it sometime in 2024?

**Tom:** Uh, I took a job in, uh, I, I mean I joined val.town in the early 2023 and then wrapped up in November, 2023.

**Jeremy:** At what point did you really start feeling the, the stress? Like I, I imagine maybe when you first started out, you said you were doing consulting and stuff, so, um, probably things were okay, but once you kind of shifted away from that, is that kind of when the, the, the worries about money started coming in?

**Tom:** Yeah. Um, I think maybe it was like six or eight months, um, in. Just that I felt like I wasn't finding, uh, like a, a way to grow the product without adding lots of complexity to it. and being a solo founder, the idea of succeeding, but having built like this hulking mess of a product felt just as bad as not succeeding.

like ideally it would be something that I could really be happy maintaining for the long term. Uh, but I was just seeing like, oh, maybe I could succeed by adding every feature in QGIS and that's just not, not a, not something that I wanted to commit to. but yeah, I don't, I don't know. I've been, uh, do you know, uh, Ramit Sethie he's like a,

**Jeremy:** I don't.

**Tom:** an internet money guy.

He's less scummy than the rest of them, but still, I. an internet money guy. Um, but he does adjust a lot of stuff about like, money psychology. And that has made me realize that a lot of what I thought at the time and even think now is kind of a rational, you know, like, I think one of the main things that I would do differently is just set a budget for Placemark.

Like if I had just set away, like, you know, enough money to live on for a year and put that in, like the, this is for Placemark bucket, then it would've felt better to me then having it all be ad hoc, month to month, feeling like you're burning money instead of investing money in a thing. but yeah, nobody told me, uh, how to, how to think about it then.

Uh, yeah, you only get experience by experiencing it.

**Jeremy:** You're just seeing your, your bank account shrinking and there's this, psychological toll, right?

Where you're not, you're not used to that feeling and it, it probably feels like something's wrong,

**Tom:** Yeah, yeah. I'm, I think it, I'm really impressed by people who can say, oh, I invested, uh, you know, 50 or a hundred thousand dollars into this business and was comfortable with that risk. And like, maybe it works out, maybe it doesn't. Maybe you just like threw a lot of money down into that. and the people, I think with the healthy, productive, uh, relationship with it. Do think of it as like, oh, I, I paid for kind of a bet on a risk. and that's, that's what I was doing anyway. You know, like I was paying my rent and my health insurance and spending all my time working on the product instead of paying, uh, freelance work. but if you don't frame it that way, it doesn't feel like an investment.

It feels like you're making a risky gamble.

**Jeremy:** Yeah. And I think that makes sense to, to actually, I think, like you were saying, have a separate account or a separate thing set aside where you are like, this is, this is this money for this purpose. And like you said, look at it as an investment, which with regular investments can go down.

**Tom:** Yeah, exactly. Yeah. 

**Jeremy:** Yeah


## [00:44:26] In hindsight might have raised money or tried smaller bets

**Jeremy:** Were there, there other things, whether technical or or business wise, that, that if you were to to do it again, you would do differently?

**Tom:** I go back and forth on whether I should have raised venture capital. there are, there's kind of a, an assumption in venture capital that once you're on it, you have to go the whole way. You have to become a billion dollar company, uh, or at least really tell people that you're going to be a billion dollar company and I am not. yeah, I, I don't know. I've seen, I've seen other companies in my space, or like our friends of my current company who are not really targeting that, or ones who were, and then they had somewhere in between the billion dollar and the very small outcome. Uh, and that's a little bit of a point in the favor of accepting a big pile of money from the venture capitalists. I'm also a little bit biased right now because val.town has one investor and he's like the, the best venture capitalist that I have ever met. Big fan. don't quote me on that. If he sacks me in like a year, we'll see. Um, but uh, yeah, there, I, I think that I understand more why people take that approach. or I've understood more why people take like the venture capital but not taking $300 million from SoftBank approach. yeah, and I don't know, I think that, trying a lot of things also seems really appealing. Uh, people who do the same kind of.

of Maybe 10 months, but they build four or five different products or three different products instead of just one.

I think that, that feels, feels like a good idea to me. 

**Jeremy:** And in doing that, would that be more of a, like as a solo entrepreneur or you, you're thinking you would take investment and then say, I'm gonna try all these things with, with your money.

**Tom:** Oh, I've seen both. I, that I, yeah, one friend's company has pivoted like four times between very different ideas and yeah, it, it's one way to do it, but I think in the long term, I would want to do that as a solo developer and try to figure out, you know, something. but yeah, I, I think, uh, so much of it is mindset, that even then if I was working on like three different projects, I think I.

My qualifications for something being worth, really adopting and spending all my time doing, you just have to accept, uh, a lot of hits and a lot of misses and a lot of like keeping things alive and finding out how to turn them into something. I am really inspired by my friends who like started around the same time that I did and they're not that much further in terms of revenue and they're like still, still doing it because that is what they want to do in life.

and if you develop the whole ecosystem and mindset around it, I think that's somewhere that people can stay and, and be happy. just trying to find, trying to find a company that they own and control and they like.

**Jeremy:** While, while making the the expenses work. 

**Tom:** Yeah.

Yeah. that's the, that's the hard part, like freelancing on the side also. I probably could have kept that up. I liked my freelance clients. I would probably still work with them as well. but I kind of just wanted the, I wanted the focus, I wanted the motivation of, of being without a net.

**Jeremy:** Yeah, I mean, energy wise, do you think that that would've worked? I mean, I imagine that Placemark took a lot of your time when you were working full time, so you're trying to balance, you know, clients and all your customers and everything you're doing with the software. It just feels like it might be a lot.

**Tom:** Yeah. Yeah. Maybe with different freelance clients. I, I loved my freelance clients because I, after. leaving config. I, I wanted to work on climate change stuff and so I was working for climate change foundations and that is not the way to max out your paycheck. It's the way to feel good about your conscience.

And so I still feel great about those projects, but in the future, yeah, I would probably just work for, uh, you know, a hedge fund or something.


## [00:49:02] Marketing to developers but not potential customers

**Jeremy:** I think something you mentioned in one of your posts is that you maybe could have spent more time or had a different approach with marketing. Maybe you could kind of say what you did do and then what maybe worked and what didn't.

**Tom:** Yeah. So I like my sweet spot is writing documentation and blog posts and technical stuff. And so I did a lot of that and a lot of that like worked in a way that didn't matter. I am at this point, weirdly good at writing stuff that gets on Hacker News. I've written a lot of stuff that's gotten to the top of Hacker News and unfortunately, writing about your technical approach and your geospatial project for handling errors, uh, in your JavaScript code is not really a way to get customers.

and I think doing a lot of documentation was also great, but it was also, 

I think that the, the thing that was missing is the thing that I think Mapbox does fairly well now, in which the homepage really pushes you toward use cases immediately. and I should have been saying to each customer who had anything compelling as a use case, like, let's write an article about you and what you're doing, and here's how you use this in your industry.

and that probably would've also been like a good, a good way to figure out which of those verticals was the one that was most worth spending all the time on. yeah. So it, it was, it was a lot of good marketing to nerds. and it could have been better in terms of marketing to actual customers and to people who are making the buying decisions.

**Jeremy:** Yeah. Looking at the, the Placemark blog, I can definitely see how as a developer, a lot of the posts are appealing to me, right? It's about how you worked on a technical challenge or decisions you made, but maybe less so to somebody who they wanna. Draw a map to manage their crops. They're like, I don't care about any of this.

Right.

**Tom:** Yeah, like the Mapbox blog used to be, just all that stuff as well. We would write about designing protocol buffer layouts, and it was amazing for hiring and amazing for getting nerds in the door. But now it's just, Toyota is launching with, Mapbox Maps or something like that. And that's, that's what you, you should do if you're trying to sell a product.

**Jeremy:** Yeah. And I think the, the sort of technical aspect, it makes sense too. If you're venture funded and you are looking to hire, right? You wanna build your team and you just want to increase like, the amount of stuff you're building and not worrying so much about, am I gonna have a paycheck next

**Tom:** Yeah. Yeah. I, I just kind of do it because it's fun, which is not the right reason to do it, but, Yeah, I mean, I still write my blog mostly just because it's, it's a fun thing to do, but it's not the best way to, um, to run a business.

**Jeremy:** Yeah. Well, the fun part is important too though.

**Tom:** Yeah. Yeah. That's, that's maybe the whole thing. May, that's maybe the most important thing, but you can't do it if you don't do the, the money part.


## [00:52:35] Most customers came from existing audience

**Jeremy:** Right. So the people who did find you, was it mostly word of mouth from people who did identify with the technical posts, or were there places that surprised you, that people found you?

**Tom:** Uh, a lot of it was people who were familiar with the Mapbox ecosystem or with, with me. and then eventually, yeah, a few of the users came in through, um, through Hacker News, but it was mostly, mostly word of mouth also. The geospatial community is like fairly tight and it's, and it's not too hard to be the person who writes the article about some geospatial challenge that everyone finds.

**Jeremy:** Hmm. Okay. Yeah, that's a good point about like being in that community, especially since you've done so much work in geospatial and in open source that you have this little, this built-in audience, I guess.

**Tom:** yeah. Which I appreciate. It makes me nervous, but yeah.


## [00:53:43] Val.town marketing to developers

**Jeremy:** Comparing that to something like val.town, how is val.town marketing? How is it finding users? 'cause from what I can tell, it's, it's getting a lot of, uh, a lot of people coming in, right?

**Tom:** Yeah. Uh, well, right now our, our kind of target user, or the user that we think of is a hobbyist, is somebody who's, sometimes a pro developer or somebody, sometimes just somebody who's really interested in the field. And so writing these things that are just about, you know, programming, does super well.

Uh, but it, we have exactly the same problem and that that is kind of being revamped as we speak. uh, we hired somebody who actually knows marketing and has a good sense for it. And so a lot of that stuff is shifting to show you what you can do with val.town because it, it suffers from the same problem as well.

It's an empty text field in which you can type, type script, code, and it runs. And knowing what you can do with that or what you should do with that is, is hard if you don't have a grasp of TypeScript and web applications. so pretty soon we'll have pages which are like, here's how to connect linear and GitHub with OW Town, or, you know, two nouns connect them, for all of those companies and to do automations and all these like concrete applications.

I think that's, you have to do it. You have to figure it out.

**Jeremy:** Just briefly for someone who hasn't heard of val.town, like what, what does it do?

**Tom:** Uh, val.town is a social website, so it has comments and likes and all of that stuff. but it's for writing these little snippets of TypeScript and JavaScript code that run. So a lot of them are websites, some of them are automations, so they receive emails or send emails or connect one service to another.

And yeah, it's, it's like combining some aspects of, GitHub or like a code platform, uh, but with the assumption that every time that you save, everything's instantly deployed.

**Jeremy:** So it's maybe a little bit like, um, like a glitch, I guess? 

**Tom:** Uh, yeah. Yeah, it takes a lot of experience, a lot of, uh, inspiration from Glitch.

**Jeremy:** And I, I think, like you had mentioned, you enjoy writing the, the technical blog posts and the documentation. And so at least with val.town, your audience is developers versus, the geospatial community who probably largely doesn't care about, TypeScript and the, the different technical decisions there.

**Tom:** Yeah, it, it makes it easier, that's for sure. The customer is, is me.


## [00:56:30] Shifting from solo to in-person teams

**Jeremy:** Nice. Yeah. Looking at, you know, you, you worked as a, a solo developer for Placemark, and then now you've got a team of, is it like maybe five

**Tom:** Uh, it is seven at the moment.

**Jeremy:** Seven people. Okay. Are you all in person or is it, remote

**Tom:** We all sit around two tables in Brooklyn. It's very nice.

**Jeremy:** So how did that feel? Like shifting from, I'm in, I don't know if you worked from home while you were working on Placemark or if you were in coworking spaces, but you're, you're shifting from I'm like in my own head space doing everything myself to, to, I'm in a room with all these people and we're like working on this thing together.

I'm kind of curious like how that felt for you.

**Tom:** Yeah, it's been a big difference. And I think that I was just talking with, um, one, one of our, well an engineer at, at val.town about how everyone kind of had, had been working remote for obvious pandemic world reasons. And this kind of privilege of just being around the same table, if that's what you like is, a huge difference in terms of, I just remember having to.

Trick myself into going on a walk around the block because I would get into such a dark mental head space of working on the same project for eight hours straight and skipping lunch. and now there's a little bit more structure. yeah, it's, it's been, it's been a overall, an improvement. Some days I wish that I could go on a run at noon 'cause that's the warmest time of the day.

but, uh, overall, like it makes things so much easier. just reading the emotions in people's faces when they're telling you stuff and being able to, uh, not get into discussions that you don't need to get into because you can talk and just like understand each other very quickly. It's, it's very nice.

I don't wanna force everyone to do it, you know, but it it for the people who want it, they, they, uh, really enjoy it.

**Jeremy:** Yeah. I think if you have the right set of people, it's definitely more enjoyable. And um, if you don't, maybe not so 

**Tom:** Yeah, we haven't hired any, like, extremely loud chewers yet or anything like that, but yeah, maybe my story will change.

**Jeremy:** No, no one microwaving fish.

**Tom:** No, there's, uh, yeah, thankfully the microwave is outside of the office.

**Jeremy:** Do you live close to the office?

**Tom:** Yeah. Yeah. Like most of the team is within a 20 or 30 minute walk of the office and

it's very fortunate. I think there's been something of a mass migration to New York. A lot of us didn't live in New York before four years ago, and now all of us do. it's, it's, uh, it's very comfortable to be here.

**Jeremy:** I think that makes, uh, such a big difference. 'cause I think the majority of people, at least within the US you know, you're, you're getting in your car, you're sitting in traffic. and I know people who, during the pandemic, they actually moved further, right? Because they went, oh, like, uh, I don't need to come into the office.

but yeah, if you are close enough where you can walk, yeah, I think that makes a big difference.

**Tom:** Oh yeah. If I had to drive to work, I think my blood pressure would be so much higher. Uh, especially in New York. Oh, I feel so bad for the people who have to drive, whereas I'm just walking with, you know, a bagel in hand, enjoying listening to the birds.

**Jeremy:** Yeah. Yeah. well now they have, what is it, the congestion pricing in

**Tom:** Yeah. Yeah. We're all in Brooklyn, so it doesn't affect us that much, but it's supposedly, it's, it's working great. Um, yeah. I hope we can keep it.

**Jeremy:** I've never driven in New York and I, I wouldn't want to

**Tom:** Yeah. It's only for the brave or the crazy.


## [01:00:37] The value of public writing and work

**Jeremy:** I think that's probably a good place to, to wrap up, but is there any other thoughts you had or things you wanted to mention?

**Tom:** No, I've just, uh, thank you so much. This has been, this has been a lot of fun. You're, you're very good at this as well. I feel like it's, uh,

**Jeremy:** Thank you

**Tom:** It's not easy to, to steer a conversation in a way that makes awkward people sound, uh, normal.

**Jeremy:** I wouldn't say that, but um, what's been actually pretty helpful to me is, you have such a body of work, I guess I would say, in terms of your blogging and, just the amount that you write and the long history of projects that, that there's, you know, there's a lot to talk about and I'm sure it helps, helps your thought process as well. 

**Tom:** Yeah. I, I've been lucky to have a lot of jobs where people, where companies were like, cool with publishing everything, you know? so a lot of what I've done is, uh, is public. it's, it's, uh, I'm very, very thankful for like, early on that being a big part of company culture.

**Jeremy:** And you can definitely tell, I think for people who look at the Placemark blog posts or, or now your, your val.town blog posts, like there's, there's a clear difference when somebody like is very intentional and, um, you know, it's good at writing versus you're doing it because, um, it's your corporate responsibility or whatever, like people can tell.

Yeah.

**Tom:** Yeah. You can't fake being interested. so you gotta work on things that are interesting. 

**Jeremy:** Tom, thanks again for, for agreeing to chat. This was fun.

**Tom:** Yeah thank you so much.

