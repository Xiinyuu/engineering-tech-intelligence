# Human-in-the-Loop Engineering Technology Intelligence

A portfolio-oriented n8n workflow for turning high-volume, heterogeneous technical information into **structured evidence for engineering review**.

The project demonstrates a practical pattern for industrial AI decision support:

**collect / ingest → normalize → deduplicate → filter noise → assess relevance → classify → score & summarize → human review**

> This public repository is a sanitized demonstrator. It contains no company data, supplier data, private source registry, internal database identifiers, or credentials.

## Why this project

Engineering R&D teams face more technical information than an individual engineer can review consistently. The challenge is not simply summarization: information must first be filtered, categorized, evaluated, and kept traceable to its source before it can support an engineering decision.

This workflow uses LLMs as **information-processing assistants**, while keeping the engineer in the loop for verification, prioritization, and downstream decisions.

## What the workflow does

1. Normalizes incoming technical items.
2. Removes duplicate items using link/title/content-derived keys.
3. Filters promotional and administrative noise.
4. Assesses whether an item is relevant to automotive powertrain engineering.
5. Classifies relevant items into technical domains.
6. Produces an engineering-value score and concise technical summaries.
7. Returns a structured record for human review and optional downstream storage.

## Human-in-the-loop design

The system does **not** autonomously make engineering decisions.

LLM outputs are treated as intermediate evidence:
- the original title/content/link remain available for traceability;
- summarization is constrained to the supplied source text;
- scoring is separated from relevance filtering;
- unsupported claims of external verification are explicitly avoided;
- final interpretation and use remain with an engineer.

This makes the workflow a small demonstrator of **human-in-the-loop decision support and trustworthy industrial AI** rather than a fully autonomous agent.

## Architecture

See [`docs/architecture.md`](docs/architecture.md).

## Repository structure

```text
engineering-tech-intelligence/
├── README.md
├── SECURITY.md
├── PUBLICATION_CHECKLIST.md
├── workflow
│   └── public-demo.json
├── prompts/
│   ├── noise-filter.zh.md
│   ├── powertrain-relevance.zh.md
│   ├── engineering-value-scoring.zh.md
│   └── technical-summarization.zh.md
├── examples/
│   ├── sample-input.json
│   └── sample-output.json
└── docs/
    └── architecture.md
```

## Two workflow files

### `public-demo.json`
The recommended file for a public portfolio. It starts from synthetic demo articles and contains no private Feishu/Lark integration. After import, attach your own supported LLM credentials in n8n.

### `sanitized-reference.json`
A closer representation of the production architecture. Private identifiers and credential references have been removed or replaced with placeholders. It is included to show the full integration pattern, not as a zero-configuration demo.

## Important implementation fixes included in the public version

The sanitized version also corrects several issues discovered during publication review:

- scoring levels now use thresholds consistent with a 0–100 total score (`>=80` high, `>=50` medium);
- deduplication reads the normalized article-title/link field names correctly;
- duplicate detection prefers canonical link/title across sources instead of automatically including the source name;
- the noise-filter label typo `Irrelavent` is corrected to `Irrelevant`;
- engineering-value scoring no longer instructs the LLM to claim an external industry search when no retrieval/search tool is connected.

## Technology

- n8n
- LLM-based classification and summarization
- JavaScript transformation nodes
- RSS/API/database integrations in the private deployment
- structured JSON-style outputs for downstream knowledge systems

## Language

The production source corpus is primarily Chinese, so the included prompt templates are in Chinese. The architecture and methodology are language-agnostic and can be adapted by replacing the prompt layer.

## Scope and limitations

This is a workflow demonstrator, not a validated autonomous engineering system. LLM classifications and scores can be inconsistent, sensitive to prompt/model changes, and wrong. For consequential engineering use, evaluation datasets, confidence/uncertainty handling, provenance tracking, access control, and formal human-review gates should be added.

## Publication note

The production implementation uses private source registries and collaborative database integrations. Those integrations are intentionally excluded from the public demonstrator.
