# Learning React Notes

Author Info
-----------
Author: Andrew Gurung <br>
URL: http://www.andrewgurung.com/

Context
-----------------
## Learning React - Kirupa Chinnathambi <br/>
- Kirupa Chinnathambi

Notes
-----
## Introducing React

### Old School VS New School
- OLD: Multiple individual pages where each page get torn down and redrawn
- New: Single-Page Apps(SPA) where different views of an app are loaded and unloaded into the same pages

### Major issues with SPA
- Extra effort trying to keep data in sync with UI
- Manipulating DOM is really slow
- Working with HTML templates can be a pain

### React
- Facebook create a library called `React` based on their experience with single-page apps

### Benefits of using React
1. Automatic UI State Management
  - React takes care of all state management stuff
  - All you need to worry is: the final state of your UI

2. Lightning-fast DOM Manipulation
  - Since DOM modifications are really slow, React came up with an extremely fast virtual DOM
  - Does the least amount of DOM manipulation to update the UI

3. APIs to Create Truly Composable UIs
  - React core APIs make it easier to create smaller, self contained visual components

4. Visuals Defined Entirely in JavaScript
  - Combines HTML templating with Javascript in a same file
  - HTML-like syntax --`JSX` makes things even easier

5. Just the V in an MVC architecture

------------------------------------

# Building Your First React App

### Dealing with JSX
- JSX is a language that allows us to mix Javascript with HTML-like tags
- But a browser only understands plain HTML, CSS and Javascript

### Solutions to convert JSX into plain old Javascript
1. Use build tools in Node that converts JSX on every build. Preferred solution
2. Let browser rely on Javascript library to automatically convert JSX. Quick dirty way which takes a performance hit each time browser spends time translating JSX to JS

### Getting Your React On
[Codepen.io Practice link](https://codepen.io/andrewgurung/pen/wqwQVr)

#### Using Solution #2 -- letting browser handle JSX conversion
- Start with blank HTML page
- Add core React libraries (React + ReactDOM) -- add after `title` tag
```
<script src="https://unpkg.com/react@15.3.2/dist/react.js"></script>
<script src="https://unpkg.com/react-dom@15.3.2/dist/react-dom.js"></script>
```
- Add Babel JS compiler -- convert JSX into JS
```
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.
js"></script>
```

#### Empty skeleton
```
<html>
<head>
  <title>React! React! React!</title>
  <script src="https://unpkg.com/react@15.3.2/dist/react.js"></script>
  <script src="https://unpkg.com/react-dom@15.3.2/dist/react-dom.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-core/5.8.23/browser.min.js"></script>
</head>
<body>
  <script>
  </script>
</body>
</html>
```

### Display Name
- ReactDOM.render(displayBody, element)
- displayBody: HTML body that you want to render
- element: Where to render?
- Babel compilation: Add `type="text/babel"` attribute to script tag for Babel to do its magic
- Run your first React App



------------------------------------

# Components in React

------------------------------------

# Styling in React

------------------------------------

# Creating Complex Components

------------------------------------

# Transferring Properties (Props)

------------------------------------

# Meet JSX

------------------------------------

# Dealing with State

------------------------------------

# Going from Data to UI

------------------------------------

# Working with Events

------------------------------------

# The Component Lifecycle

------------------------------------

# Accessing DOM Elements

------------------------------------

# Creating a Single-Page App Using React Router

------------------------------------

# Building a Todo List App

------------------------------------

# Setting Up Your React Development Environment

----------------------------
