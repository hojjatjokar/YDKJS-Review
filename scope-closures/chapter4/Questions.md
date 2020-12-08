# Chapter 4

1. ### Why a program's outermost scope is all that important in modern JS?

Whether a bundler tool is used for an application, or whether the (non-ES
module) files are simply loaded in the browser individually (via <script> tags
or other dynamic JS resource loading), if there is no single surrounding scope
encompassing all these pieces, the global scope is the only way for them to
cooperate with each other

2. ### Most applications are composed of multiple individual JS files. So how exactly do all those separate files get stitched together in a single runtime context by the JS engine?

With respect to browser-executed applications, there are three main ways:

**First**, if you're directly using ES modules, these files are loaded
individually by the JS environment. Each module then imports references to
whichever other modules it needs to access. The separate module files cooperate
with each other exclusively through these shared imports, without needing any
shared outer scope.

**Second**, if you're using a bundler in your build process, all the files are
typically concatenated together before delivery to the browser and JS engine,
which then only processes one big file. Even with all the pieces of the
application co-located in a single file, some mechanism is necessary for each
piece to register a name to be referred to by other pieces, as well as some
facility for that access to occur.

**Third**: whether a bundler tool is used for an application, or whether the
(non-ES module) files are simply loaded in the browser individually (via

`<script>` tags or other dynamic JS resource loading), if there is no single
surrounding scope encompassing all these pieces, the **global scope** is the
only way for them to cooperate with each other

3. ### In addition to accounting for where an application's code resides during runtime, and how each piece is able to access the other pieces to cooperate, the global scope is also where?

- JS exposes its built-ins
- The environment hosting the JS engine exposes its own built-ins:

4. ### What are JS built-ins that exposed to global object?

- primitives: `undefined`, `null`, `Infinity`, `NaN`
- natives: `Date()`, `Object()`, `String()`, etc.
- global functions: `eval()`, `parseInt()`, etc.
- namespaces: `Math`, `Atomics`, `JSON`
- friends of JS: `Intl`, `WebAssembly`

5. ### What are the environment hosting the JS engine exposes its own built-ins to global object?

- `console` (and its methods)
- the DOM (`window`, `document`, etc)
- timers (`setTimeout(..)`, etc)
- web platform APIs: `navigator`, `history`, geolocation, WebRTC, etc.

6. ### What are different JS environments that handle the scopes of your programs differently?

- Browser "Window"
- Web Worker
- Developer Tools Console/REPL
- ESM

7. ### What's The purest environment JS can be run in is?

The purest environment JS can be run in is as a standalone .js file loaded in a
web page environment in a browser.

8. ### What's the default behavior expected from global scope and global object?

   The default behavior expect from a reading of the JS specification: the outer
   scope is the global scope and the variable declared in global scope is
   legitimately created as a global variable.

9. ### What's consequence of the difference between a global variable and a global property of the same name?

An unusual consequence of the difference between a global variable and a global
property of the same name is that, within just the global scope itself, a global
object property can be shadowed by a global variable.

10. ### What's the effect of a DOM element with an id attribute on global scope?

A DOM element with an id attribute automatically creates a global variable that
references it.

11. ### What's Web Worker?

Web Workers are a web platform extension on top of browser-JS behavior, which
allows a JS file to run in a completely separate thread (operating system wise)
from the thread that's running the main JS program.

12. ### What's Web worker restriction? and why is that?

Since these Web Worker programs run on a separate thread, they're restricted in
their communications with the main application thread, to avoid/limit race
conditions and other complications. Web Worker code does not have access to the
DOM, for example. Some web APIs are, however, made available to the worker, such
as the navigator.

13. ### Is global scope shared between main program and Web Worker? and why?

Since a Web Worker is treated as a wholly separate program, it does not share
the global scope with the main JS program.

14. ### What's global object reference in Web Worker?

    In a Web Worker, the global object reference is typically made using self.

15. ### In Web Worker what's behavior of var and let and const declarations to global scope and global object?

    Just as with main JS programs, var and function declarations create mirrored
    properties on the global object (aka, self), where other declarations (let,
    etc) do not.

16. ### What's Developer Tools Console/REPL?

    Developer Tools don't create a completely adherent JS environment. They do
    process JS code, but they also lean in favor of the UX interaction being
    most friendly to developers (aka, developer experience, or DX).

    In some cases, favoring DX when typing in short JS snippets, over the normal
    strict steps expected for processing a full JS program, produces observable
    differences in code behavior between programs and tools. For example,
    certain error conditions applicable to a JS program may be relaxed and not
    displayed when the code is entered into a developer tool.

17. ### What's differences in behavior of scope in Developer Tools observable?

- The behavior of the global scope
- Hoisting
- Block-scoping declarators (`let` / `const`) when used in the outermost scope

18. ### What's global scope and global object behavior in ESM?

Identifiers declared at the top level of the (module) file, in the outermost
obvious scope are not global variables. Instead, they are module-wide, or if you
prefer, "module-global."

However, in a module, there's no implicit **"module-wide scope object"** for
these top-level declarations to be added to as properties, as there is when
declarations appear in the top-level of non-module JS files. This is not to say
that global variables cannot exist or be accessed in such programs. It's just
that global variables don't get created by declaring variables in the top-level
scope of a module.

19. ### What's Node behavior according to global scope?

Node treats every single .js file that it loads, including the main one you
start the Node process with, as a module (ES module or CommonJS module). The
practical effect is that the top level of your Node programs is never actually
the global scope, the way it is when loading a non-module file in the browser.

20. ### What's Node globals?

As noted earlier, Node defines a number of "globals" like require(), but they're
not actually identifiers in the global scope (nor properties of the global
object). They're injected in the scope of every module, essentially a bit like
the parameters listed in the Module(..) function declaration.

21. ### How do you define actual global variables in Node?

The only way to do so is to add properties to another of Node's automatically
provided "globals," which is ironically called global. global is a reference to
the real global scope object, somewhat like using window in a browser JS
environment.

22. ### What's Global This?

We have `window`, `self`, `global`, and this ugly `new Function(..)` trick.
That's a lot of different ways to try to get at this global object.

As of ES2020, JS has finally defined a standardized reference to the global
scope object, called `globalThis`. So, subject to the recency of the JS engines
your code runs in, you can use `globalThis` in place of any of those other
approaches.

23. ### Another "trick" for obtaining a reference to the global scope object ?

```
const theGlobalScopeObject = (new Function("return this"))();
```
