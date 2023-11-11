## Hooks

### `useCallback`

In JavaScript a `function(){}` or a `() => {}` always creates a new function. That means if a function is passed as a prop to a child component, every time the parent re-renders, the child will get a new function. This prevents any optimizations done in child component where the props are memoized to skip re-rendering when the props remain the same.

(One way to work around it is instead of calling a component in the parent component, use the children prop. Props are independent from each other and does not re-render when other props change.)

The `useCallBack` hook can be used to solve this by caching a function. In this way react saves the function during the first render and only creates a new function when the any dependencies of the hook are updated. Otherwise it returns the saved function.

When combined with memoization, it keeps the props same for the child component and skips re-renders properly.

Syntax:

```javascript
const function_name = useCallback(
    // function definition
  },
  [/* dependency array*/],
);
// the function_name variable will refer to the same function unless the any dependencies change
```
