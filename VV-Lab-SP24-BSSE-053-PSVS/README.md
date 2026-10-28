# VV-Lab-SP24-BSSE-053-PSVS

Verification and Validation lab project: Polar Seed Vault System (PSVS).

| | |
|---|---|
| Student | Faizan Ali |
| Roll No. | SP/24/BSSE/053 |
| Course | Software Verification & Validation (SV&V) |
| Teacher | Saleha Yousaf |

## About the system
A polar vault stores sealed boxes of crop seeds deposited by registered institutions (gene banks, universities, governments). Each box holds seed samples of one species. The vault has several freezer chambers. Depositors keep ownership of their boxes; the vault is a custodian, not an owner.

## Repository layout
This repository has one folder and one file. All lab artefacts are sections of this README.md:

| Section | Content |
|---------|---------|
| 1 | Requirements PSVS-REQ-v1.0 (S1-S12), baseline-1 |
| 2 | Change-request template |
| 3 | Defect taxonomy |
| 4 | Defect log |
| 5 | Peer review comparison |
| 6 | Summary table and chart |

## Tags and branches
| Name | Meaning |
|------|---------|
| baseline-1 | Requirements S1-S12 as issued (PSVS-REQ-v1.0), before defect analysis |
| main | Approved work only |
| defect-analysis | Taxonomy, defect log and summary; merged into main when complete |        


## 1. Requirements: PSVS-REQ-v1.0 (Baseline 1)

| ID | Requirement |
|----|-------------|
| S1 | The system shall accept seed boxes only from registered depositors. |
| S2 | Each chamber can hold a large number of boxes. |
| S3 | Chambers 1-3 hold at most 50,000 boxes each; Chamber 4 holds at most 20,000. |
| S4 | A box belongs to exactly one depositor, and only that depositor may withdraw it. |
| S5 | In an emergency, the vault authority may release any box to any requesting party. |
| S6 | Boxes shall be stored at a safe temperature. |
| S7 | Chamber temperature shall never rise above -18°C. |
| S8 | During maintenance, a chamber may be warmed to 0°C. |
| S9 | Seed samples with low viability shall be flagged promptly for regeneration. |
| S10 | A depositor may withdraw at most 20% of its boxes of a species per year. |
| S11 | A withdrawn box may be redeposited only after re-inspection. |
| S12 | The system shall keep a good audit trail of all actions. | 


## 2. Change-Request Template

Copy this table for every proposed change to a baselined artefact.

| Field | Entry |
|-------|-------|
| ID | CR-001 |
| Artifact | (section and version, e.g. Section 1, PSVS-REQ-v1.0, requirement S7) |
| Reason | (why the change is needed, e.g. defect D13: S7 contradicts S8) |
| Impact | (affected requirements, tests, effort and risk) |
| Approver | (name and role of the person who approves or rejects) |

Example:

| Field | Entry |
|-------|-------|
| ID | CR-001 |
| Artifact | Section 1, PSVS-REQ-v1.0, S7 |
| Reason | Defect D13: S7 ("never above -18°C") contradicts S8 (warming to 0°C during maintenance). |
| Impact | S6, S7, S8 change; a maintenance mode is needed; tests for S7 need a maintenance case. |
| Approver | Course teacher / requirements owner |  

# Task 2

## 3. Defect Taxonomy

| # | Category | Definition | Example |
|---|----------|------------|---------|
| 1 | Ambiguity | A statement can be understood in two or more different ways. | "Per year" in S10: calendar year or rolling 12 months? |
| 2 | Vagueness | A statement uses imprecise words with no measurable meaning. | "Safe temperature" in S6. |
| 3 | Incompleteness | Needed information is missing: conditions, actors, exceptions or failure behaviour. | S1 does not say what happens to an unregistered depositor. |
| 4 | Contradiction | Two requirements cannot both be satisfied. | S7 "never above -18°C" vs S8 "warmed to 0°C". |
| 5 | Non-verifiability | No test or measurement can decide whether the requirement is met. | "Good audit trail" in S12. |
| 6 | Redundancy | The same thing is stated more than once, risking inconsistent updates. | S2 repeats the idea of S3. |
| 7 | Infeasibility | The requirement cannot be achieved within physical or technical limits. | "Never rise above -18°C" cannot be guaranteed during a power failure. |
| 8 | Untraceability | A requirement cannot be linked to its source, rationale, design item or test. | S1-S12 have no source or rationale. |

Severity scale:
- Critical: safety, data loss or ownership/security violation possible.
- High: requirement cannot be implemented or tested as written.
- Medium: misunderstanding likely, but a workaround exists.
- Low: style or duplication only.
