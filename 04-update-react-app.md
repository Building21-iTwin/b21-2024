# Update learn-react app

## Variables

Variables hold information, someones name, their age, a list of cities they have visisted.

This variable holds a name:

```js
const myName = "Colin" 
```

Add this variable to your App.js file about the return and modify 'Hello World' to say 'Hello Colin'.

```js
const myName = "Colin"

function App() {
  return (
    <div className="App">
      <h1>Hello {myName}</h1>
```

### Arrays

An array is a list of values, just like a grocery list.

```js
const list = ["Hello", "how", "are", "you", "doing?"];
```

Add this list after your name:

```js
      <h1>Hello {myName}. {list}</h1>
```

Notice that there are no spaces, how might y0u add spaces.

> HINT: try the 'join' method.

### Generate components from arrays

We can generate one component from each entry in an array.  For example adding a large number of images.

Before we begin find several additional pictures and add them to the 'public' folder.

Create a new variable to hold the URLs of the images, start with the image from last week then add all the new images.

```js
const imageUrls = ["./cat.jpg"]

```

Use the `map` command to generate the img tags:

```js
const images = imageUrls.map (url => <img src={url} />)
```

Then add the generated `images` variable so it's rendered.

> HINT: replace the existing `<img>` tag.


## State Variables

Some variables are changed when you interact with the application, these variables are called 'state'.

This variable holds a number and can be changed by calling the 'setCount' function.

```js
const [count, setCount] = useState(0)
```

> NOTE: this code requires that you import 'useState' from react.  Add the following code to the top of the file:

```js
import { useState } from 'react'
```

```js
function MyComponent () {
  const [count, setCount] = useState(0);

  function incrementCount() {
    let newCount = count + 1;
    setCount(newCount)
  }

  return (
    <div>
      <button onClick={incrementCount}>Count is {count}</button>
    </div>
  )
}
```