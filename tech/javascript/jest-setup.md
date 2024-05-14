# Jest Setup

Jest is a testing framework we use to write tests for features written in Javascript. Jest is designed to be fully functional with zero config but we also have some recommended config to set it up such that it fits our standards.

## Installation

The most basic installation is as simple as adding the library:

```bash
yarn add jest
```

When working with Javascript, it's also standard practice to use typescript for better safety so we also install that along with ts-jest which provides better support for typescript.

```bash
yarn add typescript ts-jest
```

We tend to use javascript more for frontend work and so we need a jest environment that is closer to the browser. Hence we install libraries for jsdom

```bash
yarn add jest-environment-jsdom
```

## Configuration

To store configuration, create a `jest.config.js` file in the root of the project. We recommend to set at least these configurations and you can add more depending on project needs.

```javascript
module.exports = {
  // Add local code as source to look for when importing
  moduleDirectories: ['node_modules', 'app/javascript'],
  // File extensions used in codebase. Since most projects use typescript it's recommended to declare those first.
  moduleFileExtensions: ['ts', 'tsx', 'js', 'json', 'jsx', 'node'],
  // Use a typescript ready preset for easier integration
  preset: "ts-jest",
  // Recommended especially for projects that are not pure JS. Replace accordingly.
  roots: ['<rootDir>/app/javascript'],
  // Important for frontend JS code to have access to most browser behaviors when testing. If pure backend JS code (e.g. API), use node instead
  testEnvironment: "jsdom"
}

```
