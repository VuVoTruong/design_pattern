# Visitor Pattern

## Problem
Adding new operations to an object structure without modifying its classes.

## Solution
Visitor design pattern provides:
- Separates the operations from the objects on which they operate.
- Allows adding new operations without modifying the object structure.
- Enhances extensibility by enabling new visitors to be added easily.
- Follows the Open/Closed principle.

## When To Use
Use the Visitor pattern when:
- You have a complex object structure with multiple types of objects.
- You want to add new operations to the objects without modifying their classes.
- The behavior of the objects is likely to change or be extended frequently.
- You want to avoid polluting the object classes with unrelated behavior.

## Example
```ruby
# Visitor Interface
class Visitor
  def visit_file(file)
    raise NotImplementedError, "Subclasses must implement the visit_file method."
  end

  def visit_folder(folder)
    raise NotImplementedError, "Subclasses must implement the visit_folder method."
  end
end

# Concrete Visitors
class SizeVisitor < Visitor
  attr_reader :size

  def initialize
    @size = 0
  end

  def visit_file(file)
    @size += file.size
  end

  def visit_folder(folder)
    folder.elements.each { |element| element.accept(self) }
  end
end

class CountVisitor < Visitor
  attr_reader :count

  def initialize
    @count = 0
  end

  def visit_file(file)
    @count += 1
  end

  def visit_folder(folder)
    @count += 1
    folder.elements.each { |element| element.accept(self) }
  end
end

# Element Interface
class FileSystemElement
  def accept(visitor)
    raise NotImplementedError, "Subclasses must implement the accept method."
  end
end

# Concrete Elements
class File < FileSystemElement
  attr_reader :size

  def initialize(size)
    @size = size
  end

  def accept(visitor)
    visitor.visit_file(self)
  end
end

class Folder < FileSystemElement
  attr_reader :elements

  def initialize
    @elements = []
  end

  def add_element(element)
    @elements << element
  end

  def accept(visitor)
    visitor.visit_folder(self)
  end
end

# Client code
folder = Folder.new

file1 = File.new(100)
file2 = File.new(50)
folder.add_element(file1)
folder.add_element(file2)

subfolder = Folder.new
file3 = File.new(75)
subfolder.add_element(file3)
folder.add_element(subfolder)

size_visitor = SizeVisitor.new
folder.accept(size_visitor)
puts "Total size of files: #{size_visitor.size} bytes"

count_visitor = CountVisitor.new
folder.accept(count_visitor)
puts "Total number of files and folders: #{count_visitor.count}"
```

In this example, we have a file system representation with two types of elements: File and Folder. The FileSystemElement serves as the element interface, which defines the accept method that accepts a visitor.

The Visitor interface declares the visit_file and visit_folder methods, which are implemented by concrete visitor classes (SizeVisitor and CountVisitor). These visitors perform operations on the file system elements.

The client code creates a file system structure with files and folders. Visitors are created to calculate the total size of files (SizeVisitor) and count the number of files and folders (CountVisitor). The visitors traverse the file system structure by calling the accept method on each element, and the appropriate visit methods are invoked based on the element's type.

This example demonstrates how the Visitor pattern separates the operations (visitors) from the objects (file system elements) and allows adding new operations easily without modifying the element classes.

