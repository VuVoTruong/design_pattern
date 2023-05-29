# Factory Pattern

## Problem
We need to create objects without having to specify the exact class of the object that will be created.

## Solution
The **Factory** pattern is a specialization of the [Template](template_method.md) pattern. We start by creating a generic base class where we don't make the "which class" decision. Instead, whenever it needs to create a new object, it calls a method that is defined in a subclass. So, depending on the subclass we use (**factory**), we create objects of one class or another (**products**).

## Example
Imagine that you are asked to build a simulation of life in a pond that has plenty of ducks:

```ruby
class Pond
  def initialize(number_ducks)
    @ducks = number_ducks.times.inject([]) do |ducks, i|
      ducks << Duck.new("Duck#{i}")
      ducks
    end
  end

  def simulate_one_day
    @ducks.each {|duck| duck.speak}
    @ducks.each {|duck| duck.eat}
    @ducks.each {|duck| duck.sleep}
  end
end

pond = Pond.new(3)
pond.simulate_one_day
```

But how would we model our `Pond` if we wanted to have frogs instead of ducks? In the implementation above, we are specifying in the `Pond`'s initializer that it should be filled up with ducks. So, we'll refactor it so that the decision of creating one type of animal or another is made in a subclass:

```ruby
class Pond
  def initialize(number_animals)
    @animals = number_animals.times.inject([]) do |animals, i|
      animals << new_animal("Animal#{i}")
      animals
    end
  end

  def simulate_one_day
    @animals.each {|animal| animal.speak}
    @animals.each {|animal| animal.eat}
    @animals.each {|animal| animal.sleep}
  end
end

class FrogPond < Pond
  def new_animal(name)
    Frog.new(name)
  end
end

pond = FrogPond.new(3)
pond.simulate_one_day
```

## Example 2
```ruby
# Product interface
class Product
  def operation
    raise NotImplementedError, "Subclasses must implement the operation method."
  end
end

# Concrete Products
class ConcreteProductA < Product
  def operation
    puts "Operation of ConcreteProductA"
  end
end

class ConcreteProductB < Product
  def operation
    puts "Operation of ConcreteProductB"
  end
end

# Factory
class Factory
  def create_product(type)
    case type
    when :product_a
      ConcreteProductA.new
    when :product_b
      ConcreteProductB.new
    else
      raise ArgumentError, "Invalid product type"
    end
  end
end

# Usage
factory = Factory.new

product_a = factory.create_product(:product_a)
product_a.operation
# Output: Operation of ConcreteProductA

product_b = factory.create_product(:product_b)
product_b.operation
# Output: Operation of ConcreteProductB
```
In this example, we have a **Product** interface that defines the common behavior for all products. The **ConcreteProductA** and **ConcreteProductB** classes are the concrete implementations of the product interface.

The **Factory** class is responsible for creating the products. It has a **create_product** method that takes a type parameter and returns the corresponding concrete product based on the type. In this case, it uses a case statement to determine which product to create.

In the usage section, we create an instance of the factory. Then, we can use the factory to create different products by calling **create_product** method with the appropriate type. Finally, we can call the operation method on the created product, and it will execute the specific operation of that product.

The Factory pattern allows for the creation of objects without exposing the instantiation logic to the client. It provides a single point of entry to create different products, and it can encapsulate the complexity of object creation.

