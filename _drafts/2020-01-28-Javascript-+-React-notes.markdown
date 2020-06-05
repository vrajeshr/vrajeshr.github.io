---
layout: post
title:  "Javascript and React notes"
description: Notes I took while learning Javascript and React for an upcoming project.
date:   2020-01-28
---

General JS
Immediately Invoke Function Expression - IIFE
IIFE - Write a function and immediately invoke it
	Used for privacy, 
	
(function() {
	console.log("hello");
})(); 
() is the invoke
	
Closure a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.
Pure functions
Functions that accept an input and returns a value without modifying any data outside its scope
With the same input, expect the same output.
Math.max(1,2,3) returns 3 always //Pure
Math.random() returns something from 0.00 -> 1.00 //non-pure
Destructuring
const personOne = {
	name: "test",
	age : 32,
	address : {
		city: "somewhere",
		"state”: somewhere"
	}
}

const { name, age } = personOne
const { name: uniqueName , age } = personOne
const { name: uniqueName , address : { state } } = personOne




const printUser = ( { name, age} ) => {
	console.log(`Name is: ${name}. Age is ${age}`)
}

printUser(personOne)

Arrow functions allows to bind the context of the components properly since auto-binding is not available by default

JSX - extension for JavaScript, 
	cannot be read directly by the browser
	uses babel, to convert to regular JS func

debugging is easier with the combination of redux + components

Events - triggered reactions to specific actions like mouse hover, click, key press, etc
	How to create: 
		show(event){
			//Something
		}
		render -> return <div onClick={this.show}>Something</div>

Hoisting - variable delectations and function declarations moved to the top

React
What is virtual DOM?
	Updating DOM is really expensive.
	REACT came up with the idea of a virtual DOM, react generates a copy of a DOM
	Any updates that happen from props,states,components, the virtual DOM gets updated and both the virtual dom and dom are reconsiled  

React keys - Identifiers, used for react to see if the component has changed
What is context – Globally available prop that should only be used on occations, 
Prop types – A way to knowing what the types a component is expecting

Refs – References
⦁	To return references to a particular element or component in the render(), useful when DOM measurement or add methods to components
⦁	cases when to use: Manage focus, text selection, or media playback

Controlled components - don't maintain own state, data is controlled by parent, current value through props, notifies w/ callbacks
Uncontrolled - Maintain their own state, data is controlled by DOM, refs are used to get their current value
High order components (HOC) - Custom components which wrap other components, 
Stateful- Stores info about component state in memory, has authority to change state, knows about past, current and possible future changes to the state, stateless components notify stateful components about requirements of the state change, and then sends down the props to them

Stateless - Calculates the internal state of the component, does not have authority to change state, contains no knowledge of paste, current and future possible changes, receive the props from the stateful components, treated as callbacks




Phases of React Component lifecycle
⦁	Mounting
⦁	render, getDefault,Props, getInitalState, componentWillMount, render, componentDidMount
⦁	Updating
 render, componentWillRecieveProps, shouldComponentupdate, componentWillUpdate,
⦁	Unmounting
⦁	componentWillUnmount




Fragments - 
	<ChildA />
	<ChildB />  //Doesn't work
	
	<> //Or <React.Fragment>
		<ChildA />
		<ChildB />  //Doesn't work
	</>
Optimizing react app
	Maybe re-rendering? use shouldcomponentupdate
	Maybe API's are slow?
	double checking where states are getting changed
	assets are loading slowly?

Components
setState - will always trigger a re-render of the component
	if state was directly changed, re-render will not know of an update




Redux.
Flux - Unidirectional flow for data (bad)
Flux, multiple stores per application as a singleton object.
Redux a single store is per application
 

 

Used to state management, easier to test and help applications behave consistently
3 principles of redux:
⦁	single source of truth
⦁	state is read only
⦁	changes are made with pure functions

Components of Redux
⦁	Action Object that describes what happens
⦁	Should always have a type of action being performed (Like “ADD_TODO”)
⦁	Reducer Function that handles how state will change
⦁	Pure functions used to specify how application state changes based on the ACTION dispatched
⦁	Takes previous state and an action and returns a new state
⦁	If no work needs to be done, return original state.
⦁	Store Object of the entire application’s state
⦁	Holds application state
⦁	Provides a few helper methods to access the state, dispatch actions and register listeners
⦁	Large applications are easier and faster with the store.
⦁	View Displays the data provided by the store
Since source of truth – Redux uses a store for storing all application state
middle ware - in between front and database/backend in order to ensure data is synced
	redux-saga - 
	redux-thunk – 
Problem with MVC framework
	DOM manipulation is very expensive, slow and inefficient
	Memory wastage
Component – Piece of the user interface
Root component = App component

