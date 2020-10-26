1. What exactly makes a new bubble? is it only the function? can other
   structures in javascript create bubbles of scope?

2. Consider this code:

```javascript
function foo(a){
  var b = 2;

  function bar(){
    ...
  }

  var c = 3;
}
```

- The scope bubble for foo(...) includes which identifiers?
- The scope bubbke fir bar(...) has which identifiers?
- The scope bubble for global scope has which identifiers?
- This code in global scope has what result?

```javascript
bar();
console.log(a, b, c);
```

3. How to hide the code in plain scope?
4. What's principle of least privilege?
5. What's benefits of principle of least privilege?
6. Explain collisions in global namespaces and how they handle problem?
7. Another option for collision avoidance?
8. What's module management?
9. Problems of hiding in plain scope?
10. According to this code:

```javascript
var a = 2;
function foo() {
  var a = 3;
  console.log(a);
}
foo();
console.log();
```

- Show problems of this code
- Solve problems with afunction expression?

11. What's difference between function declaration vs. expression? with example?
    function name bound to where?
12. What is anonymous function expression?
13. Can function declarations ommit the name? why?
14. Drawback of anonymous function? (3)
15. IIFE pattern is stands for?
16. What is IIFE?
17. Most common form of IIFE?
18. Less common form of IIFE?
19. Which form is best practice? why?
20. JS has 4 facility for block scope? name them?
21. What's let and how it declare variable?
22. declarations made with let will hoist? why?
23. How block scoping is usefull relates to closures and garbage collection?
    with example?
24. Benefit of let for loops?(2)
25. What's const?
