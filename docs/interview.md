# 面试题目

## 1. Proxy 和 Object.defineProperty 的区别

api 这样的：
`Object.defineProperty(target, property, descriptor)`
`new Proxy(object, handler)`

- 前者初始化麻烦性能低，需要遍历对象中的每个属性，Proxy 直接作用于对象本身，而且是按需收集依赖（查询的时候）
- 前者无法劫持属性添加、删除等情况
