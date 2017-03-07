---
layout: post
title: "Owin and Katana. First view"
date: 2015-06-15 23:35:35 +0300
comments: true
categories: [Owin, Katana]
---

I think a lot of developers meet OWIN and Katana titles into different articles and presentation from Microsoft.
Let’s try to understand that is this and how we can cook it.

##A bit of history
Let`s look on classical ASP.NET application. Main characteristic of this application is that it has dependencies from System.Web
This assembly is a part of .NET Framework and, in general, represents a functionality of IIS. It can be represented in next way:
<!--more-->

![Owin and Katana](http://www.codeguru.com/imagesvr_ce/9947/OWIN_Katana_Figure01.png)

The main disadvantage here is that we have strong dependencies from System.Web. It means that to move it to a different type of server (e.g. self-hosted server) without any changes is impossible.

Next obstacle is more complicated. As I mentioned before - System.Web is a part of .NET Framework, so its releases will be at the same time as in Framework. With current temp of web development it’s a long term.

Developers in Microsoft decided to change this situation. First step became to create NuGet and ASP.NET MVC library. Last one has faster development cycle than core libraries. After that,  Microsoft created ASP.NET Web API, which hasn`t any dependencies from System.Web. Finally, they represent a signalR with similar properties.

It became clear that we required some abstraction, represented a server by itself and allowed to build personal pipeline for request processing. 

##Owin 
OWIN (Open Web Interface for .NET) - specification (neither a library nor platform!), defined the interface that eliminates the strong coupling web application to a particular server implementation. Basically, we can represent it in next way:

![Owin](http://farm4.static.flickr.com/3784/8895179754_3f52e9db7a.jpg)

---------
 
 This is allowed us to run an application on different platforms, supported OWIN, without changes. It used different modules, created by developers. In its turn, specification declares the interaction interface with the server. The main part of it is this delegate:

```
using App = Func<IDictionary<string,object>, Task>
```

He is responsible for a processing the request to the server. Parameter `IDictionary<string, object>` contains current environment, request and response. The result of this operation is Task, i.e. some executable task.
At the time of launching the web application developer configure a chain of working modules for processing request. Thus, we use only the required functionality.  

It may seem that new application required a lot of code. Besides, we need a presentation of OWIN for target server. Here comes to help Katana project.

##Katana
Katana is a realization of OWIN specification, which:

 * Helped us to work with our app in such way as for IIS.
 * Gives us helper methods that simplify the creation of modules for OWIN.

Within its framework have been developed and are available modules and WebAPI signalR.

Many of readers can ask: Need we start to study everything from scratch. The answer is NO. These features are using only in code, that related to server. For example - in Global.aspx. Instead we got new class Startup for module`s configuration.