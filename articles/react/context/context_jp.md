## Context
ContextはReactのコンポーネント間でデータを渡すための方法を提供します。
propsを介して親から子に渡す必要がなくなります。

## useContext
下記のコードはブラウザに"Jun Ueno"と表示します。
1. コンテキストを作成します。
2. コンポーネントをコンテキストプロバイダでラップします。
3. コンポーネントを使用します。

```js
import React, { useContext } from 'react'

// 1. コンテキストを作成します。
const MyNameContext = React.createContext("")

const App: React.FC = () => {
  return (
    // 2. コンポーネントをコンテキストプロバイダでラップします。
    <MyNameContext.Provider value="Jun Ueno">
      <Second />
    </MyNameContext.Provider>
  )
}
const Second: React.FC = () => {
  return (
    <>
      <Last />
    </>
  )
}
const Last: React.FC = () => {
  // 3. コンポーネントを使用します。
  const myName = useContext(MyNameContext)
  return (
    <>
      <div>{myName}</div>
    </>
  )
}

export default App
```

## 参照
https://ja.reactjs.org/docs/context.html   
https://ja.reactjs.org/docs/hooks-reference.html#usecontext