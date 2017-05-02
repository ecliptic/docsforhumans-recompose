# Manipulating Props

One of the most fundamental uses for Recompose is to adjust the props coming into your components. A big motivation for this is the separation of business logic from presentation and style.

You often need to transform the values that come into your components as props. The initial way that most React developers handle this is by putting this logic directly into their `render()` method. The drawback to this approach is that it ties this couples this logic directly to the generation of the markup and style. You can't reuse that logic without also reusing that presentation.

If you decide later that you'd like to use that logic somewhere else in your application, or in a React Native or Electron version of your application intended for another platform, you have to reproduce that logic for the new platform.

## Composable logic

Recompose makes it easy to build that logic into reusable higher-order components. Using utilities like [`withProps`](api/withprops.md), you can transform props in a manner that leverages React's convenient hierarchical structure without depending on any rendered DOM or Native elements. Just import your logic and attach it to your "dumb" presentational components to render it on any platform.

```js
// formUtils.js
import {withProps} from 'recompose'

type Props = {
  choices: Array<{text: string, value: string}>,
  selected: string,
}

export const withSelectedText = withProps((props: Props) => {
  const choice = props.choices[props.selected]
  const selectedText = choice
    ? choice.text
    : 'Please select a choice'
  return {selectedText}
})
```

```js
// SelectedText.js
import React from 'react'
import {compose} from 'recompose'
import {withSelectedText} from './formUtils'

type Props = {
  selectedText: string,
}

function SelectedText (props: Props) {
  return (
    <div>{selectedText}</div>
  )
}

export default compose(
  withSelectedText,
)(SelectedText)
```

**Incoming props**

```js
{
  choices: {
    one: {text: 'One!', value: 'one'},
    two: {text: 'Two!', value: 'two'},
    three: {text: 'Three!', value: 'three'},
  },
  selected: 'two',
}
```

**Outgoing props**

```js
{
  choices: {
    one: {text: 'One!', value: 'one'},
    two: {text: 'Two!', value: 'two'},
    three: {text: 'Three!', value: 'three'},
  },
  selected: 'two',
  selectedText: 'Two!',
}
```

**Rendered JSX**

```html
<div>Two!<div>
```

## API

For more details, visit the API documentation for each of the following higher-order function creators:

* [`mapProps`](api/mapprops.md)
* [`withProps`](api/withprops.md)
* [`withPropsOnChange`](api/withpropsonchange.md)