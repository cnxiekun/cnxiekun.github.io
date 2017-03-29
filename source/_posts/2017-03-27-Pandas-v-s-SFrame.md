---
title: Pandas v.s. SFrame
date: 2017-03-27 23:59:38
categories: Technique
tags: [Python, Pandas, SFrame]
description:
---

Which one is better for data manipulation in python: Pandas or SFrame?

## Introduction:

- Pandas is an independent Python package (Pandas stands for Python Data Analysis)
- SFrames (short for Scalable Frames) are part of the bigger ecosystem of Graphlab Create

## Licensing and Fees:

- You can use Pandas in commercial applications without any fee
- You need to buy a license to use Graphlab Create SFrames for commercial use. SFrame is open source now.

<!--more-->

## *Scalability*:

- Pandas is an in-memory data structure. This means you can usually not store data frames bigger than the main memory (aka RAM) on your machine
- SFrame is an out-of-core data structure. This means you can virtually store any size dataframe as long as you do not run out of both disk space and memory
- SFrame must be able to handle large amounts of data compared to Pandas, but must be slower in performance compared to Pandas.
-  SFrame is for solid-state hard-drives. You can scale with speed. - Pandas is if you want to work only with RAM. You can use SFrame with normal hard-drives as well but speed would be very low.

## Library Dependencies:

- Pandas does not need any other package to store data. You can not do much data modelling using Pandas, you will need scikit learn or other packages from the Anaconda Python Distribution
- SFrame is closely coupled with Graphlab Create and hence, you will not need to setup or install anything if you are using Graphlab Create. It is self sufficient for most tasks

## Language and Machine Dependencies:

- Pandas, to the best of my knowledge, works in both 32 bit and 64 bit machines
- SFrame works only in 64 bit machines.
- Pandas works with both Python 2.x and 3.x
- SFrame works with only Python 2.7

Owing to licensing fees and some other less important reasons, most users have not tried Graphlab Create. Thereby, we do not appreciate the immense power from the Graphlab Create python stack.

What should you learn?

If you are a beginner, start with Pandas and the Anaconda python distribution (which includes scikit learn, numpy, scipy, matplotlib, flask etc.). I recommend Pandas because there are much more tutorials and StackOverflow answers available in comparison.

But please do keep in mind, that just because most brilliant people have not tried Graphlab Create does not make it a bad tool. Use the tool that works for you the best.