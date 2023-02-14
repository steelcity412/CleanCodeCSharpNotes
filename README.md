# Notes from _Clean Code: A Handbook of Agile Software Craftsmanship_ by Robert C. Martin

![GitHub last commit](https://img.shields.io/github/last-commit/steelcity412/CleanCodeCSharpNotes?label=Last%20updated&logo=LastCommit&style=plastic) ![GitHub Repo stars](https://img.shields.io/github/stars/steelcity412/CleanCodeCSharpNotes?color=Green&logo=RepoStars&style=plastic) ![GitHub forks](https://img.shields.io/github/forks/steelcity412/CleanCodeCSharpNotes?color=green&logo=Forks&style=plastic) ![GitHub watchers](https://img.shields.io/github/watchers/steelcity412/CleanCodeCSharpNotes?color=green&label=watchers&logo=RepoWatchers&style=plastic) ![GitHub followers](https://img.shields.io/github/followers/steelcity412?label=GitHub%20Followers&style=plastic) ![GitHub User's stars](https://img.shields.io/github/stars/steelcity412?affiliations=OWNER&label=GitHub%20Stars&logo=UserStats&style=plastic)

Link to book:

- [Amazon](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

## :warning: **Disclaimers**:

- **These are just notes I took while reading the book.**
- **I do not cover all the topics in this book so take sometime to read the book and show support to the author!**
- **Examples provided will be written in C#**
- **Give this a follow if this helped you out!** :)

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
  - The Whack() is suppose to represent the action of killing an application. So it might be better to name the method Kill() or KillApplication().

---

# Chapter 3: Functions

## Blocks and Indenting

- If you are starting to see nested structures such as IF statements, you should consider trying refactor the structure down into a method.

## Do One Thing (aka Single Responsibility Principle):

- Functions should be preforming one action or task
- "Functions should do one thing. They should do it well. They should do it only." - pg 35

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
- **Note**: Multiple levels of abstraction is not always bad. Just be aware of it when it pertains to building methods :)

## The Stepdown Rule

- Reading code from top to bottom
- This is a technique used to keeping the level of abstraction for functions at one level.
  > "We want every function to be followed by those at the next level of abstraction so that we can read the program, descending one level of abstraction at a time as we read down the list of functions." - pg 37

## Use Descripttive Names

### Use names that better describe the function

- Practice **Ward's Principle**
  > "You know you are working on clean code when each routine turns out to be pretty much what you expected." pg39
- The goal of achieving this principle is simple, make sure to choose good names for small functions that do one thing.
- The smaller and more focused a function is, the easier it is to choose a descriptive name.
  Ex: `IsTestable()` or `IsLeapYear()`.

### Don't be afraid to make a long name

- A long descriptive name is always better than:

  - having a short and non-descriptive method name
  - a long descriptive comment

- Try implementation a naming convention that can be easily read and used for other method names
  Ex: `GetCustomerAddress()` or `GetCompanyAddress()`

  - Using **Customer** and **Company** tells us what type of Address the method will be retrieving.

- Don't be afraid to spend sometime on the method name.

  - If I haven't mentioned it enough, it is very useful to have a meaningful name! :sunglasses:

- Be consistent with your names
  - Use the same **phrases, nouns, and verbs** in the function names

## Function Arguments :monocle_face:
