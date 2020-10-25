1. What scope models are there? JS has which one?
2. What's lexing?
3. What's lexical scope?
4. Highlight scopes?

```javascript
function foo(a) {
  var b = a * 2;

  function bar(c) {
    console.log(a, b, c);
  }

  bar(b * 3);
}

foo(2);
```

5. What's shadowing?
6. What's global variables? how can be accessed?
7. Where is function lexical scope?
8. How many mechanism are there for cheating lexical scope?
9. What's eval?
10. How can you programatically generate code inside your authored code?
11. How engine behave to eval(...)?
12. How eval(...) can modifies the existing lexical scope?
13. How eval(...) behave in strict-mode?
14. What's other facilities in javascript similar to **eval**? How they work?
    Which one is safer? Which one should be avoided?
15. What's **with** for?
16. How is **with** work?
17. Explain how is impacts of **eval** and **with** on performance
