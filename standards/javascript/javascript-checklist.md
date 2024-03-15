## Javascript

### Variables
Our choice of variable syntax is based on what is immutable and what is explicit
- We use `const` as default when declaring variables
- We avoid using `let` unless absolutely necessary

### List/object manipulation
We prefer the functional way of manipulating lists and objects. As such we put priority in using immutable and explicit functions
- We avoid for loops
- We prefer the functional style for iterations (`map`, `reduce`, `find`)
- We prefer immutable versions of operations (e.g. `...` instead of `.push`, `.slice` instead of `.pop`)

### Promises
Promises should be written such that they are easy to understand, trace, and debug
- We make sure to catch rejected promises and provide clear error messages
- We avoid mixing promise chains (`.then`, `.catch`) and `async`/`await` syntax in the same function

## React

### Components
Class components tend to have a lot of implicit behavior that can cause confusion in the dev process hence we avoid it. We also adopt component based thinking to divide applications into clear parts.
- We prefer functional components over class components
- We prefer to keep reusable components stateless (dumb components)
- We prefer to put state in one place in a parent container (smart component) that passes data to multiple dumb components.
- We extract non UI logic out of components

### Testing
We generally follow the philosophy of [testing library](https://testing-library.com/) where we try to test our components as close as possible to how a user uses them
- We test components based on visible interactions
- We avoid testing implementation details (e.g. state, variable names)
- We prefer to mock 3rd party functions (e.g. library, API) using dependency injection
- We use `data-testid` as a last resort

## Typescript

### Type Declarations
We write types that are as explicit and reusable as possible
- We avoid using `any` as much as possible
- We apply generics for repeating types
- We split nested types into their own types
- We put reused types in external files
- We put explicit return types for function

### Type over interface
We generally prefer to use `type` over `interface` because type is more flexible and avoids declaration merging which is an implicit behavior that can be cause unexpected behavior for those unaware
