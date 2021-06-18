# wrap

A small library that lets you wrap methods around a function. This is useful for when you need to pass a function as an argument.

## Installation

The wrap.lua file should be dropped into an existing project and required by it.

```lua
wrap = require "wrap"
```

You can then use `wrap` to create a new wrapper with `wrap.new(obj)`, where you pass the object you want to use wrap with.

```lua
self.wrap = wrap.new(self)
```

## Usage

### Function wrap

Let's assume your object has the function `foo`. We can then use wrap like this:

```lua
f = self.wrap:foo()
```

Which is equal to this:

```lua
f = function () self:foo() end
```

### Properties wrap

By calling `wrap(props)` you get a function that upon calling updates the passed properties of your object.

```lua
f = self.wrap({bar = 10})
```

Which is equal to this:

```lua
f = function () self.bar = 10 end
```

### Chaining

By using `wrap:chain()` you can chain multiple methods. Finish the chain with `:done()`.

```lua
f = self.wrap:chain():foo()({bar = 10, test = "example"}):foobar("Hello world"):done()
```

Which is equal to this:

```lua
f = function ()
    self:foo()
    self.bar = 10
    self.test = "example"
    self:foobar("Hello world")
end
```

## License

This library is free software; you can redistribute it and/or modify it under the terms of the MIT license. See [LICENSE](LICENSE) for details.