# General Testing Guidelines

Testing is important but can be challenging when not handled well. These are some guidelines we follow to write effective tests, regardless of language.

## Limit testing to project scope

In most cases, we should only test things directly related to the project we're working on. Any plugins, libraries or extensions should not be our concern to test since that should be the author's job. Moreover we don't have control over implementation of external code which means updates can break our tests unexpectedly. Be guided by the following scenarios:
- ✅ any module, class, function, etc in project written by you
- ✅ any module, class, function, etc in project written by your colleague
- ✅ project code that calls external library (e.g. API fetcher)
- ❌ implementation of external libraries or plugins (e.g. GraphQL routing)
- ❌ the internals of languages used in project (e.g. Ruby class implementation)
- ❌ the internals of frameworks used in project (e.g. Phoenix controller implementation)
