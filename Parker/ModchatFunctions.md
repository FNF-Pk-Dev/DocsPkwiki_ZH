# Modifiers

***

## Modifiers简介

Modifiers是一种由模型图表使用的“效果”，每
个模型都运行代码，每次绘制到屏幕上时都
会修改箭头/弹奏的位置和数据,它们可以简
单到可以抵消X/Y/Z，也可以复杂到可以单
独编辑每个箭头的信息。Modifiers可以堆叠，
并设置为仅适用于特定的车道、操场或播放器

每个Modifiers都有自己的值，用来改变它的效
果，Modifiers也可以有子值来编辑某些东西，
比如效果的速度。Modifiers也有一个基值，当
值-基值时，它总是不做任何事情，作为禁
用它的一种方式，对于大多数Modifiers来说,
这个值为'0'。

***

## 创建Modifiers

**在编辑器中：**

你可以在编辑器内的“Modifiers”选项卡中创建它们。

创建Modifiers需要以下几样东西：

* **Name**（必须唯一）
* **Class**
* **Type**（可选）
* **Playfield**（可选）
* **Lane**（可选）

**Name：**一个字符串，用于输入“Modifiers名称”输入框，它们必须是唯一的，如果重复将会覆盖之前的Modifiers。

**Class：**一个字符串，用于表示Modifiers使用的Class，你可以从下拉菜单中选择内置的Class，或者在“ModifiersClass”输入框中输入自定义Modifiers的名称，Class决定了Modifiers的实际功能（例如，选择 XModifier 作为Class意味着它只会改变箭头的 x 值）。

**Type：**一个字符串，用于表示Type，Type是可选的，默认为“全部”，有 4 种Type可以选择，分别是“全部”、“玩家”、“对手”和“Lane”，其中大部分是不言自明的，“Lane”还需要设置一个单独的值来改变它影响的Lane。

**Playfield：**一个值，用于影响Modifiers将影响的Playfield，如果设置为 -1，它将作用于所有Playfield。

**Lane：**一个与“Lane”Type一起使用的值，用于改变它影响的Lane。

***

## **在脚本中：**

`startMod(name:String, class:String, type:String, playfield:Int)`

*  开始一个Modifiers

`setModTargetLane(name:String, lane:Int)`

* 为Modifiers设置目标Lane

**示例：**

`startMod('reverse', 'ReverseModifier', 'Lane', -1)`

* 开始一个名为“reverse”的Modifiers，使用“ReverseModifier”类，类型为“Lane”，作用于所有游戏区域（-1）。

`setModTargetLane('reverse', 0)`

*  将名为“reverse”的Modifiers的目标Lane设置为 0。

这段代码定义了一系列 Lua 回调函数，用于在游戏中操控Modifiers。

* `setMod(name:String, value:Float)`：设置名为 `name` 的Modifiers的值为 `value`。

### setSubMod'(name:String, subValName:String, value:Float)`：设置名为 `name` 的Modifiers的子值 `subValName` 为 `value`。

### setModTargetLane'(name:String, value:Int)`：设置名为 `name` 的Modifiers的目标音轨为 `value`。

### setModPlayfield'(name:String, value:Int)`：设置名为 `name` 的Modifiers作用的游戏区域为 `value`。

### addPlayfield'(?x:Float = 0, ?y:Float = 0, ?z:Float = 0)`：添加一个新的游戏区域，坐标为 (x, y, z)。

### removePlayfield'(idx:Int)`：移除索引为 `idx` 的游戏区域。

### tweenModifier'(modifier:String, val:Float, time:Float, ease:String)`：在 `time` 时间内，使用 `ease` 过渡方式，将名为 `modifier` 的Modifiers的值过渡到 `val`。

### tweenModifierSubValue'(modifier:String, subValue:String, val:Float, time:Float, ease:String)`：在 `time` 时间内，使用 `ease` 过渡方式，将名为 `modifier` 的Modifiers的子值 `subValue` 过渡到 `val`。

### setModEaseFunc'(name:String, ease:String)`：设置名为 `name` 的Modifiers的过渡方式为 `ease`。

### set'(beat:Float, argsAsString:String)`：在一个指定的 `beat` 上设置Modifiers，具体的参数通过字符串 `argsAsString` 传递。

### ease(beat:Float, time:Float, easeStr:String, argsAsString:String) :在一个指定的 `beat` 开始，使用 `easeStr` 过渡方式，在 `time` 时间内过渡Modifiers，具体的参数通过字符串 `argsAsString` 传递。

## 内置Modifiers列表

**DrunkXModifier, DrunkYModifier, DrunkZModifier** - 琴弦和箭头摇摆/波动，箭头以不同的速度移动，因此它们在到达琴弦线时会“摆动”，主值影响波浪的大小，也有子值“speed”（速度）。

**TipsyXModifier, TipsyYModifier, TipsyZModifier** - 琴弦和箭头以交替的模式摇摆/波动，主值影响波浪的大小，也有子值“speed”（速度）。

**ReverseModifier** - 翻转滚动方向（向上变为向下，向下变为向上）。

**IncomingAngleModifier** - 改变箭头的来源角度，主Modifiers值无效，具有子值“x”和“y”。

**RotateModifier** - 围绕屏幕旋转箭头/琴弦（基于其默认位置），主Modifiers值无效，具有子值“x”和“y”。

**StrumLineRotateModifier** - 围绕屏幕旋转琴弦线（基于其默认位置），主Modifiers值无效，具有子值“x”和“y”。

**XModifier, YModifier, ZModifier** - 改变 x/y/z 位置。

**ConfusionModifier** - 改变箭头角度。

**ScaleModifier, ScaleXModifier, ScaleYModifier** - 改变箭头/琴弦的缩放比例，基值为 1！而不是 0。

**SpeedModifier** - 速度倍增器，基值为 1！而不是 0。

**StealthModifier, NoteStealthModifier** - 改变琴弦/箭头的透明度（0 = 可见，1 = 不可见，别搞混了）。

**InvertModifier** - 交换箭头轨道/列，未反转：0,1,2,3 反转：1,0,3,2。

**FlipModifier** - 翻转轨道/列，未翻转：0,1,2,3 翻转：3,2,1,0。

**MiniModifier** - 缩小整个琴弦线，基值为 1！而不是 0。

**BeatXModifier, BeatYModifier, BeatZModifier** - 箭头/琴弦将随着歌曲的节拍移动。

**BounceXModifier, BounceYModifier, BounceZModifier** - 箭头在向琴弦线移动时弹跳。

**BoostModifier** - 箭头在向琴弦线移动时加速。

**BrakeModifier** - 箭头在向琴弦线移动时减速。

## 自定义Modifiers

你可以使用 .hx 文件中的 hscript 创建自定义Modifiers，这些文件必须放在歌曲数据文件夹（包含图表 .json 文件的文件夹）内名为“customMods”的文件夹中。

**模板：**

```haxe
 initMod(mod)
{
    mod.noteMath = (noteData, lane, curPos, pf)
    {
        // 在这里添加修改音符位置的代码
    };
    mod.strumMath = (noteData, lane, pf)
    {
        // 在这里添加修改琴弦位置的代码
    };
    mod.incomingAngleMath = (lane, curPos, pf)
    {
        // 返回一个包含 x 和 y 角度的数组
        return [0, 0];
    };
    mod.curPosMath = (lane, curPos, pf)
    {
        // 返回修改后的 curPos 值
        return curPos;
    };
    mod.noteDistMath = (noteDist, lane, curPos, pf)
    {
        // 返回修改后的音符距离值
        return noteDist;
    };
}
```