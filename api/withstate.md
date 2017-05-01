# withState

Manages a single state value, providing a function to update the value and accepting an optional default value.

## Flow Type

```js
type withState = (
  stateName: string,
  stateUpdaterName: string,
  initialState: any | (props: Object) => any
) => HigherOrderComponent
```

## Examples

### Simple state

```js
withState('count', 'setCount', 0)
```

**Incoming props**

```js
{}
```

**Outgoing props**

```js
{
  count: 0,
  setCount: (count: number) => {},
}
```

If the `setCount` prop is called like this:

```js
setCount(1)
```

Then the new outgoing props would be:

```js
{
  count: 1,
  setCount: (count: number) => {},
}
```

### Event handlers

The `withState` utility is often combined with [`withHandlers`](api/withhandlers.md) to create simple value setters:

```js
compose(
  withState('count', 'setCount', 0),
  withHandlers({
    incrementCount: props => event => {
      event.preventDefault()
      props.setCount(props.count + 1)
    },
    decrementCount: props => event => {
      event.preventDefault()
      props.setCount(props.count - 1)
    },
  })
)
```

### Dynamic initial values

You can also pass a function as the third `initialState` argument. This function will take the incoming props, and return the initial value for the state manager.

```js
withState('balance', 'setBalance', props => {
  return props.initialBalance - props.totalPurchases
})
```

This would set the initial value of `balance` to the value of `initialBalance` minus the `totalPurchases`.