# State Pattern

## Problem
Objects need to change their behavior dynamically based on their internal state.

## Solution
State design pattern provides:
- Allows objects to alter their behavior when their internal state changes.
- Encapsulates each state as a separate class.
- Simplifies complex conditional logic.
- Enhances extensibility and maintainability.

## When To Use
Use the State pattern when:
- Objects have multiple states and their behavior varies based on these states.
- You have complex conditional logic that can be simplified by encapsulating each state in a separate class.
- You want to avoid using large switch or if-else statements to handle different states.

## Example
```ruby
# State Interface
class OrderState
  def ship(order)
    raise NotImplementedError, "Subclasses must implement the ship method."
  end

  def cancel(order)
    raise NotImplementedError, "Subclasses must implement the cancel method."
  end
end

# Concrete States
class NewOrderState < OrderState
  def ship(order)
    puts "Shipping the order."
    order.state = ShippedOrderState.new
  end

  def cancel(order)
    puts "Canceling the order."
    order.state = CanceledOrderState.new
  end
end

class ShippedOrderState < OrderState
  def ship(order)
    puts "Order has already been shipped."
  end

  def cancel(order)
    puts "Cannot cancel a shipped order."
  end
end

class CanceledOrderState < OrderState
  def ship(order)
    puts "Cannot ship a canceled order."
  end

  def cancel(order)
    puts "Order has already been canceled."
  end
end

# Context
class Order
  attr_accessor :state

  def initialize
    @state = NewOrderState.new
  end

  def ship
    @state.ship(self)
  end

  def cancel
    @state.cancel(self)
  end
end

# Client code
order = Order.new
order.ship
order.cancel
order.ship
```

In this example, we have an Order class that represents the context in which the state changes. It has an attribute state which holds the current state of the order.

We define a OrderState interface that declares the common behavior for all states. The concrete state classes, such as NewOrderState, ShippedOrderState, and CanceledOrderState, implement the state interface and define behavior specific to each state.

The client code creates an Order object and initially sets its state to NewOrderState. The order can be shipped or canceled by calling the ship and cancel methods. The behavior of these methods depends on the current state of the order.

This example showcases how the State pattern allows objects to change their behavior dynamically based on their internal state. It encapsulates each state as a separate class and simplifies complex conditional logic.

