1. ### Sparse array?
leaving or creating empty/missing slots.  It can lead to some confusing behavior with the "empty slots" you leave in between. While the slot appears to have the undefined value in it, it will not behave the same as if the slot is explicitly set (a[1] = undefined). 
2. ### Array-like? (2 example)
A numerically indexed collection of values.

For example, various DOM query operations return lists of DOM elements that are not true `array`s but are `array`-like enough for our conversion purposes. Another common example is when functions expose the `arguments` (`array`-like) object (as of ES6, deprecated) to access the arguments as a list.
3. ### How to convert Array-like to array?
One very common way to make such a conversion is to borrow the `slice(..)` utility against the value:

```jsx
function foo() {
	var arr = Array.prototype.slice.call( arguments );
	arr.push( "bam" );
	console.log( arr );
}

foo( "bar", "baz" ); // ["bar","baz","bam"]
```

If `slice()` is called without any other parameters, as it effectively is in the above snippet, the default values for its parameters have the effect of duplicating the `array` (or, in this case, `array`-like).

As of ES6, there's also a built-in utility called `Array.from(..)` that can do the same task:

`...
var arr = Array.from( arguments );
...`

**Note:** `Array.from(..)` has several powerful capabilities, and will be covered in detail in the *ES6 & Beyond* title of this series.
4. ### Array and string similarities?
JavaScript `string`s are really not the same as `array`s of characters. The similarity is mostly just skin-deep.

Strings do have a shallow resemblance to `array`s -- `array`-likes, as above -- for instance, both of them having a `length` property, an `indexOf(..)` method (`array` version only as of ES5), and a `concat(..)` method:
5. ### Array and string differences?
So, they're both basically just "arrays of characters", right? **Not exactly.**

- JavaScript `string`s are immutable, while `array`s are quite mutable.
- Moreover, the `a[1]` character position access form was not always widely valid JavaScript. Older versions of IE did not allow that syntax (but now they do). Instead, the *correct* approach has been `a.charAt(1)`.
- A further consequence of immutable `string`s is that none of the `string` methods that alter its contents can modify in-place, but rather must create and return new `string`s. By contrast, many of the methods that change `array` contents actually *do* modify in-place.
- Also, many of the `array` methods that could be helpful when dealing with `string`s are not actually available for them, but we can "borrow" non-mutation `array` methods against our `string`:
6. ### Which array methods we can borrow to use with strings?
Also, many of the `array` methods that could be helpful when dealing with `string`s are not actually available for them, but we can "borrow" non-mutation `array` methods against our `string`:

- join
- map
- ...
7. ### reversing string?
reversing a `string`. `array`s have a `reverse()` in-place mutator method, but `string`s do not:

```jsx
a.reverse;		// undefined

b.reverse();	// ["!","o","O","f"]
b;				// ["!","o","O","f"]
```

Unfortunately, this "borrowing" doesn't work with `array` mutators, because `string`s are immutable and thus can't be modified in place:

Another workaround (aka hack) is to convert the `string` into an `array`, perform the desired operation, then convert it back to a `string`.
```javascript
var c = a
	// split `a` into an array of characters
	.split( "" )
	// reverse the array of characters
	.reverse()
	// join the array of characters back to a string
	.join( "" );

c; // "oof"
```
8. ### JS number type includes what numbers?
JavaScript has just one numeric type: number. This type includes both "integer" values and fractional decimal numbers.
9. ### The implementation of JS numbers is base on what?
Like most modern languages, including practically all scripting languages, the implementation of JavaScript's numbers is based on the "IEEE 754" standard, often called "floating-point." JavaScript specifically uses the "double precision" format (aka "64-bit binary") of the standard.
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
