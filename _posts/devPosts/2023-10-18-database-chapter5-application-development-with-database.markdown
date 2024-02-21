---
layout: post
title: "[Database]Chapter5. Application Development with Database"
subtitle: "application development with database"
categories: dev
tags: database
comments: false
---

## Introduction
> Some tools to use for application developing with database.

- Contents
	- [User Interfaces and Tools](#user-interfaces-and-tools)
	- [Web Interfaces and Database](#web-interfaces-and-database)
	- [The basic concept of Web](#the-basic-concept-of-web)
	- [Servlets and JSP](#servlets-and-jsp)
	
## User Interfaces and Tools
---
The layers about database appliance can be divided into :

- Front-end : make user interface for using and accessing database. Today, most of user interfaces is based on Web.
- Middle Layer
- Back-end



## Web interfaces and Database

---
In 1960, there are terminals that can be connected with propietary network or dial up phone lines for mainframe computer.

Then in 1980 to 1990, there are personal PC that connect with Local Area Network to Database. So some company like Bank give users CD, which contains Local Area Network Program to connect Bank's database.

Nowaday, Web browers can connect to database with internet. So we can connect to database from anywhere.



Web browers is the standard of Database application these days, because it can support universal front end, make dynamic web page, can use hyperlink on HTML, etc.



## The basic concept of Web
---
- URL(Uniform Resource Locator) is like the pointer of Web.

  For example. 'http://www.acm.org/sigmod' is one of the URL. It can direct to unique web page.

- HTML(HyperText Markup Language) is the set of tags, which about the table, style sheet, pop-up menus, radio buttons, text boxes, etc.

  It can used to send user data inputs to server, and receive result from server.

- Client-Side Scripting : The language that can be executed on client's web browser. The most famous language of it is **Javascript**. It helps to compose active web page, which has flexible UI, animation, etc.

- HTTP(HyperText Transfer Protocol) is the protocol that can be used to connect within the Internet. As it doesn't save the data, Cookie and Session can be used to solve that issue.



## Servlets and JSP
---
Servlets and JSP is a web programming technology to use database.

- Java Servlets : A server side program that creates responses by HTTP request. Apache Tomcat is the most famous server to use Java Servlets.
- Server-Side Scripting : Making a web page dynamically from a server to a browser. JSP, PHP can be used for that.



