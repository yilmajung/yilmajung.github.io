---
title: 'Will "They" also click on the same ad?'
subtitle: 'Detecting potential ad-audiences using a lookalike modeling'
date: 2022-08-11 00:00:00
featured_image: '/images/project/yulia-matvienko-kgz9vsP5JCU-unsplash.jpg'
---

![](/images/project/yulia-matvienko-kgz9vsP5JCU-unsplash.jpg){:width="60%"}

*IMG Source: Yulia Matvienko, Unsplash*

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
Lookalike modeling is commonly used to identify new potential users and expand audience base. The basic idea is pretty simple: given a seed set *S* from a universal set $U$, find groups of audiences from *U-S* who look and act like the audiences in *S*. Lookalike modeling can be addressed from the three different methodological approaches: rule-based, similarity-based, and model-based.

![](/images/project/journal_wj_images.png){:width="70%"}


I took a model-based approach, namely PU learning in this project, which goes through the following procedure:

Given a training set containing only positives (*P*) and unknown (*U*) classes:

1. Treating all *U* as negatives (*N*), train a classifier *P* vs. *U*
2. Using the classifier, score the unknown class and isolate the set of ‘reliable’ negatives (*RN*)
3. Train a new classifier on *P* vs. *RN*, use it to score the remaining U, isolate additional *RN* and enlarge *RN*
4. Repeat Step 3 until no new negative cases are classified

Although it sounds quite simple, there are two key issues to be tackled before conducting the PU learning. The first issue is sampling related. That is, what is an ideal probability boundary for reliable negative (RN) cases? And, which sampling technique performs better in terms of efficiency and effectiveness? The second issue is prediction related: which prediction model brings the best results? Depending on the sampling and prediction techniques and their combinations, many different PU learning designs can be devised.


### Research Framework
![](/images/project/lookalike/research_framework.png){:width="70%"}

- Stage 1: Identify seed audiences from the WaPo user data (The seed audiences are ad-receptive users who have once clicked on a specific ad)

- Stage 2: Conduct look-alike modeling on the seed set and find potential audiences



### Data
To make the experiment simple, I used a specific advertisement which has been clicked 294 times out of 30,463 impressions. Therefore, there are 294 positive cases (*S*) and 30,463 unlabeled cases (*U-S*). After collecting the ad-related dataset such as the number of articles read by topic, clicking propensity, advertisement size and position, the number of line item, the number of impressions on a specific user, user device info, and user demographic info, I categorized them into three levels: article-level, ad-level, and user-level. The time gap between the dataset is as below.

![](/images/project/lookalike/timegap.png){:width="70%"}

The first seven days of the whole advertising period were used for training and testing the look-alike modeling, and the remaining period was used for monitoring and evaluation.


### Method
- Sampling: Spy sampling and bootstrapping sampling
- Prediction: Logistic regression and AdaBoost

#### ___Spy Sampling (Liu et al. 2002)___

Input: Positive Sample Set *P*, unlabeled Sample Set *U*

Output: Negative Sample Set *N* with size *k*

1. Randomly select a subset from *P* as the spy set *P'*;
2. Train a classifier *M* based on *P-P'* and *U+P'*;
3. Select a subset *N* of *k* samples from *U* with least prediction scores;
4. Return *N*;

The key idea of the Spy sampling is that the spies behave identically to the unknown positive users in *U*.


#### ___Bootstrap (Boosting) Sampling (Mordelet and Vert 2014, Zhao et al. 2022)___
Input: Positive Sample Set *P*, unlabeled Sample Set *U*

Output: Negative Sample Set *N* with size *k*

1. for $t \leq T$ do 

    Bootstrap a subset $U'$ from $U$;

    Train a classifier $M$ on $P$ and $U'$;

    Predict U-U' using classifier M;

    Record the classifying scores;

2. Average the classifying scores of all iterations;
3. Select a subset N of k samples with least average scores;
4. Return N;


In addition, since the dataset has very small number of positive cases (less than 0.01\%), SMOTE and SMOTE+RUS methods were applied to the training set.

- SMOTE (Synthetic Minority Oversampling Technique): upsampled minority (positive) to make the ratio of positive to unlabeled cases 1 to 1 (Chawla et al. 2002)

- SMOTE + RUS (Random Under Sampler): combined SMOTE with random undersampling of the majority to make the ratio 1 (positive) to 2 (unlabeled). This combined technique is also suggested in Chawla et al (2002). Also check [this online article](https://machinelearningmastery.com/smote-oversampling-for-imbalanced-classification/) for more detailed use cases of both methods.


### Results
![](/images/project/lookalike/results.png){:width="70%"}

The models based on bootstrap sampling show a better performance on test set than the models with spy sampling.