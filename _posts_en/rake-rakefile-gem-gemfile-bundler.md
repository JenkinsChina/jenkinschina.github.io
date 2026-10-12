---
title: A Clear Guide to the Relationships Between rake, Rakefile, gem, gemspec, bundler, bundle, and Gemfile
date: 2020-02-15
author: Tang MoYing
categories: [Ruby]
tags: [rake, Rakefile, gem, gemspec, bundler, bundle, Gemfile, Ruby]
lang: en
alt_url: /post/rake-rakefile-gem-gemfile-bundler
---
* TOC
{:toc}

# Overview

These are all concepts from the Ruby language. Below I introduce the meaning of each term and compare it with similar tools, so that readers can understand them.

<!--以上为摘要内容-->

# Ruby

`Ruby` means ruby (the gemstone); it is the name of a programming language. The logo of the `Ruby` language is a ruby.

`Ruby` is an open-source dynamic programming language that values simplicity and efficiency. Its syntax is elegant, it reads naturally, and it is comfortable to write.

The source files of the `Ruby` language use the `.rb` extension.

# rake and Rakefile

`rake` is the `make`-like program of the `Ruby` language. You can define tasks and source-code dependencies in it.

rake = r(uby's m)ake

Just as `make` has a `Makefile`, `rake` has the corresponding `Rakefile`.

Both belong to the category of build tools.

The table is shown below:

| Language | Build tool name | Build tool configuration file |
| --- | ---------- | ------------- |
| C   | Make       | Makefile      |
| Ruby | Rake      | Rakefile      |


# gem and gemspec

`gem` means gemstone, which you can easily associate with `Ruby` the ruby.

`gem` is the package management system of `Ruby`; the command is `gem`, and the package extension is also `.gem`, similar to `rpm`.

However, `rpm` can only install local packages, and cannot download over the network. Downloading over the network requires `yum` or `dnf`.

Likewise, on Debian-based systems the package management system is `dpkg`, which cannot download over the network. Network downloads require `apt`.

The gemspec file is the description file of a gem. It contains gem-related information such as package name, version, summary, description, author, and homepage.

Similarly, packaging for dpkg requires a spec file, and packaging for deb requires a control file.

The table is shown below:

| Language | Package management system | Package extension | Local | Network | Description file name |
| --- | ---------- | ---- | ---- | --- | --------- |
| Ruby | gem       | .gem |  ✅  | ✅  | \<package-name\>.gemspec |
| Red Hat-based | rpm  | .rpm |  ✅  | ❌  | SPECS/\<package-name\>.spec    |
| Red Hat-based | yum/dnf  | .rpm |  ❌  | ✅ |  -                  |
| Debian-based  | dpkg | .deb |  ✅  | ❌ |  debian/control         |
| Debian-based  | apt | .deb |  ❌  | ✅  |  -                      |

Note here that the file corresponding to gem is gemspec. Gemfile has nothing to do with gem; it is actually the name of bundler's configuration file.


# bundler, bundle, and Gemfile

`bundler` is the external dependency management tool for Ruby applications.

`bundle` is another gem, created to solve the problem of "misspelling bundler as bundle"; its only function is to install bundler, so that the two agree and no error is raised.

The `Gemfile` file describes the external dependency gems needed to run the related Ruby application, including information such as the source, gem name, and gem version.

When you run `bundler install`, `bundler` reads the `Gemfile` and installs all the dependency gems in one go.

# Summary

rake is the build tool of the Ruby language, and its configuration file is the Rakefile.

gem is the package management tool of the Ruby language, and its configuration file extension is .gemspec.

bundler is the external dependency management tool of the Ruby language. It has an alias, "bundle", and its configuration file is the Gemfile.
