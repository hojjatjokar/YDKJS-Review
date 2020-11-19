# Chapter 4

1. ### Is Javascript interpreted line by line, top-down? All declarations, both

   variables and functions, are processed first, before any part of your code is
   executed.

2. ### Consider this line of code, what will be logged?

```javascript
a = 2;
var a;
console.log(a);
```

undefined

3.  ### consider this line of code, what will be logged?

```javascript
console.log(a);
var a = 2;
```

undefined

4. ### How javscript sees **var a = 2;**? How many statement? and each will processsed in which phase?

JavaScript thinks of it as two statements: var a; and a = 2;. The first
statement, the declaration, is processed during the compilation phase. The
second statement, the assignment, is left in place for the execution phase.

5. ### What's hoisting?
   Variable and function declarations are "moved" from where they appear in the
   flow of the code to the top of the code. This gives rise to the name
   "Hoisting".
6. ### Which one will hoisted?

- declarations
- assignments
- expressions
- executable logic

Only the declarations themselves are hoisted, while any assignments or other
executable logic are left in place. If hoisting were to re-arrange the
executable logic of our code, that could wreak havoc.

7. ### Consider this code:

```javascript
foo();

function foo() {
  console.log(a);
  var a = 2;
}
```

- Foo will be called? why?
- **variable a** will be what? why?

The function foo's declaration is hoisted, such that the call on the first line
is able to execute. And **undefined** will be logged

8. ### consider this code, What will be the result?

```javascript
foo();
var foo = function bar(){
  ...
};
```

The variable identifier foo is hoisted and attached to the enclosing scope
(global) of this program, so foo() doesn't fail as a ReferenceError. But foo has
no value yet (as it would if it had been a true function declaration instead of
expression). So, foo() is attempting to invoke the undefined value, which is a
TypeError illegal operation.

9. ### consider this code

```javascript
foo();
bar();
var foo = function bar(){
  ...
};
```

foo(); // TypeError bar(); // ReferenceError

10. ### consider this code, What will be logged?

```javascript
foo();

var foo;

function foo() {
  console.log(1);
}

foo = function () {
  console.log(2);
};
```

1 is printed instead of 2! 11. ### consider this code, what will be logged?

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

While multiple/duplicate var declarations are effectively ignored, subsequent
function declarations do override previous ones. so 3 will be logged.
