1. Sparse array?
2. Array-like? (2 example)
3. How to convert Array-like to array?
4. Array and string similarities?
5. Array and string differences?
6. Which array methods we can borrow to use with strings?
7. reversing string?
8. JS number type includes what numbers?
9. The implementation of JS numbers is base on what?
10. In js numbers which portions are optional ?
11. Numbers by default output in which form? large and small numbers outputed in which form?
12. toFixed?
13. toPrecision?
14. Can we use methods on literal numbers? How?
15. Explain? means?

```javascript
var a = 1e3;
```

16. Can numbers expressed in other bases? with example?
17. The most famous side effect of using library floating point numbers?
18. The most commonly accepted practice for this side effect?
19. Number.MAX_VALUE?
20. Number.MIN.VALUE?
21. Number.MAX_SAFE_INTEGER
22. Number.MIN_SAFE_INTEGER
23. 32-Bit Integers? why? what's range?
24. **null** is special keyword or identifier?
25. **undefined** is special keyword or identifier?
26. Is it posisble to assign a value to **undefined** ? in strict mode / no strict?
27. Can you create a local variable of the name **undefined**? in strict mode? non-strict mode?
28. **void** operator?
29. NaN?
30. **typeof** NaN?
31. isNaN?
32. Number.isNaN()
33.

```javascript
var a = 1 / 0;
var b = -1 / 0;
```

34. INFINITY(Number.POSITIVE_INFINITY)
35. -INFINITY(Number.NEGATIVE_INFINITY)
36.

```javascript
var a = Number.MAX_VALUE;
a + a; //?
a + Math.pow(2, 970); // ?
a + Math.pow(2, 969); // ?
```

37.

```javascript
var a = 0 / -3; // ?
var b = 0 * -3; // ?
```

38. Addition and subtraction can result in negative zero?
39.

```javascript
var a = 0 / -3;
a; // ?
a.toString(); // ?
a + ""; // ?
String(a); // ?
JSON.stringify(a); // ?
```

40.

```javascript
+"-0"; // ?
Number("-0"); // ?
JSON.Parse("-0"); // ?
```

41. How to distinguish -0 from 0 ?
42. Why do we need a negative zero?
43. Object.is() ?
44.

```javascript
var a = 2 / "foo";
var b = -3 * 0;
Object.is(a, NaN); // ?
Object.is(b, -0); // ?
Object.is(b, 0); // ?
```

45. When to use **Object.is()** and when not to use?
46.

```javascript
var a = 2;
var b = a;
b++;
a; // ?
b; // ?
```

47.

```javascript
var c = [1, 2, 3];
var d = c;
d.push(4);
c; // ?
d; // ?
```

48.

```javascript
var a = [1, 2, 3];
var b = a;
a; // ?
b; // ?
b = [4, 5, 6];
a; // ?
b; // ?
```

49.

```javascript
function foo(x) {
    x.push(4);
    x; // ?
    x = [4, 5, 6];
    x.push(7);
    x; // ?
}
var a = [1, 2, 3];
foo(a);
a; // ?
```
