# glua-standart
Within the expansive **Garry's Mod community**, a standardized approach to writing Glua code has yet to be defined. Consequently, code contributions from various authors often ask consistency and aesthetic appeal. In response to this challenge, I have taken the initiative to establish the inaugural standard

I eagerly await your feedback and suggestions for further enhancements :+1:

## 1. Formatting
1. Use 4 spaces for each level of indentation
2. There is no difference between using double quotes `"` and single quotes `'`
3. Spaces are placed around operators and after commas, but not inside parentheses and after function names
```lua
-- Good
x = 10
fruits = {"apple", "banana", "orange", "kiwi", "pineapple"}

-- Bad
x=10
fruits = {"apple","banana","orange","kiwi","pineapple"}
```
4. Avoid extra spaces around parentheses, square brackets, and curly braces
```lua
-- Good
function foo(x)
    return x * 2
end

local tabl = {key = "value"}
local myArray = {1, 2, 3, 4, 5}

-- Bad
function foo( x )
    return x * 2
end

local tabl = { key = "value" }
local myArray = { 1, 2, 3, 4, 5 }
```
5. If an invisible VGUI element is needed, do not create an empty paint function - assign it to `nil`
```lua
-- Good
local pan = vgui.Create("DPanel")
pan.Paint = nil

-- Bad
local pan = vgui.Create("DPanel")
pan.Paint = function() end
```
6. Use `_` for ignored variables.
```lua
for _, item in ipairs(items) do
    foo(item)
end
```
7. Functions and methods have uppercase syntax, object properties are always lowercase
8. Arguments in functions are lowercase
9. Prefer using `Is` when naming boolean functions
```lua
local function IsEven(x)
    return x % 2 == 0
end
```
10. Prefer function syntax over variable syntax
```lua
-- Good
local function eat()
    ...
end

-- Bad
local eat = function()
    ...
end
```
11. Use dot notation to access known properties
```lua
local Person = {
    age = 20
}

-- Good
Person.age

-- Bad
Person["age"]
```
12. `false` and `nil` are falsy in conditional expressions
```lua
-- Good
if name then
    ...
end

-- Bad
if name != nil then
    ...
end
```
13. Put a space after `//` and `--`
14. Avoid aligning variable declarations
```lua
-- Bad
local a               = 1
local long_identifier = 2
```
15. Use the name of the net requests, taking into account the script/addon to which they belong, and what role they perform
```lua
-- Examples
util.AddNetworkString("GangSystem-InvitePlayer")
util.AddNetworkString("HatShop-Buy")
```
16. When sending a net request, the nested syntax of the writing data should be preserved
```lua
net.Start("Test")
    net.WriteString("Hello World")
    net.WriteTable({6, 8, 10, 12})
net.SendToServer()
```
17. When writing a block/blocks of code, use the same style of variable names
18. The name of the hook should indicate the addon/script to which the code and the meaning of the hook belong
```lua
hook.Add("PlayerSay", "AutoDonate.OpenMenu", function(pl, text)
    if text == "/donate" then
        pl:ConCommand("autodonate_menu")
    end
end)
```
19. During the declaration of color and material variables, their affiliation is indicated
```lua
local color_button = Color(75, 75, 75)
local mat_medal = Material("icon16/rosette.png")
```
19. If there is an iteration in the code block, cache the variables
```lua
local color_text = Color(25, 25, 25)

hook.Add("HUDPaint", "CustomHUD.Test", function()
    draw.SimpleText("Hello there", "TargetID", 25, 25, color_text)
end)
```
```lua
-- Somewhere during the creation of the interface

local pl_nick = LocalPlayer():Name()

pnl.Paint = function(_, w, h)
    draw.RoundedBox(6, 0, 0, w, h, color_black)
    draw.SimpleText(pl_nick, "Trebuchet24", w * 0.5, h * 0.5, color_white, TEXT_ALIGN_CENTER, TEXT_ALIGN_CENTER)
end
```

## 2. File Structure
1. GLua files should be named in lowercase
2. Dedicate a separate folder for your addon within the `lua/` directory. Refer to it through a `*_autorun.lua` file in `lua/autorun/`
