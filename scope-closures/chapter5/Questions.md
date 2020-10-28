1. Closure difinition?

2. Explain this code:

```javascript
function foo() {
  var a = 2;

  function bar() {
    console.log(a);
  }

  return bar;
}
var baz = foo();
baz();
```

3. Explain this code:

```javascript
  function(){
    var a = 2;

    function baz(){
      consolel.log(a);
    }

    bar(baz);
  }

  function bar(fn){
    fn();
  }
```

4. explain this code

```javascript
var fn;
function foo() {
  var a = 2;

  function baz() {
    console.log(a);
  }

  fn = baz;
}

function bar() {
  fn();
}

foo();
bar();
```

5. explain this code:

```javascript
function wait(message) {
  setTimeout(function timer() {
    console.log(message);
  }, 1000);
}

wait('Hell, closure');
```

6. When functions exercising closure? example?
7. explain this code:

```javascript
for(var i = 1; i <= 5; i++){
  setTimeout(funtion timer() {
    console.log(i);
  }, i*1000);
}
```

8. Explain this code:

```javascript
for (var i = 1; i <= 5; i++) {
  (function () {
    setTimeout(function timer() {
      console.log(i);
    }, i * 1000);
  })();
}
```

9. Explain this code:

```javascript
for(var i = 1; i <= 5; i++){
  (funciton (j){
    setTimeout(function timer(){
      console.log(j);
    }, j * 1000);
  })(i);
}
```

10.

```javascript
for (let i = 1; i <= 5; i++) {
  setTimeout(function timer() {
    consoele.log(i);
  }, i * 1000);
}
```

11. Revealing module? example
12. Public API for module?
13. Requirements for module pattern to be exercised?
14. An object with a function property on it alone is a module?
15. An object which is returned from a function invocation which only has data
    properties on it, is this module?
16. Es6 modules?
