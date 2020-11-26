# Chapter 1

1.  ### What's code compilation?
    Code compilation is a set of steps that process the text of your code and
    turn it into a list of instructions the computer can understand. Typically,
    the whole source code is transformed at once, and those resulting
    instructions are saved as output (usually in a file) that can later be
    executed.
2.  ### What's Interpretation, and how is it different from code compilation?
    Interpretation performs a similar task to the compilation, in that it
    transforms your program into machine-understandable instructions. But the
    processing model is different. Unlike a program being compiled all at once,
    with the interpretation the source code is transformed line by line; each
    line or statement is executed before immediately proceeding to processing
    the next line of the source code.
3.  ### Why does it even matter whether JS is compiled or not?
    Scope is primarily determined during compilation, so understanding how
    compilation and execution relate is key in mastering scope.
4.  ### What are the basic stages that a program is processed by a compiler?
    1. **Tokenizing/Lexing:** breaking up a string of characters into meaningful
       (to the language) chunks, called tokens.
    2. **Parsing:** taking a stream (array) of tokens and turning it into a tree
       of nested elements, which collectively represent the grammatical
       structure of the program. This is called an Abstract Syntax Tree (AST).
    3. **Code Generation:** taking an AST and turning it into executable code.
       This part varies greatly depending on the language, the platform it's
       targeting, and other factors.
5.  ### Explain what happens to this code snippet in those each steps from previous question?
    ```
        var a = 2;
    ```
    1. This program would likely be broken up into the following
       tokens: `var`, `a`, `=`, `2`, and `;`. Whitespace may or may not be
       persisted as a token, depending on whether it's meaningful or not.
    2. the tree for `var a = 2;` might start with a top-level node
       called `VariableDeclaration`, with a child node
       called `Identifier` (whose value is `a`), and another child
       called `AssignmentExpression` which itself has a child
       called `NumericLiteral` (whose value is `2`)
    3. The JS engine takes the just described AST for `var a = 2;` and turns it
       into a set of machine instructions to actually create a variable called
       `a` (including reserving memory, etc.), and then stores a value into a.
6.  ### What's difference between tokenizing and lexing?
    The difference between tokenizing and lexing is subtle and academic, but it
    centers on whether or not these tokens are identified in
    a stateless or stateful way. Put simply, if the tokenizer were to invoke
    stateful parsing rules to figure out whether `a` should be considered a
    distinct token or just part of another token, that would be lexing.)
7.  ### What else the JS engine will do beside this three steps?
    The JS engine is vastly more complex than just these three stages. In the
    process of parsing and code generation, there are steps to optimize the
    performance of the execution (i.e., collapsing redundant elements). In fact,
    code can even be re-compiled and re-optimized during the progression of
    execution.
8.  ### When is JS compilation happens?
    JS compilation doesn't happen in a build step ahead of time, as with other
    languages. It usually must happen in mere microseconds (or less!) right
    before the code is executed.
9.  ### What JS engine will do for performance optimizations?
    JS engines don't have the luxury of an abundance of time to perform their
    work and optimizations. To ensure the fastest performance under these
    constraints, JS engines use all kinds of tricks (like JITs, which lazy
    compile and even hot re-compile); these are well beyond the "scope" of our
    discussion here.
10. ### Which steps has processing of JS programs?

    Processing of JS programs is that it occurs in (at least) two phases: 1.
    Parsing/compilation 2. Then execution

11. ### What are characteristics to prove JS has compilation step?
    There are three program characteristics you can observe to prove this to
    yourself:
    - Syntax errors
    - Early errors
    - Hoisting
12. ### How syntax errors can spot that JS has compilation phase?

    ```
        var greeting = "Hello";

        console.log(greeting);

        greeting = ."Hi";
        // SyntaxError: unexpected token .
    ```

    The only way the JS engine could know about the syntax error on the third
    line, before executing the first and second lines, is by the JS engine first
    parsing the entire program before any of it is executed. This program
    produces no output (`"Hello"` is not printed), but instead throws
    a `SyntaxError` about the unexpected `.` token right before
    the `"Hi"` string. Since the syntax error happens after the
    well-formed `console.log(..)` statement, if JS was executing top-down line
    by line, one would expect the `"Hello"` message being printed before the
    syntax error being thrown. That doesn't happen. In fact, the only way the JS
    engine could know about the syntax error on the third line, before executing
    the first and second lines, is by the JS engine first parsing the entire
    program before any of it is executed.

13. ### How early errors can spot that JS has compilation phase?

    ```
    console.log("Howdy");

    saySomething("Hello","Hi");
    // Uncaught SyntaxError: Duplicate parameter name not
    // allowed in this context

    function saySomething(greeting,greeting) {
        "use strict";
        console.log(greeting);
    }
    ```

    The `"Howdy"` message is not printed, despite being a well-formed statement.
    Instead, the `SyntaxError` here is thrown before the program is executed. In
    this case, it's because strict-mode (opted in for only
    the `saySomething(..)` function here) forbids, among many other things,
    functions to have duplicate parameter names; this has always been allowed in
    non-strict-mode. The error thrown is not a syntax error in the sense of
    being a malformed string of tokens (like `."Hi"` prior), but in strict-mode
    is nonetheless required by the specification to be thrown as an "early
    error" before any execution begins. But how does the JS engine know that
    the `greeting` parameter has been duplicated? How does it know that
    the `saySomething(..)` function is even in strict-mode while processing the
    parameter list (the `"use strict"` pragma appears only later, in the
    function body)? Again, the only reasonable explanation is that the code must
    first be *fully* parsed before any execution occurs.

14. ### How early hoisting spot that JS has compilation phase?

    ```
        function saySomething() {
            var greeting = "Hello";
            {
                greeting = "Howdy";  // error comes from here
                let greeting = "Hi";
                console.log(greeting);
            }
        }

        saySomething();
        // ReferenceError: Cannot access 'greeting' before
        // initialization
    ```

    The noted ReferenceError occurs from the line with the statement
    `greeting = "Howdy"`. What's happening is that the greeting variable for
    that statement belongs to the declaration on the next line,
    `let greeting = "Hi"`, rather than to the previous `var greeting = "Hello"`
    statement.

    The only way the JS engine could know, at the line where the error is
    thrown, that the next statement would declare a block-scoped variable of the
    same name (greeting) is if the JS engine had already processed this code in
    an earlier pass, and already set up all the scopes and their variable
    associations. This processing of scopes and declarations can only accurately
    be accomplished by parsing the program before execution.

    The ReferenceError here technically comes from greeting = "Howdy" accessing
    the greeting variable too early, a conflict referred to as the Temporal Dead
    Zone (TDZ).

15. ### What roles occurrences of variables/identifiers in a program serve?
    All occurrences of variables/identifiers in a program serve in one of two
    "roles": either they're the target of an assignment or they're the source of
    a value.
16. ### What are LHS and RHS?
    "LHS" (aka, target) and "RHS" (aka, source). As you might guess from the "L"
    and the "R", the acronyms mean "Left-Hand Side" and "Right-Hand Side", as in
    left and right sides of an = assignment operator. However, assignment
    targets and sources don't always literally appear on the left or right of an
    =, so it's probably clearer to think in terms of target/source rather than
    left / right.
17. ### How do you know if a variable is a target or source?
    Check if there is a value that is being assigned to it; if so, it's a
    target. If not, then the variable is a source.
18. ### Spot targets and sources in this snippet of codes?

    ```
    var students = [
        { id: 14, name: "Kyle" },
        { id: 73, name: "Suzy" },
        { id: 112, name: "Frank" },
        { id: 6, name: "Sarah" }
    ];

    function getStudentName(studentID) {
        for (let student of students) {
            if (student.id == studentID) {
                return student.name;
            }
        }
    }

    var nextStudent = getStudentName(73);

    console.log(nextStudent);
    // Suzy
    ```

19. ### How can modify a program's scopes during runtime?

    In **non-strict-mode**, there are technically two ways to cheat lexical
    scope, modifying a program's scopes during runtime.

    - The `eval(..)` function
    - `with` keyword

20. ### What's best practice to cheating lexical scope?
    Neither of these techniques should be used—they're both dangerous and
    confusing, and you should be using strict-mode (where they're disallowed)
    anyway. But it's important to be aware of them in case you run across them
    in some programs.
21. ### How eval() function cheat lexical scope?
    The eval(..) function receives a string of code to compile and execute on
    the fly during the program runtime. If that string of code has a var or
    function declaration in it, those declarations will modify the current scope
    that the eval(..) is currently executing in:
22. ### Explain this snippet of code?
    ```
        function badIdea() {
            eval("var oops = 'Ugh!';");
            console.log(oops);
        }
        badIdea();   // Ugh!
    ```
    If the eval(..) had not been present, the oops variable in console.log(oops)
    would not exist, and would throw a ReferenceError. But eval(..) modifies the
    scope of the badIdea() function at runtime. This is bad for many reasons,
    including the performance hit of modifying the already compiled and
    optimized scope, every time badIdea() runs.
23. ### How with cheat lexical scope?

    The second cheat is the with keyword, which essentially dynamically turns an
    object into a local scope—its properties are treated as identifiers in that
    new scope's block

24. ### Explain the code?

        ```
        var badIdea = { oops: "Ugh!" };

        with (badIdea) {
            console.log(oops);   // Ugh!
        }
        ```

    The global scope was not modified here, but badIdea was turned into a scope
    at runtime rather than compile time, and its property oops becomes a
    variable in that scope. Again, this is a terrible idea, for performance and
    readability reasons.

25. ### What's lexical scope?

    JS's scope is determined at compile time; the term for this kind of scope is
    "lexical scope". "Lexical" is associated with the "lexing" stage of
    compilation.

26. ### What's the key idea of lexical scope?
    the key idea of "lexical scope" is that it's controlled entirely by the
    placement of functions, blocks, and variable declarations, in relation to
    one another.
27. ### What's function scope and block scope?

    If you place a variable declaration inside a function, the compiler handles
    this declaration as it's parsing the function, and associates that
    declaration with the function's scope. If a variable is block-scope declared
    (let / const), then it's associated with the nearest enclosing { .. } block,
    rather than its enclosing function (as with var).

28. ### How is nested scope work?

    a reference (target or source role) for a variable must be resolved as
    coming from one of the scopes that are lexically available to it; otherwise
    the variable is said to be "undeclared" (which usually results in an
    error!). If the variable is not declared in the current scope, the next
    outer/enclosing scope will be consulted. This process of stepping out one
    level of scope nesting continues until either a matching variable
    declaration can be found, or the global scope is reached and there's nowhere
    else to go.

29. ### Does compilation do memory allocation?

    It's important to note that compilation doesn't actually do anything in
    terms of reserving memory for scopes and variables. None of the program has
    been executed yet.

30. ### How compilation handle scope for program execution?
    Instead, compilation creates a map of all the lexical scopes that lays out
    what the program will need while it executes. You can think of this plan as
    inserted code for use at runtime, which defines all the scopes (aka,
    "lexical environments") and registers all the identifiers (variables) for
    each scope. In other words, while scopes are identified during compilation,
    they're not actually created until runtime, each time a scope needs to run.
