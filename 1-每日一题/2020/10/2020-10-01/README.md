# 实现instanceOf

## 问题描述
实现一个instanceOf函数

要求效果跟instanceof一样

```js
function instanceOf(a,b){
    // ...code
}

xx instanceof XX // true
instancoOf(xx,XX) // true
```
## 题解

根据原型之间的关系可得出

![](https://img.cdn.sugarat.top/mdImg/MTU4NDM2MzA5ODkyOA==584363098928)

### 迭代

```js
/**
 * 检测构造函数的原型是否在实例的原型链上
 * @param {object} a 
 * @param {Object} b 
 */
function instanceOf(a, b) {
    const prototype = b.prototype
    let __proto__ = a.__proto__
    while (1) {
        if (__proto__ === prototype) {
            return true
        }

        if (!__proto__) {
            return false
        }
        __proto__ = __proto__.__proto__
    }
}
```

### 递归
```js
/**
 * 检测构造函数的原型是否在实例的原型链上
 * @param {object} a 
 * @param {Object} b 
 */
function instanceOf(a, b) {
    return a !== null && (a.__proto__ == b.prototype || instanceOf(a.__proto__, b))
}
```

### 测试代码
```js
console.log(instanceOf([], Array));
console.log(instanceOf({}, Object));
console.log(instanceOf(/^$/, RegExp));
console.log(instanceOf(function () { }, Function));
console.log(instanceOf([], Function));
```