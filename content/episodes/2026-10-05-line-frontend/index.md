+++
title = "Theo Steiner on Frontend Development at LINE"

description = "From contemporary literature to frontend"

[extra]
episode_url = "https://pinecast.com/listen/44dbc43c-05f4-4aec-8aa5-6cabfe677f36.mp3"
social_title = "Theo Steiner on Frontend Development at LINE"
social_description = "From contemporary literature to frontend"
+++

Theo is a Web Developer at LINE Yahoo Corporation in Tokyo with a master's degree in contemporary Japanese literature. We discuss how mapping events in literature led him to software, pitching Svelte to his team, frontend development at LINE, and hosting the UIT Inside podcast.

This episode was recorded at the LY Corporation offices in Tokyo. I hope you enjoy it!

### Theo Steiner
- [Theo homepage](https://theosteiner.de/)
- [1Q84](https://en.wikipedia.org/wiki/1Q84) (Murakami novel that got Theo interested in contemporary japanese literature)
- [Where the Magic Happens](https://literary.tokyo/) (Mapping locations from the 1Q84 novel)
- [svebcomponents](https://github.com/svebcomponents/svebcomponents) (Theo's svelte web components library)
- [Sophia University](https://www.sophia.ac.jp/eng/) (Theo's Graduate school)
- [Simultaneous recruiting of new graduates](https://en.wikipedia.org/wiki/Simultaneous_recruiting_of_new_graduates) (The process Theo skipped)
- [What exactly is the Working Holiday programme?](https://www.auswaertiges-amt.de/en/visa-service/buergerservice/faq/06-workingholiday-606672)

### UIT Inside
- [UIT Inside](https://uit-inside.linecorp.com/) (LINE frontend dev Japanese podcast hosted by Theo)
- [Walking up the ATProto Stack](https://uit-inside.linecorp.com/episode/192) (English episode with Dan Abramov)

### LINE
- [LINE Restaurant Plus](https://www.lycbiz.com/jp/column/line-official-account/restaurant/service-information/line-restaurant-plus/) (Japanese)
- [LINE Mini app](https://www.lycbiz.com/jp/service/line-mini-app/) (Japanese)
- [LINE Front-end Framework](https://developers.line.biz/en/docs/liff/overview/)
- [LINE Yahoo Corporation](https://www.lycorp.co.jp/en/)

### Frontend
- [Svelte](https://svelte.dev/)
- [Svelte Japan Offline Meetups](https://svelte-jp.connpass.com/)
- [Japanese Svelte Companies](https://github.com/svelte-jp/japanese-svelte-companies)
- [SvelteKit routing](https://svelte.dev/docs/kit/routing) (file based routing)
- [Introducing runes](https://svelte.dev/blog/runes) (to Svelte)
- [Vue.js](https://vuejs.org/)
- [Vue Router](https://router.vuejs.org/file-based-routing/) (file based routing)
- [Vue Fes](https://vuefes.jp) (Japanese Vue conference)
- [Lit](https://lit.dev/) (Helps build Web components)
- [SolidJS](https://www.solidjs.com/)
- [React](https://react.dev/)

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).

## Introductions

[00:00:00] **Jeremy:** Today I'm talking to Theo Steiner.

[00:00:02] We're here at the beautiful LINE offices here in, in Tokyo, Japan. And, uh, I wanted to talk to to Theo because I think he has such an interesting background. Um, a lot of people, they come from backgrounds that are purely just, "I liked computers, so I got into computer science," but I think, your background is a little bit different 

[00:00:25] maybe you could start with first off how you got here to, to Japan from, all the way from, from Germany, was it? 


## Path to Japan

[00:00:33] **Theo:** Yeah, I'm from Germany. Yeah, that too is a bit of like a unconventional story, I'd say. So many Germans, like when they turn 18, they go somewhere. Like we used to have like military service, but that got, canceled when I... Just before I turned 18. So like a lot of people used that, like newly gained freedom and like they went somewhere like to New Zealand, Australia, Canada, I think are like the typical places to go.

[00:01:01] And I actually, I wanted to go to Russia, but back then, it was, it just happened to be at the time where Russia started the war in Ukraine. So my mom was like, "Okay, you can go anywhere, but please don't go to Russia." So I, I checked like which country does Germany have working holiday agreements with.

[00:01:23] And the usual suspects came up, and then also Korea and Japan. And I was like, "Oh, that sounds interesting. I'll just text the embassies and whoever writes back first, like I go there." And the Japanese Embassy was like a day quicker than the Korean Embassy. So that's like the whole background to why I ended up in Japan, and I knew nothing about Japan at the time.

[00:01:48] So I loved sushi. I always was like a, a huge fish eater. So I knew sushi and I was like, a country with like food that delicious can't be bad, so why not just go? And that's how I ended up here. Like I came for a year and fell in love with the country, made great friends, and yeah,

[00:02:10] **Jeremy:** So it's almost like a, a coin flip. You were saying, "Well, Korea or Japan, whoever gets back to me first." That's, that's quite a leap.

[00:02:18] **Theo:** Yeah. And actually, I think I was like, I knew Korea more than Japan because I, I was like, growing up I used to play StarCraft,

[00:02:26] And Korea, all the, like, legendary players were from Korea. So I, I knew a bit about Korea. I knew almost nothing about Japan. So I think, yeah, it was, like, purely luck that I ended up here.


## Working at farms and snow camp

[00:02:39] **Jeremy:** And how was your, your first year here? what were you doing that, that first year?

[00:02:43] **Theo:** So I came, as I said, on that working holiday visa, and, you're allowed to work almost any job except, in nightlife for obvious reasons. And, I started, working on farms, so I wouldn't receive any money, but I'd receive, food and, a place to sleep. So I worked my way north starting from Tokyo, and, I had this, weird plan of, like, in the winter I wanna be in Hokkaido because I knew they have, like, great snow, and I like snowboarding, so I need to get there by winter.

[00:03:14] So I worked myself up, slowly going north from Tokyo, working on, like, a farm that, I think they were, like, growing eggplants and tomatoes. 

[00:03:23] And then I went further to the north and did, like, a snow camp for kids.

[00:03:28] And, and Further to the north, and then I ended up in Hokkaido, and I,I was actually hired to shovel snow.

[00:03:36] Which was perfect because it was, like, in a ski resort, and I would get to, snowboard after work

[00:03:41] **Jeremy:** Oh, that's awesome. So it's, it's really interesting because these are almost the furthest things possible from computer programming. (laughs) 

[00:03:50] **Theo:** Mm-hmm

[00:03:51] **Jeremy:** So, so how did you go from, uh, running the snow camps and working at ski resorts and farming to, to programming?


## Majoring in Japanese literature to get back to Japan

[00:04:01] **Theo:** Yeah. So I actually got even further from computer programming doing that. So I, I wanted to stay in Japan, but, my parents were like, "No, you gotta go back to Germany and, do a proper university degree first." And I was like, "Okay, which university degree is gonna guarantee me that I can come back here and, like, reunite with my friends?"

[00:04:23] So I enrolled for, uh, Japanese studies with, a major in literature. So I, I actually ended up being a literature major at university. But I did pick... I had this, like... I've always had an interest in computers, like growing up playing StarCraft and stuff like that. I never really knew how to code. Maybe I did some, bare minimum, like HTML editing when I was younger.

[00:04:47] But I thought, "Yeah, I need something that can, like, carry, carry my interest in Japan and carry my addiction to sushi when I get older." So I... Some reasonable part inside of me was like, "Okay, let's pick a minor that can be turned into money," and I picked computer science as a minor actually.

[00:05:05] **Jeremy:** I, I take it there aren't too many opportunities for Japanese literature jobs here

[00:05:10] **Theo:** Ah, like some of my friends who studied with me actually pulled it off. Like many of them are like translators. Yeah, but like you have to be like very skillful to be, to like translate literature.

[00:05:22] And there's not as much demand, sadly.


## Literary Cartographic Analysis

[00:05:26] **Jeremy:** And were you, you studying particular classics in literature or what was the, the major like?

[00:05:33] **Theo:** I was actually, um, most interested in contemporary literature and also contemporary literature set in Tokyo. So I was always interested in, like, the, the urban space. 

[00:05:43] And during the end of my bachelor's degree, I started working towards that. And I thought I wanted to continue to work in that actually.

[00:05:52] So I, I picked for my master's degree, I picked a university in Tokyo that would allow me to, like, study in the actual urban environment in Tokyo and, like... I did this thing called, um, literary cartographic analysis, where you basically, you map out a book onto a map, and then you look at the map at the cartography of the story, and you check what kind of, characters appear at which places and, like, how does the urban space relate to the, content and, like, the analytical layer of the work you're working with.

[00:06:31] And that's actually one of the points where I got back into touch with my, like, computer science part because, like, you obviously don't wanna do that sort of analysis on a paper map. You wanna map it onto Google Maps or, OpenStreetMaps and, have all those, digital ways of working with your data to, like, make your life a bit easier.

[00:06:51] So for my master's degree, I actually, I built... I think it's still up. it's literary.tokyo, and, uh, it's basically this service. It's a system as a service for mapping literature onto Tokyo, which is very specific, but I did it for my master's thesis. And if you ever wanna check it out and maybe do your own research, uh, feel free to go there.

[00:07:17] **Jeremy:** Is it where you were reading modern literature and, and manually saying what locations are people talking about or what hints can I get so that I know where these characters are and where these events are taking 

[00:07:30] **Theo:** Exactly. So I was, my thesis was concerning itself with, magic realism. And like magic realism, to the people who don't know maybe listening, it's like this literary genre where like out of the blue something like really weird and magical happens. It's like often associated with, Latin America. But like many contemporary Japanese art, authors are also like associated with this, genre.

[00:07:57] Like for example, Murakami Haruki, who is like probably the most famous Japanese writer of all times. He can be like put into this genre. So I wanted to l- see how like the magic realism interf- interferes with the Japanese like urban space and like study if there's like particular spaces where like magic stuff happens.

[00:08:24] Like I had this theory that like magic events would happen at like liminal spaces, like perhaps where the like city interferes with the ocean or like where like daylight and nightlife interfere and stuff like that. So I, I tried to map that out onto a map and I actually, I don't quite re- remember the results of my analysis, but yeah, I think I had a lot of fun playing with like maps and literature

[00:08:51] **Jeremy:** Yeah, that's really interesting. I think that, the visualization of I read a book and where did these people go? And like you said, where did these more magical things happen? And yeah, that would be interesting to know if there was a trend of these parts of Tokyo or these neighborhoods for some reason inspire people to, to see those things.

[00:09:16] Yeah.

[00:09:16] **Theo:** Yeah, and then it sort of allowed me to connect my passions of, Japan and literature, and then also I've had always had a passion for,computers. So it was like the perfect intersection of everything, and it allowed me to, like, really dive into stuff I didn't know about back then. So I, I had no idea about, like, how databases work, but, building a SaaS for, like, research forced me to, like, learn about SQL and stuff like that, and it, it made a lot of things click and was really a nice experience.

[00:09:50] **Jeremy:** Yeah, I think it's not until you build a project and then you really see how each piece comes together, whether it's, like you said, the database or the front end or back end. And basically everything before is all abstract, and then when it comes time to build something, that's when you realize, "Oh, these are, this is what I actually need to know."

[00:10:13] Yeah was there a specific, book or a specific thing from, I suppose, contemporary literature that got you interested in all this?


## Got interested due to Murakami's 1Q84

[00:10:23] **Theo:** Yeah. So I think it's a bit cliche, but like it's one of the, the Murakami books. It's, 1Q84. So ichi Q hachi yon is the Japanese title, and it's like a... I'd say it's like a, a romance set in Tokyo, and it really plays with like the, the spatial, arrangements of the city. actually mapping this out on a map was so interesting because, like, there's like two, protagonists, as you would have it with a romance, and like there's three books.

[00:10:57] It's a, it's a huge epic of like three books. And like during the first book, like their spheres of action, I think is the term I used back then, didn't like overlap at all because they were like... I don't wanna spoil the book for anyone, but like TLDR, it's like they used to be in the same class in school and had like this,I don't know, like meteorite, connection to each other.

[00:11:23] Like they immediately, felt connected, and then they got separated, and then they-- The book is about how they find back to each other in this like world where like a lot of magic events happen. And like books one and two, their like spheres of action on the map don't interlap at-- overlap at all. So like it's almost as if, like they're like separated physically from each other, and then the book and the events in the books like force them to like come closer and closer together, and that's like sort of on a geographic or cartographic level, like how they're like separated and then have to find back together, which I thought was like a, a beautiful metaphor.

[00:12:10] And maybe that's intrinsic to like every romance, but it was like really interesting finding that like connection on the map

[00:12:19] **Jeremy:** It's really cool how that also connects to your, your master's, thesis, was it? Where it's, you got interested because of the spatial component and then you you built, software basically researching that, that spatial component So we've kind of gone into how you got to Japan, how you got into programming and your experience with literature.

[00:12:45] Where did you go from there? How did you end up here? we're at the LINE offices today. How did you make that connection?


## Getting into programming and svelte

[00:12:52] **Theo:** So I basically building that, research project, I realized, wait, this is a lot more fun than I thought. It's like building web apps is super interesting. So I I always kinda knew that, being in academia, at least in academia when it comes to Japanese literature, is, like, not the most sustainable passion.

[00:13:18] So I wanted to, get a foothold in somewhere, in some area that, was related with, a bit more earning. I started freelancing from there, and, like, I actually did remote work from Japan for, like, um, companies in Germany where, like, friends had connected me with. And during that, I honestly, I had so little technical knowledge, and I wanted to get more knowledgeable.

[00:13:44] So I, I started researching online and I remember, like, bumping into React, and at the time I thought React was, like, the most complicated rocket science ever. And I couldn't grasp it. I saw, like, the, the hooks and, like, useEffects, and I was like, "No, I don't, I don't have the mathematical knowledge to do React."

[00:14:05] And I, I researched further, and I'm not sure if you're familiar with, Svelte and Rich Harris, but I saw this, talk by Rich Harris that is called Rethinking Reactivity, which is, I think, the talk he did just before announcing Svelte 3. And, it basically, suggests that, like, HTML is the mother language of the web, and therefore a web app should be authored in, like, a subset or, like, a superset of HTML rather than JSX with...

[00:14:37] J- JSX, which is a superset of, JavaScript. And to me, as a, like, person who was at the time not comfortable with, like, a lot of JavaScript code, that felt like such a revelation, and I was like, "Oh, wait, I can actually grok this," because this is just HTML, and then you have,the declarative logic sprinkled onto it.


## Starting Svelte offline meetups

[00:14:58] **Theo:** And I got really excited about Svelte, and I searched if there were, like, any meetups. And there were no meetups in Japan. There was, like, this one, fellow from Canada, Takoyaki, I think, was his name, and he was running this Discord server, Svelte Japan, and I was, I think, one of the first members to join that server, and I was like, "Let's do a offline meetup."

[00:15:19] And I think he was based not in Tokyo, so it, it was difficult to, do a meetup with him. But I found a couple of other folks, and I think I organized the first ever Svelte meetup in Japan. It was, like, in the stinky cellar of a Shinjuku hotel. It was pretty interesting looking back. But, uh, yeah, that allowed me to connect with, like- a lot of, web developers in Japan and like with the community, the growing community around Svelte.

[00:15:54] And I, at that s- time, I also got more active on Discord, on the Svelte Discord. First, like I came there to ask questions because I had no clue about programming, and I, I asked, like looking back, I asked the most basic questions and like there were so many kind people helping me and like not just giving me the solution, but like help me arrive at the solution on my own terms, and they were like really patient with helping me learn.

[00:16:21] And I really appreciated that, and I thought to myself, "I wanna be that person. I wanna be the, the person like helping others understand this." And through that, I got like more and more active on the Svelte Discord, and also more and more on the Japanese community side of things. And I think around that time, I did my first open source contribution to Svelte.

[00:16:44] Looking back at that PR, I think it... Like nowadays I would be in horror, like just seeing it. I think I, I committed the like entire node modules to the,

[00:16:53] **Jeremy:** Oh, 

[00:16:54] **Theo:** repo or something. But like once again, the Svelte maintainers were super nice about me, and they told me, "Hey, you don't do that." And, uh, that's how I learned a lot.


## Only applying to LINE

[00:17:05] **Theo:** And yeah, so I guess that was my transition into actual software development, like the, the Svelte ecosystem. And I started contributing and, like, uh, being more a-active. And when the time came and I was about to graduate university, I was like, "I wonder if I can work in this field." And I did some research, and it just happened to be that, the LINE offices were right next to my university.

[00:17:35] So I went to Sophia University, which is quite close from where we are, and the, the LINE office used to be in a different building back then, but it's still quite close to where we are right now. And I saw that, and I... It f- felt like fate. no way, it's, right next to my university. So I, I, I thought, "I'll just give it a shot."

[00:17:53] I didn't think I ha- I'd have any chance to, like, work at a big tech company, so I just applied there. And, like most, people in Japan, when graduating university, they apply to... They do this, it's called shukatsu, which means, basically job hunting. And, you buy, like, a suit, and then you apply at, I don't know, 30 or 40 companies, and then you go, to the interviews, and it's, a really gruesome process, and I didn't wanna go do that.

[00:18:19] So I was like, "It's gonna be LINE," because I really e-enjoyed their app, or no one else. So I only applied to them. And I thought my backup plan was, if it d-doesn't work out, I'll, A, either stay in academia or, B, I'll continue freelancing. And somehow mirac-miraculously it, worked out, and I've been here ever since.

[00:18:45] I, I think I've grown a lot as an engineer. I have, amazing peers, amazing colleagues, amazing superiors. I really learned a lot.

[00:18:55] **Jeremy:** that's, that's pretty amazing to, apply to one place and get it.

[00:18:59] **Theo:** It was like a, a one shot.


## The progression of the Svelte Japan meetups

[00:19:01] **Jeremy:** yeah. yeah.Yeah, so you were running this, this Svelte meetup here, right? And you said it started just in some b- basement hotel. Um, is it, uh... How has it grown? Do you still run in-person meetups or

[00:19:19] **Theo:** So I am still involved with the community, especially the, the Svelte Japan community, but like turns out there are people way more capable of like making connections and like running events than me. And, um, there's this, person called Yuki, and he has taken over since, and he like... We literally changed in entire different levels.

[00:19:43] Like we're like now being hosted at like the DeNA offices in Shibuya on like the 35th floor of like some skyscraper. It's like it doesn't compare at all. And so I still, I, I really enjoy going to these events and I, I still enjoy hanging out with all those folks. Yeah. But not as involved anymore

[00:20:05] **Jeremy:** So as an attendee. As an attendee. Uh, yeah, yeah, yeah. Yeah. Less, less work that way too. 

[00:20:11] **Theo:** That's less work, yeah


## What's LINE?

[00:20:13] **Jeremy:** I think a lot of people, if they don't live in Japan, they don't necessarily know what LINE is. Could you maybe talk about what it is?

[00:20:22] **Theo:** Okay, so yeah,that's an important thing to cover. So LINE is basically WhatsApp in Japan, but it's, it does more than WhatsApp does. So probably people listening have heard of WeChat, the like Chinese super app where you can buy stuff and there's like payments integrated into the app and like mini apps running on the app, and LINE is sort of the Japanese, equivalent of that.

[00:20:51] I first got in touch with it actually when I came here in 2014, the f- very first time, uh, f- for my working holiday. And back then in Germany, like WhatsApp was, had already kicked off, but like people were only using it to message. And if you wanted to call, you would still use the normal like telephone LINEs to call people.

[00:21:13] But I came here and no one was like ever exchanging phone numbers or anything. You would just exchange your LINE, and back then you would exchanging by shaking your phone. And if you would shake your phone in the vicinity of somebody else, the phones would interpret the shaking as you wanting to exchange contacts, and then the people shaking their phones would like pop up in your LINE app and you could add them as friends. 

[00:21:37] **Jeremy:** Okay. (laughs) 

[00:21:38] **Theo:** It was so cool, and I was like blown away by it. And then also, it has since been retired. I actually don't know why. Maybe it was too goofy. But yeah, I... Like the first time I came here, I would just go, let's say, to the beach with my friends, and there was like a friend I didn't know, and then we were like, "Let's, exchange contacts," and we would

[00:21:59] just 

[00:21:59] **Jeremy:** shake.

[00:22:00] **Theo:** Each other's phones. Yeah.

[00:22:03] **Jeremy:** Yeah, it, it is interesting how each country has a different, way of doing text messages or or voice. Like you said, a lot of other countries use WhatsApp,um, and then WeChat in China. And I, I think in the United States it feels like people are m- mostly using just iMessage or regular text messages.

[00:22:25] Uh, so I'm not really sure how all these things happened, but- Yeah ... each country has picked their own way of doing things, I suppose.

[00:22:35] **Theo:** It's like, it's almost as if they all developed at the same time, and as such, the apps, fit different ecological, niches almost, like ecological... Different parts in the ecosystem depending on what the country needed at the time. And actually, LINE started out just after the 2011 earthquake.

[00:22:58] Back in the day, LINE Corporation still was... So it's no longer LINE Corporation, it's LY Corporation nowadays, since we merged with Yahoo Japan. but back in the days, it used to be NHN, which is, the, the Japanese branch of Naver, which is a Korean company. And then, the big earthquake hap- happened in 2011, and, like, people really had, like, issues reaching out to their loved ones.

[00:23:28] And, LINE actually got initiated as a project to help connect people after, like, disasters, because the phone LINEs got, massively overloaded after the disaster. And, like, it was thought that if you used, mobile internet, you could, fit a lot more bandwidth into the same slot. So that's, uh, the, I think, initial thought that started LINE app, which is a very nice thing, yeah.

[00:23:57] And it just exploded from there. nowadays, I think you would really have to look for a while to find a Japanese person who doesn't have LINE installed on their phone. It's just, the default messaging app.

[00:24:10] **Jeremy:** Yeah, it's interesting that you mentioned that it was the, the Japanese branch of Naver, which you said was a Korean company, 'cause I think Korea, they also have their own messaging systems that they use. Is, is there one by Naver as well? 

[00:24:25] **Theo:** There's, it's not by Naver, it's by Kakao. 

[00:24:27] **Jeremy:** Kakao. Oh, okay okay. 

[00:24:28] **Theo:** the Korean one.

[00:24:29] **Jeremy:** Okay. KakaoTalk, right? yeah, yeah.

[00:24:32] yeah, everybody's got their own, so now we have to have all the different apps on our phones.

[00:24:37] **Theo:** I have like, yeah, I think I have at least 15 messenger apps on my phone, including Signal, 


## Line integrated browser for businesses

[00:24:44] **Jeremy:** That's right. Yeah, those have gotten big too. Yeah. at least for your part now that we've kind of explained what LINE is, um, what do you work on at LINE?

[00:24:55] **Theo:** So there's this thing called official accounts, which means basically if you run a business, you can have an account on LINE, and you can have people add you as a friend, and then you can, like, do customer relations via that. You can, contact your friends and send out coupons, send out,reward cards and stuff like that.

[00:25:16] And, those are deeply integrated into the native app, but a lot of the, like, additional features run as mini apps on the native app. And the native app has, a special browser. It's called the Liff Browser. If you're ever curious, you can Google it. There's, an, a API that has been published and everything.

[00:25:34] It's L-I-F-F, and, it's short for LINE Integrated Frontend Framework. And it's basically this special browser where once you open it, your auth token is automatically injected. Mini apps don't need you to log in. They can just reuse your LINE login for, doing stuff. And I work on a team that maintains, quite a few of those mini apps, and we're only six people at the time, but we...

[00:26:06] I think we maintain, seven or eight quite big mini apps, which is interesting because, like, with LINE, since basically everyone in Japan uses it, everything has, like, huge scale. You roll out something new, and you're like, you check, like, Sentry or something for the logs to see how everything is doing.

[00:26:26] And, instead of, having a few hundred requests, you get, a few hundred thousand requests or something. It's, it's a really, interesting scale of things, and it's really rewarding because when I go to, like, a restaurant or something, most places actually use the apps that I build for work.

[00:26:44] So it's really easy if I go with friends and they ask, "What do you even do?" I can just point at something and like, "This screen, I built this screen," or, "I made this button green," or something. 

[00:26:55] **Jeremy:** Can you give an example for people who haven't seen these apps, like a specific way that they would see it and what it did?


## Order with LINE

[00:27:04] **Theo:** So I think the most interesting app is the one I've been working on recently. It's it's called Order with LINE, and it l- allows you in restaurants... They would put up, either a, a QR code or like a NFC thing that you can touch to start the app, and then it opens, this mini browser inside the LINE app, and you can order straight from your table.

[00:27:26] In Japan, it's, surprisingly common now to, like, not talk to your waiters anymore, but instead order from, like, a little mini app. And, it's, integrated with the a- with the app in that, for example, if you forgot to send your card, you will get, a notification, a native notification from your app that you forgot to send your card.

[00:27:46] Or, you can look at your... even after you've paid, you can look at the things you ordered because it still remembers you via your LINE account 

[00:27:56] **Jeremy:** Okay. Yeah. What I've personally seen a lot of times is it's a website outside of an app, but you're saying that, some of these businesses, when you scan the QR code they give you, it actually opens up LINE and has you do those transactions inside of LINE

[00:28:12] **Theo:** We actually launched two months ago or three months ago, so it's still rolling out, but I suspect the next time you're gonna be in Japan, you're gonna see it a lot more often. I hope, I hope. 

[00:28:23] **Jeremy:** yeah, it's always a little tricky too where sometimes depending on where the business is, maybe your connection isn't so good and you're trying to do the QR code thing and it's like, "Hmm."

[00:28:36] **Theo:** Yeah. I try to be as, uh, thoughtful with, people's data as possible. So I, I actually... I got to be tech lead on this project, so of course I picked Svelte, which is, famous for smaller bundles than React. So I thought, if people... once a store adopts this app, people are basically forced to use it, right?

[00:28:59] Because it's the default way of ordering inside the store. And whenever you have those sorts of situations where people can't really pick which app they wanna use, I feel like you have to be really responsible about, the amount of JavaScript they have to download, the, like, amount of, like, annoyances they f- face, when using your app.

[00:29:21] So we made it explicitly so you don't have to use it within LINE. For example, if you're a tourist or something and you don't have LINE, you can, uh, open it in a web browser. And then also, like, you don't have to add the store as a friend, because, some people think that's annoying or they don't wanna give away their, contact to a place.

[00:29:40] So I was very conscious about that building this app

[00:29:44] **Jeremy:** Yeah, that makes sense. I actually remember, uh, this trip, there was a conveyor belt sushi place that to see what place you were in line or, or, yeah, in a literal line in the queue, uh, yeah, they wanted you to add them as a friend, um, so that they would message you your position in queue. And,I mean, I did it, but I also felt like that's a little odd, not, I'm not your friend, right? Uh, in terms of the business anyways.

[00:30:14] **Theo:** I mean, it makes sense from, like, a small business perspective. They, they want you, to become a recurring customer, and then they, if they have your contact, they probably won't even do anything nefarious with it. They just wanna, like, remind you of their existence

[00:30:29] **Jeremy:** But that's good though that you, you've probably personally had your own issues or annoyances where you have friends come visit who, who don't have LINE or aren't familiar with it. So letting them be able to check out and not have to go make an account and all that, I think that's that's really helpful, especially for people who don't necessarily live here.


## Getting the team to use Svelte

[00:30:52] **Jeremy:** So you said you used, uh, Svelte for this. was your team all familiar with Svelte before you started this project?

[00:31:00] **Theo:** They were not. And I had to do a lot of convincing work. actually I, like ever since a previous project, I wanted to use Svelte, and I didn't just wanna use the framework Svelte, I wanted to use the meta framework that is, available. It's called SvelteKit. It's basically like what Next.js is to React.

[00:31:19] And, being young and foolish, I wanted to like go all in on it, like because it was the hot new stuff and I wanted to try it. But my manager actually, being the voice of reason, he was like, "Wait, so you are familiar with this. You have contributed to Svelte. You're like a Svelte stan. You read all the news and everything, but the other folks on this team are not."

[00:31:41] Like, we usually work in Vue, which is a great framework as well, I think. But like,I, I just wanted to work with Svelte, and I think there were like a couple of good reasons why we should have picked Svelte, because like the bundle size at the time was even smaller, and then it featured like a lot of, features that made the end user experience better.

[00:32:04] So it's, really easy to build,nice UIs with, like, animations and stuff in Svelte, and then it w- had, like, really sophisticated bundle splitting to make, the bundle sizes when, when downloading the app, as small as possible. And,it also had, like, great developer experience, so I wanted to get my colleagues to experience that as well.

[00:32:22] But I think my manager was right at the time to, like, sort of stop me and be like, "Hey, this is not the right time to, just, introduce something new." So we instead did something different.


## Starting with file-based routing

[00:32:35] **Theo:** So SvelteKit, features file-based routing, and at the time my team had never, worked with, apps that had file-based routing.

[00:32:45] And, recently even, Next.js and, most meta frameworks have switched to this model of, like, sort of declaratively, stating which routes you have based on your file system. So my, my boss was like, "Why don't we just, try to get this one part that SvelteKit offers and, get, everyone familiar with that first, and then evaluate if we wanna take the next step and, go on and, maybe use SvelteKit in a future project."

[00:33:12] And I think, like, looking back, I think that was what... why I was junior and he was senior. Like, I really grew a lot, due to that experience. But, like, we, we picked this library that allowed us to have file-based routing in Vue, which, at the time it was called unplugin-vue-router, but, now it's called...

[00:33:32] it's just Vue Router, like Vue Router has merged with them or with it. And, yeah, the team, it was really a slam dunk because the team really enjoyed the way of how it, how it made routing in the app obvious, and how you no longer needed to look at, like, a huge imperative file to understand which routes are, like, routed to in which situations.

[00:34:00] And it also introduced this concept of loaders, which a lot of frameworks have nowadays, where, each route declares, like, a, a loader that runs before the router, enters the page, and it made, working with data a lot easier in, like, SPAs. So yeah. it took some convincing and, we did this, first step of, I don't know, this was probably three years ago, where we introduced, file-based routing at first, and then the team really enjoyed it.

[00:34:30] And w- then we also started with, web components, and, at the time I felt like Svelte had the most compelling front-end framework, integration with w- web components and, building web components. So we picked Svelte for that as well. And without,diving into Svelte, we got the team familiar with the technologies required for SvelteKit.

[00:34:50] And then I think I, I can't really take any credit for that. that's all my managers working, and I learned so much, doing that. But yeah, when we started the current project, the Order with LINE project, a year ago, everyone was familiar with Svelte. Everyone was familiar with file-based routing.

[00:35:09] So at that point it was just like a matter of putting the two together and actually adopting SvelteKit, and I think the team has really enjoyed working with it

[00:35:18] **Jeremy:** So the file-based routing that was in a existing project that you introduced it, and then when you were talking about the web components, is it where you were using web components in a project or was it where they were just getting familiar with them?


## Web components to make components sharable across projects

[00:35:33] **Theo:** No, it was, uh, it was a different project. My team has way too many projects. Uh, if you, if you wanna hi- work with us, we're hiring. yeah. So we have... Having that many projects, we kinda wanna share a lot of the UI code we have, and we were always looking for ways to do that. We initially started out, sharing actual Vue components, but that is fragile because you need to care about, like, are the runtime versions compatible, and stuff like that.

[00:36:03] And then, other projects that were not directly affiliated with us also wanted to start using our, like, shared components, and that's where everything breaks down, because you can't just, run Vue inside React or... yeah, it just crashes and burns. So that was the reason why we, we started, like, an internal component library that compiled to web components.

[00:36:29] So we didn't wanna author web components because, even if you use a framework like Lit, the DX of that is quite manual and quite involved, and we wanted to be at a higher level so we can move faster. We didn't have that m- many, really complex, like UIs, so it was fine to work at a high level.

[00:36:51] And for that, we picked, uh, Svelte simply because we wanted to get familiar with it. And, so this is actually no longer true for Svelte 5, but at the time, Svelte 3 and Svelte 4, they also had by far the lowest, the smallest bundle sizes for web components when w- when compiling to web components. And I thought that was really attractive for the thing we tried to do, so that's why we picked Svelte.


## Svelte added a runtime and increased bundle size

[00:37:16] **Jeremy:** Hmm. And when you say it's no longer true, does that mean the si- the bundle got bigger or?

[00:37:20] **Theo:** actually, so, uh, Svelte, like Svelte 4 to Svelte 5 was quite the breaking change. I don't know if you're familiar, but they introduced something that's called runes. it's a new way of authoring, reactivity inside the Svelte components, Behind the scenes, it's very similar to how a lot of front-end frameworks have started to do things, which is they use, signals.

[00:37:46] So Ryan Carniato, the, the creator of SolidJS, which is like the, the underdog under the frameworks, he, popularized this new paradigm of reactivity where, you're no longer, like, diffing parts of your app, but it's mostly about, really fine-grained reactivity, and you have, a, a signal that tr- directly triggers, like, derived effects or effects.

[00:38:17] And, that comes with, a bunch of benefits, and, is actually way faster, so that's why, Svelte changed to that model. But the downside or the trade-off they had to make is now Svelte used to, like, compile away. It would have no runtime, but it, it would... At compile time, it would, like, sort of inline all the reactivity.

[00:38:42] But, that doesn't work anymore if you use signals. So now there's, a small... It's a quite the small runtime, but it does have a runtime, and when you ship, web components, you usually have to include that runtime into every web component, so the, the baseline of how small a web component can be as in bundle size becomes bigger.

[00:39:04] And yeah, I think that's basically the only trade-off they made with the move to signals, and it kinda kneecapped the web component story, but I still think it was the right move to make for them.

[00:39:18] **Jeremy:** So in your own projects, you would choose to use signals and just take the, the hit on the the size?

[00:39:24] **Theo:** Yeah, I think, I think it depends on what you wanna do. if you really wanna get the smallest bundle size for your users, you should probably author your components by hand. But that that comes with, massive cost in terms of developer experience, because writing web components, even nowadays, still is no treat.

[00:39:45] There are so many rough edges, and, if you use something like Lit, it becomes a bit more bearable, but it's still very, low level, and it, it's still very imperative. And if you wanna do, declarative development of, uh, web components, which I think is, a huge gain when it comes to,developer ex-experience and productivity as well, as in how fast you can move, I think picking, like, a framework like Svelte is the right thing to do.

[00:40:13] And actually, I recently created a open source project, svebcomponents. The name is terrible, I know, but it's basically this library to make working with web components in Svelte even easier, and, creating web components with Svelte even easier


## Works on frontend, the backend and scaling is for another team

[00:40:30] **Jeremy:** One of the things you mentioned earlier was that working with the scale you do here, you saw a lot of new problems. Can you give an example of one of those and how you, you addressed it?

[00:40:43] **Theo:** So the, the best thing about my job here is that I only do front-end development. So the people who have to worry about the scale is not my team. It's other people. It's the back-end people, and I think they, they face way more problems with that. For us, it's mostly... Like, for... If you're building an SPA, you don't really care if it's, 1,000 users or a million users that, use it.

[00:41:09] I mean, you wanna be careful about, not being wasteful with, API calls, and you don't wanna DDoS your own server. So obviously we're conscious about that. But honestly, there's not too much besides from that that we have to be careful about. It's quite comfortable. Yeah. 

[00:41:28] **Jeremy:** It's, uh, I imagine the, the backend team would have a very uh, story to tell.

[00:41:33] **Theo:** Definitely. I mean, they're the ones with, like, the pagers ringing at night

[00:41:38] **Jeremy:** Uh, okay. okay. So you don't, you don't have that, I guess. 

[00:41:41] **Theo:** I have a pager, but it never rings because,

[00:41:43] **Jeremy:** That's good. That's good. (laughs) 

[00:41:46] it's hard to even think about just, the amount of people using, just the chat part of the app,it has to be getting used all the time so frequently, so there's there's gotta be very interesting, uh, architecture decisions there.


## Hosting UiT Inside Podcast

[00:42:01] **Jeremy:** one thing we haven't talked about is you actually have your-- or you host a, a podcast yourself. could you tell us, like, a little bit about how that started and what that's about?

[00:42:11] **Theo:** So that's... Yeah. I host the UiT Inside podcast, which is mostly in Japanese. Sometimes we do, episodes in English. and that basically started at work. So UiT is the name of the front-end organization at LINE. And one of my good friends and colleagues here, Alan Davalos, I don't know if he's gonna listen to this, actually asked me about, wanting to come on for an episode, I think back when Lit version three was first released, and we just chatted about Lit.

[00:42:46] And it ended up being really fun, and I had... Yeah, I really enjoyed talking about tech. I'm really passionate about tech, as you can probably tell. so I, I sort of got hooked, and I, I continued making episodes. And at first, I, I came on as a guest, and I was just, like, the sidekick to the main host and would,throw in, things I had picked up on the internet or, like, uh, bring up, my own experiences.

[00:43:14] But then I, I moved into becoming a host myself, and you don't believe, like, how nervous I was, like, being a host in Japanese in, not m- not my mother tongue and, like, speaking to really, amazing people in tech. So I've had, I've had on people like sapphi-red from the Vite core team. I had people on like, um, Anthony Fu, Dan Abramov, like, all those people I look up to.

[00:43:41] And I think that's also one of the other perks of, hosting a podcast because you can... I think we talked about this earlier. You, you get to, talk to people you otherwise would have had no chance to meet or, like, talk to. It's such a privilege. Yeah. I've also gotten to go to,conferences to, like, gather, content for the podcast.

[00:44:00] So I've been to Vue Fes a couple times, which is such an amazing experience. if you're even slightly, like, involved with the Vite, Vue or, general web dev audience, I think you would have a blast at Vue Fes. And then, Google I/O. I went to Google I/O three times and did, like, podcasts about that as, as well.

[00:44:22] It was really interesting. And, like, seeing how a, big corporate conference works in the US. Yeah, I I slid into it and, things escalated from there and yeah.


## English usage at LINE

[00:44:35] **Jeremy:** Yeah, I think something that you mentioned that's interesting is that most of the recordings are in Japanese with a few that are English. For the, for your coworkers here at at LINE, would you say that most of your business is done in Japanese? Japanese Like, what is the... Is English used here? Would they understand the podcast that you recorded, for example, with, Dan Abramov?

[00:45:02] **Theo:** so when it comes to English, some teams at LINE use English actually as their primary language, but that's mostly, like the native teams that work on the actual messenger app. for my team, it's like 100% Japanese, and I always joke that, the people who start at LINE are the brightest people in Japan that don't speak English.

[00:45:28] Yeah, a lot of people obviously can read English, and they have no, problems, like reading, like English documentation or something. But when it comes to something like a podcast where it's like native people speaking like full on speed, and there's like also a lot of like, difficult ways to formulate something or I don't know.

[00:45:52] Like for example, with me, I'm not native. I'm not a native English speaker, so like sometimes I end up phrasing things in a weird way. And I think since my native language is like a Germanic language, which is the same family as English, it still somehow works. But like people really underestimate how different Japanese is from English.

[00:46:12] Like they're so completely different, like nothing is similar. And I think like a lot of people are like quite harsh on Japanese people not being like in the average, not being great English speakers. But man, those languages are so different. And yeah, you, you don't pick that up just from like standard ed-education

[00:46:36] **Jeremy:** Yeah, it's always different learning a language in school. I'm from the United States. We all take foreign languages, but I would guess that the average American's ability to speak one is lower than the average Japanese person's ability to speak English. So, don't be too hard on yourselves, I guess. Yeah. But that is interesting though that it, you, you're saying it's on a team-by-team basis that that some would communicate in Japanese and some would communicate in English

[00:47:10] **Theo:** Maybe 95% of the company, like the daily communication is in Japanese. And then for the rest of the 5%, it's not even all English, it's Chinese and Korean. 

[00:47:21] And then I think English is this tiny blob where like some teams speak in English, but it's honestly just a few teams.

[00:47:28] Like it's a very big company. I just, I don't know like the exact numbers, but I think there's like over 20,000 employees.

[00:47:37] Most of them don't speak English on a day-to-day basis.

[00:47:42] **Jeremy:** since you would say 95% speak Japanese,uh, I, I assume that the vast majority of the employees are probably native speakers as well then, yeah. I'm not sure how true it is, but somebody was telling me that, was just in engineering teams, but at Rakuten they were trying to use English more natively, I guess, within the company.

[00:48:04] **Theo:** Yeah, I think Rakuten made the decision to only speak in English. the, the company is English first, and I think Mercari, the, like, eBay of Japan, so to say, also made the same decision. So there's a few companies, PayPay as well, I think, that, I think it's mostly about the ability to hire foreign talent

[00:48:25] **Jeremy:** They decided that English should be their, primary form of communication, yeah

[00:48:29] yeah, I guess we've kinda covered a lot. Is there, there anything else you wanted to mention or think we should've talked about?

[00:48:37] **Theo:** Yeah, if we still have some time, I would love to talk about like at Proto or something because 

[00:48:42] you reached out to me not on Twitter, but on Blue Sky, which I think is kinda uncommon, so

[00:48:47] **Jeremy:** Yeah, that's a whole-- thing that's going on. 

[00:48:49] **Theo:** It's a huge rabbit hole, so I don't know if we have time to get 

[00:48:52] into that 

[00:48:54] **Jeremy:** not today, but yeah, yeah, maybe sometime in the future. That would be a fun one. 

[00:48:58] **Theo:** Yeah. I'm pretty AtProto pilled, and if I can like shamelessly plug the, the podcast I recorded with Dan Abramov was on like the AtProto,

[00:49:06] **Jeremy:** 

[00:49:06] **Theo:** protocol. So if someone is interested, please feel free to listen to that

[00:49:12] **Jeremy:** For sure. Uh, we'll put that one in the show notes. And that one is in English, so don't don't worry. (laughsc) Theo, if people wanna see what you're up to or check out your podcasts, uh, where should they look?

[00:49:24] **Theo:** So I think the easiest place would be my homepage, which is, T-H-E-O-S-T-E-I-N-E-R.de, so theosteiner.de

[00:49:35] **Jeremy:** Theo thank you so much for for joining me today. This was fun. 

[00:49:37] **Theo:** Thank you so much for having me on 