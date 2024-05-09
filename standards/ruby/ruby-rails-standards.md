# Ruby Guidelines

here are our best practices when it comes to ruby and on rails.

## Indentation
We only use spaces for indentation rather than hard tabs.

### Classes
We prefer two-space indents.
```ruby
# bad
class Car
    def initialize(params)
    end
end
```
```ruby
# good
class Car
  def initialize(params)
  end
end
```

### Method Parameters
We prefer to neatly stack long method arguments.
```ruby
# bad
class Car
  def self.create(brand_id, brand_name, manufacturer_year, chassis_type,
                  rubber_type, number_of_doors, transmition_type, country_of_origin)
    ...
  end
end
```
```ruby
# good
class Car
  def self.create(brand_id,
                  brand_name,
                  manufacturer_year,
                  chassis_type,
                  rubber_type,
                  number_of_doors,
                  transmition_type,
                  country_of_origin)
    ...
  end
end
```
```ruby
# good
class Car
  def self.create(
    brand_id,
    brand_name,
    manufacturer_year,
    chassis_type,
    rubber_type,
    number_of_doors,
    transmition_type,
    country_of_origin
  )
    ...
  end
end
```

### Method Body: Multi-line boolean statements
We prefer to properly indent Multi-line boolean statements with indentation.
```ruby
# bad
def can_race?(car)
  Fia::CarStandards.check_qualification?(car) &&
  is_fuel_check_passed? &&
  is_with_wheels?
end
```
```ruby
# good
def can_race?(car)
  Fia::CarStandards.check_qualification?(car) &&
    is_fuel_check_passed? &&
    is_with_wheels?
end
```

### Control Statements: Case Statements
```ruby
# bad
case color
  when 'red'
    puts 'ferrari'
  when 'blue'
    puts 'ford'
  when 'black'
    puts 'nissan'
  else
    puts 'just a car'
end
```

```ruby
# good
case color
when 'red'
  puts 'ferrari'
when 'blue'
  puts 'ford'
when 'black'
  puts 'nissan'
else
  'just a car'
end
```
### Control Statements: If Statements
```ruby
# bad
result = if cool?
  do_something_cool
else
  do_something_uncool
end
```

```ruby
# good
result =
  if cool?
    do_something_cool
  else
    do_something_uncool
  end
```

### Control Statements: If modifier statements
We use if modifiers if the condition can fit within one line else, we avoid using it
```ruby
# bad
some_very_long_statement_about_coding_and_managing_states(some_very_long_variable_naming_convention) if valid?
```
```ruby
# good
if valid?
  some_very_long_statement_about_coding_and_managing_states(some_very_long_variable_naming_convention)
end
```

### Chaining method calls
```ruby
# bad
Car.create(params).add_detail.select_time_compound.race
```

```ruby
# good
Car
  .create(params)
  .add_detail
  .select_time_compound
  .race
```

## Lines Terminations
### Methods
We use single empty line to terminate method definitions.
```ruby
# bad
def create_drink(raw_ingredients)
  prepared_ingredients = init_ingredients(raw_ingredients)
  drink = mix(prepared_ingredients)
  garnish_drink(drink)
end
def init_ingredients(ingredients)
  ...
end
def mix_ingredients(ingredients)
  ...
end
def garnish_drink(drink)
  ...
end
```
```ruby
# good
def create_drink(raw_ingredients)
  prepared_ingredients = init_ingredients(raw_ingredients)
  drink = mix(prepared_ingredients)
  garnish_drink(drink)
end

def init_ingredients(ingredients)
  ...
end

def mix_ingredients(ingredients)
  ...
end

def garnish_drink(drink)
  ...
end
```

### Attribute Accessors
We use single empty line to terminate declartion of accessors.
```ruby
# bad
class Car
  attr_reader :brand
  def initialize
    ...
  end
end
```
```ruby
# good
class Car
  attr_reader :brand

  def initialize
    ...
  end
end
```

### Method Privacy policies
We use single empty line to terminate declartion of privacy policies.
```ruby
# bad
class Car
  def initialize
    ...
  end
  private
  def tire_compound
    ...
  end
end
```
```ruby
# good
class Car
  def initialize
    ...
  end

  private

  def tire_compound
    ...
  end
end
```

## Trailing Commas
We avoid commas after the last parameter in a method call.
```ruby
# bad
def create(brand_id, brand_name, manufacturer_year,)
  ...
end
```
```ruby
# bad
def create(brand_id, brand_name, manufacturer_year)
  ...
end
```

## String line continuations
We use "backslashes" as a point of continuation for long strings.
```ruby
# good
long_string = 'The quick brown fox jumps over the lazy dog' \
              ' cat, elephant, tiger, goose, goat, mouse' \
              ' human, and alien.'
```

## Naming Conventions
### Method Suffixes
For methods that are expecting boolean as a return value, we use "?" as a suffix
```ruby
# bad
def race_worthy(car)
  ...
end
```
```ruby
# good
def race_worthy?(car)
  ...
end
```

For methods that are implying that it will modify something, we use "!" as a suffix
```ruby
# bad
class Car
  def retire(car)
    car.destroy!
  end
end
```
```ruby
# good
class Car
  def retire!(car)
    car.destroy!
  end
end
```

### Method Prefixes
We avoid using prefixes such as "is, does or can" but we properly allot a meaningful adjective.
```ruby
# bad
def can_race?(car)
  ...
end

def is_aerodynamic?(car)
  ...
end
```
```ruby
# good
def race_worthy?(car)
  ...
end

def aerodynamic?(car)
  ...
end
```

We use "_" for unused variables
```ruby
# bad
def get_driver_license(driver)
  personal_data, license = register_driver(driver)
  return license
end
```
```ruby
# good
get_driver_license(driver)
  _personal_data, license = register_driver(driver)
  return license
end
```

## Control Statements

### Built-in Ruby iterators over for loops
We definitely don't use for loop, not unless we had no choice, but instead use Ruby's array of iterators
```ruby
# bad
numbers = [1, 2, 3]
for number in numbers do
  puts number + 1
end
```
```ruby
# good
numbers = [1, 2, 3]
numbers.each {|number| number + 1}
```

### Ternary Operators over if else statements
We use ternary operators in place of single if else statments
```ruby
# bad
result = if condition then do_something else do_something_else end
```
```ruby
# good
result = condition ? do_something : do_something_else end
```

### Nested Ternary Operators
Terneries are not meant to be nested. We fix this by introducing a layer of single if else statement
```ruby
# bad
condition then (nested_condition ? nested_do_something : do_something) else do_something_else end
```
```ruby
# good
if condition
  nested_condition ? nested_do_something : do_something
else
  do_something_else
end
```

### Nested Conditionals
We avoid nested conditionals as this could be prove to be difficult to read. In these cases, we prefer to use guard clauses.
```ruby
# bad
def prepare_car(car)
  if car
    install_tires(car)
    if car.soft_compound_tires?
      set_stop_strategy(2)
    else
      set_stop_strategy(1)
    end
  end
end
```
```ruby
# bad
def prepare_car(car)
  return if car.blank?
  install_tires(car)
  return set_stop_strategy(2) if car.soft_compound_tires?
  set_stop_strategy(1)
end
```

## Safe Navigation and delegation
We avoid using chained "&" but we replace it with check instead.
```ruby
# bad
driver&.address&.zip_code
```
```ruby
# good
driver && driver.address&.zip_code
```
Or we can use delegation
```ruby
# good
class Driver
  def zip_code
    address&.zip_code
  end
end
```

## Method Definitions
### Keyword Arguments
We seldom use positional arguments, but in place we use keyword arguments.
```ruby
# bad
def officiate_race(drivers, teams = [], cars = [], country = '', race_date = Time.now)
  ...
end
```
```ruby
# good
def officiate_race(drivers, teams: [], cars: [], country: '', race_date: Time.now)
  ...
end
```
Or if keyword arguments are not yet available, just use options hash instead
```ruby
# good
def officiate_race(drivers, options)
  options = {
    teams: [],
    cars: [],
    country: '',
    race_date: Time.now
  }.merge(options)
  ...
end
```

## Variable Assignment
### Constants
There are no such thing as constants ni Ruby as these so called constants are mutable.
In order to workaround this issue, we call freeeze on our so called constants.
```ruby
# bad
class Car
  WHEELS = 4
  COLORS = [
    'red',
    'blue',
    'yellow'
  ]
end
```
```ruby
# good
class Car
  WHEELS = 4.freeze
  COLORS = [
    'red',
    'blue',
    'yellow'
  ].freeze
end
```

# Rails Guidelines

## Routing
### Member and collection Routes
When we wanted to add more actions to a plain RESTful controller, we use `member` and or `collection` routes
```ruby
# bad
get 'cars/:id/decommission'
resources :cards
end
```
```ruby
# good
resources :cars do
  put 'decommission', on: :member
end
```
```ruby
# good
resources :cars do
  get 'search', on: :collection
end
```

### Namespacing
There are scenarios where we need to logicaly group/name our endpoints.
```ruby
# good
namespace :formula_1 do
  # route is /formula_1/cards/*
  # controller is Formula1::CarsController
  resources :cars
end
```

## Controller
### Thin controllers
We keep our controllers very slim. Most of our business logic resides in testable service objects

### Render: View
We never render inline but we render views by corresponding view files
```ruby
# bad
class CarsController < ApplicationController
  def index
    render inline: "<% cars.each do |c| %><p><%= c.name %></p><% end %>", type: :erb
  end
end
```
```ruby
# good
class CarsController < ApplicationController
  def index
    render :index
  end
end

## app/views/cars/index.html.erb
<p><%= product.name %></p>
<p><%= product.price %></p>
```

### HTTP status code symbols
We prefer using human recognizeable HTTP status codes.
[List of HTTP status codes](https://gist.github.com/mlanett/a31c340b132ddefa9cca)
```ruby
# bad
render status: 403
```
```ruby
# bad
render status: :forbidden
```

## Models
### Model: Contents
We keep our models thin as well, containing just logic used for persistence only.
On some instances, our models also contains business logic as well.

### Models: Content declaration grouping
We group contents of models by:
```ruby
class Car < ApplicationRecord
  # default scopes
  default_scope { where(active: true) }

  # named scopes
  scope :inactive, -> { where(is_active: false) }

  # constants
  COLORS = ['red', 'blue', 'white'].freeze

  # accessors
  attr_accessor :formatted_brand_name

  # enums
  enum type: {
    active: 0,
    inactive: 1
  }

  # associations
  belongs_to :brand

  has_many :parts, dependent: :destroy

  # validations
  validates :name, presence: true

  # callbacks
  before_save :format_brand_name

  # gem related macros
end
```

### Model: Enums
Using enums is not the norms for us here. But in case its needed, we use hash types for it
```ruby
# bad
class Car < ApplicationRecord
  enum type: %i[active inactive]
end
```
```ruby
# good
class Car < ApplicationRecord
  enum type: {
    active: 0,
    inactive: 1
  }
end
```

### Model: Updating
Some of the methods for updating skips validation which what we don't want to skip.
[List of methods that skips validations](https://guides.rubyonrails.org/active_record_validations.html#skipping-validations)
```ruby
# bad
Article.first.decrement!(:view_count)
DiscussionBoard.decrement_counter(:post_count, 5)
Article.first.increment!(:view_count)
DiscussionBoard.increment_counter(:post_count, 5)
person.toggle :active
product.touch
Billing.update_all("category = 'authorized', author = 'David'")
user.update_attribute(:website, 'example.com')
user.update_columns(last_request_at: Time.current)
Post.update_counters 5, comment_count: -1, action_count: 1
```
```ruby
# good
car.update_attributes(color: 'red')
```

### Model: Collection iteration
We normally don't query for `all` as this loads the entirety of the records associated with the model.
To solve that we employ batch processing.
```ruby
# bad
Car.all.each do |car|
  car.do_something
end
```
```ruby
# good
Car.find_each do |car|
  car.do_something
end
```
```ruby
# good
Car.where(active: true).find_each do |car|
  car.do_something
end
```
```ruby
# good
Car
  .where(active: true)
  .in_batches(batch_size: 1000)
  .each_record(&:do_something)
```

### Model: Saving with a bang(!)
When saving, we used save with the `bang` operator as it raises exceptions on failing saves.
```ruby
# bad
Car.create(name: 'Some car')
car.save(name: 'Some car')
```
```ruby
# good
Car.create!(name: 'Some car')
car = Car.create(name: 'some car')
if car.persisted?
  ...
else
  ...
end
```
```ruby
# good
car.save!

if car.save
  ...
else
  ...
end
```

### Model: Active record queries
We avoid string interpolation when constructing active record queries as doing so
opens us to SQL injection attacks.
```ruby
# bad
Car.where("active = #{active}")
```
```ruby
# good
Car.where("active = ?", active)
```

We use named placeholders instead of positional placeholders when we have more than one placeholders needed
```ruby
# good
Car.where("active = ? AND brand = ?", active, brand_name)
```
```ruby
# better
Car.where("active = :active AND brand = :brand_name", active: active, brand_name: brand_name)
```

### Model: Sorting chronologically
We seldom use `id` as a basis for sorting chronologically, but instead we use `create_at` fields.
We also don't use sorting as part of a default scope as that slows down general usecase for queries.
```ruby
# bad
class Car
  scope :by_date, -> { order(id: :asc) }
end
```
```ruby
# good
class Car
  scope :by_date, -> { order(created_at: :asc) }
end
```

### Model: Pluck
We use `pluck` in times where we just want to pick one column value from a query.
`Pluck` is efficient as the query it constructs only return the field plucked.
```ruby
# bad
Car.all.map(&:name)
```
```ruby
# good
Car.pluck(:name)
```

## Migrations
### Schema Version
`schema.rb` or `structure.sql` is always properly version controlled.

### Schema loading
We use `rake db:schema:load` instead of `rake db:migrate` for newly spawned setup.

### Migration: Default values
When there is a need to enforce defaults, we enforce them on the migration itself and not
handled on the application itself. Reason is for consistency.
```ruby
# good
class AddDefaultNumberOfDoorsToCars < ActiveRecord::Migration
  def change
    change_column_default :cards, :number_of_doors, 4
  end
end
```

### Migration: Boolean fields with default values
We enforce a rule that whenever a field stands as a `boolean`, it needs an outright `default value`.
As compared with no default, you'll be dealing with 3 states, null, true and false.
```ruby
# bad
class AddVintageToCars < ActiveRecord::Migration
  def change
    add_column :cars, :vintage, :boolean
  end
end
```
```ruby
# good
class AddVintageToCars < ActiveRecord::Migration
  def change
    add_column :cars, :vintage, :boolean, default: false, null: false
  end
end
```

### Migration: Foreign keys
We always enforce foreign keys when migrating tables with relationships.
```ruby
# bad
class CreateCarsTable < ActiveRecord::Migration
  def change
    create_table :cars do |t|
      ...
      t.belongs_to :brand
    end
  end
end
```
```ruby
# good
class CreateCarsTable < ActiveRecord::Migration
  def change
    ...
    t.belongs_to :brand, foreign_key: true
  end
end
```

### Migration: Up and Down
When we are working with migrations that can be rollbacked, we normally have `up` and `down` methods.
But in essence we can also use the `change` method as well.

```ruby
# good
class AddVintageToCars < ActiveRecord::Migration
  def up
    add_column :cars, :vintage, :boolean, default: false, null: false
  end

  def down
    remove_column :cars, :vintage
  end
end
```
```ruby
# good
class AddVintageToCars < ActiveRecord::Migration
  def change
    add_column :cars, :vintage, :boolean, default: false, null: false
  end
end
```
