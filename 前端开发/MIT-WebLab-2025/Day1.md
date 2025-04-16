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
<html> <!--(Opening tag)-->
    <head>
        <title>Title!</title>
    </head>
    <body>
        <h1>Heading!</h1>
        <p>Paragraph!</p>
    </body>
</html> <!--(Closing tag)-->
```

Some Basic HTML Tags:

|Tag|Purpose|
|---|---|
| `<html>` |Root|
|`<head>`|Info about Document|
|`<body>`|Body|
|`<h1>`, `<h2>`, `<h3>`...| Header tags|
|`<p>` | Paragraph tag|
|`<div>`| Generic block section tag|
|`<span>`| Generic inline section tag|

### HTML Attributes:

`<tagname abc="xyz">`

* Insert a link:

```html
<a href="some_url_link">The text you want to show here</a>
```

* Insert an image:
```html
<img src="src_of_img"/>`
```
- Not that this is a self-closing tag!
- So we don't need to add `</img>` at the end!
```html
<!-- Alt: when the image failed to display, the text will be shown-->
<img src="img/someimg.gif" alt="This is a gif"/>
```

### Lists

|Tag|List|
|---|---|
|`<ol>`| Ordered List|
|`<ul>`|Unordered List|
|`<li>`| List Item|

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
    <p>Paragraph!<p>
</div>

<div id="div-1">
    <h2>Div 1!</h2>
    <p>Paragraph!<p>
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

### Use `class`:

```html
<h1>Heading</h1>
<div>Paragraph</div>
<div class="info"> Info </div> <!-- Notice that we add a class here-->
```
```css
.info {
    color: red;
}
```
This will only change the style of `class="info"`, not all `div`.

#### ID vs Class:
* An element can only have 1 ID, but it can have multiple classes.

