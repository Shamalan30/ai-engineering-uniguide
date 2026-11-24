# UniGuide – UTM Academic Information Assistant

## 1. Project Overview

UniGuide is an AI-powered academic information assistant designed to help Universiti Teknologi Malaysia (UTM) students access academic information more easily.

The system uses official UTM academic documents as its knowledge sources to provide relevant information about academic regulations, course registration and academic schedules.

The project follows a structured AI engineering development process, covering requirements analysis, data preparation, pipeline development, data-quality assessment, bias evaluation and responsible data practices.

## 2. Project Objectives

- Provide students with easier access to UTM academic information.
- Reduce the time required to search through lengthy academic documents.
- Organise official academic information into structured and searchable data.
- Develop a reliable document-based academic information assistant.
- Ensure data quality, source traceability and responsible data handling.
- Provide answers supported by relevant document and page references.

## 3. Data Sources

The project currently uses three official UTM academic documents:

| Source ID | Document | Original Records | Cleaned Records |
|---|---|---:|---:|
| S01 | Academic Regulations 2026 | 251 | 232 |
| S02 | Course Registration Guide 2026/2027 | 17 | 13 |
| S03 | Academic Calendar 2026/2027 | 17 | 17 |
| **Total** | | **285** | **262** |

These documents provide the foundation for UniGuide's future document-based question-answering system.

## 4. Technologies Used

- Python
- Google Colab
- PyPDF
- Tesseract OCR
- Pandas
- Pandera
- Matplotlib
- LangChain Document Objects
- SHA-256 Hashing
- JSON / JSONL
- Pickle
- GitHub
- Markdown

## 5. Project Structure

```text
UniGuide/
│
├── data/
│   ├── pipeline_v1/
│   │   └── documents/
│   │       ├── prepared_text.jsonl
│   │       └── pipeline_manifest.json
│   ├── prepared_text.jsonl
│   ├── sources.csv
│   ├── week3_manifest (1).json
│   ├── prepared_chunks_clean.jsonl
│   └── chunks_clean.pkl
│
├── docs/
│   ├── week2_requirements.md
│   ├── week2_architecture_v1.png
│   ├── week3_pipeline_diagram.png
│   ├── week3_pipeline_decisions.md
│   ├── week3_data_inventory.md
│   ├── week4_data_quality_report.md
│   ├── week4_validation_failures.csv
│   ├── week4_duplicate_review.csv
│   ├── week4_coverage_by_source.png
│   └── week4_triage.csv
│
├── evaluation/
│   └── questions.csv
│
├── notebooks/
│   ├── Week 3 pipeline notebook
│   └── week4_quality.ipynb
│
├── prompts/
├── src/
└── README.md
```

Note: This structure represents the intended project organisation. Restricted source documents and datasets are maintained locally unless redistribution is authorised.

## 6. Data Processing Pipeline — Week 3

The UniGuide data pipeline prepares academic documents through the following stages:

1. **Data Collection:** Collect selected official UTM academic PDF documents.
2. **Text Extraction:** Extract document text using PyPDF.
3. **OCR Fallback:** Apply OCR when normal text extraction is insufficient.
4. **Text Cleaning:** Clean and organise the extracted text.
5. **Chunking:** Divide the extracted content into smaller sections using paragraph-aware chunking.
6. **Validation:** Verify that the prepared outputs exist and contain data.
7. **Provenance Tracking:** Record source fingerprints, output fingerprints and source-to-output mappings.

The pipeline produces structured JSONL records containing document text, source IDs, page references and record identifiers.

A total of 285 prepared records were generated for subsequent data-quality assessment.

## 7. Data Quality and Responsible Data Practices — Week 4

Week 4 focuses on evaluating the quality, reliability, representation and responsible use of the prepared dataset from Week 3.

### 7.1 Data Quality Assessment

The assessment covers five operational data-quality dimensions:

| Quality Dimension | Score |
|---|---:|
| Completeness | 3/5 |
| Consistency | 4/5 |
| Accuracy | 3/5 |
| Timeliness | Not Verified |
| Uniqueness | 5/5 |

The uniqueness score reflects exact duplicate detection only. Timeliness remains unverified because source currency has not been fully confirmed.

### 7.2 Automated Validation

Pandera was used to perform structured validation across all 285 prepared records.

The validation checks include:

- Non-empty document text.
- Valid source metadata.
- Valid source and page references.
- Detection of corrupted characters.
- Detection of unresolved GID extraction patterns.
- Valid and unique record identifiers.
- Identification of unusually short text chunks.

No hard validation failures were identified. However, short text fragments and suspicious extraction artefacts required further manual review.

### 7.3 Manual Inspection and Triage

A representative sample of 15 records was inspected across the three academic documents.

Following automated validation and anomaly identification, 28 flagged records were manually reviewed.

| Review Decision | Number of Records |
|---|---:|
| Retained | 5 |
| Removed | 7 |
| Quarantined | 16 |
| **Total Reviewed** | **28** |

The removal and quarantine of 23 records reduced the prepared dataset from 285 to 262 records.

Quarantined records require further verification against the original academic documents before they can be restored to the retrieval dataset.

Manual review decisions are recorded in `docs/week4_triage.csv`.

### 7.4 Duplicate Detection

SHA-256 hashing was applied to normalised text content to identify exact duplicate records.

| Metric | Result |
|---|---:|
| Records after manual triage | 262 |
| Exact duplicate candidates | 0 |
| Final cleaned records | 262 |

No exact duplicate records were detected. Semantic or near-duplicate content has not yet been evaluated.

### 7.5 Representation Coverage and Bias Assessment

The cleaned dataset contains records from all three selected academic documents.

| Source | Cleaned Records | Representation |
|---|---:|---:|
| Academic Regulations | 232 | 88.55% |
| Course Registration Guide | 13 | 4.96% |
| Academic Calendar | 17 | 6.49% |
| **Total** | **262** | **100%** |

The Academic Regulations document contributes the largest proportion of the dataset.

The identified potential bias risks include:

- Unequal representation of academic topics across document sources.
- Limited student-group coverage in the course registration guide.
- Information loss caused by extraction errors and quarantined records.
- Incomplete coverage of programme-specific information due to missing programme handbooks.

These risks may affect future retrieval opportunities and answer completeness.

Mitigation measures include expanding document coverage, reviewing quarantined records and evaluating retrieval performance across different academic topics and student groups.

Coverage visualisation: [Week 4 Source Coverage](docs/week4_coverage_by_source.png)

### 7.6 Responsible Data Practices

The project maintains source references and preparation information through its pipeline manifests and review records.

The following responsible data practices are applied:

- Preserve source IDs and original page references.
- Maintain records of validation and manual review decisions.
- Avoid unnecessary exposure of personal information.
- Verify source currency and document reuse permissions.
- Restrict public redistribution of unauthorised academic documents and extracted content.
- Revalidate datasets when source documents are updated.

Document reuse permissions and source currency remain outstanding verification requirements.

### 7.7 Quality-Gate Decision

**Decision: GO WITH CONDITIONS**

The cleaned dataset contains 262 records after automated validation, manual review and exact duplicate detection.

The dataset may proceed to permitted local development and evaluation, subject to the following conditions:

1. Verify quarantined records against the original academic documents.
2. Confirm source document versions and currency.
3. Resolve identified representation and coverage limitations.
4. Review potential personal information within source documents.
5. Verify document reuse and redistribution permissions.

Public deployment and unauthorised redistribution remain on hold until the relevant conditions are resolved.

**Full Week 4 Report:** [Data Quality and Bias Report](docs/week4_data_quality_report.md)

## 8. Current Project Progress

| Component | Status |
|---|---|
| Project setup and source identification | Completed |
| Week 2 requirements analysis | Completed |
| Data extraction using PyPDF | Completed |
| OCR fallback | Implemented |
| Text cleaning and chunking | Completed |
| Part B prepared dataset | Completed |
| Part B lineage manifest | Completed |
| Part C data pipeline | Implemented |
| Repeatability and provenance verification | Implemented |
| Week 4 quality-gate planning | Completed |
| Week 4 data inventory | Completed |
| Week 4 manual inspection | Completed |
| Pandera validation | Completed |
| Manual review and triage | Completed |
| SHA-256 duplicate detection | Completed |
| Representation coverage analysis | Completed |
| Bias and governance assessment | Documented |
| Week 4 Data Quality Report | Completed |
| Week 4 quality-gate decision | GO WITH CONDITIONS |
| Source currency and reuse permissions | Pending verification |
| Original PDF verification of quarantined records | Pending |
| Embedding and retrieval development | Not started |
| RAG system implementation | Not started |

## 9. Pipeline Outputs

### Week 3 Outputs

- `data/prepared_text.jsonl` — prepared document records.
- `data/week3_manifest (1).json` — Part B preparation and lineage information.
- `data/pipeline_v1/documents/prepared_text.jsonl` — structured pipeline output.
- `data/pipeline_v1/documents/pipeline_manifest.json` — pipeline configuration, fingerprints and provenance information.

### Week 4 Outputs

| File | Description |
|---|---|
| `notebooks/week4_quality.ipynb` | Week 4 implementation and assessment notebook |
| `data/prepared_chunks_clean.jsonl` | Cleaned dataset containing 262 records |
| `data/chunks_clean.pkl` | Serialised cleaned document objects |
| `docs/week4_data_quality_report.md` | Final data quality and bias assessment report |
| `docs/week4_validation_failures.csv` | Automated validation findings |
| `docs/week4_duplicate_review.csv` | Exact duplicate detection results |
| `docs/week4_coverage_by_source.png` | Source representation visualisation |
| `docs/week4_triage.csv` | Manual review and triage decisions |

Restricted outputs are maintained locally unless sharing is authorised.

## 10. How to Run the Project

### Week 3 — Data Preparation

1. Open the Week 3 pipeline notebook in Google Colab.
2. Upload the required academic PDF documents.
3. Execute the extraction, cleaning and chunking processes.
4. Generate the prepared JSONL records and pipeline manifests.
5. Verify the pipeline outputs and provenance information.
6. Download the project backup.

### Week 4 — Data Quality Assessment

1. Open `notebooks/week4_quality.ipynb` in Google Colab.
2. Restore the existing project backup.
3. Install the required Python libraries.
4. Execute A0 to A4 for quality planning, data loading, inventory, inspection and validation.
5. Complete A5 manual review or restore previously saved decisions using A5.1.
6. Execute B1 for duplicate detection and cleaned dataset generation.
7. Execute B2 for representation coverage analysis.
8. Review B3 and B4 for bias assessment and responsible data practices.
9. Generate the final report using C1.
10. Execute C2 to verify the required deliverables.
11. Download the final project backup.

**Important:** If manual review decisions have already been completed and saved, restore them using A5.1 instead of repeating the interactive A5 activity.

## 11. Data and Access Considerations

UniGuide uses institutional academic documents that may be subject to copyright and distribution restrictions.

The project treats document reuse permissions as Not Verified until appropriate authorisation or another applicable legal basis is established.

The following practices must be maintained:

- Preserve original source references and version information.
- Avoid uploading restricted documents to public repositories.
- Do not publish confidential or personally identifiable information.
- Verify document permissions before downstream use.
- Maintain local backups of restricted project artefacts.
- Revalidate prepared data when source documents are updated.

## 12. Future Development

Future development will focus on:

- Resolving outstanding data-quality and permission issues.
- Expanding academic document and programme coverage.
- Improving extraction quality for complex PDF layouts.
- Implementing document embeddings and semantic retrieval.
- Developing a Retrieval-Augmented Generation (RAG) system.
- Generating answers with references to original documents and pages.
- Evaluating retrieval quality, answer accuracy and response time.
- Developing a user-friendly interface for UTM students.

---

**Project Name:** UniGuide – UTM Academic Information Assistant

**Institution:** Universiti Teknologi Malaysia (UTM)

**Course:** AI Engineering

**Current Development Stage:** Week 4 — Data Quality, Bias Assessment and Responsible Data Practices

**Quality-Gate Decision:** GO WITH CONDITIONS
