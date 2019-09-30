# Thinkmill Design System Style Guide

Important Note: This style guide is currently very WIP

---

This style guide documents the standards for building and maintaining design systems we follow at Thinkmill along with explaining the reasoning for our decisions and tooling.

This style guide is intended to be a living representation of how we work with design systems so over time, the recommendations will change as tools and workflows evolve. While the guide is designed holistically, the tools and decisions in this guide can be used independently of each other.

## Concepts

> What is a design system? Purpose, Goals, Reasoning.

"A Design System is an artefact of the culture and collaboration in your company" -- Dom

> Need to either cover or link out to methodolgy here, see [Dom's first notes on this](https://github.com/Thinkmill/design-system/blob/master/org.md)

### Terminology

(all wip and in need of further discussion)

- Design Language

> The collection of design decisions that represent a company, brand or product. Usually includes colour, typography, spacing, language and tone of voice, illustrations and iconography, visual style, and patterns of applying all of these to reference designs.

- Design System

> The composition of components, patterns and processes that is consumable, documented, published to be able to be reusable and scalable in a business domain

- Design Tokens

> Implementation agnostic variables that describe the subset of values core to a design system.

- Theme

> A customisable subset of design decisions that expresses sweeping style changes through the system.

- Packs

> A cluster of design tokens grouped according to how they should be used. See [Packs](#Packs)

- Packages

> A collection of one or more components or utilities, conceptually identifiable as a concern of the design system, documented and published to a package registry.

- Components

> Components encapsulate functionality that renders a `view` with `styles` based on a `state`.
> See [Components](#Components)

- State

> The combination of component that affect the appearance or behaviour of the

- Controllable State

> This is an important concept regarding how state can be optionally provided to a component, along with a callback that is invoked when the state should change. The fallback behaviour is for the component to manage the state and default callback behaviour internally.

- Switches

> Props that can change the appearance and/or behaviour of a component. Often selected from a set of possible values. Examples include appearance or color of a button, first day of the week in a calendar, etc.

# Design Tokens

## Global Tokens

## Packs

# Theming

# Components

> NOTE: Here we describe developing React components for a design system. The principles are largely translatable to React Native projects as well, but other frameworks and technologies are out of scope for our style guide at this time.

> TODO: Review [React Patterns](https://reactpatterns.com) for inspiration - this does a good job of presenting various technical approaches you can take in React, and we can learn from the way it is organised and presented!

Components encapsulate functionality that renders a `view` with `styles` based on a `state`.

`(state) => ({ styles, view })`

We also recognise functional building blocks and controllers that are used by components to manage state, side effects and other concerns.

## Types of Components

_Note that a package in the design system may include one or multiple components, of the following types. Not all components in a package must be exported._

- **Elements**
  - design system components that do not have internally managed state that reflect styles and attributes onto a dom element.
- **Primitives**
  - design system components that do have internally managed state generally only consist of one primary identifiable component.
- **Compound Components**
  - design system components that consist of multiple primitives.
- **Composite Components**
  - components comprised of multiple components some of which are published elsewhere in the design system.

The term "stateful", as applied to components, may mean state that is managed internally by the component or accepted as props.

## Package Structure

> TODO: this needs to go hand-in-hand with some more depth around how documentation and examples are developed and published to make sense.

```
- docs/
- examples/
- src/
  - index.js
  - styles.js
- tests/
- package.json
```

## Types

Use [TypeScript](https://www.typescriptlang.org).

Among other things, it'll help you easily generate [Documentation](#Documentation) for your component APIs.

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

> Performance notes?

> Best practice for structuring styles in react.

## Accessibility

> Resources for best practices around accessibility
> Dom to provide (?)

## Composition

### Spreading props and attributes into Views

> @gwyneplaine I have no idea what to write here

Prop spreading is fine if there is only one primary dom element
Prop spreading is not as fine if you have multiple meaningful dom elements in your component. In these situations it is best to have a more targeted strategy for passing attributes and props down to key elements ([see overrides](#Overrides)).

### Wrapper Components

Wrap components to add features, rather than blowing out the complexity of your low-level components, and their increasing API/prop surface area.

For example, if your basic button takes an `isPressed` prop, and you want to add a toggle button to your design system, you can achieve the effect by creating a wrapping component that manages the toggle state:

```js
const ToggleButton = props => {
  const [toggled, setToggled] = useState(false);
  const handleClick = e => {
    props.onToggle && props.onToggle(e, !toggled);
    setToggled(!toggled);
  };
  return <Button {...props} isPressed={toggled} onClick={handleClick} />;
};
```

This works best when your building-block components accept semantic and granular props with a well thought out API that closely reflects the state(s) the component can be in.

#### Counterpoints

This can get complex if you want to compose multiple components together.

### Render Props

Render props allow us to take control over the key state, attributes and styles of a particular component, while giving the user ownership over the shape of the DOM.

```js
const Modal = () => ()
export default () => (
  <Modal>
    {({ styles, props, containerRef )) => (
      <div ref={containerRef} css={styles} {...props}>
        ...
      </div>
    )}
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

# Analytics

Components exist in a hierarchy. Capture the context of where events are called down through the hierarchy using decorators, then bubble events up to listener components that wrap around the application.

# Publishing and Versioning

> See [monorepo style guide](https://github.com/Thinkmill/monorepo)

# Observability

> See https://twitter.com/kaelig/status/1172579203893456896

# Documentation

> [monorepo style guide](#)

# Definition of Done 

> We should recommend (some derividation of) Emma Wedekind's Component Checklist here.
> https://twitter.com/EmmaWedekind/status/1177248937763311617?s=20

# Development

>

