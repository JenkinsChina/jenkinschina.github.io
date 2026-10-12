---
title: 'Groovy Syntax Tutorial Series: Comments (Part 1)'
date: 2020-02-15
author: Tang MoYing
categories: [Groovy]
tags: [Groovy]
lang: en
alt_url: /post/groovy-syntax-comments
---
* TOC
{:toc}

# Groovy Syntax Overview

This tutorial series introduces the syntax of the Groovy programming language. Groovy's syntax is derived from Java's syntax, but it is enhanced with specific types and allows certain simplifications.

<!--以上为摘要内容-->

# 1. Comments

## 1.1 Single-line comments

A single-line comment starts with `//` and can be used anywhere on a line. The characters following `//` (up to the end of that line) are considered part of the comment.

```groovy
// a standalone single-line comment
println("My blog: https://tangming.org/") // a comment from here to the end of the line
```

## 1.2 Multi-line comments

A multi-line comment starts with `/*` and can be used anywhere on a line. The characters following `/ *` are treated as part of the comment, including line breaks, until the first `*/` ends the comment.
Therefore, a multi-line comment can be placed at the end of a statement, or even inside a statement.

```groovy
/* a standalone multi-line comment
   spanning two lines */
println "My blog: https://tangming.org/" /* the start of a multi-line comment
                   the end of the multi-line comment */
println 1 /* comment: one */ + 2 /* comment: two */
```

## 1.3 Groovydoc comments

Like multi-line comments, Groovydoc comments are multi-line comments, but they start with `/**` and end with `*/`.

The lines after the first comment line of a Groovydoc comment may optionally start with an asterisk *.

These comments relate to the following concepts:

- Type definitions (classes, interfaces, enums, annotations)
- Field and property definitions
- Method definitions

If you do not add Groovydoc in the places above, the compiler will not warn you. But you should add comments before these constructs.

```groovy
/**
 * comment for the class
 */
class Person {
    /** Person's name */
    String name

    /**
     * Create a greeting method
     *
     * @param otherPerson the person to greet
     * @return the greeting
     */
    String greet(String otherPerson) {
       "Hello, ${otherPerson}"
    }
}
```

Groovydoc follows the same conventions as Java's Javadoc. Therefore, the same tags as Javadoc can be used.

## 1.4 The shebang line

There is a special kind of single-line comment, usually called the `shebang line` on UNIX systems.

It lets a script be run directly from the command line. This requires that you have the Groovy distribution installed and the groovy command configured in your `PATH`.

```bash
#!/usr/bin/env groovy
println "Hello! My blog: https://tangming.org/"
```

The `＃` character must be the first character of the file. Any indentation will cause a compilation error.
