# Clearer Calculator

Pre-confirmation consolidation summary screen — shows a user how consolidating their existing debts with a single loan compares on monthly payment, total cost, and time to debt-free.

## Project Details
- **Name**: Clearer Calculator
- **View Type**: Mobile View
- **Canvas Size**: 428px width (iPhone viewport)
- **Created**: 15/03/2026

## Versions
- `v1-pre-confirmation.html` — First version. Compares 3 existing debts (Barclaycard CC, HSBC loan, Capital One CC) against a Novuna consolidation loan. Shows savings callout, at-a-glance metrics, cash breakdown, debt list, and sticky CTA.

## What This Prototype Tests
- Can we present a consolidation comparison that's clear enough for users to make a confident decision?
- Does surfacing data confidence (verified vs estimated) build trust or create anxiety?
- Is the "at a glance" format the right information hierarchy for pre-confirmation?

## Key Design Decisions
- **Data confidence tags**: Each debt shows whether its data is "Verified" (Open Banking) or "Estimated" (bureau-matched). Expandable explainer at the bottom.
- **Settlement figures omitted**: These come from the lender, not ClearScore. A prototype note calls this out explicitly.
- **Real calculations**: All comparisons use reducing balance formula — changing the mock data updates every metric.
- **Savings callout adapts**: Shows green "estimated total saving" if consolidation saves money, amber warning if it costs more (but monthly payment still drops).

## Files
- `v1-pre-confirmation.html` — Single-file React prototype with all components and calculation logic
