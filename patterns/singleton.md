# Singleton Pattern

## Problem
We need to have a single instance of a certain class across the whole application.

## Solution
In the **Singleton** pattern, the access to the constructor is restricted so that it cannot be instantiated. So, the creation of the single instance is done inside the class and is held as a class variable. It can be accessed through a getter across the application.

## Example
Let's consider the implementation of a logger class:

```ruby
class SimpleLogger
  attr_accessor :level

  ERROR = 1
  WARNING = 2
  INFO = 3
  
  def initialize
    @log = File.open("log.txt", "w")
    @level = WARNING
  end

  def error(msg)
    @log.puts(msg)
    @log.flush
  end

  def warning(msg)
    @log.puts(msg) if @level >= WARNING
    @log.flush
  end

  def info(msg)
    @log.puts(msg) if @level >= INFO
    @log.flush
  end
end
```

Logging is a feature used across the whole application, so it makes sense that there should only be a single instance of the logger. We can make sure that nobody instantiates the `SimpleLogger` class twice by making its constructor private:

```ruby
class SimpleLogger

  # Lots of code deleted...
  @@instance = SimpleLogger.new

  def self.instance
    return @@instance
  end

  private_class_method :new
end

SimpleLogger.instance.info('Computer wins chess game.')
```

We can get the same behavior by including the `Singleton` module, so that we can avoid duplicating code if we create several singletons:

```ruby
require 'singleton'

class SimpleLogger
  include Singleton
  # Lots of code deleted...
end
```

## Example 2
```ruby
class SingletonClass
  @@instance = SingletonClass.new

  private_class_method :new

  def self.instance
    @@instance
  end

  def say_hello
    puts "Hello, I am a Singleton!"
  end
end

# Usage
singleton = SingletonClass.instance
singleton.say_hello

# Trying to create a new instance will result in an error
# new_instance = SingletonClass.new
#=> private method `new' called for SingletonClass:Class (NoMethodError)
```
In this example, the *SingletonClass* is designed as a singleton. The class has a private class method *new* to prevent direct instantiation of objects. Instead, it provides a class method *instance* that returns the single instance of the class.

When using the *SingletonClass*, you can obtain the instance by calling *SingletonClass.instance*. Once you have the instance, you can call its methods as usual.

Trying to create a new instance using *SingletonClass.new* will result in an error because the new method is private.

The Singleton pattern ensures that only one instance of the class is created and provides a global point of access to that instance. It is commonly used when you need to have a single instance shared across multiple parts of your codebase.

