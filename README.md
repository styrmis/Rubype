# Ruby with Type.

Matz has mentioned Ruby3.0 with static type at some confluences. But almost all rubyists(include me) are not sure how typed Ruby is.

But it's worth thinking more. This gem is kind of trial without so much side-effect.

```rb
require 'haskell'

# ex1: (Ruby 2.1.0+)
class MyClass
  type Numeric >= Numeric >= Numeric, def sum(x, y)
    x + y
  end

  type Numeric >= Numeric >= Numeric, def wrong_sum(x, y)
    'string'
  end
end

MyClass.new.sum(1, 2)
#=> 3

MyClass.new.sum(1, 'string')
#=> ArgumentError: Wrong type of argument, type of "str" should be Numeric

MyClass.new.wrong_sum(1, 2)
#=> TypeError: Expected wrong_sum to return Numeric but got "str" instead


# ex2: (Ruby 2.1.0+)
class People
  type People >= Any, def marry(people)
    # Your Ruby code as usual
  end
end

People.new.marry(People.new)
#=> no error

People.new.marry('non people')
#=> ArgumentError: Wrong type of argument, type of "non people" should be People


# ex3: (Ruby 1.8.0+)
class MyClass
  def sum(x, y)
    x + y
  end
  type Numeric >= Numeric >= Numeric, :sum
end
```

## Feature
### Typed method can coexist with non-typed method

```ruby
# It's totally OK!!
class MyClass
  type Numeric >= Numeric >= Numeric, def sum(x, y)
    x + y
  end

  def wrong_sum(x, y)
    'string'
  end
end
```

### Duck typing

```ruby

class MyClass
  type Any >= Numeric, def foo(any_obj)
    1
  end
end

# It's totally OK!!
MyClass.new.foo(1)
# It's totally OK!!
MyClass.new.foo('str')
```

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'haskell'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install haskell

## Contributing

1. Fork it ( https://github.com/[my-github-username]/haskell/fork )
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create a new Pull Request


## Credits
[@chancancode](https://github.com/chancancode) first brought this to my attention. I've stolen some idea from him.
