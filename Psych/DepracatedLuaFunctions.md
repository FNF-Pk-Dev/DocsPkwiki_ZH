
!> 此处介绍的功能已弃用，这意味着不建议使用它们并且已过时。原因可能是名称或参数发生更改。本维基页面是为了告知人们不要使用这些函数，而应该使用新的函数。_

## 对象函数
### luaSpriteMakeGraphic(tag:String, width:Int, height:Int, color:String)
`makeGraphic()` 已弃用；初始化**创建一个彩色填充纹理**。

- `tag` - 要使用的贴图对象标签名称。
- `width` - 对象的宽度值（以像素为单位）。
- `height` - 对象的高度值（以像素为单位）。
- `color` - 对象的十六进制颜色值。

### luaSpriteAddAnimationByPrefix(tag:String, name:String, prefix:String, framerate:Int = 24, loop:Bool = true)
`addAnimationByPrefix()` 已弃用；添加贴图对象的**指定动画**。

- `tag` - 要使用的贴图对象标签名称。
- `name` - 要播放的动画的名称。
- `prefix` - 要播放的 `xml` 文件中的前缀名称。
- `framerate` - 动画每秒有多少帧；默认值：`24`。
- `loop` - 动画结束后是否循环播放；默认值：`true`。

### luaSpriteAddAnimationByIndices(tag:String, name:String, prefix:String, indices:String, framerate:Int = 24)
`addAnimationByIndices()` 已弃用；添加贴图对象的**指定动画以及每个索引/帧**。

- `tag` - 要使用的贴图对象标签名称。
- `name` - 要播放的动画的名称。
- `prefix` - 要播放的 `xml` 文件中的前缀名称。
- `indices` - 动画的指定索引/帧；例如：`1, 2, 3`。
- `framerate` - 动画每秒有多少帧；默认值：`24`。

### addAnimationByIndicesLoop(tag:String, name:String, prefix:String, indices:String, framerate:Int = 24)
> **注意**：_此函数仅在 `0.6.3` 以上版本中已弃用。_

`addAnimationByIndices()` 已弃用；循环添加贴图对象的**指定动画以及每个索引/帧**。

- `tag` - 要使用的贴图对象标签名称。
- `name` - 要播放的动画的名称。
- `prefix` - 要播放的 `xml` 文件中的前缀名称。
- `indices` - 动画的指定索引/帧；例如：`1, 2, 3`。
- `framerate` - 动画每秒有多少帧；默认值：`24`。

### luaSpritePlayAnimation(tag:String, name:String, forced:Bool = false)
`playAnim()` 已弃用；播放贴图对象的动画。

- `tag` - 要使用的贴图对象标签名称。
- `name` - 要播放的动画的名称。
- `forced` - 如果动画名称与当前播放的动画名称相同，动画是否将重新启动；默认值：`false`。

### objectPlayAnimation(obj:String, name:String, forced:Bool = false, ?startFrame:Int = 0)
`playAnim()` 已弃用；播放贴图对象的动画。

- `obj` - 要使用的贴图对象标签名称。
- `name` - 要播放的动画的名称。
- `forced` - 如果动画名称与当前播放的动画名称相同，动画是否将重新启动；默认值：`false`。
- `reverse` - 可选参数，将从 `最后一帧` 播放到 `第一帧`。
- `startFrame` - 可选参数，动画的指定起始帧。

### characterPlayAnim(character:String, anim:String, ?forced:Bool = false)
`playAnim()` 已弃用；播放贴图对象的动画。

- `obj` - 要使用的贴图对象标签名称。
- `anim` - 要播放的动画的名称。
- `forced` - 可选参数，如果动画名称与当前播放的动画名称相同，动画是否将重新启动；默认值：`false`。

### setLuaSpriteCamera(tag:String, camera:String = '')
`setObjectCamera()` 已弃用；更改对象的**相机状态**。

- `obj` - 要使用的对象标签名称。
- `camera` - 要设置的相机状态；可以是：`camGame`、`camHUD` 或 `camOther`。

### setLuaSpriteScrollFactor(tag:String, scrollX:Float, scrollY:Float)
`setScrollFactor()` 已弃用；更改相机移动时对象滚动的程度。

- `obj` - 要使用的对象标签名称。
- `scrollX` - 要设置的滚动的 x 值。
- `scrollY` - 要设置的滚动的 y 值。

### scaleLuaSprite(tag:String, x:Float, y:Float)
`scaleObject()` 已弃用；**按比例属性**设置对象大小。

- `obj` - 要使用的对象标签名称。
- `x` - 要设置的对象的 `scale.x` 值。
- `y` - 要设置的对象的 `scale.y` 值。

***

# 值设置和获取函数
### setPropertyLuaSprite(tag:String, variable:String, value:Dynamic)
`setProperty()` 已弃用；使用新值设置 **Playstate 内**的当前**属性变量**。

- `tag` - 要使用的 Playstate 或对象内的变量。
- `variable` - 对象的属性；例如：`x`、`y`、`alpha` 等。
- `value` - 要设置的新值。

### getPropertyLuaSprite(tag:String, variable:String)
`getProperty()` 已弃用；获取 **Playstate 内**的当前**属性变量**的当前值。

- `tag` - 要使用的 Playstate 或对象内的变量。
- `variable` - 对象的属性；例如：`x`、`y`、`alpha` 等。

***

# 声音和音乐函数
### musicFadeIn(duration:Float, fromValue:Float = 0, toValue:Float = 1)
`soundFadeIn()` 已弃用；使音乐**淡入**；与 `soundFadeIn()` 不同，不支持 Lua 声音。

- `duration` - 声音淡入的持续时间长度，从 `fromValue` 到 `toValue`。
- `fromValue` - 可选参数，淡入的起始音量；范围从 `0` 到 `1`；默认值：`0`。
- `toValue` - 可选参数，淡入的结束音量；范围从 `0` 到 `1`；默认值：`1`。

### musicFadeOut(duration:Float, toValue:Float = 0)
`soundFadeOut()` 已弃用；使音乐**淡出**；与 `soundFadeOut()` 不同，不支持 Lua 声音。

- `duration` - 声音淡出的持续时间长度，从当前音量到 `toValue`。
- `toValue` - 可选参数，淡出的结束音量；范围从 `0` 到 `1`；默认值：`0`。
