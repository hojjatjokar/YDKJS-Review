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
10. ### In js numbers which portions are optional ?
The leading portion of a decimal value, if `0`, is optional:

```jsx
var a = 0.42;
var b = .42;
```

Similarly, the trailing portion (the fractional) of a decimal value after the `.`, if `0`, is optional:

```jsx
var a = 42.0;
var b = 42.;
```
11. ### Numbers by default output in which form? large and small numbers outputed in which form?
- 11. Which form number's output will be? large and small numbers outputed in which form?

    By default, most `number`s will be outputted as base-10 decimals, with trailing fractional `0`s removed. So:

    ```jsx
    var a = 42.300;
    var b = 42.0;

    a; // 42.3
    b; // 42
    ```

    Very large or very small `number`s will by default be outputted in exponent form, the same as the output of the `toExponential()` method, like:

    ```jsx
    var a = 5E10;
    a;					// 50000000000
    a.toExponential();	// "5e+10"

    var b = a * a;
    b;					// 2.5e+21

    var c = 1 / a;
    c;					// 2e-11
    ```
12. ### toFixed?
The `toFixed(..)` method allows you to specify how many fractional decimal places you'd like the value to be represented with:

```jsx
var a = 42.59;

a.toFixed( 0 ); // "43"
a.toFixed( 1 ); // "42.6"
a.toFixed( 2 ); // "42.59"
a.toFixed( 3 ); // "42.590"
a.toFixed( 4 ); // "42.5900"
```

Notice that the output is actually a `string` representation of the `number`, and that the value is `0`-padded on the right-hand side if you ask for more decimals than the value holds.
13. ### toPrecision?
`toPrecision(..)` is similar, but specifies how many *significant digits* should be used to represent the value:

```jsx
var a = 42.59;

a.toPrecision( 1 ); // "4e+1"
a.toPrecision( 2 ); // "43"
a.toPrecision( 3 ); // "42.6"
a.toPrecision( 4 ); // "42.59"
a.toPrecision( 5 ); // "42.590"
a.toPrecision( 6 ); // "42.5900"
```
14. ### Can we use methods on literal numbers? How?
You don't have to use a variable with the value in it to access these methods; you can access these methods directly on `number` literals. But you have to be careful with the `.` operator. Since `.` is a valid numeric character, it will first be interpreted as part of the `number` literal, if possible, instead of being interpreted as a property accessor.

```jsx
// invalid syntax:
42.toFixed( 3 );	// SyntaxError

// these are all valid:
(42).toFixed( 3 );	// "42.000"
0.42.toFixed( 3 );	// "0.420"
42..toFixed( 3 );	// "42.000"
```

`42.toFixed(3)` is invalid syntax, because the `.` is swallowed up as part of the `42.` literal (which is valid -- see above!), and so then there's no `.` property operator present to make the `.toFixed` access.

`42..toFixed(3)` works because the first `.` is part of the `number` and the second `.` is the property operator. But it probably looks strange, and indeed it's very rare to see something like that in actual JavaScript code. In fact, it's pretty uncommon to access methods directly on any of the primitive values. Uncommon doesn't mean *bad* or *wrong*.

This is also technically valid (notice the space):

`42 .toFixed(3); // "42.000"`

However, with the `number` literal specifically, **this is particularly confusing coding style** and will serve no other purpose but to confuse other developers (and your future self). Avoid it.
15. Explain? means?

```javascript
var a = 1e3;
```

`number`s can also be specified in exponent form, which is common when representing larger `number`s, such as:

```jsx
var onethousand = 1E3;						// means 1 * 10^3
var onemilliononehundredthousand = 1.1E6;	// means 1.1 * 10^6
```
16. ### Can numbers expressed in other bases? with example?
`number` literals can also be expressed in other bases, like binary, octal, and hexadecimal.

These formats work in current versions of JavaScript:

```jsx
0xf3; // hexadecimal for: 243
0Xf3; // ditto

0363; // octal for: 243
```

**Note:** Starting with ES6 + `strict` mode, the `0363` form of octal literals is no longer allowed (see below for the new form). The `0363` form is still allowed in non-`strict` mode, but you should stop using it anyway, to be future-friendly (and because you should be using `strict` mode by now!).

As of ES6, the following new forms are also valid:

```jsx
0o363;		// octal for: 243
0O363;		// ditto

0b11110011;	// binary for: 243
0B11110011; // ditto
```

Please do your fellow developers a favor: never use the `0O363` form. `0` next to capital `O` is just asking for confusion. Always use the lowercase predicates `0x`, `0b`, and `0o`.
17. ### The most famous side effect of using library floating point numbers?
The most (in)famous side effect of using binary floating-point numbers (which, remember, is true of **all** languages that use IEEE 754 -- not *just* JavaScript as many assume/pretend) is:

```jsx
0.1 + 0.2 === 0.3; // false
```

Mathematically, we know that statement should be `true`. Why is it `false`?

Simply put, the representations for `0.1` and `0.2` in binary floating-point are not exact, so when they are added, the result is not exactly `0.3`. It's **really** close: `0.30000000000000004`, but if your comparison fails, "close" is irrelevant.
18. ### The most commonly accepted practice for this side effect?
The most commonly accepted practice is to use a tiny "rounding error" value as the *tolerance* for comparison. This tiny value is often called "machine epsilon," which is commonly `2^-52` (`2.220446049250313e-16`) for the kind of `number`s in JavaScript.

As of ES6, `Number.EPSILON` is predefined with this tolerance value, so you'd want to use it, but you can safely polyfill the definition for pre-ES6:

```jsx
if (!Number.EPSILON) {
	Number.EPSILON = Math.pow(2,-52);
}
```

We can use this `Number.EPSILON` to compare two `number`s for "equality" (within the rounding error tolerance):

```jsx
function numbersCloseEnoughToEqual(n1,n2) {
	return Math.abs( n1 - n2 ) < Number.EPSILON;
}

var a = 0.1 + 0.2;
var b = 0.3;

numbersCloseEnoughToEqual( a, b );					// true
numbersCloseEnoughToEqual( 0.0000001, 0.0000002 );	// false
```
19. ### Number.MAX_VALUE?
The maximum floating-point value that can be represented is roughly 1.798e+308 (which is really, really, really huge!), predefined for you as Number.MAX_VALUE.
20. ### Number.MIN.VALUE?
On the small end, Number.MIN_VALUE is roughly 5e-324, which isn't negative but is really close to zero!
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
