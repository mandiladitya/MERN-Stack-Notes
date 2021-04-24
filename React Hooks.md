# React Hooks Cheatsheet

- [Overview](#headers)
- [Rules/Guidelines](#rules)
- [The "useState" Hook](#usestate)
- [The "useEffect" Hook](#useeffect)
- [Custom Hooks](#customhooks)

<a name="headers"></a>
## Overview
React (v16.8+) Hooks let you use state and lifecycle methods in function components (now formerly known as "stateless components").

Function components need to return a JSX element

    const MyComponent = (props) => {
      // hook calls will go here
      return (
        <div>Hello World</div>
      );
    }

<a name="rules"></a>
## Rules/Guidelines
- Hooks ***must*** be called in the top level of a function component or custom hook, not inside a loop or condition

- Hooks are just JS functions, but by convention their names should always start with a lowercase `use`

<a name="usestate"></a>
## The "useState" Hook
The useState hook allows a function component to have state

    const MyComponent = (props) => {
      const [myValue, setMyValue] = useState(24);
      ...
    }

- Calling `useState()` returns an array of 2 elements
  - The first element is the state variable itself
  - The second is a setter function to change the state variable

- Passing a value to useState will set the initial state variable to that value (otherwise it will init to 'undefined')

- If you need multiple state values, just call `useState` multiple times

      const [name, setName] = useState('Doug');
      const [age, setAge] = useState(46);

- State variables can be arrays or objects

- Passing a single parameter function to the state setter gives you access to the previous state. That function must return the new state. This is useful when you can no longer depend on the state variable itself (i.e. inside of a `setTimeout` or `setInterval`).

      const [age, setAge] = useState(46);
      ...
      const onBirthday = () => {
        setAge(previousAge => previousAge + 1);
      }

<a name="useeffect"></a>
## The "useEffect" Hook
The useEffect hook adds lifecycle functionality to function components

- useEffect takes a function (can be referred to as an "effect") as a paramater

      const MyComponent = (props) => {
        useEffect(() => {
          document.title = 'Hello';   // this will run after every render
        });    
        ...
      }

- The "effect" will run ***after*** the DOM has rendered

- useEffect can have a second parameter (known as a "dependency") which should be an array of state variables and/or props, that means the "effect" will only run when the specified state or props variable(s) has changed

      const [title, setTitle] = useState('Hello');
      useEffect(() => {
        document.title = title;   // this will run only when 'title' has changed
      }, [title]);

- If you pass multiple dependecies, the effect will run when one dependency changes

- You can pass an empty array `[]` as the second parameter if you want the effect to run only once (similar to the `ComponentDidMount` method in class components)

- The "effect" can return a function, which will be treated as a "clean up" phase for the effect

      useEffect(() => {
        // api call...
        return () => {
          // do some cleanup here
        }
      });

- The "clean up" function runs on every re-render (not on the component's first render) before the "effect" runs, but any state it has will be from the previous render. This gives the "effect" a chance to clean up anything related to the previous state before doing something with the new state

      const [value, setValue] = useState();
      useEffect(() => {
        console.log(value);   // this will have the latest 'value'
        return () => {
          console.log(value);   // this will print before the above console.log but it will have the previous 'value'
        }
      }, [value]);

<a name="customhooks"></a>
## Custom Hooks
If there is complicated state or lifecycle logic that is used by multiple components, it can be placed into one function aka hook. This does ***NOT*** mean components share state with each other between the custom hook, only that they reuse the logic. This makes it so you don't have to write duplicate logic for each component.

- A custom hook is just a function that may or may not take a parameter(s) or may or may not return a value

      const useAdd5 = (number) => {
        return number + 5;
      };

- A custom hook can use other hooks (the following would loop infinitely, if not for the empty array passed as the second parameter to `useEffect`. The `setData()` call would trigger another render which would run the API call again, rinse and repeat)

      const useFetchData = () => {
        const [data, setData] = useState(null);
        useEffect(() => {
          getDataFromAPI(newData => {
            setData(newData);
          }, []);
        });
        return data;
      };
-------------------------------------------------------------------------
(use instead of redux lol) => gives functional components state and life-cycle methods (faster to use than classes)
- To use a basic state: .useState()
- To use lifecycle methods: useEffect()
- To define state changes by using reducers: .useReducer()
- To access the state directly instead of props use Context

#### useState():
Returns an array, the first thing is what you want to keep track of. 
The second is a function which allows you to edit it (aka set the state). 

If you have multiple things to track the state of, use a seperate useState() for each one. 

Usually destructured like follows: 
````js
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount(count + 1);
  };

  const decrement = () => {
    setCount(count - 1);
  };

  const reset = () => {
    setCount(count = 0);
  };
````

#### useEffect():
A replacement for lifecycle methods in class-based components. i.e. component did mount / update etc. 
````js
import React, {useState, useEffect} from 'react';
````

useEffect is something we call, and we pass to it a function. 
````js
  useEffect(() => {
    console.log('useEffect ran');
    document.title = count
  });
````

useEffect updates when the page loads and every time there is a state change.

useEffect allows us to specify the things we care about: done via an array as the 2nd argument. Not required but ..

````js
useEffect(() => { 
    console.log('useEffect ran');
    document.title = count;
  }, [count]);
````

just like with useState(), we can use the useEffect() as many times as we need to in a functional component.

````js
  useEffect(() => { //a mirror of 'componentDidMount'!
    console.log('this should only run once!');
  }, []); // will only run once when component mounts, due to empty array

  useEffect(() => {
    console.log('useEffect ran');
    document.title = count
  }, [count]);
````

now count is the second argument (its an array of things to include as state-changers), it ONLY runs when the count state is changed.

 Cleaning up effect, aka "component did unmount" 

 ````js
const Note = ({note, removeNote}) => {
  useEffect(() => {
    console.log('Setting up effect!');

    return () => {
      console.log("Cleaning up effect!")
      //runs when component unmounts! (aka note is deleted from dom)
    }
  }, [])
````

#### useReducer():
A simpler way to define state changers by defining reducers.

````js
import React, {useState, useEffect, useReducer } from 'react';

//need to define reducer function before you can call it. 
const notesReducer = (state, action) => {
  //state is an array of notes
  //action provides info of action to perform

  switch(action.type){
    case 'POPULATE_NOTES':
      return action.notes;
    default: 
      return state;
  }
}
````

Instead of useState, you call useReducer: 
````js
  const [notes, dispatch] = useReducer(notesReducer, [])
````
useReducer takes two arguments, the reducer function and the starting (or default value) 
First item returns the thing to be tracked, in this case an array. 
Second thing (dispatch) is a function you call and pass in a reducer.

````js
dispatch({ type: "POPULATE_NOTES", notes: getNotes() });
````

In essence: 
If we find state is more complex, we can switch from useState to useReducer to store different logic in another function. 

useState uses useReducer behind the scenes.

#### CONTEXT / createContext() / useContext():
1. first you have notes-context in the file providing context, and the file consuming context. Thats why you have it in its own file. 
````js
import React from 'react';
const NotesContext = React.createContext()
export default NotesContext;
````
2. In main component (that renders all related stuff):
````js
  return (
    <NotesContext.Provider value={{ notes, dispatch }}>
      <h1>Notes</h1>
      <p>Add note</p>
      <AddNoteForm />
      <NoteList />
    </NotesContext.Provider>
  )
````
3. Inside the components that use this, grab the value like so: 
````js
  const {notes, dispatch} = useContext(NotesContext);
````
