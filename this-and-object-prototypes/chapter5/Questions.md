1. ### What's **[[prototype]]**?

Objects in JavaScript have an internal property, denoted in the specification as `[[Prototype]]`, which is simply a reference to another object. Almost all objects are given a non-null value for this property, at the time of their creation.

2. ### The default [[GET]] operatopn, if it cannot find the requested property on the object directly what happens?

The default [[Get]] operation proceeds to follow the [[Prototype]] link of the object if it cannot find the requested property on the object directly.

3. ### What will be output?

```javascript
var anotherObject = {
  a: 2,
};
var myObject = Object.create(anotherObject);
myObject.a; // ?
```

The output will be 2

4. ### What's return result from the [[GET]] operation if no matching property ever found by the end of the chain?

If no matching property is ever found by the end of the chain, the return result from the [[Get]] operation is undefined.

5. ### Where exactly does the [[prototype]] chain ends?

The top-end of every normal [[Prototype]] chain is the built-in Object.prototype.

6. ### `Object.prototype` includes what?

This object includes a variety of common utilities used all over JS, because all normal (built-in, not host-specific extension) objects in JavaScript "descend from" (aka, have at the top of their [[Prototype]] chain) the Object.prototype object.

7. ### Setting properties on object if property doesn't exist on objects?

If `property` is not already present directly on `object`, the `[[Prototype]]` chain is traversed, just like for the `[[Get]]` operation. If `property` is not found anywhere in the chain, the property `property` is added directly to `myObject` with the specified value, as expected.

However, if `property` is already present somewhere higher in the chain:

a. If a normal data accessor property is found anywhere higher on the `[[Prototype]]` chain, **and it's not marked as read-only (`writable:false`)** then a new `property` is added directly to `object`, resulting in a **shadowed property**.
b. If a `property` is found higher on the `[[Prototype]]` chain, but it's marked as **read-only (`writable: false`)**, then both the setting of that existing property as well as the creation of the shadowed property on `object` **are disallowed**. If the code is running in `strict mode`, an error will be thrown. Otherwise, the setting of the property value will silently be ignored. Either way, **no shadowing occurs**.
c. If a `property` is found higher on the `[[Prototype]]` chain and it's a setter, then the setter will always be called. No `property` will be added to (aka, shadowed on) `object`, nor will the `property` setter be redefined.

8. ### What's shadowing?

If the property name foo ends up both on myObject itself and at a higher level of the [[Prototype]] chain that starts at myObject, this is called shadowing. The foo property directly on myObject shadows any foo property which appears higher in the chain, because the myObject.foo look-up would always find the foo property that's lowest in the chain.

9. ### 3 scenarios for the **myObject.foo = "bar"** assignment when foo is not already on myObject directly, but is at a higher level of myObject's [[prototype]] chain?

a. If a normal data accessor property named `foo` is found anywhere higher on the `[[Prototype]]` chain, **and it's not marked as read-only (`writable:false`)** then a new property called `foo` is added directly to `myObject`, resulting in a **shadowed property**.

b. If a `foo` is found higher on the `[[Prototype]]` chain, but it's marked as **read-only (`writable:false`)**, then both the setting of that existing property as well as the creation of the shadowed property on `myObject` **are disallowed**. If the code is running in `strict mode`, an error will be thrown. Otherwise, the setting of the property value will silently be ignored. Either way, **no shadowing occurs**.

c. If a `foo` is found higher on the `[[Prototype]]` chain and it's a setter, then the setter will always be called. No `foo` will be added to (aka, shadowed on) `myObject`, nor will the `foo` setter be redefined.

10. ### What's whole scenarios for setting property a value?
    If property is present in object:

- If has setter, the setter will be called
- Else if `writable: false`, assignment will be ignored
- Else assignment be done as normal

If property is not present in object:

- If not present in its prototype, assignment take affect as normal
- If it's present in its prototype chain and is `writable: false`, the assignment will not take effect
- If it's present in its prototype chain, and has setter , setter will be called
- If it's present in its prototype chain, and does not have setter and doesn't have `writable: false` it will be shadowed

11. ### If a property on Object is **writable: false** higher in [[prototype]] chain how can it be shadowed?
    If you want to shadow foo in cases #2 and #3, you cannot use = assignment, but must instead use Object.defineProperty(..)  to add foo to myObject.
12. ### What's result? why? explain

```javascript
var anotherObject = {
  a: 2,
};
var myObject = Object.create(anotherObject);
anotherObject.a;
myObject.a;
myObject.hasOwnProperty("a"); // ?
anotherObject.hasOwnProperty("a"); // ?
myObject.a++;
anotherObject.a; // ?
myObject.a; // ?
anotherObject.hasOwnProperty("a"); // ?
myObject.hasOwnProperty("a"); // ?
```

Though it may appear that `myObject.a++` should (via delegation) look-up and just increment the `anotherObject.a` property itself *in place*, instead the `++` operation corresponds to `myObject.a = myObject.a + 1`. The result is `[[Get]]` looking up `a` property via `[[Prototype]]` to get the current value `2` from `anotherObject.a`, incrementing the value by one, then `[[Put]]` assigning the `3` value to a new shadowed property `a` on `myObject`. Oops!

Be very careful when dealing with delegated properties that you modify. If you wanted to increment `anotherObject.a`, the only proper way is `anotherObject.a++`.

13. ### Class function?

All functions by default get a public, non-enumerable property on them called `prototype`, which points at an otherwise arbitrary object. This object is often called "Foo's prototype".

Each object created from calling `new Foo()` will end up `[[Prototype]]`-linked to this "Foo dot prototype" object.

14. ### Explain

```javascript
function Foo() {}
var a = new Foo();
Object.getPrototypeOf(a) === Foo.prototype; // ?
```

When a is created by calling new Foo(), one of the things (see Chapter 2 for all four steps) that happens is that a gets an internal [[Prototype]] link to the object that Foo.prototype is pointing at.

15. ### When an object created by calling **new Foo()** one of things that happen is what?

Each object created from calling new Foo() will end up [[Prototype]]-linked to this "Foo dot prototype" object.

16. ### What's the difference between constructing objects in class-oriented languages and Javascript?
    **In class-oriented languages**, multiple **copies** (aka, "instances") of a class can be made, like stamping something out from a mold. As we saw in Chapter 4, this happens because the process of instantiating (or inheriting from) a class means, "copy the behavior plan from that class into a physical object", and this is done again for each new instance.
    **But in JavaScript,** there are no such copy-actions performed. You don't create multiple instances of a class. You can create multiple objects that `[[Prototype]]` *link* to a common object. But by default, no copying occurs, and thus these objects don't end up totally separate and disconnected from each other, but rather, quite **_linked_**.
17. ### When constructing an object in Javascript, what's the relation between constructor function and created objected?
    But in JavaScript, there are no such copy-actions performed. You don't create multiple instances of a class. You can create multiple objects that [[Prototype]] link to a common object. But by default, no copying occurs, and thus these objects don't end up totally separate and disconnected from each other, but rather, quite linked.
18. ### **new Foo()** is direct or indirect way to (a new object linked) to another object? what's direct way?
    In fact, the secret, which eludes most JS developers, is that the `new Foo()` function calling had really almost nothing *direct* to do with the process of creating the link. **It was sort of an accidental side-effect.** `new Foo()` is an indirect, round-about way to end up with what we want: **a new object linked to another object**.
    Can we get what we want in a more *direct* way? **Yes!** The hero is `Object.create(..)`. But we'll get to that in a little bit.
19. ### In JS we don't make copy from one object (class) to another (instance), what we make?
    a new object linked to another object.
20. ### prototypal inheritance? is this term ok? why?
21. ### Differential inheritance?
22. ### What exactly leads us to think Foo is a "class"?
    For one, we see the use of the new keyword, just like class-oriented languages do when they construct class instances. For another, it appears that we are in fact executing a constructor method of a class, because Foo() is actually a method that gets called, just like how a real class's constructor gets called when you instantiate that class.
23. ### What will be the rusult?

```javascript
fucntion Foo() {}
var a = {};
a.constructor === Foo; // ?
a.constructor === Foo.constructor; // ?
a.constructor === Foo.prototype.constructor; // ?
a.constructor === Foo.__prototype__.constructor; // ?
a.__proto__.constructor === Foo; // ?
a.__proto__.constructor === Foo.constructor; // ?
a.__proto__.constructor === Foo.prototype.constructor; // ?
a.__proto__.constructor === Foo.__proto__.constructor; // ?
```

Answer: `false`

24. ### Constructor function or constructor call?
    In reality, `Foo` is no more a "constructor" than any other `function` in your program. Functions themselves are not constructors. However, when you put the new keyword in front of a normal function call, that makes that function call a "constructor call". In fact, new sort of hijacks any normal function and calls it in a fashion that constructs an object, in addition to whatever else it was going to do.
25. ### This snippet shows two additional **"class orientation"** tricks in play:

```javascript
function Foo(name) {
  this.name = name;
}
Foo.prototype.myName = function () {
  return this.name;
};
var a = new Foo("a");
var b = new Foo("b");
a.myName();
b.myName();
```

This snippet shows two additional "class-orientation" tricks in play:

a. `this.name = name`: adds the `.name` property onto each object (`a` and `b`, respectively; see Chapter 2 about `this` binding), similar to how class instances encapsulate data values.
b. `Foo.prototype.myName = ...`: perhaps the more interesting technique, this adds a property (function) to the `Foo.prototype` object. Now, `a.myName()` works, but perhaps surprisingly. How?

26. ### Explain code? How it end up to delegate to object constructor?

```javascript
function foo() {}
Foo.prototype = {};
var a1 = new Foo(); // ?
a1.constructor === Foo; // ?
a1.constructor === Object; // ?
```

Answer:

```javascript
a1.constructor === Foo; // false

a1.constructor === Object; // true
```

27. ### The words "constructor" and "prototype" only have a what meaning? loose default meaning? why?

The fact is, `.constructor` on an object arbitrarily points, by default, at a function who, reciprocally, has a reference back to the object -- a reference which it calls `.prototype`. The words "constructor" and "prototype" only have a loose default meaning that might or might not hold true later. The best thing to do is remind yourself, "constructor does not mean constructed by".

`.constructor` is not a magic immutable property. It *is* non-enumerable, but its value is writable (can be changed), and moreover, you can add or overwrite (intentionally or accidentally) a property of the name `constructor` on any object in any `[[Prototype]]` chain, with any value you see fit.

28. ### Explain

```javascript
function Foo(name) {
  this.name = name;
}
Foo.prototype.myName = function () {
  return this.name;
};
function Bar(name, lable) {
  Foo.call(this, name);
  this.label = lable;
}
Bar.prototype = Object.create(Foo.prototype);
Bar.prototype.myLabel = function () {
  return this.lable;
};
var a = new Bar("a", "obj a");
a.myName();
a.myLabel();
```

**Note:** To understand why `this` points to `a` in the above code snippet, see Chapter 2.The important part is `Bar.prototype = Object.create( Foo.prototype )`. `Object.create(..)` *creates* a "new" object out of thin air, and links that new object's internal `[[Prototype]]` to the object you specify (`Foo.prototype` in this case). In other words, that line says: "make a *new* 'Bar dot prototype' object that's linked to 'Foo dot prototype'." When `function Bar() { .. }` is declared, `Bar`, like any other function, has a `.prototype` link to its default object. But *that* object is not linked to `Foo.prototype` like we want. So, we create a *new* object that *is* linked as we want, effectively throwing away the original incorrectly-linked object.

29. ### How to find out an object delegates to what object?
    `Object.getPrototypeOf( a );`
30. ### Prototypal inheritance soloutions? pros and cons?

- Bar.prototype = Foo.prototype;
  `Bar.prototype = Foo.prototype` doesn't create a new object for `Bar.prototype` to be linked to. It just makes `Bar.prototype` be another reference to `Foo.prototype`, which effectively links `Bar` directly to **the same object as** `Foo` links to: `Foo.prototype`. This means when you start assigning, like `Bar.prototype.myLabel = ...`, you're modifying **not a separate object** but *the* shared `Foo.prototype` object itself, which would affect any objects linked to `Foo.prototype`. This is almost certainly not what you want. If it *is* what you want, then you likely don't need `Bar` at all, and should just use only `Foo` and make your code simpler.
- Bar.prototype = new Foo();
  Bar.prototype = new Foo() does in fact create a new object which is duly linked to Foo.prototype as we'd want. But, it uses the Foo(..) "constructor call" to do it. If that function has any side-effects (such as logging, changing state, registering against other objects, adding data properties to this, etc.), those side-effects happen at the time of this linking (and likely against the wrong object!), rather than only when the eventual Bar() "descendants" are created, as would likely be expected.
- Object.create()
  So, we're left with using Object.create(..) to make a new object that's properly linked, but without having the side-effects of calling Foo(..). The slight downside is that we have to create a new object, throwing the old one away, instead of modifying the existing default object we're provided.
- Object.setPrototypeOf()
  It would be nice if there was a standard and reliable way to modify the linkage of an existing object. Prior to ES6, there's a non-standard and not fully-cross-browser way, via the .**proto** property, which is settable. ES6 adds a Object.setPrototypeOf(..) helper utility, which does the trick in a standard and predictable way.

31. ### Introspection (or reflection)?
    Inspecting an instance (just an object in JS) for its inheritance ancestry (delegation linkage in JS) is often called introspection (or reflection) in traditional class-oriented environments.
32. ### `instanceof` ?

    How do we then introspect `a` to find out its "ancestry" (delegation linkage)? The first approach embraces the "class" confusion:

    ```jsx
    a instanceof Foo; // true
    ```

    The `instanceof` operator takes a plain object as its left-hand operand and a **function** as its right-hand operand. The question `instanceof` answers is: **in the entire `[[Prototype]]` chain of `a`, does the object arbitrarily pointed to by `Foo.prototype` ever appear?**

33. ### isPrototypeOf()?

    The second, and much cleaner, approach to `[[Prototype]]` reflection is:
    `Foo.prototype.isPrototypeOf( a ); // true`
    Notice that in this case, we don't really care about (or even *need*) `Foo`, we just need an **object** (in our case, arbitrarily labeled `Foo.prototype`) to test against another **object**. The question `isPrototypeOf(..)` answers is: **in the entire `[[Prototype]]` chain of `a`, does `Foo.prototype` ever appear?**

34. ### getPrototypeOf()

    We can also directly retrieve the `[[Prototype]]` of an object. As of ES5, the standard way to do this is:
    `Object.getPrototypeOf( a );`
    And you'll notice that object reference is what we'd expect:
    `Object.getPrototypeOf( a ) === Foo.prototype; // true`

35. ### **proto**?

- What is it?
- It exists where?
- It's property or getter/setter?
  The strange `.__proto__`  property "magically" retrieves the internal `[[Prototype]]` of an object as a reference, which is quite helpful if you want to directly inspect (or even traverse: `.__proto__.__proto__...`) the chain. Just as we saw earlier with `.constructor`, `.__proto__` doesn't actually exist on the object you're inspecting. In fact, it exists on the built-in `Object.prototype`, along with the other common utilities (`.toString()`, `.isPrototypeOf(..)`, etc). Moreover, `.__proto__` looks like a property, but it's actually more appropriate to think of it as a getter/setter.

36. ### What's [[prototype]] mechanism?
    The [[Prototype]] mechanism is an internal link that exists on one object which references some other object.
37. ### When [[prototype]] linkage exercise?
    This linkage is (primarily) exercised when a property/method reference is made against the first object, and no such property/method exists. In that case, the [[Prototype]] linkage tells the engine to look for the property/method on the linked-to object. In turn, if that object cannot fulfill the look-up, its [[Prototype]] is followed, and so on. This series of links between objects forms what is called the "prototype chain".
