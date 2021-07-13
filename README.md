# Functional programming
## What is functional programming?
It is a programming style focused on having specific cases, in which we worry about what to solve, not how to solve it. The important thing in functional programming is to have a function that can solve the problem no matter where it comes from. 

**Functional programming is based on:**
- Functions 
- Data

### Benefits of functional programming
- **Legibility**: We focus on what to solve, the functions will be more explicit about what it does, not how it does it.
- **Testing**: It will be easier to test, because having the code separated into small problems is easier to test a single function than having to solve the whole system.
- **Concurrency**: Concurrency becomes more dynamic because functional programming allows to release many simultaneous processes from the same function.
- **More defined behaviors**: behaviors will be given by simple functions, we will quickly understand what they do.
- **Less state management.**
- **No need to install anything additional.**
- 
## What is a function?
A data type or object that takes an **X** value and generates a **Y** value. Ideally, for every **X** it always generates a **Y**.
- A series of parameterized steps.
- May or may not return a result
- Can be defined, stored or declared on demand (like any other type).

**f(x) = x² + 5**

```bash
double parabola(double x){
	return Math.pow(x, 2) + 5;
}
```
**We can define functions with respect to other functions**
```bash
esPar(x) = ¡esNon(x)
```
**We can define functions with respect to themselves (recursion).**

 ```bash
 factorial(x) = if x <= 2 : 
x
else : x *
 factorial(x-1)

```
**We can define functions that take other functions as parameters**
```bash
f(x, g(x)) = x² * g(x)
```
### First Class Citizens
First class citizens, this means that functions are now recognized by the language as something we can define or use.
It is now possible to declare variables of type function and it is even possible to assign a value to them.

**How to define types?**
```bash
Function x;
Function sum =
...
```

**Take them as parameters or returns**
```bash
Int foo(Function param)

Function
bar(int x)
```

Define them on demand
```bash
//Defining a String
funWithString("Hi")

//A function (for now)
//Not obtained from a variable or somewhere else.
funWithFunction(x-> x * 2)
```

## Pure Functions
It is a function that always generates the same result for the same parameter.
```bash
//It will always be 8
sum(5, 3)
```
They are deterministic, meaning that we can predict the result of the execution of a pure function.
Example:
**f(x) = x³**
**Pure functions:**
- Does not generate random values
- Does not change the value of x
- Does not generate side effects
  - Does not change a database
  - Does not create a file 
  - Does not modify the system

**A pure function in Java**
```bash
Boolean hasAvailableFound(double balance){
Return balance > 0.0;
}
```
Functions that are not pure are known as impure functions.
The rules dictate that:
|     Function    |    may invoke: pure    |     may invoke: impure   |
|----------------|------------------------------|--------------------------------|
|     Pure       |     ✔                        |     ×                          |
|     Impure     |     ✔                        |    ✔                          |


## Side effects
Impure functions generate side effects
"Every change observable from outside the system is a side effect"

**Some side effects are:**
- Read/Create/Change/Delete files
- Read/Write a database
- Send/Receive a network call
- Altering an object/variable used by other functions

**Side effects**
- But we can reduce/control when they happen!
- Why avoid side effects?
- Side effects are unavoidable

## higher order function
A higher order function has at least one of the following characteristics:
- **It takes a function as parameter**
```bash
Int foo(Function param)
```
- **Returns a function as a result**
```bash
Function bar(int x)
```
- **Or both**.
```bash
Function baz(Function f)
```
**Advantages**
- Passing behaviors
- Share a communication medium (callbacks)
- Share logic/rules

## Lambda functions
They are based on a mathematical concept from the 1930s (Alonzo Church), 
They are anonymous functions, when you have a function that has no name it is known as anonymous functions.

**Function
It has a name:**
- Function baz = ...
- Int foo(...)
**Lambda
Does not have a name**
- X -> ...

**Why use them?**
- It is a single-use behavior
- A rule that is only required in one place
- It is an extremely simple function

**A lambda is still a function**
```bash
int calculateWith(Function calculatorFun){
//Do calculations and use the parameter_
return _
}

//Calling the function
int result = calculateWith(x -> x * 9);
```

## Immutability
### Advantages
- Once created, it cannot be altered.
- Makes it easy to create pure functions.
- Easy to use threads/concurrency.

### Disadvantages
- New Instance for each set of modifications.
- Requires special attention to design.
- Mutable objects out of reach.


## Functional Java 8: Operations and Collectors
### Lambdas, operations and returns
Using Stream we can simplify some operations, such as filtering, mapping, conversions and more.
When we talk about passing lambdas to a Stream operation, we are actually delegating to Java the creation of an object based on an interface:
- Consumer<T>: takes a data of type T and does not generate any result.
- Function<T,R>: takes a data of type T and generates a result of type R
- Predicate<T>: takes a data of type T and evaluates if the data meets a condition.
- Supplier<T>: does not receive any data, but generates a data of type T each time it is invoked.
- UnaryOperator<T>: takes a data of type T and generates a result of type T

### Operations
These functions that receive lambdas and are in charge of working (operating) on the data of a Stream are generally known as Operations.
There are two types of operations: intermediate and final.
Each operation applied to a Stream makes the original Stream no longer usable for further operations. It is important to remember this, because trying to add operations to a Stream that is already being processed is a very common mistake.
	
### Collectors
Once you have added operations to your data Stream, you usually reach a point where you can no longer work with a Stream and need to send your data in another format, for example, JSON or a List to a database.
There is a unique interface that combines all the above mentioned interfaces and that has as only utility to provide an operation to obtain all the elements of a Stream: Collector.
Collector<T, A, R> is an interface that will take data of type T from the Stream, a mutable data type A, where the elements will be added (mutable implies that we can change its content, like a LinkedList), and will generate a result of type R.
	
```bash
public List<String> getJavaCourses(Stream<String> coursesStream) {
    List<String> javaCourses =
        coursesStream.filter(course -> course.contains("Java"))
        .collect(Collectors.toList());
	
    return javaCourses;
}
```
## Terminal Operations
Terminal operations are those operations that do not generate a new Stream as a result. Their result may vary depending on the operation. The utility of these is to be able to generate a final value to all our operations or to consume the final data.
#### The most common terminal operations found in Stream are:
- anyMatch()
- allMatch()
- noneMatch()
- findAny()
- findFirst()
- min()
- max()
- reduce()
- count()
- toArray()
- collect()
- forEach()

### Matching terminal operations
The operations **anyMatch**, **allMatch** and **noneMatch** are used to determine if there are elements in a Stream that comply with a certain Predicate. This can be a simple way to validate the data of a Stream. They are terminal because all three return a boolean:
### Terminal search operations
**findAny**, **findFirst**
These operations return an Optional as a result of searching for an element inside the Stream.
The difference between the two is that findFirst will return an Optional containing the first element in the Stream if the Stream has a previously defined sort or find operation. Otherwise, it will work the same way as findAny, trying to return any element present in the Stream in a non-deterministic (random) way.
If the found element is null, you will have to deal with an annoying NullPointerException. If the Stream is empty, the return is equivalent to Optional.empty().
### Terminal reduction operations
**min**, **max**
They are two operations whose purpose is to obtain the smallest element (min) or the largest element (max) of a Stream using a Comparator. There can be cases of empty Stream, that is why the two operations return an Optional so that in those cases we can use Optional.empty.
The Comparator interface is a @FunctionalInterface, so it is easy to use min and max with lambdas:
```bash
Stream bigNumbers = Stream.of(100L, 200L, 1000L, 5L);
Optional minimumOptional = bigNumbers.min((numberX, numberY) -> (int) Math.min(numberX, numberY));
```
### Iteration terminal operations
forEach
It is an operation that receives a Consumer and has no return value (void). The main utility of this operation is to give an end use to the elements of the Stream.
```bash
Stream<list> courses = getCourses();
courses.forEach(courseList -> System.out.println("Available courses: " + courseList));
```
### Intermediate operations
An intermediate operation is any operation within a Stream that returns a new Stream as a result. That is to say, after invoking an intermediate operation with a certain type of data, we will obtain as a result a new Stream containing the already modified data.
The Stream that receives the intermediate operation becomes "consumed" after the invocation of the operation, being unusable for further operations. If we decide to use the Stream for some other type of operations we will have an IllegalStateException.
Example:
		
```bash
	Stream initialCourses = Stream.of("Java", "Spring", "Node.js");

Stream lettersOnCourses = initialCourses.map(course -> course.length());
//From this point on, initialCourses cannot add any more operations.

Stream evenLengthCourses = lettersOnCourses.filter(courseLength -> courseLength % 2 == 0);
//lettersOnCourses is consumed at this point and cannot add any more operations. It is not possible to use the Stream except as a reference.
```


 	
