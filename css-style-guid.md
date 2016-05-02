CSS编码指南

## 前言
CSS 作为网页样式的描述语言，在前端开发中有着广泛的应用。本文档的目标是使 CSS 代码风格保持一致，容易被理解和被维护。

虽然本文档是针对 CSS 设计的，但是在使用各种 CSS 的预编译器(如 less、sass、stylus 等)时，适用的部分也应尽量遵循本文档的约定。


## 核心规范
核心规范规定了洽客前端使用的css框架和基础类，主要包含两个css文件，`weui.css` 与 `style.css`。

### 基础类
style.css = 重置类reset.css + 原子类base.css + 组件类component.css;

**重置类** 包含了对基本类型标签样式的重置

**原子类** 包含了常用的工具：图像大小，百分比，文本对齐，常用行高，常用字体大小，常用边距，学用字体颜色，边框等。

**组件类** 包含了图标字体iconfont，弹框，登录等

### weui框架
见 [weui文档说明](https://github.com/weui/weui/wiki)

页面引用，先引用 `style.css` 再引入 `weui.css`


### 兼容性要求
- PC端兼容webkit内核浏览器即可
- 移动端兼容到Android4.4及以上，iOS7.0及以上版本。

### 图片使用
- 小图标：单色图标使用原则 css图标 > iconfont > gif > png
- 图片使用：优先使用jpg，PS导出质量为高，压缩比率为75%左右。


## 基本规范
基本规范规定了代码的编写风格，推荐使用下面的规范，以便以团队成员的沟通协作。

### 代码风格

#### 文件
CSS 文件使用无 `BOM` 的 `UTF-8` 编码。

解释：win系统自带的记事本新建的txt文件都是带BOM的，带BOM的叫UTF-8+，不带BOM的为UTF-8，部分语言或工具对UTF-8+格式的文档不能正确解析。

#### 缩进
属性展开写法下：以 `2` 个空格做为层级缩进

推荐采用折叠属性写法，将多个属性写在同一行，属性过多可多行书写

```
.ui-mask { 
  position: fixed; top: 0; right: 0; bottom: 0; left: 0; z-index: 1100;
  display: none; width: 100%; height: 100%; background-color: rgba(0,0,0,.6);
  opacity: 0; -webkit-transition: opacity .15s; transition: opacity .15s; 
}
```

#### 空格
- `选择器` 与 `{` 之间必须包含空格。
- `属性名` 与之后的 `:` 之间不允许包含空格， `:` 与 `属性值` 之间必须包含空格。
- `列表型属性值` 书写在单行时，`,` 后必须跟一个空格。

```
/* good */
.ui-tbl{
  display: table;
  width: 100%;
  box-sizing: border-box;
}
.avatar { font-family: Arial, sans-serif; }

/* bad */
.ui-tbl{
display: table;width: 100%;box-sizing: border-box;}
.avatar {font-family: Arial,sans-serif;}
```

#### 顺序
按功能分组书写，并以 Formatting Model（布局方式、位置） > Box Model（尺寸） > Typographic（文本相关） > Visual（视觉效果） 的顺序书写，以提高代码的可读性。

解释：

- Formatting Model 相关属性包括：position / top / right / bottom / left / float / display / overflow 等
- Box Model 相关属性包括：border / margin / padding / width / height 等
- Typographic 相关属性包括：font / line-height / text-align / word-wrap 等
- Visual 相关属性包括：background / color / transition / list-style / animation / transform 等

另外，如果包含 content 属性，应放在最前面。

```
.sidebar {
  position: absolute; top: 50px; left: 0; overflow-x: hidden;
  width: 200px; padding: 5px; border: 1px solid #ddd;
  font-size: 14px; line-height: 20px;
  background: #f5f5f5; color: #333; -webkit-transition: color 1s; -moz-transition: color 1s; transition: color 1s; 
}
```

#### 注释
	建议使用块注释 `/* ... */`，注释独占一行。
	独立的CSS模块，要添加注释说明

#### 选择器
如无必要，不得为 `id`、`class` 选择器添加类型选择器进行限定
解释：在性能和维护性上，都有一定的影响。

```
/* good */
#error,.danger-message { font-color: #c00; }

/* bad */
dialog#error, p.danger-message { font-color: #c00; }

```

- 属性选择器中的值必须用双引号包围。
- 选择器嵌套层级应少于 `4` 级
- 尽量使用class选择器
- 避免直接使用类型选择器
- 避免空的class
- 禁用通配符
- 对需要javascript操作的元素加上ID，ID尽量以驼峰命名法命名。

```
/* good */ 
div.vip-wrap
	ul.vip-list
		li.vip-item*3

.vip-item { ... }

/* bad */ 
div.vip-wrap
	ul.vip-list
		li*3

.vip-wrap .vip-list li { ... }
```

#### 属性缩写
在可以使用缩写的情况下，尽量使用属性缩写。
```
/* good */
.post {
    font: 12px/1.5 arial, sans-serif;
}

/* bad */
.post {
    font-family: arial, sans-serif;
    font-size: 12px;
    line-height: 1.5;
}
```

使用 `border / margin / padding` 等缩写时，应注意隐含值对实际数值的影响，确实需要设置多个方向的值时才使用缩写。
解释：`border / margin / padding` 等缩写会同时设置多个属性的值，容易覆盖不需要覆盖的设定。如某些方向需要继承其他声明的值，则应该分开设置。


### 命令规则
尽量使用BEM命令规则(Block-Element-Modifie)，但可以适当修改，结合组合式命名更加灵活。

模块名/业务名 - 区域名/元素名 - 状态/颜色

全局组件以 'ui-' 开头

```
 /* Msg 弹窗模块 */
.ui-msg {}
.ui-msg.alert {}
.ui-msg.prompt {}
.ui-msg.actions {}
.ui-msg-hd {}
.ui-msg-bd {}
.ui-msg-ft {}
```

#### z-index
在使用relative 或 absolute 定位时，尽量指定固定的z-index的值，值的大小为`10倍数`，小于999999;

### 值与单位
#### 数值
 当数值为 0 - 1 之间的小数时，省略整数部分的 0
```
/* good */
panel {
    opacity: .8;
}

/* bad */
panel {
    opacity: 0.8;
}
```

#### 路径
- url() 函数中的路径不加引号。
- url() 函数中的绝对路径可省去协议名。

```
body {
    background: url(//baidu.com/img/bg.png) no-repeat 0 0;
}
```

#### 长度
长度为 0 时须省略单位。 (也只有长度单位可省)

```
/* good */
body {
    padding: 0 5px;
}

/* bad */
body {
    padding: 0px 5px;
}
```

#### 颜色
颜色值可以缩写时，必须使用缩写形式。

```
/* good */
.success {
    background-color: #aca;
}

/* bad */
.success {
    background-color: #aaccaa;
}
```

颜色值不允许使用命名色值。

```
/* good */
.success {
    color: #90ee90;
}

/* bad */
.success {
    color: lightgreen;
}
```

#### 边框
在定义无边框样式时，使用 0 代替 none。

```
/* good */
.foo {
  border: 0;
}

/* bad */
.foo {
  border: none;
}
```
