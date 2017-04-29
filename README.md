<div style="text-align: center;"><img src="assets/recompose.png"  />
</div>

# Docs for Humans: Recompose

[Recompose](https://github.com/acdlite/recompose) is a toolkit for creating composable pipelines of higher order components. It allows you to easily separate your logic from your components, creating re-usable building blocks. You can use it to drive your presentational components on any platform React supports.

Recompose was created by [Andrew Clark](https://github.com/acdlite), and you can find more information about it on [the official repository](https://github.com/acdlite/recompose).

This is the first in a series of in-depth documentation sites created by [Ecliptic](http://ecliptic.io) for popular libraries in the functional front-end development ecosystem. One of the most challenging thing for a new developer getting started in an unfamiliar landscape is finding detailed documentation for the wealth of tools that are available. In the functional programming world especially, it's very common for new developers to come across vital tools that have almost no documentation. "Read the code!" taunts the README file, but newcomers need guidance, advice, and examples to truly understand how to use a tool effectively.

We're hoping to demystify some of the most outstanding tools in the front end ecosystem, and help teams get up to speed quickly on effective architectures.

## Why Recompose?

One of the great strengths of React and JSX is the way it allows you to separate concerns in your user interface in a more modular and obvious way. Instead of grouping together all of your styles and all of your markup and all of your behavior - you can separate your application into easily understandable components that include only the markup, style, and behavior they need in one easy-to-maintain place.

In addition, with the use of higher-order components you can decouple your components even further - separating your business logic and API integration from your presentation and style. With higher-order components you can manipulate props, handle events efficiently, dynamically control rendering, and optimize performance.

If you make heavy use of these patterns, you'll find yourself writing the same boilerplate over and over. If you constrain yourself to stateless functional components as many in the FP community do, you may find yourself missing the backing instance of ES6 classes. You may even run into tricky performance issues from inefficient event handlers.

## Lodash for React

Andrew calls Recompose "Lodash for React", and that's a fitting title! Recompose provides a set of functional tools for creating composable higher-order components, most often used in a functional "pipeline" with Recompose's implementation of `compose`.

Take a look at the "Use Cases" in the Table of Contents to learn more about the various ways to use Recompose to construct higher-order components for your application. You can also review the full API with minimal examples of each function, and "Recipes" from the community highlighting the ways that they have used Recompose to build composable logic for React.