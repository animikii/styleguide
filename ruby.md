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
