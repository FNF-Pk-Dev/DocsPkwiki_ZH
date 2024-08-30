## 关于标签的重要提示

> _对于 `tag` 参数，如果您再次使用相同的标签名称，则具有相同标签**和**相同对象类型（例如，贴图、字体、计时器等）的先前对象将被 **删除**；此规则适用于所有 `tag` 参数。_

# 创建/添加/移除贴图

### makeLuaSprite(tag:String, ?image:String = null, ?x:Float = 0, ?y:Float = 0)
初始化**创建 Lua 贴图对象**。这不会立即将贴图添加到游戏中，只有通过 `addLuaSprite()` 函数才能实现。

- `tag` -  贴图的标签名称，供以后引用。
- `image` - 可选参数，要显示的图像。贴图图像必须相对于 `mods/images`、`assets/shared/images` 或 `assets/images` 文件夹。
- `x` -  可选参数，要设置的贴图对象的 x 坐标值。
- `y` -  可选参数，要设置的贴图对象的 y 坐标值。

### makeAnimatedLuaSprite(tag:String, ?image:String = null, ?x:Float = 0, ?y:Float = 0, ?spriteType:String = "sparrow")
初始化**创建动画 Lua 贴图对象**。这不会立即将贴图添加到游戏中，只有通过 `addLuaSprite()` 函数才能实现。

- `tag` - 动画贴图的标签名称，供以后引用。
- `image` - 可选参数，要显示的图像。贴图图像必须相对于 `mods/images`、`assets/shared/images` 或 `assets/images` 文件夹。
- `x` - 可选参数，要设置的贴图对象的 x 坐标值。
- `y` - 可选参数，要设置的贴图对象的 y 坐标值。
- `spriteType` - 可选参数，Lua 贴图的指定贴图类型可以是用于 `sparrow` 的贴图表或用于 `tex` 的纹理图集；默认值：`sparrow`。

### addLuaSprite(tag:String, front:Bool = false)
**将 Lua 贴图对象添加**到游戏中。如果彼此重叠放置，此函数将**覆盖其他贴图对象**。

- `tag` - 要添加到游戏中的贴图的标签名称。
- `front` - 贴图对象是否添加到角色的顶部；对于 camHUD 对象，将其设置为 `true` 会将其放置在 HUD 元素之上；默认值：`false`。

### removeLuaSprite(tag:String, destroy:Bool = true)
从游戏中**移除 Lua 贴图对象**。为了性能起见，如果**不再使用贴图对象**，建议使用此函数。

- `tag` - 要从游戏中移除的贴图的标签名称。
- `destroy` - 如果设置为 `true`，将从游戏中永久移除贴图。如果不重新制作贴图，则无法重新添加它；默认值：`true`。

***

# 创建/添加/移除字体

### makeLuaText(tag:String, text:String, width:Int, x:Float, y:Float)
初始化**创建字体对象**。这不会立即将字体添加到游戏中，只有通过 `addLuaText()` 函数才能实现。

- `tag` - 字体的标签名称，供以后引用。
- `text` - 要在游戏中显示的字体内容。
- `width` - 要设置的字体框宽度；将其设置为 `0` 将自动为您确定宽度。
- `x` -  要设置的字体对象的 x 坐标值。
- `y` -  要设置的字体对象的 y 坐标值。

### addLuaText(tag:String)
**将字体对象添加**到游戏中。如果彼此重叠放置，此函数将**覆盖其他字体对象**。

- `tag` - 要添加到游戏中的字体的标签名称。

### removeLuaText(tag:String, destroy:Bool = true)
从游戏中**删除字体对象**。为了性能起见，如果**不再使用字体对象**，建议使用此函数。

- `tag` - 要从游戏中移除的字体的标签名称。
- `destroy` - 如果设置为 `true`，将从游戏中永久移除字体。如果不重新制作字体，则无法重新添加它；默认值：`true`。

***

# 字体属性设置器

### setTextString(tag:String, text:String)
使用新内容设置字体对象的**当前字体内容**。

- `tag` -  要使用的字体的标签名称。
- `text` -  要设置的新字体内容。

### setTextSize(tag:String, size:Int)
使用新大小设置字体对象的**当前字体大小**。

- `tag` -  要使用的字体的标签名称。
- `size` -  要设置的新字体大小。

### setTextAutoSize(tag:String, value:Bool)
设置字体对象的 `autoSize` 值，该值将确定**是否应自动确定宽度和高度**。

- `tag` -  要使用的字体的标签名称。
- `value` -  是否应自动确定宽度和高度。

### setTextWidth(tag:String, width:Float)
使用新宽度设置字体对象的**当前字体框宽度**。

- `tag` -  要使用的字体的标签名称。
- `width` -  要设置的新字体框宽度。

### setTextHeight(tag:String, height:Float)
使用新高度设置字体对象的**当前字体框高度**。

- `tag` -  要使用的字体的标签名称。
- `height` -  要设置的新字体框高度。

### setTextBorder(tag:String, size:Float, color:String, ?style:String = 'outline')
使用新的值设置字体对象的**当前字体边框大小、颜色和样式**。

- `tag` -  要使用的字体的标签名称。
- `size` -  要设置的新字体边框大小。
- `color` -  要设置的新字体边框颜色。
- `style` -  可选参数，要设置的新字体边框样式；默认值：`outline`。

### setTextColor(tag:String, color:String)
使用新颜色设置字体对象的**当前字体颜色**。

- `tag` -  要使用的字体的标签名称。
- `color` -  要设置的新字体颜色。

### setTextAlignment(tag:String, alignment:String = 'left')
使用新对齐方式设置字体对象的**当前字体对齐方式**。

- `tag` -  要使用的字体的标签名称。
- `alignment` -  要设置的新字体对齐方式；可以是 `left`、`right`、`center`；默认值：`left`。

### setTextFont(tag:String, newFont:String)
使用新字体设置字体对象的**当前字体字体**。

- `tag` -  要使用的字体的标签名称。
- `newFont` -  要设置的新字体字体。字体字体必须相对于 `mods/fonts` 文件夹。

### setTextItalic(tag:String, italic:Bool)
将字体对象设置为**斜体**。

- `tag` -  要使用的字体的标签名称。
- `italic` -  字体是否将被设为斜体。

***

# 字体属性获取器

### getTextString(tag:String)
获取字体的当前字体内容。

- `tag` -  字体对象的当前字体内容的标签名称。

### getTextSize(tag:String)
获取字体的当前字体大小。

- `tag` -  字体对象的当前字体大小的标签名称。

### getTextWidth(tag:String)
获取字体的当前字体框宽度。

- `tag` -  字体对象的当前字体框大小的标签名称。

### getTextFont(tag:String, font:String)
获取字体的当前字体字体。

- `tag` -  字体对象的当前字体字体的标签名称。 
