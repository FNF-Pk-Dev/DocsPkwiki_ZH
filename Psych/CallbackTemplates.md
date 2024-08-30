## 开始/结束回调

### onCreate()

<ins>每次脚本启动时</ins>触发，可用于创建对象、预缓存、属性设置器/获取器；<ins>有些变量</ins> 尚未创建，具体取决于启动时间。

### onCreatePost()

在脚本<ins>启动后</ins>触发。<ins>HUD 元素和角色</ins>在此处创建；只会触发一次。

### onDestroy()

<ins>脚本关闭时</ins>触发。

***

## 游戏回调

### onStepHit()

默认情况下，每小节触发<ins>16 次</ins>。我建议在此处使用 `curStep` 变量，因为它将在每次拍子时被调用。

### onBeatHit()

默认情况下，每小节触发<ins>4 次</ins>。我建议在此处使用 `curBeat` 变量，因为它将在每次拍子时被调用。

### onSectionHit()

每小节最多触发<ins>1 次</ins>。我建议在此处使用 `curSection` 变量，因为它将在每次拍子时被调用。

### onRecalculateRating()

在计算评分<ins>之前</ins>触发。建议使用 `setRatingPercent()` 函数设置计算时的准确度百分比，使用 `setRatingName()` 函数设置史诗级评分名称。

> 此回调可以使用 `Function_Stop`；如果要重新计算评分，则**不得**返回 `Function_Stop`。

### onMoveCamera(focus)

当<ins>镜头聚焦于某个角色</ins>时触发；可以是“boyfriend”、“dad”或“gf”。

- `focus` - 要检查的角色。

示例：

```lua
function onMoveCamera(focus)
	if focus == 'boyfriend' then
		-- 当该小节启用了“必须击中”小节时调用；即当镜头聚焦于男朋友时。
	elseif focus == 'dad' then
		-- 当该小节未启用“必须击中”小节时调用；即当镜头聚焦于爸爸时。
	elseif focus == 'gf' then
		-- 当该小节启用了“女朋友”小节时调用；即当镜头聚焦于女朋友时。
	end
end
```

## 更新

### onUpdate(elapsed)

在游戏的<ins>每一帧之前</ins>触发。

- `elapsed` - 以毫秒为单位显示的每一帧；`getPropertyFromClass('flixel.FlxG', 'elapsed')` 的快捷方式。

### onUpdatePost(elapsed)

在游戏的<ins>每一帧</ins>触发。HUD 元素在此处更新。

- `elapsed` - 以毫秒为单位显示的每一帧；`getPropertyFromClass('flixel.FlxG', 'elapsed')` 的快捷方式。

### onUpdateScore(miss)

`scoreTxt` 文本更新<ins>之后</ins>触发。

- `miss` - 检查玩家是否漏掉了一个箭头；返回一个 `boolean` 值。

### preUpdateScore(miss)

`scoreTxt` 文本更新<ins>之前</ins>触发。

> 此回调可以使用 `Function_Stop`；如果要更新 `scoreTxt` 变量并调用 `onUpdateScore()`，则**不得**返回 `Function_Stop`。

- `miss` - 检查玩家是否漏掉了一个箭头；返回一个 `boolean` 值。

## 歌曲

### onSongStart()

在<ins>歌曲开始</ins>或<ins>倒计时结束</ins>时触发。

### onEndSong()

在<ins>歌曲结束</ins>时触发，如果<ins>解锁了成就</ins>，则会延迟；不要与 `onDestroy()` 混淆。

> 此回调可以使用 `Function_Stop`；如果要结束歌曲，则**不得**返回 `Function_Stop`。

***

# 倒计时回调

### onStartCountdown()

在<ins>倒计时开始</ins>时触发；不要与 `onCountdownStarted()` 混淆。

> 此回调可以使用 `Function_Stop`；如果要开始倒计时并调用 `onCountdownStarted()`，则**不得**返回 `Function_Stop`。

### onCountdownStarted()

在<ins>倒计时开始后</ins>触发；<ins>箭头弹奏</ins>在此处创建。

### onCountdownTick(counter)

每次<ins>倒计时</ins>触发。

- `counter` - 当前倒计时数字；从 `0` 到 `4`。

示例：

```lua
function onCountdownTick(counter)
     local counterArray = {'Three', 'Two', 'One', 'Go!', 'The song starts here'}
     debugPrint('Counter Num: '..counter..' | '..counterArray[counter + 1]) 
end
```

将打印：

```terminal
Counter Num: 0 | Three
Counter Num: 1 | Two
Counter Num: 2 | One
Counter Num: 3 | Go!
Counter Num: 4 | The song starts here
```

<details><summary><b>Haxe 独有：</b></summary>
<p> 

- `tick` - 当前倒计时数字（以单词表示）；从 `THREE` 到 `START`。
- `counter` - 当前倒计时数字；从 `0` 到 `4`。

示例：

```lua
function onCountdownTick(counter)
     local counterArray = {'Three', 'Two', 'One', 'Go!', 'The song starts here'}
     debugPrint('Counter Num: '..counter..' | '..counterArray[counter + 1]) 
end
```

将打印：

```terminal
Counter Num: 0 | Three
Counter Num: 1 | Two
Counter Num: 2 | One
Counter Num: 3 | Go!
Counter Num: 4 | The song starts here
```

</p>
</details>

***

# 事件钩子回调

### onEvent(eventName, value1, value2, strumTime)

如果<ins>事件箭头播放</ins>，则触发；可用于创建事件。

- `eventName` - 要使用的事件名称。
- `value1` - 事件的第一个值。
- `value2` - 事件的第二个值。
- `strumTime` - 执行事件的弹奏时间。

### onEventPushed(name, value1, value2, strumTime)

针对<ins>每个事件箭头</ins>触发，建议预缓存资源。

- `eventName` - 要使用的事件名称。
- `value1` - 事件的第一个值。
- `value2` - 事件的第二个值。
- `strumTime` - 执行事件的弹奏时间。

### eventEarlyTrigger(eventName, value1, value2, strumTime)

使<ins>事件提前触发</ins>。使用 `return` 语句以及指定的偏移量<ins>（以毫秒为单位）</ins>。

- `eventName` - 要使用的事件名称。
- `value1` - 事件的第一个值。
- `value2` - 事件的第二个值。
- `strumTime` - 执行事件的弹奏时间。

示例：

```lua
function eventEarlyTrigger(eventName)
     if eventName == 'Your event' then
          return 1000; -- 将提前 1 秒返回
     end
end
```

***

# 对话回调

### onNextDialogue(dialogueCount)

如果玩家<ins>移动到下一行对话</ins>，则触发。

- `dialogueCount` - 要检查的下一行对话；从 `0` 开始，但在到达下一行对话之前不会被实际调用。

### onSkipDialogue(dialogueCount)

如果<ins>当前对话行在文本中间被跳过</ins>，则触发。

- `dialogueCount` - 要检查的当前对话行；从 `0` 开始。

***

# 子状态回调

### onPause()

如果游戏从播放状态<ins>暂停</ins>，则触发。

> 此回调可以使用 `Function_Stop`；如果要打开暂停菜单，则**不得**返回 `Function_Stop`。

### onResume()

如果游戏从暂停状态<ins>恢复</ins>，则触发。

### onGameOver()

如果<ins>玩家因技术问题死亡</ins>，则触发。

> 此回调可以使用 `Function_Stop`；如果要让玩家能够死亡，则**不得**返回 `Function_Stop`。

### onGameOverStart()

在<ins>游戏结束画面开始</ins>时触发。

### onGameOverConfirm(retry)

如果<ins>玩家确认重试</ins>或返回菜单，则触发。

- `retry` - 检查玩家是否按下了重试按钮；返回一个 `boolean` 值。

***

# 按键回调

## 箭头
 
!> 对于与箭头相关的回调，HScript 上的参数将替换为箭头本身；例如：`note.noteType`。

### goodNoteHit(membersIndex, noteData, noteType, isSustainNote)
当**玩家成功击中箭头**时触发。

> _在此回调函数中可以使用 `Function_Stop`，但它目前仅用于阻止 HScript 版本的函数被调用；Lua 版本**不能**返回 `Function_Stop`，否则 HScript 版本将不会被调用。_

- `membersIndex` - 箭头成员 ID。
- `noteData` - 箭头方向；取值：`0,1,2,3`，分别对应左、下、上、右。
- `noteType` - 要检查的箭头类型。
- `isSustainNote` - 检查箭头是否为长按箭头；返回一个 `boolean` 值。

### goodNoteHitPre(membersIndex, noteData, noteType, isSustainNote)
在**计算成功击中箭头之前**触发；参数与 `goodNoteHit` 相同。

> _在此回调函数中可以使用 `Function_Stop`，但它目前仅用于阻止 HScript 版本的函数被调用；Lua 版本**不能**返回 `Function_Stop`，否则 HScript 版本将不会被调用。_

### opponentNoteHit(membersIndex, noteData, noteType, isSustainNote)
当**对手成功击中箭头**时触发；参数与 `goodNoteHit` 相同。

> _在此回调函数中可以使用 `Function_Stop`，但它目前仅用于阻止 HScript 版本的函数被调用；Lua 版本**不能**返回 `Function_Stop`，否则 HScript 版本将不会被调用。_

### opponentNoteHitPre(membersIndex, noteData, noteType, isSustainNote)
在**计算对手成功击中箭头之前**触发；参数与 `goodNoteHit` 相同。

> _在此回调函数中可以使用 `Function_Stop`，但它目前仅用于阻止 HScript 版本的函数被调用；Lua 版本**不能**返回 `Function_Stop`，否则 HScript 版本将不会被调用。_

### onSpawnNote(membersIndex, noteData, noteType, isSustainNote, strumTime)
当**箭头生成**时触发。

- `strumTime` - 箭头的击打时间。

### noteMiss(membersIndex, noteData, noteType, isSustainNote)
当**玩家错过箭头**时触发；参数与 `goodNoteHit` 相同。

> _在此回调函数中可以使用 `Function_Stop`，但它目前仅用于阻止 HScript 版本的函数被调用；Lua 版本**不能**返回 `Function_Stop`，否则 HScript 版本将不会被调用。_

### noteMissPress(noteData)
当**没有箭头时玩家按下按键**时触发。仅在**禁用“Ghost Tapping”（幽灵点击）**时才会激活。

- `noteData` - 每个方向上的箭头数据；取值：`0,1,2,3`，分别对应左、下、上、右。

## 按键事件

### onKeyPress(key)
当玩家按下**箭头控制按钮**时触发。

- `key` - 按下的按键方向；取值：`0,1,2,3`，分别对应左、下、上、右。

### onKeyPressPre(key)
在**计算按键按下之前**触发。

> _在此回调函数中可以使用 `Function_Stop`，但**不能**返回 `Function_Stop`，否则输入系统将无法正常工作，并且 `onKeyPress()` 和 `onGhostTap()` 也将不会被调用；除非您打算创建自己的输入系统，否则不建议在此函数中使用 `Function_Stop`。_

- `key` - 按下的按键方向；取值：`0,1,2,3`，分别对应左、下、上、右。

### onKeyRelease(key)
当玩家释放**箭头控制按钮**时触发。

- `key` - 释放的按键方向；取值：`0,1,2,3`，分别对应左、下、上、右。

### onKeyReleasePre(key)
在**计算按键释放之前**触发。

> _在此回调函数中可以使用 `Function_Stop`，但**不能**返回 `Function_Stop`，否则弹奏动画将无法播放，并且 `onKeyRelease()` 也将不会被调用。_

- `key` - 释放的按键方向；取值：`0,1,2,3`，分别对应左、下、上、右。

### onGhostTap(key)
当**没有箭头时按下箭头控制按钮**时触发；不要与 `noteMissPress()` 混淆。

- `key` - 按下的按键方向；取值：`0,1,2,3`，分别对应左、下、上、右。

***

## 完成回调

### onTimerCompleted(tag, loops, loopsLeft)
当**计时器完成**时触发；不要与 `onTweenCompleted()` 函数混淆。

- `tag` - 要使用的计时器标签。
- `loops` - 检查计时器完全结束后循环的次数。
- `loopsLeft` - 检查计时器剩余的循环次数。

### onTweenCompleted(tag, vars)
当**补间动画完成**时触发。

- `tag` - 要使用的补间动画标签。
- `vars` - 补间动画中使用的变量；仅在调用 `startTween()` 和 `doTween()` 函数时才会被调用。

### onSoundFinished(tag)
当**声音播放完成**时触发。

- `tag` - 要使用的音频标签。

***

## 动态函数

动态函数/回调可以在 HScript 或 `runHaxeCode()` 中**被覆盖**，这意味着您可以改变函数的工作方式。

例：

```haxe
function onCreatePost() {
     game.updateIconsPosition = function() {
          game.iconP1.x = 314;
          game.iconP2.x = 114;
          // 现在图标将更新到这些位置并保持静态，而不是根据生命值更新位置
          // 如果您不希望它执行任何操作，甚至可以将函数设置为空
     }
}
```

**说明：**

这段代码展示了如何覆盖 `updateIconsPosition` 函数。默认情况下，该函数会根据玩家的生命值更新图标位置。但是，通过在 `onCreatePost()` 函数中重新定义该函数，您可以将其更改为将图标固定在特定位置。
