# Adapter Pattern

## Problem
We want an object talk to some other object but their interfaces don't match.

## Solution
We simply wrap the **adaptee** with our new **adapter** class. This class implements an interface that the invoker understands, although all the work is performed by the adapted object.

## When To Use
- When we are working with two incompatible systems or class or interface, the adapter pattern can be very powerful to use. It makes the code simpler, consistent, and easy to reason about.
- Whenever we have several objects or methods doing something but have different implementations or different syntaxes, an adapter pattern can be definitely a good option

## Example
Let's think of a class that takes two open files (a reader and a writer) and encrypts a file.

```ruby
c# Adaptee: Existing Component with incompatible interface
class LegacyPrinter
  def initialize(text)
    @text = text
  end

  def print_out
    puts "Legacy Printer: #{@text}"
  end
end

# Target: Desired interface
class Printer
  def initialize(text)
    @text = text
  end

  def print
    raise NotImplementedError, "Subclasses must implement the print method."
  end
end

# Adapter: Adapts the Adaptee to the Target interface
class PrinterAdapter < Printer
  def initialize(legacy_printer)
    @legacy_printer = legacy_printer
  end

  def print
    @legacy_printer.print_out
  end
end

# Usage
text = "This is a text to be printed."

legacy_printer = LegacyPrinter.new(text)
legacy_printer.print_out
# Output: Legacy Printer: This is a text to be printed.

printer_adapter = PrinterAdapter.new(legacy_printer)
printer_adapter.print
# Output: Legacy Printer: This is a text to be printed.
```
In this example, we have an existing component **LegacyPrinter** that has an incompatible interface. We want to use this legacy printer in our code, but we also have a **Printer** class that represents our desired interface.

To make the **LegacyPrinter** compatible with the **Printer** interface, we create an **Adapter** class called **PrinterAdapter**. This adapter class inherits from the **Printer** class and wraps an instance of the **LegacyPrinter** class.

The **PrinterAdapter** implements the print method of the **Printer** interface by delegating the call to the **print_out** method of the **LegacyPrinter**.

In the usage section, we demonstrate both the direct use of the **LegacyPrinter** and the use of the **PrinterAdapter**. When using the **LegacyPrinter**, the output shows the legacy format. When using the **PrinterAdapter**, the output is the same, but it goes through the adapted interface.

The **Adapter** pattern allows objects with incompatible interfaces to work together. It acts as a bridge between the client code and the legacy component, allowing the client to use the legacy code through a common interface.

