1. ### OO programming?
   object oriented (OO) programming
2. ### Is class orientation a design pattern?
   "class orientation" as a design pattern
3. ### Mechanics of classes?
   mechanics of "classes": "instantiation", "inheritance" and "(relative) polymorphism".
4. ### Class/inheritance describes what?
   "Class/Inheritance" describes a certain form of code organization and architecture -- a way of modeling real world problem domains in our software.
5. ### Class oriented programming stress what about data? example?
   OO or class oriented programming stresses that data intrinsically has associated behavior (of course, different depending on the type and nature of the data!) that operates on it, so proper design is to package up (aka, encapsulate) the data and the behavior together. This is sometimes called "data structures" in formal computer science.
6. ### Relation between classes and data structure? (classification)
   Classes also imply a way of classifying a certain data structure. The way we do this is to think about any given structure as a specific variation of a more general base definition.
7. ### Classification process with car example? class? inheritance? instantiation?

   The definition of `Vehicle` might include things like propulsion (engines, etc.), the ability to carry people, etc., which would all be the behaviors. What we define in `Vehicle` is all the stuff that is common to all (or most of) the different types of vehicles (the "planes, trains, and automobiles").
   It might not make sense in our software to re-define the basic essence of "ability to carry people" over and over again for each different type of vehicle. Instead, we define that capability once in `Vehicle`, and then when we define `Car`, we simply indicate that it "inherits" (or "extends") the base definition from `Vehicle`. The definition of `Car` is said to specialize the general `Vehicle` definition.While `Vehicle` and `Car` collectively define the behavior by way of methods, the data in an instance would be things like the unique VIN of a specific car, etc.
   **And thus, classes, inheritance, and instantiation emerge.**

8. ### Relative polymorphism?
   Another key concept with classes is "polymorphism", which describes the idea that a general behavior from a parent class can be overridden in a child class to give it more specifics. In fact, relative polymorphism lets us reference the base behavior from the overridden behavior.
9. ### Class design pattern? lower level mechanics or design pattern? compare with functional programming? languages?

   Class theory strongly suggests that a parent class and a child class share the same method name for a certain behavior, so that the child overrides the parent (differentially). As we'll see later, doing so in your JavaScript code is opting into frustration and code brittleness.

10. ### Class in JS?

Where does JavaScript fall in this regard? JS has had *some* class-like syntactic elements (like `new` and `instanceof`) for quite awhile, and more recently in ES6, some additions, like the `class` keyword.

But does that mean JavaScript actually *has* classes? Plain and simple: **No.**

11. ### Explain building in class mechanics?

- Where come form, traditional metaphor for class and instance?
- An Architect plans out what?
- An Architect care about what? and not care about what?
- Relationship between blueprints and construction?
- What does constructor of building?
- Relationship between blueprint and buildin is direct or indirect?
- Relationship between class and instance is direct or indirect?

A. The traditional metaphor for "class" and "instance" based thinking comes from a building construction.
B. An architect plans out all the characteristics of a building: how wide, how tall, how many windows and in what locations, even what type of material to use for the walls and roof.
C. She doesn't necessarily care, at this point, *where* the building will be built, nor does she care *how many* copies of that building will be built. She also doesn't care very much about the contents of the building -- the furniture, wall paper, ceiling fans, etc. -- only what type of structure they will be contained by.
D. The architectural blue-prints she produces are only *plans* for a building. They don't actually constitute a building we can walk into and sit down. We need a builder for that task. A builder will take those plans and follow them, exactly, as he *builds* the building. In a very real sense, he is *copying* the intended characteristics from the plans to the physical building.
E. The architectural blue-prints she produces are only *plans* for a building. They don't actually constitute a building we can walk into and sit down. We need a builder for that task. A builder will take those plans and follow them, exactly, as he *builds* the building. In a very real sense, he is *copying* the intended characteristics from the plans to the physical building.
F. The relationship between building and blue-print is indirect. You can examine a blue-print to understand how the building was structured, for any parts where direct inspection of the building itself was insufficient. But if you want to open a door, you have to go to the building itself -- the blue-print merely has lines drawn on a page that *represent* where the door should be.
G. It's more useful to consider the direct relationship of a class to an object instance, rather than any indirect relationship between an object instance and the class it came from. **A class is instantiated into object form by a copy operation.**

12. ### What's constructor? example?
    Instances of classes are constructed by a special method of the class, usually of the same name as the class, called a *constructor*. This method's explicit job is to initialize any information (state) the instance will need.

**For example**, consider this loose pseudo-code (invented syntax) for classes:

```jsx
class CoolGuy {
  specialTrick = nothing;

  CoolGuy(trick) {
    specialTrick = trick;
  }

  showOff() {
    output("Here's my trick: ", specialTrick);
  }
}
```

To *make* a `CoolGuy` instance, we would call the class constructor:

```jsx
Joe = new CoolGuy("jumping rope");

Joe.showOff(); // Here's my trick: jumping rope
```

13. ### What's object in result of instantiation of class?
    We get an object back (an instance of our class) from the constructor,
14. ### Class inheritance?
    In class-oriented languages, not only can you define a class which can be instantiated itself, but you can define another class that inherits from the first class.
15. ### What's child class and parent class?
    The second class is often said to be a "child class" whereas the first is the "parent class". These terms obviously come from the metaphor of parents and children, though the metaphors here are a bit stretched.
16. ### What's relationship between child and parent?
    When a parent has a biological child, the genetic characteristics of the parent are copied into the child. Obviously, Once the child exists, he or she is separate from the parent. The child was heavily influenced by the inheritance from his or her parent, but is unique and distinct. If a child ends up with red hair, that doesn't mean the parent's hair was or automatically becomes red.
17. ### Vehicle, Car, SpeedBoat example?

```javascript
class Vehicle {
	engines = 1

	ignition() {
		output( "Turning on my engine." )
	}

	drive() {
		ignition()
		output( "Steering and moving forward!" )
	}
}

class Car inherits Vehicle {
	wheels = 4

	drive() {
		inherited:drive()
		output( "Rolling on all ", wheels, " wheels!" )
	}
}

class SpeedBoat inherits Vehicle {
	engines = 2

	ignition() {
		output( "Turning on my ", engines, " engines." )
	}

	pilot() {
		inherited:drive()
		output( "Speeding through the water with ease!" )
	}
}
```

We define the `Vehicle` class to assume an engine, a way to turn on the ignition, and a way to drive around. But you wouldn't ever manufacture just a generic "vehicle", so it's really just an abstract concept at this point.

So then we define two specific kinds of vehicle: `Car` and `SpeedBoat`. They each inherit the general characteristics of `Vehicle`, but then they specialize the characteristics appropriately for each kind. A car needs 4 wheels, and a speed boat needs 2 engines, which means it needs extra attention to turn on the ignition of both engines.

18. ### Super class?
    In many languages, the keyword super is used, in place of this example's inherited:, which leans on the idea that a "super class" is the parent/ancestor of the current class.
19. ### Polymorphism? relative polymorphism?

    `Car` defines its own `drive()` method, which overrides the method of the same name it inherited from `Vehicle`. But then, `Car`s `drive()` method calls `inherited:drive()`, which indicates that `Car` can reference the original pre-overridden `drive()` it inherited. `SpeedBoat`s `pilot()` method also makes a reference to its inherited copy of `drive()`.
    This technique is called "polymorphism", or "virtual polymorphism". More specifically to our current point, we'll call it "relative polymorphism".

20. ### In JS what is relationship between class and construction?
    Note: Another thing that traditional class-oriented languages give you via super is a direct way for the constructor of a child class to reference the constructor of its parent class. This is largely true because with real classes, the constructor belongs to the class. However, in JS, it's the reverse -- it's actually more appropriate to think of the "class" belonging to the constructor (the Foo.prototype... type references). Since in JS the relationship between child and parent exists only between the two .prototype objects of the respective constructors, the constructors themselves are not directly related, and thus there's no simple way to relatively reference one from the other (see Appendix A for ES6 class which "solves" this with super).
21. ### Multiple inheritance?
    Another aspect of polymorphism is that a method name can have multiple definitions at different levels of the inheritance chain, and these definitions are automatically selected as appropriate when resolving which methods are being called.
22. ### Dimond problem with multiple inheritance?
    There's another variation, the so called "Diamond Problem", which refers to the scenario where a child class "D" inherits from two parent classes ("B" and "C"), and each of those in turn inherits from a common "A" parent. If "A" provides a method drive(), and both "B" and "C" override (polymorph) that method, when D references drive(), which version should it use (B:drive() or C:drive())?
23. ### Does JS have multiple inheritance?
24. JS object mechanism does perform copy behavior when you inherit? or instantiate?
25. Is there class in JS?
26. JS has object, and objects don't get copied, but they get what? how?
27. How JS developers fake the missing copy behavior of classes in javascript?
28. Type of mixins?
29. Explicit mixin? example?
30. In explicit mixin, how function and object will be copied?
31. Polymorphism in explicit mixin?
32. Parasitic inheritance?
33. Implicit mixin?
