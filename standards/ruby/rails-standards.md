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
