# Decorator-Pattern

## summary

Decorator-Pattern is the pattern that the decorator class is inherited by target interface(or abstract class) to serve as a target class and composite it to add additional functionally in specific functions 

this pattern helps adding additional functionality without modifying an existing object as decorating this

### example: Cafe

there are a few coffee type class inherited by beverage, abstract class.
let's imagine that you want to add more options like whip, milk, and soy in a coffee 

1. let's create new classes (latte with whip, latte with soy)
	- there would be too many classes
2. let's add the options(toppings) in beverage abstract class
	- it makes modification for existing code and adding useless fields and functions for some of sub-class  

so, solution: decorator pattern
- Just create the decorator classes(milk, soy, whip classes) and apply it to them
- we can extend functionality more flexible
	- when you have to add new functionality, it helps extension without modification


### notes of caution

- complex architecture
	- we have many other options
- it is bad to dig into decorators and do something like parsing or reading something

## difference with strategy pattern

the **strategy pattern** allow you to change the implementation of something used at runtime
the **decorator pattern** allow you to add to an existing functionality with additional functionality at runtime

https://stackoverflow.com/questions/26422884/strategy-pattern-v-s-decorator-pattern


