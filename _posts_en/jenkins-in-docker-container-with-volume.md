---
title: 'Jenkins Containerized Deployment: How to Persist JENKINS_HOME'
date: 2020-04-04
author: Tang MoYing
categories: [Jenkins, Docker]
tags: [Jenkins, Docker]
lang: en
alt_url: /post/jenkins-in-docker-container-with-volume
---
* TOC
{:toc}

# Symptom

In the Docker Preferences options, "Enabel Kubernetes" is selected to enable Kubernetes, but it stays in the `starting` state and cannot be used normally.

# Cause

To enable the Kubernetes feature, Docker needs to pull the Kubernetes-related images from an image registry.

Because access to [Docker Hub](https://hub.docker.com) is too slow from within China, the images cannot be pulled successfully, which leaves Kubernetes stuck in the `starting` state.


<!--以上为摘要内容-->

# Solution

Step 1: Download the code from the repository [https://github.com/hummerstudio/k8s-docker-desktop-for-mac](https://github.com/hummerstudio/k8s-docker-desktop-for-mac) to your local machine. You can run the following command directly in a terminal:

```bash
git clone git@github.com:hummerstudio/k8s-docker-desktop-for-mac.git
```
Step 2: Run the `load_images.sh` script in the root directory and the images will download correctly:

```bash
cd k8s-docker-desktop-for-mac
sh load_images.sh
```
