# Handling Events

One of the hidden performance issues in the `render()` function of our components is event handlers that are re-created every time the component is rendered. Since the prop is changed on every render, your application can't take advantage of any pure rendering optimizations. Code in `shouldComponentUpdate()` that relies on equality is effectively useless.

## "Immutable" Event Handlers

Recompose provides a great utility to handle events, providing props to the event handlers via a closure and preserving the identities of the functions themselves. The `withHandlers` function takes an object and creates props for each key. The values are functions that take the props and return another function. This function takes the event and handles it. Here's an example:

```js
// container.js
import {connect} from 'react-redux'
import {compose, withHandlers} from 'recompose'

import {actions} from './actions.js'

export const withMyActionHandlers = compose(
  connect(mapStateToProps, {
    myAction: actions.myAction,
  })
  withHandlers({
    onClick: props => event => {
      event.preventDefault()
      props.myAction(event.target.value)
    },
  })
)
```

```js
// component.js
import React from 'react'
import {withMyActionHandlers} from './container.js'

type Props = {
  onClick: () => void,
}

export default function MyComponent (props: Props) {
  return (
    <button onClick={props.onClick}>Click me!</button>
  )
}
```

## API

For more details, visit the API documentation:

* [`withHandlers`](api/withhandlers.md)
