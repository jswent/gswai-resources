## Bullet requirements

```
- Anonymous vs require check-in
   - Check-in: fill in name, email, etc.
   - Anonymous: no info required
- Basic Questions Supported
   - Text (variable length)
   - Number
   - Multiple Choice
- Live poll vs async
   - Real-time communication
- Results shown vs hidden
   - Live: option to show results after question closed or proceed immediately
   - Async: option to show poll results at end or hide
- Login for Admin only
   - CRUD Polls
   - Open/Close Polls
- Misc: English only.

```

## PRD prompt

```
I want you to put together a product spec (not engineering, this should focus
on product functionality - a PRD) for the product given the following bullet
points. Do not be overly verbose or overcomplicate things. You can put this
spec in the [YOUR REPO] directory.
```

## Implementation plan prompt

```
put together a high-level implementation plan for V1. you should act as an
engineering manager, so you don't need to go into specific technical detail but
you should outline each milestone and success criteria. as an engineering
manager, you should make sure the plan includes defining interfaces and
building the foundation first such that other work can be parallelized among
developers and integrating at logical points.
```

## Implementation prompt (hands off)

```
Look at the [YOUR REPO] directory which contains a template for the
demo app I want to build for my workshop class, as well as PRD and
implementation plan in the docs/ directory. I want you to act as an engineering
manager and coordinate a team of developers to implement the v1 product as
outlined. You should treat me as the product owner. You should aim to resolve
trivial ambiguities yourself and only prompt me for critical design decisions.
You should treat this as a real world engineering exercise and use standard
industry engineering management practices.
```
