![This is me](/img/avatar.png)

# Projects

## Object detection for MapHub

**PyTorch**, **YOLOv5**, **OpenCV**, **Docker**, **Python**, **GeoTIFF**

Sometimes developer companies, farmers, or city mayors want to have a bird's view photos of their land.
On the other side, there are people who can launch their flying drones to collect aerial imagery
to produce GeoTIFF.

One team wants to make a service, so they can easily find each other and close deals.

They asked me to create an object detection model to detect buildings, coconut trees, etc. in GeoTIFF files. 

### Challenges

First challenge is that GeoTIFF files are typically very huge.
For example: `40,000 x 50,000` pixels, `RGBA`, with file sizes 1...3 Gb.

I found a lightweight [library](https://github.com/KipCrossing/geotiff/),
which is capable of loading some patches from large GeoTIFF files.

Second challenge was to build a docker image of some reasonable size.
As, docker images with PyTorch library can grow up to 2.5...3 Gb!

I exported model into [ONNX](https://onnxruntime.ai/) format,
and constructed a lightweight docker image of only 300 Mb.

## Pet Project - Intraday

**Gym**, **Numpy**, **Pandas**, **Pyglet**, **Python**, **Binance**

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

**PyTorch**, **Tensorflow**, **OpenCV**, **Python**, **AWS**

RTS Munity is an e-sport odds and trading provider.

I created a real-time OCR reader of different values of teams and players
on video streams of [**League of Legends**](https://www.leagueoflegends.com/) game.

### Challenges

The first challenge was that there are 57 different values,
such as: gold, kills, turrets, minions, health, mana, etc.,
which can be located in different places for different video stream providers.
My code automatically recognizes layout of these values.

The second challenge was to read all these values in real-time.
On possible solution is to utilize server with GPU card.
But this would have increased costs.

Instead, I carefully constructed a lightweight CRNN-based model architecture,
to reach an optimal balance between speed and accuracy, which runs fast enough on CPU.

<details>
<summary>Examples: here are some examples of how real-time recognition works.</summary>

![video1](/img/ocr_lol_rts_munity.1.avi)

![video2](/img/ocr_lol_rts_munity.2.avi)

![video3](/img/ocr_lol_rts_munity.3.avi)

![video4](/img/ocr_lol_rts_munity.4.avi)

![video5](/img/ocr_lol_rts_munity.5.avi)
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

