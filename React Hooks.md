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
