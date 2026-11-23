# Week 4 — Data Quality and Bias Report

**Project:** UniGuide — UTM Academic Information Assistant  
**Course:** AI Engineering  
**Lab:** Topic 4 — Data Quality and Responsible Data Practices  
**Data Pathway:** A — PDF/TXT

## 1. Project and Data Overview

UniGuide is an AI-powered academic information assistant designed to help Universiti Teknologi Malaysia (UTM) students access information about academic regulations, course registration and academic schedules. The system aims to provide relevant answers using official university documents.

This audit evaluates the quality of the text data prepared during Topic 3 before its use in future AI retrieval and question-answering tasks.

**Related Topic 2 requirements:**
- Requirement 1: [Insert exact Topic 2 requirement ID for accurate academic information retrieval]
- Requirement 2: [Insert exact Topic 2 requirement ID for source traceability or reliable responses]

Three UTM documents were processed:

| Source ID | Document | Prepared Records |
|---|---|---:|
| S01 | Academic Regulations 2026 | 251 |
| S02 | Course Registration Guide 2026/2027 | 17 |
| S03 | Academic Calendar 2026/2027 | 17 |
| **Total** | | **285** |

The audit examined the prepared text output from the Topic 3 Part C PDF/TXT pipeline.

**Audited output:** `data/pipeline_v1/documents/prepared_text.jsonl`  
**Matching manifest:** `data/pipeline_v1/documents/pipeline_manifest.json`

A representative sample of 15 records was selected across the three sources. Automated validation was also performed on all 285 records.

The sample supports initial inspection but does not establish the quality of every extracted passage.

## 2. Five-Dimension Quality Scorecard

The prepared dataset was evaluated using five operational data-quality dimensions.

| Dimension | Finding and Evidence | Impact / Decision |
|---|---|---|
| Completeness | All 15 sampled records contained the required fields, and no empty text was detected. | Pass for sampled structural completeness; full content coverage not verified. |
| Consistency | No invalid source IDs or page numbers were detected in the sample. | Pass for checked metadata consistency. |
| Accuracy | Two records contained unreadable extracted text. Comparison with the original PDF identified them as the cover and final barcode page. | Warning: extraction quality requires additional monitoring. |
| Timeliness | The Academic Regulations document is dated 2026, while the other two sources relate to the 2026/2027 academic session. | Review: confirm that these remain the applicable versions before deployment. |
| Uniqueness | No repeated text records were detected in the 15-record sample. | Pass for sampled exact duplicates; wider semantic duplication not verified. |

The results indicate that the prepared dataset meets basic structural requirements. However, structural validity does not guarantee that all extracted content is readable, complete or accurate.

## 3. Validation Findings

Two project-specific validation rules were applied to all 285 prepared records.

**V1 — Basic Text Integrity**

Each record must contain non-empty text without unresolved `/gid` extraction patterns.

- Records tested: 285
- Passed: 285
- Failed: 0

**V2 — Source Traceability**

Each record must contain a recognised source ID, a valid positive page number and a non-empty source filename.

- Records tested: 285
- Passed: 285
- Failed: 0

Both validation rules achieved a 100% pass rate against their defined conditions.

However, manual inspection identified two unreadable records that passed V1. This demonstrates that basic automated validation is insufficient to detect all PDF extraction errors.

## 4. Duplicate, Anomaly and Coverage Findings

No exact repeated text records were detected in the 15-record sample.

Two suspicious records were identified:

| Record ID | Source | PDF Page | Finding |
|---|---|---:|---|
| 1 | S01 | 1 | Unreadable text extracted from the cover page |
| 251 | S01 | 81 | Unreadable text extracted from the final barcode page |

Inspection of the original PDF confirmed that these pages do not contain substantive academic regulations. Their extracted text should be reviewed for exclusion from future retrieval while retaining the original source document.

**Coverage assessment:**

Academic regulations are represented by 251 prepared records across 79 pages. These records support questions involving university academic policies.

Course registration information is represented by 17 prepared records across 10 pages. These records support questions about registration procedures and related guidance.

The academic calendar contributes another 17 records across two pages.

Although all three sources are represented, this does not confirm complete coverage of every academic question. Additional topic-level verification is required.

## 5. Bias Assessment

A potential **pipeline-induced bias** was identified during PDF text extraction.

Documents with clear, machine-readable text may be represented more accurately than documents containing scanned pages, complex layouts or images.

This may cause UniGuide's future retrieval system to favour well-extracted academic information while overlooking content affected by extraction errors.

Another potential issue is unequal source representation. Academic Regulations contributes 251 records, compared with 17 records each from the Course Registration Guide and Academic Calendar.

This difference does not automatically indicate bias because the documents have different lengths. However, it may affect retrieval if chunking and ranking are not properly evaluated.

**Proposed mitigation:**

- Review unreadable or suspicious text against original documents.
- Exclude confirmed non-content extraction artefacts from future retrieval.
- Evaluate question coverage across different academic topics.
- Preserve source references for verification.

These are potential risks, not evidence of unfair system behaviour. Model-level fairness and retrieval accuracy have not yet been evaluated.

## 6. Privacy, Rights and Governance

The dataset originates from UTM academic documents, with source references and preparation information recorded in the Topic 3 pipeline manifest.

The inspected material consists of institutional academic information rather than student-specific personal records. However, the complete dataset has not undergone a formal sensitive-information review.

The Academic Regulations publication includes a copyright notice restricting reproduction and use in information storage and retrieval systems without written permission.

Therefore, permission for UniGuide's intended document reuse is currently **Not Verified**.

Recommended safeguards include:

- Confirming permission or another valid legal basis before using restricted material in the intended retrieval system.
- Keeping original documents and source information traceable.
- Avoiding the publication of confidential or personally identifiable information.
- Revalidating documents whenever official academic policies are updated.

The project maintainer should be responsible for reviewing document versions and correcting identified extraction issues.

## 7. Mitigation and Impact on Requirements

Two improvements are prioritised.

**Improvement 1 — Extraction Quality Review**

Review suspicious text records and exclude confirmed non-content artefacts from future retrieval. Any extraction errors affecting actual academic information should be corrected using the original documents.

This supports the requirement for accurate academic information retrieval.

**Improvement 2 — Source Governance and Coverage Verification**

Verify document reuse permissions, confirm current document versions and assess whether important academic topics are adequately represented.

This supports reliable, traceable and responsible information delivery.

Both improvements should be completed before the prepared data is used in a deployed retrieval or question-answering system.

Residual risks include undetected OCR errors, incomplete topic coverage and future changes to university academic policies.

## 8. Quality-Gate Decision

**Decision: HOLD for downstream use of the audited dataset.**

The dataset passed both automated validation rules across all 285 prepared records, demonstrating acceptable basic text and metadata structure under the defined checks.

Nevertheless, manual inspection identified two extraction anomalies, showing that automated validation alone cannot guarantee content readability.

More importantly, permission for the intended reuse of the Academic Regulations publication has not been verified.

The dataset should therefore not proceed to downstream retrieval-system use until the relevant rights and permissions have been clarified.

**Conditions for re-review:**

1. Verify permission or another applicable legal basis for the intended document use.
2. Review and appropriately handle the two identified extraction anomalies.
3. Confirm the applicable document versions and inspect representative academic content against the original sources.

Once these conditions are addressed, the dataset can be reassessed for progression to the next development stage.

---

## Supporting Evidence

- Topic 3 pipeline notebook, including Week 4 validation cells.
- Prepared text output and corresponding pipeline manifest.
- Five-dimension data-quality inspection output.
- V1 and V2 full-dataset validation output.
- Manual extraction review identifying records 1 and 251.
- Source coverage output for S01, S02 and S03.

**Audit limitation:** The results establish basic data-quality findings for the specified prepared dataset. They do not demonstrate final retrieval performance, answer accuracy or system fairness.
