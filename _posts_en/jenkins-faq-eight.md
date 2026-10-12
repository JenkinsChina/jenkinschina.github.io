---
title: Jenkins FAQ Collection (Part 8)
date: 2020-05-20
author: Tang MoYing
categories: [Jenkins]
tags: [Jenkins, Pipeline]
lang: en
alt_url: /post/jenkins-faq-eight
---
* TOC
{:toc}

# Question 36: What is the relationship between Hudson and Jenkins?

Answer: Both are open-source continuous integration tools written in Java.

In fact, Jenkins is a fork of Hudson.

<!--以上为摘要内容-->

Hudson was started by Sun Microsystems in 2004, and its first version was released on java.net in 2005.

Starting in 2007, Hudson gradually took over the leading position held by CruiseControl and other open-source build tools.

At the 2008 JavaOne conference, it won the Duke's Choice Award in the developer solutions category.

In November 2010, Oracle's acquisition of Sun brought up the question of Hudson's ownership.

Between the main project contributors and Oracle, although many agreements were reached, one key issue was the trademark name "Hudson".

In December 2010, Oracle asserted that it owned the name and the right to apply for the trademark.

Therefore, on January 11, 2011, a vote was called to change the project name from "Hudson" to "Jenkins".

On January 29, 2011, the proposal was approved by a community vote, and the Jenkins project was created.

On February 1, 2011, Oracle stated that it intended to continue developing Hudson, and considered Jenkins merely a branch rather than a rename.

As a result, Jenkins and Hudson went on as two independent projects, each considering the other a branch of itself.

By December 2013, Jenkins on GitHub had 567 project members and about 1,100 public repositories, compared with 32 project members and 17 public repositories for Hudson.

Today the differences between the two are greater still; Jenkins has clearly surpassed Hudson across the board.

In addition, perhaps out of a dislike of Oracle, as Java developers we naturally ought to support and use Jenkins.

From the logos of the two projects you can also see the kinship between them — both are two old men. Later Hudson was donated by Oracle to the Eclipse Foundation, so the Hudson old man has an Eclipse halo.

Hudson has stopped development and has not released a new version for years (the latest version was released in 2016), while the Jenkins community and development are exceptionally active, and Jenkins 2.x has extended it into the CD domain.

Jenkins 1 is already the most widely used CI/CD tool on the market today.


# Question 37: What are the similarities and differences between Jenkins plugins and shared libraries? When should I use a plugin and when should I use a shared library?

Answer: A shared library is a feature that only Pipeline-type jobs can use.

Plugins focus on extending the functionality of the Jenkins system itself, and their scope is broader. For example, defining new job types (Pipeline itself is implemented through a plugin), new parameter types, new trigger types, new SCM types, new notification types, new authorization strategies, new cloud types, and so on.

Plugins can also define new build steps, which can be configured graphically in freestyle jobs and invoked through a DSL by optimizing compatibility with Pipeline jobs.

Pipeline also has a dedicated API for defining new DSL steps (which can only be invoked through code).

Plugins are written in Java and shared libraries are written in Groovy, and a shared library can in turn call the DSL steps provided by plugins.

Using a plugin requires installing the plugin package on the Jenkins master before it takes effect; to upgrade it, you also need to restart the master.

A shared library, by contrast, only needs its address to be configured in Jenkins before it can be used, and you can specify different branches to use. Changes to shared library code take effect in real time.

As a best practice, plugins provide generic tool-level steps (the building blocks), and shared libraries implement functional steps (assembling the blocks), combining steps and sharing them across multiple Jenkins jobs. It is similar to the relationship between an API and an APP.


# Question 38: Can Jenkins do everything?

Answer: Be clear that Jenkins is an automation server. It can automate your operations, and automation mainly consists of three parts. The first is trigger automation: a Jenkins job can be triggered automatically according to certain rules,
for example on a schedule, or when a change is committed to the code repository, or when the contents of the code repository change, and so on. The second is execution automation; the third is notification automation. The second part is defined by users themselves, and what makes Jenkins convenient is that it supports
various ways of invoking automation scripts, such as ant, maven, sh, bat, powershell, python, groovy, and so on. The automation scripts themselves are something users have to write.
Only after your operations have been reworked so that they can be carried out by automation scripts can you connect them to Jenkins and have it run them automatically. So a Jenkins engineer should be very familiar with automation principles and with the various automation scripting languages and automation tools, and should provide suggestions and guidance for the team's automation work.

# Question 39: What is the relationship between slave, node, and agent, and are there any differences?

Answer: Conceptually they are basically the same. `agent` can be seen as the new name for `slave` (because slave carries the meaning of "slave"...). In terms of usage, as Pipeline keywords they differ slightly.
In scripted pipeline, `node` is used to specify the execution node; in declarative pipeline, the `agent` keyword is used, and under the `agent` keyword there are further keywords such as `node`, `docker`, and `kubernetes`.

# Question 40: How does Jenkins integrate with tools such as Ant and Maven?

Answer: There are two ways to use this kind of build tool in Jenkins.

One is to pre-configure it in the Jenkins Global Tool Configuration, setting the tool name and path, and specifying the name when using it.
The advantage of this approach is that Jenkins can automatically install the build tool on the `agent` machine and add the executable file to the `PATH` directory.
The inconvenient part is that it requires pre-configuration, and when using it you need to explicitly specify the name; automatic installation also requires the machine to be able to access the external network.

The other approach is to install the corresponding tool in advance directly on the `agent` machine and configure its executable file into the system `PATH` directory.
The advantage of this approach is that you can use the `ant` and `mvn` commands directly. The disadvantage is that it requires pre-installation, but it can also avoid job execution failures caused by a machine being unable to access the external network.
Pre-installation also makes the `agent` environment more controllable. In practice, `agent` machines need a number of tools installed anyway, and this has been automated. Adding one more tool makes little difference to the workload.

If the Jenkins environment has external network access and Ant and Maven both use the default configuration (repository addresses, etc.), you can use the first approach. In other cases, the second approach is recommended.

>This article was first published on the WeChat public account "DevOps持续交付" (DevOps Continuous Delivery), account ID: devopscd. You are welcome to follow.
