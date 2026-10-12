---
title: Jenkins FAQ Collection (Part 7)
date: 2019-08-14
author: Tang MoYing
categories: [Jenkins]
tags: [Jenkins, Pipeline]
lang: en
alt_url: /post/jenkins-faq-seven
---
* TOC
{:toc}

# Question 31: I have several nodes with the same environment and want jobs to be automatically assigned to idle nodes. Is that possible?

Reference: You only need to configure the same label on these nodes that share the same environment, and have the job specify that label as its run node; Jenkins will then automatically pick an idle node to execute the job.
A label in Jenkins carries the sense of a category or group, just like the label feature in WeChat's contacts. It is simply not designed very conspicuously, so if you don't know about it, it's easy to mistake it for a unique ID.

# Question 32: How does Jenkins work with the various static analysis tools?

<!--以上为摘要内容-->

Reference: This question is a big one; I'll write a dedicated article about it later.

# Question 33: Besides turning GUI clicks into code, what other advantages does Jenkins Pipeline have, and how can I understand it more deeply?

Reference: Turning mouse clicks into written code is one aspect of it — it looks like the previous GUI form-filling has simply become you writing code to call those same things.
That is one aspect, and because these features turn into code with simple, easy-to-understand keywords, you can write just a few lines to achieve the same functionality.
Another point is running a single job on multiple nodes; everyone is probably already doing this and takes it for granted, not even thinking of it as a feature unique to Pipeline!
There are also two very important points that people tend to overlook.
One is that you can write your own shared libraries to reuse code — that is, take a long piece of logic, encapsulate it in a shared library, and calling it becomes a single simple command again;
the other is that Pipeline supports many native steps, and these steps are cross-platform and can be implemented directly in Pipeline,
such as unzipping, reading and storing text files and JSON files, checking whether a node is a Unix environment, sending HTTP requests, and so on. All of these can be called with pure Pipeline script,
native, cross-platform, native, cross-platform, native, cross-platform — for important things, say them three times!
In the past, you might have had to write a Windows bat batch file and a Linux sh script to do it yourself!

# Question 34: What is the best way to manage a Jenkinsfile?

Reference: The more standard approach is to store it with the source code, in the root directory of the source repository, just as pom.xml lives in the root of the source repository.
Sometimes, depending on the actual production situation, you can also manage it in a separate repository — a single repository or multiple repositories are both fine. If you have no special requirements, storing it with the source code is recommended.

# Question 20: When upgrading Jenkins, how should I choose a version?

Reference: Jenkins has two release lines: one is the long-term support release, and the other is the weekly release. The long-term support release is updated every 12 weeks (close to 3 months, one quarter); the weekly release, as its name suggests, is updated every week. For production environments (enterprises, organizations) and similar settings, use the long-term support release; for personal use or learning, you can chase the newest and use the weekly release to learn about the latest bug fixes and feature updates. The long-term support release is updated about once a quarter, so you can decide according to your needs whether to upgrade a production environment.

>This article is also published on the WeChat public account "DevOps持续交付" (DevOps Continuous Delivery), account ID: devopscd. You are welcome to follow.
