---
title: "OCR reader for RTS Munity s.a."
excerpt: "Real-time OCR reader of different values of teams and players on video streams of League of Legends game"
categories:
  - machine learning
tags:
  - ocr
  - pytorch
  - tensorflow
  - opencv
  - python
  - aws
  - esport
sidebar:
  - title: "Period"
    text: "June 2020 - Oct 2020"
  - title: "Technologies"
    text: "**PyTorch**, **Tensorflow**, **OpenCV**, **Python**, **AWS**"
  - title: "Role"
    text: "Senior Data Scientist"
  - title: "Responsibilities"
    text: "Creating a model for real-time reading"
---

RTS Munity is an e-sports betting and trading provider.
There are many online tournaments held every day,
and there are a lot of people watching them online and making their bets.
RTS Munity analyzes the gameplay and gives the chances (probabilities)
of winning a particular team in real time. 

I created a real-time OCR reader of different values of teams and players
on video streams of [**League of Legends**](https://www.leagueoflegends.com/) game.

## Challenges

The first challenge was that there are 57 different values,
such as: gold, kills, turrets, minions, health, mana, etc.,
which can be located in different places for different video stream providers.

I created the algorithm which can automatically recognize layout of these values.
It takes about 0.5...2 secs to recognize new layout.

The second challenge was to read all these values in real-time.
On possible solution is to utilize server with GPU card.
But this would have increased costs.

Instead, I carefully constructed a lightweight CRNN-based model architecture,
with only ~ 3 million parameters,
to reach an optimal balance between speed and accuracy, which runs fast enough on CPU.

<video width="80%" controls>
    <source src="/assets/video/ocr_lol_rts_munity.2.mp4">
</video>

<details>
<summary>View some other examples of how real-time recognition works</summary>

<video width="80%" controls>
    <source src="/assets/video/ocr_lol_rts_munity.1.mp4">
</video>

<video width="80%" controls>
    <source src="/assets/video/ocr_lol_rts_munity.3.mp4">
</video>

<video width="80%" controls>
    <source src="/assets/video/ocr_lol_rts_munity.4.mp4">
</video>

<video width="80%" controls>
    <source src="/assets/video/ocr_lol_rts_munity.5.mp4">
</video>

</details>
