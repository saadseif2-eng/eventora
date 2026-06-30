# Product Requirements Document (PRD)
## Product: **Eventora** — Premium Interactive Invitations & Event Websites

| Field | Value |
|---|---|
| Document version | 1.1 |
| Status | Production-ready draft |
| Author | Lead Product Manager & Chief Software Architect |
| Last updated | June 2026 |
| Audience | Engineering, Design, Marketing, Leadership |
| Supersedes | v1.0 (product formerly named *Evite Studio*) |

> **What changed in v1.1 (architecture upgrade).** Eventora is no longer built on static, pre-baked templates. It now runs on a **reusable design system and modular architecture** — four cooperating engines (**Theme Engine, Layout Engine, Component Engine, Rendering Engine**) that assemble every event website dynamically from reusable components. The AI produces a **structured JSON configuration**, and a frontend **Rendering Engine** converts that JSON into the final interactive website. All v1.0 features are preserved; this revision enhances the foundation beneath them. The full architecture is documented in the new **Section 6A**, with corresponding updates to the AI Engine (§7.4), Site Editor (§7.5), Dashboard (§7.3), Marketplace (§7.15), Admin Panel (§7.16), System Architecture (§9), and Roadmap (§13).

---

## 1. Executive Summary

Eventora is a worldwide SaaS platform that lets anyone create a **premium, interactive event website and matching digital invitation in under 3 minutes** — powered by an AI Design Engine, a modular design system, a creator marketplace, and an integrated guest-management toolkit (RSVP, QR check-in, analytics, payments).

The wedge is **speed-to-beauty**: most competitors force users to choose between fast-but-ugly (generic invite apps) and beautiful-but-slow (hire a designer / DIY website builders). We collapse that trade-off.

**Technical direction (v1.1):** Eventora is explicitly **not** a library of static invitation templates. It is a **reusable design system and modular architecture**. Every published website is generated dynamically by composing **Themes** (visual language), **Layouts** (structural compositions), and **Components** (reusable building blocks) through a **Rendering Engine** driven by **structured JSON configuration**. This makes designs infinitely recombinable, instantly themeable, RTL/LTR-ready, and far more scalable than a fixed template catalog. See **Section 6A**.

**One-line pitch:** *"Describe your event. Get a stunning event website and invitation in 3 minutes. Manage everything in one place."*

---

## 2. Problem Statement

People hosting events face three persistent problems:

1. **Effort vs. quality gap.** Beautiful event sites require time, taste, and tools most hosts don't have. Free tools look cheap; premium results require designers or hours of work.
2. **Fragmentation.** Invitations live in one tool, RSVPs in a spreadsheet, the venue map in a text message, payments in a third app, photos somewhere else. No single source of truth.
3. **No feedback loop.** Hosts rarely know who opened the invite, who's coming, dietary needs, or who actually showed up.

**Opportunity:** A single platform that produces designer-grade output instantly and centralizes the entire guest lifecycle — from "save the date" to post-event gallery.

---

## 3. Goals & Success Metrics

### 3.1 Product Goal
Enable a non-technical host to publish a live, premium event website + invitation in **under 3 minutes** from sign-up.

### 3.2 North Star Metric
**Number of published event sites that receive ≥1 RSVP per week.** (Captures both creation success *and* real-world usefulness.)

### 3.3 Key Results / KPIs

| Category | Metric | Target (Year 1) |
|---|---|---|
| Activation | % of sign-ups who publish a site | ≥ 45% |
| Speed | Median time sign-up → published site | ≤ 3 min |
| Conversion | Free → paid conversion | ≥ 8% |
| Retention | Hosts who create a 2nd event within 12 mo | ≥ 25% |
| Engagement | Median RSVPs per published site | ≥ 30 |
| Marketplace | % of sites using a marketplace/AI-generated design (theme/layout/component) | ≥ 70% |
| Revenue | Blended ARPU | Defined post-pricing test |
| Quality | NPS | ≥ 50 |

### 3.4 Non-Goals (v1)
- Full CRM / email marketing automation suite.
- Native mobile apps (responsive web first; apps on roadmap).
- Ticketing platform parity (basic paid RSVP only in v1).
- Physical print fulfillment (roadmap).

---

## 4. Target Market & Personas

**Market:** Worldwide, all event types. Initial GTM focus on weddings + milestone birthdays (highest willingness to pay, viral guest exposure).

| Persona | Description | Primary need | Willingness to pay |
|---|---|---|---|
| **The Bride/Couple** (Layla & Omar) | Planning a wedding, design-conscious, time-poor | Stunning site, RSVP & guest tracking, multilingual | High |
| **The Milestone Host** (Maria, 40th birthday) | Wants a "wow" invite to impress friends | Fast, beautiful, shareable | Medium–High |
| **The Corporate Organizer** (David, events lead) | Conferences, galas, product launches | Branding, QR check-in, analytics, paid tickets | High (B2B) |
| **The Casual Host** (Sam) | BBQ, baby shower, reunion | Free, dead-simple, mobile | Low (freemium) |
| **The Designer/Seller** | Creates Themes, Layouts & Components to sell | Marketplace earnings | Revenue share |
| **The Guest** | Receives invite | Easy RSVP, info, directions | Free |
| **The Platform Admin** | Internal ops/support | Moderation, support, oversight | Internal |

### Key worldwide requirements
- **i18n**: multi-language UI + RTL support (Arabic, Hebrew).
- **Localization**: dates, timezones, currencies, address formats.
- **Compliance**: GDPR, CCPA, and regional data residency.

---

## 5. End-to-End User Journey (Happy Path, < 3 min)

1. **Sign up** (email / Google / Apple) — 15s
2. **Tell us about your event** — event type, name, date, location, vibe (3–4 questions) — 30s
3. **AI Design Engine generates** — produces a **Theme**, recommends a **Layout** and **Components**, and assembles a **JSON configuration** rendered into 3 complete site+invite concepts — 20s
4. **Pick & tweak** colors/photo/text in live editor — 60s
5. **Publish** to a free subdomain (`yourevent.eventora.com`) — 5s
6. **Share** invitation link / QR / WhatsApp — 10s
7. (Optional) Upgrade for custom domain, paid RSVP, advanced analytics.

Total core path: **~2:20**. The 3-minute promise is a *design constraint*, not just a marketing line — every screen in the path is measured against it.

---

## 6. Information Architecture / Page Map

```
PUBLIC
├── Landing / Marketing site
├── Marketplace (browse, preview)
│   ├── Theme Marketplace
│   ├── Layout Marketplace
│   └── Component Marketplace
├── Pricing
├── Auth (Sign up / Log in / Reset / SSO)
├── Published Event Website (guest-facing, JSON-rendered)
│   ├── Hero + Countdown
│   ├── Story / Schedule / Details
│   ├── Gallery
│   ├── Map / Directions
│   ├── RSVP form
│   ├── Music player
│   └── Gift / Payment (optional)
└── Guest RSVP confirmation page

AUTHENTICATED (HOST)
├── Onboarding wizard
├── Dashboard
│   ├── My Themes
│   ├── My Layouts
│   ├── Drafts
│   ├── Published Websites
│   ├── AI History
│   ├── Assets
│   └── Analytics
├── Event workspace
│   ├── AI Design Engine (Theme → Layout → Components → JSON → Render)
│   ├── Site Editor (Theme controls + Layout + Component canvas)
│   ├── Invitation Generator
│   ├── RSVP Manager (guest list)
│   ├── QR Code center
│   ├── Gallery manager
│   ├── Music manager
│   ├── Map / location setup
│   ├── Analytics
│   ├── Payments / Gifts
│   └── Settings (domain, language, privacy, collaborators)
├── Account & Billing
└── Marketplace (buy Themes/Layouts/Components; for sellers: upload & earnings)

ADMIN (INTERNAL)
└── Admin Dashboard
    ├── Users / content moderation / support / feature flags
    ├── Marketplace approval / payments / payouts / analytics
    ├── Themes / Layouts / Components management
    ├── Renderer Versions
    ├── AI Prompt Versions
    ├── Assets
    └── System Logs
```

---

## 6A. Eventora Design System & Modular Architecture ⭐ (v1.1)

> **Core principle:** Eventora does **not** ship static invitation templates. Every event website is **composed at render time** from reusable, versioned building blocks. A "design" is data, not a frozen HTML file. This section is the architectural contract for the platform.

### 6A.0 The pipeline at a glance

```
User Data ─┐
Theme ─────┤
Layout ────┼──►  JSON Configuration  ──►  Rendering Engine  ──►  Interactive Event Website
Components ┘                                                     (RTL/LTR · Responsive · SEO · A11y)
```

The four engines below are independent, separately versioned services/libraries that cooperate to turn structured input into a live website. The AI Design Engine (§7.4) orchestrates them; the Site Editor (§7.5) lets humans edit the same underlying configuration.

---

### 6A.1 Theme Engine

**Purpose:** Defines the *visual language* of a website — the "skin" — fully decoupled from structure and content. A Theme can be reused across **any** event, layout, or component set.

**A Theme is a structured token set containing:**

| Token | Description / examples |
|---|---|
| **Primary Color** | Brand/lead color; drives accents, key CTAs |
| **Secondary Color** | Supporting color; backgrounds, secondary actions |
| **Typography** | Heading + body font pairing, scale, weights, line-height (script-aware: Latin, Arabic, etc.) |
| **Border Radius** | Global rounding scale (sharp → pill) |
| **Button Style** | Filled / outline / ghost / gradient; size & padding tokens |
| **Card Style** | Surface treatment: flat, bordered, glass, elevated |
| **Shadows** | Elevation scale (none → soft → dramatic) |
| **Animation Preset** | Motion language: none, subtle, lively, cinematic (honors reduced-motion) |
| **Icon Style** | Line, solid, duotone, rounded |
| **Background Style** | Solid, gradient, pattern, image, animated/particle |

**Behavior**
- Themes are **portable**: apply one Theme to many events; swap Themes on a live site without touching content or layout.
- Themes expose **design tokens** (CSS custom properties / JSON) consumed by every component, guaranteeing visual consistency.
- Themes can be **AI-generated**, hand-built in the editor, saved to **"My Themes,"** or sold in the **Theme Marketplace**.
- Theme tokens enforce **accessibility guardrails** (minimum contrast) at creation time.

**User stories**
- As a host, I want to recolor my entire site by switching one Theme.
- As a host, I want to save a Theme and reuse it for my next event.
- As a designer, I want to publish Themes others can buy.

**Edge cases**
- Theme with poor contrast → blocked/auto-corrected before save.
- Theme typography lacks glyphs for the site language (e.g., Arabic) → automatic font fallback within the same style family.
- Applying a "dramatic shadow / lively animation" Theme on low-end devices → graceful degradation via render hints.

**Acceptance criteria**
- Switching a Theme re-skins a site with zero content/layout loss.
- All Theme presets pass WCAG AA for body text by default.

---

### 6A.2 Layout Engine

**Purpose:** Defines the *structure* of a page — the ordered composition of components and their arrangement. A Layout is **theme-agnostic** and **content-agnostic**.

**A Layout is a composition of Components.** Curated starter Layouts include:

| Layout | Character |
|---|---|
| **Luxury Layout** | Spacious, serif-led, gold/jewel accents, cinematic motion |
| **Modern Layout** | Clean grid, sans-serif, bold imagery |
| **Minimal Layout** | Whitespace-heavy, restrained type, few sections |
| **Classic Layout** | Traditional, centered, formal |
| **Islamic Layout** | RTL-first, geometric patterns, Arabic-optimized typography, culturally appropriate ornamentation |
| **Royal Layout** | Ornate, symmetrical, regal palette affinity |
| **Floral Layout** | Botanical motifs, soft, organic framing |
| **Dark Layout** | Dark-surface-first, high-contrast accents |

**Behavior**
- A Layout specifies **which components appear, in what order, with what arrangement** (single-column, split, grid) and responsive rules — but **not** colors/fonts (Theme) or text/photos (content).
- Layouts are **interchangeable**: switch Layout while keeping Theme + content; the engine remaps content into the new structure and flags anything that doesn't fit.
- Layouts are RTL/LTR aware — e.g., the Islamic Layout mirrors for Arabic by default.
- Layouts can be AI-recommended, saved to **"My Layouts,"** or sold in the **Layout Marketplace**.

**User stories**
- As a host, I want to try a different structure without redoing my content.
- As a host planning a wedding in Arabic, I want a layout designed RTL-first.

**Edge cases**
- New Layout has fewer slots than current content → surplus components parked in a "hidden" tray, not deleted.
- Layout expects a component the event lacks (e.g., Gift Registry) → renders an empty, dismissible placeholder.

**Acceptance criteria**
- Switching Layout preserves 100% of content and the active Theme.
- Every shipped Layout renders correctly in both LTR and RTL.

---

### 6A.3 Component Engine

**Purpose:** The reusable building blocks a page is assembled from. **This replaces the concept of "static templates" internally** — pages are now composed from versioned components, each with multiple variants.

**Core component library:**

`Hero` · `Countdown` · `RSVP` · `Gallery` · `Story` · `Timeline` · `Venue` · `Map` · `Gift Registry` · `Footer` · `Music Player` · `FAQ` · `Schedule`

(Extensible: Schedule/Agenda, Sponsors, Custom Block, etc.)

**Behavior**
- **Every component supports multiple variants** — e.g., Hero: *full-bleed photo*, *split*, *video*, *typographic*; Countdown: *flip*, *circular*, *minimal*; Gallery: *grid*, *masonry*, *carousel*, *slideshow*.
- Each component declares a **typed schema** (its editable props + content slots), making it editor-driven and JSON-serializable.
- Components consume **Theme tokens** for styling and receive **content** from user data — they hold neither hard-coded colors nor hard-coded copy.
- Components are independently **versioned**; the Rendering Engine pins versions per site for stability.
- Components can be AI-recommended, configured in the editor, and (future) sold in the **Component Marketplace**.

**User stories**
- As a host, I want to add a "Timeline" or "Gift Registry" block in one click.
- As a host, I want to switch a component's variant (e.g., a different Gallery style) without losing my photos.

**Edge cases**
- Variant change → content preserved; unsupported props gracefully defaulted.
- Deprecated component version → renderer falls back to a compatible version; host notified of optional upgrade.
- Component with no content (empty RSVP) → sensible empty state, never a broken block.

**Acceptance criteria**
- Any component variant can be swapped without data loss.
- Each component renders valid, accessible markup in isolation and in composition.

---

### 6A.4 Rendering Engine

**Purpose:** The runtime that turns a JSON configuration into the final, interactive event website.

**Inputs → Output**

```
INPUTS                          OUTPUT
─ User Data (content)
─ Selected Theme        ──►     Interactive Event Website
─ Layout                        (server-rendered, hydrated, cached)
─ Components (+variants)
```

**The Rendering Engine must support:**
- **RTL & LTR** — full bidirectional rendering, automatic mirroring of layouts/components.
- **Arabic & English** (and additional languages) — script-aware typography, locale-aware dates/times/numbers.
- **Responsive** — mobile-first; every component adapts across breakpoints.
- **SEO** — server-side rendering, semantic HTML, meta/Open Graph tags, sitemaps, fast LCP.
- **Accessibility** — WCAG 2.1 AA: semantic landmarks, ARIA, keyboard nav, reduced-motion.

**Behavior**
- Deterministic: the **same JSON + same engine version → the same website** (reproducible, cacheable, CDN-friendly).
- **Versioned renderer** (see Admin §7.16): sites pin a renderer version; upgrades are opt-in/managed to avoid regressions.
- Handles guest-scale read traffic via SSR/ISR + CDN edge caching.
- Emits a **static fallback** for no-JS/feature-phone guests.

**Edge cases**
- Malformed/partial JSON → schema validation rejects or repairs with safe defaults; never ships a broken page.
- Unknown component/variant ID → skip-with-warning, render the rest.
- Renderer version mismatch → pinned version used; migration tooling for upgrades.

**Acceptance criteria**
- Valid JSON renders identically across runs and environments.
- Guest site meets §8 performance, SEO, A11y, and i18n/RTL targets.

---

### 6A.5 JSON-Driven Rendering (the contract)

**Principle:** The AI (and the editor) generate **structured JSON configuration**, *not* HTML directly. The frontend Rendering Engine is the single authority that converts JSON → website. This decouples "design intelligence" from "rendering," enabling reuse, versioning, marketplace assets, and multi-surface output (web, invitation card, future native).

**Illustrative configuration concept:**

```json
{
  "eventId": "evt_123",
  "renderer": { "version": "1.4.2" },
  "locale": { "language": "ar", "direction": "rtl", "timezone": "Africa/Cairo" },
  "theme": {
    "id": "thm_royal_emerald",
    "primaryColor": "#0B6B53",
    "secondaryColor": "#C9A227",
    "typography": { "heading": "Amiri", "body": "Cairo", "scale": "lg" },
    "borderRadius": "md",
    "buttonStyle": "filled",
    "cardStyle": "elevated",
    "shadows": "soft",
    "animationPreset": "cinematic",
    "iconStyle": "duotone",
    "backgroundStyle": "pattern-geometric"
  },
  "layout": { "id": "lay_islamic_v2" },
  "components": [
    { "id": "cmp_hero",      "variant": "full-bleed", "content": { "title": "...", "media": "asset_a1" } },
    { "id": "cmp_countdown", "variant": "flip",       "content": { "target": "2026-09-12T18:00:00+02:00" } },
    { "id": "cmp_story",     "variant": "timeline",   "content": { "blocks": [] } },
    { "id": "cmp_venue",     "variant": "map",        "content": { "placeId": "..." } },
    { "id": "cmp_rsvp",      "variant": "standard",   "content": { "questions": [] } },
    { "id": "cmp_gallery",   "variant": "masonry",    "content": { "assets": [] } },
    { "id": "cmp_music",     "variant": "ambient",    "content": { "trackId": "..." } },
    { "id": "cmp_footer",    "variant": "minimal",    "content": {} }
  ]
}
```

**Why this matters**
- **Reusability:** themes/layouts/components recombine without code changes.
- **Versioning & safety:** renderer and component versions are pinned per site.
- **Portability:** the same JSON drives the website, the invitation card (§7.6), exports, and future native renderers.
- **Editability:** the Site Editor reads/writes the exact same JSON the AI produces — one source of truth.
- **Marketplace:** themes, layouts, and components are sold as JSON-described, validated assets.

**Acceptance criteria**
- AI output is valid against the published JSON schema 100% of the time (validated before render).
- Editor and AI operate on the identical configuration object (no divergent formats).

---

## 7. Detailed Feature Specifications

> Each module includes: **Purpose · User Stories · Functional Requirements · Edge Cases · Acceptance Criteria.**

---

### 7.1 Authentication & Account

**Purpose:** Frictionless, secure entry. Must not threaten the 3-minute goal.

**User stories**
- As a host, I want to sign up with Google/Apple in one tap so I can start instantly.
- As a host, I want to start designing *before* committing to an account (guest/lazy auth) so I'm not blocked.
- As a returning user, I want secure login and password reset.
- As a corporate user, I want SSO (SAML/OIDC) — *roadmap*.

**Functional requirements**
- Email/password, Google OAuth, Apple Sign-In.
- **Lazy registration:** allow design work in an anonymous session; prompt for account only at publish. Persist work to the account on sign-up.
- Email verification (non-blocking; gate only publishing/custom domain).
- Password reset via emailed token (expiry 30 min).
- MFA (TOTP) optional; required for Admin.
- Session management, "log out everywhere," device list.
- Role model: Owner, Collaborator/Editor, Viewer (per event), Admin (internal), Seller.

**Edge cases**
- User signs up with email already used via Google → offer account linking.
- Anonymous session abandoned, returns later → recover via magic link if email captured.
- OAuth provider returns no email → request email manually.
- Token replay / expired reset link → clear error + re-request.
- Bulk bot sign-ups → rate limiting + bot detection (e.g., invisible captcha).

**Acceptance criteria**
- A new user can reach the AI generation step within 20s without completing full registration.
- Failed login shows specific, non-leaky errors (no "user exists" enumeration).
- All auth endpoints rate-limited and logged.

---

### 7.2 Onboarding Wizard

**Purpose:** Capture the minimum input the AI needs to generate great output, fast.

**User stories**
- As a host, I want to answer a few simple questions and get instant designs.
- As a host, I want to skip questions and still get a result.

**Functional requirements**
- Step 1: Event type (wedding, engagement, birthday, corporate, other).
- Step 2: Essentials — event name, date/time (+ timezone auto-detected), location (Google Places autocomplete).
- Step 3: Vibe/style — pick mood (elegant, modern, playful, luxe, minimal) or describe in free text (feeds AI).
- Step 4: Optional — upload a photo, choose language.
- Progress indicator; every step skippable with sensible defaults.
- "Generate" triggers AI Design Engine.

**Edge cases**
- No date yet → "Date TBD" supported; countdown hidden until set.
- Location not found in Places → manual address entry + optional pin drop.
- Free-text vibe is empty or nonsensical → fall back to event-type defaults.
- User picks "corporate" → branding/logo fields surfaced.

**Acceptance criteria**
- Wizard completable in ≤ 45s.
- All fields editable later in the editor.

---

### 7.3 Dashboard

**Purpose:** Home base to manage all events.

**User stories**
- As a host with multiple events, I want to see all of them at a glance.
- As a host, I want quick stats (RSVPs, views) without opening each event.
- As a host, I want to duplicate a past event.

**Functional requirements**
- Card/grid of events with thumbnail, status (Draft/Published/Past), date, RSVP count, view count.
- Primary CTA: "Create new event."
- Quick actions per card: edit, view live, share, duplicate, archive, delete.
- Filter/sort (upcoming, drafts, past), search.
- Empty state guiding first-time creation.
- Notifications feed (new RSVPs, comments, payment received).
- **Dashboard sections (v1.1):**
  - **My Themes** — saved/purchased/AI-generated Themes (§6A.1); apply, edit, duplicate, share/sell.
  - **My Layouts** — saved/purchased Layouts (§6A.2); preview in LTR/RTL.
  - **Drafts** — unpublished event sites with resume + last-edited time.
  - **Published Websites** — live sites with status, domain, view/RSVP stats, quick re-publish.
  - **AI History** — log of past AI generations (prompts, generated Theme/Layout/Components, JSON snapshots) with one-click restore/reuse.
  - **Assets** — uploaded media library (images, video, audio, logos) reusable across events; storage usage.
  - **Analytics** — cross-event rollup linking into per-event analytics (§7.14).

**Edge cases**
- 0 events → onboarding-style empty state.
- 100s of events (agency user) → pagination/virtualized list + folders (roadmap).
- Deleting a published event with RSVPs → confirmation + export-before-delete prompt.

**Acceptance criteria**
- Dashboard loads key metrics in < 1.5s (P95).
- "Create new event" reachable in 1 click everywhere.

---

### 7.4 AI Design Engine ⭐ (core differentiator)

**Purpose:** Turn minimal input into complete, premium site+invitation concepts by orchestrating the modular engines (§6A) — the engine of the 3-minute promise. **The AI no longer "generates a template." It generates a Theme, recommends a Layout and Components, and emits a validated JSON configuration that the Rendering Engine turns into a website.**

**AI workflow (v1.1)**

```
1. Generate Theme          (colors, typography, radius, buttons, cards, shadows, animation, icons, background)
        ↓
2. Recommend Layout        (best structural composition for the event type/vibe; RTL/LTR aware)
        ↓
3. Recommend Components    (select components + variants to fill the layout; AI-written copy)
        ↓
4. Build JSON Configuration (assemble theme + layout + components + content into the §6A.5 schema)
        ↓
5. Render Website          (Rendering Engine converts JSON → interactive site; 3 concept variations)
        ↓
6. Publish                 (host confirms → live on subdomain/custom domain)
```

**User stories**
- As a host, I want the system to design for me so I don't have to be a designer.
- As a host, I want multiple options and the ability to regenerate.
- As a host, I want to nudge the design ("make it warmer," "more minimal") in plain language.
- As a host, I want auto-generated copy (welcome text, story, schedule headings) I can edit.
- As a host, I want the AI to pick the right Layout and Components for my event, not just colors.

**Functional requirements**
- Inputs: event type, vibe, photo (optional), language/direction, brand colors (corporate).
- **Stage outputs:** a Theme object (§6A.1), a recommended Layout (§6A.2), a selected Component+variant set (§6A.3), assembled into a JSON configuration (§6A.5).
- Outputs per concept: full themed layout, color palette, typography pairing, component structure, placeholder/AI-written copy, matching invitation card — all expressed as JSON, rendered by the Rendering Engine (§6A.4).
- Generate **3 variants**; "Regenerate" and "Surprise me" (re-run any stage independently — e.g., keep Layout, regenerate Theme).
- **Conversational refinement:** natural-language edits ("use deeper greens," "add a gift section") map to JSON mutations (Theme token change, add Component, etc.).
- **Image intelligence:** extract palette from uploaded photo (feeds Theme); suggest crops; optional AI background/pattern generation (no copyrighted/real-person likenesses).
- **Brand kit** (corporate): upload logo → Theme palette + font suggestions.
- Accessibility guardrails: enforce minimum contrast ratios in generated Themes.
- **Schema validation:** every generated JSON is validated against the published schema before render.
- Cost/latency budget: target < 25s for 3 concepts.

**Edge cases**
- AI service timeout/failure → graceful fallback to curated Themes + Layouts matching the chosen vibe (still rendered via the same engine).
- Inappropriate free-text prompt → content filter + safe refusal.
- Uploaded photo low-res / wrong aspect → upscale suggestion or reframe.
- Non-Latin / RTL language → Theme typography that supports the script; Layout mirrors for RTL automatically.
- Invalid/partial JSON from the model → schema repair or regenerate; never render a broken page.
- Repeated regenerations → diversity constraint so variants differ meaningfully.

**Acceptance criteria**
- ≥ 70% of users keep an AI-generated concept (vs. starting blank).
- Generated Themes pass WCAG AA contrast for body text.
- 100% of AI outputs are schema-valid JSON before rendering.
- Every AI output is fully editable in the Site Editor (same JSON); nothing is locked.

---

### 7.5 Event Website Generator / Site Editor

**Purpose:** Live editor to refine the generated site by editing the **same JSON configuration** the AI produced (§6A.5) — through Theme controls, Layout switching, and a Component canvas.

**User stories**
- As a host, I want to edit text inline and see changes instantly.
- As a host, I want to add/remove/reorder Components (story, schedule, FAQ, gift) and switch their variants.
- As a host, I want to swap my Theme or Layout without losing content.
- As a host, I want a real-time mobile preview (most guests are on phones).
- As a host, I want to invite a collaborator (partner/planner) to edit.

**Functional requirements**
- **Component canvas:** add/remove/reorder Components from the library — Hero, Countdown, Our Story, Timeline, Schedule/Agenda, Details/Venue, Gallery, Map, RSVP, Music, Gift Registry/Payment, FAQ, Footer, Sponsors (corporate), Custom Block (Pro) — each with **variant switching**.
- **Theme controls (§6A.1):** primary/secondary color, typography, border radius, button style, card style, shadows, animation preset, icon style, background style — applied globally and live.
- **Layout switching (§6A.2):** change the structural composition (Luxury, Modern, Minimal, Classic, Islamic, Royal, Floral, Dark…); content is remapped, overflow parked, nothing deleted.
- Inline WYSIWYG editing; drag-to-reorder; show/hide Components.
- Live device preview (desktop/tablet/mobile toggle) **and LTR/RTL toggle**.
- Autosave + version history + undo/redo (operating on the JSON config).
- Multi-language site content (per-Component translations; optional AI translate).
- Privacy: public, unlisted (link only), password-protected, guest-list-gated.
- Real-time collaboration with presence and edit locks.
- "Save as Theme" / "Save as Layout" → reuse later (My Themes / My Layouts).

**Edge cases**
- Two editors change the same Component → conflict resolution (last-write + version history).
- Removing RSVP Component while RSVPs exist → warn, don't delete data.
- Very long content → graceful overflow, no layout break.
- Switching Layout or Theme after edits → preserve content; remap to new structure where possible; park surplus Components; warn on anything that can't be placed.
- Switching a Component variant → content preserved; unsupported props defaulted.

**Acceptance criteria**
- Edits reflect in preview < 300ms.
- Autosave never loses > 5s of work.
- Theme/Layout/variant changes never destroy host content.
- Site renders correctly (via the Rendering Engine) on iOS Safari, Android Chrome, and major desktop browsers, in both LTR and RTL.

---

### 7.6 Invitation Generator

**Purpose:** Produce a shareable digital invitation (card + link) consistent with the site.

**User stories**
- As a host, I want a beautiful invite auto-matched to my site theme.
- As a host, I want to share via WhatsApp/email/SMS/social with one tap.
- As a host, I want a personalized invite per guest (name token) — *Pro*.
- As a host, I want to download the invite as image/PDF/animated video.

**Functional requirements**
- Auto-generate invite from site theme (static image, animated, and link preview).
- Invite variants: still card, motion/video invite, story-format (9:16) for social (rendered from the same JSON/Theme as the site).
- Personalization tokens ({GuestName}) for per-guest links.
- Export: PNG, PDF, MP4/GIF (Pro).
- Rich link unfurling (Open Graph) for WhatsApp/social previews.
- Share sheet: WhatsApp, email, SMS, copy link, QR.
- Optional scheduled "Save the Date" → reminder send.

**Edge cases**
- Guest opens invite link on a feature phone / no JS → static fallback page.
- Personalized link forwarded to others → still works but shows generic name.
- Very long names / non-Latin scripts → text fitting & font fallback.
- Animated invite too heavy on slow networks → adaptive quality + static poster frame.

**Acceptance criteria**
- Invite link generates a correct social preview on WhatsApp, iMessage, Facebook.
- Export files match on-screen design (color-accurate).

---

### 7.7 RSVP Management

**Purpose:** Collect and manage guest responses; the data backbone.

**User stories**
- As a guest, I want to RSVP in seconds without an account.
- As a guest, I want to RSVP for my +1s / family and note dietary needs.
- As a host, I want a live guest list with attending/declined/pending counts.
- As a host, I want to import a guest list and send invites in bulk.
- As a host, I want custom RSVP questions (meal choice, song requests, allergies).
- As a host, I want to export the guest list (CSV).

**Functional requirements**
- Guest-facing RSVP form: attending Y/N/Maybe, party size, custom questions.
- No-account RSVP; optional email/phone capture for reminders.
- Guest list manager: statuses, search, filter, tags, notes, bulk actions.
- Import via CSV / Google Contacts; deduplication.
- Per-guest unique links + RSVP tracking (who responded).
- Plus-ones rules: allow/disallow, max party size, named vs. count.
- Automated reminders (configurable cadence) to non-responders.
- Waitlist + capacity limits (auto-close RSVP when full).
- RSVP deadline with auto-lock.
- Multi-language form.
- Export CSV/Sheets; print-friendly check-in list.

**Edge cases**
- Duplicate RSVP from same guest → update existing, not create new.
- Guest RSVPs after deadline / when full → waitlist or polite closed message.
- Guest changes from Yes → No after paying (paid RSVP) → refund policy flow.
- Group/household RSVP where one declines → per-person status preserved.
- Bulk import with malformed rows → row-level error report, partial import.
- Spam/bot RSVP submissions → rate-limit + optional captcha.

**Acceptance criteria**
- A guest can submit a basic RSVP in < 20s, mobile, no login.
- Host counts update in real time.
- Export contains all custom fields and timestamps.

---

### 7.8 QR Code

**Purpose:** Bridge digital ↔ physical; sharing and event-day check-in.

**User stories**
- As a host, I want a QR code linking to my event site for printed cards.
- As a host, I want per-guest QR codes for fast check-in.
- As a host/staff, I want to scan guests in on event day and see live attendance.

**Functional requirements**
- Auto-generated QR for the event site URL; styled (color, logo center).
- Per-guest QR encoding unique RSVP/ticket ID.
- Downloadable in print resolutions (SVG/PNG/PDF, with bleed for print).
- **Check-in mode (PWA):** scan QR → validate → mark "checked in"; works on phone camera.
- Offline-tolerant check-in (queue + sync).
- Live check-in dashboard (arrived vs. expected).
- Duplicate-scan and invalid-code handling.

**Edge cases**
- Scanned QR already checked in → warn "already checked in at HH:MM."
- Invalid/forged QR → reject clearly.
- No internet at venue → offline queue, sync on reconnect; conflict resolution.
- Guest lost their QR → staff search by name + manual check-in.
- Screenshot/shared QR (paid event) → single-use enforcement option.

**Acceptance criteria**
- Branded QR scans reliably across standard scanners.
- Check-in scan-to-confirmation < 1s online; queued offline with no data loss.

---

### 7.9 Countdown

**Purpose:** Build anticipation; visible engagement element.

**User stories**
- As a guest, I want to see how long until the event.
- As a host, I want the countdown styled to my theme and timezone-correct.

**Functional requirements**
- Live countdown (days/hrs/min/sec) to event start in event timezone.
- Renders in guest's local time optionally, with timezone label.
- Multiple themes/animations; honors "reduce motion."
- Post-event state ("The celebration has begun!" / link to gallery).
- Multi-day events: countdown to first day; per-day schedule below.

**Edge cases**
- Date TBD → countdown hidden.
- Daylight saving transitions → correct via timezone library.
- Guest device clock wrong → server-anchored time.
- Event in the past (old shared link) → graceful post-event message.

**Acceptance criteria**
- Countdown accurate to the second across timezones/DST.

---

### 7.10 Music

**Purpose:** Ambient audio enhances the premium feel.

**User stories**
- As a host, I want background music matching the mood.
- As a guest, I want music that doesn't autoplay loudly without consent.

**Functional requirements**
- Royalty-free/licensed music library, categorized by mood.
- Upload own track (Pro) with rights attestation.
- Play/pause control always visible; default **muted/opt-in** (respect browser autoplay policies).
- Per-section volume / fade; loop.
- Remember mute preference per guest.

**Edge cases**
- Mobile browsers block autoplay → show tap-to-play affordance.
- Copyrighted upload → require rights confirmation; takedown mechanism.
- Slow network → stream/lazy-load; never block page render.
- Accessibility → audio never the only channel of information.

**Acceptance criteria**
- No audio plays without a user gesture where the browser requires it.
- Music never delays first contentful paint.

---

### 7.11 Gallery

**Purpose:** Showcase photos before the event and collect memories after.

**User stories**
- As a host, I want a beautiful photo/video gallery on the site.
- As a host, I want guests to upload their photos to a shared album.
- As a host, I want to moderate guest uploads before they go public.

**Functional requirements**
- Upload images/videos; drag-reorder; layouts (grid/masonry/slideshow/carousel).
- Auto-optimization (resize, compress, responsive, lazy-load, CDN).
- **Guest upload mode** (during/after event), optional moderation queue.
- Captions, albums, cover image.
- Download album (host); per-photo download toggle.
- Storage limits per plan; overage prompts upgrade.

**Edge cases**
- Huge/unsupported files (HEIC, RAW, 4K video) → transcode or reject with guidance.
- Inappropriate guest uploads → moderation + report; auto NSFW detection.
- Storage quota exceeded → block upload, prompt upgrade, never corrupt existing.
- EXIF/location privacy → strip sensitive metadata by default.

**Acceptance criteria**
- Gallery images served via CDN, responsive, lazy-loaded.
- Guest upload works on mobile without an account (if host enables).

---

### 7.12 Google Maps / Location

**Purpose:** Help guests find and navigate to the venue(s).

**User stories**
- As a guest, I want an embedded map and one-tap directions.
- As a host, I want multiple venues (ceremony, reception) with details.
- As a guest, I want parking/transport/accommodation info.

**Functional requirements**
- Google Maps embed with custom pin/styling.
- Google Places autocomplete for address entry.
- "Get directions" deep links (Google/Apple Maps).
- Multiple locations with labels, times, notes.
- Optional travel info blocks (parking, hotels, shuttle).
- Static map fallback image.

**Edge cases**
- Address not geocodable → manual pin drop + coordinates.
- Maps API quota/outage → static map + plain address + directions link.
- Region where Google Maps is restricted → alternative provider fallback.
- Privacy: hide exact address until RSVP confirmed (option).

**Acceptance criteria**
- Directions deep links open the guest's default maps app correctly on iOS/Android.
- Map degrades gracefully if API fails.

---

### 7.13 Payment & Monetization

**Purpose:** Monetize the platform (subscriptions, marketplace, add-ons) and let hosts collect money (paid RSVP/tickets, cash gifts, registry).

> **Note on safe handling:** the platform integrates a PCI-compliant processor (e.g., Stripe). The platform never stores raw card data; all sensitive entry happens in the processor's hosted/embedded fields.

**User stories**
- As a host, I want to subscribe / buy add-ons / unlock premium design assets (Themes/Layouts/Components).
- As a host, I want guests to pay for tickets or contribute a cash gift.
- As a guest, I want a secure, simple checkout.
- As a seller, I want payouts for my design-asset sales (Themes/Layouts/Components).

**Functional requirements**
- **Platform billing:** subscriptions (monthly/annual), one-time design-asset purchases (Themes/Layouts/Components), add-on packs (custom domain, extra storage).
- **Host monetization:** paid RSVP/ticketing, cash gift fund, registry links.
- Processor integration (Stripe + regional methods: cards, Apple/Google Pay, and local rails where available).
- Multi-currency; tax/VAT handling; invoices/receipts.
- Marketplace payouts to sellers (Stripe Connect), revenue share, payout schedule.
- Refunds and partial refunds; dispute/chargeback handling.
- Coupons/discount codes; free trials.
- Dunning for failed subscription renewals.

**Edge cases**
- Currency mismatch (host in EUR, guest in USD) → clear conversion + processor rules.
- Payment succeeds but webhook fails → idempotent reconciliation, no double-charge.
- Guest pays then event canceled → refund workflow + notifications.
- Seller payout in unsupported country → hold + alternative payout.
- Tax/VAT by jurisdiction → tax engine + correct invoices.
- Strong Customer Authentication (SCA/3DS) in EU → enforced.

**Acceptance criteria**
- No raw card data ever touches our servers (PCI SAQ-A scope).
- All payment state changes are webhook-driven and idempotent.
- Receipts/invoices generated for every transaction.

---

### 7.14 Analytics (Host-facing)

**Purpose:** Give hosts visibility into invite performance and guest behavior.

**User stories**
- As a host, I want to see views, RSVP rate, and where guests come from.
- As a host, I want to know who opened a personalized invite.
- As a corporate organizer, I want exportable engagement reports.

**Functional requirements**
- Metrics: page views, unique visitors, RSVP funnel (viewed → started → submitted), response rate, traffic source, device/geo breakdown.
- Per-guest invite open tracking (for personalized links).
- Check-in analytics (attendance vs. RSVP).
- Time-series + comparisons; export CSV/PDF.
- Real-time RSVP feed.
- Privacy-respecting analytics (consent-aware, no unnecessary PII).

**Edge cases**
- Ad blockers / cookie refusal → server-side counting for core metrics.
- Bot traffic inflating views → filter known bots.
- Very low traffic → avoid misleading percentages (show counts).

**Acceptance criteria**
- Funnel numbers reconcile with RSVP records.
- Analytics respect guest consent and regional privacy law.

---

### 7.15 Marketplace (Themes · Layouts · Components)

**Purpose:** Expand selection via curated and community **design assets** — now sold as modular **Themes, Layouts, and Components** rather than static templates; create a creator economy and additional revenue. *(In v1.0 this was the "Template Marketplace"; in v1.1 it sells reusable assets that plug into the design system of §6A.)*

**User stories**
- As a host, I want to browse and apply premium Themes, Layouts, and Components.
- As a host, I want to preview an asset with my own event data, in LTR or RTL.
- As a designer/seller, I want to publish Themes/Layouts/Components and earn revenue.
- As an admin, I want to review/approve submissions for quality and safety.

**Functional requirements**
- Browse three asset types — **Themes**, **Layouts**, **Components** — with categories (by event type/style), search, filters, sort (popular/new/price), ratings/reviews.
- Free and paid assets; "use" → loads the asset into the editor and applies it to the current JSON config.
- Live preview with sample or the host's data; LTR/RTL preview.
- **Seller portal:** upload, set price, versioning, analytics, earnings, payouts.
- **Admin review queue:** quality, originality, schema-validity, content-safety, and RTL/long-content validation before listing.
- Revenue share; licensing terms; DMCA/takedown process.
- Featured/curated collections; seasonal collections.

**Edge cases**
- Plagiarized/copyrighted submission → review + takedown; repeat-offender bans.
- Asset breaks with edge content (long text, RTL) → validation before approval.
- Seller deletes an asset others purchased/used → keep buyers' pinned versions functional.
- Asset built on a deprecated component/renderer version → migration prompt; buyers unaffected.
- Price changes → don't retroactively charge existing users.

**Acceptance criteria**
- Every paid asset is previewable before purchase.
- No asset lists publicly without passing admin review **and** schema validation.
- Applying a Theme/Layout/Component to an existing event preserves the host's content where possible.

---

### 7.16 Admin Dashboard (Internal)

**Purpose:** Operate the platform — support, moderation, marketplace, finance, oversight.

**User stories**
- As an admin, I want to find a user/event and assist with support issues.
- As an admin, I want to moderate reported content and uploads.
- As an admin, I want to approve marketplace assets (Themes/Layouts/Components) and manage payouts.
- As an admin, I want platform-wide metrics and feature flag control.

**Functional requirements**
- User management: search, view, impersonate (audited), suspend, refund.
- Content moderation queue: reported sites/uploads/marketplace assets; takedown tools.
- Marketplace admin: approval queue, seller management, payout oversight.
- Financial ops: transactions, refunds, disputes, revenue dashboards.
- Platform analytics: signups, activation, conversion, churn, MRR.
- Feature flags / experiments / config.
- Support tooling: ticket links, audit logs.
- Role-based access control with full audit trail; admin MFA mandatory.
- **Design-system & platform management pages (v1.1):**
  - **Themes** — manage the official Theme catalog: create, version, publish/deprecate, set defaults.
  - **Layouts** — manage official Layouts; LTR/RTL validation; publish/deprecate.
  - **Components** — manage the Component library and variants; schema definitions; version lifecycle.
  - **Renderer Versions** — list/publish Rendering Engine versions; pin/migrate sites; rollback; track which sites run which version.
  - **AI Prompt Versions** — version-control the AI prompts/policies for each pipeline stage (Theme/Layout/Component/JSON); A/B test; roll back; monitor quality.
  - **Assets** — global asset/media governance: storage, CDN, moderation, licensing.
  - **System Logs** — render errors, schema-validation failures, AI generations, webhook events, audit trail; searchable + alerting.

**Edge cases**
- Impersonation misuse → every impersonation session logged + time-boxed + consent policy.
- Mass-moderation actions → require confirmation + reversible where possible.
- Legal/law-enforcement data requests → defined, logged workflow.

**Acceptance criteria**
- Every privileged action is logged with actor, target, timestamp, reason.
- Admin requires MFA; least-privilege roles enforced.

---

## 8. Non-Functional Requirements

| Area | Requirement |
|---|---|
| **Performance** | Guest site LCP < 2.5s on 4G mobile; editor interactions < 300ms; global CDN. |
| **Scalability** | Handle viral spikes (one invite → thousands of guests in minutes); autoscale; queue heavy jobs (AI, media transcode). |
| **Availability** | 99.9% uptime SLA for published guest sites. |
| **Security** | OWASP Top 10 hardening, encryption in transit & at rest, secrets management, regular pen tests, WAF, rate limiting. |
| **Privacy/Compliance** | GDPR, CCPA; data export/delete (DSAR); consent management; data residency options; processor-only card handling (PCI SAQ-A). |
| **Accessibility** | WCAG 2.1 AA for editor and guest sites; keyboard nav; reduced-motion; screen-reader labels. |
| **Internationalization** | Full i18n, RTL, locale-aware dates/times/currencies, multi-language guest sites. |
| **Reliability of data** | Autosave, version history, soft-delete with recovery window, backups + tested restore. |
| **Observability** | Logging, tracing, error monitoring, real-user monitoring, alerting. |

---

## 9. Suggested High-Level Architecture (non-binding)

- **Design system layer (v1.1, see §6A):** four cooperating engines — **Theme Engine**, **Layout Engine**, **Component Engine**, **Rendering Engine** — operating on a versioned **JSON configuration** as the single source of truth. Themes, Layouts, and Components are independently versioned, reusable assets (DB-backed + asset store).
- **Frontend / Rendering Engine:** React/Next.js (SSR/ISR for fast, SEO-friendly, JSON-driven guest sites), responsive + PWA (for QR check-in offline), full RTL/LTR + i18n. Renderer is **versioned**; sites pin a version with managed migrations.
- **Backend:** API services (Node/Go); event-driven workers for AI generation, media processing, email/SMS, webhooks. A **Configuration Service** stores/validates JSON against a published schema.
- **Data:** Primary relational DB (Postgres) for users/events/RSVPs and for Themes/Layouts/Components/Renderer/Prompt versions; object storage + CDN for media/assets; cache (Redis); search index for marketplace.
- **AI layer:** staged pipeline (Generate Theme → Recommend Layout → Recommend Components → Build JSON → Render) using an LLM for copy + conversational edits and a design-reasoning service; **versioned prompts** (Admin §7.16); image processing (palette/crop/optimize); schema validation + content-safety filters. AI emits **JSON, never raw HTML**.
- **Integrations:** Stripe (+Connect), Google Maps/Places, email/SMS providers, OAuth providers, push/WhatsApp Business API.
- **Multi-tenant** with per-event isolation; subdomain + custom domain routing with managed TLS.

---

## 10. Pricing & Packaging (initial hypothesis — validate)

| Plan | Audience | Includes |
|---|---|---|
| **Free** | Casual hosts | 1 event, subdomain, AI design, basic RSVP, branded footer, limited storage |
| **Premium** | Weddings/milestones | Custom domain, unlimited RSVP, no branding, premium Themes/Layouts/Components, gallery uploads, analytics, animated invites |
| **Pro/Corporate** | Organizers | Branding kit, QR check-in, paid ticketing, advanced analytics, collaborators, priority support |
| **Add-ons** | All | Custom domain, extra storage, single premium design asset (Theme/Layout/Component), paid-RSVP processing fee |
| **Marketplace** | Sellers/buyers | One-time asset purchases (Themes/Layouts/Components); revenue share to sellers |

Monetization streams: subscriptions, marketplace commission, paid-RSVP/ticketing fees, add-ons.

---

## 11. Analytics & Instrumentation Plan (events to track)

`sign_up`, `lazy_session_start`, `onboarding_step_completed`, `ai_generate_requested`, `ai_theme_generated`, `ai_layout_recommended`, `ai_components_recommended`, `ai_json_built`, `ai_render_completed`, `ai_concept_selected`, `ai_regenerate` (stage-scoped), `editor_edit`, `theme_switched`, `layout_switched`, `component_variant_switched`, `site_published`, `time_to_publish`, `invite_shared` (channel), `invite_opened`, `rsvp_started`, `rsvp_submitted`, `payment_completed`, `qr_checkin`, `asset_previewed/purchased` (theme/layout/component), `upgrade_started/completed`, `churned`.

These feed the North Star and the KPI table in §3.

---

## 12. Cross-Cutting Edge Cases & Risks

**Edge cases**
- Viral guest spikes overwhelming a single site → CDN + caching for read-heavy guest pages (JSON-rendered output is cacheable).
- Host deletes account with live event + RSVPs → grace period, export, guest-facing fallback.
- Multi-day / recurring events.
- Events with no fixed date (TBD) across countdown/RSVP/reminders.
- Mixed-language guest lists → per-guest language preference.
- Time zone correctness everywhere (the #1 silent bug source for events).
- **Renderer version drift** → sites pin a Rendering Engine version; upgrades are opt-in/migrated, never silently breaking a live site.
- **Invalid/partial JSON configuration** → schema validation blocks render; safe repair or regenerate; broken pages never publish.
- **Deprecated Theme/Layout/Component versions** → pinned versions keep working; host prompted (not forced) to upgrade.

**Risks & mitigations**

| Risk | Mitigation |
|---|---|
| AI quality/latency hurts 3-min promise | Curated Theme/Layout fallback (same engine); cache; strict latency budget |
| AI cost per generation erodes margin | Caching, smaller models for refinements, usage caps on free tier |
| Marketplace plagiarism/copyright | Mandatory review, originality checks, DMCA process |
| Payment/compliance complexity worldwide | Lean on Stripe; phase country rollout |
| Privacy law variance | Consent framework, data residency, DSAR tooling from day 1 |
| Seasonality (wedding season peaks) | Autoscaling; capacity planning |
| Content moderation at scale | Automated NSFW/abuse detection + human queue |
| Modular-engine complexity / regressions | Versioned renderer + components, schema validation, pinned per-site versions, migration tooling |
| AI emitting invalid configuration | Strict JSON schema, validate-before-render, auto-repair/regenerate, prompt versioning |

---

## 13. Future Roadmap

### Phase 1 — MVP (validate the 3-minute promise)
Auth (incl. lazy/OAuth), Onboarding, **Modular Design Engine** (Theme/Layout/Component/Rendering + JSON-driven rendering, §6A), AI Design Engine (staged pipeline), Site Editor (Theme/Layout/Component editing), Invitation Generator, RSVP (core), Countdown, Google Maps, Gallery (basic), Music (library), QR (site link), Dashboard (incl. My Themes, My Layouts, Drafts, Published Websites, AI History, Assets, Analytics), Free + one paid plan, Stripe subscriptions, essential Admin (incl. Renderer Versions, AI Prompt Versions, System Logs), core analytics, i18n + RTL foundation.

### Phase 2 — Monetize & scale
Marketplace (buy + seller portal + admin review) starting with curated assets, per-guest QR check-in (offline PWA), paid RSVP/ticketing, cash-gift fund, advanced analytics, collaborators/real-time editing, custom domains, guest photo uploads + moderation, personalized invites, animated/video invites, reminders & dunning, multi-currency/tax.

### Phase 3 — Differentiate & expand
Conversational AI design refinement at depth, AI translation for guest sites, native mobile apps, SSO for enterprise, registry integrations, white-label for planners/agencies, AI budget helpers, print fulfillment partnerships.

### Phase 4 — Platform & ecosystem
Public API/integrations, advanced experimentation platform, recommendation engine for design assets, creator monetization expansion, post-event engagement (thank-you flows, shared memory albums, anniversary re-engagement loops).

### Future Features (target backlog, v1.1)
Building on the modular architecture and creator economy:
- **Theme Marketplace** — buy/sell reusable Themes (§6A.1).
- **Component Marketplace** — buy/sell reusable Components & variants (§6A.3).
- **AI Video Invitations** — AI-generated motion/video invites from the event's Theme + content.
- **AI Seating Planner** — auto-arrange guests into tables from RSVP data + constraints.
- **Vendor Marketplace** — connect hosts with photographers, venues, caterers, etc.
- **Guest Messaging** — in-platform host↔guest messaging and announcements.
- **Email Campaigns** — branded email blasts (save-the-date, invites, reminders, thank-you).
- **SMS Campaigns** — SMS invites/reminders with delivery tracking.
- **WhatsApp Invitations** — native WhatsApp Business invite delivery + RSVP.
- **Guest Analytics** — per-guest engagement (opens, RSVP behavior, check-in).
- **Event Analytics** — deep event-level dashboards (funnel, attendance, revenue, channel performance).

*(Layout Marketplace is delivered alongside the Theme and Component marketplaces as part of the unified Marketplace, §7.15.)*

---

## 14. Open Questions
1. Initial GTM wedge — weddings only, or weddings + birthdays simultaneously?
2. Build vs. buy for the AI design-reasoning layer (Theme/Layout/Component recommendation)?
3. Marketplace revenue-share % and minimum quality bar (across Themes, Layouts, Components)?
4. Which regional payment methods are required for launch markets?
5. Free-tier generosity vs. conversion — where's the line?
6. Custom domain: included in Premium or paid add-on?
7. Renderer strategy: single SSR renderer vs. multiple surface renderers (web/invite/native) sharing one JSON schema?
8. Versioning policy: how long are deprecated Theme/Layout/Component/renderer versions supported for live sites?

---

*End of PRD v1.1 — Eventora.*

> **Technical direction (restated):** Eventora is built on a **reusable design system and modular architecture** — Theme Engine, Layout Engine, Component Engine, and Rendering Engine driven by structured JSON — **not** a catalog of static invitation templates. Every event website is composed dynamically from reusable, versioned components.
