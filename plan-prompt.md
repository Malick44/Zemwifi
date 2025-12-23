# Figma Make — Reusable “Plan → Build” Master Prompt (Template)

Use this file as a reusable, copy/paste prompt you can drop into Figma Make (or any code-gen assistant) to:
1) turn an idea into a complete product spec, and
2) generate a working multi-page prototype using a consistent design system.

---

## How to use

1. Fill in the **App Inputs** section (the bracketed placeholders).
2. Send **Phase 1** to generate the spec.
3. Paste Phase 1 outputs into **Phase 2** and run Phase 2 to build.

If you already have a spec/design system, skip Phase 1 and go straight to Phase 2.

---

## App Inputs (fill these in)

- **App name:** [APP_NAME]
- **Target platform:** [Web / Mobile / Desktop]
- **Primary users:** [e.g., freelancers, students, admins]
- **Primary job-to-be-done:** [what the user is trying to accomplish]
- **Key constraints:** [time, budget, tech constraints, offline, etc.]
- **Tone/brand adjectives:** [e.g., calm, premium, playful]
- **Competitors/inspiration (optional):** [links or names]

### Data & integrations (optional)

- **Auth:** [none / email+password / SSO]
- **Payments:** [none / Stripe]
- **Backend:** [mock data / REST / GraphQL]
- **Storage:** [local only / cloud]
- **3rd-party APIs:** [list]

---

## Phase 1 — Product planning output (spec you can build from)

### Output format (follow strictly)

Return a single structured document with these sections in this exact order:

1. **App Summary**
2. **Users & Roles**
3. **Core Features (5–7)**
4. **Primary User Journeys** (at least 2)
5. **Information Architecture (IA)** (site map / screen list)
6. **Screen-by-screen Specs** (for EVERY screen)
7. **Reusable Components Inventory**
8. **Design System**
9. **Content Style Guide**
10. **Acceptance Criteria**
11. **Open Questions / Assumptions**

### 1) App Summary

Based on our conversation and the App Inputs above, write:

- **App Type & Purpose:** what it is and what problem it solves
- **Non-goals:** explicitly list what is out of scope for v1

### 2) Users & Roles

List roles (e.g., Guest, Member, Admin) and what each can do.

### 3) Core Features (5–7)

List the main features with a 1–2 sentence description each.

### 4) Primary User Journeys

Describe the main user journeys from start to finish (happy path + 1 edge case).

### 5) Information Architecture (IA)

Create a list of screens/pages with:

- **Screen name**
- **Route** (if web) or **Navigation label** (if mobile)
- **One-line purpose**

### 6) Screen-by-screen Specs (repeat for EVERY screen)

For each screen, provide:

- **Screen Name:**
- **Purpose:**
- **Primary actions:** (top 3)
- **Layout regions:** (e.g., header, sidebar, main, secondary panel)
- **Key components:** (cards, tables, forms, modals, toasts, etc.)
- **Data shown:** (fields/columns with example values)
- **Validation rules:** (forms)
- **States:**
	- Loading
	- Empty
	- Error
	- Success
- **Navigation:** where users come from/go next
- **Accessibility notes:** focus order, keyboard interactions, labels

### 7) Reusable Components Inventory

List reusable UI building blocks to create once and reuse everywhere. Include:

- Component name
- Props (inputs)
- Variants
- States

Aim for: Button, Input, Select, Textarea, Checkbox, Toggle, Modal, Drawer, Toast, Card, Badge, Tabs, Table, Pagination, Breadcrumbs, Navbar/Sidebar, EmptyState.

### 8) Design System

Create a complete design guide with tokens that are easy to implement.

#### Color

- **Primary:** #______
- **Secondary:** #______
- **Accent:** #______
- **Neutrals:** (at least 6 steps, e.g., 50–900)
- **Backgrounds:** default, elevated, subtle
- **Text:** primary, secondary, muted, inverse
- **Status:** success/error/warning/info (bg + text)
- **Focus ring:** color + style

#### Typography

- Font family (heading/body)
- Scale: H1/H2/H3/H4/Body/Small/Caption
- Weights: regular/medium/semibold/bold
- Line heights

#### Spacing & layout

- Spacing scale (4px base recommended)
- Grid/container widths (if web)
- Radii (sm/md/lg)
- Elevation/shadows

#### Interaction

- Hover/active/disabled patterns
- Motion (durations/easings)—keep subtle

### 9) Content Style Guide

Define:

- Voice/tone
- Button text conventions (verb + object)
- Form labels and helper text style
- Empty state messaging style
- Error message style (clear + actionable)

### 10) Acceptance Criteria

Provide a checklist that can be used to verify the prototype is “done”:

- All screens implemented
- All primary user journeys possible end-to-end
- All interactive components have hover/focus/disabled states
- Keyboard navigation works for all interactive elements
- Loading/empty/error states exist for every data surface
- Layout is responsive (define breakpoints)

### 11) Open Questions / Assumptions

If anything is unclear, ask up to 10 questions. If you must assume, list assumptions explicitly.

---

## Phase 2 — Build the full prototype in Figma Make (paste spec outputs here)

### Build rules (non-negotiable)

- **Accessibility:** meet WCAG 2.1 AA (labels, focus states, contrast, keyboard support).
- **Reusable components:** build a small component library first and reuse it.
- **Layout:** avoid absolute positioning for layout; use Flexbox/Grid.
- **Real UI:** build code components (no screenshot/image-based UIs).
- **Clean architecture:** keep code maintainable and consistent.
- **Responsive:** support mobile + desktop (define breakpoints).

### What to build

You will build a complete app prototype from the spec below.

#### PROJECT OVERVIEW
[PASTE “App Summary / Users / Features / Journeys / IA” FROM PHASE 1]

#### SCREEN-BY-SCREEN SPECS
[PASTE “Screen-by-screen Specs” FROM PHASE 1]

#### REUSABLE COMPONENTS INVENTORY
[PASTE “Reusable Components Inventory” FROM PHASE 1]

#### DESIGN SYSTEM
[PASTE “Design System” FROM PHASE 1]

### Implementation expectations

1. **Start by generating the base UI kit** (tokens + core components) before building screens.
2. **Create each screen as its own component/page** using the shared layout and shared components.
3. **Use realistic placeholder data** consistent across screens.
4. **Wire interactions** so the prototype feels real:
	 - navigation between screens
	 - form validation
	 - modals/drawers
	 - toasts
	 - empty/loading/error states
5. **Document key decisions** (briefly) if the spec has gaps.

### Quick iteration loop (so we don’t drift)

Before finalizing, present:

- a list of screens built
- a list of reusable components created
- any assumptions made
- any TODOs that remain

Then wait for my confirmation to iterate.

---

## Optional: Mini “single-feature” version (when you want to move fast)

If you want a smaller prompt for quick prototypes, use this:

- Build **only** these screens: [LIST]
- Focus on **only** these journeys: [LIST]
- Reuse a minimal component set: Button, Input, Card, Modal, Toast, Table/List
- Still include loading/empty/error states and keyboard accessibility