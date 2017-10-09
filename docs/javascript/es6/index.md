

# Module

模块功能主要由两个命令构成：`export`和`import`。
- `export`命令用于规定模块的对外接口
- `import`命令用于输入其他模块提供的功能

## export

### export 变量

```javascript
// profile.js
export var firstName = 'Michael';
export var lastName = 'Jackson';
export var year = 1958;
```

```javascript
// profile.js
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;

export {firstName, lastName, year};
```
### export 函数和类

```javascript
export function multiply(x, y) {
  return x * y;
};
```

```javascript
function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```
> 上面代码使用`as`关键字，重命名了函数`v1`和`v2`的对外接口。重命名后，`v2`可以用不同的名字输出两次。

> 需要特别注意的是，`export`命令规定的是对外的接口，必须与模块内部的变量建立一一对应关系。
```javascript
// 报错
export 1;

// 报错
var m = 1;
export m;

// 报错
function f() {}
export f;
```


## import

```javascript
// main.js
import {firstName, lastName, year} from './profile';

function setName(element) {
  element.textContent = firstName + ' ' + lastName;
}
```

```javascript
import { lastName as surname } from './profile';
```

### import *

下面是一个`circle.js`文件，它输出两个方法`area`和`circumference`。

```javascript
// circle.js
export function area(radius) {
  return Math.PI * radius * radius;
}

export function circumference(radius) {
  return 2 * Math.PI * radius;
}
```

```javascript
// main.js
import * as circle from './circle';

console.log('圆面积：' + circle.area(4));
console.log('圆周长：' + circle.circumference(14));
```
## export default

## 模块的继承
