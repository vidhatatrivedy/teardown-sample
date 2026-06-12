# Skill — Add Frontend Screen

Add a new dashboard page in Next.js App Router for Chef's Console.

## When to use

New route under `frontend/src/app/dashboard/`

## Steps

### 1. Create page

`frontend/src/app/dashboard/{feature}/page.tsx`

```tsx
'use client';

import { useRestaurant } from '@/contexts/restaurant-context';
import { apiClient } from '@/lib/api';

export default function FeaturePage() {
  const { currentRestaurant } = useRestaurant();
  // fetch with currentRestaurant.id
  return ( ... );
}
```

### 2. Add nav link

`frontend/src/app/dashboard/layout.tsx` — sidebar item with permission guard if needed.

### 3. API method

Add to `frontend/src/lib/api.ts` or domain split module.

### 4. Types

Add interface to `frontend/src/types/index.ts` or import from generated OpenAPI types.

### 5. Permission guard (if restricted)

```tsx
<PermissionGuard permission="view_analytics">
  ...
</PermissionGuard>
```

## States to handle

- Loading skeleton
- Empty state with CTA
- Error toast from API `detail`
- No restaurant selected — prompt to select

## Checklist

- [ ] Uses `currentRestaurant.id` for all API calls
- [ ] Does not call deprecated `/enquiries` unscoped paths
- [ ] Matches [design_system.md](../../02_BUILD_SPEC/design_system.md) tokens
- [ ] Responsive on tablet width

## Do not

- Store tokens outside auth context
- Hardcode restaurant ID
- Use inline styles for colors — use Tailwind + CSS variables
