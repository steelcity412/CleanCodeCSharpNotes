# Clean Code: A Handbook of Agile Software Craftsmanship

by Robert C. Martin

Link to book:

- [Amazon](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

## :warning: **Disclaimer: Examples provided will be written in C#**

---
# Chapter 1: Introduction

What is the purpose of Clean Code?

- To make the code concise and readable within the code base
- "The code should be matter-of-fact as opposed to speculative" - pg 9
	- Meaning that the code should be factual and accurate instead of uncertainty and containing risks

---
# Chapter 2: Meaningful Names

## Class Names

- Class names should be nouns or a noun phrase
	- Ex: Customer, Product, Employee
- Avoid words such as Manager, Data, Processor, or Info
- Classes should never be written as a verb.

## Method Names

- Method names should be a verb or a verb phrase
	- Ex: Save, SendMessage, Publish
- Accessors, Mutators, and predicates should be named by their value
	- Ex: get, set, is, isNewOrder

## Don't be cute

- "Choose clarity over entertainment value" - pg26
- "Say what you mean. Mean What you say" - pg26
	- Ex: Whack() may be a clever/funny way to describe a method. However, if the next developer doesn't share the author's sense of humor then they might miss the true intent of the method.  
	- The Whack() is suppose to represent the action of killing an application.  So it might be better to name the method Kill() or KillApplication().

---
# Chapter 3: Functions

## Blocks and Indenting

- If you are starting to see nested structures such as IF statements,  you should consider trying refactor the structure down into a method.

## Do One Thing (aka Single Responsibility Principle):

- Functions should be preforming one action or task
- "Functions should do one thing.  They should do it well. They should do it only." - pg 35

##What do this quote mean by "one thing"?

- In order for our function to be executing "one thing", we need to make sure that the statements within our function are all on the same level of abstraction.


- Let's look at an example where having multiple levels of abstraction could be confusing
- Example: **Multiple levels of abstraction**

```C#
using System; 
public class Program 
{ 
	public static void Main() 
	{ 
		Console.WriteLine("Hello World"); 
		var mydate = Program.RetrieveDateTask(); 
	} 
	public static DateTime RetrieveDateTask() 
	{ 
		return GetDate(); 
	} 
	public static DateTime GetDate() 
	{ 
		return DateTime.Now; 
	} 
}
```
- Mixing and having multiple levels of abstraction within a function is always confusing.
- This is a very basic sample but if possible, try to minimize/reduce the levels of abstraction to the code to make it more readable and easier to understand.

- Lets see what happens when we take out the `RetrieveDateTask()` and just call `GetDate()`
- Example: **One level of abstraction**

```C#
using System;
public class Program
{
	public static void Main()
	{
		Console.WriteLine("Hello World");
		var mydate = Program.GetDate();
	}
	public static DateTime GetDate()
	{
		return DateTime.Now;
	}
}
```
- Removing that additional method makes the code much easier to read and understand.
- **Note**: Multiple levels of abstraction is not always bad.  Just be aware of it when it pertains to building methods :)

## The Stepdown Rule

- Reading code from top to bottom
- This is a technique used to keeping the level of abstraction for functions at one level.
	- "We want every function to be followed by those at the next level of abstraction so that we can read the program, descending one level of abstraction at a time as we read down the list of functions." - pg 37
	- 