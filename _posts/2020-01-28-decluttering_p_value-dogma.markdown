---
layout: post
title: Decluttering P-value Dogma
date: 2020-01-28 10:14:45 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Statistics, p-value]
---
<p>Understandably, our focus is on statistics. Prior to jumping the gun, let us be confident about where we are coming from. The statistics evolved as a discipline to capture the notion of a population, that is rather “next to impossible” to pursue. Imagine yourself being tasked to visit your state of residency and document age, gender, height, weight of the individuals. As crazy as it may sound, you would take years to pull this information, not to mention also any inconceivable errors, and table it.</p>
<p>On the flipside, imagine if you can consider having a sample (from the population) that has fair representation of your state: diverse ethnicity, balanced in terms of age and sex (having people from different age groups of “all” sexes). This will make your life a lot easier. This will be your sample for the state population and even if it is not perfect, you’re still having a reference. This sample will, for some terms, be an enactment for your population and will imbibe same virtues (well, largely) as compared to some random sample coming from a different state; probably, the language and culture.</p>  
<p>Actually, let’s make it more fun with the following example. Hypothesize six folks hanging out together. Now, contrary to some outsider claiming to sample three individuals from the population (six here), let’s have a setting where any three of these people are voluntarily getting sifted in the four rounds conducted.</p>

![Problem Statement](/assets/img/declut_p1.png)

<p>As illustrated above, we have the following counts associated with the draws. The lawyer seems to be befitting in several scenarios and is getting maximum selections, followed by the plumber, doctor, chef, baseball player, and cleaner.</p> 

![Cardinatity](/assets/img/declut_p2.png)

<p>This also demonstrates the ordering where the selection with greater count shall possess greater certitude, and hence lower p-value. This also means that the entities with lower p-value have something “innately” associated with the “black-box” selection mechanism, and their selection is not random.</p>

![Finally](/assets/img/declut_p3.png)