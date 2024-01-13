## EventCallbacks
EventCallbacks is a Kristal library that exposes event calls made by `Kristal.callEvent` for objects.

### Usage:
```lua
Mod.libs.EventCallbacks.subscribe(eventName, obj, func)
```

Sets `func(obj, ...)` to be called whenever `Kristal.callEvent(eventName)` is called.
If object `obj` is already subscribed to the event, the new `func` will replace the old.

```lua
Mod.libs.EventCallbacks.unsubscribe(eventName, obj)
```

Removes the call to `func(obj, ...)` whenever `Kristal.callEvent(eventName)` is called.
Omitting `eventName` unsubscribes all events from `obj`.

### Example:
This is a simple example of an object that recieves `onKeyPressed` events, and prints the key pressed to console:
```lua
local Keylogger, super = Class(Object, "Keylogger")

function Keylogger:init(x,y)
    super.init(self, x,y)
    Mod.libs.EventCallbacks.subscribe("onKeyPressed", self, self.onKeyPressed)
end

function Keylogger:onRemove()
    Mod.libs.EventCallbacks.unsubscribe(self)
end

function Keylogger:onKeyPressed(key, is_repeat)
    print(key, is_repeat)
end

return Keylogger
```
