# Chapter 8

### An example of import react, where it’s used.

```cpp
import React from "react"; 

class Profile extends React.Component{}; 
```

You see we have basically used something from React.

## Random

We basically use extend, cause we want to inherit some properties from somewhere.

---

We cannot have a class based component without the render(){} function. It basically returns some JSX which is rendered in the DOM. And then, we just export this normally like a functional component.

---

**************************************************************Props in Class based components**************************************************************

This is how we get props in class based components.

```jsx
// D:\Development\swiggy\src\components\ProfileClass.js
import React from "react";
// Note, how we're using React.component 
// we don't need to import react everywhere in our file. Just do it when it's needed

class ProfileClass extends React.Component{
    render() {
      return (
        <div>
          <h1>Hey this is the class based profile component.</h1>
          <h1>{this.props.name}</h1>
        </div>
      )
    }
}

export default ProfileClass;
```

And, this is where we’re getting the props from - 

```jsx
// D:\Development\swiggy\src\components\About.js

import { Outlet } from "react-router-dom"
import Profile from "./Profile"
// this outlet is a component.
import ProfileClass from "./ProfileClass"
import ProfileFunction from "./Profile" // we can basically import anything default by some other name as well

const About = () => {
  return (
    <div>
      <h1>About us page</h1>
      <p>Hello This is the about page.</p>
      <Outlet/>
      <ProfileFunction name ="Aditya"/>
      <ProfileClass name ="Aditya Class Based"/>

    </div>
  )
}

export default About
```

- Now, what’s happening is, React is basically keeping a track of our class based component. It knows that `class ProfileClass extends React.Component` is a class based component. And, whenever, there’s a state change or a prop change, it needs to re-render the component.
- Whenever, we’re passing props from the parent component, to a class based component, what React does is that it basically attaches the props to the `this` keyword (which is similar to an object.) So, `this.props` would be an object, which contains everything inside the props.

---

### Constructors in JS

- Constructor is a place used for initialization.
- Whenever the class is invoked, (or whenever the class based component is rendered, a constructor is called) and this is the best place to create our state.
- Whenever we load a class, constructor is called.
- Just like React gives us access to `this.props()` it also gives us access to `this.state()`

---

### Class based components in React, and managing states in them

- All the state variables are declared inside a single state object. i.e., `this.state = {}`
- In class based components, React uses 1 big state object to manage the whole state.
    - Even in functional components, behind the scenes, React uses one big state object to store the whole state.
- This is how we setState in class based components
    
    ```jsx
    constructor(props) {
        super(props);
    
        this.state = {
          count : 0, 
          count2: 0
    
        };
      }
    // And, this ^ is how we've defined the state.
    
    <button onClick={()=>{
              this.setState({
                count: this.state.count+1 
    			    });
    }} >
    Set Count
    </button>
    ```
    

---

### Something about Lifecycle of class based components.

- First of all, the `constructor` is called.
- Then, the `render()` function is called. (or, the component renders)
- Then, the `componentDidMount()` is called.

---

**********************Question:********************** Consider the below code, and try to find out the console.log() sequence.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/215746ce-b175-4e29-84a8-c98d148b2593/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d1ba8d60-7df3-4ccf-95d9-d207ee51abe8/Untitled.png)

---

********************Question:******************** Consider the below code, and try to find out the console.log() sequence

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f5182d91-080e-4bb7-ab45-4c2bfcb7d082/Untitled.png)

But, before answering this, let’s understand this - 

# Life Cycle Methods

- When react is rendering things, it does it in 2 phase.
    - **The first phase is the render phase (this is very fast)**
        - Constructor is called
        - Render is called
    - **The second phase is the commit phase (this is comparatively slow,** cause it has to update the DOM, which takes up a lot of time**)**
        - `componentDidMount()` is called.
            - After the render is done, we’re ready to put things into our DOM. So, in the commit phase, React will update the DOM, and after they have updated the initial DOM, then it will call `componentDidMount()`

********And, what happens is, if there are more than 1 children, react tries to batch the render phase of every children, and then start the second phase.********

********But, why?********

- Say that there’s an API call in the `componentDidMount()` of a child, and if we call that, it may take a lot of time to fetch everything, which may delay the render and the other process of further children.
- So, React creates batches, and tries to complete the render phase of all the children, first and then, when every children is done with the render phase, it starts the second phase of every children, and when that is done, it starts the second phase of the parent.

Now, let’s come back to answering this.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f5182d91-080e-4bb7-ab45-4c2bfcb7d082/Untitled.png)

What would be he order of console logs. 

---

## Random 1 liners

1. Kinda obv but I’ll still write this: It’s not mandatory to always define the set function in useState. 
    
    i.e., `const [count] = useState(0);` is also valid.
    
2. Reconciliation works the same way in both functional and class based components.
3. In class based components in react, first of all the ********constructor******** is called, then the **component is rendered** (i.e., the render() function is called).
4. **We used to call our API in the `useEffect()` in functional components.**
5. **In class based components, we call the API  in the `componentDidMount()` cause**
    1. First of we want to show all the stuff which doesn’t need the data, could be anything. Could be Shimmer as well. 
    2. And, then, as soon as we show that, we then fetch our data and update our components.

---

# Things to do post session

- Read about routing name conventions in react-router-dom
- Read about classes in JS.
    - Read about why we use `Super()` in JS, and all that Jazz regarding classes in general.
- Read more about this `<ProfileClass name ="Aditya Class Based" age = {12} />` would not give an error, but this `<ProfileClass name ="Aditya Class Based" age = 12 />` would.
- Read about **********************************React lifecycle.**********************************
