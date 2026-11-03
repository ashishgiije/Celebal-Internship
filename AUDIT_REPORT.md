# Source Audit — Celebal-Internship

Reviewed 4 November 2026 against source commit `b13918eba4210ae4aeb6c2211db95dc582938f67`. This is a focused code/documentation review and selected local validation, not a penetration test or an exhaustive vulnerability scan. Application files and credentials were not changed. Secret values are intentionally omitted.

## Severity summary

| Critical | High | Medium | Low |
|---:|---:|---:|---:|
| 0 | 0 | 3 | 1 |

Critical: direct resource/identity boundary failure. High: serious exposure or a core reproducibility blocker. Medium: correctness, validation, or deployment issue. Low: maintenance or coverage gap. Static findings describe potential impact; only explicitly listed runtime checks were executed.

## Findings

### 1. Medium — Exercise 3

- **Affected file:** [week1_Ashish_gije.ipynb](<week1_Ashish_gije.ipynb>)
- **Evidence:** Exercise 3.1 constructs name_dept_df with only name although the prompt requests name and department; the assertion checks only the object type.
- **Potential impact:** The notebook can report success while the assignment requirement is unmet.
- **Recommended correction:** Select both columns and assert the exact column set.

### 2. Medium — Exercise 4

- **Affected file:** [week1_Ashish_gije.ipynb](<week1_Ashish_gije.ipynb>)
- **Evidence:** Exercise 4.2 assigns QP a boolean comparison instead of the Q @ P product.
- **Potential impact:** The displayed matrix comparison and noncommutativity assertion do not test the intended calculation.
- **Recommended correction:** Compute QP = Q @ P and compare the two numeric products.

### 3. Medium — The external delivery dataset is absent; Week 3 likewise references a missing country CSV

- **Affected file:** [week2_AshishGije.ipynb](<week2_AshishGije.ipynb>)
- **Evidence:** The external delivery dataset is absent; Week 3 likewise references a missing country CSV.
- **Potential impact:** Those experiments cannot run from the checkout alone.
- **Recommended correction:** Document provenance and retrieval with schema checks.

### 4. Low — RAG dependencies and model artifacts are not version-pinned

- **Affected file:** [week7_Ashish_Gije_Assignment/week7_Ashish_Gije.ipynb](<week7_Ashish_Gije_Assignment/week7_Ashish_Gije.ipynb>)
- **Evidence:** RAG dependencies and model artifacts are not version-pinned.
- **Potential impact:** LangChain interfaces and provider model availability can change.
- **Recommended correction:** Pin a tested environment and record a retrieval/generation smoke test.

## Validation evidence

Week 1: 26 nonempty code cells executed successfully, including existing assertions; other weeks unrun

## Review scope and limits

Reviewed tracked application source, entry points, manifests/configuration, routes and data models where present, existing documentation, and available test definitions. Generated dependencies and binary artifacts were inventoried rather than treated as authored application logic. Provider calls, cloud deployment, and external data/model claims remain unverified unless explicitly listed above. No secret was rotated and no migration was run against a user database.

## Priorities

Address Critical and High findings before public deployment. Then add regression tests for the affected boundary or workflow, fix Medium issues, and resolve Low maintenance findings. All application corrections require a separate reviewed coding change.
