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
   4. `new` Binding
9. ### When default binding will apply?
   Standalone `function` invocation. Think of this this rule as the default catch-all rule when none of the other rules apply.
10. ### Consider this code;

```javascript
function foo() {
  console.log(this.a);
}
var a = 2;
foo();
```

a. Which rule will apply?
b. What will be the value of `this`?
c. How do we know that the default binding rule applies?

Answer:

a. The **default binding** for this applies to the function call, and so points this at the global object
b. Global Object
c. We examine the call-site to see how `foo()` is called. In our snippet, `foo()` is called with a plain, un-decorated function reference. None of the other rules we will demonstrate will apply here, so the default binding applies instead.

11. ### If strict mode is in effect, what will happen to default binding?
    If strict mode is in effect, the global object is not eligible for the default binding, so the `this` is instead set to `undefined`.
12. ### In default binding, is it important that content of function running in strict-mode or call-site?
    A subtle but important detail is: even though the overall `this` binding rules are entirely based on the call-site, the global object is only eligible for the default binding if the contents of `foo()` are not running in strict mode; the strict mode state of the call-site of `foo()` is irrelevant.
13. ### Consider this code:

```javascript
function foo() {
  console.log(this.a);
}
var a = 2;
(function () {
  "use strict";
  foo();
})();
```

Answer:

```
// 2
```

14. ### Is mixing strict mode and non strict mode in code good? What about third-party library?
    Intentionally mixing strict mode and non-strict mode together in your own code is generally frowned upon. Your entire program should probably either be Strict or non-Strict. However, sometimes you include a third-party library that has different Strict'ness than your own code, so care must be taken over these subtle compatibility details.
15. ### Explain implicit binding?

Another rule to consider is: does the call-site have a **context object,** also referred to as an owning or containing object, though these alternate terms could be slightly misleading.

When there is a context object for a function reference, the implicit binding rule says that it's that object which should be used for the function call's this binding.

16. ### In implicit binding what is difference between when `foo` is initially declared on object or is added as reference later?

Another rule to consider is: does the call-site have a **context object,** also referred to as an owning or containing object, though these alternate terms could be slightly misleading.

When there is a context object for a function reference, the implicit binding rule says that it's that object which should be used for the function call's this binding.

17. ### Which level of an object property reference chain matters to the call-site in implicit binding?

    Only the top/last level of an object property reference chain matters to the call-site. For instance:

    ```javascript
    function foo() {
      console.log(this.a);
    }

    var obj2 = {
      a: 42,
      foo: foo,
    };

    var obj1 = {
      a: 2,
      obj2: obj2,
    };

    obj1.obj2.foo(); // 42
    ```

18. ### What's implicitly lost? When it happens?

One of the most common frustrations that `this` binding creates is when an implicitly bound function loses that binding, which usually means it falls back to the default binding, of either the global object or `undefined`, depending on `strict mode`.

19. ### How implicitly lost happens with assigning variable?

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
  foo: foo,
};

var bar = obj.foo; // function reference/alias!

var a = "oops, global"; // `a` also property on global object

bar(); // "oops, global"
```

Even though bar appears to be a reference to `obj.foo`, in fact, it's really just another reference to foo itself. Moreover, the call-site is what matters, and the call-site is `bar()`, which is a plain, un-decorated call and thus the default binding applies.

20. ### How implicitly lost happens with passing a call back function?

The more subtle, more common, and more unexpected way this occurs is when we consider passing a callback function:

```javascript
function foo() {
  console.log(this.a);
}

function doFoo(fn) {
  // `fn` is just another reference to `foo`

  fn(); // <-- call-site!
}

var obj = {
  a: 2,
  foo: foo,
};

var a = "oops, global"; // `a` also property on global object

doFoo(obj.foo); // "oops, global"
```

Parameter passing is just an implicit assignment, and since we're passing a function, it's an implicit reference assignment, so the end result is the same as the previous snippet.

21. ### Does implicitly lost happen if function is built-in?

No difference, same outcome.

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
  foo: foo,
};

var a = "oops, global"; // `a` also property on global object

setTimeout(obj.foo, 100); // "oops, global"
```

22. ### What is explicit binding?

With *implicit binding* as we just saw, we had to mutate the object in question to include a reference on itself to the function and use this property function reference to indirectly (implicitly) bind `this` to the object.

If you want to force a function call to use a particular object for `this` binding, without putting a property function reference on the object you have to use explicit binding.

23. ### Which methods are there for explicit binding?

"All" functions in the language have some utilities available to them (via their [[Prototype]]) which can be useful for this task. Specifically, functions have `call(..)` and `apply(..)` methods. Technically, JavaScript host environments sometimes provide functions which are special enough that they do not have such functionality. But those are few. The vast majority of functions provided, and certainly all functions you will create, do have access to `call(..)` and `apply(..)`.

24. ### How `call` and `apply` methods work?

They both take, as their first parameter, an object to use for the this, and then invoke the function with that this specified. Since you are directly stating what you want the this to be, we call it explicit binding.

```javascript
function foo() {
  console.log(this.a);
}

var obj = {
  a: 2,
};

foo.call(obj); // 2
```

Invoking foo with explicit binding by `foo.call(..)` allows us to force its this to be obj.

25. ### What will happen If you pass a simple primitive value as the this binding to `apply` or `call`?

If you pass a simple primitive value (of type string, boolean, or number) as the this binding, the primitive value is wrapped in its object-form (`new String(..)`, `new Boolean(..)`, or `new Number(..)`, respectively). This is often referred to as "boxing".

26. ### What's the difference between call and apply with respect to `this`?

With respect to this binding, `call(..)` and `apply(..)` are identical. They do behave differently with their additional parameters, but that's not something we care about presently.

27. ### What is explicit binding response to losing `this` binding (implicit lost)?

Unfortunately, explicit binding alone still doesn't offer any solution to the issue mentioned previously, of a function "losing" its intended this binding, or just having it paved over by a framework, etc.

28. ### What is hard binding?

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

bar(); // 2
setTimeout(bar, 100); // 2

// `bar` hard binds `foo`'s `this` to `obj`
// so that it cannot be overriden
bar.call(window); // 2
```

We create a function `bar()` which, internally, manually calls `foo.call(obj)`, thereby forcibly invoking `foo` with `obj` binding for `this`. No matter how you later invoke the function bar, it will always manually invoke `foo` with `obj`. This binding is both explicit and strong, so we call it hard binding.

29. ### Explain

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

30. ### What is `function.prototype.bind` ? How it works?

Since hard binding is such a common pattern, it's provided with a built-in utility as of ES5: `Function.prototype.bind`, and it's used like this:

```jsx
function foo(something) {
  console.log(this.a, something);
  return this.a + something;
}

var obj = {
  a: 2,
};

var bar = foo.bind(obj);

var b = bar(3); // 2 3
console.log(b); // 5
```

`bind(..)` returns a new function that is hard-coded to call the original function with the this context set as you specified.

31. ### What is API call context? What they use internally?

Many libraries' functions, and indeed many new built-in functions in the JavaScript language and host environment, provide an optional parameter, usually called "context", which is designed as a work-around for you not having to use `bind(..)` to ensure your callback function uses a particular this.

Internally, these various functions almost certainly use explicit binding via `call(..)` or `apply(..)`, saving you the trouble.

32. ### What is constructor in traditional class-oriented languages?

In traditional class-oriented languages, "constructors" are special methods attached to classes, that when the class is instantiated with a `new` operator, the constructor of that `class` is called. This usually looks something like this:

```javascript
something = new MyClass(..);
```

33. ### What is constructor in JS? Is it constructor function or constructor call? are they special funtion?

First, let's re-define what a "constructor" in JavaScript is. In JS, constructors are just functions that happen to be called with the `new` operator in front of them. They are not attached to classes, nor are they instantiating a class. They are not even special types of functions. They're just regular functions that are, in essence, hijacked by the use of `new` in their invocation.

34. ### What is the relationship between JS constructor and class oriented constructor?

JavaScript has a `new` operator, and the code pattern to use it looks basically identical to what we see in those class-oriented languages; most developers assume that JavaScript's mechanism is doing something similar. However, there really is no connection to class-oriented functionality implied by new usage in JS.

35. ### What things automatically happen When a `function` is invoked with `new` keyword in front of it (constructor call)?

When a `function` is invoked with `new` in front of it, otherwise known as a constructor call, the following things are done automatically:

1. A brand new `object` is created (aka, constructed) out of thin air
2. _The newly constructed object is `[[Prototype]]`linked_
3. The newly constructed object is set as the `this` binding for that function call
4. Unless the function returns its own alternate **object**, the `new` invoked function call will *automatically* return the newly constructed object.

-

36. ### Explain

```javascript
function foo(a) {
  this.a = a;
}
var bar = new foo(2);
console.log(bar.a); // ?
```

By calling `foo(..)` with `new` in front of it, we've constructed a new object and set that new object as the this for the call of foo(..). So `new` is the final way that a function call's this can be bound. We'll call this `new` binding.

37. ### If the call-site has multiple eligible rules which will be apply? what order?

- The default binding
- Implicit binding
- Explicit binding
- `new` being able to override hard binding

38. ### How hard bind physically works?

`Function.prototype.bind(..)` creates a new wrapper function that is hard-coded to ignore its own this binding (whatever it may be), and use a manual one we provide. the built-in `Function.prototype.bind(..)` as of ES5, The part that's allowing `new` overriding is:

```javascript
this instanceof fNOP && oThis ? this : oThis;

// ... and:

fNOP.prototype = this.prototype;
fBound.prototype = new fNOP();
```

39. ### Why is usful for the `new` keyword to able to override hardbinding?

The primary reason for this behavior is to create a function (that can be used with new for constructing objects) that essentially ignores the this hard binding but which presets some or all of the function's arguments. One of the capabilities of `bind(..)` is that any arguments passed after the first this binding argument are defaulted as standard arguments to the underlying function (technically called "partial application", which is a subset of "currying").

40. ### What is prtial application/curring/defaulted argument? example?

One of the capabilities of `bind(..)` is that any arguments passed after the first this binding argument are defaulted as standard arguments to the underlying function (technically called "partial application", which is a subset of "currying").

```javascript
function foo(p1, p2) {
  this.val = p1 + p2;
}

// using `null` here because we don't care about
// the `this` hard-binding in this scenario, and
// it will be overridden by the `new` call anyway!
var bar = foo.bind(null, "p1");

var baz = new bar("p2");

baz.val; // p1p2
```

41. ### Ask 4 question to determine `this`?

1. Is the function called with `new` (**new binding**)? If so, `this` is the newly constructed object.

   ```jsx
   var bar = new foo();
   ```

1. Is the function called with `call` or `apply` (**explicit binding**), even hidden inside a `bind` *hard binding*? If so, `this` is the explicitly specified object.

   ```jsx
   var bar = foo.call(obj2);
   ```

1. Is the function called with a context (**implicit binding**), otherwise known as an owning or containing object? If so, `this` is *that* context object.

   ```jsx
   var bar = obj1.foo();
   ```

-

42. ### What are binding exeptions?

- Ignored this
- Indirection

43. ### When ignored `this` will happen? and what will be applies?

If you pass null or undefined as a this binding parameter to `call`, `apply`, or `bind`, those values are effectively ignored, and instead, the default binding rule applies to the invocation.

44. ### Explain

```javascript
function foo() {
  console.log(this.a);
}
var a = 2;
foo.call(null);
```

45. ### What are usages of passing something like `null` for a `this` binding?

It's quite common to use `apply(..)` for spreading out arrays of values as parameters to a function call. Similarly, `bind(..)` can curry parameters (pre-set values), which can be very helpful.

46. ### Explain

```javascript
function foo(a, b) {
  console.log("a: " + a + "b: " + b);
}
foo.apply(null, [2, 3]); // ?
var bar = foo.bind(null, 2);
bar(3); // ?
```

47. ### ES6 subsitute option for `spread out`?

ES6 has the `...` spread operator which will let you syntactically "spread out" an array as parameters without needing `apply(..)`, such as `foo(...[1,2])`, which amounts to `foo(1,2)` -- syntactically avoiding a this binding if it's unnecessary.

48. ### ES6 subsitute option for `curring`?

Unfortunately, there's no ES6 syntactic substitute for currying, so the this parameter of the `bind(..)` call still needs attention.

49. ### Is there any danger in using `null` when you don't care about the `this` binding ?What's safer `this`?

Perhaps a somewhat "safer" practice is to pass a specifically set up object for `this` which is guaranteed not to be an object that can create problematic side effects in your program. Borrowing terminology from networking (and the military), we can create a "DMZ" (de-militarized zone) object -- nothing more special than a completely empty, non-delegated (see Chapters 5 and 6) object.

If we always pass a DMZ object for ignored `this` bindings we don't think we need to care about, we're sure any hidden/unexpected usage of `this` will be restricted to the empty object, which insulates our program's `global` object from side-effects.

50. ### What's indirection in binding exceptions?

Another thing to be aware of is you can (intentionally or not!) create "indirect references" to functions, and in those cases, when that function reference is invoked, the default binding rule also applies.

51. ### Explain the result?

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

52. ### Softening binding? why?

We saw earlier that *hard binding* was one strategy for preventing a function call falling back to the *default binding* rule inadvertently, by forcing it to be bound to a specific `this` (unless you use `new` to override it!). The problem is, *hard-binding* greatly reduces the flexibility of a function, preventing manual `this` override with either the *implicit binding* or even subsequent *explicit binding* attempts.

It would be nice if there was a way to provide a different default for *default binding* (not `global` or `undefined`), while still leaving the function able to be manually `this` bound via *implicit binding* or *explicit binding* techniques.

53. ### Soft bind utility?

    We can construct a so-called soft binding utility which emulates our desired behavior.

    ```javascript
    if (!Function.prototype.softBind) {
      Function.prototype.softBind = function (obj) {
        var fn = this,
          curried = [].slice.call(arguments, 1),
          bound = function bound() {
            return fn.apply(
              !this ||
                (typeof window !== "undefined" && this === window) ||
                (typeof global !== "undefined" && this === global)
                ? obj
                : this,
              curried.concat.apply(curried, arguments)
            );
          };
        bound.prototype = Object.create(fn.prototype);
        return bound;
      };
    }
    ```

54. ### Explain?

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

55. ### What's lexical this ?

    Normal functions abide by the 4 rules we just covered. But ES6 introduces a special kind of function that does not use these rules: arrow-function.
    instead of using the four standard `this` rules, arrow-functions adopt the `this` binding from the enclosing (function or global) scope.

56. ### Explain?

```javascript
function foo() {
  // return an arrow function
  return (a) => {
    // `this` here is ?
    console.log(this.a);
  };
}

var obj1 = {
  a: 2,
};

var obj2 = {
  a: 3,
};

var bar = foo.call(obj1);
bar.call(obj2); // ?
```

Answer:

```javascript
function foo() {
  // return an arrow function
  return (a) => {
    // `this` here is lexically adopted from `foo()`
    console.log(this.a);
  };
}

var obj1 = {
  a: 2,
};

var obj2 = {
  a: 3,
};

var bar = foo.call(obj1);
bar.call(obj2); // 2, not 3!
```

The arrow-function created in `foo()` lexically captures whatever `foo()`s this is at its call-time. Since `foo()` was this-bound to `obj1`, bar (a reference to the returned arrow-function) will also be this-bound to `obj1`. The lexical binding of an arrow-function cannot be overridden (even with new!).
