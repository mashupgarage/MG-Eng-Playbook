# General Testing Guidelines

Testing is important but can be challenging when not handled well. These are some guidelines we follow to write effective tests, regardless of language.

## Limit testing to project scope

In most cases, we should only test things directly related to the project we're working on. Any plugins, libraries or extensions should not be our concern to test since that should be the author's job. Moreover we don't have control over implementation of external code which means updates can break our tests unexpectedly. Use the following checklist as guide:
- ✅ any module, class, function, etc in project written by you
- ✅ any module, class, function, etc written by your colleague
- ✅ project code that calls external library (e.g. API fetcher)
- ❌ implementation of external libraries or plugins (e.g. GraphQL routing)
- ❌ the internals of languages used in project (e.g. Ruby class implementation)
- ❌ the internals of frameworks used in project (e.g. Phoenix controller implementation)

## Inputs and outputs should be predictable

We don't want tests that randomly pass or fail unexpectedly. This can cause delays in CI pipelines which hinders delivery of updates. As such we need to make tests predictable where given a certain input we are sure of what the output will be. Here are some practices we recommend:

### Always use explicit dates

When we rely on current system date/time we can end up with tests that fail unexpectedly on certain dates. For example we have a function that changes logic at the end of the month. If we rely on system time to test this behavior there's a chance that it behaves different at end of month compared to other days. We need a way to control the date to make things predictable
- ✅ pass date as argument
- ✅ use time tools to set current time (e.g. `travel_to` in rails)
- ❌ use system time (e.g. DateTime.current, Timex.now(), Date())

### Mock external dependencies

Sometimes we may have data or integrations that are external to the class or module we're working on. This can be data from a 3rd party API or a function from a library. We don't have full control over these dependencies like in the case of API it might disconnect during testing which can slow down the test or for a 3rd party function they might update the implementation. Moreover, for an API with payment per use, calling it every test is costly. Hence, we should use an approach called mocking where we replicate the expected behavior of the external dependencies and use those in place of the actual thing. This way we can control the data we receive but still simulate the actual behavior.
