---
title:  "Learning Go, first impressions"
date: 2019-12-28T13:06:49+01:00
draft: true
---

![Gopher mascot by Renee French](/img/go_first_impressions/gopher.png)

Over the past couple of weeks, I have been interested in a new language called Go. I have been developing mostly in Java and Python for 3 years now and I was keen to learn a new language. As I was looking for a new language to learn, Go caught my attention. Indeed, this language created by Googlers in 2007 has a lot of traction these days, espescially with the rise of cloud-native apps  and projects like [Kubernetes](https://kubernetes.io/) or [CockroachDB](https://www.cockroachlabs.com/) that are essentially developed in Go. Moreover, Go seems to be popular within the developer community according to the [latest StackOverflow survey](https://insights.stackoverflow.com/survey/2019) and for my colleagues who are eulogistic about Go.

My goal in this article is to provide you unbiased information about Go's features, its adadvantages and drawbacks. I would also like to share links to resources I have found particularly useful through my journey and I will conclude this article by giving you my humble opinion on what has amazed me and what I have liked the least.

## Creation and adoption

Go was orginally designed at Google by 3 Googlers: [Robert Griesemer](https://github.com/griesemer), [Rob Pike](https://github.com/robpike) and [Ken Thompson](https://github.com/ken). The aim was to increase their productivity by creating a new language suitable for the nascent era of multicore machines and distributed systems.

They imagined a language with the following characteristics:

* highly efficient (similar to C/C++)
* [simple and easy-to-read](https://www.youtube.com/watch?v=cQ7STILAS0M) (like Python)
* appropriate for networking and multiprocessing

Since Google open-sourced Go in 2009, its adoption kept increasing. Nowadays, [major tech companies are using Go](https://github.com/golang/go/wiki/GoUsers) for multiple reasons and they are worth a detailed explanation.

![Companies that use Go](/img/go_first_impressions/go_users.png)

## Why Go is so popular

### Go performs well while remaining simple

Old languages like Java or C/C++ are good but they were born when [Moore's Law](https://en.wikipedia.org/wiki/Moore%27s_law) was [still valid](https://www.economist.com/technology-quarterly/2016-03-12/after-moores-law). Since a few years now, we entered a new era where we physically can't miniaturize integrated circuits anymore. We now get more compute thanks to multicore hardware. It is the era of distribued compute on a single machine but also on clusters of machines. And in this context, Go offers a solid alternative. Natively concurrent, it also compiles amazingly fast. Legend has even it that it was during the time the Google engineers' program was compiling that they had the idea to create Go.

Performance often comes with more complexity. For example, Rust is extremely performant but it may be harder to learn than Go. Go is simple because:

* There is a garbage collector that manages memory for you.
* The documentation of packages is extremely good, espescially with the brand new [site](https://pkg.go.dev/) which centralizes documentation for a lot of packages.
* It is opinionated. It avoids endless debates because there often is one correct way to do things, thus allowing you to get to the point.
* It does not have too many features. It leaves out many features of object-oriented programming languages like classes, inheritance, constructors but also annotations and generics (well the latter might [change](https://blog.golang.org/why-generics)).

Furthermore, Go's learning journey is very smooth thanks to awesome resources. I will share with you only a few of them trying to diversify their formats.

* Go Time
* TDD
* Gophercises
* A Tour of Go
* Just for func
* Go by example

## You can deploy on almost every platform

## Lots of use cases

* CLI apps (point to my repo)
* Back-end web development (point to my repo)
* Infrastructure tools (Terraform)
