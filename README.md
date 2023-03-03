# Personal Notes from _Clean Code: A Handbook of Agile Software Craftsmanship_ by Robert C. Martin

![GitHub last commit](https://img.shields.io/github/last-commit/steelcity412/CleanCodeCSharpNotes?label=Last%20updated&logo=LastCommit&style=plastic) ![GitHub Repo stars](https://img.shields.io/github/stars/steelcity412/CleanCodeCSharpNotes?color=Green&logo=RepoStars&style=plastic) ![GitHub forks](https://img.shields.io/github/forks/steelcity412/CleanCodeCSharpNotes?color=green&logo=Forks&style=plastic) ![GitHub watchers](https://img.shields.io/github/watchers/steelcity412/CleanCodeCSharpNotes?color=green&label=watchers&logo=RepoWatchers&style=plastic) ![GitHub followers](https://img.shields.io/github/followers/steelcity412?label=GitHub%20Followers&style=plastic) ![GitHub User's stars](https://img.shields.io/github/stars/steelcity412?affiliations=OWNER&label=GitHub%20Stars&logo=UserStats&style=plastic)

## Summary:

This document contains my notes and highlights from reading the book 'Clean Code: A Handbook of Agile Software Craftsmanship' by Robert Cecil Martin. The book delves into the principles and practices of writing clean, maintainable, and readable code. It covers topics such as naming conventions, functions, objects, and data structures, as well as larger issues such as architecture and system design. By following the author's guidelines and examples, I aim to improve my own coding skills and enhance the quality of my code. The author's expertise in software development and his clear and concise writing style make 'Clean Code' a valuable resource for anyone looking to improve their coding skills and write high-quality, maintainable code. If you're interested in learning more about writing clean and maintainable code, I highly recommend this book.

## :open_book: Where to buy book:

- [Amazon](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
- [Barnes & Noble](https://www.barnesandnoble.com/w/clean-code-robert-c-martin/1101628669)

## :warning: **Disclaimers**:

- **These are just notes I took while reading the book.**
- **I do not cover all the topics in this book so take sometime to read the book and show support to the author!**
- **Examples provided will be written in C#**
- **Give this a follow if this helped you out!** :smiley:

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
  - Ex: `Save()`, `SendMessage()`, `Publish()`
- Accessors, Mutators, and predicates should be named by their value
  - Ex: get, set, is, isNewOrder

## Don't be cute

- "Choose clarity over entertainment value" - pg26
- "Say what you mean. Mean What you say" - pg26
  - Ex: `Whack()` may be a clever/funny way to describe a method. However, if the next developer doesn't share the author's sense of humor then they might miss the true intent of the method.
  - The `Whack()` is suppose to represent the action of killing an application. So it might be better to name the method `Kill()` or `KillApplication()`.

---

# Chapter 3: Functions

## Blocks and Indenting

- If you are starting to see nested structures such as IF statements, you should consider trying refactor the structure down into a method.

## Do One Thing (aka Single Responsibility Principle):

- Functions should be preforming one action or task
- "Functions should do one thing. They should do it well. They should do it only." - pg 35

## What do this quote mean by "one thing"?

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
- **Note**: Multiple levels of abstraction is not always bad. Just be aware of it when it pertains to building methods :smiley:

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

  - If I haven't mentioned it enough, it is very useful to have a meaningful method name! :sunglasses:

- Be consistent with your names
  - Use the same **phrases, nouns, and verbs** in the function names

## Function Arguments 

### Fewer Arguments are Better
- Functions with fewer arguments are easier to understand and use. 
- When a function has too many arguments, it can become difficult to keep track of what each argument represents and how they should be used.

### Arguments Should Tell a Story 
- Good function arguments should clearly communicate what the function does. 
- Ideally, someone should be able to read the arguments and understand the purpose of the function without reading the implementation.

### Use Default Values 
- When a function has many optional arguments, it can be helpful to use default values for the ones that are frequently used. 
- This allows the caller to only specify the arguments that are important to them.

### Use Exceptions Instead of Error Codes
- Functions should use exceptions to indicate error conditions instead of returning error codes. 
- This makes it easier to understand the code and reduces the likelihood of bugs.

### Avoid Output Arguments 
- Functions should return values, not modify output arguments. 
- This makes the code easier to understand and avoids unexpected side effects.


## Structure Programming
- Structured programming is a programming paradigm that emphasizes the use of structured control flow constructs (such as loops, conditionals, and subroutines) to make code easier to reason about.
- This concept helps avoid the "spaghetti code" problem that can occur when code becomes too complex and difficult to follow. By breaking code into smaller, more understandable pieces, developers can more easily identify bugs, make changes, and ensure that code is working as intended.
- A basic example in C# that demonstrates structured programming principles:

```C#
public int FindMax(int[] numbers)
{
    int max = numbers[0];

    for (int i = 1; i < numbers.Length; i++)
    {
        if (numbers[i] > max)
        {
            max = numbers[i];
        }
    }

    return max;
}
```
- This function takes an array of integers and returns the maximum value in the array. 
- It uses a simple for `loop` to iterate over the array, comparing each value to the current maximum value and updating it if a larger value is found. 
- By breaking the problem down into smaller steps, and using a clear and concise control flow structure, this code is easier to understand and maintain than if it were written as a long, convoluted series of nested conditionals or loops.

## How do I write functions with the concepts mentioned in this chapter?
- To put it simply - you can't on your first try.
- My rule is to build out the function and then come back and refactor with the concepts mentioned in this section
- You can spend time refactoring when you start building the function but I've found that it is beneficial to refactor once the function or logic is built.