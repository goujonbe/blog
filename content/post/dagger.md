---
title: "I wrote my first CI pipeline with dagger"
author: "Benoît Goujon"
date: 2022-06-01T07:54:21+02:00
tags: ["DevOps", "rust", "CI/CD"]
---

![dagger logo](/img/dagger/dagger-logo.png)

*Disclaimer #1: the aim of this article is to provide constructive and objective criticism. I don't want to undervalue the work of the contributors. I would not be able to do a hundredth of what they did. I highly respect their commitment to this project.*

*Disclaimer #2: I chose to illustrate this article with an example. As a dagger newbie, I'm pretty sure there is room for improvement. But it's working and the purpose is to introduce the concepts through an example. Optimization will come later.*

A few weeks ago, dagger, a company founded by the creators of Docker, announced they raised $20M to speed up the development of their product. Their mission: **simplify the app deployment experience**. With such a tagline, they had my attention!

So what is Dagger?

Dagger brings a new way to create CI/CD pipelines. It provides the following benefits:

- **unify dev and CI environments**. With Dagger, you can run your pipelines locally!
- **reduce CI lock-in**. The code stays the same whether you are running your CI/CD pipelines with GitHub Actions or GitLab CI or any other CI runner.

With the introduction of a set of reusable packages, the aim is also to favor the developer's velocity.

If you don't know Dagger yet, I got you covered. I will start with a presentation of a real-world use case. Thus, you will be armed for a review of the tool.

At the end of this article, you will hopefully know a bit more about dagger and get a sense of where the project stands at the moment.

## Testing Dagger on a simple use case

I like getting my hands dirty when I test a new tool. My use case is simple: **run tests on a Rust project with GitHub Actions**.

Once the environment is set up, the process is almost the same for all projects:

1. define your actions and add them to your plan. Actions are the building blocks of your pipeline.
2. make sure your actions are discoverable with the CLI.
3. execute your actions locally.
4. deploy to your remote CI runner.

In my case, there wasn't any packages for rust, neither built-in nor from the community. So, I had to use the docker package to set up a reproducible environment and run my test suite.

To configure the actions, dagger leverages a language called **CUE**. My configuration looks like this:

{{< gist goujonbe d8a835045d6cb6624699989f70367570 >}}

I can now run my actions.

```shell
dagger do test
```

All tests pass. I can now deploy to GitHub Actions. The team at dagger kindly created a GitHub action we can reuse, which makes the transition very smooth.

My config file is simple.

{{< gist goujonbe ed9a530ce7cbb0165d5bd2ce2adb32b5 >}}

And that's it! I have a pipeline that executes my tests as soon as I push a new change.

Now it works, time to take a step back and take a critical look at dagger.

## What I really like

### CUE, a supercharged configuration language

First thing I love about dagger: **CUE**! It has been a fantastic discovery. I didn't know this language before but I immediately fell in love with it. This is a great design choice the team made.

![Cuelang logo](/img/dagger/cuelang-logo.png)

CUE is a **configuration language**. See it as an alternative to YAML and JSON. It is actually a superset of JSON.

The following built-in features particularly caught my interest:

- **package management**: you can reuse boilerplate code easily with a system of packages
- **type checking**
- **schema enforcement**: you can define a schema and validate your data against it. Your data can even be a YAML file or a JSON file!
- **a built-in dev toolchain**: you can download the `cue` binary that will allow you to verify your schema and format your files for instance

There's a lot more to say about CUE but I need to hold back my enthusiasm as it is not the topic of the day. 😇

### DAG auto-generation and caching

I found the dependency management between dagger actions well done. It builds a **Directed Acyclic Graph (DAG)** without having you explicitly define the order in which dagger should run the actions.

In my example, when I run `dagger do test`, it also runs the `deps` action because of the `input: deps.output` parameter. dagger detects a dependency and will execute the actions in the right order.

![DAG with two tasks: deps and test](/img/dagger/dag-dagger.png)

At first sight, you may think a CUE file is very similar to a Makefile. But the implicit task dependency management is a key difference between the two.

The other difference is the caching system. dagger stores the artifacts in a cache. Therefore, you don't need to run the whole pipeline if there's only a small change in your code.

### Re-usable packages from the universe

dagger offers a limited set of core actions. But you can rely on a set of packages that contain more actions. This set of packages is called the universe.

Thus, you can create your own actions using a mix of core actions and actions from external packages.

Although the number is for now quite limited, it will scale well once the community will contribute.

## What kept me skeptical

The more you work with dagger, the more you see its potential. However, dagger still is a nascent project and as such, there's a lot of work to be done.

### The developer experience is not perfect yet

As a dagger newbie, I read the official documentation first. Honestly, the onboarding wasn't smooth. Some code snippets didn't work. The content was not very well organized. For example, the documentation contains contributing guides alongside user guides. Furthermore, packages from the universe are not documented at all, so you need to go to the code (fortunately it is open source 😅) to get the info you need.

The maintainers are aware of the problem because there is a technical writer open position. The community also wrote a couple of GitHub issues.

**Documentation is hard**. This is a full-time job. Keeping it up-to-date as things change rapidly is a huge challenge. So, congrats to the team for doing their best! I wish I had time to contribute to help them enhance the onboarding process.

Besides the lack of documentation, I struggled a bit with the **developer interface**, especially the CLI and the standard to define actions with CUE. The terminology is sometimes confusing. The difference between a project and a plan is not clear. Some parts of the configuration file are counter-intuitive like the client section.

The CLI design could be revamped. Here is what you get when you run the help command.

![CLI output dagger command](/img/dagger/dagger-command.png)

You have verbs like `do` and nouns like `project`. But when you run `dagger project`, subcommands are verbs. I don't know the reasons behind those choices but I dream of a better interface.

I took a bit of time to navigate through the open issues on GitHub and I have discovered they are thinking a lot about the interface. We are still at the beginning of the project and this is the best moment to make structural changes.

### A lot of CI runners and languages are not supported yet

Of course, it's the beginning of the project and they had to prioritize work. They did it openly, so I wasn't surprised. But for my day-to-day job, I need more packages to avoid reinventing the wheel. The good thing is that I can vote on GitHub for the next CI runners and the next packages to develop! 📨

Also, as it is open-source, I can contribute!

## Conclusion

Testing dagger was on my to-do list for too long. I really had fun playing with it!

The product is in **public beta**, so I'm not surprised by the amount of work that remains. I **wouldn't use dagger in production right now**, but I will definitely check in a few months to see the evolution.

I see a real benefit as a developer working for a consulting firm. Indeed, we often switch between projects that don't have the same CI/CD stack. The promise to create a layer of abstraction on top of existing CI runners is therefore interesting. We could define our own actions and leverage them on our projects independently of CI runners.

Finally, this project shows **how difficult it is to build successful open-source software**. It is a technical challenge but also a human challenge. Everyone has an opinion on the direction the project should take (myself included) and maintainers must decide. I wish them the best!

## References

- [Introducing Dagger: a new way to create CI/CD pipelines](https://dagger.io/blog/public-launch-announcement)
- [Dagger official documentation](https://docs.dagger.io/)
- [Dagger for GitHub repo](https://github.com/dagger/dagger-for-github)
- [Dagger official repo](https://github.com/dagger/dagger)
- [list of universe package](https://github.com/dagger/dagger/tree/main/pkg/universe.dagger.io)
