---
layout: post
title: "Show invisible characters (whitespace) in Visual Studio 2022"
date: 2024-01-29 14:00:00 +0100
categories: space tab crlf visual studio
---

Whenever I edit already existing C# file, I try to clean it up and keep it in-sync with our current coding standards.

That also includes getting rid of all unnecessary white space characters (like space at the end of the line, or an empty line, but with 10 spaces there).

It's quite easy to spot it in Word or Notepad Plus Plus with white space characters visible. Obviously I will not set Word as my default C# editor, but fortunately it can be done in Visual Studio as well.

The command is called `Edit.ViewWhiteSpace` and `CTRL+R`, `CTRL+W` toggles it on/off.