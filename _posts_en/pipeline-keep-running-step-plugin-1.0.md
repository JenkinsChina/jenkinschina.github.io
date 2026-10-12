---
title: Processes Started by Jenkins Always Exit After the Build? Use the keepRunning Step for an Elegant Fix
date: 2020-05-04
author: Tang MoYing
categories: [SonarQube]
tags: [SonarQube]
lang: en
alt_url: /post/pipeline-keep-running-step-plugin-1.0
---
* TOC
{:toc}

# Background

Starting a process through Jenkins is a fairly common scenario in real-world work.

But under normal circumstances, a process started by a Jenkins job is killed by Jenkins once the build finishes.

<!--以上为摘要内容-->

This is determined by Jenkins' process tree management mechanism.

We can work around it by changing the value of a variable, but that approach has a few drawbacks:

1. It is not intuitive — even after it works, you cannot tell how the problem was solved;
1. It is hard to think of solving the problem this way.
1. Poor readability is in fact a problem that should be avoided as much as possible while writing code.


# Solution

The [pipeline-keep-running-step-plugin](https://github.com/hummerstudio/pipeline-keep-running-step-plugin) plugin provides a more intuitive `keepRunning` step, offering an elegant solution to this problem.

With the `keepRunning` step, the name tells you exactly what it does, so the readability problem is solved.

Using it is simple as well. To start tomcat, for example, this is all you need:

```
keepRunning {
    sh '/usr/local/apache-tomact/bin/startup.sh
}
```

# Project Information

Open source project home page: [https://github.com/hummerstudio/pipeline-keep-running-step-plugin](https://github.com/hummerstudio/pipeline-keep-running-step-plugin)

hpi plugin package download: [https://github.com/hummerstudio/pipeline-keep-running-step-plugin/releases](https://github.com/hummerstudio/pipeline-keep-running-step-plugin/release)
