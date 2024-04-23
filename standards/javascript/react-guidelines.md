# React Guidelines

This is the MG way to write react code. Generally we want react components to be simple to understand and easy to reuse.

## Prefer functional components over class components

Previously the practice was to use functional components for stateless components and use class components for stateful components. However, with the arrival of React Hooks, we rarely use class components now. We prefer functional components for the following reasons:

1. It helps keep things consistent. Previously we would have to switch between two paradigms of functional and object oriented programming, which made refactors challenging and sometimes caused confusion (e.g. `this` in classes). By sticking with functional components we can have behavior that is consistent and in line with our JS standard of going functional.
2. It makes components lighter. Class components would usually inherit all behaviors and apply the whole lifecycle immediately while functional components can start basic and get expanded with these behaviors progressively, through hooks.

## Keep reusable components stateless

Components with state tend to be coupled to specific behaviors and become less flexible to reuse. When creating new components we should start stateless and only add state when needed (More info on state in the next point).

## Keep shared state in a container

## Extract non UI logic out of components
