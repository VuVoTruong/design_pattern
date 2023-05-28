# Memento Pattern

## Problem
Need to capture and restore the internal state of an object without violating encapsulation

## Solution
Memento design pattern provides:
- Ability to capture and restore the internal state of an object.
- Allows objects to be restored to a previous state.
- Preserves encapsulation by keeping the state private.
- Supports undo/redo functionality.

## When To Use
Use the Memento pattern when:
- You need to capture and restore the state of an object.
- You want to save and manage different versions of an object's state.
- You want to implement undo/redo functionality.
- You want to preserve encapsulation while providing state restoration.

## Example
```ruby
# Memento
class EditorMemento
  attr_reader :content

  def initialize(content)
    @content = content
  end
end

# Originator
class TextEditor
  attr_accessor :content

  def initialize(content)
    @content = content
  end

  def create_memento
    EditorMemento.new(content)
  end

  def restore_memento(memento)
    @content = memento.content
  end
end

# Caretaker
class UndoManager
  attr_accessor :mementos

  def initialize
    @mementos = []
  end

  def save_state(editor)
    mementos << editor.create_memento
  end

  def undo(editor)
    return unless can_undo?

    editor.restore_memento(mementos.pop)
  end

  def can_undo?
    !mementos.empty?
  end
end

# Client code
text_editor = TextEditor.new("Hello, World!")
undo_manager = UndoManager.new

puts "Initial content: #{text_editor.content}"

# Save state
undo_manager.save_state(text_editor)

text_editor.content = "Modified content"
puts "After modification: #{text_editor.content}"

# Undo
undo_manager.undo(text_editor)
puts "After undo: #{text_editor.content}"

```

In this example, we have a TextEditor class representing the originator, which contains the content to be edited. The EditorMemento class represents the memento that stores the state of the TextEditor.

The UndoManager class acts as the caretaker and manages the mementos. It provides methods to save the state of the TextEditor and to undo the changes by restoring the previous state from the memento.

The client code creates a TextEditor instance with an initial content. It then saves the state using the UndoManager. The content is modified, and then the undo operation is performed, which restores the previous state.

This example showcases how the Memento pattern allows capturing and restoring the state of an object. It enables undo/redo functionality and provides a way to manage different versions of an object's state.

