---
layout: post
title: "Owin and Katana. Part 2"
date: 2015-07-05 21:54:39 +0300
comments: true
categories: [Owin, Katana]
---

Owin and Katana. Simple WebApi app
=====
In the second part we will create simple WebAPI application, based on OWIN.
Need to say, that Katana`s developers used [convention over configuration](https://en.wikipedia.org/wiki/Convention_over_configuration) instead of base types and interfaces. Also, they have promised that many of them will be redefinable. But in this time we will not dig deeper and will use default namespaces and values.

Prepare application
------
So, our task is create application that uses WebAPI. We will use IIS server as a default -  therefore we create empty web project (ASP.NET Empty Web Application). It does not meter for the Katana,  we just will have project with included `System.Web`  and configured for debugging in IIS Express. 

<!--more-->

With help of NuGet (Package Manager Console), we install WebAPI library for OWIN:
```
PM> Install-Package Microsoft.Asp.Net.WebApi.Owin -Prerelease 
```
Katana`s assembly ([Microsoft realization](previouspart) of OWIN specification) will be added into project automatically. Because it do not depend on the type of server, you must also include the library that implements OWIN for IIS (the other options considered in the next part):
```
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```
Preparing is done. Now it is time to consider the first of the agreements of Katana.

Agreement for the configuration of the conveyor of messages
-----
After application launch, Katana search `Startup` class and call method `Configuration()` for creating and configuration conveyor of messages:
```
public class Startup{
	public void Configuration(IAppBuilder app)
		//creating, configuration and installing modules
	}
}
```
`IAppBuilder` interface is used to specify the modules in use. For this, it is necessary to pass them as parameters in `app.Use()`. However, the `Microsoft.AspNet.WebApi.Owin` library adds its own extension method `UseWebApi()`, which facilitates its connection. 

As in usual web application, we need create configuration for correct work of WebAPI. Therefore we add new variable `config` and define simple route way - `{'controller'}`. As a result, we add next class to out project:
```
namespace OwinDemoPart2
{
    using System.Web.Http;
    using Owin;
 
    public class Startup
    {
        public void Configuration(IAppBuilder app)
        {
            var config = new HttpConfiguration();
            config.Routes.MapHttpRoute("default", "{controller}");
 
            app.UseWebApi(config);
        }
    }
}
```
Assume that the application needs to use multiple modules. Then, after `UseWebApi()`  we must add calls of `Use()` or other methods of  extensions. Their order determines the order in which the processing of the request and the formation of a response will be done. As you can see, everything is quite easy and clear.

Working with WebAPI
----
We just need to add controller. So, its time to create the `Controller` folder and add `HomeController` class. Let it returns random number in scope [0...10]:

```
namespace OwinDemoPart2.Controllers
{
    using System.Collections.Generic;
    using System.Linq;
    using System.Web.Http;
 
    public class HomeController : ApiController
    {
        public int GetNumber()
        {
	        var rand = new Random();
            return rand.Next(0, 10);
        }
    }
}
```
Run the app and knock to address:
```
http://localhost:[port]/Home
```
The answer will represent some random number. We can notice, that created app is more simply than default WebAPI.

In the next [part]() we deal with some details of the work of Katana more detail. In particular, we will write module, and change the type of server with IIS on a standalone application (self-host).