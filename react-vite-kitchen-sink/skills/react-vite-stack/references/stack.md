# Stack Reference

Complete list of packages installed by `react-vite-kitchen-sink`.

## Production Dependencies

| Package | Purpose |
|---------|---------|
| tailwindcss | Utility-first CSS framework |
| postcss | CSS transformation pipeline |
| autoprefixer | Vendor prefix automation |
| @tailwindcss/vite | Native Vite integration for Tailwind |
| @tanstack/react-query | Server state management, caching, background refetching |
| react-router | Core routing library |
| react-router-dom | DOM bindings for React Router |
| axios | HTTP client with interceptors and request/response transforms |
| qs | Query string serialization (arrays as comma-separated) |
| zod | Runtime schema validation with TypeScript type inference |

## Dev Dependencies

| Package | Purpose |
|---------|---------|
| vitest | Vite-native test runner (Jest-compatible API) |
| jsdom | DOM environment for tests |
| @testing-library/react | React component testing utilities |
| @testing-library/jest-dom | Custom matchers (toBeInTheDocument, etc.) |
| @testing-library/user-event | Realistic user interaction simulation |
| @types/qs | TypeScript types for qs |
| @vitejs/plugin-react | React Fast Refresh and JSX transform for Vite |

## Base Template

Built on `create-vite` with the `react-ts` template (React 18 + TypeScript).
