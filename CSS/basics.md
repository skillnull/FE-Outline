#### CSS简介
```markdown
> 什么是CSS？

层叠样式表(Cascading Style Sheets)是一种用来表现HTML或XML等文件样式的计算机语言。
```

```markdown
> CSS有什么特点？

1、丰富的样式定义
2、易于使用和修改
   可以将所有的样式声明统一存放，进行统一管理。
3、多页面引用
   可以在多个页面中使用同一个CSS样式表。
4、层叠
   层叠就是对一个元素多次设置同一个样式，这将使用最后一次设置的属性值。
5、页面压缩
   将样式的声明单独放到CSS样式表中，可以大大的减小页面的体积。
```

#### CSS选择器
```markdown
> 什么是CSS选择器？

CSS 选择器规定了 CSS 规则会被应用到哪些元素上。

备注：暂时没有能够选择 父元素、父元素的同级元素，或 父元素的同级元素的子元素 的选择器或者组合器。
```

```markdown
> CSS选择器权重：
    
10000 !important 
⇓ 
1000 行内样式 (style) 
⇓ 
100 ID (#id ) 
⇓ 
10 类(.class) | 属性([type="text"]) | 伪类(:hover)
⇓ 
1 标签(div) | 伪元素(::before)
⇓
0 通配选择符(*)、关系选择符(+, >, ~, ' ', ||)、否定伪类(:not())

```

```markdown
> 浏览器是如何解析CSS选择器的？

CSS选择器的读取顺序是从右向左。
从右向左读取，会在一开始就过滤掉大量不符合条件的节点，从而提升性能。
```

#### CSS盒子模型
```markdown
> 什么是CSS盒子模型？

CSS盒模型本质上是一个封装周围的HTML元素的盒子，
包括外边距(Margin)、边框(Border)、内边距(Padding)和内容(Content)。
```

```markdown
> 什么是标准盒模型和IE盒模型？

 W3C标准盒模型：盒子的大小为盒子的内容content大小。
 IE盒模型：盒子的大小为盒子的内容content，加上内边距和边框的大小，即 width = content + padding + border。

使用<!DOCTYPE html>来声明使用标准盒模型，
或者使用 box-sizing: content-box 选择标准盒模型
使用 box-sizing: border-box 选择IE盒模型
```

```markdown
> 什么是BFC？

BFC(Block Formatting Context)块级格式化上下文，是一种边距重叠解决方案。
在整个文档流里，触发了BFC特性的元素，就像系统里的虚拟机一样。虚拟机里的东西，相对于承载虚拟机的系统来说，
是完全隔离开的。

> 如何触发BFC？

1、根元素（<html>）
2、浮动元素（元素的 float 不是 none）
3、overflow 值不为 visible 的块元素
4、绝对定位元素（元素的 position 为 absolute 或 fixed）
5、contain 值为 layout、content 或 paint 的元素
6、display 值为 grid、inline-grid、flow-root、flex、inline-flex、inline-block、table、table-cell、table-caption 的元素
7、多列容器（元素的 column-count 或 column-width 不为 auto，包括 column-count 为 1）
8、column-span 为 all 的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中

> BFC解决了什么问题？

1.避免外边距折叠
2.清除浮动
3.阻止普通文档流元素被浮动元素覆盖
4.自适应两栏布局
```
