---
name: react-vite-stack
description: Use this skill when the user is working in a React+Vite project that uses Tailwind CSS, React Query, React Router, Axios, Zod, or Vitest. Applies when writing components, setting up routes, fetching data, configuring API clients, writing tests, or styling with Tailwind in a Vite-based React project.
version: 1.1.2
---

# React Vite Kitchen Sink Stack Conventions

Best practices and patterns for projects scaffolded with `react-vite-kitchen-sink`.

## Provider Hierarchy

`main.tsx` wraps the app in this order — maintain it when adding new providers:

```tsx
<StrictMode>
  <Router>
    <QueryClientProvider client={queryClient}>
      <App />
    </QueryClientProvider>
  </Router>
</StrictMode>
```

When adding providers (e.g., auth, theme), insert them between `QueryClientProvider` and `<App />`.

## Data Fetching with React Query

Use `@tanstack/react-query` for all server state:

```tsx
import { useQuery, useMutation, useQueryClient } from "@tanstack/react-query";
import { api } from "../api/client";

// Fetch
const { data, isLoading, error } = useQuery({
  queryKey: ["items"],
  queryFn: () => api.get("/items").then(res => res.data),
});

// Mutate + invalidate
const queryClient = useQueryClient();
const mutation = useMutation({
  mutationFn: (newItem: Item) => api.post("/items", newItem),
  onSuccess: () => queryClient.invalidateQueries({ queryKey: ["items"] }),
});
```

Conventions:
- Query keys are descriptive arrays: `["items"]`, `["items", id]`, `["items", { filter }]`
- Keep `queryFn` in the component or extract to a `src/api/` module — not in a custom hook unless reused 3+ times
- Use `enabled` option to conditionally fetch

## API Client

`src/api/client.ts` provides a pre-configured Axios instance:

```ts
import { api } from "../api/client";
```

- Set `VITE_BASE_API_URL` in `.env.local`
- Arrays serialize as comma-separated via `qs`
- Add interceptors (auth headers, error handling) directly to the `api` instance

## Routing

Use React Router v7 patterns:

```tsx
import { Routes, Route, Link, useParams, useNavigate } from "react-router";

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/items/:id" element={<ItemDetail />} />
    </Routes>
  );
}
```

## Validation with Zod

Use Zod for runtime validation at system boundaries:

```tsx
import { z } from "zod";

const ItemSchema = z.object({
  id: z.string().uuid(),
  name: z.string().min(1),
  price: z.number().positive(),
});

type Item = z.infer<typeof ItemSchema>;

// Validate API responses
const items = ItemSchema.array().parse(response.data);
```

## Styling with Tailwind CSS

- Use utility classes directly in JSX — avoid `@apply` unless extracting a design system component
- Tailwind is configured via the Vite plugin (`@tailwindcss/vite`), not PostCSS config
- Both `index.css` and `app.css` include Tailwind directives

## Testing with Vitest + Testing Library

```tsx
import { render, screen } from "@testing-library/react";
import userEvent from "@testing-library/user-event";
import { describe, it, expect } from "vitest";

describe("Component", () => {
  it("renders correctly", () => {
    render(<Component />);
    expect(screen.getByText("Hello")).toBeInTheDocument();
  });

  it("handles interaction", async () => {
    const user = userEvent.setup();
    render(<Component />);
    await user.click(screen.getByRole("button"));
    expect(screen.getByText("Clicked")).toBeInTheDocument();
  });
});
```

Conventions:
- Test files live next to the component: `Component.test.tsx`
- Use `screen` queries over destructured render results
- Prefer `getByRole` > `getByText` > `getByTestId`
- Use `userEvent` over `fireEvent` for realistic interaction simulation
