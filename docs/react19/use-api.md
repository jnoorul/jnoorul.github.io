---
sidebar_position: 2
---

# use()

```use``` is a React API that lets you read the value of a resource like a Promise or context.

## 🚀 Key Points

- Can be called within loops and conditional statements (unlike hooks)
- The function that calls use must be a Component or Hook
- When called with a Promise, the use API integrates with Suspense and error boundaries.
- You can read the context with ```use```
- ```use``` is prefered compared to ```useContext``` as it is more flexible



## ✅ Usage Example (Promise)

```tsx
import {use} from 'react';

function Comments({commentsPromise}) {
  // `use` will suspend until the promise resolves.
  const comments = use(commentsPromise);
  return comments.map(comment => <p key={comment.id}>{comment}</p>);
}
```

## ✅ Usage Example (Theme)

```tsx
import { use } from 'react';

function Button() {
  const theme = use(ThemeContext);
  // ...
```






