# Career Advisor Platform

Career Advisor is a Next.js application for career exploration, quizzes, college discovery, and personalized learning roadmaps. It uses Next.js 14, React 18, TypeScript, Prisma, Supabase integrations, and Playwright.

## Requirements

- Node.js 20 or newer
- npm
- Optional: a Supabase project and AI/payment/map provider credentials for the corresponding integrations

## Local development

```powershell
npm install
Copy-Item .env.example .env.local
npm run db:generate
npm run db:push
npm run db:seed
npm run dev
```

Open <http://localhost:3000>. Local development is configured for SQLite and seeded demo data. Do not expose the demo account or local database to the public internet.

## Interactive prototype demo

Open <http://localhost:3000/demo> to demonstrate the main student journey without signing in or configuring external providers. The demo includes an editable sample profile, a short career assessment, college search and comparison, a progress-tracked learning roadmap, career exploration, learning resources, sample job/resume tools, and an illustrative career coach. Changes are saved in the current browser only; use **Reset sample data** to restore the starting profile. Sample recommendations, college details, fees, and job listings are illustrative and are not live or authoritative. Optionally configure a rotated Azure OpenAI API key and a private demo access code for live AI features; see [PROTOTYPE_DEMO_GUIDE.md](./PROTOTYPE_DEMO_GUIDE.md).

The homepage quiz button and the **Interactive Demo** navigation item open this workspace. Real authentication, database-backed persistence, AI-provider responses, maps, and payment processing remain separate integrations; read [PROTOTYPE_DEMO_GUIDE.md](./PROTOTYPE_DEMO_GUIDE.md) before presenting the project or configuring a deployment.

## Environment variables

Copy `.env.example` to `.env.local` and replace the local JWT secret with a unique random value. Keep real credentials in local environment files or your deployment provider's secret manager. Never add credentials to source files, documentation, issue reports, or logs.

Supabase, AI, map, and payment settings are optional for local development. Features that depend on an integration require that provider's credentials and configuration. Do not put service-role, payment-secret, or AI-provider keys in `NEXT_PUBLIC_*` variables.

## Validation

```powershell
npm run check:env
npx tsc --noEmit
npm run build
npm run test:simple
```

Playwright may require browser installation on a new machine: `npx playwright install chromium`.

## Deployment status

The repository contains both SQLite/Prisma and Supabase-backed code paths. Before deploying for real users, choose and validate one persistent production database/authentication configuration, apply its schema and access policies, configure rate limiting and monitoring, rotate any credentials that have ever appeared in repository files, and test the deployed signup, sign-in, persistence, and payment/webhook flows. The local SQLite database is not suitable as persistent storage on serverless hosting.

See [DEPLOYMENT_GUIDE.md](./DEPLOYMENT_GUIDE.md) for prerequisites and [SUPABASE_SETUP_GUIDE.md](./SUPABASE_SETUP_GUIDE.md) for Supabase configuration. Other implementation and migration reports are historical notes; verify their instructions against the current code before using them.

For a temporary Vercel presentation that exposes only the browser-based demo and blocks the backend APIs, follow [PROTOTYPE_DEMO_GUIDE.md](./PROTOTYPE_DEMO_GUIDE.md). This is not a production deployment configuration.

## Project structure

- `app/` — App Router pages and API routes
- `components/` — reusable UI and visualization components
- `contexts/` — client-side auth, chat, and language state
- `lib/` — auth, data, AI, payment, and integration helpers
- `prisma/` — local SQLite Prisma schema
- `tests/` — Playwright end-to-end tests
- `docs/` — integration setup documentation
