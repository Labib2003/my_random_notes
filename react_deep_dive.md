## Hooks

### `useCallback`

In JavaScript a `function(){}` or a `() => {}` always creates a new function. That means if a function is passed as a prop to a child component, every time the parent re-renders, the child will get a new function. This prevents any optimizations done in child component where the props are memoized to skip re-rendering when the props remain the same.

(One way to work around it is instead of calling a component in the parent component, use the children prop. Props are independent from each other and does not re-render when other props change.)

The `useCallBack` hook can be used to solve this by caching a function. In this way react saves the address of the function during the first render and only updates the address when the any dependencies of the hook are updated. Otherwise it uses the saved function.

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

### `useMemo`

Similar to useCallback, except it caches the return value of the function provided whenever the dependencies change.

It can be used to cache expensive calculations.

Syntax:

```javascript
const cachedValue = useMemo(calculateValue, dependencies);
```

### `useReducer`

Managest state in a redux like pattern.

Syntax:

```javascript
function reducer(state, action) {
  // actions can have two properties, type and payload
  switch (action.type) {
    case "case1":
      return {
        //modified part
        ...state,
      };
    case "case2":
      return {
        //modified part
        someProp: action.payload,
        ...state,
      };
    default:
      return state;
  }
}

const [state, dispatch] = useReducer(reducer, initialState);
```

If the initial value is calculated by some function, useReducer can take an optional 3rd argument, an initializer function.

Syntax:

```javascript
const [state, dispatch] = useReducer(reducer, arg, initializer);
// here the second argument is the argument for the initializer. If the initializer does not required any arguments, this can be set to null.
```

### `useDebugValue`

A way to add labels to custom hooks so that their state can be seen in the devtools without expanding the hook.

### `useId`

Generates unique id. Should be used when ids are used in a component to make sure the html ids remain unique even if that component is rendered multiple times.

### `useLayoutEffect`

Similar to useEffect, except it runs after react finishes the calculations for the new ui and the browser rendering the ui.
