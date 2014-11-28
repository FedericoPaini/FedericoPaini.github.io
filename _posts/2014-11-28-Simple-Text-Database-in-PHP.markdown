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

###How it works
The  HTML page calls the PHP script to manipulate the text database. Simple and effective.

The actions we can perform on the database are the following:
1.Add a new record (sequentially)
2. Empty the database
3. Display all the records in the database (all the lines in the text file) with the option to delete a selected line

The record added will be in the form of *timestamp,note*, for example: 

1. `Wednesday Jun 11 2014 20:54:54,first record`
2. `Thursday Jun 12 2014 22:07:55,second record`
3. `Thursday Jun 12 2014 21:08:14,third record`

The HTML source code:

```
<head>
    <meta charset="utf-8" />
    <title>Text File Database Demo</title>
</head>
<body>

<form action="databaseAction.php" method="post">

Add a Record: <button type="submit"> Timestamp </button>
Notes: <input type="text" name="note">
<input type=hidden name=operation value=1>
<p></p>
</form>

<form action="databaseAction.php" method="post">
<input type=hidden name=operation value=2>
Clear Data: <button type="submit">Erase</button>
<p></p>
</form>

<form action="databaseAction.php" method="post">
<input type=hidden name=operation value=3>
Records in the Database: <button type="submit">Show</button>
<p></p>
</form>
```




















[here]: http://www.paini.org/federico/TextDatabase/index.php