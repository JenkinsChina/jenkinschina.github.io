---
title: 'Groovy syntax tutorial, part 2: keywords and identifiers'
date: 2020-02-16
author: Tang MoYing
categories: [Groovy]
tags: [Groovy]
lang: en
alt_url: /post/groovy-syntax-keywords-and-identifiers
---
* TOC
{:toc}

# Groovy Syntax Overview

This tutorial series introduces the syntax of the Groovy programming language. Groovy's syntax derives from Java syntax, but it is enhanced with specific types and allows certain simplifications.

<!--以上为摘要内容-->

# 2. Keywords

All the keywords of the Groovy language:

```
as

assert

break

case

catch

class

const

continue

def

default

do

else

enum

extends

false

finally

for

goto

if

implements

import

in

instanceof

interface

new

null

package

return

super

switch

this

throw

throws

trait

true

try

while
```

# 3. Identifiers

## 3.1 Ordinary Identifiers

An identifier starts with a letter, a dollar sign `$` or an underscore, and cannot start with a digit.

Letters can be in the following ranges:

- "a" to "z" (lowercase ascii letters)

- "A" to "Z" (uppercase ascii letters)

- '\ u00C0' to '\ u00D6'

- '\ u00D8' to '\ u00F6'

- '\ u00F8' to '\ u00FF'

- '\ u0100' to '\ uFFFE'

The letters that follow may contain letters and digits.

Here are some examples of valid identifiers:

```groovy
def blog
def blog2
def my_blog
def $blog
def 博客
```

These, on the other hand, are invalid identifiers:

```
def 3blog
def my+blog
def my#blog
```

When preceded by a dot, all keywords are also valid identifiers. For example:

```groovy
blog.break
blog.case
blog.assert
```

## 3.2 Quoted Identifiers

Quoted identifiers appear after the dot of a dotted expression. For example, the `name` part of the `person.name` expression can be referenced as `person."name"` or `person.'name'`.

Some identifiers contain characters that the Java language specification forbids as illegal characters, but Groovy allows them once they are quoted. For example, dashes, spaces, exclamation marks and similar characters.

```groovy
def map = [:]

map."an identifier with a space and double quotes" = "ALLOWED"
map.'with-dash-signs-and-single-quotes' = "ALLOWED"

assert map."an identifier with a space and double quotes" == "ALLOWED"
assert map.'with-dash-signs-and-single-quotes' == "ALLOWED"
```

As we will see in the section on strings below, Groovy provides different string literals.

In fact, all types of strings are allowed after the dot:

```groovy
map.'single quote'
map."double quote"
map.'''triple single quote'''
map."""triple double quote"""
map./slashy string/
map.$/dollar slashy string/$
```
