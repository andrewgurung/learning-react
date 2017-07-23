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
- displayBody: HTML-like elements (aka JSX) that you want to output
- element: Where to render?
- Babel compilation: Add `type="text/babel"` attribute to script tag for Babel to do its magic
- Run your first React App

### Changing the Destination
- Move render element from `body` to `div`
```
<div id="container"></div>
<script type="text/babel">
  var destination = document.querySelector("#container");
  ReactDOM.render(
  <h1>Andrew Gurung</h1>,
  destination);
</script>
```

### Style up
- Add style using CSS
```
#container {
  background-color: #EEE;
}

#container h1{
  font-size: 48px;
  font-family: sans-serif;
  color: #0080A8;
}
```
------------------------------------

# Components in React
[Codepen.io Link](https://codepen.io/andrewgurung/pen/JyPxyO)
- React components are resuable chunks of Javascript that output HTML elements
- `function` helps to structure our app and reuse code
- Component is like `function` for the UI
- Note: JSX cannot have multiple adjacent elements so it must be wrapped by a single element. Eg: Wrap with `div`

### First React Component
[Codepen.io Link](https://codepen.io/andrewgurung/pen/JyPxyO)
- Components can be created using `React.createClass`
- Eg: `var HelloWorld = React.createClass({ ... })` where HelloWorld is a Component
- Every React Component requires a `render` property

Component:
```
var HelloWorld = React.createClass({
  render: function() {
    return (
      <p>Hello, componentized world!</p>
    )
  }
});
```

Using component:
```
ReactDOM.render(
  <HelloWorld/>,
  document.querySelector('#container')
);
```

### Passing argument to React Component
[Codepen.io Link](https://codepen.io/andrewgurung/pen/jLNdxW)
1. Updating Component Definition
- Use `this.props`
```
render: function() {
  return (
    <p>Hello, {this.props.greetTarget}!</p>
  )
}
```

2. Modifying component call
- Wrap in `div` and pass argument through JSX attributes
```
<div>
  <HelloWorld greetTarget="Batman"/>
  <HelloWorld greetTarget="Iron Man"/>
  <HelloWorld greetTarget="Jon Snow"/>
</div>
```

### Dealing with Children
[Codepen.io Link](https://codepen.io/andrewgurung/pen/jLNdpq)
- Parent element have the capability to access its children property
- Syntax: `this.props.children`
Component:
```
var Buttonify = React.createClass({
  render: function() {
    return (
      <div>
        <button type={this.props.behavior}>{this.props.children}</button>
      </div>
    )
  }
});
```

Calling Component:
```
ReactDOM.render(
  <div>
    <Buttonify behavior="Submit">Send Data</Buttonify>
  </div>,
  document.querySelector('#container')
);
```
------------------------------------

# Styling in React
[Codepen.io Link](https://codepen.io/andrewgurung/pen/NvKZLv)
- React favors components to be little black boxes where everything related to how the UI looks and works are stored

### Displaying some vowels
Component:
```
var Letter = React.createClass({
  render: function() {
    return (
      <div>
        {this.props.children}
      </div>
    );
  }
});
```

Calling component:
```
<Letter>A</Letter>
```

### Styling component using CSS
- Define CSS style with `.letter` class
- Add `className` attribute to `div` with value of `letter`
- WARNING: Attribute must be `className` not `class`. JSX is different

Update component:
```
...
<div className="letter">
 {this.props.children}
</div>
```

CSS:
```
.letter {
  padding: 10px;
  margin: 10px;
  ...
}
```

### Styling Content the React way
1. Create a Style Object
2. Assign the style object to JSX component

#### Creating a Style Object
- Define an object with all CSS properties
- Style object should be defined **inside** the component's `render` method
- The CSS properties inside of style object can take customizable values
- Values inside style object must be enclosed in quotes `"` or remove `px` for numbers. Eg: 32px --> 32 to avoid quotes
- WARNING: Single word CSS properties are unchanged. Multi-word CSS are turned into camelCase with dash removed. Eg: `background-color` --> `backgroundColor`
```
var Letter = React.createClass({
     render: function() {
         var letterStyle = {
           padding: 10,
           margin: 10,
           backgroundColor: "#ffde00",
           color: "#333",
          ...
         }
```

#### Assigning style object to JSX UI component
- Use `style` attribute instead of `className`
- Set the `style` attribute with style object surrounded by parenthesis `{ }`
```
<div style={letterStyle}>
 {this.props.children}
</div>
```

#### Making the background color customizable
- We can make style values easily customizable through the parent (aka the consumer of the component)

Style object:
```
var letterStyle = {
 ...
 backgroundColor: this.props.bgcolor,
 ...
}
```

Component (Parent aka consumer):
```
<Letter bgcolor="#58B3FF">A</Letter>
```

------------------------------------

# Creating Complex Components
- Combine components to compose more complex components
- All components do is return a chunk of HTML to whatever called it

## Steps
1. Identify the major visual elements into tree-like structure for better feel
2. Identify which visual elements will turn into a component and which ones will not. A component should do just one thing
3. Create components

### Creating component
[Codepen.io Link](https://codepen.io/andrewgurung/pen/BdBXqP)
- Create three components -- `Card`, `Label` and `Square`

#### Card component
- Container for both `Square` and `Label` components
- Create `cardStyle` style object inside render method of `Card` component and assign to `Card` component
```
```

#### Square Component
- Similar to Card component with a smaller height
- Create `squareStyle` style object and assign to `Square` component
- Compose: Add `Square` component inside the `Card` component

Square component:
```
var Square = React.createClass({
 render: function() {
   var squareStyle = {
     height: 150,
     backgroundColor: "#FF6663"
   }
   return (
     <div style={squareStyle}>
     </div>
```

```
/* Inside Card component */
var Card = React.createClass({
  render: function() {
    ...
    return (
      <div style={cardStyle}>
        <Square/>
      </div>
    );


ReactDOM.render(
    <div>
      <Card/>
    </div>,
    document.querySelector('#container')
  );
```

#### Label Component
- Create `labelStyle` style object and assign to `Label` component
- Compose: Add `Label` component inside the `Card` component

Label component:
```
return (
 <p style={labelStyle}>#FF6663</p>
);
```

Card component:
```
var Card = React.createClass({
  render: function() {
    ...
    return (
      <div style={cardStyle}>
        <Square/>
        <Label/>
      </div>
    );
```

### Passing Properties
- Remove the hard-color color value in `Square` and `Label` components
- In this example, we pass the color property from Parent `<Card>` component to its descendants through property chain
- Can be difficult if there are multiple properties to be passed across multilevels

1. Card component: Pass properties
```
var Card = React.createClass({
 render: function() {
   ...
   return (
     <div style={cardStyle}>
       <Square color={this.props.color}/>
       <Label color={this.props.color}/>
     </div>
   );
 }
});

ReactDOM.render(
  <div>
    <Card color="#FF6663"/>
  </div>,
  document.querySelector('#container')
);
```

2. Square component:
```
var Square = React.createClass({
   render: function() {
     var squareStyle = {
       height: 150,
       backgroundColor: this.props.color
     }
    ...
   }
 });
```

3. Label component:
```
var Label = React.createClass({
 render: function() {
   ...
   return (
     <p style={labelStyle}>{this.props.color}</p>
   );
 }
});
```
------------------------------------

# Transferring Properties (Props)
- Passing property across multiple layers of components is complicated
- React enforces a chain of command where properties have to flow from parent to immediate child
- IMPORTANT: Communication is `one-way` from parent to child
- Renaming or removing a property in one component will effect everyone in the chain

### Detailed Look at the Problem
[Codepen.io Link](https://codepen.io/andrewgurung/pen/zdYOmE)
- Shirt --> Label --> Display
- The properties travels all the way from `Shirt` to `Display` component through `props` object
```
var Display = React.createClass({
  render: function() {
    return (
      <div>
        <p>{this.props.color}</p>
        <p>{this.props.num}</p>
        <p>{this.props.size}</p>
      </div>
    );
  }
});

var Label = React.createClass({
  render: function() {
    return (
      <div>
        <Display
          color={this.props.color}
          num={this.props.num}
          size={this.props.size}
        />
      </div>
    );
  }
});

var Shirt = React.createClass({
  render: function() {
    return (
      <div>
        <Label
          color={this.props.color}
          num={this.props.num}
          size={this.props.size}
        />
      </div>
    );
  }
});

ReactDOM.render(
  <div>
    <Shirt color="steelblue" num="3.14" size="medium"/>
  </div>,
  document.querySelector('#container')
);
```

### Better solution using the Spread Operator
- In JavaScript, spread operator is represented by `...` before our array
- Eg: `...items` which represents items[0], items[1], items[2] etc
- Spread operator allows us to unwrap an element into its individual elements
- Using `spread` operator if there is any change in a property, only two places needs change -- where property is defined and where it is consumed
- `spread` operator only works with arrays out of the box. The reason it works with React object literal `props` is because of Babel transpilation

Apply `spread` operator to Label and Shirt components:
```  
var Label = React.createClass({
  render: function() {
    return (
      <div>
        <Display {...this.props}/>
      </div>
    );
  }
});

var Shirt = React.createClass({
  render: function() {
    return (
      <div>
        <Label {...this.props}/>
      </div>
    );
  }
});
```
------------------------------------

# Meet JSX
- JSX is converted into JavaScript by Babel for the browser

JSX:
```
<div style={cardStyle}>
  <Square color={this.props.color}>
</div>
```

Babel conversion of JSX to JavaScript:
```
var Card = React.createClass({
  displayName: "Card",
  render: function render() {
    var cardStyle = {
      height: 200,
      width: 150,
      padding: 0,
      backgroundColor: “#FFF”,
      WebkitFilter: "drop-shadow(0px 0px 5px #666)",
      filter: "drop-shadow(0px 0px 5px #666)""
    };
    return React.createElement(
      "div",
      { style: cardStyle },
      React.createElement(Square, { color: this.props.color }),
      React.createElement(Label, { color: this.props.color })
    );
  }
});
```

## JSX Quirks
1. Can only return a single root Node
2. Cannot specify CSS inline
  - The following snippet is not allowed where CSS is defined inside styled. Instead CSS has to be defined using style object
  ```
  /* NOT ALLOWED */
  <div style=”font-family:Arial;font-size:24px“>
    <p>Blah!</p>
  </div>
  ```
3. Javascript reserved Keywords and className cannot be used
4. Comments: JSX comments are quite similar to HTML and JS except for comments as a child of tag. Such comments needs to be wrapped by `{` and `}`
  - Child Comments: Comment is a Child of <div>
    ```
    <div class=“slideIn”>
      <p class=“emphasis”>Gabagool!</p>
      {/* I am a child comment */}
      <Label/>
    </div>,
    ```
  - Tag comment: Wholly inside a tag
    ```
    <Label
      /* This comment
      goes across
      multiple lines */
      className=“colorCard” // end of line
    />
    ```
5. Capitalization, HTML Elements and Components: HTML elements should be lowercase, whereas Components must be capitalized
6. JSX Can Be Anywhere: JSX can be defined outside of render function
```
var swatchComponent = <Swatch color=“#2F004F”></Swatch>;

ReactDOM.render(
  <div>
    {swatchComponent}
  </div>,
  document.querySelector(“#container”)
);
```
------------------------------------

# Dealing with State
[Codepen.io Link](https://codepen.io/andrewgurung/pen/ZJEQXN)
- State is a way to store data on a component that goes beyond properties
- We are taking an example of a Lightning strike counter that calls `timerTick` function which adds 100 to the initial count. setInterval is used to trigger the `timerTick` function every 1000ms or 1sec

### React Component exposes three APIs
1. getInitialState: This method runs `before` component gets mounted
2. componentDidMount: This method runs `after` component gets rendered
3. setState: This method allows to update the value of `state` object

### Setting the Initial State Value
- Set `strikes` as our counter with value of 0 in `LightningCounter` component using `getInitialState` function
- The object that is returned is the initial value of our component's `state` object
- Render the counter value using `{this.state.strikes}`
- At this point, the UI will display `0`
```
var LightningCounter = React.createClass({
    getInitialState: function() {
      return {
        strikes: 0
      };
    }
    ...
```

### Starting our Timer
- After the component has been rendered, start increasing the `strikes` counter by 100 every second using `componentDidMount` function
- `setInterval` function will trigger at a fixed interval
```
componentDidMount: function() {
  setInterval(this.timerTick, 1000);
}
```

### Setting State
- Use `setState` API to update the state of `strikes` property
- IMPORTANT: Calling `setState` will update the `state` object and automatically calls `render` method to display the updated `strikes` value
- React is great in syncing data and UI for us
```
timerTick: function() {
  this.setState({
    strikes: this.state.strikes + 100
  });
}
```

------------------------------------

# Going from Data to UI
- 
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
