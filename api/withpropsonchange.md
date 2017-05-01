# withPropsOnChange

Works like [withProps](api/withprops.md), but it only executes when the specified incoming props are changed. This is a performance optimization that helps ensure that expensive computations are only done when needed.

The first argument can either be an array of incoming key names to watch, or a function that takes the current and next props and returns a boolean that determines whether the function is executed.

## Flow Type

```js
type withPropsOnChange = (
  shouldMapOrKeys: Array<string> | (props: Object, nextProps: Object) => boolean,
  createProps: (ownerProps: Object) => Object
) => HigherOrderComponent
```

## Examples

### Derive props only when dependencies change

The following higher order component generates the fibonacci sequence out to a length of `props.length` numbers. This isn't something you want to do lightly on each render, so the `fibonacci` prop is *only* recalculated when the `length` prop changes.

```js
withPropsOnChange(['length'], props => {
  const fibonacci = Array
    .apply(0, Array(props.length))
    .reduce((x, y, z) => x.concat((z < 2) ? z : x[z-1] + x[z-2]), [])

  return {fibonacci}
})
```

**Incoming props**

```js
{
  length: 5,
  title: 'Title!',
}
```

**Outgoing props**

The function is always executed the first time the higher order component is rendered, returning these initial outgoing props:

```js
{
  length: 5,
  title: 'Title!',
  fibonacci: [0, 1, 1, 2, 3],
}
```

**Next incoming props**

```js
{
  length: 10,
  title: 'Title!',
}
```

**Outgoing props**

The function **is** executed, returning these new outgoing props:

```js
{
  length: 10,
  title: 'Title!',
  fibonacci: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34],
}
```

**Next incoming props**

```js
{
  length: 10,
  title: 'Other Title!',
}
```

**Outgoing props**

The function is **not** executed since the `length` prop has not changed. It allows the incoming props to flow through and returns the same outgoing `fibonacci` prop as last time:

```js
{
  length: 10,
  title: 'Other Title!',
  fibonacci: [0, 1, 1, 2, 3, 5, 8, 13, 21, 34],
}
```
