---
title: "Supply Chain Security Python"
date: 2021-11-01T11:51:34+01:00
tags: ["Python", "Cybersecurity"]
---

![Cover photo that highlights the theme of the blog post](/img/supply_chain_security_python/cover.jpg)

*TL;DR A new kind of cyber threat has come to light recently: software supply chain attacks. While rare, they have massive impacts, and protecting against them is a rising concern. Because of its variety of use cases, there is no single rule to apply to your python projects to be safe and as always it depends on your context.*

## Introduction

In traditional industries, a supply chain is anything that allows a company to deliver a product to the customer. For example, when you buy a croissant at the bakery, all the ingredients, the packaging, and the transportation are part of the supply chain.

In the software domain, a supply chain is anything that affects your software before its deployment into production. It covers everything from the development phase to the release process including the code you wrote, your dependencies, your build environment, your IDE, your image registry-every component your software interacts with at any point!

![The supply chain concept applied to the Software Industry](/img/supply_chain_security_python/supply_chain.png)

The term “supply chain” has come to light recently because of cyberattacks that had an extensive impact. Among all attacks, Solarwinds may be the most famous. Indeed, the US government, big tech companies like Microsoft and Intel but also hospitals, power companies, financial institutions have been impacted.

Ironically, the root cause is the infection of Solarwinds Orion, a network security monitor. The build system had been compromised and all new releases between March and June 2020 were infected by malware. The result is that all the customers that updated their software during that period were compromised.

Even though the Solarwinds attack has been largely covered by the media, there are dozens of similar attacks that we have never heard of. Fortunately, the Cloud Native Computing Foundation keeps track of all of them in a [public repository](https://github.com/cncf/tag-security/tree/main/supply-chain-security/compromises). You may be surprised by the acceleration of these attacks in the past few years.

Covering everything related to supply chain security is not feasible in a single blog post so we will focus in this article particularly on projects that use Python as a primary language.

## How to manage your dependencies in Python

Even though Python has a “batteries included” philosophy, you often need external libraries you may download from PyPI, the official Package Index and this is at this point you need to be very careful.

The Python ecosystem has already been targeted, in particular through the use of two techniques:

* **Typo-squatting**
* **Dependency confusion**

The first technique affects a command every Python developer has executed at least once throughout his/her career:

```bash
pip install <my package>
```

Hackers publish packages with almost the same name as existing packages hoping you will make a typo and install their package instead of the official package. For example, a package called `python3-dateutil` instead of the official `dateutil` has been [recently detected](https://snyk.io/blog/malicious-packages-found-to-be-typo-squatting-in-pypi/).

The python community is [working hard](https://lwn.net/Articles/834078/) to mitigate the risk but the risk is still high.

The second technique, **dependency confusion**, is more sophisticated than the first one and has to do with how `pip` works under the hood.

This time, this command exposes you to the risk:

```bash
pip install <my package> --extra-index-url <url internal index>
```

When you type this command, here is what happens:

![The process that pip follows when you use the --extra-index-url option](/img/supply_chain_security_python/flow_dependency_confusion.png)

Let’s take an example:

![Silly meme it's not a bug, it's a feature](/img/supply_chain_security_python/example_dependency_confusion.png)

In this example, the package from the malicious hacker will be installed on the machine. Indeed, the higher version number is on the public package index.

You may have understood what can go wrong with this process. Someone with bad intentions can publish packages on a public repository that have the same names as the ones hosted on internal package indexes and tag them with a ridiculously high version number. Moreover, finding relevant package names is not that hard as [demonstrated by this security researcher](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610).

This command could be qualified as “insecure by design”. This attack leverages a feature of the Python package manager and only a few developers are aware of this behavior.

![The process that pip follows illustrated with a simple example](/img/supply_chain_security_python/meme_bug_feature.png)

## How to defend against these supply chain attacks

To defend against typo-squatting attacks, you can use a **lock file**. A [good lock file](https://www.youtube.com/watch?v=VWWgkF-0cDQ) has the following attributes:

* **Version pins**: they make your builds predictable and deterministic.
* **Hashes**: they are a way to verify the integrity of the package.
* **Full dependency graph**: this allows you to also control the dependencies of your dependencies.

The good news is there is a package whose purpose is to create a lock file for you: `pip-tools`. With only a few commands, you can generate a lock file with all the attributes we previously described.

```bash
$ python3 -m venv my-env # create a new virtual environment
$ source my-env/bin/activate # activate it
$ pip install pip-tools==6.3.0 # install the package that will let you properly manage your dependencies
$ echo “sacremoses==0.0.46” >> requirements.in # add the package of your choice in requirements.in
$ pip-compile --generate-hashes # compiles requirements.txt with hashes based on what you put in requirements.in
```

Your requirements.txt file should look like this:

![Example of a requirements.txt file generated with pip-tools](/img/supply_chain_security_python/requirements_pip_tools.png)

Now that you have this file that contains all your dependencies with their associated versions and hashes, you can execute the following command next time you deploy:

```bash
pip install --require-hashes -r requirements.txt
```

Thus, you are sure that the packages you use in production have not been altered. Assuming you have been careful when you wrote your `requirements.in` file :eyes:, you can also be confident that you will download the package you really want as everything is automated. No risk of a typo!

This best practice is good to defend against typo-squatting attacks but what about dependency confusion?

If you look at the `pip` documentation, you will see that there are two options that you can use to download packages from an internal repository:

* `--extra-index-url`
* `--index-url`

The documentation says:

![pip install command documentation](/img/supply_chain_security_python/pip_documentation.png)

As you can see, there is a slight difference between the two and it is not obvious at first sight. The difference is that if you specified the `--index-url` option, `pip` would only pull packages from the repo with the URL you provided, and not from public repositories. So, if you want to avoid the behavior we described earlier, use `--index-url` rather than `--extra-index-url` and you will be safe!

Finally, to follow the latest vulnerabilities that are discovered in your dependencies, you can choose to periodically check the [GitHub advisory database](https://github.com/advisories?query=ecosystem%3Apip) or better, leverage tools like [dependabot](https://dependabot.com/) that will automatically submit a pull request on your repo to update a dependency in which a critical vulnerability has been recently identified.

## Summary

In this article, we introduced the concept of supply chain for the software world. We specifically studied how this concept applies to the Python ecosystem. Typo-squatting and dependency confusion have been explained and solutions have been proposed to mitigate the risk to be compromised.

This quick introduction to supply chain security only covered the tip of the iceberg, we did not have the chance to discuss how [build systems](https://about.codecov.io/security-update/) or even your [IDEs](https://snyk.io/blog/vulnerable-visual-studio-code-extensions-marketplace/) can be compromised, but I leave that for another article!

## References and credits

[1] [Is your software supply chain secure?](https://blog.convisoappsec.com/en/is-your-software-supply-chain-secure/)

[2] Icons by [Freepik](https://www.freepik.com/) and [Smashicons](https://www.flaticon.com/authors/smashicons)

[3] Cover photo by [Reproductive Health Supplies Coalition](https://unsplash.com/@rhsupplies?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/supply-chain?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
  