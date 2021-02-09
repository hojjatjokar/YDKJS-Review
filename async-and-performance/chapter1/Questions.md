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

## 5. How `setTimeout()` works?

It's important to note that `setTimeout(..)` doesn't put your callback on the event loop queue. What it does is set up a timer; when the timer expires, the environment places your callback into the event loop, such that some future tick will pick it up and execute it.

What if there are already 20 items in the event loop at that moment? Your callback waits. It gets in line behind the others -- there's not normally a path for preempting the queue and skipping ahead in line. This explains why `setTimeout(..)` timers may not fire with perfect temporal accuracy. You're guaranteed (roughly speaking) that your callback won't fire *before* the time interval you specify, but it can happen at or after that time, depending on the state of the event queue.

## 6. What's difference between parallel and async?

Async is about the gap between now and later. But parallel is about things being able to occur simultaneously.

## 7. What are processors and threads as parallel computing tools?

The most common tools for parallel computing are processes and threads. Processes and threads execute independently and may execute simultaneously: on separate processors, or even separate computers, but multiple threads can share the memory of a single process.

## 8. How event loop works due to serialism or parallelism?

An event loop, by contrast, breaks its work into tasks and executes them in serial, disallowing parallel access and changes to shared memory. Parallelism and "serialism" can coexist in the form of cooperating event loops in separate threads.
