---
title: "Thoughts on “The Error of Counting “Errors””"
author: ""
date: 
lastmod: 2020-01-18T10:38:25-08:00
draft: true
description: ""

subtitle: "This is my thoughts on the published paper of the error of counting errors and is part of a series of my learnings on Resilience…"

image: "/posts/draft__thoughts-on-the-error-of-counting-errors/images/1.png" 
images:
 - "/posts/draft__thoughts-on-the-error-of-counting-errors/images/1.png" 


aliases:
    - "/"
---

![image](/posts/draft__thoughts-on-the-error-of-counting-errors/images/1.png)



This is my thoughts on the published paper of the error of counting errors and is part of a series of my learnings on Resilience Engineering. It contains my initial thoughts and reactions to the paper in order to encompass learnings. My comments are in the head space of systems and software and sometimes the contrast between these and other fields.

### Format, layout, medium and discovery.

I am not accustomed to reading papers like this. I am trying to learn more through reading these. I chose this one randomly from a collection someone sent me and I find it to be a good starter because of its length. It was easy to read and short yet with several interesting points allowing me to read it multiple times over. The layout I didn’t feel was great. I dropped it on my kindle and needed to pinch zoom and scroll many times to read. Considering this is from 2008 I can’t hold any fault to the format in the digital era.

On googling for it via the title alone, it appeared to be a minefield of broken sites, pay or sign up gates, or web rings. The first 5 hits on google didn’t allow me to read it, or even linked to different papers. Perhaps the gates are by design. This is a published, copyrighted document and perhaps pay is expected, but for something that is around 1200 words it seems like a high cost to read. It is hard for me to understand if any of the paywalls would go to the author at all.

I believe this is a difference in fields of medicine and technology. From my naive understanding, medical journals are common practice and many of the meaningful ones are not free. In the tech world I would expect to google and be able to read this, or at least find a pointer to the single representation of the material. When I think of gates like this I think of Gartner or paywalls behind sites, not like O’Reilly or other books. I’d say that would primarily because of length of this content.

There are 15 references in the article. Reading them would would probably make me more educated on the topics but I imagine a number of these are hard to find and #6 is already a broken link.

### Main Ideas

The most interesting high level idea expressed in here seems to be that there is no such thing as human error, and that essentially by design this is the way human works, and therefore it is impossible for there to be an error under normal operation. Feels a bit like this is a feature, not a bug!

In thinking about it I would imagine this is a bit like Data from Star Trek feels, even though he technically has no emotion. From Data’s point of view, humans are flawed and often make mistakes and errors. From everyone else’s point of view they just acted “human”. We are by design imperfect, and that is actually what makes us great. It is what Data strives and looks for in the whole show. This is a weird take on this paper and I can’t believe I already did a Star Trek reference.

I generally agree with this article and do think it is insightful. 

### Positives

The notion that our systems are not intrinsically safe I think is a very good message that I strongly agree with.

Human error is not a cause but a sign of something deeper inside the system. Strongly agree with this. I often think of this when an issue occurs the problem is in the system and not with the person. If a system does not work like someone expected it to, the system is broken.

The notion that people do not operate in isolation and are part of complex, joint cognitive systems is a great frame of thought.

I agree with the sentiment on counting errors in this article. You can’t summarize what is here with a number very well at all. I agree that error counts are measures of ignorances rather than measures of risk.

### Troubles, Confusions or Questions

#### It pits one way against another and creates 2 “camps” of people. 

The old and the new. It also suggests the old way is wrong. This in itself is a bit polarizing but I am also happy that the paper itself talks directly to that and helps the reader understand.

One of the key points of the old way is: 
> Safety can be improved by protecting the system from the erratic humans through selection, training, procedures, protocols, automation, and discipline.

If we flip that, because it’s been inferred as “wrong” and there are only 2 “camps”:
> Safety **cannot** be improved by protecting the system from the erratic humans through selection, training, procedures, protocols, automation, and discipline.

I would fundamentally disagree with this statement. This is an issue I have in this paper where the mental model of folks could likely build 2 camps, and suggests the first camp is wrong, throwing all lines of thought, good or bad, out. 

Can we realistically say that a selected, trained doctor on procedure who is familiar with the protocols is not safer than someone who is not?

#### It suggests that “human error” cannot be a stopping point of an investigation

I’ve seen people really take this to heart and defend it and honestly had always wondered where this was from. I totally agree with the statements around this in the article, but what matters here is not the ending, it is the journey. If the most important thing is learning from an incident, and you do a great job about it, who cares if the ending was human error? In my mind that is not the material part of this. I absolutely agree that cutting an investigation short by labeling something as “human error” is the wrong thing to do. It is possible that a reasonable process can go both ways.

This is one of my issues I have experienced in this space, sentences or excerpts are taken as gospel. This space is all about learning and I’ve seen folks discard large portions of thought and audiences because of strict nomenclature over shared goals. Asking how and why rather than dismissing thoughts because of quotes and papers is an anti-pattern.

### Other thoughts

I worry this article makes human error a bad word. Why can’t we be comfortable with this phrase and accept that humans are by design imperfect and this is what makes us great? I am human, and the “errors” I have made to date are what make me who I am and I am happy to have them. I’d rather be a human in Star Trek than Data, but that’s just me.
