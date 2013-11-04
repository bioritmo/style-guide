# Ruby #

## Code style ##

* Use 2 spaces for indentation, no tabs.
* Insert spaces around operators, commas, colons, semicolons, ```{``` and before ```}```.

```ruby
  hash = { key: value }
  sum = 1 + 2
  collection.each { |elem| puts elem }
  def some_method(name, status = 'active')
    # ...
  end
```

* Add spaces around ```=``` when assigning default values in method arguments.

```ruby
  # Instead of this...
  def some_method(name, status='active')
    # ...
  end
  # ...You should do this.
  def some_method(name, status = 'active')
    # ...
  end
```

* Don't put spaces around ```(```, ```[``` and before ```)``` or ```]```.

```ruby
  values = [1, 2, 3]
  filter(values)
```

* Add a blank line between method definitions.

```ruby
  def initialize(var)
    @var = var
  end
  def filter(values)
    values.select { |value| value.allowed? }
  end
```

* Don't add a blank line after a class, method, spec definition or before their respective ```end```.

```ruby
  # Instead of this...
  class MyClass
    def my_method
      # ...
    end
  end
  # ...You should do this.
  class MyClass
    def my_method
      # ...
    end
  end
```

* Indent private methods at the same column as the public methods.

```ruby
  class SomeClass
    def find(name)
      # ...
    end
    private
    def update_cached_values
      # ...
    end
  end
```

Indent when as deep as ```case```. Do the same for ```if``` and ```else``` as well.


```ruby
  case
  when song.name == 'Misty'
    puts 'Not again!'
  when song.duration > 120
    puts 'Too long!'
  when Time.now.hour > 21
    puts "It's too late"
  else
    song.play
  end
  kind = case year
         when 1850..1889 then 'Blues'
         when 1890..1909 then 'Ragtime'
         when 1910..1929 then 'New Orleans Jazz'
         when 1930..1939 then 'Swing'
         when 1940..1950 then 'Bebop'
         else 'Jazz'
         end
  result = if something
             'that'
           else
             'this'
           end
```

Use the same style for arguments:
```ruby
this_is_an_example(first: 1,
                   second: 2)
```

## Idioms ##
* When defining methods don't use parentheses for methods that don't take arguments. Use parentheses only for methods that accept arguments.

```ruby
  def save
    # ...
  end
  def create(name, age)
    # ...
  end
```

# Naming

* Use ```CamelCase``` for classes names.
* Use ```snake_case``` for methods and variable names.
* Use ```SCREAMING_SNAKE_CASE``` for constants.
* Names of predicate methods should end with ```?```.

* Avoid types in names.

```ruby
  # Instead of this...
  people_array = Person.all
  # ...You should do this.
  people = Person.all
```

# Syntax

* Always use ```&&``` and ```||``` for boolean expressions. Do not use ```and``` and ```or``` to avoid precedence issues.
```ruby
  if something && other
    do_this
  end
```

* Don't use ```unless``` with ```else```. Switch the clauses and use ```if``` instead.

```ruby
  # Instead of this...
  unless success?
    puts 'failure'
  else
    puts 'success'
  end
  # ...You should do this.
  if success?
    puts 'success'
  else
    puts 'failure'
  end
```

* Don't use ```then``` for multi-line ```if/unless```.

```ruby
  # Avoid this
  if something then
    do_that
  end
```

* When having a single-line body for a conditional consider using the ```if/unless``` modifier.

```ruby
  do_this if something
```

* Don't use ```for``` unless you have a very good reason. Use ```each``` instead.

* Avoid ```return``` when not required.

```ruby
  # Instead of this...
  def filter(values)
    return values.select { |value| value.allowed? }
  end
  # ...you should do this.
  def filter(values)
    values.select { |value| value.allowed? }
  end
```

* Avoid ```self``` when not required.

```ruby
  # Instead of this...
  def big_name
    self.name * 50
  end
  # ...you should do this.
  def big_name
    name * 50
  end
```

* Use ```_``` for unused block parameters.

```ruby
  # Instead of this...
  hash.map { |k, v| v + 1 }
  # ...you should do this.
  hash.map { |_, v| v + 1 }
```

* Use ```attr_*``` to define trivial methods.

```ruby
  # Instead of this...
  class Person
    def initialize(name, age)
      @name = name
      @age = age
    end
    def name
      @name
    end
    def age
      @age
    end
  end
  # ...you should do this.
  class Person
    attr_reader :name, :age
    def initialize(name, age)
      @name = name
      @age = age
    end
  end
```

* When defining class methods use def ```self.method``` if there isn't too many methods. If there's too much prefer using ```class << self```. There's no threshold number for this, you just need to follow your <3.

* Use implicit ```begin``` blocks.

```ruby
  # Instead of this...
  def method
    begin
      do_something
    rescue SomeError => e
      puts e
    end
  end
  # ...you should do this.
  def method
    do_something
  rescue SomeError => e
    puts e
  end
```

* If you're defining a class that doesn't have any methods, do it in a single-line. This happens a lot when defining exceptions.

```ruby
  # Instead of this...
  class MyClass
  end
  class MyError < StandardError
  end
  # ...you should do this.
  class MyClass; end
  class MyError < StandardError; end
```

* Use ```{...}``` for single-line blocks instead of ```do...end```. For multi-line blocks use ```do...end```.

```ruby
  # Instead of this...
  people.each { |person|
    # lots
    # of
    # stuff
    # happening
    # here
  }
  people.each do |person|
    puts person.name
  end
  # ...you should do this.
  people.each do |person|
    # lots
    # of
    # stuff
    # happening
    # here
  end
  people.each { |person| puts person.name }
```

* Signal exceptions using ```raise```. Use ```fail``` only if the exception should not be catched.

```ruby
  begin
    raise 'Unexpected'
  rescue => e
    fail if e.message == 'Can not be handled'
  end
```

## Data syntax ##

* Use ```%()`` to define single-line strings which require interpolation and embedded double-quotes. For multi-line strings, prefer heredocs.

```ruby
  # This is good
  %(<div class="my-class">#{my_content}</div>)
  # Instead of this...
  %(<div>\n<span class="my-class">Content</span>\n</div>)
  # ...you should do this.
  <<-STR
  <div>
    <span class="my-class">Content</span>
  </div>
  STR
```

## Standard library ##

* When using methods with bang! on strings, arrays and other enumerables, do not chain them:

```ruby
  # Instead of this...
  articles = associations.select { |a| a.is_a?(Article) }.sort_by!(&:published_at)
  # ...you should do this.
  articles = associations.select { |a| a.is_a?(Article) }
  articles.sort_by!(&:published_at)
  articles
```
This is because many bang! methods return ```nil``` if no change happens ([for example](http://ruby-doc.org/core-1.9.3/Array.html#method-i-reject-21), [Array#reject!](http://ruby-doc.org/core-1.9.3/Array.html#method-i-reject-21)) and those mistakes are very hard to detect since it only happens in special circumstances.

* Avoid ```Object#tap``` when it does not lead to more concise code. In the following case, it seems unnecessary and compromises readability. By using variable the returning value is clearer.

```ruby
  # Instead of this...
  article.save.tap do |saved|
    do_something if saved
  end
  # ...you should do this.
  saved = article.save
  do_something if saved
  saved
```

The memoization might be an use case for using tap instead of using ```begin..end``` block.

```ruby
  def result
    @result ||= Result.parse(@data).tap do |r|
      raise 'Invalid data input' unless r.valid?
    end
  end
```

Alternatively, you can move to a method and use variable assignment.

* Use ```inject``` when you need to work with the accumulated value in the next iteration. It is known as ```foldl``` (fold left) in functional languages, where you reduce the collection from the left to a result. For example:

```ruby
  [1, 2, 3, 4].inject(0) do |sum, n|
    sum + n
  end
  # => 10
  [1, 2, 3, 4].inject(:+)
  [1, 2, 3, 4].reduce(:+)
  # finding the longest word in collection
  ['cat', 'foobar', 'john'].inject('') do |longest_word, word|
    word.length > longest_word.length ? word : longest_word
  end
  # => 'foobar'
```

However, it might lead to some misuses:

```ruby
  # Instead of this...
  [1, 2, 3, 4].inject({}) do |hash, n|
    hash[n] = 'a' * n
    hash
  end
  # ...you should do this.
  [1, 2, 3, 4].each_with_object({}) do |n, hash|
    hash[n] = 'a' * n
  end
  # => {1=>"a", 2=>"aa", 3=>"aaa", 4=>"aaaa"}
```

Reading the second example, you can see that the next interation doesn't require the previous ```state```. You just need that the object in use is a ```Hash``` to associate key-values into. So, in these cases, ```each_with_object``` is preferable.

Recall that you can always use simple ruby code to achieve the same result:
```ruby
  hash = {}
  [1, 2, 3, 4].each { |n| hash[n] = 'a' * n }
  hash # => {1=>"a", 2=>"aa", 3=>"aaa", 4=>"aaaa"}
```
