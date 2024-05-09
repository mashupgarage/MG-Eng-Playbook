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
