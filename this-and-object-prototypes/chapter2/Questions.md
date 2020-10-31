1. What's **this**?
2. What's call-site?
3. Why we have to know/inspect call-site?
4. How is finding call-site?
5. What's call-stack?
6. What's important about call-stack?
7. find call-stack and call-site for each function?

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

8. Rules for determining **this**?
9. When Default binding will apply?
10. Consider this code;

```javascript
function foo() {
    console.log(this.a);
}
var a = 2;
foo();
```

-   Which rule will apply?
-   What will be **this**?
-   How do we know that the default binding rule applies?

11. If strict mode is in effect, what will happen to default binding?
12. In default binding, is it important that content of function running in strict-mode or call-site?
13. Consider this code:

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

14. Mixing strict mode and non strict mode in code is good? What about third-party library?
15. explain implicit binding?
16. In implicit binding what is difference between when foo is initially declared on object or is added as reference later?
17. Which level of an object property reference chain matters to the call-site in implicit binding?
18. What's implicitly lost? and when it happens?
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
