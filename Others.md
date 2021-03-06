#### TCP三次握手和四次挥手

 > 建立一个连接需要三次握手。第三次握手可以携带数据，第一次、第二次不可以

 + 第一次，客户端发送报文，服务端能接收到。服务端得出结论：客户端发送能力、服务端接收能力正常。
 + 第二次，服务端发送报文，客户端能接收到。客户端得出结论：客户端接收能力、服务端发送能力正常。
 + 第三次，客户端发送报文，服务端能接收到。服务端得出结论：客户端和服务端的发送、接收能力都正常。

 > 终止一个连接需要四次挥手
 
 + 第一次，客户端发送连接释放报文，关闭TCP连接，等待服务端确认
 + 第二次，服务端发送确认报文
 + 第三次，服务端发送连接释放报文，等待客户端确认
 + 第四次，客户端发送确认报文
  
#### 重绘和回流

> 回流必将引起重绘，重绘不一定引起回流

+ 浏览器渲染机制
  - 浏览器采用流式布局模型。
  - 浏览器会把 HTML 解析成 DOM，把 CSS 解析成 CSSOM，DOM 和 CSSOM 相结合产生渲染树。
  - 根据渲染树计算所有节点在页面上的大小和位置，然后把节点绘制到页面上。
  - 由于浏览器使用流式布局，对渲染树的计算通常只需要遍历一次就可以完成。 但是 table 及其内部元素除外，
    他们可能需要多次计算，通常需要花费3倍同等元素的时间，这也是避免使用 table 布局的原因之一。
    
+ 重绘

    > 当元素样式的改变不影响它在文档流中的位置时，浏览器会将新样式赋给元素并重新绘制它，这个过程称为重绘。
    
    - 导致重绘的情况：
      * 修改 DOM
      * 修改样式
      * 用户事件（鼠标悬停、页面滚动、文本框输入文字、改变窗口大小等）
      
+ 回流

    > 当渲染树中部分或全部元素的尺寸、结构或某些属性发生改变时，浏览器重新渲染部分或全部文档的过程称为回流。
        
    - 导致回流的情况：
      * 页面首次渲染
      * 浏览器窗口大小发生改变
      * 元素尺寸或位置发生改变
      * 元素内容发生变化
      * 元素字体大小变化
      * 添加或者删除可见的 DOM 元素
      * 激活 CSS 伪类
      * 查询某些属性或调用某些方法
      
      
> 如何避免回流和重绘
      
 + CSS
   - 避免使用 table 布局
   - 尽可能在 DOM 树的末端改变 class
   - 避免设置多层内联样式
   - 避免使用 CSS 表达式（如：calc）。
   - 将动画效果应用到 position 为 absolute 和 fixed 的元素上。
   
 + JS
   - 避免频繁操作样式
   - 避免频繁操作DOM
   - 先设置 display: none 操作结束后再显示出来，不会引发回流和重绘。
   - 使具有复杂动画的元素脱离文档流，避免父元素及后续元素频繁回流。  
   
#### 性能优化       

  > 使用服务端渲染
    
     - 优点：首屏渲染快，利于SEO
     - 缺点：配置麻烦，增加服务器压力
  
  > 静态资源使用 CDN   
     
   + 内容分发网络 CDN 是一组分布在多个不同地理位置的 web 服务器。缩短服务器与用户之间的距离，从而缩短请求时间。
   + CDN 原理：
        - 1、浏览器向本地 DNS 发送请求
        - 2、本地 DNS 依次向根服务器、顶级域名服务器、权限服务器发出请求，得到全局负载均衡系统(GSLB)的 IP 地址
        - 3、本地 DNS 再向 GSLB 发出请求，GSLB 根据 DNS 的 IP 地址判断用户位置，
             然后筛选出最近的本地负载均衡系统(SLB)，并将该 SLB 的 IP 返回给本地 DNS
        - 4、本地 DNS 将 SLB 的 IP 地址发回给浏览器，浏览器向 SLB 发出请求
        - 5、SLB 根据请求的资源和地址，选出最优的缓存服务器发回给浏览器     
        - 6、浏览器重定向到缓存服务器
        - 7、若缓存服务器有浏览器需要的资源则返回，若没有，则向源服务器发送请求，得到资源发给浏览器并缓存
             
  > 减少重绘和回流
   
  > 压缩文件
   
  > 减少 HTTP 请求

  > 使用 HTTP2 
    
   + 如何使用HTTP2：nginx server 配置
     server {
        listen 443 ssl http2;
     }
    
   + HTTP2 相比 HTTP1.1 有如下几个优点：
             
   - 解析速度快
      
          服务器解析 HTTP1.1 请求时，必须不断读入字节，直到遇到分隔符 CRLF 为止。
          而 HTTP2 是基于帧的协议，每帧都有表示帧长度的字段，所以请求速度会更快。
    
   - 多路复用
       
          HTTP1.1 如果同时发起多个请求，就会建立多个 TCP 连接，
          HTTP2 多个请求可以共用一个 TCP 连接，通过流 ID 来标识，称为多路复用。 
               
   - 首部压缩
          
          客户端和服务器端使用 "首部表" 来跟踪和存储之前发送的键值对，对于相同的内容，
          不再每次请求和响应都发送。
    
   - 优先级
        
          HTTP2 可以对比较紧急对请求设置一个较高的优先级，服务器在收到这样的请求后，会优先处理。
    
   - 流量控制
    
          由于 TCP 链接的流量带宽是固定的，当有多个请求并发时，一个请求占用的流量多，其他的就会少。
          流量控制可以对不同的流量进行精准控制。
    
   - 服务器推送
             
          HTTP2 可以对一个客户端请求发送多个响应。               
             
             
#### webpack热更新HMR原理 

  + 1、调用 webpack 的 api 对文件系统 watch，发现有变更则重新打包，保存到内存中
  + 2、devServer 通过 webSocket 通知浏览器文件发生变更             
  + 3、webpack-dev-server/client 接收到服务端消息做出响应           
  + 4、webpack 接收到新的 hash 值验证并请求模块代码
  + 5、HotModuleReplacement.runtime 对模块进行热更新           
       
#### 为什么JS是单线程而不是多线程？

   JS的主要用途是与用户互动，以及操作DOM，单线程可以避免带来复杂的同步问题。
   假定JS是多线程，两个线程同时操作一个DOM节点，则会出现问题。             
   
