---
sidebar_position: 5
---

# useFormStatus

```useFormStatus``` gives the status of the last form submission. 

## 🚀 Key Points

- The useFormStatus Hook must be called from a component that is rendered inside a ```<form>```.
- useFormStatus will only return status information for a parent ```<form>```. It will not return status information for any ```<form>``` rendered in that same component or children components.



## ✅ Usage Example 

```tsx
import { useFormStatus } from "react-dom";
import { submitForm } from "./actions.js";

function Submit() {
  const { pending } = useFormStatus();
  return (
    <button type="submit" disabled={pending}>
      {pending ? "Submitting..." : "Submit"}
    </button>
  );
}

function Form({ action }) {
  return (
    <form action={action}>
      <Submit />
    </form>
  );
}
```










