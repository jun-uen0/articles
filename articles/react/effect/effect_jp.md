## Effects
データの取得、購読、DOMの手動変更などをコンポーネントから行うことができます。   
Reactでは、これらの操作を「副作用」と呼び、短く「エフェクト」と呼びます。   
そして、これらの副作用を実行するためにはuseEffectを使用する必要があります。   

## useEffect
下記のコンポーネントは、ReactがDOMを更新した後にタイトルを設定します。   
コンポーネントがマウントされた後にタイトルが更新されていることがわかります。   

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

「クリーンアップ」は、実行後にエフェクトを行うことができます。   

```jsx
useEffect(() => {
  ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
  return () => {
    ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
  };
})
```
1つのコンポーネントでuseEffectを複数回使用することもできます。   

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

useEffectを使用することで、コードを整理することができます。   
useEffectを使用しない場合は、コードを複数の関数に分割する必要があります。   

## 参照
https://reactjs.org/docs/hooks-overview.html