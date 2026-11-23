Week 4 — Data Quality and Bias Report

Project: UniGuide: An AI-Powered Academic Information Assistant for UTM Undergraduate Students
Course: AI Engineering
Lab: Topic 4 — Data Quality and Responsible Data Practices
Data Pathway: A — PDF/TXT

1. Project and Data Overview

UniGuide is an AI-powered academic information assistant designed to help UTM undergraduate students obtain answers about academic regulations, course registration and academic schedules using official university documents.

This audit examines the quality of the text data prepared in Topic 3 and its suitability for future document retrieval and question answering.

Two Topic 2 functional requirements were selected:

Requirement	Description	Data Needed
FR1	Answer undergraduate academic enquiries related to UTM academic regulations, programme handbooks and academic guidelines.	Accurate, readable and sufficiently complete academic document text.
FR3	Provide references to relevant official UTM documents that support generated answers.	Reliable source IDs, filenames and page references.

The Week 2 evaluation criteria specify a target of at least 80% answer correctness for FR1/FR2 and at least 95% citation-source correctness for FR3/RAI1. These are future system evaluation targets, not results measured in this lab.

The audited data comes from Topic 3 Part C:

* Output: data/pipeline_v1/documents/prepared_text.jsonl
* Manifest: data/pipeline_v1/documents/pipeline_manifest.json

Source ID	Document	Records	Pages Represented
S01	Academic Regulations 2026	251	79
S02	Course Registration Guide 2026/2027	17	10
S03	Academic Calendar 2026/2027	17	2
Total		285	91

Fifteen records were selected across the three sources for representative inspection, using approximately five evenly distributed records per source. Automated validation was subsequently applied to all 285 records.

2. Five-Dimension Quality Scorecard

Dimension	Observed Finding and Evidence	Potential Impact	Decision
Completeness	All 15 sampled records contained required fields and non-empty text.	Missing academic content could prevent UniGuide from answering FR1 enquiries.	Pass for sampled structural completeness
Consistency	No invalid source IDs or page numbers were detected in the sample.	Inconsistent metadata could produce incorrect source references under FR3.	Pass for checked metadata
Accuracy	Two sampled records contained unreadable extraction artefacts. The original PDF shows that these correspond to a cover and barcode page.	Similar errors in substantive pages could reduce answer correctness.	Warning
Timeliness	The Academic Regulations publication is dated 2026; the other sources are labelled 2026/2027. Current applicability has not been independently confirmed.	Outdated rules or dates could lead to incorrect academic advice.	N.V. — current applicability
Uniqueness	No exact repeated text was detected within the 15-record sample.	Unnecessary duplication could influence retrieval results.	Pass for sampled exact duplicates

The findings show that the dataset satisfies basic structural checks. However, text readability, complete content coverage and source freshness require further verification.

3. Validation Findings

Two validation rules were applied to the full prepared dataset.

V1 — Basic Text Integrity (FR1)

Condition: Each record must contain non-empty text without unresolved /gid extraction patterns.

V2 — Source Traceability (FR3)

Condition: Each record must contain a recognised source ID, a positive integer page number and a non-empty source filename.

Rule	Records Tested	Passed	Failed	Action
V1	285	285	0	Retain records for further readability review
V2	285	285	0	Retain source metadata; verify citation correctness later

Both rules passed for all 285 records.

However, V1 did not identify two records containing unreadable text because those records were non-empty and contained no /gid patterns. Therefore, the results demonstrate compliance with the defined rules rather than complete extraction accuracy.

4. Duplicate, Anomaly and Coverage Findings

No exact repeated text was identified in the 15-record sample.

Two extraction anomalies were identified during manual inspection:

Record ID	Source	PDF Page	Observation
1	S01	1	Unreadable extracted text from the cover page
251	S01	81	Unreadable extracted text from the final barcode page

Comparison with the original PDF confirmed that these pages do not contain substantive academic regulations. Their corrupted text should be reviewed for exclusion from future retrieval, without deleting the original document.

Two task-relevant coverage areas were considered:

Academic regulations: The 251 prepared records from S01 provide material for answering questions about academic policies, assessment, registration rules and other undergraduate regulations. However, the completeness of individual policy sections has not been fully verified.

Course registration: The 17 records from S02 provide material for course registration enquiries. Their presence confirms source representation but not complete coverage of every registration procedure.

The academic calendar contributes another 17 records from S03, supporting future questions about semester schedules and important dates.

These observations are based on record counts and selected inspection, not a comprehensive assessment of every academic topic.

5. Bias Assessment

A potential pipeline-induced bias was identified in the document preparation process.

PDF pages containing machine-readable text may be extracted more accurately than scanned pages, complex tables or image-based content. This could result in some academic information being represented less clearly in the prepared dataset.

The possible consequence is that UniGuide may retrieve well-extracted information more frequently while overlooking relevant content affected by extraction problems.

There is also unequal representation across sources: S01 contributes 251 records, while S02 and S03 contribute 17 each. This difference is partly explained by document length and does not establish unfairness. Nevertheless, it should be considered during future retrieval evaluation.

Proposed controls: Compare suspicious prepared records with original PDFs, correct substantive extraction errors, review coverage across academic topics and evaluate retrieval results using questions from all three sources.

No claim about final model fairness or retrieval accuracy can be made because the question-answering system has not yet been evaluated.

6. Privacy, Rights and Governance

The dataset was prepared from three UTM academic documents. Source IDs and preparation information are recorded in the Topic 3 pipeline manifest.

The inspected records concern institutional academic information rather than individual student records. However, a complete sensitive-information audit has not been performed.

The Academic Regulations 2026 publication identifies UTM Press as its publisher and contains a copyright notice restricting reproduction and information storage and retrieval uses without written permission.

Therefore, permission for the intended downstream reuse remains Not Verified. The reuse rights of the other sources also require confirmation.

The original documents should be retained in approved storage, and restricted content should not be uploaded to a public repository without authorisation.

The project maintainer is responsible for reviewing source updates, checking permissions and revalidating prepared data whenever documents or extraction methods change.

A concrete safeguard is to maintain source references and restrict public distribution of original or extracted content until the relevant permissions are verified.

7. Mitigation and Impact on Requirements

Priority	Improvement	Responsibility and Timing	Requirement Impact
1	Review suspicious text and verify important extracted academic sections against the original PDFs.	Project developer, before retrieval implementation	FR1 — accurate academic information
2	Verify document reuse permissions, source versions and citation metadata.	Project developer with appropriate UTM source owners, before downstream use	FR3 — reliable official source references

The first improvement reduces the risk of incorrect or incomplete academic answers, supporting the future answer correctness target of at least 80%.

The second improvement supports reliable citations and responsible data use, contributing to the future citation-source correctness target of at least 95%.

These thresholds are evaluation targets and have not been measured in Topic 4.

Residual risks include undetected extraction errors, incomplete topic coverage, outdated academic information and unresolved reuse permissions.

8. Quality-Gate Decision

Decision: HOLD for downstream use of the audited dataset.

The dataset passed both automated validation rules across all 285 records, demonstrating acceptable basic text integrity and source metadata structure under the defined checks.

However, manual inspection identified two extraction anomalies, and the intended reuse permissions for the source documents have not been verified.

The dataset should therefore remain on HOLD for downstream retrieval-system use until these issues are addressed.

Conditions for re-review:

1. Confirm permission or another applicable legal basis for the intended document use.
2. Review and appropriately handle the identified extraction anomalies.
3. Verify source versions and inspect representative substantive academic content against the original documents.

Once these conditions are satisfied, the prepared dataset can be reassessed for further development.

⸻

Supporting Evidence

* Week 2 Requirements Specification — docs/week2_requirements.md
* Week 2 Evaluation Criteria — docs/week2_evaluation_criteria.md
* Week 3 prepared text output — data/pipeline_v1/documents/prepared_text.jsonl
* Week 3 pipeline manifest — data/pipeline_v1/documents/pipeline_manifest.json
* Week 3/Week 4 notebook — UniGuide_Week3_Pipeline_Week4_Data_Quality_Audit.ipynb
* Week 4 sample inspection, validation and source coverage outputs
* Original Academic Regulations 2026 PDF, pages 1 and 81

Audit limitation: The findings establish the observed quality of the audited prepared data under the stated checks. They do not establish final answer accuracy, retrieval performance, citation correctness or system fairness.
