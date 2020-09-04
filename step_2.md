# Step 2: Components

Here's a simple way to think of a React component: *it is simply a JavaScript function that returns HTML.**

Let's take a look at a sample Button component.

```
function Button() {
  return <button class="fancy-button">submit</button>;
}
```

Now, let's say we want to nest this component inside a form. This could look like:
```
function Form() {
  return (
    <form>
      <input type="email" />
      <input type="password" />

      {/* This calls the previously defined Button component */}
      <Button /> 
    </form>
  );
}
```

As you can see, an individual React component simply returns HTML elements as we are used to. However, this can become very powerful once we start nesting and reusing components across an entire website.

Notice that while any HTML code could theoretically be it's own React component, it's typically best to make React components that are re-used multiple times across a website.


