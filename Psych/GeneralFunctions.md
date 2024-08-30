# 角色函数

### characterDance(character:String)
让一个角色跳待机舞蹈。

- `character` - 要使用的角色类型；可以是：`boyfriend`、`dad` 或 `gf`。

### setCharacterX(type:String, value:Float)
将角色组的当前 <ins>x 位置值</ins> 设置为一个新值。 这也会将来自同一类型的所有预缓存角色移动到您想要的位置。

- `type` - 要使用的角色类型；可以是：`boyfriend`、`dad` 或 `gf`。
- `value` - 角色位置的新的 x 值。

### setCharacterY(type:String, value:Float)
将角色组的当前 <ins>y 位置值</ins> 设置为一个新值。 这也会将来自同一类型的所有预缓存角色移动到您想要的位置。

- `type` - 要使用的角色类型；可以是：`boyfriend`、`dad` 或 `gf`。
- `value` - 角色位置的新的 y 值。

### getCharacterX(type:String)
获取角色组的当前 <ins>x 位置值</ins>；返回一个 `float` 数字。

- `type` - 要使用的角色类型；可以是：`boyfriend`、`dad` 或 `gf`。

### getCharacterY(type:String)
获取角色组的当前 <ins>y 位置值</ins>；返回一个 `float` 数字。

- `type` - 要使用的角色类型；可以是：`boyfriend`、`dad` 或 `gf`。

***

# 精准度条函数

### addScore(value:Int = 0)
将 `value` 参数添加到当前的 <ins>歌曲总分</ins> 并重新计算评级；默认值：`0`。

### addMisses(value:Int = 0)
将 `value` 参数添加到当前的 <ins>歌曲失误总数</ins> 并重新计算评级；默认值：`0`。

### addHits(value:Int = 0)
将 `value` 参数添加到当前的 <ins>歌曲击中总数</ins> 并重新计算评级；默认值：`0`。

### addHealth(value:Float = 0)
将 `value` 参数添加到当前的 <ins>歌曲生命值总数</ins>；默认值：`0`。

***

### setScore(value:Int = 0)
使用新值设置当前 <ins>歌曲总分</ins> 的 `value` 参数并重新计算评级；默认值：`0`。

### setMisses(value:Int = 0)
使用新值设置当前 <ins>歌曲失误总数</ins> 的 `value` 参数并重新计算评级；默认值：`0`。

### setHits(value:Int = 0)
使用新值设置当前 <ins>歌曲击中总数</ins> 的 `value` 参数并重新计算评级；默认值：`0`。

### setHealth(value:Int = 0)
使用新值设置当前 <ins>歌曲生命值总数</ins> 的 `value` 参数；默认值：`0`。

***

### setRatingPercent(value:Float)
将当前的 <ins>评级百分比</ins> 设置为一个新值，以防您想进行自己的评级计算。

- `value` - 新的精度评级百分比，范围从 `0` 到 `1`。

### setRatingName(value:String)
将当前的 <ins>评级名称</ins> 设置为一个新值，以防您想进行自己的评级计算。

- `value` - 新的评级字符串名称。

### setRatingFC(value:String)
将当前的 <ins>评级连击名称</ins> 设置为一个新值。

- `value` - 新的评级连击名称。

***

### getScore()
获取当前的 <ins>歌曲总分</ins> 当前值；返回一个 `int` 数字。

### getMisses()
获取当前的 <ins>歌曲失误总数</ins> 当前值；返回一个 `int` 数字。

### getHits()
获取当前的 <ins>歌曲击中总数</ins> 当前值；返回一个 `int` 数字。

### getHealth()
获取当前的 <ins>歌曲生命值总数</ins> 当前值；返回一个 `float` 数字。

***

# 相机函数

### cameraSetTarget(target:String)
使 <ins>相机聚焦</ins> 于目标。

- `target` - 要瞄准的角色类型；可以是：`boyfriend` 或 `dad`。

### cameraShake(camera:String, intensity:Float, duration:Float)
使 <ins>相机抖动</ins>。

- `camera` - 要设置的相机状态；可以是：`camGame`、`camHUD` 或 `camOther`。
- `intensity` - 相机抖动的强度，建议值为 `0.05`。
- `duration` - 相机抖动的持续时间。

### cameraFlash(camera:String, color:String, duration:Float, forced:Bool)
使 <ins>相机闪光</ins>。

- `camera` - 要设置的相机状态；可以是：`camGame`、`camHUD` 或 `camOther`。
- `color` - 闪光的颜色。
- `duration` - 相机闪光的持续时间。
- `forced` - 如果设置为 `true`，如果当前已经有闪光发生，则闪光将重新开始。

### cameraFade(camera:String, color:String, duration:Float, forced:Bool)
使 <ins>相机淡入颜色</ins>。

- `camera` - 要设置的相机状态；可以是：`camGame`、`camHUD` 或 `camOther`。
- `color` - 淡入的颜色。
- `duration` - 相机淡入的持续时间。
- `forced` - 如果设置为 `true`，如果当前已经有淡入发生，则淡入将重新开始。

***

# 对话/过场动画函数

### startDialogue(dialogueFile:String, music:String = null)
启动 <ins>对话内容</ins>，它将加载相对于 `data/your-song-name/` 文件夹的 `json` 文件。 当 <ins>对话结束</ins> 时，将根据您开始对话的位置调用 `startCountdown()` 或 `endSong()` 函数。

如果 <ins>对话行已完成</ins>，则将调用 `onNextDialogue()`。 如果它被 <ins>跳过</ins>，则将调用 `onSkipDialogue()`。

- `dialogueFile` - 对话 `json` 文件的名称。
- `music` - 可选参数，要播放的 `ogg` 音乐文件；必须相对于 `mods/music` 或 `assets/music` 文件夹；默认值：`nil`。

### startVideo(videoFile:String)
启动 <ins>视频</ins>。

- `videoFile` - 视频 `mp4` 文件的名称；必须相对于 `mods/videos` 文件夹。

### startCountdown()
启动 <ins>倒计时</ins>，如果您想手动跳过烦人的对话或视频，请使用它。

***

## 歌曲函数

### loadSong(?name:String = null, ?difficultyNum:Int = -1)
加载一首新歌。

> [!WARNING]
> _如果歌曲的周 `json` 难度名称与当前名称不同，则无法加载歌曲。_

- `name` - 可选参数，要加载的歌曲的名称；默认值：`nil`。（表示它将选择当前的歌曲名称）
- `difficultyNum` - 可选参数，歌曲的难度 ID 号；默认值：`-1`。（表示它将选择歌曲正在播放的当前难度号）

### restartSong(?skipTransition:Bool = false)
重新开始歌曲。

- `skipTransition` - 可选参数，歌曲重新开始时是否会有过渡；默认值：`false`。

### exitSong(?skipTransition:Bool = false)
退出歌曲，可以选择是否使用过渡效果；不要与 `endSong()` 函数混淆。

- `skipTransition` - 可选参数，歌曲退出时是否会有过渡；默认值：`false`。

### endSong()
手动结束歌曲。

***

## 调试函数

### debugPrint(text:Dynamic = '', color:String = 'WHITE')
这将在 <ins>屏幕左上角</ins> 显示一条调试消息。

- `text` - 要显示的文本。
- `color` - 可选参数，用来显示文本的指定颜色。

示例：`debugPrint("Current boyfriend character: ", getProperty('boyfriend.curCharacter')` 这将使用 `getProperty()` 函数获取当前的 bf 角色，并打印 `Current boyfriend character: 'bf'`。

### close()
停止使用此函数的脚本。建议将其放在 <ins>舞台脚本</ins> 上，因为它们通常不再使用；如果脚本需要不断更新或有不断更新的内容，请不要将此函数放在任何地方；例如 `onUpdate()` 或 `onStepHit`。

***

## 颜色函数

### getColorFromHex(color:String)
获取 <ins>特定的十六进制颜色</ins>。这在设置/获取特定的十六进制颜色时非常有用，说实话真的很有用。

- `color` - 指定的十六进制颜色，不用多说了吧。

### getColorFromName(color:String)
<ins>从名称获取颜色</ins>。此函数还有其他可用的名称：`FlxColor()`、`getColorFromString()`。

- `color` - 颜色名称。

### setHealthBarColors(leftHex:String, rightHex:String)
更改 <ins>生命条</ins> 的背景颜色。

- `leftHex` - 生命条的对手十六进制颜色。
- `rightHex` - 生命条的玩家十六进制颜色。

### setTimeBarColors(leftHex:String, rightHex:String)
更改 <ins>时间条</ins> 的背景颜色。

- `leftHex` - 时间条的百分比条十六进制颜色。
- `rightHex` - 时间条的背景颜色十六进制颜色。

### getPixelColor(obj:String, x:Int, y:Int)
<ins>按像素获取对象的十六进制颜色</ins>；返回一个 `number`，当转换为十六进制时，格式为 `FFFFFFFFAARRGGBB`。

- `obj` - 要使用的对象标签名称。
- `x` - 以像素为单位的 x 坐标值。
- `y` - 以像素为单位的 y 坐标值。

***

## 其他函数

### triggerEvent(name:String, arg1:Dynamic, arg2:Dynamic)
触发事件，无需将事件插入图表编辑器。

- `name` - 事件的名称。
- `arg1` - 值 1 上的值。
- `arg2` - 值 2 上的值。

### getModSetting(saveTag:String, ?modName:String = null)
从模组 `data` 文件夹内的设置 `json` 中获取设置值。

- `saveTag` - `json` 中指定的设置名称标签。
- `modName` - 可选参数，给定的模组名称；默认值：`nil`。

### changePresence(details:String, state:Null\<String\>, ?smallImageKey:String, ?hasStartTimestamp:Bool, ?endTimestamp:Float)
更改您的 [Discord RPC](https://raw.githubusercontent.com/Jxyme/simple-discord-rpc/main/screenshots/8zptsNqx.png) 状态。

- `details` - 您在游戏中正在做的事情的详细信息。
- `state` - 对 `details` 的描述。
- `smallImageKey` - 可选参数，要显示在左下角的图像键。
- `hasStartTimestamp` - 可选参数，您的 Discord RPC 是否应该有时间戳。
- `endTimestamp` - 可选参数，要显示多少个小数位。

### getSongPosition()
以毫秒为单位返回当前歌曲位置；`getPropertyFromClass('backend.Conductor', 'songPosition')` 的快捷方式。

已弃用：`getPropertyFromClass('Conductor', 'songPosition')`