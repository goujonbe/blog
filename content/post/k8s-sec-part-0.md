---
title: "K8s security - part 0"
date: 2020-02-16T16:51:34+01:00
draft: true
---

## Prerequisite

You already know Kubernetes architecture, its components and have notions of cybersecurity.

## Abstract

In this introduction of a series devoted to Kubernetes security, we will first see that Kubernetes, although very popular and used by thousands of companies is very hard to completely protect from attacks espescially if you create and operate your own cluster. Vulnerabilities have been discovered in the past and sometimes exploited by attackers. We will explore the reasons that make Kubernetes hard to secure by default and propose a model that represents the layers that need to be secured. Finally, we will report a couple of projects initiated by the CNCF to make the life of cluster administrators more peaceful.

## Introduction

