# 虚拟dom


dom操作消耗性能


演变 => 如何有效的操作dom

vdom存在复杂度，无法减少计算，所以把计算转移到js计算(JS计算速度快)
vdom
> 用js模拟dom结构
``` javascript
// 通过对象模拟

```

snabbdom 
> vdom的库，可以做示例

## diff算法
> 对比差异，获取最小更新

时间复杂度 o(n**3)
1. 遍历tree1 
2. 遍历tree2
3. 排序

演变 => o (n)
规则
1. 只比较同级，不跨级比较
2. 若tag 不相同，则删除重建
3. 若tag和key相同，则认为是相同节点，不再深度比较
jiff库：二个对象的diff