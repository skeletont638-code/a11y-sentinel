---
name: accessibility-audit
description: Use when building, reviewing, auditing, or remediating any website, web app, or mobile UI for accessibility / ADA / Section 508 / WCAG compliance — or when handling alt text, color contrast, keyboard navigation, screen-reader support, ARIA, focus order, form labels, captions, an accessibility statement, or an ADA demand letter / lawsuit. Loads the complete WCAG 2.2 A/AA criteria checklist so every requirement is checked, not guessed.
---

# Accessibility Audit (WCAG 2.2 A/AA)

## Core principle

**Conform to WCAG 2.1 AA as the legal floor; build to WCAG 2.2 AA.** 2.2 AA is a superset of 2.1 AA, so building to it satisfies the floor and future-proofs. Never target "WCAG 3.0" (an early draft, not for conformance).

Two facts that shape everything below:
1. **Automated tools detect only ~30–40% of WCAG issues.** A clean axe/Lighthouse run is a *floor, not a verdict*. The remaining ~60–70% (is the alt text *meaningful*? is focus order *logical*? do labels *describe*?) require human/agent judgment — **this judgment layer is the real value; a scanner cannot do it.**
2. **Fix the source code. Overlay/widget products (accessiBe, AudioEye, UserWay, EqualWeb) are NOT a fix and NOT a legal shield** — they're routinely named in lawsuits; the FTC fined accessiBe $1M in 2025 for claiming otherwise. If one is present, recommend removing it and remediating the source.

This is an engineering reference, not legal advice. For litigation risk, jurisdictions, state damages, case law, and the accessibility statement, read `reference/legal.md`. For scan commands, manual-test procedures, and the WCAG-EM report format, read `reference/auditing.md`.

## Workflow

1. **Scope** — pin version+level (2.2 AA), enumerate domain + subdomains, pick a representative page sample (home, key templates, forms, login/auth, search, error states, complex widgets). A conformance claim requires *whole pages* and *complete processes* to pass — partial-page conformance is invalid.
2. **Automated pass** — run ≥2 engines (axe-core + pa11y/Lighthouse). Catches the machine-detectable ~30–40%. See `reference/auditing.md`.
3. **Manual pass (required)** — keyboard-only, screen reader (NVDA+VoiceOver min), 200% zoom / 400% reflow (320px), contrast spot-checks over images/states. This is where most real failures live.
4. **Fix source code** — by risk-based triage (below), not file order.
5. **Report** — one row per success criterion (Pass/Fail/Not-Present/Inconclusive), separating automated vs. manual provenance.

**Risk-based triage — fix in this order:**
- **Tier 0 — transaction blockers:** checkout, login, search, all forms fully keyboard + screen-reader operable (2.1.1, 2.1.2, 3.3.2, 4.1.2); alt text (1.1.1); visible focus (2.4.7); contrast (1.4.3). Remove any overlay.
- **Tier 1 — site-wide structure (fix once, everywhere):** semantic headings/landmarks/skip link (1.3.1, 2.4.1), page `<title>` (2.4.2) + `lang` (3.1.1), error identification+suggestion (3.3.1, 3.3.3), never color-only (1.4.1), reflow/zoom (1.4.10, 1.4.4), captions/transcripts (1.2.x).
- **Tier 2 — program/defensibility:** accessibility statement, ongoing monitoring, dated remediation records, third-party/vendor controls, born-accessible design system.

## The judgment layer (what scanners CANNOT catch — check these by hand)

- **Is alt text *meaningful*** for the context, or just present? (functional images describe the action/destination, not the picture)
- **Is focus order *logical*** and does it match visual order?
- **Do labels/headings/links *describe*** their target (not "click here", "more", "Section 1")?
- **Is ARIA correct** — right role/name/state, and announced? ("No ARIA is better than bad ARIA.")
- **Are captions accurate** (auto-captions are non-compliant until reviewed)?
- **Do color/contrast hold** over images, gradients, and hover/focus/disabled states?
- **Is every status message announced** (live regions) without stealing focus?

## THE FULL CHECKLIST — every WCAG 2.2 Level A & AA success criterion

Target = all of these. **4.1.1 Parsing is OBSOLETE in 2.2 — do not score against it.** The 3 new 2.2 focus/auth-enhanced criteria (2.4.12, 2.4.13, 3.3.9) are **AAA — out of scope.** Count: **31 Level A + 24 Level AA = 55** (the 2.1 AA floor is the same set minus the 6 new 2.2 criteria, plus 4.1.1 = 50).

### Perceivable

| SC | Name · Level | Check for | Common failure |
|---|---|---|---|
| 1.1.1 | Non-text Content · A | Text alt for all non-text; decorative marked `alt=""`; functional images name the action | Missing/auto alt, `alt="image.jpg"`, icon buttons with no name. **#1 cited.** |
| 1.2.1 | Audio-only & Video-only (Prerecorded) · A | Transcript for audio-only; transcript/audio for silent video | Podcasts/demos with no transcript |
| 1.2.2 | Captions (Prerecorded) · A | Synchronized captions on all prerecorded video-with-audio | None, or unreviewed auto-captions |
| 1.2.3 | Audio Description or Media Alt (Prerecorded) · A | Audio description of visuals OR full text alternative | On-screen action not narrated, no transcript |
| 1.2.4 | Captions (Live) · AA | Synchronized captions for all **live** audio content | Live webinars/streams/events with no live captioning |
| 1.2.5 | Audio Description (Prerecorded) · AA | Audio description track for all prerecorded video-with-audio | Important on-screen visuals not described in audio |
| 1.3.1 | Info and Relationships · A | Structure programmatic: headings, lists, tables (`<th>`/scope), associated labels | Faux headings via bold, layout tables, unlabeled fields |
| 1.3.2 | Meaningful Sequence · A | DOM/reading order correct where order conveys meaning | CSS flex/grid/absolute order ≠ DOM order |
| 1.3.3 | Sensory Characteristics · A | Instructions not by shape/size/location/sound alone | "Press the green button", "the box on the right" |
| 1.3.4 | Orientation · AA | Not locked to one orientation unless essential | App locked to portrait |
| 1.3.5 | Identify Input Purpose · AA | `autocomplete` tokens on user-info fields | name/email/address/phone without `autocomplete` |
| 1.4.1 | Use of Color · A | Color never the only cue for info/state/action | Links/errors/required by color only |
| 1.4.2 | Audio Control · A | Auto-play >3s has pause/stop/volume | Auto-playing audio, no stop |
| 1.4.3 | Contrast (Minimum) · AA | ≥4.5:1 normal text, ≥3:1 large (18pt/14pt bold) | Light-gray text, low-contrast placeholders. **Top-cited.** |
| 1.4.4 | Resize Text · AA | Text to 200% with no loss, without AT | Fixed px; clipping at 200% |
| 1.4.5 | Images of Text · AA | Real text, not images of text (logos exempt) | Headings/buttons as flat images |
| 1.4.10 | Reflow · AA | Single-column, no 2D scroll at 320px (=400% zoom) | Fixed-width; horizontal scroll at zoom |
| 1.4.11 | Non-text Contrast · AA | UI components, states, focus rings, meaningful graphics ≥3:1 | Low-contrast borders, toggles, focus rings |
| 1.4.12 | Text Spacing · AA | No loss when user overrides line/para/letter/word spacing | Fixed-height `overflow:hidden` clipping |
| 1.4.13 | Content on Hover or Focus · AA | Hover/focus content dismissable (Esc), hoverable, persistent | Tooltips vanish on move / can't dismiss |

### Operable

| SC | Name · Level | Check for | Common failure |
|---|---|---|---|
| 2.1.1 | Keyboard · A | All functionality keyboard-operable | Mouse-only menus/sliders/modals; click on non-focusable `<div>` |
| 2.1.2 | No Keyboard Trap · A | Focus can always leave by keyboard | Modals/widgets trap Tab |
| 2.1.4 | Character Key Shortcuts · A | Single-char shortcuts off/remappable/focus-scoped | Single-letter shortcuts fire while typing |
| 2.2.1 | Timing Adjustable · A | Time limits off/adjustable/extendable (20s warning) | Checkout/session timeout, no warning |
| 2.2.2 | Pause, Stop, Hide · A | Moving/auto-updating >5s can pause/stop/hide | Auto-advancing carousels, tickers |
| 2.3.1 | Three Flashes or Below · A | Nothing flashes >3×/sec | Rapid flashing animation/GIF |
| 2.4.1 | Bypass Blocks · A | Skip link / landmarks / headings to bypass repeats | No skip link, no landmarks |
| 2.4.2 | Page Titled · A | Descriptive `<title>` per page | "Home", "Untitled", duplicates |
| 2.4.3 | Focus Order · A | Sequential focus preserves meaning | Positive `tabindex`; modal doesn't move focus |
| 2.4.4 | Link Purpose (In Context) · A | Purpose clear from text or context | "Click here", "Read more", bare URLs |
| 2.4.5 | Multiple Ways · AA | >1 way to find a page (search + nav/sitemap) | Single nav, no search/sitemap |
| 2.4.6 | Headings and Labels · AA | Headings/labels describe topic/purpose | "More", "Section 1"; vague labels |
| 2.4.7 | Focus Visible · AA | Visible keyboard focus on every operable element | Global `outline:none` with no replacement. **Critical.** |
| 2.4.11 | Focus Not Obscured (Minimum) · AA *(new 2.2)* | Focused element not fully hidden by author content | Sticky header/cookie banner covers focus |
| 2.5.1 | Pointer Gestures · A | Multipoint/path gestures have single-pointer alt | Swipe/pinch-only with no tap alt |
| 2.5.2 | Pointer Cancellation · A | Not completed on down-event (abort/undo) | Fires on `mousedown`/`touchstart` |
| 2.5.3 | Label in Name · A | Accessible name contains the visible label text | `aria-label` differs from visible text |
| 2.5.4 | Motion Actuation · A | Motion-triggered actions have UI alt + can disable | Shake-to-undo, tilt-to-scroll only |
| 2.5.7 | Dragging Movements · AA *(new 2.2)* | Dragging achievable with single pointer, no drag | Drag-only reorder, sliders, kanban |
| 2.5.8 | Target Size (Minimum) · AA *(new 2.2)* | Pointer targets ≥24×24 CSS px or spaced | Tiny icon/close buttons, dense pagination |

### Understandable

| SC | Name · Level | Check for | Common failure |
|---|---|---|---|
| 3.1.1 | Language of Page · A | Valid `lang` on `<html>` | Missing/wrong `lang` |
| 3.1.2 | Language of Parts · AA | `lang` on differing-language passages | Foreign quote with no `lang` |
| 3.2.1 | On Focus · A | Focus doesn't change context | Auto-navigate/submit on focus |
| 3.2.2 | On Input · A | Changing a setting doesn't unexpectedly change context | Select auto-navigates; auto-submit |
| 3.2.3 | Consistent Navigation · AA | Repeated nav in same relative order | Nav reordered page to page |
| 3.2.4 | Consistent Identification · AA | Same-function components named consistently | "Search" vs "Find"; mismatched icons |
| 3.2.6 | Consistent Help · A *(new 2.2)* | Repeated help in same relative location | Help/contact link jumps around |
| 3.3.1 | Error Identification · A | Errors identified and described in text | Error by red color only; generic "has errors" |
| 3.3.2 | Labels or Instructions · A | Labels/instructions incl. format & required | Placeholder-only labels; no `<label>` |
| 3.3.3 | Error Suggestion · AA | Correction suggestions when known | "Invalid input", no guidance |
| 3.3.4 | Error Prevention (Legal/Financial/Data) · AA | Reversible / checked / confirmed | Irreversible purchase/delete, no confirm |
| 3.3.7 | Redundant Entry · A *(new 2.2)* | Re-use prior entries (except passwords) | Multi-step form re-typing address |
| 3.3.8 | Accessible Authentication (Minimum) · AA *(new 2.2)* | No cognitive-function test unless alt (paste, password mgrs, OTP) | Paste-blocked login; puzzle CAPTCHA, no alt |

### Robust

| SC | Name · Level | Check for | Common failure |
|---|---|---|---|
| 4.1.1 | Parsing · **OBSOLETE (removed in 2.2)** | Do **not** score. Issues now fall under 1.3.1 / 4.1.2 | (historically: duplicate `id`, mis-nested tags) |
| 4.1.2 | Name, Role, Value · A | Name/role programmatic; states settable & announced (incl. custom widgets) | `<div>` widgets with no role/name; missing `aria-expanded`/`-checked`. **Critical.** |
| 4.1.3 | Status Messages · AA | Status announced via live region (`role=status`/`alert`) without focus | Toasts, "X results", success never announced |

## Mobile, PDFs, and beyond

- **Native apps** (covered by ADA Title II 2024 rule, increasingly Title III): map WCAG via **WCAG2ICT**; implement with platform a11y APIs; test VoiceOver (iOS) / TalkBack (Android); target ≥44–48dp. **App-store review ≠ ADA compliance.**
- **PDFs/documents** are a common cited violation: tagged PDF, reading order, real text (not scanned), alt text, table headers, `lang`. Standard = PDF/UA + WCAG. Or provide an accessible HTML equivalent.
- **Third-party embeds** (checkout iframes, chat, maps, video) are *your* liability: require WCAG conformance in contracts, demand a VPAT/ACR, test the embed, provide a human/phone fallback.

## Common mistakes

- Treating a clean automated scan as conformance. It covers ~30–40%; **always do the manual pass.**
- Stripping focus outlines for aesthetics (fails 2.4.7) — always provide a visible replacement (≥3:1).
- Placeholder text used as the only label (fails 3.3.2).
- Adding ARIA to "fix" things — wrong ARIA fails 4.1.2. Prefer native HTML.
- Scoring against 4.1.1 under 2.2 (it's obsolete) or treating 2.4.13/2.4.12/3.3.9 as AA (they're AAA).
- Relying on an overlay widget, or claiming "fully ADA compliant" — the latter becomes an admission + FTC false-advertising risk. Underclaim; cite an honest target.
