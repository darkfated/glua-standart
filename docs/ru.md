# Стандарт GLua

## 1. Форматирование

1. Используйте 4 пробела для каждого уровня отступа.
2. Нет разницы между использованием двойных кавычек `"` и одинарных кавычек `'`.
3. Пробелы ставятся вокруг операторов и после запятых, но не внутри скобок и после имён функций.

```lua
-- Правильно
x = 10
fruits = {"apple", "banana", "orange", "kiwi", "pineapple"}

-- Неправильно
x=10
fruits = {"apple","banana","orange","kiwi","pineapple"}
```

4. Избегайте лишних пробелов вокруг круглых, квадратных и фигурных скобок.

```lua
-- Правильно
function foo(x)
    return x * 2
end

local tabl = {key = "value"}
local myArray = {1, 2, 3, 4, 5}

-- Неправильно
function foo( x )
    return x * 2
end

local tabl = { key = "value" }
local myArray = { 1, 2, 3, 4, 5 }
```

5. Если нужен невидимый элемент VGUI, не создавайте пустую функцию рисования — присвойте её `nil`.

```lua
-- Правильно
local pan = vgui.Create("DPanel")
pan.Paint = nil

-- Неправильно
local pan = vgui.Create("DPanel")
pan.Paint = function() end
```

6. Используйте `_` для игнорируемых переменных.

```lua
for _, item in ipairs(items) do
    foo(item)
end
```

7. Функции и методы пишутся с заглавной буквы, свойства объектов всегда с маленькой буквы.
8. Аргументы в функциях пишутся с маленькой буквы.
9. Предпочитайте использовать `Is` при именовании булевых функций.

```lua
local function IsEven(x)
    return x % 2 == 0
end
```

10. Предпочитайте синтаксис функции вместо синтаксиса переменной.

```lua
-- Правильно
local function eat()
    ...
end

-- Неправильно
local eat = function()
    ...
end
```

11. Используйте точечную нотацию для доступа к известным свойствам.

```lua
local Person = {
    age = 20
}

-- Правильно
Person.age

-- Неправильно
Person["age"]
```

12. `false` и `nil` являются ложными значениями в условных выражениях.

```lua
-- Правильно
if name then
    ...
end

-- Неправильно
if name != nil then
    ...
end
```

13. Ставьте пробел после `//` и `--`.
14. Избегайте выравнивания объявлений переменных.

```lua
-- Неправильно
local a               = 1
local long_identifier = 2
```

15. Используйте имена сетевых запросов, учитывая скрипт/аддон, к которому они принадлежат, и их роль.

```lua
-- Примеры
util.AddNetworkString("GangSystem-InvitePlayer")
util.AddNetworkString("HatShop-Buy")
```

16. При отправке сетевого запроса вложенный синтаксис записи данных должен сохраняться.

```lua
net.Start("Test")
    net.WriteString("Hello World")
    net.WriteTable({6, 8, 10, 12})
net.SendToServer()
```

17. При написании блока/блоков кода используйте один и тот же стиль имен переменных.
18. Имя хука должно указывать на аддон/скрипт, к которому принадлежит код, и на значение хука.

```lua
hook.Add("PlayerSay", "AutoDonate.OpenMenu", function(pl, text)
    if text == "/donate" then
        pl:ConCommand("autodonate_menu")
    end
end)
```

19. При объявлении переменных цвета и материала указывайте их принадлежность.

```lua
local color_button = Color(75, 75, 75)
local mat_medal = Material("icon16/rosette.png")
```

20. Если в кодовом блоке есть итерация, кэшируйте переменные.

```lua
local color_text = Color(25, 25, 25)

hook.Add("HUDPaint", "CustomHUD.Test", function()
    draw.SimpleText("Hello there", "TargetID", 25, 25, color_text)
end)
```

```lua
-- Где-то во время создания интерфейса

local pl_nick = LocalPlayer():Name()

pnl.Paint = function(_, w, h)
    draw.RoundedBox(6, 0, 0, w, h, color_black)
    draw.SimpleText(pl_nick, "Trebuchet24", w * 0.5, h * 0.5, color_white, 1, 1)
end
```

## 2. Структура файлов

1. Файлы GLua должны именоваться строчными буквами.
2. Посвятите отдельную папку для вашего аддона в каталоге `lua/`. Ссылайтесь на неё через файл `*_autorun.lua` в `lua/autorun/`.
