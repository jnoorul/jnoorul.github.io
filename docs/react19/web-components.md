---
sidebar_position: 12
---

# Web Components

## 🌐 What Are Web Components?

**Web Components** are a set of standardized browser APIs that allow you to create **reusable, encapsulated, custom HTML elements**, using native browser features without relying on any framework.

They are made up of four core technologies:

1. **Custom Elements** – define your own HTML elements.
2. **Shadow DOM** – encapsulate styles and markup.
3. **HTML Templates** – define markup to reuse.
4. **ES Modules** – package functionality cleanly.

---

### 🔧 Example of a Web Component

```js
// my-greeting.js
class MyGreeting extends HTMLElement {
  connectedCallback() {
    this.innerHTML = `<p>Hello from Web Component 👋</p>`;
  }
}
customElements.define("my-greeting", MyGreeting);
```

Now, you can use `<my-greeting></my-greeting>` anywhere in HTML.

---

## 🎯 Why Were Web Components Introduced?

Web Components solve key problems in frontend development:

- 🔁 **Reusability** across frameworks (React, Angular, Vue, etc.)
- 🧼 **Encapsulation** of logic and styles
- 🔀 **Interoperability** between projects or legacy stacks
- 📦 **Distribution** of UI elements as libraries (like design systems)

They are **framework-agnostic** and **natively supported by modern browsers** — no runtime or polyfill needed in evergreen environments.

---

## 📦 When Are Web Components Useful?

Use Web Components when:

- You need to share UI components across multiple frameworks
- You're building a **design system** or micro-frontend architecture
- You're integrating with **third-party widget libraries**
- You're modernizing a legacy app without rewriting everything in React

---

## ⚛️ Using Web Components in React 19

React 19 improves **Web Component interoperability**, especially around props/attributes and event handling.

---

### ✅ Rendering a Web Component in React

```jsx
import "./my-greeting.js";

export default function App() {
  return (
    <div>
      <h2>React using Web Component below:</h2>
      <my-greeting></my-greeting>
    </div>
  );
}
```

React will render `<my-greeting>` like a regular HTML tag.

---

### 🧩 Passing Properties (Attributes)

Web components use **attributes**, not props. React now better handles these:

```js
class FancyCounter extends HTMLElement {
  static observedAttributes = ["count"];
  attributeChangedCallback(name, oldVal, newVal) {
    this.innerHTML = `<button>Count is ${newVal}</button>`;
  }
}
customElements.define("fancy-counter", FancyCounter);
```

```jsx
export default function App() {
  return <fancy-counter count="5"></fancy-counter>;
}
```

---

### 🔁 Handling Events from Web Components

If a Web Component dispatches a custom event:

```js
// Inside Web Component
this.dispatchEvent(new CustomEvent("clicked", { detail: { id: 42 } }));
```

You can now capture it using `onClick`-like syntax in React 19:

```jsx
<fancy-button onClicked={(e) => console.log(e.detail.id)}></fancy-button>
```

✅ In React 19, custom event names are now **camelCase** (`onClicked`) instead of `onclicked`.

---

## ⚡ Advantages of Web Components in React

| Feature                         | Web Components |
| ------------------------------- | -------------- |
| ✅ Framework agnostic           | Yes            |
| 🧩 Reusable across apps         | Yes            |
| 🔐 Scoped styles via Shadow DOM | Yes            |
| ⚙️ Native browser feature       | Yes            |
| 📦 Ideal for design systems     | Yes            |

---

## 🧠 Summary

- **Web Components** are native custom elements that encapsulate behavior and styling.
- They are ideal for **cross-framework reuse**, **micro frontends**, and **third-party widgets**.
- **React 19** greatly improves support for:
  - Passing props as attributes
  - Listening to custom events
  - Avoiding hydration mismatches

---

## 🔗 Want to Try It?

✅ Try this in CodeSandbox or your local React 19 project by:

1. Creating a `.js` file that defines a Web Component.
2. Importing it into your React component.
3. Using it like `<my-element></my-element>`.

---
