---
layout: post
title: "WWCode Hackathon Recap"
date: 2016-08-02 23:06:42
author: "Lauren Oldja"
categories:
- blog
- WWCode
img: wwchack-logo.jpg
thumb: wwcatlhack-thumb.gif
---

Last weekend I had an unparalled opportunity to participate in the [WWCodeATL hackathon](http://www.wwcodehackathon.com/), hosted at [ATDC](http://atdc.org/) in Tech Square. This was the first such hackathon co-organized by the Tampa, Atlanta, and Charlotte chapters of Women Who Code, and I'll highlight below some unusual aspects of the event that, as a participant, I think worked really well.<!--more-->

Day One
====== 

For starters, an entire day (Friday) was devoted to brainstorming and inspiration, which lay foundation for what would traditionally be the first event at a hackathon: the idea pitch session and team formation. Friday morning, several of the mentors who would be available throughout the weekend hosted breakout sessions to demo code and project ideas of their own, then after lunch WWCodeATL gave a session called "Hackathon 101", in which they went over the format, strategies for working under tight deadlines, and broke us into very broad interest groups (IoT, Social, Media, Misc) from which smaller groups organically emerged. It was from during these sessions that the idea my team ultimately decided to pitch and present came. 

After "Hackathon 101" WWCode organized a powerful inspirational keynote from none other than Regina Wallace-Jones, the Head of Security at Facebook, who had also spoken at [Connect](http://www.geekwire.com/2016/women-who-code/) in March. After describing her own journey in tech, she shared this inspirational take away message: 

> Step out of the smallness of technical skills. Step into inspiring millions. Look inside yourself, how you surround yourself, how you spend your time. Ask: Am I just checking the boxes? Really find what unleashes what's inside you, then run with it. That's where your engineering begins.


A happy hour followed, which was great for informal networking. I met several future team members this way, connecting with them as known actors during the team formation/ pitch meeting that followed. This team formation was the final event for Friday. Saturday we had access to the space for all day hacking from 8AM - 10PM. Sunday the space was again available from 8AM, and our final presentations in front of judges began at 4PM. What a whirlwind!

Day Two &amp; Three
====== 

Within IoT I personally have a soft spot for commercial and industrial applications. Consumer goods tend to capture the imagination due to their relatability and everyman-relevance (motion sensing cameras on your front door! a fridge that tells you when you're out of milk! [a sous vide you can set from work!](http://anovaculinary.com/anova-precision-cooker/)). Meanwhile the non-consumer IoT revolution has proceeded quietly and without marketing fanfare, but none of us are strangers to the concept of smart traffic lights or early warning systems. IoT already has significant adoption among the largest industry players and far greater potential for wide-reaching productivity improvements. 

We framed our hacking around a central idea: small- to mid-sized fuel farms need sensors to automatically check for abnormalities in the system which could indicate a leak or otherwise unsafe condition. We aimed to target small- to medium-sized fuel farms, likely with <100 employees per location and <$50M in revenue for an off-the-shelf solution requiring no dedicated engineers on staff. 

Shirley, from WWCodeBirmingham, was thoughtful enough to bring with her five Arduino starter kits fron her local hackerspace for open use during the event. This seemed as good of an excuse as any to hack around with the hardware. We decided to take our idea and run with it, acknowledging up front that -- especially since none of us had experience with Arduino and no mentors would be on hand having had direct experience with the system -- we were unlikely to achieve **MVP** (minimum viable product) within the course of a single weekend and therefore were also extremely unlikely to "win" the hackathon.

Nonetheless, we sketched out what MVP would look like:

+ Obtain sensor data using Processing language and Arduino
+ Pyrebase script on computer physically attached to Arduino sends input data to Firebase
+ Data stored in Firebase are JSON objects, get out via API
+ Multiple system monitoring tools can read this API, whether a simple web dashboard using jQuery, HTML, CSS, and Bootstrap
+ Real time montinoring should have real-time alerts to SMS, or other

And in the end we were able to get temperature sensor data from an Arduino-attached thermistor real-time into [Google Firebase](https://firebase.google.com/). Our (messy) codebase is available on [Github](https://github.com/kafsima/wwc-atl-hack/). We presented on this demo as well as our business case, which was pretty solid. In fact, we ended up getting a nod from the judges for it, winning the "Business Smart" team award and six months of coworking space access -- cool!

![Business Smart WWCode Hackathon team winners](/assets/img/blog/wwcatlhack-3.jpg)

In Summary
====== 
+ For the majority of participants by show of hands, this was her first hackathon. And yet nearly all participants I spoke with had worked in tech professionally for over five years. In my team, for example, we only had one student and one career-changer (me). It's clear there is demand for female-friendly hackathons in the tech sector that is being unmet. Women want to participate in these types of focused coding events, and WWCode provides an environment where the perceived *culture* of hackathons is more appealing. There were no all-night sessions, enabling parents to participate. There were meals that consisted of more than pizza. Nobody smelled bad. There were non-alcoholic options (yes please and thank you, LaCroix). Everyone was welcome, and in the end all teams stayed for the full event and presented.
+ I really liked that there was a good mix of local and regional participants. I flew in for the event and stayed at a hotel across the street, which couldn't be more convenient. The presence of regional WWCode chapters and invited judges and speakers gave the event more gravitas than a typical weekend chapter meeting. And yet, the presence of so many local participants gave the hackathon a sense of place. After this experience, I really do feel that in some small way I am a welcome part of the Atlanta tech scene. Following the Hackathon, I attended the Monday happy hour meetup for [All the Nerdy Ladies](https://www.meetup.com/Women-Who-Code-Atlanta/events/228475340/), and it was fun to see so many familiar faces at that event.
+ The logistics of pulling together any large event like this are non-trivial, and WWCodeATL went way above and beyond what I expected out of this event. Kudos to WWCodeATL and partners for impressive organizing from this first-time volunteer team!

Lessons Learned
====== 
+ Existing Arduino tutorials are not very cloud-friendly. Those that use Firebase are few and far between and tend to link to out-of-date documentation.
+ In an attempt to be user friendly, current Firebase documentation asks that you first choose your path, whether you're building a mobile or web app, but does not let you get by saying "neither". Since we were just running a local script, all the rest seemed unnecessarily "helpful".
+ If you're in it to win it, determine the skill set of available mentors on site before proceeding. Our IoT mentors had brought their own (non-Arduino) kits designed for wearables, and we may have achieved more technically had we decided to go down that route instead of stubbornly focusing on leaky pipes ;) (I have no regrets.) Similarly, these days I tend to prefer Python, but Pythonista mentors were underrepresented. That said, even if you code in Python, don't miss the next event since this one was super fun!
+ I found this bracelet. You never know where the best advice might come from. So don't panic, because when it comes to your product/idea/code...:
![Bracelet says 'it could always suck more'](/assets/img/blog/suckmore.jpg)

---

**Full disclosure**: While travel and accommodation were provided on my own dime, I did receive a sponsored ticket the WWCode CODE Review newsletter lottery. You can join the newsletter [here](https://www.womenwhocode.com/).

---


