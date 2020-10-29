1. Why is **this** useful?
2. How many incorrect assumtion are there about **this**? name them?
3. Consider this code:

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

4. How to reference a function object form inside itself?
5. What is **argument.callee**? is it good practice to use it?
6. **this** refers to function lexical scope? T/F? explain?
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

8. Is **this** author-time binding or runtime binding?
9. For **this** binding, is it important to where a function declared or where it called?
10. When a function is invoked, an activation record(execution contex) is created, what information it contains?
