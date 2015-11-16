---
layout: post
title: "Swift Snippet: Comparing NSDate"
summary: "Swift snippet with an extension to NSDate to compare dates with the simple >, <, >= and <= operands."
date: 2015-11-16 16:00:00
categories: swift snippet nsdate
---


There may be a really good reason why `NSDate` doesn't implement the `Comparator` protocol. Until I can find out why, this is a snippet that enables the use of `>`, `<`, `=>` and `<=` with `NSDate`.

{% gist miguellara/28a06578c88cc50b10c6 %}
