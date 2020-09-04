# Step 1: Components

The first thing we need to understand is that React is based on components. Components represent a part of a website, like a button, a form, a paragraph, etc. To make a full website, we simply nest individual components. A sample website might look like:

```
- LoginComponent
  - EmailFormComponent
    - EmailInput
    - PasswordInput
  - SubmitButtonComponent
```

At the end, we simply return a `LoginComponent` and our entire page renders!

Let's take a look at what a component looks like.