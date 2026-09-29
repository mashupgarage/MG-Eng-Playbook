# RSpec Setup

RSpec is a popular testing framework used for Ruby and Ruby on Rails projects.
Its design and purpose revolves around the concepts of BDD (Behavior Driven Development).
Writing tests based on behavior of the application and in times, tests the functional specification of the application.
It sports a very rich DSL, which in its simplicity could be powerful enough but when paired with RSpec's array of tools and modules could be
a well rounded testing tool for your Ruby based projects.

Writing tests in RSpec could be summarized by the following steps:
* write the smallest test case that matches a behavior you want to test
* run the test expect it to fail
* write code to make the test pass
* re-run the test suite
* repeat until test passes
* do cleanup and refactor
* repeat test steps until green

## Installation

Basic installation is as simple as adding RSpec to your Gemfile

```ruby
source "https://rubygems.org"

...
# have it on the development and or test segments
group :development, :test do
  gem 'rspec-rails'
end
```

Save the above changes then run bundle install

```bash
bundle install
```

After bundling, next up is to actually install and initialize RSpec on our project

```bash
rails generate rspec:install
```

Doing so will create the necessary directories and files

```bash
create .rspec
create spec
create spec/spec_helper.rb
create spec/rails_helper.rb
```

## File Structure

Even though initializing RSpec does all the work creating the initial directories.
We normally stay with the default directory structure

```
app/
bin/
config/
db/
lib/
log/
public/
spec/
  controllers/
  factories/
  fixtures/
  integration_tests/
  models/
  workers/
  rails_helper.rb
  spec_helper.rb
storage/
test/
tmp/
vendor/
```
