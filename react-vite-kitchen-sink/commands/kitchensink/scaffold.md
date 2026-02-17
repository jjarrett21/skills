---
description: Scaffold a new React+Vite project with the kitchen sink stack (Tailwind, React Query, Router, Vitest, Axios)
argument-hint: [project-name]
allowed-tools: [Bash, Read, Write, Edit, Glob]
---

# Scaffold React Vite Kitchen Sink Project

The user wants to create a new React project using the kitchen sink stack.

## Arguments

Project name (optional): $ARGUMENTS

If no project name was provided, ask the user for one.

## Instructions

Run the following command to scaffold the project:

```bash
npx react-vite-kitchen-sink
```

When prompted:
1. Enter the project name (use the argument if provided)
2. Enter any additional packages the user has requested

After scaffolding completes, confirm the project was created and remind the user:

```bash
cd <project-name>
npm run dev
```

## What Gets Installed

**Production dependencies:**
- tailwindcss, postcss, autoprefixer, @tailwindcss/vite
- @tanstack/react-query
- react-router, react-router-dom
- axios, qs
- zod

**Dev dependencies:**
- vitest, jsdom
- @testing-library/react, @testing-library/jest-dom, @testing-library/user-event
- @types/qs, @vitejs/plugin-react

## Generated Structure

```
<project>/
├── src/
│   ├── api/client.ts          # Axios with VITE_BASE_API_URL
│   ├── main.tsx               # StrictMode > BrowserRouter > QueryClientProvider > App
│   ├── index.css              # Tailwind directives
│   └── app.css                # Tailwind directives
├── vite.config.ts             # react() + tailwindcss() plugins
└── package.json
```

## Post-Scaffold Guidance

If the user asks for help after scaffolding, guide them on:
- **Routing:** Add routes in App.tsx using `<Routes>` and `<Route>` from react-router
- **Data fetching:** Use `useQuery` / `useMutation` from @tanstack/react-query
- **API calls:** Import `api` from `src/api/client.ts` — set `VITE_BASE_API_URL` in `.env.local`
- **Testing:** Create `*.test.tsx` files, run with `npm run test`
- **Validation:** Use Zod schemas for form and API response validation
