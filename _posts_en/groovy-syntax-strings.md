---
title: 'Groovy Syntax Tutorial Series: Strings (Part 3)'
date: 2020-02-21
author: Tang MoYing
categories: [Groovy]
tags: [Groovy]
lang: en
alt_url: /post/groovy-syntax-strings
---
* TOC
{:toc}

# Groovy Syntax Overview

This tutorial series introduces the syntax of the Groovy programming language. Groovy's syntax is derived from Java's syntax, but it is enhanced with specific types and allows certain simplifications.

<!--以上为摘要内容-->

# 4. Strings

Text literals are represented as a series of concatenated characters, and are called strings.

Groovy lets you instantiate `java.lang.String` objects as well as GStrings (`groovy.lang.GString`), the latter also known as interpolated strings in other programming languages.

## 4.1 Single-quoted strings

Single-quoted strings are a series of characters surrounded by single quotes:
```groovy
'My blog: https://tangming.org/'
```

Single-quoted strings are plain `java.lang.String` and do not support interpolation.

## 4.2 String concatenation

All Groovy strings can be concatenated with the `+` operator:

```groovy
assert 'ab' == 'a' + 'b'
```

## 4.3 Triple-single-quoted strings

Triple-single-quoted strings are a series of characters surrounded by three single quotes:

```groovy
'''a triple-single-quoted string'''
```

Triple-single-quoted strings are also plain `java.lang.String` and do not support interpolation.

Triple-single-quoted strings can span multiple lines.

The content of the string can cross line boundaries without the need to split the string into several pieces, and without concatenation or newline characters:

```groovy
def aMultilineString = '''First line
Second line
Third line'''
```

If your code is indented, for example in a method body of a class, your string will contain the indentation whitespace.

The Groovy Development Kit includes the `String＃stripIndent()` method for stripping indentation, and the `String＃stripMargin()` method for removing text from the beginning of a string using a delimiter.

When a string is created as follows:

```groovy
def startingAndEndingWithANewline = '''
First line
Second line
Third line'''
```

You will notice that the first character of the resulting string is a newline. That character can be removed by escaping the newline with a backslash:

```groovy
def strippedFirstNewline = '''\
First line
Second line
Third line'''

assert !strippedFirstNewline.startsWith('\n')
```

### 4.3.1 Escaping special characters

You can use the `\` backslash character to escape a single quote, to avoid terminating the string literal:
```groovy
'an escaped single quote: \'needs a backslash'
```

You can escape the escape character with a double backslash:

```groovy
'an escaped escape character: \\needs a double backslash'
```

Some special characters also use the backslash as an escape character:

| Escape character | Meaning | 
| ------- | ---- | 
| \t      | tab | 
| \b      | backspace | 
| \n      | newline | 
| \r      | carriage return | 
| \f      | form feed | 
| \\\     | backslash | 
| \'      | single quote in a single-quoted string (optional for triple-single-quoted and double-quoted strings) | 
| \"      | double quote in a double-quoted string (optional for triple-double-quoted and single-quoted strings) | 
| \t      | tab | 
| \b      | backspace | 

We will learn more about escaping in the other string types introduced later.

### 4.3.2 Unicode escape sequences

For characters that do not exist on the keyboard, you can use a Unicode escape sequence: a backslash, followed by 'u', then 4 hexadecimal digits.

For example, the euro currency symbol can be represented as:

```groovy
'euro sign: \u20AC'
```

## 4.4 Double-quoted strings


Double-quoted strings are a series of characters surrounded by double quotes:

```groovy
"a double-quoted string"
```

If there is no interpolation expression, a double-quoted string is a plain `java.lang.String`; if interpolation is present, it is a `groovy.lang.GString` instance.

To escape a double quote, you can use the backslash character: `double quotes: \""`.

### 4.4.1 String interpolation

Groovy expressions can be interpolated into all types of strings, except single-quoted and triple-single-quoted strings.

Interpolation is the act of replacing placeholders in a string with their values when the string is evaluated. Placeholder expressions are surrounded by `${}`.

For unambiguous dotted expressions, the curly braces can be omitted, i.e. in that case we can just use the `$` prefix.

If a GString is passed to a method that takes a String, the expression value inside the placeholder is evaluated to its string representation (by calling `toString()` on that expression), and the resulting String is passed to the method.

Below is a string with a placeholder that refers to a local variable:

```groovy
def url = 'https://tangming.org' // a plain string
def greeting = "Welcome to ${url}"

assert greeting.toString() == 'Welcome to https://tangming.org'
```

Any Groovy expression is valid, as shown by using an arithmetic expression:

```groovy
def sum = "2 plus 3 equals ${2 + 3}"
assert sum.toString() == '2 plus 3 equals 5'
```

Between the `${}` placeholders, not only expressions but also statements are allowed. However, the value of a statement is `null`.
 
Therefore, if several statements are interpolated in such a placeholder, the last one should return a meaningful value to be interpolated in some way. For example, `"1 and 2 add up to$ {def a = 1; def b = 2; a + b}"` is supported and works as expected, but a good practice is generally to stick to simple expressions inside GString placeholders.

In addition to the `${}` placeholder, we can also prefix a dotted expression with a single `$` sign:

```groovy
def blog = [url: 'https://tangming.org', author: hummerstudio]
assert "Url of $blog.author's blog is $blog.url" == "Url of hummerstudio's blog is https://tangming.org"
```

But only dotted expressions of the form `a.b`, `a.b.c`, etc. are valid.

Expressions containing parentheses (for example method calls, braces for closures, dots that are not part of a property expression or an arithmetic operator) will not work.
 
Given the following numeric variable definition:

```groovy
def number = 3.14
```

The following statement will throw a `groovy.lang.MissingPropertyException` exception, because Groovy thinks you are trying to access the `toString` property of the number, but that property does not exist:

```groovy
shouldFail(MissingPropertyException) {
    println "$number.toString()"
}
```

You can think of `"$number.toString()"` as being interpreted by the parser as `"${number.toString}()"`.

Similarly, if an expression is ambiguous, the curly braces need to be kept:

```groovy
String thing = 'treasure'
assert 'The x-coordinate of the treasure is represented by treasure.x' ==
    "The x-coordinate of the $thing is represented by $thing.x"   // <= not allowed: ambiguous
assert 'The x-coordinate of the treasure is represented by treasure.x' ==
        "The x-coordinate of the $thing is represented by ${thing}.x"  // <= braces required
```

If you need to escape the `$` or `${}` placeholders in a GString so that they appear as-is without interpolation, you only need to escape the dollar sign with the `\` backslash character:

```groovy
assert '$5' == "\$5"
assert '${name}' == "\${name}"
```

### 4.4.2 Special case of interpolating closure expressions


So far we have seen that arbitrary expressions can be interpolated inside `${}` placeholders, but closure expressions have a special case and notation.

When the placeholder contains the arrow `${->}`, the expression is actually a closure expression — you can think of it as a closure with a dollar sign in front of it:

```groovy
def sParameterLessClosure = "1 + 2 == ${-> 3}" 
assert sParameterLessClosure == '1 + 2 == 3'

def sOneParamClosure = "1 + 2 == ${ w -> w << 3}" 
assert sOneParamClosure == '1 + 2 == 3'
```

The closure on the first line is a parameter-less closure (a closure with no arguments).

The closure on the third line uses a single `java.io.StringWriter` argument, to which you can append with the `<<` left-shift operator.

In either case, both placeholders are embedded closures.

On the face of it, this looks like a more verbose way to define the expression to be interpolated, but closures have one interesting advantage over plain expressions: lazy evaluation.

Let's consider the following example:

```groovy
def number = 1 
def eagerGString = "value == ${number}"
def lazyGString = "value == ${ -> number }"

assert eagerGString == "value == 1" 
assert lazyGString ==  "value == 1" 

number = 2 
assert eagerGString == "value == 1" 
assert lazyGString ==  "value == 2" 
```

- Line 1. We define a `number` variable equal to `1`, then interpolate it in two GStrings, as an expression in `eagerGString` and as a closure in `lazyGString`
- Line 4. We expect the resulting string to contain the same string value 1 as `eagerGString`
- Line 5. Similarly for `lazyGString`
- Line 6. We then change the value of the variable to a new number
- Line 7. With a plain interpolation expression, the value is effectively bound when the GString is created.

- Line 8. With a closure expression, however, the closure is called every time the GString is coerced to a String, producing a string that contains the new numeric value.

An embedded closure expression with several parameters will produce an exception at runtime. Closures are only allowed to have zero or one parameter.

### 4.4.3 Interoperability with Java

When a method (whether implemented in Java or Groovy) expects a `java.lang.String` but we pass a `groovy.lang.GString` instance, the `toString()` method of the GString is called automatically and transparently.

```groovy
String takeString(String message) {         
    assert message instanceof String        
    return message
}

def message = "The message is ${'hello'}"   
assert message instanceof GString           

def result = takeString(message)            
assert result instanceof String
assert result == 'The message is hello'
```

- We create a `GString` variable
- We check again that it is an instance of `GString`
- Then we pass that `GString` to a method that takes a `String` as its parameter
- The declaration of the `takeString()` method clearly states that its only parameter is a String
- We also verify that the parameter is really a `String` and not a `GString`

### 4.4.4  Hash codes of GString and String

Although interpolated strings can be used in place of plain Java strings, they are different from strings: their hash codes differ.

Plain Java strings are immutable, whereas the String representation produced by a GString may vary depending on its interpolated values.

Even for the same resulting string, the hash codes of GString and String are different.

```groovy
assert "one: ${1}".hashCode() != "one: 1".hashCode()
```

GString and String have different hash values, and you should avoid using a GString as a key of a Map, especially when we try to look up the associated value with a String rather than a GString.

```groovy
def key = "a"
def m = ["${key}": "letter ${key}"]     

assert m["a"] == null   
```

With a GString as the key, when we try to get the value with a String key, we will not find it, because String and GString have different hash values.

## 4.5 Triple-double-quoted strings

Triple-double-quoted strings behave like double-quoted strings, but they can be multi-line, similar to triple-single-quoted strings.

```groovy
def name = 'students'
def template = """
    Dear ${name},

    Hello!

    Learning Groovy and Jenkins
    
    Welcome to https://tangming.org
"""

assert template.toString().contains('students')
```

Neither double quotes nor single quotes need to be escaped in a triple-double-quoted string.

## 4.6 Slashy strings

In addition to the usual quoted strings, Groovy also provides slashy strings, which use `/` as the opening and closing delimiter.

Slashy strings are particularly useful for defining regular expressions and patterns, because there is no need to escape backslashes.

Slashy string example:

```groovy
def fooPattern = /.*foo.*/
assert fooPattern == '.*foo.*'
```

You only need to escape the forward slash with a backslash:

```groovy
def escapeSlash = /a character \/ is a forward slash/
assert escapeSlash == 'a character / is a forward slash'
```

Slashy strings are multi-line:

```groovy
def multilineSlashy = /First line
    Second line
    Third line/

assert multilineSlashy.contains('\n')
```

Slashy strings can be thought of as another way of defining a `GString`, but with different escaping rules. Therefore, they support interpolation:

```groovy
def color = 'blue'
def interpolatedSlashy = /a ${color} car/

assert interpolatedSlashy == 'a blue car'
```

### 4.6.1 Special cases

The empty slashy string cannot be represented with a double slash, because the Groovy parser interprets it as a line comment.

That is why the following assertion will not actually compile, since it looks like an unfinished statement:

```
assert '' == //
```

Since the main purpose of slashy strings is to make regular expressions easier to use, things that would be errors in a GString, such as `$()` or `$5`, are fine in a slashy string.

Remember that there is no need to escape backslashes. Or you can think of it as not actually supporting escaping. The slashy string `/\t/` will not contain a tab character, but a backslash followed by the character "t".

Only the slash character can be escaped, i.e. `/\/folder/` will be a slashy string containing `'/folder'`.

A very important point about slash escaping is that a slashy string cannot end with a backslash. Otherwise, it would escape the slashy string terminator.

You can use a special trick instead, `/ends with slash ${'\'}/`. But it is best to avoid slashy strings in that case.

## 4.7 Dollar slashy strings

Dollar slashy strings are multi-line GStrings that start with `$/` and end with `/$`.

The escape character is the dollar sign, which can escape another dollar or a forward slash.

Neither the dollar nor the forward slash needs to be escaped, except for `/$` and `$/`.

Example:

```groovy
def name = "Guillaume"
def date = "April, 1st"

def dollarSlashy = $/
    Hello $name,
    today we're ${date}.

    $ dollar sign
    $$ escaped dollar sign
    \ backslash
    / forward slash
    $/ escaped forward slash
    $$$/ escaped $/
    $/$$ escaped /$
/$

assert [
    'Guillaume',
    'April, 1st',
    '$ dollar sign',
    '$ escaped dollar sign',
    '\\ backslash',
    '/ forward slash',
    '/ escaped forward slash',
    '$/ escaped $/',
    '/$ escaped /$'
].every { dollarSlashy.contains(it) }
```

It was created to overcome some of the limitations of the slashy escaping rules.

Use it when its escaping rules suit your string content (usually when there are some slashes you do not want to escape).

## 4.8 Summary table of string types

| String type | String syntax | Interpolatable | Multi-line | Escape character |
| -------- | --------- | ----- | ----- | ------- |
| Single-quoted    | `'...'`   | ❌    | ❌    | `\`     |
| Triple-single-quoted | `'''...'''` | ❌ | ✅    | `\`     |
| Double-quoted    | `"..."`   | ✅   | ❌    | `\`     |
| Triple-double-quoted |   `""""..."""` | ✅  | ✅  | `\`   |
| Slashy      | `/.../`  | ✅   | ✅     | `\`     |
| Dollar slashy | `$/.../$`  | ✅  | ✅      | `$`    |

## 4.9 Characters

Unlike Java, Groovy has no explicit character literal.

However, you can explicitly convert a Groovy string into an actual character in three different ways:

```groovy
char c1 = 'A' //first way
assert c1 instanceof Character

def c2 = 'B' as char //second way
assert c2 instanceof Character

def c3 = (char)'C' //third way
assert c3 instanceof Character
```

- First way: declare the variable with the explicit `char` type
- Second way: coerce using the `as` operator
- Third way: cast to char

Use the first approach when you want to keep a character in a variable, and the other two when a char value must be passed as an argument to a method call.