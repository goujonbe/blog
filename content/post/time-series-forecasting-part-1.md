---
title: "Time series forecasting series, part 1: introduction"
layout: single
date: 2019-06-01 14:34:59 +0800
tags: ["Data science"]
---

Forecasting has fasinated people for thousands of years because it is about prediciting the future. It sounds magical but it is not. There are metods to do so and this is the aim of this series: **showing the different techniques and present real-world use cases**.

There are many applications of those techniques in various fields such as politics, finance, healthcare, energy and many others. This series will be very practical with code examples and real-world data. Code examples can be accessed [here](https://github.com/goujonbe/time_series_examples).

Throughout this series we will see different time series, more and more complex, and we will try to forecast the next points as accurately as possible.

Ok, let's dive in!

## Time series definition

Time series is a number of **successive observations collected over time**. More precisely, we define a **variable** of interest and we observe its behaviour. This behaviour has to be a **quantifiable** value.

## A real-world example

For instance, a good use case of time series forecasting can be a study of the trends in the fashion industry. Imagine an entrepreneur who would like to create its startup with the idea to sell swimsuits whose color change when you get into water (yeah, that's a hell of an idea :joy:). Before launching its business, he or she studies the trends of the market and there is a powerful tool to do that: [Google trends](https://trends.google.com/trends/).

The graph below shows how trending is the topic of swimsuits during the last 5 years.

![Swimsuit trends](/img/ts_series_part_1/swimsuits_trends.png)

Similarly, we can plot other trends like a comparison of one-piece swimsuits versus bikini.

In this case, forecasting can help **make decisions** about which type of swimsuit to sell (one-piece or bikini? Which one is trendy?). It can also help **schedule the production and personnel needs** (looks like backup will be needed before the summer).

However, it is not an easy task, forecasting is hard. It requires statistical expertise and data skills. So, a data scientist able to forecast as accurately as possible the future is a main asset for a company. 

## Time series forecasting methodology

Before diving into the techniques, you need to ask yourself the good questions and frame the problem correctly.

1. Do you already have data? If yes, what kind of data? How many sources? It is crucial because there are techniques that rely on the time series itself and others that can combine multiple sources to enhance the prediction. Sometimes, the data is not available yet, so you need to find relevant data and collect them.
2. What is your forecasting horizon? Short-term? Medium-term? Or long-term?
3. How frequently are forecasts required? If the answer is "very frequently", you may need to automate your system. Is is not possible for every technique. Otherwise, you can choose a method that requires careful manual work.
4. What level of accuracy is expected? This is important because there are methods that require a little effort and are quite good but if you want to use your forecast for critical decisions like in finance, it may be worth to spend more time.
5. Are your data regularly spaced? In this series, we will focus on time series that are observed at regular intervals of time because it is easier but irregularly spaced time series can also occur but this is way more complicated :sweat:.

Answering each question of this checklist is half the job done. Indeed, there is no method that is good for every time series. So, if you precisely define what you expect from the model, you will surely pick the good one thanks to a quick benchmark of the capabilities of each technique! 

## Techniques to forecast time series

We will suppose in this series that you have **information about the past** available and that we will find **past patterns** in the future too. This latter is a strong assumption and we will see why later. The simple methods we will see only rely on the **patterns discovered in the past observations** to forecast. Therefore, they ignore all **external factors**. For instance, external factors such as financial crises, natural disasters, geopolitical conflicts or marketing campaigns can have a huge impact on our time series but they are not taken into account by the model.

Both statistical and machine learning methods will be tackled. We will use in particular the following techniques in the next chapters of this series:

* **Autoregressive** models
* **Moving average** models
* **ARIMA** models
* **SARIMA** models
* **Additive** models
* **LSTM neural networks**

That's it for today! Stay tuned for the next chapter! We will talk about **preliminary exploratory analysis**.

I hope you found this content interesting, we will get our hands on in the next chapter I promise :smile:.
