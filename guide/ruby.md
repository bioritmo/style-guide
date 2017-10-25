# Ruby

### Estilo de Código

##### Use 2 espaços para indentação, não use tabulação.

```ruby
class Person
  attr_acessor :first_name, :last_name

  def full_name
    first_name + last_name
  end
end
```

##### Adicione espaços entre os operatores, `,`, `;`, `:`, ```{``` e antes ```}```.

```ruby
  hash = { key: value }
  sum = 1 + 2
  collection.each { |elem| puts elem }
  def some_method(name, status = 'active')
    # ...
  end
```

##### Adicione espaços em volta  ```=``` quanto definir valores padrão para argumentos de um método.

```ruby
  # Ao invés de...
  def some_method(name, status='active')
    # ...
  end
  # ... você deve escrever assim
  def some_method(name, status = 'active')
    # ...
  end
```

##### Não coloque espaços em volta de  ```(```, ```[``` e antes de ```)``` ou ```]```.

```ruby
  values = [1, 2, 3]
  filter(values)
```

##### Adicione uma linha em branco entre as definições de métodos.

```ruby
  def initialize(var)
    @var = var
  end

  def filter(values)
    values.select { |value| value.allowed? }
  end
```

##### Não adicione uma linha em branco depois de definir um nome de classe, método, teste ou antes de seus respectivos ```end```.

```ruby
  # Ao invés de...
  class MyClass

    def my_method
      # ...
    end

  end
  # ... você deve escrever assim
  class MyClass
    def my_method
      # ...
    end
  end
```

##### Idente métodos privados na mesma coluna que os métodos públicos.

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

##### Idente `when` no mesmo nível de `case`. Faça o mesmo para ```if``` e ```else```.

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

##### Use o mesmo estilo para argumentos:

```ruby
this_is_an_example(first: 1,
                   second: 2)
```

### Idiomas

##### Quando definir métodos, não use parenteses para métodos que não tenham argumentos. Use parenteses apenas para métodos que aceitem argumentos.

```ruby
  def save
    # ...
  end

  def create(name, age)
    # ...
  end
```

### Nomemclaturas

##### Use ```CamelCase``` para nomes de classes.

```ruby
  MyCustomError = Class.new(StandardError)
```

##### Use ```snake_case``` para nomear métodos e variáveis.

```ruby
  area = height * width
```

##### Use ```SCREAMING_SNAKE_CASE``` para constantes.

```ruby
  COISO_PREFIX = "Coiso".freeze
```

##### Nomes de métodos predicados devem terminar com ```?```.

```ruby
  def paulista?
    acronym == "PTA"
  end
```

##### Evite tipos em definições de nomes.

```ruby
  # Ao invés de ...
  people_array = Person.all
  # você deve escrever assim.
  people = Person.all
```

### Sintaxe

##### Sempre use ```&&``` e ```||``` para expressões booleanas. Não use ```and``` e ```or``` para evitar problemas de precedência.

```ruby
  if something && other
    do_this
  end
```

##### Não use ```unless``` com ```else```. Sempre dê preferência a começar com a condição que não seja negativa. Se for o caso, inverta as cláusulas e use ```if```.

```ruby
  # Ao invés de ...
  unless success?
    puts 'failure'
  else
    puts 'success'
  end
  # você deve escrever assim.
  if success?
    puts 'success'
  else
    puts 'failure'
  end
```

##### Não use ```then``` para ```if/unless``` em múltiplas linhas.

```ruby
  # Evite
  if something then
    do_that
  end
```

##### When having a single-line body for a conditional consider using the ```if/unless``` modifier.

```ruby
  do_this if something
```

##### Don't use ```for``` unless you have a very good reason. Use ```each``` instead.

##### Avoid ```return``` when not required.

```ruby
  # Ao invés de ...
  def filter(values)
    return values.select { |value| value.allowed? }
  end
  # você deve escrever assim.
  def filter(values)
    values.select { |value| value.allowed? }
  end
```

##### Avoid ```self``` when not required.

```ruby
  # Ao invés de ...
  def big_name
    self.name * 50
  end
  # você deve escrever assim.
  def big_name
    name * 50
  end
```

##### Use ```_``` for unused block parameters.

```ruby
  # Ao invés de ...
  hash.map { |k, v| v + 1 }
  # você deve escrever assim.
  hash.map { |_, v| v + 1 }
```

##### Use ```attr_*``` to define trivial methods.

```ruby
  # Ao invés de ...
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
  # você deve escrever assim.
  class Person
    attr_reader :name, :age
    def initialize(name, age)
      @name = name
      @age = age
    end
  end
```

##### When defining class methods use def ```self.method``` if there isn't too many methods. If there's too much prefer using ```class << self```. There's no threshold number for this, you just need to follow your <3.

##### Use implicit ```begin``` blocks.

```ruby
  # Ao invés de ...
  def method
    begin
      do_something
    rescue SomeError => e
      puts e
    end
  end
  # você deve escrever assim.
  def method
    do_something
  rescue SomeError => e
    puts e
  end
```

##### If you're defining a class that doesn't have any methods, do it in a single-line. This happens a lot when defining exceptions.

```ruby
  # Ao invés de ...
  class MyClass
  end
  class MyError < StandardError
  end
  # você deve escrever assim.
  class MyClass; end
  class MyError < StandardError; end
```

##### Use ```{...}``` for single-line blocks instead of ```do...end```. For multi-line blocks use ```do...end```.

```ruby
  # Ao invés de ...
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
  # você deve escrever assim.
  people.each do |person|
    # lots
    # of
    # stuff
    # happening
    # here
  end
  people.each { |person| puts person.name }
```

##### Signal exceptions using ```raise```. Use ```fail``` only if the exception should not be catched.

```ruby
  begin
    raise 'Unexpected'
  rescue => e
    fail if e.message == 'Can not be handled'
  end
```

### Data syntax

##### Use ```%()`` to define single-line strings which require interpolation and embedded double-quotes. For multi-line strings, prefer heredocs.

```ruby
  # This is good
  %(<div class="my-class">#{my_content}</div>)
  # Ao invés de ...
  %(<div>\n<span class="my-class">Content</span>\n</div>)
  # você deve escrever assim.
  <<-STR
  <div>
    <span class="my-class">Content</span>
  </div>
  STR
```

### Standard library

##### When using methods with bang! on strings, arrays and other enumerables, do not chain them:

```ruby
  # Ao invés de ...
  articles = associations.select { |a| a.is_a?(Article) }.sort_by!(&:published_at)
  # você deve escrever assim.
  articles = associations.select { |a| a.is_a?(Article) }
  articles.sort_by!(&:published_at)
  articles
```
This is because many bang! methods return ```nil``` if no change happens ([for example](http://ruby-doc.org/core-1.9.3/Array.html#method-i-reject-21), [Array#reject!](http://ruby-doc.org/core-1.9.3/Array.html#method-i-reject-21)) and those mistakes are very hard to detect since it only happens in special circumstances.

##### Avoid ```Object#tap``` when it does not lead to more concise code. In the following case, it seems unnecessary and compromises readability. By using variable the returning value is clearer.

```ruby
  # Ao invés de ...
  article.save.tap do |saved|
    do_something if saved
  end
  # você deve escrever assim.
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

##### Use ```inject``` when you need to work with the accumulated value in the next iteration. It is known as ```foldl``` (fold left) in functional languages, where you reduce the collection from the left to a result. For example:

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
  # Ao invés de ...
  [1, 2, 3, 4].inject({}) do |hash, n|
    hash[n] = 'a' * n
    hash
  end
  # você deve escrever assim.
  [1, 2, 3, 4].each_with_object({}) do |n, hash|
    hash[n] = 'a' * n
  end
  # => {1=>"a", 2=>"aa", 3=>"aaa", 4=>"aaaa"}
```

Lendo o segundo exemplo, você pode ver que a próxima interação não requer o `estado` anterior.
Você só precisa que o objeto em uso seja um ```Hash``` para associar valores-chave.
Então, nesses casos, é preferível usar ```each_with_object```.

Lembre-se de que você sempre pode usar o código ruby mais simples para obter o mesmo resultado:
```ruby
  hash = {}
  [1, 2, 3, 4].each { |n| hash[n] = 'a' * n }
  hash # => {1=>"a", 2=>"aa", 3=>"aaa", 4=>"aaaa"}
```
