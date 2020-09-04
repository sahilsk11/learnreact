# Step 4: States vs. Variables

There are two key differences between states and variables:

1. When a state is updated, the entire React component will re-render. Updating a local variable does not cause a component to re-render.
2. The value of React states is remembered across *lifecycles* (every time the component re-renders). Local variables will be re-initialized every time the component renders.

Let's take a look at two examples to see the difference.

<hr>

## States Cause Re-renders. Local vars don't.

This is the exact same code as step_3, except we've replaced the state with a local variable.

```
function Button() {
  var isClicked = false;

  function handleClick() {
    isClicked = true;
  }
  
  if (isClicked) {
    return <button>The button was clicked!</button>
  } else {
    return <button onClick={() => handleClick()}>Hello</button>
  }
}
```

Just as we did before, let's take a look at this component across stages:

### Stage 1
- isClicked is false
- if-condition evalutates to false
- component returns button that says "Hello"

### Stage 2
- User clicks on button, triggering `handleClick` function to execute.
- `handleClick` sets the `isClicked` value to false.

However, we terminate here. Updating a local variables *does not cause the React component to re-render*, whereas updating a state causes a re-render. So, despite clicking on the button and the `isClicked` value changing, our component will not re-execute to reflect the new value.

## State Values are Remembered Across Lifecycles

Every time a React component renders is called a *lifecycle*. React states are remembered across lifecycles, meaning when a component updates, the previous value of the state is remembered by the component. In contrast, local variables are overwritten each time. Let's use an example.

```
function Button() {
  const [isClicked, updateClicked] = useState(false); //use a hook here
  var numClicks = 0;

  function handleClick() {
    updateClicked(true);
    numClicks += 1;
  }
  
  if (isClicked) {
    return <button>The button was clicked {numClicks} times.</button>
  } else {
    return <button onClick={() => handleClick()}>Hello</button>
  }
}
```

As before, when we click on the "Hello" button that initially renders, the `isClicked` state will update and the component will re-render. However, we will also increment the value of `numClicks` in `handleClick()`.

Upon re-rendering, we will see a button that says "The button was clicked 0 times"

Why?

Well, upon the second execution, all of the code from `Button()` will be executed again. This includes the line:
```
var numClicks = 0;
```

which resets numClicks back to 0. If we wanted this value to be properly remembered across lifecycles, we would update it to use a state:

```
function Button() {
  const [isClicked, updateClicked] = useState(false); //use a hook here
  const [numClicks, updateNumClicks] = useState(false); //use a hook here

  function handleClick() {
    updateClicked(true);
    updateNumClicks(numClicks + 1);
  }
  
  if (isClicked) {
    return <button>The button was clicked {numClicks} times.</button>
  } else {
    return <button onClick={() => handleClick()}>Hello</button>
  }
}
```

<hr>

Note: technically, the reason `numClicks` as a `var` is not remembered across lifecycles is because the variable is local to the particular lifecycle of the component. The following render has no knowledge that `numClicks` existed in the previous lifecycle, so it does not know its value.

However, I find it easier to think of values as being "overwritten" - so I explain it this way.