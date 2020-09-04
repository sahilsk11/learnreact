# Step 3: Buidling our First React File

What makes React tricky for beginners is that React has a *ton* of dependencies and mannerisms in the way code must be structured. However, if someone else is able to manage the setup and configuration, React makes it fairly simple to focus on a very specific part of a codebase and ignore the rest of the codebase (in fact, that's my favorite part of React).

Airbnb's React styleguide  recommends that every React component should be in it's own file - for good reason - so let's build our first React file called `SubmitButton.jsx` that only contains a single button. To include styling, let's also include a `submitButton.css` in the same directory. Our file structure looks like this:

```
src/
  App.jsx     <---- the root of the project
  app.css
  RandomComponent/
  RandomComponent2/
  SubmitButton/
    SubmitButton.jsx
    submitButton.css
```

Other contributers can independently manage `RandomComponent`(s) while we focus on this button. Meanwhile, all of our components can tied together back in the "root" file, `App.jsx`. Think of this as the "main" component in which all of our code will end up. 

Let's start with this code in `ReactButton.jsx`.

```
import React from "react";

function SubmitButton() {
  return <button className="submit-button">submit</button>
}

// This line exports the component so it can be imported
// in another file
export default SubmitButton;

```

Admittedly, it's not very exciting, and we typically wouldn't make a component out of something so small (and probably not used a lot in the project), but this simple example works pretty well.

Now, in `submitButton.css`, let's add the following:

```
.submit-button {
  background-color: rgb(105, 200, 30);
  border: none;
  padding: 30px;
  width: 100px;
}
```

And that's it! We now have a completely independently managed button component with it's own code and CSS in one directory. Let's see how this pices together with the rest.
<hr>

Let's look at `App.jsx`:

```
import React from "react";

import RandomComponent from "./RandomComponent/RandomComponent.jsx";
import RandomComponent2 from "./RandomComponent2/RandomComponent2.jsx";

import SubmitButton from "./SubmitButton/SubmitButton.jsx";

function App() {
  return (
    <RandomComponent />
    <RandomComponent2 />

    <SubmitButton />
  )
}

export default App;
```

App will be injected directly into our HTML file to be served. Just like that, we've managed to piece together a simple website using React!

So far, you've covered enough to start contributing simple components to a web project. The next few modules will dig into advanced React techniques.