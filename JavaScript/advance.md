#### JavaScript常见面试题

> Object.is() 与原来的比较操作符 "==="、"==" 的区别？

   - "==" 比较时会进行隐性类型转换
   - "===" 会进行严格比较，类型不同则会返回 false 
   - Object.is() 在三等号判断的基础上特别处理了NaN、-0、0，保证-0和0不再相同
     
> JavaScript 有几种判断变量类型的方法？
 
  - typeof
  - instanceof
  - constructor
       
     ```js
        const a = []
        a.constructor() // []
        a.constructor // ƒ Array() { [native code] }
        const b = {}
        b.constructor() // {}
        b.constructor // ƒ Object() { [native code] }
        const c = "hello world"
        c.constructor() // ""
        c.constructor // ƒ String() { [native code] }
     ```