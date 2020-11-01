1. Objects comes in what forms?
2. Example of literal syntax for object?
3. Example of constructed form for object?
4. Difference between literal form and constructed form?
5. Which form is more common? literal or constructed?
6. Primary types?
7. **null** is object types?
8. Object sub-types (built-in objects)?
9. What's first class functions?
10. Functions are objects? What they have more than object?
11. Arrays are objects? What they have more than object?
12. Object sub-types are just what?
13. What's relationship between these built-in functions and simple primitives?
14. Have **null**, **undefined**, object wrapper?
15. Date have literal form or constructed form?
16. What's difference between two form of creating objects, arrays, functions and RegExp? Which is more prefered?
17. Error objects created in which way most? How can we create?
18. Content of an object consist of what?
19. How engin store object values? inside object? What is stored object container? property names act as what?
20. How to access value in object?
21. Which access method to value in object preferred?
22. What's difference between two method of acessing?
23. In object, property names are always in whih type? If you use another type what will happen?
24.

```javascript
var myObject = {};
myObject[true] = "foo";
myObject[3] = "bar";
myObject[myObject] = "baz";
myObject["true"]; // ?
myObject["3"]; // ?
myObject["[object object]"]; // ?
```

25. What's computed property names?
26. The most common usage of computed property names?
27.

```javascript
var prefix = "foo";
var myObject = {
    [prefix + "bar"]: "hello",
    [prefix + "baz"]: "world",
};
myObject["foobar"]; // ?
myObject["foobaz"]; // ?
```

28. What is array?
29. Whuch access form arrays use?
30. In Array, values strored in which location?
31. What is rray indexing ?
32.

```javascript
var myArray = ["foo", 42, "bar"];
myArray.length; // ?
myArray[0]; // ?
myArray[2]; // ?
```

33. Can you add properties to array? why?
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
