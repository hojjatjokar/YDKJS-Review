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

    Processing of JS programs is that it occurs in (at least) two phases:

        1. Parsing/compilation
        2. Then execution
