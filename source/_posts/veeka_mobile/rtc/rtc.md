---
title: Agora & BBRTC Debug steps
index_img: >-
  https://rmt.dogedoge.com/fetch/fluid/storage/hello-fluid/cover.png?w=480&fmt=webp
author: Dylan
tags:
  - Agora
  - BBRTC
math: true
mermaid: true
sticky: 100
date: 2023-03-08 18:26:00
---
>Steps to debug agora and bbrtc

## Background
Agora is a paid service of video, voice and live interactive streaming, whereas bbrtc is developed by ola team.
Agora is used in video room whereas bbrtc is used in other room
However, due to the network connection issue in some region including Taiwan, Agora is still the default rtc engine to use in Veeka App.

## How to determine if we have agora/bbrtc issue
Check if the following items are having issues:
- Listen music in room
- Video call and see if other can view the video

## Possible issue
1. Agora/BBRTC app id expired issue
- Currently the app id for both rtc engine is set by Veeka mobile app, although there is api and remote config to replace these app id, none of them are used currently. The developer_options.dart should be the only source of truth when it comes to the app id configuration.


## How to solve
1. Change to different environment and check if the issue persist
2. If it does not exist on the other environment, it is high likely that the app id is expired, find X教授 if it is related to Agora, bbrtc team if it is related to bbrtc
