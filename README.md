# Introduction to Functional Programming

## Contents

 1. What is Functional Programming?  
  1.1 Imperative vs Declarative, Functional vs Object Oriented  
  1.2 Examples of imperative vs functional style  
 2. Functional Programming: an overview  
  2.1 Principles of FP  
  2.2 FP and code quality: reasoning about your code  
  2.3 Functional language features  
 3. Recommended reading

## What is Functional Programming?

Functional Programming (FP) is a programming paradigm that orients itself around functions and function composition. It is *not* bound by language necessarily, though certain languages accommodate it more easily than others. We will see examples of this in the section about language features.

### Imperative vs Declarative, Functional vs Object Oriented

You might already be familiar with the Object Oriented Programming paradigm. This is an example of an imperative programming paradigm, which means: a statement-based programming paradigm, where the programmer uses statements to change a program's state. Functional Programming, on the other hand, is a declarative programming paradigm. This means: the programmer declares *what* a program should do, rather than *how* it should do this. In functional programming, this is done by declaring functions and composing them.

This leads to an important distinction between FP and OOP: FP is, in most cases, stateless, whereas OOP is not. This is important to realise because it affects the way in which you reason about your code.

### Examples of imperative vs functional style

**Example: getting the lengths of strings in an array**
```csharp
// Imperative

class LengthGetter {
  public static int[] StringLengths(string[] input) {
    int[] lengths = new int[input.Length];

    for (int i = 0; i < input.Length; i++) {
      lengths[i] = input[i].Length;
    }

    return lengths;
  }
}
```

```haskell
-- Functional

stringLengths :: [String] -> [Int]
stringLengths strs = map length strs
```

**Functional style in C#: using Linq!**

```csharp
using System.Linq;

class LengthGetter {
  public static int[] StringLengths_Func(string[] input) {
    return input.Select(str => str.Length).ToArray();
  }
}
```

## Functional Programming: an overview

### Principles of FP
Four important principles of FP are:
- Functions as first-class citizens
- Function purity
- Referential Transparency
- Recursion

**Functions as first-class citizens**

Functions should be treated as primary components of a program. They should be transferrable throughout the program like any other type is. This enables another principle of Functional Programming: higher-order functions. Higher order functions are functions that either take in another function as its input, or return another function as their output. Once such higher-order function was already mentioned previously: the function `map` shown in the imperative vs functional style examples.

**Function purity**

In imperative languages, a function can produce two outputs: returned values and side effects. Side effects include things like state mutation. Functional programming is, in principle, stateless. Because there is no state, it can also not be mutated. 

Some examples of the difference can be seen in the C# code below.

```csharp
class Example {
  private int counter;

  /// This function is pure.
  public int Pure(int num) {
    return num * 2;
  }

  /// This function is not pure because it changes the value of this.counter.
  public int NotPure(int num) {
    this.counter++;
    return num * 2;
  }

  /// This function is not pure because its result is dependent on the state (this.counter).
  public int NotPure2(int num) {
    return num * this.counter;
  }
}
```

**Referential Transparency**

A result of function purity is referential transparency. The principle of referential transparency describes that for all expressions in the program, if they are replaced with their corresponding results, this does not change the program's behaviour. As long as your functions are pure, this should be the case.

**Recursion**

Recursion describes the principle of defining methods in terms of themselves. In a lot of Functional Programming languages, recursion is the primary way of doing iteration. Recursive functions consist of two components: one or more recursive cases and one or more base cases, as demonstrated below. 

```csharp
class Example {
  /// This function is recursive.
  public static int SumUpTo(int num) {
    // For demonstration purposes, we assume num >= 0
    
    // The base case
    if (num == 0) { 
      return 0;
    }

    // The recursive case
    return num + SumUpTo(num - 1);
  }
}
```

### FP and code quality: reasoning about your code

As demonstrated in the principle of referential transparency, the principles of Functional Programming allow us to make certain assumptions. These assumptions should make it easier to reason about our code, because they limit what can go wrong. Function purity, for example, prevents the (program) state from interfering with your functions, which allows you to focus on your program's logic instead. 

### Functional language features
Four important functional language features are:
- Laziness
- Algebraic data types
- Pattern matching
- Partial function application

**Laziness**

Laziness in programming describes the idea that calculations should only be performed when used. For instance, if you were to get the length of the first element of a list of strings, only the length of the first element would be calculated. This is made possible by function purity, as this guarantees that no other side effects will occur while calculating the string's length.
```haskell
getFirstLength :: [String] -> Int
getFirstLength strs = head (map length strs)
```

**Algebraic data types**

Algebraic data types allow the programmer to form and name composite types from other types. This sets strict limits on which kinds of data you deal with, as well as that enables the developer to form algebras. 

```haskell
-- Algebraic data type of a linked list
data List a = Nil | Cons a (List a)
```

**Pattern matching**

Pattern matching is, among other things, a companion feature to algebraic data types. It works somewhat like a `switch`, except it also allows you to extract values from the type you're matching on. 

```haskell
-- Using pattern matching and recursion to get the List's size
size :: List -> Int
size Nil = 0
size (Cons _ n) = 1 + size n
```

**Partial function application**

In some functional languages, functions are defined with one argument at a time. This allows you to craft functions on the fly by partially applying the arguments a function needs. 

```haskell
-- 'mult' takes in 2 arguments: x and y
mult :: Int -> Int -> Int
mult x y = x * y

-- 'mult2' is defined as mult, but with the first argument defined as 2.
-- this function will multiply any number by 2.
mult2 :: Int -> Int
mult2 = mult 2

```

## Recommended reading

- [Microsoft's Tour of F#](https://docs.microsoft.com/en-us/dotnet/fsharp/tour)
- [Haskell in 5 steps](https://wiki.haskell.org/Haskell_in_5_steps)
- [Programming in Haskell](https://www.bol.com/nl/p/programming-in-haskell/9200000061967819/)