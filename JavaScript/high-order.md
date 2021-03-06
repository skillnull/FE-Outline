#### 框架

> React/Vue 中列表组件中为什么要写 key，其作用是什么？

    key 是给每一个虚拟节点的唯一 id，依靠 key 可以更准确、更快的拿到旧虚拟节点对应的虚拟节点。
    如果不使用 key， 会使用最大限度减少动态元素并且尽可能的尝试就地修改/复用相同类型元素的算法。
    而使用 key时，它会基于 key 的变化重新排列元素顺序，并且会移除 key 不存在的元素。
   
> React/Vue 理念上的差别是什么？

    Vue 进行数据拦截/代理，它对侦测数据的变化更敏感、更精确。所以 Vue hook 只会被注册一次，直接对数据进行代理观察。
    
    React 推崇函数式，它直接进行局部刷新重新渲染，简单粗暴。React hook 底层是基于链表(Arry)实现，每次组件被 render的时候都会顺序执行所有 hooks，因为底层是链表，每个 hook 的 next 是下一个 hook，所以不能在不同 hook 中使用判断条件，因为判断条件会导致顺序不正确，从而导致报错。
    
> Vue 的优点是什么？
    
    - 轻量级框架
    - 数据双向绑定
    - 组件化
    
> React 的优点是什么？

    - 提供强大而复杂的机制，适应更多复杂情况          
    
#### SSR
    
> ssr 的优点

    - 利于SEO   
    - 白屏时间更短

> ssr 的缺点

    - 服务端压力大
    - 代码复杂度增加            
    
> 表单回退劫持

   1、监听浏览器刷新事件
        
   ```js
      // 监听刷新或关闭事件
      window.onbeforeunload = e => {
        // 使用字段进行控制
        if (!flag) {
          return 
        }
        // 阻止默认事件
        e.preventDefault()
      }
      // 取消刷新或关闭事件的监听
      window.onbeforeunload = null
   ```

   2、点击浏览器前进或回退按钮
   
   ```javascript
      window.on('popstate', ()=>{
        // TODO
      })
   ```

   3、路由守卫
   
   ```javascript
      // beforeRouterEnter 组件第一次被渲染时调用
      // beforeRouterUpdate 路由改变但组件被复用时调用
      // 导航离开组件时调用
      beforRouterLeave(to, form, next) {
        // TODO
      }
   ```