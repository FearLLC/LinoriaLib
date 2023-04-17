# LinoraLib :)
Loading - 
```lua
local repo = 'https://raw.githubusercontent.com/FearLLC/LinoriaLib/main/'

local Library = loadstring(game:HttpGet(repo .. 'Library.lua'))()
local ThemeManager = loadstring(game:HttpGet(repo .. 'addons/ThemeManager.lua'))()
local SaveManager = loadstring(game:HttpGet(repo .. 'addons/SaveManager.lua'))()
```
Createing Window - 
```lua
local Window = Library:CreateWindow({
    Title = 'Example menu',
    Center = true,
    AutoShow = true,
    TabPadding = 8
})
```
Watermark and Notifications - 
```lua
Library:SetWatermark(game.PlaceId..' | Fear - V1 | '..game:GetService("Players").LocalPlayer.Name)
Library:Notify(" - Loaded - ", 3)
```
Createing Tabs - 
```lua
local Tabs = {
    Main = Window:AddTab('Main'),
    ['UI Settings'] = Window:AddTab('UI Settings'),
}
```
Creating Group Boxes - 
```lua
local LeftGroupBox = Tabs.Main:AddLeftGroupbox('Left')
local RightGroupBox = Tabs.Main:AddRightGroupbox('Right')
```
Creating Toggle - 
```lua
LeftGroupBox:AddToggle('MyToggle', {
    Text = 'This is a toggle',
    Default = true, -- Default value (true / false)
    Tooltip = 'This is a tooltip', -- Information shown when you hover over the toggle

    Callback = function(Value)
        print('[cb] MyToggle changed to:', Value)
    end
})
```
Createing Button - 
```lua
LeftGroupBox:AddButton({
    Text = 'Button',
    Func = function()
        print('You clicked a button!')
    end,
    DoubleClick = false,
    Tooltip = 'This is the main button'
})
```
Createing Label - 
```lua
LeftGroupBox:AddLabel('This is a label')
LeftGroupBox:AddLabel('This is a label\n\nwhich wraps its text!', true)
```
Creating Divider - 
```lua
LeftGroupBox:AddDivider()
```
Create Slider - 
```lua
LeftGroupBox:AddSlider('MySlider', {
    Text = 'This is my slider!',
    Default = 0,
    Min = 0,
    Max = 5,
    Rounding = 1,
    Compact = false,

    Callback = function(Value)
        print('[cb] MySlider was changed! New value:', Value)
    end
})
```
Create Input - 
```lua
LeftGroupBox:AddInput('MyTextbox', {
    Default = 'My textbox!',
    Numeric = false, -- true / false, only allows numbers
    Finished = false, -- true / false, only calls callback when you press enter

    Text = 'This is a textbox',
    Tooltip = 'This is a tooltip', -- Information shown when you hover over the textbox

    Placeholder = 'Placeholder text', -- placeholder text when the box is empty
    -- MaxLength is also an option which is the max length of the text

    Callback = function(Value)
        print('[cb] Text updated. New text:', Value)
    end
})
```
Create Dropdown - 
```lua
LeftGroupBox:AddDropdown('MyDropdown', {
    Values = { 'This', 'is', 'a', 'dropdown' },
    Default = 1, -- number index of the value / string
    Multi = false, -- true / false, allows multiple choices to be selected

    Text = 'A dropdown',
    Tooltip = 'This is a tooltip', -- Information shown when you hover over the dropdown

    Callback = function(Value)
        print('[cb] Dropdown got changed. New value:', Value)
    end
})
```
Create ColorPicker - 
```lua
LeftGroupBox:AddLabel('Color'):AddColorPicker('ColorPicker', {
    Default = Color3.new(0, 1, 0), -- Bright green
    Title = 'Some color', -- Optional. Allows you to have a custom color picker title (when you open it)
    Transparency = 0, -- Optional. Enables transparency changing for this color picker (leave as nil to disable)

    Callback = function(Value)
        print('[cb] Color changed!', Value)
    end
})
```
Create Keybind - 
```lua
LeftGroupBox:AddLabel('Keybind'):AddKeyPicker('KeyPicker', {
    -- SyncToggleState only works with toggles.
    -- It allows you to make a keybind which has its state synced with its parent toggle

    -- Example: Keybind which you use to toggle flyhack, etc.
    -- Changing the toggle disables the keybind state and toggling the keybind switches the toggle state

    Default = 'MB2', -- String as the name of the keybind (MB1, MB2 for mouse buttons)
    SyncToggleState = false,


    -- You can define custom Modes but I have never had a use for it.
    Mode = 'Toggle', -- Modes: Always, Toggle, Hold

    Text = 'Auto lockpick safes', -- Text to display in the keybind menu
    NoUI = false, -- Set to true if you want to hide from the Keybind menu,

    -- Occurs when the keybind is clicked, Value is `true`/`false`
    Callback = function(Value)
        print('[cb] Keybind clicked!', Value)
    end,

    -- Occurs when the keybind itself is changed, `New` is a KeyCode Enum OR a UserInputType Enum
    ChangedCallback = function(New)
        print('[cb] Keybind changed!', New)
    end
})
```
Create Settings - 
```lua
Library:OnUnload(function()
    print('Unloaded!')
    Library.Unloaded = true
end)

-- UI Settings
local MenuGroup = Tabs['UI Settings']:AddLeftGroupbox('Menu')

-- I set NoUI so it does not show up in the keybinds menu
MenuGroup:AddButton('Unload', function() Library:Unload() end)
MenuGroup:AddLabel('Menu bind'):AddKeyPicker('MenuKeybind', { Default = 'End', NoUI = true, Text = 'Menu keybind' })

Library.ToggleKeybind = Options.MenuKeybind -- Allows you to have a custom keybind for the menu
ThemeManager:SetLibrary(Library)
ThemeManager:SetFolder('MyScriptHub')
ThemeManager:ApplyToTab(Tabs['UI Settings'])
```
