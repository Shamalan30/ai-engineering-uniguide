# Week 3 – Data Pipeline Decisions

## 1. Project Overview

**Project Name:** UniGuide – UTM Academic Information Assistant

**Data Type:** PDF/TXT Documents

**Pipeline Type:** Batch Processing

UniGuide uses official UTM academic documents to provide students with accurate academic information. The Week 3 pipeline prepares these documents through text extraction, inspection, cleaning and chunking.

## 2. Selected Data Sources

Three official UTM academic documents were selected:

| Source ID | Document |
|---|---|
| S01 | Academic Regulations 2026 |
| S02 | Course Registration Guide 2026/2027 |
| S03 | Academic Calendar 2026/2027 |

These documents contain relevant academic information needed by UTM students.

## 3. Data Preparation Method

The PDF/TXT pathway was selected because the project uses PDF documents as its primary data sources.

The preparation process includes:

1. Extracting text using PyPDF.
2. Applying OCR as a fallback for scanned or poorly extracted pages.
3. Cleaning the extracted text.
4. Inspecting page-level text quality.
5. Dividing text into smaller chunks using paragraph-aware chunking.
6. Retaining source IDs and page numbers for traceability.

| Setting | Configuration |
|---|---|
| Chunking Method | Paragraph-aware |
| Chunk Size | 500 characters |
| Source IDs | S01, S02, S03 |
| Output Format | JSONL |

## 4. Comparison and Evidence from Part B

Part B involved extracting and inspecting the three PDF documents. The extracted content was reviewed to identify readable text and pages requiring additional attention.

OCR was used as a fallback for scanned or poorly extracted pages. Paragraph-aware chunking was selected to organise the content while retaining page references.

The prepared dataset from Part B contained 285 records. This demonstrated that the selected preparation approach could produce structured text records for UniGuide.

## 5. ETL or ELT Decision

The pipeline follows an ETL (Extract, Transform, Load) approach.

- **Extract:** Retrieve text from the selected PDF documents.
- **Transform:** Clean the text and divide it into smaller chunks.
- **Load:** Save the prepared records in JSONL format.

ETL was selected because the documents need to be cleaned and prepared before further use.

## 6. Batch or Streaming Decision

Batch processing was selected because the academic documents are relatively static and do not require continuous real-time updates.

The documents can be processed whenever new versions become available. This approach is simpler and suitable for the current project.

## 7. Pipeline Stages and Failure Handling

| Stage | Expected Action | Failure Handling |
|---|---|---|
| Ingest | Locate and access PDF files. | Stop if a required file is missing. |
| Inspect | Check extracted text and readability. | Flag unreadable pages. |
| Prepare | Clean text and perform chunking. | Report transformation errors. |
| Validate | Check that output exists and is not empty. | Stop if output is missing or empty. |
| Record Lineage | Store fingerprints and source-output mappings. | Report missing metadata. |

## 8. Output Location

Prepared pipeline output:

`data/pipeline_v1/documents/prepared_text.jsonl`

Pipeline manifest:

`data/pipeline_v1/documents/pipeline_manifest.json`

The manifest records source files, processing configuration, output information, validation results and source-to-output mappings.

## 9. Limitations and Considerations

Some PDF pages may contain scanned images, unusual formatting or text that cannot be extracted accurately. OCR may also introduce recognition errors.

The pipeline retains page references and source IDs to support traceability. However, extracted text should still be reviewed for accuracy.

Source versions and access rights must be verified before distributing or sharing the documents and prepared outputs.

## 10. Topic 2 Requirements

**Related Topic 2 Requirement ID(s):** [Insert the relevant requirement ID(s) from your Week 2 documentation.]

This pipeline supports the UniGuide requirements by preparing official UTM academic documents in a structured and traceable format.

## 11. Conclusion

The Week 3 pipeline provides a structured process for preparing UTM academic documents. Text extraction, OCR fallback, cleaning, paragraph-aware chunking and provenance tracking produce organised data that can support the future development of UniGuide.
