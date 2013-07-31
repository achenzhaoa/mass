## mass 
mass a css toolbox based on [ __mcss(The new css preprocessor)__ ](https://github.com/leeluolee/mcss)

mass提供大量的函数, 同时也是mcss的官方使用示例. 

## 使用

### 1. 安装mcss
首先,确保你安装了nodejs 和 npm.

```shell
npm install -g mcss
```


### 2. 引入mass库

__直接import__ : 

mcss可以依赖远程mcss文件, (只要进程不退出, 远程文件会缓存在内存中, 比如开启了watch参数，这样只会在第一次build中会有载入开销), 我们可以很方便的引用网络上的mcss文件
```css
/* mass入口文件 */
@import 'https://rawgithub.com/leeluolee/mass/master/mass/index.mcss';

/* 此时你就可以使用mass的函数了 */
.m-home{
  $transition: all .1s ease-in-out; 
}
```


__本地使用时，你也可以将mass加入到你的include path__(配置文件或命令),
```
mcss --include path/to/mass_dir
```
 然后就只需要`@import`短名了

```css
@import 'mass/css3';
@import 'mass/helper';
```


## 文档目录

1. [__css3.mcss__](#css3)[(源码)](https://github.com/leeluolee/mass/blob/master/mass/css3.mcss)      —— 提供海量的css3的兼容处理(由于mcss的强大特性，其实没写多少代码)
2. [__reset.mcss__](#reset)[(源码)](https://github.com/leeluolee/mass/blob/master/mass/reset.mcss)       —— 提供多种reset函数, nec-reset, normalize ... etc
3. [__helper.mcss__](#helper)[(源码)](https://github.com/leeluolee/mass/blob/master/mass/helper.mcss)      —— 提供一些常用帮助函数，比如$clearfix等等
4. [__layout.mcss__](#layout)[(源码)](https://github.com/leeluolee/mass/blob/master/mass/layout.mcss)      —— 提供一些布局相关函数
5. [__effect.mcss__](#effect)[(源码)](https://github.com/leeluolee/mass/blob/master/mass/effect.mcss)      —— 提供一些常用的animation mixin, 并提供参数控制.
6. [__functions.mcss__](#functions)[(源码)](https://github.com/leeluolee/mass/blob/master/mass/functions.mcss)   —— 一些函数集合, mass的每个文件都或多或少依赖了这个函数
7. index.mcss[(源码)](https://github.com/leeluolee/mass/blob/master/mass/index.mcss)      —— 以上所有子文件的入口文件, 你偷懒可以只引入这个文件

__需要注意的是__ : mass中的所有文件都可以单独引入, 已经处理好了依赖关系。


<a name="doc"></a>
## 使用文档
源码请看对应文件

<a name="css3"></a>
### 1. [css3.mcss](https://github.com/leeluolee/mass/blob/master/mass/css3.mcss)

css3主要是帮助我们无痛的使用css3特性,

#### 同名vendor prefixr:

一些简单的vendor prefix占据了css3处理的大部分，参考的是这个在维护中的[css浏览器实验列表](http://peter.sh/experiments/vendor-prefixed-css-property-overview/)

__Example__

```css
.u-btn{
  /* 注意mcss同时支持两种函数调用方式 */
  $transition: background-color 0.1s ease-in-out;
  $box-sizing(border-box)
}

```
__Outport__

```css
.u-btn{
  -webkit-transition:background-color 0.1s ease-in-out;
  -moz-transition:background-color 0.1s ease-in-out;
  transition:background-color 0.1s ease-in-out;
  -webkit-box-sizing:border-box;
  -moz-box-sizing:border-box;
  box-sizing:border-box;
}
```

其它例如`$box-sizing`之类的也是一致,详细列表[`css3.file:L12`](https://github.com/leeluolee/mass/blob/master/mass/css3.mcss#L12)

* transition (webkit moz),
* transition-delay (webkit moz),
* transition-property (webkit moz),
* transition-duration (webkit moz),
* transition-timing-function (webkit moz),
* animation (webkit moz), 
* animation-delay (webkit moz), 
* animation-name (webkit moz), 
* animation-direction (webkit moz), 
* animation-duration (webkit moz), 
* animation-fill-mode (webkit moz), 
* animation-iteration-count (webkit moz), 
* animation-timing-function (webkit moz), 
* columns (webkit moz),
* column-count (webkit moz),
* column-gap (webkit moz),
* column-fill (webkit moz),
* column-rule (webkit moz),
* column-rule-color (webkit moz),
* column-rule-style (webkit moz),
* column-rule-width (webkit moz),
* column-span (webkit moz),
* column-width (webkit moz),
* box-orient (webkit moz),
* box-sizing (webkit moz),
* box-pack (webkit moz),
* box-align (webkit moz),
* box-direction (webkit moz),
* box-lines (webkit moz),
* box-ordinal-group (webkit moz),
* box-flex (webkit moz),
* box-flex-group (webkit moz),
* box-shadow (webkit moz),
* transform null,
* transform-origin null,
* transform-style null,
* perspective (webkit moz),
* perspective-origin (webkit moz),
* appearance (webkit moz ms o),
* backface-visibility (webkit moz),
* background-clip webkit,
* background-origin webkit,
* background-size webkit,
* border-box (webkit moz),
* box-shadow webkit,
* user-select (webkit moz ms),
* hyphens (epub moz ms),
* filter (moz webkit);


__所有以上css3的参数与原样式一致__


#### $border-radius($radius, $direction)
`$border-radius` 除了处理前缀, 可以传入额外参数控制位置, 

__Arguments__

1. $radius —— 圆角半径
2. $direction —— (可选) 圆角的位置 可以是角(top left) 也可以是边(top)

__Example__

```
.radius{
  $border-radius: 3px;
}
.radius-corner{
  $border-radius: 3px, top left;
}
.radius-side{
  $border-radius: 3px, top;
}
```

__Outport__

```
.radius{
  -moz-border-radius:3px;
  border-radius:3px;
}
.radius-corner{
  -moz-border-top-left-radius:3px;
  border-top-left-radius:3px;
}
.radius-side{
  -moz-border-top-left-radius:3px;
  border-top-left-radius:3px;
  -moz-border-top-right-radius:3px;
  border-top-right-radius:3px;
}
```



#### $linear-gradient = ($direct, $color-stops...)
线型渐变

__Argument__

1. `$direct`[可以选默认top] : 从哪个方向开始  如 `top left`，`top` 或者以哪个角度 如 45deg 等;
2. `$color-staops`: 颜色值列表, 可以加入百分比或长度 如 #fff 50%, #ccc 20px , color-stop可以有无限个;

__要点__

0. 总体就是参数与规范类似
1. 默认会mix 最末和最先的颜色进行mix 作为ie低版本的fallback
2. 如果是垂直或者水平渐变，比如 top bottom right 和 left 会生成ie下的滤镜形式，其它角度则不生成

__Exmaple__

```
$primary = #f6ffc1;
.m-top{
  /* l-adjust 是调节亮度 */
  $linear-gradient: right, $primary , l-adjust($primary, 10%);
}
```

__Outport__
```css
.m-top{
  background-color:#faffdb;
  background-image:-webkit-linear-gradient(right,#f6ffc1,#fdfff4);
  background-image:-moz-linear-gradient(right,#f6ffc1,#fdfff4);
  background-image:-ms-linear-gradient(right,#f6ffc1,#fdfff4);
  background-image:-o-linear-gradient(right,#f6ffc1,#fdfff4);
  background-image:linear-gradient(to left,#f6ffc1,#fdfff4);
  filter:progid:DXImageTransform.Microsoft.gradient(startColorstr='#fdfff4', endColorstr='#f6ffc1', GradientType=1) \9;
}
```


#### $radial-gradient = ($color-stops...) 
圆形渐变, 与线性渐变类似，不过这里color-stop的扩散方向是从圆点到外圈，

__Argument__

1. `$color-stops`: 从内向外的圆颜色层级, 一样可以加入百分比或长度值控制比例

__Exmaple__
```
.m-top{
  $radial-gradient: #aaa, #ccc 20%, #ddd 80%, #eee;
}
```

__Outport__
```
.m-top{
  background-color:#ccc;
  background-image:-webkit-radial-gradient(ellipse,#aaa,#ccc 20%,#ddd 80%,#eee);
  background-image:-moz-radial-gradient(ellipse,#aaa,#ccc 20%,#ddd 80%,#eee);
  background-image:-ms-radial-gradient(ellipse,#aaa,#ccc 20%,#ddd 80%,#eee);
  background-image:-o-radial-gradient(ellipse,#aaa,#ccc 20%,#ddd 80%,#eee);
  background-image:radial-gradient(ellipse,#aaa,#ccc 20%,#ddd 80%,#eee);
  background-repeat:no-repeat;
}
```


#### $keyframes = ($name, $block)
兼容浏览器的keyframs写法, 与@keyframes对应, mass同时利用它封装了[`effect.mcss`](https://github.com/leeluolee/mass/blob/master/mcss/effect.mcss)

__Arguments__ 

1. $name  —— keyframes 名称
2. $block —— 传入的block函数, 这个函数接受的第一个参数是前缀, 大部分情况你不需要这个参数, 比如 `-o-`, `-webkit-`


__Example__

```
$block =  ($prefix){
    20%{
        #{$prefix}transform: scale(2.0,2.0);
    }
    to{
        #{$prefix}transform: scale(1.0,1.0);
    }
}

$keyframes(hello, $block);
```

__Outport__

```css
@-webkit-keyframes hello{
  20%{
    -webkit-transform:scale(2,2);
  }
  to{
    -webkit-transform:scale(1,1);
  }
}
@-moz-keyframes hello{
  20%{
    -moz-transform:scale(2,2);
  }
  to{
    -moz-transform:scale(1,1);
  }
}
@-o-keyframes hello{
  20%{
    -o-transform:scale(2,2);
  }
  to{
    -o-transform:scale(1,1);
  }
}
@keyframes hello{
  20%{
    transform:scale(2,2);
  }
  to{
    transform:scale(1,1);
  }
}
```



#### $placeholder ($block)  

控制placeholder的样式

__参数__:
一个block(即无参数的函数);

__示例__:

```
#input1{
  $placeholder({
    color:#090; 
    background:#fff; 
    text-transform:uppercase;
  });
}

// 在最外层调用
$placeholder({
  color:#090; 
  background:#fff; 
  text-transform:uppercase;
});
 
```

__输出__

```css
#input1::-webkit-input-placeholder{
  color:#090;
  background:#fff;
  text-transform:uppercase;
}
#input1::-moz-placeholder{
  color:#090;
  background:#fff;
  text-transform:uppercase;
}
#input1:-moz-placeholder{
  color:#090;
  background:#fff;
  text-transform:uppercase;
}
#input1:-ms-placeholder{
  color:#090;
  background:#fff;
  text-transform:uppercase;
}

::-webkit-input-placeholder{
  color:#090;
  background:#fff;
  text-transform:uppercase;
}
::-moz-placeholder{
  color:#090;
  background:#fff;
  text-transform:uppercase;
}
:-moz-placeholder{
  color:#090;
  background:#fff;
  text-transform:uppercase;
}
:-ms-placeholder{
  color:#090;
  background:#fff;
  text-transform:uppercase;
}
```

#### $hidpi = ($block, $ratio = 1.5)
由于处理高dpi的media query的兼容性问题

__Arguments__

1. $block -- 传入@media中的block
2. $ratio —— device-pixel-ratio 默认1.5


__Example__ 

```
$hidpi({
    body{
        left: 10px;
    }
    p{
        right: 20px;
    }
}, 2.0)

```

__Outport__
```
@media only screen and (-webkit-min-device-pixel-ratio: 2),
  only screen and (min--moz-device-pixel-ratio: 2),
  only screen and (-o-min-device-pixel-ratio: 2/1),
  only screen and (min-resolution: 192dpi),
  only screen and (min-resolution: 2dppx){
  body{
    left:10px;
  }
  p{
    right:20px;
  }
}

```


<a name="reset"></a>
### 2. [reset.mcss](https://github.com/leeluolee/mass/blob/master/mass/reset.mcss)
目前提供`$reset-normalize` 和 `$nec-reset` 分别提供不同功能层级的reset需要,分别Copy自[NEC](http://nec.netease.com/framework/css-reset.html) 与 [normalize](https://github.com/necolas/normalize.css/tree/v1)

__Exmaple__

```
@import 'mass/reset.mcss'
$reset-nec();
// or $reset-normalize();

```

或者, 自动设置配置变量`$include-reset` 进行对应reset的include

```
$include-reset = nec;
@import 'mass/reset.mcss'
```


__Tips__

除了使用函数之外, 你可以在include 进reset 之前 设置 $ ?= false;


<a name="helper"></a>
### 3. [helper.mcss](https://github.com/leeluolee/mass/blob/master/mass/helper.mcss)

helper主要提供一些类似 $clearfix的帮助函数,帮助处理一些兼容性问题, 或者集合缩写



#### $clearfix
清除浮动, 这应该是最常用的mixin

__Example__
```
.container{
  $clearfix();
}
```

__Outport__
```css
.container{
  *zoom:1;
}
.container:before,.container:after{
  display:table;
  content:"";
  line-height:0;
}
.container:after{
  clear:both;
}
```


#### $display($type)

display处理了有关display的兼容性问题, 比如inline-box, box.

__Example__:

```css
body{
  $display: inline-block;
}
p{
  $display: box;
}

```

__Outport__:

```
body{
  display:inline-block;
  vertical-align:baseline;
  zoom:1;
  *display:inline;
  *vertical-align:auto;
}
p{
  display:-webkit-box;
  display:-moz-box;
  display:box;
}
```



<a name="layout"></a>
### 4. [layout.mcss](https://github.com/leeluolee/mass/blob/master/mass/layout.mcss)

layout处理一些常见的布局问题 , 以及栅格布局生成等功能, 跟reset一样，一般就是在页面的初始化搭建中使用. 


#### 1. $fixed-layout($widths..., $margin = 0px)

具体宽度的布局生成, 可以传入`auto` 代表这是个n栏自适应的布局


#### 2. $fixed-grid()

固定布局(基于px)的栅格系统生成


#### 3. $fluid-grid()

流式布局栅格系统生成(基于%)


#### 4. $elastic-grid()

弹性布局栅格系统生成(基于em)




<a name="effect"></a>
### 5. [effect.mcss](https://github.com/leeluolee/mass/blob/master/mass/effect.mcss)

__参数配置__ 
1. `$effect-outport` —— 是否输出内置的几种效果, 默认为不输出

__effect.mcss__ 中的所有效果都是基于以下两个函数`$effect`, `$effect-func`.
它们参数完全一致，区别是`$effect-func` 只在全局注册对应的函数，而`$effect`是直接输出

__注意__ 
@import effect 会引入几个样式


#### $effect($name, $block, $with-class)


__Arguments__

1. $name[text]         keyframes的名字以及输出的className
2. $block[func]        keyframesblock，接受代表`-o-`等前缀的参数
3. $with-class[func]—— 可选，代表输出类要做的额外样式

解决keyframes的跨浏览器生成, 并生成对应的class.

__Example__

```
$effect(flip, ($prefix){
  0% {
    #{$prefix}transform: perspective(300px) rotateY(0);
    #{$prefix}animation-timing-function: ease-out; }
  40% {
    #{$prefix}transform: perspective(300px) translateZ(100px) rotateY(170deg);
    #{$prefix}animation-timing-function: ease-out; }
  50% {
    #{$prefix}transform: perspective(300px) translateZ(100px ) rotateY(190deg) scale(1);
    #{$prefix}animation-timing-function: ease-in; }
  80% {
    #{$prefix}transform: perspective(300px) rotateY(360deg) scale(.95);
    #{$prefix}animation-timing-function: ease-in; }
  100% {
    #{$prefix}transform: perspective(300px) scale(1);
    #{$prefix}animation-timing-function: ease-in; }
},{
  $backface-visibility:  visible;
});
```

__Outport__
```

```


#### $effect-func($name, $block, $with-class)

`$effect-func` 相当于是把`$effect`的动作延迟到了函数调用时发生

<a name="functions"></a>
### 6. [functions.mcss](https://github.com/leeluolee/mass/blob/master/mass/functions.mcss)

这里只列出公有函数

#### $if( $test, $value, $value2)

如果test通过 则返回 $value, 否则返回$value2, __是的 仅仅只是用来减少@if @else的书写__ 

body{

}

#### $map($valueslist, $key)



### 7. [var.mcss](https://github.com/leeluolee/mass/blob/master/mass/var.mcss)

集中的参数控制, 所有单独的对外文件都依赖它

<a name="index"></a>
### 7. [index.mcss](https://github.com/leeluolee/mass/blob/master/mass/index.mcss)

可以调用以上所有函数



## Changelog




