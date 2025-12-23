# Figma Make — Phase 2 Build Prompt (Ready to Paste)

Use this prompt in **Figma Make** to generate the full working prototype based on the Phase 1 spec below.

---

## Build rules (non‑negotiable)

- **Accessibility:** meet WCAG 2.1 AA (labels, focus states, contrast, keyboard support).
- **Reusable components:** build a small component library first and reuse it everywhere.
- **Layout:** avoid absolute positioning for layout; use Flexbox/Grid.
- **Real UI:** build code UI components (no image/screenshot-based UI).
- **Clean architecture:** keep code maintainable and consistent.
- **Responsive:** support mobile + desktop (define breakpoints and apply them consistently).
- **States everywhere:** for each data surface include loading/empty/error/success states.

---

## What to build

Build a complete application prototype exactly from the specification below.

### Implementation expectations (sequence)

1. **Create the design tokens + base UI kit first** (colors, type scale, spacing, radii, shadows, focus ring).
2. **Create reusable components** (Button, Inputs, Cards, Lists/Tables, Modals/Drawers, Toasts, Tabs, Badges, EmptyState, etc.).
3. **Create shared layout primitives** (AppShell with header/tab bar, page container, section headers).
4. **Implement screens** as separate pages/components using reusable pieces.
5. **Wire interactions** so the prototype feels real:
   - navigation between screens
   - form validation
   - modals/drawers
   - toasts
   - loading/empty/error states
6. **Use consistent placeholder data** aligned with the “Data shown” examples.
7. If the spec has gaps, **make the smallest reasonable assumption**, list it, and continue.

---

## Phase 1 Spec (source of truth)

> Paste-in provided from `app-phase1.txt`.
> If any section appears incomplete (e.g., missing Design System tokens), infer a cohesive system and note assumptions.

```text
1) App Summary
App Type & Purpose

ZemNet is a community Wi-Fi access marketplace for Burkina Faso. It enables Hosts (Wi-Fi owners) to sell short internet access passes and Users to discover nearby hotspots, pay via mobile money or platform wallet credit, receive a voucher, and connect through a captive portal. Access control is enforced locally on the router (OpenWrt + openNDS) using offline-verifiable vouchers, so connections remain reliable even when mobile data is weak.

Non-goals (out of scope for v1)

A full Admin mobile application (Ops is web-first; minimal internal tools only).

Full offline payment processing (payments require provider confirmation; only voucher validation is offline).

Advanced fraud/ML, automated chargebacks, complex dispute workflows (basic manual tools only).

Multi-currency and tax-grade accounting.

Roaming federation (Passpoint/Hotspot 2.0) and RADIUS-based enterprise authentication.

Ed25519/COSE voucher signing (v1 uses HS256; upgrade later).

2) Users & Roles
Guest (not logged in)

Can discover hotspots (map/list) without login.

Cannot purchase until logged in (recommended), or can purchase with minimal OTP step at checkout.

User (Buyer)

OTP login, profile basics.

View hotspot details (GPS pin + landmark text) and host-defined plans.

Purchase via Wave/Orange/Moov or pay with Wallet Credit.

Store vouchers offline; open connect help; copy code / view QR.

View purchase history and wallet ledger.

Receive and confirm cash-in requests initiated by hosts.

Host (Seller)

Complete KYC + payout method.

Claim router via QR and configure hotspot metadata.

Create/update host-defined plans; pause sales.

Accept cash and initiate cash-in to credit a user’s wallet (expires in 10 minutes).

View cash-in history, sessions (approx), earnings, payouts.

Admin/Ops (optional, web-first)

Approve/reject KYC; freeze/unfreeze hosts.

Configure platform fee rates, cash-in commission rates, limits.

Review suspicious cash-ins; manual reversals/refunds.

Run payout batches and troubleshoot failures.

3) Core Features (5–7)

Hotspot Discovery (No Login Required)

Map and low-data list of nearby online hotspots using GPS pins + landmark-only descriptions.

Host-Defined Plans & Sales Controls

Hosts create and manage pricing plans (time/data/price), and can pause/resume sales.

Pass Purchase (Mobile Money + Wallet Credit)

Users pay via Wave/Orange/Moov or spend wallet credit; voucher is delivered instantly after confirmation.

Platform Wallet Credit (Cash-In + Spend Anywhere)

Any KYC-approved host can accept cash and initiate a wallet credit for a user; the user confirms; credit is usable at any host.

Policy: Wallet credit is not refundable to cash.

Offline Voucher Wallet + Captive Portal Connect

Vouchers stored securely on-device; users can connect even when the app has no internet (router validates offline).

One-Device-Per-Voucher Enforcement

Each voucher can be used by exactly one device (MAC binding on first use, enforced by the router).

Earnings & Payouts

Hosts see sales/fees/commission summaries and receive scheduled payouts; payout states are transparent.

4) Primary User Journeys (at least 2)
Journey A — Discover → Buy pass → Connect (Happy Path)

Guest opens app → sees hotspots on Map/List (no login).

Select hotspot → view host-defined plans → choose plan.

App prompts OTP login to purchase (if not logged in).

Choose payment method (Wave/Orange/Moov or Wallet).

On success → voucher shown (QR + code) and saved to wallet.

User joins SSID → captive portal opens → enters voucher.

Router validates voucher offline; binds voucher to device (first MAC); grants access.

Edge case: Payment is completed but webhook confirmation is delayed → Payment Status shows “En attente” with refresh, “J’ai payé”, and Support link; voucher appears once confirmed.

Journey B — Cash top-up at Host A → Spend at Host B (Happy Path)

User opens Wallet → shows Top-up QR (user identifier).

Host A selects “Recharger un client” → scans QR or enters phone → enters amount → collects cash.

Cash-in request created (expires in 10 minutes).

User receives notification/request → confirms.

Wallet balance increases by the full cash amount.

User buys a pass at Host B using Wallet → voucher issued → connect through portal.

Edge case: User does not confirm within 10 minutes → request expires; host sees “Expiré” and can re-initiate.

5) Information Architecture (IA) (site map / screen list)

Routes shown for Expo Router. “Label” refers to tab label where applicable.

Auth & Onboarding

Welcome / Mode Select — /(auth)/welcome — Language + brief intro.

Phone Number — /(auth)/phone — Start OTP.

OTP Verify — /(auth)/otp — Verify & sign in.

Profile Setup — /(auth)/profile — Name/consents (optional).

User Mode (Tabs)

Map — /(app)/(user)/map (Tab: “Carte”) — Nearby hotspots (pins).

List — /(app)/(user)/list (Tab: “Liste”) — Low-data discovery.

Hotspot Details — /(app)/(user)/hotspots/[id] — Plans + buy.

Wallet — /(app)/(user)/wallet (Tab: “Portefeuille”) — Balance + vouchers.

Top-up QR — /(app)/(user)/wallet/topup-qr — Show QR/ID for cash-in.

Top-up Requests — /(app)/(user)/wallet/topup-requests — Pending confirmations.

Top-up Request Details — /(app)/(user)/wallet/topup-requests/[id] — Confirm/deny.

Voucher Details — /(app)/(user)/wallet/[voucherId] — QR/code + expiry.

History — /(app)/(user)/history (Tab: “Historique”) — Purchases/receipts.

Connect Help — /(app)/(user)/connect-help — Captive portal guide.

Payment Method — /(app)/(user)/payment/method — Provider vs Wallet.

Payment Status — /(app)/(user)/payment/status — Pending/success/fail.

Payment Success — /(app)/(user)/payment/success — Voucher issued.

Host Mode (Tabs)

Host Start — /(app)/(host)/start (Tab: “Hôte”) — Become host.

KYC — /(app)/(host)/kyc — Identity + payout setup.

Host Dashboard — /(app)/(host)/dashboard — Online + KPIs.

Claim Router — /(app)/(host)/claim — QR claim.

Hotspot Setup — /(app)/(host)/setup — Name/landmark/hours/limits.

Hotspot Management — /(app)/(host)/hotspot/[id] — Plans + sales toggle.

Plan Editor (Modal) — /(modal)/plan-editor — Create/edit plan.

Sessions Monitor — /(app)/(host)/sessions — Session list.

Earnings — /(app)/(host)/earnings — Revenue/fees/commissions.

Payouts — /(app)/(host)/payouts — Payout list/status.

Top-up Customer (Cash-in) — /(app)/(host)/cashin — Credit user wallet.

Cash-in History — /(app)/(host)/cashin/history — Cash-in records.

Shared

Settings — /(app)/(shared)/settings — Language/cache/notifications.

Support — /(app)/(shared)/support — WhatsApp/phone + FAQ.

Legal — /(app)/(shared)/legal — Terms/AUP/Privacy.

About — /(app)/(shared)/about — Version/build.

Modals

Plan Picker — /(modal)/plan-picker — Select plan.

QR Fullscreen — /(modal)/qr — Voucher/top-up QR fullscreen.

6) Screen-by-screen Specs (for EVERY screen)
6.1 Welcome / Mode Select

Purpose: Language selection and short intro.

Primary actions: Select language; Continue as User; Continue as Host.

Layout regions: Header (logo), Main (value props), Footer (CTAs).

Key components: LanguageToggle, FeatureCard, PrimaryButton.

Data shown: “Achetez un pass Wi-Fi près de vous.” / “Partagez votre Wi-Fi et gagnez.”

Validation rules: None.

States: Loading n/a; Empty n/a; Error n/a; Success → Phone Number.

Navigation: Entry → Phone Number.

Accessibility notes: 44px targets; toggle announced; clear CTA labels.

6.2 Phone Number

Purpose: Capture phone for OTP.

Primary actions: Enter phone; Continue; Change country code.

Layout regions: Header back; Main form; Footer continue.

Key components: PhoneInput, HelperText, Toast.

Data shown: Default +226; example formatting.

Validation rules: Required; numeric; length; rate-limit messaging.

States: Loading (request OTP); Empty n/a; Error (invalid/rate-limited); Success → OTP.

Navigation: From Welcome → OTP Verify.

Accessibility notes: Label + hint; error announced; numeric keypad.

6.3 OTP Verify

Purpose: Verify OTP and authenticate session.

Primary actions: Enter code; Verify; Resend.

Layout regions: Header; Main OTP; Footer actions.

Key components: OTPInput(6), Timer, Toast.

Data shown: Masked phone; resend countdown.

Validation rules: 6 digits; resend cooldown.

States: Loading (verify); Empty n/a; Error (wrong/expired); Success → Profile Setup or App.

Navigation: Phone → OTP → Profile/App.

Accessibility notes: Auto-advance; screen reader “digit 1 of 6”.

6.4 Profile Setup

Purpose: Optional name + accept legal.

Primary actions: Save; Skip; Open Legal.

Layout regions: Header; Main form; Footer.

Key components: TextInput, Checkbox, Link.

Data shown: Name; consent state.

Validation rules: Consent required if enforced.

States: Loading (save); Empty n/a; Error (network); Success → app home.

Navigation: OTP → Profile → User/Host home.

Accessibility notes: Checkbox labeled; links accessible.

6.5 Hotspots Map (Guest allowed)

Purpose: Discover nearby hotspots via GPS pins.

Primary actions: Refresh; Select pin; Change radius.

Layout regions: Header controls; Map; Bottom sheet preview.

Key components: MapView, Marker, BottomSheet, FilterChips, EmptyState.

Data shown: Name, distance, “À partir de 100 XOF”, online badge, landmark snippet.

Validation rules: Location permission; fallback to manual city selection if denied (optional).

States: Loading (fetch); Empty (none nearby); Error (location denied/API); Success (pins).

Navigation: Map → Hotspot Details; tabs to Wallet/History/Support.

Accessibility notes: Provide list alternative; markers have accessible labels.

6.6 Hotspots List (Guest allowed)

Purpose: Low-data discovery list.

Primary actions: Sort; Select hotspot; Refresh.

Layout regions: Header sort/filter; List.

Key components: ListItem, Badge, Skeleton, EmptyState.

Data shown: Same as map rows.

Validation rules: None.

States: Loading; Empty; Error; Success.

Navigation: List → Hotspot Details.

Accessibility notes: Entire row tappable; announces distance + price.

6.7 Hotspot Details

Purpose: Display hotspot info (GPS + landmark) and host-defined plans.

Primary actions: Choose plan; Buy; Open Connect Help.

Layout regions: Header; Main details; Plans; Sticky CTA.

Key components: PlanCard, StatusPill, InfoRow, CTAButton.

Data shown: Hotspot name; landmark text; plan list (duration/data/price); online state.

Validation rules: Plan active; hotspot online (or allow pre-buy with warning).

States: Loading (plans); Empty (no plans); Error; Success.

Navigation: Details → Plan Picker → Payment Method.

Accessibility notes: Plan cards have radio semantics; CTA announces price.

6.8 Plan Picker (Modal)

Purpose: Confirm selected plan.

Primary actions: Select plan; View details; Continue.

Layout regions: Modal header; Plan list; Footer.

Key components: RadioCardGroup, PriceSummary, Button.

Data shown: Plan name, seconds, bytes, price XOF.

Validation rules: Exactly one selected.

States: Loading; Empty; Error; Success → Payment Method.

Navigation: Hotspot Details → Plan Picker → Payment Method.

Accessibility notes: Focus trap; close button first.

6.9 Payment Method

Purpose: Choose wallet or mobile money provider.

Primary actions: Pay with Wallet; Pay with Wave; Pay with Orange/Moov.

Layout regions: Header; Methods list; Footer.

Key components: PaymentMethodCard, BalanceBanner, Toast.

Data shown: Wallet balance; plan price; fee note (if shown).

Validation rules: Wallet must have sufficient balance; otherwise disable and show “Recharger”.

States: Loading; Empty n/a; Error (provider unavailable); Success → Payment Status/Success.

Navigation: Plan Picker → Payment Method → Status/Success.

Accessibility notes: Insufficient balance announced; provider buttons labeled.

6.10 Payment Status

Purpose: Handle provider redirect + pending confirmation.

Primary actions: Open provider; “J’ai payé”; Retry.

```

---

## Required final check before you stop

Before you finalize, output:

- **Screens built:** checklist of every screen from the IA and whether it’s implemented
- **Reusable components built:** checklist
- **Assumptions made:** bullet list
- **Known gaps/TODOs:** bullet list

Then wait for my confirmation to iterate.
