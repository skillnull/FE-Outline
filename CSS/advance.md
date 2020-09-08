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
     