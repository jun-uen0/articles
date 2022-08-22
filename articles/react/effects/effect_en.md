## Effects

We can perform data fetching, subscripting, and manually changing DOM from React components.
In React, we call these operation 'side-effects' or 'effects' in short.
And we have to use useEffect to perform these side-effects.

## useEffect

Component below sets the title after React updates the DOM.
You can see the title is updated after the component is mounted.

```jsx
import React, { useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  })
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClock={() => setCount(count+1)}>
        Click here
      </button>
    </div>
  )
}
```

You can "clean up" effects after running them.
```jsx
useEffect(() => {
  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
})
```

You can also use useEffect multiple times in a component.
```jsx
function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }
  // ...
```

You can organize your code by using useEffect.
If you do not use hooks, you have to split your code into multiple functions.

## Reference
https://reactjs.org/docs/hooks-overview.html