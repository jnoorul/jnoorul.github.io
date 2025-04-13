---
sidebar_position: 9
---

# React Server Components

## 🧠 What Are Server Components?

React Server Components (RSC) are a new type of React component that runs **only on the server**. They allow you to build dynamic, data-rich apps while sending **less JavaScript** to the browser, resulting in better performance and scalability.

Unlike traditional client-side components, Server Components are rendered on the server and streamed to the browser. The browser never sees or downloads the component’s source code.

---

## 🚀 Key Characteristics

- Run **only on the server** – never executed in the browser
- Can access **databases**, **file systems**, **secrets**, etc.
- Use **async/await** directly during rendering
- Can be **composed with Client Components**
- Are **not bundled** into client-side JavaScript
- Support **streaming** and **progressive hydration**

---

## 💡 Benefits of Server Components

1. **Smaller client bundles** – Reduce the amount of JavaScript sent to the browser.
2. **Secure data access** – Query databases, read files, and handle secrets safely.
3. **Faster initial load** – Less JS means faster time to interactivity.
4. **Simplified data fetching** – Fetch during render, no useEffect/useState needed.
5. **Improved performance** – Ideal for large-scale apps and data-heavy UIs.
6. **SEO-friendly** – Rendered HTML content is visible to search engines.

---

## 📚 Server vs Client Components

| Feature                            | Client Component        | Server Component                |
| ---------------------------------- | ----------------------- | ------------------------------- |
| Runs in browser                    | ✅ Yes                  | ❌ No                           |
| Included in JS bundle              | ✅ Yes                  | ❌ No                           |
| Can use useState/useEffect         | ✅ Yes                  | ❌ No                           |
| Can access backend logic (DB, API) | ❌ No                   | ✅ Yes                          |
| Ideal for                          | Interactivity, UI logic | Data rendering, secure fetching |

---

## 🔄 How Server Components Work (Simplified Flow)

React Server Component Flow:

- A Server Component:
  - Fetches data securely (e.g., DB, APIs)
  - Renders HTML on the server
  - Streams that HTML to the client
- A Client Component:
  - Hydrates where interactivity is required

This allows React to render a full page with data on the server, but hydrate only parts that require browser interaction.

---

## ⚙️ When to Use Server Components

**Use RSC when:**

- You need to access secure backend resources (DB/API)
- You want to reduce your JavaScript bundle size
- Your UI is non-interactive (e.g., article content, product lists)
- You’re building high-performance or SEO-sensitive pages

**Avoid RSC when:**

- You need interactivity (click handlers, forms, modals)
- You rely on browser-only APIs (window, document)
- You use hooks like `useState`, `useEffect`, `useRef`, etc.

---

## 🔀 Mixing Server and Client Components

React lets you mix both types:

Example structure:

```
<App>
  ├── <ProductList />    ← Server Component
  └── <CartButton />     ← Client Component
</App>
```

- Use **Server Components** for rendering read-only, backend-fetched UI.
- Use **Client Components** for anything interactive or stateful.
- Client components are marked explicitly using `"use client"` at the top of the file.

---

## 🧠 Mental Model Shift

Think of Server Components as **React-powered templates** that:

- Run only on the server
- Can use `async/await` directly in render
- Never get shipped to the browser
- Reduce load times by keeping JavaScript minimal

Then, interactivity is layered using lightweight Client Components where necessary.

---

## 🧾 Summary

- Server Components simplify data fetching and reduce client-side load.
- They allow secure, efficient rendering with zero runtime JS for non-interactive parts.
- Best used for read-only, performance-critical, or SEO-sensitive UI.
- Combine them with Client Components to balance performance and interactivity.

---

## 🔗 Further Reading

- GitHub Discussion: https://github.com/reactwg/server-components/discussions/5
- Official React Docs: https://react.dev/learn/server-components

---
