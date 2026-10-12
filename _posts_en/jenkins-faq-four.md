---
title: Jenkins FAQ Collection (Part 4)
date: 2019-08-05
author: Tang MoYing
categories: [Jenkins]
tags: [Jenkins, Pipeline]
lang: en
alt_url: /post/jenkins-faq-four
---
* TOC
{:toc}

# Question 16: Can a timeout be set with Pipeline code?

Reference: Yes. The following code sets a timeout of 1 hour, and it can be set either globally for the pipeline or at the stage level:

```
options {
  timeout(time: 1, unit: 'HOURS')
}
```

# Question 17: Is there a plugin that can monitor changes to the Jenkins configuration?

<!--以上为摘要内容-->

Reference: Yes. The jobConfigHistory plugin can monitor and compare changes to Jenkins job configuration. In principle, it compares the corresponding config.xml files.
For Pipeline-type jobs, the usual approach is to configure a code repository and specify the location of the Jenkinsfile.
That way, even if the contents of the Jenkinsfile are modified, the corresponding config.xml does not change.
To solve this problem there is another plugin — Pipeline Configuration History — which can track not only the Jenkinsfile but also changes to global shared libraries. Very comprehensive.

# Question 18: Emails fail to send?

Reference: There are various causes. One fairly common one is that the "System Admin e-mail address" on the system configuration page is not consistent with the configured mail sender, which is easy to overlook.

# Question 19: Is there a Chinese community for Jenkins?

Reference: Yes. Official site: https://jenkins-zh.cn  It is still under construction — contributions of code and PRs, as well as feedback and suggestions, are all welcome.

# Question 20: Sometimes the cause of an error can't be seen in the job log?

Reference: You can try looking at the Jenkins system log. It also holds a lot of warnings and error information and is a good place to pin down problems — most people don't know about it. Path: Home page - Manage System - System Log - All System Logs.

>This article was first published on the WeChat public account "DevOps持续交付" (DevOps Continuous Delivery), account ID: devopscd. You are welcome to follow.
