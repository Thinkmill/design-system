# Thinkmill Design System Style Guide

Important Note: This style guide is currently very WIP

---

This style guide documents the standards for building and maintaining design systems we follow at Thinkmill along with explaining the reasoning for our decisions and tooling.

This style guide is intended to be a living representation of how we work with design systems so over time, the recommendations will change as tools and workflows evolve. While the guide is designed holistically, the tools and decisions in this guide can be used independently of each other.

## Concepts

> What is a design system? Purpose, Goals, Reasoning.

> Need to either cover or link out to methodolgy here, see [Dom's first notes on this](https://github.com/Thinkmill/design-system/blob/master/org.md)

### Terminology

- Design System
- Design Tokens
- Theme
- Packs
- Components
- Foundations

# Design Tokens

## Global Tokens

## Packs

# Theming

# Components

Components encapsulate functionality that renders a `view` with `styles` based on a `state`.

`(state) => ({ styles, view })`

We also recognise functional building blocks and controllers that are used by components to manage state, side effects and other concerns.

## Package Structure

## API Design

## State Management

// Todo

> needs content from @jedwatson and @simonswiss.

> There's definitely stuff here from treatise on state we need to clarify

> But beyond that we should also have stuff around the different kinds of UI state (Mike R.)

## Styles

Use [emotion](https://emotion.sh/) with the [css prop](https://emotion.sh/docs/css-prop).

Specify styles in a function that is invoked with the current state of the component and design tokens, and return a css object:

```js
const getButtonStyles = ({ isPressed, tokens }) => ({
  background: isPressed ? 'blue' : 'white',
  text: !isPressed ? 'blue' : 'white',
});

export const Button = ({ children, ...props }) => {
  const { isPressed, events } = useButton(props);
  const styles = getButtonStyles({ isPressed });
  return (
    <button {...props} {...events}>
      {children}
    </button>
  );
};
```

For how to allow style overrides, see [Composition](#Composition)

### Why?

Emotion gives us several benefits over other approaches:

- Styles can be composed directly, without introducing the need for additional components
- Dynamic styles (and the props or state they are based on) can easily be codified in the `getStyles()` function
- Automatic SSR support with no additional server or build configuration required (this is important when publishing packages to npm that should have no understanding of where or how they may be used)

> When to use interpolated styles over css-in-js object?

> Performance notes?

> Best practice for structuring styles in react.

## Spreading props and attributes into Views

## Accessibility

> Resources for best practices around accessibility
> Dom to provide (?)

## Composition

### Render Props

Render props allow us to take control over the key state, attributes and styles of a particular component, while giving the user ownership over the shape of the DOM.

```
const Modal = () => (

)
export default () => (
  <Modal>
    {
      (props, styles) => (
        <select>
      )
    }
  </Modal>
)

```

### Overrides

Overrides allow users to make targeted changes without inheriting complexity

- [Overrides / Flex / Extends] are meant for customisation that fall in the 20% case (advanced usage):
- cssFn for customizing the CSS APPLICATION within a component
- more explicit control over how tokens are applied
  _ i.e. setState in react (either a config object or a more explicit function that is passed previous state)
  _ for example spacing token used in padding instead of margin \* feedback loop with documented 80% case
- A way for users to make stylistic changes that aren’t currently exposed as part of the theming / tokens API

# Documentation

[monorepo style guide](#)
