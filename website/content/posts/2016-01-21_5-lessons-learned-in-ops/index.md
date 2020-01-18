---
title: "5 Lessons Learned in Ops"
author: "Pete Shima"
date: 2016-01-21T18:05:58.569Z
lastmod: 2020-01-18T10:37:08-08:00

description: ""

subtitle: "I have a lot of knowledge I would like to share but personally consider specific or situational which makes it hard for me to feel like…"

image: "/posts/2016-01-21_5-lessons-learned-in-ops/images/1.png" 
images:
 - "/posts/2016-01-21_5-lessons-learned-in-ops/images/1.png" 
 - "/posts/2016-01-21_5-lessons-learned-in-ops/images/2.gif" 
 - "/posts/2016-01-21_5-lessons-learned-in-ops/images/3.gif" 
 - "/posts/2016-01-21_5-lessons-learned-in-ops/images/4.gif" 
 - "/posts/2016-01-21_5-lessons-learned-in-ops/images/5.gif" 
 - "/posts/2016-01-21_5-lessons-learned-in-ops/images/6.gif" 


aliases:
    - "/5-lessons-learned-in-ops-4164a9cdd911"
---

I have a lot of knowledge I would like to share but personally consider specific or situational which makes it hard for me to feel like this could be valuable to a broader audience, but here goes. I am also trying out Medium for the first time, it seems like a good platform. I have always maintained my own blog which has fallen to the wayside.

Looking back, there were a considerable amount of great posts on systems, operations, DevOps and reliability in 2015, but the one that stood out the most for me was [Charity Majors](https://twitter.com/mipsytipsy) on [Hiring A Tech Ops Team](http://www.heavybit.com/library/video/2015-02-24-charity-majors). I did not see any of the presentations on this unfortunately, only the post which stands out clearly in my mind.

If there was one talk I wish I would have been able to see this year, it would have been this one. There are a considerable amount of gems in this information. My other favorite post was on being a senior engineer but I can’t find it at the moment. It was probably posted in 2013 or 2014 anyway.

I also enjoyed [Adam Jacob’s](https://twitter.com/adamhjk) talk on DevOps: [Chef Style DevOps Kungfu](https://www.youtube.com/watch?v=_DEToXsgrPc). It made me change the way I think about DevOps and my overall feelings around it.

So I will start 2016 by posting a few lessons learned in working on operations teams, either a solo team or a team of many.

### 1. Why

Questioning how things are operating and getting deeper to the whys is the greatest tool available at your disposal. Why? Good question. If you work in operations it is your goal to get others to care about operations as well. I don’t just mean technical specifics like getting to care about why that shell script you wrote back in 1999 is so perfect that servers cower in defeat while they are provisioned in silence. I mean about how things work. I tend to find that great engineers are those that really want to know how things work and why they work that way. Not just in technical operations but how code works, how their microwave works, how spaceships work. They spend a great deal understanding not just the code they checked into GitHub, but how that code actually operates in production. Until you’ve got it running in production it is theory with some unit tests. 100% code coverage on a system that doesn’t operate or fails often isn’t a great system.

Asking why helps with comprehension and leads people in helping to understand each other, and following down this path can help with empathy. If someone really wants you or your team to do some work, stop to ask them why. Problem solve with them. In the heat of battle, a lot of solutions come out of emotional reaction to issues. Take the emotion out of the solution and see what makes the most sense to solve it. Use the why to get there and use data to back it up.

It is too often that “ops” becomes an overloaded term and teams become overloaded with work that doesn’t belong anywhere. If there is a mess to clean up, that doesn’t default to an “ops” problem. In some organizations that may be the truth, but this leads to “ops” being mostly clean up work which the business does not value. There is an age old saying about what you put in to something is what you get out of it. Use the why to guide the conversation.




![image](/posts/2016-01-21_5-lessons-learned-in-ops/images/1.png)



Some would say this is just the 5 whys in disguise and could be considered harmful, but used as a communication tool this can really help to get people on the same page.

### 2. Invisible Work

People that have worked with me will tell you that I am a big enemy of invisible work. What is invisible work say you? It is the work that gets done that no one knows is happening or happens in the background. This comes hand and feet with operations, frantically trying to put out the next tire fire before it becomes a real problem.




[![image](/posts/2016-01-21_5-lessons-learned-in-ops/images/2.gif)](http://devopsreactions.tumblr.com/post/133585717447/answering-support-emails)



But in all seriousness, visibility is the second most valuable tool you can use in your ops organization to persuade others. Making data driven decisions helps put things into perspective and can help others understand what the hell it is you do here.

Once a week, send an email out to the entire team that can be read in 5 minutes. Include in this email what happened last week and what the plan is for this week. Include things that went well and went poorly. Air your “dirty laundry”. Keep it to a couple sentences and 5 bullet points. Probably 90% of it will end up in junk mail but for those 5 people that do read it, they know a little bit more about what you do.

Build a list of projects you want to complete each month and try and stick to it. Any unplanned work that comes up keep track of it and keep track of how many times that plan changed in a month. Anything that is not written down never happened (ok it did happen but you get the point).

If you have worked with me, you know I am overly verbose in written communication and tend to over communicate. My issues are long and filled with my thought process. I consider these positives while some would not, but looking at the last month in Slack I am not the top talker!

### 3. Positive space, not negative space

A skilled engineer once told me that operations teams operate in the negative space and this is something that resonated with me time and time again. Engineering teams often operate with a roadmap or a waterfall or some specific areas of work that they focus on. This is the positive space they have defined for their team and what they do, areas of responsibility.

Operations is generally the opposite. If it doesn’t fit in one of the teams areas of responsibility, it is operational work. Operations becomes responsible for everything that isn’t a feature. This can be a real challenge. Take some time to really think about what it is your team does, and bring that identity to your team in any way you can. Be realistic though and use the why to question your own decisions on if your plans make sense. Saying that all your team does is write Chef recipes, when the business goals are not to write Chef recipes will not help you.

In a meet-up last week I heard someone mention that they tell their folks that there is no “ops” team and I find that to be a common movement in my travels. This is because their team has specific goals that are not to do all the work that no one else wants to do. Every team has work they don’t want to do or don’t have time to do, throwing it over the wall creates conflict.




[![image](/posts/2016-01-21_5-lessons-learned-in-ops/images/3.gif)](http://devopsreactions.tumblr.com/post/115927876082/forkbomb)



But what happens to the other work? Those hosts aren’t going to reboot themselves and that mess over in service B isn’t going to clean itself up. Take time to write down the problem and possible solutions to it that clean it up for good. Sometimes you are just going to need to bite the bullet and take that work, but the three messes that now became projects and are divided across many teams will help everyone scale. Highlight the operational work that others do in demos or by calling them out to leadership. Write them a nice personal note about their project. Include their manager.

### 4. Safety through process, not police work

A very common theme I have seen for ops teams in the past is to become the police of the system. You have to sign ten papers to do a deployment, you have to follow a specific change management practice and if you decide to break the law, just don’t get caught! I have seen this style bring an incredible amount of frustration to both sides of an argument and it is not worth it.

Don’t tell people they can’t do something because it is against the rules. If you see someone crossing a dangerous ops cavern, build them a bridge that lets them cross safely. No one is going to purposefully login to try and take down production(ok well there was that one time). But really, people want to get in there, get their changes or deployments out and get out with no harm caused. Sometimes there will be some cuts and bruises and hurt feelings, but learning from your mistakes is incredibly valuable, as long as it doesn’t cost you your business or lasting impact with your customers.




[![image](/posts/2016-01-21_5-lessons-learned-in-ops/images/4.gif)](http://devopsreactions.tumblr.com/post/105343812909/accidentally-destroying-the-wrong-vm)



There is a line that does need to be crossed though; it is easy to say there are no rules everyone do whatever they want in production! It will be fine! Build safety mechanisms to allow people not to hurt themselves. When you see someone about to hurt someone or themselves, be a good citizen and stop them. Citizen’s arrest!

Sometimes it is difficult to put safety checks in the tools you use, or you just don’t have time to rewrite that 2000 line server provisioning script from 1999 with no tests. In that case, create a process that others can use to do things safely, but make sure to include the context as why this has to be done this way. If you have documentation for a previous real issue that this caused, link directly to it. Remember that time in ’98 when production was down for eight days, yeah, be careful. Follow these steps to avoid the Indiana Jones Temple of Operational Doom.

### 5. Optimize for safety and speed

As an operator you may be faced with a situation where you may need to do something dangerous to get something done. So what do you do? Take production down to get that feature out or wait two weeks to change the architecture so the bus doesn’t crash half way up the mountain. This is something I still struggle with today, as speed is very important to business.




[![image](/posts/2016-01-21_5-lessons-learned-in-ops/images/5.gif)](http://devopsreactions.tumblr.com/post/114745110667/data-decapsulation)



A manager of mine once taught me something that became more important over time. When confronted with a situation that may be dangerous, categorize each item you think needs to be changes into need, want, and nice-to-have. Need should be items that are likely to cause a production outage based on data, wants are things that you might need for rarer cases and other nice-to-haves are things you generally just want to share. Make plans and get commitments to get the rest of the work done after the launch. If there are no real blockers and no data to back up your case, the fact that you don’t like it isn’t a good enough reason to halt a launch.

The important point that my manager was making here is “Don’t let perfect be the enemy of good.” I have worked with many engineers and I myself have thought at times that we must have a perfect system before it can be deployed, but when that means you won’t have anything to work with for months or years the trade off ends up not being worth it. Take the path that is acceptable and can be iterated on. Get incremental value. Finding the balance here without cutting dangerous corners is still very difficult for me.These are a few things I have learned over time and I hope they are helpful or interesting to you. Your success rate may vary, along with your leadership! If you enjoyed or hated this article, either way, I would love to hear from you.

My name is [Pete Shima](https://twitter.com/Petey5K) and I am an Engineer at [HashiCorp](http://www.hashicorp.com). These opinions do not reflect that of my employer.Credit to most of the images to [DevOps Reactions](http://devopsreactions.tumblr.com/). I’ve tried to link to the existing posts because I cannot add direct links as images here on Medium.




[![image](/posts/2016-01-21_5-lessons-learned-in-ops/images/6.gif)](http://devopsreactions.tumblr.com/post/134259409293/mondays-login-after-fridays-password-change)
