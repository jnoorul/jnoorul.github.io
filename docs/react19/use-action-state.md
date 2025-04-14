---
sidebar_position: 4
---

# useActionState

`useActionState` is a Hook that allows you to update state based on the result of a action

## 🚀 Key Points

useActionState returns an array with the following values:

- The current state
- A new action that you can pass as the action prop to your form component or formAction prop to any button component within the form.
- The isPending flag that tells you whether there is a pending Transition.

## ✅ Usage Example

```tsx
import { useActionState, useState } from "react";
import { addToCart } from "./actions.js";

function AddToCartForm({ itemID, itemTitle }) {
  const [message, formAction, isPending] = useActionState(addToCart, null);
  return (
    <form action={formAction}>
      <h2>{itemTitle}</h2>
      <input type="hidden" name="itemID" value={itemID} />
      <button type="submit">Add to Cart</button>
      {isPending ? "Loading..." : message}
    </form>
  );
}

export default function App() {
  return (
    <>
      <AddToCartForm itemID="1" itemTitle="JavaScript: The Definitive Guide" />
      <AddToCartForm itemID="2" itemTitle="JavaScript: The Good Parts" />
    </>
  );
}
```

### actions.ts

```tsx
"use server";

export async function addToCart(prevState, queryData) {
  const itemID = queryData.get("itemID");
  if (itemID === "1") {
    return "Added to cart";
  } else {
    // Add a fake delay to make waiting noticeable.
    await new Promise((resolve) => {
      setTimeout(resolve, 2000);
    });
    return "Couldn't add to cart: the item is sold out.";
  }
}
```

## Demo

https://react.dev/reference/react/useActionState#display-information-after-submitting-a-form
