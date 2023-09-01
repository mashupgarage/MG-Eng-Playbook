# Javascript Guidelines

The Javascript language is continuously changing and adding more ways to do things, which have their own nuances and sometimes weird behavior. To mitigate possible confusion we have a set of standards based on our years of experience writing Javascript. These ideas can serve as guiding principles to rules we apply in linters like eslint.

## Go Functional

There are several paradigms used in Javascript: procedural, object oriented, and functional. At MG we prefer to write Javascript towards the functional style. JS code written should generally follow these rules:

- Avoid mutating or changing values that are already set
- Use pure functions: basically functions that have predictable outputs given certain input and don't have side effects

So when writing code, it's important to always ask "Is this the functional way to do this?".

## Prefer const variables

One functional practice is to avoid changing values, also called mutating, once they are set to make them more predictable and easier to debug. Generally, use const, avoid let, and forget about var.

- ✅ const declaration
    ```javascript
    const myVar = 1
    myVar = 2 // error: Assignment to constant variable.
    const myVar = 2 // error: Identifier 'myVar' has already been declared

    console.log(myVar) // will still be 1
    ```
    Constant variables do not allow reassignment nor redeclaration. This works well to avoid mutating and should be the default way to assign.
- ❌ let declaration
    ```javascript
    let myVar = 1
    myVar = 2
    let myVar = 2 // error: Identifier 'myVar' has already been declared

    console.log(myVar) // will be 2
    ```
    Let allows reassignment but not redeclaration. There may be a few cases where let is better to use but generally if you're reassigning values, you should rethink your approach.
- ❌ var declaration
    ```javascript
    var myVar = 1
    myVar = 2
    var myVar = 3

    console.log(myVar) // will be 3
    ```
    Var allows both reassignment and redeclaration. This can potentially cause bugs and rarely will `var` be preferred over `const` and `let`. You can forget about `var``.

## Use pure versions of functions

For JS code to functional, it needs to use pure functions. When using predefined functions from JS libaries, as much as possible use functions that don't modify the original thing.

- ❌ push()
    ```javascript
    const arr = [1,2,3]
    arr.push(4) // [1,2,3,4]

    console.log(arr) // [1,2,3,4]
    ```
- ✅ spread operator (...)
    ```
    const arr1 = [1,2,3]
    const arr2 = [...arr1, 4] // [1,2,3,4]

    console.log(arr1) // [1,2,3]
    ```
