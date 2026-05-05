# 🎟️ Event Platform

> A full-featured **Next.js 16** demo project that showcases the latest and most powerful features of the Next.js App Router — built as a real-world event management platform.

---

## 🚀 Overview

This project is a hands-on showcase of **Next.js 16** capabilities, demonstrating how its new architecture and performance primitives come together in a production-style application. Every feature implemented here is intentional — designed to illustrate what modern full-stack React development looks like with Next.js 16.

Built with **React 19**, **TypeScript**, **Tailwind CSS v4**, **MongoDB (Mongoose)**, and **Cloudinary** for media management.

---

## ✨ Next.js 16 Features Showcased

### 🔍 SEO
Metadata is handled at every level of the app — statically, dynamically, and via file-based conventions — ensuring every page is crawlable and well-described without any manual `<head>` management.

### ⚡ Turbo Cache
The project leverages Next.js's built-in Turbopack caching to dramatically speed up local development rebuilds and production builds — changes are reflected near-instantly, with only the affected modules recompiled.

### 🖥️ Server-Side Rendering (SSR)
Pages that require up-to-date data are rendered on the server at request time, giving users always-fresh content without sacrificing performance or SEO.

### 🧠 Automatic Memoization
Next.js 16's automatic memoization of `fetch` calls means that duplicate data requests within a single render tree are deduplicated without any manual caching logic. Data is fetched once and shared across the component tree automatically.

### 🗂️ File-Based Routing
The App Router's file-system routing is used extensively throughout the project, including:
- **Nested routes** — for deeply structured pages like event detail views
- **Dynamic routes** — `[id]`, `[slug]` for event and category pages
- **Route groups** — `(marketing)`, `(auth)`, etc., to organise layouts without affecting URL structure

### 🧩 Layout Deduplication — Downloaded Once
Shared UI elements like navigation and sidebars are defined in `layout.tsx` files and are only sent to the browser once. Navigating between sibling routes does not re-download or re-render parent layouts — a key App Router performance win.

### 🚨 Error Handling with `error.js`
Each route segment has its own `error.tsx` boundary. Errors are caught at the nearest boundary, allowing graceful degradation — a broken event detail page won't take down the entire app.

### 📡 Data Fetching Without `useEffect`
All data fetching happens in Server Components using `async/await` directly — no `useEffect`, no `useState`, no loading spinners on the client. Data arrives with the initial HTML payload.

### 🔄 Server Components HMR Cache
During development, the HMR (Hot Module Replacement) cache for Server Components means edits to server-rendered content are reflected instantly without full page reloads — preserving client state where possible.

### 🌊 Network Waterfall Avoided
Data dependencies are structured so that multiple fetches run in **parallel** using `Promise.all`, rather than sequentially. This eliminates the classic waterfall problem where each fetch waits for the previous one to complete.

### 🚫 Request Deduplication Avoided
Thanks to Next.js 16's built-in request deduplication, the same `fetch` call made in multiple components during a single render cycle is only executed once. No custom caching layers or context providers needed.

### 🏷️ Metadata — Static, Dynamic & File-Based

| Type | Description |
|------|-------------|
| **Static** | Hardcoded `metadata` exports for fixed pages like Home and About |
| **Dynamic** | `generateMetadata()` functions that fetch event data and return page-specific titles, descriptions, and OG images |
| **File-based** | `opengraph-image.tsx`, `twitter-image.tsx`, `favicon.ico`, and `robots.ts` placed in the `app/` directory per Next.js conventions |

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| [Next.js](https://nextjs.org) | 16.2.4 | Framework |
| [React](https://react.dev) | 19.2.4 | UI Library |
| [TypeScript](https://www.typescriptlang.org) | ^5 | Type Safety |
| [Tailwind CSS](https://tailwindcss.com) | ^4 | Styling |
| [Mongoose](https://mongoosejs.com) | ^9.6.1 | Database (MongoDB) |
| [Cloudinary](https://cloudinary.com) | ^2.10.0 | Image/Media Management |
| [shadcn/ui](https://ui.shadcn.com) | ^4.6.0 | UI Components |
| [Radix UI](https://www.radix-ui.com) | ^1.4.3 | Accessible Primitives |
| [Lucide React](https://lucide.dev) | ^1.14.0 | Icons |
| [PostHog](https://posthog.com) | ^1.372.6 | Analytics & Feature Flags |

---

## 🤖 Developer Tooling

### 🐰 CodeRabbit
This project uses [CodeRabbit](https://coderabbit.ai) for AI-powered code review. CodeRabbit automatically reviews pull requests, catches bugs, suggests improvements, and ensures code quality standards are upheld — reducing the manual burden on reviewers and catching issues earlier in the development cycle.

### 📊 PostHog
[PostHog](https://posthog.com) is integrated for product analytics, session replay, and feature flags. It tracks user behaviour across the event platform — from page views and click events to funnel analysis — all self-hostable and privacy-friendly. The `posthog-js` client is initialised in a Client Component wrapper and wired into the App Router's layout for global coverage.

---

## 📁 Project Structure

```
event-platform/
├── app/                    # App Router — all routes and layouts
│   ├── (auth)/             # Route group: auth pages
│   ├── (root)/             # Route group: main app
│   │   ├── events/
│   │   │   ├── [id]/       # Dynamic route: event detail
│   │   │   │   ├── page.tsx
│   │   │   │   └── error.tsx
│   │   │   └── page.tsx
│   │   └── layout.tsx      # Shared layout (rendered once)
│   ├── layout.tsx          # Root layout
│   ├── page.tsx            # Home page
│   ├── error.tsx           # Root error boundary
│   ├── opengraph-image.tsx # File-based OG image
│   └── robots.ts           # File-based robots.txt
├── components/             # Shared UI components
├── database/               # Mongoose models and DB connection
├── lib/                    # Utility functions and data fetchers
└── public/                 # Static assets
```

---

## 🏁 Getting Started

### Prerequisites

- Node.js 18.17 or later
- A MongoDB connection string
- A Cloudinary account
- A PostHog project key

### Installation

```bash
git clone https://github.com/Bhhgtr/Event-Platform.git
cd Event-Platform
npm install
```

### Environment Variables

Create a `.env.local` file in the root directory:

```env
MONGODB_URI=your_mongodb_connection_string
NEXT_PUBLIC_CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret
NEXT_PUBLIC_POSTHOG_KEY=your_posthog_project_api_key
NEXT_PUBLIC_POSTHOG_HOST=https://app.posthog.com
```

### Running the Development Server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Building for Production

```bash
npm run build
npm run start
```

---

## 🚢 Deployment

The recommended deployment target is [Vercel](https://vercel.com), the platform built by the creators of Next.js. It has zero-config support for all Next.js 16 features including Server Components, Route Handlers, and ISR.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/Bhhgtr/Event-Platform)

---

## 📚 Learn More

- [Next.js 16 Documentation](https://nextjs.org/docs)
- [Next.js App Router Guide](https://nextjs.org/docs/app)
- [React 19 Release Notes](https://react.dev/blog/2024/12/05/react-19)
- [PostHog Next.js Integration](https://posthog.com/docs/libraries/next-js)
- [CodeRabbit Documentation](https://docs.coderabbit.ai)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
