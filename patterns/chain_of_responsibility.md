# Chain of Responsibility

## Problem
Need to process a request through a series of handlers, with each handler having the ability to handle or pass the request to the next handler.

## Solution
Chain of Responsibility design pattern provides:
- Decoupling of sender and receiver of a request.
- Allows multiple handlers to process a request in a chain.
- Dynamically configures the chain and order of handlers.
- Provides flexibility and extensibility.

## When To Use
Use the Chain of Responsibility pattern when:
- You have a series of objects that can handle a request.
- You want to decouple the sender from the receiver and allow multiple receivers to handle the request.
- You want to dynamically configure the handling chain or change the order of handlers.
- You want to avoid coupling the sender to specific receiver classes.

## Example
```ruby
# Handler Interface
class Handler
  attr_accessor :successor

  def handle_request(request)
    raise NotImplementedError, "Subclasses must implement the handle_request method."
  end
end

# Concrete Handlers
class AuthenticationHandler < Handler
  def handle_request(request)
    if request[:type] == :authentication
      puts "AuthenticationHandler: Handling authentication request."
    elsif successor
      successor.handle_request(request)
    else
      puts "No handler can process the request: #{request[:type]}"
    end
  end
end

class AuthorizationHandler < Handler
  def handle_request(request)
    if request[:type] == :authorization
      puts "AuthorizationHandler: Handling authorization request."
    elsif successor
      successor.handle_request(request)
    else
      puts "No handler can process the request: #{request[:type]}"
    end
  end
end

class LoggingHandler < Handler
  def handle_request(request)
    if request[:type] == :logging
      puts "LoggingHandler: Handling logging request."
    elsif successor
      successor.handle_request(request)
    else
      puts "No handler can process the request: #{request[:type]}"
    end
  end
end

# Client code
authentication_handler = AuthenticationHandler.new
authorization_handler = AuthorizationHandler.new
logging_handler = LoggingHandler.new

authentication_handler.successor = authorization_handler
authorization_handler.successor = logging_handler

authentication_handler.handle_request(type: :logging)
authentication_handler.handle_request(type: :authorization)
authentication_handler.handle_request(type: :authentication)
authentication_handler.handle_request(type: :unknown)

```

In this example, we have three concrete handlers: AuthenticationHandler, AuthorizationHandler, and LoggingHandler. Each handler is responsible for handling a specific type of request.

The handlers are connected in a chain where each handler has a reference to its successor. If a handler cannot handle a request, it passes the request to the next handler in the chain until either a handler handles the request or the end of the chain is reached.

The client code creates instances of the concrete handlers and sets up the chain by assigning the successor for each handler. Then, it sends requests to the first handler in the chain using the handle_request method.

Each handler checks the type of the request and handles it if it can. If it cannot handle the request, it passes the request to the next handler in the chain until a handler can handle the request or there are no more handlers left.

This example showcases how the Chain of Responsibility pattern allows a series of handlers to process requests in a flexible and extensible manner. It decouples the sender from the receiver, promotes code reusability, and simplifies the client code.