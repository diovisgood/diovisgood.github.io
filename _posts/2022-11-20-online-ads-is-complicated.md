---
date: 2022-11-20
title: "Introduction to Online Ads Industry"
excerpt: "Having completed a ML project in online ads, I obtained some basic knowledge of how this industry works and where it is moving now. Here you can read some recapitulation of my experience in the form of an introduction."
category: analysis
tags: ads
---

## Introduction

Some time ago I have completed an interesting project in the online ads industry.
My role was: a Data Scientist, then a Team Lead and System Architect.

This was a completely new world for me.
This established industry has some specializations and definitions for each of the parties involved.  
Now it is undergoing a tektonik shift, that may change it dramatically.
But more on that later.

Please treat this essay not as a comprehensive guide,
but rather as some kind of recapitulation of my experience.

## Online Ads Industry

The fact is: advertising is as essential to the economy as lubricant is to your car.
Whether you like it or not.

There are many channels by which advertisement can reach you, but I would like to focus on online ad.
You see these ads on webpages, in games on your smartphone, in YouTube videos, and so on. 

But many people don't even realize what complicated story is behind an advertisement being shown to them!
So lets dive in.

### A User Opens a Webpage...

Imagine, a user opens a webpage in a browser.

It often happens so, that a website owner may decide to monetize his website traffic.
Especially when content there is useful and website is popular.

To do this, the website owner enters into a deal with some online advertising platform and becomes a *Publisher*.
The platform is called - *Supply-Side Platform* (SSP), because it provides: "places to show ads".

Back to our user. First, a browser loads the webpage - a HTML document.
Then it starts to load all the other content, such as: scripts, fonts, images.

One of the parts of a webpage is a special placeholder for an ad - a frame,
which is to be loaded from the SSP.
That is why at this point the browser connects to the SSP and ask it for the frame.

![user opens webpage](/assets/img/online-ads-1.png)

But the SSP does not send advertisement frame back immediately.
Instead, it initiates an auction **for the right to display an advertisement to you this very moment**.

> Each time you load a webpage with an advertisement in it there is an auction being held,
> and some companies compete for the right to show their advertisement to you.
> The winner of this auction not only sends its ad to you,
> but also pays all intermediate parties from his budget for this.

One important note here: 
Before opening an auction, the SSP collects as much information about you,
as possible, taking into account the time limits for an auction.

Often this is performed with the help of another party: the Data Management Platform (DMP).
These are companies, which collect or, sometimes, buy information about you.
This may include:
- your visits to a certain webpages, which have their trackers installed;
- places you visited, by tracking your smartphone with public Wi-Fi networks;
- model of devices you possess: mobile phone, car, tv, ...;
- your purchases with a card;
- etc.

This information may represent you and your interests at the moment.
It is compiled into a packet and sent to the auction.

![ssp starts auction](/assets/img/online-ads-2.png)

For obvious reason, this auction lasts just a fraction of a second.
There are millions of auctions being held in each second.
That is why only the fastest computers can participate in it.
Moreover, as a rule, these computers must be located in the same data center
with the auction servers in order to meet the time frame!

There are not many companies, which have the required infrastructure.
Such companies are called: **Demand-Side Platform (DSP)**.

![dsp had got creatives from advertisers](/assets/img/online-ads-3.png)

DSP represent the interests of those companies,
which need to advertise their goods or services - **Advertisers**.

Typically, when an advertiser initiates an advertisement campaign,
it presents some images or videos for it. These are called: **Creatives**.

Also, advertiser specifies the **Target Audience**.
This is to show ad only to users which meet some specified criteria.
There could be different kinds of criteria:
- user location: continent, region, country, city, etc.;
- user gender criteria;
- user age criteria;
- user income criteria;
- user interests criteria;
- webpage content criteria.

> The interests of a user is the hardest thing to estimate.
> And this is where the most efforts of industry are concentrated.

Another important thing which Advertiser specifies is the overall budget
which will be spent on a campaign.
Advertiser can set a limit for how much money to bid for each display of an advertisement.

Each event when advertisement is displayed to an end user is called: **Impression**.
The more you are ready to pay for each Impression - the faster you spend your budget.

![dsp which won sends creative to ssp](/assets/img/online-ads-4.png)

Once all interested DSPs have submitted their bids to the auction server,
the auction ends and the winner is determined.
Its Creative is then sent back to the end user.

![creative is displayed to the user](/assets/img/online-ads-5.png)

Finally, the advertisement (Creative) is displayed to the user, but the story does not end.
Because user's reaction to this Impression is also being tracked.

For how long have the user been observing an advertisement?
Did the user click it or not?
And if the user clicked it - what did he do on the Advertiser's webpage?

This way the Advertiser may compute the statistics of how his campaign is going.
Advertisers do often correct their campaigns on the fly.

### Tracking as the Foundation for Online Ads

TODO

### The Ongoing Change in the Industry

TODO

### What is the Future of Online Ads Industry?

TODO

## Conclusion

TODO
