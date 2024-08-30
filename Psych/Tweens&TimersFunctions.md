## 补间动画函数
### startTween(tag:String, vars:String, values:Any = null, duration:Float, options:Any = null)
开始对对象的属性进行补间动画。

!> _此函数在补间动画完成时不会自动调用 `onTweenCompleted()`。您必须手动添加 onComplete 回调函数，示例如下所示；这也允许您在补间动画完成时设置自定义函数名_。

- `tag` - 用于引用补间动画函数的标签名称。
- `vars` - 供补间动画函数引用的对象。
- `values` - 要进行补间动画的对象属性，必须是表字典；例如：`{angle = 360, alpha = 0}`；默认值：`nil`。
- `duration` - 补间动画函数结束的持续时间长度。
- `options` - 用于补间动画的其他选项属性，必须是表字典；例如：`{ease = 'linear', type = 'PINGPONG', onComplete = 'onTweenCompleted'}`；默认值：`nil`。

也可以通过将 `vars` 值设置为 `this` 来对 PlayState 的变量进行补间动画：
```lua
local tag_valParam = {songLength = 215000, defaultCamZoom = 1.2, ['camGame.zoom'] = 1.2}
local tag_optnParam = {ease = 'linear', onComplete = 'onTweenCompleted'}
startTween('tag', 'this', tag_valParam, 1, tag_optnParam)
```

<details><summary><b>选项子参数：</b></summary>
<p>

- `type` - 确定要使用的补间动画类型，可以是以下类型之一：
     - `ONESHOT` - 完成后将停止并从核心容器中移除自身。
     - `PERSIST` - 完成后将停止，但与 `ONESHOT` 不同。它将始终保持附加到核心容器。
     - `LOOPING` - 顾名思义，将在补间动画播放完成后重新启动。
     - `PINGPONG` - 播放“来回”的补间动画。它类似于 `LOOPING`，但每隔一次执行都是反向的。
     - `BACKWARD` - 以相反的方向播放补间动画，很明显。
- `ease` - 要播放的特定 [缓动](https://github.com/ShadowMario/FNF-PsychEngine/blob/experimental/source/psychlua/LuaUtils.hx#L335C1-L371C59) 类型；例如：`linear`、`sineIn`、`bounceOut` 等。
- `startDelay` - 补间动画播放前要等待的秒数。
- `loopDelay` - 补间动画再次循环前要等待的秒数；仅适用于 `LOOPING` 和 `PINGPONG` 类型。
- `onUpdate` - 补间动画处于活动状态的每一帧要执行的函数。
- `onStart` - 补间动画开始播放时要执行的函数。
- `onComplete` - 补间动画播放完成后要执行的函数。

</p>
</details>

## 对象
### doTweenX(tag:String, vars:String, value:Dynamic, duration:Float, ease:String)
对对象的 <ins>x 位置值</ins> 进行补间动画。

- `tag` - 用于引用补间动画函数的标签名称；将在完成后调用 `onTweenCompleted()` 函数。
- `vars` - 供补间动画函数引用的对象或音符名称。
- `value` - 供补间动画函数引用的目标 x 位置值。
- `duration` - 补间动画函数结束的持续时间长度
- `ease` - 要播放的特定 [缓动](https://github.com/ShadowMario/FNF-PsychEngine/blob/experimental/source/psychlua/LuaUtils.hx#L335C1-L371C59) 类型；例如：`linear`、`sineIn`、`bounceOut` 等。

### doTweenY(tag:String, vars:String, value:Dynamic, duration:Float, ease:String)
对对象的 <ins>y 位置值</ins> 进行补间动画。

### doTweenAngle(tag:String, vars:String, value:Dynamic, duration:Float, ease:String)
对对象的 <ins>角度值</ins> 进行补间动画。

### doTweenAlpha(tag:String, vars:String, value:Dynamic, duration:Float, ease:String)
对对象的 <ins>alpha/不透明度值</ins> 进行补间动画。

### doTweenColor(tag:String, vars:String, targetColor:String, duration:Float, ease:String)
对对象的 <ins>十六进制颜色值</ins> 进行补间动画。

- `targetColor` - 供补间动画函数结束的目标颜色值。

### doTweenZoom(tag:String, vars:String, value:Dynamic, duration:Float, ease:String)
对相机的 <ins>缩放值</ins> 进行补间动画。

- `vars` - 要设置的相机状态；可以是：`camGame`、`camHUD` 或 `camOther`。

## 吉他拨片/接收器
### noteTweenX(tag:String, note:Int, value:Dynamic, duration:Float, ease:String)
对吉他拨片的 <ins>x 位置值</ins> 进行补间动画。

- `tag` - 用于引用补间动画函数的标签名称；将在完成后调用 `onTweenCompleted()` 函数。
- `note` - 供补间动画函数使用的吉他拨片的成员 ID；对手：`0,1,2,3`；玩家：`4,5,6,7`。
- `value` - 供补间动画函数引用的目标 x 位置值。
- `duration` - 补间动画函数结束的持续时间长度
- `ease` - 要播放的特定 [缓动](https://github.com/ShadowMario/FNF-PsychEngine/blob/experimental/source/psychlua/LuaUtils.hx#L335C1-L371C59) 类型；例如：`linear`、`sineIn`、`bounceOut` 等。

### noteTweenY(tag:String, note:Int, value:Dynamic, duration:Float, ease:String)
对吉他拨片的 <ins>y 位置值</ins> 进行补间动画。

### noteTweenAngle(tag:String, note:Int, value:Dynamic, duration:Float, ease:String)
对吉他拨片的 <ins>角度值</ins> 进行补间动画。

### noteTweenAlpha(tag:String, note:Int, value:Dynamic, duration:Float, ease:String)
对吉他拨片的 <ins>alpha/不透明度值</ins> 进行补间动画。

### noteTweenDirection(tag:String, note:Int, value:Dynamic, duration:Float, ease:String)
对吉他拨片的 <ins>接收器方向值</ins> 进行补间动画。

***

# 其他补间动画和计时器函数
### runTimer(tag:String, time:Float = 1, loops:Int = 1)
运行计时器；完成后，`tag` 参数中的标签将被调用到 `onTimerCompleted()` 函数。

- `tag` - 要赋予计时器的标签名称。
- `time` - 计时器结束的持续时间长度；默认值：`1`。
- `loops` - 计时器将执行多少次循环；默认值：`1`。_（设置为 0 表示无限循环）_

### cancelTimer(tag)
取消当前正在运行的 <ins>计时器</ins>。

- `tag` - 要取消的计时器标签名称。

### cancelTween(tag)
取消正在运行的 <ins>补间动画</ins>。

- `tag` - 要取消的补间动画标签名称
