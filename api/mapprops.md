# mapProps

Replaces the current props with whatever the given function returns. This means that it disregards the incoming props and completely replaces them with the outgoing props. This is different from [`withProps`](api/withprops.md), which merges the outgoing props into the incoming props.

**Flow type:**

```js
type mapProps = (
  propsMapper: (inProps: Object) => Object
) => HigherOrderComponent
```

**PureScript type:**

```haskell
mapProps :: forall inProps outProps.
  (ownerProps -> props) -> HigherOrderComponent inProps outProps
```

## Examples

### Replacing props

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
  total: 15,
}
```
### Deriving other mappers

You can easily derive other mappers the same way you compose functions in functional programming:

```js
const omitProps = keys => mapProps(props => omit(keys, props))
```

If you're using Ramda or Lodash-FP, the following expression is equivalent because of currying:

```js
const omitProps = compose(mapProps, omit)
```
