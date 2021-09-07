---
title: JS深度优先遍历和广度优先遍历
---

之前知识对深度优先遍历和广度优先遍历有一个浅显的了解，后来详细查询资料，做了如下整理。

### 理念

#### 1、深度优先遍历

是指自上而下的遍历。

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b7ecdca589f64da4b94c972424943a26~tplv-k3u1fbpfcp-watermark.image)

#### 2、广度优先遍历

是指逐层遍历。

![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a96d2a99ca284ee98e46ee9d3805660d~tplv-k3u1fbpfcp-watermark.image)

### 优势对比

#### 1、理念对比

深度优先不需要记住所有的节点，所以占用空间小；

而广度优先需要记录所有的节点，所以占用大。

深度优先有回溯操作(走到最底层，再从第一层开始)所以相对而言时间会长一点。

> 深度优先采用的是 堆栈 的形式, 即先进后出

> 广度优先则采用的是 队列 的形式, 即先进先出

#### 2、事例对比

深度遍历, 多采用递归实现；

广度遍历, 采用队列实现；


```
const data = [
    {
        name: 'a',
        children: [
            { name: 'b', children: [{ name: 'e' }] },
            { name: 'c', children: [{ name: 'f' }] },
            { name: 'd', children: [{ name: 'g' }] },
        ],
    },
    {
        name: 'a2',
        children: [
            { name: 'b2', children: [{ name: 'e2' }] },
            { name: 'c2', children: [{ name: 'f2' }] },
            { name: 'd2', children: [{ name: 'g2' }] },
        ],
    }
]

// 深度遍历, 多采用递归
function getName(data) {
    const result = [];
    data.forEach(item => {
        const map = data => {
            result.push(data.name);
            data.children && data.children.forEach(child => map(child));
        }
        map(item);
    })
    return result.join(',');
}

// 广度遍历, 创建一个执行队列, 当队列为空的时候则结束
function getName2(data) {
    let result = [];
    let queue = data;
    while (queue.length > 0) {
        [...queue].forEach(child => {
            queue.shift();
            result.push(child.name);
            child.children && (queue.push(...child.children));
        });
    }
    return result.join(',');
}

console.log(getName(data))
console.log(getName2(data))
```

### 应用

在Vue中多用于深度优先；

在React重多用于广度优先