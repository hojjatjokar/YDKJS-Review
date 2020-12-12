# Chapter 7

1. ### What approach closure has been builds on?

Closure builds on this approach: for variables we need to use over time, instead
of placing them in larger outer scopes, we can encapsulate (more narrowly scope)
them but still preserve access from inside functions, for broader use. Functions
remember these referenced scoped variables via closure.

2. ### How can closured be observed?

For closure to be observed, a function must be invoked, and specifically it must
be invoked in a different branch of the scope chain from where it was originally
defined. A function executing in the same scope it was defined would not exhibit
any observably different behavior with or without closure being possible; by the
observational perspective and definition, that is not closure.

3. ### How closure works in arrow functions?

Because of how terse the syntax for `=>` arrow functions is, it's easy to forget
that they still create a scope. The `student => student.id == studentID` arrow
function is creating another scope bubble inside the `greetStudent(..)` function
scope.

It's just important not to skip over the fact that **even tiny arrow functions
can get in on the closure party.**

4. ### Explain how closure works in this example?

```
  function adder(num1) {
      return function addTo(num2){
          return num1 + num2;
      };
  }

  var add10To = adder(10);
  var add42To = adder(42);

  add10To(15);    // 25
  add42To(9);     // 51
```

closure is associated with an instance of a function, rather than its single
lexical definition. In the preceding snippet, there's just one
inner `addTo(..)` function defined inside `adder(..)`, so it might seem like
that would imply a single closure.

But actually, every time the outer `adder(..)` function runs,
a *new* inner `addTo(..)` function instance is created, and for each new
instance, a new closure. So each inner function instance
(labeled `add10To(..)` and `add42To(..)` in our program) has its own closure
over its own instance of the scope environment from that execution
of `adder(..)`.

Even though closure is based on lexical scope, which is handled at compile-time,
closure is observed as a runtime characteristic of function instances.

5. ### Does accessing to variable via closure is snapshot or real link?

We **read the value from a variable** that was held in a closure. That makes it
feel like closure might be a snapshot of a value at some given moment. Indeed,
that's a common misconception.

Closure is actually a live link, preserving access to the full variable itself.
We're not limited to merely reading a value; the closed-over variable can be
updated (re-assigned) as well! By closing over a variable in a function, we can
keep using that variable (read and write) as long as that function reference
exists in the program, and from anywhere we want to invoke that function. This
is why closure is such a powerful technique used widely across so many areas of
programming!

6. ### Explain the code?

```
var keeps = [];

for (var i = 0; i < 3; i++) {
    keeps[i] = function keepI(){
        // ??
        return i;
    };
}

keeps[0]();   // ?
keeps[1]();   // ?
keeps[2]();   // ?
```

7. ### What are common closures?

Common Closures: Ajax and Events

8. ### Does global scope variables need closure, why ?

All function invocations can access global variables, regardless of whether
closure is supported by the language or not. Global variables don't need to be
closed over.

9. ### Does variables that are never access result in closure?

Variables that are merely present but never accessed don't result in closure.

10. ### What's closure?

Closure is observed when a function uses variable(s) from outer scope(s) even
while running in a scope where those variable(s) wouldn't be accessible.

The key parts of this definition are:

- Must be a function involved
- Must reference at least one variable from an outer scope
- Must be invoked in a different branch of the scope chain from the variable(s)

11. ### What's closure lifecycle and garbage collection?

Since closure is inherently tied to a function instance, its closure over a
variable lasts as long as there is still a reference to that function.

If ten functions all close over the same variable, and over time nine of these
function references are discarded, the lone remaining function reference still
preserves that variable. Once that final function reference is discarded, the
last closure over that variable is gone, and the variable itself is GC'd.

This has an important impact on building efficient and performant programs.
Closure can unexpectedly prevent the GC of a variable that you're otherwise done
with, which leads to run-away memory usage over time. That's why it's important
to discard function references (and thus their closures) when they're not needed
anymore.

12. ### Explain this snippet of code in context of closure lifecycle and garbage collection?

```
function manageBtnClickEvents(btn) {
    var clickHandlers = [];

    return function listener(cb){
        if (cb) {
            let clickHandler =
                function onClick(evt){
                    console.log("clicked!");
                    cb(evt);
                };
            clickHandlers.push(clickHandler);
            btn.addEventListener(
                "click",
                clickHandler
            );
        }
        else {
            // passing no callback unsubscribes
            // all click handlers
            for (let handler of clickHandlers) {
                btn.removeEventListener(
                    "click",
                    handler
                );
            }

            clickHandlers = [];
        }
    };
}

// var mySubmitBtn = ..
var onSubmit = manageBtnClickEvents(mySubmitBtn);

onSubmit(function checkout(evt){
    // handle checkout
});

onSubmit(function trackAction(evt){
    // log action to analytics
});

// later, unsubscribe all handlers:
onSubmit();
```

In this program, the inner `onClick(..)` function holds a closure over the
passed in `cb` (the provided event callback). That means
the `checkout()` and `trackAction()` function expression references are held via
closure (and cannot be GC'd) for as long as these event handlers are subscribed.

When we call `onSubmit()` with no input on the last line, all event handlers are
unsubscribed, and the `clickHandlers` array is emptied. Once all click handler
function references are discarded, the closures of `cb` references
to `checkout()` and `trackAction()` are discarded.

13. ### How is impact of unsubscribing event handler on performance?

When considering the overall health and efficiency of the program, unsubscribing
an event handler when it's no longer needed can be even more important than the
initial subscription!

14. ### Does closure preserve only to the referenced outer variable(s), or does closure preserve the entire scope chain with all its variables?

Conceptually, closure is **per variable** rather than *per scope*. Ajax
callbacks, event handlers, and all other forms of function closures are
typically assumed to close over only what they explicitly reference.

But the reality is more complicated than that.

Many modern JS engines do apply an *optimization* that removes any variables
from a closure scope that aren't explicitly referenced. However, as we see
with `eval(..)`, there are situations where such an optimization cannot be
applied, and the closure scope continues to contain all its original variables.
In other words, closure must be *per scope*, implementation wise, and then an
optional optimization trims down the scope to only what was closed over (a
similar outcome as *per variable* closure).

15. ### Why Closure?

Two similar techniques from the Functional Programming (FP) paradigm that rely
on closure are **partial application** and **currying.**

Briefly, with these techniques, we alter the *shape* of functions that require
multiple inputs so some inputs are provided up front, and other inputs are
provided later; the initial inputs are remembered via closure. Once all inputs
have been provided, the underlying action is performed.

By creating a function instance that encapsulates some information inside (via
closure), the function-with-stored-information can later be used directly
without needing to re-provide that input. This makes that part of the code
cleaner, and also offers the opportunity to label partially applied functions
with better semantic names.

16. ### What are partial application and currying?

Briefly, with these techniques, we alter the shape of functions that require
multiple inputs so some inputs are provided up front, and other inputs are
provided later; the initial inputs are remembered via closure. Once all inputs
have been provided, the underlying action is performed.
