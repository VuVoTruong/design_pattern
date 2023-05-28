# Bridge Pattern

## Problem
Decoupling an abstraction from its implementation can be challenging and lead to a rigid and complex codebase

## Solution
Bridge design pattern provides:
- Separation of an abstraction from its implementation.
- Allows changes to the abstraction and implementation independently.
- Promotes loose coupling and flexibility.
- Facilitates the extension of both abstractions and implementations.

## When To Use
Use the Bridge pattern when:
- You want to separate an abstraction from its implementation.
- You need to change or extend both the abstraction and implementation independently.
- You want to avoid a rigid and tightly coupled codebase.
- You want to promote flexibility and future scalability.

## Example
```ruby
# Abstraction
class Shape
  attr_reader :renderer

  def initialize(renderer)
    @renderer = renderer
  end

  def draw
    raise NotImplementedError, "Subclasses must implement draw method"
  end
end

# Implementor
class Renderer
  def render_circle(radius)
    raise NotImplementedError, "Subclasses must implement render_circle method"
  end
end

# Concrete Abstraction: Circle
class Circle < Shape
  attr_reader :x, :y, :radius

  def initialize(renderer, x, y, radius)
    super(renderer)
    @x = x
    @y = y
    @radius = radius
  end

  def draw
    renderer.render_circle(radius)
  end
end

# Concrete Implementor: VectorRenderer
class VectorRenderer < Renderer
  def render_circle(radius)
    puts "Drawing a circle of radius #{radius} using Vector Renderer."
  end
end

# Concrete Implementor: RasterRenderer
class RasterRenderer < Renderer
  def render_circle(radius)
    puts "Drawing a circle of radius #{radius} using Raster Renderer."
  end
end

# Usage
vector_renderer = VectorRenderer.new
raster_renderer = RasterRenderer.new

circle1 = Circle.new(vector_renderer, 5, 10, 15)
circle1.draw

circle2 = Circle.new(raster_renderer, 2, 4, 8)
circle2.draw
```

In this example, we have an abstraction Shape that takes a Renderer object in its constructor. It defines the method draw, which delegates the rendering functionality to the implementation provided by the renderer.

The Renderer class is the implementor that declares the method render_circle, which is implemented by its concrete subclasses VectorRenderer and RasterRenderer.

The concrete abstraction Circle inherits from Shape and provides its implementation of the draw method. It utilizes the renderer object to render the circle using the specified implementation.

The client code creates instances of the concrete abstractions (circle1 and circle2) with different renderers (vector_renderer and raster_renderer) and calls the draw method to render the circles using the respective implementations.

This example demonstrates how the Bridge pattern separates the abstraction (shape) from the implementation (renderer), allowing them to vary independently. It promotes loose coupling and flexibility, making it easier to add new shapes or renderers in the future.