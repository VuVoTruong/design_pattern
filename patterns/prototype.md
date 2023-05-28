# Prototype Pattern

## Problem
Creating new objects by cloning existing objects can be complex and error-prone.

## Solution
Prototype design pattern provides:
- A way to create new objects by copying existing objects (prototypes).
- Avoids the need for complex initialization and reduces object creation overhead.
- Allows dynamic creation of objects at runtime.
- Promotes flexibility and easy customization.

## When To Use
Use the Prototype pattern when:
- You want to create new objects by cloning existing ones.
- The object creation process is complex or resource-intensive.
- You need to customize object creation at runtime.
- You want to avoid subclassing to create new objects.

## Example
```ruby
# Abstract Prototype
class Character
  attr_accessor :name, :health

  def initialize(name, health)
    @name = name
    @health = health
  end

  def clone
    raise NotImplementedError, "Subclasses must implement clone method"
  end
end

# Concrete Prototype: Warrior Character
class Warrior < Character
  attr_accessor :weapon

  def initialize(name, health, weapon)
    super(name, health)
    @weapon = weapon
  end

  def clone
    Warrior.new(name, health, weapon)
  end
end

# Concrete Prototype: Mage Character
class Mage < Character
  attr_accessor :spell

  def initialize(name, health, spell)
    super(name, health)
    @spell = spell
  end

  def clone
    Mage.new(name, health, spell)
  end
end

# Client code
warrior_prototype = Warrior.new("Warrior", 100, "Sword")
warrior_clone = warrior_prototype.clone

mage_prototype = Mage.new("Mage", 80, "Fireball")
mage_clone = mage_prototype.clone

# Output
puts warrior_clone.name # Output: Warrior
puts warrior_clone.health # Output: 100
puts warrior_clone.weapon # Output: Sword

puts mage_clone.name # Output: Mage
puts mage_clone.health # Output: 80
puts mage_clone.spell # Output: Fireball
```

In this example, we have an abstract prototype class Character, which defines the interface for cloning characters.
It has two concrete subclasses, Warrior and Mage, which implement the cloning behavior by overriding the clone method.

The client code creates instances of the concrete prototypes (warrior_prototype and mage_prototype) and clones them to create new instances (warrior_clone and mage_clone). The cloned objects retain the attributes of the prototypes but are separate instances.

This example showcases how the Prototype pattern allows us to create new objects by cloning existing ones, in this case, game characters. It provides a convenient way to customize and create variations of objects without the need for complex initialization or subclassing.