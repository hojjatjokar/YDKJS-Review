# Questions

## 1. Explain handling async with callback pattern?

```jsx
// A
ajax( "..", function(..){
	// C
} );
// B
```

`// A` and `// B` represent the first half of the program (aka the *now*), and `// C` marks the second half of the program (aka the *later*). The first half executes right away, and then there's a "pause" of indeterminate length. At some future moment, if the Ajax call completes, then the program will pick up where it left off, and *continue* with the second half.

In other words, the callback function wraps or encapsulates the *continuation* of the program.

## 2. How this code?

```jsx
// A
ajax( "..", function(..){
	// C
} );
// B
```

`// A` and `// B` represent the first half of the program (aka the *now*), and `// C` marks the second half of the program (aka the *later*). The first half executes right away, and then there's a "pause" of indeterminate length. At some future moment, if the Ajax call completes, then the program will pick up where it left off, and *continue* with the second half.

## 3. How this code works?

```jsx
// A
setTimeout(function () {
  // C
}, 1000);
// B
```

## 4. What problem does call back functions have ?

- Sequential brain
- Trust Issues

## 5. Explain Sequential brain?

Synchronous brain planning maps well to synchronous code statements.

How we express asynchrony (with callbacks) in our code doesn't map very well at all to that synchronous brain planning behavior.

We think in step-by-step terms, but the tools (callbacks) available to us in code are not expressed in a step-by-step fashion once we move from synchronous to asynchronous.

And **that** is why it's so hard to accurately author and reason about async JS code with callbacks: because it's not how our brain planning works.

## 6. What's callback hell?

```jsx
listen("click", function handler(evt) {
  setTimeout(function request() {
    ajax("http://some.url.1", function response(text) {
      if (text == "hello") {
        handler();
      } else if (text == "world") {
        request();
      }
    });
  }, 500);
});
```

We've got a chain of three functions nested together, each one representing a step in an asynchronous series.

This kind of code is often called "callback hell," and sometimes also referred to as the "pyramid of doom".

But "callback hell" actually has almost nothing to do with the nesting/indentation. It's a far deeper problem than that.
