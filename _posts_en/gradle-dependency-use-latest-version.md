---
title: Using the Latest Version of a Gradle Dependency
date: 2023-11-04
author: Tang MoYing
categories: [Gradle]
tags: [Gradle]
lang: en
alt_url: /post/gradle-dependency-use-latest-version
---
* TOC
{:toc}

If you configure a dependency in `Gradle` without specifying a version, the build fails with an error saying the dependency cannot be found.
But when you have a lot of dependencies, you also have to trawl the repository one by one to see what the latest version of each library is.

So does Gradle support using the latest version of a dependency directly?

The answer is yes, though `gradle`'s documentation doesn't flag it in any prominent place.

The trick is to put a plus sign `+` in the `version` field, and `gradle` will work out the latest version automatically and download it.

Once everything is pointed at the latest version, you can then work through the few remaining dependency-conflict errors from the log, which saves a great deal of effort.
