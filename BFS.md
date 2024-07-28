js 树结构，广度遍历查找某个元素，非递归实现，如何在查找时，记录所有的父级 id

ChatGPT

在 JavaScript 中，对树结构进行广度优先遍历（Breadth-First Search, BFS）时，可以使用队列来帮助实现非递归的遍历方式。如果你想在查找过程中记录每个节点的所有父级 ID，可以通过在队列中存储每个节点的路径（而不仅仅是节点本身）来实现。

下面是一个示例代码，展示了如何在广度优先搜索中记录所有父级 ID：

```javascript
function bfsFindWithParents(tree, targetId) {
  // 创建一个队列，用于存储待检查的节点及其路径
  let queue = [{ node: tree, path: [] }];

  // 循环，直到队列为空
  while (queue.length > 0) {
    const { node, path } = queue.shift(); // 从队列中取出第一个元素

    // 当前节点路径中加入当前节点的 id
    const currentPath = path.concat(node.id);

    // 检查当前节点的 id 是否为目标 id
    if (node.id === targetId) {
      return { found: true, path: currentPath }; // 返回找到的结果和路径
    }

    // 将当前节点的所有子节点加入队列
    if (node.children && node.children.length > 0) {
      node.children.forEach((child) => {
        queue.push({ node: child, path: currentPath });
      });
    }
  }

  // 如果遍历完所有节点仍未找到目标，返回未找到的结果
  return { found: false, path: [] };
}

// 示例树结构
const tree = {
  id: 1,
  children: [{ id: 2, children: [{ id: 5 }, { id: 6 }] }, { id: 3, children: [{ id: 7 }] }, { id: 4 }],
};

// 测试函数
const result = bfsFindWithParents(tree, 7);
console.log(result);
```

### 代码解释：

1. **初始化队列**： 队列中存储的对象包括当前节点和到达该节点的路径（以节点 ID 数组形式表示）。
2. **处理队列中的节点**： 在每次循环中，队列的头部元素被取出。我们检查这个节点的 ID 是否是我们要找的目标 ID。如果是，就返回一个对象，包含 `found: true` 和该节点的路径。
3. **子节点入队**： 如果当前节点有子节点，那么这些子节点会被加入队列，并且它们的路径会更新为包含当前节点的 ID。
4. **结果返回**： 如果队列被清空仍未找到目标节点，函数返回 `{ found: false, path: [] }`。

这种方式非常适合在树结构中寻找节点的同时需要追踪节点的父级链。在实际应用中，这个方法可以帮助我们理解和调试树结构的处理过程，特别是在复杂的数据结构中寻找问题时。
