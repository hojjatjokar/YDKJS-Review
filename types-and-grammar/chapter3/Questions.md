1. List of most commonly used natives?
2. Are these natives actually built-in functions?
3.

```javascript
var a = new String("abc");
typeof a; // ?
a instanceof String; // ?
Object.prototype.toString.call(a); // ?
```

4. What's result of the constructor from of value creation?
5. How can access internal [[class]]?
6. What's Internal [[class]] for type of object?
7. What's internal [[class]] for **null** and **undefined**?
8. What's internal [[calss]] for promitive values?
9. Object.prototype.toString([1,2,3]); // ?
10. Object.prototype.toString(/regex.literal/); // ?
11. Object.prototype.toString({}); // ?
12. Object.prototype.toString(fn(){}); // ?
13. Object.prototype.toString("abc"); // ?
14. Object.prototype.toString(42); // ?
15. Object.prototype.toString(true); // ?
16. Object.prototype.toString(null); // ?
17. Object.prototype.toString(undefined); // ?
18. Boxing wrappers?
19. Is it good to use object form of primitive value instead of js engine implicitly create it for us?
20. How you can box a primitive value?
21. How to unbox object box wrappers? implicitly and explicitly?
22.

```javascript
var a = new Boolean(false);
if (!a) {
    console.log("oops");
}
```

23.

```javascript
  var a = 'abc';
  var b = new String(a);
  var c = Object(a);
  typeof a; // ?
  typeof b; // ?
  typeof c; // ?

  b.instanceof String; // ?
  c.instanctof String; // ?
  Object.prototype.toString.call(b); // ?
```

24.

```javascript
var a = new String("abc");
a.valueOf(); // ?
var b = a + ""; // ?
```

25. For natives(Array, Object, Function, Regex, Date, Error, Symbol) answer this questions?

-   Has constructor?
-   Has literal?
-   Which form is preffered?
-   Is there difference between two form?

26. How to create 'presize array'?
27. Array constructor does require new keyword in front of it? What happen if you omit it?
28.

```javascript
  var a = new Array(3);
  var b = [undefined, undefined, undefined];
  var c = [];
  c.length = 3;
  a; // ?
  b; // ?
  c; // ?
  a.join('_ ');
  b.join('_ ');
  a.map(fn(v, i){ return i;}); // ?
  b.map(fn(v, i){ return i;}); // ?
```

29. Where Function constructor is helpful?
30. Where RegExp constructor is helpful?
31. What's Date(...) constructor parameters? are they required or optional? if ommited whats happens?
32. Whats's most common reason to construct a date object(2 ways)
33. What's Unix timestamp?
34. The main reason to create an error object?
35. What's stack context and how to get that?
36. Error object unstance have what properties?
37. All of Error natives? (7)
38. What's Symbol? how you can define?
39. What's native properties? What they contain?
40.

-   String #indexOf()
-   String #chatAt()
-   String #substr()
-   String #substring()
-   String #slice()
-   String #toUppercase()
-   String #toLowerCase()
-   String #trim()

41. String methods does modify the string in place? How modifications apply?
42. How any string
43. Number #toFixed?
44. Array #concat?
45.

-   Function #call
-   Function #apply
-   Function #bind

46. Some of the native prototype aren't just plain objects, which of natives? what are they?

47. Is it better to use prototypes as default or try to declare empty value? why?
