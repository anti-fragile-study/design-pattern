# Decorator-Pattern


## Summary

Decorator-Pattern is the pattern where the decorator class inherits from the target interface(or abstract class) and holds a reference to an instance of the target interface. This composition allows the decorator to add additional functionality to specific methods without altering the existing object’s structure.

### Example: Cafe

There are a few coffee type class inherited by the beverage, abstract class.
Let's imagine that you want to add more options like whip, milk, and soy in a coffee 

**Without Decorator Pattern:**

1. You might create new classes for each combination, such as LatteWithWhip and LatteWithSoy.
	- This approach leads to an explosion of classes as more options are added.
2. Modifying the Beverage abstract class to include all possible options can result in unnecessary fields and methods for some subclasses.

**With Decorator Pattern:**

- Just create the decorator classes for each options (e.g., milk, soy, whip classes) and apply it to the base Beverage objects as needed
- this approach allows for more flexible and scalable functionality extension without modifying existing code.

### notes of caution

- complex architecture, making the system harder to understand
	- we have many other options
- when we use the decorator pattern, it is hard to dig into decorators and do something like parsing or reading data

## difference with strategy pattern

The **strategy pattern** allow you to change the implementation of something used at runtime.

The **decorator pattern** allow you to add to an existing functionality with additional functionality at runtime

https://stackoverflow.com/questions/26422884/strategy-pattern-v-s-decorator-pattern


