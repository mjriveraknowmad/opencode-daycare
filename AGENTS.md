<!-- BEGIN:nextjs-agent-rules -->

## This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->

<!-- BEGIN:nextjs-agent-feedback -->

## Report Next.js feedback

The project owner enabled `experimental.agentFeedback`, authorizing this feedback pass. When enabled, `next dev` writes this block and restores it if removed. Commit `AGENTS.md` with your work to keep the tree clean.

During the current user request, retain anonymized facts as feedback candidates for meaningful or recurring Next.js issues:

- Crashes, hangs, OOMs, or unexpected slowness
- Incorrect behavior, output, errors, or diagnostics
- Missing, unclear, or conflicting documentation
- Unexpected CLI, codemod, Skill, or upgrade behavior and non-obvious workarounds

Continue the current user request without reporting immediately. Routine debugging is not feedback. Verify changes before retaining them as feedback candidates. Never retain code, logs, paths, URLs, secrets, personal information, or project-specific data.

Retain qualifying friction even if it is later fixed or worked around; record the final outcome during the reporting pass.

Before the final response, run one reporting pass. If candidates remain, from this file's directory run `npx --no-install next internal agent-feedback-instructions` once without piping or truncating its output. Follow its output or error guidance. If a network sandbox blocks it, retry with network access; if it still returns no output, continue normally.

<!-- END:nextjs-agent-feedback -->

## MCPs
- Context 7 Usaremos este MCP para obtener documentación actualizada del framework.

## What this repo is

A Spanish-language daycare app (daycare feed, children, families, posts). It is still the `create-next-app` scaffold: only `app/layout.tsx` and `app/page.tsx` exist. The real UI target lives in `references/`:

- `references/pantallas/*.dc.html` — design mockups (`feed`, `login`, `ninos`, `perfil-nino`, `resumen-dia`, etc.). Reference only, never imported or served.
- `references/screenshots/*.png` — expected rendered output for those screens.

`instrucciones_seguidas.md` is a log of past setup prompts, not a spec.

## Stack quirks (verified against config, not docs)

- Next.js **16.4.5** App Router, React 19.3, TypeScript strict, Turbopack.
- `cacheComponents: true` + `partialPrefetching: true` in `next.config.ts`. Data fetching is dynamic by default: cache explicitly with `"use cache"` / `cacheLife` / `cacheTag`, and wrap async uncached components in `<Suspense>` with a fallback. Node runtime only — do not add a `runtime` route segment export.
- Tailwind **v4** is wired through `turbopack.rules` (`*.css` → `@tailwindcss/turbopack`) in `next.config.ts`, with `@import "tailwindcss"` in `app/globals.css`. There is **no** `postcss.config.*` or `tailwind.config.*` — don't add them; that is not how this project is configured.
- Path alias `@/*` maps to the repo root (so `@/app/...`), not to `src/`.
- `LayoutProps<"/">` and similar are global types generated into `.next/dev/types`; `next-env.d.ts` imports them and must not be edited.

## Commands

```bash
npm run dev                # next dev (writes .next/dev, regenerates AGENTS.md blocks)
npm run build              # next build
npx eslint app             # lint app code only
npx tsc --noEmit           # typecheck
npx next typegen           # regenerate route types if .next is missing (needed by tsc)
```

- **`npm run lint` currently fails** and is not a useful signal: bare `eslint` lints the whole repo, including the mockup bundle `references/pantallas/support.js` (2 errors). Use `npx eslint app` (or another explicit path) instead of changing the mockups or the shared ESLint config to silence them.
- No test runner, test script, or CI is configured. Verify behavior in the browser through the Playwright MCP (`opencode.json`); artifacts go to the gitignored `.playwright-mcp/`.

## Spec-driven workflow

`.agents/skills/spec` and `.agents/skills/spec-impl` (Fernando Herrera skills, pinned in `skills-lock.json`) are the intended flow for features:

1. `/spec <feature>` — asks questions first, then writes `specs/NN-slug.md` with `**Status:** Draft`. `specs/` does not exist yet; the next number starts at `01`.
2. A human flips the status to `Approved`; the agent must not do this.
3. `/spec-impl NN-slug` — refuses non-approved specs, creates/switches to branch `spec-NN-slug` (unless `AutoCreateBranch: false` in `specs/.spec-config.yml`), then implements plan steps one at a time, pausing for review after each.

Do not write code during `/spec`, and never commit on the user's behalf during `/spec-impl`.


## Spec Driven Development - Skills

- /spec Usaremos esta habilidad para crear las especificaciones.
- /spec-impl Usaremos esta skill para hacer las implementaciones.
- /verify-spec Usaremos este comando para verificar los criterios de aceptación de una spec.
- **Database specs**: Cualquier archivo de especificación relacionado con la base de datos debe guardarse en la carpeta `specs/database/`.

## Installed Skills

- **supabase**: Use for any Supabase-related task (database, auth, edge functions, realtime, storage, RLS, migrations, security audits). Loads comprehensive security guidelines, CLI/MCP usage, and best practices.
- **supabase-postgres-best-practices**: Use when writing, reviewing, or optimizing Postgres queries, schema designs, or database configurations. Covers query performance, connection management, security & RLS, schema design, concurrency, and advanced features.

## Reglas de código

- Usar código limpio, nombres, funciones, variables, etc. en inglés.
