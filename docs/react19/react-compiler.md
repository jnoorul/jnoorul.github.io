---
sidebar_position: 8
---

# React Compiler

## What Is It?

React Compiler is a build-time optimization tool introduced in React 19. It automatically applies memoization to your components and hooks, reducing unnecessary re-renders and enhancing performance—without requiring manual use of useMemo, useCallback, or React.memo.

## Why do we need it?

**To prevent unneccessary rerenders**

![alt text](react-rendering-tree.png)

## Key Features

- **Automatic Memoization**: Analyzes your code to determine where memoization can be applied, optimizing performance.

- **Build-Time Only**: Operates during the build process, ensuring no runtime overhead.

- **ESLint Integration**: Provides an ESLint plugin to surface potential issues and guide optimizations directly in your editor.

- **Graceful Degradation**: If it encounters code that violates React's rules, it safely skips optimization for that part, continuing with the rest. 

---

## Installation

To install the compiler and its ESLint plugin:

```npm install -D babel-plugin-react-compiler@beta eslint-plugin-react-compiler@beta```


**🚫 Manual Optimization without React Compiler**

```tsx
import { useState, useCallback } from "react";

const ExpensiveChild = React.memo(({ value }: { value: number }) => {
  console.log("Child rendered");
  return <div>Value: {value}</div>;
});

export default function App() {
  const [count, setCount] = useState(0);
  const [other, setOther] = useState(0);

  const handleClick = useCallback(() => setCount((c) => c + 1), []);

  return (
    <div>
      <button onClick={handleClick}>Increment Count</button>
      <button onClick={() => setOther((o) => o + 1)}>Change Other</button>
      <ExpensiveChild value={count} />
    </div>
  );
}
```

**✅ Auto Optimization with React Compiler**

```tsx
import { useState } from 'react';

function Counter({ onIncrement }: { onIncrement: () => void }) {
  const handleClick = () => {
    onIncrement();
  };

  console.log('Counter rendered');
  return <button onClick={handleClick}>Increment</button>;
}

export default function App() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('');

  const increment = () => {
    setCount((c) => c + 1);
  };

  return (
    <div>
      <h1>Count: {count}</h1>
      <Counter onIncrement={increment} />
      <input
        value={name}
        onChange={(e) => setName(e.target.value)}
        placeholder="Type your name"
      />
    </div>
  );
}
```




