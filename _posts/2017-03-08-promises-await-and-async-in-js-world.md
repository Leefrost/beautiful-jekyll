---
layout: post
published: false
title: Promises. Await and Async in JS world
subtitle: Asynchronous JS
---
## What is a Promise?

A promise is an object that may produce a single value some time in the future: either a resolved value, or a reason that it's not resolved (e.g., a network error occurred). A promise may be in one of 3 possible states: fulfilled, rejected, or pending. Promise users can attach callbacks to handle the fulfulled value or the reason for rejection.

Promises are eager, meaning that a promise will start doing whatever task you give it as soon as the promise constructor is invoked. If you need lazy, check out task or observables.

## An Incomplete Hsitory of Promises




Also to read:
- [Promise standart](https://promisesaplus.com/)