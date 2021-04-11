# Introduction to Functional Programming

## Contents

TODO

## What is Functional Programming?

Functional Programming (FP) is a programming paradigm that orients itself around functions and function composition. It is *not* bound by language necessarily, though certain languages accommodate it more easily than others.

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
# Functional

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

### FP and Code Quality: reasoning about your code


### Functional language features




## Functional Programming in Practice

### Haskell


### C# & F#


### JavaScript


## Recommended reading

- [Microsoft's Tour of F#](https://docs.microsoft.com/en-us/dotnet/fsharp/tour)
- [Programming in Haskell](https://www.bol.com/nl/p/programming-in-haskell/9200000061967819/)