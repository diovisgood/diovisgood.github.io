---
date: 2020-11-10
title: "Fair Bets for Blockchain"
excerpt: "First I disclose some problems of existing blockchain betting schemes. Then I propose a new kind of blockchain bets, aimed to solve those problems."
category: analysis
tags: blockchain bets game-theory
---

## Summary

Here I share my thoughts on blockchain betting technology, its comparison to bookmaker betting,
overview of currently existing schemes of blockchain bets and their disadvantages.

I also propose a new kind of blockchain bets, aimed to solve some problems.

## Introduction

When two friends make a bet, they don’t need a bookmaker to count results and pay the revenue.
But when many unfamiliar people want to make bets the problems arise:
 
- How to collect money for bets and later distribute revenues?
- How to solve trust issues, as you don’t know what bets other people have made,
  and you may not believe your revenue is calculated correctly?

Typically, a **bookmaker** – a third party – is called to solve both problems.
People make bets and give a bookmaker their money;
it computes results and distributes incomes, taking only a small percent for his work.

However, according to the *Game Theory*, a bookmaker would have a desire to cheat.
Indeed, it can earn more money if it decides to compute revenue *incorrectly*.
Simply because its clients don’t have all the information required to check its computation.
Shortly – the more money a gamer loses – the more money bookmaker wins.
That is why the problem of trust remains.

**Blockchain** technology was invented to solve both problems,
thought it was aimed initially for another target – for cryptocurrency transfers.
In general, Blockchain allows many people which are unfamiliar and don’t trust each other
to safely utilize a common public database of some records.

Features of Blockchain make it ideally suited for betting and solve both problems at once.
Now any person can see all the bets of other persons, and revenues are computed automatically,
so nobody can cheat.

### Different Schemes of Blockchain Bets

However, betting in Blockchain is different from bookmaker’s betting.
Currently, there are following kinds of bets possible:

- Pool bets
- Peer-to-peer bets
- Multi-peer bets

#### Pool Bets

Players bet on their desired outcomes and all stakes go into a single pool.
Winners share the pool.
The odds are dynamic and depend on the number of participants and the amounts they wagered.

This means you do not know what odds will be when you place a bet.
To increase your part of stake you need to place a greater amount in pool.

This may lead to a situation, that you’ve placed a bet on *team A* at the beginning of a game,
when nobody believed in it.
But at the end of the game *team A* gained leadership,
and many more people also placed their bets on *team A*.
Thus making your part of revenue stake smaller.

#### Peer-to-peer Bets

The purest form of peer-to-peer betting.
One player opens the bet and defines the odds and the size he wants for the bet,
and another player matches the bet.

This also means that you may fail to find another player to match your bet!
Some platforms offer solution to this problem by establishing “Houses”,
which can provide liquidity for some fixed fee.

> Example:
> There will be a game between team A and team B.
> You don’t know which team has more chances to win, but you like the team A.
> Your probability for the team A to win is 50%.
> Hence, your odds for team A is 2.0, and the same value for team B.
> You place a bet (A: 2.0, B: 2.0) and wait for some other user, who thinks that team B will win, to join your bet.

#### Multi-peer Bets

If you want to bet for a large amount, you may end up failing to find a peer for your bet.
The solution for this case: your bet can be partially matched by multiple players.
Similar to peer-to-peer bets, the odds are defined by the player who opens the bet.

## Empirical Study

### Establishing criteria

In order to design a better blockchain betting scheme,
we first need to select the evaluation criteria.

I believe that a good betting scheme:
- makes it easy and quick to place a bet.
- provides for a fair distribution of winnings.

Let's try to find some criteria for *easiness* and *fairness*.

#### What kind of betting player you are?

A beginner or an experienced one.
These two kinds of players may have different expectation of *easiness* of placing bets.

#### Does player have to specify odds manually?

When you want to make a bet do you need to specify odds?
Or you can simply bet on *team A* or *team B*? 

I believe, that beginners prefer to make simple bets.
Whereas more experienced players may prefer to specify odds manually,
as this way they can precisely manage their risk.

#### Can player freely choose the amount to bet?

Of course, a good betting scheme is one, where **you can freely choose the amount to bet**.
So you can manage your risk.

But this condition can contradict the previous condition, where you can specify odds manually.

#### Does player have to wait or look for another player to place a bet? 

The quicker you can make a bet - the better the technology is.
I believe, in a good betting scheme **you do NOT have to wait or look for another player to join your bet**.

But this condition depends on two previous conditions:
can you choose the odds and the size of the bet.

#### How obvious or uncertain leadership in match influences player behavior

First we should separate experience a player gets betting on different matches:

- When one team is stronger than other, and soon after the start of the match it gains leadership.
  These matches become not interesting, as soon as you recognize the leader.
  But, of course, surprises are still possible, albeit rare.
- When competing teams are almost equal, and leadership during the match shifts from one team to another several times.
  These matches are the most interesting, because until the end of match, no one knows which team will win.

I believe, in a *fair* betting scheme
**when you bet on an obvious loser, and it suddenly wins - you should get more revenue**.

#### How does time when player makes a bet affect his revenue?

Next we should distinguish when the player made a bet:

- before the match or shortly after the start
- during the match
- almost the end of the match

**This is important:** The earlier you place a bet - the less information you have to choose a team for the bet.
Conversely, the closer to the end of the match you place your bet,
the more confident you are in the most likely winner. 
{: .notice}

I believe, in a *fair* betting scheme
**the earlier you make a bet - the more revenue you should get**.

#### Table of Criteria

| Criteria | Value | Good for beginners? | Good for matures? |
| :---- | :---: | :---: | :---: |
| Can player specify odds manually? | Yes/No | Yes/No | Yes/No |
| Can player freely choose the amount to bet? | Yes/No | Yes/No | Yes/No |
| You do NOT have to wait or look for another player? | Yes/No | Yes/No | Yes/No |
| Do you get more revenue if you bet on obvious loser, and it suddenly wins? | Yes/No | Yes/No | Yes/No |
| Do you get more revenue if place your bet earlier? | Yes/No | Yes/No | Yes/No |
| **Results:** | # of Yes | # of Yes | # of Yes |

Now that we specified the criteria, we can evaluate existing blockchain betting schemes.

### Evaluating existing schemes

#### Pool bets

In pool bets the best strategy is to place one big bet towards the end of a match,
when it becomes clear which team is leading.
Also putting a lot of money increases your chance to get major part a winning stake.

A naive better will soon realize that placing bets on his favorite team
at the beginning of a match - is a bad strategy,
and over time he may switch to the strategy, described above.

If many betters follow this best strategy then winning pool will be almost empty,
because towards the end of a match nobody will place bet on a team which is likely to lose.

| Criteria | Value | Good for beginners? | Good for matures? |
| :---- | :---: | :---: | :---: |
| Can player specify odds manually? | No | Yes | No |
| Can player freely choose the amount to bet? | Yes | Yes | Yes |
| You do NOT have to wait or look for another player? | Yes | Yes | Yes |
| Do you get more revenue if you bet on obvious loser, and it suddenly wins? | Yes | Yes | Yes |
| Do you get more revenue if place your bet earlier? | No | No | No |
| **Results:** | 3 | 4 | 3 |

This betting scheme has its advantages for beginner players.
But I believe, over time, interest in this kind of bets will **fade away**.  

#### Peer-to-peer Bets

| Criteria | Value | Good for beginners? | Good for matures? |
| :---- | :---: | :---: | :---: |
| Can player specify odds manually? | Yes | No | Yes |
| Can player freely choose the amount to bet? | Yes | Yes | Yes |
| You do NOT have to wait or look for another player? | No | No | No |
| Do you get more revenue if you bet on obvious loser, and it suddenly wins? | Yes | Yes | Yes |
| Do you get more revenue if place your bet earlier? | No | No | No |
| **Results:** | 3 | 2 | 3 |

The main disadvantage of this betting scheme is the fact
that player needs to search or wait for other player to place a bet.

Also, you can, of course, freely choose the odds and the amount to bet.
But in fact you may fail to find a peer player who will agree to accept your numbers.

#### Multi-peer Bets

| Criteria | Value | Good for beginners? | Good for matures? |
| :---- | :---: | :---: | :---: |
| Can player specify odds manually? | Yes | No | Yes |
| Can player freely choose the amount to bet? | Yes | Yes | Yes |
| You do NOT have to wait or look for another player? | No | No | No |
| Do you get more revenue if you bet on obvious loser, and it suddenly wins? | Yes | Yes | Yes |
| Do you get more revenue if place your bet earlier? | No | No | No |
| **Results:** | 3 | 2 | 3 |

The main disadvantage of this betting scheme is the same as with previous,
that player needs to search or wait for other player to place a bet.

In this scheme you may also freely choose the odds and the amount to bet,
but fail to find a peer player who will agree to accept your numbers.
Nevertheless, here you have more chances to make a bet than in a previous scheme.

## New Proposed Blockchain Betting Scheme

### Definition

Probably, there could not be a betting scheme suitable for both beginners and matures.
In fact, **Multi-peer Bets**, which is an evolution of **Peer-to-peer Bets**,
seems to be the best scheme for mature players.

Instead, I would like to focus attention on beginner players.
Of all betting schemes **Pool bets** gain the biggest score for beginner players.
But we need to change it so that player will get more revenue if he placed a bet earlier.

This could be easily achieved if we change the algorithm of computing the revenue as follows:

**Each player, whose bet is won, receives a part of the winning pie
from the amounts of those players who made a bet AFTER him and lost.** 

Next this scheme is described in details.

### Input data

Let's study proposed scheme on some synthetic example.
Imagine a group of people make pool bets on either *teamA* or *teamB*.

The input data for proposed blockchain betting scheme is the list of bets.
Note, that the order in which bets are placed is important!

<pre>
09:55 Ezra bets on teamB, 50$.
10:00 John bets on teamA, 20$.
10:05 Nika bets on teamB, 10$.
10:10 Jade bets on teamB, 10$.
10:15 Liam bets on teamA, 20$.
10:20 Noah bets on teamA, 30$.
10:25 Owen bets on teamB, 100$.
10:30 Luke bets on teamB, 20$.
10:35 Jack bets on teamA, 50$.
10:40 Levi bets on teamA, 100$.
10:45 Ryan bets on teamB, 70$.
10:50 Jose bets on teamB, 20$.
10:55 Adam bets on teamA, 20$.
</pre>

Total sum of bets for *teamA* is: 240$.
Total sum of bets for *teamB* is: 280$.

### Distribution Coefficients

Imagine: *teamA* wins the match.
It means that John, Liam, Noah, Jack, Levi and Adam win, and others lose.
Now let's compute the **coefficients of revenue** for each winner, starting from the end:

1. Adam gets **nothing**, since no player placed bet on *teamB* after him.

2. Levi shares the winning pie with John, Liam, Noah and Jack - those,
   who placed bets on *teamA* before him.

   For Levi the winning pie is formed from amounts of Ryan and Jose.
   Levi's part of a pie is computed as: ``100$ / (20$ + 20$ + 30$ + 50$ + 100$) = 0.454``.

   We keep the following coefficients: ``Rian -> Levi: 0.454`` and ``Jose -> Levi: 0.454``.

3. Jack shares the winning pie with John, Liam and Noah - those,
   who placed bets on *teamA* before him.
 
   The winning pie is formed from amounts of Ryan and Jose.
   Jack's part of a pie is computed as: ``50$ / (20$ + 20$ + 30$ + 50$) = 0.417``.

   We keep the following coefficients: ``Rian -> Jack: 0.417`` and ``Jose -> Jack: 0.417``.

4. Noah shares the winning pie with John and Liam - those,
   who placed bets on *teamA* before him.

   The winning pie is formed from amounts of Owen, Luke, Ryan and Jose.
   Noah's part of a pie is computed as: ``30$ / (20$ + 20$ + 30$) = 0.429``.

   We keep the following coefficients:
   ``Owen -> Noah: 0.429``, ``Luke -> Noah: 0.429``, ``Rian -> Noah: 0.429`` and ``Jose -> Noah: 0.429``.

5. Liam shares the winning pie with John - the one, who placed bets on *teamA* before him.

   The winning pie is formed from amounts of Owen, Luke, Ryan and Jose.
   Liam's part of a pie is computed as: ``20$ / (20$ + 20$) = 0.5``.

   We keep the following coefficients:
  ``Owen -> Liam: 0.5``, ``Luke -> Liam: 0.5``, ``Rian -> Liam: 0.5`` and ``Jose -> Liam: 0.5``.
   
6. John 'does not' share the winning pie, because no one placed bets on *teamA* before him.

   The winning pie is formed from amounts of Nika, Jade, Owen, Luke, Ryan and Jose.

   John's part of a pie is computed as: ``20$ / 20$ = 1``.

   We keep the following coefficients:
   ``Nika -> John: 1``, ``Jade -> John: 1``, ``Owen -> John: 1``,
   ``Luke -> John: 1``, ``Rian -> John: 1`` and ``Jose -> John: 1``.

Now that we have computed **coefficients of revenue** we can write them in the table form:

|        |Losers:       |  Ezra |  Nika |  Jade |  Owen |  Luke |  Ryan |  Jose | Revenue |
| ------ | :---:        | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---:   |
|**Winners:**|**Amount**| 50$   | 10$   | 10$   | 100$  | 20$   | 70$   | 20$   |**280$** |
|**John**| 20$          | 0.0   | 1.0   | 1.0   | 1.0   |  1.0  | 1.0   | 1.0   |         |
|**Liam**| 20$          | 0.0   | 0.0   | 0.0   | 0.5   | 0.5   | 0.5   | 0.5   |         |
|**Noah**| 30$          | 0.0   | 0.0   | 0.0   | 0.429 | 0.429 | 0.429 | 0.429 |         |
|**Jack**| 50$          | 0.0   | 0.0   | 0.0   | 0.0   | 0.0   | 0.417 | 0.417 |         |
|**Levi**| 100$         | 0.0   | 0.0   | 0.0   | 0.0   | 0.0   | 0.454 | 0.454 |         |
|**Adam**| 20$          | 0.0   | 0.0   | 0.0   | 0.0   | 0.0   | 0.0   | 0.0   |         |
|**SUM** |**240$**      |**0.0**|**1.0**|**1.0**|**1.929**|**1.929**|**2.8**|**2.8**|     |

The rows correspond to winner players, and the columns - to losers.

Note, that Adam has all zeroes in his row.
It means, he will receive nothing.

Also note that Ezra column is all zeroes.
This is because there is no bet on *teamA* before Ezra.
There are several ways to manage her money:
- we can return it back to Ezra
- we can share it among all winners in proportion to the size of their bet.

Let's choose the second option and compute coefficients for spreading Ezra's money:

|        |Losers:       |  Ezra |  Nika |  Jade |  Owen |  Luke |  Ryan |  Jose | Revenue |
| ------ | :---:        | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---:   |
|**Winners:**|**Amount**| 50$   | 10$   | 10$   | 100$  | 20$   | 70$   | 20$   |**280$** |
|**John**| 20$          | 0.083 | 1.0   | 1.0   | 1.0   |  1.0  | 1.0   | 1.0   |         |
|**Liam**| 20$          | 0.083 | 0.0   | 0.0   | 0.5   | 0.5   | 0.5   | 0.5   |         |
|**Noah**| 30$          | 0.125 | 0.0   | 0.0   | 0.429 | 0.429 | 0.429 | 0.429 |         |
|**Jack**| 50$          | 0.208 | 0.0   | 0.0   | 0.0   | 0.0   | 0.417 | 0.417 |         |
|**Levi**| 100$         | 0.417 | 0.0   | 0.0   | 0.0   | 0.0   | 0.454 | 0.454 |         |
|**Adam**| 20$          | 0.083 | 0.0   | 0.0   | 0.0   | 0.0   | 0.0   | 0.0   |         |
|**SUM** |**240$**      |**1.0**|**1.0**|**1.0**|**1.929**|**1.929**|**2.8**|**2.8**|     |

Note, that Adam now has non-zero coefficient, so he will also receive some revenue from Ezra.

### Coefficients Normalization 

Now we need to normalize each column, so that the sum of the coefficients does not exceed 1.0.
After all, the total amount of revenue cannot exceed the amount of bets of the losers.

There are many ways to normalize coefficients.
We will examine two of them: **division by sum** and **softmax**.

#### Normalization by Dividing by Sum

The simplest method is to divide each coefficient in a column by the sum of coefficients in this column.
If we apply this method for our example, we get:

|        |Losers:       |  Ezra |  Nika |  Jade |  Owen |  Luke |  Ryan |  Jose | Revenue   |
| ------ |     :---:    | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---:     |
|**Winners:**|**Amount**| 50$   | 10$   | 10$   | 100$  | 20$   | 70$   | 20$   |**280$**   |
|**John**| 20$          | 0.083 | 1.0   | 1.0   | 0.518 | 0.518 | 0.357 | 0.357 |**118.46$**|
|**Liam**| 20$          | 0.083 | 0.0   | 0.0   | 0.259 | 0.259 | 0.179 | 0.179 |**51.36$** |
|**Noah**| 30$          | 0.125 | 0.0   | 0.0   | 0.223 | 0.223 | 0.153 | 0.153 |**46.78$** |
|**Jack**| 50$          | 0.208 | 0.0   | 0.0   | 0.0   | 0.0   | 0.148 | 0.148 |**23.74$** |
|**Levi**| 100$         | 0.417 | 0.0   | 0.0   | 0.0   | 0.0   | 0.163 | 0.163 |**35.50$** |
|**Adam**| 20$          | 0.083 | 0.0   | 0.0   | 0.0   | 0.0   | 0.0   | 0.0   |**4.17$**  |
|**SUM** |**240$**      |**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**280$**   |

For example, here is how the revenue is computed for John:

``0.083*50 + 1*10 + 1*10 + 0.518*100 + 0.518*20 + 0.357*70 + 0.357*20 = 118.46$`` 

> Note: in this article I do not include the sum player put in a bet into the revenue.
> It is assumed, that if bet wins, the player automatically receives back the amount of his bet.
> And the revenue comes additionally.

**With this normalization method, John receives too much of total revenue!**

#### Softmax Normalization

I believe, it would be better to use the [softmax](https://en.wikipedia.org/wiki/Softmax_function)
function, or any of its variations.

For softmax we first need to compute the: ``Exp(k * coefficient)`` for each coefficient in the table.
The meaning of additional multiplier `k` will be explained later. For now set ``k=1``.

Next we should divide each value by the sum of values of the column.

For example: the coefficients vector for distributing the Ryan's money is:
``[1.000, 0.500, 0.429, 0.417, 0.454, 0.000]``

After applying **softmax** to it, we get:
``[0.272, 0.165, 0.154, 0.152, 0.158, 0.100]``

The whole table after applying softmax looks like this:

|        |Losers:       |  Ezra |  Nika |  Jade |  Owen |  Luke |  Ryan |  Jose | Revenue   |
| ------ |     :---:    | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---:     |
|**Winners:**|**Amount**| 50$   | 10$   | 10$   | 100$  | 20$   | 70$   | 20$   |**280$**   |
|**John**| 20$          | 0.083 | 0.352 | 0.352 | 0.305 | 0.305 | 0.272 | 0.272 |**72.33$** |
|**Liam**| 20$          | 0.083 | 0.130 | 0.130 | 0.185 | 0.185 | 0.165 | 0.165 |**43.83$** |
|**Noah**| 30$          | 0.125 | 0.130 | 0.130 | 0.173 | 0.173 | 0.154 | 0.154 |**43.37$** |
|**Jack**| 50$          | 0.208 | 0.130 | 0.130 | 0.112 | 0.112 | 0.152 | 0.152 |**40.15$** |
|**Levi**| 100$         | 0.417 | 0.130 | 0.130 | 0.112 | 0.112 | 0.158 | 0.158 |**51.08$** |
|**Adam**| 20$          | 0.083 | 0.130 | 0.130 | 0.112 | 0.112 | 0.100 | 0.100 |**29.24$** |
|**SUM** |**240$**      |**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**280$**   |

Advantages:
- New coefficients are distributed more *evenly*.
- John's revenue is lesser in comparison with previous normalization method: **72$ < 118.46$**.
- Zero coefficients of Adam become nonzero. Adam receives more revenue: **29.24$ > 4.17$**.
- Still we achieve our goal, and those who place bets earlier receive more revenue.

#### Adjustable Softmax Normalization

If we change the value of additional multiplier `k`, we can adjust distribution of revenues,
making it *sharper* (John receives more), or *smoother* (Adam receives more).

For example, let's see how the distribution of revenue changes if we set ``k=0.5``.
The resulting table then becomes as follows:

|        |Losers:       |  Ezra |  Nika |  Jade |  Owen |  Luke |  Ryan |  Jose | Revenue   |
| ------ |     :---:    | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---:     |
|**Winners:**|**Amount**| 50$   | 10$   | 10$   | 100$  | 20$   | 70$   | 20$   |**280$**   |
|**John**| 20$          | 0.083 | 0.248 | 0.248 | 0.230 | 0.230 | 0.215 | 0.215 |**56.09$** |
|**Liam**| 20$          | 0.083 | 0.150 | 0.150 | 0.179 | 0.179 | 0.168 | 0.168 |**43.75$** |
|**Noah**| 30$          | 0.125 | 0.150 | 0.150 | 0.173 | 0.173 | 0.162 | 0.162 |**44.56$** |
|**Jack**| 50$          | 0.208 | 0.150 | 0.150 | 0.139 | 0.139 | 0.161 | 0.161 |**44.63$** |
|**Levi**| 100$         | 0.417 | 0.150 | 0.150 | 0.139 | 0.139 | 0.164 | 0.164 |**55.32$** |
|**Adam**| 20$          | 0.083 | 0.150 | 0.150 | 0.139 | 0.139 | 0.131 | 0.131 |**36.66$** |
|**SUM** |**240$**      |**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**280$**   |

Note: by changing `k=0.5` we made distribution *smoother*.
John now receives even less, while Adam gets more.

**This adjustment seems reasonable, though, the exact formula of how to choose the value of `k`
should be studied additionally.**

### Comparison with Pool Bets

Let's compare results with original **Pool Bets** scheme.
The table of coefficients for Pool Bets is very simple:

|        |Losers:       |  Ezra |  Nika |  Jade |  Owen |  Luke |  Ryan |  Jose | Revenue |
| ------ | :---:        | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---:   |
|**Winners:**|**Amount**| 50$   | 10$   | 10$   | 100$  | 20$   | 70$   | 20$   |**280$** |
|**John**| 20$          | 0.083 | 0.083 | 0.083 | 0.083 | 0.083 | 0.083 | 0.083 |**23.33$**|
|**Liam**| 20$          | 0.083 | 0.083 | 0.083 | 0.083 | 0.083 | 0.083 | 0.083 |**23.33$**|
|**Noah**| 30$          | 0.125 | 0.125 | 0.125 | 0.125 | 0.125 | 0.125 | 0.125 |**35.00$**|
|**Jack**| 50$          | 0.208 | 0.208 | 0.208 | 0.208 | 0.208 | 0.208 | 0.208 |**58.33$**|
|**Levi**| 100$         | 0.417 | 0.417 | 0.417 | 0.417 | 0.417 | 0.417 | 0.417 |**116.67$**|
|**Adam**| 20$          | 0.083 | 0.083 | 0.083 | 0.083 | 0.083 | 0.083 | 0.083 |**23.33$**|
|**SUM** |**240$**      |**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**1.0**|**280$**  |

Notice, how much revenue receives Levi: **116.67$**.
Imagine that *teamA* showed clear leadership during the match.
And Levy decided to make a big bet, taking most of the total revenue. 

Meanwhile, in the proposed betting scheme, Levi's revenue is only **51.08$ .. 55.32$**
(depending on the `k` value).

## Conclusion

In this article I proposed the idea of new blockchain betting scheme,
which I called: **Blockchain Fair Bets**.

It is an evolution of a **Pool Bets** scheme, which solves at least one problem:
players do not get more revenue even when place their bets earlier.

The proposed scheme solves this problem by introducing
new algorithm for computing revenue distributing coefficients.
This algorithm provides that players get more revenue when place their bet earlier.

Also proposed scheme has built-in mechanism to adjust the *smoothness* of revenue distribution.

If we evaluate proposed Blockchain Fair Bets according to the selected criteria, we get the following result:

| Criteria | Value | Good for beginners? | Good for matures? |
| :---- | :---: | :---: | :---: |
| Can player specify odds manually? | No | Yes | No |
| Can player freely choose the amount to bet? | Yes | Yes | Yes |
| You do NOT have to wait or look for another player? | Yes | Yes | Yes |
| Do you get more revenue if you bet on obvious loser, and it suddenly wins? | Yes | Yes | Yes |
| Do you get more revenue if place your bet earlier? | Yes | Yes | Yes |
| **Results:** | 4 | 5 | 4 |

Blockchain Fair Bets is mostly suited for beginner players.

**Please, consider this as an idea, which needs more research!**

It would be great, though, if somebody could build a blockchain contract for this idea.
