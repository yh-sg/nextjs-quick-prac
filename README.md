## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

# Next.js App Router Project

A modern web application built using **Next.js (App Router)**, **TypeScript**, and **Tailwind CSS**. This repository adheres to standard file conventions and modular architecture for maximum scalability.

## 🚀 Getting Started

### Prerequisites

Ensure you have **Node.js 18.17.0** or later installed.

### Installation

1. Install dependencies:
   ```bash
   pnpm install
   ```

2. Set up environment variables:
   ```bash
   cp .env.example .env
   ```
   *Open `.env` and fill in your local secrets. This part is needed for hooking up postgres url from vercel.* Use hobby selection in vercel for free. 

3. Run the development server:
   ```bash
   pnpm dev
   ```
---

## 📁 Directory Structure

This project isolates framework configuration files from the application core source using the `src/` directory.

```text
my-nextjs-app/
├── public/                 # Static assets (images, fonts, favicons)
├── src/                    # Main application source directory
│   ├── app/                # App Router (file-system based routing)
│   │   ├── layout.tsx      # Global root layout (Required html/body tags)
│   │   ├── page.tsx        # Home page route (/)
│   │   ├── error.tsx       # Error boundary fallback for the segment
│   │   ├── loading.tsx     # Loading skeleton via React Suspense
│   │   ├── not-found.tsx   # Custom 404 page for the segment
│   │   ├── global.css      # Main global styles stylesheet
│   │   ├── api/            # API Route handlers
│   │   │   └── route.ts    # Endpoint for /api
│   │   ├── (auth)/         # Route Group (organizes routes, ignored in URL)
│   │   │   ├── login/
│   │   │   │   └── page.tsx# Renders at /login
│   │   │   └── register/
│   │   │       └── page.tsx# Renders at /register
│   │   └── dashboard/      # Nested route segment
│   │       ├── [id]/       # Dynamic route segment (e.g., /dashboard/123)
│   │       │   └── page.tsx
│   │       ├── _components/# Private folder for route-specific UI
│   │       ├── layout.tsx  # Nested layout wrapping dashboard pages only
│   │       └── page.tsx    # Renders at /dashboard
│   ├── components/         # Reusable global UI elements (button, navbar)
│   ├── hooks/              # Custom global React hooks
│   ├── lib/                # Third-party SDK initializations (prisma, supabase)
│   ├── services/           # Data fetching functions and external API calls
│   └── types/              # Global TypeScript interfaces and declarations
├── .env                    # Local environment variables
├── next.config.js          # Next.js specific framework configuration
├── package.json            # Node.js project scripts and dependencies
├── tailwind.config.js      # Tailwind CSS configuration
└── tsconfig.json           # TypeScript configuration rules
```

---

## ⚙️ Core Architecture Concepts

### 1. App Router Routing Conventions
* **`layout.tsx`**: Defines shared, state-preserving UI across multiple nested sub-routes.
* **`page.tsx`**: The core component that makes a folder segment publicly accessible via a URL.
* **`loading.tsx`**: Automatically wraps the page segment in a React Suspense boundary to show a skeleton UI during data resolution.
* **`error.tsx`**: React Error Boundary capturing client or server crashes gracefully without crashing the entire app.

### 2. File Organization Rules
* **Route Groups `(name)`**: Folders wrapped in parentheses group sections (like marketing vs. app states) without modifying the public URL paths.
* **Private Folders `_name`**: Folders prefixed with an underscore completely opt out of the file-system routing system. Use this pattern to safely colocate components directly next to your routing pages.

### 3. Server vs. Client Components
* **Server Components (Default)**: All components in the `app/` folder are React Server Components by default. They fetch data securely on the server and reduce client-side JavaScript bundles.
* **Client Components**: Add the `'use use-client'` directive at the very top of a file whenever you use interactivity (e.g., `useState`, `useEffect`, or click listeners).
