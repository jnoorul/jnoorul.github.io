---
sidebar_position: 2
---

# use()

`use` is a React API that lets you read the value of a resource like a Promise or context.

## 🚀 Key Points

- Can be called within loops and conditional statements (unlike hooks)
- The function that calls use must be a Component or Hook
- When called with a Promise, the use API integrates with Suspense and error boundaries.
- You can read the context with `use`
- `use` is prefered compared to `useContext` as it is more flexible

## ✅ Usage Example (Promise)

```tsx
"use client";

import { use, Suspense } from "react";
import { ErrorBoundary } from "react-error-boundary";

export function MessageContainer({ messagePromise }) {
  return (
    <ErrorBoundary fallback={<p>⚠️Something went wrong</p>}>
      <Suspense fallback={<p>⌛Downloading message...</p>}>
        <Message messagePromise={messagePromise} />
      </Suspense>
    </ErrorBoundary>
  );
}

function Message({ messagePromise }) {
  const content = use(messagePromise);
  return <p>Here is the message: {content}</p>;
}
```

## ✅ Usage Example (Theme)

```tsx
import { use } from 'react';

function Button() {
  const theme = use(ThemeContext);
  // ...
```

## ✅ Without `use`

```tsx
"use client";

import { useEffect, useState } from "react";

export function MessageContainer({ messagePromise }) {
  return <Message messagePromise={messagePromise} />;
}

function Message({ messagePromise }) {
  const [content, setContent] = useState(null);
  const [error, setError] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    let isMounted = true;
    setLoading(true);
    setError(null);
    setContent(null);

    messagePromise
      .then((result) => {
        if (isMounted) {
          setContent(result);
          setLoading(false);
        }
      })
      .catch((err) => {
        if (isMounted) {
          setError(err);
          setLoading(false);
        }
      });

    return () => {
      isMounted = false;
    };
  }, [messagePromise]);

  if (loading) return <p>⌛Downloading message...</p>;
  if (error) return <p>⚠️Something went wrong</p>;

  return <p>Here is the message: {content}</p>;
}
```

## Demo

https://react.dev/reference/react/use#displaying-an-error-to-users-with-error-boundary
