---
title: Distinguishing the three different levels of dependencies in Gradle
date: 2023-11-04
author: Tang MoYing
categories: [Gradle]
tags: [dependencies]
lang: en
alt_url: /post/gradle-dependencies-plugins-buildscript
---
* TOC
{:toc}

`Gradle` is a very flexible and powerful build system, but its concepts are relatively complex. As long as you grasp the core and keep the distinctions straight, it will not feel confusing.

Does the build script below look hard to understand?

```
buildscript {
    repository for build script dependencies
    repositories {
        mavenCentral()
    }
    // build script dependencies
    dependencies {
        classpath 'com.android.tools.build:gradle:4.2.0'
    }
}
repositories {
    mavenCentral()
    jcenter()
    google()
}
dependencies {
    implementation 'com.google.guava:guava:30.1-jre'
    testImplementation 'junit:junit:4.13.2'
}  
plugins {
      id 'com.android.application'
      id 'org.jetbrains.kotlin.jvm' version '1.5.10'
}
```

<!--以上为摘要内容-->

DevOps involves a great many tools, and every one of them comes with lengthy documentation; rote memorization will not get you anywhere. The right path is to understand the terminology of the core concepts, tell the different objects apart, and grasp what the designers had in mind, until you reach the point where it all feels "a matter of course" and "naturally so".

There are three principal entities in `Gradle`: gradle itself, the project (the one to be built with gradle), and the build script (the one written with gradle).


Because `Gradle` is an extensible build system, its build scripts are executable scripts as well, rather than the `xml` markup language used by `Ant` and `Maven`; so both of them have dependencies.


Of course, the project has dependencies too.


gradle's own dependencies are called `plugins`: they extend gradle's own functionality, just as `IDEA` has plugins and `Jenkins` has plugins. They are declared with `plugins`.

The project's dependencies do not directly provide functionality; rather, the code you write in the project needs to rely on these libraries. They are declared with `dependencies`.

The `gradle` build script is declared with `buildscript` — the name says it all.


Once these concepts are clear, take another look at the build script below with comments added, and it becomes very easy to understand!

```
// build script configuration  
buildscript {
    repository for build script dependencies
    repositories {
        mavenCentral()
    }
    // build script dependencies
    dependencies {
        classpath 'com.android.tools.build:gradle:4.2.0'
    }
}
// repository for project dependencies
repositories {
    mavenCentral()
    jcenter()
    google()
}
// project dependencies configuration
dependencies {
    implementation 'com.google.guava:guava:30.1-jre'
    testImplementation 'junit:junit:4.13.2'
}  
// plugins that the gradle build tool depends on
plugins {
      id 'com.android.application'
      id 'org.jetbrains.kotlin.jvm' version '1.5.10'
}
```
