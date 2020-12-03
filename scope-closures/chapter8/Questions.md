# Chapter 8

1. ### What's one of the most important code organization patterns?

   One of the most important code organization patterns in all of programming:
   the module.

2. ### What are modules built from?

   Modules are inherently built from lexical scope and closure.

3. ### What's the goals of encapsulation?

   The **goal of encapsulation** is the bundling or co-location of information
   (data) and behavior (functions) that together serve a common purpose.

   Another key goal is the control of visibility of certain aspects of the
   encapsulated data and functionality. Recall from Chapter 6 the *least
   exposure* principle (POLE), which seeks to defensively guard against
   various *dangers* of scope over-exposure; these affect both variables and
   functions. In JS, we most often implement visibility control through the
   mechanics of lexical scope.

4. ### What's the idea of encapsulation?

The idea is to group alike program bits together, and selectively limit
programmatic access to the parts we consider private details. What's not
considered private is then marked as public, accessible to the whole program.

5. ### What are benefits of encapsulation?

- The natural effect of this effort is better code organization.
- It's easier to build and maintain software when we know where things are, with
  clear and obvious boundaries and connection points.
- It's also easier to maintain quality if we avoid the pitfalls of over-exposed
  data and functionality.

6. ### What Is a Module?

A module is a collection of related data and functions, characterized by a
division between hidden *private* details and *public* accessible details,
usually called the "public API."

A module is also stateful: it maintains some information over time, along with
functionality to access and update that information.

7. ### What it means when we say module is stateful?

A module is also stateful: it maintains some information over time, along with
functionality to access and update that information.

8. ### What's broader concern of the module pattern?

A broader concern of the module pattern is fully embracing system-level
modularization through loose-coupling and other program architecture techniques.

9. ### What are Namespaces? compare with module?

If you group a set of related functions together, without data, then you don't
really have the expected encapsulation a module implies. The better term for
this grouping of stateless functions is a namespace.

10. ### Explain how Namespaces are not module with this snippet of code?

```
// namespace, not module
  var Utils = {
      cancelEvt(evt) {
          evt.preventDefault();
          evt.stopPropagation();
          evt.stopImmediatePropagation();
      },
      wait(ms) {
          return new Promise(function c(res){
              setTimeout(res,ms);
          });
      },
      isValidEmail(email) {
          return /[^@]+@[^@.]+\.[^@.]+/.test(email);
      }
  };
```

Utils here is a useful collection of utilities, yet they're all
state-independent functions. Gathering functionality together is generally good
practice, but that doesn't make this a module. Rather, we've defined
a Utils namespace and organized the functions under it.

11. ### What are Data Structures? and compare with modules?

Even if you bundle data and stateful functions together, if you're not limiting
the visibility of any of it, then you're stopping short of the POLE aspect of
encapsulation; it's not particularly helpful to label that a module.

12. ### Explain how Data Structures are not module with this snippet of code?

```
  // data structure, not module
  var Student = {
      records: [
          { id: 14, name: "Kyle", grade: 86 },
          { id: 73, name: "Suzy", grade: 87 },
          { id: 112, name: "Frank", grade: 75 },
          { id: 6, name: "Sarah", grade: 91 }
      ],
      getName(studentID) {
          var student = this.records.find(
              student => student.id == studentID
          );
          return student.name;
      }
  };

  Student.getName(73);
  // Suzy
```

Since `records` is publicly accessible data, not hidden behind a public
API, `Student` here isn't really a module.

`Student` does have the data-and-functionality aspect of encapsulation, but not
the visibility-control aspect. It's best to label this an instance of a data
structure.

13. ### How does the classic module format work? explain this example ?

```
var Student = (function defineStudent(){
    var records = [
        { id: 14, name: "Kyle", grade: 86 },
        { id: 73, name: "Suzy", grade: 87 },
        { id: 112, name: "Frank", grade: 75 },
        { id: 6, name: "Sarah", grade: 91 }
    ];

    var publicAPI = {
        getName
    };

    return publicAPI;

    // ************************

    function getName(studentID) {
        var student = records.find(
            student => student.id == studentID
        );
        return student.name;
    }
})();

Student.getName(73);   // Suzy
```

Notice that the instance of the module is created by the `defineStudent()` IIFE
being executed. This IIFE returns an object (named `publicAPI`) that has a
property on it referencing the inner `getName(..)` function.

Naming the object `publicAPI` is a stylistic preference on my part. The object
can be named whatever you like (JS doesn't care), or you can just return an
object directly without assigning it to any internal named variable. More on
this choice in Appendix A.

From the outside, `Student.getName(..)` invokes this exposed inner function,
which maintains access to the inner `records` variable via closure.

You don't *have* to return an object with a function as one of its properties.
You could just return a function directly, in place of the object. That still
satisfies all the core bits of a classic module.

By virtue of how lexical scope works, defining variables and functions inside
your outer module definition function makes everything *by default* private.
Only properties added to the public API object returned from the function will
be exported for external public use.

The use of an IIFE implies that our program only ever needs a single central
instance of the module, commonly referred to as a "singleton." Indeed, this
specific example is simple enough that there's no obvious reason we'd need
anything more than just one instance of the `Student` module.

14. ### What is Module Factory?

If we did want to define a module that supported multiple instances in our
program, we can slightly tweak the code:

    ```
      // factory function, not singleton IIFE
      function defineStudent() {
          var records = [
              { id: 14, name: "Kyle", grade: 86 },
              { id: 73, name: "Suzy", grade: 87 },
              { id: 112, name: "Frank", grade: 75 },
              { id: 6, name: "Sarah", grade: 91 }
          ];

          var publicAPI = {
              getName
          };

          return publicAPI;

          // ************************

          function getName(studentID) {
              var student = records.find(
                  student => student.id == studentID
              );
              return student.name;
          }
      }

      var fullTime = defineStudent();
      fullTime.getName(73);            // Suzy
    ```

    Rather than specifying `defineStudent()` as an IIFE, we just define it as a
    normal standalone function, which is commonly referred to in this context as
    a "module factory" function. We then call the module factory, producing an
    instance of the module that we label `fullTime`. This module instance
    implies a new instance of the inner scope, and thus a new closure
    that `getName(..)` holds over `records`. `fullTime.getName(..)` now invokes
    the method on that specific instance.

15. ### Classic Module Definition?

So to clarify what makes something a classic module:

- There must be an outer scope, typically from a module factory function running
  at least once.
- The module's inner scope must have at least one piece of hidden information
  that represents state for the module.
- The module must return on its public API a reference to at least one function
  that has closure over the hidden module state (so that this state is actually
  preserved).

16. ### Can you use ESM in not-strict-mode?

ESM files are assumed to be strict-mode, without needing a "use strict" pragma
at the top. There's no way to define an ESM as non-strict-mode.

17. ### Explain this snippet of code?

```
export { getName };

// ************************

var records = [
    { id: 14, name: "Kyle", grade: 86 },
    { id: 73, name: "Suzy", grade: 87 },
    { id: 112, name: "Frank", grade: 75 },
    { id: 6, name: "Sarah", grade: 91 }
];

function getName(studentID) {
    var student = records.find(
        student => student.id == studentID
    );
    return student.name;
}
```
