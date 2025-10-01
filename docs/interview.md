# 面试题目

## 1. Proxy 和 Object.defineProperty 的区别

api 这样的：
`Object.defineProperty(target, property, descriptor)`
`new Proxy(object, handler)`

- 前者初始化麻烦性能低，需要遍历对象中的每个属性，Proxy 直接作用于对象本身，而且是按需收集依赖（查询的时候）
- 前者无法劫持属性添加、删除等情况

## 2. Vue3 中依赖收集和触发更新的机制是怎样的

基于一个内部 API `effect`函数和一个 WeakMap 映射结构实现的。

收集：副作用函数访问响应式数据（`effect(render)`），触发 Proxy 的 get，get 中进行依赖收集（`track`），建立`target -> key -> effect`这样的属性依赖关系结构。

触发：响应式数据改变，触发 Proxy 的 set，set 中触发更新（`trigger`）,通过依赖树+target+key，找到 key 对应的所有副作用函数（上例中的 render），全部执行，就完成了触发更新。
