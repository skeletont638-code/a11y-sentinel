# Legal & litigation reference (US, 2026)

*Engineering/operations reference, not legal advice — consult counsel for a specific matter. Compiled 2026-06-22.*

## Lawsuit risk (why this matters)

- ~3,117 federal website-accessibility suits filed in 2025 (+27% YoY), ~36% of all 8,667 federal ADA Title III suits; total US digital-accessibility filings (incl. state court) exceeded ~5,000.
- ~41% of 2024 federal filings targeted companies **already sued** — paying a nuisance settlement without fixing invites a repeat suit.
- Driven by a few repeat "tester" plaintiffs + a handful of firms filing templated complaints in volume (one plaintiff filed ~287 suits in 2025; one firm 600+).
- Typical sequence: barrier encountered → **pre-suit demand letter** (~$5,000) → complaint if ignored or in damages states.
- **No small-business exemption** for the Title III accessibility duty (the 15-employee threshold is Title I employment only). Serial plaintiffs *prefer* small/mid businesses (more likely to settle).

## The standard, precisely

- **WCAG 2.1 AA = legal floor** (the only version made binding by US regulation for the broadest category; the version courts/settlements reference). 50 criteria (30 A + 20 AA).
- **WCAG 2.2 AA = build target** (superset; conforming satisfies the floor). 55 criteria (minus obsolete 4.1.1).
- **Honesty caveat:** there is **no binding federal regulation** specifying a technical standard for ADA **Title III** (private business). WCAG AA is the **de facto** benchmark, not a DOJ mandate — in a Feb 2, 2026 Statement of Interest (*Alcazar v. Fashion Nova*), DOJ said it "does not endorse WCAG as the appropriate or necessary standard" for Title III. It remains the only objective, testable target; describe it as de facto, not mandated.
- Federal ADA remedy for private plaintiffs: **injunctive relief + attorneys' fees only — no damages.** State laws add the damages (below).

## Version-by-statute matrix (don't state a single "ADA standard")

| Source | Binds | WCAG |
|---|---|---|
| ADA Title II (2024 DOJ rule) | State/local government, **incl. mobile apps + PDFs** | **2.1 AA (binding)** |
| ADA Title III | Private public accommodations | No codified standard; **2.1 AA de facto** |
| Section 508 | Federal agencies + their ICT vendors | **2.0 AA** |
| ACAA (14 CFR 382.43) | Airlines (primary website) | **2.0 AA** |
| HHS Section 504 (2024 rule) | Recipients of HHS funding (hospitals, clinics, Medicare/Medicaid orgs) | **2.1 AA (binding)** |

WCAG dates (W3C Recommendations, backward-compatible): 2.0 = Dec 2008; 2.1 = Jun 2018; 2.2 = Oct 2023 (also ISO/IEC 40500:2025).

**Binding-rule deadlines (use CURRENT, extended dates):**
- Title II: population ≥50,000 → **Apr 26, 2027**; <50,000 + special districts → **Apr 26, 2028** (extended by the Apr 20, 2026 IFR; standard unchanged).
- HHS 504: 15+ employees → **May 11, 2027**; <15 → **May 10, 2028** (extended May 2026 IFR). **Do not cite the superseded May 11, 2026 date.**

## State laws = the damages engine

- **California — Unruh Civil Rights Act:** an ADA violation is per se an Unruh violation; **≥$4,000 per offense** + treble actual + fees. Biggest serial-filing driver. (Pure web-only-business coverage remains contested in CA.) **AB 1757 did NOT pass** — not law.
- **New York — NYSHRL + NYCHRL:** highest-volume jurisdiction; compensatory/punitive damages + fees; NYCHRL construed liberally. As federal courts tightened standing (2024–25), filings shifted to NY **state court**.
- **Colorado HB21-1110:** government entities only, WCAG 2.1 AA, $3,500/violation — **not private business.**
- CA + NY together ≈40% of digital-accessibility suits.

## Key case law

- **Robles v. Domino's** (9th Cir. 2019, cert. denied) — Title III applies to a site/app with a **nexus** to a physical place; on remand, summary judgment for Robles + Unruh $4,000. Most-cited modern precedent.
- **Gil v. Winn-Dixie** (11th Cir. 2021) — held websites aren't public accommodations, then **VACATED as moot** — not binding.
- **NAD v. Netflix** (D. Mass. 2012) — web-only service is a public accommodation with **no nexus**; consent decree required 100% captioning.
- **NAD v. Harvard / MIT** (2020) — captioning obligations under Title III + Section 504; auto-captions treated as non-compliant.
- **Andrews v. Blick Art** (EDNY 2017) — site is a public accommodation; ADA + NY state/city claims stacked.
- **Circuit split (nexus):** nexus/physical-place required — 9th, 3rd, 6th, 5th. Online-only can be covered — 1st, 2nd, 7th. No SCOTUS resolution; plaintiffs forum-shop into CA/NY/FL/PA/IL.
- **Tester standing:** *Acheson Hotels v. Laufer* (2023) dismissed as moot, left open; courts more skeptical of serial plaintiffs since.

## Overlays (critical warning)

Overlay/widget products (accessiBe, AudioEye, UserWay, EqualWeb) **mask** issues without fixing source, are **routinely named in lawsuits** (~25% of 2024 suits cited overlays as *barriers*), and confer **no legal immunity**. **FTC fined accessiBe $1,000,000 (final order Apr 2025)** for deceptive WCAG-compliance claims and barred such claims. 700+ accessibility professionals signed a public statement against them. **Remediate the actual source code.**

## Accessibility statement (publish an honest one)

Required elements: conformance target (e.g. WCAG 2.1/2.2 AA) · measures taken (audits, training) · **specific** known limitations · feedback/contact channel **+ response timeframe** · date · alternative access (phone/human fallback).
**Never overclaim** "fully ADA/WCAG compliant" — it becomes an admission when violations exist and invites an **FTC false-advertising** claim. Underclaim slightly; don't auto-generate from an overlay.

## Defensibility records ("ongoing efforts" evidence)

Maintain dated: audit reports · remediation logs/tickets · conformance roadmap with target dates · VPATs/ACRs · training records · document-retention policy. Dated proof you were actively remediating *before* suit blunts damages and supports mootness.

## Other regimes that may stack on top of Title III

Section 508 (federal vendors) · Section 504 (federal-funding recipients; HHS rule) · ACAA (airlines, FCC) · Title I (employee-facing tools: HR portals, ATS, intranets — separate EEOC exposure, 15+ employees) · CVAA (comms/video products, FCC) · EU **EAA** (enforcement began Jun 28, 2025; EN 301 549 → WCAG 2.1 AA) · Canada AODA/ACA. A US firm selling into the EU/Canada inherits those obligations.

*Residual uncertainty: DOJ does not endorse WCAG for Title III (de facto only); tester standing unresolved; cost figures are vendor ranges; CA web-only coverage contested.*
