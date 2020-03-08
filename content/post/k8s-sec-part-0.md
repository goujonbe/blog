---
title: "K8s security - part 0 - Security Model"
date: 2020-02-16T16:51:34+01:00
---

## Prerequisite

You already know Kubernetes architecture, its components and have notions of cybersecurity.

## Abstract

*In this introduction of a series devoted to Kubernetes security, we will first see that Kubernetes, although very popular and used by thousands of companies, is very hard to completely protect from attacks espescially if you create and operate your own cluster. Vulnerabilities have been discovered in the past and have sometimes been exploited by attackers. We will explore what makes Kubernetes hard to secure by default and propose a model that represents the layers that need to be secured. Finally, we will report a couple of projects initiated by the CNCF to make the life of cluster administrators more peaceful.*

## Introduction

Have you ever heard about Tesla cyberattack? This is [one of the most famous cyberattacks on a Kubernetes cluster](https://redlock.io/blog/cryptojacking-tesla). The attackers found a breach through the default administration console that was not password protected while being exposed on the Internet. Thank to this interface, they got access to credentials and sensitive data (telemetry data from autonomous cars). They used credentials to install a malware in order to mine cryptocurrencies. The attack was really sophisticated and was still in progress when security researchers discover what was going on.

This attack is not an isolated case. Lots of companies have suffered from similar attacks before Tesla. However, a couple of companies were lucky enough to discover vulnerabilities before attackers. For instance, [Shopify](https://www.youtube.com/watch?v=2XCm7vveU5A) prevented its whole Kubernetes cluster from being torn down thanks to a bug bounty program.

I am not going to bother you any longer with attacks that are purely due to container vulnerabilities. If you are interested in container security check out [heartbleed](https://heartbleed.com/) or the recent report on [vulnerabilities in DockerHub images](https://blog.banyansecurity.io/blog/over-30-of-official-images-in-docker-hub-contain-high-priority-security-vulnerabilities).

So why is it so hard to secure a cluster even with the help of public cloud providers?

## The 4C's of cloud native security

The first answer to this question is generally *"Because there is so many components and we don't know where to start"*. This is illustrated by what we call the 4C's of cloud native security.

![4C security model](/img/k8s_security_part_0/4c_security_model.png)

This model represents pretty well the different layers that can be hardened by an attacker.

* **Code**: every programming language has its vulnerabilities. Think of [buffer overflow](https://owasp.org/www-community/vulnerabilities/Buffer_Overflow) for example. Moreover, think about all the vulnerabilities a developer might introduce in terms of authentication, password storage policy and so on.
* **Container**: technologies like Docker or [Apache Mesos](https://mesos.apache.org/) are regularly collared for being unsecure.
* **Cluster**: Kubernetes is a distributed system that has a large **attack surface** and the bigger the attack surface, the easier it is for an attacker to find a way in.
* **Cloud**: nowadays, every cloud provider offers **managed Kubernetes services**. But configurations are not the same between the main actors and users still have to secure their clusters, in particular their worker nodes.

Each layer deserves a dedicated blog post, so we will come back to them shortly.

This model allows us to understand how hard it can be to secure your applications that are running on Kubernetes because of the number of layers to take into consideration. Furthermore, Kubernetes has for quite a bit of time been **insecure by default** as [Ian Coldwater](https://twitter.com/IanColdwater) and [Duffie Cooley](https://twitter.com/mauilion) pointed out in their talk at Black Hat USA 2019.

{{< youtube HmoVSmTIOxM >}}

This is mainly due to the fact that Kubernetes has been thought by developers for developers in the aim of increasing developer velocity. But security was not in their minds at the beginning and this is why deploying on Kubernetes in the early days of the project was a brave act. The [Cloud Native Computing Fundation](https://www.cncf.io/) has since lauched a bunch of initiatives like [open sourcing security audits](https://www.cncf.io/blog/2019/08/06/open-sourcing-the-kubernetes-security-audit/), a [bug bounty program](https://kubernetes.io/blog/2020/01/14/kubernetes-bug-bounty-announcement/) and published a lot of tutorials to help system administrators secure their clusters.

## Conclusion

So, in the first blog post of this series dedicated to Kubernetes security, we have seen that a lot of companies suffer from cyberattacks on their Kubernetes clusters. The recurrence of these attacks can be explained on the one hand by the number of layers administrators have to secure and on the other hand by the maturity and the nature of the project itself.

## Future work

This first episode was a short and high-level introduction. In the next episodes, we will dive into more details. Stay tuned for the next episode. If you want to get notified once the next episode will be ready, follow me on [twitter](https://twitter.com/benoit_goujon) :blush:.

## References

1. [Cloud native security model](https://kubernetes.io/docs/concepts/security/)
2. [Attacking and defending Kubernetes, with Ian Coldwater](https://kubernetespodcast.com/episode/065-attacking-and-defending-kubernetes/)
