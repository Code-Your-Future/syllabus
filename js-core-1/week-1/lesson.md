![Lesson Ready](https://img.shields.io/badge/status-ready-green.svg)

# JavaScript Core I - 1

[Mentor Notes](./mentors.md)

**What we will learn today?**

* [Hello World](#hello-world)
* [Variables](#variables)
* [Strings](#strings)
* [String concatenation](#string-concatenation)
* [Numbers](#numbers)
* [Floats](#floats)
* [Functions](#functions)
* [Function Parameters](#function-parameters)
* [Nested Functions](#functions-nested)

---

> Please make sure you've forked [the js-exercises repo](https://github.com/CodeYourFuture/js-exercises) at the start of the class. This is the repo we will use during the class, and for homework.

## Prerequisites
1. Access to a Linux console (either on Mac, Ubuntu or by using Ubuntu WSL for Windwos 10)
2. VS Code running a default Linux terminal
3. NodeJS must be installed

## Hello World

It is programming tradition that the first thing you do in any language is make it output 'Hello world!'.

We'll do this in JavaScript, using a command called `console.log()`. The `console.log()` method writes a message to the console.

The console is a tool which is mainly used to log information - it's useful for testing purposes.

### Exercise (10 minutes)
*(This exercise will help you understand how to run a basic JS script and explore the different ways you can run JS code)*
1. Create your first `js1-week1.js` script
2. Type `console.log("Hello World!")`
3. There are 2 ways you can run this script - one way is by pressing F5 in your VS Code application. Can you find out what the second way is? Pair up and use a search engine to find out! Choose your favourite method and use that from now on.

**BONUS:** there is a third way of running JS code (notice how I haven't said scipt) - do you know what that is?

### Exercise (5 minutes)
*(This exercise will help you expand your understanding of console.log)*

Write 10 statements like these, but in different languages.

For example:

```
Halo, dunia! // Indonesian
Ciao, mondo! // Italian
Hola, mundo! // Spanish
```

## Variables

When you write code, you'll want to create shortcuts to data values so you don't have to write out the same value every time.

We can use a _variable_ to create a reference to a value. Variables can be thought of as named containers. You can place data into these containers and then refer to the data simply by naming the container.

Before you use a variable in a JavaScript program, you must declare it. Variables are declared with _let_ and _const_ keywords as follows.

```js
let greeting = "Hello world";

console.log(greeting);
```

```js
const name = "Irina";

console.log(name);
```

The program above will print "Hello world" to the console. Notice how it uses the value assigned to the variable `greeting`.

### Exercise (5 minutes)

1. Add a variable `greeting` to js1-week1.js and assign a greeting of your choice to the variable
2. Print your `greeting` to the console 3 times. You should see your greeting 3 times on the console, one on each line.

## Strings

In programming there are different _types of_ data. You've used one data type already: **string**.

Computers recognise strings as a sequence of characters but to humans, strings are simply lines of text.

```js
const message = "This is a string";
```

Notice that strings are always wrapped **inside of quote marks**. We do this so that the computer knows when the string starts and ends.

You can check that the data is a string by using the `typeof` operator:

```js
const message = "This is a string";
const messageType = typeof message;

console.log(messageType); // logs 'string'
```

### Exercise (5 minutes)

1. Write a program that logs a variable `colors` which contains the primary colors that make Orange color as a string separated by comma and also logs its type using `typeof`.
2. What is the `typeof` a number?

## String concatenation

You can add two strings together using the plus operator (`+`) or *string interpolation*. String interpolation is a useful JavaScript feature that allows you to inject variables directly into a string:

```js
// Here is an example using the plus operator to concat strings
const greetingStart = "Hello, my name is ";
const name = "Daniel";

const greeting = greetingStart + name;

console.log(greeting); // Logs "Hello, my name is Daniel"
```

```js
// Here is example using the String interpolation to concat strings
const greetingStart = "Hello";
const name = "Daniel";

const greeting = `${greetingStart}, my name is ${name}`;

console.log(greeting); // Logs "Hello, my name is Daniel"
```

### Exercise (5 mins)

1. Write a program that logs a message with a greeting and your name using the two concatenation methods we used

## Numbers as integer

The next data type we will learn is **number**.

Unlike strings, numbers do not need to be wrapped in quotes.

```js
const age = 30;
```

You can use mathematical operators to calculate numbers:

```js
const sum = 10 + 2; // 12
const product = 10 * 2; // 20
const quotient = 10 / 2; // 5
const difference = 10 - 2; // 8
```

### Exercise (10 mins)

1. Create two variables `numberOfStudents` and `numberOfMentors`
2. Log a message that displays the total number of students and mentors

#### Expected result

```sh
Number of students: 15
Number of mentors: 8
Total number of students and mentors: 23
```

## Numbers as decimals

Numbers can be integers (whole numbers) or floats (numbers with a decimal).

```js
const preciseAge = 30.612437;
```

Numbers with decimals can be rounded to the nearest whole number using the `Math.round` function:

```js
const preciseAge = 30.612437;
const roughAge = Math.round(preciseAge); // 30
```

### Exercise (15 mins)

1. Using the variables provided in the exercise calculate the percentage of mentors and students in the group
2. Using online documentation, what other things can you do with the `Math` library? Pick one thing on your table that you can do other than `Math.round` and prepare an explanation for the rest of the class

#### Expected result

```sh
Percentage students: 65%
Percentage mentors: 35%
```

## Functions

Functions are blocks of code that can do a task as many times as you ask them to. They take an input and return an output.

Here's a function that doubles a number:

```js
function double(number) {
  return number * 2;
}
```

To use the function we need to:
a) _call_ it with an input and
b) assign the returned value to a variable

```js
var result = double(2);

console.log(result); // 4
```

The input given to a function is called a **parameter**.

A function can take more than one parameter:

```js
function add(a, b) {
  return a + b;
}
```

When you write a function (sometimes called _declaring a function_) you assign names to the parameters inside of the parentheses (`()`). Parameters can be called anything.

This function is exactly the same as the on above:

```js
function add(num1, num2) {
  return num1 + num2;
}
```

### Exercise (20 minutes)

1. In pairs, design and create a function that:
  * takes in more than one input
  * uses string concatenation
  * performs some form of operation on a number
  * uses `return` to return a **string**
2. Comment your function to explain what it does
3. Call your function and run your script
4. What's the difference between a `return` and `console.log`?
5. When would you choose to use functions over the way we have been scripting so far?

### Exercise (10 minutes)
1. Swap your laptop with your neighbouring pair and review each other's code - what can be improved? Is the code readable?

## Nested Functions

Functions are very powerful.

* You can write more than one line of code inside of functions.
* You can use variables inside of functions.
* You can call other functions inside of functions!

```js
function getAgeInDays(age) {
  return age * 365;
}

function createGreeting(name, age) {
  var ageInDays = getAgeInDays(age);
  var message =
    "My Name is " + name + " and I was born over " + ageInDays + " days ago!";
  return message;
}
```

## Exercise (20 mins)

1. Write a function that returns the year someone is born given their age as input
2. Using the answer from step 1, write a function that takes someone's name and age as input and returns a string that states the person's name and age in a sentence

{% include "./homework.md" %}