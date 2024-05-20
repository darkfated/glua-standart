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
local myArray = [ 1, 2, 3, 4, 5 ]
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
9. Prefer using Is when naming boolean functions
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

## 2. File Structure
1. GLua files should be named in lowercase
2. Dedicate a separate folder for your addon within the `lua/` directory. Refer to it through a `*_autorun.lua` file in `lua/autorun/`
