# Chapter 3

1. ### What exactly makes a new bubble? is it only the function? can other structures in javascript create bubbles of scope?
   Each function you declare creates a bubble for itself, and block scope and
   **catch** in try/catch and **with**
2. ### Consider this code:

```javascript
function foo(a){
  var b = 2;

  function bar(){
    ...
  }

  var c = 3;
}
```

- The scope bubble for **_foo(...)_** includes which identifiers? `a, b, c, bar`
- The scope bubble for **_bar(...)_** has which identifiers? `a, b, c, bar`

- The scope bubble for global scope has which identifiers? `foo`
- This code in global scope has what result?

```javascript
bar();
console.log(a, b, c);
```

It will throw ReferenceError

3. ### How to hide the code in plain scope?

   The traditional way of thinking about functions is that you declare a
   function, and then add code inside it. But the inverse thinking is equally
   powerful and useful: take any arbitrary section of code you've written, and
   wrap a function declaration around it, which in effect "hides" the code.

4. ### What's principle of least privilege?
   This principle states that in the design of software, such as the API for a
   module/object, you should expose only what is minimally necessary, and "hide"
   everything else. This principle extends to the choice of which scope to
   contain variables and functions. If all variables and functions were in the
   global scope, they would of course be accessible to any nested scope. But
   this would violate the "Least..." principle in that you are (likely) exposing
   many variables or functions which you should otherwise keep private, as
   proper use of the code would discourage access to those variables/functions.
5. ### Explain collisions in global namespaces and how they handle problem?
   A particularly strong example of (likely) variable collision occurs in the
   global scope. Multiple libraries loaded into your program can quite easily
   collide with each other if they don't properly hide their internal/private
   functions and variables. Such libraries typically will create a single
   variable declaration, often an object, with a sufficiently unique name, in
   the global scope. This object is then used as a "namespace" for that library,
   where all specific exposures of functionality are made as properties of that
   object (namespace), rather than as top-level lexically scoped identifiers
   themselves.
6. ### Another option for collision avoidance?

   Another option for collision avoidance is the more modern "module" approach,
   using any of various dependency managers.

7. ### What's module management?
   Using these tools, no libraries ever add any identifiers to the global scope,
   but are instead required to have their identifier(s) be explicitly imported
   into another specific scope through usage of the dependency manager's various
   mechanisms. It should be observed that these tools do not possess "magic"
   functionality that is exempt from lexical scoping rules. They simply use the
   rules of scoping as explained here to enforce that no identifiers are
   injected into any shared scope, and are instead kept in private,
   non-collision-susceptible scopes, which prevents any accidental scope
   collisions.
8. ### Problems of hiding in plain scope?
   The first is that we have to declare a named-function foo(), which means that
   the identifier name foo itself "pollutes" the enclosing scope (global, in
   this case). We also have to explicitly call the function by name (foo()) so
   that the wrapped code actually executes.
9. ### According to this code:

```javascript
var a = 2;
function foo() {
  var a = 3;
  console.log(a);
}
foo();
console.log(a);
```

- Show problems of this code?
  `foo is pulluted the scope and extra foo invocation`
- Solve problems with a function expression?

```javascript
var a = 2;

(function foo() {
  // <-- insert this

  var a = 3;
  console.log(a); // 3
})(); // <-- and this

console.log(a); // 2
```

11. ### What's difference between function declaration vs. expression? function name bound to where?

    First, notice that the wrapping function statement starts with (function...
    as opposed to just function.... While this may seem like a minor detail,
    it's actually a major change. Instead of treating the function as a standard
    declaration, the function is treated as a function-expression. The easiest
    way to distinguish declaration vs. expression is the position of the word
    "function" in the statement (not just a line, but a distinct statement). If
    "function" is the very first thing in the statement, then it's a function
    declaration. Otherwise, it's a function expression. The key difference we
    can observe here between a function declaration and a function expression
    relates to where its name is bound as an identifier. In other words,
    (function foo(){ .. }) as an expression means the identifier foo is found
    only in the scope where the .. indicates, not in the outer scope. Hiding the
    name foo inside itself means it does not pollute the enclosing scope
    unnecessarily.

12. ### What is anonymous function expression?

```javascript
setTimeout(function () {
  console.log('I waited 1 second!');
}, 1000);
```

This is called an "anonymous function expression", because function()... has no
name identifier on it. Function expressions can be anonymous, but function
declarations cannot omit the name -- that would be illegal JS grammar.

13. ### Can function declarations ommit the name? why?
    Function declarations cannot omit the name -- that would be illegal JS
    grammar.
14. ### Drawback of anonymous function? (3)

- Anonymous functions have no useful name to display in stack traces, which can
  make debugging more difficult.

- Without a name, if the function needs to refer to itself, for recursion, etc.,
  the deprecated arguments.callee reference is unfortunately required. Another
  example of needing to self-reference is when an event handler function wants
  to unbind itself after it fires.

- Anonymous functions omit a name that is often helpful in providing more
  readable/understandable code. A descriptive name helps self-document the code
  in question.

15. ### IIFE pattern is stands for?

    Immediately Invoking Function Expressions

16. ### What is IIFE?
    Now that we have a function as an expression by virtue of wrapping it in a (
    ) pair, we can execute that function by adding another () on the end, like
    (function foo(){ .. })(). The first enclosing ( ) pair makes the function an
    expression, and the second () executes the function. This pattern is so
    common, a few years ago the community agreed on a term for it: IIFE, which
    stands for Immediately Invoked Function Expression.
17. ### Most common form of IIFE?
    IIFE's don't need names, necessarily -- the most common form of IIFE is to
    use an anonymous function expression.
18. ### Less common form of IIFE?
    While certainly less common, naming an IIFE has all the aforementioned
    benefits over anonymous function expressions, so it's a good practice to
    adopt.
19. ### JS has 4 facility for block scope? What are they?

- with
- try/catch
- const
- let

20. ### What's let and how it declare variable?

    ES6 introduces a new keyword **let** which sits alongside **var** as another
    way to declare variables. The **\*let** keyword attaches the variable
    declaration to the scope of whatever block (commonly a **{ .. }** pair) it's
    contained in. In other words, **let** implicitly hijacks any block's scope
    for its variable declaration.

21. ### Declarations made with let will hoist? why?

    However, declarations made with **let** will not hoist to the entire scope
    of the block they appear in. Such declarations will not observably "exist"
    in the block until the declaration statement.

22. ### How block scoping is usefull relates to closures and garbage collection? with example?

Another reason block-scoping is useful relates to closures and garbage
collection to reclaim memory.

```javascript
  function process(data) {
    // do something interesting
  }

  var someReallyBigData = { .. };

  process( someReallyBigData );

  var btn = document.getElementById( "my_button" );

  btn.addEventListener( "click", function click(evt){
    console.log("button clicked");
  }, /*capturingPhase=*/false );
```

The click function click handler callback doesn't need the **someReallyBigData**
variable at all. That means, theoretically, after **process(..)** runs, the big
memory-heavy **data** structure could be garbage collected. However, it's quite
likely (though implementation dependent) that the JS engine will still have to
keep the structure around, since the click function has a closure over the
entire scope. Block-scoping can address this concern, making it clearer to the
engine that it does not need to keep someReallyBigData around:

```javascript
function process(data) {
	// do something interesting
}

// anything declared inside this block can go away after!
{
	let someReallyBigData = { .. };

	process( someReallyBigData );
}

var btn = document.getElementById( "my_button" );

btn.addEventListener( "click", function click(evt){
	console.log("button clicked");
}, /*capturingPhase=*/false );
```

23. ### Benefit of let for loops?(2)

    Not only does let in the for-loop header bind the i to the for-loop body,
    but in fact, it re-binds it to each iteration of the loop, making sure to
    re-assign it the value from the end of the previous loop iteration.

24. ### What's const?

In addition to let, ES6 introduces const, which also creates a block-scoped
variable, but whose value is fixed (constant). Any attempt to change that value
at a later time results in an error.
