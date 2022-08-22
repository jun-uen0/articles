## useState

useState is a hook that lets we add a local state to our component.
Where is state data? It is stored in the component's props.
Which means we can not refer state from other components. But we can call the function (Ex. Example()) to use the state.

## Simple useState

useState has __only one argumemnt__, and it's the initial value of the state.
For example, the simple code below, uesState has an argument `0`. So variable'count' has '0' as initial value.

You can declare different names to the state variables by using array destructuring. (`[count, setCount]`)
It's very common to use 'set' as the name of the function that sets the state. If the first argument is 'name', then the second argument is 'setName'.

~~~jsx
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
~~~

## Use useState multiple times in the same component

You can use useState multiple times in the same component.
~~~jsx
function ExampleWithManyStates() {
  // Declare multiple state variables!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
~~~

## Reference

https://reactjs.org/docs/hooks-overview.html