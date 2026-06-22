<div align="center">

# a11y-sentinel

**Give your AI coding agent every WCAG 2.2 criterion — so it audits and fixes accessibility properly instead of guessing.**

A portable [Agent Skill](https://agentskills.io) for Claude Code, Cursor, Codex, and Gemini CLI. Loads the **complete WCAG 2.2 Level A/AA checklist** (all 55 success criteria) plus the US ADA legal context and a real audit procedure — the moment accessibility work starts.

</div>

---

## Why this exists

US web-accessibility lawsuits are at record highs — **~3,117 federal suits in 2025** (plus thousands more in state court), driven by templated complaints against businesses of every size. There is **no small-business exemption.** Yet most AI agents "fix accessibility" by pattern-matching a few obvious issues and calling it done.

The problem isn't detection — [axe](https://github.com/dequelabs/axe-core), Lighthouse, and pa11y already catch the machine-detectable ~30–40%. The problem is the **other ~60–70%**: *is the alt text meaningful? is focus order logical? do labels describe? is the ARIA correct?* That requires judgment against the **full** criteria set — which is exactly what this skill loads into your agent.

`a11y-sentinel` is **not another scanner** and **not an overlay widget** (those don't work and get you *sued* — the FTC fined one $1M in 2025). It makes your agent **fix the source code**, checking against every requirement.

## What's inside

| File | What it gives the agent |
|---|---|
| **`SKILL.md`** | The full **55-criterion WCAG 2.2 A/AA checklist** (every SC, level, what to check, common failure) · the audit workflow · risk-based triage · the *judgment layer* scanners can't do · mobile/PDF/third-party coverage |
| **`reference/legal.md`** | ADA Title II/III, Section 508, ACAA, HHS 504 · the version-by-statute matrix · state damages (CA Unruh $4k/violation, NY) · key case law · the overlay warning · accessibility-statement requirements |
| **`reference/auditing.md`** | Copy-paste axe / pa11y / Lighthouse / IBM commands · the required manual tests + screen-reader matrix · the WCAG-EM report format |

It targets **WCAG 2.1 AA as the legal floor and builds to 2.2 AA** — correctly handling the obsolete 4.1.1 (Parsing) and the new 2.2 criteria (target size, dragging, accessible auth, focus-not-obscured, consistent help, redundant entry).

## Install

```bash
npx skills add https://github.com/skeletont638-code/a11y-sentinel
```

Or just copy `skills/accessibility-audit/SKILL.md` into your project's `.claude/skills/` (or paste it into any agent chat). It activates whenever you work on accessibility, ADA/WCAG compliance, alt text, contrast, keyboard nav, screen readers, ARIA, form labels, captions — or respond to a demand letter.

## How to use it

Once installed, just ask your agent to work on accessibility:

> *"Audit this page for WCAG 2.2 AA and fix what you can."*

The agent now has every criterion in context, runs the automated + manual workflow, fixes the source code by risk-based priority (transaction-blockers first), and writes an honest report — instead of guessing.

## Honest scope

- **This is an engineering reference, not legal advice.** Consult counsel for a specific matter.
- **Automated checks are a floor, not a verdict.** A clean scan ≠ conformance; the manual pass is required.
- **Never claim "fully ADA compliant."** That becomes an admission when violations exist (and an FTC false-advertising risk). Underclaim; cite an honest target.

## License

MIT — see [LICENSE](LICENSE). Contributions welcome; open an issue or PR.
