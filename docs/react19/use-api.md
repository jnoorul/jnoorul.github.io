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

async function fetchUser() {
  const res = await fetch("https://jsonplaceholder.typicode.com/users/1");
  return res.json();
}

const userPromise = fetchUser();

function UserProfileContent() {
  const user = use(userPromise);

  return (
    <div className="p-6 max-w-md mx-auto bg-white rounded-xl shadow-md space-y-4">
      <h2 className="text-xl font-semibold text-gray-800">User Profile</h2>
      <p className="text-gray-600">Name: {user.name}</p>
      <p className="text-gray-600">Email: {user.email}</p>
    </div>
  );
}

export default function UserProfile() {
  return (
    <Suspense fallback={<p>Loading user data...</p>}>
      <UserProfileContent />
    </Suspense>
  );
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

export default function UserProfile() {
  const [user, setUser] = useState<any>(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users/1")
      .then((res) => res.json())
      .then((data) => {
        setUser(data);
        setLoading(false);
      });
  }, []);

  if (loading) {
    return (
      <div className="p-6 max-w-md mx-auto bg-white rounded-xl shadow-md space-y-4">
        <p className="text-gray-500">Loading...</p>
      </div>
    );
  }

  return (
    <div className="p-6 max-w-md mx-auto bg-white rounded-xl shadow-md space-y-4">
      <h2 className="text-xl font-semibold text-gray-800">User Profile</h2>
      <p className="text-gray-600">Name: {user.name}</p>
      <p className="text-gray-600">Email: {user.email}</p>
    </div>
  );
}
```
