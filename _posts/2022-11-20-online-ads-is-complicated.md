---
date: 2022-11-20
title: "Introduction to Online Ads Industry"
excerpt: "Having completed a ML project in online ads, I obtained some basic knowledge of how this industry works and where it is moving now. Here you can read some recapitulation of my experience in the form of an introduction."
category: analysis
tags: ads
---

## Introduction

Some time ago I have completed an interesting [project]({% link _portfolio/indata-webpages-semantic-analysis.md %})
in the online ads industry.
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
You can change it to: "a user launches a game on a smartphone" -
the mechanics for displaying an advertisement is the same.

> Disclaimer: the mechanics for YouTube advertisement is different.

It often happens so, that a website owner may decide to monetize his website traffic.
Especially when content there is useful and website is popular.

To do this, the website owner enters into a deal with some online advertising platform and becomes a **Publisher**.
The platform is called - **Supply-Side Platform (SSP)**, because it provides: "places to show ads".

Back to our user. First, a browser loads the webpage - a HTML document.
Then it starts to load all the other content, such as: scripts, fonts, images.

One of the parts of a webpage is a special placeholder for an ad - a frame,
which is to be loaded from the SSP.
That is why at this point the browser connects to the SSP and asks it for the frame.

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

Often this is performed with the help of another party: the **Data Management Platform (DMP)**.
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

For obvious reason, this auction lasts just a fraction of a second (100...200ms).
It is called: **Real-Time Bidding (RTB)**. 
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

### Recognizing User and its Interests

An important thing in the process described above is the ability of
parties to recognize a user and its interests.
Without this Advertisers would waste their budget showing irrelevant advertisement to some random users.
Typically, the Data Management Platform (DMP) is doing this.

Recognizing a user can be difficult because of the following reasons:
- Internet providers often pass user's request through a NAT gateway.
  This allows to use a single IP for multiple users.
  Which is good for providers which experience the lack of IPv4 addresses nowadays.
- A user can access Internet through multiple devices:
  PC, mobile phone, tablet, home assistant, multimedia in car, etc.
- Family members with completely different interests can access Internet through the same devices.

![multiple users share the same IP](/assets/img/online-ads-6.png)

Recognizing users interests is even harder.
Imagine, you were browsing Internet and spent some time reading an article about a new car model.
Does this mean you are interested in this product?
Should a car selling company spend their budget showing you their advertisement?

Yet, a lot of companies try to do this. Here are some examples:
- When you search for some goods or services your search engine keeps that in mind.
- When you speak near your smartphone or home assistant they are eager to hear some keywords
  of products or services you might be interested in.
- When you watch video on a streaming platform like YouTube or TikTok,
  they all pay attention to what videos you watched and liked.
- When you read some webpages about goods or services,
  trackers on these websites save this information for the latter usage.

Another problem is that this information about a user is being collected by competing parties,
which do not want to share it with an arbitrary Advertiser for free:
- Google (Search Engine, YouTube, Chrome, Android, Assistant, ...) knows a lot about your interests.
  An Advertiser can use it only if it pays to Google Ads.
- Facebook knows a lot about you. As an Advertiser you can use it, but only on the Facebook.
- Apple knows a lot about you. Of course, it does not share this information with others.
- etc.

No single platform has all the information about a user and its interests.

> An Advertiser often has to run multiple campaigns on different platforms,
> as they all provide some different audience targeting services.
> This is not very efficient for the Advertiser's budget,
> as a single user can receive the same advertisement
> multiple times through different channels.


### Third-Party Cookies as the Foundation for Online Ads

The solution to these problems is the [**Third-Party Cookies**](https://en.wikipedia.org/wiki/HTTP_cookie){:target="_blank"}.
Following is just a short description of how they work.

Many webpages often contain some small scripts: **Trackers**.
When a user loads such webpage, this script saves the information about a date and time of visit to a certain webpage
in a browser's local storage.

Later, when the user opens another webpage, and this webpage wants to show some advertisement to this user,
this collected information is being sent to the SSP, which can now identify the user and its interests.

This scheme has been working for decades. But now the situation is changing...

## The Ongoing Change in the Industry

### Third-Party Cookies are Being Forbidden

In August 2019 Google announced the
["privacy sandbox"](https://www.blog.google/products/chrome/building-a-more-private-web){:target="_blank"} initiative,
which was about to restrict third-party cookies.
This announcement was made due to the trend for privacy,
earlier supported by Apple Safari [in 2020](https://www.theverge.com/2020/3/24/21192830/apple-safari-intelligent-tracking-privacy-full-third-party-cookie-blocking){:target="_blank"}
and [Mozilla Firefox](https://support.mozilla.org/en-US/kb/third-party-cookies-firefox-tracking-protection?redirectslug=disable-third-party-cookies&redirectlocale=en-US){:target="_blank"}.
Yet, Google Chrome occupies the major stake of the browser market, that is why its actions are more important,
than those of its rivals.

As a substitute Google offered: **Federated Learning of Cohorts (FLoC)**.
Let me quote from a [source](https://devops.com/google-floc-is-dead-meta-ai-supercomputer-lives-arm-deal-is-dead/){:target="_blank"}: 

> FLoC lets advertisers use behavioral targeting without cookies.
> It runs in Google’s Chrome browser and tracks a user’s online behavior.
> Then, it assigns that browser history an identifier and adds it to a group
> of other browsers with similar behaviors called a “cohort.”
> Supposedly, advertisers would be able to see the behaviors that people in
> a cohort share without being able to identify individuals within that cohort,
> because each person’s browser is given an anonymized ID.

But in January 2022 Google abandoned FLoC and proposed another idea: **Topics**.
Quote from an [article](https://devops.com/google-floc-is-dead-meta-ai-supercomputer-lives-arm-deal-is-dead/){:target="_blank"}:

> Your browser will learn about your interests as you move around the web.
> … When you hit upon a site that supports the Topics API for ad purposes,
> the browser will share three topics you are interested in.
> … The site can then share this with its advertising partners to decide which ads to show you.
> … Users will be able to review and remove topics from their lists [or] turn off the entire Topics API.
> … FLoC was doing unsupervised clustering of users, whereas Topics allocates users into predetermined clusters.
> This makes it potentially more transparent and also seems designed
> to work around the “protected categories” objection.

Yet, on July 27, 2022, Google [postponed](https://blog.google/products/chrome/update-testing-privacy-sandbox-web/){:target="_blank"}
the restriction of third-party cookies.

On May 18, 2023, Google [announced](https://privacysandbox.com/news/the-next-stages-of-privacy-sandbox-general-availability){:target="_blank"}
it will start "experiments to deprecate third-party cookies for one percent of Chrome users in Q1 of 2024".

*Stay tuned* and keep the track of events here: [www.privacysandbox.com](https://www.privacysandbox.com/intl/en_us/){:target="_blank"}

Despite the long history of third-party cookies and its importance for online ads,
I believe, this functionality will be prohibited in Google Chrome sooner or later.

### What is the Future of Online Ads Industry?

For now, I see the following possible outcomes:
- probabilistic identifiers prove their efficiency and are massively adopted by industry,
- parties concur and create some industry standard of how to store and share information about a user,
- the worst scenario: a few monopolies are sharing the whole market, which drives the prices up. 

#### Probabilistic identifiers

An example: [id5](https://wiki.id5.io/){:target="_blank"}.

They try to identify a particular user by analysing some sparce available information:
- IP address,
- browser/device fingerprint,
- login information, if provided by a website (not all websites require login),
- etc.

Probabilistic identifiers assign some long unique identifier to each user. Example:

```ID5*9L-LURfnuiHBtUH21KR1sE4PESzdsavUEHaDx-oPW5oc4tAFJtNcehD92RkenqN2```

They claim they can recognize this user even when he is using another device or connects from another network.
But from my own experience of processing a large amounts of data,
this is not always true.

#### Common Industry Standard

This is the preferred scenario, when all parties in industry come to an agreement on how to
collect, store and share information about a user and its interests.

Probably, a browser is the best place to store such information.
Yet it must give a user the right to control this function.

#### Monopolization

This is the worst scenario, when the whole market is owned by large companies like:
Google, Apple, Facebook, Microsoft, etc.

This will surely lead to the increase of costs and decrease of quality for a regular Advertiser.

## Conclusion

I believe, the industry will adapt to changes and find a solution of how
to let advertisement find a way to those people which may be interested in it.
Because we all will benefit from it!
