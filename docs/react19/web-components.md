---
sidebar_position: 12
---

# Web Components

## What are Web Components?

Web Components let you create your **own HTML tags** that work just like built-in tags (`<button>`, `<input>`, etc.), but with **custom behavior and design**.

Think of it like building a **reusable mini-component** using plain HTML, CSS, and JavaScript — no frameworks needed.

---

## Why Use Web Components?

- **Reusable**: Build once, use anywhere (React, Angular, Vue, or plain HTML).
- **Encapsulated**: CSS and behavior don’t leak or interfere with other parts of the page.
- **Standard**: Supported natively in all modern browsers.

---

## Create a Simple Web Component

Create a file called `my-message.js`:

```js
// my-message.js
class MyMessage extends HTMLElement {
  connectedCallback() {
    const msg = this.getAttribute("text") || "Hello!";
    this.innerHTML = `<p style="color: green; font-weight: bold;">📢 ${msg}</p>`;
  }
}

customElements.define("my-message", MyMessage);
```

This creates a new HTML tag: `<my-message text="Hi there!"></my-message>`

---

## ⚛️ Use It in React (React 19)

Now, let’s use it inside a React component.

### Step 1: Load the Web Component

In your React file:

```jsx
"use client";

import { useEffect } from "react";

export default function Demo() {
  useEffect(() => {
    import("./my-message.js"); // Load the custom element
  }, []);

  return (
    <div>
      <h2>Using Web Component in React</h2>
      <my-message text="Welcome to React 19!"></my-message>
    </div>
  );
}
```

That’s it! Now `<my-message>` works just like any other HTML tag — no need for `useState`, `useEffect`, etc., unless you want to pass dynamic data.

---

## Final Thoughts

- **Web Components** are great for sharing UI between projects.
- **React 19** can use them easily with JSX.
- Think of them as "HTML + JS mini-apps" you can drop into any webpage.
