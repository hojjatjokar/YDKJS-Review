# Chapter 1

## 1. What is Async in programming?

It's about what happens when part of your program runs now, and another part of your program runs later -- there's a gap between now and later where your program isn't actively executing.
In fact, the relationship between the now and later parts of your program is at the heart of asynchronous programming.
Tasks that cannot complete now are, by definition, going to complete asynchronously, and thus we will not have blocking behavior as you might intuitively expect or want.

## 2. Is there specification for console.log() in JS? how they are added to JS?

There is no specification or set of requirements around how the console.\* methods work -- they are not officially part of JavaScript, but are instead added to JS by the hosting environment

## 3. How console.log() works?

In particular, there are some browsers and some conditions that console.log(..) does not actually immediately output what it's given. The main reason this may happen is because I/O is a very slow and blocking part of many programs (not just JS). So, it may perform better (from the page/UI perspective) for a browser to handle console I/O asynchronously in the background, without you perhaps even knowing that occurred.

## 4. what is the event loop?

In computer science, the event loop is a programming construct or design pattern that waits for and dispatches events or messages in a program. The event loop almost always operates asynchronously with the message originator.
The Event Loop has one simple job — to monitor the Call Stack and the Callback Queue. If the Call Stack is empty, the Event Loop will take the first event from the queue and will push it to the Call Stack, which effectively runs it.

So, in other words, your program is generally broken up into lots of small chunks, which happen one after the other in the event loop queue. And technically, other events not related directly to your program can be interleaved within the queue as well.
