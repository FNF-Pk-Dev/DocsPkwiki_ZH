# 按键/键盘按下函数

> _所有键盘和游戏手柄函数最近都被添加到 <kbd>0.6+</kbd> 版本的 HScript 中。_

<details><summary><b>按键输入版本兼容性：</b></summary>
<p> 

| 按键     | 支持版本  | 支持的函数                                  |
|----------|-------------|-----------------------------------------------------|
| `left`   | 仍然使用     | `keyJustPressed()`, `keyPressed()`, `keyReleased()` |
| `down`   | 仍然使用     | `keyJustPressed()`, `keyPressed()`, `keyReleased()` |
| `up`     | 仍然使用     | `keyJustPressed()`, `keyPressed()`, `keyReleased()` |
| `right`  | 仍然使用     | `keyJustPressed()`, `keyPressed()`, `keyReleased()` |
| `accept`  | 仍然使用     | `keyJustPressed()`, `keyPressed()`, `keyReleased()` |
| `back` | 仍然使用     | `keyJustPressed()`, `keyPressed()`, `keyReleased()` |
| `pause`   | 仍然使用     | `keyJustPressed()`, `keyPressed()`, `keyReleased()` |
| `reset`  | 仍然使用     | `keyJustPressed()`, `keyPressed()`, `keyReleased()` |
| `space`  | 仍然使用 | `keyJustPressed()`, `keyPressed()`, `keyReleased()` |

</p>
</details>

### keyJustPressed(name:String)
获取当前游戏中**刚刚按下**的控制键绑定。

- `name` - 要使用的键绑定的名称。

### keyPressed(name:String)
获取当前游戏中**正在按下**的控制键绑定。

- `name` - 要使用的键绑定的名称。

### keyReleased(name:String)
获取当前游戏中**刚刚释放**的控制键绑定。

- `name` - 要使用的键绑定的名称。

### keyboardJustPressed(name:String)
获取当前游戏中**刚刚按下**的键盘按键。

- `name` - 键盘上的按键名称；必须为大写字母。

### keyboardPressed(name:String)
获取当前游戏中**正在按下**的键盘按键。

- `name` - 键盘上的按键名称；必须为大写字母。

### keyboardReleased(name:String)
获取当前游戏中**刚刚释放**的键盘按键。

- `name` - 键盘上的按键名称；必须为大写字母。

***

# 鼠标函数
按钮：`left`、`right`、`middle`

### mouseClicked(name:String)
获取当前帧中**刚刚按下**的鼠标按钮。

- `name` 鼠标按钮的名称；默认值：`left`。

### mousePressed(name:String)
获取当前帧中**正在按下**的鼠标按钮。

- `name` 鼠标按钮的名称；默认值：`left`。

### mouseReleased(name:String)
获取当前帧中**刚刚释放**的鼠标按钮。

- `name` 鼠标按钮的名称；默认值：`left`。

***

### getMouseX(camera:String)
返回特定相机上鼠标的**当前 x 值**。

- `camera` - 当前相机状态，可以是 `camGame`、`camHUD` 或 `camOther`。

### getMouseY(camera:String)
返回特定相机上鼠标的**当前 y 值**。

- `camera` - 当前相机状态，可以是 `camGame`、`camHUD` 或 `camOther`。

***

# 游戏手柄函数
!> _由于这些函数在脚本中很少使用，我不确定这是否是使用它们的方式，因此请谨慎对待本节内容，并请帮助我。_

[点击此处查看 ID 控制列表](https://api.haxeflixel.com/flixel/input/gamepad/FlxGamepadInputID.html)

### gamepadJustPressed(id:Int, name:String)
获取当前帧中**刚刚按下**的游戏手柄按钮。

- `id` - 游戏手柄的 ID 控制。
- `name` - 游戏手柄按键的名称。

### gamepadPressed(id:Int, name:String)
获取当前帧中**正在按下**的游戏手柄按钮。

- `id` - 游戏手柄的 ID 控制。
- `name` - 游戏手柄按键的名称。

### gamepadReleased(id:Int, name:String)
获取当前帧中**刚刚释放**的游戏手柄按钮。

- `id` - 游戏手柄的 ID 控制。
- `name` - 游戏手柄按键的名称。

### anyGamepadJustPressed(name:String)
获取当前帧中**刚刚按下**的**任何游戏手柄**按钮。

- `name` - 任何游戏手柄按键的名称。

### anyGamepadPressed(name:String)
获取当前帧中**正在按下**的**任何游戏手柄**按钮。

- `name` - 任何游戏手柄按键的名称。

### anyGamepadReleased(name:String)
获取当前帧中**刚刚释放**的**任何游戏手柄**按钮。

- `name` - 任何游戏手柄按键的名称。

***

### gamepadAnalogX(id:Int, ?leftStick:Bool = true)
游戏手柄摇杆的**x 轴值**。

- `id` - 游戏手柄的 ID 控制。
- `leftStick` - 是否是左摇杆还是右摇杆；默认值：`true`。

### gamepadAnalogY(id:Int, ?leftStick:Bool = true)
游戏手柄摇杆的**y 轴值**。

- `id` - 游戏手柄的 ID 控制。
- `leftStick` - 是否是左摇杆还是右摇杆；默认值：`true`。
