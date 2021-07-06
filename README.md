# Setup Basic App - Create React App

## create-react-app

Create React App is a fantastic tool to spin up a basic React App. It includes several useful libraries that allow for rapid development and efficient coding. Let's use it now to setup up a new app.

- Make sure you are in the `appdev-week1-todolist` folder.
- Run `npx create-react-app .` 

*If you want `create-react-app` to dynamically create the root directory for you, you can run `npx create-react-app <app-name>`*

And that's it! We now have a basic React App. We can go ahead and run the app right away.

### Run `npm start`.

![Image](/tutorial/app_basic.png)

As the message states, we can make changes to `App.js` to update the page. Let's make a few changes.

### Edit `src/App.js`
``` javascript
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Hello World!
        </p>
      </header>
    </div>
  );
}

export default App;
```

So we've removed some unnecessary links, and changed the text. Let's save and update the site.

![Image](/tutorial/app_helloWorld.png)

Cool right?

For our Todo App, we are going to want to have a list of Todos, so let's go over making a new component.


## Basic Component
- Create a folder, `components`
- Create a new file, `List.js`

### Edit `List.js`
``` javascript
import React from 'react'

function List() {
    return (
        
    );
}

export default List;
```

Here's our basic component. We are importing our necessary `React` library, defining our `List` component, and exporting it for use in `App.js`.

Let's think about this a bit. We are going to have a list of items, so let's define an array to hold that list, and make up some entries.

``` javascript
const itemList = ["Get milk", "Buy Amazon", "Take over the world"];
```

Now let's render this list by mapping each item in the array to a `<p>` tag.

### Edit `List.js`
``` javascript
import React from 'react'

function List() {
    const itemList = ["Get milk", "Buy Amazon", "Take over the world"];

    return (
        itemList.map((item) => (
            <p>{item}</p>
        ))
    );
}

export default List;
```

Great! We've created our first custom component! Now we need to import it into `App.js` and use it.

### Edit `App.js`
``` javascript
import logo from './logo.svg';
import './App.css';

import List from './components/List';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <List />
      </header>
    </div>
  );
}

export default App;
```

Now save, and reload the site.

![Image](/tutorial/app_withList.png)

Awesome! But that's just the start. We can make our component more dynamic using `props`.

## Component Props

Okay, so we have our `List.js` component, but it's not very dynamic. It just takes the array we specified and spits out each item as text. We can move the array out of the `List` component and provide it as a `prop` instead.

### Edit `List.js`
``` javascript
import React from 'react'

function List(props) {
    const { itemList } = props;

    return (
        itemList.map((item) => (
            <p>{item}</p>
        ))
    );
}

export default List;
```

Now our `List` component is going to be looking for a `prop` called `itemList` that contains an array. We will provide that prop when we use the component.

``` javascript
<List itemList={["Get milk", "Buy Amazon", "Take over the world"]}/>
```

Let's add this to `App.js`.

### Edit `App.js`
``` javascript
import logo from './logo.svg';
import './App.css';

import List from './components/List';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <List itemList={["Get milk", "Buy Amazon", "Take over the world"]}/>
      </header>
    </div>
  );
}

export default App;
```

What this allows us to do is reuse our `List` component for any given array. Let's add another `List` component.

``` javascript
<List itemList={["Get bread", "Get eggs"]} />
```

![Image](/tutorial/app_2lists.png)

Now our component is dynamic! All we need to do is get a list of items as an array, and we can use our component to list the items out.

...But we can go deeper

## Going Deeper

![deeper](/tutorial/deeper.gif)

Let's make another new component

`components/Item.js`
``` javascript
import React from 'react';

function Item(props) {
    const { item } = props;

    return (
        <p>{item}</p>
    );
}

export default Item;
```

And import and use this component in place of `<p>{item}</p>` in our `List` component.

### Edit `List.js`
``` javascript
import React from 'react';
import Item from './Item';

function List(props) {
    const { itemList } = props;

    return (
        itemList.map((item) => (
            <Item item={item} />
        ))
    );
}

export default List;
```

Now we have an `Item` component that we can customize. For example, we can give the item a different background when the user mouses over.

### Edit `Item.js`
``` javascript
import React from 'react';

function Item(props) {
    const { item } = props;
    const [bg, setBg] = React.useState('');

    const handleMouseOver = () => {
        setBg('red');
    }
    const handleMouseOut = () => {
        setBg('');
    }

    return (
        <p 
            onMouseOver={handleMouseOver} 
            onMouseOut={handleMouseOut} 
            style={{backgroundColor: bg}}
        >
            {item}
        </p>
    );
}

export default Item;
```

![item](/tutorial/app_customItem.gif)

Or we can add input to each item.

### Edit `Item.js`
``` javascript
import React from 'react';

function Item(props) {
    const { item } = props;
    const [isChecked, setIsChecked] = React.useState(false);

    return (
        <div>
            <input
                type="checkbox"
                checked={isChecked}
                onChange={() => setIsChecked(true)}
            />
            <label>{item}</label>
        </div>
    );
}

export default Item;
```

![item](/tutorial/app_inputItem.gif)


Voila!