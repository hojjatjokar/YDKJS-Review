1. ### What's type?
A type is an intrinsic, built-in set of characteristics that uniquely identifies the behavior of a particular value and distinguishes it from other values, both to the engine and to the developer.

2. ### JS built-in types?
JavaScript defines seven built-in types:

- `null`
- `undefined`
- `boolean`
- `number`
- `string`
- `object`
- `symbol` -- added in ES6!

3. ### typeof operator? what return?
The `typeof` operator inspects the type of the given value, and always returns one of seven string values
4. ### typeof **null** ?
"object"
5. ### How to test a variable for a **null** value?
```javascript
(!a && typeof a === "object");
```
6. ### typeof function(){}
"function"
7. ### Explain

```javascript
  function a(b,c){...}
  a.length
```

8. ### What is function type?
"function"
9. ### What is function in JS compared to object?
A function is referred to as a "callable object" -- an object that has an internal `[[Call]]` property that allows it to be invoked.
10. ### In JS variables have type or values?
In JavaScript, variables don't have types -- values have types. Variables can hold any value, at any time.
11. ### **undefined** vs undeclared?
An "undefined" variable is one that has been declared in the accessible scope, but *at the moment* has no other value in it. By contrast, an "undeclared" variable is one that has not been formally declared in the accessible scope.

Consider:

```jsx
var a;

a; // undefined
b; // ReferenceError: b is not defined
```

An annoying confusion is the error message that browsers assign to this condition. As you can see, the message is "b is not defined," which is of course very easy and reasonable to confuse with "b is undefined." Yet again, "undefined" and "is not defined" are very different things. It'd be nice if the browsers said something like "b is not found" or "b is not declared," to reduce the confusion!

12. ### Explain

```javascript
var a;
typeof a;
typeof b;
```

There's also a special behavior associated with `typeof` as it relates to undeclared variables that even further reinforces the confusion. Consider:

```jsx
var a;

typeof a; // "undefined"

typeof b; // "undefined"
```

The `typeof` operator returns `"undefined"` even for "undeclared" (or "not defined") variables. Notice that there was no error thrown when we executed `typeof b`, even though `b` is an undeclared variable. This is a special safety guard in the behavior of `typeof`.

Similar to above, it would have been nice if `typeof` used with an undeclared variable returned "undeclared" instead of conflating the result value with the different "undefined" case.

13. ### Special safetey gaurad of type of?
This safety guard is a useful feature when dealing with JavaScript in the browser, where multiple script files can load variables into the shared global namespace.
14. ### usage of safetey gaurd of typeof?
This sort of check is useful even if you're not dealing with user-defined variables (like `DEBUG`). If you are doing a feature check for a built-in API, you may also find it helpful to check without throwing an error:

```javascript
if (typeof atob === "undefined") {
	atob = function() { /*..*/ };
}
```
14. Dependency enjection?
Other developers would prefer a design pattern called "dependency injection," where instead of `doSomethingCool()` inspecting implicitly for `FeatureXYZ` to be defined outside/around it, it would need to have the dependency explicitly passed in, like:

```jsx
function doSomethingCool(FeatureXYZ) {
	var helper = FeatureXYZ ||
		function() { /*.. default feature ..*/ };

	var val = helper();
	// ..
}
```
