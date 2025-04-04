# Props, State, and Hooks

React provides **Props, State, and Hooks** to manage data and UI updates efficiently. Understanding these concepts is essential for building interactive applications.

---

## Props (Properties)

Props are **read-only data** passed from a parent component to a child component.

- **Used for passing data** from parent to child.
- **Immutable** (cannot be changed by the child component).
- **Makes components reusable** by allowing dynamic content.

### Example: Passing Props

```jsx
function StockPrice({ symbol, price }) {
  return <p>{symbol} Price: ${price}</p>;
}


// Usage in Parent Component
<StockPrice symbol="AAPL" price={150} />
```

## State

State is **data that changes over time** within a component.

- **Managed inside a component** (not passed like props).
- **Triggers UI updates** when modified.
- **Used for interactive elements**, like form inputs, toggles, etc.

### Example: Using State

```jsx
import { useState } from 'react';

function StockTracker() {
  const [price, setPrice] = useState(null);

  const fetchPrice = async () => {
    const response = await fetch('https://api.example.com/stock');
    const data = await response.json();
    setPrice(data.price);
  };

  return (
    <div>
      <button onClick={fetchPrice}>Get Stock Price</button>
      {price && <p>Price: ${price}</p>}
    </div>
  );
}

export default StockTracker;
```

## Hooks

Hooks are **functions that let you use React features (like state) inside functional components**.

### Common Hooks:

- **`useState`** – Manages state inside a function component.  
- **`useEffect`** – Runs code in response to changes (e.g., fetching data).  
- **`useContext`** – Shares data between components without passing props manually.  

---

### Example: Using `useEffect` to Fetch Data

```jsx
import { useState, useEffect } from 'react';

function StockInfo({ symbol }) {
  const [price, setPrice] = useState(null);

  useEffect(() => {
    async function fetchPrice() {
      const response = await fetch(`https://api.example.com/stock/${symbol}`);
      const data = await response.json();
      setPrice(data.price);
    }
    fetchPrice();
  }, [symbol]); // Runs when 'symbol' changes

  return <p>{symbol} Price: ${price}</p>;
}

export default StockInfo;
```

