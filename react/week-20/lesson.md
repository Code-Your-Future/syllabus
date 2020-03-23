# React 2

![](https://img.shields.io/badge/status-draft-darkred.svg)

**What will we learn today?**

- [Recap](#recap)
- [Making an Argument for Props](#making-an-argument-for-props)	
- [What Are Props?](#what-are-props)
- [Reacting to Changes](#reacting-to-changes)
- [State](#state)

## Recap

Last week we looked at how to write a `HelloMentor` React component ([interactive example](https://stackblitz.com/edit/react-jnkuqk)):


```js
// Mentor.js
class Mentor extends React.Component {
    render() {
        return <span>Ali</span>
    }
}

// index.js
import Greeting from './Greeting'
import Mentor from './Mentor'

class HelloMentor extends React.Component {
    render() {
        return (
            <div>
                <Greeting />
                <Mentor />
            </div>
        )
    }
}
```
## Making an Argument for Props	

 What's the problem with this component? Hint: imagine what a user story might look like for this small application. How might changes to the user story affect changes to the code?	

 Our components are very inflexible. They cannot say hello to other mentors, and they can only say "hello", not "hi" or "greetings". If our user stories change, for example if we wanted to say hello to a different mentor, we would have to to change the code too. This is easy in our tiny application but for "real" applications this might be more difficult.	

 Instead wouldn't it be good if we could change which mentor we are saying hello to every time we render the component? This is what "props" are for.	

 ## What Are Props?	

 Props are what we use in React to pass "arguments" to components. They are very similar to arguments in functions - you can "pass" props to components, and you can use those props in a component.	

 First let's look at passing props to your components ([interactive example](https://stackblitz.com/edit/react-ketrwi?file=index.js)):	

 ```js	
<Mentor mentor="Kash" />	
```	

 As you can see props are key-value pairs, in this example the key is `mentor` and the value is the string `'Kash'`. We don't have to use strings, we can use any valid JavaScript data like numbers, arrays and objects. Remember that in JSX you can use curly braces (`{` & `}`) to inject data that is not a string:	

 ```js	
<HotelRoom price={123}>	
```	

 Now let's take a look at using props that we have passed to a component ([interactive example](https://stackblitz.com/edit/react-ketrwi?file=Mentor.js)):	

 ```js	
<span>{this.props.mentor}</span>	
```	

 React gives you access to props via the `this.props` object. We can then inject into our component using curly braces. Because `this.props` is just a regular object, you can also inject into DOM attributes:	

 ```js	
<div id={'my-id-' + this.props.id}>{this.props.content}</div>	
```	

 > **Exercise:**	
> Open the `my-hotel` React application that your created last week	
> 1. Edit the `Logo` component so that the hotel name in the welcome message is passed as a prop	
> 2. Edit the `SpecialDeals` component so that the array is passed as a prop

## Reacting to Changes

Now let's write a more interesting app that responds to some user input. We'll see how React will take care of updating the DOM for you.

A counter is a common React example, showing the number of times a button has been clicked. First lets render a button and a counter which set to 0 clicks ([interactive example](https://stackblitz.com/edit/react-bb5vjg)):

```js
let count = 0

class Counter extends React.Component {
    render() {
        return (
            <div>
                Count: {this.props.count}
                <button id="click-me">Click me!</button>
            </div>
        )
    }
}
function renderCounter() {
    ReactDOM.render(<Counter count={count} />, document.getElementById('root'))
}

renderCounter(count)
```

Note that this example is simplified compared to your `my-hotel` application, because some parts are split into separate files to keep the code clean. You'll find the `ReactDOM.render` call in `index.js`

This example isn't very useful yet as it doesn't do anything when clicking the button. Now let's listen for clicks on the button and increment the counter ([interactive version](https://stackblitz.com/edit/react-tghfje)):

```js
let count = 0

class Counter extends React.Component {
    // ...
}
function renderCounter(count) {
    // ...
}

renderCounter(count)

document.getElementById('click-me').addEventListener('click', () => {
    count = count + 1
    renderCounter(count)
})
```

As you can see, the DOM automatically updates when you render. This is an incredibly powerful feature of React. Even better, React will figure out exactly the right bits of the DOM that need to be changed. This makes it extremely efficient and fast. This is concept is called the ["virtual DOM"](https://reactjs.org/docs/faq-internals.html).

## State

Let's take another look at the the counter example. A new user story has been created to show multiple counters. How would you add another counter?

You could add some more `count` global variables:

```js
let count1 = 0
let count2 = 0
let count3 = 0
```

What might be the problem here?

- It's quite verbose
- It's hard to make sure that you're updating the correct counter
- It's stuck at 3 counters - to add more, a new user story would have to be created

What other approaches can we take?

The solution that React provides for us is called "state". It allows a component to "remember" some variables. Let's take a look at how we could rewrite the counter with React state.

First we'll get rid of the global variables. **Generally having global variables is a bad idea**, since it is very easy to create a bug which affects the whole application. We can also get rid of the `renderCounter` function and just call `ReactDOM.render` directly:

```js
ReactDOM.render(<Counter count={0} />, document.getElementById('root'))
```

Next we'll change the component to use the count from `this.state` instead of `this.props`:

```js
class Counter extends Component {
    render() {
        return (
            <div>
                Count: {this.state.count}
                <button id="click-me">Click me!</button>
            </div>
        )
    }
}
```

This code has a bug! `this.state` is initialised as an empty object, and so `this.state.count` is undefined. We need to initialise it from props. We can do this in the class constructor:

```js
class Counter extends Component {
    constructor(props) {
        this.state = {
            count: props.count
        }
    }

    render() {
        // ...
    }
}
```

This is a common pattern in React. Props often act like "initial configuration" for a component which are copied to state. If state doesn't need to be configured through props, you can set it's initial value here too.

Now the counter component is "remembering" that it's count, however it is stuck at 0. Next we'll look at how we change what the component is remembering ([interactive example](https://stackblitz.com/edit/react-znvcmk)):

```js
class Counter extends Component {
    constructor(props) {
        // ...
    }

    increment = () => {
        let currentCount = this.state.count
        this.setState({
            count: ++currentCount
        })
    }

    render() {
        return (
            <div>
                Count: {this.state.count}
                <button onClick={this.increment}>Click me!</button>
            </div>
        )
    }
}
```

There's a couple of things happening here. We've added an click handler to the button, which will call the `increment` function when the button gets clicked. When the `increment` function is called, it gets the current value of the count from `this.state`. Then it calls `this.setState` function with an incremented count.

`this.setState` is a special function provided by React, and it is used to change what the component is "remembering". It will also tell React that the old value that is still shown in the DOM is outdated and needs to be updated. This will trigger React to re-render, like we did manually with the `renderCounter` function.

Now that we have refactored to use React state, we can easily add multiple counters ([interactive example](https://stackblitz.com/edit/react-678rgd)):

```js
class App extends Component {
    render() {
        return (
            <div>
                <Counter count={0} />
                <Counter count={0} />
                <Counter count={0} />
            </div>
        )
    }
}
```

> **Exercise:**
> Open the `my-hotel` React application that your created last week
> 1. Set the initial state of the `BookingsMessage` component to have 0 bookings
> 2. Show the number of bookings from state in `BookingsMessage`
> 3. Add an "Add Booking" button to the `BookingsMessage` component
> 4. Create an `addBooking` function on the `BookingsMessage` component
> 5. Add a click handler to the button which calls the `addBooking` function
> 6. Use `this.setState` to increment the number of bookings in state

## Functional Components	

 So far we have been using the `class` keyword to create React components. There is another way of creating components that is shorter, which are called "functional" components:	

 ```js	
function Greeting(props) {	
    return (	
        <div>Hello {props.name}</div>	
    )	
}	
```	

 Because it is just a function we can make this even shorter:	

 ```js	
const Greeting = (props) => <div>Hello {props.name}</div>	
```	

 If we use some destructuring, we can make it shorter again!	

 ```js	
const Greeting = ({ name }) => <div>Hello {name}</div>	
```	

 So why don't we always use functional components? Because they can only return JSX (and inject props if there are some). Additionally they cannot hold state or have lifecycle methods (which we'll look at next week).	

 In real world applications, the things we want to remember in state follow the "business logic" required by our users. So for example the number of bookings in the exercise above increases when you add a booking. To help us cleanly split up code that performs business logic from code that shows the user interface we split components into "presentational" and "connected" or "connected" components. Often I have components that don't do anything except manage state according to the business rules and render the right "presentational" components.	

 "Connected" or "connected" components usually have some state and handler methods. Because of this they must use the `class` syntax that we have been using so far. "Presentational" components on the other hand don't require the more verbose syntax. Instead they can use the functional syntax.	

 > **Exercise:**	
> Open the `my-hotel` React application once again	
> 1. Look at the components we have created so far, and decide which should be converted to functional ("presentational") components	
> 2. Convert these components to functional components	
 ## Passing Functions as Props	

 Usually we want to change the application state when users interact with our "presentational" components. But as discussed above, we don't want our presentational components to have state, so how do we change state from a presentational component?	

 Remember that functions in JavaScript are "first class" - that means we can pass a function as a variable and call it elsewhere. This includes React props ([interactive example](https://stackblitz.com/edit/react-bjljxh)):	

 ```js	
class Counter extends Component {	
    constructor(props) {	
        super(props)	
        this.state = { count: 0 }	
    }	
     increment = () => {	
        this.setState({ count: ++this.state.count })	
    }	
     render() {	
        return (	
            <div>	
                {this.state.count}	
                <FancyButton whenClicked={this.increment} />	
            </div>	
        )	
    }	
}	
 const FancyButton = ({ whenClicked }) => {	
    return (	
        <button	
            className="fancy-button"	
            onClick={whenClicked}	
        >	
            Click Me!	
        </button>	
    )	
}	
```	

 What is happening here?	

 - The `Counter` component initialises state and an `increment` method	
- Then the `Counter` component passes the `increment` function as a prop to `FancyButton`	
- Next the `whenClicked` prop (which is the `increment` function) is attached as a click handler in `FancyButton`	
- When the button is clicked, React calls the click handler attached via `onClick`. Because we passed the `increment` function as the `whenClicked` prop, the `increment` function will be called	
- The state in `Counter` will be set to an incremented value	

 This pattern is extremely useful in separating business logic code from user interface code. It is also crucial to the concept of [Lifting State Up](https://reactjs.org/docs/lifting-state-up.html).	

# Homework

{% include "./homework.md" %}
