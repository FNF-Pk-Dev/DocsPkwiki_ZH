# 图像函数

### makeGraphic(tag:String, width:Int = 256, height:Int = 256, color:String = 'FFFFFF')
初始化<ins>创建一个彩色填充纹理</ins>；必须在 `makeLuaSprite()` 函数之后声明。

- `tag` - 要使用的精灵对象的标签名称。
- `width` - 对象的宽度值，以像素为单位；默认值：`256`。
- `height` - 对象的高度值，以像素为单位；默认值：`256`。
- `color` - 对象的颜色值；默认值：`FFFFFF`。

### loadGraphic(variable:String, image:String, ?gridX:Int = 0, ?gridY:Int = 0)
用新的<ins>精灵纹理</ins>替换现有的精灵纹理。可以选择<ins>设置精灵对象的裁剪大小</ins>。

- `variable` - 要使用的精灵对象的标签名称。
- `image` - 精灵对象要使用的新图像精灵。
- `gridX` - 可选参数，精灵纹理的裁剪宽度；默认值：`0`。
- `gridY` - 可选参数，精灵纹理的裁剪高度；默认值：`0`。

### setBlendMode(obj:String, blend:String = '')
更改对象的<ins>混合模式</ins>。如果您想查看更多混合模式，[请点击这里](https://api.haxe.org/flash/display/BlendMode.html)。_（工作原理类似于 Photoshop）_

- `obj` - 要使用的精灵对象的标签名称。
- `blend` - 要使用的混合模式；例如：`add`、`darken`、`invert` 等；默认值：`''`。

***

# 动画函数

### playAnim(obj:String, name:String, forced:Bool = false, ?reverse:Bool = false, ?startFrame:Int = 0)
播放精灵对象的现有动画；它可以<ins>覆盖动画</ins>。如果 `name` 参数中存在两个或多个相似的名称；<ins>此规则将应用于所有 `name` 参数</ins>。

- `obj` - 要使用的精灵对象的标签名称。
- `name` - 要使用的动画的指定名称。
- `forced` - 如果动画名称与当前播放的动画名称相同，动画是否会重新开始；默认值：`false`。
- `reverse` - 可选参数，动画是否会反向播放；默认值 `false`。
- `startFrame` - 可选参数，动画开始的帧；默认值：`0`。

### addAnimation(obj:String, name:String, frames:Array\<Int\>, framerate:Int = 24, loop:Bool = true)
为精灵对象添加一个<ins>新动画</ins>。

- `obj` - 要使用的精灵对象的标签名称。
- `name` - 要使用的动画的指定名称。
- `frames` - 指示要按什么顺序播放哪些动画帧的索引；例如：`{1, 2, 3}`。
- `framerate` - 动画每秒播放的帧数；默认值：`24`。
- `loop` - 动画是否循环；默认值 `true`。

### addAnimationByPrefix(obj:String, name:String, prefix:String, framerate:Int = 24, loop:Bool = true)
从<ins>xml 文件</ins>中添加一个<ins>新动画</ins>，供精灵对象使用。

- `obj` - 要使用的精灵对象的标签名称。
- `name` - 要使用的动画的指定名称。
- `prefix` - 要播放的 xml 文件中的前缀名称。
- `framerate` - 动画每秒播放的帧数；默认值：`24`。
- `loop` - 动画是否循环；默认值 `true`。

### addAnimationByIndices(obj:String, name:String, prefix:String, indices:String, framerate:Int = 24, loop:Bool = false)
> **注意**：_在 0.7 之前的版本中，如果您想循环播放动画，必须使用 `addAnimationByIndicesLoop`，因为这里不存在第六个参数；<ins>除循环参数外，所有参数都相同</ins>。_

添加一个<ins>新动画</ins>，其中包含要为动画帧播放的指定索引，供精灵对象使用。

- `obj` - 要使用的精灵对象的标签名称。
- `name` - 要使用的动画的指定名称。
- `prefix` - 要播放的 xml 文件中的前缀名称。
- `frames` - 指示要按什么顺序播放哪些动画帧的索引；例如：`1, 2, 3`。
- `framerate` - 动画每秒播放的帧数；默认值：`24`。
- `loop` - 动画是否循环；默认值：`false`。

### addOffset(obj:String, anim:String, x:Float, y:Float)
在每个动画上添加一个新的偏移值。

- `obj` - 要使用的精灵对象的标签名称。
- `anim` - 要使用的动画的指定名称。
- `x` - 动画的新 x 偏移值。
- `y` - 动画的新 y 偏移值。

### loadFrames(variable:String, image:String, spriteType:String = "sparrow")
加载 Lua 精灵的<ins>动画帧</ins>。

- `variable` 要使用的精灵对象的标签名称。
- `image` - 精灵要使用的图像精灵。
- `spriteType` - 可选参数，Lua 精灵的指定精灵类型可以是 `sparrow` 的精灵表或 `tex` 的纹理图集；默认值：`sparrow`。

***

# 预缓存函数

!> _强烈建议您在 `onCreate()` 回调中使用此功能。这些函数主要用于避免在首次使用资源时出现游戏卡顿。_

### addCharacterToList(name:String, type:String)
预缓存<ins>精灵角色</ins>，如果您要切换角色，请使用此函数。

- `name` - 角色的 `json` 名称。
- `type` - 要使用的角色类型；可以是：`boyfriend`、`dad` 或 `gf`。

### precacheImage(name:String, ?allowGPU:Bool = true)
预缓存<ins>图像精灵</ins>；必须相对于 `mods/images`、`assets/images` 或 `assets/shared/images` 文件夹。

- `name` - 精灵要使用的图像精灵。
- `allowGPU` - 可选参数，如果启用了 GPU 缓存，是否允许在 GPU 上缓存；默认值：`true`。

### precacheSound(name:String)
预缓存<ins>声音</ins>；必须相对于 `mods/sounds` 或 `assets/sounds` 文件夹。

- `name` - 要播放的 `ogg` 声音文件。

### precacheMusic(name:String)
预缓存<ins>音乐</ins>；必须相对于 `mods/music` 或 `assets/music` 文件夹。

- `name` - 要播放的 `ogg` 音乐文件。

***

# 对象顺序函数

### setObjectOrder(obj:String, position:Int)
<ins>使用新值</ins>设置对象的当前图层位置。

- `obj` - 要使用的对象的标签名称。
- `position` - 要设置的新图层位置。

### getObjectOrder(obj:String)
获取对象的当前图层位置<ins>当前值</ins>；返回一个 `int` 数字。

- `obj` - 要使用的对象的标签名称。

### objectsOverlap(obj1:String, obj2:String)
检查两个对象是否<ins>相互重叠</ins>；返回一个 `boolean`。

- `obj1` - 要使用的第一个对象的标签名称。
- `obj2` - 要使用的第二个对象的标签名称。

***

# 缩放函数

### setGraphicSize(obj:String, x:Int, y:Int = 0, updateHitbox:Bool = true)
<ins>按像素</ins>设置对象图形大小；不要与 `scaleObject()` 混淆。

- `obj` - 要使用的对象的标签名称。
- `x` - 要设置的对象的宽度值。
- `y` - 要设置的对象的高度值；默认值：`0`。
- `updateHitbox` - 是否更新对象的尺寸或碰撞盒；默认值：`true`。

### scaleObject(obj:String, x:Float, y:Float, updateHitbox:Bool = true)
通过缩放属性设置对象<ins>大小</ins>。

- `obj` - 要使用的对象的标签名称。
- `x` - 要设置的对象的 `scale.x` 值。
- `y` - 要设置的对象的 `scale.y` 值。
- `updateHitbox` - 是否更新对象的尺寸或碰撞盒；默认值：`true`。

### updateHitbox(obj:String)
更新对象的<ins>尺寸或碰撞盒</ins>。如果您要更改对象的缩放比例，请使用此选项。 

- `obj` - 要使用的对象的标签名称。

***

# 中点/位置函数
### getGraphicMidpointX(variable:String)
获取对象的<ins>图形中点的 x 值</ins>；不要与 `getMidpointX()` 函数混淆；返回一个 `float` 数字。

- `variable` - 要使用的对象的标签名称。

### getGraphicMidpointY(variable:String)
获取对象的<ins>图形中点的 y 值</ins>；不要与 `getMidpointY()` 函数混淆；返回一个 `float` 数字。

- `variable` - 要使用的对象的标签名称。

### getMidpointX(variable:String)
获取对象的<ins>中点 x 值</ins>；返回一个 `float` 数字。

- `variable` - 要使用的对象的标签名称。

### getMidpointY(variable:String)
获取对象的<ins>中点 y 值</ins>；返回一个 `float` 数字。

- `variable` - 要使用的对象的标签名称。

***

### getScreenPositionX(variable:String, ?camera:String)
获取对象在特定摄像机上的<ins>屏幕 x 位置</ins>；返回一个 `float` 数字。

- `variable` - 要使用的对象的标签名称。
- `camera` - 可选参数，要检查其位置的摄像机。

### getScreenPositionY(variable:String, ?camera:String)
获取对象在特定摄像机上的<ins>屏幕 y 位置</ins>；返回一个 `float` 数字。

- `variable` - 要使用的对象的标签名称。
- `camera` - 可选参数，要检查其位置的摄像机。

### screenCenter(obj:String, pos:String = 'xy')
将对象居中到 `X` 或 `Y` 位置；也可以同时居中。

- `obj` - 要使用的对象的标签名称。
- `pos` - 要设置的位置；可以是：`X`、`Y`、`XY`；默认值：`XY`。

***

# 其他函数
### setScrollFactor(obj:String, scrollX:Float, scrollY:Float)
更改摄像机移动时对象<ins>滚动的程度</ins>。

- `obj` - 要使用的对象的标签名称。
- `scrollX` - 要设置的滚动的 x 值。
- `scrollY` - 要设置的滚动的 y 值。

### setObjectCamera(obj:String, camera:String = '')
更改对象的<ins>摄像机状态</ins>。

- `obj` - 要使用的对象的标签名称。
- `camera` - 要设置的摄像机状态；可以是：`camGame`、`camHUD` 或 `camOther`；默认值：`''`。