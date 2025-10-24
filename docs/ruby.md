## Ruby Basics

Ruby is a dynamic, open-source programming language with a focus on simplicity and productivity. It has an elegant syntax that is natural to read and easy to write.

### Install Ruby

You can install Ruby using a version manager like RVM or rbenv.
Here’s how to install Ruby using RVM:

1. Install RVM:
   ```bash
   \curl -sSL https://get.rvm.io | bash -s stable
   ```
2. Load RVM:
   ```bash
   source ~/.rvm/scripts/rvm
   ```
3. Install a specific version of Ruby:
   ```bash
   rvm install 3.1.2
   ```
4. Set the default Ruby version:
   ```bash
   rvm use 3.1.2 --default
   ```
5. Verify the installation:
   ```bash
   ruby -v
   ```
6. List installed Ruby versions:
   ```bash
   rvm list
   ```
7. Switch Ruby versions:
   ```bash
   rvm use <version>
   ```
8. Remove/uninstall a Ruby version:
   ```bash
   rvm uninstall <version>
   ```
9. List all gemsets:
   ```bash
   rvm gemset list
   ```
10. Create a new gemset:
    ```bash
    rvm gemset create <gemset_name>
    ```
11. Delete all gems in the current gemset:
    ```bash
    rvm gemset empty <gemset_name>
    ```
12. Delete a gemset:
    ```bash
    rvm gemset delete <gemset_name>
    ```
13. List all current gems:
    ```bash
    gem list
    ```
14. Install/uninstall a gem:
    ```bash
    gem install <gem_name> [--version/-v <version>]
    gem uninstall <gem_name>
    ```

Here’s how to install Ruby using rbenv:

1. Install rbenv and ruby-build:
   ```bash
   # Using Homebrew on macOS
   brew install rbenv ruby-build
   ```
2. Initialize rbenv:
   ```bash
   rbenv init
   ```
3. Install a specific version of Ruby:
   ```bash
   rbenv install 3.1.2
   ```
4. Set the global Ruby version:
   ```bash
   rbenv global 3.1.2
   ```
5. Verify the installation:

   ```bash
   ruby -v
   ```

   **Cheat Sheet**: https://karloespiritu.github.io/cheatsheets/rbenv/

### Name Conventions

- File names: snake_case (e.g., `my_script.rb`)
- Class names: CamelCase (e.g., `MyClass`)
- Function/method names: snake_case (e.g., `my_method`)
- Variable names: snake_case (e.g., `my_variable`)
- Constants: UPPER_SNAKE_CASE (e.g., `MY_CONSTANT`)

### Basic Syntax

Here are some basic Ruby syntax examples:

```ruby
# Variables
name = "World"
puts "Hello, #{name}!"
# Methods
def greet(name)
  "Hello, #{name}!"
end
puts greet("Ruby")
# Control Structures
if name == "World"
  puts "It's a beautiful day!"
else
  puts "Welcome, #{name}!"
end
# Loops
5.times do |i|
  puts "Iteration #{i}"
end
# Arrays
fruits = ["apple", "banana", "cherry"]
fruits.each do |fruit|
  puts fruit
end
# Hashes
person = {name: "Alice", age: 30}
person.each do |key, value|
  puts "#{key}: #{value}"
end
```

### Variables and Constants

- Variables: dynamically typed, no need to declare type
- Constants: start with an uppercase letter, should not be changed

### Types of Variables, and cycling scope

- `Global Variables`: start with `$` (e.g., `$my_var`), accessible from anywhere in the program
- `Constant Variables`: start with an uppercase letter (e.g., `MY_CONSTANT`), should not be changed once assigned, accessible from anywhere in the program
- `Class Variables`: start with `@@` (e.g., `@@my_var`), accessible within the class and its subclasses
- `Instance Variables`: start with `@` (e.g., `@my_var`), accessible within the instance of the class
- `Local Variables`: start with a lowercase letter or underscore (e.g., `my_var`), accessible only within the scope they are defined

### Data Types

- `Integer`: whole numbers (e.g., `42`, `-7`)
- `Float`: decimal numbers (e.g., `3.14`, `-0.001`)
- `String`: sequence of characters (e.g., `"Hello, World!"`, `'Ruby'`)
- `Boolean`: `true` or `false`
- `Array`: ordered collection of elements (e.g., `[1, 2, 3]`, `["apple", "banana", "cherry"]`)
- `Hash`: key-value pairs (e.g., `{name: "Alice", age: 30}`, `{"key1" => "value1", "key2" => "value2"}`)
- `Date` and `Time`: represent dates and times (e.g., `Date.today`, `Time.now`)
- `Symbol`: lightweight, immutable identifier (e.g., `:my_symbol`, `:name`)
- `NilClass`: represents "nothing" or "no value" (`nil`)

### Functions/Methods

- Define a method using `def` keyword
- Methods can take parameters and return values

```ruby
def add(a, b)
  return a + b
end
result = add(5, 10) # -> 15
```

### Classes and Objects

- Define a class using `class` keyword
- Create objects (instances) of the class using `new` method

```ruby
class Dog
  def bark
    puts "Woof!"
  end
end

dog = Dog.new
dog.bark # -> "Woof!"
```

### Modules

- Define a module using `module` keyword, which is a collection of methods and constants
- Include modules in classes using `include` or `extend`
  - `include`: adds module methods as instance methods
  - `extend`: adds module methods as class methods

```ruby
module Barking
  def bark
    puts "Woof!"
  end
end

class Dog
  include Barking
end

dog = Dog.new
dog.bark # -> "Woof!"
```

### Operators

- Arithmetic Operators: `+`, `-`, `*`, `/`, `%`, `**`

  ```ruby
  # Note "/"
  20 / 10 = 2
  7 / 3 = 2
  7.0 / 3 = 2.33333
  10 / 0 = # -> ZeroDivisionError: divided by 0

  # Float are represented using the IEEE 754 standard
  # IEEE (Institute of Electrical and Electronics Engineer)
  2.3 - 1 = 1.2999999999999998 # 1.3
  0.0 / 0.0 = NaN
  1.0 / 0 = Infinity
  -1.0 / 0 = -Infinity
  ```

- Comparison Operators: `==`, `!=`, `>`, `<`, `>=`, `<=`, `<=>`, `===`, `.eql?`, `equal?`

  ```ruby
  # a = 10, b = 20
  a == b # -> false // 1.0 == 1 -> true
  a != b # -> true
  a > b # -> false
  a >= b # -> false
  a < b # -> true
  a <= b # -> true

  # <=> Combined comparison operator
  # Return 0 if equal, 1 if left is greater, -1 if right is greater
  1 <=> 1 # -> 0
  2 <=> 1 # -> 1
  1 <=> 2 # -> -1

  # === -> true / false, use in case statement
  case 10
  when String
    p 'String here'
  when (1..10)
    p 'Range here'
  end
  # String === 10 # -> false
  # (1..10) === 10 # -> true -> 'Range here'

  # Range
  (1..10) === 10 # -> true
  (1...10) === 10 # -> false
  # NOTE
  10 === (1..10) # -> false, only Class/Module on left side

  # Class
  Integer === 10 # -> true
  Integer === '10' # -> false
  # NOTE
  10 === Integer # -> false

  # .eql? -> true if same type and equal values.
  1.eql?(1.0) # -> false

  # equal? -> true if two objects are the same object in memory.
  a = { test: 1 }
  b = { test: 1 }
  a.equal?(b) # -> false
  c = a
  a.equal?(c) # -> true
  ```

- Assignment Operators: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `**=`

  Parallel Assignment:

  ```ruby
  a, b = 10, 20
  a += 5 # a = a + 5
  b *= 2 # b = b * 2
  ```

- Logical Operators: `and`, `or`, `&&`, `||`, `!`, `not`

  ```ruby
  a = true
  b = false
  a and b # -> false
  a or b # -> true
  a && b # -> false
  a || b # -> true
  !a # -> false
  not b # -> true
  ```

- Ternary Operator: `condition ? true_value : false_value`

  ```ruby
  age = 18
  status = age >= 18 ? "Adult" : "Minor" # -> "Adult"
  ```

- Dot `.` and Double Colon `::` Operators:

  - Dot `.`: used to call methods on objects or access attributes.

    ```ruby
    str = "hello"
    str.upcase # -> "HELLO"
    ```

  - Double Colon `::`: used to access constants, class methods, or modules.

    ```ruby
    module MathModule
      PI = 3.14
      def self.square(x)
        x * x
      end
    end

    MathModule::PI # -> 3.14
    MathModule.square(4) # -> 16
    ```

- Operators Precedence:

  ```ruby
  # Highest to Lowest
  1. Parentheses: ()
  2. Exponentiation: **
  3. Logical NOT: !
  4. Multiplication, Division, Modulus: *, /, %
  5. Addition, Subtraction: +, -
  6. Comparison: ==, !=, >, <, >=, <=, <=>, ===
  7. Logical AND: &&
  8. Logical OR: ||
  9. Ternary: ?:
  10. Assignment: =, +=, -=, *=, /=, %=, **=
  11. Defined?: defined?
  12. Logical negation: not
  13. Logical composition: or, and
  ```

### Control Structures

- Conditional Statements: `if`, `elsif`, `else`, `unless`, `case`
- Loops: `while`, `until`, `for`, `each`, `times`, `loop`
- break, next, redo, retry Statements: https://www.tutorialspoint.com/ruby/ruby_loops.htm

### Common Methods

- String methods: `upcase`, `downcase`, `length`, `split`, `gsub`
- Array methods: `push`, `pop`, `shift`, `unshift`, `each`, `map`, `select`, `reject`, `sort`, `include?`, `compact`, `flatten`, `uniq`, `empty?`
- Hash methods: `keys`, `values`, `each`, `merge`, `delete`, `fetch`, `has_key? (key?)`, `has_value? (value?)`
- Numeric methods: `to_i`, `to_f`, `round`, `ceil`, `abs`

### Exceptions

- Handle exceptions using `begin`, `rescue`, and `ensure` blocks
- Raise exceptions using `raise` keyword

```ruby
begin
  # Code that may raise an exception
  result = 10 / 0
rescue ZeroDivisionError
  puts "Division by zero error occurred"
rescue StandardError => e
  puts "An error occurred: #{e.message}"
else
  puts "Otherwise block executed if no exception"
ensure
  puts "This will always execute"
end
```
