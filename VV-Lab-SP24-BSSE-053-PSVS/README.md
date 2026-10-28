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


## 4. Defect Log

| Defect ID | Req ID | Category | Description | Evidence | Severity | Suggested fix | Status |
|-----------|--------|----------|-------------|----------|----------|---------------|--------|
| D01 | S1 | Incompleteness | "Registered" is not defined: no registry, no registration process, no behaviour for an unregistered depositor. | S1: "only from registered depositors" | High | Add a depositor registry; reject and log a deposit from an unregistered ID with a reason code. | Open |
| D02 | S1 | Ambiguity | "Depositors" differs from the scenario's "registered institutions"; unclear if individuals can register or what happens if registration is revoked. | Scenario: "registered institutions (gene banks, universities, governments)" | Medium | Define depositor = registered institution; define status of boxes when registration is revoked. | Open |
| D03 | S2 | Vagueness | "A large number of boxes" gives no number. | S2: "a large number of boxes" | Medium | Delete S2 (numbers are in S3) or give a measurable capacity. | Open |
| D04 | S2, S3 | Redundancy | S2 says in general what S3 says exactly; it adds no testable content. | S2 "large number" vs S3 "at most 50,000 / 20,000" | Low | Merge S2 into S3. | Open |
| D05 | S3 | Incompleteness | Only chambers 1-4 are given though the scenario says "several"; no rule for which chamber gets a box or what happens when a chamber is full. | S3 lists Chambers 1-3 and 4 only | High | List every chamber with capacity; define allocation and the behaviour when full. | Open |
| D06 | S4 | Ambiguity | "Withdraw" is not defined (physical return, ownership transfer, or access?); no rule if a depositor dissolves or merges. | S4: "only that depositor may withdraw it" | Medium | Define withdrawal and a procedure for ownership transfer or succession. | Open |
| D07 | S4, S5 | Contradiction | S4 says only the owner may withdraw; S5 lets the authority release any box to any party. | S4 "only that depositor" vs S5 "any box to any requesting party" | Critical | Make S4 "except release authorised under S5" and restrict S5 with conditions. | Open |
| D08 | S5 | Vagueness | "Emergency" is not defined; nobody is named who declares it; no criteria. | S5: "In an emergency" | Critical | Define emergency types, who declares one and how it ends. | Open |
| D09 | S5 | Ambiguity | "The vault authority" and "any requesting party" are unbounded; this also conflicts with the vault being a custodian, not an owner. | S5: "vault authority ... any requesting party" | High | Name the authorised roles (for example two-person approval) and the eligible requesting parties. | Open |
| D10 | S5, S12 | Incompleteness | Emergency releases have no logging or notification rule; a release could leave no trace and the owner might never know. | S5 has no audit clause; S12 says only "all actions" | High | Log every emergency release (who, why, when, box) and notify the depositor. | Open |
| D11 | S6 | Vagueness | "Safe temperature" has no value, tolerance or measurement point. | S6: "a safe temperature" | High | State the numeric limit (for example at or below -18°C) or delete S6. | Open |
| D12 | S6, S7 | Redundancy | S6 describes in words what S7 states numerically. | S6 "safe temperature" vs S7 "-18°C" | Low | Merge S6 into S7. | Open |
| D13 | S7, S8 | Contradiction | S7 forbids any temperature above -18°C; S8 allows warming to 0°C during maintenance. | S7 "never rise above -18°C" vs S8 "warmed to 0°C" | Critical | Change S7 to "except in authorised maintenance mode (S8)" and define that mode, including what happens to the boxes. | Open |
| D14 | S7 | Infeasibility | "Never" cannot be guaranteed (power failure, door opening, sensor error) or tested; no measurement point, tolerance, duration or breach reaction. | S7: "shall never rise above" | High | Use: measured at a defined point, alarm within a set time of a breach, maximum excursion time. | Open |
| D15 | S8 | Incompleteness | S8 is only a permission: no authorisation, no rule for boxes inside, no maximum duration, no recovery rule. | S8: "a chamber may be warmed to 0°C" | High | Define who authorises, require boxes to be moved or protected, set a maximum duration and recovery rule. | Open |
| D16 | S9 | Non-verifiability | "Low viability", "promptly" and "regeneration" are undefined, so no test can pass or fail; how and when viability is measured is missing. | S9: "low viability ... flagged promptly" | High | "When germination test is below X percent, flag within 24 hours; test every N years." | Open |
| D17 | S9, S10 | Contradiction | Regeneration needs a withdrawal, but S10 caps withdrawals at 20 percent per year and S4 allows only the depositor. | S9 "regeneration" vs S10 "at most 20%" | High | State whether regeneration is exempt from S10 and who may perform it. | Open |
| D18 | S10 | Ambiguity | "Per year" may be calendar or rolling 12 months; base for 20 percent (start of year or current stock) and rounding (20 percent of 3 boxes) are undefined. | S10: "at most 20% ... per year" | High | Define the period, base count and rounding rule. | Open |
| D19 | S10, S11 | Incompleteness | Not stated whether a redeposited box restores the allowance, or whether S5 emergency releases count toward the 20 percent. | S10, S11, S5: no interaction rule | Medium | Add a rule for how redeposit and emergency releases affect the allowance. | Open |
| D20 | S11 | Incompleteness | "Re-inspection" is not defined: who does it, what is checked, what happens if it fails. | S11: "only after re-inspection" | High | Define inspector role, checklist, pass/fail criteria and action on failure. | Open |
| D21 | S12 | Non-verifiability | "Good" and "all actions" cannot be tested; fields, retention period and tamper protection are missing. | S12: "a good audit trail of all actions" | High | Specify fields (who, what, when, box ID, result), retention and append-only protection. | Open |
| D22 | S1-S12 | Untraceability | No requirement has a source, rationale, owner or acceptance test. | Requirement table has only ID and text | Medium | Add columns Source, Rationale, Verification method and trace links. | Open |
| D23 | S10 (scenario) | Incompleteness | Scenario says each box holds one species, but no requirement makes the system record or enforce the species at deposit, though S10 depends on it. | Scenario: "Each box holds seed samples of one species" | Medium | Add: species is mandatory at deposit and one box holds exactly one species. | Open |

Cross-requirement defects: D04 (S2, S3), D07 (S4, S5), D10 (S5, S12), D12 (S6, S7), D13 (S7, S8), D17 (S9, S10), D19 (S10, S11).
