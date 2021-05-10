# Notes
## Links
* 🎥 [GP](https://youtu.be/O2fhyPyyJBo)
* 📝 [MP](https://github.com/nora-exe/web-module-project-reducer/tree/nora-corser)

## Key Concepts:
* [Business Logic](https://simplicable.com/new/business-logic) - The outline of the data and types of manipulations of data needed to create a working application
* [Application State](https://www.youtube.com/watch?v=7ilYJAG-_Ug) - Data that is used across all of our application's components.
* [Component State](https://stackoverflow.com/questions/22883759/what-is-the-difference-between-application-state-and-component-local-state-in-cl) - Data that is used within the context of a single component
* [The Reducer Pattern](https://redux.js.org/tutorials/fundamentals/part-2-concepts-data-flow) - A design pattern for managing and modularizing out application state.
* [useReducer Hook](https://www.geeksforgeeks.org/reactjs-usereducer-hook/) - A hook used to connect reducers and state to a React component
* [What does dispatch do?](https://dev.to/dustinmyers/what-even-is-a-dispatch-function-27ma) - Awesome article by our own @Dustin Myers on the inner workings of dispatch

## Key Terminology:
* [switch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch) - a javascript keyword used to streamline complex if else logic
* [action](https://redux.js.org/tutorials/fundamentals/part-2-concepts-data-flow) - a single piece of data manipulation in a reducer pattern
* [reducer](https://redux.js.org/tutorials/fundamentals/part-2-concepts-data-flow) - a pure, predictable immutable function that executes action on state data
* [immutability](https://www.youtube.com/watch?v=5qQQ3yzbKp8) - an object or variable that can not be modified (and thus should only be copied)
* [pure functions](https://www.youtube.com/watch?v=dZ41D6LDSBg) - a pure, predictable immutable function that executes action on state data

## Notes
Reducer functions take two arguments – the current state and action – and return a new, updated state object based on both arguments.
```javascript
const initialState = { count: 0 }
const reducer = (state, action) => {
  if (action.type === 'increment') {
    return { count: state.count + 1 }
  }
}

reducer(initialState, { type: 'increment' })
```
Current state passes into the reducer, and an action follows to tell the reducer *how* to update the state.


You can also add a `payload` property to your action objects (sometimes called data). Our reducer needs to have some data passed into it through the action to be able to update the state correctly, and this is where that data would live.
```javascript
const initialState = { name: 'Donald Duck' }
const reducer = (state, action) => {
  if (action.type === 'changeName') {
    // how do we know what to change the name to? The action payload!
    return { name: action.payload }
  }
}

reducer(initialState, { type: 'changeName', payload: 'Mickey Mouse' });
```


Lastly, use JavaScript's switch statement to make `if` `else` parts of our reducer a lot more readable:
```javascript
const initialState = { count: 0 }
const reducer = (state, action) => {
  switch(action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 }
    default:
      return state;
  }
}

reducer(initialState, { type: 'increment' });
reducer(initialState, { type: 'decrement' });
```


Alternatively, employ the `useReducer` hook to manage state in a component if you find yourself with a lot of state properties (more than 3) in a single component. It takes in a reducer function & a value for the `initialState`. Then it returns both the current state and a `dispatch` method in an array, just like `useState` does.
```const [state, dispatch] = useReducer(reducer, initialState);```
`dispatch` will "dispatch" an action to the reducer when specific events occur in the application. Dispatch lets you combine the reducer function with the ability to **maintain state at the level of the component.**
```javascript
// Return JSX that displays the count for the user
/* Note the two button elements which allow the user to increase and decrease the count. 
Each of them contains an onClick event that dispatches the desired action object, with its
given type.  Each action, when fired, is dispatched to the reducer and the appropriate logic
is applied.*/
return (
<>
    {/* Note, we have access to the current state and the dispatch method from the useReducer hook,
    so we can utilize them to display the count as well as couple the dispatching of the actions
    from the appropriate buttons.*/}
    <div className="count">Count: {state.count}</div>
    <button onClick={() => dispatch({ type: 'INCREASE' })}>+1</button>
    <button onClick={() => dispatch({ type: 'DECREASE' })}>-1</button>
</>
)
```

# The Reducer Pattern Module Project: The Calculator

This module explored the reducer pattern. During the module, you studied what immutability is, what reducers, actions and dispatch are, and how to use the reducer hook. In this project, you will practice each of the steps of building state and actions into an application. We will do this by both adding in and building from scratch all of the pieces of the reducer pattern.

## Objectives
- Understand how to use useReducer hook.
- Get comfortable connecting a reducer state to an application's UI.
- Successfully connect UI user events to the dispatching of reducer actions.
- Understand how to create reducer cases and the action creators that trigger them.
- Learn how to step through and test thoroughly each step of the process.

## Introduction
In this project, you will build an complete a simple calculator app that can add, multiply, subtract and clear numbers in any order as well as add in memory save and recall features. You will start by adding in missing pieces to the code and complete the process by building features in to the UI, reducer and actions files from scratch.

This simplified calculator adds the entire number selected, rather then adds digits into end of number. In the end of the process, your calculator should function as follows:

![Calculator Example](project-goals.gif)

***Make sure to complete your tasks one at a time and complete test each task before proceding forward.***

## Instructions
### Task 1: Project Set Up
* [ ] Create a forked copy of this project.
* [ ] Clone your OWN version of the repository in your terminal
* [ ] cd into the project base directory `cd web-module-project-reducer-pattern`
* [ ] Download project dependencies by running `npm install`
* [ ] Start up the app using `npm start`

### Task 2: Project Requirements
#### Connect The Reducer
> *Let's start our process by connecting our UI to our reducer and initial state.*
* [ ] Take a tour of application, in particular the `App.js`, `/reducer/index.js`, and `/action/index.js` files.
* [ ] Note that the `TotalDisplay` component takes in a value and displays it in a styled textarea. YOU WILL NOT NEED TO MODIFY THIS COMPONENT.
* [ ] Note that the `CalcButton` component takes in an `onClick` method and a value, displays that value and attaches the passed `onClick` method to the button ui. YOU WILL NOT NEED TO MODIFY THIS COMPONENT.
* [ ] Within App.js, import the useReducer hook, our application's reducer and initialState object.
* [ ] Use useReducer hook to get access to the application state and the dispatch function.

#### Display our state within the UI.
> *We now have access to the state within our App component (You can even test this using console.log or your React dev tools). Let's render the state as is on our screen.*
* [ ] Replace "X" with a reference to `state.operation` within the operation element.
* [ ] Replace "0" with a reference to `state.memory` within the memory element.
* [ ] Replace "0" with a reference to `state.total` when passing a value to our TotalDisplay component.
* [ ] Check to see that your total, operation and memory display in the UI match your initialState (100, * and 100 respectively)
* [ ] **Test** that you are connected to state by changing the initialState value in your reducer to:
```
export const initialState = {
    total: 0,
    operation: "+",
    memory: 0
}
```
* [ ] Check to see that your display correctly reflects the change to your state.

#### Connect a premade action.
> *Now that we can see our state, let's change allow the user to change it. Let's start with a simple premade action...adding one to our total.*
* [ ] Note the `ADD_ONE` action case (in ./reducer/index.js) and `addOne` action creator (in ./actions/index.js). This action adds 1 to our total.
* [ ] Import the `addOne` action creator into App.js.
* [ ] Within `App.js`, create an event handler connected to the 1 button's `onClick` method.
* [ ] Within your event handler, dispatch the `addOne` action creator.
* [ ] **Test** that your event is correctly connected by pushing the 1 button in the browser. Your total should increase by 1.
* [ ] **Think** about the path of execution from the clicking of the one button to the rendering of the updated total. What is the order of execution? Within the `Understanding-Question.md` file, write out in your own words the steps of that process.


#### Connect a better premade action.
> *Adding indivisual actions for every number would be tedious. Let's add in an action that can work for ALL numerical input*
* [ ] Note the `APPLY_NUMBER` action case (in ./reducer/index.js) and `applyNumber` action creator (in ./actions/index.js). This action adds, multiplies or subtracts a number passed into the action creator.
* [ ] Import the `applyNumber` action creator into `App.js.`
* [ ] Remove or comment out the `addOne` event handler from the 1 button.
* [ ] Create an eventhandler that takes in a number as an argument and dispatches `applyNumber` with it.
* [ ] Attach that eventhandler to the 1 button's `onClick` method, passing in a 1 as an argument. (Remember that we pass a function into that click handler, not the execution of a function)
* [ ] **Test** that clicking the one button still adds one to the total display on the browser.
* [ ] Connect all other number buttons to your new event handler, passing in their respective values.
* [ ] **Test** that clicking on each button will add its respective value to the total display.

#### Create and connect an action creator.
> *Right now our application only adds. Let's change that and give you practice creating and connecting action creators of your own!*
* [ ] Note the `CHANGE_OPERATION` action case (in `./reducer/index.js`). This reducer case takes in a operator value (+, * or -) and assigns it to state.
* [ ] Create an action creator (in `./actions/index.js`) that takes in an operator as an argument and creates an action object with the type `CHANGE_OPERATION.`
* [ ] Import in your new action creator into `App.js.`
* [ ] Create and attach event handlers to the `+`, `-` and `*` buttons that dispatch your new action creator. Make sure you pass in the appropriate operator string in each case.
* [ ] **Test** that you can successfully change operators and apply numbers in each case.

#### Create and connect a reducer case and action creator.
> *Now let's add in the clear display feature. For this, you will be doing every part of the reducer / action creator process.*
* [ ] Within `./reducers/index,` add in a case for `CLEAR_DISPLAY`. Clear display should set the total value in state to 0.
* [ ] Within `./actions/index,` add in an action creator and action string constant to for `CLEAR_DISPLAY`. Make sure to import that constant into your reducer file.
* [ ] Within `App.js,` import in your clearDisplay action creator.
* [ ] Create and connect an event handler to the "CE" button that dispatches your clearDisplay action creator.
* [ ] **Test** that your clearDisplay button works as expected.

#### Task 8: Add in memory functions from scratch.
> *Congratulations! You have gone through the entire process for adding an action to your app! Now, see if you can follow the same process (reducer case => action creator => UI connection) for the following app features. IN EACH CASE, ALWAYS TEST THAT YOUR FEATURE WORKS BEFORE PROCEEDING FORWARD.*

* [ ] When `M+` is pressed, the state's current memory value should be set to the current total value. Test by seeing the result of memory in the UI.
* [ ] When `MR` is pressed, the state's current total value should be set to the current total value applied to the current memory value (See the APPLY_NUMBER case). Test by adding a value to memory and then seeing if the total updates correctly when pressed.
* [ ] When `MC` is pressed, the state's current memory value should be set to zero. Test by adding a value to memory and then seeing the memory value reset to zero when pressed.


### Task 3: Stretch goals
- [ ] There is a version of the calculator focuses on adding individual digits, rather then entire numbers. How do you imagine adding an individual digit to the total state?
- [ ] [Here is an example](https://freshman.tech/calculator/) of a (non-reducer) approach to building an javascript calculator. Feel free to make a new branch and use the basic ideas in the post to build a new version of the calculator.
