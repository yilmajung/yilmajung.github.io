---
title: 'Will "They" also click on the same ad?'
subtitle: 'Detecting potential ad-audiences using a lookalike modeling'
date: 2022-08-11 00:00:00
featured_image: '/images/project/yulia-matvienko-kgz9vsP5JCU-unsplash.jpg'
---

![](/images/project/yulia-matvienko-kgz9vsP5JCU-unsplash.jpg){:width="60%"}

*Source: Unsplash*

I designed and conducted this standalone project during my internship at **The Washington Post** (Summer 2022).

### Project Background & Purpose

Online news platforms provide a meeting place where they match ads and audiences to promote advertisers’ products or services. There are three main stakeholders in this process: 
- Audiences: react differently to online ads according to their personal interests, disposition, access location and time, a device they use, etc. 
- Advertisers: seek to show ads to users who are valuable to their marketing campaigns
- News platform: a service provider 

Although the service provider collects audiences’ clickstream information about which ads the user has clicked on, it is difficult to predict whether or not the users will click on a certain ad in the future. This is not a simple clicking-or-not-clicking problem, but more like a clicking-or-unlabeled problem since we do not know if the negative (non-clicking) cases are true negative. Actually they could be either positive or negative.

In this project, I designed a lookalike modeling study (1) to address the positive-or-unlabeled case effectively, (2) to more accurately detect potential audiences who are likely to click on a specific ad from the unlabeled audiences, and (3) to expand advertisers’ audience base and increase campaign reach.
One strong assumption underlying the lookalike modeling is that potential audiences are possibly ad-receptive users who have the similar identified traits to the existing members who already clicked on the ad.


### Lookalike Modeling
Lookalike modeling is commonly used to identify new potential users and expand audience base. The basic idea is pretty simple: given a seed set $S$ from a universal set $U$, find groups of audiences from $U-S$ who look and act like the audiences in $S$. Lookalike modeling can be categorized into three different methodological approaches: rule-based, similarity-based, and model-based.

![](/images/project/journal_wj_images.png){:width="70%"}

