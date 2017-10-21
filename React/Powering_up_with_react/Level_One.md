# Powering up with react

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
class RobotBox extends React.Component{
      render(){
        return(<div> Hello From React </div> )
      }
}

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
