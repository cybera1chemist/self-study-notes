# JS: Callback and Arrays (Extra)

## An exercise of using callback

Write a callback function `modifyArray`:

```js
const modifyArray = (arr, func) => {
  let new_arr = [...arr];
  for (let i=0; i<arr.length; i++;) {
    new_arr[i] = func(new_arr[i]);
  }
  return new_arr;
};
```

## Shortened Notation of Functions

```js
// if the function's content only contains 1 line,
// then we can use no "{}",
// and content after "=>" is returned!!!
const CToF = (tempC) => (tempC * 9) / 5 + 32;
```

## map(...)

purpose: create a new array using an old array

grammar: `arr.map(someFunction);`

```js
const oldArr = [1, 2, 3, 4, 5];
const newArr = oldArr.map((i) => i * 3);

// An exercise:
const areas = rectangles.map((rec) => rec.width * rec.height);
```

## filter(...)

example:

```js
let values = [-1, -5, 0, 100, -100, 99, 555];
let postiveValues = values.filter((x) => x > 0);
```

## Callback Functions in Web Dev:

Some Examples:

`setInterval(func, t)`: When the timer of `t` goes off, call `func`

`addEventListener(keyboard_input, func)`: When keyboard_input is ..., call `func`

```js
Comment.find({ parent: req.query.parent }).then((comments) => {
  res.send(comments);
});

router.get("/comment", (req, res) => {
  Comment.find({ parent: req.query.parent }).then((comments) => {
    res.send(comments);
  });
});
```

# Intro to React!

## What is React?

React is a framework that lets us

- divide up websites into reusable components
- components are like "custome HTML tag"
- consider a tree hierarchy

## Components:

### Props:

Components are like skeletons, and we need to fill some information into them, thus we need props.

Props are informtion passed down from a parent to a child component.

(just like providing parameters to a function)

Tips:

1. Props are immutable.
2. Props can Not be passed from child to parent.

### State:

What is state?

- Just like memory of component. Can be updated (mutable).

An example:

- In facebook, a post can have many comments.
- Then, we can set `<Post/>` 's state contains an array of `<Comment/>` array.
- In `<Comment/>` 's Props, there are information about this comment. (such as author, content, like, reply, etc.)

Another example: implement "show hidden replys"

In `<Comment/>`: `showReplys` state. (false/true)

## Examples

### How to define a component:

```js
// First, we need to import React.
// Note that import dosen't end with ";"
import React, {useState} from 'react'

// Define the component
const CommentReply = (pros) => {
    return (
        // What you want to render
    )
}

// We need to export this file as a component
export default CommentReply
```

### How to use Props:

```js
import React, { useState } from "react";

const CommentReply = (pros) => {
  // "()" allows us to write JSX("HTML") inside JS
  return (
    <div className="comment-text">
      <h5>{props.name}</h5>
      <p>{props.content}</p>
    </div>
  );
  // "{}" allows us to use JS variables inside JSX
  // Note that JSX uses "className=...", instead of "class=..."
};

export default CommentReply;
```

### Add some states:

```js
import React, { useState } from "react";

const CommentReply = (pros) => {
  // Add some states
  const [isLiked, setIsLiked] = useState(false);

  return (
    <div className="comment-text">
      <h5>{props.name}</h5>
      <p>{props.content}</p>
      {/* Render the new state*/}
      <p>{isLiked ? "Liked" : "Like"}</p>
    </div>
  );
};

export default CommentReply;
```

## Add several components together:

Example: `App.js`

```js
// import react itself
import React from "react";
// import the components that we've written
import NavBar from "./NavBar";
import Intro from "./Intro";
import Photos from "./Photos";
import Post from "./Post";

const App = () => {
  //JSX
  return (
    <div>
      <NavBar />
      <div>
        {/* We can pass Props here*/}
        <Intro education="CUHKSZ" city="Shenzhen" />
        <Photos />
      </div>
      <Post name="C.A." />
    </div>
  );
};

// export App.js
export default App;
```
