---
title: Learning Robust Quadrupedal and Bipedal Locomotion on a Quadruped Robot using One Policy
date: 2026-03-03
tags:
  - Reinforcement Learning
  - Quadruped Robot
  - Bipedal Locomotion
  - Quadrupedal Locomotion
---

## Abstract

Locomotion is an essential ability for legged robots to be applied in various conditions. The ability to perform quadrupedal and bipedal locomotion on one robot can bring excellent versatility for legged robots. However, few works have studied learning both quadrupedal and bipedal locomotion using one policy. Using different policies for different locomotion requires switching between polices. The switching process may introduce undesired behaviors during the transition because of distribution shift. In this work, we propose a framework for a quadruped robot to learn quadrupedal and bipedal locomotion in a unified policy via reinforcement learning (RL). Through task-dependent reward designs based on binary task indicators, a policy can learn both kinds of locomotion even they are mutually conflicting. Results show that the quadruped robot can perform robust bipedal and quadrupedal locomotion on complex terrains. Besides, the robot can perform smooth transition within 1 second between two kinds of locomotion even during motion at speeds as high as 1.5 m/s. Our framework outperforms previous methods in terms of training efficiency and still demonstrates comparable terrain traversal performance on stairs and slopes.

## Demo Video

{{< video src="videos/ICARM_video_17M.mp4" controls="yes" >}}

<!--more-->
