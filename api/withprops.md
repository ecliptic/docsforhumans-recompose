# withProps

Merges the current props with whatever the given function returns. This is different from [`mapProps`](api/withprops.md) because it doesn't disregard the incoming props. It merges the outgoing props into the incoming props.

## Flow Type

```js
type withProps = (
  propsMapper: (ownerProps: Object) => Object
) => HigherOrderComponent
```

## Examples

### Adding props

```js
withProps(props => {
  return {
    total: props.initialValue + props.change,
  }
})
```

**Incoming props**

```js
{
  initialValue: 10,
  change: 5,
}
```

**Outgoing props**

```js
{
  initialValue: 10,
  change: 5,
  total: 15,
}
```



