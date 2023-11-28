# React Testing Guidelines

Testing React code has a bit of learning curve and can be confusing at times. This is a collection of practices and techniques we adopted through our years of experience working with React JS.

## Test the application like how a user would

We follow the philosophy of [testing library](https://testing-library.com/), which states that tests that are written close to how the application is actually used give more confidence. As developers, our first tendency when testing code is to test it based on internal details we wrote (e.g. variable names, state). However, when users use your application they don't think of these things. They test based on what they see on the screen (e.g. labels, element visibility, number of elements). This discrepancy in approach may potentially cause some test cases to be missed, which we can mitigate by testing in a similar fashion. Additionally, avoiding internal details in tests also make components easier to refactor, which is a characteristic of an effective automated test.

## Apply dependency injection

## Write your components with accessibility in mind

## Add visible loading states

## Use react-select-event to test react-select elements
