# Mediator Pattern

## Problem
Managing complex communication and interactions between multiple objects can lead to tight coupling and spaghetti code

## Solution
Mediator design pattern provides:
- Centralized control and coordination of interactions between objects.
- Decouples objects by promoting indirect communication through a mediator.
- Simplifies object interactions and reduces dependencies.
- Enhances flexibility and maintainability.

## When To Use
Use the Mediator pattern when:
- You have a set of objects that need to communicate with each other in complex ways.
- Direct communication between objects leads to tight coupling and a lack of flexibility.
- You want to decouple objects by promoting indirect communication through a mediator.
- You want to simplify and manage complex interactions between objects.

## Example
```ruby
# Mediator Interface
class Mediator
  def send_message(message, sender)
    raise NotImplementedError, "Subclasses must implement the send_message method."
  end
end

# Concrete Mediator
class ChatroomMediator < Mediator
  attr_accessor :users

  def initialize
    @users = []
  end

  def add_user(user)
    @users << user
    user.mediator = self
  end

  def send_message(message, sender)
    @users.each do |user|
      user.receive_message(message, sender) unless user == sender
    end
  end
end

# Colleague
class User
  attr_accessor :name, :mediator

  def initialize(name)
    @name = name
  end

  def send_message(message)
    @mediator.send_message(message, self)
  end

  def receive_message(message, sender)
    puts "#{@name} received a message from #{sender.name}: #{message}"
  end
end

# Client code
mediator = ChatroomMediator.new

user1 = User.new("John")
user2 = User.new("Alice")
user3 = User.new("Bob")

mediator.add_user(user1)
mediator.add_user(user2)
mediator.add_user(user3)

user1.send_message("Hello, everyone!")
user2.send_message("Hi, John!")
user3.send_message("Hey, Alice!")
```

In this example, we have a Mediator interface that declares the send_message method. The ChatroomMediator is a concrete mediator that manages the communication between users.

The User class represents a colleague object that interacts with other users through the mediator. Each user has a reference to the mediator and can send messages using the send_message method. The mediator is responsible for relaying the message to the other users.

The client code creates a ChatroomMediator and adds users to it. Each user can send a message using the send_message method, which goes through the mediator to reach the other users. The users receive the messages through the receive_message method.

This example demonstrates how the Mediator pattern enables centralized control and coordination of interactions between multiple objects. It decouples the users by promoting indirect communication through the mediator, simplifying the object interactions and reducing dependencies.