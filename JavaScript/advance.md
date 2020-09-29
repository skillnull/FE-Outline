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
    
> Promise
    
   + 特点
      
      - 对象的状态不受外界影响。  
           
            Promise 对象代表一个异步操作，
            有三种状态：pending（进行中）、fulfilled（已成功）、rejected（已失败）。
            只有异步操作的结果，可以决定当前是哪一种状态。
    
      - 一旦状态改变，就不会再变，任何时候都可以得到这个结果。
      
            Promise 的状态改变，只有两种可能：从 pending 到 fulfilled 和从 pending 到 rejected。
            这两种状态一旦发生，就会一直保持这个结果不再改变，这个时候称为 resolved（已定型）。
            
                        pending
                           |
                          / \
                        /     \
                   fulfilled  rejected
                        \     /
                          \ /
                           |
                        resolved
   
   + 缺点
   
     - Promise 一旦创建就会立即执行，无法中途取消。
     - 如果不设置会回调函数，Promise 内部抛出的错误，不会反映到外部。
     - 处于 pending 状态时，无法得知是刚开始还是即将完成。 
     
> 继承与原型链
     
    每个对象都有一个私有属性（_proto_）指向他的构造函数的原型对象（prototype）。
    该原型对象也有一个自己的原型对象（_proto_），层层向上直到一个原型的对象为null。
    根据定义，null没有原型，并作为这个原型链中的最后一个环节。