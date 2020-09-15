#### CSS常见面试题

> display: none; 和 visibility: hidden; 的区别

   - 是否占据空间
     + display: none; 不占据空间
     + visibility: hidden; 占据空间

   - 是否渲染
     + display: none; 会触发reflow(回流)进行渲染
     + visibility: hidden; 只会触发repaint(重绘)，因为没有发现位置变化，不进行渲染
     
   - 是否是继承属性(株连性)
     + display不是继承属性，display:none; 元素及子元素都会消失
     + visibility是继承属性，visibility: hidden; 的子元素若使用了 visibility: visible; 则子孙元素又会显现出来

  
> visibility: collapse 在不同浏览器有什么区别？
  
  - Chrome 中 等同于 hidden
  - Firefox、Opera、IE等同于 display: none
       
> CSS3新增伪类有哪些？
    
  - p:first-of-type 匹配第一个出现的p元素，而不管其在兄弟内的位置如何
  - p:last-of-type  匹配最后一个出现的p元素，而不管其在兄弟内的位置如何
  - :only-of-type 匹配所有没有其他相同类型的元素
  - :only-child 匹配所有只有一个子元素的元素
  - :nth-child(an+b) 找到所有当前元素的兄弟元素，然后按照位置先后顺序从1开始排序，选择结果为括号中表达式(an+b)匹配到的元素集合
  - :enabled 匹配任何被启用的元素。如果一个元素能够被激活或者获取焦点，着该元素是启用的。
  - :disabled 匹配任何被禁用的元素。
  - :checked 匹配任何选中状态的radio、checkbox、option
  - ::before 创建一个伪元素，将其成为被匹配选中的元素的第一个子元素。
  - ::after 创建一个伪元素，将其成为被匹配选中的元素的最后一个子元素。
  
  注：::before和::after生成的伪元素包含在元素格式框内，因此不能引用在替换元素上，比如img、video、embed、iframe、audio、option、canvas、object、applet、br、input
  
> 为什么要初始化CSS样式？
  
  因为不同浏览器对有些标签对默认值不同，不对CSS进行初始化，往往会出现不同浏览器之间的页面显示差异。但是样式初始化会对SEO有一定影像。
  
> absolute 的 containing block(容器块: 相对父元素如何定位) 计算方式跟正常流有什么不同？  

  absolute 会先向上找到第一个 position 不为 static 或 fixed 的祖先元素；
  如果该祖先元素的display为块级元素，则容器块为该块级元素的padding box；
  如果该祖先元素的display为行内元素，则容器块为该祖先元素内所有行内元素的padding box；
  
  正常流的容器块是其最近的块级元素的content box。

> 设置元素浮动后，该元素的 display 值是多少？
  
  自动变成 display: block;
  