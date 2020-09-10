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