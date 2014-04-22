Rails Styleguide
================

Gemfile
=======

Break gems into groups and responsibilities, sorting them alphabetically. Add comments if necessary, to remind why this gem is being required.

```ruby

gem 'rails', '3.2.11'

# Database
gem 'activerecord-mysql2-adapter'
gem 'mysql2'

# Background processing
gem 'resque'
gem 'resque-cleaner'
gem 'resque-retry'

# Frontend
gem 'haml'
gem 'jquery-rails'
gem 'pdfkit','0.5.2'        # Prints PDF

# External Services
gem "aws-s3", :require => "aws/s3"

group :development do
  gem 'better_errors'         # Nice page for exceptions, with console
  gem 'binding_of_caller'
  gem 'foreman'               # Load many services at once (web, worker, smtp)
  gem 'mailcatcher'           # Emulates SMTP and provides visualization of emails
  gem 'rails_best_practices'
end
```

Models
======

Querying
--------

Hash params is preferred as argument in ```where``` clause.

All queries must live inside their own model. Never use ```where``` from outside of the model.
* When you have to call queries out of the model it must be done through ```scope```.
```ruby
    class VipsController < ActiveController
      def vip
        # Never
        # @vip_plans = Plan.where(:kind => "vip")

        # Always
        @vip_plans = Plan.vip
      end
    end
```
* When you have to call conditions from another model it must be done through ```merge```.
```ruby
    class Purchase < ActiveRecord::Base
      belongs_to :plan

      # Never
      # scope :vip, includes(:plan).where('plans.kind = ?', "vip")

      # Always
      scope :vip, includes(:plan).merge(Plan.vip)
    end
```

Migrations
==========

Use a `""` (blank string) as default value on string columns instead `NULL`. This will make your life easier when create queries:

If you do not follow the rule:
```ruby
Person.where("(people.email IS NULL OR email = '') AND (people.phone IS NULL OR phone = '')")
```

If you follow the rule:
```ruby
Person.where(:email => "", :phone => "")
```
