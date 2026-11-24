# Topic 4 — Data Quality, Bias and Responsible Data Assessment Report

**Project:** UniGuide — An AI-Powered Academic Information Assistant for UTM Undergraduate Students

**Version:** 1.0

**Quality Gate Decision:** GO WITH CONDITIONS

## 1. Data Quality Scorecard

The purpose of this assessment is to evaluate the quality of the
prepared academic documents before proceeding to subsequent
AI system development activities.

The original dataset contained 285 chunks extracted from three
UTM academic documents. Following validation, manual review
and duplicate detection, 262 chunks were retained.

The following scores represent engineering judgement based
on the available evidence, using a scale of 1 to 5.
N.V. indicates that the dimension has not been fully verified.

| Quality Dimension | Score | Evidence | Recommended Action |
|---|---|---|---|
| Completeness | 3/5 | All three selected sources are represented, but programme handbooks are missing and some chunks were excluded. | Expand source coverage and review quarantined chunks. |
| Consistency | 4/5 | No hard structural validation failures were identified, but a potential calendar date inconsistency remains. | Verify dates and maintain consistent metadata. |
| Accuracy | 3/5 | Manual inspection identified extraction noise and incomplete academic statements. | Verify suspicious text against original PDFs. |
| Timeliness | N.V. | Document editions and academic sessions are identifiable, but their current official status has not been verified. | Confirm document versions with official UTM sources. |
| Uniqueness | 5/5 | No exact duplicate candidates were detected in the reviewed corpus using SHA-256 hashing. | Repeat duplicate checks after future updates. |

The dataset demonstrates good structural quality. However,
semantic accuracy, completeness and document currency
require further attention.

## 2. Validation and Data-Defect Findings

Pandera validation and additional profiling checks were used
to identify structural problems, missing information,
corrupted characters and suspiciously short text.

### 2.1 Validation Results

| Validation Check | Number of Affected Chunks |
|---|---:|
| Missing text | 0 |
| Missing source | 0 |
| Detected corrupted characters | 0 |
| Noisy whitespace | 0 |
| GID extraction errors | 0 |
| Hard validation failures | 0 |
| Short-text warnings | 26 |
| Additional suspicious OCR chunks | 2 |

The short-text threshold of 100 characters was used as a
warning condition rather than an automatic rejection rule.

A total of 26 chunks, representing 9.12% of the original
dataset, triggered the short-text warning.

Two additional chunks were flagged because manual inspection
identified suspicious OCR or extraction noise.

### 2.2 Manual Review and Triage

All 28 flagged chunks were manually reviewed.

| Decision | Number of Chunks |
|---|---:|
| Retain | 5 |
| Remove | 7 |
| Quarantine | 16 |
| Total | 28 |

Examples of reviewed cases are shown below.

| Chunk ID | Finding | Decision | Justification |
|---|---|---|---|
| 1 | Unreadable extracted text from the academic regulations cover page. | Quarantine | Requires verification against the original PDF. |
| 10 | Isolated contents heading and page number. | Remove | Contains no meaningful standalone academic information. |
| 150 | Incomplete statement concerning academic status and CGPA. | Quarantine | Missing context could result in misleading academic advice. |
| 251 | Significant extraction noise from the final page. | Quarantine | Text is unsuitable for reliable retrieval without verification. |
| 252 | Identifies the registration guide's intended audience. | Retain | Provides important information about the document's scope. |
| 260 | Instructions for viewing the course registration slip. | Retain | Short but meaningful academic guidance. |

The review demonstrates that short chunks are not necessarily
defective. Some contain useful information and should be
retained.

The detailed validation and triage evidence is recorded in:

- docs/week4_validation_failures.csv
- docs/week4_triage.csv

## 3. Duplicate and Anomaly Findings

Exact duplicate detection was performed using SHA-256 hashing
after normalising whitespace in the reviewed chunks.

| Processing Stage | Number of Chunks |
|---|---:|
| Original prepared dataset | 285 |
| After manual review | 262 |
| Exact duplicate candidates | 0 |
| After duplicate review | 262 |

A total of 23 chunks were excluded through manual review.
The cleaned dataset retains 91.93% of the original chunks.

No exact duplicate candidates were identified in the reviewed
corpus. However, this method does not detect all semantic
duplicates or differently worded repeated information.

Other identified anomalies include:

- OCR and PDF extraction noise.
- Incomplete sentence boundaries.
- Isolated headings and word fragments.
- A potential year inconsistency in the academic calendar.

The calendar inconsistency requires verification against
the original document before any correction is made.

Duplicate review evidence is stored in:

docs/week4_duplicate_review.csv

## 4. Representation Coverage and Bias Assessment

### 4.1 Source Coverage

| Source | Cleaned Chunks | Percentage | Pages Represented | Original Pages |
|---|---:|---:|---:|---:|
| Academic Regulations 2026 | 232 | 88.55% | 74 | 81 |
| Course Registration Guide 2026/2027 | 13 | 4.96% | 10 | 10 |
| Academic Calendar 2026/2027 | 17 | 6.49% | 2 | 2 |
| Total | 262 | 100% | 86 | 93 |

Academic regulations represent the largest proportion of the
dataset. This is partly explained by the original document
lengths.

Adequate coverage does not require equal chunk counts.
Instead, every supported academic task should have sufficient
authoritative evidence.

Page representation indicates that at least one chunk from
a page is present. It does not guarantee that all information
on that page has been preserved.

The coverage visualisation is stored in:

docs/week4_coverage_by_source.png

### 4.2 Identified Bias Risks and Propagation

| Bias Risk | Origin | Corpus Effect | Potential Retrieval Effect | Potential User Impact |
|---|---|---|---|---|
| Representation bias | Unequal source document lengths | Academic regulations dominate the corpus | Other topics may have fewer retrieval opportunities | Registration or calendar answers may be less relevant |
| User coverage bias | Registration guide targets senior full-time students | Other student groups are underrepresented | Applicable guidance may not be retrieved | New students may receive unsuitable guidance |
| Measurement and processing bias | PDF extraction and chunking decisions | Important academic statements may be fragmented or excluded | Supporting evidence may become unavailable | Students may receive incomplete academic answers |
| Knowledge coverage bias | Programme handbooks are absent | Programme-specific information is missing | Relevant programme evidence cannot be retrieved | Programme-specific questions may remain unanswered |

These are potential data-level bias risks. They do not prove
that the final retrieval or generation system is biased.

Further retrieval and answer evaluation will be required
during subsequent development activities.

## 5. Privacy, Consent, Rights and Data Governance

### 5.1 Privacy and Consent

UniGuide is designed to answer general academic enquiries.
It does not require access to individual student academic
records, identification numbers or login credentials.

The course registration guide contains a sample registration
slip on Page 9. This page requires further inspection to
determine whether unnecessary personal information is present.

Any identified personal information should be removed or
anonymised before the dataset is approved for deployment.

The project does not intentionally collect personal
information directly from students. Consent requirements
should be assessed according to the actual information
identified and its intended use.

### 5.2 Copyright and Access Rights

| Document | Intended Use | Access Rights Status |
|---|---|---|
| Academic Regulations 2026 | Academic regulations and policies | To be verified |
| Course Registration Guide 2026/2027 | Registration procedures | To be verified |
| Academic Calendar 2026/2027 | Academic dates and schedules | To be verified |

Public accessibility does not automatically grant permission
to redistribute copyrighted documents or their extracted
contents.

Access rights and permitted usage must be verified before
public deployment or redistribution through GitHub.

### 5.3 Data Governance Practices

| Governance Area | Practice |
|---|---|
| Traceability | Preserve source IDs, document names and page numbers. |
| Integrity | Use SHA-256 hashing for integrity and duplicate checks. |
| Version control | Record document versions and academic sessions. |
| Access control | Restrict access to sensitive or unapproved data. |
| Cleaning records | Preserve manual triage decisions and reasons. |
| Retention | Maintain original documents securely for verification. |
| Updates | Reprocess and validate updated official documents. |
| Redistribution | Publish only files that are authorised for sharing. |

## 6. Mitigation Plan and Residual Risk

| Identified Risk | Proposed Mitigation | Priority | Status |
|---|---|---|---|
| OCR and extraction noise | Verify suspicious chunks against original PDF pages. | High | Pending |
| Incomplete academic statements | Improve sentence-aware chunking and restore verified information. | High | Pending |
| Potential calendar inconsistency | Confirm dates against the official academic calendar. | High | Pending |
| Potential personal information | Inspect the sample registration slip and anonymise sensitive information if present. | High | Pending |
| Unverified access rights | Confirm permitted document usage and redistribution rights. | High | Pending |
| Unverified document currency | Confirm the latest applicable document editions. | High | Pending |
| Missing programme handbooks | Include relevant approved programme handbooks. | Medium | Pending |
| Unequal source representation | Evaluate retrieval separately across academic topics. | Medium | Planned |

### Residual Risk

Although the dataset has been structurally validated and
cleaned, important academic information may still be missing
or incomplete.

The exclusion of 16 quarantined chunks reduces exposure to
unreliable text but may also reduce information coverage.

Document currency, privacy and access rights remain
unverified. Therefore, the dataset should not be considered
fully approved for public deployment.

## 7. Impact on Topic 2 Requirements and Evaluation Criteria

The Topic 4 assessment supports the requirements defined
in the Topic 2 UniGuide Requirements Specification.

| Requirement | Topic 4 Contribution | Remaining Limitation |
|---|---|---|
| FR1 | Reviewed academic regulation content. | Programme handbooks are missing. |
| FR2 | Preserved registration and calendar sources. | Some registration information requires verification. |
| FR3 | Maintained source and page metadata. | Final citation correctness requires system testing. |
| FR4 | Identified knowledge gaps and unsupported areas. | Insufficient-information behaviour must be implemented and tested. |
| FR5 | Removed or quarantined unclear text. | Generated answer clarity remains untested. |
| NFR1 | Established a reviewed corpus for subsequent development. | Response latency has not been measured. |
| NFR2 | Reduced exposure to defective academic text. | Factual answer correctness requires evaluation. |
| NFR3 | Established repeatable validation procedures. | End-to-end reliability remains untested. |
| NFR4 | Preserved source metadata and repeatable processing. | Document update time has not been tested. |
| RAI1 | Improved traceability and identified misinformation risks. | Citation-source correctness requires evaluation. |
| RAI2 | Documented knowledge and user coverage limitations. | Refusal and redirection behaviour remains untested. |
| RAI3 | Identified potential privacy concerns. | Original document inspection and privacy testing remain necessary. |

### Topic 2 Evaluation Targets

| Requirement | Original Evaluation Target | Topic 4 Status |
|---|---|---|
| NFR1 | p90 response latency of 10 seconds or less | Not yet evaluated |
| NFR2 | Correct answer rate of at least 80% | Not yet evaluated |
| NFR3 | Successful query handling rate of at least 95% | Not yet evaluated |
| NFR4 | Document update time of 10 minutes or less | Not yet evaluated |
| RAI1 | Citation-source correctness rate of at least 95% | Not yet evaluated |
| RAI2 | Correct refusal and redirection rate of at least 95% | Not yet evaluated |
| RAI3 | Zero unnecessary personal information disclosures | Not yet evaluated |

Topic 4 provides dataset-level evidence supporting these
requirements. It does not demonstrate that the final
system-level evaluation targets have been achieved.

## 8. Topic 4 Quality Gate Decision

### Decision: GO WITH CONDITIONS

The UniGuide dataset is conditionally suitable for continued
controlled development and subsequent model selection.

This decision is supported by the following measured findings:

- 285 original chunks were assessed.
- No hard structural validation failures were identified.
- All 28 flagged chunks were manually reviewed.
- Seven chunks were removed.
- Sixteen chunks were quarantined.
- Five flagged chunks were retained.
- No exact duplicate candidates were detected.
- All three selected academic sources remain represented.
- A cleaned dataset containing 262 chunks was generated.

### Conditions

1. Verify quarantined academic information against the
   original PDF documents before restoring it.
2. Resolve the potential academic calendar date inconsistency.
3. Inspect the sample registration slip for personal information.
4. Verify document currency, access rights and permitted usage.
5. Expand programme-specific and student-group coverage
   before claiming full application scope.
6. Evaluate retrieval relevance, answer correctness, citation
   accuracy and responsible AI behaviour in later activities.

Public deployment and unauthorised dataset redistribution
must remain on hold until the relevant governance and
accuracy concerns have been resolved.

### Conclusion

The Topic 4 assessment established a reviewed and traceable
academic corpus for UniGuide. Automated validation,
manual inspection, duplicate detection and coverage analysis
provided evidence of the dataset's strengths and limitations.

The cleaned corpus can support subsequent controlled
development activities, subject to the identified conditions.

The assessment does not establish final system accuracy,
fairness, reliability or deployment readiness.