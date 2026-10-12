---
title: Jenkins Plugin Update Center address changer — switch to a domestic mirror with one click
date: 2020-04-06
author: Tang MoYing
categories: [Plugin Center, Jenkins]
tags: [Plugin Center, Jenkins]
lang: en
alt_url: /post/change-jenkins-plugin-center-source-to-cn
---
* TOC
{:toc}

# The Jenkins Plugin Center domestic mirror

The 1500+ plugins Jenkins offers are its most valuable resource and its defining feature; they give Jenkins powerful functionality, flexibility, and the ability to connect and interact with other platforms.

Recently, however, users in China have clearly felt that Jenkins downloads plugins very slowly, and that downloads often time out and fail. This problem has caused a great deal of trouble for users in China.

This is mainly because the network infrastructure servers of the Jenkins open source community are all located abroad.

In November 2019, the Jenkins Chinese community released a domestic mirror address.

This mirror solved the problem that other mirrors had always had — that they could not really be used — so that users in China can now download plugins at the full speed their bandwidth allows.

<!--以上为摘要内容-->

# A high barrier to switching

But switching the Jenkins Plugin Center to a domestic mirror address is not easy.

Users have to do more than change the plugin center address; they also have to manually add a certificate file in a specific directory.

In practice, users often run into all kinds of problems and propose various solutions based on their own understanding, which makes the configuration methods even more confusing.

So I built the Jenkins Plugin Update Center address changer (jenkins-update-center-changer), which switches to the domestic mirror address in one click.

# The one-click switching script

It is very simple to use: just run the following command in any directory on the Jenkins master server (the script reads the `JENKINS_HOME` environment variable automatically):

`bash -c "$(curl -fsSL https://gitee.com/hummerstudio/jenkins-update-center-changer/raw/master/jenkins-update-center-changer.sh)"`

After the change succeeds, the script also prints guidance for what to do next:

![jenkins-update-center-changer](/static/img/2020/04/jenkins-update-center-changer.png)

# An open source project — contributions welcome

This tool is an open source project, and everyone is welcome to file issues and submit PRs!

Gitee address: [https://gitee.com/hummerstudio/jenkins-update-center-changer](https://gitee.com/hummerstudio/jenkins-update-center-changer)

GitHub address: [https://github.com/hummerstudio/jenkins-update-center-changer](https://github.com/hummerstudio/jenkins-update-center-changer)

(The Gitee repository is the primary one, mainly because it is a domestic service and therefore faster.)
