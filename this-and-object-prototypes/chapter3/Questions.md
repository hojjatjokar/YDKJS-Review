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
40. How Object.assign works?
