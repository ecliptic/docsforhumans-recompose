# withPropsOnChange

Works like [withProps](api/withprops.md), but it only executes when the specified incoming props are changed. This is a performance optimization that helps ensure that expensive computations are only done when needed.

The first argument can either be an array of incoming key names to watch, or a function that takes the current and next props and returns a boolean that determines whether the function is executed.

**Flow type:**

```js
type withProps = (
  propsMapper: (ownerProps: Object) => Object
) => HigherOrderComponent
```

**PureScript type:**

