---
layout: post
title: "MySql.Data and MySql.EntityFrameworkCore for MariaDB"
date: 2023-12-02 13:37:00 +0100
categories: MySql MariaDB .Net EF.Core nuget
---
Looks like `MySql.Data` and `MySql.EntityFrameworkCore` packages do not work with MariaDB and gives very strange error:

{% highlight exception %}
System.InvalidCastException: Object cannot be cast from DBNull to other types.
   at System.DBNull.System.IConvertible.ToInt32(IFormatProvider provider)
   at System.Convert.ToInt32(Object value, IFormatProvider provider)
   at MySql.Data.MySqlClient.Driver.LoadCharacterSets(MySqlConnection connection)
   at MySql.Data.MySqlClient.Driver.Configure(MySqlConnection connection)
   at MySql.Data.MySqlClient.MySqlConnection.Open()
{% endhighlight %}

Fix for that is quite easy. Just delete nuget reference to `MySql.Data` or `MySql.EntityFrameworkCore` and add reference to 
`MySqlConnector` (if you don't want EF Core), or `Pomelo.EntityFrameworkCore.MySql` (if you want EF Core).

Both connectors will work with MySql and MariaDB.

MySqlConnector will just work, Pomelo requires to change the way you connect to the database.

Instead of:
{% highlight c# %}
options.UseMySql(ConnectionString);
{% endhighlight %}

Use:
{% highlight c# %}
options.UseMySql(ConnectionString, ServerVersion.AutoDetect(ConnectionString));
{% endhighlight %}