# Lifecycle Methods

One of the significant challenges you encounter when embracing stateless functional components is the fact that you no longer have access to a backing instance with lifecycle methods. If you want to perform operations in hooks like `componentDidMount` or `shouldComponentUpdate` you have to use a class-based component.

One thing you may also want is the ability to reuse lifecycle method logic across multiple components. With `recompose`, you can interact with a class-based backing instance in a functional and composable way!

## Portable Lifecycles

