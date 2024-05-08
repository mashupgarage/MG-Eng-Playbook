# Ruby/Rails Competencies

# Ruby

## Classes and objects
### Description
Have the understanding of how classes and objects works
### Example
- Able to read, understand and write ruby classes and objects.
- Able to write and understand class's and object's use case, capabilities and methods.
- Able to apply the principles of SOLID when writing classes.
- Able to understand the concept of mutability and immutability.
- Able to write/refactor classes and objects as DRY as possible.

## Class Inheritance and composition
### Description
Understanding of Class Inheritance and composition and use case
### Example
- Able to apply single level inheritance for classes with a "is a" relationship.
- In case of "has a" relationship, prefer composition over inheritance.

## Class namespacing
### Description
Know how of Ruby's class naming organization
### Example
- Able to use modules when grouping classes based on purpose context (e.g Payments for payment related grouping).

## Single responsibility class/instance methods
### Description
Understanding of writing class according to its namesake use case
### Example
- Able to write short and concise methods that only does what it's named for.

## Private/Public class methods
### Description
Understanding of Ruby's private and public class methods
### Example
- Able to properly discern proper use case for public and private methods.

## Enumerables and methods
### Description
Understanding of Ruby's enumerables
### Example
- Able to properly manage aggregation of Arrays in varying scenarios (map, select, reduce, etc.).
- Able to properly select the efficient method to iterate over an Array or Hash (e.g difference between select and find).

## Regular Expressions
### Description
Understanding of Ruby's regular expression
### Example
- Able to construct regular expressions using special characters and character classes.
- Able to match values using regular expressions.

## Exceptions
### Description
Management and understanding of Ruby's exceptions
### Example
- Able to understand exception messages and how to handle appropriately.
- Able to discern when to rescue exceptions and when to make it fail loudly.
- Able to catch execeptions and manage response to that exception based on the type of exception.

# Rails

## Migrations
### Description
Management of rails migration
### Example
- Able to write proper indexing strategies for new and or existing columns.
- Able to write up and down methods for migrations that allows for the latter.
- Able to properly manage db schema on newly executed migrations.
- Able to properly decern when to employ defaults to fields.

## Models
### Description
Management of rails models
### Example
- Able to maintain models as thin models with business logic abstracted to service objects.
- Understands that adding in sorting to scopes contains additional overhead when it comes to query speed.
- Able to write model validation and model relationships

## Controllers
### Description
Management of rails Controllers
### Example
- Able to maintain controllers as thin controllers with logic abstracted to service objects.
- At most, make controllers as CRUD controllers.
- Use service objects for business logic employed by controller endpoints.
- Able to properly manage http responses (e.g 200, 404, 401 etc).
- Able to write appropriate routes as well in pair with controller methods.

## Views
### Description
Management of rails Views
### Example
- Able to use partials in attempts to DRY components
