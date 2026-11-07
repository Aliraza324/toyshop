# Project Instructions & Development Guidelines

This document outlines the strict architectural, coding, and structural rules for the **Follow** web application project.

---

## 1. Core Development Rules

### Rule 1: Maximum 200 Lines Per File
- No single code file (`.jsx`, `.js`, `.css`, etc.) must exceed **200 lines**.
- If any component, layout, or page approaches or exceeds 200 lines, immediately break it down into modular child components, dedicated hooks, or sub-modules inside `src/components/`.

### Rule 2: No `<a>` Tag — Use `<Link>` Exclusively
- Do not use HTML `<a>` tags for navigation anywhere in the codebase.
- Always use `<Link>` or `<NavLink>` from `react-router` (`react-router` v8 / `react-router-dom`).
- For external links or trigger actions, use appropriate semantic elements like `<button>` or a dedicated routing wrapper without raw anchor tags.

### Rule 3: Dedicated `mockup/` Folder for Data
- All mock data, placeholder records, lists, navigation items, cards, and dataset constants must live in `src/mockup/`.
- Components, sections, and pages must import and consume data from `src/mockup/` instead of hardcoding heavy data objects inside JSX files.
- Each major domain or section must have its own dedicated mock file (e.g., `navigation.js`, `hero.js`, `programs.js`, etc.).

### Rule 4: Zero Comments in Code
- Do not write comments in any source code file (`//`, `/* */`, `{/* */}`).
- Code must be self-explanatory, clean, and readable through clear variable, function, and component naming.
- Never leave commented-out code snippets.

### Rule 5: Lucide Animated Icons & Parent-Triggered Animation
- **Use `lucide-animated`**: Always use `lucide-animated` for icons across the application.
- **Parent Section / Container Trigger (No Direct Icon-Only Hover)**:
  - Icons must **not** animate only when the mouse hovers directly over the icon itself.
  - The animation must trigger as soon as the mouse enters the **parent section, card, or container** (`onMouseEnter` / parent hover / `group-hover`).
  - When the cursor enters the section/wrapper div containing the icon, the icon must animate smoothly.
- **Dedicated `src/icons/` Directory**:
  - All icon definitions, customized icon components, and wrappers must reside in `src/icons/`.
  - Icon files are created inside `src/icons/`, importing from `lucide-animated` (managing parent hover triggers, refs, or animation controls).
  - Components, sections, and pages must import their required icons directly from `src/icons/` rather than importing ad-hoc throughout the codebase.

---

## 2. Complete Folder Structure Analysis

### Current Workspace Audit

```text
Follow/
├── public/                 # Static assets served as-is
├── src/
│   ├── assets/             # Media assets (hero.png, react.svg, vite.svg)
│   ├── components/         # Reusable UI widgets and atomic components
│   ├── icons/              # Centralized animated icons components and wrappers
│   ├── layouts/            # Page shell layouts (MainLayout.jsx)
│   ├── mockup/             # Mock datasets and static JSON/JS arrays
│   ├── pages/              # Route views and page components
│   ├── routes/             # Route configurations and router definitions
│   ├── App.jsx             # Root component
│   ├── index.css           # Global Tailwind CSS v4 styling
│   └── main.jsx            # Application mount point (StrictMode, Root)
├── .gitignore
├── eslint.config.js        # ESLint configuration
├── index.html              # HTML entry point
├── package.json            # Dependencies: React 19, React Router 8, Tailwind v4, Vite 8
├── README.md
└── vite.config.js          # Vite config with React and Tailwind plugins
```

### Folder Breakdown & Responsibilities

| Directory | Purpose | Rule Checklist |
| :--- | :--- | :--- |
| `src/icons/` | Centralized animated icon components and wrappers built with `lucide-animated`. | Modular, parent-triggered animations (no icon-only hover), under 200 lines, zero comments. |
| `src/mockup/` | Holds all static datasets, mock arrays, and content objects. | Modularized by feature, imported by components, under 200 lines. |
| `src/components/` | Reusable sections, cards, UI buttons, headers, footers, modals. | Modular, under 200 lines each, no raw `<a>` tags, no comments. |
| `src/layouts/` | Shell layouts like `MainLayout.jsx` wrapping `<Outlet />` or header/footer. | Under 200 lines, provides standard framing and Lenis container. |
| `src/pages/` | Primary views corresponding to routes. | Assembled from `src/components/`, data driven via `src/mockup/`. |
| `src/routes/` | Router setup (`createBrowserRouter` or `<Routes>`). | Clean route definitions and code-split loaders if needed. |
| `src/assets/` | Local static images, SVGs, and brand graphics. | Optimized image formats (WebP, SVG, PNG). |

---

## 3. Design System & Animation Blueprint (Baseline Reference)

When actual project content is provided, apply the following design and motion standards:

- **Adaptive Rem Scaling**:
  - Base width: 1920px (`FONT_BASE = 16px`).
  - Proportional `vw` media queries for `< 1920px`, `< 1440px`, `< 1024px`, `< 640px`.
  - Dynamic JS scale-up for viewports `> 1920px`.
  - Outer page framing inset (`0.5rem` / `0.75rem`) giving card-like frames.

- **Motion & Interaction Architecture**:
  - Smooth scroll driven by Lenis.
  - Spring-based micro-interactions (`tension` / `friction` model).
  - Clip-mask staggered reveals for headlines and text.
  - In-view scroll-triggered reveals (`IntersectionObserver`).
  - Staggered hover animations (card lift, icon rotate, arrow nudge).
  - Parent-triggered animated icons (`lucide-animated` icons trigger animations on parent section/card/div mouse enter, not isolated direct icon hover).

