# Projects

## Object detection for MapHub

`Sep 2021 - Oct 2021`

**PyTorch**, **YOLOv5**, **OpenCV**, **Docker**, **Python**, **GeoTIFF**

Sometimes developer companies, farmers, or city mayors want to have a bird's view photos of their land.
On the other side, there are people who can launch their flying drones to collect aerial imagery
to produce GeoTIFF.

One team wants to make a service, so these two can easily find each other and close deals.
They asked me to create an object detection model to detect buildings, coconut palms, etc. in GeoTIFF files. 

I wrote utility to grab image patches from GeoTIFF files and constructed the training dataset. 
Then I used a YOLOv5 project to train the model, as its license allows commercial usage.
I wrote my own code which runs model on multiple patches of source image
and implements non-maximum suppression algorithm to produce the final predictions list.
After that I created script to build a lightweight docker image ready for deployment.

### Challenges

First challenge is that GeoTIFF files are typically very huge.
For example: `40,000 x 50,000` pixels, `RGBA`, with file sizes 1...3 Gb.

Typically, the [GDAL](https://gdal.org/) library is used to work with GeoTIFF,
but it is too huge, and I've met some memory issues when tried to use it.
I found a lightweight [library](https://github.com/KipCrossing/geotiff/),
which is capable of loading some patches from large GeoTIFF files.

Second challenge was that inference code from `YOLOv5` is not capable
of processing large GeoTIFF files by parts.

That is why I created my own code which runs model on multiple patches of source image
and implements non-maximum suppression algorithm to produce the final predictions list.

Third challenge was to build a docker image of some reasonable size.
As, docker images with PyTorch library can grow up to 2.5...3 Gb!

I exported model into [ONNX](https://onnxruntime.ai/) format,
and constructed a lightweight docker image of only 300 Mb.

## Pet Project - Intraday

`Jun 2021 - Sep 2021`

**Gym**, **Numpy**, **Pandas**, **Pyglet**, **Python**, **Binance**

Here should be description of a gym compatible environment to train agents for intraday trading
for different assets like stocks or cryptocurrencies.

## Pet Project - Reinforce

`Feb 2021 - Jun 2021`

**Reinforcement-Learning**, **CMA-ES**, **DQN**, **Duelling-DQN**, **A3C**, **A2C**, **PPO**, **PyTorch**, **Python**

Here should be description of a project I recently completed
during my study of reinforcement learning algorithms.

I believe, if you really want to understand some algorithm, **you should write it yourself**.

That is why I implemented several algorithms from scratch and ensured they work as intended:

- Covariance Matrix Adaptation for Evolution Strategy (CMA-ES).
- Deep Q-Network (DQN), with options: Duelling-DQN, ...
- Asynchronous Advantage Actor-Critic (A3C)
- Advantage Actor-Critic (A2C), the synchronized version of A3C, yet with multiple worker threads.
- Proximal Policy Optimization (PPO)

## Analysis of Blockchain Betting Platforms for RTS Munity s.a.

`Oct 2020 - Nov 2020`

RTS Munity is an e-sports betting and trading provider.
They asked me to analyze 

I performed analysis of about 18 past and present blockchain projects,
specially designed for making bets.

I studied and described types of blockchain bets:

- Pool bets 
- Peer-to-peer bets 
- Multi-peer bets

## OCR reader for RTS Munity s.a.

`June 2020 - Oct 2020`

**PyTorch**, **Tensorflow**, **OpenCV**, **Python**, **AWS**

RTS Munity is an e-sports betting and trading provider.
There are many online tournaments held every day,
and there are a lot of people watching them online and making their bets.
RTS Munity analyzes the gameplay and gives the chances (probabilities)
of winning a particular team in real time. 

I created a real-time OCR reader of different values of teams and players
on video streams of [**League of Legends**](https://www.leagueoflegends.com/) game.

### Challenges

The first challenge was that there are 57 different values,
such as: gold, kills, turrets, minions, health, mana, etc.,
which can be located in different places for different video stream providers.

I created the algorithm which can automatically recognize layout of these values.
It takes about 0.5...2 secs to recognize new layout.

The second challenge was to read all these values in real-time.
On possible solution is to utilize server with GPU card.
But this would have increased costs.

Instead, I carefully constructed a lightweight CRNN-based model architecture,
to reach an optimal balance between speed and accuracy, which runs fast enough on CPU.

<video width="100%" controls>
    <source src="/assets/ocr_lol_rts_munity.1.mp4">
</video>

<details>
<summary>View some other examples of how real-time recognition works</summary>

<video width="100%" controls>
    <source src="/assets/ocr_lol_rts_munity.2.mp4">
</video>

<video width="100%" controls>
    <source src="/assets/ocr_lol_rts_munity.3.mp4">
</video>

<video width="100%" controls>
    <source src="/assets/ocr_lol_rts_munity.4.mp4">
</video>

<video width="100%" controls>
    <source src="/assets/ocr_lol_rts_munity.5.mp4">
</video>

</details>

## OCR reader for RTS Munity s.a.

**R-language**

RTS Munity is an e-sport odds and trading provider.

I implemented a bundle of small models for predictions of different match outcomes
for bets on e-sports games.
Predictions were made based on some preliminary data available.

### Challenge

The challenge for me was the necessity to use the **R-language**,
which I had no experience earlier.

I learned new language and created a complete R-package with unit-tests and documentation.

