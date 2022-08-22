## Custome hooks

We can create our own hooks.
This is a custom hook that wraps `01_useState.md` and `02_useEffect.md`.
Naming `useFriendStatus`
Tip: Usually cutom hooks are stored at `/hooks` directories in React projects.

```jsx
// /hooks/useFriendStatus.js

import React, { useState, useEffect } from 'react';

function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(friendID, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(friendID, handleStatusChange);
    };
  });

  return isOnline;
}
```

A component that shows the status of friends.

```jsx
// /FriendStatus.tsx

function FriendStatus(props) {
  const isOnline = useFriendStatus(props.friend.id);

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

Another component that show a list of friends
```jsx
// /FriendsList.tsx

function FriendListItem(props) {
  const isOnline = useFriendStatus(props.friend.id);

  return (
    <li style={{ color: isOnline ? 'green' : 'black' }}>
      {props.friend.name}
    </li>
  );
}
```

## Reference
https://reactjs.org/docs/hooks-overview.html