1. ### Objects comes in what forms?
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

5. ### Which form is more common? literal or constructed?

It's extremely uncommon to use the "constructed form" for creating objects as just shown. You would pretty much always want to use the literal syntax form. The same will be true of most of the built-in objects.

6. ### Primary types?

Objects are the general building block upon which much of JS is built. They are one of the 6 primary types (called "language types" in the specification) in JS:

-   `string`
-   `number`
-   `boolean`
-   `null`
-   `undefined`
-   `object`

7. ### `null` is object types?

null is sometimes referred to as an object type, but this misconception stems from a bug in the language which causes typeof null to return the string "object" incorrectly (and confusingly). In fact, null is its own primitive type.

8. ### Object sub-types (built-in objects)?

By contrast, there *are* a few special object sub-types, which we can refer to as *complex primitives*.

`function` is a sub-type of object (technically, a "callable object"). Functions in JS are said to be "first class" in that they are basically just normal objects (with callable behavior semantics bolted on), and so they can be handled like any other plain object.

Arrays are also a form of objects, with extra behavior. The organization of contents in arrays is slightly more structured than for general objects.

9. ### What's first class functions?

Functions in JS are said to be "first class" in that they are basically just normal objects (with callable behavior semantics bolted on), and so they can be handled like any other plain object.

10. ### Functions are objects? What they have more than object?

function is a sub-type of object. Functions in JS are said to be "first class" in that they are basically just normal objects (with callable behavior semantics bolted on), and so they can be handled like any other plain object.

11. ### Arrays are objects? What they have more than object?

Arrays are also a form of objects, with extra behavior. The organization of contents in arrays is slightly more structured than for general objects.

12. ### Object sub-types are just what?

There are a few special object sub-types, which we can refer to as complex primitives.

13. ### What's relationship between these built-in functions and simple primitives?

    For some of them, their names seem to imply they are directly related to their simple primitives counter-parts, but in fact, their relationship is more complicated.

    Luckily, the language automatically coerces a `"string"` primitive to a `String` object when necessary, which means you almost never need to explicitly create the Object form. It is **strongly preferred** by the majority of the JS community to use the literal form for a value, where possible, rather than the constructed object form.

14. ### Have **null**, **undefined**, object wrapper?

`null` and `undefined` have no object wrapper form, only their primitive values.

15. ### Date have literal form or constructed form?

Date values can only be created with their constructed object form, as they have no literal form counter-part.

16. ### What's difference between two form of creating objects, arrays, functions and RegExp? Which is more prefered?

`Object`s, `Array`s, `Function`s, and `RegExp`s (regular expressions) are all objects regardless of whether the literal or constructed form is used. The constructed form does offer, in some cases, more options in creation than the literal form counterpart. Since objects are created either way, the simpler literal form is almost universally preferred. **Only use the constructed form if you need the extra options.**

17. ### Error objects created in which way most? How can we create?

Error objects are rarely created explicitly in code, but usually created automatically when exceptions are thrown. They can be created with the constructed form new Error(..), but it's often unnecessary.

18. ### Content of an object consist of what?

The contents of an object consist of values (any type) stored at specifically named locations, which we call properties.

19. ### How engin store object values? inside object? What is stored object container? property names act as what?

It's important to note that while we say "contents" which implies that these values are actually stored inside the object, that's merely an appearance. The engine stores values in implementation-dependent ways, and may very well not store them in some object container. What is stored in the container are these property names, which act as pointers (technically, references) to where the values are stored.

20. ### How to access value in object?

To access the value at the location a in myObject, we need to use either the . operator or the [ ] operator. The .a syntax is usually referred to as "property" access, whereas the ["a"] syntax is usually referred to as "key" access. In reality, they both access the same location, and will pull out the same value, 2, so the terms can be used interchangeably. We will use the most common term, "property access" from here on.

21. ### Which access method to value in object preferred?

the `.` operator

22. ### What's difference between two method of acessing?

The main difference between the two syntaxes is that the . operator requires an Identifier compatible property name after it, whereas the [".."] syntax can take basically any UTF-8/unicode compatible string as the name for the property. To reference a property of the name "Super-Fun!", for instance, you would have to use the ["Super-Fun!"] access syntax, as Super-Fun! is not a valid Identifier property name.

23. ### In object, property names are always in whih type? If you use another type what will happen?

In objects, property names are always strings. If you use any other value besides a string (primitive) as the property, it will first be converted to a string. This even includes numbers, which are commonly used as array indexes, so be careful not to confuse the use of numbers between objects and arrays.

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

```jsx
var prefix = "foo";

var myObject = {
    [prefix + "bar"]: "hello",
    [prefix + "baz"]: "world",
};

myObject["foobar"]; // hello
myObject["foobaz"]; // world
```

26. ### The most common usage of computed property names?

The most common usage of computed property names will probably be for ES6 Symbols. They're a new primitive data type which has an opaque unguessable value (technically a string value). You will be strongly discouraged from working with the actual value of a Symbol (which can theoretically be different between different JS engines), so the name of the Symbol, like Symbol.Something (just a made up name!), will be what you use:

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

Arrays also use the `[ ]` access form, but as mentioned above, they have slightly more structured organization for how and where values are stored.

Arrays assume *numeric indexing*, which means that values are stored in locations, usually called *indices*, at non-negative integers, such as `0` and `42`.

29. ### Which access form arrays use?

Arrays also use the `[ ]` access form

30. ### In Array, values strored in which location?
    Arrays assume numeric indexing, which means that values are stored in locations, usually called indices, at non-negative integers, such as 0 and 42.
31. ### What is array indexing ?

Arrays assume numeric indexing, which means that values are stored in locations, usually called indices, at non-negative integers, such as 0 and 42.

32. ### Explain

```javascript
var myArray = ["foo", 42, "bar"];
myArray.length; // ?
myArray[0]; // ?
myArray[2]; // ?
```

33. ### Can you add properties to array? why?
    Arrays are objects, so even though each index is a positive integer, you can also add properties onto the array
34. Adding named properties does change reported length of array?
35. Could you use an array as a plain key/value object? is it good idea? why?
36. If you try to add a property to an array but the property name looks like a number, what will happen?
37.

```javascript
var myArray = ["foo", 42, "bar"];
myArray.baz = "baz";
myArray.length; // ?
myArray.baz; // ?
```

38.

```javascript
var myArray = ["foo", 42, "bar"];
myArray["3"] = "baz";
myArray.length; // ?
myArray[3]; // ?
```

39. How to copy objects in JS?
40. How **Object.assign** works?
41. **Object.assign** is shallow or deep copy?
42. In general what way is there to copy obj?
43. What's deep copy object problems? (2)
44. Infinit circulation problem what decision we must take?
45. Is There a way for copy a function?
46. Explain JSON safe object copy?
47. In Object.assign what will happen to property descriptor?
48. What's property descriptor?
49. How to get property descriptor for specified property in object?
50. What property descriptor includes?
51. What is property descriptor characteristics default values ?
52. **Object.define** property? new property or modify eexisting? on existing it will fail in which situations?
53.

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

54. Generally when we use defineProperty?
55. Writable characteristict?
56.

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

57. If we try to change a non-writable property what will happen? in strict-mode what happen?
58. Configurable?
59. Configurable exception about writable?
60. **configurable: false** and **delete** operator?
61. If an object propertyy is the last remaining reference to some object/function, and you delete it, what will happen?
62. Enumerable?
63. Immutability?
64. Immutability in which ways?
65. All this approaches are shallow or deep immutability?
66. What's "shallow immutability" means?
67. What's object consonant? and what can or can't happen to obejct property?
68. If you want to prevent an object from having new properties ?
69. **Object.preventExtensions**?
70. Explain?

```javascript
var myObject = {
    a: 2,
};
Object.preventExtentions(myObject);
myObject.b = 3;
myObject.b; // normal mode ?
// use strict ?
```

71. Object.seal();
72. Object.freeze();
73. [[GET]]
74. Property access actually perform what?
75. If [[GET]] operation cannot come up with a value for the requested property what return?
76. consider:

```javascript
var myObject = {
    a: undefined,
};
myObject.a; // ?
myObject.b; // ?
```

    - What's difference between two references form a value perspective?
    - What's difference between two form [[GET]] operation?
    - Can you distinguish whether property exist and holds the explicit value of **undefined** or whether the property does not exist with inspecting only the result?
    - How can you distinguish these two scenario?

77. When invoking [[put]], how it behaves?
78. If the property is present on the object, the [[put]] what will do?
79. What's getters and setters are in property level or object level?
80. What's Getters and Setters?
81. When you define a prperty to have either a getter or setter or both, it's definition becomes what?
82. For accessor-descriptor, the value and writable characteristics will be what?
83. Consideer:

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

84. How to set getters and setters in literal syntax or with defineProperty?
85. Explain

```javascript
myObject = {
    get a() {
        return 2;
    },
};
myObject.a = 3;
myObject.a; // ?
```

86. Setter will override what?
87. Explain

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

88. How to check property existance?
89. What's difference between **in** operator and **hasOwnProperty**>
90. What's enumerable means?
91. Explain:

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

92. propertyIsEnumerable?
93. keys();
94. getOwnPropertyNames?
95. What's difference between **keys()** and getOwnPropertyNames?
96. Is there built-in way to get a list of all properties which equivalent to what the **in** operator test would consult? how you can get manually?
97. for ... in ?
98. Iterating over the values typically done with a standard for loop in arrays?
99. Difference between forEach, every(...), some()?
100.    **for...of**? How it works?
101.

```javascript
var myArray = [1, 2, 3];
for (var v of myArray) {
    console.log(v);
}
```

102.

```javascript
var myArray = [1, 2, 3];
var it = myArray[Symbol.iterator]();
it.next(); // { value: ?, done: ? }
it.next(); // { value: ?, doen: ? }
it.next(); // ?
it.next(); // ?
it.next(); // ?
```

103. **@@iterator**?
104. The return value from an iterator's **next()** call is what? What includes?
