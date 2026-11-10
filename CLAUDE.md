# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project context

This is the starter project for a Claude Code course ("Expense Tracker" / `finance-tracker`). It is a small React 19 + Vite 7 app that **intentionally** ships with a bug, a poor UI and messy code, which the course fixes step by step. Expect to be asked to find bugs, refactor and restyle. Don't treat the current structure as a pattern to keep.

## Commands

```bash
npm install       # install dependencies
npm run dev       # Vite dev server at http://localhost:5173 (HMR)
npm run build     # production build to dist/
npm run preview   # serve the built dist/
npm run lint      # ESLint (flat config, eslint.config.js)
```

The project has no test framework and no `test` script yet.

## Architecture

- `src/main.jsx` mounts `<App />` inside `StrictMode`. `src/index.css` holds the global styles.
- `src/App.jsx` is the whole app in one component:
  - Transactions are kept in local `useState`, seeded with hard-coded sample data. Nothing is saved, so data resets on reload, and the app has no backend or API.
  - Form fields (description, amount, type, category) and the filters (type, category) are each a separate `useState`.
  - The income, expense and balance totals and the filtered list are worked out inline on every render.
  - The `categories` array is defined inside the component and used by both the add form and the category filter.
- `src/App.css` holds the component styles, matched by class name (`.summary-card`, `.income-amount`, `.expense-amount`, …).

## Known data quirks (relevant when debugging)

- `amount` is stored as a **string**, both in the seed data and from the form input. The totals use `reduce((sum, t) => sum + t.amount, 0)`, which joins the strings together instead of adding the numbers.
- In the seed data, "Freelance Work" has category `salary` but type `expense`.

## Lint config notes

- ESLint uses the recommended JS rules, plus `react-hooks` and `react-refresh` (Vite preset).
- `no-unused-vars` ignores names that match `^[A-Z_]`.
- `dist/` is ignored.
