# mapProps

Replaces the current props with whatever the given function returns.

```js
type mapProps = (propsMapper: (ownerProps: Object) => Object): HigherOrderComponent
```

## Examples

### Replacing Props

```js
mapProps(props => {
  return {
    total: props.initialValue + props.change,
  }
})
```

*Incoming Props*

```js
{
  initialValue: 10,
  change: 5,
}
```

*Outgoing Props*

```js
{
  total: 15,
}
```
