## Context
Context in React.js provides a way to pass data through the components without props.   
We can avoid to pass props again and again. (Parent to child via props)   

## useContext
Code below shows "Jun Ueno" in Browser.   
1. Create a context   
2. Wrap the component with the context provider   
3. Use the component   

```js
import React, { useContext } from 'react'

// 1. Create a context
const MyNameContext = React.createContext("")

const App: React.FC = () => {
  return (
    // 2. Wrap the component with the context provider
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
  // 3. Use the component
  const myName = useContext(MyNameContext)
  return (
    <>
      <div>{myName}</div>
    </>
  )
}

export default App
```

## Reference
https://ja.reactjs.org/docs/context.html   
https://ja.reactjs.org/docs/hooks-reference.html#usecontext