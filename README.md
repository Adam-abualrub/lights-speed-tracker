# lights-speed-tracker — PRD

**Status:** Draft | **Version:** 1.0 | **Date:** 2026-11-11
**Author:** TBD | **Stakeholders:** Builder (dev/design/QA), Reviewer
**Goal:** Portfolio MVP, working demo in 2 weeks | **Storage:** Local-only (no backend)

## Executive Summary

**One-liner:** Log any expense in 3 taps and see remaining budget instantly.

lights-speed-tracker is a mobile-first expense tracker for students, weekly earners, and travelers. The MVP covers quick setup (base currency + weekly/monthly cycle), 3-step expense logging (title → category → amount), and a home dashboard showing remaining balance. Data persists in `localStorage`; no accounts, sync, or bank integration.

**Quick Facts:**
- Target users: students, non-fixed-income workers, travelers
- Problem: overspending from untracked small purchases + rigid monthly-only budgets
- Key metric: activation — % of first-time users completing setup + first expense in ≤60s
- Target: working demo in 2 weeks (static HTML prototype → Vue 3 MVP)

## Table of Contents

1. [Problem Statement](#1-problem-statement)
2. [Goals & Objectives](#2-goals--objectives)
3. [User Personas](#3-user-personas)
4. [User Stories & Requirements](#4-user-stories--requirements)
5. [Success Metrics](#5-success-metrics)
6. [Scope](#6-scope)
7. [Technical Considerations](#7-technical-considerations)
8. [Design & UX Requirements](#8-design--ux-requirements)
9. [Timeline & Milestones](#9-timeline--milestones)
10. [Risks & Mitigation](#10-risks--mitigation)
11. [Dependencies & Assumptions](#11-dependencies--assumptions)
12. [Open Questions](#12-open-questions)
13. [Sign-Off & Change Log](#13-sign-off--change-log)

## 1. Problem Statement

### The Problem

1. **Untracked small spending:** users make frequent small purchases with no fast logging method, so money leaks into non-essential categories.
2. **Rigid budget cycles:** existing tools assume fixed monthly income; weekly earners and students cannot match budgets to pay cadence.
3. **High friction:** current prototype (`index.html`, `budget.html`) is static — no persistence, no transaction create/edit, placeholder copy ("place-holder", "$xxxxx").
4. **Single-currency assumption:** travelers spending in foreign currencies have no explicit base-currency setting.

### Current State

Users rely on memory, notes apps, or spreadsheets. Workaround cost: manual reconciliation at month end; no real-time remaining-balance signal at purchase time.

### Why Now?

Portfolio MVP scope is small enough (3 screens, local-only) to ship a demonstrable Vue 3 app in 2 weeks and prove the 3-tap logging interaction.

## 2. Goals & Objectives

### Business Goals (portfolio context)

1. **G1 — Demonstrable MVP:** reviewer can run the app, complete setup, log an expense, and see the budget update with no errors.
2. **G2 — Prove core interaction:** expense logging completes in ≤10s / 3 steps on mobile viewport.
3. **G3 — Clean cutover:** replace static HTML placeholders with real Vue state + persistence; delete dead markup.

### User Goals

1. Set base currency and budget cycle once, in under 60 seconds.
2. Log any purchase in 3 taps from Home.
3. See remaining balance per cycle at a glance.
4. Organize spending with defaults (Food, Housing, Health) + custom categories.

### Non-Goals

- Becoming a full personal-finance suite (investments, bills, bank sync).
- Real-time FX conversion or financial advice.

## 3. User Personas

### Primary: Student — "Dana, 20, tracks daily snacks/transport"

- Tech savviness: high; mobile-only.
- Behaviors: many small cashless payments daily; checks balance before buying.
- Needs: sub-10s logging; simple category list.
- Pain points: forgets to log if >3 steps; monthly budgets don't match allowance cadence.

> "I just want to type 12k + Food and see what's left this week."

### Secondary: Weekly earner — "Riko, 27, gig/retail, paid Fridays"

- Behaviors: income arrives weekly, irregular amounts; budgets week-to-week.
- Needs: weekly cycle with clear "ends in X days"; manual income entry per cycle.
- Pain points: monthly-only apps overstate available funds mid-month.

### Tertiary: Traveler — "Sinta, 31, short trips, multi-currency spend"

- Behaviors: pays in foreign currency, thinks in home currency.
- Needs: one base currency for totals; MVP records amounts as-entered in base currency (manual conversion by user).
- Pain points: mixed-currency totals without a base reference.

## 4. User Stories & Requirements

### Epic: MVP tracking (P0 unless noted)

#### US-01: Quick setup (base currency + cycle)

```text
As a new user,
I want to set my base currency and budget cycle (weekly/monthly),
So that totals and remaining balance match my pay cadence.
```

Acceptance Criteria:

- [ ] Given first launch, when I complete setup, then base currency and cycle type are persisted and applied to Home/Budgets.
- [ ] Given setup, when currency is unset, then Continue is disabled with inline hint.
- [ ] Given returning launch, when settings exist, then setup is skipped.
- [ ] Supported currencies (MVP): USD, EUR, IDR, JPY, GBP, SGD, AUD — single-select list.

**Priority:** P0 | **Effort:** S

#### US-02: Log expense in 3 steps

```text
As a purchaser,
I want to log title → category → amount in 3 steps,
So that recording takes seconds at checkout.
```

Acceptance Criteria:

- [ ] Given Home, when I submit title + category + amount > 0, then the transaction appears in the list and cycle total updates immediately.
- [ ] Given amount ≤ 0 or empty title, when I submit, then I see an inline error and nothing is saved.
- [ ] Given slow input, when measured on mobile viewport, then happy-path completion is ≤10s (manual test).

**Priority:** P0 | **Effort:** M

#### US-03: Remaining balance on Home

```text
As a budgeter,
I want to see remaining balance for the current cycle on Home,
So that I know what is safe to spend.
```

Acceptance Criteria:

- [ ] Given a cycle limit and logged expenses, when I view Home, then `remaining = limit − spent(current cycle)` in base currency.
- [ ] Given overspend, when remaining < 0, then the UI flags it (color + label, not color alone).
- [ ] Given no transactions, when I view Home, then remaining equals the full cycle limit.

**Priority:** P0 | **Effort:** S

#### US-04: Custom categories

```text
As a user,
I want to create custom spending categories,
So that tracking matches my life beyond Food/Housing/Health.
```

Acceptance Criteria:

- [ ] Given defaults (Food, Housing, Health), when I add a unique name, then it appears in the logging category picker.
- [ ] Given a duplicate name (case-insensitive), when I submit, then I see a duplicate error.
- [ ] Given custom categories, when I reload, then they persist.

**Priority:** P0 | **Effort:** S

#### US-05: Transaction history (P0)

```text
As a user,
I want to view and delete my transactions,
So that I can correct mistakes.
```

Acceptance Criteria:

- [ ] Given logged transactions, when I open Transactions, then I see reverse-chronological list (title, category, amount, date).
- [ ] Given a transaction, when I delete it, then totals and remaining update immediately.
- [ ] Edge case: deleting from a prior cycle does not alter the current cycle total.

**Priority:** P0 | **Effort:** M

#### US-06: Budget cycle overview (P1)

```text
As a weekly/monthly budgeter,
I want to see cycle limit, spent, and days remaining,
So that I can pace spending.
```

Acceptance Criteria:

- [ ] Given a weekly cycle starting Friday, when I view Budgets, then "ends in X days" is correct across week boundaries.
- [ ] Given cycle end passes, when I open the app, then a new empty cycle starts and old transactions remain viewable under history.
- [ ] Given I edit the limit mid-cycle, when saved, then remaining recalculates immediately.

**Priority:** P1 | **Effort:** M

### Functional Requirements

| Req ID | Description | Priority |
|--------|-------------|----------|
| FR-01 | First-run setup: base currency (fixed 7-item list) + cycle type (weekly/monthly) + limit | P0 |
| FR-02 | Log expense: title (required, ≤80 chars), category (required), amount (required, >0, 2dp) | P0 |
| FR-03 | Home dashboard: cycle spent, remaining, transaction count | P0 |
| FR-04 | Categories: defaults Food/Housing/Health + user-created, duplicate-proof | P0 |
| FR-05 | Transactions screen: list, delete; income logging is display-only in MVP (no separate income type) | P0 |
| FR-06 | Budgets screen: limit, spent-by-category, days remaining, edit limit | P1 |
| FR-07 | Persistence: all state in `localStorage` under versioned key; reload-safe | P0 |

### Non-Functional Requirements

| Req ID | Category | Target |
|--------|----------|--------|
| NFR-01 | Performance | First load <2s on desktop; instant (<100ms) logging feedback |
| NFR-02 | Responsive | Mobile-first 360px primary; usable to 1024px without layout breakage |
| NFR-03 | Accessibility | Semantic HTML, visible focus, labeled inputs, contrast ≥4.5:1 for text |
| NFR-04 | Data integrity | Amounts stored as integer minor units; no float rounding errors |
| NFR-05 | Reliability | No data loss on reload; corrupt storage resets to setup with no crash |

## 5. Success Metrics

Framework: HEART-lite (Task Success + Activation); no analytics backend in MVP — verify manually.

- **North Star (demo):** expenses logged per session — reviewer logs ≥3 expenses across ≥2 categories during demo without errors.
- **Activation:** setup completion + first expense in ≤60s (manual stopwatch, 3/3 trials).
- **Task Success:** expense log happy path ≤10s; 100% of valid submissions appear in totals immediately.
- **Quality gate:** 0 console errors during demo path (setup → log → delete → edit budget → reload).
- **Counter-metric:** no placeholder copy remains ("place-holder", "$xxxxx", "Category1").

Events to log if analytics is added later: `setup_completed`, `expense_logged`, `budget_edited`, `category_created`.

## 6. Scope

### In Scope (MVP)

- Setup (currency + cycle + limit), Home dashboard, Transactions list + delete, Budgets overview + edit limit, custom categories, `localStorage` persistence, mobile-first CSS.

### Out of Scope (explicitly excluded)

- Bank/card auto-sync and imports.
- Auth, accounts, multi-device sync.
- Auto FX rates / conversion API (user enters amounts in base currency).
- Advanced reports, charts beyond category totals, CSV export.
- Push notifications, reminders, recurring transactions.
- Income-type tracking (screen label "income/expenses" in old draft is out; MVP tracks expenses against a cycle limit).

### Future Considerations

- Editable transactions, income types, monthly rollover rules, FX API, export, PWA offline.

## 7. Technical Considerations

- **Stack:** Vue 3 + Vite, Vue Router (Home `/`, Transactions `/transactions`, Budgets `/budgets`), vanilla CSS mobile-first. No UI framework; reuse existing classes where sane (`nav-bar`, `budget-box`, `category-box`), delete the rest.
- **State:** single store (Pinia or composable): `settings`, `categories`, `transactions`, `cycles`. Derived: `spentThisCycle`, `remaining`, `daysRemaining`.
- **Data model:**
  - `Transaction { id: string, title: string, categoryId: string, amountMinor: int, createdAt: ISO, cycleId: string }`
  - `Cycle { id: string, type: 'weekly'|'monthly', startISO: string, endISO: string, limitMinor: int }`
  - `Settings { baseCurrency: 'USD'|..., categories: [{id, name, builtin: bool}] }`
- **Cycle logic:** weekly = 7 days from chosen start weekday (default Monday — see OQ-1); monthly = calendar month. New cycle auto-created on boundary; history preserved.
- **Validation:** title trim 1–80 chars; amount parses to minor units, rejects ≤0 / NaN; category must exist.
- **No backend/APIs.** No auth. Single `lights-speed-tracker.v1` storage key + JSON schema guard.

## 8. Design & UX Requirements

- **Screens (3):** Home (remaining + quick log + recent), Transactions (full list + delete), Budgets (limit + spent-by-category + days remaining + edit).
- **Primary flow:** Home → enter title → pick category → enter amount → Save → remaining updates, no navigation needed.
- **Visual:** reuse `budget.html` card pattern (`budget-box`, `centertext`) as the canonical card; convert `.nav-bar` from absolute-positioned `<p>` tags to real router links with active state and ≥44px targets.
- **Copy fixes (required):** replace "Goodmorning Mr Rifky" with neutral greeting, "flyers" typo, "place-holder", "$xxxxx", "Category1/2/3".
- **Accessibility:** `<label>` per input, keyboard-operable picker, error text linked via `aria-describedby`, never color-only status.

## 9. Timeline & Milestones

Target: **2 weeks** from kickoff (portfolio demo).

| Phase | Deliverables | End |
|-------|--------------|-----|
| Setup + data layer | Vite+Vue scaffold, router, store, `localStorage`, setup screen | Day 3 |
| Core logging | Home log flow + validation, Transactions list + delete | Day 7 |
| Budgets + polish | Budgets screen, cycle rollover, copy/CSS cleanup, placeholder purge | Day 10 |
| Demo hardening | Manual pass on metrics (§5), README demo script, freeze scope | Day 14 |

Milestones: Day 3 setup demoable → Day 7 log/delete working → Day 10 cycle-correct → Day 14 frozen demo.

## 10. Risks & Mitigation

| Risk | Impact | Prob. | Mitigation | Owner |
|------|--------|-------|------------|-------|
| Scope creep (reports/FX/auth) | Miss 2-week demo | High | Enforce §6 out-of-scope list; defer to Future | Builder |
| Cycle-boundary bugs (weekly start, month lengths) | Wrong remaining | Med | Centralize date logic + unit-test 4 cases (week cross, month end, limit edit, delete old) | Builder |
| Float rounding on money | Wrong totals | Med | Integer minor units everywhere; format only at render | Builder |
| Static→Vue migration drag (dead CSS/markup) | Bloated code | Med | Delete unused classes post-cutover; no shims | Builder |
| Single-device data loss (cleared storage) | User confusion | Low | Versioned key + corrupt-state fallback to setup | Builder |

## 11. Dependencies & Assumptions

Dependencies: Node + Vite, modern mobile browser; no external APIs or services.

Assumptions:

- Single user, single device; no concurrent editing.
- Amounts entered in base currency (manual conversion for foreign spend).
- Weekly cycle default start Monday (confirm in OQ-1).
- Existing `index.html`/`budget.html`/`index.css` are throwaway prototype, not constraints.

## 12. Open Questions

- [ ] **OQ-1: Weekly start day?** Options: fixed Monday vs. user-pickable. Recommendation: user-pickable, default Monday. Owner: Builder. Needed by: Day 3.
- [ ] **OQ-2: Currency list final?** Draft proposes 7 (USD/EUR/IDR/JPY/GBP/SGD/AUD). Confirm or trim. Owner: Builder. Needed by: Day 3.
- [ ] **OQ-3: Edit transaction, or delete-only in MVP?** Recommendation: delete-only to hold timeline. Owner: Builder. Needed by: Day 7.
- [ ] **OQ-4: Cycle overspend behavior?** Options: warn-only vs. block logging. Recommendation: warn-only. Owner: Builder. Needed by: Day 7.

## 13. Sign-Off & Change Log

| Stakeholder | Role | Status |
|-------------|------|--------|
| TBD | Builder (eng/design/QA) | ⏳ Pending |
| TBD | Reviewer | ⏳ Pending |

| Version | Date | Changes |
|---------|------|---------|
| 0.1 | pre-2026-11-11 | Original draft (problem/users/MVP/screens/Vue) |
| 1.0 | 2026-11-11 | Standard-PR restructure: goals, personas, stories + AC, metrics, scope, tech, UX, timeline, risks, OQs |

## Appendix — Demo Script (2 min)

1. Fresh load → setup (IDR + weekly) → Home shows full remaining.
2. Log `Nasi goreng / Food / 25000` → remaining drops instantly.
3. Add category `Transport` → log second expense.
4. Budgets → edit limit → remaining recalculates.
5. Transactions → delete one → totals correct. Reload → state persists.
