---
layout: post
published: true
title: The future of the Web. WebAssembly
image: img/WebAssembly.jpg
tags:
  - WebAssembly
  - Js
  - Web
---
![WebAssembly]({{site.baseurl}}/img/WebAssembly.jpg)

## The future is coming 

Evolution is everywhere. Even in web stack, there are changes which were made to update the current status of development up to the new edge. We are involved in this process not only as spectators but as essential parts - we got async/await, promises, iterators, etc. Now, from March 2017 (for Chrome) we can use WebAssembly directly in our web apps. But let's start from the beginning - why, what and where are our best friends in our way of WebAssembly ambassadors.

## What is WebAssembly

**Web Assembly (WASM)** - its a new binary format which allows us to run our code directly in our browsers. 

### Problem

Why it was invented and what is the problem was solved by WASM? It's easy - our code should be faster in our browsers. But its not only full problem - it consists of next sub-problems:

- Our code should be faster for JS (almost like a direct code in CPU)
- Zero configuration - solution should be "out from the box" - no special installations, the only browser required
- Security - new technology should be safe
- Cross-platform - desktop, mobile, tablet
- Easy to use and development 

### What is wrong with JS?

Nothing. But due to its design, it is not possible to make it faster. A long way and combination of interpreter and compiler at runtime makes JS 'hard predictable' in execution. Eg. - you have a function `foo(a,b)`. And you run this function a lot of times only with numbers. From some time interpreter push this code to the compiler, and the compiler will provide machine code, which are super fast for calculation. But if you will pass a string as parameters, an engine will make 'de-optimization': this function will be shifted back to an interpreter and ready-state machine code will throw away.

![JsRuntime]({{site.baseurl}}/img/js-runway.png)


## WebAssembly goals

WASM is aimed to fix troubles, described above:

- Speed. WASM executed almost with native speed of CPU
- Effectivity. Binary format, fast parsing, and compilation.
- Security. Run in the sandbox.
- Open standard. Was accepted in 2017
- Debug is supporting natively in browsers.

