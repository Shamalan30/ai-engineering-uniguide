# UniGuide – UTM Academic Information Assistant

## 1. Project Overview

UniGuide is an AI-powered academic information assistant designed to help Universiti Teknologi Malaysia (UTM) students access academic information more easily.

The system uses official UTM academic documents as its knowledge sources to provide relevant information about academic regulations, course registration and academic schedules.

## 2. Project Objectives

- Provide students with easier access to UTM academic information.
- Reduce the time required to search through lengthy academic documents.
- Organise official academic information into structured and searchable data.
- Develop a reliable document-based academic information assistant.

## 3. Data Sources

The project currently uses three official UTM academic documents:

| Source ID | Document |
|---|---|
| S01 | Academic Regulations 2026 |
| S02 | Course Registration Guide 2026/2027 |
| S03 | Academic Calendar 2026/2027 |

## 4. Technologies Used

- Python
- Google Colab
- PyPDF
- Tesseract OCR
- JSON / JSONL
- GitHub

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
│   └── week3_data_inventory.md
│
├── notebooks/
│   └── week3_pipeline.ipynb
│
└── README.md
```

*Note: The structure above describes the intended project organisation. Update filenames if your actual repository differs.*

## 6. Data Processing Pipeline

The UniGuide data pipeline prepares academic documents through the following stages:

1. **Data Collection:** Collect the selected official UTM academic PDF documents.
2. **Text Extraction:** Extract document text using PyPDF.
3. **OCR Fallback:** Apply OCR to scanned pages or pages where normal text extraction is insufficient.
4. **Text Cleaning:** Clean and organise the extracted text.
5. **Chunking:** Divide the extracted content into smaller sections using paragraph-aware chunking.
6. **Validation:** Verify that the prepared outputs exist and contain data.
7. **Provenance Tracking:** Record source fingerprints, output fingerprints and source-to-output mappings.

## 7. Current Project Progress

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

## 8. Pipeline Outputs

The project generates structured outputs for further development:

**Part B outputs**
- Prepared document records in JSONL format.
- `data/week3_manifest.json` – records information about the Part B preparation process.

**Part C outputs**
- `data/pipeline_v1/documents/prepared_text.jsonl` – prepared text records with source and page references.
- `data/pipeline_v1/documents/pipeline_manifest.json` – records pipeline configuration, source fingerprints, output validation and source-to-output mappings.

## 9. How to Run the Project

1. Open the Week 3 notebook in Google Colab.
2. Place the required academic PDF documents in `data/raw/`.
3. Run the notebook cells in order.
4. Complete the Part B extraction and preparation process.
5. Execute the Part C pipeline.
6. Run the repeatability and provenance verification.
7. Check the generated outputs and manifests.

## 10. Data and Access Considerations

The project uses official UTM academic documents. Source permissions and distribution conditions should be checked before sharing the original PDFs or extracted content publicly.

Restricted or unapproved source files should not be uploaded to a public GitHub repository.

## 11. Future Development

Future development will focus on:

- Implementing document-based question answering.
- Retrieving relevant information from prepared academic documents.
- Generating answers with references to original documents and pages.
- Evaluating answer accuracy and reliability.
- Developing a user-friendly interface for UTM students.

---

**Project Name:** UniGuide – UTM Academic Information Assistant  
**Institution:** Universiti Teknologi Malaysia (UTM)
