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
