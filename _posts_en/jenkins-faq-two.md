---
title: Jenkins FAQ Roundup (Part 2)
date: 2019-08-02
author: Tang MoYing
categories: [Jenkins]
tags: [Jenkins, Pipeline, Blue Ocean, Python, Groovy]
lang: en
alt_url: /post/jenkins-faq-two
---
* TOC
{:toc}

# Question 6: What is the relationship between Blue Ocean and Jenkins?

Answer: Put simply, Blue Ocean can be seen as a new UI that Jenkins introduced, with a more modern look and better interaction.

Of course, the most important thing is its support for the new pipeline job type introduced in Jenkins 2.x, which can clearly show the serial/parallel relationships and statuses of the various stages in the whole Pipeline.

<!--以上为摘要内容-->

Blue Ocean is implemented as a plugin; you just need to install the "Blue Ocean" plugin from the Jenkins Plugin Center. After installing it, in the classic UI, click "Open Blue Ocean" on the left to access the new interface.

# Question 7: Can a stage written in a shared library be displayed in the Blue Ocean interface?

Answer: Yes.

# Question 8: How can I check the Groovy version on Jenkins? For example, when I log into the server I can run groovy --version to see the Groovy version installed on the server.

Answer: You can find the jar package for groovy under the `${JENKINS_HOME}/war/WEB-INF/lib` directory. The version number is visible in the jar package name.

# Question 9: In a Jenkins pipeline, I run a bat command inside a stage and use it to set a variable. Is there any way to get that variable in the bat command of the next stage? With Groovy interpolation I can get variables defined in Groovy inside bat, but can I save a variable from bat back into Groovy?

Answer: A variable defined by set lasts only until the current bat command ends; it cannot be retrieved in the bat command of the next `stage`. Even within the same `stage`, if you write two separate bat commands, the later one cannot get the value defined by the earlier one. In this case, it is recommended to write the information you need to a file first and then read it back from the file. If the two stages run on different nodes, just add a step in between to archive the file.

# Question 10: Is there a Python library for working with Jenkins?

Answer: There are two. One is called `python-jenkins` and the other is called `jenkinsapi`. The former is older, the latter newer. You can choose whichever suits your preferences and functional needs.

<https://pypi.org/project/python-jenkins/>

<https://pypi.org/project/jenkinsapi/>

>This article was first published on my WeChat public account "左手编程右手文化" (Programming in the Left Hand, Culture in the Right), account ID: shanyshanb. You are welcome to follow.
