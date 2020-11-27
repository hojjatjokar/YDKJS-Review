# Chapter 2

1. ### When scope bubbles determined and based on where?

   Scope bubbles are determined during compilation based on where the
   functions/blocks of scope are written, the nesting inside each other, and so
   on.

2. ### Can a scope be in two outer scope? Where each scope bubble contained?

   Each scope bubble is entirely contained within its parent scope bubble—a
   scope is never partially in two different outer scopes.

3. ### When the JS engine determine scope buckets?

   The JS engine doesn't generally determine these marble colors during runtime;
   the "lookup" here is a rhetorical device to help you understand the concepts.
   During compilation, most or all variable references will match already-known
   scope buckets, so their color is already determined, and stored with each
   marble reference to avoid unnecessary lookups as the program runs.

4. ### What are The members of the JS engine that will have conversations as they process our program?

- _Engine_: responsible for start-to-finish compilation and execution of our
  JavaScript program.
- _Compiler_: one of *Engine*'s friends; handles all the dirty work of parsing
  and code-generation (see previous section).
- _Scope Manager_: another friend of *Engine*; collects and maintains a lookup
  list of all the declared variables/identifiers, and enforces a set of rules as
  to how these are accessible to currently executing code.

5. ### What's conversations between JS engine members for this snippet of code?

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

6. ### How JS treats var students = [ .. ] ?

   We typically think of that as a single statement, but that's not how our
   friend *Engine* sees it. In fact, JS treats these as two distinct operations,
   one which *Compiler* will handle during compilation, and the other
   which *Engine* will handle during execution.

   To review and summarize how a statement like `var students = [ .. ]` is
   processed, in two distinct steps:

   1. *Compiler* sets up the declaration of the scope variable (since it wasn't
      previously declared in the current scope).
   2. While *Engine* is executing, to process the assignment part of the
      statement, *Engine* asks *Scope Manager* to look up the variable,
      initializes it to `undefined` so it's ready to use, and then assigns the
      array value to it.

7. ### Can scopes be lexically nested to any depth as the program defines?
   Scopes can be lexically nested to any arbitrary depth as the program defines.
8. ### What happens when at the beginning of a scope, if any identifier came from a function declaration?

   At the beginning of a scope, if any identifier came from
   a function declaration, that variable is automatically initialized to its
   associated function reference

9. ### What happens when at the beginning of a scope, if any identifier came from a var declaration?

   if any identifier came from a var declaration (as opposed to let/const), that
   variable is automatically initialized to undefined so that it can be used;

10. ### What happens when at the beginning of a scope, if any identifier came from a let/const declaration?

At the beginning of a scope, Any identifier came from a let/const declaration,
the variable remains uninitialized (aka, in its "TDZ,") and cannot be used until
its full declaration-and-initialization are executed.

11. ### In this snippet of code, in the for (let student of students) { statement, students is a source reference that must be looked up. But how will that lookup be handled, since the scope of the function will not find such an identifier?

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
```

To explain, let's imagine that bit of conversation playing out like this:

> Engine: Hey, Scope Manager (for the function), I have a source reference for
> students, ever heard of it?

> (Function) Scope Manager: Nope, never heard of it. Try the next outer scope.

> Engine: Hey, Scope Manager (for the global scope), I have a source reference
> for students, ever heard of it?

> (Global) Scope Manager: Yep, it was formally declared, here it is.

> ...

One of the key aspects of lexical scope is that any time an identifier reference
cannot be found in the current scope, the next outer scope in the nesting is
consulted; that process is repeated until an answer is found or there are no
more scopes to consult.

12. ### What's Nested Scope?

One of the key aspects of lexical scope is that any time an identifier reference
cannot be found in the current scope, the next outer scope in the nesting is
consulted; that process is repeated until an answer is found or there are no
more scopes to consult.

13. ### What happen when Engine exhausts all lexically available scopes (moving outward) and still cannot resolve the lookup of an identifier?

    When Engine exhausts all lexically available scopes (moving outward) and
    still cannot resolve the lookup of an identifier, an error condition then
    exists. However, depending on the mode of the program (strict-mode or not)
    and the role of the variable (i.e., target vs. source;), this error
    condition will be handled differently.

14. ### What will happen when If the variable is a source, an unresolved identifier lookup is considered an undeclared (unknown, missing) variable?

If the variable is a source, an unresolved identifier lookup is considered an
undeclared (unknown, missing) variable, which always results in
a ReferenceError being thrown.

15. ### What will happen when if the variable is a target, and the code at that moment is running in strict-mode, the variable is considered undeclared?

if the variable is a target, and the code at that moment is running in
strict-mode, the variable is considered undeclared and similarly throws
a ReferenceError.

16. ### What'll be printed? what's different between two of them?

```
var studentName;
typeof studentName;     // ?

typeof doesntExist;     // ?
```

```
var studentName;
typeof studentName;     // "undefined"

typeof doesntExist;     // "undefined"
```

17. ### What will happen when If the variable is a target and strict-mode is not in effect?

If the variable is a target and strict-mode is not in effect, a confusing and
surprising legacy behavior kicks in. The troublesome outcome is that the global
scope's Scope Manager will just create an accidental global variable to fulfill
that target assignment!

18. ### What'll be printed?

```
function getStudentName() {
    nextStudent = "Suzy";
}

getStudentName();

console.log(nextStudent);
```

```
function getStudentName() {
    // assignment to an undeclared variable :(
    nextStudent = "Suzy";
}

getStudentName();

console.log(nextStudent);
// "Suzy" -- oops, an accidental-global variable!
```

19. ### What will happen to Assign a never-declared variable?

    Assigning to a never-declared variable is an error, so it's right that we
    would receive a ReferenceError here.
