# JavaScript 总结

## 问题
* 创建对象的方法有哪些？
* 保留字有哪些？
* 什么是对象直接量？
* == 与 === 的区别？
* null 和 undefined 的区别？
* JavaScript 使用的什么字符集？ 

## 解答

## 箭头函数
```js
m => console.log(m)
相当于
function(m){
    console.log(m)
}
```
## JavaScript 认知框架
从运行时、文法（词法，语法）、执行过程三个角度去剖析 JS 的知识体系。
![](/Users/lotsd/Pictures/图床/重学前端/JS.png)

## 类型
null, undefined, Boolean, String, Number, Symbol, Object
1. undefined 是变量，不是关键字，为了避免无意中被篡改，推荐使用 `void 0` 来获取 undefined 值。
2. String 用来表示文本数据。String 最大长度是 2^53 -1 ，String 操作的是字符串的 UTF16 编码。
3. 

## 知识点
* `/* */` 多行注释不可嵌套
* 声明方式
  - var , let , const
  var 是函数作用域，let 块级作用域，const 块级作用域且只读。