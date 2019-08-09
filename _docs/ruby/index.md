---
layout: page
title: Ruby
permalink: /ruby
---

This guide is an adaptation of [ClearCove's](http://rails-recipes.clearcove.ca/pages/ruby_coding_style_guide.html) guide and [Bozhidar Batsov's](https://github.com/bbatsov/ruby-style-guide) guide.

## RuboCop
We are using [RuboCop](https://docs.rubocop.org/en/latest/installation/) to police our standards as you develop.

Global
```
$ gem install rubocop
```

your project `Gemfile`
```ruby
group :development, :test do
  gem 'rubocop'
  gem 'rubocop-rspec'
end
```

Config Files for RuboCop
Add the file [rails/.rubocop-rails.yml](/animikii/styleguide/tree/master/rails/.rubocop-rails.yml) to the project root.
Update your `.rubocop.yml` to look this.

```
require: rubocop-rspec

inherit_from:
  - .rubocop-rails.yml
```

## Formatting

* Use UTF-8 encoding.
* End lines with an `LF` (Unix style).
* Indent with 2 spaces, no tabs.
* No trailing whitespace.
* End each file with a blank newline.
* Indent only at the beginning of a line.

  ```ruby
  # Bad
  {
    first_key:      "value",
    second_key:     "value",
    third_key:      "value",
    thousandth_key: "value"
  }

  # Good
  {
    first_key: "value",
    second_key: "value",
    third_key: "value",
    thousandth_key: "value"
  }
  ```
* Use spaces around operators, after commas, colons and semicolons, around `{` and before `}`.

  ```ruby
  1 + 3

  array = [1, 2, 3, 4]

  hash = { :a => 1, :b => 2, :c => 3 }

  "#{ interpolated_strings }"

  lambda { |args| also_for_blocks }
  ```
* No spaces after `(`, `[` or before `]`, `)`.

  ```ruby
  some(arg).other
  [1, 2, 3].length
  ```
* No spaces after `!`.

  ```ruby
  !array.include?(element)
  ```
* Indent `when` as deep as `case`.

  ```ruby
  case int
  when 1
    puts "one"
  when 2
    puts "two"
  else
    puts ":("
  end
  ```
* Use empty lines between `def`s for readability.

  ```ruby
  def method_one
    puts "Hello, World"
  end

  def method_two
    puts "Hello again, World"
  end
  ```
* Put two spaces before statement modifiers such as postfixed `if`, `unless`, `while`, `until`, or `rescue`.

  ```ruby
  "true"  if true
  "true"  unless false
  ```
* Leave an empty line after a `class` and before its `end`.

  ```ruby
  class Person

    def method
      # ...
    end

  end
  ```
* Don't use a `;` to separate statements or expressions. An exception to this would be the definition of a class with no body.

  ```ruby
  class SomeError < StandardError; end
  ```

  However, for such a case, the alternative syntax is preferable as it avoids the use of a semi-colon.

  ```ruby
  SomeError = Class.new(StandardError)
  ```
* Add underscores to large numerical literals to improve their readability.

  ```ruby
  # Bad
  number = 1000000

  # Good
  number = 1_000_000
  ```
## Documentation

Use [YARD](http://yardoc.org/) and it's conventions for code documentation.

```ruby
# Checks if a {Foo} is the same as a {Bar}.
#
# @param foo [Foo] a foo
# @param bar [Bar] a bar
# @return [Boolean] true if foo is equal to bar
def foobar(foo, bar)
  true  if Foo == Bar
end
```

## Comments

* Comments longer than one word should be capitalized and properly punctuated.
* Avoid superfluous comments.

## Naming things

* Use `snake_case` for methods and variables.
* Use `CamelCase` for classes and modules (keep acronyms like HTTP, or XML uppercase).
* Use `SCREAMING_SNAKE_CASE` for constants.
* Avoid prefixing methods that return a boolean with verbs such as `is_` or `has_`.

  ```ruby
  is_admin = true
  has_permissions = true
  ```
* Suffix methods with an `?` if they return a `Boolean`.

  ```ruby
  def exists?
    true  unless false
  end
  ```
* The names of potentially dangerous methods (i.e. methods that modify `self` or the arguments, `exit!`, etc.) should end with an exclamation mark. Bang methods should only exist if a non-bang method exists. ([More on this](http://dablog.rubypal.com/2007/8/15/bang-methods-or-danger-will-rubyist)).
  * Idea: the dangerous method can perform the operation on `self`, the non-dangerous version can perform the operation on a `dup` of the `self`.
* Use one-letter variables for short block/method parameters.
  * `k` for the key part of a `Hash`
  * `v` for the value part of a `Hash`
  * `e` for the elements of an `Enumerable`
  * `f` for files and names of files
  * `s` for a string
  * `i`, `j`, `k`... for indexes
  * `v` for any value
* When using `inject` and  the block is short, use the argument names `|m, e|` (memo, each).
* Start expensive method names with `compute_`

  ```ruby
  def compute_the_meaning_of_life
    # 1. Write some code
    # 2. ???
    # 3. Profit!
  end
  ```
* Use `_` for unused parameters.

  ```ruby
  hash.map { |_, v| v ^ 2 }
  ```

## Syntax

* Use parenthesis around method arguments.

  ```ruby
  def some_method(with, arguments)
    # ...
  end
  ```
* When a method accepts multiple arguments, or has optional arguments, consider using keyword arguments.

  ```ruby
  def some_method(foo: nil, bar: nil)
    # ...
  end
  ```

  If the method in question is high-use and has the potential to change its arguments down the road, keyword arguments can be preferable due to the ease of maintenance, as potentially not every call of the method has to be updated with the new arguments.
* Use `each` to iterate over `Enumerable` objects.
* Don't use `then` in a multi-line `if`.
* Only use the ternary operator if the expressions are trivial.

  ```ruby
  completed? ? "Accepted" : "Denied"
  ```
* Don't use `and` or `or` keywords. Stick to `&&` and `||` (unless you really know why you *should* use them).
* Never use `unless` with an `else`. Re-write it with the positive case first.

  ```ruby
  # Bad
  unless success?
    "failure"
  else
    "success"
  end

  # Good
  if success?
    "success"
  else
    "failure"
  end
  ```
* Don't use parenthesis around the condition in an `if`, `unless`, or `while` **unless** you are assigning a value.

  ```ruby
  # Bad
  if (x > y)
    "okay"
  end

  # Good
  if x > y
    "okay"
  end

  # Acceptable
  if (x = y)
    "okay"
  end
  ```
* Use `do`...`end` for multi-line blocks. Use `{`...`}` for single-line blocks.
* Don't use `return` unless it's required.
* Don't use `for` unless it's intentional. `for` doesn't introduce a new scope, and variables defined within a `for` loop are available outside the loop.

  ```ruby
  array = [1, 2, 3]

  # Bad
  for number in array do
    puts number
  end

  # Note that number is accessible outside of the for loop
  number # => 3

  # Good
  array.each { |number| puts number }

  # number is not accessible outside each's block
  number # => NameError: undefined local variable or method `number'
  ```
* Omit paranthesis for method calls with no arguments.

## Structure

* Don't use `@@class_variables` unless you know what you're doing.
* Use `self.method_name` to define class methods.
* Don't indent `private`, `protected`, or `public`.

  ```ruby
  class Person

    def some_method
      # ...
    end

  private

    def method_name
      # ...
    end

  end
  ```
* Use `self` when referring to internal attributes.

  ```ruby
  class Person

    attr_accesible :first_name, :last_name

    def full_name
      "#{ self.first_name } #{ self.last_name }"
    end

  end
  ```
* Obey the Law of Demeter

  A method `m` of an object `O` may only invoke methods of the following kinds of objects:

  1. `O` itself
  2. `m`'s parameters
  3. Any object created/instantiated within `m`
  4. `O`'s direct component objects
  5. A global variable, accessible by `O`, in the scope of `m`

  Use delegation where it makes sense in order to obey the Law of Demeter in your code.

## Exceptions

* Don't rescue `StandardError`, instead, rescue specific exceptions.
* Feel free to add new exception classes for cases that make sense (i.e. `OutOfDiskSpaceError = Class.new(StandardError)`). Exception class names should be suffixed with `Error` to go along with the convention.

## Strings

* Use string interpolation, not concatenation. (Review [#formatting](#formatting) or more information on spacing.)

  ```ruby
  # Bad
  "Something " + some_var + " wrong?"

  # Good
  "Something #{ some_var } wrong?"
  ```
* When constructing a large string, use `<<` instead of `+`.

  ```ruby
  # Bad
  html = "<p>"
  html = html + some_variable
  html = html + "</p>"

  # Good
  html = "<p>"
  html << some_variable
  html << "</p>"
  ```
* Don't use `Object#to_s` on interpolated objects, as it's invoked automatically.
* Prefer double-quotes `"` for defining string literals.
  * If the string contains double-quotes `"`, use single-quotes `'` to define it.
* Prefer the use of `()` for delimiters of `%` literals. In the case of regular expressions, `{}` to avoid conflicts, since `()` commonly appear.

## Hashes

* Use the newest syntax style for defing hashes.

  ```ruby
  # Bad :'(
  { :key => "value" }

  # Good :|
  { key: "value" }
  ```

  Use hash rockets where it makes sense (i.e. `"foo" => "bar"`).

## Lambdas

* Use the new stabby lambda for single-line body blocks.

  ```ruby
  l = ->(a, b) { puts [a, b] }
  ```
* Use the `lambda` method for multi-line body blocks.

  ```ruby
  l = lambda do |a, b|
    if a == b
      puts a
    end
  end
  ```
* Omit parameter paranthesis when defining a stabby lambda with no parameters.

  ```ruby
  l = -> { puts "foo" }
  ```
* Use `proc` over `Proc.new`.
* Use `proc.call()` for both lambdas and procs.

## Arrays

* Use `Array()` over `[*var]`.

  ```ruby
  foo = "bar"

  # Bad
  foos = [*foo]

  # Good
  foos = Array(foo)
  ```
