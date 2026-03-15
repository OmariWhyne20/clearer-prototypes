# Clearer Prototypes — Claude Code Rules

## What This Repo Is

This repo hosts **interactive prototypes** for the Clearer squad at ClearScore. Each prototype lives in its own folder under the repo root. They are deployed to GitHub Pages so stakeholders, designers, and engineers can view them in a browser without any local setup.

**Live site:** https://omariwhyne20.github.io/clearer-prototypes/

## Clearer Domain Context

Clearer is ClearScore's automated debt consolidation product. It helps UK consumers consolidate multiple debts (credit cards, personal loans, store cards) into a single, lower-cost loan.

Key concepts you must understand to build useful prototypes:

- **Data confidence**: Clearer knows about a user's debts from two sources. "Categorised" (Open Banking-connected) debts have verified balances, payments, and interest rates. "Extrapolated" debts are fuzzy-matched from credit bureau data — the APR is estimated from credit profile and product type. Always surface this distinction in the UI.
- **Settlement figures**: The amount required to actually close a debt. These come from the lender, not ClearScore, and may differ from outstanding balances (early settlement fees, accrued interest). Settlement figures are NOT a configuration Clearer controls — never present them as editable or ClearScore-generated.
- **Configuration options**: Clearer offers lenders three tiers of integration. Config 1 (post-disbursal settlement), Config 2 (debt selection data pre-decisioning — highest leverage), Config 3 (mandated debts + enforcement). Prototypes should be aware of which tier they're demonstrating.
- **Lender partners**: Current and prospective partners include Novuna, Oakbrook, 118 Money, Plata. Use real partner names in prototypes where contextually appropriate.

## CRITICAL: Folder Rules

**All prototype work goes inside `projects/<project-name>/`.** Never create files at the repo root (except `index.html` and this file).

```
repo root/
├── CLAUDE.md                                   ← this file (do not edit unless asked)
├── index.html                                  ← listing page (update when adding prototypes)
├── _shared/
│   └── slate-cs24-tokens.css                   ← shared design tokens (do not edit unless asked)
└── projects/
    ├── clearer-calculator/
    │   ├── README.md                           ← project context, versions, design decisions
    │   └── v1-pre-confirmation.html
    └── <next-prototype>/
        ├── README.md
        └── ...
```

### Before starting any prototype work, ask:

1. **New prototype or iteration on an existing one?**
2. **What should it be called?** (Use kebab-case for folder names, e.g. `debt-selection-flow`)

Do not infer names. Do not skip this step.

### Adding a new prototype

1. Create a subfolder under `projects/` with a descriptive kebab-case name
2. Create a `README.md` with project details (see template below)
3. Create the prototype file(s)
4. Add an entry to `index.html` linking to the new prototype
5. Link the shared tokens: `<link rel="stylesheet" href="../../_shared/slate-cs24-tokens.css" />`

### README.md template for new projects

```markdown
# <Project Name>

One-line description of what this prototype shows.

## Project Details
- **Name**: <Project Name>
- **View Type**: Mobile View
- **Canvas Size**: 428px width (iPhone viewport)
- **Created**: <dd/mm/yyyy>

## Versions
- `v1-<descriptor>.html` — What this version shows

## What This Prototype Tests
- Question 1 this prototype answers
- Question 2 this prototype answers

## Key Design Decisions
- Decision and rationale
- Decision and rationale

## Files
- `v1-<descriptor>.html` — Description
```

## Design System: Slate CS24

All Clearer prototypes use ClearScore's **Slate design system** with the **CS24 theme**. The shared tokens file at `_shared/slate-cs24-tokens.css` contains:

- CSS custom properties (colours, shadows, borders, typography, component tokens)
- Base reset styles
- Utility classes for common Slate component patterns

### Always use tokens — never hard-code values

```css
/* GOOD */
color: var(--slate-color-content-text-primary);
background: var(--slate-components-card-background-primary);

/* BAD */
color: #0d2634;
background: white;
```

### Key colour tokens

| Purpose | Token | Appearance |
|---|---|---|
| Primary text | `--slate-color-content-text-primary` | Dark teal-navy |
| Secondary text | `--slate-color-content-text-secondary` | Muted dark |
| Disabled text | `--slate-color-content-text-disabled` | Light grey |
| Inverted text | `--slate-color-content-text-inverted-primary` | White |
| Action/link | `--slate-color-action-text-primary` | Teal |
| Positive | `--slate-color-positive-text-primary` | Green |
| Negative | `--slate-color-negative-text-primary` | Pink-red |
| Warning | `--slate-color-warning-text-primary` | Orange |
| Page background | `--slate-color-surface-background-primary` | Light teal-grey |
| Card background | `--slate-components-card-background-primary` | White |
| Primary button bg | `--slate-components-button-primary-background` | Teal-to-navy gradient |

### Key typography tokens

| Style | Token | Weight / Size |
|---|---|---|
| Hero 5 | `--slate-font-mobile-hero-level-5` | 900 / 2rem (CS Clarity Display) |
| Hero 6 | `--slate-font-mobile-hero-level-6` | 900 / 1.5rem (CS Clarity Display) |
| Heading 3 | `--slate-font-mobile-heading-level-3` | 700 / 1.25rem |
| Heading 4 | `--slate-font-mobile-heading-level-4` | 700 / 1rem |
| Body | `--slate-font-mobile-body-default` | 400 / 1rem |
| Body bold | `--slate-font-mobile-body-bold` | 700 / 1rem |
| Body small | `--slate-font-mobile-body-small` | 400 / 0.875rem |
| Caption | `--slate-font-mobile-special-caption` | 400 / 0.75rem |
| Overline | `--slate-font-mobile-special-overline` | 500 / 0.75rem (uppercase) |
| Button | `--slate-font-mobile-button-medium` | 700 / 1rem |

Font family is **CS Clarity** (body) and **CS Clarity Display** (hero headings), falling back to Helvetica Neue → Arial → sans-serif. These fonts won't render outside ClearScore's network — the fallback is fine for prototypes.

### Utility classes available in the shared CSS

- **Cards**: `.slate-card`, `.slate-card-content`
- **Callouts**: `.slate-callout`, `.slate-callout-positive`, `.slate-callout-warning`, `.slate-callout-negative`
- **Buttons**: `.slate-btn`, `.slate-btn-primary`, `.slate-btn-tertiary`
- **Text sentiment**: `.slate-text-primary`, `.slate-text-secondary`, `.slate-text-disabled`, `.slate-text-positive`, `.slate-text-negative`, `.slate-text-warning`, `.slate-text-action`, `.slate-text-inverted`, `.slate-text-inverted-secondary`
- **Cell separators**: `.slate-cell-separator` (adds border-bottom, removed on `:last-child`)
- **Tags**: `.slate-tag`, `.slate-tag-positive`, `.slate-tag-warning`
- **Layout**: `.slate-sticky-bottom`, `.slate-divider`
- **Animation**: `.fade-in`

## Prototype Stack

### Default: Single-file React via CDN

Most prototypes should be a **single HTML file** using React + Babel loaded from CDN. This keeps things demoable — open the file in a browser, paste the URL into Slack, or screen-share in a stakeholder meeting.

```html
<link rel="stylesheet" href="../_shared/slate-cs24-tokens.css" />
<script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
```

Write JSX inside `<script type="text/babel">` blocks. Use React hooks (`useState`, `useMemo`, `useEffect`) for interactivity. Keep state simple — no state management libraries.

### When to split files

Only split into multiple files if:
- The prototype has multiple distinct pages/screens
- A shared calculation engine is reused across versions
- The file exceeds ~800 lines and readability suffers

Even then, keep it to HTML + one JS file. No build tools, no npm, no bundlers.

### Mobile-first

Prototypes simulate a mobile experience. Use `max-width: 428px` (iPhone viewport) centered on the page. Use Slate's mobile font tokens (desktop breakpoint tokens exist but mobile-first is the default).

## Data Conventions

Use realistic UK data in prototypes:

- **Creditor names**: Barclaycard, HSBC, Lloyds, Capital One, Tesco Bank, Virgin Money, Nationwide, NatWest, Sainsbury's Bank, M&S Bank, NewDay, Vanquis
- **Lender names**: Novuna, Oakbrook, 118 Money, Zopa, Shawbrook
- **Debt amounts**: Credit cards £1,000–£8,000, personal loans £3,000–£15,000
- **APR ranges**: Credit cards 19.9%–39.9%, personal loans 5.9%–14.9%, consolidation loans 5.9%–9.9%
- **Formatting**: £ symbol, dd/mm/yyyy dates, "per month" or "/mo" for payments
- **Currency function**: Format as `£X,XXX` with `toLocaleString('en-GB')`

## Calculation Logic

If a prototype compares debts vs consolidation, the calculations must actually work — no hardcoded outputs.

- **Credit cards**: Use reducing balance formula. Monthly rate = APR / 12 / 100. Months to repay = `ceil(-log(1 - (balance × r) / payment) / log(1 + r))`.
- **Personal loans**: Use remaining term × monthly payment for total cost.
- **Consolidation loan**: Total cost = monthly payment × term months.
- **If monthly payment ≤ monthly interest**: Cap at 360 months (30 years) — the debt is effectively never repaid at that rate.

## What Not To Do

- Do not edit `_shared/slate-cs24-tokens.css` unless explicitly asked — it's the shared foundation
- Do not add npm dependencies or build tools to prototypes
- Do not use absolute paths — all links must be relative
- Do not hard-code colour or font values — always use CSS custom properties
- Do not create documentation files (README, etc.) unless asked
- Do not present settlement figures as something ClearScore generates or controls
- Do not use generic placeholder data — use realistic UK creditor names and amounts

## Versioning Prototypes

Name prototype files with a version prefix and descriptor:
- `v1-pre-confirmation.html` — first version, pre-confirmation screen
- `v2-with-debt-selector.html` — second version, adds debt selection
- `v1-post-confirmation.html` — first version of a different screen

This makes it easy to compare iterations side by side and link specific versions to stakeholders.

## Deployment

The repo uses GitHub Pages deployed from the `main` branch. To ship changes:

```
git add <files>
git commit -m "describe what changed"
git push
```

Changes go live within a couple of minutes. The live URL pattern is:
`https://omariwhyne20.github.io/clearer-prototypes/projects/<project-name>/<file>.html`
