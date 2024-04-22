# React Guidelines

This is the MG way to write react code. Generally we want react components to be simple to understand and easy to reuse.

## Prefer functional components over class components

Previously the practice was to use functional components for stateless components and use class components for stateful components. However, with the arrival of React Hooks, we rarely use class components now. We prefer functional components for the following reasons:

1. It helps keep things consistent. Previously we would have to switch between two paradigms of functional for function components and OOP for class components, which made refactors challenging and sometimes caused confusion. By sticking with functional components we can have consistent behavior that is easier to understand.
2. It makes components lighter. Class components would usually get all behaviors and apply the whole lifecycle immediately while functional components can start light and be expanded with these behaviors through hooks progressively.

## Keep reusable components stateless

## Keep shared state in a container

## Extract non UI logic out of components
