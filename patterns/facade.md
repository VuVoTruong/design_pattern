# Facade Pattern

## Problem
Complex subsystems with numerous interdependencies can be difficult to understand and use

## Solution
Facade design pattern provides:
- Simplified interface to a complex subsystem.
- Hides the complexity and interdependencies of the subsystem.
- Improves code readability and maintainability.
- Promotes loose coupling and encapsulation.

## When To Use
Use the Facade pattern when:
- You want to provide a simple and unified interface to a complex subsystem.
- You need to reduce coupling between clients and subsystems.
- You want to hide the complexity of the subsystem and provide a higher-level abstraction.
- You want to improve code organization and maintainability.

## Example
```ruby
# Complex Subsystem: Computer
class CPU
  def freeze
    puts "CPU: Freezing..."
  end

  def execute
    puts "CPU: Executing..."
  end
end

class Memory
  def load(address, data)
    puts "Memory: Loading data '#{data}' into address '#{address}'."
  end
end

class HardDrive
  def read(sector, size)
    puts "Hard Drive: Reading #{size} bytes from sector #{sector}."
  end
end

# Facade
class ComputerFacade
  attr_reader :cpu, :memory, :hard_drive

  def initialize
    @cpu = CPU.new
    @memory = Memory.new
    @hard_drive = HardDrive.new
  end

  def start
    cpu.freeze
    memory.load(0, "BOOT_ADDRESS")
    hard_drive.read(BOOT_SECTOR, BOOT_SIZE)
    cpu.execute
  end
end

# Client code
computer = ComputerFacade.new
computer.start

```
In this example, we have a complex subsystem represented by different computer components: CPU, Memory, and HardDrive. Each component has specific functionalities defined.

The ComputerFacade acts as a facade that simplifies the usage of the computer components. It initializes instances of CPU, Memory, and HardDrive and provides a start method that orchestrates the steps needed to start the computer.

The client code creates an instance of the ComputerFacade and calls the start method on it. The facade internally manages the interactions between the components, such as freezing the CPU, loading data into memory, and reading from the hard drive.

By using the facade, the client code does not need to deal with the complexities of the individual components. It provides a higher-level interface that abstracts away the details of the subsystem.

This example demonstrates how the Facade pattern simplifies the usage of a complex subsystem (in this case, starting a computer) by providing a unified and simplified interface. It promotes code organization, encapsulation, and improves readability.

