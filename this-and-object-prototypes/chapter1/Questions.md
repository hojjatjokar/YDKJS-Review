1. ### Why is **this** useful?

    `this` mechanism provides a more elegant way of implicitly "passing along" an object reference, leading to cleaner API design and easier re-use.

2. ### How many incorrect assumtion are there about **this**? name them?

-   assumption with `this` refers to the function **itself**
-   assumption with `this` refers to the **function's Scope**

3. ### Consider this code:

```javascript
function foo(num) {
    console.log("foo: " + num);
    this.count++;
}

foo.count = 0;
var i;
for (i = 0; i < 10; i++) {
    if (i > 5) {
        foo(i);
    }
}
console.log(foo.count);
```

-   **foo.count** value will be?
-   **foo** will call how many times?
-   Explain the code?
-   What's the problem with this code?
-   Solve the problem with lexical scoope?
-   What's problem solving with lexical scope?
-   Solve the problem using function object reference
-   What's problem solving with using function object?
-   Solve using **this**

4. ### How to reference a function object form inside itself?
    To reference a function object from inside itself, `this` by itself will typically be insufficient. You generally need a reference to the function object via a lexical identifier (variable) that points at it.

```javascript
function foo() {
    foo.count = 4; // `foo` refers to itself
}

setTimeout(function () {
    // anonymous function (no name), cannot
    // refer to itself
}, 10);
```

In the first function, called a "named function", `foo` is a reference that can be used to refer to the function from inside itself.

5. ### What is `argument.callee`? is it good practice to use it?

The old-school but now deprecated and frowned-upon `arguments.callee` reference inside a function also points to the function object of the currently executing function. This reference is typically the only way to access an anonymous function's object from inside itself. The best approach, however, is to avoid the use of anonymous functions altogether, at least for those which require a self-reference, and instead use a named function (expression). `arguments.callee` is deprecated and should not be used.

6. ### `this` refers to function lexical scope? T/F? explain?

The next most common misconception about the meaning of `this` is that it somehow refers to the function's scope.

To be clear, `this` does not, in any way, refer to a function's **lexical scope**. It is true that internally, scope is kind of like an object with properties for each of the available identifiers. But the scope "object" is not accessible to JavaScript code. It's an inner part of the *Engine*'s implementation.

7. What's problems with this code?

```javascript
function foo() {
    var a = 2;
    this.bar();
}
function bar() {
    console.log(this.a);
}
foo();
```

There's more than one mistake in this snippet. While it may seem contrived, the code you see is a distillation of actual real-world code that has been exchanged in public community help forums. It's a wonderful (if not sad) illustration of just how misguided this assumptions can be.

8. ### Is **this** author-time binding or runtime binding?

`this` is not an author-time binding but a runtime binding.

9. For **this** binding, is it important to where a function declared or where it called?

`this` binding has nothing to do with where a function is declared, but has instead everything to do with the manner in which the function is called.

10. ### When a function is invoked, an activation record(execution contex) is created, what information it contains?

When a function is invoked, an activation record, otherwise known as an execution context, is created. This record contains information about where the function was called from (the call-stack), how the function was invoked, what parameters were passed, etc. One of the properties of this record is the this reference which will be used for the duration of that function's execution.
