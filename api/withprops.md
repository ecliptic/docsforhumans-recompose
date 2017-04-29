# withProps

Merges the current props with whatever the given function returns. This is different from [`mapProps`](api/withprops.md) because it doesn't disregard the incoming props. It merges the outgoing props into the incoming props.

**Flow type:**

```js
type withProps = (
  propsMapper: (ownerProps: Object) => Object
) => HigherOrderComponent
```

**PureScript type:**

```purescript
withProps :: forall ownerProps props.
  (ownerProps -> props) -> HigherOrderComponent ownerProps props
```

## Examples

### Adding props

```js
mapProps(props => {
  return {
    total: props.initialValue + props.change,
  }
})
```

**Incoming Props**

```js
{
  initialValue: 10,
  change: 5,
}
```

**Outgoing Props**

```js
{
  initialValue: 10,
  change: 5,
  total: 15,
}
```
