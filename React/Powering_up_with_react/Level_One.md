# Level 1: First Component
Learn how to solve problems in terms of React components, and get familiar with the JSX markup language.

## 1.2 Breaking Down Problems

In React, What do we create in order to solve problems? 
Answer: Component

## 1.3 Identifying Components

Here is the mockup for a social media feed app that we would like to build with React. 
Before we start converting this mockup into a real React app, we need to identify what parts of the app will become components.

- Select the box that will become the StoryForm component.

Answer: Post a comment box



## 1.4 The rendering process
Before React makes any changes to the page, it generates an in-memory representation of the DOM called the 
*virtual  DOM.


## 1.5 Creating a component
Time to write our first React component.
- Make the RobotBox class a React component.
- Now define an instance method responsible for rendering the component.
- Inside the render() instance method, return a div element with the content Hello From React.

Remember: no quotes are needed when markup is returned in React components.

component.js
```sh
class RobotBox extends React.Component {
   render() {
     return( <div> Hello from React </div> );
   }
}

ReactDOM.render(
   <StoryBox />, document.getElementById('story-app')
);
```


## 1.6 Rendering a Component
Now let's use ReactDOM to render components to our HTML page.
- As the first argument to the renderer, invoke the RobotBox component.
- As the second argument, pass the target container element.

component.js
```sh
class RobotBox extends React.Component {
  render() {
    return <div>Hello From React</div>;
  }
}

let target = document.getElementById('robot-app');

ReactDOM.render(< RobotBox />, target);
```

## 1.7

No Code

## 1.8 The Markup Used by React
The markup we return from ```sh render() ``` methods in React components is called:
Answer: JSX

## 1.9 Coding JSX
Let's finish coding our RobotBox component. 
- Add an ```sh <h3>``` tag as a child node to the existing ```sh <div>``` with the following content: McCircuit is my name
- Add a ```sh <p> ``` element as a child node of the existing ```sh <div> ``` and after the ```sh <h3>``` tag. 
      - Give it the CSS class name message and the following content: I am here to help.
      
component.js
```sh
class RobotBox extends React.Component {
  render() {
    return (
      <div>
        <h3> McCircuit is my name </h3>
         <p className="message"> I am here to help. </p>
      </div>
    );
  }
}
```

## 1.10  JSX and Plain JavaScript

- Before the return statement, create a new variable called pi and assign it the value of PI. In case you don't remember, you can use the built-in Math.PI property from JavaScript.
- Reference the pi variable from inside the render() method so that the message returned by our component says: The value of PI is approximately 3.141592653589793.
- Lastly, add a CSS class to the component <div> called is-tasty-pie.
component.js
      
```sh 
class RobotTime extends React.Component {
  render() {
  	const pi = Math.PI;
    return (
      <div className="is-tasty-pie">
        The value of PI is approximately {pi};
      </div>
    );
  }
}  
```
## 1.11 JSX and Collections

- Using the map() method on the topics array, let's start by returning an empty <li> element for each item.
- Using the single argument to the callback function passed to map(), render each topic inside the <li> tag.   
      component.js

```sh  
class RobotItems extends React.Component {
  render() {
    const topics = ["React", "JSX", "JavaScript", "Programming"];
    return (
      <div>
        <h3>Topics I am interested in</h3>
        <ul>
          {topics.map( topic => <li> {topic}</li>)}
        </ul>
      </div>
    );
  }
}
```
