---
sidebar_position: 2
---

# React Compiler

## 🚀 What Is It?

The **React Compiler** (codename: **React Forget**) is a **new ahead-of-time (AOT) compiler** introduced in React 19. It analyzes your code and **automatically optimizes** component rendering by skipping unnecessary re-renders — **without requiring manual use of `useMemo`, `useCallback`, or `memo`**.

Think of it as “reactivity with no ceremony.”

---

## 🎯 Goals

- **Zero-cost reactivity**: Eliminate manual memoization boilerplate.
- **Performance by default**: Scale well across deeply nested trees and high-frequency updates.
- **Ergonomic**: Preserve idiomatic, declarative React code.
- **Predictable**: Be sound and conservative — never skip renders unless it’s clearly safe.

---

## ⚙️ How It Works

- Performs **static analysis** on components to understand data flow and side effects.
- Builds a **reactivity graph** of variables and functions.
- Automatically memoizes values and functions that don’t depend on changed data.
- Skips component re-renders when input values remain stable.
- All transformations happen at **build time**, not at runtime.

---

## ✅ Benefits

| Without Compiler                     | With React Compiler             |
|-------------------------------------|---------------------------------|
| Manual use of `useCallback`, `useMemo` | Eliminated in most cases         |
| Tedious dependency arrays           | No longer needed                |
| Prone to stale closures & bugs      | Handled automatically           |
| Verbose & error-prone code          | Clean, readable code            |
| Dev responsible for optimization    | Compiler does the heavy lifting |

---

## 📌 Key Takeaways

- Lets you **write simple React**, while still getting **performance like hand-tuned apps**.
- React behaves more like “reactive programming” — but fully within the React paradigm.
- Still experimental, but expected to become **core to React's future performance story**.

## Example

---

**🚫 React 18 (Manual Optimization)**

```tsx
// App.tsx (React 18-style)
import { useState, useCallback } from 'react';

function Counter({ onIncrement }: { onIncrement: () => void }) {
  const handleClick = useCallback(() => {
    onIncrement();
  }, [onIncrement]);

  console.log('Counter rendered');
  return <button onClick={handleClick}>Increment</button>;
}

export default function App() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState('');

  const increment = useCallback(() => {
    setCount((c) => c + 1);
  }, []);

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

**✅ React 19 with Compiler (No Manual Memoization)**

```
// App.tsx (React 19 with Compiler)
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




