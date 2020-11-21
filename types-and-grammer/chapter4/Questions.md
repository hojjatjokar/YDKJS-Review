1. Type casting? coercion?
2. Javascript coercions always result in what?
3. Type casting occurs in which languages? as in which time?
4. Type coercion occurs in which languages? an in which time?
5. In JS refers this conversions as?
6. Difference between implicit and explicit coerscion?
7.

```javascript
var a = 42;
var b = a + ""; // implicit or explicit?
var c = String(a); // implicit or explicit?
```

8. Abstract value operations? (4)
9. ToString abstract value operation?
10. What's stringification for built-in primitive values?

-   null
-   undefined
-   true
-   false
-   10

11. For regular objects, what happen in ToString abstract value operation?
12. ToString abstract value operation for Array?
13.

```javascript
var a = [1, 2, 3];
a.toString();
```

14. What's JSON.stringify()
15. For simple values, What's difference between toString and JSON.stringify?
16. JSON.stringify(42);
17. What's JSON-safe?
18. Which values are not JSON-safe? (4)
19. JSON.stringify utility what will do with not safe values?
20. What's result?

-   JSON.stringify(undefined);
-   JSON.stringify(fn(){});
-   JSON.stringify([1, undefined, fn(){}, 4]);
-   JSON.stringify({
    a: 2,
    b: function(){},
    });

21. toJSON? What's it usage? What's it return?
22. Explain

```javascript
    var o = {};
    var a = {
        b: 42,
        c: o,
        d: fn(){}
    }
    o.e = a;
    a.toJSON = function(){
        return {
            b: this.b,
        };
    }
    JSON.stringify(a);
```

23. What's second argument for **JSON.stringify()**?
24. What's third parameter for JSON.stringify()?
25. How JSON.stringify() and ToString is related?
26. What's ToNumber abstract value operation?
27. What's ToNumber define these values become to number?
    -   true
    -   false
    -   undefined
    -   null
28. ToNumber for a string value, how it works?
    -   How it works?
    -   If fails, What's result?
    -   0-prefixed value?
29. ToNumber abstract value operation for objects(and arrray)?
30. ToPrimitive abstract operation?
31. How to create non coercible object?
