# AI Contract Sentinel

Risk triage for AI-generated or AI-reviewed contracts.

> Version: 1.0.0 | License: MIT | Status: production-oriented v1 foundation

## Problem

Contracts increasingly include AI-generated clauses, but parties need transparent checks for hallucinated obligations, missing provenance, and risky automated edits.

## What this project solves

A contract review manifest checker that validates source documents, reviewer role, clause risk tags, and unresolved human review items.

AI Contract Sentinel ships as a small, dependency-free CLI and library. It validates a domain-specific JSON packet, emits actionable findings, and gives contributors a concrete surface for adding adapters, richer checks, schemas, and integrations.

## Who it is for

Legal ops teams, open legal tech contributors, procurement teams.

## Quick start

```bash
npm test
npm start -- sample
```

Analyze your own packet:

```bash
ai-contract-sentinel ./packet.json
```

Or pipe JSON:

```bash
cat packet.json | node src/cli.js
```

## Example packet

```json
{
  "contract": {
    "id": "msa-42",
    "jurisdiction": "NY"
  },
  "review": {
    "aiGeneratedClauses": [
      "data_processing"
    ],
    "humanReviewer": ""
  },
  "risks": [
    {
      "clause": "indemnity",
      "severity": "medium"
    }
  ]
}
```

## Library usage

```js
const { analyze } = require("./src/index.js");

const report = analyze({
  "contract": {
    "id": "msa-42",
    "jurisdiction": "NY"
  },
  "review": {
    "aiGeneratedClauses": [
      "data_processing"
    ],
    "humanReviewer": ""
  },
  "risks": [
    {
      "clause": "indemnity",
      "severity": "medium"
    }
  ]
});
console.log(report.summary);
```

## v1 behavior

- Validates required fields for the domain packet.
- Scores readiness from 0 to 100.
- Reports missing or weak governance evidence.
- Suggests next actions and contributor extension points.
- Runs fully offline with no API keys and no network access.

## Contribution map

Good first contributions:

- Add clause taxonomies.
- Add citation checkers.
- Add redline provenance.
- Add jurisdiction adapters.

Larger contributions:

- Add a JSON Schema and compatibility tests.
- Build import/export adapters for popular AI frameworks.
- Add real-world fixtures from public, non-sensitive examples.
- Improve scoring with transparent, documented heuristics.

## Project principles

- Human agency over blind automation.
- Open standards over vendor lock-in.
- Auditable decisions over hidden magic.
- Privacy and safety as design constraints, not release notes.

## GitHub Pages

The marketing site lives in `site/index.html`. Enable GitHub Pages from the `site` folder or use the included Pages workflow after publishing.

## Security

This project does not process secrets by default. If you build adapters that touch production systems, keep least privilege, explicit consent, and auditable logs in the design.
