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

10. ### Class in JS?

11. Explain building in class mechanics?

- Where come form, traditional metaphor for class and instance?
- An Architect plans out what?
- An Architect care about what? and not care about what?
- Relationship between blueprints and construction?
- What does constructor of building?
- Relationship between blueprint and buildin is direct or indirect?
- Relationship between class and instance is direct or indirect?

12. What's constructor? example?
13. What's object in result of instantiation of class?
14. Class inheritance?
15. What's child class and parent class?
16. What's relationship between child and parent?
17. Vehicle, Car, SpeedBoat example?
18. Super class?
19. Polymorphism? relative polymorphism?
20. In JS what is relationship between class and construction?
21. Multiple inheritance?
22. Dimond problem with multiple inheritance?
23. Does JS have multiple inheritance?
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
