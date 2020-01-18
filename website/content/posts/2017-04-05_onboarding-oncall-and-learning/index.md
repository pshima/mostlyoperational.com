---
title: "Onboarding, On-Call and Learning"
author: "Pete Shima"
date: 2017-04-05T16:32:47.353Z
lastmod: 2020-01-18T11:48:58-08:00

description: ""

subtitle: "A while back in the hangops slack I offered to try and help anyone that I could in the #career_advice or #job_board channels. I am no…"
tags:
 - DevOps
 - Onboarding
 - On Call
 - Sre




aliases:
    - "/onboarding-on-call-and-learning-46ff297a2587"

---

A while back in the [hangops](https://signup.hangops.com/) slack I offered to try and help anyone that I could in the #career_advice or #job_board channels. I am no expert on these topics but maybe I have some knowledge that will help others. I recently received an email with some great questions that I thought would share.

### 1. Onboarding
> There’s an unlimited amount of stuff to go through for SRE #2, but I want to have their onboarding experience be an enjoyable one. How do you balance those things? I need to bring the second SRE up to speed fast(-ish), but I don’t want to burn them out quickly. Also, what does a good onboarding process look like for an SRE?

Onboarding is a very critical part of someone starting at a new job and this is universal across job roles. The first 90 days of someone starting a job can be the most critical period for their long term experience and satisfaction.

#### Get your house in order

It’s very common when things are hectic to wait for someone to join before really starting to figure out how to expand the team. You really need to start planning this change well before they start, otherwise it can be a big red flag for folks if they jump in to chaos. Take a step back — why are you hiring this person? What will they work on and who will they work with in their first 90 days? What does your team’s roadmap look like? This can be hard on a team of one or a team of many especially if a lot of your time is spent firefighting. Keep in mind that hiring someone to the team is not a short term exercise and you likely aren’t hiring someone to work for a few months, but a few years. Don’t lose sight of what impact you expect that person to make in the first twelve months.

#### Build an onboarding plan

This is highlighted in the previous part, but it is really important. It also can be a bit intimidating and might feel a bit corporate but it doesn’t have to be. Start with what they should do on their first day, and each day of their first week. Then what they should do on their second week, third week and fourth week. Following that, what they should do in their third month at the company.

Re-read what you have written. Does it sound interesting? Does it sound like a bunch of clean up work? Would you join the company to do this? Focusing on the impact that they will make will help avoid putting people on busy work their first few months.

Give them something they can own. If it really is just the need for a fire extinguisher for the first few months then just be honest about it, it will go a lot further than trying to hide it. A word of warning though, if you really need help in fire fighting is one person going to solve that? Probably not. Make sure your plan involves getting yourself out of the red, not just calming the tide.

Give them a small project to work on on day one. Some people prefer to just dive straight in to working or coding and giving them that opportunity can be great when they want to take a break from learning.

Make sure to include also basic steps in the onboarding plan to enable them to commit code or changes without shooting themselves in the foot. If they can deploy safely on day 1, have them do it. Be cautious on safety here though, taking down production day 1 or even in the first 90 days isn’t a good sign so make sure to either pair with them on it or have them use processes that have the appropriate guard rails.

#### Get historical

Onboarding can often miss the history and context of how things got to the point they are today. Don’t forget to build a timeline out of what happened before this person joined. Helping them understand the whys about a broken system or why something is built a certain way is context that will really help them and something they are very unlikely to read on a wiki — if they can even find it on the wiki. Speaking of which, build a wiki index for them as well on the main points they should read up on. Have them pick three things they learned when they joined and have them write wikis on them. If they are learning them, it is likely the next person joining will need that info as well.

If you have post mortems, pick the most important ones to review and spend some in-person time actually walking through them, what happened and how some of the conclusions were made. This might also be a good opportunity to rework that process. If you don’t have a post mortem process now might be a good time to start one.

#### Mixed mediums

When the new person is learning give them different mediums to learn on. While wikis and videos are great for solo learning it can be exhausting to be thrown into a pool of documents or videos to just spend a week reviewing. Try and have at minimum a one hour interactive session once a day for the first couple of weeks to leave time to ask questions and have open ended conversation. Spend time white boarding out the organization, and the infrastructure and focus on how things work. If you are unable to whiteboard these things then it is a good opportunity to polish up on these things yourself, or involve others in the conversation as well. Setup specific sessions with other teams to talk about what they work on, how they work, what challenges they are facing today. Having different ways of learning also depends on the person but I find having a balance between conversation driven and solo driven information is very important.

#### Be a connector

As the person doing the onboarding you will know a lot more of the people and team structure of the company. Connect this person up to people all around the company, not just people they will immediately work with but as many people as you can immediately after they start. Setup 1:1 coffee or lunch meetings with people from all sorts of other departments. As an SRE or ops member it’s likely they will be dealing with putting out fires, maybe sometimes even big ones, that can have an impact on people, revenue, or the success of the company. Having this new person get to know people will help them be successful and have a human connection for folks when big incidents do occur. It can easily be forgotten during high impact situations that a human probably wrote the code, built the system/architecture, and is not a robot on the other end of a conference call or email. Making that human connection before high impact situations occur can be a positive experience.

### 2. On-call
> Because the operations team is so small and we’re moving towards services, I want to balance the pager load amongst the development team. But there’s a major hurdle in that. Developers seem a little unwilling to take on-call and there’s very little trust from up above in the ability of folks to manage their own services. Have you had to convince a team of the merits of this before? What works?

I’ve been in many different situations before:

*   No on call (aka pray mode)
*   Ops on call 24x7 (sometimes single individual)
*   Ops on call during the day, dev at night, one rotation
*   Devs and ops on call, shared rotation
*   Devs on call, ops as escalation on call
*   Devs on call for their services, ops on call for customer issues

There is no one right answer for the way to approach on call, so much depends on the company size, company culture, and business expectations.

If developers don’t have to pick up the pager why would they? What advantages do they have from being on a pager rotation and responding to events?

There have been a couple things that have helped me along the way.

#### You build it, you run it

This is a great quote from the CTO of Amazon and it’s talked about in this [blog post](http://aronatkins.github.io/2014/12/23/you-build-it-you-own-it.html). In short, the quality of the software and the customer experience with that software rises significantly in this model.

#### 100% ownership culture

Another great example from Netflix: [https://youtu.be/-mL3zT1iIKw?t=1010](https://youtu.be/-mL3zT1iIKw?t=1010)

“Why would I take someone who’s expertise is in operations and try to make them a software engineer that happens to write this piece of software and understand what it is supposed to do, when I actually have the software developers that actually wrote this software and understand what it’s supposed to do. So we engage with our service teams that own that software when there are problems so I have the world experts on how that thing is supposed to be operating right there with me protecting my customer experience.”

Watch the whole video on this there is a lot of great ideas and information.

#### You probably aren’t Netflix or Amazon or Google

While the above are great examples of success stories, you probably aren’t at this same scale or have the same business requirements that they do. But there is an important bit these companies have learned: having a centralized operations team that handles all issues does not scale well. Operations quickly becomes the bottleneck for a ton of things that then has an impact at the speed at which the entire company operates. In a small company having a centralized operations team that handles these things might be the right move, but there is definitely a tipping point where availability and reliability of services are more important than features and the ops team likely won’t be able to scale. It doesn’t matter what features you have if your services are down. This comes back to customer trust and something else mentioned in the Netflix video, protecting the customer experience.

#### Page only on things you know cause customer impact

One thing I like to do is to just propose to delete alarms or lower alarm severity. I’ve seen and worked at a number of places that tend to have a bunch of noise in alarming. When proposing to delete alarms, see who reacts to that. It’s not uncommon for someone to speak up to say “We can’t delete that alarm!” Asking why it doesn’t make sense to delete that alarm gives different context on what the true value of that alarm is. Noise reduction is incredibly important to making this successful. Everyone should care if people are getting woken up at night, and if alarms are moved to the development teams and they are being woken up then it is still everyone’s responsibility to try and reduce wake up calls. On each page have a mini post mortem — did we need to wake someone up for this? Regular review of this is paramount.

#### A big opportunity to learn

Some of the best people I have worked with are very curious people that love to learn. This is an opportunity for people on the team to learn a superpower — Opsing! This sounds a bit cheesy but it’s entirely true, learning how things operate and applying that knowledge in the software development process is incredibly valuable.

#### Make data driven decisions

Using data is incredibly important in this process as well. If 90% of the time an alarm fires the cause has to be solved by the development team why wouldn’t we just page them directly and they can escalate to ops if needed? Another important data point when moving alarms is to determine how often that engagement is likely to happen. If it’s once every 6 months it shouldn’t be a huge deal to move(or conversely not), but if it is once a week that is a significantly different conversation.

#### Have a good understanding around what can, and should be, moved to development teams

This again goes back to a thought in the Netflix video above. Asking a software developer to be a network engineer or know deep internals on infrastructure isn’t realistic and is probably going to cause more problems than it solves. Start with the alarms that are known (through data) to be resolved by the development teams. It’s unrealistic to think that with previous help of the ops team, that a dev team can own the whole stack overnight. Ownership has to be realistic, take a pragmatic approach. Build tools that help the development teams be successful.

#### Don’t put up with shit

Honestly, don’t tolerate crappy alarms and lack of action on reoccurring problems. It’s easy to fall in to traps where people become desensitized to alarms and noise. At the end of the day it’s up to you on what actions you are going to take.

#### There’s no silver bullet

There isn’t one single trick that is going to make all of this work. The most successful thing I have seen in the past has been with strong leadership and company culture. If you have those the rest will fall in to place.

### 3. Learning
> What resources do you use to learn?

#### Twitter

Twitter is by far the best learning resource I have come across, however it took me a very long time to build up the list of people I follow to give me a stream of information I can use.

#### DevOps Weekly

This is a pretty great newsletter for dev opsing [http://www.devopsweekly.com/](http://www.devopsweekly.com/)

#### SRE Weekly

Another great weekly newsletter focused on SRE specific content. [https://sreweekly.com/](https://sreweekly.com/)

#### Monitoring Weekly

A newer newsletter focused around monitoring. [http://weekly.monitoring.love/](http://weekly.monitoring.love/)

#### Software Lead Weekly

Whether you are a lead or not there is really great information here. [http://softwareleadweekly.com/](http://softwareleadweekly.com/)

#### Google SRE Handbook

Some great information in here that is now available free online: [https://landing.google.com/sre/book/index.html](https://landing.google.com/sre/book/index.html)

#### Adventure Time/Reading Rainbow

Adventure Time and or Reading Rainbow are meetings I tend to schedule across the company to talk more about how things work. Open ended Q&amp;A, no slides, just chat. Come and learn! Learning is fun!

#### Mentorship

Mentorship is a fantastic way to learn more. Find someone outside of your team or organization that you can learn from.

#### Hangops

There are a lot of great conversations that happen in [this slack](https://signup.hangops.com/). I mostly idle/lurk but a lot of interesting things going on here.

### Contact

If you’d like to ask me some questions please do, or if you’d like to share your thoughts on onboarding, learning or sharing on-call please send me a tweet or an email.
