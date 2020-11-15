# Chapter 1

1. ### What's program state?
   The ability to store values and pull values out of variables is what gives a
   program state.
2. ### What's scope?
   Scope is the set of rules that determines where and how a variable
   (identifier) can be looked-up.
3. ### Is Javascript interpreted or compiled?
   Despite the fact that JavaScript falls under the general category of
   "dynamic" or "interpreted" languages, it is in fact a compiled language.
4. ### When Javascript compiled?
   For JavaScript, the compilation that occurs happens, in many cases, mere
   microseconds (or less!) before the code is executed.
5. ### What's compilation? What steps it includes typically?
   Tokenizing/Lexing, Parsing, Code-Generation
6. ### What's tokenizing ?
   Breaking up a string of characters into meaningful (to the language) chunks,
   called tokens.
7. ### Be tokenizer an tokenize this?

   ```javascript
   var a = 2;
   ```

   This program would likely be broken up into the following tokens: var, a, =,
   2, and ;. Whitespace may or may not be persisted as a token, depending on
   whether it's meaningful or not.

8. ### What's difference between tokenizing and lexing?

   if the tokenizer were to invoke stateful parsing rules to figure out whether
   **a** should be considered a distinct token or just part of another token,
   that would be lexing.

9. ### What's parsing?

   Taking a stream (array) of tokens and turning it into a tree of nested
   elements, which collectively represent the grammatical structure of the
   program. This tree is called an "AST" (Abstract Syntax Tree).

10. ### Be parser and parse this?

    ```javascript
    var a = 2;
    ```

    The tree start with a top-level node called VariableDeclaration, with a
    child node called Identifier (whose value is a), and another child called
    AssignmentExpression which itself has a child called NumericLiteral (whose
    value is 2).

11. ### What is code generation?

    The process of taking an AST and turning it into executable code.

12. ### Is there any performance optimization? in which step? name 3 of them?

    Collapsing redundant elements, JS engines use all kinds of tricks (like
    JITs, which lazy compile and even hot re-compile, etc.)

13. ### Does js has plenty of time for optimization? why?

    JavaScript engines don't get the luxury (like other language compilers) of
    having plenty of time to optimize, because JavaScript compilation doesn't
    happen in a build step ahead of time, as with other languages.

14. ### Characters that intract to process the process the program?

    Engine, Compiler, Scope

15. ### Whats's engine role in process of program?

    Responsible for start-to-finish compilation and execution of our JavaScript
    program.

16. ### What's compiler role in proccess of program?

    One of Engine's friends; handles all the dirty work of parsing and
    code-generation .

17. ### What's scope role in proceess of program?

    another friend of Engine; collects and maintains a look-up list of all the
    declared identifiers (variables), and enforces a strict set of rules as to
    how these are accessible to currently executing code.

18. ### Two actions are taken for a variable assignment, What are they?

    Two distinct actions are taken for a variable assignment: First, Compiler
    declares a variable (if not previously declared in the current scope), and
    second, when executing, Engine looks up the variable in Scope and assigns to
    it, if found.

19. ### How engine and friends will approch this program?

```javascript
var a = 2;
```

20. ### There is 2 lookups to see variable has been declared and they consulting scope. What are they? each has 6 property, what are those?

    An LHS look-up is done when a variable appears on the left-hand side of an
    assignment operation, and an RHS look-up is done when a variable appears on
    the right-hand side of an assignment operation.An RHS look-up is
    indistinguishable, for our purposes, from simply a look-up of the value of
    some variable, whereas the LHS look-up is trying to find the variable
    container itself, so that it can assign. In this way, RHS doesn't really
    mean "right-hand side of an assignment" per se, it just, more accurately,
    means "not left-hand side". You could also think "RHS" instead means
    "retrieve his/her source (value)", implying that RHS means "go get the value
    of...".

21. ### Function declaration is look up? LHS or RHS? why?
    Compiler handles both the declaration and the value definition during
    code-generation, such that when Engine is executing code, there's no
    processing necessary to "assign" a function value to **foo**. Thus, it's not
    really appropriate to think of a function declaration as an LHS look-up
    assignment
22. ### write down engin/scope conversation?

```javascript
function foo(a) {
  console.log(a);
}
foo(2);
```

Engine: Hey Scope, I have an RHS reference for foo. Ever heard of it?

Scope: Why yes, I have. Compiler declared it just a second ago. He's a function.
Here you go.

Engine: Great, thanks! OK, I'm executing foo.

Engine: Hey, Scope, I've got an LHS reference for a, ever heard of it?

Scope: Why yes, I have. Compiler declared it as a formal parameter to foo just
recently. Here you go.

Engine: Helpful as always, Scope. Thanks again. Now, time to assign 2 to a.

Engine: Hey, Scope, sorry to bother you again. I need an RHS look-up for
console. Ever heard of it?

Scope: No problem, Engine, this is what I do all day. Yes, I've got console.
He's built-in. Here ya go.

Engine: Perfect. Looking up log(..). OK, great, it's a function.

Engine: Yo, Scope. Can you help me out with an RHS reference to a. I think I
remember it, but just want to double-check.

Scope: You're right, Engine. Same guy, hasn't changed. Here ya go.

Engine: Cool. Passing the value of a, which is 2, into log(..).

23. ### What is nested scope? how engine find values for variables in nested scope? and until when it will continue to consulting scopes?

    Just as a block or function is nested inside another block or function,
    scopes are nested inside other scopes. So, if a variable cannot be found in
    the immediate scope, Engine consults the next outer containing scope,
    continuing until found or until the outermost (aka, global) scope has been
    reached.

24. ### What are the rules for traversing nested scope ?

    The simple rules for traversing nested Scope: Engine starts at the currently
    executing Scope, looks for the variable there, then if not found, keeps
    going up one level, and so on. If the outermost global scope is reached, the
    search stops, whether it finds the variable or not.

25. ### When ReferenceError happens?

    If an RHS look-up fails to ever find a variable, anywhere in the nested
    Scopes, this results in a ReferenceError being thrown by the Engine. It's
    important to note that the error is of the type ReferenceError. By contrast,
    if the Engine is performing an LHS look-up and arrives at the top floor
    (global Scope) without finding it, and if the program is not running in
    "Strict Mode" [^note-strictmode], then the global Scope will create a new
    variable of that name in the global scope, and hand it back to Engine.
    "Strict Mode" [^note-strictmode], which was added in ES5, has a number of
    different behaviors from normal/relaxed/lazy mode. One such behavior is that
    it disallows the automatic/implicit global variable creation. In that case,
    there would be no global Scope'd variable to hand back from an LHS look-up,
    and Engine would throw a ReferenceError similarly to the RHS case.

26. ### When TypeError happens?

    Now, if a variable is found for an RHS look-up, but you try to do something
    with its value that is impossible, such as trying to execute-as-function a
    non-function value, or reference a property on a null or undefined value,
    then Engine throws a different kind of error, called a TypeError.

27. ### What's difference between TypeError and ReferenceError?

    ReferenceError is Scope resolution-failure related, whereas TypeError
    implies that Scope resolution was successful, but that there was an
    illegal/impossible action attempted against the result.

28. ### Identify all the LHS look-ups and all the RHS look-ups ?

```javascript
function foo(a) {
  var b = a;
  return a + b;
}

var c = foo(2);
```

LHS Lokkups:

```
    c = .., a = 2 (implicit param assignment) and b = ..
```

RHS Lokkups:

```
    foo(2.., = a;, a + .. and .. + b
```
