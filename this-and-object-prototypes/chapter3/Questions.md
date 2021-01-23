1. ### What forms objects come in ?
   Objects come in two forms: the declarative (literal) form, and the constructed form.
2. ### Example of literal syntax for object?

```javascript
var myObj = {
  key: value,
  // ...
};
```

3. ### Example of constructed form for object?

```javascript
var myObj = new Object();
myObj.key = value;
```

4. ### Difference between literal form and constructed form?

The constructed form and the literal form result in exactly the same sort of object. The only difference really is that you can add one or more key/value pairs to the literal declaration, whereas with constructed-form objects, you must add the properties one-by-one.

5. ### Which form of obejects is more common? literal or constructed?

It's extremely uncommon to use the "constructed form" for creating objects as just shown. You would pretty much always want to use the literal syntax form. The same will be true of most of the built-in objects.

6. ### Primary types?

Objects are the general building block upon which much of JS is built. They are one of the 6 primary types (called "language types" in the specification) in JS:

- `string`
- `number`
- `boolean`
- `null`
- `undefined`
- `object`

7. ### `null` is object types?

`null` is sometimes referred to as an object type, but this misconception stems from a bug in the language which causes `typeof null` to return the string "object" incorrectly (and confusingly). In fact, `null` is its own primitive type.

8. ### Object sub-types (built-in objects)?

By contrast, there are a few special object sub-types, which we can refer to as *complex primitives*.

`function` is a sub-type of object (technically, a "callable object"). Functions in JS are said to be "first class" in that they are basically just normal objects (with callable behavior semantics bolted on), and so they can be handled like any other plain object.

Arrays are also a form of objects, with extra behavior. The organization of contents in arrays is slightly more structured than for general objects.

9. ### What's first class functions?

Functions in JS are said to be "first class" in that they are basically just normal objects (with callable behavior semantics bolted on), and so they can be handled like any other plain object.

10. ### Functions are objects? What they have more than object?

`function` is a sub-type of `object`. Functions in JS are said to be "first class" in that they are basically just normal objects (with callable behavior semantics bolted on), and so they can be handled like any other plain object.

11. ### Arrays are objects? What they have more than object?

Arrays are also a form of objects, with extra behavior. The organization of contents in arrays is slightly more structured than for general objects.

12. ### What are Object sub-types?

There are a few special object sub-types, which we can refer to as complex primitives.

13. ### What's relationship between these built-in functions and simple primitives?

For some of them, their names seem to imply they are directly related to their simple primitives counter-parts, but in fact, their relationship is more complicated. Luckily, the language automatically coerces a `"string"` primitive to a `String` object when necessary, which means you almost never need to explicitly create the Object form. It is **strongly preferred** by the majority of the JS community to use the literal form for a value, where possible, rather than the constructed object form.

14. ### Have `null`, `undefined`, object wrapper?

`null` and `undefined` have no object wrapper form, only their primitive values.

15. ### Date have literal form or constructed form?

    Date values can only be created with their constructed object form, as they have no literal form counter-part.

16. ### What's difference between two form of creating objects, arrays, functions and RegExp? Which is more prefered?

    `Object`s, `Array`s, `Function`s, and `RegExp`s (regular expressions) are all objects regardless of whether the literal or constructed form is used. The constructed form does offer, in some cases, more options in creation than the literal form counterpart. Since objects are created either way, the simpler literal form is almost universally preferred. **Only use the constructed form if you need the extra options.**

17. ### which way Error objects created in most? How can we create?

Error objects are rarely created explicitly in code, but usually created automatically when exceptions are thrown. They can be created with the constructed form `new Error(..)`, but it's often unnecessary.

18. ### Content of an object consist of what?

The contents of an `object` consist of values (any type) stored at specifically named locations, which we call properties.

19. ### How engin store object values? inside object? What is stored object container? property names act as what?

It's important to note that while we say "contents" which implies that these values are actually stored inside the object, that's merely an appearance. The engine stores values in implementation-dependent ways, and may very well not store them in some object container. What is stored in the container are these property names, which act as pointers (technically, references) to where the values are stored.

20. ### How to access value in object?

To access the value at the location a in `myObject`, we need to use either the `.` operator or the `[ ]` operator. The `.a` syntax is usually referred to as "property" access, whereas the `["a"]` syntax is usually referred to as "key" access. In reality, they both access the same location, so the terms can be used interchangeably.

21. ### Which access method to value in object preferred?

the `.` operator

22. ### What's difference between two method of accessing?

The main difference between the two syntaxes is that the `.` operator requires an Identifier compatible property name after it, whereas the `[".."]` syntax can take basically any `UTF-8/unicode` compatible string as the name for the property. To reference a property of the name "Super-Fun!", for instance, you would have to use the `["Super-Fun!"]` access syntax, as Super-Fun! is not a valid Identifier property name.

23. ### In object, property names are always in whih type? If you use another type what will happen?

In objects, property names are always strings. If you use any other value besides a string (primitive) as the property, it will first be converted to a `string`. This even includes numbers, which are commonly used as array indexes, so be careful not to confuse the use of numbers between objects and arrays.

24. ### Explain

```javascript
var myObject = {};
myObject[true] = "foo";
myObject[3] = "bar";
myObject[myObject] = "baz";
myObject["true"]; // ?
myObject["3"]; // ?
myObject["[object object]"]; // ?
```

25. ### What's computed property names?

ES6 adds *computed property names*, where you can specify an expression, surrounded by a `[ ]` pair, in the key-name position of an object-literal declaration:

```javascript
var prefix = "foo";

var myObject = {
  [prefix + "bar"]: "hello",
  [prefix + "baz"]: "world",
};

myObject["foobar"]; // hello
myObject["foobaz"]; // world
```

26. ### The most common usage of computed property names?

The most common usage of computed property names will probably be for ES6 `Symbol`s. They're a new primitive data type which has an opaque unguessable value (technically a string value). You will be strongly discouraged from working with the actual value of a `Symbol` (which can theoretically be different between different JS engines), so the name of the `Symbol`, like `Symbol.Something` (just a made up name!), will be what you use:

27. ### Explain

```javascript
var prefix = "foo";
var myObject = {
  [prefix + "bar"]: "hello",
  [prefix + "baz"]: "world",
};
myObject["foobar"]; // ?
myObject["foobaz"]; // ?
```

28. ### What is array?

Arrays also use the `[ ]` access form, but as mentioned above, they have slightly more structured organization for how and where values are stored. Arrays assume *numeric indexing*, which means that values are stored in locations, usually called *indices*, at non-negative integers, such as `0` and `42`.

29. ### Which access form arrays use?

Arrays also use the `[ ]` access form

30. ### Which location values stored in array?
    Arrays assume numeric indexing, which means that values are stored in locations, usually called indices, at non-negative integers, such as 0 and 42.
31. ### What is array indexing ?

Arrays assume numeric indexing, which means that values are stored in locations, usually called indices, at non-negative integers, such as ‍‍0 and 42.

32. ### Explain

```javascript
var myArray = ["foo", 42, "bar"];
myArray.length; // ?
myArray[0]; // ?
myArray[2]; // ?
```

33. ### Can you add properties to array? why?
    Arrays are objects, so even though each index is a positive integer, you can also add properties onto the array
34. ### Adding named properties does change reported length of array?

Notice that adding named properties (regardless of `.` or `[ ]` operator syntax) does not change the reported length of the array.

35. ### Could you use an array as a plain key/value object? is it good idea? why?

You could use an array as a plain key/value object, and never add any numeric indices, but this is a bad idea because arrays have behavior and optimizations specific to their intended use, and likewise with plain objects. Use objects to store key/value pairs, and arrays to store values at numeric indices.

36. ### If you try to add a property to an array but the property name looks like a number, what will happen?

If you try to add a property to an array, but the property name looks like a number, it will end up instead as a numeric index (thus modifying the array contents)

37. ### Explain

```javascript
var myArray = ["foo", 42, "bar"];
myArray.baz = "baz";
myArray.length; // ?
myArray.baz; // ?
```

Answer:

```javascript
var myArray = ["foo", 42, "bar"];

myArray.baz = "baz";

myArray.length; // 3

myArray.baz; // "baz"
```

38. ### Explain

```javascript
var myArray = ["foo", 42, "bar"];
myArray["3"] = "baz";
myArray.length; // ?
myArray[3]; // ?
```

Answer:

```javascript
var myArray = ["foo", 42, "bar"];

myArray["3"] = "baz";

myArray.length; // 4

myArray[3]; // "baz"
```

39. ### How to copy objects in JS?

Using `Object.assign`

40. ### How `Object.assign` works?

`Object.assign(..)` takes a target object as its first parameter, and one or more source objects as its subsequent parameters. It iterates over all the enumerable, owned keys (immediately present) on the source object(s) and copies them (via = assignment only) to target.

41. ### `Object.assign` is shallow or deep copy?

shallow

42. ### In general what way is there to copy obj?

We should answer if it should be a *shallow* or *deep* copy. A *shallow copy* would end up with `a` on the new object as a copy of the value `2`, but `b`, `c`, and `d` properties as just references to the same places as the references in the original object.

A *deep copy* would duplicate not only `myObject`, but `anotherObject` and `anotherArray`. But then we have issues that `anotherArray` has references to `anotherObject` and `myObject` in it, so *those* should also be duplicated rather than reference-preserved. Now we have an infinite circular duplication problem because of the circular reference.

43. ### What's deep copy object problems? (2)

Should we detect a circular reference and just break the circular traversal (leaving the deep element not fully duplicated)? Should we error out completely? Something in between?

Moreover, it's not really clear what "duplicating" a function would mean? There are some hacks like pulling out the `toString()` serialization of a `function`'s source code (which varies across implementations and is not even reliable in all engines depending on the type of `function` being inspected).

44. ### Infinit circulation problem what decision we must take?

Should we detect a circular reference and just break the circular traversal (leaving the deep element not fully duplicated)? Should we error out completely? Something in between?

45. ### Is There a way for copy a function?

Moreover, it's not really clear what "duplicating" a function would mean? There are some hacks like pulling out the `toString()` serialization of a function's source code (which varies across implementations and is not even reliable in all engines depending on the type of function being inspected).

46. ### Explain JSON safe object copy?

One subset solution is that objects which are JSON-safe (that is, can be serialized to a JSON string and then re-parsed to an object with the same structure and values) can easily be *duplicated* with:

`var newObj = JSON.parse( JSON.stringify( someObj ) );`

Of course, that requires you to ensure your object is JSON safe. For some situations, that's trivial. For others, it's insufficient.

47. ### In `Object.assign` what will happen to property descriptor?

The duplication that occurs for `Object.assign(..)` however is purely = style assignment, so any special characteristics of a property (like writable) on a source object are not preserved on the target object.

48. ### What's property descriptor?

property characteristics

49. ## How to get property descriptor for specified property in object?

    ```javascript
    Object.getOwnPropertyDescriptor(myObject, "a");
    // {
    //    value: 2,
    //    writable: true,
    //    enumerable: true,
    //    configurable: true
    // }
    ```

50. ### What property descriptor includes?

    It includes 3 other characteristics: writable, enumerable, and configurable.

51. ### What is property descriptor characteristics default values ?

```javascript
{
	...
	writable: true,
	configurable: true,
	enumerable: true
}
```

52. ### What is `Object.defineProperty`? It adds new property or modifies an existing one? on existing, it will fail in which situations?

We can use `Object.defineProperty(..)` to add a new property or modify an existing one (if it's `configurable`!), with the desired characteristics.

Using `defineProperty(..)`, we added the plain, normal `a` property to `myObject` in a manually explicit way.

53. ### Explain

```javascript
var myObject = {};
Object.defineProperty(myObject, "a", {
  value: 2,
  writable: true,
  configurable: true,
  enumerable: true,
});
myObject.a; // ?
```

54. ### Generally when we use defineProperty?

You generally wouldn't use this manual approach unless you wanted to modify one of the descriptor characteristics from its normal behavior.

55. ### What's `writable` characteristict?
    The ability for you to change the value of a property is controlled by `writable`.
56. ### Explain

```javascript
var myObject = {};
Object.defineProperty(myObject, "a", {
  value: 2,
  writable: false,
  configurable: true,
  enumerable: true,
});
myObject.a = 3;
myObject.a; // ?
```

57. ### If we try to change a non-writable property what will happen? in strict-mode what happen?
    Modification of the value silently fails. If we try in strict mode, we get an error
58. ### Whta's configurable?

    As long as a property is currently configurable, we can modify its descriptor definition, using the same `defineProperty(..)` utility.
    `defineProperty(..)` call results in a TypeError, regardless of `strict mode`, if you attempt to change the descriptor definition of a non-configurable property.
    Be careful: as you can see, changing `configurable` to `false` is a **one-way action, and cannot be undone!**

59. ### Configurable exception about writable?
    There's a nuanced exception to be aware of: even if the property is already `configurable:false`, writable can always be changed from true to false without error, but not back to true if already false.
60. ### `configurable: false` and `delete` operator?

Another thing `configurable:false` prevents is the ability to use the delete operator to remove an existing property.

61. ### If an object property is the last remaining reference to some object/function, and you delete it, what will happen?

If an object property is the last remaining reference to some object/function, and you delete it, that removes the reference and now that unreferenced object/function can be garbage collected. But, it is not proper to think of delete as a tool to free up allocated memory as it does in other languages (like C/C++). delete is just an object property removal operation -- nothing more.

62. ### What's enumerable?

The name probably makes it obvious, but this characteristic controls if a property will show up in certain object-property enumerations, such as the `for..in` loop. Set to `false` to keep it from showing up in such enumerations, even though it's still completely accessible. Set to `true` to keep it present.

All normal user-defined properties are defaulted to `enumerable`, as this is most commonly what you want. But if you have a special property you want to hide from enumeration, set it to `enumerable:false`.

63. ### What's Immutability?

It is sometimes desired to make properties or objects that cannot be changed (either by accident or intentionally). ES5 adds support for handling that in a variety of different nuanced ways.

64. ### How many ways are available for immutability?

- Object Constant
- `Object.preventExtensions`
- `Object.seal`
- `Object.freeze`

65. ### All this approaches are shallow or deep immutability?

It's important to note that all of these approaches create shallow immutability.

66. ### What's "shallow immutability" means?

It's important to note that all of these approaches create shallow immutability. That is, they affect only the object and its direct property characteristics. If an object has a reference to another object (array, object, function, etc), the contents of that object are not affected, and remain mutable.

67. ### What's object consonant? and what can or can't happen to obejct property?

By combining `writable:false` and `configurable:false`, you can essentially create a constant (cannot be changed, redefined or deleted) as an object property

68. ### If you want to prevent an object from having new properties ?

`Object.preventExtensions`

69. ### `Object.preventExtensions`?

If you want to prevent an object from having new properties added to it, but otherwise leave the rest of the object's properties alone, call `Object.preventExtensions(..)`

70. ### Explain?

```javascript
var myObject = {
  a: 2,
};
Object.preventExtentions(myObject);
myObject.b = 3;
myObject.b; // normal mode ?
// use strict ?
```

71. ### Whats `Object.seal()`?

`Object.seal(..)` creates a "sealed" object, which means it takes an existing object and essentially calls `Object.preventExtensions(..)` on it, but also marks all its existing properties as `configurable:false`.

So, not only can you not add any more properties, but you also cannot reconfigure or delete any existing properties (though you *can* still modify their values).

72. ### What's `Object.freeze()`?

`Object.freeze(..)` creates a frozen object, which means it takes an existing object and essentially calls `Object.seal(..)` on it, but it also marks all "data accessor" properties as `writable:false`, so that their values cannot be changed.

73. ### What is [[GET]]?

According to the spec, `myObject.a` actually performs a `[[Get]]` operation (kinda like a function call: `[[Get]]()`) on the `myObject`. The default built-in `[[Get]]` operation for an object *first* inspects the object for a property of the requested name, and if it finds it, it will return the value accordingly.

However, the `[[Get]]` algorithm defines other important behavior if it does *not* find a property of the requested name. Traversal of the `[[Prototype]]` chain, if any.

74. ### Property access actually perform what?

Performs a `[[Get]]` operation (kinda like a function call: `[[Get]]())`

75. ### If `[[GET]]` operation cannot come up with a value for the requested property what return?

If it cannot through any means come up with a value for the requested property, it instead returns the value `undefined`.

76. ### Consider:

```javascript
var myObject = {
  a: undefined,
};
myObject.a; // ?
myObject.b; // ?
```

    - What's difference between two references form a value perspective?
    - What's difference between two form `[[GET]]` operation?
    - Can you distinguish whether property exist and holds the explicit value of **undefined** or whether the property does not exist with inspecting only the result?
    - How can you distinguish these two scenario?

    a. None
    b.  The `[[Get]]` operation underneath, though subtle at a glance, potentially performed a bit more "work" for the reference `myObject.b` than for the reference `myObject.a`.
    c. Inspecting only the value results, you cannot distinguish whether a property exists and holds the explicit value `undefined`, or whether the property does *not* exist and `undefined` was the default return value after `[[Get]]` failed to return something explicitly.

77. ### When invoking [[Put]], how it behaves?

    When invoking `[[Put]]`, how it behaves differs based on a number of factors, including whether the property is already present on the object or not.

    If the property is present, the `[[Put]]` algorithm will roughly check:

    a. Is the property an accessor descriptor? **If so, call the setter, if any.**
    b. Is the property a data descriptor with `writable` of `false`? **If so, silently fail in `non-strict mode`, or throw `TypeError` in `strict mode`.**
    c. Otherwise, set the value to the existing property as normal.

    If the property is not yet present on the object in question, the `[[Put]]` operation is even more nuanced and complex. We will revisit this scenario in Chapter 5 when we discuss `[[Prototype]]` to give it more clarity.

78. ### If the property is present on the object, the [[put]] what will do?

    If the property is present, the `[[Put]]` algorithm will roughly check:

    1. Is the property an accessor descriptor? **If so, call the setter, if any.**
    2. Is the property a data descriptor with `writable` of `false`? **If so, silently fail in `non-strict mode`, or throw `TypeError` in `strict mode`.**
    3. Otherwise, set the value to the existing property as normal.

79. ### What's getters and setters are in property level or object level?

If the property is not yet present on the object in question, the `[[Put]]` operation is even more nuanced and complex. We will revisit this scenario in Chapter 5 when we discuss `[[Prototype]]` to give it more clarity.

80. ### What's Getters and Setters?

The default `[[Put]]` and `[[Get]]` operations for objects completely control how values are set to existing or new properties, or retrieved from existing properties, respectively.

81. ### When you define a prperty to have either a getter or setter or both, it's definition becomes what?

When you define a property to have either a getter or a setter or both, its definition becomes an "accessor descriptor" (as opposed to a "data descriptor"). For accessor-descriptors, the value and writable characteristics of the descriptor are moot and ignored, and instead JS considers the set and get characteristics of the property (as well as configurable and enumerable).

82. ### For accessor-descriptor, the value and writable characteristics will be what?

For accessor-descriptors, the value and writable characteristics of the descriptor are moot and ignored, and instead JS considers the set and get characteristics of the property (as well as configurable and enumerable).

83. ### Consider:

```javascript
var myObject = {
  get a() {
    return 2;
  },
};
Object.defineProperty(myObject, "b", {
  get: function () {
    return this.a * 2;
  },
  enumerable: true,
});
myObject.a; // ?
myObject.b; // ?
```

Either through object-literal syntax with `get a() { .. }` or through explicit definition with `defineProperty(..)`, in both cases we created a property on the object that actually doesn't hold a value, but whose access automatically results in a hidden function call to the getter function, with whatever value it returns being the result of the property access.

84. ### How to set getters and setters in literal syntax or with defineProperty?

```javascript
var myObject = {
  // define a getter for `a`
  get a() {
    return 2;
  },
};

Object.defineProperty(
  myObject, // target
  "b", // property name
  {
    // descriptor
    // define a getter for `b`
    get: function () {
      return this.a * 2;
    },

    // make sure `b` shows up as an object property
    enumerable: true,
  }
);
```

85. ### Explain

```javascript
myObject = {
  get a() {
    return 2;
  },
};
myObject.a = 3;
myObject.a; // ?
```

86. ### Setter will override what?
    Override the default `[[Put]]` operation (aka, assignment)
87. ### Explain

```javascript
    var myObject = {
        get a() {
            return this._a;
        }
        set a(val){
            this._a = val * 2;
        }
    };
    myObject.a = 2;
    myObject.a; // ?
```

Note: In this example, we actually store the specified value 2 of the assignment ([[Put]] operation) into another variable *a*. The *a* name is purely by convention for this example and implies nothing special about its behavior -- it's a normal property like any other.

88. ### How to check property existance?

The `in` operator will

`hasOwnProperty(..)`

89. ### What's difference between **in** operator and **hasOwnProperty**?

    The in operator will check to see if the property is in the object, or if it exists at any higher level of the [[Prototype]] chain object traversal. By contrast, hasOwnProperty(..) checks to see if only myObject has the property or not, and will not consult the [[Prototype]] chain.

90. ### What's enumerable means?
91. ### Explain:

```javascript
myObject = {};
Object.defineProperty(myObject, "a", {
  enummerable: true,
  value: 2,
});
Object.defineProperty(myObject, "b", {
  enummerable: false,
  value: 3,
});
myObject.b; // ?
"b" in myObject; // ?
myObject.hasOwnProperty("b"); // ?
for (let k in myObject) {
  console.log(k, myObject[k]); // ?
}
```

`propertyIsEnumerable(..)` tests whether the given property name exists *directly* on the object and is also `enumerable:true`.

`Object.keys(..)` returns an array of all enumerable properties, whereas `Object.getOwnPropertyNames(..)` returns an array of *all* properties, enumerable or not.

Whereas `in` vs. `hasOwnProperty(..)` differ in whether they consult the `[[Prototype]]` chain or not, `Object.keys(..)` and `Object.getOwnPropertyNames(..)` both inspect *only* the direct object specified.

There's (currently) no built-in way to get a list of **all properties** which is equivalent to what the `in` operator test would consult (traversing all properties on the entire `[[Prototype]]` chain, as explained in Chapter 5). You could approximate such a utility by recursively traversing the `[[Prototype]]` chain of an object, and for each level, capturing the list from `Object.keys(..)` -- only enumerable properties.

92. ### What does `propertyIsEnumerable` do?
    `propertyIsEnumerable(..)` tests whether the given property name exists directly on the object and is also enumerable:true.
93. ### What does `keys()` do?
    `Object.keys(..)` returns an array of all enumerable properties, whereas Object.getOwnPropertyNames(..) returns an array of all properties, enumerable or not.
94. ### What does getOwnPropertyNames do?
    `Object.getOwnPropertyNames(..)` returns an array of all properties, enumerable or not.
95. ### What's difference between **keys()** and getOwnPropertyNames?

    Whereas `in` vs. `hasOwnProperty(..)` differ in whether they consult the `[[Prototype]]` chain or not, `Object.keys(..)` and `Object.getOwnPropertyNames(..)` both inspect only the direct object specified.

96. ### Is there built-in way to get a list of all properties which equivalent to what the **in** operator test would consult? how you can get manually?
    There's (currently) no built-in way to get a list of all properties which is equivalent to what the in operator test would consult. You could approximate such a utility by recursively traversing the [[Prototype]] chain of an object, and for each level, capturing the list from Object.keys(..) -- only enumerable properties.
97. ### What is `for..in` ?
    The `for..in` loop iterates over the list of enumerable properties on an object (including its [[Prototype]] chain). But what if you instead want to iterate over the values?
98. ### Iterating over the values typically done with a standard for loop in arrays?
    With numerically-indexed arrays, iterating over the values is typically done with a standard for loop
99. ### Difference between `forEach`, `every(...)`, `some()`?

`forEach(..)` will iterate over all values in the array, and ignores any callback return values. `every(..)` keeps going until the end *or* the callback returns a `false` (or "falsy") value, whereas `some(..)` keeps going until the end *or* the callback returns a `true` (or "truthy") value.

These special return values inside `every(..)` and `some(..)` act somewhat like a `break` statement inside a normal `for` loop, in that they stop the iteration early before it reaches the end.

100. ### `for...of`? How it works?
     Iterate over the values directly instead of the array indices (or object properties).

The `for..of` loop asks for an iterator object (from a default internal function known as `@@iterator` in spec-speak) of the *thing* to be iterated, and the loop then iterates over the successive return values from calling that iterator object's `next()` method, once for each loop iteration.

101. ### Explain?

```javascript
var myArray = [1, 2, 3];
for (var v of myArray) {
  console.log(v);
}
```

The for..of loop asks for an iterator object (from a default internal function known as @@iterator in spec-speak) of the thing to be iterated, and the loop then iterates over the successive return values from calling that iterator object's next() method, once for each loop iteration.

102. ### Explain?

```javascript
var myArray = [1, 2, 3];
var it = myArray[Symbol.iterator]();
it.next(); // { value: ?, done: ? }
it.next(); // { value: ?, doen: ? }
it.next(); // ?
it.next(); // ?
it.next(); // ?
```

Arrays have a built-in `@@iterator`, so `for..of` works easily on them, as shown. But let's manually iterate the array, using the built-in `@@iterator`, to see how it works:

**Note:** We get at the `@@iterator` *internal property* of an object using an ES6 `Symbol`: `Symbol.iterator`.

As the above snippet reveals, the return value from an iterator's `next()` call is an object of the form `{ value: .. , done: .. }`, where `value` is the current iteration value, and `done` is a `boolean` that indicates if there's more to iterate.

Notice the value `3` was returned with a `done:false`, which seems strange at first glance. You have to call the `next()` a fourth time (which the `for..of` loop in the previous snippet automatically does) to get `done:true` and know you're truly done iterating. The reason for this quirk is beyond the scope of what we'll discuss here, but it comes from the semantics of ES6 generator functions.

103. ### `@@iterator`?
     `@@iterator` is not the iterator object itself, but a function that returns the iterator object -- a subtle but important detail!
104. ### The return value from an iterator's `next()` call is what? What includes?
     The return value from an iterator's next() call is an object of the form `{ value: .. , done: .. }`, where value is the current iteration value, and done is a boolean that indicates if there's more to iterate.
