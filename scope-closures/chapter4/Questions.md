1. Is Javascript interpreted line by line, top-down? explain

2. Consider this line of code, what will be logged?

```javascript
a = 2;
var a;
console.log(a);
```

3. consider this line of code, what will be logged?

```javascript
console.log(a);
var a = 2;
```

4. How javscript sees **var a = 2;**? How many statement? and each will
   processsed in which phase?

5. What's hoisting?
6. Which one will hoisted?

- declarations
- assignments
- expressions
- executable logic

7. Consider this code:

```javascript
function foo() {
  console.log(a);
  var a = 2;
}
```

- Foo will be called? why?
- **variable a** will be what? why?

8. consider this code

```javascript
foo();
var foo = function bar(){
  ...
};
```

- What will be the result?
- If error happens what error it will be? why?

9. consider this code

```javascript
foo();
bar();
var foo = function bar(){
  ...
};
```

- What will happen?
- How it interpreted?

10. consider

```javascript
foo();
var foo();
function foo(){
  console.log(1);
}
foo = function()
```

- What will be logged?
- This snippet will interpreted as?

11. consider :

```javascript
foo();
function foo() {
  console.log(1);
}
var foo = function () {
  console.log(2);
};
function foo() {
  console.log(3);
}
```

- what will be logged?
