#### JavaScript常见面试题

> Object.is() 与原来的比较操作符 "==="、"==" 的区别？

   - "==" 比较时会进行隐性类型转换
   - "===" 会进行严格比较，类型不同则会返回 false 
   - Object.is() 在三等号判断的基础上特别处理了NaN、-0、0，保证-0和0不再相同
     
> JavaScript 有几种判断变量类型的方法？
 
  - typeof
  - instanceof
  - Object.prototype.toString.call()
    
    常用于判断浏览器内置对象。
    ```javascript
        Object.prototype.toString.call('An') // "[object String]"
        Object.prototype.toString.call(1) // "[object Number]"
        Object.prototype.toString.call(Symbol(1)) // "[object Symbol]"
        Object.prototype.toString.call(null) // "[object Null]"
        Object.prototype.toString.call(undefined) // "[object Undefined]"
        Object.prototype.toString.call(function(){}) // "[object Function]"
        Object.prototype.toString.call({name: 'An'}) // "[object Object]"
    ```
    
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
     - 如果不设置回调函数，Promise 内部抛出的错误，不会反映到外部。
     - 处于 pending 状态时，无法得知是刚开始还是即将完成。 
     
> 继承与原型链
     
    每个对象都有一个私有属性（_proto_）指向他的构造函数的原型对象（prototype）。
    该原型对象也有一个自己的原型对象（_proto_），层层向上直到一个原型的对象为null。
    根据定义，null没有原型，并作为这个原型链中的最后一个环节。
    
  + 继承方式
    - 原型链继承
          
          将父类的实例作为子类的原型:
          Sub.prototype = new Super()
          // 所有涉及到原型链继承的继承方式都要修改子类构造函数指向，否则子类构造函数会指向父类
          Sub.prototype.constructor = Sub
          
          优点：父类方法可以复用
          缺点：1、父类的引用属性会被所有子类实例共享
               2、子类构建实例时不能向父类传递参数
    
    - 构造函数继承
    
          将父类构造函数的内容复制给子类构造函数。这是继承中唯一不涉及 prototype 的继承。
          Super.call(Sub)
          
          优点：1、父类的引用属性不会被共享
               2、子类构建实例时可以向父类传递参数
          缺点：父类的方法不能复用，子类实例的方法每次都是单独创建的。     
  
    - 组合继承
  
           原型式继承和构造函数继承的组合，兼具了二者的优点。      
           function Super() {
                this.name = 'exercise'
           }       
           Super.prototype.say = function() {
                console.log('hello')
           }
           function Sub() {
                // 第二次调用Super
                Super.call(this)
           }
           // 第一次调用Super
           Sub.peototype = new Super() 
           
           优点：1、父类的方法可以被复用
                2、父类的引用属性不会被共享
                3、子类构建实例时可以向父类传递参数
           缺点：父类构造函数被调用了两次，造成了性能上的浪费  
           
    - 原型式继承
  
           原型式继承的object方法本质上是对参数对象的一个浅复制。
           Object.create(person)
           优缺点同原型链继承。
           
    - 寄生式继承
  
            使用原型式继承获得一个目标对象的浅复制，然后增强这个浅复制的能力。
            优缺点：仅是一种思路，谈不上优缺点。
            
    - 寄生组合继承
       
           浅复制父类原型，修正原型的构造函数，将子类原型替换这个原型，
           从而解决组合继承调用两次父类构造函数造成的性能浪费。    
           function object(o) {
              function F(){}
              F.prototype = o
              return new F()
           }   
           function inhert(sub,super) {
              // 创建父原型的浅复制
              var prototype = object(super.prototype)
              // 修正原型的构造函数
              prototype.constructor = sub
              // 替换子类原型
              sub.prototype = prototype    
           }                         
           function Super(name) {
              this.name = name
           }
           function Sub(name) {
              Super.call(this,name)
           }
           inhert(Sub,Super)
           Sub.prototype.say = function() {
                console.log(this.name)
           }
           
    - ES6 Class extends       
    
          本质上ES6继承是ES5继承的语法糖。不同点在于ES6继承中子类的构造函数的原型链指向父类
          的构造函数，ES5中使用的是构造函数的复制，没有原型链指向。
          ES6中子类实例的构建，基于父类实例，ES5中不是。
          class A {}
          class B {}
          Object.setPrototypeOf = function(obj, proto) {
                obj.__proto__ = proto
                return obj
          }
          // B 的实例继承 A 的实例
          Object.setPrototypeOf(B.prototype, A.prototype)
          // B 继承 A 的静态属性
          Object.setPrototypeOf(B, A)
          

> 节流和防抖     

  + 函数节流（throttle）
    
    > 高频事件触发，但在n秒内只会执行一次。
    
    ```javascript
    function throttle(fn, gap = 500) {
      // 通过闭包保存一个标记
      let flag = true 
      return function() {
        if (!flag) return
        flag = false
        setTimeout(()=>{
          fn.apply(this, arguments)
          flag = true
        }, gap)
      }
    }
    
    function hello(e) {
      console.log(e.target)
    }
    
    window.addEventListener('resize', throttle(hello))
    ```                        
                            
  + 函数防抖（debounce）
    
    > 在事件被触发n秒后再执行回调，如果在这n秒内又被触发，则重新计时。  
     
    ```javascript
    function debounce(fn, gap = 500) {
      // 存放定时器
      let timeout = null
      return function() {
        clearTimeout(timeout)
        timeout = setTimeout(()=>{
          fn.apply(this, arguments)
        }, gap)        
      }
    }
    
    function hello() {
      console.log('hello')
    }
    
    const input_list = document.getElementsByTagName('input')
    input_list && input_list.length > 0 && input_list.map((item)=>{
      item.addEventListener('change', debounce(hello))
    })
    ```                                              
    
> setTimeout、Promise、Async/Await 的区别

+ setTimeout
     
     setTimeout的回调函数放到宏队列里，等到执行栈清空以后执行。
     
+ Promise
   
     Promise本身是同步的立即执行函数，当在执行器中执行 reslove 和 reject 的时候，此时是异步操作，
     会先执行 then/catch 等，当主栈完成时，才会调用 reslove/reject 方法中存放的方法。
     
+ async

     async 函数返回一个 Promise 对象，当函数执行的时候，一旦遇到 await 就会先返回，等到触发的异步操作
     完成，再执行函数体内后面的语句。可以理解为，是让出了线程，跳出了 async 函数体。
     
> 跨域     

+ 同源策略
    域名、协议、端口三者均相同，才是同源，否则为不同源。
    
+ 跨域解决方案

    - JSONP： 利用<script>等标签不受同源策略限制，来实现数据跨域传输。缺点是只支持GET请求。
    - CORS：跨域资源共享，允许服务器声明哪些源站有权访问哪些资源，允许浏览器向声明了CORS的跨域服务器，发送XMLHttpRequest请求。
    - nginx 反向代理
    - postMessage: 多窗口之间的消息传递，iframe消息传递。
    - websocket 双向通信    
    - node 转发
    
>  国际化中时间时区怎么处理，冬令时夏令时处理

    1、GMT（前世界标准时间），UTC（现世界标准时间）
    2、夏令时（DST），冬令时（标准时间）
    3、国际时间处理
    
   ```js
       function getTimesByZone () {
          // 获取本地时间
          let date = new Date()
          // 得到 1970年1月1日 到现在到秒数
          let local = date.getTime()
          // 获取本地时间与 GMT 时间的偏移差
          let offset = date.getTimezoneOffset() * 60000
          // 获取本地时区
          let localUTC = date.getTimezoneOffset() / 60
          // 得到现在的格林威治时间
          let UTCTime = localUTC > 0 ? parseInt(local - offset) : parseInt(local + offset)
          // 得到时区的绝对值
          let localTime = UTCTime + 60 * 1000 * 60 * Math.abs(localUTC)
          console.log(`${localUTC}时区的时间是：${new Date(localUTC).toLocaleString()}`)
          return localTime
       }
   ```