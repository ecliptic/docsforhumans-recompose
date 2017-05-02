# withHandlers

`withHandlers` allows you to create **"handlers,"** which are functions that do things in response to DOM events being triggered \(or synthetic events, in the case of React.\) These handler functions accept your base component's `props` as their first argument and can accept the `event` argument \(which represents the data collected from the triggered event\) as well as multiple values passed to the handler from your `onEvent` property.

Handlers created with `withHandlers` are passed to your base component as **immutable props.** This means, no matter how many times your component re-renders or how much your state changes, their identity remains the same. This fixes an issue with a new handler being created on every single re-render, breaking `shouldComponentUpdate` optimizations and causing possible memory leaks with event listeners. This is why you should use `withHandlers` to create your handlers instead of `mapProps` or `withProps` , which create new handlers every update.

## Flow Type

```js
withHandlers(
  handlerCreators: {
    [handlerName: string]: (props: Object) => Function
  } |
  handlerCreatorsFactory: (initialProps) => {
    [handlerName: string]: (props: Object) => Function
  }
): HigherOrderComponent
```

## Examples

### Creating "onEvent" Handlers

**Defining handler in recompose**

```js
withHandlers({
  handleClick: props => event => {
    console.log(event)
    alert('<div> was clicked!')
    props.doSomething()
  },
})
```

**Calling handler in base component**

```js
class MyComponent extends Component {
  static propTypes = {
    handleClick: PropTypes.func, 
  }
  render () {
    const {handleClick} = this.props
    return (
      <div onClick={handleClick} />
    )
  }
}
```

### Creating "onEvent" Handlers With Arguments

**Defining handler with arguments in recompose**

```js
withHandlers({
  handleClick: props => (value1, value2) => event => {
    console.log(event)
    alert(value1 + ' was clicked!')
    props.doSomething(value2)
  },
})
```

**Calling handler with arguments in base component**

```js
class MyComponent extends Component {
  static propTypes = {
    handleClick: PropTypes.func, 
  }
  render () {
    const {handleClick} = this.props
    return (
      <div onClick={handleClick(value1, value2)} />
    )
  }
}
```

### Creating "addEventListener" Handlers

**Defining handler in recompose**

```js
withHandlers({
  handleResize: props => event => {
    console.log(event)
    alert('Window was resized!')
    props.doSomething()
  },
})
```

**Calling handler in event listener**

```js
componentDidMount () {
  const {handleResize} = this.props
  window.addEventListener('resize', handleResize)
}

componentWillUnmount () {
  const {handleResize} = this.props
  window.removeEventListener('resize', handleResize)
}
```



