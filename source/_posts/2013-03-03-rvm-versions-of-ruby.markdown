---
layout: post
title: "Setting a Default Version of Ruby"
date: 2013-03-03 17:09
comments: true
categories: 
---

Have you ever experienced the problem of using your Terminal to run some Ruby code only to realize that you're not using the version of Ruby that you want? And although you have the latest version installed, Terminal somehow keeps mysteriously reverting to a different version? 

I came across this issue a couple of weeks ago and learned that it's good practice to explicitly set a default version of Ruby to avoid unexpected results. This is where the Ruby Version Manager (RVM), a tool for installing and managing several different versions and implementations of Ruby on one computer, comes in really handy.

Once you have <a href="https://rvm.io/rvm/install/">RVM installed</a>, go into your terminal and type "rvm list" to see all the versions of Ruby that are installed on your computer.

The output also tells you what version you're currently using and what the default version is if there is one set.

<img src="/images/rvm_list.png">

To set a specific version of Ruby, say the latest version (currently 1.9.3-p374), as your default, type:

<code>rvm use ruby-1.9.3-p374 --default</code>

You can always change the current version that you're using or the default by repeating these steps.