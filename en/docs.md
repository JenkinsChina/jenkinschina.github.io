---
layout: page
title: Docs
permalink: /en/docs/
lang: en
alt_url: /doc_old
icon: octicon-book
isNavItem: false
nav_order: 50
---

The Jenkins project maintains its documentation in English upstream, so this page points you to the authoritative sources first. Below them you will find the English translations produced by this site.

## Official documentation

<ul class="listing">
    <li class="listing-item"><a href="https://www.jenkins.io/doc/" target="_blank">Jenkins User Documentation</a></li>
    <li class="listing-item"><a href="https://www.jenkins.io/doc/book/" target="_blank">Jenkins Handbook</a></li>
    <li class="listing-item"><a href="https://www.jenkins.io/doc/book/pipeline/syntax/" target="_blank">Pipeline syntax reference</a></li>
    <li class="listing-item"><a href="https://plugins.jenkins.io/" target="_blank">Jenkins Plugins index</a></li>
    <li class="listing-item"><a href="https://www.jenkins.io/doc/developer/" target="_blank">Extending Jenkins</a></li>
    <li class="listing-item"><a href="https://www.jenkins.io/doc/book/installing/" target="_blank">Installing Jenkins</a></li>
    <li class="listing-item"><a href="https://www.jenkins.io/security/" target="_blank">Jenkins Security Advisories</a></li>
</ul>

## Reference manuals on this site

<ul class="listing">
    <li class="listing-item"><a href="{{ '/wiki/bash/' | prepend: site.baseurl | prepend: site.url }}">Bash Reference Manual</a></li>
    <li class="listing-item"><a href="{{ '/wiki/coreutils/' | prepend: site.baseurl | prepend: site.url }}">GNU Coreutils Manual</a></li>
    <li class="listing-item"><a href="{{ '/wiki/rfc2616/' | prepend: site.baseurl | prepend: site.url }}">RFC 2616: HTTP/1.1</a></li>
    {% for wiki in site.wiki_en %}
    <li class="listing-item"><a href="{{ wiki.url | prepend: site.baseurl | prepend: site.url }}">{{ wiki.title }}</a></li>
    {% endfor %}
</ul>

## Translated articles

<ul class="listing">
    {% assign en_posts = site.posts_en | sort: "date" | reverse %}
    {% for post in en_posts %}
    <li class="listing-item"><a href="{{ post.url | prepend: site.baseurl | prepend: site.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>
