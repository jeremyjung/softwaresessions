+++
title = "Bryan Cantrill on Oxide Computer"

description = "Why the biggest cloud providers build their own hardware"

[extra]
episode_url = "https://pinecast.com/listen/5898fc0b-bdd7-423a-b428-08f56a2eaf42.mp3"
social_title = "Bryan Cantrill on Oxide Computer"
social_description = "Why the biggest cloud providers build their own hardware"
+++

Bryan Cantrill is the co-founder and CTO of Oxide Computer Company.

We discuss why the biggest cloud providers don't use off the shelf hardware, how scaling data centers at samsung's scale exposed problems with hard drive firmware, how the values of NodeJS are in conflict with robust systems, choosing Rust, and the benefits of Oxide Computer's rack scale approach.

This is an extended version of an interview posted on Software Engineering Radio.

## Related links

- [Oxide Computer](https://oxide.computer)
- [Oxide and Friends](https://oxide-and-friends.transistor.fm)
- [Illumos](https://illumos.org)
- [Platform as a Reflection of Values](https://www.youtube.com/watch?v=Xhx970_JKX4)
- [RFD 26](https://rfd.shared.oxide.computer/rfd/26)
- [bhyve](https://bhyve.org)
- [CockroachDB](https://www.cockroachlabs.com)
- [Heterogeneous Computing with Raja Koduri](https://oxide-and-friends.transistor.fm/episodes/heterogeneous-computing-with-raja-koduri)

## Transcript

[You can help correct transcripts on GitHub](https://github.com/jeremyjung/softwaresessions/tree/master/content/episodes).


## Intro

[00:00:00] **Jeremy:** Today I am talking to Bryan Cantrill. He's the co-founder and CTO of Oxide computer company, and he was previously the CTO of Joyent and he also co-authored the DTrace Tracing framework while he was at Sun Microsystems.

[00:00:14] **Jeremy:** Bryan, welcome to Software Engineering radio. 

[00:00:17] **Bryan:** Uh, awesome. Thanks for having me. It's great to be here.

[00:00:20] **Jeremy:** You're the CTO of a company that makes computers. But I think before we get into that, a lot of people who built software, now that the actual computer is abstracted away, they're using AWS or they're using some kind of cloud service. So I thought we could start by talking about, data centers.

[00:00:41] **Jeremy:** 'cause you were. Previously working at Joyent, and I believe you got bought by Samsung and you've previously talked about how you had to figure out, how do I run things at Samsung's scale. So how, how, how was your experience with that? What, what were the challenges there?


## Samsung scale and migrating off the cloud

[00:01:01] **Bryan:** Yeah, I mean, so at Joyent, and so Joyent was a cloud computing pioneer. Uh, we competed with the likes of AWS and then later GCP and Azure. Uh, and we, I mean, we were operating at a scale, right? We had a bunch of machines, a bunch of dcs, but ultimately we know we were a VC backed company and, you know, a small company by the standards of, certainly by Samsung standards.

[00:01:25] **Bryan:** And so when, when Samsung bought the company, I mean, the reason by the way that Samsung bought Joyent is Samsung's. Cloud Bill was, uh, let's just say it was extremely large. They were spending an enormous amount of money every year on, on the public cloud. And they realized that in order to secure their fate economically, they had to be running on their own infrastructure.

[00:01:51] **Bryan:** It did not make sense. And there's not, was not really a product that Samsung could go buy that would give them that on-prem cloud. Uh, I mean in that, in that regard, like the state of the market was really no different. And so they went looking for a company, uh, and bought, bought Joyent. And when we were on the inside of Samsung.

[00:02:11] **Bryan:** That we learned about Samsung scale. And Samsung loves to talk about Samsung scale. And I gotta tell you, it is more than just chest thumping. Like Samsung Scale really is, I mean, just the, the sheer, the number of devices, the number of customers, just this absolute size. they really wanted to take us out to, to levels of scale, certainly that we had not seen.

[00:02:31] **Bryan:** The reason for buying Joyent was to be able to stand up on their own infrastructure so that we were gonna go buy, we did go buy a bunch of hardware.


## Problems with server hardware at scale

[00:02:40] **Bryan:** And I remember just thinking, God, I hope Dell is somehow magically better. I hope the problems that we have seen in the small, we just. You know, I just remember hoping and hope is hope. It was of course, a terrible strategy and it was a terrible strategy here too. Uh, and the we that the problems that we saw at the large were, and when you scale out the problems that you see kind of once or twice, you now see all the time and they become absolutely debilitating.

[00:03:12] **Bryan:** And we saw a whole series of really debilitating problems. I mean, many ways, like comically debilitating, uh, in terms of, of showing just how bad the state-of-the-art. Yes. And we had, I mean, it should be said, we had great software and great software expertise, um, and we were controlling our own system software.

[00:03:35] **Bryan:** But even controlling your own system software, your own host OS, your own control plane, which is what we had at Joyent, ultimately, you're pretty limited. You go, I mean, you got the problems that you can obviously solve, the ones that are in your own software, but the problems that are beneath you, the, the problems that are in the hardware platform, the problems that are in the componentry beneath you become the problems that are in the firmware.


## IO latency due to hard drive firmware

[00:04:00] **Bryan:** Those problems become unresolvable and they are deeply, deeply frustrating. Um, and we just saw a bunch of 'em again, they were. Comical in retrospect, and I'll give you like a, a couple of concrete examples just to give, give you an idea of what kinda what you're looking at. one of the, our data centers had really pathological IO latency.

[00:04:23] **Bryan:** we had a very, uh, database heavy workload. And this was kind of right at the period where you were still deploying on rotating media on hard drives. So this is like, so. An all flash buy did not make economic sense when we did this in, in 2016. This probably, it'd be interesting to know like when was the, the kind of the last time that that actual hard drives made sense?

[00:04:50] **Bryan:** 'cause I feel this was close to it. So we had a, a bunch of, of a pathological IO problems, but we had one data center in which the outliers were actually quite a bit worse and there was so much going on in that system. It took us a long time to figure out like why. And because when, when you, when you're io when you're seeing worse io I mean you're naturally, you wanna understand like what's the workload doing?

[00:05:14] **Bryan:** You're trying to take a first principles approach. What's the workload doing? So this is a very intensive database workload to support the, the object storage system that we had built called Manta. And that the, the metadata tier was stored and uh, was we were using Postgres for that. And that was just getting absolutely slaughtered.

[00:05:34] **Bryan:** Um, and ultimately very IO bound with these kind of pathological IO latencies. Uh, and as we, you know, trying to like peel away the layers to figure out what was going on. And I finally had this thing. So it's like, okay, we are seeing at the, at the device layer, at the at, at the disc layer, we are seeing pathological outliers in this data center that we're not seeing anywhere else.

[00:06:00] **Bryan:** And that does not make any sense. And the thought occurred to me. I'm like, well, maybe we are. Do we have like different. Different rev of firmware on our HGST drives, HGST. Now part of WD Western Digital were the drives that we had everywhere. And, um, so maybe we had a different, maybe I had a firmware bug.

[00:06:20] **Bryan:** I, this would not be the first time in my life at all that I would have a drive firmware issue. Uh, and I went to go pull the firmware, rev, and I'm like, Toshiba makes hard drives? So we had, I mean. I had no idea that Toshiba even made hard drives, let alone that they were our, they were in our data center.

[00:06:38] **Bryan:** I'm like, what is this? And as it turns out, and this is, you know, part of the, the challenge when you don't have an integrated system, which not to pick on them, but Dell doesn't, and what Dell would routinely put just sub make substitutes, and they make substitutes that they, you know, it's kind of like you're going to like, I don't know, Instacart or whatever, and they're out of the thing that you want.

[00:07:03] **Bryan:** So, you know, you're, someone makes a substitute and like sometimes that's okay, but it's really not okay in a data center. And you really want to develop and validate a, an end-to-end integrated system. And in this case, like Toshiba doesn't, I mean, Toshiba does make hard drives, but they are a, or the data they did, uh, they basically were, uh, not competitive and they were not competitive in part for the reasons that we were discovering.

[00:07:29] **Bryan:** They had really serious firmware issues. So the, these were drives that would just simply stop a, a stop acknowledging any reads from the order of 2,700 milliseconds. Long time, 2.7 seconds. Um. And that was a, it was a drive firmware issue, but it was highlighted like a much deeper issue, which was the simple lack of control that we had over our own destiny.

[00:07:53] **Bryan:** Um, and it's an, it's, it's an example among many where Dell is making a decision. That lowers the cost of what they are providing you marginally, but it is then giving you a system that they shouldn't have any confidence in because it's not one that they've actually designed and they leave it to the customer, the end user, to make these discoveries.

[00:08:18] **Bryan:** And these things happen up and down the stack. And for every, for whether it's, and, and not just to pick on Dell because it's, it's true for HPE, it's true for super micro, uh, it's true for your switch vendors. It's, it's true for storage vendors where the, the, the, the one that is left actually integrating these things and trying to make the the whole thing work is the end user sitting in their data center.


## AWS / Google are not buying off the shelf hardware but you can't use it

[00:08:42] **Bryan:** There's not a product that they can buy that gives them elastic infrastructure, a cloud in their own DC The, the product that you buy is the public cloud. Like when you go in the public cloud, you don't worry about the stuff because that it's, it's AWS's issue or it's GCP's issue. And they are the ones that get this to ground.

[00:09:02] **Bryan:** And they, and this was kind of, you know, the eye-opening moment. Not a surprise. Uh, they are not Dell customers. They're not HPE customers. They're not super micro customers. They have designed their own machines. And to varying degrees, depending on which one you're looking at. But they've taken the clean sheet of paper and the frustration that we had kind of at Joyent and beginning to wonder and then Samsung and kind of wondering what was next, uh, is that, that what they built was not available for purchase in the data center.

[00:09:35] **Bryan:** You could only rent it in the public cloud. And our big belief is that public cloud computing is a really important revolution in infrastructure. Doesn't feel like a different, a deep thought, but cloud computing is a really important revolution. It shouldn't only be available to rent. You should be able to actually buy it.

[00:09:53] **Bryan:** And there are a bunch of reasons for doing that. Uh, one in the one we we saw at Samsung is economics, which I think is still the dominant reason where it just does not make sense to rent all of your compute in perpetuity. But there are other reasons too. There's security, there's risk management, there's latency.

[00:10:07] **Bryan:** There are a bunch of reasons why one might wanna to own one's own infrastructure. But, uh, that was very much the, the, so the, the genesis for oxide was coming out of this very painful experience and a painful experience that, because, I mean, a long answer to your question about like what was it like to be at Samsung scale?

[00:10:27] **Bryan:** Those are the kinds of things that we, I mean, in our other data centers, we didn't have Toshiba drives. We only had the HDSC drives, but it's only when you get to this larger scale that you begin to see some of these pathologies. But these pathologies then are really debilitating in terms of those who are trying to develop a service on top of them.

[00:10:45] **Bryan:** So it was, it was very educational in, in that regard. And you're very grateful for the experience at Samsung in terms of opening our eyes to the challenge of running at that kind of scale.

[00:10:57] **Jeremy:** Yeah, because I, I think as software engineers, a lot of times we, we treat the hardware as a, as a given where,

[00:11:08] **Bryan:** Yeah.

[00:11:08] **Bryan:** Yeah.


## There's software in chard drives

[00:11:09] **Jeremy:** It sounds like in, in this case, I mean, maybe the issue is not so much that. Dell or HP as a company doesn't own every single piece that they're providing you, but rather the fact that they're swapping pieces in and out without advertising them, and then when it becomes a problem, they're not necessarily willing to, to deal with the, the consequences of that. 

[00:11:34] **Bryan:** They just don't know. I mean, I think they just genuinely don't know. I mean, I think that they, it's not like they're making a deliberate decision to kind of ship garbage. It's just that they are making, I mean, I think it's exactly what you said about like, not thinking about the hardware. It's like, what's a hard drive?

[00:11:47] **Bryan:** Like what's it, I mean, it's a hard drive. It's got the same specs as this other hard drive and Intel. You know, it's a little bit cheaper, so why not? It's like, well, like there's some reasons why not, and one of the reasons why not is like, uh, even a hard drive, whether it's rotating media or, or flash, like that's not just hardware.

[00:12:05] **Bryan:** There's software in there. And that the software's like not the same. I mean, there are components where it's like, there's actually, whether, you know, if, if you're looking at like a resistor or a capacitor or something like this Yeah. If you've got two, two parts that are within the same tolerance. Yeah.

[00:12:19] **Bryan:** Like sure. Maybe, although even the EEs I think would be, would be, uh, objecting that a little bit. But the, the, the more complicated you get, and certainly once you get to the, the, the, the kind of the hardware that we think of like a, a, a microprocessor, a a network interface card, a a, a hard driver, an NVME drive.

[00:12:38] **Bryan:** Those things are super complicated and there's a whole bunch of software inside of those things, the firmware, and that's the stuff that, that you can't, I mean, you say that software engineers don't think about that. It's like you, no one can really think about that because it's proprietary that's kinda welded shut and you've got this abstraction into it.

[00:12:55] **Bryan:** But the, the way that thing operates is very core to how the thing in aggregate will behave. And I think that you, the, the kind of, the, the fundamental difference between Oxide's approach and the approach that you get at a Dell HP Supermicro, wherever, is really thinking holistically in terms of hardware and software together in a system that, that ultimately delivers cloud computing to a user.

[00:13:22] **Bryan:** And there's a lot of software at many, many, many, many different layers. And it's very important to think about, about that software and that hardware holistically as a single system.

[00:13:34] **Jeremy:** And during that time at Joyent, when you experienced some of these issues, was it more of a case of you didn't have enough servers experiencing this? So if it would happen, you might say like, well, this one's not working, so maybe we'll just replace the hardware. What, what was the thought process when you were working at that smaller scale and, and how did these issues affect you?


## 
UEFI / Baseboard Management Controller

[00:13:58] **Bryan:** Yeah, at the smaller scale, you, uh, you see fewer of them, right? You just see it's like, okay, we, you know, what you might see is like, that's weird. We kinda saw this in one machine versus seeing it in a hundred or a thousand or 10,000. Um, so you just, you just see them, uh, less frequently as a result, they are less debilitating.

[00:14:16] **Bryan:** Um, I, I think that it's, when you go to that larger scale, those things that become, that were unusual now become routine and they become debilitating. Um, so it, it really is in many regards a function of scale. Uh, and then I think it was also, you know, it was a little bit dispiriting that kind of the substrate we were building on really had not improved.

[00:14:39] **Bryan:** Um, and if you look at, you know, the, if you buy a computer server, buy an x86 server. There is a very low layer of firmware, the BIOS, the basic input output system, the UEFI BIOS, and this is like an abstraction layer that has, has existed since the eighties and hasn't really meaningfully improved. Um, the, the kind of the transition to UEFI happened with, I mean, I, I ironically with Itanium, um, you know, two decades ago.

[00:15:08] **Bryan:** but beyond that, like this low layer, this lowest layer of platform enablement software is really only impeding the operability of the system. Um, you look at the baseboard management controller, which is the kind of the computer within the computer, there is a, uh, there is an element in the machine that needs to handle environmentals, that needs to handle, uh, operate the fans and so on.

[00:15:31] **Bryan:** Uh, and that traditionally has this, the space board management controller, and that architecturally just hasn't improved in the last two decades. And, you know, that's, it's a proprietary piece of silicon. Generally from a company that no one's ever heard of called a Speed, uh, which has to be, is written all on caps, so I guess it needs to be screamed.

[00:15:50] **Bryan:** Um, a speed has a proprietary part that has a, there is a root password infamously there, is there, the root password is encoded effectively in silicon. So, uh, which is just, and for, um, anyone who kind of goes deep into these things, like, oh my God, are you kidding me? Um, when we first started oxide, the wifi password was a fraction of the a speed root password for the bmc.

[00:16:16] **Bryan:** It's kinda like a little, little BMC humor. Um, but those things, it was just dispiriting that, that the, the state-of-the-art was still basically personal computers running in the data center. Um, and that's part of what, what was the motivation for doing something new?

[00:16:32] **Jeremy:** And for the people using these systems, whether it's the baseboard management controller or it's the The BIOS or UF UEFI component, what are the actual problems that people are seeing seen?


## Security vulnerabilities and poor practices in the BMC

[00:16:51] **Bryan:** Oh man, I, the, you are going to have like some fraction of your listeners, maybe a big fraction where like, yeah, like what are the problems? That's a good question. And then you're gonna have the people that actually deal with these things who are, did like their heads already hit the desk being like, what are the problems?

[00:17:06] **Bryan:** Like what are the non problems? Like what, what works? Actually, that's like a shorter answer. Um, I mean, there are so many problems and a lot of it is just like, I mean, there are problems just architecturally these things are just so, I mean, and you could, they're the problems spread to the horizon, so you can kind of start wherever you want.

[00:17:24] **Bryan:** But I mean, as like, as a really concrete example. Okay, so the, the BMCs that, that the computer within the computer that needs to be on its own network. So you now have like not one network, you got two networks that, and that network, by the way, it, that's the network that you're gonna log into to like reset the machine when it's otherwise unresponsive.

[00:17:44] **Bryan:** So that going into the BMC, you can are, you're able to control the entire machine. Well it's like, alright, so now I've got a second net network that I need to manage. What is running on the BMC? Well, it's running some. Ancient, ancient version of Linux it that you got. It's like, well how do I, how do I patch that?

[00:18:02] **Bryan:** How do I like manage the vulnerabilities with that? Because if someone is able to root your BMC, they control the system. So it's like, this is not you've, and now you've gotta go deal with all of the operational hair around that. How do you upgrade that system updating the BMC? I mean, it's like you've got this like second shadow bad infrastructure that you have to go manage.

[00:18:23] **Bryan:** Generally not open source. There's something called open BMC, um, which, um, you people use to varying degrees, but you're generally stuck with the proprietary BMC, so you're generally stuck with, with iLO from HPE or iDRAC from Dell or, or, uh, the, uh, su super micros, BMC, that H-P-B-M-C, and you are, uh, it is just excruciating pain.

[00:18:49] **Bryan:** Um, and that this is assuming that by the way, that everything is behaving correctly. The, the problem is that these things often don't behave correctly, and then the consequence of them not behaving correctly. It's really dire because it's at that lowest layer of the system. So, I mean, I'll give you a concrete example.

[00:19:07] **Bryan:** a customer of theirs reported to me, so I won't disclose the vendor, but let's just say that a well-known vendor had an issue with their, their temperature sensors were broken. Um, and the thing would always read basically the wrong value. So it was the BMC that had to like, invent its own ki a different kind of thermal control loop.

[00:19:28] **Bryan:** And it would index on the, on the, the, the, the actual inrush current. It would, they would look at that at the current that's going into the CPU to adjust the fan speed. That's a great example of something like that's a, that's an interesting idea. That doesn't work. 'cause that's actually not the temperature.

[00:19:45] **Bryan:** So like that software would crank the fans whenever you had an inrush of current and this customer had a workload that would spike the current and by it, when it would spike the current, the, the, the fans would kick up and then they would slowly degrade over time. Well, this workload was spiking the current faster than the fans would degrade, but not fast enough to actually heat up the part.

[00:20:08] **Bryan:** And ultimately over a very long time, in a very painful investigation, it's customer determined that like my fans are cranked in my data center for no reason. We're blowing cold air. And it's like that, this is on the order of like a hundred watts, a server of, of energy that you shouldn't be spending and like that ultimately what that go comes down to this kind of broken software hardware interface at the lowest layer that has real meaningful consequence, uh, in terms of hundreds of kilowatts, um, across a data center. So this stuff has, has very, very, very real consequence and it's such a shadowy world. Part of the reason that, that your listeners that have dealt with this, that our heads will hit the desk is because it is really aggravating to deal with problems with this layer.

[00:21:01] **Bryan:** You, you feel powerless. You don't control or really see the software that's on them. It's generally proprietary. You are relying on your vendor. Your vendor is telling you that like, boy, I don't know. You're the only customer seeing this. I mean, the number of times I have heard that for, and I, I have pledged that we're, we're not gonna say that at oxide because it's such an unaskable thing to say like, you're the only customer saying this.

[00:21:25] **Bryan:** It's like, it feels like, are you blaming me for my problem? Feels like you're blaming me for my problem? Um, and what you begin to realize is that to a degree, these folks are speaking their own truth because the, the folks that are running at real scale at Hyperscale, those folks aren't Dell, HP super micro customers.

[00:21:46] **Bryan:** They're actually, they've done their own thing. So it's like, yeah, Dell's not seeing that problem, um, because they're not running at the same scale. Um, but when you do run, you only have to run at modest scale before these things just become. Overwhelming in terms of the, the headwind that they present to people that wanna deploy infrastructure.


## The problem is felt with just a few racks

[00:22:05] **Jeremy:** Yeah, so maybe to help people get some perspective at, at what point do you think that people start noticing or start feeling these problems? Because I imagine that if you're just have a few racks or 

[00:22:22] **Bryan:** do you have a couple racks or the, or do you wonder or just wondering because No, no, no. I would think, I think anyone who deploys any number of servers, especially now, especially if your experience is only in the cloud, you're gonna be like, what the hell is this? I mean, just again, just to get this thing working at all.

[00:22:39] **Bryan:** It is so it, it's so hairy and so congealed, right? It's not designed. Um, and it, it, it, it's accreted it and it's so obviously accreted that you are, I mean, nobody who is setting up a rack of servers is gonna think to themselves like, yes, this is the right way to go do it. This all makes sense because it's, it's just not, it, I, it feels like the kit, I mean, kit car's almost too generous because it implies that there's like a set of plans to work to in the end.

[00:23:08] **Bryan:** Uh, I mean, it, it, it's a bag of bolts. It's a bunch of parts that you're putting together. And so even at the smallest scales, that stuff is painful. Just architecturally, it's painful at the small scale then, but at least you can get it working. I think the stuff that then becomes debilitating at larger scale are the things that are, are worse than just like, I can't, like this thing is a mess to get working.

[00:23:31] **Bryan:** It's like the, the, the fan issue that, um, where you are now seeing this over, you know, hundreds of machines or thousands of machines. Um, so I, it is painful at more or less all levels of scale. There's, there is no level at which the, the, the pc, which is really what this is, this is a, the, the personal computer architecture from the 1980s and there is really no level of scale where that's the right unit.


## Running elastic infrastructure is the hardware but also, hypervisor, distributed database, api, etc

[00:23:57] **Bryan:** I mean, where that's the right thing to go deploy, especially if what you are trying to run. Is elastic infrastructure, a cloud. Because the other thing is like we, we've kinda been talking a lot about that hardware layer. Like hardware is, is just the start. Like you actually gotta go put software on that and actually run that as elastic infrastructure.

[00:24:16] **Bryan:** So you need a hypervisor. Yes. But you need a lot more than that. You, you need to actually, you, you need a distributed database, you need web endpoints. You need, you need a CLI, you need all the stuff that you need to actually go run an actual service of compute or networking or storage. I mean, and for, for compute, even for compute, there's a ton of work to be done.

[00:24:39] **Bryan:** And compute is by far, I would say the simplest of the, of the three. When you look at like networks, network services, storage services, there's a whole bunch of stuff that you need to go build in terms of distributed systems to actually offer that as a cloud. So it, I mean, it is painful at more or less every LE level if you are trying to deploy cloud computing on.


## What's a control plane?

[00:25:00] **Jeremy:** And for someone who doesn't have experience building or working with this type of infrastructure, when you talk about a control plane, what, what does that do in the context of this system?

[00:25:16] **Bryan:** So control plane is the thing that is, that is everything between your API request and that infrastructure actually being acted upon. So you go say, Hey, I, I want a provision, a vm. Okay, great. We've got a whole bunch of things we're gonna provision with that. We're gonna provision a vm, we're gonna get some storage that's gonna go along with that, that's got a network storage service that's gonna come out of, uh, we've got a virtual network that we're gonna either create or attach to.

[00:25:39] **Bryan:** We've got a, a whole bunch of things we need to go do for that. For all of these things, there are metadata components that need, we need to keep track of this thing that, beyond the actual infrastructure that we create. And then we need to go actually, like act on the actual compute elements, the hostos, what have you, the switches, what have you, and actually go.

[00:25:56] **Bryan:** Create these underlying things and then connect them. And there's of course, the challenge of just getting that working is a big challenge. Um, but getting that working robustly, getting that working is, you know, when you go to provision of vm, um, the, all the, the, the steps that need to happen and what happens if one of those steps fails along the way?

[00:26:17] **Bryan:** What happens if, you know, one thing we're very mindful of is these kind of, you get these long tails of like, why, you know, generally our VM provisioning happened within this time, but we get these long tails where it takes much longer. What's going on? What, where in this process are we, are we actually spending time?

[00:26:33] **Bryan:** Uh, and there's a whole lot of complexity that you need to go deal with that. There's a lot of complexity that you need to go deal with this effectively, this workflow that's gonna go create these things and manage them. Um, we use a, a pattern that we call, that are called sagas, actually is a, is a database pattern from the eighties.

[00:26:51] **Bryan:** Uh, Katie McCaffrey is a, is a database reCrcher who, who, uh, I, I think, uh, reintroduce the idea of, of sagas, um, in the last kind of decade. Um, and this is something that we picked up, um, and I've done a lot of really interesting things with, um, to allow for, to this kind of, these workflows to be, to be managed and done so robustly in a way that you can restart them and so on.

[00:27:16] **Bryan:** Uh, and then you guys, you get this whole distributed system that can do all this. That whole distributed system, that itself needs to be reliable and available. So if you, you know, you need to be able to, what happens if you, if you pull a sled or if a sled fails, how does the system deal with that?

[00:27:33] **Bryan:** How does the system deal with getting an another sled added to the system? Like how do you actually grow this distributed system? And then how do you update it? How do you actually go from one version to the next? And all of that has to happen across an air gap where this is gonna run as part of the computer.

[00:27:49] **Bryan:** So there are, it, it is fractally complicated. There, there is a lot of complexity here in, in software, in the software system and all of that. We kind of, we call the control plane. Um, and it, this is the what exists at AWS at GCP, at Azure. When you are hitting an endpoint that's provisioning an EC2 instance for you.

[00:28:10] **Bryan:** There is an AWS control plane that is, is doing all of this and has, uh, some of these similar aspects and certainly some of these similar challenges.


## Are vSphere / Proxmox / Hyper-V in the same category?

[00:28:20] **Jeremy:** And for people who have run their own servers with something like say VMware or Hyper V or Proxmox, are those in the same category? 

[00:28:32] **Bryan:** Yeah, I mean a little bit. I mean, it kind of like vSphere Yes. Via VMware. No. So it's like you, uh, VMware ESX is, is kind of a key building block upon which you can build something that is a more meaningful distributed system. When it's just like a machine that you're provisioning VMs on, it's like, okay, well that's actually, you as the human might be the control plane.

[00:28:52] **Bryan:** Like, that's, that, that's, that's a much easier problem. Um, but when you've got, you know, tens, hundreds, thousands of machines, you need to do it robustly. You need something to coordinate that activity and you know, you need to pick which sled you land on. You need to be able to move these things. You need to be able to update that whole system.

[00:29:06] **Bryan:** That's when you're getting into a control plane. So, you know, some of these things have kind of edged into a control plane, certainly VMware. Um, now Broadcom, um, has delivered something that's kind of cloudish. Um, I think that for folks that are truly born on the cloud, it, it still feels somewhat, uh, like you're going backwards in time when you, when you look at these kind of on-prem offerings.

[00:29:29] **Bryan:** Um, but, but it, it, it's got these aspects to it for sure. Um, and I think that we're, um, some of these other things when you're just looking at KVM or just looks looking at Proxmox you kind of need to, to connect it to other broader things to turn it into something that really looks like manageable infrastructure.

[00:29:47] **Bryan:** And then many of those projects are really, they're either proprietary projects, uh, proprietary products like vSphere, um, or you are really dealing with open source projects that are. Not necessarily aimed at the same level of scale. Um, you know, you look at a, again, Proxmox or, uh, um, you'll get an OpenStack.

[00:30:05] **Bryan:** Um, and you know, OpenStack is just a lot of things, right? I mean, OpenStack has got so many, the OpenStack was kind of a, a free for all, for every infrastructure vendor. Um, and I, you know, there was a time people were like, don't you, aren't you worried about all these companies together that, you know, are coming together for OpenStack?

[00:30:24] **Bryan:** I'm like, haven't you ever worked for like a company? Like, companies don't get along. By the way, it's like having multiple companies work together on a thing that's bad news, not good news. And I think, you know, one of the things that OpenStack has definitely struggled with, kind of with what, actually the, the, there's so many different kind of vendor elements in there that it's, it's very much not a product, it's a project that you're trying to run.

[00:30:47] **Bryan:** But that's, but that very much is in, I mean, that's, that's similar certainly in spirit.

[00:30:53] **Jeremy:** And so I think this is kind of like you're alluding to earlier, the piece that allows you to allocate, compute, storage, manage networking, gives you that experience of I can go to a web console or I can use an API and I can spin up machines, get them all connected. At the end of the day, the control plane. Is allowing you to do that in hopefully a user-friendly way. 

[00:31:21] **Bryan:** That's right. Yep. And in the, I mean, in order to do that in a modern way, it's not just like a user-friendly way. You really need to have a CLI and a web UI and an API. Those all need to be drawn from the same kind of single ground truth. Like you don't wanna have any of those be an afterthought for the other.

[00:31:39] **Bryan:** You wanna have the same way of generating all of those different endpoints and, and entries into the system.


## Building a control plane now has better tools (Rust, CockroachDB)

[00:31:46] **Jeremy:** And if you take your time at Joyent as an example. What kind of tools existed for that versus how much did you have to build in-house for as far as the hypervisor and managing the compute and all that? 

[00:32:02] **Bryan:** Yeah, so we built more or less everything in house. I mean, what you have is, um, and I think, you know, over time we've gotten slightly better tools. Um, I think, and, and maybe it's a little bit easier to talk about the, kind of the tools we started at Oxide because we kind of started with a, with a clean sheet of paper at oxide.

[00:32:16] **Bryan:** We wanted to, knew we wanted to go build a control plane, but we were able to kind of go revisit some of the components. So actually, and maybe I'll, I'll talk about some of those changes. So when we, at, For example, at Joyent, when we were building a cloud at Joyent, there wasn't really a good distributed database.

[00:32:34] **Bryan:** Um, so we were using Postgres as our database for metadata and there were a lot of challenges. And Postgres is not a distributed database. It's running. With a primary secondary architecture, and there's a bunch of issues there, many of which we discovered the hard way. Um, when we were coming to oxide, you have much better options to pick from in terms of distributed databases.

[00:32:57] **Bryan:** You know, we, there was a period that now seems maybe potentially brief in hindsight, but of a really high quality open source distributed databases. So there were really some good ones to, to pick from. Um, we, we built on CockroachDB on CRDB. Um, so that was a really important component. That we had at oxide that we didn't have at Joyent.

[00:33:19] **Bryan:** Um, so we were, I wouldn't say we were rolling our own distributed database, we were just using Postgres and uh, and, and dealing with an enormous amount of pain there in terms of the surround. Um, on top of that, and, and, you know, a, a control plane is much more than a database, obviously. Uh, and you've gotta deal with, uh, there's a whole bunch of software that you need to go, right.

[00:33:40] **Bryan:** Um, to be able to, to transform these kind of API requests into something that is reliable infrastructure, right? And there, there's a lot to that. Uh, especially when networking gets in the mix, when storage gets in the mix, uh, there are a whole bunch of like complicated steps that need to be done, um, at Joyent.

[00:33:59] **Bryan:** Um, we, in part because of the history of the company and like, look. This, this just is not gonna sound good, but it just is what it is and I'm just gonna own it. We did it all in Node, um, at Joyent, which I, I, I know it sounds really right now, just sounds like, well, you, you built it with Tinker Toys. You Okay.

[00:34:18] **Bryan:** Uh, did, did you think it was, you built the skyscraper with Tinker Toys? Uh, it's like, well, okay. We actually, we had greater aspirations for the Tinker Toys once upon a time, and it was better than, you know, than Twisted Python and Event Machine from Ruby, and we weren't gonna do it in Java. All right.

[00:34:32] **Bryan:** So, but let's just say that that experiment, uh, that experiment did ultimately end in a predictable fashion. Um, and, uh, we, we decided that maybe Node was not gonna be the best decision long term. Um, Joyent was the company behind node js. Uh, back in the day, Ryan Dahl worked for Joyent. Uh, and then, uh, then we, we, we.

[00:34:53] **Bryan:** Uh, landed that in a foundation in about, uh, what, 2015, something like that. Um, and began to consider our world beyond, uh, beyond Node.


## Rust at Oxide

[00:35:04] **Bryan:** A big tool that we had in the arsenal when we started Oxide is Rust. Um, and so indeed the name of the company is, is a tip of the hat to the language that we were pretty sure we were gonna be building a lot of stuff in.

[00:35:16] **Bryan:** Namely Rust. And, uh, rust is, uh, has been huge for us, a very important revolution in programming languages. you know, there, there, there have been different people kind of coming in at different times and I kinda came to Rust in what I, I think is like this big kind of second expansion of rust in 2018 when a lot of technologists were think, uh, sick of Node and also sick of Go.

[00:35:43] **Bryan:** And, uh, also sick of C\+\+. And wondering is there gonna be something that gives me the, the, the performance, of that I get outta C. The, the robustness that I can get out of a C program but is is often difficult to achieve. but can I get that with kind of some, some of the velocity of development, although I hate that term, some of the speed of development that you get out of a more interpreted language.

[00:36:08] **Bryan:** Um, and then by the way, can I actually have types, I think types would be a good idea? Uh, and rust obviously hits the sweet spot of all of that. Um, it has been absolutely huge for us. I mean, we knew when we started the company again, oxide, uh, we were gonna be using rust in, in quite a, quite a. Few places, but we weren't doing it by fiat.

[00:36:27] **Bryan:** Um, we wanted to actually make sure we're making the right decision, um, at, at every different, at every layer. Uh, I think what has been surprising is the sheer number of layers at which we use rust in terms of, we've done our own embedded firmware in rust. We've done, um, in, in the host operating system, which is still largely in C, but very big components are in rust.

[00:36:47] **Bryan:** The hypervisor Propolis is all in rust. Uh, and then of course the control plane, that distributed system on that is all in rust. So that was a very important thing that we very much did not need to build ourselves. We were able to really leverage, uh, a terrific community. Um. We were able to use, uh, and we've done this at Joyent as well, but at Oxide, we've used Illumos as a hostos component, which, uh, our variant is called Helios.

[00:37:11] **Bryan:** Um, we've used, uh, bhyve um, as a, as as that kind of internal hypervisor component. we've made use of a bunch of different open source components to build this thing, um, which has been really, really important for us. Uh, and open source components that didn't exist even like five years prior.

[00:37:28] **Bryan:** That's part of why we felt that 2019 was the right time to start the company. And so we started Oxide.


## The problems building a control plane in Node

[00:37:34] **Jeremy:** You had mentioned that at Joyent, you had tried to build this in, in Node. What were the, what were the, the issues or the, the challenges that you had doing that? 

[00:37:46] **Bryan:** Oh boy. Yeah. again, we, I kind of had higher hopes in 2010, I would say. When we, we set on this, um, the, the, the problem that we had just writ large, um. JavaScript is really designed to allow as many people on earth to write a program as possible, which is good. I mean, I, I, that's a, that's a laudable goal.

[00:38:09] **Bryan:** That is the goal ultimately of such as it is of JavaScript. It's actually hard to know what the goal of JavaScript is, unfortunately, because Brendan Ike never actually wrote a book. so that there is not a canonical, you've got kind of Doug Crockford and other people who've written things on JavaScript, but it's hard to know kind of what the original intent of JavaScript is.

[00:38:27] **Bryan:** The name doesn't even express original intent, right? It was called Live Script, and it was kind of renamed to JavaScript during the Java Frenzy of the late nineties. A name that makes no sense. There is no Java in JavaScript. that is kind of, I think, revealing to kind of the, uh, the unprincipled mess that is JavaScript.

[00:38:47] **Bryan:** It, it, it's very pragmatic at some level, um, and allows anyone to, it makes it very easy to write software. The problem is it's much more difficult to write really rigorous software. So, uh, and this is what I should differentiate JavaScript from TypeScript. This is really what TypeScript is trying to solve.

[00:39:07] **Bryan:** TypeScript is like. How can, I think TypeScript is a, is a great step forward because TypeScript is like, how can we bring some rigor to this? Like, yes, it's great that it's easy to write JavaScript, but that's not, we, we don't wanna do that for Absolutely. I mean that, that's not the only problem we solve.

[00:39:23] **Bryan:** We actually wanna be able to write rigorous software and it's actually okay if it's a little harder to write rigorous software that's actually okay if it gets leads to, to more rigorous artifacts. Um, but in JavaScript, I mean, just a concrete example. You know, there's nothing to prevent you from referencing a property that doesn't actually exist in JavaScript.

[00:39:43] **Bryan:** So if you fat finger a property name, you are relying on something to tell you. By the way, I think you've misspelled this because there is no type definition for this thing. And I don't know that you've got one that's spelled correctly, one that's spelled incorrectly, that's often undefined. And then the, when you actually go, you say you've got this typo that is lurking in your what you want to be rigorous software.

[00:40:07] **Bryan:** And if you don't execute that code, like you won't know that's there. And then you do execute that code. And now you've got a, you've got an undefined object. And now that's either gonna be an exception or it can, again, depends on how that's handled. It can be really difficult to determine the origin of that, of, of that error, of that programming.

[00:40:26] **Bryan:** And that is a programmer error. And one of the big challenges that we had with Node is that programmer errors and operational errors, like, you know, I'm out of disk space as an operational error. Those get conflated and it becomes really hard. And in fact, I think the, the language wanted to make it easier to just kind of, uh, drive on in the event of all errors.

[00:40:53] **Bryan:** And it's like, actually not what you wanna do if you're trying to build a reliable, robust system. So we had. No end of issues. 

[00:41:01] **Bryan:** We've got a lot of experience developing rigorous systems, um, again coming out of operating systems development and so on. And we want, we brought some of that rigor, if strangely, to JavaScript. So one of the things that we did is we brought a lot of postmortem, diagnos ability and observability to node.

[00:41:18] **Bryan:** And so if, if one of our node processes. Died in production, we would actually get a core dump from that process, a core dump that we could actually meaningfully process. So we did a bunch of kind of wild stuff. I mean, actually wild stuff where we could actually make sense of the JavaScript objects in a binary core dump.


## JavaScript values ease of getting started over robustness

[00:41:41] **Bryan:** Um, and things that we thought were really important, and this is the, the rest of the world just looks at this being like, what the hell is this? I mean, it's so out of step with it. The problem is that we were trying to bridge two disconnected cultures of one developing really. Rigorous software and really designing it for production, diagnosability and the other, really designing it to software to run in the browser and for anyone to be able to like, you know, kind of liven up a webpage, right?

[00:42:10] **Bryan:** Is kinda the origin of, of live script and then JavaScript. And we were kind of the only ones sitting at the intersection of that. And you begin when you are the only ones sitting at that kind of intersection. You just are, you're, you're kind of fighting a community all the time. And we just realized that we are, there were so many things that the community wanted to do that we felt are like, no, no, this is gonna make software less diagnosable. It's gonna make it less robust.


## The NodeJS split and why people left

[00:42:36] **Bryan:** And then you realize like, I'm, we're the only voice in the room because we have got, we have got desires for this language that it doesn't have for itself. And this is when you realize you're in a bad relationship with software. It's time to actually move on. And in fact, actually several years after, we'd already kind of broken up with node.

[00:42:55] **Bryan:** Um, and it was like, it was a bit of an acrimonious breakup. there was a, uh, famous slash infamous fork of node called IoJS Um, and this was viewed because people, the community, thought that Joyent was being what was not being an appropriate steward of node js and was, uh, not allowing more things to come into to, to node.

[00:43:19] **Bryan:** And of course, the reason that we of course, felt that we were being a careful steward and we were actively resisting those things that would cut against its fitness for a production system. But it's some way the community saw it and they, and forked, um, and, and I think the, we knew before the fork that's like, this is not working and we need to get this thing out of our hands.


## Platform is a reflection of values node summit talk

[00:43:43] **Bryan:** And we're are the wrong hands for this? This needs to be in a foundation. Uh, and so we kind of gone through that breakup, uh, and maybe it was two years after that. That, uh, friend of mine who was um, was running the, uh, the node summit was actually, it's unfortunately now passed away. Charles er, um, but Charles' venture capitalist great guy, and Charles was running Node Summit and came to me in 2017.

[00:44:07] **Bryan:** He is like, I really want you to keynote Node Summit. And I'm like, Charles, I'm not gonna do that. I've got nothing nice to say. Like, this is the, the, you don't want, I'm the last person you wanna keynote. He's like, oh, if you have nothing nice to say, you should definitely keynote. You're like, oh God, okay, here we go.

[00:44:22] **Bryan:** He's like, no, I really want you to talk about, like, you should talk about the Joyent breakup with NodeJS. I'm like, oh man. 

[00:44:29] **Bryan:** And that led to a talk that I'm really happy that I gave, 'cause it was a very important talk for me personally. Uh, called Platform is a reflection of values and really looking at the values that we had for Node and the values that Node had for itself. And they didn't line up.

[00:44:49] **Bryan:** And the problem is that the values that Node had for itself and the values that we had for Node are all kind of positives, right? Like there's nobody in the node community who's like, I don't want rigor, I hate rigor. It's just that if they had the choose between rigor and making the language approachable.

[00:45:09] **Bryan:** They would choose approachability every single time. They would never choose rigor. And, you know, that was a, that was a big eye-opener. I do, I would say, if you watch this talk. 

[00:45:20] **Bryan:** because I knew that there's, like, the audience was gonna be filled with, with people who, had been a part of the fork in 2014, I think was the, the, the, the fork, the IOJS fork. And I knew that there, there were, there were some, you know, some people that were, um, had been there for the fork and.

[00:45:41] **Bryan:** I said a little bit of a trap for the audience. But the, and the trap, I said, you know what, I, I kind of talked about the values that we had and the aspirations we had for Node, the aspirations that Node had for itself and how they were different.

[00:45:53] **Bryan:** And, you know, and I'm like, look in, in, in hindsight, like a fracture was inevitable. And in 2014 there was finally a fracture. And do people know what happened in 2014? And if you, if you, you could listen to that talk, everyone almost says in unison, like IOJS. I'm like, oh right. IOJS. Right. That's actually not what I was thinking of.

[00:46:19] **Bryan:** And I go to the next slide and is a tweet from a guy named TJ Holloway, Chuck, who was the most prolific contributor to Node. And it was his tweet also in 2014 before the fork, before the IOJS fork explaining that he was leaving Node and that he was going to go. And you, if you turn the volume all the way up, you can hear the audience gasp.

[00:46:41] **Bryan:** And it's just delicious because the community had never really come, had never really confronted why TJ left. Um, there. And I went through a couple folks, Felix, bunch of other folks, early Node folks. That were there in 2010, were leaving in 2014, and they were going to go primarily, and they were going to go because they were sick of the same things that we were sick of.

[00:47:09] **Bryan:** They, they, they had hit the same things that we had hit and they were frustrated. I I really do believe this, that platforms do reflect their own values. And when you are making a software decision, you are selecting value.

[00:47:26] **Bryan:** You should select values that align with the values that you have for that software. That is, those are, that's way more important than other things that people look at. I think people look at, for example, quote unquote community size way too frequently, community size is like. Eh, maybe it can be fine.

[00:47:44] **Bryan:** I've been in very large communities, node. I've been in super small open source communities like AUMs and RAs, a bunch of others. there are strengths and weaknesses to both approaches just as like there's a strength to being in a big city versus a small town. Me personally, I'll take the small community more or less every time because the small community is almost always self-selecting based on values and just for the same reason that I like working at small companies or small teams.

[00:48:11] **Bryan:** There's a lot of value to be had in a small community. It's not to say that large communities are valueless, but again, long answer to your question of kind of where did things go south with Joyent and node. They went south because the, the values that we had and the values the community had didn't line up and that was a very educational experience, as you might imagine.

[00:48:33] **Jeremy:** Yeah. And, and given that you mentioned how, because of those values, some people moved from Node to go, and in the end for much of what oxide is building. You ended up using rust. What, what would you say are the, the values of go and and rust, and how did you end up choosing Rust given that.


## Go's decisions regarding generics, versioning, compilation speed priority

[00:48:56] **Bryan:** Yeah, I mean, well, so the value for, yeah. And so go, I mean, I understand why people move from Node to Go, go to me was kind of a lateral move. Um, there were a bunch of things that I, uh, go was still garbage collected, um, which I didn't like. Um, go also is very strange in terms of there are these kind of like.

[00:49:17] **Bryan:** These autocratic kind of decisions that are very bizarre. Um, there, I mean, generics is kind of a famous one, right? Where go kind of as a point of principle didn't have generics, even though go itself actually the innards of go did have generics. It's just that you a go user weren't allowed to have them.

[00:49:35] **Bryan:** And you know, it's kind of, there was, there was an old cartoon years and years ago about like when a, when a technologist is telling you that something is technically impossible, that actually means I don't feel like it. Uh, and there was a certain degree of like, generics are technically impossible and go, it's like, Hey, actually there are.

[00:49:51] **Bryan:** And so there was, and I just think that the arguments against generics were kind of disingenuous. Um, and indeed, like they ended up adopting generics and then there's like some super weird stuff around like, they're very anti-assertion, which is like, what, how are you? Why are you, how is someone against assertions, it doesn't even make any sense, but it's like, oh, nope.

[00:50:10] **Bryan:** Okay. There's a whole scree on it. Nope, we're against assertions and the, you know, against versioning. There was another thing like, you know, the Rob Pike has kind of famously been like, you should always just run on the way to commit. And you're like, does that, is that, does that make sense? I mean this, we actually built it.

[00:50:26] **Bryan:** And so there are a bunch of things like that. You're just like, okay, this is just exhausting and. I mean, there's some things about Go that are great and, uh, plenty of other things that I just, I'm not a fan of. Um, I think that the, in the end, like Go cares a lot about like compile time. It's super important for Go Right?

[00:50:44] **Bryan:** Is very quick, compile time. I'm like, okay. But that's like compile time is not like, it's not unimportant, it's doesn't have zero importance. But I've got other things that are like lots more important than that. Um, what I really care about is I want a high performing artifact. I wanted garbage collection outta my life.


## Don't think garbage collection has good trade offs

[00:51:00] **Bryan:** I, I gotta tell you, I, I like garbage collection to me is an embodiment of this like, larger problem of where do you put cognitive load in the software development process. And what garbage collection is saying to me it is right for plenty of other people and the software that they wanna develop.

[00:51:21] **Bryan:** But for me and the software that I wanna develop, infrastructure software, I don't want garbage collection because I can solve the memory allocation problem. I know when I'm like, done with something or not. I mean, it's like I, whether that's in, in C with, I mean it's actually like, it's really not that hard to not leak memory in, in a C base system.

[00:51:44] **Bryan:** And you can. give yourself a lot of tooling that allows you to diagnose where memory leaks are coming from. So it's like that is a solvable problem. There are other challenges with that, but like, when you are developing a really sophisticated system that has garbage collection is using garbage collection.

[00:51:59] **Bryan:** You spend as much time trying to dork with the garbage collector to convince it to collect the thing that you know is garbage. You are like, I've got this thing. I know it's garbage. Now I need to use these like tips and tricks to get the garbage collector. I mean, it's like, it feels like every Java performance issue goes to like minus xx call and use the other garbage collector, whatever one you're using, use a different one and using a different, a different approach.

[00:52:23] **Bryan:** It's like, so you're, you're in this, to me, it's like you're in the worst of all worlds where. the reason that garbage collection is helpful is because the programmer doesn't have to think at all about this problem. But now you're actually dealing with these long pauses in production.

[00:52:38] **Bryan:** You're dealing with all these other issues where actually you need to think a lot about it. And it's kind of, it, it it's witchcraft. It, it, it's this black box that you can't see into. So it's like, what problem have we solved exactly? And I mean, so the fact that go had garbage collection, it's like, eh, no, I, I do not want, like, and then you get all the other like weird fatwahs and you know, everything else.

[00:52:57] **Bryan:** I'm like, no, thank you. Go is a no thank you for me, I, I get it why people like it or use it, but it's, it's just, that was not gonna be it.


## Choosing Rust

[00:53:04] **Bryan:** I'm like, I want C. but I, there are things I didn't like about C too. I was looking for something that was gonna give me the deterministic kind of artifact that I got outta C. But I wanted library support and C is tough because there's, it's all convention. you know, there's just a bunch of other things that are just thorny. And I remember thinking vividly in 2018, I'm like, well, it's rust or bust.


## Ownership model, algebraic types, error handling

[00:53:28] **Bryan:** I'm gonna go into rust. And, uh, I hope I like it because if it's not this, it's gonna like, I'm gonna go back to C I'm like literally trying to figure out what the language is for the back half of my career. Um, and when I, you know, did what a lot of people were doing at that time and people have been doing since of, you know, really getting into rust and really learning it, appreciating the difference in the, the model for sure, the ownership model people talk about.

[00:53:54] **Bryan:** That's also obviously very important. It was the error handling that blew me away. And the idea of like algebraic types, I never really had algebraic types. Um, and the ability to, to have. And for error handling is one of these really, uh, you, you really appreciate these things where it's like, how do you deal with a, with a function that can either succeed and return something or it can fail, and the way c deals with that is bad with these kind of sentinels for errors.

[00:54:27] **Bryan:** And, you know, does negative one mean success? Does negative one mean failure? Does zero mean failure? Some C functions, zero means failure. Traditionally in Unix, zero means success. And like, what if you wanna return a file descriptor, you know, it's like, oh. And then it's like, okay, then it'll be like zero through positive N will be a valid result.

[00:54:44] **Bryan:** Negative numbers will be, and like, was it negative one and I said airo, or is it a negative number that did not, I mean, it's like, and that's all convention, right? People do all, all those different things and it's all convention and it's easy to get wrong, easy to have bugs, can't be statically checked and so on. Um, and then what Go says is like, well, you're gonna have like two return values and then you're gonna have to like, just like constantly check all of these all the time. Um, which is also kind of gross. Um, JavaScript is like, Hey, let's toss an exception. If, if we don't like something, if we see an error, we'll, we'll throw an exception.

[00:55:15] **Bryan:** There are a bunch of reasons I don't like that. Um, and you look, you'll get what Rust does, where it's like, no, no, no. We're gonna have these algebra types, which is to say this thing can be a this thing or that thing, but it, but it has to be one of these. And by the way, you don't get to process this thing until you conditionally match on one of these things.

[00:55:35] **Bryan:** You're gonna have to have a, a pattern match on this thing to determine if it's a this or a that, and if it in, in the result type that you, the result is a generic where it's like, it's gonna be either the thing that you wanna return. It's gonna be an okay that contains the thing you wanna return, or it's gonna be an error that contains your error and it forces your code to deal with that.

[00:55:57] **Bryan:** And what that does is it shifts the cognitive load from the person that is operating this thing in production to the, the actual developer that is in development. And I think that that, that to me is like, I, I love that shift. Um, and that shift to me is really important. Um, and that's what I was missing, that that's what Rust gives you.

[00:56:23] **Bryan:** Rust forces you to think about your code as you write it, but as a result, you have an artifact that is much more supportable, much more sustainable, and much faster.


## Prefer to frontload cognitive load during development instead of at runtime

[00:56:34] **Jeremy:** Yeah, it sounds like you would rather take the time during the development to think about these issues because whether it's garbage collection or it's error handling at runtime when you're trying to solve a problem, then it's much more difficult than having dealt with it to start with. 

[00:56:57] **Bryan:** Yeah, absolutely. I, and I just think that like, why also, like if it's software, if it's, again, if it's infrastructure software, I mean the kinda the question that you, you should have when you're writing software is how long is this software gonna live? How many people are gonna use this software? Uh, and if you are writing an operating system, the answer for this thing that you're gonna write, it's gonna live for a long time.

[00:57:18] **Bryan:** Like, if we just look at plenty of aspects of the system that have been around for a, for decades, it's gonna live for a long time and many, many, many people are gonna use it. Why would we not expect people writing that software to have more cognitive load when they're writing it to give us something that's gonna be a better artifact?

[00:57:38] **Bryan:** Now conversely, you're like, Hey, I kind of don't care about this. And like, I don't know, I'm just like, I wanna see if this whole thing works. I've got, I like, I'm just stringing this together. I don't like, no, the software like will be lucky if it survives until tonight, but then like, who cares? Yeah. Yeah.

[00:57:52] **Bryan:** Gar garbage clock. You know, if you're prototyping something, whatever. And this is why you really do get like, you know, different choices, different technology choices, depending on the way that you wanna solve the problem at hand. And for the software that I wanna write, I do like that cognitive load that is upfront.


## With LLMs maybe you can get the benefit of the robust artifact with less cognitive load

[00:58:10] **Bryan:** Um, and although I think, I think the thing that is really wild that is the twist that I don't think anyone really saw coming is that in a, in an LLM age. That like the cognitive load upfront almost needs an asterisk on it because so much of that can be assisted by an LLM. And now, I mean, I would like to believe, and maybe this is me being optimistic, that the the, in the LLM age, we will see, I mean, rust is a great fit for the LLMH because the LLM itself can get a lot of feedback about whether the software that's written is correct or not.

[00:58:44] **Bryan:** Much more so than you can for other environments.

[00:58:48] **Jeremy:** Yeah, that is a interesting point in that I think when people first started trying out the LLMs to code, it was really good at these maybe looser languages like Python or JavaScript, and initially wasn't so good at something like Rust. But it sounds like as that improves, if. It can write it then because of the rigor or the memory management or the error handling that the language is forcing you to do, it might actually end up being a better choice for people using LLMs. 

[00:59:27] **Bryan:** absolutely. I, it, it gives you more certainty in the artifact that you've delivered. I mean, you know a lot about a Rust program that compiles correctly. I mean, th there are certain classes of errors that you don't have, um, that you actually don't know on a C program or a GO program or a, a JavaScript program.

[00:59:46] **Bryan:** I think that's gonna be really important. I think we are on the cusp. Maybe we've already seen it, this kind of great bifurcation in the software that we write where the rigorous software becomes much more important. We, we have this foundational software that we're gonna rely on as much more bedrock, and then we're gonna have much more software.

[01:00:06] **Bryan:** Where that rigor is not as more much of a constraint because the constraints are the ability for it to be, uh, customized to my need and done very quickly. And it's, it's going to feel like, I think two different worlds. Um, and I think in an exciting way, I think it's gonna be, I think that the future's definitely exciting for software.


## Illumos

[01:00:27] **Jeremy:** Another interesting decision about the oxide computer is you chose an operating system that I think most people aren't familiar with rather than, rather than a Linux or a free BSD, you chose I believe it's Illumos.

[01:00:44] **Jeremy:** Is that how you pronounce it? 

[01:00:45] **Bryan:** Yeah, yeah, yeah, yeah. I mean, yes. So I Illumos and, uh, Illumos, which very much inherits from, uh, open Solaris, um, which inherits from the, uh, Solaris heritage, which was SunOS 4.X before that was the Solaris itself is, is kind of, uh, this unholy love child of SunOS 4.X and the, the true kind of BSD lineage and the AT&T lineage in Unix and SVR4.

[01:01:15] **Bryan:** in many ways I know that people haven't necessarily heard of it, um, but it. Is, it is true Unix in a, in, in a real historical sense, um, in a way that, that Linux and even the bsds are not. Uh, and it, and there are aspects where it shows it, but in terms of, it is an idiosyncratic decision.

[01:01:35] **Bryan:** It's not one that we took lightly. people assume like, oh, you know, it's a bunch of, it's a bunch of old Sun folks.

[01:01:41] **Bryan:** Like of course they're gonna pick Illumos like that's, and we had a lot of operational experience with, with SmartOS, uh, at Joyent But that's a, it's more nuance than that, I would say. it is true that a bunch of the technologies that we have developed over the years, uh, we developed them for good reasons.


## Debugability of the OS

[01:01:55] **Bryan:** Um, and we don't want to be without them. I mentioned the postmortem diagnosability of JavaScript. Uh, postmortem diagnosability is really important to us, and to me, debug ability is really important. Um, and debug ability is not something that others operating systems have taken that seriously.

[01:02:10] **Bryan:** Just to put it bluntly, you can, you, you can judge a lot about an operating system by it's built in debugger. and, uh, there's not really a built in debugger present for Linux. but it, it, it, it's more than just that. 


## Linux is a Kernel, not an OS, so you need many things on top of it

[01:02:22] **Bryan:** You know, uh, if you look at Linux in particular, Linux is a kernel.

[01:02:27] **Bryan:** It is not. And you know, this is something that. Linus Torvalds makes clear that you know, in his defense, at more or less every juncture, Linux is a kernel. And thi this is the kind of the very famous, you know, the Stallman is of like what you were calling Linux. I call it GNU/Linux Linux. And it's obviously like, on the one hand, a little bit ridiculous.

[01:02:45] **Bryan:** On the other hand, like not wrong in that the software that you need to actually have a functional system is a lot more than just Linux. You need a libc, right? And there's actually more than one libc you. Is it gonna be musl Is it gonna be glibc? There are some other alternate libcs, um, you need. And part of the problem is if you're going to use a Linux kernel as the basis for a host operating system. That's nowhere near enough because you need to now build an entire distro effectively of all these different tools on top of that. And the maintenance burden of that is off the charts. Um, and it's actually funny, one of our colleagues, Laura Abbott, came from Red Hat 

[01:03:26] **Bryan:** And I'm like, well, this will be interesting. 'cause I, again, my mind was open, more open than it had been in, you know, a long time about like, maybe we should use Linux I don't know. And Laura felt strongly that we shouldn't, but for reasons that were different. 

[01:03:40] **Bryan:** Laura was very concerned about what the, the distro management burden would be, and she had really seen that upfront at Red Hat, and she's like, do not make this decision lightly, that you've gotta make all these other decisions. It's something I really like. I remember at the time being like, okay, yeah, I know I get that.

[01:03:58] **Bryan:** But then in a year since I'm like, oh, wow, that's a really big deal. That's a bigger deal than I realized. and so we, you know, we, we don't have to do that. We, we, we get an operating system that's got a lot of stuff like built in. Um, and now of course it means that like we've also, it, it's talk about small communities, definitely a small community.

[01:04:16] **Bryan:** Um, and there, there you, there are, there are challenges there too. Um, but we, it, it is one that has allowed us to get the technologies that we really need. ZFS, containers, DTrace, the, the virtual networking, a bunch of things that we really needed, we had in place and then allowed us to also move the system in a dimension that we needed and wanted to move it.

[01:04:37] **Bryan:** So, um, for us it's been the right decision. but I think, again, the internet is kind of disbelieving that we actually were at a real juncture there. But, uh, but we were, um, we, we hand on heart were, uh, actually at the moment where I was like most potentially intrigued or at least wanted to explore something like Linux.

[01:04:56] **Bryan:** Uh, Linux Torvalds was just on an absolute bender against ZFS which he's done occasionally. And I'm like, this is, dude, this is the wrong time to be on this th this ZFS tamper tantrum, which he's again done a couple of times. Um, but it was kind of the, and, and a problem with Linux is that ZFS is not a first class, first class file system.

[01:05:16] **Bryan:** Um, has always been on the outside because of this kind of, these ridiculous licensing concerns. And it was a reminder of like, oh yeah, right this yeah okay i think yeah we'll go our own way.


## Illumos and FreeBSD include a lot more making it easier to manage a distribution 

[01:05:28] **Jeremy:** And you, you mentioned one of the, the risks would be managing your own distribution, but for Illumos you actually did create your own distribution. 

[01:05:38] **Bryan:** Yeah, you do, but like it's yes and no. I mean, you are creating your own distribution, but you're not having to like go be like, okay, God, we gotta go get our own version of GDB. We gotta go get our own version of grep, we gotta get our own version of tar, we gotta get our own version. And it's like you, that's what I mean about like in Illumos and FreeBSD is like this too, by the way.

[01:05:55] **Bryan:** It's not the only operating system like this. Actually Windows is like this. It is the operating system is more, is the kernel plus the system libraries, plus the commands to run So you are, you're not having these things operate across purposes. You've got, and technologies like DTrace that are able to straddle this user kernel boundary in a really important way.

[01:06:16] **Bryan:** So that's what I mean by a distro. we, we've got our, our own derivative. Um, but we actually very deliberately in part because of our experiences at Joyent, uh, we really get stuff upstream. So we are as, as much as we humanly can, everything is, is upstream. The other thing we knew we wanted to go do, or had a hunch we wanted to go do, we knew that we wanted to eliminate the BIOS completely and for all of the things that we did at Oxide, which is we did our own switch.

[01:06:45] **Bryan:** We did our own compute sled. We did, you know, that, that our own microcontroller operating system in many ways, the riskiest thing was this idea of eliminating the BIOS. And so we knew one of the things we wanted to go do was actually do that lowest level of platform, initialization ourselves from the actual operating system, from the host operating system.

[01:07:05] **Bryan:** And that required us to get this thing really under a knife. we've managed to pull that off. But that would've been much thornier, I think, trying to kind of battle, um, in upstream, because it's a very different architecture. what we have is not a PC architecture, it's an x86 machine, AMD.

[01:07:23] **Bryan:** But we have done, we in the host operating system have done the lowest level of platform neutralization that's historically done by the BIOS. Um, which was a huge challenge. And one by the way that AMD didn't think we could do, AMD was very surprised when we were, you know, sometimes you know that somebody is like not explicitly underestimating you, but then they're very surprised when you've succeeded and you realize like, oh, okay, yeah, you actually, I guess you were underestimating me.

[01:07:48] **Bryan:** I didn't realize that. And that was definitely the, the case here where, uh, AMD was very surprised that we lived, um, and that we actually had a machine that could boot, um, without running a UEFI BIOS. But that, that very much, Was hand in glove with this decision to have our own Illumos derivativefor Helios.

[01:08:05] **Jeremy:** And it, it sounded like possibly for this to work, you would have to upstream things to Illumos. Is that right? 

[01:08:13] **Bryan:** I mean, for sure. You just don't wanna be you, you don't wanna be battling a, you are gonna end up with your own kind of derivative at some level. And this is where it's actually just helpful to have a smaller community, frankly. Um, just makes it easier to go do that stuff.


## Upstreaming to Linux is a fight and rust is a battlefield

[01:08:28] **Jeremy:** Yeah, because with Linux having so many users, it would be much more of a fight trying to, yeah.

[01:08:36] **Bryan:** Oh everything's a fight. I mean, everything's a fight is the problem. I mean, uh, and you get like, I mean, and I'll tell you another thing, it's actually, this is like really funny because, uh, this is is something that, um, that that Torvalds and I actually agree on, uh, pretty thoroughly, which is what the, the presence of rust in the system.

[01:08:52] **Bryan:** so we've been able to add, I mean, I'm absolutely believed that like we want to have rust internal modules and we do in, in, in Helios. We've, we've got, rust in kernel modules in terms of, of our oxide packet, transformation engine, OPTE. and we, that will increase over time. That is an absolute civil war in Linux ironically, one that like, again, Torvalds and I agree, but there are people, other people in Linux who ardently disagree over ardently, disagree over rust in the kernel and like I, that is not a fight I want to have.

[01:09:26] **Bryan:** Like I'm just, I am. Absolutely disinterested in having an argument over Rust versus C. Like, no, thank you. that is the peril of a larger community is you end up with people and then, you know, a larger community that like look is not exactly an exemplar of, of positive community behavior. Um, and there are plenty of people that have been, uh, that have done Linux kernel development and then have walked away from it because it was not exactly an uplifting experience.

[01:09:52] **Bryan:** And, uh, their treatment of rust is really bad right now. I mean, I think that's like one of the big open challenges that I think Linux has, what does the future of the system look like with respect to Rust? I feel it's like, it's the Torvalds position is the only one that's ultimately tenable in the limit, but clearly there are people inside of Linux maintainers inside of Linux that hardly disagree with that.

[01:10:11] **Jeremy:** And for those who aren't familiar with the fight, what is, what is his

[01:10:16] **Jeremy:** opinion versus the, 

[01:10:17] **Bryan:** I mean, Torvalds I think is, is Torvalds is Pro Rust. Is, is is, I, I think is the, the, the short answer. I shouldn't speak for him obviously, but, but my read on this from the outside looking in is Torvalds is broadly like, yeah, this is like, this is interesting. The same reasons I think it's interesting and that we should have kernel components written in rust.

[01:10:33] **Bryan:** Um, but you've got, um, I think maintainers of sub of subsystems that have, are ardently opposed to it and are kinda holding aspects of the hostage of the project hostage over it. there's gonna be, there's gonna continue to be friction, um, uh, over the, the, the future of the operating system there.

[01:10:53] **Bryan:** And like I. I don't want to have debates. I really don't. I mean, I, I, I, I guess maybe, you know, okay, maybe I, I, I, I do kick an occasional hornet's nest on the internet, but I, I really like, don't wanna be spending, I, I would much rather find a community where we're gonna broadly agree on our values and then we, than I just find that there is, that there is, much less discord, um, when you, you have that kind of, that value alignment.

[01:11:21] **Bryan:** Um, and I think that that's one of the big challenges for Linux is there is a, there is, um, some, some, uh, disalignment there, uh, in terms of what people view as the future of the operating system.

[01:11:33] **Jeremy:** And, and this choice of your operating system as a user of an oxide computer, would they

[01:11:40] **Bryan:** No, you don't know. I mean, it, it's just like you don't know, like, you know, if you're a user of AWS you've got no idea what Nitro is or Annaperna or these other things that are like, you know, do you know whether they use KVM at AWS? No, you've got no idea. I mean, the, do they use KVM or Zen? It's like, the answer is like, well, it depends on your instance type and the age of the thing.

[01:12:00] **Bryan:** And, but, but like, as a user that's, that, that's opaque to you. Um, what you've got is like, you wanna hit an API endpoint, you wanna provision an instance and you wanna run the, uh, a, an operating system of your choice. You wanna run Windows or Linux or, or, you know, or previous SD or whatever as a, in your cloud.

[01:12:19] **Bryan:** That's what you actually want to go do. Um, and that's what we enable you to do.


## FPGAs, ASICS, etc

[01:12:25] **Jeremy:** Something I find interesting about the OXIDE project is you not only write software that's general compute to run on x86. There's also parts of the system that are written for FPGAs and written for ASICS I wonder if you could explain to people who might not be familiar what the difference is and what it's like building for those things versus running something on a a VM on an x86 machine. 

[01:12:59] **Bryan:** Yeah, I mean, so you, you've got, I mean, there's a whole spectrum of, and, and this is all kind of constitutes the, the platform for compute. I mean, you have the x86 cores, uh, AMD cores, which are the, I mean, that, that's the kind of compute that you know about, right? That, that is kind of architecturally present in terms of the compute that's elsewhere in the system.

[01:13:16] **Bryan:** I mean, you've got microcontrollers, so we talked with a baseboard management controller. Uh, we have turned that into a much smaller thing, a service processor, that, that's a microcontroller, a, a Cortex m uh, microcontroller that is running that, that you don't see as a user. Um, but we've got our own system software, appropriately enough called Hubris.

[01:13:36] **Bryan:** Um, that, that, because we actually thought we were not gonna use our, we thought we were gonna use a, a, an a, an open source operating system, but then realized that actually we needed to go our own way. and the, the debugger for hubris is appropriately enough, called the Humility. Um, so y the but hubris runs on that microcontroller, it runs on our root of trust microcontroller.

[01:13:56] **Bryan:** Um, you, but that you also have, um, we've got FPGAs in the system. Um, FPGA is doing different kinds of things and FPGA is a field programmable gate array and you also call, you'll hear it referred to as soft logic. And, uh, FPGAs are really neat because they are, uh, they are hardware that you can reconfigure dynamically.

[01:14:16] **Bryan:** And the thing that's really cool about that is we, we can take our FPGA payload and put it into a hubris, larger hubris payload, and then you can sign that and attach to that. And so now you, you, you've got confidence about that whole bundle that you're loading onto the system. And then when we start the system, we will actually load this Bitstream onto the FPGA.

[01:14:38] **Bryan:** You know, for in, in our different platforms, the FPGAs have different roles, but they're doing low level things like power sequencing. They're doing, we generally are using FPGAs. Historically we're using FPGAs to do this kind of, this, these low level things on the board. 'cause it makes for a simple board, right?

[01:14:54] **Bryan:** It makes for a simple board when you can just put the soft logic down. Um, and some of these are crazy small FPGAs, that are, are small, but they're, there are enough for what we need. we also have higher performance FPGAs that we are increasingly using, uh, for things like NICs uh, network interface cards.

[01:15:11] **Bryan:** So we are. some of the, the kind of the next gen FPGAs, are really pretty cool because they have what you call a hard block, which is say kind of like one of the components that the, the hard components on. They're not programmable. That allows you to have like a surveys that allows you to actually speak over a network, which is actually a really hard part of a nick.

[01:15:30] **Bryan:** And then you could do the NIC in soft logic, which is really neat. Um, so we're really excited about that. That's the kind of in a forthcoming platform. We're working on a, uh, an FPGA there. Uh, and then of course we've got, so in asic uh, um, is an application specific integrated circuit, and that's, uh, not dynamically reconfigurable.

[01:15:51] **Bryan:** Um, and ASIC is is where, and we've got any number of asics on the system where you've got a, a deliberately fabbed part. and so we, you know, like our traditional NIC is an ASIC Um, and we haven't done any ASIC development yet at oxide, but I think any oxide engineer would say would emphasize the yet, uh, that at some point we almost, we'll do an asic.

[01:16:12] **Bryan:** And ASIC is still really, really hairy to do. Um, FPGAs are great because they look a lot like software. Asics are a lot more complicated and for a bunch of reasons that are, that are owed, that's they're that own kinda like deep well of complexity. Um, but uh, not least the software licensing for an ASIC is brutal.

[01:16:32] **Bryan:** 'cause you actually need to get EDA tools from the likes of synopsis or cadence and, you're kind of mating yourself onto a fab in a process. And it's like, there's a whole, like, it's very, very involved to do an asic, very expensive to do an asic. It's higher performing, consumes less power. It's cheaper when you're actually, when you actually have the artifact.

[01:16:49] **Bryan:** Uh, and there are reasons why we, you know, we can envision ourselves doing asics in the future, but for right now, the asics we buy are all off the shelf. and then we use FPGAs in a bunch of different places of the system. it, I, I would, uh, refer folks, you know, we've got an Oxide and Friends podcast.

[01:17:03] **Bryan:** We actually have, uh, Raja Kodori um, joined us, uh, for one of our episodes talking about exactly this, about these different kinds of compute elements. And that's another, a great episode that I would steer people to if they wanted to learn more about the different kinds of compute.


## The Oxide Computer

[01:17:17] **Jeremy:** The oxide machine itself, I don't think we've really explained physically what it is. You know, what are people going to be receiving, what are the components, what is it, how is it different?

[01:17:31] **Jeremy:** Yeah. What, what would I actually be buying and, and getting into my data center. So maybe you could talk a little bit about what that

[01:17:38] **Bryan:** Yeah. So what, so, uh, you get a crate, um, you get a very large crate. Um, and in that crate is a rack and that rack is a, uh, it's an oxide designed rack. Um, and that rack has two switches and 32 compute sleds that are in it. Um, and that rack has been designed holistically. So we have designed all these parts to work together.

[01:18:03] **Bryan:** We've got some very basic things. We've got a DC bus bar in the rack. So we've got a power shelf that rectifies from AC to DC and then we run DC up and down the back of, of the rack and our compute sleds blind mate into that DC power. That is basic. And anybody at all of the hyperscalers have a DC busbar based system.

[01:18:27] **Bryan:** You can't buy a DC busbar based system from Dell, HP, Supermicro because in order to have a busbar based system, you really need to be designing at at least the rack level because the rack needs to be the, you can't just buy an oxide sled. Um, you need to buy the rack that is gonna, is gonna contain it. And then we very much designed the rack around the switch.

[01:18:53] **Bryan:** So the switch, we actually have a cable, the back plane, and in addition to blind mating into power, our compute slots blind made into networking. So the networking is a passive cabled back plane, and it means there's no actual cabling in the sled itself. So if you wanna take a sled out, you just like take a sled out, there's no cables.

[01:19:13] **Bryan:** One of the challenges with the kind of traditional server design and the baseboard management controller, it's gotta be on two different networks. Well, ours is on two different networks too, but you don't see any of those because it's all sitting on that cable back plane.

[01:19:23] **Bryan:** And our switch, which has that intel tofino at its core, has a, there's actually another switch that that serves as the switch for the service processors on the system. And then that's all, that's all, uh, coherently interconnected. Um, so what you get is a real product and that thing wheels into the data center.

[01:19:41] **Bryan:** You get power applied. And you are on the, the, the tech port doing the basic configuration we need, which basically like we need to know, like who to talk to for time, more or less. We gotta find, you know, there, there's some real basics that we need. We need a BGP session and we need to be able to actually like connect to a network.

[01:19:59] **Bryan:** But once we can do that, we're off. And you're provisioning VMs. Uh, you're provisioning storage, you're provisioning networks, virtual networks, just like you're on the public cloud. And one of the things that's been really, really fun, because this is really painful with traditional infrastructure, it's, it's this kind of bag of bolts approach can take a long, it can take a comically long time. I'm talking like easily months to get the gear has arrived. Get to the point where devs are on there. You're like, what takes months? It's like, well glad you asked. It's like we got the wrong switch from this vendor. This, that server came with the wrong rack rails, we're missing the cabling over here. We got it all together and the software vendor, the software didn't work and the software vendors pointing at the, so it's like these things just like can take a long time to get up and running with the oxide rack.

[01:20:48] **Bryan:** That thing wheels in, you power it on, you plug it in, you get a BGP session and your provisioning of VMs. And one of the thi the experiences that's been really fun is to be with customers as they are doing that for the first time and be like, oh my God, I'm on the, like we're provisioning infrastructure.

[01:21:05] **Bryan:** Like, and I can just like. Let my devs at it. Like we, we just got this thing powered on like two hours ago and that is really, really neat. Um, and very vindicating of the approach that we've taken. It's really exciting. I.

[01:21:21] **Jeremy:** And for a, a listener who's never had to do it the traditional way, what are all the different things that they would need to get into this rack to have the 

[01:21:31] **Bryan:** They would need, you gotta go buy, switch from a switch vendor. You gotta go buy, you're buying your compute from someone else. Maybe you're buying storage from someone else. You're cabling it together. You're get you, you've got, you've got your service. Your BMCs gotta be on a network. So you got a separate switch for that.

[01:21:44] **Bryan:** You've gotta have, and then you, that's all, that's the hardware you get. Get software on it. Like, what are you doing for, are you getting OpenStack? You're doing VMware, are you doing something else? And it's like, then that's all gotta work. You've gotta get that image on there. You've gotta, and it's like you're just kind of building this thing as you go.

[01:21:58] **Bryan:** I mean, there's just nothing that is, you're the one kind of literally cobbling this thing together. Um, and there it's just not a product experience.

[01:22:08] **Jeremy:** Yeah, and I think the interesting part was something you talked about earlier too, is that if something isn't behaving the way you expect, for example. IO latency or maybe some kind of compute issue it, it seems like in most of those cases, you really have no one to turn to. You can go to Dell or HP and they'll probably just shrug.

[01:22:32] **Bryan:** Um, the, well, yeah, you know, there was, there was kind of a, a, a tweet when we were starting the company that, that we were all, I I, I think may have made it into a slide deck or two, uh, where someone said that they, they were, uh, dealing with a, a support issue with Dell and EMC, and they felt like they were talking to their divorced parents.

[01:22:51] **Bryan:** It's not necessarily malicious because like a lot of the problem is that like you have these systems that are each well designed on their own, or they're well designed, maybe that's putting, that's, that is giving them way too much credit.

[01:23:04] **Bryan:** They're designed on their own and then they have an issue when you put them together. That each can plausibly blame on the other. Where there, you know, just like anything where you got like, you know, miscommunication with someone or what have you, where it's like, well, you know, you thought I was to blame and I thought you were to blame.

[01:23:22] **Bryan:** And I don't know, it's kinda like, it, it, it's in the middle, right? And this happens a lot where you have, it's like actually these two things are kind of behaving somewhat reasonably in on their own, but you put it together and it, it, like the, the result is terrible. And the problem is, it is the end user that is left being like, well, who helps me in my terrible problem?

[01:23:44] **Bryan:** It's like, great, you each have made a convincing case that it's not your problem. Like, so I guess it's who's, I guess it's my problem I guess. Um, and that is what is really really frustrating to people.

[01:23:56] **Jeremy:** And I, I'm curious, back when you were at Sun and, and Sun was selling their own servers, was like if somebody had a problem with one of those servers, was that a case where they could go to Sun and then Sun would actually go and figure out, okay, what's the problem here?

[01:24:16] **Bryan:** Uh, that was, uh, on its best days. Yeah. On its best days. Uh, its days. Were not always its best days. certainly the vision that, I always had for Sun Systems is that you'd be able to do that. It was not always the case. uh, I, I started a storage group inside of Sun, uh, called Fishworks, um, in 2006.

[01:24:35] **Bryan:** And we, we. partly wanted to really make good on this idea of systems thinking. The, uh, in, in Fish the Fish in FISHworks stands for fully integrated software and hardware, and we learned a whole set of painful lessons, um, because we were still relying on quote unquote commodity hardware there and got bit by a bunch of firmware we didn't control.

[01:24:58] **Bryan:** Um, so I, throughout my career, I have tried to make good on this promise, but I really feel it's only at oxide that we've been able to control our, our fate sufficiently from top to bottom to really make good on it. Um, and it shows in the experiences that people are having, which is really great.

[01:25:16] **Jeremy:** And it sounds like maybe that's primarily because the software running on each of these components is in your control, so you're able to trace through and see where the actual problem is, rather than having all these proprietary vendors. 

[01:25:33] **Bryan:** It is, yes, it is. It is that for sure it is that we just like have more of the components that our own control. don't wanna understate the importance of that. 

[01:25:41] **Bryan:** Um, I think it's also just the sense of responsibility that we take, that we, like our view is like, we're gonna own this problem no matter what. And the, you know, we've had now a couple of concrete examples where we have customer issues that, like at the end is like not a. You know, is it an oxide problem?

[01:26:02] **Bryan:** It's like, well, no, it fill in a gap between oxide and a system we were talking to. And I think it's a point of pride that we take responsibility for taking that all the way to, to root cause. I sorry to be plugging around podcast here, whenever the, the internet jokes that we're not, that we are actually a podcasting company that is merely creating computers for content creation.

[01:26:23] **Bryan:** And I'm not sure they're wrong, Uh, and so every, you know, whenever we have any kind of like crisis at Oxide in terms of debugging a problem or what have you, we're like, God, this is gonna be great content. And we had one of these, uh, an episode that we called Hell is other networks where, uh, we, um, had a customer.

[01:26:40] **Bryan:** Where we took this particular switch and, and uh, talking to, to the oxide rack and each, the oxide rack and the router were, were making like reasonable decisions on their own, but you added it up and it was a nightmare. um, you know, we were able to get that debugged to root cause 

[01:26:56] **Bryan:** And even though you, again, like our behavior was reasonable and its behavior was reasonable, um, but we wanna be able to take responsibility for that. So I think it's a, it is twofold. It's the fact that we can control these layers of the stack, but then it's also very much the sense that we have suffered at the other end of this.

[01:27:10] **Bryan:** And what we wanna be able to do is really take on that responsibility and get a customer actually righted wherever the problem may lie.

[01:27:21] **Jeremy:** I think that's a good spot to end it on, but anything else you wanted to mention?

[01:27:26] **Bryan:** No, it was great. I know I be hit on a bunch of things, so hopefully the, thanks for the wide ranging conversation. This is, this was, this was great. Started to go on and probably went on a couple, one too many rants, but, you know, as I'm want to do

[01:27:37] **Jeremy:** That's what the people wanna hear.

[01:27:39] **Bryan:** it is what the people want is what you gotta give the people what they want.

[01:27:42] **Bryan:** You gotta give the people what, you know, what I actually didn't do at all as I did, I didn't go on any anti Oracle screed, which is now like the, I, I, uh, I, you know, am somewhat internet famous for my, my unvarnished opinions on Oracle. And, uh, you know, as, uh, as the, uh, David Ellison in Paramount has been more in the news, I've had journalists talking, calling me up because they see Hacker News comments where I'm talking about Oracle.

[01:28:06] **Bryan:** So it's like, you know, I, I'm, this is what I'm, I'm famous for now. It's my, my unvarnished opinions and Oracle. So I'm sorry to not give the people what they want in that regard, you know? I'm sorry.

[01:28:14] **Jeremy:** You'll, you'll always be tied to, to Larry, I guess.

[01:28:19] **Bryan:** Minute 33 I know is always gonna, it's fine. I'll, I'll take it. Truth to power. I, I don't mind speaking it.

[01:28:27] **Jeremy:** All right, So if people wanna check out what's going on at Oxide, check out your podcast, 

[01:28:32] **Bryan:** You have Oxide and friends. Um, you can join us live in the Discord I would love to have people, uh, join us live. Um, but, but check out the podcast feed, um, and check out the rfds. You can. Those are all, uh, out there as well. uh, and then check out the repos. Um, you know, we're, we're, everything we've talked about today is open source, so, um, people can dive in there and see what we're actually doing.

[01:28:52] **Bryan:** we are really pride ourselves on that transparency. So, we leave nothing to the imagination. I think that sometimes people are like, okay, maybe you guys could share just a little bit less, you know, so maybe transparency to a fault, but, um, there's a lot to go dive into if you wanna, dive into oxide.

[01:29:10] **Jeremy:** Yeah, I, I think for the people who are actually managing these data centers and working with traditional vendors, transparency is exactly what they wanna hear.

[01:29:21] **Bryan:** It is, it is. Yes. I think that that transparency is, we did have an early customer that had an issue and we wanted to get back to them and let them know like, Hey, we're working on your issue. The customer's like, no, no, I know you're working on it. I'm watching the GitHub issue actually.

[01:29:35] **Bryan:** It's great. It's like, oh, okay. So, you know, the, it, it's, um, we love that we, we love the fact that people can see what we're working on. We have always felt there's much more to gain than there is to lose

[01:29:48] **Jeremy:** Very cool. Well, Bryan, thank you for chatting with me today. This was fun.

[01:29:51] **Bryan:** Absolutely. Thanks for having me. This was a, this was a lot of fun. Uh, and, and sorry to take you into the filth that is the modern data center.