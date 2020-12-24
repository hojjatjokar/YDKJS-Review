1. ### What's `this`?

`this` is a binding made for each function invocation, based entirely on its call-site (how the function is called).

2. ### What's call-site?
    The location in code where a function is called (not where it's declared)
3. ### Why we have to know/inspect call-site?
    To understand this binding, we have to understand the call-site: the location in code where a function is called (not where it's declared). We must inspect the call-site to answer the question: what's this this a reference to?
4. ### How is finding call-site?

Finding the call-site is generally: "go locate where a function is called from", but it's not always that easy, as certain coding patterns can obscure the true call-site.

What's important is to think about the call-stack (the stack of functions that have been called to get us to the current moment in execution). The call-site we care about is in the invocation before the currently executing function.

5. ### What's call-stack?

The stack of functions that have been called to get us to the current moment in execution

6. ### What's important about call-stack?

The call-site we care about is in the invocation before the currently executing function.

7. ### Find call-stack and call-site for each function?

```javascript
function baz() {
    // call-stack is:
    // call-site is:
    console.log("baz");
    bar();
}

function bar() {
    // call stack is:
    // call-site is:
    consolel.log("bar");
    foo();
}
function foo() {
    // call stack is:
    // call-site is:
    console.log("foo");
}
baz(); // call site for?
```

8. ### Rules for determining `this`?
    1. Default Binding
    2. Implicit Binding
    3. Explicit Binding
    4. new Binding
9. ### When Default binding will apply?
    standalone function invocation. Think of this this rule as the default catch-all rule when none of the other rules apply.
10. ### Consider this code;

```javascript
function foo() {
    console.log(this.a);
}
var a = 2;
foo();
```

1. Which rule apply?
2. What will be **_this_**?
3. How do we know that the default binding rule applies?

Answer:

1.  The **default binding** for this applies to the function call, and so points this at the global object
2.  Global Object
3.  We examine the call-site to see how `foo()` is called. In our snippet, `foo()` is called with a plain, un-decorated function reference. None of the other rules we will demonstrate will apply here, so the default binding applies instead.

-

11. ### If strict mode is in effect, what will happen to default binding?
    If strict mode is in effect, the global object is not eligible for the default binding, so the this is instead set to undefined.
12. ### In default binding, is it important that content of function running in strict-mode or call-site?
    A subtle but important detail is: even though the overall this binding rules are entirely based on the call-site, the global object is only eligible for the default binding if the contents of foo() are not running in strict mode; the strict mode state of the call-site of foo() is irrelevant.
13. ### Consider this code:

```javascript
function foo() {
    console.log(this.a);
}
var a = 2;
(function () {
    "use strict";
    foo(); // 2
})();
```

14. ### Mixing strict mode and non strict mode in code is good? What about third-party library?
    Note: Intentionally mixing strict mode and non-strict mode together in your own code is generally frowned upon. Your entire program should probably either be Strict or non-Strict. However, sometimes you include a third-party library that has different Strict'ness than your own code, so care must be taken over these subtle compatibility details.
15. ### Explain implicit binding?

Another rule to consider is: does the call-site have a **context object,** also referred to as an owning or containing object, though these alternate terms could be slightly misleading.

When there is a context object for a function reference, the implicit binding rule says that it's that object which should be used for the function call's this binding.

16. ### In implicit binding what is difference between when foo is initially declared on object or is added as reference later?

Another rule to consider is: does the call-site have a **context object,** also referred to as an owning or containing object, though these alternate terms could be slightly misleading.

When there is a context object for a function reference, the implicit binding rule says that it's that object which should be used for the function call's this binding.

17. ### Which level of an object property reference chain matters to the call-site in implicit binding?

    Only the top/last level of an object property reference chain matters to the call-site. For instance:

    ```
    function foo() {
        console.log( this.a );
    }

    var obj2 = {
        a: 42,
        foo: foo
    };

    var obj1 = {
        a: 2,
        obj2: obj2
    };

    obj1.obj2.foo(); // 42
    ```

18. ### What's implicitly lost? and when it happens?
19. Implicitly lost when assigning variable? example?
20. Implicitly lost when passing a call back function?
21. What if the function is built-in for implicitly lost, what is difference?
22. What is explicit binding?
23. Which methods for explicit binding?
24. How call, apply work? example?
25. If you pass a simple primitive value as the this binding to apply or call, what will happen?
26. What's difference between call and apply with respect to this?
27. What is explicit binding response to losing this binding (implicit lost)?
28. What is hard binding? example
29. Explain

```javascript
function foo() {
    console.log(this.a);
}
var obj = {
    a: 2,
};
var bar = function () {
    foo.call(obj);
};
bar(); // ?
setTimeout(bar, 100); // ?
bar.call(window); // ?
```

30. **function.prototype.bind** ? why provided? how it works? example
31. What is API call context? example? what they use internall?
32. In traditional class-oriented languages, what is constructor?
33. In JS what is constructor? constructor function or constructor call? are they special funtion?
34. What is relationship between JS constructor and class oriented constructor?
35. When a function is invoked with new in front of it (constructor call), what things will automatically happens?
36.

```javascript
function foo(a) {
    this.a = a;
}
var bar = new foo(2);
console.log(bar.a); // ?
```

37. If the call-site has multiple eligible rules which will be apply? what order?
38. How har bind physical works?
39. Why is new being able to override hardbinding useful?
40. What is prtial application/curring/defaulted argument? example?
41. Ask 4 question to determine **this**?
42. What are binding exeptions?
43. When ignored **this** will happen? and what will be applies?
44.

```javascript
function foo() {
    console.log(this.a);
}
var a = 2;
foo.call(null);
```

45. Why would intentionally pass something like **null** for a **this** binding?
46.

```javascript
function foo(a, b) {
    console.log("a: " + a + "b: " + b);
}
foo.apply(null, [2, 3]); // ?
var bar = foo.bind(null, 2);
bar(3); // ?
```

47. ES6 subsitute option for **spread out**?
48. ES6 subsitute option for **curring**?
49. Is there **danger** in using **null** when you don't care about the **this** binding ?What's safer **this**?
50. What's indirection in binding exceptions?
51.

```javascript
function foo() {
    console.log(this.a);
}
var a = 2;
var o = {
    a: 3,
    foo: foo,
};
var p = {
    a: 3,
};
o.foo(); // ??
(o.foo = o.foo)(); // ??
```

52. Softening binding? why?
53. Soft bind utility?
54.

```javascript
function foo() {
    console.log("name: " + this.name);
}
var obj = { name: "obj" },
    obj2 = { name: "obj2" },
    obj3 = { name: "obj3" };
var fooOBJ = foo.softBind(obj);
fooObj();
obj2.foo = foo.softBind(obj);
obj2.foo(); // ??
fooOBJ.call(obj3); // ??
setTimeout(obj2.foo, 10); // ??
```
