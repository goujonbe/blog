---
title: "K8s security - part 0"
date: 2020-02-16T16:51:34+01:00
draft: true
---

## Prerequisite

You already know Kubernetes architecture, its components and have notions of cybersecurity.

## Abstract

*In this introduction of a series devoted to Kubernetes security, we will first see that Kubernetes, although very popular and used by thousands of companies, is very hard to completely protect from attacks espescially if you create and operate your own cluster. Vulnerabilities have been discovered in the past and sometimes exploited by attackers. We will explore the reasons that make Kubernetes hard to secure by default and propose a model that represents the layers that need to be secured. Finally, we will report a couple of projects initiated by the CNCF to make the life of cluster administrators more peaceful.*

## Introduction

Have you ever heard about Tesla cyberattack? This is [one of the most famous cyberattacks on a Kubernetes cluster](https://redlock.io/blog/cryptojacking-tesla). The attackers found a breach through the default administration console that was not password protected and exposed on the Internet. Thank to this interface, they got access to credentials and sensitive data (telemetry data from autonomous cars). They used credentials to install a malware in order to mine cryptocurrencies. The attack was really sophisticated and was still in progress when security researchers discover what was going on.

This attack is not an isolated case. Lots of companies suffered from similar attacks before Tesla. However, a couple of companies were lucky enough to discover vulnerabilities before attackers. For instance, [Shopify](https://www.youtube.com/watch?v=2XCm7vveU5A), thanks to a bug bounty program prevented its whole Kubernetes cluster from being torn down.

And I don't want to bother you with attacks that are purely due to container vulnerabilities. If you are interested in container security check out [heartbleed](https://heartbleed.com/) or the recent report on [vulnerabilities in DockerHub images](https://blog.banyansecurity.io/blog/over-30-of-official-images-in-docker-hub-contain-high-priority-security-vulnerabilities).

So why is it so hard to secure a cluster even with the help of public cloud providers?

## The 4C's of cloud native security

