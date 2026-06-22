# Auditing procedure (WCAG-EM) + commands

A defensible audit is **two layers**: automated scanning (machine-detectable subset) **plus** structured manual testing. W3C WAI: *"No tool alone can determine if a site meets accessibility standards. Knowledgeable human evaluation is required."* Automated tools find **~30–40%**; the rest needs manual review. Automated results alone cannot support a conformance claim.

## Step 1 — Scope (WCAG-EM)

Pin **version + level** (2.1 AA floor / 2.2 AA target). Enumerate domain + all in-scope subdomains. Select a **representative page sample**: home, key templates, forms, login/auth, search, content-heavy pages, error states, complex widgets. A valid conformance claim specifies **version, level, scope (URIs), and technologies relied upon** — and **whole pages and complete processes** must conform (no partial-page conformance).

## Step 2 — Automated scans (run ≥2 engines)

```bash
# axe-core CLI (Deque) — low false positives; powers Lighthouse/DevTools
npm install -g @axe-core/cli
npm i -g browser-driver-manager && npx browser-driver-manager install chrome
axe https://example.com --tags wcag2a,wcag2aa,wcag21a,wcag21aa,wcag22aa --save results.json

# Pa11y-CI — sitemap-aware, ideal for whole-site / subdomain coverage
npx pa11y-ci --sitemap https://example.com/sitemap.xml --sitemap-exclude '\.pdf$'
pa11y --standard WCAG2AA https://example.com          # single page

# Lighthouse — runs axe-core; also lists manual checks it cannot perform
npm i -g lighthouse
lighthouse https://example.com --only-categories=accessibility \
  --output=json --output-path=./lh.json --chrome-flags='--headless'

# IBM Equal Access (achecker) — maps findings to specific WCAG criteria
npm install --save-dev accessibility-checker
npx achecker urls.txt
```

**Multi-subdomain:** enumerate subdomains, then loop a URL list through axe/pa11y. **Caveat:** sitemaps often omit auth-gated, JS-rendered, or dynamically generated pages — add those manually or they're never scanned. **WAVE** (WebAIM) is a good per-page human-in-the-loop visualizer.

**Coverage disclaimer (put in every report):** automated results are a floor, not a verdict (~30–40% coverage); "zero violations" must disclose the inconclusive/manual categories. A Lighthouse score (e.g. 95/100) is **not** a conformance measure.

## Step 3 — Required manual tests

- **Keyboard-only** (Tab/Shift+Tab/Enter/Space/arrows, no mouse): everything reachable/operable, no traps, visible focus, logical order, skip link, correct widget patterns. → 2.1.1, 2.1.2, 2.4.3, 2.4.7, 2.4.11
- **Screen readers** (NVDA + VoiceOver min; JAWS if budget): *meaningful* alt, names/roles/states, heading hierarchy, list/table semantics, label+error association, link purpose, live-region announcements. → 1.1.1, 1.3.1, 2.4.6, 3.3.2, 4.1.2, 4.1.3. *Only a human/SR pass can judge whether alt text is meaningful.*
- **200% zoom & 400% reflow (320px):** no loss/clipping, no 2D scrolling for text. → 1.4.4, 1.4.10, 1.4.12
- **Contrast spot-checks** (catch what tools miss: text over images/gradients, hover/focus/disabled, placeholders): 4.5:1 / 3:1. → 1.4.3, 1.4.11, 1.4.1
- **2.2 add-ons:** focus not obscured by sticky elements (2.4.11), target size ≥24px (2.5.8), drag alternatives (2.5.7), accessible auth (3.3.8).

**Screen-reader / browser matrix** (~80–85% of SR users covered by NVDA + VoiceOver):

| Screen reader | Browser | Platform |
|---|---|---|
| NVDA | Firefox / Chrome | Windows |
| JAWS | Chrome / Edge | Windows |
| VoiceOver | Safari | macOS / iOS |
| TalkBack | Chrome | Android |

Test with **actual disabled users** where possible — surfaces issues no tool or proxy finds.

## Step 4 — Report (WCAG-EM Step 5)

1. **Scope** — URLs/subdomains, version+level, AT/browser baseline.
2. **Date** + tools/AT used.
3. **Per-page-sample results.**
4. **Findings — one row per success criterion**: Pass / Fail / Not Present / Inconclusive, with SC number+name, severity, affected URLs, evidence (screenshot/code/SR output), user impact, remediation. **Separate automated vs. manual provenance.**
5. State explicitly whether a **full conformance claim** can be made (every applicable SC passes on whole pages + complete processes) or whether this is a **gap/remediation audit**.

## Born-accessible (shift-left)

Cheapest fixes happen at design/component time: accessible design system + component library, design-stage checks (contrast, focus order, target size in mockups), WCAG acceptance criteria, automated checks in CI, accessibility in definition-of-done, and training for designers, developers, **and content authors** (CMS users reintroduce barriers constantly).
