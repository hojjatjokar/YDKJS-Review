1. What's **[[prototype]]**?
2. The default [[GET]] operatopn, if it cannot find the requested property on the object directly what happens?
3. What will be output?

```javascript
var anotherObject = {
    a: 2,
};
var myObject = Object.create(anotherObject);
myObject.a; // ?
```

4. What's return result from the [[GET]] operation if no matching property ever found by the end of the chain?

5. Where exactly does the [[prototype]] chain ends?
6. Object.prototype includes what?
7. Setting properties on object if property doesn't exist on objects?
8. What's shadowing?
9. 3 scenarios for the **myObject.foo = "bar"** assignment when foo is not already on myObject directly, but is at a higher level of myObject's [[prototype]] chain?
10. What's whole scenarios for setting property a value?
11. If a property on Object is **writable: false** higher in [[prototype]] chain how can it be shadowed?
12. What's result? why? explain

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

13. Class function?
14.

```javascript
function Foo() {}
var a = new Foo();
Object.getPrototypeOf(a) === Foo.prototype; // ?
```

15. When an object created by calling **new Foo()** one of things that happen is what?
16. In JS you create multiple instances of a class? or you create multiple objects that are [[prototype]]-linked to a common object?

17. By default, no copying occurs, and thus these objects don't end up totally separate and disconnected from each other, but?

18. **new Foo()** is direct or indirect way to (a new object linked) to another object? what's direct way?
19. In JS we don't make copy from one object (class) to another (instance), what we make?
20. prototypal inheritance? is this term ok? why?
21. Differential inheritance?
22. What exactly leads us to think Foo is a "class"?
23. What will be the rusult?

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

24. Constructor function or constructor call?
25. This snippet shows two additional **"class orientation"** tricks in play:

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
