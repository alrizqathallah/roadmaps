# Frontend Development Learning Roadmap
### From Zero to Industry-Ready — Practical, Structured, Effective

---

## How to Use This Roadmap

This roadmap is divided into **4 phases**. Each phase builds on the previous one and includes:
- **Core concepts** to learn
- **Exercises** (small, targeted drills)
- **Mini-projects** (1–3 day builds)
- **Large projects** (1–2 week builds)
- **Industry relevance notes** to keep you grounded in real-world expectations

Estimated total time: **9–14 months** at ~10–15 hours/week.

---

## Phase 1 — Foundations
### Duration: 6–8 weeks
### Goal: Understand how the web works and build static pages confidently.

---

### 1.1 How the Web Works

**Concepts:**
- Client–server model, HTTP/HTTPS basics
- What browsers do (parsing, rendering, DOM construction)
- DNS, URLs, and request/response lifecycle
- Web standards bodies (W3C, WHATWG)

**Industry Note:** Developers who understand the browser aren't just coders — they debug faster, optimize better, and communicate more effectively with backend teams.

**Exercise:**
- Open DevTools → Network tab. Load any website and trace one HTML request: inspect status codes, headers, and response time.
- Answer in writing: what happens between typing a URL and seeing a page?

---

### 1.2 HTML — Structure & Semantics

**Concepts:**
- Document structure: `<!DOCTYPE>`, `<head>`, `<body>`
- Semantic elements: `<header>`, `<main>`, `<article>`, `<section>`, `<footer>`, `<nav>`, `<aside>`
- Forms: inputs, labels, validation attributes
- Accessibility basics: ARIA roles, `alt` text, tab order
- HTML5 media: `<video>`, `<audio>`, `<picture>`
- Metadata and SEO: `<meta>`, Open Graph tags

**Industry Note:** Semantic HTML is not optional — it directly affects SEO, screen reader support, and code maintainability. Employers expect it.

**Exercises:**
1. Mark up a blog post using only semantic HTML, no `<div>` tags allowed.
2. Build a multi-field contact form with proper labels, `required`, `type`, and `placeholder` attributes.
3. Audit any webpage with a screen reader (NVDA or macOS VoiceOver) and note what breaks.

**Mini-Project: Personal Bio Page**
- A single HTML-only page about yourself
- Must include: navigation, sections, a contact form, an image with alt text, and a footer
- No CSS yet — pure structure only

---

### 1.3 CSS — Visual Styling

**Concepts:**
- Selectors, specificity, and the cascade
- Box model: `margin`, `border`, `padding`, `content`
- Display values: `block`, `inline`, `inline-block`, `none`
- Typography: `font-family`, `font-size`, `line-height`, `letter-spacing`
- Colors: hex, rgb, hsl, and CSS custom properties (`--variables`)
- Flexbox: `flex-direction`, `justify-content`, `align-items`, `gap`, `flex-wrap`
- CSS Grid: `grid-template-columns`, `fr`, `grid-area`, `auto-fill`/`auto-fit`
- Responsive design: media queries, mobile-first approach
- Transitions and simple animations: `transition`, `@keyframes`, `animation`
- Pseudo-classes and pseudo-elements: `:hover`, `:focus`, `::before`, `::after`

**Industry Note:** Flexbox and Grid are the industry standard for layout. Avoid older techniques like `float` for layout — they are legacy patterns.

**Exercises:**
1. Recreate a navigation bar with logo on the left and links on the right using only Flexbox.
2. Build a 3-column card grid that collapses to 1 column on mobile.
3. Create a button with a hover animation using only CSS transitions.
4. Define a color palette using CSS custom properties and apply it across a small page.

**Mini-Project: Product Landing Page**
- A responsive landing page for any product (real or fictional)
- Must include: hero section, feature grid, pricing table, and footer
- Must be fully responsive (mobile + desktop)
- Apply a custom color palette via CSS variables

---

### 1.4 JavaScript — Core Language

**Concepts:**
- Variables: `var`, `let`, `const`; scoping rules
- Data types: string, number, boolean, null, undefined, object, array, symbol
- Operators, expressions, and type coercion
- Control flow: `if/else`, `switch`, loops (`for`, `while`, `for...of`, `for...in`)
- Functions: declarations, expressions, arrow functions, default params, rest params
- Arrays: `map`, `filter`, `reduce`, `find`, `forEach`, `some`, `every`
- Objects: literals, destructuring, spread/rest, optional chaining (`?.`)
- DOM manipulation: `querySelector`, `addEventListener`, `classList`, `innerHTML`, `createElement`
- Events: click, input, submit, keyboard, custom events
- Error handling: `try/catch/finally`, custom errors
- Asynchronous JS: callbacks → Promises → `async/await`
- `fetch` API and working with JSON

**Industry Note:** Learn JavaScript before any framework. Frameworks abstract JavaScript — if you don't know what they're abstracting, you won't be able to debug them.

**Exercises:**
1. Write a function that takes an array of numbers and returns only the even ones — without using `filter`. Then rewrite it with `filter`.
2. Implement a debounce function from scratch.
3. Fetch data from `https://jsonplaceholder.typicode.com/posts` and render the first 5 posts into a list on the DOM.
4. Build a simple event emitter class with `on`, `emit`, and `off` methods.

**Mini-Project: Interactive Quiz App**
- 5-question quiz with multiple choice answers
- Show score at the end
- No frameworks — vanilla HTML, CSS, JS only
- Add a timer per question as a bonus

**Large Project: Weather Dashboard (Vanilla JS)**
- Integrate the OpenWeatherMap API (free tier)
- Users search for a city and see: current temperature, humidity, wind speed, 5-day forecast
- Responsive layout
- Handle loading states and errors gracefully
- Store last searched city in `localStorage`

---

## Phase 2 — Modern Tooling & React
### Duration: 8–10 weeks
### Goal: Build dynamic, component-based applications with industry-standard tools.

---

### 2.1 Development Environment & Tooling

**Concepts:**
- Node.js and npm/pnpm ecosystem
- `package.json`, `node_modules`, scripts
- Vite: fast dev server and bundler
- ESLint and Prettier: linting and code formatting
- Git: branching, staging, commits, merging, rebase basics
- GitHub: pull requests, code review workflow

**Industry Note:** Every professional frontend project uses some version of this toolchain. Knowing it makes you immediately productive on day one at a new job.

**Exercises:**
1. Initialize a new Vite project, set up ESLint + Prettier, and push it to a new GitHub repo.
2. Practice the Git feature branch workflow: create a branch, make changes, open a pull request, and merge it.

---

### 2.2 React — Component Model

**Concepts:**
- JSX syntax and rules
- Functional components
- Props: passing, typing with PropTypes or TypeScript, default values
- State: `useState` — initializing, reading, and updating
- Event handling in React
- Conditional rendering: ternary, `&&`, early return
- Lists and keys
- Component composition and the children prop
- Lifting state up

**Industry Note:** React powers a huge proportion of the industry. Understanding its component model is transferable to Vue, Svelte, and Angular.

**Exercises:**
1. Build a `<Button>` component that accepts `label`, `onClick`, `variant` (primary/secondary), and `disabled` props.
2. Build a counter with increment, decrement, and reset — manage state in the parent, pass handlers as props.
3. Render a list of products from a JS array. Each item should show a name, price, and an "Add to Cart" button.

**Mini-Project: Kanban Board (Local State)**
- Three columns: To Do, In Progress, Done
- Add tasks via a form, move them between columns
- State lives at the board level; columns and cards are separate components
- No backend — all in-memory

---

### 2.3 React — Hooks & Side Effects

**Concepts:**
- `useEffect`: side effects, dependency array, cleanup functions
- `useRef`: DOM references and mutable values
- `useMemo` and `useCallback`: performance optimization
- Custom hooks: extracting reusable logic
- Context API: `createContext`, `useContext`, `Provider`

**Industry Note:** Custom hooks are how senior React developers share logic without repeating code. Expect to write and read them constantly.

**Exercises:**
1. Build a `useLocalStorage` custom hook. Use it in a notes app to persist notes across page reloads.
2. Build a `useFetch` custom hook that handles loading, error, and data states.
3. Use `useEffect` to sync a document title with a counter's current value.

**Mini-Project: Movie Search App**
- Search movies via the OMDB API
- Show results as cards with poster, title, and year
- Implement a debounced search input (debounce with `useEffect`)
- Show loading spinner and error state

---

### 2.4 Routing & Navigation

**Concepts:**
- React Router v6: `<BrowserRouter>`, `<Routes>`, `<Route>`, `<Link>`, `<NavLink>`
- URL params: `useParams`
- Programmatic navigation: `useNavigate`
- Nested routes and layout routes
- Protected routes (authentication guard pattern)

**Exercises:**
1. Build a 3-page site (Home, About, Contact) with React Router. Highlight the active nav link.
2. Create a dynamic route `/users/:id` that fetches and displays a user from an API.
3. Build a protected `/dashboard` route that redirects unauthenticated users to `/login`.

---

### 2.5 Global State Management

**Concepts:**
- When local state isn't enough: prop drilling problem
- Context + useReducer pattern
- Zustand: minimal, practical global state
- Redux Toolkit (RTK): for larger applications
- Server state vs. client state distinction

**Industry Note:** Most companies use either Zustand, Redux Toolkit, or Jotai. Learn Zustand first — it's minimal, testable, and increasingly preferred.

**Exercises:**
1. Refactor a prop-drilled cart system to use Zustand.
2. Implement undo/redo using `useReducer`.

**Large Project: E-commerce Store**
- Product listing page with filter and sort
- Product detail page
- Shopping cart (add, remove, update quantity)
- Checkout form with validation
- Zustand for cart state
- React Router for navigation
- Fetch products from a mock API (mockapi.io or your own JSON)

---

### 2.6 TypeScript Fundamentals

**Concepts:**
- Why TypeScript: catching errors at compile time
- Basic types: `string`, `number`, `boolean`, `null`, `undefined`, `any`, `unknown`
- Arrays, tuples, and enums
- Interfaces and type aliases
- Function signatures and return types
- Generics: `<T>`, common use cases
- React with TypeScript: typing props, state, events, and refs
- Utility types: `Partial`, `Required`, `Pick`, `Omit`, `Record`

**Industry Note:** TypeScript is the default in professional React projects. Treat it as essential, not optional.

**Exercises:**
1. Type a `fetchUser` function that returns `Promise<User>` where `User` is an interface you define.
2. Create a generic `useLocalStorage<T>` hook.
3. Type a form's `onChange` handler precisely using `React.ChangeEvent<HTMLInputElement>`.

---

## Phase 3 — Professional Practices
### Duration: 8–10 weeks
### Goal: Build production-quality apps that are performant, tested, and maintainable.

---

### 3.1 CSS at Scale

**Concepts:**
- Tailwind CSS: utility-first philosophy, configuration, responsive variants
- CSS Modules: scoped styles in component files
- CSS-in-JS: styled-components or Emotion (know the trade-offs)
- Design tokens: spacing scale, type scale, color system
- Component library patterns: building your own UI library
- Dark mode: `prefers-color-scheme`, CSS variable theming

**Industry Note:** Tailwind CSS dominates new projects. Learn it deeply — including how to extend it, not just use default utilities.

**Exercises:**
1. Rebuild the Phase 1 landing page using only Tailwind CSS.
2. Create a reusable `<Card>` component with variants (default, elevated, outlined) using Tailwind's `cva` pattern.
3. Implement a dark/light mode toggle using CSS variables and `localStorage`.

**Mini-Project: Design System Starter**
- A small component library with: Button, Input, Badge, Card, Modal, Toast
- Each component has documented props
- Dark mode support built in

---

### 3.2 Data Fetching & Server State

**Concepts:**
- TanStack Query (React Query): `useQuery`, `useMutation`, query keys, stale time
- Optimistic updates
- Pagination and infinite scroll
- SWR as an alternative
- Caching strategies
- REST vs. GraphQL fundamentals

**Industry Note:** TanStack Query has become the industry standard for data fetching in React. It eliminates enormous amounts of manual state management.

**Exercises:**
1. Convert a `useEffect`-based fetch to `useQuery`. Compare the before/after code.
2. Implement an optimistic "like" button using `useMutation` with `onMutate`.
3. Build a paginated list that fetches the next page on scroll.

---

### 3.3 Forms & Validation

**Concepts:**
- Controlled vs. uncontrolled inputs
- React Hook Form: `useForm`, `register`, `handleSubmit`, `formState`
- Zod: schema-based validation, integration with React Hook Form
- Field arrays: dynamic form fields
- Multi-step forms

**Exercises:**
1. Build a registration form with: email, password (min 8 chars), confirm password, and terms checkbox. Validate with Zod.
2. Build a dynamic form where users can add/remove team member fields.

---

### 3.4 Testing

**Concepts:**
- Why testing: catching regressions, documenting behavior, enabling refactoring
- Unit testing with Vitest
- Component testing with React Testing Library (RTL)
- Querying: `getByRole`, `getByText`, `getByLabelText` (prefer accessible queries)
- Firing events and asserting outcomes
- Mocking: API calls, modules, timers
- End-to-end testing with Playwright: writing tests, selectors, assertions, CI integration

**Industry Note:** The testing pyramid: many unit tests, fewer integration tests, few E2E tests. Knowing RTL and Playwright covers the vast majority of frontend testing scenarios employers care about.

**Exercises:**
1. Write unit tests for a `formatCurrency(amount, currency)` utility function.
2. Test a `<LoginForm>` component: assert that a validation error appears when the email is blank on submit.
3. Write a Playwright E2E test that: navigates to a product page, adds an item to cart, and verifies the cart count updates.

---

### 3.5 Performance Optimization

**Concepts:**
- Core Web Vitals: LCP, FID/INP, CLS — what they measure and why they matter
- Code splitting: `React.lazy` + `Suspense`, dynamic `import()`
- Bundle analysis: Rollup Visualizer or Webpack Bundle Analyzer
- Image optimization: modern formats (WebP, AVIF), lazy loading, `srcset`
- Memoization: `React.memo`, `useMemo`, `useCallback` — when to and when NOT to use them
- Virtualization: `TanStack Virtual` for long lists
- Web Workers for heavy computation

**Exercises:**
1. Audit your E-commerce project with Lighthouse. Identify 3 issues and fix them.
2. Implement virtualization for a list of 10,000 items using TanStack Virtual.
3. Lazy-load the checkout route and measure the impact on initial bundle size.

---

### 3.6 Accessibility (a11y)

**Concepts:**
- WCAG 2.1 AA: the standard most companies target
- Keyboard navigation: focus management, skip links, tab trapping in modals
- ARIA: when to use it and when HTML semantics are sufficient
- Color contrast requirements
- Accessible forms: labels, error messages, `aria-describedby`
- Screen reader testing workflow

**Industry Note:** Accessibility is a legal requirement in many jurisdictions and increasingly a hiring signal. It also improves UX for all users.

**Exercises:**
1. Fix a provided inaccessible modal (no focus trap, no close on Escape, no ARIA) to be fully accessible.
2. Run axe DevTools on your E-commerce project. Fix every critical and serious violation.

---

## Phase 4 — Advanced & Architecture
### Duration: 10–14 weeks
### Goal: Architect scalable applications, contribute to teams, and lead technical decisions.

---

### 4.1 Next.js & Server-Side Rendering

**Concepts:**
- Rendering strategies: CSR, SSR, SSG, ISR — trade-offs for each
- Next.js App Router: layouts, pages, loading, error boundaries
- Server Components vs. Client Components
- Data fetching in Server Components
- API Routes and Route Handlers
- Next.js Image and Font optimization
- Deployment: Vercel, static export, Docker

**Industry Note:** Next.js is the dominant React meta-framework. Most React job postings now list it explicitly.

**Exercises:**
1. Convert your Movie Search App to Next.js. Move the API call to a Server Component.
2. Implement ISR for a blog: posts are statically generated but revalidate every 60 seconds.

**Mini-Project: Blog Platform**
- Markdown-powered blog with static generation
- Category filtering
- RSS feed
- SEO metadata per post
- Deployed on Vercel

---

### 4.2 Authentication & Authorization

**Concepts:**
- Cookie-based vs. token-based (JWT) auth
- NextAuth.js / Auth.js: OAuth providers, sessions, callbacks
- Role-based access control (RBAC)
- Secure storage: never store JWTs in localStorage
- CSRF protection

**Exercises:**
1. Add Google OAuth login to a Next.js app using Auth.js.
2. Implement route-level RBAC: admin-only pages, user-only pages.

---

### 4.3 Real-Time Features

**Concepts:**
- WebSockets: connection lifecycle, sending/receiving messages
- Socket.io: rooms, namespaces, events
- Server-Sent Events (SSE): one-way real-time streams
- Optimistic UI for real-time interactions

**Mini-Project: Real-Time Chat App**
- Rooms and direct messages
- Online presence indicator
- Message history persisted to a database (Supabase or PlanetScale free tier)
- Built with Next.js + Socket.io

---

### 4.4 Frontend Architecture Patterns

**Concepts:**
- Feature-based folder structure vs. type-based
- Colocation: keep tests, styles, and stories near the component
- Barrel files: benefits and pitfalls
- Monorepos: Turborepo or Nx — when and why
- The BFF (Backend for Frontend) pattern
- Micro-frontends: concept, trade-offs, when to use

**Exercises:**
1. Refactor your E-commerce project from a type-based structure to a feature-based structure.
2. Set up a Turborepo with two apps (web, docs) sharing a common UI package.

---

### 4.5 CI/CD & DevOps Basics for Frontend

**Concepts:**
- GitHub Actions: writing workflows for lint, test, and build
- Preview deployments (Vercel, Netlify)
- Environment variables: `.env` files, secret management
- Bundle size budgets in CI
- Lighthouse CI for automated performance regression detection

**Exercises:**
1. Write a GitHub Actions workflow that runs ESLint + Vitest on every pull request.
2. Add a Lighthouse CI step that fails the build if LCP > 2.5s.

---

### 4.6 Large Capstone Project: Full-Stack SaaS Application

**Project: Project Management Tool (Jira-lite)**

This project consolidates everything learned across all four phases.

**Features:**
- Authentication (Google OAuth + email/password via Auth.js)
- Workspaces and Projects
- Kanban board with drag-and-drop (dnd-kit)
- Task CRUD: title, description, assignee, priority, due date, labels
- Real-time updates (Socket.io or Supabase Realtime)
- Activity log per task
- Notifications (in-app + email via Resend)
- Dashboard with charts (Recharts or Victory)
- Full-text search
- Role-based access: owner, member, viewer
- Responsive design with dark mode

**Tech stack:**
- Next.js 14+ (App Router)
- TypeScript
- Tailwind CSS
- TanStack Query
- React Hook Form + Zod
- Zustand (UI state)
- Prisma + PostgreSQL (Supabase)
- Auth.js
- Playwright E2E tests
- GitHub Actions CI
- Deployed on Vercel

**Deliverables:**
- Public GitHub repo with a detailed README
- Live deployed URL
- At minimum 80% test coverage on core business logic
- Lighthouse score: Performance ≥ 90, Accessibility ≥ 90

---

## Supplementary Skills (Integrate throughout)

| Skill | When to Learn | Tools |
|---|---|---|
| Browser DevTools | Phase 1 | Chrome DevTools |
| Command Line | Phase 1 | Bash / Zsh basics |
| Figma (read designs) | Phase 2 | Figma free tier |
| REST API design basics | Phase 2 | Postman / Insomnia |
| SQL basics | Phase 3 | SQLite / PostgreSQL |
| Documentation | Phase 3 | Storybook, JSDoc |
| Open Source contribution | Phase 4 | GitHub |

---

## Resource Index

### HTML & CSS
- [MDN Web Docs](https://developer.mozilla.org) — primary reference, always
- [CSS Tricks — A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [CSS Tricks — A Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)

### JavaScript
- *Eloquent JavaScript* by Marijn Haverbeke (free online)
- [javascript.info](https://javascript.info) — the best free JS resource
- *You Don't Know JS* series by Kyle Simpson (free on GitHub)

### React
- [React official docs (react.dev)](https://react.dev) — excellent, start here
- *Road to React* by Robin Wieruch

### TypeScript
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [Total TypeScript](https://www.totaltypescript.com) — free workshops

### Testing
- [Testing Library docs](https://testing-library.com/docs/)
- [Playwright docs](https://playwright.dev/docs/intro)
- *Testing JavaScript* by Kent C. Dodds

### Performance
- [web.dev/performance](https://web.dev/performance/)
- [Chrome DevTools Performance panel](https://developer.chrome.com/docs/devtools/performance/)

### System Design / Architecture
- [Frontend System Design — roadmap.sh](https://roadmap.sh/frontend)
- *Learning Patterns* by Lydia Hallie (patterns.dev, free online)

---

## Progress Checkpoints

Use these to self-assess before moving to the next phase.

### After Phase 1
- [ ] Can build a responsive multi-section page from scratch without referencing docs
- [ ] Understands the box model, Flexbox, and Grid without guessing
- [ ] Can manipulate the DOM and handle events in vanilla JS
- [ ] Built and deployed the Weather Dashboard

### After Phase 2
- [ ] Understands React's rendering model and can explain why re-renders happen
- [ ] Comfortable with hooks, custom hooks, and Context
- [ ] Can type React components and hooks in TypeScript
- [ ] Built and deployed the E-commerce Store

### After Phase 3
- [ ] Can write meaningful tests for components and utilities
- [ ] Has audited and improved a real app's Lighthouse score
- [ ] Understands TanStack Query and uses it instead of raw `useEffect` for fetching
- [ ] Can articulate accessibility requirements and fix violations

### After Phase 4
- [ ] Can architect a feature-based project structure and explain the decisions
- [ ] Has shipped a full-stack app to production
- [ ] Understands CI/CD workflows and can write GitHub Actions
- [ ] Has a public portfolio with at least 3 substantial projects

---

*Built for developers who want to work in the industry, not just pass interviews. Focus on shipping real things.*