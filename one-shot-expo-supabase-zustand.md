# One-shot LLM Prompt — Expo + Supabase + Zustand (ZemNet)

Use this prompt to build out the **complete ZemNet WiFi marketplace app** in the ZemwifiApp workspace.

## Current workspace state

The ZemwifiApp workspace at `/Users/malickdes/worksapace/ZemwifiApp` already has:

### ✅ Completed
- Expo project initialized with TypeScript
- Basic routing structure (`app/(tabs)`)
- Supabase client configured (`src/lib/supabase.ts`)
- Initial Zustand stores: `authStore`, `cashInStore`, `discoveryStore`, `purchasesStore`, `walletStore`
- Core types defined (`src/types/domain.ts`)
- Error handling utilities (`src/lib/errors.ts`)
- AsyncStorage persistence (`src/lib/storeStorage.ts`)
- Basic UI components (`components/`)
- Dependencies installed: `@supabase/supabase-js`, `zustand`, `@react-native-async-storage/async-storage`

### 📋 Documentation available
- Product spec: `Prompt-repo/zemNet.md`
- App build spec: `Prompt-repo/zemNet-expo-build-prompt.md`
- Repo standards: `Prompt-repo/constitution.md`
- Supabase backend contract: `Prompt-repo/supabase/migrations/*`

### 🔨 Needs implementation
- Complete auth flow (welcome, phone, OTP, profile screens)
- All user screens (map, list, hotspot details, payment flow, wallet, history)
- All host screens (dashboard, setup, earnings, payouts, cash-in)
- Technician screens
- Shared screens (settings, support, legal)
- Full Zustand store logic and Supabase integration
- i18n system (French/English)
- QR code functionality
- Complete UI components

---

## Non‑negotiable instructions (read carefully)

1. **Build upon the existing workspace structure** at `/Users/malickdes/worksapace/ZemwifiApp`
2. **No placeholders / no TODOs** for core functionality. If something must be mocked (payments, router captive portal), implement the mock fully.
3. **Follow repository standards** from `Prompt-repo/constitution.md`.
4. **Backend is Supabase** and **state is Zustand** (already configured).
5. **Do not invent database columns or table names**. Use the SQL in `Prompt-repo/supabase/migrations/*` as the contract.
6. **Environment variables** must use exactly:
   - `EXPO_PUBLIC_SUPABASE_URL`
   - `EXPO_PUBLIC_SUPABASE_KEY`
7. Do **not** include any service role keys. Client uses publishable/anon only.
8. **Preserve existing files** unless they need modification for the full implementation.
9. Use the existing Zustand stores as starting points and expand them with full logic.

---

## Implementation approach

Since the workspace is already initialized, you should:

1. **Review existing code** in `src/stores/`, `src/lib/`, and `src/types/`
2. **Extend the app routing** to match the complete structure below
3. **Complete the Zustand stores** with full business logic
4. **Implement all screens** according to `Prompt-repo/zemNet-expo-build-prompt.md`
5. **Add i18n system** for French/English support
6. **Implement UI components** needed for all screens
7. **Add error handling and loading states** throughout

---

## Target file structure (expand from current baseline)

Your implementation must create this complete structure:

```
.
├── app
│   ├── (auth)
│   │   ├── _layout.tsx
│   │   ├── welcome.tsx
│   │   ├── phone.tsx
│   │   ├── otp.tsx
│   │   └── profile.tsx
│   ├── (app)
│   │   ├── _layout.tsx
│   │   ├── (user)
│   │   │   ├── _layout.tsx
│   │   │   ├── map.tsx
│   │   │   ├── list.tsx
│   │   │   ├── hotspot
│   │   │   │   └── [id].tsx
│   │   │   ├── payment
│   │   │   │   ├── method.tsx
│   │   │   │   ├── status.tsx
│   │   │   │   └── success.tsx
│   │   │   ├── wallet
│   │   │   │   ├── index.tsx
│   │   │   │   ├── topup-qr.tsx
│   │   │   │   ├── topup-requests
│   │   │   │   │   ├── index.tsx
│   │   │   │   │   └── [id].tsx
│   │   │   │   └── [voucherId].tsx
│   │   │   ├── history.tsx
│   │   │   └── connect-help.tsx
│   │   ├── (host)
│   │   │   ├── _layout.tsx
│   │   │   ├── start.tsx
│   │   │   ├── kyc.tsx
│   │   │   ├── dashboard.tsx
│   │   │   ├── claim.tsx
│   │   │   ├── setup.tsx
│   │   │   ├── hotspots.tsx
│   │   │   ├── hotspot
│   │   │   │   └── [id].tsx
│   │   │   ├── sessions.tsx
│   │   │   ├── earnings.tsx
│   │   │   ├── payouts.tsx
│   │   │   ├── cashin.tsx
│   │   │   ├── cashin-history.tsx
│   │   │   └── technician-requests
│   │   │       ├── index.tsx
│   │   │       ├── new.tsx
│   │   │       └── [id].tsx
│   │   ├── (technician)
│   │   │   ├── _layout.tsx
│   │   │   └── technician
│   │   │       └── dashboard.tsx
│   │   └── (shared)
│   │       ├── _layout.tsx
│   │       ├── settings.tsx
│   │       ├── support.tsx
│   │       ├── legal.tsx
│   │       ├── about.tsx
│   │       └── transaction-detail
│   │           └── [id].tsx
│   ├── (modal)
│   │   ├── qr.tsx
│   │   └── plan-editor.tsx
│   ├── _layout.tsx
│   └── index.tsx
│
├── src
│   ├── lib
│   │   ├── supabase.ts          [✅ EXISTS - already configured]
│   │   ├── storeStorage.ts      [✅ EXISTS]
│   │   ├── errors.ts            [✅ EXISTS]
│   │   ├── i18n.ts              [🔨 CREATE - translation system]
│   │   ├── format.ts            [🔨 CREATE - formatting utilities]
│   │   └── time.ts              [🔨 CREATE - time/date utilities]
│   ├── stores
│   │   ├── authStore.ts         [✅ EXISTS - expand with full auth logic]
│   │   ├── discoveryStore.ts    [✅ EXISTS - expand with hotspot discovery]
│   │   ├── walletStore.ts       [✅ EXISTS - expand with wallet operations]
│   │   ├── purchasesStore.ts    [✅ EXISTS - expand with purchase flow]
│   │   └── cashInStore.ts       [✅ EXISTS - expand with cash-in logic]
│   ├── components
│   │   ├── ui
│   │   │   ├── Button.tsx
│   │   │   ├── TextField.tsx
│   │   │   ├── Card.tsx
│   │   │   ├── Badge.tsx
│   │   │   └── EmptyState.tsx
│   │   └── AppHeader.tsx
│   └── types
│       ├── domain.ts            [✅ EXISTS - expand if needed]
│       └── index.ts             [🔨 CREATE if needed]
│
├── components                   [✅ EXISTS - current UI components]
│   ├── external-link.tsx
│   ├── haptic-tab.tsx
│   ├── hello-wave.tsx
│   ├── parallax-scroll-view.tsx
│   ├── themed-text.tsx
│   ├── themed-view.tsx
│   └── ui/
│       ├── collapsible.tsx
│       ├── icon-symbol.ios.tsx
│       └── icon-symbol.tsx
│
├── constants
│   └── theme.ts                 [✅ EXISTS]
│
├── assets
│   └── images/                  [✅ EXISTS]
│
├── tests                        [🔨 CREATE]
│   ├── cashin-expiry.test.ts
│   └── voucher-persist.test.ts
│
├── app.json                     [✅ EXISTS]
├── package.json                 [✅ EXISTS]
├── tsconfig.json                [✅ EXISTS]
├── README.md                    [✅ EXISTS - update with ZemNet info]
├── .env.example                 [🔨 CREATE]
└── .gitignore                   [🔨 CREATE if missing]
```

**Legend:**
- ✅ EXISTS: File already in workspace
- 🔨 CREATE: File needs to be created
- No marker: New file to create
│   │   │   │   ├── index.tsx
│   │   │   │   ├── new.tsx
│   │   │   │   └── [id].tsx
│   │   ├── (technician)
│   │   │   └── technician
│   │   │       └── dashboard.tsx
│   │   ├── (shared)
│   │   │   ├── settings.tsx
│   │   │   ├── support.tsx
│   │   │   ├── legal.tsx
│   │   │   ├── about.tsx
│   │   │   └── transaction-detail
│   │   │       └── [id].tsx
│   ├── (modal)
│   │   ├── qr.tsx
│   │   └── plan-editor.tsx
│   ├── _layout.tsx
│   └── index.tsx
│
├── src
│   ├── lib
│   │   ├── supabase.ts
│   │   ├── i18n.ts
│   │   ├── format.ts
│   │   └── time.ts
│   ├── stores
│   │   ├── authStore.ts
│   │   ├── discoveryStore.ts
│   │   ├── walletStore.ts
│   │   ├── purchasesStore.ts
│   │   └── cashInStore.ts
│   ├── components
│   │   ├── ui
│   │   │   ├── Button.tsx
│   │   │   ├── TextField.tsx
│   │   │   ├── Card.tsx
│   │   │   ├── Badge.tsx
│   │   │   └── EmptyState.tsx
│   │   └── AppHeader.tsx
│   └── types
│       └── index.ts
│
├── scripts
│   └── scaffold.mjs
├── tests
│   ├── cashin-expiry.test.ts
│   └── voucher-persist.test.ts
│
├── app.json
├── package.json
├── tsconfig.json
├── README.md
├── .env.example
└── .gitignore
```

---

## Current dependencies (already installed)

The workspace has these dependencies configured in package.json:

**Core:**
- `expo@~54.0.30`, `expo-router@~6.0.21`
- `react@19.1.0`, `react-native@0.81.5`
- `typescript@~5.9.2`

**State & Storage:**
- `zustand@^5.0.9`
- `@react-native-async-storage/async-storage@^2.2.0`
- `@supabase/supabase-js@^2.89.0`

**Navigation & UI:**
- `@react-navigation/native@^7.1.8`
- `@react-navigation/bottom-tabs@^7.4.0`
- `@expo/vector-icons@^15.0.3`
- `expo-haptics@~15.0.8`
- `expo-symbols@~1.0.8`

### Additional libraries needed

Add these for full functionality:

- QR code library: `react-native-qrcode-svg` or similar Expo-compatible library
- Map library if using native maps: `react-native-maps` (or use web-based map for simplicity)
- Testing: `jest`, `@testing-library/react-native` (optional but recommended)

---

## Supabase backend contract

The workspace includes SQL migrations as the authoritative backend contract:

- `Prompt-repo/supabase/migrations/001_initial_schema.sql`
- `Prompt-repo/supabase/migrations/002_rls_policies.sql`
- `Prompt-repo/supabase/migrations/003_functions_and_triggers.sql`
- `Prompt-repo/supabase/migrations/004_seed_data.sql`
- `Prompt-repo/supabase/migrations/005_admin_features.sql`
- `Prompt-repo/supabase/migrations/006_ratings.sql`

Refer to `Prompt-repo/supabase/README.md` and `SCHEMA_DIAGRAM.md` for detailed documentation.

### Required Supabase usage

- **Supabase client** is already initialized in `src/lib/supabase.ts`
- Use Supabase Auth for sign-in:
  - Preferred: phone OTP
  - Fallback: email OTP (document if used)
- Discovery (guest) reads use public RLS policies:
  - Online hotspots and active plans
- Authenticated reads respect RLS:
  - User vouchers, purchases, transactions, wallet
- All mutations must respect RLS policies defined in migrations

---

## Zustand rules

The workspace has initial store files that need expansion:

### Existing stores (expand these)

1. **authStore.ts** - Currently has basic structure
   - Add: Full phone/email OTP flow
   - Add: Profile management
   - Add: Session persistence and refresh
   - Keep: Language preference (already implemented)

2. **discoveryStore.ts** - Needs full implementation
   - Add: Fetch online hotspots from Supabase
   - Add: Filter by location/distance
   - Add: Cache hotspot data
   - Add: Guest mode support

3. **walletStore.ts** - Needs full implementation
   - Add: Balance management
   - Add: Voucher CRUD operations
   - Add: Local voucher persistence for offline access
   - Add: Transaction history

4. **purchasesStore.ts** - Needs full implementation
   - Add: Plan selection and purchase flow
   - Add: Payment state machine
   - Add: Voucher generation (wallet or mobile money)
   - Add: Purchase history

5. **cashInStore.ts** - Needs full implementation
   - Add: Cash-in request creation
   - Add: Confirmation flow
   - Add: Expiry tracking
   - Add: Balance updates

### Persistence strategy (already configured)

- Uses `zustand/middleware` `persist` with `AsyncStorage`
- Storage wrapper exists: `src/lib/storeStorage.ts`
- **Persist:** vouchers, purchases, wallet balance, language
- **Do not persist:** loading states, UI flags, error messages

---

## App requirements

Implement the complete ZemNet app per `Prompt-repo/zemNet-expo-build-prompt.md`.

### Key features to implement

**Authentication:**
- Welcome screen with language selection
- Phone number input with country code
- OTP verification
- Profile creation/editing
- Guest mode for discovery

**User flows:**
- Browse hotspots (map + list views)
- View hotspot details and plans
- Select plan and complete payment
- Manage wallet and vouchers
- View purchase/transaction history
- Generate QR codes for voucher sharing
- Request cash-in top-ups
- Connect help/support

**Host flows:**
- Host registration and KYC
- Hotspot setup and configuration
- Dashboard with stats
- Session monitoring
- Earnings tracking
- Payout requests
- Cash-in management
- Technician request system

**Technician flows:**
- Dashboard for assigned requests
- Request management

**Shared:**
- Settings (profile, language, notifications)
- Support and help
- Legal/terms/privacy
- About/version info

### Technical requirements

- **Offline-first:** Cache vouchers and key data locally
- **Error handling:** Comprehensive error states and user feedback
- **Loading states:** For all async operations
- **Empty states:** For lists and data views
- **i18n:** French and English (switchable in settings)
- **Responsive:** Works on various screen sizes
- **Accessibility:** Proper labels and touch targets

---

## Definition of Done

The implementation is complete when:

1. ✅ **Project runs:** `npx expo start` works without errors
2. ✅ **Guest browsing:** Can browse hotspots without login
3. ✅ **Auth flow:** Phone/email OTP and profile creation works end-to-end
4. ✅ **Plan purchase:** User can select plan and complete payment state machine
5. ✅ **Voucher creation:** Voucher is created in Supabase and cached locally
6. ✅ **Offline access:** Vouchers persist and are accessible offline
7. ✅ **Cash-in flow:** Host creates request, user confirms, wallet updates
8. ✅ **i18n works:** French/English toggle changes all UI text
9. ✅ **Error/loading states:** Comprehensive feedback throughout app
10. ✅ **Empty states:** Proper empty states for all list views
11. ✅ **Host flows:** Dashboard, setup, and management screens functional
12. ✅ **Navigation:** All routes work correctly with expo-router
13. ✅ **Type safety:** No TypeScript errors
14. ✅ **Tests:** Basic smoke tests exist and pass (optional but recommended)

---

## Implementation strategy

### Phase 1: Core infrastructure (if not complete)
1. Review and expand existing Zustand stores
2. Implement i18n system (`src/lib/i18n.ts`)
3. Create utility functions (format, time)
4. Build UI component library (`src/components/ui/`)

### Phase 2: Authentication
1. Create auth screens (`app/(auth)/`)
2. Implement full auth flow in authStore
3. Handle session persistence and refresh
4. Add navigation guards

### Phase 3: User features
1. Discovery screens (map, list)
2. Hotspot detail and plan selection
3. Payment flow (method, status, success)
4. Wallet management
5. History and transaction details

### Phase 4: Host features
1. Host onboarding (start, KYC)
2. Dashboard and stats
3. Hotspot management
4. Earnings and payouts
5. Cash-in system

### Phase 5: Polish
1. Shared screens (settings, support)
2. Error boundaries
3. Loading optimizations
4. Testing
5. Documentation updates

---

## Environment setup

Create `.env.example` with:

```env
EXPO_PUBLIC_SUPABASE_URL=your-project.supabase.co
EXPO_PUBLIC_SUPABASE_KEY=your-anon-key
```

Users should copy to `.env` with their actual credentials.

---

## Final instruction

Build out the complete ZemNet application in the existing workspace at `/Users/malickdes/worksapace/ZemwifiApp`. 

**Approach:**
- Review all existing code first
- Expand existing stores and components  
- Create all missing screens and features
- Follow the phase approach for systematic implementation
- Test incrementally as you build
- Document any assumptions or limitations

**Do not:**
- Delete or break existing working code
- Ask for clarification (make reasonable assumptions)
- Leave placeholders or TODOs
- Skip error handling or loading states
