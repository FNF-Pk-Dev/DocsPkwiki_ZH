# Lua编码文档:编码基础

## 前言

Lua是一种轻量级、高级别、动态类型、多
范式的脚本语言，创建于1993年，旨在提
高其开发速度、可移植性、可扩展性和易用
性。这就是为什么它被 于Psych Engine;
这使得你可以执行Lua代码，而无需反复编
译游戏，这与在Haxe中执行源代码不同。

## Lua差异

Psych Engine中的编码与普通Lua中的
编码相比有一些“小差异”。这是由于
HaxeFlixel(Psych Engine使用的主引擎)和
Lua的实时跟踪编译器LuaJi造成的。总之
这里列出了一些你应该100%完全了解的小
差异:

1.如果你想让你的代码在游戏过程中对特定的
事件执行，你应该使用回调模板来执行,
例如`onCreate()`、`onUpdate()`、`onEvent()`等
等。但是变量、函数和内置的Lua函数可以
在任何回调模板之外声明。

?> 在Psych Engine的更新<kbd>0.7.1h</kbd>中，你现在可
以将代码放在任何回调模板之外，这是多年
来实现的最好的功能，但这只会执行一次。

2.测试代码显示也有所不同，不再使用`print()`函数，而
是使用`debugPrint()`函数。在`debugPrint()`函
数上传递的参数将显示在屏幕的左上方，并
在几秒钟内逐渐消失。

3.Psych Engine使用LuaJit作为它的Lua编程
语言,它也使用Lua<kbd>5.1</kbd>版本，但缺少一些功
能。但它可能会使用一些扩展，如位运算、
FFI库等。

## 注释功能

注释用于解释代码的上下文及其用途，或者
禁止代码的执行。这不会影响Lua程序内部
的任何内容，因为它将被完全忽略。

要定义注释，注释以双连字符开头，表示单
数注释。你可以将它们放在任何一行代码的
开头或结尾，Lua会像往常一样忽略它们。
对于多行注释，注释也以双连字符开头`--`，开
头和结尾方括号`[]`，代码介于它们之间。

演示:

```lua

-- 创建角色
function onCreate() -- 创建时开始执行
     makeLuaSprite('tag', 'imagePath', 0, 0) -- 定义Lua贴图
     addLuaSprite('tag', true)               -- 添加Lua贴图
end

--[[
function onCreatePost()
end ]]
```

?>还可以嵌套注释，这只适用于多 注释。为
此，在两个方括号的开头和结尾之间，每个
方括号都必须提供指定数量的相等字符`=`。
这在注释掉本身包含更多注释的代码块时非常有用。

例子:
```lua
--[=[
function onCreate()
     --[[ 创建字体
     makeLuaText('textStuff', 'Hi', 0, 100, 100) 定义字体
     setTextSize('textStuff', 20) 字体大小
     setObjectCamera('textStuff', 'camHUD') 字体设置HUD镜头
     addLuaText('textStuff') 添加字体
     ]]
end

function onUpdate(elapsed)
     -- 代码应该放这( 开玩笑的:) )
end
]=]
```

## 变量

变量是存储数据值的抽象可操作容器;它们
可以在整个Lua程序中使用。它们与一个相
关的名称配对，其中包含要使用的变量的数
据值。当您为变量赋新值时，变量中的数据
可以更新。

### 声明与分配

要声明变量，应赋给作用域、标识符和数据
值。作用域决定变量的作用域级别。它可以
是全局作用域(所有变量的默认值)，也可以
是局部作用域(使用`local`关键字定义)。此作
用域将仅限于声明变量的块。标识符是变量
的名称，供以后引用或使用。


现在，您可以通过使用`=`运算符指定
要保存的数据值来赋值变量。如果不存在赋
值，变量将只使用`nil`值作为替代。但您可以
稍后在其他代码行中初始化变量。这只适用
于`局部变量`，不适用于`全局变量`。


我强烈建议使用 `local` 变量而不是 `global` 变量。它有助于避免全局环境中出现不必要的标识符，提高性能，而且通常比 `global` 变量快。为什么它们更快呢？因为 `local` 变量存储在内存堆栈中，而 `global` 变量存储在全局环境中。

示例：
```lua
local object_cost1 = 20
local object_cost2 = 12
local object_price = object_cost1 + object_cost2 -- 添加两个对象值

function onCreate()
     debugPrint(object_price) --> 22
end
```
```lua
local object_cost1 -- 声明一个没有任何赋值的变量
local object_cost2
function onCreate()
     object_cost1 = 34 -- 赋值给一个局部变量
     object_cost2 = 44

     debugPrint(object_cost1) --> 34
     debugPrint(object_cost2) --> 44
end
```

您还可以将变量的 `data` 值重新分配给现有变量。如果要更改当前的 `data` 值，只需将其分配给另一个要保存的 `data` 值即可。

示例：
```lua
local object_cost1 = 100 -- 初始值
function onCreate()
     object_cost1 = 30   -- 重新分配一个新值
     debugPrint(object_cost1) --> 100
end
```
如果出于某种原因想要减少代码行数，您还可以在一行中声明多个变量。为此，每个变量的标识符和数据值应以逗号分隔。每个逗号 <kbd>,</kbd> 字符应该是相等的。

示例：
```lua
local pi, euler     = 3.14, 2.71     -- 多变量声明
function onCreate()
     debugPrint(pi)    --> 3.14
     debugPrint(euler) --> 2.71
end
```
```lua
local lua, haxe, js = 'easy', 'hard' -- 缺少变量赋值
function onCreate()
     debugPrint(lua)  --> easy
     debugPrint(haxe) --> hard
     debugPrint(js)   --> nil
end
```

## 命名约定
命名约定是在命名 `标识符` 时的一组特殊规则，以下是要遵守的规则：
- 标识符可以包含字符的组合，例如数字、字母或下划线字符。
- 标识符的名称开头不能有数字字符。
- 标识符不能包含特殊字符，例如 <kbd>$</kbd>、<kbd>,</kbd>、<kbd>=</kbd> 等。
- 标识符不能以 Lua 关键字命名。
- 标识符区分大小写，因此变量 a 和 A 彼此完全不同。
- 标识符应具有描述性名称，例如 (`health`、`misses`、`alpha`)，以使代码更易于理解。

示例：
```lua
varname   = 'Hi'   -- 一个变量（小写）
varName   = 'Hi'   -- 带有大写字母的变量（驼峰式大小写）
var_name  = 'Hi'   -- 带有下划线 '_' 字符的变量（蛇形大小写）
_var_name = 'Hi'   -- 开头带有下划线 '_' 字符的变量
VARNAME   = 'Hi'   -- 全部是大写字母的变量（大写）
varname2  = 'Hi'   -- 带有数字的变量
_______   = 'Hi'   -- 带有所有下划线的变量（这是真实的）

1varName = 'Error' -- 开头带有数字的变量
var-name = 'Error' -- 带有减号 '-' 字符的变量（烤肉串大小写）
var name = 'Error' -- 带有空格 ' ' 字符的变量
var$name = 'Error' -- 带有特殊 '$' 字符的变量
```

***

### 数据类型

## 字符串
字符串是包含任何字符的字符序列；它们可以是字母、数字、标点符号等。它们的主要用途是存储人类可读的文本，如单词和句子。它们通常用单引号 <kbd>''</kbd>、双引号 <kbd>""</kbd>，甚至是用于多行字符串的双括号 <kbd>[[]]</kbd> 包围。

示例：
```lua
local textString1 = 'Hello' -- 单引号
local textString2 = "World" -- 双引号，这是可选的
function onCreate()
     debugPrint(textString1) --> Hello
     debugPrint(textString2) --> World
end
```

## 转义字符
转义字符是在字符串中使用的特殊字符，它们是对后续字符序列中字符的另一种解释，它基本上允许您在字符串中插入非法字符。例如，一个用单引号字符串包围的单引号字符 <kbd>'</kbd>，这将导致 Lua 程序出错。它们由反斜杠字符 <kbd>\\</kbd> 后跟要使用的指定字符定义；它们列在下

示例：
```lua
function onCreate()
     debugPrint('Don\'t press \'Alt + F4\'') --> Don't press 'Alt + F4'
     debugPrint("dead \"(in a cool way)\"")  --> dead \(in a cool way)"
     debugPrint('C:\\Windows\\System32')     --> C:\Windows\System32
end
```

- <kbd>\'</kbd> - 单引号字符
- <kbd>\"</kbd> - 双引号字符
- <kbd>\\</kbd> - 反斜杠字符
- <kbd>\n</kbd> - 换行符
- <kbd>\r</kbd> - 回车符
- <kbd>\t</kbd> - 水平制表符
- <kbd>\v</kbd> - 垂直制表符

## 数字
数字是表示某事物数量或数量的算术值，它可以是正值或负值。数字可以表示为整数 (Int)，它使用整数，或者浮点数 (Float)，它使用带有小数点的数字。

示例：
```lua
local int   = 47  -- 整数
local float = 2.2 -- 浮点数
function onCreate()
     debugPrint(int)   --> 47
     debugPrint(float) --> 2.2
end
```

## 符号
符号用于以替代方式表示数字。只有两种符号可以替代地表示数字。

| 符号 | 说明 | 示例 |
|-----------|--------------|---------|
| 科学计数法 | 科学计数法允许您使用 e 符号表示极大或极小的数字。<br/> | `34e+4` 或 `34e4`<br/>`43e-3` |
| 十六进制 | 十六进制是一种基于 16 的数字系统。每个数字都以<br/>`0x` 开头，后跟前面的十六进制数字。显然<br/>用于对象的十六进制颜色。 | `0xff0000`<br/>`0xbe20ab` |

## 布尔值
布尔值，通常简称为“布尔值”，是一种数据类型，可以有两个可能的值：`true` 或 `false`。这通常用于条件语句，它允许根据条件是 `true` 还是 `false` 来修改控制流程，从而执行不同的操作。

## Nil
Nil 表示值的空或不存在。如果不再使用变量或表元素，则可以使用它销毁它们。或者使用条件语句来检查该值是否为 `nil`。

## 表
表是 Lua 中唯一的数据结构机制，它由值的集合组成，它存储字符串、数字、布尔值，甚至包括自身在内的各种值，除了 `nil` 值。这些通常用于存储值、创建模块、元表和类，在某些情况下非常有用。它们用花括号字符 <kbd>{}</kbd> 构造，可以表示为数组或字典。

如果您尝试调用一个表，它将返回该表的内存地址；示例：`table: 0x55557885d670`。但在 Psych Engine 中，它返回带有方括号的表元素。如果要从表中读取特定元素，请使用索引访问操作 `[ind]`。

!> 与某些编程语言不同，Lua 对表使用基于 1 的索引。所以基本上不是使用 `[0]` 而是使用 `[1]`。如果您问为什么他们要这样做？因为 Lua 库更喜欢使用从 `1` 开始的索引。

示例：
```lua
function onCreate()
     debugPrint({}) --> []
end
```

## 数组
数组是有序的元素列表，也是最常见的表定义类型。每个元素用逗号 <kbd>,</kbd> 字符分隔，并用一对花括号 <kbd>{}</kbd> 字符包围。

要读取表的数组元素，请添加一个索引访问操作，它是一对方括号 <kbd>[]</kbd> 字符。在给定的索引号内，如果索引不存在或无效，它将返回一个 nil 值。

示例：
```lua
local tableGroup1 = {'string', true, nil} -- 包含字符串、布尔值和 nil 值的表
local tableGroup2 = {{45, 13}, {34, 76}}  -- 包含嵌套表的表
function onCreate()
     debugPrint(tableGroup1)       --> ['string', true, null]
     debugPrint(tableGroup1[1])    --> string
     debugPrint(tableGroup2[1][2]) --> 13
end
```
```lua
local sillyNumbers = {29, 63, 12}
function onCreate()
     sillyNumbers[4] = 83 -- 插入
     sillyNumbers[1] = 30 -- 重新分配
     debugPrint(sillyNumbers) --> [30, 63, 12, 83]
end
```

## 字典
字典使用键值对来存储元素，而不是表数组使用的索引值对。它基本上使用名称或键来引用表字典中的元素。字典中的键可以用一对带有要赋予名称的方括号 <kbd>[]</kbd> 字符包围；示例：`['name']`。无论名称中是否包含特殊字符。

要读取表的字典元素，请添加一个点 <kbd>.</kbd> 字符和给定的键名。或者添加一对带有给定名称的方括号 <kbd>[]</kbd> 字符。实际上，这取决于您在编码时喜欢使用哪种方式；示例：`table.name` 或 `table.['name']`。

示例：
```lua
local stupidData = {FM = 46, PCM = 12, DA = 25}
function onCreate()
     debugPrint('FM: ' ..stupidData.FM..', PCM: '..stupidData.PCM..', DA: ' ..stupidData.DA)
     --> FM: 46, PCM: 12, DA: 25
end
```
```lua
local stupidData = {FM = 46, PCM = 12, DA = 25}
function onCreate()
     stupidData.FM  = 12 -- 插入
     stupidData.LVL = 4  -- 重新分配
     debugPrint(stupidData) --> ["FM" => 46, "PCM" => 12, "DA" => 25, "LVL" => 4]
end
```

***

## 算术
算术运算符是用于对数值执行计算的数学运算符。

| 运算符 | 名称 | 示例 | 返回值 |
|:---------:|----------------------------------------------------------------------------------|:--------|:--------|
|    `+`    | 加法 | `5 + 5` |  `10`   |
|    `-`    | 减法 | `8 - 3` |   `5`   |
|    `*`    | 乘法 | `5 * 3` |  `15`   |
|    `/`    | 除法 | `9 / 2` |  `4.5`  |
|    `%`    | [取模](https://www.calculatorsoup.com/calculators/math/modulo-calculator.php) | `8 % 4` |   `0`   |
|    `^`    | 幂运算 |  `2^4`  |  `16`   |
|    `-`    | 一元负号 |  `-8`   |  `-8`   |

## 关系
关系运算符用于在条件中比较多个操作数，以确定代码块是否执行。

| 运算符 | 描述 | 示例  | 返回值 |
|:---------:|----------------------------------------------------------------------|:---------|:--------|
|   `==`    | 检查条件是否<ins>等于</ins>右侧。 | `a == b` | `false` |
|   `~=`    | 检查条件是否<ins>不等于</ins>右侧。 | `a ~= b` | `true`  |
|    `>`    | 检查条件是否<ins>大于</ins>右侧。 | `4 > 5`  | `false` |
|    `<`    | 检查条件是否<ins>小于</ins>右侧。 | `4 < 5`  | `true`  |
|   `>=`    | 检查条件是否<ins>大于或等于</ins>右侧。 | `7 >= 7` | `true`  |
|   `<=`    | 检查条件是否<ins>小于或等于</ins>右侧。 | `2 <= 5` | `true`  |

## 逻辑
逻辑运算符用于组合多个条件，并指定需要为 `true` 的条件。

| 运算符 | 描述 | 示例 | 返回值 |
|:----------|------------------------------------------------------------------------------------------------|:---------------------------|---------|
| `and`     | 如果两个语句都为 `true`，则返回 `true`；<br> 将多个条件组合在一起。 | `a == false and b == true` | `false` |
| `or`      | 如果其中一个语句为 `true`，则返回 `true`；<br> 将多个条件组合在一起。 | `a == false or b == true`  | `true`  |
| `not`     | 反转条件；如果条件为 `false`<br> 则返回 `true`，反之亦然。 | `not false`                | `true`  |

## 其他
其他运算符仅包含两个运算符：长度运算符和连接运算符。

| 运算符 | 描述 | 示例 |
|:---------:|---------------------------------------------------------------------------|------------------|
| `#`       | 长度运算符，检查 `string` 或 `table` 的最大长度大小。 | `#'sussy'`       |
| `..`      | 连接运算符，将多个 `string` 或 `numbers` 合并在一起。 | `'snow'..'ball'` |

***

# 控制语句
控制语句允许您控制其他语句的执行。它会分析语句的条件，并决定如果条件为 `true` 是否执行代码。

## 条件语句
这是一种控制结构，用于指定是否执行代码块。它们是最常用的控制结构。只有 3 种条件语句：`if`、`else` 和 `elseif` 语句。

### If 语句
If 语句检查条件是否为 `true`。它们使用 `if` 关键字定义，后跟指定条件以使用 `then` 关键字执行语句。

示例：
```lua
local BFScore  = 354
local DADScore = 100
function onCreate()
     if BFScore > DADScore then
          debugPrint('Win!') --> Win!
     end
end
```

### Elseif 语句
Elseif 语句检查其他条件是否失败，并允许按顺序评估多个条件。它们使用 `elseif` 关键字定义，后跟指定条件以执行，以及 `then` 关键字。

示例：
```lua
local BFScore  = 245
local DADScore = 473
function onCreate()
     if BFScore > DADScore then
          debugPrint('Win!')
     else
          debugPrint('Lose!') --> Lose!
     end
end
```

### Else 语句
Else 语句检查所有其他条件是否都失败，如果都失败，则执行此语句。它们使用 `else` 关键字定义，并且应该在 `if` 或 `elseif` 语句的单个或多个条件的底部声明。

示例：
```lua
local BFScore  = 250
local DADScore = 250
function onCreate()
     if BFScore < DADScore then
          debugPrint('Win!')
     elseif BFScore == DADScore then
          debugPrint('Draw!') --> Draw!
     else
          debugPrint('Lose!')
     end
end
```

## 迭代语句
迭代语句允许语句执行零次或多次，直到满足条件或跳出循环。它们通常用于重复代码或迭代表。只有 3 种迭代语句：`for`、`while` 和 `repeat-until` 循环。

### For 循环
For 循环语句允许您循环特定次数。此循环通常用于 `setPropertyFromGroup()` 和 `getPropertyFromGroup()` 函数，用于注释更改、modchart 或其他内容。并用于读取表值或对数值执行操作。`for` 循环有 2 种类型：通用循环和数值循环。

#### 数值
数值循环使用数值来增加或减少值。此循环通常是用于 `setPropertyFromGroup()` 和 `getPropertyFromGroup()` 函数的最常见循环。它们使用 `for` 关键字定义，后跟 3 个表达式：`initializer`、`maximum` 和 `iteration`。最后是 `do` 关键字。

- `initializer` - 数值循环使用的初始变量。
- `maximum` - 数值循环停止时的最大次数。
- `iteration` - 数值循环使用的迭代器，您可以增加或减少该值。此表达式不需要初始化，它将默认为在每次循环后加 `1`。

示例：
```lua
function onCreate()
     for index = 0, 5 do     -- 增量循环
          debugPrint(index)  --> 0, 1, 2, 3, 4, 5
     end
     for index = 5, 0, -1 do -- 减量循环
          debugPrint(index)  --> 5, 4, 3, 2, 1, 0
     end
end
```

#### 通用
通用循环是另一种循环类型，允许您遍历表中的所有值；从 `in` 关键字的迭代器函数返回。这只是迭代每个表元素的另一种循环。此循环的定义与数值循环相同，但只有 2 个表达式：`initializer` 和 `iteration`。

- `initializer` - 通用循环使用的初始变量。变量的数量取决于您使用的迭代器函数，`pairs()`、`ipairs()` 和 `next()` 函数仅使用 `1` 或 `2` 个变量。但是 `string.gmatch()` 函数取决于字符串中的捕获。
- `iteration` - 用于通用循环的迭代器；要在此处使用的迭代器已在此描述的上面列出。如果您愿意，也可以使用自定义迭代器函数，但我们不打算在这里讨论。（甚至不要想）

示例：
```lua
local characters = {bf = 'boyfriend', dad = 'dad', gf = 'girlfriend'}
function onCreate()
     for k,v in pairs(characters) do
          debugPrint({k,v}) --> ["bf" => 'boyfriend'], ["dad" => 'dad'], ["gf" => 'girlfriend']
     end
end
```

### While 循环
While 循环语句将无限循环，直到条件返回 `false`。这很少使用，但如果使用，则仅在您根据条件而不是次数进行迭代时使用，请使用此循环。它使用 `while` 关键字声明，后跟要循环的条件，直到它返回 `false`，最后是 `do` 关键字。

!> 请确保检查 while 循环的条件。因为它可能会无限循环并导致游戏崩溃或软锁！我建议您在将其应用到 Lua 脚本之前，先在 [此处](https://onecompiler.com/lua) 进行测试。

## 循环语句

循环语句允许您多次执行一段代码，直到满足特定的条件。PsychEngine 支持两种类型的循环语句： `while` 循环和 `repeat-until`  循环。

示例:
```lua
local counter   = 5
local factorial = 1

function onCreate()
     while counter > 0 do
          factorial = factorial * counter
          counter   = counter - 1
     end
     debugPrint(factorial) --> 120
end
```

### Repeat-until 循环
`Repeat until` 语句的工作方式与 `while` 循环类似，但有一个主要区别。在 `repeat-until` 循环中，代码块至少会被执行一次，然后才会检查条件是否为 `true`。如果条件不满足，它会重复执行循环，直到条件满足为止。它使用 `repeat` 关键字声明，后面跟着代码块，最后是 `until` 关键字和要循环的条件。

!> 请确保检查 `while` 循环的条件。因为它可能会无限循环并导致游戏崩溃或假死！我建议您在将 Lua 脚本应用到实际项目之前，先在 [这里](https://onecompiler.com/lua) 进行测试。

示例:
```lua
function onCreate()
     repeat -- 我在赚钱
          money = money + 1
     until money >= 10
     debugPrint(money)
end
```

## 跳转语句

跳转语句允许您在满足特定条件时操纵程序的流程。它们用于管理迭代语句和函数的控制流程。跳转语句只有两种：`return` 语句和 `break` 语句。

### Return 语句
`Return` 语句会终止函数的执行并返回一个值或不返回值。如果 `return` 语句没有提供任何要返回的值，它实际上什么也不返回，没有 `nil` 值，就是什么都没有。它们使用 `return` 关键字进行定义，后面可以可选地跟着要返回的值。

示例:
```lua
function stupid()
     return 'bf'
end

function onCreate()
     debugPrint(stupid()) --> bf
end
```

它们还可以返回多个值，每个值之间必须用逗号 <kbd>,</kbd> 分隔；例如：`return 3, 4, 6`。如果您想获取这些值，请将它们转换为一个表，否则如果您不这样做，它只会获取第一个值。如果您不喜欢使用这种方法，您可以使用变量，并根据返回值使用多重赋值。

示例:
```lua
function numbers()
     return 3.14, 420
end

local numbers = {numbers()} -- 转换为一个表
function onCreate()
     debugPrint(numbers) --> 3.14, 420
end
```

```lua
function numbers()
     return 3.14, 420
end

function onCreate()
     pi, drugs      = numbers()     -- pi = 3.14, drugs = 420
     pi             = numbers()     -- pi = 3.14, drugs = nil
     pi, drugs, idk = numbers()     -- pi = 3.14, drugs = 420  (idk 被丢弃)
     pi, drugs, idk = numbers(), 47 -- pi = 3.14, drugs = 420, idk = 47
end
```

### Break 语句
`Break` 语句强制停止任何迭代语句的循环。这主要用于在满足特定条件时强制中断循环。它使用 `break` 关键字进行定义。

示例:
```lua
function onCreate()
     for index = 0, 30 do
          if index > 10 then
               break
          end
          debugPrint(index)
     end
end
```

***

# 函数

函数（也称为子例程或过程）是一系列代码，它们被设计用于执行特定的任务，并且可以在程序中的任何地方被调用。它们可以在您的 Lua 程序中实现代码的重用，从而减少代码的重复。函数可以像字符串、数字等值一样具有属性，并且可以存储在变量中。

函数使用 `function` 关键字进行定义，后面跟着函数的 `标识符`。函数的 `标识符` 遵循与变量命名约定相同的规则。之后是调用操作符 <kbd>()</kbd>，用于声明是否带有参数。函数体包含在调用函数时要执行的代码，最后是 `end` 关键字，用于标记代码块的结束。

由于函数是可以存储在变量中的值，因此这里可以可选地使用 `local` 关键字。这是因为我们在定义函数时使用了一种语法糖。而且始终建议使用局部类型来提高性能等。

!> _请注意，如果您决定在回调函数上声明局部类型，它将无法正常工作。所以请不要这样做；这样做很愚蠢。_

<details><summary><b>语法:</b></summary>
<p>

语法糖语法：
```lua
function name(parameter1, parameter2, parameterX)
     -- 函数代码
end
```

非语法糖语法：
```lua
local name = function(parameter1, parameter2, parameterX)
     -- 函数代码
end
```

</p>
</details>

示例:
```lua
local function hello()
     debugPrint('Hello Function')
end
```

## 调用函数

要调用函数，请使用函数的标识符，并在后面加上调用操作符 `()` 。如果函数需要参数，则将参数放在括号内。如果因为某些原因没有使用调用操作符，则会返回该函数的内存地址。例如：`function: 0x5616d89c0770`。

>  函数会被提升；声明函数后，函数会在代码执行之前被移动到作用域的顶部。这意味着您可以在声明函数的代码行之前调用它。但如果使用 `local` 关键字声明函数，则不能这样做。

示例：

```lua
local function hello()
  debugPrint('Hello Function')
end

function onCreate()
  hello() --> Hello Function
end
```

在大多数情况下，调用函数时都需要使用调用操作符 `()`。但是，有一条特殊规则：如果只传递一个参数，并且该参数是字符串字面量或表构造函数，则调用操作符 `()` 是可选的，只需要一个空格即可。在某些情况下，这样做可以使代码更简洁，或者在调用函数时使用命名参数来提高代码的可读性。

示例：

```lua
function onCreate()
  debugPrint "Wow, so cool"     --> Wow, so cool
  debugPrint {3.14, 3.14, 3.14} --> [3.14, 3.14, 3.14]
end
```

## 参数

参数是一种特殊的变量，位于函数定义的调用操作符 `()` 内。由于它们是函数内部的局部变量，因此它们可以保存任何值，可以使用索引访问操作符来访问表中的值，如下所示，或者使用调用操作符来调用函数。如果有多个参数，则必须使用逗号 `,` 将它们分隔开。它们的主要用途是为函数添加更多功能，以便传递任何参数。

>  “参数”和“实参”这两个词经常互换使用，但它们并不相同。参数是函数定义中的特殊变量，而实参是传递给参数的值。

示例：

```lua
local function setPos(obj, pos)  -- 连接 setProperty x 和 y
  if pos[1] ~= nil then       -- 将 pos 参数视为表
    setProperty(obj..'.x', pos[1])
  end
  if pos[2] ~= nil then
    setProperty(obj..'.y', pos[2]) 
  end
end
    
function onCreatePost()
  setPos('boyfriend', {100, 500}) -- 将位置更改为 x = 100 和 y = 500
end
```

Lua 会像在多重赋值中那样，将参数的数量调整为形参的数量。任何未分配给任何形参的额外实参都将被丢弃。如果某个形参没有接收到任何实参，它将接收到 `nil` 值。


示例：

```lua
local function choose(a, b)
  debugPrint(a or b)
end

function onCreate()
  choose(3)       --> 3 -- a = 3, b = nil
  choose(3, 4)    --> 3 -- a = 3, b = 4
  choose(3, 4, 5) --> 3 -- a = 3, b = 4   (5 被丢弃)
end
```

## 特殊类型

### 可变参数函数

可变参数函数（也称为 vararg 函数）是一种特殊类型的函数，它可以接受任意数量的参数。它在参数列表的末尾使用省略号 `...` 来表示。省略号 `...` 处的参数数量将返回多个结果。因此，建议将其包含在表构造函数 `{}` 中；例如：`{...}`。

示例：

```lua
local function average(...)
  local sum = {...}
  local result = 0
  for i = 1, #sum do
    result = result + sum[i]
  end
  return result / #sum
end

function onCreate()
  debugPrint(average(1, 2, 3))                            --> 2.0
  debugPrint(average(45, 32, 29, 34, 23, 12))             --> 29.166666666667
  debugPrint(average(43, 91, 23, 54, 38, 23, 12, 90, 34)) --> 45.333333333333
end
```

### 匿名函数

匿名函数是一种特殊的函数声明方式。它没有 `标识符`，只包含 `function` 和 `end` 关键字，以及一些可选的参数。它通常用于特定内置函数的回调函数，或者需要函数作为参数的特定参数。

示例：

```lua
function onCreate()
  createTimer('timer', 3.0, function() -- 正在使用的匿名函数
    debugPrint('You're too slow!') --> 3.0
  end)
end

local timers = {}
function createTimer(tag, timer, callback)
  table.insert(timers, {tag, callback})
  runTimer(tag, timer)
end
    
function onTimerCompleted(tag, loops, loopsLeft)
  for _,v in pairs(timers) do
    if v[1] == tag then v[2]() end
  end
end
```

***

# 模块

模块是封装数据（主要是变量和函数）的集合。它使用表来包装内部的函数和变量，充当命名空间。这非常有用，因为它可以通过创建可在所有 Lua 脚本中重用的代码库来避免代码重复。并且有助于组织代码，以维护您的小型代码库。Lua 在其语言中提供了一些内置模块，它们是：`string`、`table` 和 `math`。

创建自己的模块的一种简单方法是使用表，正如我之前提到的。您需要声明一个 `local` 变量来保存一个表，该表充当模块中每个对象的

