# Rspec #

* Add a ```#``` before the method name when describing instance methods.

```ruby
  describe '#my_method' do
    # ...
  end
```

Add a ```.``` before the method name when describing class methods.

```ruby
  describe '.class_method' do
    # ...
  end
```

* Don't write 'should' in the spec description.

```ruby
  # THIS IS BAD
  it 'should return something' do
    # spec here
  end
  # THIS IS GOOD
  it 'returns something' do
    # spec here
  end
```

* Don't negate ```should```. Use ```should_not``` instead.

* Use ```before``` do instead of ```before(:each)``` do.

* Use ```be``` matchers.

```ruby
  # THIS IS BAD
  true.should == true
  # THIS IS GOOD
  true.should be_true
```

* Use predicate matchers.

```ruby
  # THIS IS BAD
  something.awesome?.should be_true
  something.has_company_topics?.should be_true
  # THIS IS GOOD
  something.should be_awesome
  something.should have_company_topics
```

* When testing collections use ```have(n).items``` matcher.

```ruby
  # THIS IS BAD
  [1, 2, 3].size.should == 3
  # THIS IS GOOD
  [1, 2, 3].should have(3).items
```

* When comparing hashes, prefer to compare each key instead of comparing the whole hash, specially when you have other hashes as values. This helps you to easily find a broken expectation because of the rspec 2 diff.

```ruby
  # THIS IS BAD
  response.should == {
    'first_name' => 'Aaron',
    'last_name' => 'Rodgers',
    'team' => {
      'name' => 'Green Bay Packers',
      'city' => 'Green Bay'
    }
  }
  # THIS IS GOOD
  response['first_name'].should == 'Aaron'
  response['last_name'].should == 'Rodgers'
  response['team'].should == {
    'name' => 'Green Bay Packers',
    'city' => 'Green Bay'
  }
```

* Prefer to use let than ivars;

```ruby
  # THIS IS BAD
  before do
    @blog = create_blog
    @post = create_post(@blog)
    @commenter = create_user
    @comment = create_comment(@post, user: @commenter)
  end
  # THIS IS GOOD
  let(:blog) { create_blog }
  let(:post) { create_post(blog) }
  let(:commenter) { create_user }
  let(:comment) { create_comment(post, user: commenter) }
```

* Duplicated code in specs may be a good fit to go inside a ```before``` block.

```ruby
  # THIS IS BAD
  it 'validates the presence of author' do
    @post = Post.new
    @post.valid?
    @post.errors.should contain(['author', 'should not be blank'])
  end
  it 'validates the presence of title' do
    @post = Post.new
    @post.valid?
    @post.errors.should contain(['title', 'should not be blank'])
  end
  # THIS IS GOOD
  before do
    @post = Post.new
    @post.valid?
  end
  it 'validates the presence of author' do
    @post.errors.should contain(['author', 'should not be blank'])
  end
  it 'validates the presence of title' do
    @post.errors.should contain(['title', 'should not be blank'])
  end
```

* Code that is incidental (it is needed to make the test work, but it isn't related to the code being tested) may also be a good fit for a ```before``` block.

```ruby
  # THIS IS BAD
  it 'validates the presence of author' do
    blog = build_blog
    blog.save!
    @post = blog.posts.new
    @post.valid?
    @post.errors.should contain(['author', 'should not be blank'])
  end
  # THIS IS GOOD
  before do
    blog = build_blog
    blog.save!
    @post = blog.posts.new
    @post.valid?
  end
  it 'validates the presence of author' do
    @post.errors.should contain(['author', 'should not be blank'])
  end
```

* When testing with dates, avoid using the current time, even if working with a gem like [Timecop](https://github.com/travisjeffery/timecop). Prefer to use an old date to avoid issues with specs failing some time later.

```ruby
  # if today is 2013-05-06 10:00:00, use the same date from last year for example
  new_time = Time.local(2012, 5, 6, 10, 0, 0)
  Timecop.freeze(new_time)
```

* Don't use ```mock``` or ```stub```. Use ```double``` instead. Both ```mock``` and ```stub``` are [deprecated](https://github.com/rspec/rspec-mocks/commit/843a40f4483be9888ba03a415468be99182f0b4a).
