[TOC]

### 原生JS总结

#### 定时器与执行机制解析

浏览器执行JS的机制是基于事件循环。

JS是单线程，所以同一时间只能执行一个任务，其他任务就得排队，后续任务必须等到前一个任务结束才能开始执行。

为了避免因为某些长时间任务造成的无意义的等待，JS引入了异步的概念， **用另一个线程来管理异步任务**

同步任务直接在主线程队列中顺序执行，而异步任务会进入另一个任务队列，不会阻塞主线程。等到主线程队列空了的时候，就会去异步队列查询是否有可执行的异步任务了(异步任务通常进入异步队列之后还要等一些条件才能执行，如ajax请求、文件读写)，如果某个异步任务可以执行了便进入主线程队列。

##### JS定时器

目前有三个定时器 **setTimeout setInterval setImmediate**。

定时器也是一种异步任务，通常浏览器都有一个独立的定时器模块，定时器的延迟时间就是定时器模块来管理，如果某个定时器到了可执行状态，就会被加入主线程队列。

###### setTimeout

setTimeout(fn , x) 延迟x毫秒后执行fn

PS : 延迟时间总会大于x毫秒

如果多个定时器不及时清除(clearTimeout)，会存在干扰。要及时清除不需要的定时器。

HTML5规范规定最小延迟时间不能小于4ms。不同浏览器实现不一样，chrome可以设置1ms。IE/Edge是4ms。

setTimeout注册的函数fn会交给浏览器的定时器模块来处理， **延迟时间到了就将fn加入主线程执行队列，如果队列前面还有未执行的代码，还需要继续等** 。

PPS : setTimeout不能作为多线程使用，JS引擎是单线程的。

###### setInterval

setInterval 与 setTimeout 实现机制类似，只不过setInterval是重复执行的。

setInterval(fn , x)并不管fn的执行结果，每隔x毫秒将fn放入主线程执行队列。所以两次fn间隔时间不一定。

###### setImmediate(即时)

新式定时器(IE11/Edge支持、nodejs支持、chrome不支持)

setImmediate可以算是setTimeout(0)的替代版

在IE/Edge中，setImmediate延迟可以在1ms以内，而setTimeout有最小4ms的限制。所以setImmediate比setTimeout早执行。

###### Promise

Promise是一种很常用的异步模型。如果我们想让代码在 **下个事件循环执行** 可以选择setTimeout(0),setImmediate,Promise。

Promise延迟比setImmediate更低，更早执行。

```
function testSetImmediate() {
    const label = 'setImmediate';
    console.time(label);
 
    setImmediate(() => {
        console.timeEnd(label);
    });
}
 
function testPromise() {
    const label = 'Promise';
    console.time(label);
    new Promise((resolve, reject) => {
        resolve();
    }).then(() => {
        console.timeEnd(label);
    });
}
 
testSetImmediate();
testPromise();
```

Edge输出 ：Promise:0.33毫秒 setImmediate:1.66毫秒

尽管 setImmediate 的回调函数比 Promise 的早注册，但还是 Promise 先执行。 

###### process.nextTick

process.nextTick 是 Node.js 的 API，比 promise 更早执行。

事实上， process.nextTick 不会进入异步队列，而是在主线程队尾直接强插一个任务，虽然不会阻塞主线程，但是会阻塞异步任务的执行，如果有嵌套的 process.nextTick ，那异步任务永远没机会执行到。

使用 process.nextTick 需要明确，代码要在本次事件循环结束之前执行。

### 网络基础知识

#### http协议

### 浏览器兼容性