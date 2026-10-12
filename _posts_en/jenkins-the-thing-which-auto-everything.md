---
title: Jenkins——the thing which auto everything
date: 2019-08-06
author: Tang MoYing
categories: [Jenkins]
tags: [Jenkins]
lang: en
alt_url: /post/jenkins-the-thing-which-auto-everything
---
* TOC
{:toc}

# Jenkins: nothing of its own, yet capable of everything

Jenkins is, in essence, an automation server.

Create a job on Jenkins and configure it, and that job will execute automatically in whatever way you want. Archimedes once said, "Give me a fulcrum and I will move the whole earth." Wozijishuode also said, "Give me a Jenkins and I can automate everything."

<!--以上为摘要内容-->

I have summed up four characteristics for it:

## 1. Every wish fulfilled — comprehensive triggering

A job created on Jenkins can be triggered manually; it can also be triggered on a schedule; it can also poll the source repository on a schedule and trigger only when the code has been updated; or you can generate a link and trigger the job by sending a request to that link.

A dazzling variety — very complete and very thoughtful.

## 2. Connect everything — exceptional extensibility

Jenkins itself is nothing more than an automation server. But its architecture is excellent, and it provides a great many extension points of its own, through which plugins can add new functionality and new features. Its powerful capabilities are almost all implemented by plugins. Plugins can also extend extension points to add new extension points, which are then offered to other plugins for use. (It is through these plugins that Jenkins integrates all kinds of version control systems, all kinds of source build tools, all kinds of static analysis tools, all kinds of testing tools, all kinds of cloud platforms and all kinds of everything else, and thereby became the de facto standard for continuous integration / continuous delivery / DevOps practices today.)

Endlessly growing, endlessly multiplying.

## 3. Built and shared together — an active open source community

Jenkins is an open source project, and its source code is easy to obtain. The open source mechanism means the Jenkins tool itself will never become a black box — everything is transparent. Anyone can contribute code to fix problems and add new features, and everyone else can directly enjoy the benefits that code brings. Issue tracking and progress can also be queried publicly online. The many plugins in the Jenkins Plugin Center are open source as well.

Open source has power — we build it together and we share it together.

## 4. An efficiency revolution — the pipeline-as-code feature

The new generation of Jenkins introduced the new Pipeline job type. It replaces the many-click, many-round graphical configuration operations with executable script code, greatly improving the efficiency of job configuration. It also lifts work in Jenkins from the level of application operation to the level of code development.

As they say, code changes the world.

---

## Afterword

Today, Pipeline-type jobs have become mainstream, and converting classic jobs into Pipeline jobs is an unstoppable trend. But even in the "old era" before the Pipeline job type existed, Jenkins — because it integrated so many plugins and, as a continuous integration / continuous delivery tool, ran through every stage of the software development lifecycle — had the characteristic of a great many knowledge points that were fragmented and scattered. In the "new era" of using pipelines, codification makes the expression of configuration more centralized and unified, solving some old problems, but it also obeys the rule that "the greater the capability, the higher the demands", and it still has the quality of being "easy to get started with, hard to master".

Let's learn together and keep accumulating.

Let me share one of my mottos: a small step forward every day is a new height!

>This article was first published on my WeChat public account "左手编程右手文化" (Programming in the Left Hand, Culture in the Right), account ID: shanyshanb. You are welcome to follow.
