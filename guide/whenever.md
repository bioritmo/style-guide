# Whenever #

* Always set the output of the rake tasks to a file. That way we can open the log and see if something broke:

```ruby
  every 5.minutes do
    rake 'app:job', :output => 'log/job.log'
  end
```

* Prefer using 1.8 hash syntax. As this code runs outside the application, it is a better idea to keep it compatible with Ruby 1.8.

## Capistrano Integration ##

* Use this snippet inside ```config/deploy.rb``` to set Whenever and Capistrano integration:

```ruby
  set :whenever_command, 'bundle exec whenever'
  set :whenever_environment, defer { rails_env }
  require 'whenever/capistrano'
```

* Whenever's documentation recommends using ```defer { stage }```, but don't use it. Capistrano will set ```stage``` to be the filename of the environment, which can be anything like ```qa02``` or ```internal-homologation-server```. Use ```defer { environment }``` or ```defer { rails_env }``` (as above).

* By default Capistrano only runs the ```update_crontab``` task on the servers marked with the ```:db``` role. This is usually what you want, since you don't want to run cronjobs in all the machines.
