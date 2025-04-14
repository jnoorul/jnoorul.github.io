---
sidebar_position: 5
---

# useOptimistic

`useOptimistic` is a React Hook that lets you optimistically update the UI.

## What is Optimistic Update

Optimistic UI updates are a technique where the UI reflects the expected result of a user action immediately, before the server confirms it. This makes the app feel faster and more responsive by assuming the operation will succeed.

## 🚀 Key Points

### Input Params

- state: the value to be returned initially and whenever no action is pending.
- updateFn(currentState, optimisticValue): a function that takes the current state and the optimistic value passed to addOptimistic and returns the resulting optimistic state.

### Output Params

- optimisticState: The resulting optimistic state.
- addOptimistic: addOptimistic is the dispatching function to call when you have an optimistic update.

## ✅ Usage Example

```tsx
import { useOptimistic, useState, useRef } from "react";
import { deliverMessage } from "./actions.js";

function Thread({ messages, sendMessage }) {
  const formRef = useRef();
  async function formAction(formData) {
    addOptimisticMessage(formData.get("message"));
    formRef.current.reset();
    await sendMessage(formData);
  }
  const [optimisticMessages, addOptimisticMessage] = useOptimistic(
    messages,
    (state, newMessage) => [
      ...state,
      {
        text: newMessage,
        sending: true,
      },
    ]
  );

  return (
    <>
      {optimisticMessages.map((message, index) => (
        <div key={index}>
          {message.text}
          {!!message.sending && <small> (Sending...)</small>}
        </div>
      ))}
      <form action={formAction} ref={formRef}>
        <input type="text" name="message" placeholder="Hello!" />
        <button type="submit">Send</button>
      </form>
    </>
  );
}

export default function App() {
  const [messages, setMessages] = useState([
    { text: "Hello there!", sending: false, key: 1 },
  ]);
  async function sendMessage(formData) {
    const sentMessage = await deliverMessage(formData.get("message"));
    setMessages((messages) => [...messages, { text: sentMessage }]);
  }
  return <Thread messages={messages} sendMessage={sendMessage} />;
}
```

## Demo

https://react.dev/reference/react/useOptimistic#optimistically-updating-with-forms
