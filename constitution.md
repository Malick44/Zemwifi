# ZemNet Prompt Repo Constitution
<!--
This constitution governs how we write specifications and prompts in this repository.

Objective: produce LLM-ready prompts that reliably generate a runnable Expo (React Native) app,
with minimal ambiguity and strong verification.
-->

## Core Principles

### I. Spec-as-Contract (Single Source of Truth)
Every build prompt/spec is a contract:

- Pick a **primary spec** (e.g., `zemNet.md`) and treat it as the source of truth.
- Derived prompts must **not drift**. If there’s a conflict, update the prompt or the spec.
- Routes, roles, and terminology must match the source spec.
- Scope must be explicit: include **non-goals** and what is mocked/simulated.

### II. Buildability Over Beauty
We optimize for runnable prototypes:

- Prefer Expo defaults: **Expo + TypeScript + Expo Router**.
- Prefer fewer dependencies; add libraries only to reduce ambiguity (navigation, i18n, QR, Supabase client, Zustand).
- Every prompt must specify the expected deliverables and a minimal validation path.
- UI polish is welcome, but never instead of completing flows.

### III. Validation-First (NON-NEGOTIABLE)
Outputs must be verifiable:

- Each prompt must include **acceptance criteria** as a checklist.
- Require at least **two minimal automated checks** for high-risk logic (e.g., persistence, expiry timers).
- If proper tests aren’t feasible, require an alternative smoke-check script and a short explanation.

### IV. Flows > Screens
Success is measured by journeys, not page count:

- Primary journeys must complete end-to-end (e.g., discover → buy → receive voucher; host cash-in → user confirm → wallet updates).
- Each major journey must include at least one **edge case** (pending payment, expired cash-in request, insufficient wallet balance).
- Navigation transitions must be unambiguous (“from → to”).

### V. Simplicity, Safety, and Localization
Keep v1 simple, safe, and Burkina Faso‑context friendly:

- Never include secrets or real payment credentials.
- Payments are simulated; router/captive portal integration is represented via guidance screens.
- Offline-friendly storage: vouchers remain viewable without network.
- French-first + English: all user-facing strings are centralized.
- Accessibility: labels, helpful errors, touch targets, contrast.

---

## Prompt Writing Standard (Required Sections)

Every new build prompt/spec must include these sections in this order:

1. What you are building (summary + non-goals)
2. Tech constraints (platform, navigation, offline, i18n)
3. Routes & navigation map
4. Data model (types) + mock data expectations
5. Backend contract (Supabase)
6. State management & persistence
7. Screen-by-screen requirements (incl. loading/empty/error/success states)
8. UI system (tokens + core components)
9. Deliverables
10. Acceptance criteria
11. Assumptions

> Notes on section 5 (Backend contract):
> - Include Supabase tables (at minimum: users/profiles, hotspots, plans, vouchers, purchases, cash_in_requests).
> - Specify relationships, indexes, and any computed fields.
> - Include RLS policy intent per table (who can read/write).
> - Include a seed strategy for dev/prototyping.

---

## Additional Constraints (Expo App Targets)

- **Navigation:** Expo Router folder-based routing.
- **Backend:** Supabase is the default backend for all generated apps in this repo.
- **State management:** Zustand is the default client-side state management library.
- **Persistence:** Use Zustand persistence for offline-friendly UX (AsyncStorage as default; SecureStore where appropriate; choice must be justified).
- **Maps:** Allowed to use `react-native-maps` or a map placeholder UI if maps add too much build overhead.
- **QR:** Use an Expo-compatible QR generator.
- **Offline mode:** The app may read cached data while offline; writes should queue or gracefully fail with actionable messaging.
- **Assets:** No copyrighted logos/imagery; use placeholders.

### Supabase requirements (non-negotiable)

- **Auth:** Supabase Auth (phone OTP is preferred for ZemNet; if phone OTP is not feasible in the target environment, fall back to email OTP and document the gap).
- **Database:** Postgres tables must be defined (SQL migrations or a schema section in the prompt).
- **RLS:** Row Level Security must be enabled with policies that match roles (guest/user/host/admin as applicable).
- **Edge Functions:** Optional; only if it reduces client complexity (e.g., payment simulation webhook endpoint). Keep it minimal.
- **Env vars:** Prompts must instruct using `EXPO_PUBLIC_SUPABASE_URL` and `EXPO_PUBLIC_SUPABASE_KEY`.
- **Seed data:** Provide seed instructions or a seed script so the app is usable after setup.

### Zustand requirements (non-negotiable)

- Stores must be organized by domain (e.g., `authStore`, `hotspotsStore`, `walletStore`).
- The prompt must specify what is persisted (e.g., vouchers, user profile, last-known hotspots) vs what is ephemeral (e.g., transient UI state).
- Side effects (Supabase reads/writes) must be implemented as store actions or thin service functions called by stores.
- Persisted state must include a version key and a simple migration strategy when shapes change.

---

## Workflow & Quality Gates

### Workflow

1. Update spec/prompt first.
2. Update acceptance criteria.
3. Add/update validation checks (tests or smoke scripts).
4. Only then iterate on UI polish.

### Quality gates (for prompt changes)

- Completeness: routes, flows, edge cases are specified.
- Unambiguity: inputs/outputs are clear for major screens and actions.
- Consistency: names match the source spec.
- Safety: no secrets, no real payment credentials, no sensitive PII.

### Quality gates (for generated app expectations)

- App boots without crashes.
- Primary journeys achievable end-to-end.
- Lists and data surfaces have loading/empty/error states.
- i18n toggle changes visible text.
- Supabase connection works (env vars loaded; basic read succeeds).
- RLS is enabled and policies are documented/tested (at least sanity checks).
- Database schema/seed steps are included and reproducible.

---

## Governance

- This constitution supersedes ad-hoc prompting.
- Any breaking change to routes, data shapes, or terminology requires updating:
	- the source spec,
	- derived build prompts,
	- acceptance criteria.
- Amendments should be small and justified; prefer incremental evolution.

**Version**: 1.2.0 | **Ratified**: 2025-12-22 | **Last Amended**: 2025-12-22

