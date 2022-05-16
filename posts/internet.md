---
categories: 
 - Tech
tags:
 - moderation
 - projects
---
# Internet moderation
When people talk about moderation on the internet they focus on what's allowed on the internet. While that is important, we fail to consider who actually controls the flow of information.
## The problem
Lets simplify the "internet". 
 - The internet is made up of platforms
 - Each platform hosts content from users.
 - Content can be divided into desirable and undesirable content.
 - Undesirable content is naturally amplified because it drives controversy.
 - Undesirable content is by definition undesirable.
 - The platform is responsible for removing sufficiently undesirable content

I'm not going to bother explaining what undesirable or desirable content is. 
But some examples of what most will say constitutes undesirable content:
 - Child porn
 - Manifestos of mass shooters
 - ISIS Recruitment videos
 - Russian propaganda

And some desirable content that others may seek to remove:
 - Protest apps against dictators
 - LGBTQ+ apps 
 - Encrypted messengers

And some uncontroversially desirable content:
 - cat pics

There are several problems:
 - Platforms are incentivized to promote controversial content, yet are responsible for removing it.
 - The amount of content is so large that it is impossible to meaningfully sift through it.
 - Platforms, governments, and users don't agree on what is desirable and undesirable content.
 - This results in undesirable content being promoted while a small amount of desirable is removed. 

What we need is a solution which removes undesirable content and promotes desirable content.
## The solutions  
### The platform centric approach  

AKA the status quo.  
Platforms control the content which is present and promoted on their platforms.  
To remove undesirable content, people have several means:
 - Pressure the platform into removing content 
 - Force the platform through legislation or public pressure. 
 - Pressure advertisers to drop the platform 
 - Create your own platform 
 - Pressure infrastructure to drop the platform 
 - Buy your own platform 

And this solution is *not* working. The amount of undesirable content on the internet keeps growing with no end in sight.  
Make no mistake, this is intentional. [Foreign enemies](https://en.wikipedia.org/wiki/Russian_web_brigades) have used our own tools to drive us apart and wield armies of bots and trolls against us. Platforms know they promote disinformation but don't stop it because it makes them money. Information Warfare is being waged against us even if we don't accept that we're fighting this war. 

Much effort has been made to shift control of the platforms to and from groups that favor certain groups. But in the end, this is a system controlled by money and influence - not one of democratic means.
Furthermore, platforms are very vulnerable to force. Employees can be [threatened](https://www.wired.com/story/opinion-in-russia-apple-and-google-staff-get-muscled-up-by-the-state/). This means that while democratic governments wield little influence over our companies, foreign dictatorships can censor the web as they please.  
### The government centric approach 

The EU is perhaps the most likely to implement such a policy. Rules that essentially move moderation out into the open, under the hands of the government have several key advantages.
 - Governments do not have the same incentive to promote disinformation as platforms do
 - Governments can allocate resources to moderation without fear of loosing profits
 - EU Governments are democratically elected

But this has several key issues:
 - It is still weak to bots and massed disinformation. The sheer amount makes it impossible to centrally moderate 
 - Governments cannot be trusted to control speech.
 - Even if you trust *your* government, foreign governments will attempt to use their influence to force outcomes they prefer, as is already happening.
 - Governments are slow. Especially in the US, our politicians do not have the skill to implement good internet legislation.

Make no mistake, these problems can be mitigated through laws that protect US businesses from foreign censorship and increased human verification. 
This is my preferred solution and I think it's critical for a democratic society to implement these laws. 
### The people-centric approach
This idea is based on the idea of [matrix](https://matrix.org/docs/guides/moderation#outstanding-issues-2)'s [relative reputation](https://docs.google.com/document/d/1rijGLs9-RJ9Mz2Yk5wWycMbErrCDK1VJkACdUPMN0-M/edit#heading=h.j85wiuh6uzgi)
Let's say we have a censorship resistant platform. No one can remove content from it or control what's get added (assuming there's infinite storage and bandwidth).  
Everyone can create users with unique identifiers.  
We let users define their reputation with other users on a scale of -1 to 1. At each level, certain actions are preformed. For example:
- -0.5 > reputation: block
- 0.1 < reputation: can DM user 

And we can assign reputation in more user-friendly ways 
- +0.5 reputation: friend 
- +0.3 reputation: follower
- -0.3 reputation: mute 
- -0.7 reputation: report 

And we can attach content to these actions such as reasons for reports.  
But all of this has already been implemented. The real next step is to trace reputation through your reputation graph.  
Say I assigned A reputation 0.75, who after seeing B decapitate a Kitten, assigned reputation -0.5. Then I will have the reputation of the product assigned to B: -0.375. Graph reputation only follows positive reputation till the last step to prevent double negative reputation attacks.  
Alternatively, we can split reputation between users and targeted moderation groups - such as a group which reports people for kitten murder, or one for being Russian spies.  
This way, we can make moderation of a platform much more decentralized.  
Secondly, we make reputation something to value. To be able to participate in a group, you must first contribute positively through smaller groups or know people who are in the group already.  
While a platform has a single way to verify humans with no information, reputation groups can use existing participation to keep out trolls.  
Universities can give reputation to their students, friends to their friends, and people can follow sources they trust.
Bad behavior becomes easier to weed out by giving groups and individuals of whom to trust.
Censorship becomes harder because an organization would have to wield their influence and trust to do so, not their physical strength.
And we can move this beyond one platform. Platforms can track the reputation of users across platforms and discourage raiding. 
Platforms can combine this with the previous methods, removing individuals entirely from the platform manually but letting such a system filter out the hordes of trolls.  
#### Problems 
 - This heavily pushes people into boxes. While one can optimistically say people will follow "neutral" sources, this kind of moderation will push people into echo-chambers. One solution would be to favor content around ~0.5 reputation and taper off from there. But even that likely wouldn't be enough. Platforms and Governments can remove troublesome users but this makes censorship much easier.
 - Privacy: This would be difficult to implement in a privacy-friendly way. It ties everyone to an identifier with easy to follow links to their friends.
 - Power: Unlike platforms, I have no control of a platform. Unlike the government, I don't have the means to force them to do anything, especially if it hurts their profits.
 - It still leaves all this undesirable content on the internet, even if we can't see it.
#### Prototype
A prototype for this would be a browser extension which can be used to block users from the internet, similar to the [Shinigami Eyes](https://shinigami-eyes.github.io/) extension. 
There would have to be a single server which stores the reputation of everyone and assigns people handles.  
Alternatively, the matrix implementation would make it baked into a forward-thinking platform that protects user's privacy while being decentralized.  


