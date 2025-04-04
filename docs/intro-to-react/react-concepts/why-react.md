---
sidebar_position: 1
---

# Why React?

## The Problem: Imperative UI Updates

Before React, web applications were built using **imperative programming**, where developers manually manipulated the **DOM** to update the UI. This led to:

- **Complex code**: Developers had to track changes and update elements manually.
- **Performance issues**: Frequent DOM updates were slow and inefficient.
- **State management difficulties**: Keeping UI in sync with data was challenging.

Example of imperative UI updates:

```js
const button = document.getElementById("fetchPrice");
button.addEventListener("click", async () => {
  const response = await fetch("https://api.example.com/stock");
  const data = await response.json();
  document.getElementById("price").innerText = `Price: $${data.price}`;
});
```

In this approach, the developer manually selects elements and updates them, making the code harder to maintain as the application grows.

# The Solution: React and Declarative UI

React, created by **Facebook in 2013**, introduced a **declarative programming** approach, solving the challenges of UI updates by:

- **Using a Virtual DOM**: React updates only the necessary parts of the UI efficiently.
- **Encapsulating UI into Components**: Code is structured into reusable components.
- **State-driven UI updates**: The UI automatically updates when data changes.

## Example Using React

```jsx
import { useState } from "react";

function StockSearch() {
  const [price, setPrice] = useState(null);

  const fetchPrice = async () => {
    const response = await fetch("https://api.example.com/stock");
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

export default StockSearch;
```

## In this example:

- **The UI is declarative**: The component describes how the UI should look based on state (`price`).
- **React automatically updates the DOM** when state changes, without manual DOM manipulation.

---

# Why React?

✅ **Simpler code**: Focus on what the UI should look like, rather than how to update it.  
✅ **Better performance**: React updates only necessary parts of the UI using the Virtual DOM.  
✅ **Scalability**: The component-based architecture makes it easier to build and maintain large applications.

React simplifies frontend development, making it a preferred choice for modern web applications.
