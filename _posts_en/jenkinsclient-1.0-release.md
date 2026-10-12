---
title: 'Jenkinsclient 1.0 Released: A Powerful Open-Source, Cross-Platform Jenkins CLI Client Under the Mulan Open Source License'
date: 2020-04-17
author: Tang MoYing
categories: [Jenkinsclient, Jenkins]
tags: [Jenkinsclient, Jenkins, Python]
lang: en
alt_url: /post/jenkinsclient-1.0-release
---
* TOC
{:toc}

# Introducing Jenkinsclient

Jenkinsclient is a powerful, open-source, cross-platform Jenkins command-line client that supports multiple instances. The project is open-sourced under the Mulan open source license.

Version 1.0 was officially released a few days ago.

PyPI project page: [https://pypi.org/project/jenkinsclient/](https://pypi.org/project/jenkinsclient/)

<!--以上为摘要内容-->

Source code repositories:
- Gitee: [https://gitee.com/hummerstudio/jenkinsclient](https://gitee.com/hummerstudio/jenkinsclient)
- Github: [https://github.com/hummerstudio/jenkinsclient](https://github.com/hummerstudio/jenkinsclient)

# Features

Jenkins is the de facto leader among continuous integration and continuous delivery tools. It is client/server software.

When we install and start Jenkins, what we have actually done is set up a Jenkins server.

We usually use a browser as the client, but the client does not have to be a browser — a command line works just as well.

Jenkinsclient interacts with Jenkins through the API that Jenkins provides.

Jenkinsclient supports multiple Jenkins instances.
You can generate a configuration file with `jenkins config generate`, configure several Jenkins servers in it, and use the `use` field to specify the server that operations default to.

Features in version 1.0:

- Get global information
    - Get Jenkins server information
    - Get the current logged-in user
    - Get plugin information
    - Get node information
    - Get job information
    - Get queue information
- Operate Jenkins objects
   - Plugins
     - Display, search, install and uninstall plugins, plus many other operations
   - Nodes
     - Display and get node information, plus many other operations
   - Executors
     - Get the number of executors on a node, plus many other operations
   - Jobs
     - Display, build, copy, create, delete, disable, enable and rename jobs, plus many other operations
   - Queues
     - Display and cancel queue items
   - Builds
     - Get a build's environment variables, information, logs and test reports, plus many other operations
   


# Installation

The simplest way is to install jenkinsclient from PyPI with pip. Just use the following command:

`pip3 install jenkinsclient`

You can also download the source code and install it manually with the setuptools tool:

`python setup.py install`

# Upgrade

`pip3 install -U jenkinsclient`

# Release package

jenkinsclient is already hosted on PyPI. You can visit the jenkinsclient project page on PyPI to download the release package:

[https://pypi.org/project/jenkinsclient/](https://pypi.org/project/jenkinsclient/)

# Usage

After installing `jenkinsclient`, you can use the `jenkins` command to perform a great many operations.

## Quick start

1. Use `jenkins config generate` to configure the Jenkins server information.

    This command generates the jenkinsclient configuration template file, and then you need to fill in the actual values.
1. Do anything you want.

Try typing `jenkins jobs` to see all the jobs on the Jenkins server.

Try typing `jenkins plugins` to see all the plugins on the Jenkins server.


## Viewing help information

Type `jenkins` to display jenkinsclient's help information. Or use `jenkins <command group>` to display a command group's help information, such as `jenkins config`, `jenkins job`.

The help information looks something like this:

```
NAME
    jenkins - Jenkins command-line client

SYNOPSIS
    jenkins GROUP | COMMAND

DESCRIPTION
    Jenkins command-line client

GROUPS
    GROUP is one of the following:

     build
       Jenkins build related operations

     config
       Configuration information

     executor
       Jenkins executor related operations

     job
       Jenkins job related operations

     node
       Jenkins node related operations

     plugin
       Jenkins plugin related operations

     queue
       Jenkins queue related operations

COMMANDS
    COMMAND is one of the following:

     jobs
       Display the job list

     nodes
       Display the node list

     plugins
       Display the plugin list

     queues
       View the queue

     version
       Display the Jenkins server version

     whoami
       Display the current user
```

# About the author

Tang Ming, Senior Software Engineer, Certified Jenkins Engineer. Member of the Jenkins China Community and the China DevOps Community.
Passionate about open source, focused on the DevOps technology stack, and familiar with DevOps culture and related tools. Committed to promoting and putting the DevOps philosophy into practice.
