# Abstract Factory Pattern

## Problem
Creating families of related objects without specifying concrete classes.

## Solution
Abstract Factory design pattern provides:
- Encapsulation of object creation logic
- Generic interface for creating objects
- Loose coupling and high cohesion
- Support for multiple implementations of object families

## Advantage
- Abstract Factory Pattern isolates the client code from concrete (implementation) classes.
- It eases the exchanging of object families.
- It promotes consistency among objects.

## When To Use
- You need to create families of related objects.
- You want to decouple client code from specific object implementations.
- You need to support multiple variations of object families.
- You want to promote flexibility, modularity, and extensibility.

## Example
```ruby
# Abstract Factory Interface
class GUIFactory
  def create_button
    raise NotImplementedError, "Subclasses must implement create_button method"
  end

  def create_window
    raise NotImplementedError, "Subclasses must implement create_window method"
  end
end

# Concrete Factory: Windows GUI Factory
class WindowsFactory < GUIFactory
  def create_button
    WindowsButton.new
  end

  def create_window
    WindowsWindow.new
  end
end

# Concrete Factory: MacOS GUI Factory
class MacOSFactory < GUIFactory
  def create_button
    MacOSButton.new
  end

  def create_window
    MacOSWindow.new
  end
end

# Abstract Product: Button
class Button
  def render
    raise NotImplementedError, "Subclasses must implement render method"
  end
end

# Concrete Product: Windows Button
class WindowsButton < Button
  def render
    puts "Rendering a Windows button."
  end
end

# Concrete Product: MacOS Button
class MacOSButton < Button
  def render
    puts "Rendering a MacOS button."
  end
end

# Abstract Product: Window
class Window
  def render
    raise NotImplementedError, "Subclasses must implement render method"
  end
end

# Concrete Product: Windows Window
class WindowsWindow < Window
  def render
    puts "Rendering a Windows window."
  end
end

# Concrete Product: MacOS Window
class MacOSWindow < Window
  def render
    puts "Rendering a MacOS window."
  end
end

# Client code
def create_gui(factory)
  button = factory.create_button
  window = factory.create_window

  button.render
  window.render
end

# Usage
windows_factory = WindowsFactory.new
macos_factory = MacOSFactory.new

create_gui(windows_factory) # Creates Windows GUI components
create_gui(macos_factory)   # Creates MacOS GUI components
```

In this example, we have an abstract factory *GUIFactory* with two abstract methods *create_button* and *create_window*.
We then have two concrete factory classes *WindowsFactory* and *MacOSFactory* that implement these methods to create platform-specific buttons and windows.

The abstract products *Button* and *Window* define the common interface for different types of buttons and windows, while the concrete product classes *WindowsButton*, *MacOSButton*, *WindowsWindow*, and *MacOSWindow* provide the platform-specific implementations.

The client code demonstrates how to use the abstract factory to create GUI components. By passing different concrete factory objects (*windows_factory* and *macos_factory*), we can create and render platform-specific buttons and windows.

This example illustrates how the Abstract Factory pattern enables the creation of families of related objects (buttons and windows) without tightly coupling the client code to specific platform implementations, promoting flexibility and modularity.
