---
title: "Fair Bets for Blockchain"
date: 2020-11-10
category: analysis
tags: blockchain bets
---

## Summary

Here I share my thoughts on blockchain betting technology, its comparison to bookmaker betting,
overview of currently existing kinds of blockchain bets and their disadvantages.

I also propose a new kind of blockchain bets, aimed to solve described problems.

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

### Kinds of Blockchain Bets

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

This may lead to a situation, that you’ve placed a bet on team A at the beginning of a game,
when nobody believed in it.
But at the end of the game team A gained leadership,
and many more people also placed their bets on team A.
Thus making your part of revenue stake smaller.

**Disadvantage**

<pre>
Does this betting scheme favors betters which place bets earlier, at the beginning of a match, on their favorite team?
- No
</pre>

In pool bets the best strategy is to place one big bet towards the end of a match,
when it becomes clear to you which team is leading.
Also putting a lot of money increases your chance to get major part a winning stake.

A naive better will soon realize that placing bets on his favorite team
at the beginning of a match - is a bad strategy,
and over time he may switch to the strategy, described above.

If many betters follow this best strategy then winning pool will be almost empty,
because towards the end of a match nobody will place bet on a team which is likely to lose.

Of course, when the teams are almost equal,
the leadership during the match shifts from one team to another several times.
This makes it difficult to assess which team is more likely to win. 

But of 
Therefore, over time, interest in this type of bets will **fade away**.  

#### Peer-to-peer Bets

The purest form of peer-to-peer betting.
One player opens the bet and defines the odds and another player matches the bet.
This means that you may specify exact odds that you like.

This also means that you may fail to find another player to match your bet!
Some platforms offer solution to this problem by establishing “Houses”,
which can provide liquidity for some fixed fee.

> Example:
> There will be a game between team A and team B.
> You don’t know which team has more chances to win, but you like the team A.
> Your probability for the team A to win is 50%.
> Hence, your odds for team A is 2.0, and the same value for team B.
> You place a bet (A: 2.0, B: 2.0) and wait for some other user, who thinks that team B will win, to join your bet.

**Disadvantage**:

#### Multi-peer Bets

If you want to bet for a large amount, you may end up failing to find a peer for your bet.
The solution for this case: your bet can be partially matched by multiple players.
Similar to peer-to-peer bets, the odds are defined by the player who opens the bet.

## Empirical Study

In order to design a better blockchain betting scheme,
we first need to select the evaluation criteria.



## New blockchain betting scheme

Here will be description of proposed `Blockchain Fair Bets`

