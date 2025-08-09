# The Complete Next.js Guide (App Router First)

This guide takes you from zero to production with Next.js, focusing on the App Router (stable since Next.js 14). It also includes a Pages Router appendix for legacy apps. You’ll learn architecture, routing, data fetching, mutations, server actions, caching, streaming, APIs, middleware, deployment, testing, and more—with practical examples.

Who this is for:
- React devs who want to build full‑stack apps with modern SSR/SSG, server components, and great DX.
- Teams migrating from Pages Router, CRA, or other frameworks.

Prerequisites:
- Strong React fundamentals (components, hooks, suspense).
- Node.js LTS and a package manager (npm, pnpm, or yarn).
- Basic web/REST knowledge and Git.

Version note:
- This guide targets Next.js 14+ with the App Router in /app. Where behavior differs by version, notes are included.

---

## 1) Quick Start

- Create a new app:
```bash
npx create-next-app@latest my-app
# or
pnpm create next-app my-app
```

- Dev, build, start:
```bash
cd my-app
npm run dev         # start dev server (hot reload, RSC)
npm run build       # production build
npm run start       # start production server
npm run lint        # lint with next/core-web-vitals
```

- Project structure (App Router):
```
my-app/
  app/
    layout.tsx
    page.tsx
    globals.css
    (marketing)/
      page.tsx
    dashboard/
      layout.tsx
      page.tsx
      settings/
        page.tsx
      loading.tsx
      error.tsx
    api/
      hello/route.ts
  public/
    favicon.ico
  next.config.js
  package.json
  tsconfig.json
  .eslintrc.json
```

---

## 2) App Router Fundamentals

### 2.1 Server Components vs Client Components
- In /app, components are Server Components by default (rendered on server, zero client JS).
- Client Components opt in with "use client" at top of file. They can use stateful hooks, browser APIs, and event handlers.
- Prefer Server Components for data fetching and heavy logic; use Client Components for interactivity/UI state.

Example:
```tsx
// app/users/page.tsx (Server Component by default)
import { fetchUsers } from '@/lib/db';

export default async function UsersPage() {
  const users = await fetchUsers(); // runs on server; can access DB directly
  return (
    <ul>
      {users.map(u => <li key={u.id}>{u.name}</li>)}
    </ul>
  );
}
```

```tsx
// app/users/Filter.tsx (Client Component)
"use client";
import { useState } from 'react';

export default function Filter({ onChange }: { onChange: (q: string) => void }) {
  const [q, setQ] = useState('');
  return (
    <input
      value={q}
      placeholder="Filter..."
      onChange={e => { setQ(e.target.value); onChange(e.target.value); }}
    />
  );
}
```

### 2.2 File Conventions (App Router)
- app/layout.tsx: Root layout, wraps the entire app (HTML, body). Can define metadata.
- app/page.tsx: Route segment’s default page.
- app/loading.tsx: Suspense fallback for the segment (streaming/loading state).
- app/error.tsx: Error boundary for the segment.
- app/not-found.tsx: Handles not found for the segment.
- app/template.tsx: Similar to layout, but re-renders on navigation.
- app/(group)/: Route groups for organizing without affecting the URL.
- app/[param]/: Dynamic segments.
- app/[...slug]/: Catch-all.
- app/[[...slug]]/: Optional catch-all.
- app/api/**/route.ts: Route Handlers for HTTP endpoints.

### 2.3 Layouts and Pages
```tsx
// app/layout.tsx
import './globals.css';
import type { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'My App',
  description: 'A Next.js app',
};

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

```tsx
// app/page.tsx
export default function HomePage() {
  return <h1>Welcome</h1>;
}
```

### 2.4 Loading and Error UI
- loading.tsx is auto-used as Suspense fallback while children fetch data/stream.
- error.tsx is a client component boundary for errors. It receives a reset() function.

```tsx
// app/dashboard/loading.tsx
export default function Loading() {
  return <p>Loading dashboard...</p>;
}
```

```tsx
// app/dashboard/error.tsx
"use client";
export default function Error({ error, reset }: { error: Error; reset: () => void }) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <pre>{error.message}</pre>
      <button onClick={() => reset()}>Try again</button>
    </div>
  );
}
```

### 2.5 Not Found
```tsx
// app/blog/[slug]/not-found.tsx
export default function NotFound() {
  return <p>Post not found</p>;
}
```

Throw notFound() from next/navigation in a Server Component/handler to trigger it.

---

## 3) Routing

### 3.1 Basic, Nested, and Dynamic Routes
- app/about/page.tsx → /about
- app/blog/[slug]/page.tsx → /blog/my-post
- app/shop/[...slug]/page.tsx → /shop/a/b/c

```tsx
// app/blog/[slug]/page.tsx
import { notFound } from 'next/navigation';
import { getPostBySlug } from '@/lib/posts';

export default async function PostPage({ params }: { params: { slug: string } }) {
  const post = await getPostBySlug(params.slug);
  if (!post) notFound();
  return <article dangerouslySetInnerHTML={{ __html: post.html }} />;
}
```

### 3.2 Route Groups
- Organize routes without affecting URL.
```
app/
  (marketing)/home/page.tsx      -> /home
  (dashboard)/dashboard/page.tsx -> /dashboard
```

### 3.3 Parallel Routes
- Render multiple independent UI trees simultaneously with named slots.

```
app/@analytics/page.tsx
app/@feed/page.tsx
app/page.tsx // can include <Slot name="@analytics" /> with children prop
```

```tsx
// app/layout.tsx
export default function RootLayout({
  children,
  analytics,
  feed,
}: {
  children: React.ReactNode;
  analytics: React.ReactNode;
  feed: React.ReactNode;
}) {
  return (
    <html>
      <body>
        <aside>{analytics}</aside>
        <main>{children}</main>
        <aside>{feed}</aside>
      </body>
    </html>
  );
}
```

### 3.4 Intercepting Routes
- Temporarily render a different route tree in place (e.g., show a modal on top of current page).
- Use special segment prefixes:
  - (.)segment → from same level
  - (..)segment → from parent
  - (..)(..)segment → two levels up, etc.

Example: Show a photo modal over a list page without leaving the list context.

### 3.5 Navigation APIs
- Link: Prefetches on viewport by default (can disable via prefetch={false}).
- useRouter, usePathname, useSearchParams in Client Components.
- In Server Components, you can read params/searchParams from props, but navigation is client-only.

```tsx
// app/components/Nav.tsx
import Link from 'next/link';

export default function Nav() {
  return (
    <nav>
      <Link href="/">Home</Link>
      <Link href="/blog" prefetch={false}>Blog</Link>
    </nav>
  );
}
```

---

## 4) Data Fetching, Caching, and Revalidation

### 4.1 Fetch in Server Components
- fetch is enhanced on the server with caching, request deduplication, and revalidation.
- Defaults to static caching when possible; mark dynamic when needed.

```ts
// Static (default) with ISR every 60 seconds:
await fetch('https://api.example.com/posts', { next: { revalidate: 60 } });

// Dynamic (no cache):
await fetch('https://api.example.com/user', { cache: 'no-store' });

// Tag-based cache and revalidate by tag:
await fetch('https://api.example.com/posts', { next: { tags: ['posts'] } });
```

### 4.2 Route Segment Config
- export const revalidate = 60; // segment-level ISR
- export const dynamic = 'force-static' | 'force-dynamic' | 'error' | 'auto';
- export const fetchCache = 'default-cache' | 'only-cache' | 'force-cache' | 'default-no-store' | 'only-no-store' | 'force-no-store';
- export const runtime = 'nodejs' | 'edge';

```ts
// app/blog/[slug]/page.tsx
export const revalidate = 120; // re-gen every 2 minutes
```

### 4.3 Revalidate on Demand
Use in Server Actions or Route Handlers:
```ts
import { revalidatePath, revalidateTag } from 'next/cache';

// After a mutation:
revalidatePath('/blog');        // path-based
revalidateTag('posts');         // tag-based
```

### 4.4 generateStaticParams
- Pre-generate static routes for dynamic segments (SSG).

```ts
// app/blog/[slug]/page.tsx
export async function generateStaticParams() {
  const slugs = await getAllSlugs();
  return slugs.map(slug => ({ slug }));
}
```

### 4.5 Streaming with Suspense
- Combine loading.tsx with streaming data in Server Components.

```tsx
// app/dashboard/page.tsx
import { Suspense } from 'react';
import SlowWidget from './SlowWidget';

export default function Dashboard() {
  return (
    <>
      <h1>Dashboard</h1>
      <Suspense fallback={<p>Loading widget...</p>}>
        <SlowWidget />
      </Suspense>
    </>
  );
}
```

---

## 5) Server Actions (Mutations Without API Plumbing)

- Write server functions alongside UI using "use server". They run on the server and can be called from forms (progressive enhancement) or programmatically.
- Great for form submissions, DB mutations, and cache revalidation without creating API routes.

Basic form example:
```tsx
// app/todos/actions.ts
"use server";
import { createTodo } from '@/lib/db';
import { revalidatePath } from 'next/cache';

export async function addTodo(formData: FormData) {
  const title = String(formData.get('title') || '').trim();
  if (!title) throw new Error('Title is required');
  await createTodo({ title });
  revalidatePath('/todos');
}
```

```tsx
// app/todos/page.tsx (Server Component)
import { addTodo } from './actions';

export default function TodosPage() {
  return (
    <form action={addTodo}>
      <input name="title" placeholder="New todo" />
      <button type="submit">Add</button>
    </form>
  );
}
```

Status and client feedback:
```tsx
// app/todos/Form.tsx
"use client";
import { useFormStatus } from 'react-dom';

export default function SubmitButton() {
  const { pending } = useFormStatus();
  return <button disabled={pending}>{pending ? 'Saving...' : 'Save'}</button>;
}
```

Programmatic calls:
- Use server actions with useOptimistic/useTransition in Client Components for optimistic UI.

Security notes:
- Server Actions run on server; avoid trusting client data.
- Validate and sanitize input.
- Consider CSRF for non-GET if you expose them outside of progressive enhancement context.

---

## 6) Metadata, SEO, and Head

- export const metadata for static values.
- export async function generateMetadata({ params, searchParams }) for dynamic values.

```tsx
// app/blog/[slug]/page.tsx
import type { Metadata } from 'next';
import { getPostBySlug } from '@/lib/posts';

export async function generateMetadata({ params }): Promise<Metadata> {
  const post = await getPostBySlug(params.slug);
  if (!post) return { title: 'Not found' };
  return {
    title: post.title,
    description: post.excerpt,
    openGraph: { title: post.title, description: post.excerpt },
  };
}
```

---

## 7) Route Handlers (API Endpoints)

- Place in app/api/**/route.ts.
- Export HTTP methods (GET, POST, etc.).
- Access cookies and headers via next/headers.

```ts
// app/api/hello/route.ts
import { NextResponse } from 'next/server';

export async function GET() {
  return NextResponse.json({ message: 'Hello' });
}

export async function POST(req: Request) {
  const body = await req.json();
  return NextResponse.json({ ok: true, received: body });
}
```

Cookies/Headers:
```ts
import { cookies, headers } from 'next/headers';

export async function GET() {
  const cookieStore = cookies();
  const token = cookieStore.get('token')?.value;
  const h = headers();
  const ua = h.get('user-agent');
  return Response.json({ token, ua });
}
```

Edge runtime:
```ts
export const runtime = 'edge'; // opt into Edge for this route
```

---

## 8) Middleware

- File: middleware.ts at project root.
- Runs before a request; can rewrite, redirect, or add headers.
- Lightweight—use for auth gating, locale detection, A/B, etc.

```ts
// middleware.ts
import { NextResponse } from 'next/server';
import type { NextRequest } from 'next/server';

export function middleware(req: NextRequest) {
  const isLoggedIn = req.cookies.get('session')?.value;
  if (!isLoggedIn && req.nextUrl.pathname.startsWith('/dashboard')) {
    const url = new URL('/login', req.url);
    return NextResponse.redirect(url);
  }
  return NextResponse.next();
}

export const config = {
  matcher: ['/dashboard/:path*'],
};
```

---

## 9) Styling

### 9.1 Global CSS and CSS Modules
- app/globals.css for global styles (import in root layout).
- Use CSS Modules for component-scoped styles: Component.module.css

```tsx
import styles from './Card.module.css';
export function Card({ children }) {
  return <div className={styles.card}>{children}</div>;
}
```

### 9.2 Tailwind CSS
- During create-next-app, you can select Tailwind.
- Manual:
```bash
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```
- Configure content paths and import in globals.css.

### 9.3 next/font (Google & Local)
```tsx
import { Inter } from 'next/font/google';
const inter = Inter({ subsets: ['latin'] });

export default function Layout({ children }) {
  return <body className={inter.className}>{children}</body>;
}
```

### 9.4 Image Optimization
```tsx
import Image from 'next/image';

<Image
  src="/hero.jpg"
  alt="Hero"
  width={1200}
  height={600}
  priority
/>
```

- For external domains, configure next.config.js images.domains or remotePatterns.

---

## 10) Environment Variables

- .env.local for local, .env.production for prod.
- Access at build-time or runtime on server.
- For client exposure, prefix with NEXT_PUBLIC_.

Examples:
```
# .env.local
DATABASE_URL="postgres://..."
NEXT_PUBLIC_ANALYTICS_ID="abc123"
```

Use:
```ts
const dbUrl = process.env.DATABASE_URL;           // server only
const id = process.env.NEXT_PUBLIC_ANALYTICS_ID;  // client OK
```

---

## 11) next.config.js Essentials

```js
/** @type {import('next').NextConfig} */
const nextConfig = {
  reactStrictMode: true,
  images: {
    remotePatterns: [
      { protocol: 'https', hostname: 'images.example.com' },
    ],
  },
  async redirects() {
    return [{ source: '/old', destination: '/new', permanent: true }];
  },
  async rewrites() {
    return [{ source: '/blog/:slug', destination: '/api/proxy?slug=:slug' }];
  },
  async headers() {
    return [{
      source: '/(.*)',
      headers: [
        { key: 'X-Frame-Options', value: 'SAMEORIGIN' },
        { key: 'Referrer-Policy', value: 'strict-origin-when-cross-origin' },
      ],
    }];
  },
  // output: 'standalone', // good for Docker
  // experimental: { ... }, // check docs for latest flags
};
module.exports = nextConfig;
```

---

## 12) Authentication

### 12.1 Auth.js (NextAuth)
- Mature solution for OAuth, credentials, sessions, and adapters.

Quick setup:
```bash
npm install next-auth
```

```
app/api/auth/[...nextauth]/route.ts   // route handler
```

Example:
```ts
// app/api/auth/[...nextauth]/route.ts
import NextAuth from 'next-auth';
import GitHub from 'next-auth/providers/github';

const handler = NextAuth({
  providers: [GitHub({ clientId: process.env.GH_ID!, clientSecret: process.env.GH_SECRET! })],
  callbacks: {
    async session({ session, token }) {
      session.user.id = token.sub!;
      return session;
    },
  },
});
export { handler as GET, handler as POST };
```

Client usage:
```tsx
"use client";
import { signIn, signOut, useSession } from 'next-auth/react';

export function AuthButtons() {
  const { data: session } = useSession();
  return session ? (
    <button onClick={() => signOut()}>Sign out</button>
  ) : (
    <button onClick={() => signIn('github')}>Sign in</button>
  );
}
```

Protecting routes:
- Use middleware for route gating or check session in Server Components using getServerSession.

### 12.2 Custom Auth
- Use cookies/JWT in Route Handlers + Middleware.
- Store hashed passwords in DB; perform checks in Server Actions/handlers.

---

## 13) Databases and ORMs

### 13.1 Prisma + Postgres
```bash
npm install prisma @prisma/client
npx prisma init
```

schema.prisma:
```prisma
datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}
generator client {
  provider = "prisma-client-js"
}
model Post {
  id        String   @id @default(cuid())
  title     String
  content   String?
  createdAt DateTime @default(now())
}
```

Use in Server Components/Actions:
```ts
// lib/db.ts
import { PrismaClient } from '@prisma/client';
const prisma = new PrismaClient();
export const db = prisma;
```

```ts
// app/posts/actions.ts
"use server";
import { db } from '@/lib/db';
import { revalidatePath } from 'next/cache';

export async function createPost(fd: FormData) {
  const title = String(fd.get('title') || '');
  await db.post.create({ data: { title } });
  revalidatePath('/posts');
}
```

Connection pooling:
- Use a global prisma instance in dev, or Prisma’s recommended pattern for Next.js.
- For serverless/Edge, use a compatible DB provider or driver.

---

## 14) Forms and Mutations: Actions vs API

- Server Actions: simplest path for forms and UI mutations; automatic progressive enhancement.
- API Routes (Route Handlers): explicit HTTP endpoints; good for external consumers, webhooks, or non-form calls.
- RPC: You can implement server functions and call via Actions or via fetch to Route Handlers.

Validation:
- Use zod/yup to validate input server-side.
- Return structured errors and display via useFormState.

---

## 15) Performance, Bundling, and Caching

- Minimize Client Components; keep most logic/data on server for zero-JS on client.
- Use dynamic import for heavy client widgets:
```tsx
const Chart = dynamic(() => import('./Chart'), { ssr: false, loading: () => <p>Loading...</p> });
```

- Link prefetch: default prefetch on visible links; disable when necessary.
- Image optimization: next/image reduces bandwidth and improves LCP.
- Cache wisely:
  - Static by default in RSC when possible.
  - next: { revalidate } for ISR.
  - cache: 'no-store' for per-request freshness.
  - Tag content and revalidateTag on mutation.

- Avoid unnecessary cookies/headers in data fetch paths—presence of dynamic request data can force dynamic rendering.

---

## 16) Internationalization (i18n)

- App Router supports i18n via locales in next.config.js and routing.
```js
// next.config.js
module.exports = {
  i18n: {
    locales: ['en', 'fr'],
    defaultLocale: 'en',
  },
};
```

- Structure routes like app/[locale]/page.tsx and handle locale param.
- Use Middleware to rewrite to default locale on root.

---

## 17) MDX

- Use @next/mdx to add MDX pages/components.
```bash
npm install @next/mdx @mdx-js/react
```

next.config.js:
```js
const withMDX = require('@next/mdx')();
module.exports = withMDX({
  pageExtensions: ['ts', 'tsx', 'md', 'mdx'],
});
```

Use MDX in app routes (with RSC constraints—wrap client-only MDX content in "use client" islands).

---

## 18) Testing

- Unit/Component: Jest + React Testing Library.
- E2E: Playwright or Cypress.

Install:
```bash
npm install -D jest @testing-library/react @testing-library/jest-dom ts-jest
```

Example test:
```tsx
// __tests__/home.test.tsx
import { render, screen } from '@testing-library/react';
import HomePage from '@/app/page';

test('renders heading', () => {
  render(<HomePage />);
  expect(screen.getByText(/Welcome/i)).toBeInTheDocument();
});
```

Playwright:
```bash
npm init playwright@latest
npm run test:e2e
```

---

## 19) Linting and Formatting

- ESLint with next/core-web-vitals:
```json
{
  "extends": ["next/core-web-vitals"]
}
```
- Prettier for formatting:
```bash
npm install -D prettier eslint-config-prettier
```

---

## 20) Deployment

### 20.1 Vercel (Recommended)
- Zero-config for Next.js.
- Edge Functions, Image Optimization, and ISR supported out-of-the-box.

### 20.2 Self-hosted
- Build and start:
```bash
npm run build
npm run start
```
- Standalone output for Docker:
```js
// next.config.js
module.exports = { output: 'standalone' };
```
Dockerfile example:
```Dockerfile
FROM node:20-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci

FROM node:20-alpine AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

FROM node:20-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production
COPY --from=builder /app/.next/standalone ./
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next/static ./.next/static
EXPOSE 3000
CMD ["node", "server.js"]
```

---

## 21) Observability

- next build output with React Server Components info.
- Use logging in server code; integrate APM (Datadog, Sentry) by wrapping Route Handlers and Actions.
- Web Vitals reporting (custom _app in Pages Router or instrumentation in App Router via instrumentation.ts).

---

## 22) Common Recipes

### 22.1 Blog with SSG and ISR
```tsx
// app/blog/[slug]/page.tsx
export const revalidate = 300;
export async function generateStaticParams() {
  const slugs = await getAllSlugs();
  return slugs.map(slug => ({ slug }));
}
export default async function Page({ params }) {
  const post = await getPostBySlug(params.slug);
  return <article dangerouslySetInnerHTML={{ __html: post.html }} />;
}
```

### 22.2 Search with URL Params
```tsx
// app/products/page.tsx
export default async function ProductsPage({ searchParams }: { searchParams: { q?: string } }) {
  const q = searchParams.q || '';
  const products = await searchProducts(q);
  return (
    <>
      <form>
        <input name="q" defaultValue={q} />
        <button type="submit">Search</button>
      </form>
      <ul>{products.map(p => <li key={p.id}>{p.name}</li>)}</ul>
    </>
  );
}
```

### 22.3 Protect Dashboard with Middleware + getServerSession
```ts
// middleware.ts (matcher: ['/dashboard/:path*'])
// see Middleware section above

// app/dashboard/layout.tsx
import { getServerSession } from 'next-auth';
export default async function Layout({ children }) {
  const session = await getServerSession();
  return <>{children}</>;
}
```

### 22.4 File Uploads
- Use Route Handlers with formData() or a signed upload to object storage (S3, R2).
```ts
export async function POST(req: Request) {
  const form = await req.formData();
  const file = form.get('file') as File;
  // process or forward to storage
  return Response.json({ size: file.size });
}
```

---

## 23) Pages Router Appendix (Legacy)

- pages/index.tsx → /
- pages/about.tsx → /about
- pages/blog/[slug].tsx → /blog/my-post
- Data fetching:
  - getStaticProps (SSG)
  - getServerSideProps (SSR)
  - getStaticPaths (for dynamic SSG)
- API Routes: pages/api/**

Example:
```tsx
// pages/blog/[slug].tsx
export async function getStaticPaths() {
  const slugs = await getAllSlugs();
  return { paths: slugs.map(slug => ({ params: { slug } })), fallback: 'blocking' };
}
export async function getStaticProps({ params }) {
  const post = await getPostBySlug(params.slug);
  if (!post) return { notFound: true };
  return { props: { post }, revalidate: 300 };
}
export default function Page({ post }) {
  return <article dangerouslySetInnerHTML={{ __html: post.html }} />;
}
```

Migration:
- You can have both /pages and /app during incremental migration.
- Prefer building new surfaces in /app to leverage Server Components and Actions.

---

## 24) Troubleshooting and Gotchas

- Unexpected dynamic rendering: Reading cookies/headers or using request-specific APIs can force dynamic. Remove where not needed.
- Client component bloat: Move non-interactive parts to server.
- Server Actions not running: Ensure "use server" and that action is imported from a server file. Actions can only be called from forms or by reference in client via special wiring—don’t call them like regular async functions from client without proper setup.
- Edge vs Node APIs: Some Node APIs are not available on Edge. Choose runtime accordingly.
- Image domains: Configure images.domains or remotePatterns for external sources.
- Environment variables missing: .env*. Only NEXT_PUBLIC_* keys are available to client.

---

## 25) Learning Path Checklist

- Build a small app with:
  - App Router layouts/pages, loading/error/not-found
  - Server Components for data fetching
  - One Client Component with interactivity
  - A Route Handler for GET/POST
  - A form that uses a Server Action and revalidatePath
  - Image optimization and next/font
  - Deployed to Vercel

- Add:
  - Dynamic routes + generateStaticParams
  - Tag-based caching + revalidateTag
  - Middleware-based auth gating
  - Edge Route Handler (for a fast, global endpoint)
  - E2E tests with Playwright

---

## 26) Reference Links

- Next.js Docs (App Router): https://nextjs.org/docs/app
- Routing: https://nextjs.org/docs/app/building-your-application/routing
- Data Fetching & Caching: https://nextjs.org/docs/app/building-your-application/data-fetching
- Server Actions: https://nextjs.org/docs/app/building-your-application/data-fetching/server-actions-and-mutations
- Route Handlers: https://nextjs.org/docs/app/building-your-application/routing/route-handlers
- Middleware: https://nextjs.org/docs/app/building-your-application/routing/middleware
- Metadata/SEO: https://nextjs.org/docs/app/building-your-application/optimizing/metadata
- Images: https://nextjs.org/docs/app/building-your-application/optimizing/images
- Fonts: https://nextjs.org/docs/app/building-your-application/optimizing/fonts
- Auth.js: https://authjs.dev/
- Prisma: https://www.prisma.io/docs/
- Vercel Deployment: https://vercel.com/docs/frameworks/nextjs

---

You now have a full mental model and practical toolkit for building production Next.js apps with the App Router. If you want, I can scaffold a sample repo demonstrating these patterns (actions, ISR, middleware, Edge, Prisma) tailored to your stack.
