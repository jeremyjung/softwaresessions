+++
title = "Building Maps using Leaflet with Sumit Kumar"

description = "Sumit Kumar shares his experience working with GeoJSON, visualizing live data sources, and creating the Leaflet-Geoman plugin"

[extra]
episode_url = "https://media.transistor.fm/90c3816b.mp3"
social_title = "Building Maps using Leaflet"
social_description = "Sumit shares his experience creating applications and plugins for leaflet"
+++

[Sumit Kumar](https://twitter.com/TweetsOfSumit) is the creator of [Geoman](https://geoman.io/) and the head of engineering at [SHARE NOW](https://www.share-now.com/).

We cover:

- Choosing Leaflet vs other mapping libraries
- Sources for mapping layers
- Using GeoJSON to store data
- Raster vs vector data
- Working with live positions such as car data
- Picking a database with geospatial queries
- Using frontend frameworks with Leaflet
- Leaflet plugins
- Desktop vs Mobile
- His work on the Leaflet-Geoman plugin

### Related Links

- [Leaflet](https://leafletjs.com/)
- [Leaflet-Geoman](https://github.com/geoman-io/leaflet-geoman)
- [GeoJSON](https://en.wikipedia.org/wiki/GeoJSON)
- [Geoman](https://geoman.io/)
- [Mapbox](https://www.mapbox.com/)

This episode was originally on Software Engineering Radio.

### Transcript

You can help edit this transcript on [GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

<div class="transcript">

Jeremy: Today, I'm speaking with Sumit Kumar. Sumit is the head of engineering at Share Now, which is previously car2go. He's also the creator of an open source plugin called leaflet-geoman, which provides drawing tools for the leaflet mapping library.

I'll be speaking with Sumit about his experience working with leaflet and how developers can build mapping applications with it. Sumit, welcome to software engineering radio.

Sumit: Hello. Thanks for having me.

Jeremy: So the first thing I'd like to start with is for people who aren't familiar with leaflet, what is it and what types of projects would people build with it?

Sumit: So leaflet is basically a mapping library, a JavaScript library for,  mobile friendly interactive maps. That's how they say it. And if you want a map and you don't want to use Google maps, for example, for whatever reason, leaflet is basically an open source alternative to Google maps and other mapping providers. Of course, you still need a map itself. So basically the images of, of a map where you can have open street map or any other provider, but with leaflet you can. , if I would have to describe it, you basically create the layers on top of the map. So that means polygons, markers, points of interest to show any data that you might have and to zoom around the map and stuff like this. So it's the library around the map itself and gives developers really good tools to do their own mapping solutions.

Jeremy: I'm sure a lot of people are familiar with Google maps. What are some of the main reasons you might not choose it?

Sumit: So in big corporations a lot of companies don't want to be tied in. There are licensing reasons especially in Germany or in Europe, there are data protection reasons. There is simply a stigma attached to Google in that sense. Then there are Google uses a custom format for the geo data and leaflet you can use an open standard called GeoJSON.

You can use it with Google too, as far as I know, but it basically will transform everything to the Google format and it's much more expensive. That is also [a] reason, especially for startups or, individual developers with side projects. If they have a big volume, if they expect bigger traffic, then Google maps is quite expensive.

Jeremy: So what are some examples of sources people would use?

Sumit: Yeah, that's a good question. Normally people use openstreetmap which is free to use. But I think the Google street maps are not very pretty. So all the projects that I do, even if it's open source, I use Mapbox. Mapbox is a company that I would say it's built on top of leaflet.

Last time I checked even the maintainers or the core maintainers of leaflet work at Mapbox. So the company grew out of leaflet, from my understanding, and it's highly compatible with leaflet and they provide beautiful maps. This is not free. So I pay for great maps to use even for my open source projects.

But you can use basically any provider you want. So there is also HERE maps. It's a European provider. There is Google maps. Of course you can use that. I'm not entirely sure about Apple maps if you can use that with leaflet, but any provider where you can fetch the tiles you can implement it into leaflet and leaflet is a mapping tool. That means it's not about only about like satellite maps or street maps. You can also use indoor maps. You can use a map of the Moon or Mars. You can use maps of video games or Game of Thrones it doesn't matter at the end.

Any image that you can take from an area can be a map. And this could be even a (blueprint) a map of your house. You could even use that as a digital map and create whatever you need on top of it.

Jeremy: And in that case would you have a JPEG or a static image and then you  reference that so someone's able to click around that?

Sumit: I've never done a Tile layer myself. But I've seen an application built with the library that I maintain. And this is a SaaS application for construction sites. So they fly a drone on top of the construction site, take, some HD photo of it, or even 4K, I'm not entirely sure.

And then they create a map out of it. That they then draw on top of on the construction site which is really interesting. And as far as I know, it's, it's quite easy for them to make a tile layer out of it. The biggest problem with a tile layer is always zooming in and out of the map. So you need different distances basically.

And of course the file size. So if you do an HD Photo and you opened a map and it has to load multiple HD photos. This creates quite some load and is slow for the user. So this optimization is the hardest part. But other than that, if you research how to do that, I'm pretty sure there are tools for that to make it quite easy.

Jeremy: When you talk about tiles for a map is it where you're starting with a really high resolution image and then you're cutting it into a bunch of pieces so as the person zooms around the map they're not having to load that entire image?

Sumit: It's optimized for exactly this. So it loads as many tiles that are visible onscreen. So if you zoom in. Then it only loads the tiles that are visible. These are usually I would say six images or so. And they should be quite, quite optimized in size.

If you have a huge image that covers a big area. If you zoom out then instead of loading 1000 tiles, you load only six tiles that show more area but in less detail. The load for the user is basically always the same, doesn't matter which zoom level, and you start with a high resolution image and then cut it down.

But again, again, I've never done it myself so not 100% sure on that.

Jeremy: When people talk about map sources, sometimes they talk about raster tiles and sometimes they talk about vector data. What's the main difference between the two and when would you use each? 

Sumit: Oh, the vector data itself, you can think if you are a front end developer, you can think of it like an SVG. So it's an image versus an SVG. An image has a fixed dimension width and height and if you zoom in, the quality gets lower. If you zoom in with an SVG, it's rendered by the browser so it has infinite scalability in a sense. And with, vector maps, it's the same. I'm not sure if that is a bit of a stretch to mapping experts, but, the good thing for me, if I use vector maps, you can zoom in and out very fluently. There aren't particular steps to the next image it's a smooth transition.

And, especially if you use something like canvas mode in leaflet, it's a much smoother experience for the user. But. These are not individual images anymore. So I'm not talking necessarily about the tiles right now, but about the layers you put on top. So let's say you have markers of Tesla superchargers for example, and you put them on the map.

These can be individual DOM elements. And if you have 6,000 of them, it creates a lot of load for the browser. But if you have something like canvas mode it's drawn inside the one element and everything is smooth and performant again. You have the downside of you cannot interact with the DOM elements individually, of course.

But I might getting a bit out of your question right now because, vector maps itself, can be...  If you refer to tiles, there might be even some additional advantages that I'm not sure yet. What I do know is that Uber, for example, created their own library also on top of open source products. I think it was on top of Mapbox. And they use only vector tiles like this because they have huge data needs and they need very performant maps. 

And if you use leaflet only just out of the box and you have big, big, big data then you might get into performance problems. Problems that I have myself but not yet solved in particular apps that I built.

Jeremy: And when you're talking about these big sets of data, is this the mapping data in terms of things like streets and locations, or is this more overlayed on top of that?

Sumit: That's definitely overlays on top of that. So I can do some examples. II'm working in the mobility sector of a car sharing company that's also how I got into leaflet 6-7 years ago because they needed a geospatial data management tool basically that I've built. And, the data that they use are, points of interest, electric charging stations. We have parking zones, drops zones for the cars. We separate the city into polygons to track demand in specific areas of course. And then you have other companies like (masque?), which is a local logistics company. They have zones where their ships drive and stop off the harbors. Tesla for example has supercharger stations, which is small data compared to that and ridiculously detailed data if we are talking autonomous vehicles. Then you need data like you separate the road into different lanes. For example, one goes in one direction, the other one in the other direction. You have parking spots and this for a whole city or a whole country, this is data that is so big and so much your browser would just crash if you try to display it in leaflet alone.

Jeremy: Hmm. And so the very simplest case. If someone is trying to put on a list of parking locations or superchargers what does the API look like that for leaflet? Are people calling functions that are adding these one by one or is it syncing to a collection? What does that look like?

Sumit: so there are multiple options in leaflet, which is quite cool. So normally what I do is I try to use the data always in GeoJSON. So I store it maybe in a different format, but in general, in the APIs I build around leaflet use GeoJSON normally and leaflet you can add GeoJSON simply.

So there is a GeoJSON method where you just put in data and it displays it on the map. You can also create your own shapes. That means a circle marker, a circle, a polygon, a line, a marker. Then you basically give it two coordinates and it creates the shape on the map.

With GeoJSON it's a wrapper for everything. So. If you provided a GeoJSON, it can be markers, can be polygons, can be lines, and leaflet will just add everything. It depends on your needs or your source of data that you have. And particularly with my library where I create the shapes so the user can draw the shapes, him or herself. I need all of those functions. Basically.

Jeremy: And, you were saying that GeoJSON is a good option for storing the locations of different things, storing shapes. How about data that  changes often, like if you have a car sharing application you might have live locations of where cars are. Would GeoJSON be suitable for something like that?

Sumit: So I'm sure there are people that disagree with me. I had discussions actually with developers from Uber and also some, let's say, mapping experts from other companies, and the opinions vary. I can only speak for myself.  even though JSON or GeoJSON, might not be the most efficient storing format out there, it's basically a standard in modern APIs to use JSON or GeoJSON as as the format to exchange data.

And I like to have not a lot of transformations with my data, so I store it as much as I can in GeoJSON. It works fine for me. I don't have any restrictions or downsides for that? I don't build applications on a scale of Uber, but Uber also told me they store in GeoJSON and they don't have a problem with it either.

They like to use open standards and I agree with that. And if we are talking live data it doesn't matter how frequent the location, for example, of the marker is updated. Let's say every half a second, you update the location of a moving car.

You simply store the two coordinates into it and you can build it as a, you store the entire GeoJSON again or you store only the changed coordinate. Really the subset of the actual data doesn't matter how you build it. It's so small in comparison that it will only make a difference if you have, I don't know if you update a thousand or a million entries, all at the same time.

Then of course, your network is gonna slow down a little bit, but this has nothing really to do with GeoJSON  or JSON, this is any data. If you have so much data updates you should look at something like a message queue like RabbitMQ or Kafka or something like this. But if you do it just over REST API, I would personally batch the requests.

So every second or every two seconds, I would update all the entries that have been changed. If we're talking about a front end or something and batch everything together.

Jeremy: So to make sure I understand correctly, if you were getting the locations of cars, and you query the backend API, you would get a GeoJSON file, which is basically a regular JSON file that has a bunch of elements that might have the latitude and longitude of each car. And as you got updates,  maybe you get an update every second or every few seconds. You would receive new GeoJSON files from the server and it would just have the elements that had changed or new elements?

Sumit: So, there are two different, points in let's say an application stack, where you have these updates. The first one is the car sends an update to your backend. And if we are talking about our company, for example, share now, or,  companies that use my open source product, these might be, for example, 10,000 cars always connected to some sort of backend, and they send their location, maybe every second. For example, let's say you have a network hiccup and they all reconnect, at the same time, you have a huge spike because 10,000 cars send their location at once, and this is an area where we at least had the experience... Don't use just HTTP use a message queue. So we can handle all of the data because the cars do not only send a location, they also send is the window down, is it up motor, start motor, stop events or everything that happens in a connected car is sent to a server.

And this can be multiple events per second. If we're talking 10,000 to a 100,000 vehicles. Or scooters or whatever it is. This load should be handled by a message queue like Kafka or Rabbit MQ. Once it's in the backend and you just want just in quotation marks, want to display it on a front end then we are talking a different story here because, front-end doesn't have a message queue like this we can use if you want to do it really in a real time sense, you can use WebSockets, which is... Yeah, you send incremental updates as they come in to the front end and change your data and can be basically an ID and a new latitude and longitude and you connect the data and the front end.

It can be new JSON. It's completely dependent on how you build it. I normally send some metadata with the JSON that is, for example, a name of the license plate, name of the car, maybe the model, is this a Mercedes or BMW or whatever. And maybe even some other data depending on the project, depending on the data that you get.

There is maybe a lot of metadata involved. Then I don't send the entire JSON. Then I just send the updated information. But if you are not using a web socket, if you're using HTTP, then there is no push from the server. The browser has to fetch updated information. So in this case, and what I would do is, let's say I display Berlin on a map and we have taking as an example, share now and car2go here. Of course, can be applied to any company out there. 

If we are talking 2000 cars, for example, and I want to show them in real time, I will simply fetch the list of all the cars, every second or every two seconds. So there is no push or anything. I would just do a fetch a simple, interval request.

Jeremy: And so you're doing this fetch on this interval, and is it taking into account what it chooses to display? It's just taking that entire document and showing everything that you're sending, or is it performing a diff, comparing the elements you already had and the new elements?

Sumit: Yeah, that's a good question. So I do a diff, but it depends on the project. So I am building a little SaaS product around geo management basically. And there I use diffs. I would have, yeah, I did a mistake of not, not diffing. and the reason is if you redraw the layers on a map, it's a lot of performance overhead.

And if you do this every second and currently you are maybe creating another layer on the map, you are interacting with the map in some other way. This, this is a performance problem. Also, the map constantly rerenders basically your data. And the map simply gets laggy. And if you want to do anything else on the map it gets laggy and it's not a good performance.

So I use diffing that if out of 2000 cars only two move, then they will get updated and the rest is just thrown away.

Jeremy: And internally. So when you're talking about using this diff, does that mean on the leaflet side or on the JavaScript side, do you have this GeoJSON document and then you're updating that GeoJSON document and leaflet just figures out that only those two elements changed and it doesn't touch the rest of the page?

Sumit: Yeah, that would be great. But sadly, as far as I know it's not like that. So you give leaflet something to draw and they will draw it. So I do the diff, basically on the business application side, on the business logic side, I do this myself. I'm diffing, when I get the payload basically to the payload that is already there with lodash do a comparison, remove everything else.

And, then I have to remove the layers first that are currently in leaflet, and then I feed them the new ones. And I also have my own IDs associated with everything. So I can compare also individual shapes on the map or layers on the map.

Leaflet has IDs that they create when you add something to the map. But they are not consistent. So if you add a marker to the map it has an ID. If you want to add the same marker to the map again with a different location it gets a different ID. 

You can get the current one on the map and update that one. That is also possible, but then you would have to buy in completely into the leaflet logic, including the IDs and how to handle everything. And I like to separate... I like to have leaflet just as a dumb drawing tool and not as the source of truth for my IDs and business logic and all of that.

So I do this outside. I do the diffing outside. I do the storing to the database outside, and leaflet is just a component. I feed it data, it draws it, and that's, that's about it.

Jeremy: Mm. So in situations where you have live data and you have a lot of data changing, it sounds like you actually aren't using GeoJSON in that case, you have your own collection outside of leaflet. And you're using that along with your own diffing to determine, which elements you should find inside of leaflet based off of a key.

And then, moving just the ones that you've found that have changed?

Sumit: No, it's GeoJSON. It's all GeoJSON that I store. For example, the SaaS tool that I built has an API where you can fetch the layers that are displayed on the map, from an API And this is all GeoJSON. And then internally, I only use GeoJSON. And that meansif you put it into leaflet internally in leaflet, it's also transformed to something else, of course.

But the map, you can just say, okay, give me these layers and make them GeoJSON basically. And then this is how my whole application uses it. but GeoJSON has a properties block, and in there you can add all the metadata you want. So in there, I have the IDs that are basically the reference to my database in there.

I have, a gravitational center of a specific polygon, for example. I have descriptions, names, anything they use, I would like to see I store in the properties of GeoJSON and and use that everywhere. So it's still all GeoJSON.

Jeremy: You have let's say a single GeoJSON document for all of your car locations. And if you go inside that GeoJSON find the key of a car that you want to move, you can update the location through the GeoJSON?

Sumit: That's actually a pretty good question and just depends a bit on the application that you're building. So GeoJSON allows you to group layers together. That means if you have one polygon, cool, you can have that. If you have two or three or a hundred, you can group them in what's called a FeatureCollection.

You can store it this way, that's completely fine. Then you have big payloads, but you have to get into the GeoJSON and get the specifics out of it. In the SAAS application, I have this use case to count and limit the layers that a user can draw on a map and this means I want this to be separate database entries.

I can also choose to share one layer versus the other with the public or with the colleague or whatever and to have this granular permission system I need this to be separate database entries and that means... Each layer on the map is for me personally a different GeoJSON. But again this is highly customized to my use case.

I'm sure there are users out there if they fetch my data from GeoJSON through the API. They would not like to have a thousand different GeoJSONs in an array or a collection for all the markers. They would just like to have one big GeoJSON file that owns all of the data.

This is easy to do. You can just combine them. That's fine. And I will do this on the API level. But for my use case, I store them separately.

Jeremy: Okay. So when we're talking about GeoJSON in a lot of cases you actually choose to have a separate GeoJSON document for each marker or each thing that you're going to put onto the map.

Sumit: Exactly.

Jeremy: We were talking about how you're bringing in data on the backend and then you're bringing it in as GeoJSON on the frontend.

Is the GeoJSON, is that something that you're converting at the API level or are you storing your data as GeoJSON on the back end as well?

Sumit: This is the embarrassing part of the application. When you start out, and I'm building this application for a long time and there is tech debt of course and that is one thing.

So what got me up fast? I use Firebase as a data storage, or firestore it's called. And this just helps me ramp up an application quite fast. And I still use it even after many months, I think a year now that I'm building this application. And, in there, you have a limitation of the documents, how you store it.

The document format is limited. So I cannot have nested arrays, but, GeoJSON has quite a lot of nested areas, especially if you have. Multipolygons. That means multiple polygons belonging to one layer, acting as one layer, basically with holes in it. For example, this does some multiple levels of nested arrays.

You can't just store this in firestore. You have to store it as a JSON string. So basically this means is I store my GeoJSON as strings currently, that means on a database level I can't do any queries. Anything I do with the data I first fetch it via cloud functions or a node script or whatever.

I fetch the data first. Then I do the calculations on top of it. For example, is a point inside this GeoJSON or are these polygons near the user or whatever? I do all the calculations and then I serve the data as GeoJSON of course. So I store it as GeoJSON in a sense, but it's a string.

And if I would have to do it again, or if I look into the roadmap for the future, I would probably go to something like MongoDB where you can, I'm not sure if it's like native GeoJSON support, but the important part is that if you build an application that basically does a lot of of geo queries and stuff like this.

If it's made to handle spatial data use a database that can do geoqueries on a database level. That means I give a database a coordinate like my location and do a query like give me all polygons. That where this point is inside a polygon this is something. If you can do this on a database level, this adds a lot of performance, because otherwise, if we are talking thousands or millions of layers, you have to fetch everything and calculate this on your backend, on the backend side.

And this is expensive. So I would go to a database that allows geo queries, Firebase SaaS. They have this in a very, very limited format. I asked this on stackoverflow. I saw the question yesterday again. I asked this about two years ago, 2016 and back then they answered that they haven't exposed their geo queries yet and they still haven't.

So I'm not sure when they come out with it, but if I needed I would switch databases I will not wait for that. And if I would start over, I will choose a database beforehand that allows me to do that.

Jeremy: And for your work at share now, how are you storing the geo data there?

Sumit: So, I have not touched  that particular product in quite a while. But, back then when, when we built it. It was GeoJSON, but we stored, we used Mongo DB, and I'm not entirely sure if you can simply without any transformation store GeoJSON in Mongo DB, but Mongo DB has geo queries. So, I know that much, but I can't tell you right now off the top of my head if you have to transform it or if MongoDB accepts GeoJSON but transforms it internally that I don't know.

Jeremy: We're talking about how you can have an application with a lot of data but depending on where the user is looking on the map they don't necessarily need to bring in all that data at once. What are the strategies you use to deal with that?

Sumit: That is a good one. So what geo queries often allow you to do is if I look on a map you can define the borders by basically the top left, top right, bottom left, bottom right corner of your screen. So if I have a map on my screen leaflet and any mapping library can basically give you the boundaries that you are currently looking at.

And these are these four coordinates. And if your database supports geo queries, you can basically say give me all layers that are inside these boundaries and then you can just fetch that data. This is how I would do it from the top of my head. Honestly, I've not built it like this because I've not had to deal with those big datasets.

And there might be downsides to this. If the user for example moves the map how many queries do you do? Then you have a moving target, basically. But I'm sure there are ways to solve this. So this would be my first clue on how to achieve this.

Jeremy: When you're working on a leaflet application, do you have any experience integrating a leaflet map with other frameworks like React or Vue?

Sumit: That is a very good question. I get this quite often on the open source library as well. And with mapping libraries like leaflet you are basically back to the roots of HTML and JavaScript where you interact with the DOM elements directly.

And with the introduction of frameworks like Angular and React and now Vue we  moved past this. These are all abstractions to the DOM element. We say create this div and create this div. We don't do this anymore. But with leaflet you still at least a little bit have to do this in the sense that, for example, you tell it the div that it should render in and you call a specific element directly, sometimes through the leaflet API of course, but it doesn't have this reactive nature like our frameworks today do. 

So what happens is that there are a lot of abstractions to mapping libraries. So there is react-leaflet, vue-leaflet, all these abstractions, to use the mapping library in the same reactive way, in the same thinking mode of the framework, which, which is good for anyone that is starting out.

I personally like to use it bare bones. I like to interact with leaflet directly with the API it provides. I have full control over it. Maybe I'm an advanced user in a sense. But the abstractions that are out there, they limit me because I always have to go through that. If there is a new feature or an edge case I want to tackle or something I always need the buy in of the maintainer of that abstraction and this is something I don't do.

Sometimes I build my own abstraction but normally I basically build a component in Vue and it doesn't matter if it's React or Angular or Vue. I build a component that owns the map itself. And as a property I put the GeoJSON in there, for example. And the component does all the rest, maybe the diffing even, the rendering, the updating, the watching of the properties.

But you have to build your watchers yourself and stuff like this. So it's just out of context. Not every developer is as comfortable with this, especially if you start programming and you started in the world of React so you're not used to this barebone coding.

But if you use other libraries that are interacting with the DOM elements directly then it's a good exercise to connect these two worlds. Another use case might be where you could use your skillsets, in the sense are, charting libraries. So if you display charts for example on a dashboard, it's the same, same topic there.

Jeremy: So basically you recommend keeping your framework code separate from your interactions with leaflet. You'll use leaflet's built in APIs, not use a wrapper just because you want to make sure you have full control and not be limited by that wrapper.

Sumit: Exactly. And if there is a new version of leaflet coming out, I want to use it immediately. It probably has some updates that I want to put in. And again, I can control the user experience much, much better if I can interact with leaflet directly through the APIs.

I wouldn't necessarily say I would recommend it. It's the way how I do it. And I think if you build an advanced, a big application, I think you are better off using the leaflet API directly. If you just want to display a map and maybe a marker on top of it to show the location of your business on your business website, then it's totally fine to use a wrapper, right?

That's easy. You will have it done in less than an hour and that's it. But if you build a big application to handle geospatial data. Then it's a different story. I would say remove the abstraction and go directly with the library.

Jeremy: For these components that are from your framework do those end up rendering surrounding the map? Like you would have a sidebar or a top bar or something like that?

Sumit: Yeah. Also also a good question. So on Geoman, I use it. The SaaS product is also the demo website basically for the open source library, and it's called geoman. And there, I have a map component as I said, and it's basically fullscreen. From the Dom site. Of course, I have stuff around it.

I have a sidebar in a sense and a footer and whatnot. But with CSS I just display it differently. So the map is for me, always front and center. It's the biggest element. And it should be basically like Google maps. It should be the one big background thing and the header and the sidebar, just like on top of the map.

And you can build this in different ways. Like you could even add this to leaflet you could do everything in leaflet, you could even add your sidebar as a map element on the map but I don't do this. I have the map container and I just overlay my other Dom elements on top of the map, so I want to keep this really separate to the map itself. The map component is definitely one separate component for me that I interact with. Yeah. Because of lock in. Again, let's say I want to change mapping providers at one point instead of changing one component, I would have to change I don't know the whole application. So I try to keep this as separate as possible.

Jeremy: So if you were to look at the HTML the DOM nodes that have all your controls are your sidebars, things like that, they would be completely independent of the leaflet DOM node, but you use CSS maybe with a fixed position or something to appear on top of the map, is that correct?

Sumit: Yeah, that's true. I would do one exception though. I build an open source library, as you mentioned, for drawing, basically layers on the map, markers, lines, whatever. These buttons I add them to leaflet. So because it's a leaflet plugin, that means any user of leaflet that wants to use my plugin just imports it.

And it adds these buttons to the leaflet map. I basically used the leaflet framework to display this, but anything else, like for example, an address search, the list of the layers that is currently on there, an export button for downloading the GeoJSON, changing the tiles from street view to satellite view, this stuff you can all add to the map.

And a lot of people do that, but I personally keep this out of the map. I have this separately again, because In my SAAS application, I would like to have more control over the user experience. And maybe I have something like a pay wall in front of it or an upsell button or I need to limit this based on user permissions.

And I simply feel more comfortable doing this in a framework like Vue instead of leaflet itself.

Jeremy: You were talking about how you built a plugin.

Can you talk a little bit about what makes sense to be built as plugins versus built outside of them?

Sumit: Yeah. Also very good question. I thought of that as well. Sometimes my thoughts went if you have the stuff I just mentioned, an address search and the list of layers and stuff like this. I thought about, Hmm, what if everything of that is a plugin for leaflet, I could open source everything. I just add everything modular to leaflet. It's a big lock in into the leaflet ecosystem. So this is all possible and there are plugins, I think for all of that, there are plugins for your address search, there are plugins to switch tiles, plugins to draw, to export data for all of that.

There are plugins already and they add this to the leaflet map. Again, I think if you have a a use case of just having a small map showing some small stuff, or you want to create an MVP, meaning a small app that can do something where, yeah, it's not a product that you might sell, to someone.

You can do all of that and it will be completely sufficient and it's probably less work. To just use a plugin to add this to the map. But, if you have a product and you want to control the design aspects of it a lot and maybe animations and stuff like this. I think for every developer it's more convenient to not fiddle in leaflet code for that. Leafet has its own CSS also. So you have to overwrite this or compete with it over the style sometimes here and there. And keeping it out of it just means the data that is displayed and sent between these components has to flow through somewhere. And if you build a big application, you probably have an application state, a state, somewhere like in react, what is it called? Redux, for example. Redux store where you have your data store on the front end. If you use this as your source of truth, you can use it for all the components that you display on top of the map that are not inside leaflet. And it's much easier using that ecosystem then recreating everything in leaflet because if you do that you basically don't need a framework anymore.

You build everything in the leaflet library and you interact with the DOM again directly. So the abstraction that we mentioned before you would have to build this for basically everything, right? And there is no reactive thing anymore. You don't get the benefit from React anymore if you add everything directly in leaflet.

Jeremy: If you look at the leaflet website, there's a long list of plugins. Is there a set of plugins that you typically use when you know you're building a leaflet application?

Sumit: No. Somehow I'm ignorant in that sense. No, not even the address geocoding thing. I also built this on my own. There are many, many, many good plugins there honestly and what I can tell you is there are plugins that we use at SHARE NOW or Car2Go and there are plugins that I constantly see people use together with the library that I am providing and these are something like, what's it called? A marker grouping tool. It's...

Jeremy: Clustering.

Sumit: Clustering. Yes. Thank you. Marker cluster is a plugin that is used a lot and we use this as well. As the name implies it clusters the markers when you zoom out, so you don't have 10 million markers on a map, but it clusters them together.

It's also good for performance, but also for usability. so this is something that is used a lot. And then of course everything that creates heat maps and data visualization are also used a lot, at least from the circle of open source maintainers or open source users that I'm interacting with a lot.

But honesty, if you are using leaflet, look at the plugin library, see what is there before you build it yourself. Try the plugin and see if it fits your needs because you don't have to reinvent the wheel. For me, this might be a bit of a sickness and it's fun to recreate the wheel for me.

But of course it's a waste of time if you have it already there.

Jeremy: Yeah. When we talk about displaying things on the map. We were talking about cars earlier. And you're saying you display them in the form of markers. A lot of times applications want to show information that's associated with those markers, whether that's a label on the map or something else like that.

How do you typically approach that? Keep all that information grouped together and keep it updated.

Sumit: So I saw different implementations. You can, as always, the metadata that you store with your layers. You can choose to have them its own entity outside of the GeoJSON, or you add it to your GeoJSON. And so the question is, is the marker itself, your source data, your main entity that means... do you, do you associate the style for a marker with the marker or do you store the style separate and store the idea of the marker in the style that is basically an architecture question that you have to solve. 

An example that might resonate maybe more with everyone is we have cars, right? So we have cars and the cars have metadata like license plate, which tires they have, which SIM cards they use, they have all this, a lot of data, much more than the geo data. And so is the location of the car just the property of the car? Or is everything is from the car metadata of my location data?

And this is a distinction you have to decide on your own, how your complete architecture, landscape and ecosystem looks like. For me, I decided many times that the location data is the source of truth, let's say. And I put a lot of metadata in. That is because if everything the user does and everything my API does resolves around the location data I can just as well as use that as my main source of truth.

So if we go back to styling. Styling in particular I would store as metadata. So you have a marker and it should resemble a car. So I want a different icon. I maybe want a direction. If we are talking apps like Uber for example, you see the direction the car is heading. So, I might have a degree so I can, I know how to turn the icon on a map. I need a color, and maybe I wanted to display the lane that the car was driving, the route. So I want to display that and all of this data I store as metadata. And if the user changes that, I change it in the metadata of that marker. That means if any team is fetching the data from the API they have also the information how to display it. And this was for me and for us also very important to do. So styling, I would definitely recommend storing this with the geodata as metadata with everything else. Like the fuel level of the car. That decision you have to do on your own architecture wise.

Jeremy: If you wanted to make a customizable user interface in terms of somebody chose, they wanted to see what's the speed of the car or something like that and they want to be able to turn it off and on, you would store what the user chose in the same place.

Sumit: What the user chose in the sense of, okay, I want to see the fuel level. I want to see the license plate.

Jeremy: They want to be able to turn it on and off.

Sumit: Yeah. So that is a big use case. I think that's the use case for everyone that displays markers. Let's use Tesla superchargers for example. You have the location of the supercharger and if you click on one, you have the address, the exact location, how many are there? How many are currently free? Blah, blah, blah. All of all of this data like you can you, can you eat there? are there restrooms, et cetera. 

So Tesla, they don't give you the data as GeoJSON. They give you a collection of superchargers basically an array with objects. And just the location of the supercharger is a GeoJSON.

That means you have a big collection of JSON data and a subset property of each entry is a GeoJSON. That is also how we do it at Car2Go and SHARE NOW. GeoJSON is just a part of a bigger, dataset. But in Geoman, for example, I reversed that. I use GeoJSON as the main source and have.

Basically most of the data as meta data inside the GeoJSON, it doesn't make a big difference to anyone. It's just a preference of how you manage your data. And again, what is your main entity? Is your entity a car that has a location property, or is your main entity a marker and being a car is just a property of that marker, could also be a plane or user.

Because I wrote an application where everything revolves around location data, I chose the location is my main entity and that is the GeoJSON and the fact that it's a car, it's just  metadata, a property of it with a specific icon basically, like my application doesn't care if it's a plane or a car. At the end of the day.

Jeremy: I guess another thing I'd like to ask about is when people use maps, a lot of times they're on their phones as well as just being on the desktop. what's your approach or what are things to watch out for when building a site that needs to work on both desktop and mobile?

Sumit: Yeah. Very tricky. Very tricky. So, two things, if you just want to display it. So again, the use case of you have a location of a business or something that you would like to display. That is no problem at all. Leaflet is very mobile friendly, and if you just display a marker the user can zoom in and out, can easily scroll through.

So if your thumb goes on the map and you scroll, you might have seen this with Google maps right in Google maps to zoom or to move the map, you need to use two fingers. They do that so you can easily scroll through the website without, You know that you are scrolling is interrupted by your moving the map instead.

So these kinds of functionality to make it mobile friendly is there in all of these libraries. So this is an easy thing. You don't have to do anything. It just works out of the box. But if you create more advanced interactions with an app, like for example, a user should be able to draw a polygon.

Then it gets more trickier and geoman and also my library leaflet-geoman they both work on mobile. I think that is also one reason why it's getting quite popular because from my research, it's the only drawing tool that works on mobile. But if you use your thumb, it gets in your small screen, it gets less precise your drawings. So I have features like pinning. That means if you click near a different marker, it just snaps them together. So it assumes you want to place them on top of each other. That's a really cool use case, especially on desktop where you can easily move to markers. But on mobile, it's not that easy.

So. I personally think it's possible, but it's not a good way to do that except for let's say you have an iPad Pro with a pen. Then it's really cool. I was really impressed when I used my own library for the first time on an iPad Pro with a pen, because then you can draw really precisely. It's a lot of fun.

It's easy to do. that's really cool. So if you have advanced interactions with mobile. Then you will get into situations with click events and stuff like this where it gets maybe a little bit more tricky and use cases where you hover the mouse over the map and you display things or you give the user a hint of what will happen when they click.

You can't do this on mobile. It's basically a different experience and in a sense a limited functionality if we are talking about drawing, So this you should keep in mind. If it's strictly about displaying data, you will not have a problem.

Jeremy: And in terms of the UI, it may need to be significantly different, right? Between desktop and mobile, do you effectively, hide a lot of UI elements or build two components depending on what size the viewport is?

Sumit: Yeah. Yeah, of course. So in Geoman, I use the sidebar for example, right? If you display it on mobile, you don't see the map anymore and it's just a lot of data. So the more data you show and the more metadata you want to display the trickier it gets. How to display this on mobile. And the map should be front and center, especially on a tool that revolves around that.

So that means if you open geoman.io on your phone, you only see the map and you have a small icon on top that moves in the sidebar, for example. it's still not perfect. I think it's a limited use case also, my particular app to use this on mobile. But of course, you have the same problem with any website that displays a lot of data.

You have to hide some, you might have to, basically also reduce some data like some data that you just don't need on mobile. you will reduce maybe the table, columns, you know, stuff like this to make it as easy as possible for the user on mobile. And they can still open a desktop view if they want to on mobile.

But it's such a limited use case. I think that, as long as it looks good and it has the basic information, I think everyone is fine. If you go into an advanced mode than a desktop might be, or a tablet might be the way to go for the user.

Jeremy: Yeah. We've been talking about geoman. And you've mentioned that you have a leaflet plugin called geoman-leaflet. Can you go into a little bit about what geoman is and why you decided to create geoman-leaflet?

Sumit: Yep. Yeah, sure. So  just so you know, it's not a superhero or something like this, it derived from geo management, and I just noticed later that it sounds like some sort of superhero. Anyway, I have a quite, let's say, experience now in solving this for companies and seeing the problems inside companies.

And not only in the mobility space, this ranges to communication providers to, again, construction sites and logistics companies and everyone that has, geospatial data. There are two categories I would say that I'm trying to help. One is they have their own application, they have their own team that works on this or multiple teams, and they use open source products or pay products and they need more functionality.

So they probably use my open source library if they use leaflet for creating data. And, the open source library basically helps you create and edit this  data. So you need to create a polygon. You can create this of course by just providing the coordinates. But if you have a user and he needs to, for example, create a polygon around a building or around a block or a city or whatever, my library is there to help them just easily create these polygons on the map.

They can create markers, circles. rectangles, whatever it is. They can also edit each specific Vertex, add Vertexes in-between, they can move the entire shape. They can cut holes in polygons. They can of course, remove the polygon. So all of these drawing and editing features are there. And one product I'm currently thinking about, I'm just collecting feedback. I've not built it yet, is a pro version of that that has even more advanced drawing and editing features. Some companies need to have polygons that are adjacent to each other and cover a complete area like a city, and to have maybe a hundred or 200 polygons that make up the city.

So just think of it like sales territories, or something like this. And that there should not be an overlap or a hole between these polygons, so they need to stick together. Now they can do this already with the open source library that I'm providing, but if they want to change the shape of one polygon, they would have to change all of the adjacent polygons as well, which is quite a lot of work.

And I could build a tool, for example, where you just draw a new border and it automatically calculates. The new size of each of those polygons and adapts that because you basically tell them, Hey, I don't want any overlap and I don't want any hole in it. And these are such advanced niche drawing tools that require weeks and months of work to build, that I want to wait if people or if companies need this, and I'm thinking about providing basically a pro version of the open source library. So that means I have the open source library that I could constantly maintain for basic drawing and editing needs. I wouldn't say it's basic, it's quite advanced already. Then we have really advanced tools where I think a pro version of the library would be helpful for some companies.

And then we have the second bucket of companies that don't build their own application. They just want a way to easily have a service like MailChimp, for example. Instead of managing email, they want to manage geospatial data. So they want a service where they can create data where they can put data in through an API, and where all the teams and clients and apps can fetch the data again and this is where the SaaS application comes in and it's called geoman. There you have a studio where you have your map. Or you can create multiple map like projects, and then you create, for example, one map that displays your supercharging network.

You have one map that displays your sales territories or your parking spots. You can create one map that displays airlines, routes, whatever it is, whatever your data is. And for me, the powerful thing that would solve a lot of problems inside companies is any user can draw this.

It can be a working student that creates parking spots, for example, in a city. Then you have your developers that not only consume the data, but they can write the data through the API and it's updated everywhere on every consumer. And you can attach the metadata to it to put everything in.

Jeremy: To summarize, there's geoman, the application, which is where somebody can draw shapes or add data, probably import data from something like say a CSV or an API or something like that.

And then, if you had an application that wanted to consume the data, geoman itself has an API for people to get data back out.

Sumit: Exactly. 

Jeremy: and then geoman-leaflet is the leaflet plugin that you built and use within the geoman application.

Sumit: Exactly. And it's open source for anyone that wants to build basically their own application to manage your data. And, yeah, so I got asked a lot, for example, why do I open source this?  Because it seems like it's one of the best plugins out there. I don't want to, say anything false here.

And I'm not sure about that, but users tell me they switched to it, for example, from other libraries. And I also haven't seen other libraries that provide the same functionality. So it's one of the more advanced ones. And people ask me, why do it open source? Why is it not part of the geoman suite?

That makes it a reason for people to use. And the reason is simply that I know that Geoman will not cover all use cases that are out there. People need very specific needs and geo data. And I like open source. I love contributing to it. I love the interaction with the community and I think it's a great open source product.

I personally benefit a lot from open source as well specifically with leaflet and I thought Geoman as a platform can be a way for me to earn money and invest more time into the open source product that I can then give back again. You know what I mean? 

I've maintained this library for four years now. I have not earned a single Euro with it and it costs a lot of time and I feel bad if I don't maintain it for a month or something. But if, if the platform is successful, then I have more time to develop it. It serves multiple purposes, not only for me personally, but also I can maintain the library much better, add much more features for anyone that wants to build their own application with the open source tools

Jeremy: Very cool. So hopefully at some point  you'll get to spend more time, in your day job working on geoman and working on geoman-leaflet.

Sumit: Would love to. Yeah.

Jeremy: To start wrapping up, for people who are learning leaflet are there common mistakes you see people make or suggestions you have for people who are learning leaflet now?

Sumit: Yeah. If you go through the docs and the standard stack overflow tool that we all use every day you will get quite far. What I see a lot, especially if you use frameworks, and beginners with leaflet, they struggle sometimes to make this mental distinction between these two universes, these two ecosystems.

So if you use a reactive framework, like react, vue, Angular, just know that leaflet itself is not part of that. You interact with the DOM directly as mentioned before. So don't expect like this reactivity. This you just provide something and everything changes on the map.

This is something where I see a lot of questions happening and then on the other hand, the business side, so think of leaflet and mapping. Like they provide you the tools to display a map and data on top of it, but the business logic behind it, like, how do you store it in what data format or I want the tile to be red if it's overlapping something else, this stuff, you have to build yourself or use a plugin for it. It won't create business logic for you. It's basically a dumb way of rendering data. Not that dumb, but I hope you get what I mean right? You have business logic that is specific to you. And you have to build this yourself. So the library, will not do this out of the box for you. So I see these questions a lot also on the open source repository, where people just expect expect it to do things. but they can easily do this in three lines of code they just haven't wrapped their head around yet. What exactly is leaflet doing for you and what not. So if you have any business logic this is something you have to build yourself and it's honestly quite easy. But if you have any questions I'm happy to help, not only for my open source library, I'm on Twitter and everywhere, so I'm happy to help out.

Jeremy: Cool. Are there any specific projects that people should look at. If they're trying to learn how an application should be laid out in leaflet.

Sumit: So there are multiple demo projects for basically all the plugins. There are demo projects and also for leaflet itself. You can look at  geoman.io, which is quite a, let's say, more advanced use case. Everything from Uber of course is very advanced. And especially in data visualization, they have amazing tools and it's all open source also.

So if you look at demo pages from Uber and from Mapbox you will get a sense of where it can go. And then I would personally just look into the DOM and see what they do and how they do it. Maybe they have an open source repository where I can take a look.

And also, for example, if you want to write your own plugin with leaflet, look at the open source code. That's how I started. Like I had no idea how to create a plugin for leaflet or how to manage geospatial data, like I just didn't know. All I had was I needed functionality that no plugin had so leaflet-draw was back then the only one. I basically scan their code, looked at how they do it, and try to recreate it and then build my own architecture with it. But it was very similar in the beginning the code. So just look, that's what open source is there for, look into the code, learn from that, clone it, adapt it, and grow from there.

Jeremy: Yeah. How about in terms of like a full application, you're mentioning to look at, say geoman.io but geoman itself is not open source, is it?

Sumit: No. Yeah, so I'm not sure where are to look there. what I do sometimes. Okay. You have stuff like geojson.io. it's a small utility to, to edit GeoJSON. I've built the same on geoman.io. Oh. But yeah, it's a different one from Mapbox and this is open source. It's a smaller, application that, yeah, that you can take a look at.

What I can also recommend is if you for example you want to create a leaflet map and you don't know how. The demos are not enough for you. You want to see some real use cases with React for example, what I do is I used the advance search functionality on GitHub. So I look at who uses leaflet and who use react, and maybe I searched for the inception code from leaflet, and filter by it.

And then you find a lot of applications that basically use it like this, and then I scan around and try to find someone that uses the same stack as me and how they do it. And this gives me a lot of inspiration.

Jeremy: Yeah, that's a great tip. Not just for leaflet, but for anytime you're trying to learn a new library. Yeah, it's really helpful.

Sumit: Yeah. The GitHub search functionality is underrated, I think in that sense.

Jeremy: Cool. well before we finish up, is there anything that you think we should have mentioned or we should have talked about?

Sumit: I think we had a quite a awesome overview. There is not much to mention if you are into geospatial data or if you have the problem to solve the problem, for your company, or a client or whatever. I think it's quite the interesting field. It's quite niche also, but yeah, the user experience is... It's amazing, and you have such a big impact. If you build something nice on top of maps. And of course it's a field that is very, very future-proof. It doesn't matter if we're talking drones, autonomous vehicles, sales, like everything in the mobility sector specifically, but everything around us needs more and more location data because everything is connected. And, I think it's a field where you as a developer, if you have these skills are very good equipped for the future. So, don't hesitate to get into it and code a bit around it. I don't think you will regret it.

Jeremy: Cool. And for people who want to follow you or see what's going on with geoman, where should they go?

Sumit: So, I'm on too many platforms, I say, but, I'm active, very active on Twitter. my handle is tweetsofsumit. There I'm the most active. So if there is anything you would like to ask, or if you want to follow me and you know, see where geoman is going, the open source library or also even how to create a business, like I'm not an expert in it. I just share my journey. I will share everything on Twitter. And if I have a, for example, a YouTube video or even a guest appearance on a podcast like this one, and I will share everything there. So I think that is the best way. And of course, you can go to my website, which is raum.sh raum is a German word, raum for a room. raum.sh Is my personal website where I also post occasional updates here and there.

Jeremy: Very cool. Well, thank you so much for talking to me today Sumit

Sumit: Thanks for having me, Jeremy it was nice talking to you. 

</div>