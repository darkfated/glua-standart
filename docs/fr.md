# GLua Standart

## 1. Formatage

1. Utilisez 4 espaces pour chaque niveau d'indentation.
2. Il n'y a pas de différence entre l'utilisation de guillemets doubles `"` et de guillemets simples `'`.
3. Des espaces sont placés autour des opérateurs et après les virgules, mais pas à l'intérieur des parenthèses et après les noms de fonctions.

```lua
-- Correct
x = 10
fruits = {"pomme", "banane", "orange", "kiwi", "ananas"}

-- Incorrect
x=10
fruits = {"pomme","banane","orange","kiwi","ananas"}
```

4. Évitez les espaces supplémentaires autour des parenthèses, des crochets et des accolades.

```lua
-- Correct
function foo(x)
    return x * 2
end

local tabl = {key = "valeur"}
local myArray = {1, 2, 3, 4, 5}

-- Incorrect
function foo( x )
    return x * 2
end

local tabl = { key = "valeur" }
local myArray = { 1, 2, 3, 4, 5 }
```

5. Si un élément VGUI invisible est nécessaire, ne créez pas de fonction de peinture vide - assignez-la à `nil`.

```lua
-- Correct
local pan = vgui.Create("DPanel")
pan.Paint = nil

-- Incorrect
local pan = vgui.Create("DPanel")
pan.Paint = function() end
```

6. Utilisez `_` pour les variables ignorées.

```lua
for _, item in ipairs(items) do
    foo(item)
end
```

7. Les fonctions et les méthodes ont une syntaxe en majuscules, les propriétés des objets sont toujours en minuscules.
8. Les arguments des fonctions sont en minuscules.
9. Préférez utiliser `Is` lors de la nomination des fonctions booléennes.

```lua
local function IsEven(x)
    return x % 2 == 0
end
```

10. Préférez la syntaxe de fonction à la syntaxe de variable.

```lua
-- Correct
local function eat()
    ...
end

-- Incorrect
local eat = function()
    ...
end
```

11. Utilisez la notation par points pour accéder aux propriétés connues.

```lua
local Person = {
    age = 20
}

-- Correct
Person.age

-- Incorrect
Person["age"]
```

12. `false` et `nil` sont des valeurs fausses dans les expressions conditionnelles.

```lua
-- Correct
if name then
    ...
end

-- Incorrect
if name != nil then
    ...
end
```

13. Mettez un espace après `//` et `--`.
14. Évitez d'aligner les déclarations de variables.

```lua
-- Incorrect
local a               = 1
local long_identifier = 2
```

15. Utilisez les noms des requêtes réseau, en tenant compte du script/de l'addon auquel elles appartiennent, et de leur rôle.

```lua
-- Exemples
util.AddNetworkString("GangSystem-InvitePlayer")
util.AddNetworkString("HatShop-Buy")
```

16. Lors de l'envoi d'une requête réseau, la syntaxe imbriquée de l'écriture des données doit être préservée.

```lua
net.Start("Test")
    net.WriteString("Hello World")
    net.WriteTable({6, 8, 10, 12})
net.SendToServer()
```

17. Lors de l'écriture d'un bloc/de blocs de code, utilisez le même style de noms de variables.
18. Le nom du hook doit indiquer l'addon/le script auquel le code appartient et la signification du hook.

```lua
hook.Add("PlayerSay", "AutoDonate.OpenMenu", function(pl, text)
    if text == "/donate" then
        pl:ConCommand("autodonate_menu")
    end
end)
```

19. Lors de la déclaration de variables de couleur et de matériau, indiquez leur appartenance.

```lua
local color_button = Color(75, 75, 75)
local mat_medal = Material("icon16/rosette.png")
```

20. S'il y a une itération dans le bloc de code, mettez en cache les variables.

```lua
local color_text = Color(25, 25, 25)

hook.Add("HUDPaint", "CustomHUD.Test", function()
    draw.SimpleText("Bonjour", "TargetID", 25, 25, color_text)
end)
```

```lua
-- Quelque part lors de la création de l'interface

local pl_nick = LocalPlayer():Name()

pnl.Paint = function(_, w, h)
    draw.RoundedBox(6, 0, 0, w, h, color_black)
    draw.SimpleText(pl_nick, "Trebuchet24", w * 0.5, h * 0.5, color_white, 1, 1)
end
```

## 2. Structure des fichiers

1. Les fichiers GLua doivent être nommés en minuscules.
2. Consacrez un dossier séparé pour votre addon dans le répertoire `lua/`. Référez-vous à lui via un fichier `*_autorun.lua` dans `lua/autorun/`.
