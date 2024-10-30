如何让一个 react 组件 props 变化的是否，都重新挂载

ChatGPT

要让 React 组件在 props 变化时重新挂载，可以使用一个 key prop。通过改变 key 的值，React 会卸载当前组件并重新挂载一个新的实例。这是一个有效的方法来强制组件在接收新的 props 时重置其内部状态。以下是一个示例：

```jsx
function MyComponent({ someProp }) {
  return <div>{/* 组件内容 */}</div>;
}

function ParentComponent() {
  const [value, setValue] = useState('initial');

  // 改变 key 值以重新挂载 MyComponent
  return <MyComponent key={value} someProp={value} />;
}
```

在这个示例中，每当你改变 `value` 的值时，`MyComponent` 的 key 也会改变，导致组件重新挂载。这种方法通常用于处理那些难以通过内部状态或生命周期方法重置的复杂组件。
