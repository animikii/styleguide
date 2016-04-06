# Ruby

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
  sum = 1 + 2
  a, b = 1, 2
  1 > 2 ? true : false; puts "Hi"
  [1, 2, 3].each { |e| puts e }
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

## Documentation

Use [YARD](http://yardoc.org/) and it's conventions for code documentation.

```ruby
# Checks if a {Foo} is the same as a {Bar}.
#
# @param [Foo] a foo
# @param [Bar] a bar
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
* Prefix boolean variables with `is_` or `has_` when possible.

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
    #code
  end
  ```
* Use `each` to iterate over `Enumerable` objects.
* Don't use `then` in a multi-line `if`.
* Only use the ternary operator if the all expressions are trivial.

  ```ruby
  completed? ? "Accepted" : "Denied"
  ```
* Don't use `and` or `or` keywords. Stick to `&&` and `||`.
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
* Don't use parenthesis around the condition if an `if`, `unless`, or `while` **unless** you are assigning a value.

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
