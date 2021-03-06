# 对象方法的重定义

## 问题描述
重定义console的log方法

要求执行以下代码
```js
console.log('Hello');
```

输出
```js
// 2020-10-12 14:01:00 Hello
```

其中时间为当前时间

## 题解

### 方案1
```js
function rewriteConsoleLog() {
    // 取得原来的
    const log = console.log
    console.log = function () {
        // log.bind(this, new Date().toLocaleString()).apply(this, arguments)
        // or
        log(new Date().toLocaleString(), ...arguments)
    }
}

rewriteConsoleLog()

console.log('Hello');
```

### 方案2
```js
function rewriteConsoleLog() {
    // 取得原来的
    const log = console.log
    Object.defineProperty(console, 'log', {
        get() {
            return function () {
                log(new Date().toLocaleString(), ...arguments)
            }
        }
    })
}
rewriteConsoleLog()

console.log('Hello');
```