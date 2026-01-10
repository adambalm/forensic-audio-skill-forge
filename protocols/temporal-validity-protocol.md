# Temporal Validity Protocol

An extension to the Black Flag Protocol for managing document validity, supersession, and temporal state in multi-agent knowledge systems.

## Purpose

As knowledge evolves, earlier decisions become outdated. Without explicit validity tracking, LLMs may cite stale information or contradict current architecture. This protocol establishes:

1. How documents declare their validity state
2. How LLMs should interpret and prioritize documents
3. How supersession chains are maintained
4. When human intervention is required

## Document Classification

### Temporal Types

Every decision or specification document has a temporal type:

| Type | Definition | Example |
|------|------------|---------|
| `static` | True from a point in time, never changes | "We chose tool X on 2024-03-15" |
| `dynamic` | Currently true but may change | "Memory is centralized on adambalm" |
| `atemporal` | Always true regardless of time | "SQLite databases are machine-local" |

### Document Status

| Status | Meaning | LLM Behavior |
|--------|---------|--------------|
| `canonical` | Current authoritative version | **Cite freely** |
| `superseded` | Replaced by newer document | **Do not cite as current truth** |
| `draft` | Under development | Cite only if explicitly discussing drafts |
| `deprecated` | Discouraged but not replaced | Cite with caveat |
| `archived` | Historical record only | Never cite as guidance |

## LLM Bootstrap Rules

These rules MUST be followed by any agent accessing shared knowledge:

### Rule 1: Status Check
Before citing any decision or protocol document, check its `status` field:
- `canonical` → Safe to cite as current truth
- `superseded` → Follow supersession chain, cite terminal canonical document
- `draft` → Only mention if user asks about work-in-progress
- `deprecated` → Mention with explicit caveat
- `archived` → Do not cite as guidance

### Rule 2: Supersession Chain
If a document is `superseded`, trace the chain:
```
Old Decision (superseded)
  → superseded_by → Intermediate (superseded)
    → superseded_by → Current (canonical)
```
Always cite the terminal `canonical` document.

### Rule 3: Staleness Detection
If `last_verified` is older than 90 days AND `temporal_type` is `dynamic`:
- Flag to human: "This decision may be stale"
- Do not treat as authoritative without verification

### Rule 4: Conflict Resolution
If two `canonical` documents contradict:
1. Prefer the one with more recent `valid_from`
2. Flag the conflict to human
3. Do not synthesize or guess resolution

## Verification Cadence

| Document Type | Verification Frequency |
|---------------|----------------------|
| Architecture decisions | Quarterly |
| Protocol definitions | Monthly |
| Tool configurations | Weekly |
| Contact/reference info | As-needed |

## Integration with Black Flag Protocol

This protocol adds these clauses to Black Flag:

- **Clause 15**: Validity Check
  > Before citing stored knowledge, verify document status is `canonical`. Superseded documents are historical record only.

- **Clause 16**: Staleness Flag
  > Dynamic decisions not verified within 90 days require human confirmation before treating as authoritative.

- **Clause 17**: Conflict Escalation
  > Contradictions between canonical documents MUST be flagged to human. Do not resolve by inference.
