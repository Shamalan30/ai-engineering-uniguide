# UniGuide – UTM Academic Information Assistant

## 1. Project Overview

UniGuide is an AI-powered academic information assistant designed to help Universiti Teknologi Malaysia (UTM) students access academic information more easily.

The system uses official UTM academic documents as its knowledge sources to provide relevant information about academic regulations, course registration and academic schedules.

The project follows a structured AI engineering development process, covering requirements analysis, data preparation, pipeline development, data-quality assessment and responsible data practices.

## 2. Project Objectives

- Provide students with easier access to UTM academic information.
- Reduce the time required to search through lengthy academic documents.
- Organise official academic information into structured and searchable data.
- Develop a reliable document-based academic information assistant.
- Ensure data quality, source traceability and responsible data handling before AI system development.

## 3. Data Sources

The project currently uses three official UTM academic documents:

| Source ID | Document | Prepared Records |
|---|---|---:|
| S01 | Academic Regulations 2026 | 251 |
| S02 | Course Registration Guide 2026/2027 | 17 |
| S03 | Academic Calendar 2026/2027 | 17 |
| **Total** | | **285** |

These documents provide the foundation for UniGuide's future document-based question-answering system.

## 4. Technologies Used

- Python
- Google Colab
- PyPDF
- Tesseract OCR
- JSON / JSONL
- GitHub
- Markdown

## 5. Project Structure

```text
UniGuide/
│
├── data/
│   ├── raw/
│   │   ├── academic_regulations_2026.pdf
│   │   ├── course_registration_guide_2026_2027.pdf
│   │   └── academic_calendar_2026_2027.pdf
│   │
│   ├── processed/
│   │   └── Part B prepared data files
│   │
│   ├── week3_manifest.json
│   │
│   └── pipeline_v1/
│       └── documents/
│           ├── prepared_text.jsonl
│           └── pipeline_manifest.json
│
├── docs/
│   ├── week2_architecture_v1.png
│   ├── week3_pipeline_diagram.png
│   ├── week3_pipeline_decisions.md
│   ├── week3_data_inventory.md
│   └── week4_data_quality_report.md
│
├── notebooks/
│   └── UniGuide_Week3_Pipeline_Week4_Data_Quality_Audit.ipynb
│
└── README.md
```

*Note: The structure above represents the intended project organisation. Actual repository files and filenames should be verified.*

## 6. Data Processing Pipeline — Week 3

The UniGuide data pipeline prepares academic documents through the following stages:

1. **Data Collection:** Collect selected official UTM academic PDF documents.
2. **Text Extraction:** Extract document text using PyPDF.
3. **OCR Fallback:** Apply OCR to scanned pages or pages where normal text extraction is insufficient.
4. **Text Cleaning:** Clean and organise the extracted text.
5. **Chunking:** Divide the extracted content into smaller sections using paragraph-aware chunking.
6. **Validation:** Verify that the prepared outputs exist and contain data.
7. **Provenance Tracking:** Record source fingerprints, output fingerprints and source-to-output mappings.

The pipeline produces structured JSONL records containing document text, source IDs, page references and record identifiers.

## 7. Data Quality Assessment — Week 4

Week 4 focuses on evaluating the quality and responsible use of the prepared data from Week 3.

The assessment follows five operational data-quality dimensions:

1. Completeness
2. Consistency
3. Accuracy
4. Timeliness
5. Uniqueness

A representative sample of 15 records was inspected, and two validation rules were applied to the full dataset of 285 records.

### 7.1 Validation Results

| Validation Rule | Records Tested | Passed | Failed |
|---|---:|---:|---:|
| V1 — Basic Text Integrity | 285 | 285 | 0 |
| V2 — Source Traceability | 285 | 285 | 0 |

**V1 — Basic Text Integrity**

Checks whether each prepared record contains non-empty text without unresolved `/gid` extraction patterns.

**V2 — Source Traceability**

Checks whether each record contains a recognised source ID, valid positive page number and non-empty source filename.

Both rules achieved a 100% pass rate against their defined conditions.

However, these checks do not establish complete extraction accuracy, readability or source permissions.

### 7.2 Extraction Quality Findings

Manual inspection identified two suspicious records from the Academic Regulations document.

| Record ID | Source | PDF Page | Finding |
|---|---|---:|---|
| 1 | S01 | 1 | Unreadable extracted text from the cover page |
| 251 | S01 | 81 | Unreadable extracted text from the final barcode page |

Comparison with the original PDF confirmed that these pages do not contain substantive academic regulations.

The extracted artefacts should be reviewed for exclusion from future retrieval, while the original PDF remains preserved.

### 7.3 Coverage and Potential Bias

The prepared dataset contains records from all three selected UTM documents.

However, the Academic Regulations document contributes substantially more records than the other two sources because of its greater document length.

Potential risks include:

- Unequal representation of academic topics during future retrieval.
- Extraction errors affecting scanned pages or complex document layouts.
- Missing or incomplete information caused by PDF processing.
- Outdated information if university documents are revised.

These risks require further evaluation during later development stages.

### 7.4 Responsible Data Practices

The project records source references and preparation information through its pipeline manifests.

Before using the dataset in a deployed retrieval system, the project must verify relevant document reuse permissions and confirm that the source versions remain applicable.

Original documents and restricted content should not be publicly redistributed without appropriate permission.

### 7.5 Quality-Gate Decision

**Decision: HOLD for downstream use of the audited dataset.**

Although both automated validation rules passed across all 285 records, the audit identified extraction anomalies and unresolved document reuse permissions.

The following actions are required before reconsidering the decision:

1. Verify permission or another applicable legal basis for the intended use of the source documents.
2. Review and appropriately handle the identified extraction anomalies.
3. Confirm source document versions and perform additional content-quality checks.

The decision applies to downstream use of the audited dataset and does not prevent further local inspection or permitted development activities.

**Full Week 4 Report:** [Data Quality and Bias Report](docs/week4_data_quality_report.md)

## 8. Current Project Progress

| Component | Status |
|---|---|
| Project setup and source identification | Completed |
| Data extraction using PyPDF | Completed |
| OCR fallback | Implemented |
| Text cleaning and inspection | Completed |
| Text chunking and preparation | Completed |
| Part B prepared dataset (285 records) | Completed |
| Part B lineage manifest | Completed |
| Part C data pipeline | Implemented |
| Repeatability and provenance verification | Implemented |
| Week 3 pipeline diagram | Pending finalisation |
| Week 3 pipeline decisions document | Pending finalisation |
| Week 3 data inventory | Pending finalisation |
| Week 4 data-quality inspection | Completed |
| Week 4 validation rules | Completed |
| Week 4 extraction anomaly review | Completed |
| Week 4 bias and governance assessment | Documented |
| Week 4 quality-gate decision | HOLD |
| Week 4 Data Quality and Bias Report | Prepared |

## 9. Pipeline Outputs

The project generates structured outputs for future AI system development.

### Part B Outputs

- Prepared document records in JSONL format.
- `data/week3_manifest.json` — records information about the Part B preparation process.

### Part C Outputs

- `data/pipeline_v1/documents/prepared_text.jsonl` — prepared text records with source and page references.
- `data/pipeline_v1/documents/pipeline_manifest.json` — records pipeline configuration, source fingerprints, output validation and source-to-output mappings.

### Week 4 Outputs

- `docs/week4_data_quality_report.md` — documents data-quality findings, validation results, bias risks, responsible-data considerations and the quality-gate decision.
- Updated Week 3/Week 4 notebook containing additional validation and inspection cells.

## 10. How to Run the Project

1. Open `UniGuide_Week3_Pipeline_Week4_Data_Quality_Audit.ipynb` in Google Colab.
2. Place the required academic PDF documents in `data/raw/`.
3. Run the Week 3 notebook cells in order.
4. Complete the Part B extraction and preparation process.
5. Execute the Part C pipeline.
6. Run the repeatability and provenance verification.
7. Execute the Week 4 data-quality inspection cells.
8. Run the V1 and V2 validation checks.
9. Review the extraction anomalies and source coverage results.
10. Refer to the Week 4 report for the final audit findings.

## 11. Data and Access Considerations

UniGuide uses institutional academic documents that may be subject to copyright and distribution restrictions.

The Academic Regulations publication includes a copyright notice requiring written permission for certain reproduction and information storage and retrieval uses.

The project therefore treats reuse permission as Not Verified until the appropriate rights or legal basis are established.

The following practices should be maintained:

- Preserve original source references and version information.
- Avoid uploading restricted documents to public repositories.
- Do not publish confidential or personally identifiable information.
- Verify document permissions before downstream use.
- Revalidate prepared data when source documents are updated.

## 12. Future Development

Future development will focus on:

- Resolving the identified data-quality and permission issues.
- Implementing document-based question answering.
- Retrieving relevant information from prepared academic documents.
- Generating answers with references to original documents and pages.
- Evaluating retrieval quality and answer accuracy.
- Developing a user-friendly interface for UTM students.

---

**Project Name:** UniGuide – UTM Academic Information Assistant  
**Institution:** Universiti Teknologi Malaysia (UTM)  
**Course:** AI Engineering  
**Current Development Stage:** Week 4 — Data Quality and Responsible Data Practices
