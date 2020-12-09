# Chapter 5

1. ### What's Hoisting?

Definitions:

- Variable being visible from the beginning of its enclosing scope, even though
  its declaration may appear further down in the scope.
- The typical assertion of what hoisting means: *lifting* any identifiers all
  the way to the top of a scope.

2. ### What's Function hoisting?

When a function declaration's name identifier is registered at the top of its
scope, it's additionally auto-initialized to that function's reference. That's
why the function can be called throughout the entire scope!

3. ### Where `function` and `var` variable attach their name identifiers to?

One key detail is that both `function` hoisting and `var` flavored variable
hoisting attach their name identifiers to the nearest enclosing function
scope (or, if none, the global scope), not a block scope.

4. ### Does declarations with let and const hoist? Where they attach their name identifiers to?

Declarations with `let` and `const` still hoist. But these two declaration forms
attach to their enclosing block rather than just an enclosing function as with
var and function declarations.

5. ### Does function expressions hoist?

Function hoisting only applies to function declarations, not to function
expression assignments.

6. ### Variables declared with var automatically initialized to what? and what scope type (function/block) does they have?

Variables declared with `var` are also automatically initialized
to `undefined` at the beginning of their scope—again, the nearest enclosing
function, or the global.

7. ### What's the rule of hoisting in order of hoisting parts?

The "rule" of the hoisting metaphor is that function declarations are hoisted
first, then variables are hoisted immediately after all the functions.

8. ### Is there such a thing as a variable being "re-declared" in the same scope?

   No

9. ### What will happen If compiler find second var declaration statement?

The compiler would find the second `var` declaration statement and ask the Scope
Manager if it had already seen that identifier; **since it had, there wouldn't
be anything else to do**.

A repeated `var` declaration of the same identifier name in a scope is
effectively a do-nothing operation.

10. ### What happen to declaration within a scope using `let` or `const`?

Declaration within a scope using `let` or `const` throw a `SyntaxError`.

11. ### What happens if there are two declarations involving `let` and `var` ?

It's not just that two declarations involving `let` will throw this error. If
either declaration uses `let`, the other can be either `let` or `var`, and the
error will still occur.

12. ### What is const ?

`const` cannot be repeated with the same identifier in the same scope. There's
actually an overriding technical reason why that sort of "re-declaration" is
disallowed, unlike let which disallows "re-declaration" mostly for stylistic
reasons.

13. ### What happen if omit assignment part of declaration with const ?

The `const` keyword requires a variable to be initialized, so omitting an
assignment from the declaration results in a `SyntaxError`

14. ### Can you re-assign a variable that is declared with const?

const declarations create variables that cannot be re-assigned.

15. ### Explain `let` behavior in loops?

All the rules of scope (including "re-declaration" of `let`created variables)
are applied *per scope instance*. In other words, each time a scope is entered
during execution, everything resets.

Each loop iteration is its own new scope instance, and within each scope
instance, the variable declared with `let` keyword is only being declared once.
So there's no attempted "re-declaration," and thus no error. Before we consider
other loop forms,

16. ### Explain var behavior in loops?

Is variable declared with `var` keyword being "re-declared" in each loop
iteration , especially since we know var allows it? No. Because `var` is not
treated as a block-scoping declaration, it attaches itself to the global scope.

17. ### Explain the code:

```
  for (let i = 0; i < 3; i++) {
      let value = i * 10;
      console.log(`${ i }: ${ value }`);
  }
```

Answer:

```
// 0: 0
// 1: 10
// 2: 20
```

It should be clear that there's only one `value` declared per scope instance.

Variable `i` scope is in the scope of `for` loop body, just like `value` is.

`i` and `value` variables are both declared exactly once **per scope instance**.
No "re-declaration" here.

18. ### Can you use const in loops?

`for..in` and `for..of` are fine to use with `const` but not the general
`for-loop`

19. ### What's TDZ?

The TDZ is the time window where a variable exists but is still uninitialized,
and therefore cannot be accessed in any way. Only the execution of the
instructions left by Compiler at the point of the original declaration can do
that initialization. After that moment, the TDZ is done, and the variable is
free to be used for the rest of the scope.

20. ### Does var, let, const has a TDZ?

A `var` also has technically has a TDZ, but it's zero in length and thus
unobservable to our programs! Only let and const have an observable TDZ.

21. ### Why TDZ errors occur?

TDZ errors occur because `let/const` declarations do hoist their declarations to
the top of their scopes, but unlike `var`, they defer the auto-initialization of
their variables until the moment in the code's sequencing where the original
declaration appeared. This window of time (hint: temporal), whatever its length,
is the TDZ.

22. ### Explain the code?

```
greeting();

function greeting() {
    console.log("Hello!");
}
```

This code works fine. You may have seen or even written code like it before. But
did you ever wonder how or why it works? Specifically, why can you access the
identifier greeting from line 1 (to retrieve and execute a function reference),
even though the greeting() function declaration doesn't occur until line 4?

23. ### Explain the code?

```
  greeting();

  var greeting = function greeting() {
      console.log("Hello!");
  };
```

24. ### Explain the code?

```
  greeting = "Hello!";
  console.log(greeting);
  // ??

  var greeting = "Howdy!";
```

25. ### Explain the code?

```
  studentName = "Suzy";
  greeting();

  // ??
  function greeting() {
      console.log(`Hello ${ studentName }!`);
  }
  var studentName;
```

26. ### Explain the code?

```
  function greeting() {
      console.log(`Hello ${ studentName }!`);
  }
  var studentName;

  studentName = "Suzy";
  greeting();
  // ??
```

27. ### Explain the code?

```
  var studentName = "Frank";
  console.log(studentName);
  // Frank

  var studentName;
  console.log(studentName);   // ???
```

28. ### Explain the code?

```
var studentName = "Frank";
console.log(studentName);   // ??

var studentName;
console.log(studentName);   // ??

var studentName = undefined;
console.log(studentName);   // ??
```

29. ### Explain the code?

```
var greeting;

function greeting() {
    console.log("Hello!");
}

// basically, a no-op
var greeting;

typeof greeting;        // ?

var greeting = "Hello!";

typeof greeting;        // ?
```

30. ### Explain the code?

```
  let studentName = "Frank";

  console.log(studentName);

  let studentName = "Suzy";
```

31. ### Explain the code?

```
var studentName = "Frank";

let studentName = "Suzy";
```

32. ### Explain the code?

```
let studentName = "Frank";

var studentName = "Suzy";
```

33. ### Explain the code?

```
const studentName = "Frank";
console.log(studentName);
// ??

studentName = "Suzy";
```

34. ### Explain the code?

```
  const studentName = "Frank";

  // ??
  const studentName = "Suzy";
```

35. ### Explain the code?

```
  var keepGoing = true;

  while (keepGoing) {
      let value = Math.random();
      if (value > 0.5) {
          keepGoing = false;
      }
  }
```

36. ### Explain the code?

```
for (let i = 0; i < 3; i++) {
    let value = i * 10;
    console.log(`${ i }: ${ value }`);
}
// 0: ?
// 1: ?
// 2: ?
```

37. ### Explain the code?

```
  {
      // a fictional variable for illustration
      let $$i = 0;

      for ( /* nothing */; $$i < 3; $$i++) {
          // here's our actual loop `i`!
          let i = $$i;

          let value = i * 10;
          console.log(`${ i }: ${ value }`);
      }
      // 0: 0
      // 1: 10
      // 2: 20
  }
```

38. ### Explain the code?

```
var studentName = "Kyle";

{
    console.log(studentName);
    // ???

    // ..

    let studentName = "Suzy";

    console.log(studentName);
    // Suzy
}
```
