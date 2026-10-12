---
title: 'Jenkinsclient Tutorial Series: Introduction and Installation (Part 1)'
date: 2020-05-17
author: Tang MoYing
categories: [Jenkinsclient]
tags: [Jenkinsclient]
lang: en
alt_url: /post/jenkinsclient-tutorial-01
---
* TOC
{:toc}

# Introduction to jenkinsclient

Jenkinsclient is a powerful, open-source, cross-platform Jenkins command-line client. It provides a Docker-style command line for users to operate Jenkins.

Jenkinsclient is written in Python, and the project source code is open-sourced under China's Mulan Open Source License. You can view it on Gitee and Github.

Gitee: [https://gitee.com/hummerstudio/jenkinsclient](https://gitee.com/hummerstudio/jenkinsclient)

Github: [https://github.com/hummerstudio/jenkinsclient](https://github.com/hummerstudio/jenkinsclient)

Project homepage: [https://pypi.org/project/jenkinsclient](https://pypi.org/project/jenkinsclient)

<!--以上为摘要内容-->

# Jenkinsclient features

## Feature 1: Open source

As mentioned above, the Jenkinsclient project source code is open-sourced under China's Mulan Open Source License. Contributions, code submissions, issue reports, documentation, spreading the word, and sharing are all very welcome.

## Feature 2: Cross-platform

From the very beginning of development, Jenkinsclient was positioned as cross-platform, and in the end Python was chosen for the implementation.

Windows, Linux, Mac, and Unix all have Python runtime environments, which guarantees that Jenkinsclient can be used across platforms.

## Feature 3: Multi-instance support

Jenkinsclient supports multiple Jenkins instances.

You can use the `jenkins config generate` command to generate a configuration file, configure information for multiple Jenkins servers in it, and use the `use` field to specify the server operated on by default.

## Feature 4: Simple and easy to use

To achieve simple and easy-to-use command-line operations, Jenkinsclient did a great deal of technology selection work at the design stage.

My goal was to design a Docker-style command line. Put simply, operations are expressed with commands/keywords rather than the traditional approach of operating through arguments/options.

For example, to start a docker container, we use:

```
docker container start CONTAINER
```

For jenkinsclient, for something like triggering a job, I wanted the command line to look like this:

```
jenkins job build JOB_NAME
```

By contrast, a traditional-style command-line implementation would look like this:

```
jenkins job -b JOB_NAME
```

Or like this:

```
jenkins-job build JOB_NAME
```

Python has several libraries for developing command-line tools, but most of them can only produce traditional-style command-line tools. After careful screening and writing demos, I chose Fire. Fire fully meets the requirements above.

Now, with Jenkinsclient, you can perform Jenkins operations with natural command-line syntax like this:

```
jenkins jobs                          // show the job list
jenkins job build JOB_NAME            // trigger a Jenkins job
jenkins job disable JOB_NAME          // disable a Jenkins job
jenkins job enable JOB_NAME           // enable a Jenkins job

jenkins plugins                       // show the plugin list
jenkins plugin install PLUGIN_NAME    // install a plugin
jenkins plugin uninstall PLUGIN_NAME  // uninstall a plugin
jenkins plugin search KEY_WORD        // search for a plugin
```

## Feature 5: Powerful

The architecture of Jenkinsclient is designed to give it the ability to implement every Jenkins-related operation. The major features implemented so far are:

- Configure Jenkins server information
- Manage Jenkins nodes
- Manage Jenkins plugins
- Manage Jenkins credentials
- Manage Jenkins jobs
- Manage Jenkins queues
- Manage Jenkins executors
- Manage Jenkins builds

This covers essentially every kind of operable Jenkins resource.

# Installation

The simplest way is to install jenkinsclient, which is hosted on PyPI, with pip. Just use the following command:

```
pip3 install jenkinsclient
```


You can also download the source code, unzip it, enter the root directory, and install it manually with the setuptools tool:

```
python setup.py install
```

# Upgrade

```
pip3 install -U jenkinsclient
```

# Quick start

## Configure server information

Use `jenkins config generate` to configure Jenkins server information.

This command generates a template configuration file for jenkinsclient, and then you need to fill in the actual values.

## View help information

Try typing `jenkins jobs` to view all jobs on the Jenkins server.

Try typing `jenkins plugins` to view all plugins on the Jenkins server.

For more commands, you can type `jenkins`.

Or type `jenkins <command-group>` to display the help information for a command group. For example, to view the help information for the Jenkins job management commands:

```
jenkins job
```

To view the help information for the Jenkins plugin management commands:

```
jenkins plugin
```

This tutorial series will introduce these commands in detail, so stay tuned!
