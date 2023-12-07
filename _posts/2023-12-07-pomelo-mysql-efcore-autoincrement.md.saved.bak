---
layout: post
title: "Creating AUTO_INCREMENT columns with Pomelo.EntityFrameworkCore.MySql"
date: 2023-12-07 13:37:00 +0100
categories: MySql MariaDB .Net EF.Core Migrations
---
I couldn't make `AUTO_INCREMENT` work when creating migrations for MySql database using `Pomelo.EntityFrameworkCore.MySql`.

It works for Sql Server, or SQLite, but for some reason doesn't work with MySql, which means it also doesn't work with MariaDB (same connector).

Quick search around the Internet showed that I'm not the only one with that problem.

Most of people default to creating custom migrators that will look for an atribute and set `AUTO_INCREMENT` on a column.

Somehow it doesn't look very nice and "universal enough" to me, so I opted out for another solution.

In the migration I use for creating a new table that should have autoincrement I add this part of the code:

{% highlight c# %}
protected override void Up(MigrationBuilder migrationBuilder)
{
    migrationBuilder.AlterDatabase()
        .Annotation("MySQL:Charset", "utf8mb4");

    migrationBuilder.CreateTable(...my table...);

    // now I execute SQL that will set AUTO_INCREMENT

    migrationBuilder.Sql("ALTER TABLE `Podcasts` MODIFY COLUMN `Id` int(11) auto_increment NOT NULL;");

    migrationBuilder.CreateTable(...my second table that has PK relationship with the first one...);

    migrationBuilder.CreateIndex(
        name: "IX_Episodes_PodcastSerieId",
        table: "Episodes",
        column: "PodcastSerieId");

    migrationBuilder.Sql("ALTER TABLE `Episodes` MODIFY COLUMN `Id` int(11) auto_increment NOT NULL;");
}
{% endhighlight %}

The second table uses `Id` from the first one as the foreign key.

That means I can't run both `ALTER TABLE` SQL querries at the end of the migration.

I have to run the first one before creating the second table.