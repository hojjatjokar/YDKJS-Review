# Chapter 3

1. ### What's scope chain?

The connections between scopes that are nested within other scopes is called the
scope chain, which determines the path along which variables can be accessed.
The chain is directed, meaning the lookup moves upward/outward only.

2. ### When will happen determination of what scope a variable originates from?

The color of a marble's bucket (aka, meta information of what scope a variable
originates from) is usually determined during the initial compilation
processing. Because lexical scope is pretty much finalized at that point, a
marble's color will not change based on anything that can happen later during
runtime.

3. ### Where will be stored meta information of what scope a variable originates from?

Since the marble's color is known from compilation, and it's immutable, this
information would likely be stored with (or at least accessible from) each
variable's entry in the AST; that information is then used explicitly by the
executable instructions that constitute the program's runtime.

4. ### In what case would variable's scope ever not be known during compilation?

Consider a reference to a variable that isn't declared in any lexically
available scopes in the current file—each file is its own separate program from
the perspective of JS compilation. If no declaration is found, that's
not *necessarily* an error. Another file (program) in the runtime may indeed
declare that variable in the shared global scope.

So the ultimate determination of whether the variable was ever appropriately
declared in some accessible bucket may need to be deferred to the runtime.

Any reference to a variable that's initially *undeclared* is left as an
uncolored marble during that file's compilation; this color cannot be determined
until other relevant file(s) have been compiled and the application runtime
commences. That deferred lookup will eventually resolve the color to whichever
scope the variable is found in (likely the global scope).

However, this lookup would only be needed once per variable at most, since
nothing else during runtime could later change that marble's color.

The "Lookup Failures" covers what happens if a marble is ultimately still
uncolored at the moment its reference is runtime executed.

5. ### What will be printed out?

```javascript
var studentName = 'Suzy';

function printStudent(studentName) {
  studentName = studentName.toUpperCase();
  console.log(studentName);
}

printStudent('Frank');

printStudent(studentName);

console.log(studentName);
```

6. ### How can access a global variable not via scope?

It *is* possible to access a global variable from a scope where that variable
has been shadowed, but not through a typical lexical identifier reference.

In the global scope, `var` declarations and `function` declarations also expose
themselves as properties on the *global object*—essentially an object
representation of the global scope.

7. ### How can you add variable to the global scope but not directly declaring variable?

   You can even add a variable to the global scope by creating/setting a
   property on the global object.

8. ### Which kinda declarations reading/creating variable via global object works for?

   This little "trick" only works for accessing a global scope variable (not a
   shadowed variable from a nested scope), and even then, only one that was
   declared with var or function.

9. ### What will be result of this snippet of code?

```javascript
var one = 1;
let notOne = 2;
const notTwo = 3;
class notThree {}

console.log(window.one); // ?
console.log(window.notOne); // ?
console.log(window.notTwo); // ?
console.log(window.notThree); // ?
```

ANSWER:

```javascript
var one = 1;
let notOne = 2;
const notTwo = 3;
class notThree {}

console.log(window.one); // 1
console.log(window.notOne); // undefined
console.log(window.notTwo); // undefined
console.log(window.notThree); // undefined
```

10. ### How can let and var declarations shadow each other?

Summary: let (in an inner scope) can always shadow an outer scope's var. var (in
an inner scope) can only shadow an outer scope's let if there is a function
boundary in between.

11. ### Explain this snippet of code, how shadowing will happen here?

```javascript
function something() {
  var special = 'JavaScript';

  {
    let special = 42; // ?
  }
}

function another() {
  {
    let special = 'JavaScript';
    {
      var special = 'JavaScript'; // ?
    }
  }
}
```

12. ### Explain this snippet of code, how shadowing happen here?

```javascript
function another() {
  // ..

  {
    let special = 'JavaScript';

    ajax('https://some.url', function callback() {
      // ?
      var special = 'JavaScript';

      // ..
    });
  }
}
```

13. ### What's difference between function declarations and function expressions?

One major difference between function declarations and function expressions is
what happens to the name identifier of the function.

14. ### Explain this snippet of code?

```javascript
var askQuestion = function ofTheTeacher() {
  console.log(ofTheTeacher);
};

askQuestion(); // ?

console.log(ofTheTeacher); // ?
```

ANSWER

```javascript
var askQuestion = function ofTheTeacher() {
  console.log(ofTheTeacher);
};

askQuestion();
// function ofTheTeacher()...

console.log(ofTheTeacher);
// ReferenceError: ofTheTeacher is not defined
```

15. ### Explain this snippet of code? what will happen in 'strict-mode' and non 'strict-mode'

```javascript
var askQuestion = function ofTheTeacher() {
  'use strict';
  ofTheTeacher = 42; // ?

  //..
};

askQuestion();
// ?
```

16. ### What's Arrow function syntax?

- The => arrow function doesn't require the word function to define it.
- The ( .. ) around the parameter list is optional in some simple cases.
- Likewise, the { .. } around the function body is optional in some cases. And
  when the { .. } are omitted, a return value is sent out without using a return
  keyword.

17. ### Does arrow functions somehow behave differently with respect to lexical scope from standard function functions?
    Other than being anonymous (and having no declarative form), => arrow
    functions have the same lexical scope rules as function functions do. An
    arrow function, with or without { .. } around its body, still creates a
    separate, inner nested bucket of scope. Variable declarations inside this
    nested scope bucket behave the same as in a function scope.
