# Aditya-Bedarkar-University-Elective
An individual GenAI assignment proposing a multi-agent, hybrid (LLM + deterministic) architecture to automate elective/specialisation 
allocation for a PGDM-style cohort which can be scalable to other University elective allocation

# Agentic AI Solution — Student Elective Subject Allocation

An individual GenAI assignment proposing a multi-agent, hybrid (LLM + deterministic)
architecture to automate elective/specialisation allocation for a PGDM-style cohort.

## Problem

A fictional institute (The MoonLight Institute of Management Science) manually
allocates 14 major-specific electives to ~350–400 students across 5 majors,
with seat caps of 60–120 per elective. The manual, spreadsheet-based process
is slow and lacks a transparent audit trail.

## Approach

The design deliberately keeps all **mathematical scoring, ranking, and
capacity allocation inside deterministic Python scripts** — the LLM is never
allowed to perform calculations. The LLM's role is limited to orchestration,
policy interpretation, exception flagging, and drafting communications.
This separation is the core hallucination-prevention guardrail.

### Agent Architecture (5 agents)
- **Orchestrator Agent** — sequences the pipeline, calls scripts, escalates to humans
- **Policy & Data Validation Agent** — validates inputs, flags exceptions
- **Merit & Ranking Agent** — normalises scores, applies tie-breakers
- **Allocation & Compliance Agent** — matches preferences to seat caps, checks violations
- **Governance & Communication Agent** — compiles audit reports, drafts student letters

### Deterministic Scripts
| Script | Purpose |
|---|---|
| `validate_data.py` | Validates and cleans raw student records |
| `calculate_merit.py` | Computes normalised merit score (50% Academics, 20% Internship, 10% Case Competition, 20% Entrance Test) |
| `rank_students.py` | Assigns global rankings with tie-breaking logic |
| `allocate_electives.py` | Matches preferences against seat caps |
| `validate_allocation.py` | Checks for capacity overages, duplicate allocations, major mismatches |
| `generate_audit.py` | Compiles the final audit summary report |

### Guardrails
- LLM is strictly prohibited from editing scores or seat allocations
- Missing/conflicting data is flagged, never imputed or guessed
- If a policy rule isn't documented, the agent halts and reports "Ambiguity Detected"
- Results require mandatory human sign-off before publishing — nothing auto-publishes

## Validation

Tested on 15 golden test cases:
- 13 students correctly allocated end-to-end
- 2 students correctly isolated into the exceptions file (one invalid GPA, one missing entrance-test score)

## Repository Structure
Student_Elective_Allocation/
├── SKILL.md # Orchestrator agent instructions & guardrails
├── references/ # Policy, eligibility, weightage, tie-breaking rules
├── assets/ # Sample student data, communication template
├── scripts/ # Deterministic Python scripts
└── output/ # provisional/, exceptions/, audit/

## Author
Aditya Bedarkar — PGDM, Great Lakes Institute of Management, Chennai
