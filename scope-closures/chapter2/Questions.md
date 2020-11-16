# Chapter 2

1. ### What scope models are there? Javascript has which one?

   There are two predominant models for how scope works. Lexical scope and
   Dynamic scope.

2. ### What's lexing?

   The first traditional phase of a standard language compiler is called lexing
   (aka, tokenizing). The lexing process examines a string of source code
   characters and assigns semantic meaning to the tokens as a result of some
   stateful parsing.

3. ### What's lexical scope?

   Lexical scope is scope that is defined at lexing time. In other words,
   lexical scope is based on where variables and blocks of scope are authored,
   by you, at write time, and thus is (mostly) set in stone by the time the
   lexer processes your code.

4. ### Highlight scopes?

```javascript
function foo(a) {
  var b = a * 2;

  function bar(c) {
    console.log(a, b, c);
  }

  bar(b * 3);
}

foo(2);
```

Bubble 1 encompasses the global scope, and has just one identifier in it: foo.

Bubble 2 encompasses the scope of foo, which includes the three identifiers: a,
bar and b.

Bubble 3 encompasses the scope of bar, and it includes just one identifier: c.

5. ### What's shadowing?
   The same identifier name can be specified at multiple layers of nested scope,
   which is called "shadowing" (the inner identifier "shadows" the outer
   identifier). Regardless of shadowing, scope look-up always starts at the
   innermost scope being executed at the time, and works its way outward/upward
   until the first match, and stops.
6. ### What's global variables? how can be accessed?

   Global variables are also automatically properties of the global object
   (window in browsers, etc.), so it is possible to reference a global variable
   not directly by its lexical name, but instead indirectly as a property
   reference of the global object. This technique gives access to a global
   variable which would otherwise be inaccessible due to it being shadowed.
   However, non-global shadowed variables cannot be accessed.

7. ### Where is function lexical scope?
   No matter where a function is invoked from, or even how it is invoked, its
   lexical scope is only defined by where the function was declared.
8. ### How many mechanism are there for cheating lexical scope?

   Two, **eval** and **with**

9. ### What's eval?

   The eval(..) function in JavaScript takes a string as an argument, and treats
   the contents of the string as if it had actually been authored code at that
   point in the program. In other words, you can programmatically generate code
   inside of your authored code, and run the generated code as if it had been
   there at author time.

10. ### How can you programatically generate code inside your authored code?
11. ### How engine behave to eval(...)?

    On subsequent lines of code after an eval(..) has executed, the Engine will
    not "know" or "care" that the previous code in question was dynamically
    interpreted and thus modified the lexical scope environment. The Engine will
    simply perform its lexical scope look-ups as it always does.

12. ### How eval(...) can modifies the existing lexical scope?

    Evaluating eval(..) (pun intended) in that light, it should be clear how
    eval(..) allows you to modify the lexical scope environment by cheating and
    pretending that author-time (aka, lexical) code was there all along.

13. ### How eval(...) behave in strict-mode?
    eval(..) when used in a strict-mode program operates in its own lexical
    scope, which means declarations made inside of the eval() do not actually
    modify the enclosing scope.
14. ### What's other facilities in javascript similar to **eval**? How they work? Which one is safer? Which one should be avoided?
    There are other facilities in JavaScript which amount to a very similar
    effect to eval(..). setTimeout(..) and setInterval(..) can take a string for
    their respective first argument, the contents of which are evaluated as the
    code of a dynamically-generated function. This is old, legacy behavior and
    long-since deprecated. Don't do it! The new Function(..) function
    constructor similarly takes a string of code in its last argument to turn
    into a dynamically-generated function (the first argument(s), if any, are
    the named parameters for the new function). This function-constructor syntax
    is slightly safer than eval(..), but it should still be avoided in your
    code.
15. ### What's **with** for?

    with is typically explained as a short-hand for making multiple property
    references against an object without repeating the object reference itself
    each time.

16. ### How is **with** work?

    The with statement takes an object, one which has zero or more properties,
    and treats that object as if it is a wholly separate lexical scope, and thus
    the object's properties are treated as lexically defined identifiers in that
    "scope".

17. ### How is impacts of **eval** and **with** on performance?
    Both eval(..) and with cheat the otherwise author-time defined lexical scope
    by modifying or creating new lexical scope at runtime. Most of those
    optimizations it would make are pointless if eval(..) or with are present,
    so it simply doesn't perform the optimizations at all.
