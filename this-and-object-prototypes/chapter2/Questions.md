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
26.
