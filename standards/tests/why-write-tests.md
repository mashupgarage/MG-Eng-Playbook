## Why do we Test?

One of the primary benefits of writing tests is it helps developers catch errors early on in the development process. This reduces the likelihood of introducing bugs into the system and helps ensure that the code is of high quality from the outset.

However, one of the main objections on writing tests is that it can be time-consuming. Writing tests before writing code can seem like an unnecessary step that adds time to the development process but studies have shown that the time saved in debugging and fixing errors more than makes up for the time spent writing tests.

## Benefits on writing tests

It encourages developers to think about the requirements of the code before writing it. This helps ensure that the code meets the needs of the project and avoids unnecessary or extraneous features. By focusing on the requirements first, developers can create code that is both efficient and effective.

## The Mashup Garage way

Here in Mashup Garage, we actually do not solely follow TDD but we require everyone to write a test on every module/feature you worked on. This makes it easier to maintain the code in the future, which can save time and money in the long run.

At a minimum we require to write a tests for core functions implemented like services and helpers in backend. For reactjs, we write tests for each component to atleast ensure it's rendering without issue and testing the callback functions.

## Tools for testing

- [React testing library](/standards/tests/react-testing-library.md)
- [RSpecs for rails](/standards/tests/rspecs.md)
- [Built-in Phoenix testing lirary](/standards/github/phoenix-testing.md)
