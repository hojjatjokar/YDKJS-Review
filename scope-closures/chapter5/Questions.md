# Chapter 1

1. ### Closure difinition?

Closures happen as a result of writing code that relies on lexical scope. They
just happen. You do not even really have to intentionally create closures to
take advantage of them. Closures are created and used for you all over your
code. What you are missing is the proper mental context to recognize, embrace,
and leverage closures for your own will.

2. ### Explain this code:

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

Function bar() has access to the variable a in the outer enclosing scope because
of lexical scope look-up rules (in this case, it's an RHS reference look-up).

Is this "closure"?

Well, technically... perhaps. But by our what-you-need-to-know definition
above... not exactly. I think the most accurate way to explain bar() referencing
a is via lexical scope look-up rules, and those rules are only (an important!)
part of what closure is.

From a purely academic perspective, what is said of the above snippet is that
the function bar() has a closure over the scope of foo() (and indeed, even over
the rest of the scopes it has access to, such as the global scope in our case).
Put slightly differently, it's said that bar() closes over the scope of foo().
Why? Because bar() appears nested inside of foo(). Plain and simple.

3. ### Explain this code:

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

We pass the inner function baz over to bar, and call that inner function
(labeled fn now), and when we do, its closure over the inner scope of foo() is
observed, by accessing a.

4. ### Explain this code

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

These passings-around of functions can be indirect, too. Whatever facility we
use to transport an inner function outside of its lexical scope, it will
maintain a scope reference to where it was originally declared, and wherever we
execute it, that closure will be exercised.

5. Explain this code:

```javascript
function wait(message) {
  setTimeout(function timer() {
    console.log(message);
  }, 1000);
}

wait('Hell, closure');
```

We take an inner function (named timer) and pass it to setTimeout(..). But timer
has a scope closure over the scope of wait(..), indeed keeping and using a
reference to the variable message.

A thousand milliseconds after we have executed wait(..), and its inner scope
should otherwise be long gone, that inner function timer still has closure over
that scope.

Deep down in the guts of the Engine, the built-in utility setTimeout(..) has
reference to some parameter, probably called fn or func or something like that.
Engine goes to invoke that function, which is invoking our inner timer function,
and the lexical scope reference is still intact.

6. ### When functions exercising closure? example?
   Essentially whenever and wherever you treat functions (which access their own
   respective lexical scopes) as first-class values and pass them around, you
   are likely to see those functions exercising closure. Be that timers, event
   handlers, Ajax requests, cross-window messaging, web workers, or any of the
   other asynchronous (or synchronous!) tasks, when you pass in a callback
   function, get ready to sling some closure around!
7. ### Explain this code:

```javascript
for(var i = 1; i <= 5; i++){
  setTimeout(funtion timer() {
    console.log(i);
  }, i*1000);
}
```

Firstly, let's explain where 6 comes from. The terminating condition of the loop
is when i is not <=5. The first time that's the case is when i is 6. So, the
output is reflecting the final value of the i after the loop terminates.

This actually seems obvious on second glance. The timeout function callbacks are
all running well after the completion of the loop. In fact, as timers go, even
if it was setTimeout(.., 0) on each iteration, all those function callbacks
would still run strictly after the completion of the loop, and thus print 6 each
time.

But there's a deeper question at play here. What's missing from our code to
actually have it behave as we semantically have implied?

What's missing is that we are trying to imply that each iteration of the loop
"captures" its own copy of i, at the time of the iteration. But, the way scope
works, all 5 of those functions, though they are defined separately in each loop
iteration, all are closed over the same shared global scope, which has, in fact,
only one i in it.

Put that way, of course all functions share a reference to the same i. Something
about the loop structure tends to confuse us into thinking there's something
else more sophisticated at work. There is not. There's no difference than if
each of the 5 timeout callbacks were just declared one right after the other,
with no loop at all.

OK, so, back to our burning question. What's missing? We need more cowbell
closured scope. Specifically, we need a new closured scope for each iteration of
the loop.

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

We learned in Chapter 3 that the IIFE creates scope by declaring a function and
immediately executing it. Does that work? Try it. Again, I'll wait.

I'll end the suspense for you. Nope. But why? We now obviously have more lexical
scope. Each timeout function callback is indeed closing over its own
per-iteration scope created respectively by each IIFE.

It's not enough to have a scope to close over if that scope is empty. Look
closely. Our IIFE is just an empty do-nothing scope. It needs something in it to
be useful to us.

9. ### Explain this code:

```javascript
for(var i = 1; i <= 5; i++){
  (funciton (j){
    setTimeout(function timer(){
      console.log(j);
    }, j * 1000);
  })(i);
}
```

It's not enough to have a scope to close over if that scope is empty. Look
closely. Our IIFE is just an empty do-nothing scope. It needs something in it to
be useful to us.

It needs its own variable, with a copy of the i value at each iteration. Of
course, since these IIFEs are just functions, we can pass in i, and we can call
it j if we prefer, or we can even call it i again. Either way, the code works
now.

The use of an IIFE inside each iteration created a new scope for each iteration,
which gave our timeout function callbacks the opportunity to close over a new
scope for each iteration, one which had a variable with the right per-iteration
value in it for us to access.

10. ### Explain code:

```javascript
for (let i = 1; i <= 5; i++) {
  setTimeout(function timer() {
    consoele.log(i);
  }, i * 1000);
}
```

Look carefully at our analysis of the previous solution. We used an IIFE to
create new scope per-iteration. In other words, we actually needed a
per-iteration block scope. Chapter 3 showed us the let declaration, which
hijacks a block and declares a variable right there in the block.

It essentially turns a block into a scope that we can close over. So, the
following awesome code "just works"

11. ### Revealing module? example

Firstly, CoolModule() is just a function, but it has to be invoked for there to
be a module instance created. Without the execution of the outer function, the
creation of the inner scope and the closures would not occur.

Secondly, the CoolModule() function returns an object, denoted by the
object-literal syntax { key: value, ... }. The object we return has references
on it to our inner functions, but not to our inner data variables. We keep those
hidden and private. It's appropriate to think of this object return value as
essentially a public API for our module.

This object return value is ultimately assigned to the outer variable foo, and
then we can access those property methods on the API, like foo.doSomething().

Note: It is not required that we return an actual object (literal) from our
module. We could just return back an inner function directly. jQuery is actually
a good example of this. The jQuery and \$ identifiers are the public API for the
jQuery "module", but they are, themselves, just a function (which can itself
have properties, since all functions are objects).

The doSomething() and doAnother() functions have closure over the inner scope of
the module "instance" (arrived at by actually invoking CoolModule()). When we
transport those functions outside of the lexical scope, by way of property
references on the object we return, we have now set up a condition by which
closure can be observed and exercised.

To state it more simply, there are two "requirements" for the module pattern to
be exercised:

There must be an outer enclosing function, and it must be invoked at least once
(each time creates a new module instance).

The enclosing function must return back at least one inner function, so that
this inner function has closure over the private scope, and can access and/or
modify that private state.

An object with a function property on it alone is not really a module. An object
which is returned from a function invocation which only has data properties on
it and no closured functions is not really a module, in the observable sense.

example:

```javascript
function CoolModule() {
  var something = 'cool';
  var another = [1, 2, 3];

  function doSomething() {
    console.log(something);
  }

  function doAnother() {
    console.log(another.join(' ! '));
  }

  return {
    doSomething: doSomething,
    doAnother: doAnother,
  };
}

var foo = CoolModule();

foo.doSomething(); // cool
foo.doAnother(); // 1 ! 2 ! 3
```

12. ### Requirements for module pattern to be exercised?

To state it more simply, there are two "requirements" for the module pattern to
be exercised:

- There must be an outer enclosing function, and it must be invoked at least
  once (each time creates a new module instance).

- The enclosing function must return back at least one inner function, so that
  this inner function has closure over the private scope, and can access and/or
  modify that private state.

13. ### An object with a function property on it alone is a module?

An object with a function property on it alone is not really a module.

14. ### An object which is returned from a function invocation which only has data properties on it, is this module?

An object which is returned from a function invocation which only has data
properties on it and no closured functions is not really a module, in the
observable sense.

15. Es6 modules?

ES6 adds first-class syntax support for the concept of modules. When loaded via
the module system, ES6 treats a file as a separate module. Each module can both
import other modules or specific API members, as well export their own public
API members.

Note: Function-based modules aren't a statically recognized pattern (something
the compiler knows about), so their API semantics aren't considered until
run-time. That is, you can actually modify a module's API during the run-time
(see earlier publicAPI discussion).

By contrast, ES6 Module APIs are static (the APIs don't change at run-time).
Since the compiler knows that, it can (and does!) check during (file loading
and) compilation that a reference to a member of an imported module's API
actually exists. If the API reference doesn't exist, the compiler throws an
"early" error at compile-time, rather than waiting for traditional dynamic
run-time resolution (and errors, if any).
