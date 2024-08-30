
!> _由于我对着色器的了解有限，请对所有着色器函数持保留态度，您可以提出拉取请求以更正函数和参数的描述；我们始终感谢您的帮助。_

# 关于着色器
计算机图形学中的着色器是一种在图形处理单元 (GPU) 上执行的代码。<ins>它通过特殊效果来操纵渲染的对象</ins>，例如 `blur`（模糊）、`distortion`（扭曲）、`higher/lower hue`（更高/更低的色调）等 _(等等，你明白我的意思)_

Psych Engine 使用两种类型的着色器：<ins>顶点着色器和片段着色器</ins>；顶点着色器使用文件格式 `.vert` 来操纵<ins>对象顶点的属性</ins>；片段着色器使用文件格式 `.frag` 来计算<ins>对象的顏色和其他属性</ins>。这些着色器必须位于 `mods/shaders` 文件夹中。

我不会在这里详细讨论语法和其他内容。但是，如果您想了解更多信息，我强烈建议您观看[这个](https://www.youtube.com/watch?v=xZM8UJqN1eY)之类的视频。或者，您可以从[ShaderToy](https://www.shadertoy.com)“借用”一个着色器，请记住链接<ins>原始脚本并注明作者</ins>。

示例（片段着色器）：
```frag
// 作者：mrlem
// 修改者：bbpanzu
// 链接：https://www.shadertoy.com/view/lddXWS

// 此 frag 脚本已修改以提高兼容性

// 添加这两个（非常重要）
uniform vec2 iResolution;     // 视口分辨率（以像素为单位）
uniform float iTime;          // 着色器播放时间（以秒为单位）

const float RADIUS  = 200.0;
const float BLUR    = 500.0;
const float SPEED   = 2.0;

void main() { // "mainImage(out vec4 fragColor, in vec2 fragCoord)" 被替换为 "void main()"
     vec2 fragCoord = openfl_TextureCoordv * iResolution; // 出于某种原因添加了此项

     vec2 uv = fragCoord.xy / iResolution.xy;
     vec4 pic = texture2D(bitmap, vec2(uv.x, uv.y));
     // "texture2D" 被替换为 "texture"，以便像素不会渲染为黑色。
     // "iChannel" 采样器被替换为 "bitmap" 采样器
        
     vec2 center = iResolution.xy / 2.0;
     float d = distance(fragCoord.xy, center);
     float intensity = max((d - RADIUS) / (2.0 + BLUR * (1.0 + sin(iTime * SPEED))), 0.0);

     gl_FragColor = vec4(intensity + pic.r, intensity + pic.g, intensity + pic.b, 0.2);
     // "fragColor" 被替换为 "gl_FragColor"
}
```

***

# 创建/删除着色器

如果你想创建着色器在游戏里面,或者在箭头等HUD镜头
你可以试试这样
```lua
function onCreate()
runHaxeCode([[
//设置shader
game.initLuaShader('chromaticWarp');
game.initLuaShader('bloom');

//创建shader
shader0 = game.createRuntimeShader('chromaticWarp');
shader1 = game.createRuntimeShader('bloom');

//将shader设置在游戏和HUD
game.camGame.setFilters([new ShaderFilter(shader0),new ShaderFilter(shader1)]);
game.camHUD.setFilters([new ShaderFilter(shader0),new ShaderFilter(shader1)]);

//shader变量数值
shader0.setFloat('distortion',0);

//setVar全局变量
setVar('shader0',shader0);

shader1.setFloat('dim',2.5);
shader1.setFloat('size',0);
setVar('shader1',shader1);
]])
--shaderCoordFix()
end


function onUpdatePost(e)
runHaxeCode([[
//使用shader0标签的里面的iTime变量来持续变更
shader0.setFloat('iTime',]]..e..[[);
]])
end


function onDestroy()
runHaxeCode([[FlxG.game.setFilters([]);]])
end


function onGameOver()
runHaxeCode([[FlxG.game.setFilters([]);]])
end


function shaderCoordFix()
runHaxeCode([[
resetCamCache = function(?spr) {
if (spr == null || spr.filters == null) return;
@:privateAccess {
spr.__cacheBitmap = null;
spr.__cacheBitmapData = null;
}
}

fixShaderCoordFix = function(?_) {
resetCamCache(FlxG.game.flashSprite);
resetCamCache(game.camGame.flashSprite);
resetCamCache(game.camHUD.flashSprite);
resetCamCache(game.camOther.flashSprite);
}

FlxG.signals.gameResized.add(fixShaderCoordFix);
fixShaderCoordFix();
return;
]])


local temp = onDestroy
function onDestroy()
runHaxeCode([[
FlxG.signals.gameResized.remove(fixShaderCoordFix);
]])
if (temp) then temp() end
end
end
```
觉得还是太难？那就看这[脚本样例]()

***

### initLuaShader(name:String, ?glslVersion:Int = 120)
初始化对象要使用的着色器。

- `name` - 着色器的名称。
- `glslVersion` - 可选参数，GLSL 着色器版本；默认值：`120`。

### setSpriteShader(obj:String, shader:String)
设置对象要使用的指定着色器。

- `obj` - 要使用的对象标签名称。
- `name` - 着色器的名称。

### removeSpriteShader(obj:String)
从对象中删除着色器。

- `obj` - 要使用的对象标签名称。

***

# 着色器属性设置
### setShaderInt(obj:String, prop:String, value:Int)
使用新值设置当前着色器的<ins>`int` 数字类型变量</ins>。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `int` 变量。
- `value` - `int` 变量的新值。

### setShaderFloat(obj:String, prop:String, value:Float)
使用新值设置当前着色器的<ins>`float` 数字类型变量</ins>。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `float` 变量。
- `value` - `float` 变量的新值。

### setShaderBool(obj:String, prop:String, value:Bool)
使用新值设置当前着色器的<ins>`boolean` 类型变量</ins>。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `boolean` 变量。
- `value` - `boolean` 变量的新值。

### setShaderSampler2D(obj:String, prop:String, bitmapdataPath:String)
使用新值设置当前着色器的<ins>`sampler2D` 类型变量</ins>。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `sampler2D` 变量。
- `bitmapdataPath` - 精灵要使用的图像精灵。

***

### setShaderIntArray(obj:String, prop:String, values:Dynamic)
使用新值设置当前着色器的<ins>`int` 数字类型数组变量</ins>。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `int` 数组变量。
- `values` - `int` 数组变量的新值。

参考（着色器数组语法）：
```frag
// 类型名称[最大长度] = {值}; <-- 语法
// 最大长度值是可选的，将最大长度值留空将自动确定数组长度
// 数组的第一个值是'0'
int myIntArray[2] = {1, 2, 3}; 
```

### setShaderFloatArray(obj:String, prop:String, value:Dynamic)
使用新值设置当前着色器的<ins>`float` 数字类型数组变量</ins>。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `float` 数组变量。
- `values` - `float` 数组变量的新值。

### setShaderBoolArray(obj:String, prop:String, value:Dynamic)
使用新值设置当前着色器的<ins>`boolean` 类型数组变量</ins>。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `boolean` 数组变量。
- `values` - `boolean` 数组变量的新值。

***

# 着色器属性获取器
### getShaderInt(obj:String, prop:String)
获取当前着色器的<ins>`int` 数字类型变量</ins>的当前值。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `int` 变量。

### getShaderFloat(obj:String, prop:String)
获取当前着色器的<ins>`float` 数字类型变量</ins>的当前值。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `float` 变量。

### getShaderBool(obj:String, prop:String)
获取当前着色器的<ins>`boolean` 类型变量</ins>的当前值。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `boolean` 变量。

***

### getShaderIntArray(obj:String, prop:String)
获取当前着色器的<ins>`int` 数字类型数组变量</ins>的当前值。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `int` 数组变量。

### getShaderFloatArray(obj:String, prop:String)
获取当前着色器的<ins>`float` 数字类型数组变量</ins>的当前值。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `float` 数组变量。

### getShaderBoolArray(obj:String, prop:String)
获取当前着色器的<ins>`boolean` 类型数组变量</ins>的当前值。

- `obj` - 要使用的对象标签名称。
- `prop` - 要使用的 `boolean` 数组变量。