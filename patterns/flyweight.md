# Flyweight Pattern

## Problem
Managing large numbers of fine-grained objects can lead to excessive memory usage and performance issues

## Solution
Flyweight design pattern provides:
- Efficient sharing of objects to minimize memory usage.
- Separates intrinsic and extrinsic object state.
- Improves performance by reusing shared objects.
- Reduces the overall number of objects created.

## When To Use
Use the Flyweight pattern when:
- You need to manage a large number of objects with shared characteristics.
- The object state can be divided into intrinsic (shared) and extrinsic (context-specific) parts.
- You want to reduce memory consumption and improve performance.
- You want to cache and reuse objects to avoid repeated instantiation.

## Example
```ruby
# Flyweight Factory
class CharacterFactory
  def initialize
    @characters = {}
  end

  def get_character(char)
    if @characters[char]
      @characters[char]
    else
      new_character = Character.new(char)
      @characters[char] = new_character
      new_character
    end
  end
end

# Flyweight
class Character
  attr_reader :char

  def initialize(char)
    @char = char
  end

  def render(font_size)
    puts "Rendering character #{@char} with font size #{font_size}."
  end
end

# Client code
factory = CharacterFactory.new

character1 = factory.get_character('A')
character1.render(12)

character2 = factory.get_character('A')
character2.render(16)

character3 = factory.get_character('B')
character3.render(14)

character4 = factory.get_character('B')
character4.render(18)
```

In this example, we have a CharacterFactory that acts as a flyweight factory. It manages a collection of Character objects and provides a method get_character to retrieve a shared flyweight object based on the given character.

The Character class represents the flyweight object. It has an intrinsic state char that stores the character itself. The render method takes the font size as an extrinsic state and performs the rendering operation specific to that character.

The client code uses the flyweight factory to retrieve flyweight objects (character1, character2, character3, character4) based on different characters. The objects are shared and reused if they already exist, reducing memory usage.

Each flyweight object is rendered with a specific font size, which represents the extrinsic state. The objects maintain their intrinsic state (character) while the extrinsic state can vary based on the client's context.

This example demonstrates how the Flyweight pattern allows efficient sharing of objects with common characteristics. It reduces memory consumption by reusing shared objects and separates the intrinsic and extrinsic state to improve performance.