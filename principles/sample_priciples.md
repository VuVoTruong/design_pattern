# Principles

## Program to an interface, not an implementation
Not good
```ruby
class Car
  def drive
  end
end

class Motor
  def drive
  end
end

class Plane
  def fly
  end
end
```

OK
```ruby
class Vehicle
  def travel
  end
end

class Car < Vehicle
end

class Motor < Vehicle
end

class Plane < Vehicle
end
```

## Prefer composition over inheritance

Not good
```ruby
class Vehicle
  def start_engine
  end
  def stop_engine
  end
end

class Car < Vehicle
end

class Bike < Vehicle
end

#tách 2 class
class Vehicle
  def start_engine
  end

  def stop_engine
  end
end

class Bike < VehicleNoEngine
end

class Car < VehicleEngine
end

class VehicleEngine < Vehicle
  def start_engine
  end
  def stop_engine
  end
end

class VehicleNoEngine < Vehicle
end
```

Good
```ruby
class Engine
  def start
  end
  def stop
  end
end

class Car < Vehicle
  def initialize
    @engine = Engine.new
  end
  def sunday_drive
    @engine.start
    @engine.stop
  end
end
```
## Prefer composition over inheritance
Sample OK
```ruby
class Engine
  def start
  end
  def stop
  end
end

class Car < Vehicle
  def initialize
    @engine = Engine.new
  end
  def sunday_drive
    @engine.start
    @engine.stop
  end
end
```

## Delegate, delegate, delegate
Sample OK
```ruby
class Car < Vehicle
  def initialize
    @engine = Engine.new
  end
 def sunday_drive
    start_engine
    stop_engine
  end
  def start_engine
    @engine.start
  end
  def stop_engine
    @engine.stop
  end
end
```
## You ain’t gonna need it