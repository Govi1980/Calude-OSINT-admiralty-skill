# Claude OSINT Admiralty Skill

A structured Claude prompt that turns it into an OSINT research assistant using NATO's Admiralty Code. Grades sources (A–F) and information credibility (1–6), resolves conflicting reports, forces re-verification of data from interested parties, and outputs a fully sourced, risk-annotated analysis.

> **Note**: the prompt itself (`prompt-osint-bot.md`) is written in Italian, the author's working language. The methodology is language-agnostic — translations and adaptations are welcome contributions.

## What it does

This prompt configures Claude to act as an OSINT (Open Source Intelligence) analyst across three domains:
- Research on public figures (institutional, corporate, professional)
- Threat intelligence (sentiment, reputational/security risk)
- Geopolitical events, terrorism, and organized crime monitoring — based exclusively on public reporting

It applies the **Admiralty Code** (NATO source-reliability grading system), separating:
- **Source reliability** (A–F): how trustworthy the outlet/institution is in general
- **Information credibility** (1–6): how credible this specific piece of information is

On top of the base method, it includes:
- A three-tier correlation model: **Datum → Information → Assessment**, with an explicit 0–10 confidence score calculated from a two-axis grid (best-source quality + independent corroboration)
- A disagreement-resolution system for conflicting sources (letter-grade gap, then credibility-number gap, with a fixed low score for genuine unresolved disagreement between comparable sources)
- A forced re-verification rule for quantitative data reported by an interested party (e.g. an event organizer, or a security actor reporting on its own theater of operations)
- A "party-to-the-dispute" cap: an institutional source evaluating its own mandate/competence area is capped at grade B, never A
- Operator-defined source calibration and topic-priority tables, populated interactively and confirmed before being saved — never applied silently
- A full output format: situational summary, per-question breakdown, closing narrative, a one-line "so what," a structured risk-signal analysis (source inconsistencies, disinformation patterns, coverage gaps, suspicious timing, undisclosed conflicts of interest, coordinated behavior), and a cited-sources table
- Rules for consistently explaining public figures, party affiliations, and acronyms in every report, with an interactive mechanism to permanently exclude or always-explain specific acronyms

## How to use it

Paste the contents of `prompt-osint-bot.md` into:
- A Claude.ai **Project's custom instructions**, or
- A **system prompt** via the Claude API, or
- A custom **Claude Skill** (`SKILL.md`)

The reference tables ("Fonti calibrate" / calibrated sources, "Override manuali" / manual overrides, "Fonti prioritarie per argomento" / topic-priority sources, and the acronym-handling lists) ship **empty** in this repository by design — see [Privacy note](#privacy-note) below. Populate them yourself using the built-in operator commands described in the prompt ("valuta fonte" / evaluate a source, "elenco fonti per argomento" / list sources by topic, "revisione fonti" / review sources).

## Privacy note

This public version deliberately excludes the original author's own source calibrations (e.g. specific reliability judgments about individual news outlets), since those reflect personal editorial judgment, not neutral methodology. Keep your own calibrations in your Claude memory/project files or in a private file — never assume someone else's calibration table is neutral or authoritative for your use case.

## Contributing

Pull requests are welcome — methodology refinements, translations, bug fixes in the logic, new evaluation criteria. Please open an issue first for significant changes so we can discuss the approach before you invest time in a PR.

## License

Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0). See [LICENSE](./LICENSE). In short: free to use, share, and adapt — always with attribution, never for commercial purposes, and any adapted version must carry the same license.
