![This is me](/img/avatar.png)

# Projects

## Object detection for MapHub

Sometimes developer companies, farmers, or city mayors wants to have bird view photos of their land.
On the other side, there are people which run their flying drones to collect aerial footage
and stitch it into geo tiff.

One team wants to make an easy service for them to meet.

They asked me to construct an object detection model to detect buildings, coconut palms, etc.
on geo tiff files.

## Pet Project - Intraday

Here should be description of a gym compatible environment to train agents for intraday trading
for different assets like stocks or cryptocurrencies.

## Pet Project - Reinforce

Here should be description of a project I recently completed
during my study of reinforcement learning algorithms.

I believe, if you really want to understand some algorithm, **you should write it yourself**.

That is why I implemented several algorithms from scratch and ensured they work as intended:

- Covariance Matrix Adaptation for Evolution Strategy (CMA-ES).
- Deep Q-Network (DQN), with options: Duelling-DQN, ...
- Asynchronous Advantage Actor-Critic (A3C)
- Advantage Actor-Critic (A2C), the synchronized version of A3C, yet with multiple worker threads.
- Proximal Policy Optimization (PPO)

## OCR reader for RTS Munity s.a.

I created a real-time OCR reader of different values of teams and players
on video streams of League of Legends games.

The first challenge was that there are 57 different values,
such as: gold, kills, turrets, minions, health, mana, etc.,
which can be located in different places for different video stream providers.
My code automatically recognizes layout of these values.

The second challenge was to read all these values in real-time.
I carefully constructed CRNN -based model architecture,
to reach an optimal balance between speed and accuracy.

Examples: here will be videos of how real-time recognition works.
