---
layout: post
title: "[JAVA]Chapter1. Let's start JAVA!"
subtitle: "let's start java"
categories: dev
tags: java
comments: false
---

## Introduction
> Introduce the JAVA language and show how can we start with.

- Contents
	- [The brief show of JAVA](#the-brief-show-of-java)
	- [How does it runs?](#how-does-it-runs)
	- [JDK? JRE?](#jdk-jre)
	- [The very first source code](#the-very-first-source-code)
	- [Useful development tool](#useful-development-tool)
  
## The Brief show of JAVA
---
JAVA is ont of the most famous programming language we use these days, made by James Gosling. It is one of the high-level programming language, which means human can easily understead a language, not like the hex code. It also can be used for procedure-programming language or object-oriended language.  
Now, in 2023, the newest its version is JAVA 20. But I will posts its grammer for much older version, because my lecture didn't handle a modern version of JAVA. In my lecture use JAVA 8, but it does not handle Lambda Expression and Stream!!! (What the...)  
Plus, you can find the ranking of programming languages in [TIOBE Index](https://www.tiobe.com/tiobe-index/). JAVA ranks 4th in 2023.

## How does it runs?
---
Progrmmers write JAVA source file, which ends with `.java` extension. Then, it compiles to a computer for understanding, which says complie. So JAVA source file change for `.class` extension.  
JAVA has JVM(Java Virtual Machine) to run its file on ANY HARDWARE. When it run, JAVA source file change to `Byte Code` that it can be run for any hardware and OS, while other programming languages is dependent in a specific platform. Note that C and C++ links and compiles .exe extension and loads for the entire program in menory, but JAVA does not. It does not links and makes .exe file and loads some parts of a program. JAVA required only compile.  

## JDK? JRE?
---
JDK(Java Development Kit) makes you a developing envionment, so <u>you must download it for writing source code.</u> Of course you can use it for running your program.  
JRE(Java Runtime Environment) is only do runs JAVA program. It only has JVM and its API.  

## The very first source code
---
After you downloaded JDK, let's write very simple the source code in nodepad. Once you write it, please save its names `Hello2030.java`  

```java
public class Hello2030 {
    public static void main(String[] args) {
        System.out.println("Hello");
    }
}
```

Then execute Command Prompt, and go its directory to `Hello2030.java`. Once you done it, you can complie it by `javac Hello2030.java` and runs it by `java Hello2030`. Let's see what happened.  

## Useful development tool
---
But.. everytime we can't use nodepad, so we will use more effective program for development, names [Eclipse](https://www.google.com/search?client=firefox-b-d&q=Eclipse). You can search informations how to download it, set it, and use it.