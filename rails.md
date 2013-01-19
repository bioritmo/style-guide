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
