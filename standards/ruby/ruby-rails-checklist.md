Ruby
Classes and Objects
As much as possible we want our classes to be modular and reusable. We also try to avoid persistent state to keep things immutable.
We avoid class variables and shared state
We apply the SOLID principles when writing classes
Inheritance
Generally we avoid using inheritance because it's hard to pull off correctly and can lead to confusing hierarchies.
We avoid more than 1 level of inheritance
We use inheritance only for is a relationships
We apply composition instead of inheritance for has a relationships
Tests
We generally use RSpec to write ruby tests and make use of its grouping mechanisms to provide clear tests.
We group test scenarios using clearly written context blocks
We group methods to test using describe blocks
We avoid instance variables in tests
We apply fixtures when setting up complex data
We mock dependent classes when using composition
We stub API responses with something like webmock
Rails
Models
Generally we try to avoid model mechanisms that can have unexpected behaviors.
We avoid action hooks (e.g. after_save, after_commit) because of unpredictable behaviors
We avoid enums because they are an additional layer for something that can be done in a simpler way
We avoid default scopes
Associations
As part of db optimization, we need to make sure that associations are properly modeled to keep them easy and fast to query.
We apply polymorphic associations only on small data sets
Transactions
When updating multiple dependent data it's important to provide a graceful rollback in case something goes wrong. To make it work with rails we need to have good control over exceptions.
We prefer to make our methods raise inside transactions to trigger rollbacks
We name our dangerous methods with a bang (!)
Routing
We prefer routing that is straightforward and easy to trace.
We apply clear namespaces and aliases when needed
We avoid more than 3 levels of nested routes
Controllers
The main role of controllers is routing and redirection. When too many things are happening in a controller they become harder to understand and debug (fat controller) so we try to keep them simple.
We make RESTful controller actions
We apply controller filters to DRY up repeating actions (after_action, around_action, before_action)
We apply strong parameter checks to check form data before saving
We prefer to move logic to service objects to avoid "fat controllers"
We rescue exceptions to prevent pages from breaking
Views
Views should be small, manageable and reusable to make them easier to maintain and debug.
We extract complex display logic to view helpers
We apply reusable templates with yield and content_for
We prefer to split big views into manageable partials
We apply the facade pattern when there are too many instance variables
Tasks
When working with data it's important to apply a form of pagination to prevent overwhelming the system, especially with large data sets.
We prefer to use rake tasks to modify sets of data instead of data migrations
We apply batching strategies for updating large chunks of data
We use background jobs for dealing with long running tasks
Tests
For rails tests we prioritize runtime and proper separation of concerns.
We avoid testing controllers except when they have complicated routing or redirection logic, because these run slow
We avoid testing controller action logic. Any complicated logic should be extracted into service objects then tested separately
We prefer to use request specs when testing API controllers

