# Mandatory Setup: Git, Bash, vscode

(Install Git, VSCode, NodeJS)

(Create MongoDB account)

# Introduction to Course

Week1: build an app from scratch

Week2: Add cool features

Week3: Code (Competition)

Week4 Submit competition, judging, awards

## Introduction to website

### Accessing a website:

Client: Reguest GET url

Server: Response webpage files

(Files: html, css, JS, Assets)

### What we will make:

Dynamic website supported by a back-end;

Personalized experience based on user accounts;

Minimum Security requirements fulfilled;

## Milestones

0. Ideation (Day3)
1. Project Pitches (Day6)
2. Minimum Viable Product
3. Final Webite!

# Git Basics

## Staging & Commiting

After `git add woof.py`: the changes in `woof.py` are stored in staging area.

`git commit -m <message>`: the changes are moved from staging area to commit history.

## Branches: Work on multiple features at the same time

`git branch`: see branches

`git checkout [branch-name]`: switch to branch

`git checkout -b [branch-name]`: create and checkout branch

# HTML/CSS Intro

## HTML:

(Hypertext Markup Language)

Main Idea: HTML = Nested Boxes

### HTML Tags

Example: hello.html

```html
<!DOCTYPE html>
<html>
  <!--(Opening tag)-->
  <head>
    <title>Title!</title>
  </head>
  <body>
    <h1>Heading!</h1>
    <p>Paragraph!</p>
  </body>
</html>
<!--(Closing tag)-->
```

Some Basic HTML Tags:

| Tag                       | Purpose                    |
| ------------------------- | -------------------------- |
| `<html>`                  | Root                       |
| `<head>`                  | Info about Document        |
| `<body>`                  | Body                       |
| `<h1>`, `<h2>`, `<h3>`... | Header tags                |
| `<p>`                     | Paragraph tag              |
| `<div>`                   | Generic block section tag  |
| `<span>`                  | Generic inline section tag |

### HTML Attributes:

`<tagname abc="xyz">`

- Insert a link:

```html
<a href="some_url_link">The text you want to show here</a>
```

- Insert an image:

```html
<img src="src_of_img" />`
```

- Not that this is a self-closing tag!
- So we don't need to add `</img>` at the end!

```html
<!-- Alt: when the image failed to display, the text will be shown-->
<img src="img/someimg.gif" alt="This is a gif" />
```

### Lists

| Tag    | List           |
| ------ | -------------- |
| `<ol>` | Ordered List   |
| `<ul>` | Unordered List |
| `<li>` | List Item      |

Example:

```html
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

### div & span

Difference:

`<div>`: Group a block section

`<span>`: Group an inline section

```html
<div id="div-0">
  <h2>Div 0!</h2>
  <p>Paragraph!</p>
  <p></p>
</div>

<div id="div-1">
  <h2>Div 1!</h2>
  <p>Paragraph!</p>
  <p></p>
</div>

<span id="span-0"> This text is inside a span. </span>
<span id="span-1"> This text is inside another span. </span>
```

### Useful Resources

<a href="https://developer.mozilla.org/en-US/docs/Web/HTML">MDN Web Docs</a>

### Semantic Elements

`<div>` is bad, because it's not very readable and has no meaning

## CSS:

(Cascading Style Sheets)

### Rule

selector + property + value

```css
div {
  color: red;
  font-family: Arial;
  font-size: 24pt;
}
```

- Note that tags like `<h1>` have some default style, but any customed css will overwrite them. (`h1 {...})

### Use `class`:

```html
<h1>Heading</h1>
<div>Paragraph</div>
<div class="info">Info</div>
<!-- Notice that we add a class here-->
```

```css
.info {
  color: red;
}
```

This will only change the style of `class="info"`, not all `div`.

#### ID vs Class:

- An element can only have 1 ID, but it can have multiple classes.
- Different elements can't have the same ID. (1-to-1 relationship)

## Combining HTML and CSS:

example:

```html
<head>
  <title>Title</title>
  <!-- link is differnt from a. Don't use it to create a hyperlink!-->
  <link rel="stylesheet" href="style.css" />
  <!--rel stands for relationship-->
</head>
```

# JavaScript

## How to JavaScript

### Types:

#### The 5 primitive data types:

- Boolean
- Number
- String
- Null
- Undefined

#### Operators:

Arithmetic: +, -, \*, /, \*\*

Comparison: `===`, !==, <, >, <=, >=

`===` vs `==`:
|expression|boolean|
|---|---|
|`2 == 2`| True|
|`2=="2"`| True!!!|
|`2===2`| True|
|`2==="2"`| False!

### Basic Syntax:

Example:

```js
// This is a greatest common divisor function.
const GCD = (a, b) => {
  // This is a strange way to write a function... We use "=" and "=>"
  while (b != 0) {
    const temp = b; // Every sentence ends with ";"
    b = a % b;
    a = temp;
  }
  return a;
};

// Define variables
const x = 50; // This is a constant
const y = 15;
const gcd = GCD(x, y);
let myNumber = 42; // We define a not-constant var
let myString = "haha";
myNumber = 55; // This var's value can be changed later
```

#### null vs. undefined:

```js
let firstName; // Now this var is undefined.
firstName = "Albert"; // Now it's either undefined or null.
firstName = null; // Now it's null.
```

### Output:

#### log:

`console.log()`: writes to the JavaScript console.

(use it for debugging)

Use template strings for logging:

```js
const a = 5;
const b = 10;
console.log(`a * b = ${a * b}`);
```

#### Alerts

Pops up a notification.

```js
alert("Congratulations!");
```

### Flows

#### if else

```js
if (hour < 12) {
  console.log("Good morning");
} else if (hour < 16) {
  console.log("Good afternoon!");
} else {
  console.log("Good night!");
}
```

#### loops

```js
// while loop
let z = 1;
while (z < 1000) {
  z *= 2;
  console.log(z);
}

// for loop
const pets = ["cat", "dog", "pig", "bird", "fish", "rabbit", "sheep"];
for (let i = 0; i < pets.length; i++) {
  const phrase = "I love my " + pets[i];
  console.log(phrase);
}
// for ... of ...
for (const animal of pets) {
  const phrase = "I love my " + pets[i];
  console.log(phrase);
}
```

## OOP:

### Arrays:

Example:

```js
let pets = ["string", 42, false]; // it can contain items of different types.
console.lot(pets[0]); // Index is begin from 0
pets[2] = "bird"; // Modify the array
pets.pop(); // remove from end
pets.push("rabbit"); // add to end
```

### Objects:

example:

```js
// Define an object
const myCar = {
  make: "Ford",
  model: "Musang",
  year: 2025,
  color: "sapphire",
};

// Access properties
console.log(myCar.model);
console.log(marCar["color"]);
```

Object destructuring:

Obtain multiple properties at once. For example:

```js
// don't use object destructuring
const make = myCar.make;
const model = myCar.make;
// use object destructuring
const { make, model } = myCar;
```

### Equality

Object variables are references. They point to where the data is actually stored. (Arrays are the same)

#### To copy them:

use the spread operator `...`:

```js
let arr = [1, 2, 3];
let copyArr = [...arr];

let obj = { name: "Bill Gates" };
let copyObj = { ...obj };
```

## Functions:

```js
// Declare a function is just like declaring a variable!
const cToF = (tempC) => {
  const tempF = (tempC * 9) / 5 + 32;
  return tempF;
}; // Thus, we need to put a ";" at the end!
```

Callback Functions:

Those functions who take another function(s) as their parameters.

For example:

```js
setTimeout(() => {
  console.log("I print");
}, 5000);

setInterval(() => {
  console.log("I repeatedly pring");
}, 5000);
```

## Classes:

example:

```js
// Declare a class
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }
  getArea = () => {
    return this.width * this.height;
  };
}
// Create an new object of that class
const rect = new Rectangle(6, 8);
console.log(rect.getArea());
```
