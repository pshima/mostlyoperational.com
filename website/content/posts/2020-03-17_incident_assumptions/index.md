---
title: "On Incident Assumptions"
author: "Pete Shima"
date: 2020-03-17T18:46:49.944Z
lastmod: 2020-03-17T10:37:17-08:00

description: ""

subtitle: "How did this ever work?"
---

## The world is on fire

If you have been in a large number of high severity incidents you have probably been at one time or another in a place where what you thought was happening based on graphs, logs or other data wasn’t what was really happening.  Some important bit in the code, workflow, process or user case was missing. Or perhaps you were sitting there wondering to yourself, “How is this possibly working?”

The pressure is on, the site is down, or maybe you think all the data is missing, or you’ve just launched something new and amazing but the world started melting.  At this point you probably have a number of experts engaged, or in a lot of cases with this high severity of an issue, maybe you have engaged everyone that could possibly help.  Hopefully you have an organization that understands that shit happens and binds together to resolve the issue.

In these situations there is going to be a lot of brainstorming going on and a lot of hypothesis made for what is causing the outage. Often there can be a lot of guesses for what is happening.  A lot of senior folks are likely engaged who have a deep understanding of how the systems work and make assumptions on what could happen from their expertise as well as known and unknown data.

Data can often be misleading, build an imperfect picture, and still be accurate to an extent.  I’ve been in situations of near outage where latency appeared to drastically decrease.  Opening a dashboard with graphs on response times and everything looks great but everything is more or less down. 100x increase in cheap requests and longer requests timing out in places before your data.  

I often find the same situation with load testing.  Load testing will generate data that will not exactly mirror user behavior and can give people false confidence in a system.  Load testing to hundreds of thousands of requests per second will give you some measures, but using those to determine theoretical limits of a system often are fraught with peril.  You should still do load testing, you will certainly find issues, but the data you see during these tests will likely differ from what you will see in production.  

## Process 

With a million ideas or suggestions being thrown out in an incident, how do you choose what to investigate and how to prove out solutions?  Speed is important during these times and here are some tips.

### Understand and use the expertise of the people available
Some people can do certain tasks very quickly or from muscle memory.  If you have an expert log diver have them log dive and find information the team needs instead of digging in to a system they may be unfamiliar with.  This can be challenging to know what skills people have in a high severity incident, but just ask - who is the best person available to do this?  What may take someone 1 hour to do with a tool they are not familiar with may take an expert 10 minutes.  

### Educate people on the tools
People’s ability to use tools to debug, or test the system are critical.  Unfamiliarity with tooling needed to debug or test can cost an investigation considerable amount of time.  This is counter to the point about just better tools. Better tools will help but just introducing new tools that folks don’t know how to use effectively, or even log in to can slow things down further.  

### Often you don’t need all the data (for cardinality or pointers)
While there are some cases that may require 100% of data, often times looking at a sample of the data can help educate you on where else to look.  Generic commonalities across entries is an easy example.  Same user agent?  Same IP?  Later the whole data set can be analyzed but trying to get an EMR job running during an incident may lose hours of time.

### Split into working groups, run in parallel
If someone has a reasonable task to go investigate then split them(or a number of people) off.  I would suggest not to debug with everyone together in the same group.  Often conclusions or information one group finds will impact the results of the other and they will influence each other’s decisions.  Sometimes this can be positive but in the heat of a fire event miscommunications can be common or terse and what someone meant in one discovery may not mean what someone else thought.

### Choose options that narrow the funnel, or eliminate possibilities
This is somewhat of an antipattern itself but start eliminating possibilities.  If a hypothesis is made what data would you need to prove it true or false?  Choose quick and easy ones first.  Weight away from a load balancer, terminate a host, rollback.  As an example, restoring a database to see what data looked like before the incident may likely take considerable amount of time and narrow the funnel but may take hours.

### Always think about the next steps
It can be easy to run down a lead and think, “This is it, let’s wait to see what happens”. More times than not the incident won’t be resolved and you’ll have to move on to the next thing.  If there are people available to help that are also waiting, have them start on the next thing.

### Listen to everyone
Many incidents I have been a part of a junior or new member of the team had good ideas that should have been pursued earlier.  Often, assumptions the senior experts have made from their experience on the existing systems can overlook other points of failure.  Junior or new folks can be unbiased on these and provide fresh perspectives and sometimes can be hesitant to speak up.

### Don’t over analyze
If you’ve got a good reasonable idea, just go for it.  Just don’t forget peer review and communication.


## Technical
But a few technical items specific to being able to test assumptions quickly

### If there was a recent deploy, revert it immediately and without question
This assumes you have an easy way to revert to the previous code in production.  Why?  Just eliminate the variable of new code introduced.  It is one less thing to need to debug.  If things return to normal, you now can look deeper at the changes, if they don’t there’s a good chance something else is going wrong.  It’s not surefire, but this helps eliminate variables.  Pushing back against reverting code is a bit of an antipattern when it comes to speed of recovery, but can make sense if your system is not designed to do this.

### Have a safe way to debug in production
This could mean enabling some debug mode on a single or subset of hosts, or sending 1% of traffic to a testing fleet with a different build, etc

### Have tunables for your app, and quick deploys
However you are deciding to make changes, be able to do it quickly and check the results.

### Make adding log lines or events or metrics dead simple
Often a single event or log line or instrumenting a new event could help prove or disprove a theory.  The ability to add and deploy these sorts of changes quickly, easily and safely is critical.

### Have a readily available, easy to test environment
Testing in production at large scale safely is important, but sometimes you need to do deeper validation.  If you don’t have a place to test it and can’t spin up something quickly then validating these changes will likely take significantly longer than they need to.
