---
title:  "Learning Go, first impressions"
date: 2020-03-19T13:06:49+01:00
---

![Gopher mascot by Renee French](/img/go_first_impressions/gopher.png)

Over the past couple of weeks, I have been interested in Go. I have been developing mostly in Java and Python for 3 years now and I was keen to learn a new language. As I was looking for a new language to learn, Go caught my attention. Indeed, this language created by Googlers in 2007 has a lot of traction, espescially with the rise of cloud-native apps  and projects like [Kubernetes](https://kubernetes.io/) or [CockroachDB](https://www.cockroachlabs.com/) that are essentially developed in Go. Moreover, Go seems to be very popular within the developer community according to the [latest StackOverflow survey](https://insights.stackoverflow.com/survey/2019) and I had to form my own opinion.

My goal in this article is to provide you unbiased information about Go's features, its adadvantages and drawbacks. I would also like to share links to resources I have found particularly useful through my journey and I will conclude this article by giving you my humble opinion on what has amazed me and what I have liked the least.

## Creation and adoption

Go was orginally designed at Google by 3 Googlers: [Robert Griesemer](https://github.com/griesemer), [Rob Pike](https://github.com/robpike) and [Ken Thompson](https://github.com/ken). The aim was to increase their productivity by creating a new language suitable for the nascent era of multicore machines and distributed systems.

Since Google open-sourced Go in 2009, its adoption kept increasing. Nowadays, [major tech companies are using Go](https://github.com/golang/go/wiki/GoUsers).

![Companies that use Go](/img/go_first_impressions/go_users.png)

So why is Go so popular?

## Go performs well while remaining simple

Old languages like Java or C/C++ are good but they were born when [Moore's Law](https://en.wikipedia.org/wiki/Moore%27s_law) was [still valid](https://www.economist.com/technology-quarterly/2016-03-12/after-moores-law). Since a few years now, we entered a new era where we physically can't miniaturize integrated circuits anymore. We now get more compute thanks to multicore hardware. And in this context, Go offers a solid alternative. Natively concurrent, it also compiles amazingly fast.

Performance often comes with more complexity, except for Go that is simple because:

* There is a garbage collector that manages memory for you.

{{< youtube q4HoWwdZUHs >}}

* The documentation of packages is extremely good, espescially with the brand new [site](https://pkg.go.dev/) which centralizes documentation for a lot of packages.
* It is opinionated. It avoids endless debates because there often is one correct way to do things, thus allowing you to get to the point.
* It does not have too many features. It leaves out many features of object-oriented programming languages like classes, inheritance, constructors but also annotations and generics (the latter might [come with Go v2](https://blog.golang.org/why-generics)).

To conclude this paragraph about performance and simplicity, I will try to position Go in the ecosystem of languages given these two criteria in the matrix below.

![Language matrix](/img/go_first_impressions/language_matrix.png)

[Rust](https://www.rust-lang.org/) is trendy these days and we often compare it to Go because they are both supposed to replace C and C++. But as pointed out by Nick Cameron in [his article](https://pingcap.com/blog/early-impressions-of-go-from-a-rust-programmer/), they are really different from each other and we should stop comparing them. Java is widely used. It is is relatively simple and fast but it suffers from JVM's overhead. Python is in my opinion the easiest language to date but as it is not compiled, it has to interpet each line of code at runtime, which makes it inappropriate if you have efficiency requirements.

This is how I came up with this matrix but this does not mean that Go is *better* that every other language. Indeed, I only considered two criteria and this is not enough to evaluate a language. So please haters, stay calm :wink:.

## You can deploy on almost every platform

Cross-platform compilation is to me an underrated advantage of Go. The ability to compile on your Windows laptop and then deploy on a Linux server is just awesome. As you end up with a binary, this is also very easy to distribute your program. For instance, if your program is a command line tool, you can easily make it available through OS-specific package managers like [Homebrew](https://brew.sh/index_fr), [Chocolatey](https://chocolatey.org/) or [Snappy](https://snapcraft.io/). You can even deploy your binary on microcontrollers with [tiny go](https://tinygo.org/).

## It is suitable for lots of use cases

I mainly see three domains where Go is particularly good:

* **CLI apps**: a lot of CLI tools (Hugo, kubectl ...) are built with Go. The fact that a go program is a binary file makes it appropriate for CLI tools.
* **Back-end web development**: Go is used for building microservices or web servers. Its performance and ability to scale thanks to concurrency are graetly appreciated.
* **Infrastructure tools**: Go is a low-level language and is often used for building DevOps tools like [Docker](https://www.docker.com/) or [Terraform](https://www.terraform.io/).

## Summary

To wrap things up, Go is popular and its popularity is still growing up because it is fast, easy to learn and suitable for modern use cases. However, developers also [complain about it](https://bluxte.net/musings/2018/04/10/go-good-bad-ugly/) and this is is why I'm excited to see how the community will solve these well-known issues!

## List of awesome resources to get started with Go

Go's learning journey is very smooth thanks to awesome resources.

* [Go Time](https://changelog.com/gotime) is a weekly podcast that talks about Go and its ecosystem. Always super fun to hear and informative.
* [Learn Go with Test Driven Development](https://github.com/quii/learn-go-with-tests). This format is very innovative and suit intermediate developer's needs.
* [Gophercises](https://gophercises.com/). As the previous one, this is more for developers that already had experience with other languages. It may even be a good refresher for Gophers.
* [A Tour of Go](https://tour.golang.org/welcome/1). A prerequisite for self-proclaimed Gophers.
* [Just for func](https://www.youtube.com/channel/UC_BzFbxG2za3bp5NRRRXJSw). Although Francesc has not published for a bit of time, his work is very educational and stays up to date!
