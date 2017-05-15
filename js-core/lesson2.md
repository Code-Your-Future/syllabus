# JavaScript Core 2
** What we will learn today?**
- Functions
- More Arrays and loops
  - Functional utils (map, foreach, filter)
- Objects
- Callbacks

---


## Conditionals

**TODO**

### Comparisons

**TODO**

- Introduce `==` and `!=`, `<` and `>`
- Introduce the concept of truthiness and falsiness for non-boolean types
- Introduce `===` and `!==`

### If/Else

**TODO**

### Switch

**TODO**

### The ternary operator

**TODO**

## Arrays

If you want to store a bunch of things, identifiers like `name1`, `name2`, `name3` and so on quickly become tiresome. **Arrays** to the rescue!

Imagine an array like a list of variables, but instead of each variable having its own name, only the array has a name. So how do you access a variable inside, then? How do you read and write? Using an *index*!

An index is just a whole number, such as `0`, `1`, `2` and so forth. As in many areas of computing, indices in JavaScript arrays start with `0` --- so `0` is the index of the first element of an Array, `1` is the index of the second element, and so forth.

### Creating an array

The easiest way to create an array is using the bracket (`[]`) syntax. Just put whatever elements you want in your array between the brackets, separated by comma:

```js
// Arrays can hold any data type
var countries = ['Scotland', 'Germany', 'Syria'];
var numbers = [7, 1, 23, 19, 11, 5, 16, 31];

// Data types can be mixed, but be wary of that!
var mixed = ['Tim', 27];

// Arrays can also be empty
var emptyArray = [];
```

### Reading, writing and length

Once you have an array, you might want to read values from it. You do this also using brackets, placed directly behind the array's variable name (identifier). The brackets hold the index of the element you want to read.

```js
var countries = ['Scotland', 'Germany', 'Syria'];

// Remember, the first index is 0
console.log(countries[0]); // 'Scotland'
console.log(countries[1]); // 'Germany'
console.log(countries[2]); // 'Syria'
```

In a similar fashion, you can write or overwrite values.

```js
var countries = ['Scotland', 'Germany', 'Syria'];

countries[1] = 'Sudan';

console.log(countries); // ['Scotland', 'Sudan', 'Syria']
```

You can also create new array elements by just writing to the respective index.

```js
var countries = ['Scotland', 'Germany', 'Syria'];

countries[3] = 'Sudan';

console.log(countries); // ['Scotland', 'Germany', 'Syria', 'Sudan']
```

You can also use other variables to store in an array, and integer variables to define the index you want to read from.

```js
var myCountry = 'Sudan';
var countries = ['Scotland', 'Germany', 'Syria', myCountry];
console.log(countries); // ['Scotland', 'Germany', 'Syria', 'Sudan']

var index = 2;
console.log(countries[index]); // 'Syria'
```

> Exercise/Homework: What happens when yo try to read from an index that is not there?

A really useful thing to know about an array is its *length*, i.e. the number of elements it contains. You can access it by appending `.length` to the arrays identifier. The length is always 1 more than the largest element index.

```js
var countries = ['Scotland', 'Germany', 'Syria'];

console.log(countries.length); // 3
```

### Useful array methods

#### Concatenating two arrays

You've learned how you can add two numbers and append two strings, but how does this work for arrays? A simple `arr1 + arr2` will not do, but there is a method you can use: `concat()`. It is a method that you call on the array (similar to how `console.log` is the `log` function called on `console`) and takes the array you want to append as a parameter.

```js
var countries = ['Scotland', 'Germany', 'Syria'];
var moreCountries = ['Sudan', 'Ethiopia', 'France'];

countries.concat(moreCountries);
console.log(countries); // ['Scotland', 'Germany', 'Syria', 'Sudan', 'Ethiopia', 'France']
```

#### Appending an element

If you want to append an element to an array, you can just put it after the last existing element like so:

```js
countries[countries.length] = 'United States of America';
```

There is another way though, which is a bit more elegant: the `push` function.

```js
countries.push('United States of America');

// .push can also be called with multiple parameters
countries.push('United States of America', 'France');
```

> Homework: Learn about `.slice` and `.pop`

There are many more useful array functions, which you will learn in lesson 2.

## Loops

**TODO**

### `for` loops

**TODO**

#### Traversing an array

By now you might have noticed that `for` loops can be really useful for working with arrays.

Imagine you want to print out every item in an array:

```js
var countries = ['Scotland', 'Germany', 'Syria'];
var i;

for(i = 0; i < countries.length; i++) {
  console.log(countries[i]);
}
```

### `while` loops

**TODO**

## Objects

**TODO**


## Functions
Functions are "self contained" modules of code that accomplish a specific task. Functions usually "take in" data, process
it, and "return" a result. Once a function is written, it can be used over and over and over again. (Utah University)


```javascript

//Function declarations

function sayHello() {
    console.log("hello");
}

function square(number) {
    return number*number;
}

square(5); // returns 25

//Function expressions

var addTen = function(number) {
    return number + 10;
};

addTen(5); // return 15

```


> **Exercise**:
> Open [this CodePen](http://codepen.io/rarmatei/pen/jBpdzx?editors=0012) and follow the instructions there

## Callbacks

You probably noticed in last few exercises that JavaScript functions can be passed
as arguments to other functions.

Callbacks are JavaScript functions that are passed as arguments to other functions
so they can be executed inside those functions once they're finished.

Example:

```javascript

function a(callback) {
    var x = 1000;
    if(callback) {
        callback();
    }
    return x;
}

```

> **Exercise**:
> - Look up the global `setTimeout` function
> - Write a function that takes a string as a parameter, waits 2 seconds, and then logs out the string


## More arrays and loops + tests

Before we dive into the exercises, a word on testing:
- All of us write buggy code. Thinking about what inputs our software is supposed to handle
and writing tests to verify that it behaves as expected for those inputs helps us
prevent most of those bugs.
- By writing good tests for our pieces of functionality helps ensure that no one else can
break it by mistake in the future
- Sometimes, just by thinking about what tests to write might bring up big flaws in our
initial logic

Testing example; consider the following code:

```javascript
function containsBob(a) {
    return a.includes("bob");
}
```

How might we test the above? Some example inputs we can test with:

```javascript
containsBob("aabobaa"); // expected: true, actual: true
containsBob("hello"); // expected: false, actual: false
containsBob("bob"); // expected: true, actual: true
containsBob("b ob"); // expected: false, actual: false
containsBob(""); // expected: false, actual: false

containsBob(1); // expected: false, actual: TypeError
```

> **Exercise**:
> Open [this CodePen](http://codepen.io/rarmatei/pen/EWJjrZ?editors=0012) and follow the instructions there

## A taster of functional programming - forEach, map, filter

Consider the following code:

```javascript

var numbers = [1,2,3];

function addTwo(number) {
    return number + 2;
}
```

We have an array of numbers and a function that returns its argument after adding 2 to it.

How would you write a program that adds 2 to each number in the initial array and returns
the result as a new array?

You could do something like this:

```javascript
var result = [];

for(var i=0; i<numbers.length; i++) {

  var current = numbers[i];
  var transformed = addTwo(current);
  result.push(transformed);
}

console.log(result);
```

There is a term for the operation of applying a function to a value and creating a new
value: projection. And it turns out JavaScript arrays come with a simple function to project
them to a new array: the `map` operator.

Let's see how we can re-write the above program using the map function:

```javascript
var result = numbers.map(addTwo);

console.log(result);
```

That's it! We use the map operator on an array and pass to it the function we want
applied to each element in that array. The function can take two parameters: one is the value
that will be transformed, and the second one is the index of the item in the array.

The function passed into is also a..callback!

> **Exercise**:
> Open [this CodePen](http://codepen.io/rarmatei/pen/JWQqoz?editors=0012) and follow the instructions there


## More on objects

Up until now we have created objects using the "literal notation":

```javascript
var myObject = {
  greeting: "hello"  
};
```

Another way to create object is using a function, combined with the `new` keyword:

```javascript
function Cat(name, furColor) {
    this.name = name;
    this.furColor = furColor;
}

var myCat = new Cat('Ron', 'blue');
```

In most cases, using "literal notation" to create a new object will work fine,
however there might be some cases where you want some special initialisation logic to happen
every-time you create a new instance of an object:

```javascript
function Person(firstName, lastName, age) {
    this.fullName = firstName + " " + lastName;
    this.yearOfBirth = (new Date()).getFullYear() - age;
}

var rares = new Person('Rares', 'Matei', 26);

// same object shape as:
var rares2 = {
    fullName: 'Rares Matei',
    yearOfBirth: 1991
};
```

We will get back to this in lesson 4 when discussing about prototypes and inheritance.

> **Exercise**:
> Open [this CodePen](http://codepen.io/rarmatei/pen/aJgxOL?editors=0012) and follow the instructions there


## Value types vs. reference types

A variable can hold two types of values: primitives (value types) and reference types.
The distinction between them is very important and will be a fundamental addition
to your JavaScript arsenal.

Primitives are:
 - string (example: `John Doe`)
 - number (example: `100`)
 - boolean (example: `true` or `false`)


Reference types are:
- Objects (example: `{greeting: "hello"}`)
- Arrays (example: `[1,2,3]`)
- Functions (example: `function doNothing() { }`)

Variables can only hold a few bytes of data.
Because primitives have fixed sizes, when you assign a primitive to a variable,
it will hold the actual value of the primitive (hence the name "value type").
But reference types can have practically infinite sizes, so when you assign a reference type
to a variable, that variable will hold a reference to it only: an identifier which will tell our program
where to look for that object in memory.

![Memory assignment](assets/stack_heap.png)

Let's make some sense of the above with exercises!

> **Exercise**:
> Open [this CodePen](http://codepen.io/rarmatei/pen/jBjoNL?editors=0012) and follow the instructions there


## Pass by value / reference

Consider the example below.

```javascript

function addFive(value) {
    value = value + 5;
}

var ten = 10;
addFive(ten);
console.log(ten);

```

We have a function that accepts a value as an argument. The function then adds five to the
argument and logs the value.
After invoking the function with the variable `ten`, the variable is logged.

What will be the values logged?
Answer: 10 (not 15)

Explanation:
In JavaScript, variables are always passed to function by value. That means only the value
the variables was holding is passed to the function, and not a reference to the variable's
location in memory. That means that inside a function call, any changes we make to its
arguments will only apply inside the function (as seen in the previous example).

**Be careful though**, as the value of an argument might be a reference to a JavaScript
object, in which case, changing a property on that object will also reflect everywhere
else we use a reference to that object.

For example:

```javascript

function a(primitive, object) {
    primitive = primitive + 5;
    object.greeting = "how are you?";
    object = {
      greeting: "holla!"  
    };
}
var primitive = 10;
var object = {
  greeting: 'hello'  
};
a(primitive, object);
console.log(primitive); // 10
console.log(object.greeting); // "how are you?"
```

# Resources
1. [Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
1. [Pass by value/reference](http://docstore.mik.ua/orelly/webprog/jscript/ch11_02.htm)
1. [Primitive Types and Reference Types](http://docstore.mik.ua/orelly/webprog/jscript/ch04_04.htm)

1. [Callbacks](http://javascriptissexy.com/understand-javascript-callback-functions-and-use-them/)
1. [Creating objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Creating_new_objects)

# Homework

1. First part of Homework - Easy
- write a function that returns whether a number exists in a list
Example:
    [1,2,3,4] -> does 6 exist -> false
              -> does 3 exist -> true
- write a function that concatenates two lists together
Example:
    [1,2,3], [7,8,9] -> [1,2,3,7,8,9]

- given the following object shape:

    var person = {
        name: "Bob",
        age: 25
    };

    Write a function "growOlder()" that accepts a "person" as an argument and returns a new person with his/her age increased by 1.


2. Second part of Homework:
Implement solutions to solve the following problems:

Problem 1.
Given the following array
[2,5,7,2,3], and the number T = 8
Build a solution that finds the two numbers in the array that add up to T.

Problem 2.
Think about how you would represent an employee as a JavaScript object.

Create the following functions:
- addEmployee: adds an employee to the list of existing employees
- search: allows you to search for an employee by name
- fire: deletes an employee by ID from the list
- changeRole: accepts as parameters an employee ID and a string for the new role it should have. Finds the employee by ID and changes his/her role.

3. **[Bonus/Optional]**
- Try to finish as many exercises as you can from http://reactivex.io/learnrx/ (try to finish up to exercise 8 at least)
- They're difficult, the point is for you to read, learn and understand more about the `.map` and `.filter` functions. It's okay if you can't finish them all.

4. **Research:**

## Prepare for the next class
1. Look over these examples for interacting with the DOM using JavaScript. We'll discuss these in more detail next week, but try to make an idea of the different API methods and what they do. [DOM Examples](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Examples)
