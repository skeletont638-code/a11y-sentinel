<div align="center">

# a11y-sentinel

**Accessibility guidance for AI coding agents.** The complete WCAG 2.2 checklist — all 55 Level A/AA success criteria — plus US ADA legal context and a real audit procedure, loaded the moment your agent touches accessibility.

One portable skill for **Claude Code · Cursor · Codex · Gemini CLI** and every tool that reads the [Agent Skills](https://agentskills.io) standard.

`npx skills add https://github.com/skeletont638-code/a11y-sentinel`

</div>

---

## Why a11y-sentinel?

US web-accessibility lawsuits hit a record **~3,117 federal filings in 2025** (plus thousands more in state court), driven by templated complaints against businesses of *every* size — there is **no small-business exemption**. A California Unruh violation alone is **$4,000 minimum, per violation**.

Yet ask an AI agent to "make this accessible" and you get the same handful of half-fixes every time:

- `alt` text that's present but **meaningless** (or `alt="image.png"`)
- focus outlines stripped for looks (`outline: none`) with no replacement
- placeholder text used as the only form label
- low-contrast gray text, color-only error states
- `<div>` widgets with no role, name, or keyboard support
- "no ARIA is better than bad ARIA" — and the agent adds bad ARIA

The reason: agents pattern-match a few obvious issues and stop. **Real conformance is 55 criteria, and ~60–70% of them can't be caught by a scanner at all** — they need judgment against the *full* set. a11y-sentinel puts that full set in your agent's context, so it audits and **fixes the source code** properly instead of guessing.

It is **not a scanner** (axe/Lighthouse already do detection) and **not an overlay widget** — those mask issues, get named in lawsuits, and earned accessiBe a **$1M FTC fine** in 2025. This skill makes your agent do the thing that actually works: remediate the code, against every requirement.

## What it gives your agent

| File | Contents |
|---|---|
| **`SKILL.md`** | The build standard (2.1 AA floor → 2.2 AA target) · the audit workflow · risk-based triage (transaction-blockers first) · **the full 55-criterion checklist** (every SC, level, what to check, common failure) · the **judgment layer** scanners can't do · mobile / PDF / third-party-embed coverage |
| **`reference/legal.md`** | ADA Title II/III, Section 508, ACAA, HHS 504 · the version-by-statute matrix · state damages (CA Unruh, NY) · key case law · the overlay warning · accessibility-statement requirements · defensibility records |
| **`reference/auditing.md`** | Copy-paste axe / pa11y / Lighthouse / IBM commands · the required manual tests + screen-reader matrix · the WCAG-EM report format |

### The 55 criteria, by principle

- **Perceivable (20)** — text alternatives, captions & audio description, semantic structure, contrast, reflow, text spacing, hover/focus content
- **Operable (20)** — keyboard & no traps, timing, skip links, focus order & visibility, pointer gestures, **target size ≥24px**, **dragging alternatives** *(new in 2.2)*
- **Understandable (13)** — page/part language, predictable focus & input, consistent nav/help, error identification & suggestion, **redundant entry**, **accessible authentication** *(new in 2.2)*
- **Robust (2)** — name/role/value for all components, status-message announcements

*(Correctly handles the obsolete 4.1.1 Parsing and the AAA-only 2.2 criteria, so nothing is mis-scored.)*

## Install

**Recommended — one command** (scans the repo's `skills/` folder):

```bash
npx skills add https://github.com/skeletont638-code/a11y-sentinel
```

**Or copy the skill into your tool manually:**

```bash
# Claude Code — project-local
cp -r skills/accessibility-audit your-project/.claude/skills/
# Claude Code — global (all projects)
cp -r skills/accessibility-audit ~/.claude/skills/

# Cursor
cp -r skills/accessibility-audit your-project/.cursor/skills/

# Codex CLI  (also recognized at ~/.agents/skills/)
cp -r skills/accessibility-audit your-project/.agents/skills/

# Gemini CLI
cp -r skills/accessibility-audit your-project/.gemini/skills/
```

Or simply **paste `skills/accessibility-audit/SKILL.md` into any agent chat.** Restart/reload your tool afterward so it picks up the new skill.

## Usage

Once installed, the skill activates whenever you work on accessibility, ADA/WCAG compliance, alt text, contrast, keyboard nav, screen readers, ARIA, form labels, or captions. Just ask:

```
Audit this page against WCAG 2.2 AA and fix what you can.
Make the checkout flow fully keyboard- and screen-reader-operable.
Why would this form fail an accessibility audit? Fix the labels and errors.
Check our color contrast and focus states against WCAG.
Review this component for ARIA correctness (name/role/value).
```

The agent now has every criterion in context — it runs the automated + manual workflow, fixes the source in priority order (transaction-blockers first), and reports honestly, separating what a scanner verified from what needs human review.

## Honest scope

- **Engineering reference, not legal advice.** Consult counsel for a specific matter.
- **Automated checks are a floor, not a verdict** — a clean axe/Lighthouse run is ~30–40% coverage; the manual pass is required for a conformance claim.
- **Never claim "fully ADA compliant."** It becomes an admission when violations exist (and an FTC false-advertising risk). Underclaim; cite an honest target.

## Supported tools

Claude Code · Cursor · Codex CLI · Gemini CLI · and any agent that reads the [Agent Skills](https://agentskills.io) standard (Copilot, Cline, Windsurf, OpenCode, …). The `SKILL.md` is plain Markdown — it works anywhere you can give a model context.

## License

MIT — see [LICENSE](LICENSE). Issues and PRs welcome: corrections to criteria, new failure examples, framework-specific fix patterns.

---

<div align="center">
<sub>WCAG 2.2 A/AA reference compiled 2026 from primary W3C, DOJ, and case-law sources. Re-verify deadlines and figures before relying on them.</sub>
</div>
