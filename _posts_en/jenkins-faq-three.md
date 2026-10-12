---
title: Jenkins FAQ Roundup (Part 3)
date: 2019-08-03
author: Tang MoYing
categories: [Jenkins]
tags: [Jenkins, Pipeline]
lang: en
alt_url: /post/jenkins-faq-three
---
* TOC
{:toc}

# Question 11: How do I trigger other Jenkins jobs from a Pipeline script?

Answer: There is a `build` step you can look into; it supports both synchronous and asynchronous triggering.

# Question 12: Is there a convenient way to see the list of currently installed plugins and their versions on Jenkins? You can see them under Manage Plugins - Installed, but copying them out brings extra information that is hard to handle. For example, the extra plugin descriptions mean that after pasting into a spreadsheet you still have to delete them one by one manually.

<!--以上为摘要内容-->

Answer: Manage Jenkins - System Information has a plugin section at the very bottom, which shows only three columns: name, version and enabled status.

# Question 13: Different branches need different handling actions. How do I write that with Pipeline?

Answer:
```
when {
    branch 'xxx'
}
steps {
    echo 'do something'
}
```

# Question 14: How do I use a Pipeline shared library?

Answer: Once you have written a lot of Pipeline scripts, although every job is different, there are many parts that are common or similar, and writing them over and over again is unnecessary. For one thing it is duplicated effort; for another, because you type them out by hand every time, you may make a mistake and then have to debug to find the cause. A shared library lets you extract these common methods and make them available to every Pipeline job. Many of the people doing Jenkins work today do not come from a development background and have no development experience. This form is actually similar to the concept of a library in a programming language: you extract some general-purpose methods and turn them into parameterized calls, which falls under code reuse. At present, there are mainly two ways to use shared libraries. One is to generate all of the Pipeline content with a shared library, so that the `Jenkinsfile` contains just one line calling it; the other is to keep the main Pipeline framework in the `Jenkinsfile` and use the shared library only to implement a few custom individual steps. One more thing worth mentioning: most people are just starting out with Pipeline, writing their own `Jenkinsfile` and extracting common methods into a shared library to save themselves trouble, which creates the preconception that "shared libraries always have to be written by yourself". That is not the case either. In fact, as long as a library is suitable, other people's libraries can be used just as well. It means the same thing as a third-party library in a programming language. Writing Pipeline shared libraries requires knowledge of the `Groovy` programming language (Pipeline is not pure Groovy either — there is no room to go into detail here), so study it well. Young man, you are a developer now too!

# Question 15: How do I use the `post` method in a scripted Pipeline?

Answer: `post` can only be used in a declarative Pipeline; in a scripted Pipeline you use the most primitive `try...catch...` to catch exceptions. In general, unless you have a special need, it is recommended to use a scripted Pipeline, since the bar to entry is lower.

>This article was first published on my WeChat public account "左手编程右手文化" (Programming in the Left Hand, Culture in the Right), account ID: shanyshanb. You are welcome to follow.
