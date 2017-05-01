# Local State

When using stateless functional components, you don't have a backing instance to reach out to with `this`. Class-based React components are [object instances](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects), which means you can access other properties on that object using [`this`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this). When you switch to stateless functional components, you no longer have access to `this.state` or `this.setState`.

## Simple state managers

Recompose introduces a couple of tools for managing local state for your functional components. The first of those is `withState`, which manages a single piece of state. It is often used with the [`withHandlers`](handling-events.md) utility.

The following example is a select menu that only renders its children when the handle is clicked, toggling it to open:

```js
// SelectMenu.js
import React from 'react'
import {compose} from 'recompose'
import {withOpenState} from './formUtils.js'

type Props = {
  isOpen: boolean,
  children: any,
  toggleOpen: (event: Event) => void,
}

function SelectMenu (props: Props) {
  return (
    <div>
      <div className="handle" onClick={props.toggleOpen} />
      {props.isOpen && props.children}
    </div>
  )
}

export default compose(
  withOpenState,
)(SelectMenu)
```

```js
// formUtils.js
import {compose, withState, withHandlers} from 'recompose'


export const withOpenState = compose(
  withState('open', 'setOpen', false),
  withHandlers({
    toggleOpen: props => props.setOpen(!props.open),
  })
)
```

**Incoming props**

```js
{
  children: // ...
}
```

**Outgoing props**

```js
{
  open: false,
  setOpen: (open: boolean) => {},
  toggleOpen: () => {},
  children: // ...
}
```

**Rendered JSX**

```html
<div>
  <div className="handle" />
</div>
```

When the "handle" is clicked, the `toggleOpen` event handle calls the `setOpen` function, setting it to the opposite of whatever `open` is at the moment. This will cause whatever was passed in as `children` to be rendered, now that `open` is `true`.

The `withState` utility manages the value of `open`, updating it with the value passed to `setOpen`.

## Local reducers

For more complex local state, Recompose includes the `withReducer` utility. This sets up a local reducer that works very similarly to how [Redux](http://redux.js.org) does.

```js
import React from 'react'
import {compose, withReducer, withHandlers} from 'recompose'

type Props = {
  count: number,
  handleUp: (event: Event) => void,
  handleDown: (event: Event) => void,
}

function Counter (props: Props) {
  return (
    <div>
      {props.count}
      <button onClick={props.handleUp}>Up</button>
      <button onClick={props.handleDown}>Down</button>
    </div>
  )
}

const counterReducer = (count, action) => {
  switch (action.type) {
    case INCREMENT:
      return count + 1
    case DECREMENT:
      return count - 1
    default:
      return count
  }
}

export default compose(
  withReducer('counter', 'dispatch', counterReducer, 0),
  withHandlers({
    handleUp: props => () => props.dispatch({type: 'INCREMENT'}),
    handleDown: props => () => props.dispatch({type: 'DECREMENT'}),
  })
)(Counter)
```

## API

For more details on managing local state with Recompose, take a look at the API docs for the following utilities:

[`withState`](api/withstate.md)
[`withReducer`](api/withreducer.md)