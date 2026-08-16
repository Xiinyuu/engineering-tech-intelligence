# Architecture

```mermaid
flowchart LR
    A[Technical information sources] --> B[Normalize]
    B --> C[Deduplicate]
    C --> D[LLM noise filter]
    D --> E[Powertrain relevance]
    E --> F[Domain classification]
    F --> G1[Engineering-value scoring]
    F --> G2[Technical summarization]
    G1 --> H[Structured evidence package]
    G2 --> H
    H --> I[Human engineering review]
    I --> J[Decision support / knowledge base]
```

## Design principle

The workflow is deliberately **decision-support**, not autonomous decision-making.  
LLMs reduce information-processing load; engineers retain responsibility for interpretation, verification, prioritization, and downstream decisions.

## Trust controls

- Source text is retained alongside every generated field.
- Summaries are instructed not to add information absent from the source.
- Relevance and noise filtering are separated from engineering-value scoring.
- The public version does not claim external web verification unless an explicit search/retrieval tool is connected.
- Low-information cases should be treated conservatively and escalated to human review.
