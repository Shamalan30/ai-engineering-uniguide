
# UniGuide - Week 3 Data Inventory

## Project Overview

UniGuide is a document-grounded academic information assistant
designed to help UTM students retrieve accurate academic information
from official UTM documents.

The selected data sources support the document-based RAG approach.

## Data Inventory

| Source ID | Filename | Type and Purpose | Version / Date / Owner | Access / Rights | Inspection Evidence |
|---|---|---|---|---|---|
| S01 | academic_regulations_2026.pdf | PDF - UTM academic regulations and academic policies. | 2026 / Issuing owner to be verified. | Official source and usage permissions to be verified. | Page-level extraction, GID detection, OCR fallback and representative text inspection. |
| S02 | course_registration_guide_2026_2027.pdf | PDF - Course registration procedures and student guidance. | 2026/2027 / Issuing owner to be verified. | Official source and usage permissions to be verified. | PDF text extraction and representative page inspection. |
| S03 | academic_calendar_2026_2027.pdf | PDF - Academic dates, semester schedules and university events. | 2026/2027 / Issuing owner to be verified. | Official source and usage permissions to be verified. | PDF text extraction and representative page inspection. |

## Relationship to Topic 2 Requirements

| Requirement ID | Required Information | Supporting Source | Justification |
|---|---|---|---|
| FR1 | UTM academic regulations and guidelines | S01 | Supports academic rules and policy questions. |
| FR2 | Course registration information and academic dates | S02, S03 | Supports registration procedures, deadlines and academic schedules. |
| FR3 | Official document references and citations | S01, S02, S03 | Supports source traceability and document-grounded answers. |
| FR4 | Identify unavailable information instead of generating unsupported answers | S01, S02, S03 | Defines the available knowledge coverage for answering questions. |

Note: Confirm that FR1-FR4 match the actual requirement IDs
in the Topic 2 project document.

## Data Storage

- Raw documents: data/raw/
- Prepared documents: data/processed/
- Prepared text output: data/processed/prepared_text.jsonl
- Lineage manifest: data/week3_manifest.json

Raw source PDFs are retained separately from prepared outputs.

## Preparation Process

1. Select the approved PDF source files.
2. Extract page-level text using pypdf.
3. Detect pages with suspicious extraction results.
4. Apply Tesseract OCR as a fallback where required.
5. Clean unnecessary whitespace.
6. Compare fixed-size and paragraph-aware chunking.
7. Export page-aware JSONL records with source metadata.
8. Validate the prepared output.
9. Register source-to-output lineage and checksums.

## Inspection and Limitations

- PDF text extraction may lose formatting and layout information.
- Some pages may contain scanned or image-based text.
- OCR may introduce character, number and date recognition errors.
- Tables may not preserve their original structure.
- Paragraph boundaries may not be preserved during PDF extraction.
- Source ownership, access rights and redistribution permissions
  must be verified before sharing the documents.

## Data Quality Status

The initial inspection identified extraction limitations in S01.
OCR fallback and page-level quality checks are used to improve
the prepared text.

The final dataset is considered prepared only after the
B3 validation checks have passed and representative records
have been inspected.
