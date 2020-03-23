# React 1

![](https://img.shields.io/badge/status-draft-darkred.svg)

**What will we learn today?**

- [What is React?](#what-is-react)
- [What is a component?](#what-is-a-component)
- [Rendering with React](#rendering-with-react)
- [JSX](#jsx)
- [Let's Create a React App](#lets-create-a-react-app)
- [React Components](#react-components)
- [Embedding JS into JSX](#embedding-js-into-jsx)
- [Importing/Exporting Components](#importingexporting-components)

## What is React?

React is a JavaScript library created by Facebook. It is used for making complex, interactive user interfaces. It has become very popular in the last 5 years.

Why has it become so popular?

- It is fast and efficient
- It is easy to understand & less verbose than "vanilla" JS api
- It helps separate functionality into small, understandable pieces

## What is a component?

React heavily relies on a concept called "components". Components are like small Lego blocks for designing and developing user interfaces. They can be stuck together in different ways to create new UI.

Let's have a look at an example: the GitHub header. What are logical "pieces" of UI? What could be a component?

![GitHub header](../assets/components.png)

Here we've highlighted some elements that could be components:

![GitHub header with components highlighted](../assets/components-highlighted.png)

### Component tips

There are no hard & fast rules for making components. UIs can be split up into components in many different ways, requiring judgement based on your context.

- Components should follow the Single Responsibility Principle
    + Each component should only have 1 "responsibility"
    + Should only do 1 thing
- Components should have good, explicit names
    + This helps you to remember what the component's job is

> **Exercise**:
> Look at the example online shopping user interface in the [Thinking in React article](https://reactjs.org/docs/thinking-in-react.html) (the image at the top). Draw boxes around the components and give them names. Compare with the example components shown in the second image.

## Rendering with React

Remember how annoying it was to manage the DOM yourself in [week 8](https://codeyourfuture.github.io/syllabus-master/js-core-2/week-08/lesson.html)? The "vanilla" JavaScript apis for updating the DOM are quite long and difficult to remember. React makes this easier by instead of manipulating each DOM element itself. You give React a "description" of the DOM that you want and it will  update the DOM for you. React "abstracts" away the management of the DOM.

Let's take a look at an example. We are going to walk through how to render a `<div>` with the text "Hello World" within it.

First, lets recap how we could do this using "vanilla" JS ([interactive version](http://jsbin.com/motorexehu/edit?html,output)):

```html
<!DOCTYPE html>
<html>
<body>
<div id="root"></div>

<script type="text/javascript">
    var divNode = document.createElement('div');
    var textNode = document.createTextNode('Hello World');
    divNode.appendChild(textNode);

    var rootElement = document.getElementById('root');
    rootElement.appendChild(divNode);
</script>
</body>
</html>
```

Now let's convert to using React ([interactive version](http://jsbin.com/recegadexu/edit?html,output)):

```html
<!DOCTYPE html>
<html>
<body>
<!-- Load React & ReactDOM scripts -->
<!-- Don't worry about how we're doing this yet! -->
<script src="https://unpkg.com/react@16.0.0/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16.0.0/umd/react-dom.development.js"></script>

<!-- Root element -->
<div id="root"></div>

<script type="text/javascript">
    const element = React.createElement('div', {
        children: 'Hello World'
    })

    const rootElement = document.getElementById('root')
    ReactDOM.render(element, rootElement)
</script>
</body>
</html>
```

## JSX

JSX is a simple syntax "sugar" that *looks* like HTML. It improves the developer experience writing react as it is actually converted to the `React.createElement` function when you run it.

Using JSX ([interactive version](http://jsbin.com/gekahexige/edit?html,output)):

## Let's Create A React App

The Facebook team behind React have created a tool to help you create and set up React projects. It is called [Create React App](https://github.com/facebook/create-react-app). We will use it for the rest of the module.

> **Exercise**: Install & set up a Create React App by following the steps below

```
npm install -g create-react-app

create-react-app my-hotel
cd my-hotel/
npm start
```

Notice that create-react-app has created a bunch of folders for you in the `my-hotel` directory.

## React Components

We looked at the beginning of the lesson at the concept of components. Now let's look at how components are made in React.

```js
import React from 'react'
import ReactDOM from 'react-dom'

class HelloWorld extends React.Component {
    render() {
        return <div>Hello World</div>
    }
}

ReactDOM.render(<HelloWorld />, document.getElementById('root'))
```

Components get more powerful when you combine (or "compose") several components together ([interactive example](https://stackblitz.com/edit/react-nxhe2q)):

```js
class Greeting extends React.Component {
    render() {
        return <span>Hello</span>
    }
}
class Mentor extends React.Component {
    render() {
        return <span>Ali</span>
    }
}

class HelloWorld extends React.Component {
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

Notice how the components that we write (`HelloWorld`, `Greeting`, `Mentor`) are `camelCased` and always start with an uppercase letter? And "regular DOM" components (`div`, `span`) are always lowercase? This the convention to let you know whether you are using a "regular DOM component" or something that you have written.

## Embedding JS into JSX

Like Handlebars, you can insert variables (and some other things) into React components. Anything that is inside curly braces (`{` and `}`) is interpreted as a regular JavaScript "expression". That means you can use every object or function from JavaScript that we have learned so far. Let's look at an example ([interactive example](https://stackblitz.com/edit/react-byupse)):

```js
class Mentor extends React.Component {
    render() {
        const mentors = ['Ali', 'Kash', 'Davide', 'German', 'Gerald']
        return <span>{mentors.join(', ')}</span>
    }
}
```

Now we have modified the `Mentor` component to use the `Array.join` method so that it lists several mentor's names. This also works with other JS types:

```js
<span>{1 + 2 + 3}</span>
```

```js
const weather = {
    temperature: 5,
    location: 'London'
}
<p>The temperature in {weather.location} is {weather.temperature}</p>
```

```js
function formatName(user) {
    return user.firstName + ' ' + user.lastName
}
<span>{formatName(user)}</span>
```

A common pattern in React is to use `Array.map` to loop through a list of items and render a component for each one ([interactive example](https://stackblitz.com/edit/react-z51fpz)):

```js
const mentors = ['Ali', 'Kash', 'Davide', 'German', 'Gerald']

class Item extends Component {
  render() {
    return (
      <li>{this.props.name}</li>
    )
  }
}

class List extends Component {
  render() {
    return (
      <ul>
        {this.props.items.map((item) => (
          <Item name={item}/>
        ))}
      </ul>
    );
  }
}
```

Here we are using `Array.map` to turn an array of strings into an array of components. We are using a "real" map function, not just special syntax like `{{> each}}` from Handlebars.

An ([interactive example](https://stackblitz.com/edit/react-cwryrk)) of separating the 2 components in the example above in 2 files.

> **Exercise**:
> Using the `my-hotel` React app that you created earlier, edit `src/App.js` to create a hotel welcome page.
> 1. Change the title to say "Welcome to CYF Hotel" and change the `img` to have `src="https://codeyourfuture.io/static/media/cyf_brand.fbcea877.png"`
> 2. Copy the content of the `header` to a new component called `Logo`
> 3. Replace the `header` with a usage of the new `Logo` component
> 4. Replace the `p` with a message saying that there are bookings available for today's date (hint `new Date().toLocaleDateString()`)
> 5. Extract the `p` to a component named `BookingsMessage`
> 6. Create a new component `SpecialDeals` and render an empty `div`
> 7. Within the `SpecialDeals` components, use an array containing some special deal strings and render each one as a `<p>` within the `div`

## Importing/Exporting Components

To help organise your code, components can be imported and exported just like any other JavaScript code ([interactive example](https://stackblitz.com/edit/react-jnkuqk)):

```js
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

> **Exercise**:
> Using the `my-hotel` app, edit `src/App.js` to extract the `Logo`, `BookingsMessage` and `SpecialDeals` components to new files `src/Logo.js` and `src/SpecialDeals.js`
> Hint: you will need to import React

#### Credits

Inspiration & examples for this module were taken from [Kent C. Dodd's](https://twitter.com/kentcdodds) [Beginner's Guide to ReactJS](https://egghead.io/courses/the-beginner-s-guide-to-reactjs) course on Egghead.io. It's a free course, so check it out :)

# Homework

{% include "./homework.md" %}
