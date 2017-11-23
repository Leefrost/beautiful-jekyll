---
layout: post
published: true
title: The future of the Web. WebAssembly
tags:
  - WebAssembly
  - Js
  - Web
bigimg: /img/webassembly-native.png
subtitle: What? Why? How?
---
Today is very important to work with the information in fast and understandable manner. If in case of desktop application situation is fine with it, in case of Web we get some troubles - all data are under control of JS, which is fast but not in the top of the performance charts. Here, on the scene, we meet WebAssembly.

## The future is coming 

Evolution is everywhere. Even in web stack, there are changes which were made to update the current status of development up to the new edge. We are involved in this process not only as spectators but as essential part - we got async/await, promises, iterators, etc. Now, from March 2017 (for Chrome) we can use WebAssembly directly in our web apps. But let's start from the beginning - "Why?", "What? and "How?" are our best friends in our way as WebAssembly ambassadors.

## What is WebAssembly

**Web Assembly (WASM)** - its a new binary format which allows us to run our code directly in our browsers. 

### Problem

Why it was invented and what is the problem that was solved by WASM? In general - our code should be faster in our browsers. But it is not a full problem - it consists of next sub-problems:

- Our code should be faster for JS (almost like a native code in CPU)
- Zero configuration - solution should be "out of the box" - no special installations, the only browser required
- Security - new technology should be safe and run inside sandbox
- Cross-platform - desktop, mobile, tablet
- Easy to use and develop

### What is wrong with JS?

Nothing. But due to its design, it is not possible to make it faster. A long way of development and combination of interpreter and compiler at runtime makes JS 'hardly predictable' in execution. E.g. you have a function `foo(a,b)`. And you run this function a lot of times only with numbers. After some time of execution, interpreter push this code to the compiler, and the compiler provides machine code, which is super fast for calculation. But if you will pass a string as parameter to `foo(a,b)`, an engine will make 'de-optimization': this function will be shifted back to an interpreter and ready-state machine code will be thrown away.

![JsRuntime]({{site.baseurl}}/img/js-runway.png){: .center-image }

### How WebAssembly will help us?

If web app performance is our main goal then we are speaking about code optimizations. If it is not enough and we are limited by JS engine we should move code responsible for the high-pressure operation to the WASM module. We re-write this code part to C or Rust and after compilation, we will get Module.wasm file. This file we will leave on the server and provide access to it from the browser. "How it will work next?" - the right question now. Next, inside our JS code, we request this module from the server. When it will be loaded and available, JS engine will call methods from this module. The code in this module will be executed in its own sandbox and result will be returned back to JS. We can think about WASM like about native modules in JS - but in this case code inside WASM module is executed not in JS engine. 

WASM has some restrictions - it is only can be accessible via JS. So, here is a bottleneck - heavyweight operations will be executed faster but we got some costs for passing and receiving data.  


## Conclusions

WASM is aimed to fix troubles, described above:

- Speed: WASM executed almost with the speed of machine code on the CPU
- Effectivity: binary format, fast parsing, and compilation. All heavyweight operation will be hidden in WASM module
- Security: sandbox model of execution 
- An open standard: WASM has its own format and specification. They are available with RFC on the Internet
- The code, inside of the module can be debugged natively from the browser console.

On my opinion WASM is the great feature. If it will be used smart enough, working with complicated calculation will be painless for us and browser. So apps, which are working with Graphics or CV becomes a native part of the web - and it is really cool. 




