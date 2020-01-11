---
title:  "Learning Go, first impressions"
date: 2019-12-28T13:06:49+01:00
draft: true
---

Over the past couple of weeks, I have been interested in a new language called Go. I have been developing mostly in Java and Python for 3 years now and I was keen to learn a new language. As I was looking for a new language to learn, Go caught my attention. Indeed, this language created by Googlers in 2007 has a lot of traction these days, espescially with the rise of cloud-native apps  and projects like [Kubernetes](https://kubernetes.io/) or [CockroachDB](https://www.cockroachlabs.com/) that are essentially developed in Go. Moreover, Go seems to be popular within the developer community according to the [lastest StackOverflow survey](https://insights.stackoverflow.com/survey/2019) and my colleagues are eulogistic when it comes to compare Go to other languages so "Let's Go!", I said.

My goal in this article is to provide you objective (and less objective...)  information about Go's features, its adadvantages and drawbacks. I would also like to share links to resources I have found particularly useful through my journey and I will conclude this article by giving you my humble opinion on what has amazed me and what I have liked the least.

![Gopher mascot by Renee French](/img/go_first_impressions/gopher.png)

## Creation and adoption

Go was orginally designed at Google by 3 Googlers: [Robert Griesemer](https://github.com/griesemer), [Rob Pike](https://github.com/robpike) and [Ken Thompson](https://github.com/ken). The aim was to increase their productivity by creating a new language suitable for the nascent era of multicore machines and distributed systems.

They imagined a language with the following characteristics:

* highly efficient (similar to C/C++)
* [simple and easy-to-read](https://www.youtube.com/watch?v=cQ7STILAS0M) (like Python)
* appropriate for networking and multiprocessing

Since Google open-sourced Go in 2009, its adoption kept increasing. Nowadays, [major tech companies are using Go](https://github.com/golang/go/wiki/GoUsers) for multiple reasons and they are worth a detailed explanation.

<figure>
  <img src="/img/go_first_impressions/go_users.png" alt="Go users"/>
  <figcaption>Companies that extensively use Go.</figcaption>
</figure>

## Why Go is so popular 
