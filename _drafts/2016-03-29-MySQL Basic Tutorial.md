---
published: false
title: MySQL Basic Tutorial
description: MySQL Basic Tutorial
tags: [MySQL, Ubuntu]
modified:
layout: post
date: 2016-03-29 13:00:00
image:
  feature: code-wallpaper-18.png
  credit: Unknown
  creditlink: http://wonderfulengineering.com/37-programmer-code-wallpaper-backgrounds-free-download/
  background: witewall_3.png
---

We will be croving the basic setup of the MySQL server using Ubuntu along with creating a simple database with a table.

## MySQL Basic Tutorial

When working with database thinking logically is a skillet that is refined over time with practice. The key is to build a database in  such a way where you can extract the answers of a possible questions.

Setting up the MySQL Environment

Ubuntu:
{% highlight bash %}
sudo apt-get update
{% endhighlight %}

If you don't have MySQL installed on your environment then,

{% highlight bash %}
sudo apt-get install mysql-server
{% endhighlight %}

To access the MySQL shell type the following:
{% highlight bash %}
mysql -u root -p
{% endhighlight %}

Next, run {% highlight bash %}SHOW DATABASES; {% endhighlight %} The results shouls look something like this.

{% highlight bash %}
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| c9                 |
| mysql              |
| performance_schema |
| phpmyadmin         |
+--------------------+
5 rows in set (0.01 sec)
{% endhighlight %}

Creating a database is very simple:
{% highlight bash %}
CREATE DATABAE database name;
{% endhighlight %}

For example, lets create a databaes that will tracking people that are attending a bussiness meeting.
Lets create a databaes called "meetings"

{% highlight bash %}
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| c9                 |
| meetings           |
| mysql              |
| performance_schema |
| phpmyadmin         |
+--------------------+
6 rows in set (0.00 sec)
{% endhighlight %}

## *Note 
In MySQL, deleting or to "Drop" an object is done easily as well. For example, {% highlight bash %} DROP DATEBASE database name;{% endhighlight %}

## How to Acees the MySQL Database
Once you've created the database called "meetings", we can start the process of building the tables and adding data within those tables.

First, lets open up the databaes with the following command:

{% highlight bash %}USE meetings;{% endhighlight %}

Currently, our database doesn't have any tables in it. You can see that by typing the following command:

{% highlight bash %}SHOW tables;{% endhighlight %}

## Creating the MySQL Table

Lets starting by creating the structure or schema for the table. This will hold basic information for the attends of the meeting.
{% highlight sql %}
CREATE TABLE STAFF (id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
name VARCHAR(20),
department VARCHAR(30),
confirmed CHAR(1), 
signin_date DATE);
{% endhighlight %}

Now lets take a look at each line within this syntax.

1. The "CREATE" <--- Creadted the table (simple enought right?)
2. There where 5 tables created in this table  where, **id**, **name**, **department**, **confirmed** and **signin_date**.
3. The **id** column is a little special because of the **INT NOT NULL PRIMARY KEY AUTO_INCREMENT** which essentially inserts a number into each row when it is created/added to the table.
4. Then **name** column is limited by the  **VARCHAR** statement to be no more than 20 characters in length. As a side note, the **VARCHAR** statement can have a specified lenght value from 0 to 65,535.
5. to get more information on the CHAR and VARCHAR types, go to [MySQL.com](http://dev.mysql.com/doc/refman/5.7/en/char.html) for more information.

