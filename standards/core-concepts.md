# Core Concepts
This is a collection of the core ideas, practices and philosophies that we follow when building software. It is the basis of our standards and practices, and is our answer to the question "What makes good code?". Each section provides an explanation of why we value these concepts and a few bullet points of how to explain or gain appreciation of these.

## Immutability
As much as possible we try to minimize data changes to make things less confusing and less error prone. Immutable data is predictable and consistent which makes them easier to debug and helps improve developer experience and code quality.
- Demonstrate a situation where data is updated simultaneously in multiple places (race condition)
- Debug/trace code with values that updated many times

## Mocking
When testing we need to have predictable inputs and predictable outputs. Mocking helps give us more control over dependencies to make them more predictable.
- Run a test with random outputs
- Demonstrate tests that call external APIs on a slow connection
Share a real world example where a test passes on one machine but fails on another

## Clear Tests
A good test should be readable and organized. We write our tests such that scenarios are clearly explained and help readers understand how the code being tested works.
- Present an example where the test description doesn't match what it does
- Navigate through a test where the scenarios are all over the place

## Modularity
Long code can get confusing and can impact maintenance. Code is easier to handle when split into small and manageable parts.
- Navigate through long files (more than 500 lines) where everything is in one place
- Show an example of a modular file structure

## Reusability
As much as possible we try to follow the Don't Repeat Yourself (DRY) principle to keep behavior consistent and lessen maintenance when things change. However, making code reusable needs good planning and technique. Though it's more suitable for OOP, we apply the SOLID principles as general guidelines when writing reusable code.
- Demonstrate a use case where we need to update the same thing across 5 or more files
- Provide an example of badly reused code
- Analyze a piece of code based on the SOLID principles
- Show cases where too much DRY can also be bad.

## Explicit Code
We write code that is straightforward and avoids any implicit "magic" behaviors. We follow the idea of pure functions which have predictable inputs/outputs and do not modify anything outside its scope. When working with settings or config we also value transparency and flexibility to change for specific scenarios. We also prefer to handle data with a clear "shape" with minimal guesswork on its structure. Predictable code is easier to understand and easier to debug.
- Explain the dangers of global scope variables
- Analyze pure functions and impure functions
- Cite a real world example where implicit code caused problems
- Discuss examples of libraries that have unclear config or lack customization options

## Migrations
In general we prefer migrations that are consistent and are a full disclosure of everything that happened in the db. As such we discourage editing or deleting a migration that has already been run outside the local machine. Migrations should also be reversible and easy to roll back. Moreover we avoid migrations that deal with data and stick to migrations that update schema only because of risk of error and potential runtime issues, especially for big data sets.
- Demonstrate de-syncing of db between diff machines caused by edits
- Demonstrate attempt to roll back a migration that wasn't designed to be reversed
- Cite an example of a data migration that errors out

## Transactions
For data that depend on each other, we value consistency and integrity of data. If anything goes wrong, data should be rolled back to a stable state.
- Explain the dangers of inconsistent data (e.g. classic money got debited but not credited scenario)
- Demonstrate case where data errors out because of missing associations/relationships from errors

## DB/Query Optimization
We as engineers, we build our tables and or queries to be scalable and performant at first conception. We use indexing strategies (compound key indexes, primary key, foreign key, unique indexes etc.) as a means of providing better performance and data integrity as well. Knowing which join concepts to utilize in different situations so that we can get the most out of a query. With that, can the query scale and is the query performant enough that it will just need the minimal resources needed. We also decide on the proper data type to use as well as the nullability of the field.
- Provide situations where a column is frequently subjected to a where query and provide the benefits of introducing index on it.
- Cite an example of a slow query and how to fix/update it may it be introduction of indexes, or proper use of join concepts.
- Cite examples for column default values strategies, when to null or when to provide default value
- Provide scenarios when setting up relational tables is better rather than opting to go JSON type fields
- Worth mentioning as well is selecting the Primary key type. When is the proper time to use UUID vs Big Integer. Provide the pros and cons of each.

## Pagination
For data having a number of rows, especially on listings, it's more proper to paginate the data to sizable chunks to avoid overwhelming the user or the system.
- Allow for scenarios where opting to paginate a listing query as early as conception would allow for long-term scalability and better query performance.
- Demonstrate the difference between unpaginated data vs a paginated one
- The same could be considered for whenever we update/migrate huge chunks of rows of data.

## Caching
If an object is frequently accessed and it involves heavy manipulation that takes processing time and resources, we use caching as  means of mitigating these issues.
- Cite examples of when is the best time to use caching, E.g Data collection with a number of rows that doesn't change very often.
- The concept of memoization can be also attributed to be a form of caching.

## Implement Linters
To have an efficient development workflow, we use linters for our projects. These linters will prevent us from pushing badly written or even incorrectly up in our repo. Linters such as Credo for elixir and Rubocop for ruby etc.
- Cite examples for good linters and why we prefer to use that.

