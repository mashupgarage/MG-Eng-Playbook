# Typescript Guidelines

TypeScript is a programming language that builds upon JavaScript by adding static type-checking capabilities. It is often referred to as a "typed superset" of JavaScript.

## Type Annotations

TypeScript type annotations are essential for providing static type checking and improving code quality. Here are some do's and don'ts to consider:

- <b>Use Descriptive Variable Names:</b> Use clear and descriptive variable names. This makes it easier to understand the purpose of the variable and the associated type.

  ```
  ✅ const userName: string = "John"

  ❌ const u: string = "John"
  ```

- <b>Annotate Function Parameters and Return Types:</b> Always annotate function parameters and return types to ensure that the function is used correctly.

  ```
  ✅ function add(x: number, y: number): number {
      return x + y
  }

  ❌ function add(x, y) {
      return x + y
  }
  ```

- <b>Use Union Types for Flexible Variables instead of Any:</b> When a variable can have multiple types, use union types to represent this flexibility.

  ```
  ✅ const result: number | string = calculateResult()

  ❌ const result: any = calculateResult()
  ```

- <b>Use Type Inference When Possible:</b> TypeScript has excellent type inference capabilities. You don't always need to annotate types explicitly. Although the usage is more suitable for primitive types (e.g. number, string, boolean).

  ```
  ✅ const count = 42

  ❌ const count: number = 42
  ```

## Coding Practices

- <b>Comments and Documentation:</b>
  Use comments and documentation to explain complex logic, provide context, and describe the purpose of functions and classes.

  ```
  // Good practice: Comments and documentation
  /**
  * This function calculates the sum of two numbers.
  * @param x - The first number.
  * @param y - The second number.
  * @returns The sum of x and y.
  */
  function addNumbers(x: number, y: number): number {
      return x + y
  }
  ```

- <b>Prefer Type Alias over Interfaces:</b> Use Type alias as much as possible because it's more flexible to use than Interface.

  ```
  ✅ type Age = number

  function userDetails(name: Name, age: Age...) {
    // code here
  }

  const age: Age = 42

  ⚠️ interface Details {
    age: number
  }

  // Not usable in above scenario, you have to refactor your code to apply the interface.
  function userDetails(args: Details) {
    // code here
  }

  const details: Details = {
    age: 42
  }
  ```

- <b>Avoid Mutating Objects:</b> When working with objects, prefer creating new objects over mutating existing ones to prevent unexpected side effects.

  ```
  ✅ const updatedUser = { ...user, age: 35 }

  ❌ user.age = 35
  ```

- <b>Isolate type of nested groups:</b> When working with nested objects, we prefer defining the group in a separate type definition.

  ```
  ✅ type InnerType = {
    subField1: string,
    subField2: string,
  }

  type MyType = {
    field1: InnerType
    field2: string
  }



  ❌ type MyType = {
    field1: {
      subField1: string,
      subField2: string,
    }
    field2: string
  }
  ```
