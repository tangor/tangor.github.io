# Promise

## 异步回调

`Node.js`不是用多个线程为每个请求执行工作的，而是把所有工作添加到一个事件队列中，然后有一个单独线程，来循环提取队列中的事件。事件循环线程抓取事件队列中最上面的条目，执行它，然后抓取下一个条目。当执行长期运行或有阻塞I/O的代码时，注意这里：它不会被阻塞，会继续提取下一个事件，而对于被阻塞的事件Node.js会从线程池中取出一个线程来运行这个被阻塞的代码，同时把当前事件本身和它的回调事件一同添加到事件队列。

node.js事件驱动模型，

![node](/assets/img/node-architecture.png)

### Libuv

[Libuv](http://libuv.org/) 是 Node.js 关键的一个组成部分，它为上层的 Node.js 提供了统一的 API 调用，跨平台的线程池、事件池、异步 I/O 等能力，使其不用考虑平台差距，隐藏了底层实现。

![Libuv](/assets/img/Libuv-architecture.png)

它是一个对开发者友好的工具集，包含定时器，非阻塞的网络 I/O，异步文件系统访问，子进程等功能。它封装了 Libev、Libeio 以及 IOCP，保证了跨平台的通用性。

### Blocking 和 Non-Blocking

以文件系统模块为例，这是一个同步文件：
```js
const fs = require('fs');
const data = fs.readFileSync('/file.md'); // blocks here until file is read
console.log(data);
// moreWork(); will run after console.log
```
这里是一个等效的异步例子：
```js
const fs = require('fs');
fs.readFile('/file.md', (err, data) => {
  if (err) throw err;
  console.log(data);
});
// moreWork(); will run before console.log
```


## Promise



https://nodejs.org/en/docs/guides/blocking-vs-non-blocking/
http://docs.libuv.org/en/v1.x/design.html
