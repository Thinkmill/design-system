# How to get started with Design Systems in an organization

1. [Ask questions and listen](#ask-questions-and-listen)
1. [Define DS team](#define-ds-team)
1. [UI-inventory](#ui-inventory)
1. [Tech-inventory](#tech-inventory)
1. [Grouping](#grouping)
1. [Naming](#naming)
1. [Decisions](#decisions)
1. [Design Tokens](#design-tokens)
1. [Design language](#design-language)
1. [Contribution model](#contribution-model)
1. [Playback session for the company](#playback-session-for-the-company)
1. [Breaking changes](#breaking-changes)
1. [Distribution](#distribution)
1. [Documentation](#documentation)

## Ask questions and listen

- Find out about the progress of the design
- Find out about the progress of a component lib
- Find out if the design already follows a component lib like symbols in Sketch shared with designers
- Find out what the dominate tech stack is on the front end
- Find out about how designers and developers work together
  - What does the handover look like?
- Is there wire-framing, user-research, content guidelines

## Define DS team

Look to make use of the right roles. The best roles for the DS team would be:
- **Designers**
- **Front-end developers**
- **Accessibility experts**
- **Content strategists**
- **Researchers**
- **Product managers**

Find the right people to join from other parts of your company and make them champions.
Not everyone has to be in the team directly to help and be a champion.


## UI-inventory

- Get all components together
- Get all colors together
- Get all text styles together (ignore only color)
- Get all icons together (Iconography and other images)

## Tech-inventory

- Determine the stack(s)
- Find component libs (there are usually a bunch)
- Find out restrictions, eg access to GitHub, npm etc
- Talk to devs in projects and see how they work
- What js solution works best?
- What css solution works best?

## Grouping

Come up with groups of UI bits that make sense from a dev and design perspective.
Make sure you have designers and developers in the room.
If you have a content person please include them, they are exceptionally good at grouping things.

## Naming

Now the hard part: name the groups.
Have a look at theming, consistent naming for priorities like `primary`, `secondary` etc
Make sure you name things semantically so you communicate what a thing is for by it's name.

## Decisions

Note down all decisions and capture the reasons behind them all.

## Design Tokens

Tokenize your Design language.
Create tokens for:
- color
- spacing
- type
- packs

Group things together and name them like `page-headline` would be a pack consistent of:
- `font-family`
- `font-size`
- `line-height`
- `font-weight`

but not `color` or `spacing` as those are different tokens.

## Design language

Try to make your tokens your design language and document it as such.
Explain where things are used and where things are not used.
This should be your first deliverable.

## Contribution model

https://medium.com/eightshapes-llc/team-models-for-scaling-a-design-system-2cf9d03be6a0
How should we collaborate together?
How can issues be raised?
How owns what?

## Playback session for the company

Take your company on the journey by playing back what you learned so far.
Do a session every two weeks and tell them what you got so far, what you explore, what hasn't worked.

## Breaking changes

How will you break your components and communicate the impact of that break?
How will you version things?
What impact will a breaking change have on your consumers?

## Distribution

How do you deliver the DS?
What do your consumers have access to?

## Documentation

Who will you document for?
How will you document?
Where?
