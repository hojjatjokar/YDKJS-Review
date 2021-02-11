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

## 9. How threaded programming can be tricky?

if you don't take special steps to prevent this kind of interruption/interleaving from happening, you can get very surprising, nondeterministic behavior that frequently leads to headaches.

## 10. Does JS share data between threads?

No

## 11. Whats run-to-completion?

Because of JavaScript's single-threading, the code inside of `foo()` (and `bar()`) is atomic, which means that once `foo()` starts running, the entirety of its code will finish before any of the code in `bar()` can run, or vice versa. This is called "run-to-completion" behavior.

## 12. According to this code explain this situations:

```jsx
var a = 1;
var b = 2;

function foo() {
  a++;
  b = b * a;
  a = b + 3;
}

function bar() {
  b--;
  a = 8 + b;
  b = a * 2;
}

// ajax(..) is some arbitrary Ajax function given by a library
ajax("http://some.url.1", foo);
ajax("http://some.url.2", bar);
```

a. There are 3 chunks of code which of them are sync or async?

b. What result can be possibles ? ( how _deterministic_ can they be)

c. Can foo and bar interrupt each other?

## 13. What's race condition?

"race condition," as `foo()` and `bar()` are racing against each other to see which runs first. Specifically, it's a "race condition" because you cannot predict reliably how `a` and `b` will turn out.

When two function are racing against each other to see which runs first. Specifically, it's a race condition because you cannot predict reliably how the result will be

## 14. What's concurrency?

Concurrency is when two or more "processes" are executing simultaneously over the same period, regardless of whether their individual constituent operations happen in parallel (at the same instant on separate processors or cores) or not. You can think of concurrency then as "process"-level (or task-level) parallelism, as opposed to operation-level parallelism (separate-processor threads).

## 15. What's cooperative concurrency?

Here, the focus isn't so much on interacting via value sharing in scopes (though that's obviously still allowed!). The goal is to take a long-running "process" and break it up into steps or batches so that other concurrent "processes" have a chance to interleave their operations into the event loop queue.

## 16. What `setTimeout(..0)` does?

means "stick this function at the end of the current event loop queue."

**Note:** `setTimeout(..0)` is not technically inserting an item directly onto the event loop queue. The timer will insert the event at its next opportunity. For example, two subsequent `setTimeout(..0)` calls would not be strictly guaranteed to be processed in call order, so it *is* possible to see various conditions like timer drift where the ordering of such events isn't predictable. In Node.js, a similar approach is `process.nextTick(..)`. Despite how convenient (and usually more performant) it would be, there's not a single direct way (at least yet) across all environments to ensure async event ordering.

## 17. What is job (queue)?

So, the best way to think about this that I've found is that the "Job queue" is a queue hanging off the end of every tick in the event loop queue. Certain async-implied actions that may occur during a tick of the event loop will not cause a whole new event to be added to the event loop queue, but will instead add an item (aka Job) to the end of the current tick's Job queue.

It's kinda like saying, "oh, here's this other thing I need to do *later*, but make sure it happens right away before anything else can happen."

Or, to use a metaphor: the event loop queue is like an amusement park ride, where once you finish the ride, you have to go to the back of the line to ride again. But the Job queue is like finishing the ride, but then cutting in line and getting right back on.

## 18. compiler statement reordering? and why is that?

But it's *possible* that the JS engine, after compiling this code (yes, JS is compiled -- see the *Scope & Closures* title of this book series!) might find opportunities to run your code faster by rearranging (safely) the order of these statements. Essentially, as long as you can't observe the reordering, anything's fair game.
