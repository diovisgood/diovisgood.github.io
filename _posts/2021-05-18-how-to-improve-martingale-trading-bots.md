---
date: 2021-05-18
title: "How to improve Martingale trading bots"
excerpt: "There are trading bots based on Martingale strategy. I've got an idea of how one can reduce risk of losses when running multiple such bots."
category: idea
tags: martingale trading
---

## Trading Bots

Recently I played with trading bots, which I rented at **MyBotGarage**.
This team offers tradings bots, which can perform trades on your *Binance Futures* account
via an API key, that you provide.

Typically, you rent several *slots* for some period of time, say: a month or a year.
Each *slot* can trade one cryptocurrency pair, which you specify.
For example: **BTC/USDT** or **ATOM/USDT**.

There is a list of nearly 100 (or even more?) so called "shitcoins" which this system supports.
So you can freely choose what you want and run as many bots as you wish.

[Site of MyBotGarage](https://mybotgarage.com/){: .btn .btn--primary target="_blank"}

After running about 7 bots for few days I understood that they use
[Martingale trading strategy](https://en.wikipedia.org/wiki/Martingale_(betting_system)){:target="_blank"}.

## Martingale Trading Strategy

Shortly about this strategy:

Martingale is a cost-averaging strategy.
It does this by “doubling exposure” on losing trades.
This results in lowering of your average entry price.

Imagine the situation:

![](/assets/img/mybotgarage_martingale_strategy.jpg)

1. You make first BUY of 1 asset, say at the price 100$.
   Now your position is 1 asset and the average price of your position is 100$.
2. Unfortunately, the price goes down.
3. When the price drops to 70$, you BUY 2 assets.
   Now your position is 3 assets and the average price is: ``(2*70 + 1*100) / 3 = 80$``
4. But the price continues to go down.
5. When the price is 40$, you BUY 3 assets.
   Now your position is 6 assets and the average price is: ``(3*40 + 3*80) / 6 = 60$``
6. Finally, the price reverses and moves up.
7. When it becomes more than your position price: $60, you can close position with profit.
   For example: you wait for the price to reach 65$, and sell all your 6 assets.
   Then your profit will be: ``6 * (65 - 60) = 30$``

There could be many implementations of this strategy, which may differ in details:

- In the example above we increased position each time the price moved against us by 30$ range.
  But it is possible to use a different range at each next step.
  For example: second BUY could be after 30$, while third BUY - after 40$, fourth BUY - after 50$.
  In fact, you can specify some *exponential formula* to determine the price range for the next trade.
- In the example above we first bought 1, then 2, then 3 assets.
  But, in general, you could use any other formula to choose the amount for each next step.

Martingale trading strategy is based on the idea
that price movement is a [random walk](https://en.wikipedia.org/wiki/Random_walk){: target="_blank"}.
This theory has its supporters and opponents.
More about it [here](https://www.investopedia.com/terms/r/randomwalktheory.asp){: target="_blank"}.

Shortly: if the *Random Walk Prices* theory is **right**,
then the *Efficient Market Theory* is automatically **wrong**.
And vise versa.

### The General Algorithm of Martingale Strategy

The strategy itself is very simple:

1. You enter a position, either LONG or SHORT.
   Actually, in Martingale strategy it does not matter!
   
2. After that price can move up or down, stochastically.

3. If prices moves in your direction - wait until it reaches your target level.
   Then close position and take your profit.

4. If price moves against you - periodically increase your position,
   effectively averaging the position price.
   Eventually, price will move in your direction, and you will get your target profit.

![](/assets/img/mybotgarage_price_random_walks.jpg)

In theory, you should **always get some profit in each trade**,
no matter what direction, LONG or SHORT you have chosen.

What can possibly go wrong?

### Drawbacks of Martingale Strategy

The reality is not so good:

- You may have NOT enough money to make the next step of increasing the size of your position.
  In this case the average price of your position does not change.
  It means, you will have to wait for longer time for the price to come back to your desired level.

- Your account can be liquidated if the uncovered loss of your position exceeds the limit.
  This has meaning if you use marginal trading, i.e. - *futures*.
  By the way, in many countries you can open SHORT positions **only in marginal trading**.
  
- In reality price can not drop below zero. Whilst in the theory of random walk prices,
  there are no restrictions on negative values.
  But a real exchange will simply **delist an asset** if its prices gets too low.

- The real price may not be a random walk process.
  Remember: if the random walk prices theory is right, then the efficient market theory is wrong.
  In fact, there are more evidence, that on the long run **market is close to being efficient**.
  And only at small timescale it appears to be inefficient.

As you see, generating profit with Martingale strategy is not an easy task.

Are there any ways to protect against these losses?

### Tricks to Make it Work

While, you can not fully protect your account from losses or liquidation,
you can try to reduce this risk using some tricks.

1. Use as low leverage as possible. 2x...10x.
2. When opening a new position, start with very small amount.
3. Increase range for each next step, to perform BUY or SELL when averaging your position price.
   E.g.: the second BUY after 30$ movement, the third - after 60$, the fourth - after 120$, etc.
4. Use multiple martingale bots, running simultaneously on different assets.
   If one position is liquidated, you still continue to make money out of other bots.

Do these tricks guarantee you will make profit out of it?
Of course, not.

## Does it Work?

In fact, guys from **MyBotGarage** implemented all of these tricks.
They started their bot farm in autonomous mode,
in order to demonstrate its profitability.
And it gained perfect profits day by day.
Until it was eventually liquidated.

And this scenario repeated 2 or 3 times.
They have [live-streaming](https://www.twitch.tv/mybotgarage){: target="_blank"}
on twitch, so you can check it out.

Note: in most cases they managed to get enough profit and withdraw it from trading account
before the liquidation happened.

Why does liquidation happen periodically?

## Scenario for Liquidation

Like stated before, one of the tricks is to run multiple bots simultaneously on different assets.

But how to choose the direction for each bot?

**MyBotGarage** offered few options for this:

- LONG - bot will always open long positions.
- SHORT - bot will always open short positions.
- SURF - bot will alternate between long and short positions, one after the other.
- RAND - bot will randomly choose between long and short.

In fact, LONG and SHORT positions can be safely used only when the **whole** market is in uptrend or downtrend.

In most other cases SURF or RAND modes are preferable.

Like I said, I played with these bots for several days,
and soon I realized: why periodical liquidation is inevitable in this scheme,
and how to change the scheme to avoid it.

The scenario for liquidation is the following:

1.  Imagine, you run 16 martingale bots, in RANDOM mode.
    It means: each bot will choose its next direction randomly.
    On average, you'll have 8 bots in LONG, and 8 bots in SHORT, all bots are doing fine:
    
    | L | L | L | L | L | L | L | L | S | S | S | S | S | S | S | S |
    |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
    |:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:| 
    
2.  This works just fine until some **important news** appear.
    After it the whole market moves rapidly up or down.
    Suppose, that it moves DOWN.
    
3.  Nearly half of your martingale bots were in LONG positions.
    Now these bots **got stuck**:
    
    | L | L | L | L | L | L | L | L | S | S | S | S | S | S | S | S |
    |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
    |:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:| 
    
4.  Other bots are in SHORT position, and they gained a some good profit,
    as whole market went down!
    
5.  Your SHORT bots close their positions with profit.
    Now they have to randomly choose the direction for the next position.
    About 50% of your remaining bots choose long, the other 50% chooses short again.
    It means that now 12 of your bots are in long, and 4 are in short: 
    
    | L | L | L | L | L | L | L | L | L | L | L | L | S | S | S | S |
    |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
    |:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:|:smile:| 
    
6.  If news were really important the market continues to move downwards.
    It means that all you 12 long bots got stuck, and 4 short bots get good profit:
    
    | L | L | L | L | L | L | L | L | L | L | L | L | S | S | S | S |
    |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
    |:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:smile:|:smile:|:smile:|:smile:| 
    
7.  When the profit of short bots reaches desired target, they close their positions.
    And, again, they need to randomly choose the direction for the next position.
    A half of them will choose long, the other half will choose short.
    
8.  I hope, you grasped the idea.
    Now you got 14 of 16 your bots stuck in the long position,
    and only 2 of bots in short position.
    
    | L | L | L | L | L | L | L | L | L | L | L | L | L | L | S | S |
    |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
    |:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:smile:|:smile:| 
    
9.  After some time ALL your bots get stuck in the long position.
    It means, they will periodically increase their positions,
    by buying more assets, according to the Martingale strategy.
    Thus, reducing the free money on your account to cover the uncovered losses of your positions.
    
    | L | L | L | L | L | L | L | L | L | L | L | L | L | L | L | L |
    |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
    |:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:|:fearful:| 
    
10. Now everything is prepared for the liquidation of your whole account.
    If price of some asset will suddenly drop down -
    the exchange will close all positions and takes all your money to cover the losses!

Does using the SURF mode help to avoid this scenario?

No. In fact, it will happen even faster in the SURF mode.
Because all bots will choose LONG mode immediately after SHORT, and get stuck in a downtrend market.

What if you switch all your bots to the SHORT mode manually?

This is not a good a solution, because:
- You can not switch already opened positions.
  And many of your bots are already stuck in LONG.
- What if you manage to put half of your bots in SHORT mode,
  but market will suddenly reverse? Now you got many bots stuck in SHORT positions.
- This also means that your bot farm is no longer autonomous.
  You have to manually *tune it* all the time.

## The Proposed Solution

The idea of how to break this scenario and reduce the risk is the following:

**When choosing the direction for the next position, a martingale bot must take into account
all currently opened positions of other bots.**

> For example: If more than a half of your bots are in LONG position, then choose SHORT.
> And vice versa.

Another (better) approach is to look NOT at the number of bots in longs or shorts,
but at the **money you have frozen** in SHORT and LONG position.

> For example: You have 3 bots stuck in LONG positions, they have frozen 1200$ for their positions so far.
> Also, you have 10 bots in SHORT positions, they have frozen 500$ for their positions.
> Then choose SHORT!


## Conclusion

I described the Martingale strategy, its drawbacks and tricks to reduce the risk.

Also, I revealed the typical scenario and the reason for inevitable liquidation.

The proposed solution is simple and robust.
It helps to break this scenario and reduce the risk.

Does this guarantee you no longer bear the risk of losses or liquidation?
Of course, not!

Remember, this way of making money is neither safe, nor reliable.

I have sent my idea to the **MyBotGarage** team in their Telegram channel.


> **UPDATE FROM 2021-08-04** 
> 
> *MyBotGarage* team announced that they will soon implement my idea:
> ![](/assets/img/mybotgarage_new_hedge_mode.jpg)
>
> [Link to the announcement in Telegram thread](https://t.me/mybotgarage/2753){: .btn .btn--primary target="_blank"}
>
> This is good news! Maybe, someday I will try martingale trading bots one more time :)
