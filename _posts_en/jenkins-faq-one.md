---
title: Jenkins FAQ Collection (Part 1)
date: 2019-08-01
author: Tang MoYing
categories: [Jenkins]
tags: [Jenkins, Pipeline, Docker]
lang: en
alt_url: /post/jenkins-faq-one
---
* TOC
{:toc}

# Question 1: How do Jenkins and Docker work together?

Reference: You can combine Jenkins with Docker by using containers as Jenkins agent nodes, which has many advantages. For example, it unifies the execution environment, creates and destroys agents automatically, and removes the cost of maintaining environments by hand.

# Question 2: When writing a pipeline with two stages, the first of which is assigned to a random machine to run on, and the second of which has to run on the same machine as the first, is there any way to do that?

<!--以上为摘要内容-->

Reference: Set a global `agent` and don't specify an `agent` separately for each stage.

# Question 3: A project compiles part of its code on Windows and part on Linux, and then the artifacts produced on Windows have to be merged into Linux. How should this be handled?

Reference: You could consider fixing the build machines, or putting all artifacts on one fixed storage machine and fetching them back from there.

# Question 4: What advantages does Pipeline have over Jenkins' traditional job types?

Reference: With Pipeline, a single job can span multiple nodes, and the code can be reused, which is more efficient than clicking through a graphical interface. Once the configuration becomes code, it can be version-controlled, which makes it easier to manage.

# Question 5: When starting a Pipeline, I'd like to check out only the Jenkinsfile.
Reference: If you have this kind of special requirement, it is recommended that you keep the `Jenkinsfile` in a separate git repository instead of putting it together with the application source code.

>This article was first published on my WeChat public account "左手编程右手文化" (Programming in the Left Hand, Culture in the Right), account ID: shanyshanb. You are welcome to follow.
