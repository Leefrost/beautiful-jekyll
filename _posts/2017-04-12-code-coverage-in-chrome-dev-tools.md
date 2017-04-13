---
layout: post
published: true
title: Code coverage in Chrome Dev Tools
tags:
  - Chrome
  - Js
  - CSS
---
Code coverage is a new feature in Chrome Dev Tools (currently available in Canary) which is very helpful for testing not only JS but also CSS. So, I created a short demo session and here I will share a result of it.

##What does it do?

Code coverage lets you run your web app, and for each JS/CSS file, see which lines of code ran and which didn't.

![Coverage diagram for simple site in AGN cli]({{site.baseurl}}/img/CodeCoverage.png)


Here I run a simple page which used Angular CLI start up and recorded first 5 seconds. Red lines show a code which didn't executed during this period, green ones - code which executed in pipeline. 

Code coverage works like a typical timeline in dev tools - you just need to press a record button and make some actions with your site. After you finish all you work you should press stop button and chrome will take some time to make some calculation and will show data. For example you can check which CSS code is unused in your site or which js just take some traffic but does not work in production

Also Chrome support to show a detail information about file with coverage data. Same here - red lines are code which does not executed and green lines - executable code. If you have minified files you should  decompile it to normal way (Chrome support such operation) by pressing on button on left bottom corner

##Why its useful?

Large projects during development accumulate a dead code. If you use Webpack or other compilation system for JS you can skip dead code in production. But with CSS it is a little bit complicated. This feature helps a lot in daily working process for many developers

### Should to read

- Useful tips and tricks with dev tools: https://blog.logrocket.com/making-the-most-of-the-chrome-developer-tools-8cac9a206979
- Visualization of backend performance in Chrome DEV Tools: https://blog.logrocket.com/visualizing-backend-performance-in-the-chrome-devtools-bb6fd232540

