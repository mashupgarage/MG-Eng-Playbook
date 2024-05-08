# Ruby/Rails Competencies

# Ruby

## Understanding of classes and objects
### Description

Able to read, understand and write ruby classes and objects.
Able to write and understand class's and object's usecase, capabilities and methods.
Able to apply the principles of SOLID when writing classes.
Able to understand the concept of mutability and immutability.
Able to write/refactor classes and objects as DRY as possible

## Understanding of Class Inheritance and composition and use case
### Description
Able to apply single level inheritance for classes with a "is a" relationship.
In case of "has a" relationship, prefer composition over inheritance.

## Class namespacing
### Description
Able to use modules when grouping classes based on purpose context (e.g Payments for payment related grouping).

## Single responsibility class/instance methods
### Description
Able to write short and concise methods that only does what its named for.

## Private/Public class methods
### Description
Able to properly discern proper usecase for public and private methods.

## Enumerables and methods
### Description
Able to properly manage aggregation of Arrays in varying scenarios (map, select, reduce, etc.).
Able to properly select the efficient method to iterate over an Array or Hash (e.g difference between select and find).

## Regular Expressions
### Description
Able to construct regular expressions using special characters and character classes.
Able to match values using regular expressions.

## Exceptions
### Description
Able to understand exception messages and how to handle appropriately.
Able when to rescue exceptions and when to make it fail loudly.

# Rails

## Migrations
### Description
Able to write proper indexing strategies for new and or existing columns.
Able to write up and down methods for migrations that allows for the latter.
Able to properly manage db schema on newly executed migrations.
Able to properly decern when to employ defaults to fields.

## Models
### Description
Able to maintain models as thin models with logic abstracted to service objects.

## Controllers
### Description
Able to maintain controllers as thin controllers with logic abstracted to service objects.
At most, make controllers as CRUD controllers.
Use service objects for business logic employed by controller endpoints.
Able to properly manage http responses (e.g 200, 404, 401 etc).

## Views
### Description
Able to use partials in attempts to DRY components
