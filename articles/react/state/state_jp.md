## State
Reactでは、stateはコンポーネントに保存されるデータを指します。
時間とともに変化するデータを保存するために使用されます。
例えば、ボタンがクリックされた回数を保存したい場合、stateを使用できます。

## useState
useStateは、コンポーネントにローカルstateを追加するためのフックです。
stateデータは、コンポーネントのpropsに保存されます。
つまり、他のコンポーネントからstateを参照することはできません。

## 簡単なuseStateの使用例

useState has __only one argumemnt__, and it's the initial value of the state.
For example, the simple code below, uesState has an argument `0`. So variable'count' has '0' as initial value.

useStateは__1つの引数__しか持ちません。これはstateの初期値です。   
例えば、下記のコードでは、useStateに`0`が渡されています。そのため、変数`count`は`0`を初期値として持ちます。   

配列の分割代入を使うことで、state変数に異なる名前を付けることができます。(`[count, setCount]`)   
stateをセットする関数の名前には、`set`を使います。つけなくてもエラーになりませんが、慣習的に`set`を使います。   
もし、最初の引数が`name`なら、2番目の引数は`setName`になります。   

~~~jsx
import React, { useState } from 'react';

function Example() {
  // 変数countを宣言します。これはstate変数です。
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

## 1つのコンポーネントで複数のuseStateを使用する
1つのコンポーネントで複数のuseStateを使用することができます。

~~~jsx
function ExampleWithManyStates() {
  // 複数のstate変数を宣言します。
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
~~~

## 参照

https://reactjs.org/docs/hooks-overview.html