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
