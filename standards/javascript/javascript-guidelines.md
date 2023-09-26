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
    ```javascript
    const arr1 = [1,2,3]
    const arr2 = [...arr1, 4] // [1,2,3,4]

    console.log(arr1) // [1,2,3]
    ```
- ❌ pop()
    ```javascript
    const arr = [1,2,3,4]
    arr.pop() // 4

    console.log(arr) // [1,2,3]
    ```
- ✅ slice()
    ```javascript
    const arr = [1,2,3,4]
    const updatedArr = arr.slice(0, arr.length - 1)

    console.log(arr) // [1,2,3,4]
    console.log(updatedArr) // [1,2,3]
    ```
- ❌ sort()
    ```javascript
    const arr = [4,1,3,2]
    arr.sort() // [1,2,3,4]

    console.log(arr) // [1,2,3,4]
    ```
- ✅ spread then sort
    ```javascript
    const arr = [4,1,3,2]
    const updatedArr = [...arr].sort()

    console.log(arr) // [4,1,3,2]
    console.log(updatedArr) // [1,2,3,4]
    ```

## Avoid for loops

For loops are more of a procedural programming style and usually lead to mutable patterns of doing things. They should be avoided in favor of using more modern iteration functions such as forEach, map, or reduce.

- ❌ for loop printing
  ```javascript
  for(let i = 0; i < 5; i +=1) {
    console.log(i)
  }
  ```
- ✅ forEach()
  ```javascript
  [1,2,3,4,5].forEach((item) => {
    console.log(item)
  })
  ```
- ❌ updating array values with for
  ```javascript
  let arr = [1,2,3]

  for(let i = 0; i < 3; i +=1) {
    arr[i] = arr[i] * 2
  }

  console.log(arr) // [2,4,6]
  ```
- ✅ map()
  ```javascript
  const updatedArr = [1,2,3].map((item) => {
    return item * 2
  })

  console.log(updatedArr) // [2,4,6]
  ```
- ❌ combining items with for
  ```javascript
  const arr = [1,2,3]
  let sum = 0

  for(let i = 0; i < 3; i +=1) {
    sum += arr[i]
  }

  console.log(sum) // 6
  ```
- ✅ reduce()
  ```javascript
  const arr = [1,2,3]
  const initialSum = 0

  const sum = arr.reduce((accumulator, item) => {
    return accumulator + item
  }, initialSum)

  console.log(sum) // 6
  ```

## Use a consistent promise style

Promises have become a common way to handle asynchronous code in javascript and there are two key ways: promise chains and async-await. These two styles can actually be used together but we don't recommend it. It's better to be consistent and just stick with one of them, depending on the team's conventions.
- ✅ async-await
  ```javascript
  const fetchPosts = async () => {
    try {
      const posts = await fetch()
      console.log(posts)
    } catch(error) {
      console.error(error)
    }
  }
  ```
- ✅ promise chains
  ```javascript
  const fetchPosts = () => {
    fetch()
      .then((data) => console.log(data))
      .catch((error) => console.error(error))
  }
  ```
- ❌ combination of both
  ```javascript
  const fetchPosts = async () => {
    await fetch()
            .then((data) => console.log(data))
            .catch((error) => console.error(error))
  }
  ```
