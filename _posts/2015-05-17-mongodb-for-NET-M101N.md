---
title: M101N MongoDB for .NET 
tags: [mongo, .NET, mongodb, course, certification]
lang: en
ref: mongodb-net
---

I just finished the online course [M101N MongoDB for .NET](https://university.mongodb.com/courses/M101N/about) and I really enjoyed it. They combine short videos and a quiz after them checking you understood the explanation. There is also homework every week and a final exam.
I recommend it to every developer who wants to get to know this famous [NoSQL](http://www.mongodb.com/nosql-explained) database.

There are also [another possible courses](https://university.mongodb.com/courses/catalog) such as:

* MongoDB for Java developers
* MongoDB for Node.js developers
* MongoDB for DBAs
* ...

Querying in MongoDB is with *JavaScript* and it takes some time to set your mind to use it instead of SQL. I'll leave your with some SQL statements and the equivalent in MongoDB:

### Simple query

{% highlight SQL %}
SELECT *
FROM users
{% endhighlight %}

{% highlight Javascript %}
db.users.find()
{% endhighlight %}

### Filter

{% highlight SQL %}
SELECT *
FROM users
WHERE age > 25
AND   age <= 50
{% endhighlight %}

{% highlight Javascript %}
db.users.find(
   { age: { $gt: 25, $lte: 50 } }
)
{% endhighlight %}

### Filter and order

{% highlight SQL %}
SELECT *
FROM users
WHERE status = "A"
ORDER BY user_id DESC
{% endhighlight %}

{% highlight Javascript %}
db.users.find( { status: "A" } ).sort( { user_id: -1 } )
{% endhighlight %}