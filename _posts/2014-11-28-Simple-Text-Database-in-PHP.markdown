---
layout: post
title:  "Simple Text File Database in PHP"
subtitle: "Create and maintain a sequential text database in PHP"
date:   2014-11-28 16:20:40
tags:
  - PHP
  - Text database
  - PHP programming
categories: jekyll update
---
Sometimes you need to capture data sequentially without structured tables or relationships. In this case a SQL database is overkill and unnecessarily complex for the task at hand.  

To see the demo click [here].

This project has two components: a text file we use as database and a HTML/PHP page.
For simplicity I separated the files into HTML and PHP.

* Text file: *data.txt*
* HTML: *index.html*
* PHP engine: *databaseAction.php*

**Note:** *the HTML and PHP file can be combined in one single PHP file that calls itself with the use of the $_SERVER['PHP_SELF'] variable (this is what I did in the live demo).*

##How it works##
The  HTML page calls the PHP script to manipulate the text database. Simple and effective.

The actions we can perform on the database are the following:
1.Add a new record (sequentially)
2. Empty the database
3. Display all the records in the database (all the lines in the text file) with the option to delete a selected line 




















[here]: http://www.paini.org/federico/TextDatabase/index.php