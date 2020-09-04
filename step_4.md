# Step 3: States

One of React's most prominent features is the ability for components to remember *states*. A state is simply a variable that a certain component will *remember*. Let's take a look at an example.

```
function Button() {
  /*
   * the syntax for initializing a state
   *
   * useState(param) returns two items in a list: the first
   * is the initial value of the state (param), and the second
   * is a function to update the state.
   *
   */
  const [isClicked, updateClicked] = useState(false);

  //we can define helper methods in components
  function handleClick() {
    updateClicked(true);
  }
  
  if (isClicked) {
    return <button>The button was clicked!</button>
  } else {
    return <button onClick={() => handleClick()}>Hello</button>
  }
}
```

There's a lot going on here, so let's dig into it.

First, the `isClicked` state will be initialized to `false` so the component will return the second option, where the button reads "Hello".

We added a HTML onClick listener to this button, so when it's clicked, we call the local function `handleClick()`. This function updates the state `isClicked` to false.

Now the magic of React happens - the entire component will *re-render*. This means that the entire `Button` component will execute again, this time with a different value of isClicked. During this second execution, the first condition of the `if-statement` will be true, causing the `Button` to return "The button was clicked!"

Let's rewind that again.
<hr>

### Stage 1
- isClicked is false
- if-condition evalutates to false
- component returns button that says "Hello"

### Stage 2
- User clicks on button, triggering `handleClick` function to execute.
- `handleClick` updates the `isClicked` state to false.

### Stage 3
- When a state of a React component is updated, the entire component must re-render. In other words, the `Button()` function will run again, possibly producing a different `return` value.
- Upon re-execution, the if-condition evaluates to true
- The component returns a button that says "The button was clicked"
