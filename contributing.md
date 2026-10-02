## General

- ALWAYS keep local development fast; NEVER increase startup or change-reflection time.
- ALWAYS use ESM first and TypeScript first; obey current `biome` configuration.
- ALWAYS keep code simple, readable without comments, descriptive, non-repetitive, and scoped to present problem.
- NEVER future-proof, use Chinese boxes, add unneeded problems/features/abstractions, over-complicate, over-engineer, or comment unless clarity requires it.
- NEVER use optional chaining to silence access on possibly falsy object.
- ALWAYS use `async`/`await` and `try/catch`; NEVER use promises, promise chaining, or callbacks. IF callback required THEN wrap with `node:util` `promisify`.
- ALWAYS assign returned value to dedicated local variable/constant before returning; NEVER directly return inline/function call.
- ALWAYS leave 1 blank line between class methods, route definitions, before `if`/`for`/`try/except`, and before block explanatory comments.

## TypeScript

- ALWAYS use `import`/`export`; NEVER use `require`/`module.exports`.
- ALWAYS prefer `type` over `interface`; use Zod inference for cross-layer types and dedicated types for layer-internal use.
- ALWAYS prefer arrow functions, named exports, pure single-purpose functions, and readable non-overcomplicated types.
- IF class THEN maintain internal state only. IF default export THEN app entrypoint, singleton, or DB connection only. IF function exceeds ~40 lines THEN consider splitting.
- ALWAYS use object-destructured named parameters. IF input/multiple-value/complex-object return THEN define named input/return types. IF simple single-primitive return THEN NEVER define named types.
- `services/types`: define every entity/database schema and controller request/response payload.

## Entities

- Tables: plural names. Types: singular names.
- Entity types: `UserRow` raw `select`; `UserRowInsert` allowed/required raw `insert`; `UserRowUpdate` allowed raw `update`; `User` joined/computed entity; `UserFormValues` raw browser input for new-row form.
- Entity type shape: `export type UserRow = {}`; `export type UserRowInsert = Partial<UserRow> & NonNullable<Pick<UserRow, 'email' | 'password'>>`; `export type UserRowUpdate = Partial<UserRow>`; `export type User = Omit<UserRow, 'role'> & { foe: Foe[] }`; `export type UserFormValues = Omit<UserRow, 'password'>`.

## Backend

- ALWAYS enforce `controller` > `service` > `repository`; flow user → controller → service → repository → data layer.
- Backend: return raw data, including ISO8601 dates and numeric amounts. Frontend: format, localize, present raw data.
- ALWAYS route every user/agent state read/change through controller.
- Controller: parse/cast/validate client input; route validated input to service; present service output; manage authentication/authorization; expose service functions as HTTP routes and possibly timed-job CLI commands. NEVER pass `ctx` to controller; pass only needed request params/body. Route definition: handle redirects/routing.
- Service: business logic; orchestrate repositories/external services. Repository: access database/cache; retrieve/persist data.
- Structure: `index.ts` NodeJS entrypoint; `router.ts` HTTP routes; `cli.ts` CLI commands; `<resource>/<Resource>Controller.ts`, `<Resource>Service.ts`, `<Resource>Repository.ts`.
- ALWAYS use `console.log`/`console.error` appropriately; throw constant `new <HttpError>(<code>, <message>)`; validate request input and response output; document API inputs/outputs; provide health-check endpoint returning API state.
- NEVER repeat resource name in method name.
- ALWAYS use custom `ResourceRepository` extending `nano-fw` `Repository` base class for datasource access. IF base `Repository.ts` methods cannot implement operation THEN create custom repository method. NEVER use custom getters; use `Repository.get`, `getBy`, `findBy`, `getem` for row lookup.
- `packages/api/src/**/*Service.ts`: export `default class <Resource>Service`; methods: `static async`; NEVER access DB client directly; ALWAYS use repositories.
- `packages/api/src/**/*Repository.ts`: extend `Repository` from `nano-fw/database/Repository.ts`; export configured PostgreSQL singleton. NEVER use `pg` outside repositories.
- PostgreSQL timestamps: assume ISO8601 return values.

## Frontend

- ALWAYS use functional React components/hooks. Component: filename matches component; `export const Component = () => {}`; `<ComponentName>Props` above component; built-in hooks through `React` namespace.
- IF React Compiler does not optimize and performance benefit exceeds maintenance cost THEN use `useMemo`/`useCallback`. IF reuse/performance benefit exceeds maintenance cost THEN use custom hook. NEVER use nested JSX ternaries; use early-return/guard clauses for multi-branch rendering or single-level conditions.
- NEVER use external library unless strictly necessary; ALWAYS evaluate bundle-size impact.
- ALWAYS use Tailwind utilities. Frequently reused Tailwind classes: compose with `@apply` in `theme.css`.
- CONFLICT: frequently reused Tailwind classes belong in reusable `ui/` components; NEVER use `@apply`.
- NEVER use inline `style` unless dynamically computed, CSS-in-JS, or string interpolation for classnames. ALWAYS give every component `className` prop to root element as first prop; combine classes with `cx` from `clsx-tw`; dedupe Tailwind classes.
- `icons.tsx`: contain every project icon; re-export each individually.
- UX board: application UI kit with typography, `react-icons`, buttons/inputs with statuses/interactions (inputs by type), success/warning/error snackbar, yes/no confirmation, searchable/filterable table. ALWAYS provide every view at Desktop `1280x700`, Tablet `768x1024`, Smartphone `390x844`.
- Responsive UI: ONLY stack or hide elements as viewport shrinks; NEVER change DOM structure by resolution/user.
- State: use `zustand` plain objects for application/domain state; NEVER use global React Context, except scoped compound UI components.
- Data: use `useSWR` reads and `useSWRMutation` backend mutations; NEVER combine `fetch`/`axios` with manual `useState`/`useEffect` fetching. ALWAYS use meaningful cache-friendly keys and show spinner/skeleton for async operations.
- Forms: use `react-hook-form`; native `<form>`; correct input/button types for Enter submission.
- Entity components: `User` full page; `UserGrid` card explorer; `UserGridItem` card; `UserList` table dashboard; `UserListItem` row; `UserCreationForm`; `UserUpdateForm`.
- Structure: `main.tsx` root React element; `Router.tsx` react-router routes; `components/`; `hooks/`; `ui/` reused primitives including `icons.tsx`; `views/` route-level components except shared layouts.

## Testing

- ALWAYS add proper unit/integration, interaction, and happy-path E2E tests. Unit test: complex pure functions/algorithms only. Integration test: feature flows.
- ALWAYS make test setup explicit; load fixture inside test when possible; keep test input visible. NEVER use clever helpers, default `beforeEach` fixture needed by only some tests, redundant expectations, or meaningless zero-value tests.
- Expectations: one proves one behavior; remove duplicate proof; retain explicit exclusion check when testing exclusion.
- ALWAYS prefer Vitest `expect.matchObject` for grouped object-property expectations and `expect.toEqual`; avoid `expect.toBe` for single assertions.

## Environment

- ALWAYS centralize environment variables in `[.env](./env)`; list every available variable in root `sample.env`. Each service `env.ts`: read, parse, export `process.env` with Zod. NodeJS services: import/read `ENV`. IF adding env THEN update `sample.env`.
- `NODE_ENV`: `test` test build; `development` unminified/unoptimized development build; `production` minified/optimized production build. Business logic: agnostic to `NODE_ENV`.
- `APP_ENV`: `local` developer machine; `development` deployed development; `staging` deployed staging; `production` deployed production.

## Database

- Migrations: ALWAYS use `database.raw` plain SQL; NEVER use knex querybuilder; ALWAYS leave `down` empty.
- Columns: IDs `uuidv7`; dates `timestamptz(0)`; numeric `text`; text `numeric`; enums `<col> text check (col in ('x','y','z'))`.
- Tables: ALWAYS place `id`, `created_at`, `updated_at` first; avoid useless indexes; apply `updated_at` trigger setting column to `now()`.

## Docker

- ALWAYS use Alpine images when possible; minimize image size.

## Git

- Branch: `<type>-<ticker-number>-<summary>`. PR: `<type> <number>: <summary>`. Types: `feat`, `fix`, `chore`, `perf`.
- PR description: `Problem` and `Solution` sections summarizing work. ALWAYS squash-merge PR into `main`.
- CI: GitHub Actions `../.github/workflows/ci.yml`. PR to `main`: test only. Commit to `main`: test, deploy development; `staging`: test, deploy staging; `production`: test, deploy production.

## Communication

- IF requirements unclear THEN ask clarification. ALWAYS ask confirmation for design decisions.
- ALWAYS answer/code in English and ASD-STE100 Simplified Technical English. ALWAYS be concise/direct. NEVER be chatty, verbose, use dashes/emojis, or create wall of text.
- IF plan too complex THEN use HTML visualization. IF user asks clarification THEN use ELI12 mode. NEVER install dependencies without user confirmation.

## Specs

- Specs: AI coding-agent consumer only; maximize token efficiency/density; write for LLM parser.
- ALWAYS use English ASD-STE100 Simplified Technical English; H2 headings, bullets, and code blocks only; list required changes as bullets.
- NEVER use prose, introductions, background explanations, articles (`a`, `an`, `the`), conversational filler, or passive voice.
