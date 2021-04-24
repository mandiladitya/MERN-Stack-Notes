# 🌈 React Cheat Sheet

> A simple cheat sheet for facilitate the process in the workshops and event about React. Let me know if you see any problem, I'll love a pull request for improve this document.

## Table of contents

- [x] [Installation](#installation)
- [x] [No configuration](#no-configuration)
- [x] [ReactDOM](#reactdom)
- [x] [Functional Stateless Component](#functional-stateless-component)
- [x] [Class Component](#class-component)
- [x] [Composition](#composition)
- [x] [Module component](#module-component)
- [x] [Hot Module Replacement](#hot-module-replacement)
- [x] [Props](#props)
- [x] [State](#state)
- [x] [Methods and Events](#methods-and-events)
- [x] [State manipulation](#state-manipulation)
- [x] [Bindings](#bindings)
- [ ] [Refs](#refs)
- [ ] [Keys](#keys)
- [ ] [Component Lifecycle](#component-lifecycle)
- [ ] [Inline Styles](#inline-styles)
- [ ] [React Router](#react-router)
- [ ] [Storybook](#storybook)
- [ ] [Tests](#tests)
- [ ] [a11y](#a11y)
- [ ] [API comunication](#api-comunication)
- [ ] [Flux](#flux)
- [ ] [Redux](#redux)
- [ ] [MobX](#mobx)
- [ ] [Best Practices](#best-practices)
- [ ] [Concepts](Concepts)
    - [ ] [Immutable](#immutable)
    - [ ] [Functionnal programing](#functionnal-programing)
    - [ ] [Virtual Dom](#virtual-dom)
- [x] [ES6](#es6)
    - [x] [Arrow Functions](#arrow-functions)
        - [x] [Syntax](#syntax)
        - [x] [Advanced Syntax](#advanced-syntax)
    - [x] [Spread Operations](#spread-operations)
        - [x] [Spread in array literals](#spread-in-array-literals)
        - [x] [Spread in object literals](#spread-in-object-literals)

---

## Installation

* Add the tags in your HTML
    ```HTML
    <script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
    ```
* Run this scripts in your terminal
    ```SSH
    $ npm install react react-dom
    ```
 
 **[⬆ back to top](#table-of-contents)**
---
 
## No configuration

Just start with React no configuration (run the scripts bellow in your terminal)
* Install the React
    ```SSH
    $ npm install -g create-react-app
    ```
* Create your application (change `myApp` to your application name)
    ```
    $ create-react-app myApp
    ```
* Go to the application folder and install the dependencies
    ```
    $ cd myApp
    $ npm install
    ```
* Start your application
    ```
    $ npm start
    ```
* Go to the browser by `URL` bellow and see your beautiful application   
    - [localhost:8080](http://localhost:8080)

**[⬆ back to top](#table-of-contents)** 
---

## ReactDOM

```JS
import React, { Component } from 'react';
import ReactDOM from 'react-dom';

ReactDOM.render( <h1>Hello React Ladies</h1>, document.getElementById('root') );
```

**[⬆ back to top](#table-of-contents)**
---

## Functional Stateless Component

```JS
import React from 'react';

const Button = () =>
    <button> Apply</button>

export default Button;
```

```JS
import React from 'react';

const Button = ({ onClick, className = 'button', children  }) =>
    <button
        onClick={ onClick }
        className={ className }
        type='button'
    >
        { children }
    </button>

export default Button;
```

**[⬆ back to top](#table-of-contents)**
---

## Class Component

```JS
import React, { Component } from 'react';

class MyComponent extends Component {
    render() {
        return (
            <div className="main">
                <h1>Helo Devas</h1>
            </div>
        );
    }
}

export default MyComponent;
```

```JS
import React, { Component } from 'react';

class MyComponent () extends Compnent {
    constructor ( props ) {
    super(props);
    this.state = { message: 'Helo Devas' }
    };

    render() {
        return (
            <div className="main">
                <h1>{ this.state.message }</h1>
            </div>
        );
    }
}

export default MyComponent;

```

**[⬆ back to top](#table-of-contents)**
--- 

## Composition

```JS
import React, { Component } from 'react';
import ReactDOM from 'react-dom';

class Love extends Component {
    render() {
        return (
            <div clssName="love">
                <h1>My love</h1>
            </div>
        );
    }
}

class LoveList extends Component {
    render() {
        return (
            <div>
                <Love />
                <Love />
                <Love />
                <Love />
            </>
        );
    }
}

ReactDOM.render(
    <Love />,
    document.getElementById(´root´)
);

**[⬆ back to top](#table-of-contents)**
```

## Module component

```JS
//App.js
import React, { Component } from 'react';

class App extends Component {
    render() {
        return (
            <div className="app">
                <p>My App</p>
            </div>
        );
    }
}

export default App
```

```JS
//Index.js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import App from './App.js';

class Index extends Component {
    render() {
        return (
            <div className="app">
                <App />
            </div>
        );
    }
}


ReactDOM.render (
    <Index />,
    document.getElementById('root')
);

```

**[⬆ back to top](#table-of-contents)**
---

## Hot Module Replacement
* Retain application state which is lost during a full reload.
* Save valuable development time by only updating what's changed.
* Tweak styling faster -- almost comparable to changing styles in the browser's debugger.

```JS
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import MyComponent from './MyComponent';

ReactDOM.render( <MyComponent />, document.getElementById('root') );

if (module.hot) {
    module.hot.accept();
}
```

**[⬆ back to top](#table-of-contents)**
---

## Props

```JS
import React, { Component } from 'react';

class App extends Component {
    render() {
        return (
            <div className="app">
                <p>My App {this.props.name}</p>
            </div>
        );
    }
}

class Index extends Component {
    render() {
        return (
            <div className="app">
                <App name="Simone"/>
            </div>
        );
    }
}

export default Index;
```

**[⬆ back to top](#table-of-contents)**
---

## State

```JS
import React, { Component } from 'react';

class App extends Component {
    constructor(props) {
        super(props);
        this.state = {messages: 0};
    } 

    render() {
        return (
            <div className="app">
                <p>My messages: {this.state.messages}</p>
            </div>
        );
    }
}

export default App;
```

**[⬆ back to top](#table-of-contents)**
---

## Methods and Events

```JS
import React, { Component } from 'react';

class App extends Component {

    escreve() {
      console.log("Eu te amo");
    }

    render() {
        return (
            <div className="app">
                <button onClick={this.escreve}>save</button>
            </div>
        );
    }
}

export default App;
```

**[⬆ back to top](#table-of-contents)**
---

## State manipulation

```JS
import React, { Component } from 'react';

class App extends Component {
    constructor() {
        super();
        this.state = { like: 0 };
    } 

    isLiked = () => {
      this.setState({ like: this.state.like + 1});
    }

    render() {
        return (
            <div className="app">
                <button onClick={ this.isLiked }>{ this.state.like }</button>
            </div>
        );
    }
}

export default App;
```

```JS
import React, { Component } from 'react';

class App extends Component {
    constructor() {
        super();
        this.state = { messages: ['JS', 'React'] };
    } 

    addMessages = () => {
        const updateMessages = [...this.state.messages, 'Polymer']
        this.setState({ messages: [...updateMessages] })
    }

    render() {
        return (
            <div className="app">
                <button onClick={this.addMessages}>add</button>
                {console.log(this.state.messages) /* ['JS', 'React', 'Polymer'] */}
            </div>
        );
    }
}

export default App;
```


**[⬆ back to top](#table-of-contents)**
---
d
## Bindings

```JS
import React, { Component } from 'react';

class MyComponent extends Component {
    constructor () {
    super();

    this.state = { list: list };

    this.doSomethingElse = this.doSomethingElse.bind(this);
    };

    doSomething = () => {
        // do something
        /* if don't have a parameter, you can use arrow function
           and don't need to use bind */
    }

    doSomethingElse ( itemId ) {
        // do something else
    }

    render() {
        return (
            <div className="main">
                {this.state.list.map( item =>
                ...
                    <button 
                        onClick={ this.doSomething } 
                        type="button"
                    >
                        Some Thing
                    </button>

                    <button 
                        onClick={ () => this.doSomethingElse( item.objectID ) } 
                        type="button"
                    >
                        Some Thing Else
                    </button>
                ...
                )}
            </div>
        );
    }
}

export default MyComponent;
```

---

# ES6

## Arrow Functions

### Syntax

  #### Basic syntax
    ```JS
    ( param1, param2, ..., paramN ) => { statements }

    ( param1, param2, ..., paramN ) =>  expression

    ( singleParam ) => { statements }

    singleParam => { statements }

    () => { statements }
    ```
  #### Advanced Syntax
    ```JS
    params => ({ foo: bar }) /* return an object literal expression */

    ( param1, param2, ...ladies ) =>  { statements } /* rest parameters */

    ( language = JS, ladies, ..., framework = React ) => { statements } /* default parameters */

    const sum = ( [num1, num2] = [1, 2], { x: num3 } = { x : num1 + num2 } ) => num1 + num2 + num3  /*  destructuring within the parameter list */
    sum() /* 6 */
    ```

---

## Spread Operations

### Spread in array literals
```JS
const basics = [ 'JS', 'HTML', 'CSS' ];
const frameworks = [ 'React', 'Vue' ];
const web = [ ...basics, ...frameworks ]; 
console.log(web); /* ['JS', 'HTML', 'CSS', 'React', 'Vue'] */

const addWeb = [ ...web, 'al11' ];
console.log(addWeb); /* ['JS', 'HTML', 'CSS', 'React', 'Vue', 'al11'] */
```

### Spread in object literals
```JS
const basics = { behavior: 'JS', markup: 'HTML' };
const style = 'CSS';
const web = { ...basics, style }; 
console.log(web); /* { behavior: "JS", markup: "HTML", style: "CSS" } */

const devFront = { framework: 'react', event: 'React Conf' };
const devBack = { framework: 'django', state: 'cool' };

const cloneDev = { ...devFront };
console.log(cloneDev); /* { framework: 'react', event: 'React Conf' } */

const merged = { ...devFront, ...devBack };
console.log(cloneDev); /* { framework: 'django', event: 'React Conf', state: 'cool' } */
```
------------------------------------------------------------------------------------------------------------

### Component Lifecycle
```javascript
componentWillMount() {

}
```

```javascript
componentDidMount() {
  // Call after the component output has been rendered in the DOM
}
```

```javascript
componentWillReceiveProps() {

}
```

```javascript
shouldComponentUpdate() {

}
```

```javascript
componentWillUpdate() {

}
```

```javascript
componentDidUpdate() {

}
```

```javascript
componentWillUnmount() {

}
```

```javascript
componentDidCatch() {

}
```
### Handling Event
```javascript
// React Event are in camelCase
<button onClick={handleClick}>
  Action
</button>
```

```javascript
// Use preventDefault instead of return false
function handleClick(e) {
  e.preventDefault();
}

```

```javascript
// Bind this to use it in the callback
constructor(props) {
  super(props);
  this.handleClick = this.handleClick.bind(this);
}
```

```javascript
// Pass data to callback
<button onClick={(e) => this.deleteItem(id, e)}>Delete item</button>
<button onClick={this.deleteItem.bind(this, id)}>Delete item</button>
```
**[⬆ Go to top](#table-of-contents)**

### Conditional Rendering
```javascript
// Using if operator with props
function Heading(props) {
  const isHome = props.isHome;
  if (isHome) {
    return <HomeHeading />;
  }
  return <PageHeading />;
}
```

```javascript
// Using if operator with state
render() {
  const isHome = this.state.isHome;
  let heading = null;
  if (isHome) {
    heading = <HomeHeading />;
  } else {
    heading = <PageHeading />;
  }

  return (
    <div>
      {heading}
    </div>
  );
}
```

```javascript
// Using ternary operator
<div>
  {isHome ? <HomeHeading /> : <PageHeading />}
</div>
```

```javascript
// Using logical operator
<div>
  {messages.length > 0 &&
    <h1>
      You have messages
    </h1>
  }
</div>
```

```javascript
// Prevent component from rendering
function Modal(props) {
  if (!props.isShow) {
    return null;
  }

  return (
    <div>
      Modal
    </div>
  );
}
```

**[⬆ Go to top](#table-of-contents)**

### Portal
```javascript
import { createPortal } from "react-dom";

class MyPortalComponent extends React.Component {
  render() {
    return createPortal(
      this.props.children,
      document.getElementById("node"),
    );
  }
}
```
**[⬆ Go to top](#table-of-contents)**

### Fragment
```javascript
const Fragment = React.Fragment;

render() {
  return (
    <Fragment>
      Some text.
      <h2>A heading</h2>
      Even more text.
    </Fragment>
  );
}
```

```javascript
render() {
  return (
    <React.Fragment>
      Some text.
      <h2>A heading</h2>
      Even more text.
    <React.Fragment>
  );
}
```

```javascript
render() {
  return (
    <>
      <ComponentA />
      <ComponentB />
    </>
  );
}
```
**[⬆ Go to top](#table-of-contents)**

### Forms

#### Controlled Components
```javascript
// In controlled component, each state mutation have an handler function
class Form extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(e) {
    this.setState({value: e.target.value});
  }

  handleSubmit(e) {
    alert('Submitted value: ' + this.state.value);
    e.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <input type="text" value={this.state.value} onChange={this.handleChange} />
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

```javascript
// Force to uppercase in handler
handleChange(e) {
  this.setState({value: e.target.value.toUpperCase()});
}
```

```javascript
// <textarea> in React use a value attribute
<textarea value={this.state.value} onChange={this.handleChange} />
```

```javascript
// <select> use a value and not a selected attribute
<select value={this.state.value} onChange={this.handleChange}>
  <option value="a">Option A</option>
  <option value="b">Option B</option>
</select>
```

```javascript
// <select value can have an array for multiple values
<select multiple={true} value={['a', 'b']}>
```

```javascript
// Handle multiple inputs with name attribute
handleInputChange(e) {
  const target = e.target;
  const value = target.value;
  const name = target.name;

  this.setState({
    [name]: value
  });
}

render() {
  return (
    <form>
      <input name="firstName" onChange={this.handleInputChange} />
      <input name="lastName" onChange={this.handleInputChange} />
    </form>
  );
}
```
**[⬆ Go to top](#table-of-contents)**

### React without JSX
```javascript
// This two elements are similar :
const element = (
  <h1 className="heading">
    Hello!
  </h1>
);

const element = React.createElement(
  'h1',
  {className: 'heading'},
  'Hello!'
);
```
**[⬆ Go to top](#table-of-contents)**

### Typechecking props with PropTypes
```javascript
// Use PropTypes
import PropTypes from 'prop-types';
```

```javascript
// Prop is an optional array
MyComponent.propTypes = {
  optionalArray: PropTypes.array,
};
```

```javascript
// Prop is an optional boolean
MyComponent.propTypes = {
  optionalBool: PropTypes.bool,
};
```

```javascript
// Prop is an optional function
MyComponent.propTypes = {
  optionalFunc: PropTypes.func,
};
```

```javascript
// Prop is an optional number (integer, float...)
MyComponent.propTypes = {
  optionalNumber: PropTypes.number,
};
```

```javascript
// Prop is an optional object
MyComponent.propTypes = {
  optionalObject: PropTypes.object,
};
```

```javascript
// Prop is an optional string
MyComponent.propTypes = {
  optionalString: PropTypes.string,
};
```

```javascript
// Prop is an optional symbol
MyComponent.propTypes = {
  optionalSymbol: PropTypes.symbol,
};
```

```javascript
// Prop is an optional node (numbers, strings, elements, array, fragment)
MyComponent.propTypes = {
  optionalNode: PropTypes.node,
};
```

### Fetch datas
```javascript
// Use componentDidMount hook with fetch
class PostsList extends Component {
  constructor(props) {
    super(props);
    this.state = {posts: []};
  }

  componentDidMount() {
    fetch('https://example.com/posts')
      .then(response => response.json())
      .then(data => this.setState({ posts: data.posts }));
      .catch(error => console.log(error));
  }
}
```

```javascript
// Use Axios library to fetch datas
import axios from 'axios';

componentDidMount() {
  axios.get('/post', {
    params: {ID: 123}
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
}
```
