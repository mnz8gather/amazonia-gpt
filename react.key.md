MaterialItem: `key` is not a prop. Trying to access it will result in `undefined` being returned. If you need to access the same value within the child component, you should pass it as a different prop.

ChatGPT

In React, the `key` is a special property that is used by React internally for managing the list of elements and should not be accessed as a prop within child components. If you need to use a value similar to the `key` inside a child component, you should pass it under a different prop name. For instance, if you're passing an `id` that you also use for the `key`, you should pass it as another prop, such as `id` or `itemId`, to the child component:

```jsx
{
  items.map((item) => <MaterialItem key={item.id} itemId={item.id} />);
}
```

In this example, `item.id` is passed as both `key` and `itemId`, but inside `MaterialItem`, you should use `props.itemId` to access it.

翻译

ChatGPT

在 React 中，`key`是一个特殊属性，由 React 内部用于管理元素列表，并且不应在子组件中作为属性访问。如果你需要在子组件内使用类似`key`的值，你应该以不同的属性名传递它。例如，如果你正在传递一个也用作`key`的`id`，你应该将其作为另一个属性，如`id`或`itemId`，传递给子组件：

```jsx
{
  items.map((item) => <MaterialItem key={item.id} itemId={item.id} />);
}
```

在这个例子中，`item.id`既作为`key`也作为`itemId`传递，但在`MaterialItem`内部，你应该使用`props.itemId`来访问它。
