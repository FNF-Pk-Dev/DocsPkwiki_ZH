## Haxe 函数

### addHaxeLibrary(libName:String, ?libPackage:String = '')

将 Haxe 库导入解释器。基本上相当于 Haxe 中的 `import` 语句，用于将特定包（如精灵、文本、补间动画等）导入 Haxe。

- `libName` - 要引用的库名。
- `libPackage` - 可选参数，要使用的库包；默认值：`''`。

示例：

- 导入声音库： `addHaxeLibrary('FlxSound', 'flixel.sound')`
- 导入着色器滤镜： `addHaxeLibrary('ShaderFilter', 'openfl.filters')`
- 导入 CoolUtil： `addHaxeLibrary('CoolUtil', 'backend')`

<details><summary><b>导入 Haxe（参考）：</b></summary>
<p>

```haxe
package; // 它们是包含模块的目录，我不知道它是如何工作的，但使用它非常重要。

// import library_package.library_name | <-- 这是语法
import flixel.sound.FlxSound;       // 导入声音包
import openfl.filters.ShaderFilter; // 导入着色器滤镜包
import backend.CoolUtil;            // 导入 CoolUtil haxe 文件

// 另外，分号 ';' 字符在声明函数、包、变量等时非常重要。
```

</p>
</details>

<details><summary><b>预导入的库：</b></summary>
<p>

```haxe
import flixel.FlxG;
import flixel.math.FlxMath;
import flixel.FlxSprite;
import flixel.FlxCamera;
import backend.PsychCamera;
import flixel.util.FlxTimer;
import flixel.tweens.FlxTween;
import flixel.tweens.FlxEase;
import psychlua.HScript.CustomFlxColor; // 不是实际的 FlxColor，因为它是一个抽象类（HScript 不能使用抽象类），这意味着 FlxColor 中的一些函数和变量将丢失。
import backend.BaseStage.Countdown;
import states.PlayState;
import backend.Paths;
import backend.Conductor;
import backend.ClientPrefs;
import backend.Achievements;
import objects.Character;
import objects.Alphabet;
import objects.Note;
import psychlua.CustomSubstate;
import flixel.addons.display.FlxRuntimeShader;
import openfl.filters.ShaderFilter;
import StringTools;
import flxanimate.FlxAnimate;
```

</p>
</details>

### runHaxeCode(codeToRun:String, ?varsToBring:Any = null, ?funcToRun:String = null, ?funcArgs:Array\<Dynamic\> = null)

<ins>运行你的 Haxe 代码</ins>，用于你的 HScript 等。

- `codeToRun` - 要运行的 Haxe 代码，使用双括号 `[[]]` 表示多行字符串。
- `varsToBring` - 可选参数，要导入用于字符串插值的 Haxe 变量；必须是表字典；默认值：`nil`。
- `funcToRun` - 可选参数，要运行的 runHaxeCode 内部的 Haxe 函数名；必须是字符串；默认值：`nil`。
- `funcArgs` - 可选参数，要传递给 runHaxeCode 内部 Haxe 函数的参数；必须是包含所有值的表；默认值：`nil`。

示例：

```lua
function onCreate()
     -- varsToBring 示例
     runHaxeCode([[
          debugPrint(text, color); // 将打印 > 'hi'
     ]], {text = 'hi', color = 0xFF0000})

     -- funcToRun 和 funcArgs 示例
     runHaxeCode([[
          function isEven(num:Int) {
               debugPrint(num % 2 == 0);
          }
     ]], nil, 'isEven', {4})
end
```

### runHaxeFunction(funcToRun:String, ?funcArgs:Array\<Dynamic\> = null)

<ins>执行</ins> `runHaxeCode()` 函数中的 <ins>Haxe 函数</ins>。

- `funcToRun` - 要引用的 Haxe 函数名。
- `funcArgs` - 可选参数，要传递给 Haxe 函数的参数；默认值：`nil`。

示例：

```lua
function onCreate()
     runHaxeCode([[
          function isBool(bool:String) { return bool == 'true' ? true : false; }
     ]])
     
     local proof = runHaxeFunction('isBool', {'true'})
     debugPrint(type(proof)) -- 将打印 > 'boolean'
end
```

***

## Haxe 全局变量函数

### setVar(name:String, value:Dynamic)

如果 <ins>PlayState 的变量映射</ins> 中尚不存在该变量，则创建该变量并将其设置到其中，这基本上相当于 <ins>创建一个新的全局变量</ins>；否则将使用新值设置该变量。 只有在 <ins>包含该函数的 Haxe 脚本当前正在执行</ins> 时，此操作才会生效；`getVar()` 函数也是如此。

- `varName` - 要引用的变量。
- `value` - 要使用或覆盖的变量的指定类型的值。

HScript 示例（脚本 1）：

```haxe
function onCreate() {
     setVar('globalVar', 'Hello Haxe!');
     setVar('globalYes', [34, 123, 4.20]);
}
```

HScript 示例（脚本 2）：

```haxe
function onCreate() {
     debugPrint(getVar('globalVar'), 0xFFF88700);    // 将打印 > 'Hello Haxe!'
     debugPrint(getVar('globalYes')[2], 0xFFF88700); // 将打印 > 4.20
}
```

将全局 Haxe 变量调用到 Lua 中：

```lua
function onCreate()
     debugPrint(getProperty('globalYes')[1]) -- 将打印 > 34
     debugPrint(getProperty('globalYes')[2]) -- 将打印 > 123
end
```

### getVar(name:String)

从 PlayState 的变量映射中获取变量的当前值。

- `varName` - 要检索其值的变量的名称。

### removeVar(name:String)

永久删除不再使用的全局变量。

- `varName` -  要引用的变量名。

***

## Haxe 内置脚本函数

### debugPrint(text:String, ?color:FlxColor = null)

这将在屏幕的 <ins>左上角</ins> 显示一条调试信息。

- `text` -  要输出到屏幕左上角的文本。
- `color` - 可选参数，要显示的文本颜色。

### addBehindBF(obj:FlxBasic)

将对象添加到 Boyfriend 的后面；相同功能的函数还有： `addBehindGF`、`addBehindDad`。

- `obj` - 要添加的对象。

### getLuaObject(tag:String)

获取 `runHaxeCode()` 函数外部的指定标签对象。

- `tag` -  要引用的对象标签名称。

示例：
```lua
function onCreate()
     makeLuaSprite('graphicThingy', nil, 0, 0)
     makeGraphic('graphicThingy', 1000, 1000, 'ff00ff')
     addLuaSprite('graphicThingy', true)

     runHaxeCode([[
          var theLuaTag = game.getLuaObject('graphicThingy'); // 获取 lua 标签
          theLuaTag.cameras = [game.camHUD]; // 将其设置为 'camHUD'
          theLuaTag.alpha   = 0.5;           // 将不透明度设置为 '0.5'
          theLuaTag.angle   = 180;           // 将角度设置为 '180'
     ]])
end
```

### createCallback(name:String, func:Dynamic, ?funk:FunkinLua = null)

在 lua 脚本中创建一个本地函数。

!> 由于某些 parentLua 语句问题，第三个参数已损坏_。

- `name` - 函数的给定名称。
- `func` -  要使用的函数代码。
- `funk` - 可选参数，要在其上创建函数的脚本；默认值： `nil`。（如果在 runHaxeCode 中使用，将选择使用 `runHaxeCode()` 函数的脚本）

示例：
```lua
function onCreate()
     runHaxeCode([[
          createCallback('print', function(text:String) {
               debugPrint(text);
          });
     ]])
end

function onCreatePost()
    print('Hello') -- 将打印 "Hello"
end
```

### createGlobalCallback(name:String, func:Dynamic)

在 <ins>所有 lua 脚本</ins> 中创建一个全局函数。

- `name` - 全局函数的给定名称。
- `func` - 要使用的函数代码。

示例：

脚本 1 (Haxe)：
```haxe
function onCreate() {
    createGlobalCallback('print', function(text:String) {
        debugPrint(text);
    });
}
```

脚本 2 (Lua)：
```lua
function onCreatePost()
    print('Hello') -- 将打印 "Hello"
end
```
