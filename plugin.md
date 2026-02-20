# Violent Plugin Docs

Create a `.lua` file in `urexecutorsworkspacefolder/vt/plugins` and initialize the plugin:

```lua
local VT = ...
local UI, Player, Util = VT.UI, VT.Player, VT.Util
```

## UI Initialization

### `UI.Init(id)`

Creates a main tab inside the Miscellaneous -> Plugins menu. Returns the frame name.

- `id`: Unique string for the tab identifier.

### `UI.CreateSubTab(parent, id, title)`

Creates a button that opens a nested page. Returns the internal sub-frame name.

- `parent`: The internal frame name of the page you are placing the button in.
- `title`: The text displayed at the top of the menu when opened.

### `UI.Notify(title, content, duration, type)`

Sends a menu notification.

- `title`: Header text (colored based on type).
- `content`: Description text.
- `type`: String - "normal", "warn", or "error".

## Adding UI Elements
All Add functions return the button instance, which is required to use Getters. Callbacks receive the new value as the first argument.

### `UI.AddButton(parent, id, text, desc, callback)`

Standard button.

### `UI.AddToggle(parent, id, text, default, desc, callback)`

Checkmark toggle. Callback argument: boolean.

### `UI.AddSlider(parent, id, text, default, min, max, inc, desc, callback)`

Numeric slider. Users can click the value to type. Callback argument: number.

### `UI.AddTextBox(parent, id, text, default, desc, callback)`

Prompts for text input. Callback argument: string.

### `UI.AddColorPicker(parent, id, text, default, desc, callback)`

Color selection button. Callback argument: Color3. Callback is optional.

### `UI.AddLabel(parent, text)`

Displays a header with an underline.

### `UI.AddSeparator(parent)`

Adds a horizontal organizational line.

## Getters

Pass the variable saved from an Add function to read its current state at any time.

- `UI.GetToggleVal(instance)`: Returns boolean.
- `UI.GetSliderVal(instance)`: Returns number (or string if created with a list).
- `UI.GetTextBoxVal(instance)`: Returns string.
- `UI.GetColorVal(instance)`: Returns Color3.

## Player & Utilities

- `Player.LocalPlayer`: Reference to the local player.
- `Player.Character`: Reference to the current character model.
- `Player.GetRoot()`: Returns the HumanoidRootPart or Torso.
- `Player.Teleport(cframe)`: Instantly moves or tweens the player to a CFrame.
- `Util.Copy(text)`: Copies a string to the clipboard.

## Example

```lua
local plugin = ...
local UI = plugin.UI
local mainTab = UI.Init("boi it works")

UI.AddLabel(mainTab, "plugin test")
local speedTgl = UI.AddToggle(mainTab, "speed", "Enable Speed", false, "test desc12")
local subTab = UI.CreateSubTab(mainTab, "Advanced")
local anothersubtab = UI.CreateSubTab(subTab, "Advanced2")
UI.AddLabel(anothersubtab , "wwooooowo")

UI.AddLabel(subTab, "test1")

UI.AddButton(subTab, "checkMain", "blablabla", "testdesc", function()
    local isEnabled = UI.GetToggleVal(speedTgl)
    local status = isEnabled and "Enabled" or "Disabled"
    UI.Notify("Speed toggle test67", "The speed toggleeeeee is: " .. status, 5, "normal")
end)

UI.AddButton(subTab, "notifySub", "Sub tab Test", "Simple notif", function()
    UI.Notify("test41", "are u really reading ts", 3, "warn")
end)
```
