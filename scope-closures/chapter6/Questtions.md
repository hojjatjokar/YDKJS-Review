# Chapter 6

1. ## Why do we need blocks to create scopes as well?

2. ### What's The Principle of Least Privilege?
   Software engineering articulates a fundamental discipline, typically applied
   to software security, called "The Principle of Least Privilege" (POLP).
   [^polp] And a variation of this principle that applies to our current
   discussion is typically labeled as "Least Exposure" (POLE).

POLP expresses a defensive posture to software architecture: components of the
system should be designed to function with **least privilege**, **least
access**, **least exposure**. If each piece is connected with minimum-necessary
capabilities, the overall system is stronger from a security standpoint, because
a compromise or failure of one piece has a minimized impact on the rest of the
system.

In following POLE, what do we want to minimize the exposure of? Simply: the
variables registered in each scope.

3. ### Why shouldn't you just place all the variables of your program out in the global scope?

- **Naming Collisions**
- **Unexpected Behavior**: if you expose variables/functions whose usage is
  otherwise *private* to a piece of the program, it allows other developers to
  use them in ways you didn't intend, which can violate expected behavior and
  cause bugs.
- **Unintended Dependency**: if you expose variables/functions unnecessarily, it
  invites other developers to use and depend on those
  otherwise *private* pieces. While that doesn't break your program today, it
  creates a refactoring hazard in the future, because now you cannot as easily
  refactor that variable or function without potentially breaking other parts of
  the software that you don't control.

4. ### The POLP express that components of the system should be designed to function with what?

- **least privilege**
- **least access**
- **least exposure**

5. ### POLP and POLE focus on a which level?

POLP focuses on **system-level** component design,

POLE *Exposure* variant focuses on a **lower level**; we'll apply it to how
scopes interact with each other.

6. ### What POLE says when applied to scoping?

   POLE, as applied to variable/function scoping, essentially says, default to
   exposing the bare minimum necessary, keeping everything else as private as
   possible. Declare variables in as small and deeply nested of scopes as
   possible, rather than placing everything in the global (or even outer
   function) scope.

7. ### How can hiding `var` or `function` declarations in scopes?

That can easily be done by wrapping a function scope around a declaration.

8. ### What's memoization?

The illustrated technique—caching a function's computed output to optimize
performance when repeated calls of the same inputs are expected—is quite common
in the Functional Programming (FP) world, canonically referred to as
"memoization"; this caching relies on closure.

9. ### What's Invoking Function Expressions Immediately?

Notice that we surrounded the entire `function` expression in a set of `( .. )`,
and then on the end, we added that second `()` parentheses set; that's actually
calling the `function` expression we just defined. Moreover, in this case, the
first set of surrounding `( .. )` around the function expression is not strictly
necessary (more on that in a moment), but we used them for readability sake
anyway.

So, in other words, we're defining a `function` expression that's then
immediately invoked. This common pattern has a (very creative!) name:
Immediately Invoked Function Expression (IIFE).

10. ### What's usage of IIFE?

    An IIFE is useful when we want to create a scope to hide
    variables/functions. Since it's an expression, it can be used
    in **any** place in a JS program where an expression is allowed. An IIFE can
    be named, or (much more commonly!) unnamed/anonymous. And it can be
    standalone or, as before, part of another statement.

11. ### How IIFE can effect Function Boundaries?
    Beware that using an IIFE to define a scope can have some unintended
    consequences, depending on the code around it. Because an IIFE is a full
    function, the function boundary alters the behavior of certain
    statements/constructs.

For example, a `return` statement in some piece of code would change its meaning
if an IIFE is wrapped around it, because now the `return` would refer to the
IIFE's function. Non-arrow function IIFEs also change the binding of
a `this` keyword. And statements like `break` and `continue` won't operate
across an IIFE function boundary to control an outer loop or block.

So, if the code you need to wrap a scope around has `return`, `this`, `break`,
or `continue` in it, an IIFE is probably not the best approach. In that case,
you might look to create the scope with a block instead of a function.

12. ### What's block scope?

In general, any `{ .. }` curly-brace pair which is a statement will act as a
block, but **not necessarily** as a scope.

A block only becomes a scope if necessary, to contain its block-scoped
declarations (i.e., `let` or `const`).

13. ### Does all { .. } curly-brace pairs create blocks and thus are eligible to become scopes?

Not all { .. } curly-brace pairs create blocks (and thus are eligible to become
scopes)

14. ### When { .. } curly-brace pairs won't create scope blocks?

- Object literals use `{ .. }` curly-brace pairs to delimit their key-value
  lists, but such object values are **not** scopes.
- `class` uses `{ .. }` curly-braces around its body definition, but this is not
  a block or scope.
- A `function` uses `{ .. }` around its body, but this is not technically a
  block—it's a single statement for the function body. It *is*, however, a
  (function) scope.
- The `{ .. }` curly-brace pair on a `switch` statement (around the set
  of `case` clauses) does not define a block/scope.

15. ### Are explicit standalone { .. } blocks have valid JS syntax?

Explicit standalone { .. } blocks have always been valid JS syntax, but since
they couldn't be a scope prior to ES6's let/const, they are quite rare. However,
post ES6, they're starting to catch on a little bit.

16. ### What's the usage of standalone { .. } blocks?
    Post ES6, they're starting to catch on a little bit.
17. ### Does catch clause in try...catch have block scope?

Since the introduction of `try..catch` back in ES3 (in 1999), the `catch` clause
has used an additional (little-known) block-scoping declaration capability

ES2019 (recently, at the time of writing) changed `catch` clauses so their
declaration is optional; if the declaration is omitted, the `catch` block is no
longer (by default) a scope; it's still a block, though!

So if you need to react to the condition that an exception occurred (so you can
gracefully recover), but you don't care about the error value itself, you can
omit the catch declaration:

18. ### What happens when function declarations that appear directly inside blocks? (FiB = Function in Block)?

The JS specification says that function declarations inside of blocks are
block-scoped. However, most browser-based JS engines (including v8, which comes
from Chrome but is also used in Node) will behave as, meaning the identifier is
scoped outside the if block but the function value is not automatically
initialized, so it remains `undefined`.

19. ### What do you expect for this program to do?

```
if (false) {
    function ask() {
        console.log("Does this run?");
    }
}
ask();
```

ANSWER:

What do you expect for this program to do? Three reasonable outcomes:

1. The `ask()` call might fail with a `ReferenceError` exception, because
   the `ask` identifier is block-scoped to the `if` block scope and thus isn't
   available in the outer/global scope.
2. The `ask()` call might fail with a `TypeError` exception, because
   the `ask` identifier exists, but it's `undefined` (since the `if` statement
   doesn't run) and thus not a callable function.
3. The `ask()` call might run correctly, printing out the "Does it run?"
   message.

The JS specification says that `function` declarations inside of blocks are
block-scoped, so the answer should be (1). However, most browser-based JS
engines (including v8, which comes from Chrome but is also used in Node) will
behave as (2), meaning the identifier is scoped outside the `if` block but the
function value is not automatically initialized, so it remains `undefined`.

20. ### Why are browser JS engines allowed to behave contrary to the specification in FiB?

Because these engines already had certain behaviors around FiB before ES6
introduced block scoping, and there was concern that changing to adhere to the
specification might break some existing website JS code. As such, an exception
was made in Appendix B of the JS specification, which allows certain deviations
for browser JS engines (only!).

21. ### What's best practice using FiB?

FiB is not worth it, and should be avoided.
