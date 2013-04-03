---
layout: post
title: "Equal Operators: The Case of Mistaken Identity in JS"
date: 2013-03-17 18:35
comments: true
categories: 
---

A little tidbit I learned about Javascript and the equal operator:

'=' denotes assignment. 

Example: var x = 10;

'==' compares two values and returns a boolean (true or false). 

Example: 10 == '10' // returns true

'===' compares both the values AND the type of the data. 

Example: 10 === '10' // returns false

It's important to know which operator to use to get the results you expect!