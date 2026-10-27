# UniGuide — AI-Powered University Information Assistant

UniGuide is a proposed AI assistant that helps UTM undergraduate students find academic information using selected official university documents.

## Problem Statement

Academic information is available through multiple university webpages and documents. UniGuide aims to make this information easier to access by allowing students to ask questions in natural language and receive answers grounded in relevant official sources.

## Proposed Solution

UniGuide will use Retrieval-Augmented Generation (RAG) to retrieve relevant passages from selected UTM documents and generate answers with source references. If sufficient evidence is unavailable, the system should communicate this limitation rather than inventing an answer.

## Project Objectives

- Collect and prepare publicly available UTM academic documents.
- Implement a document-grounded question-answering assistant with source references.
- Evaluate retrieval relevance, answer correctness, citation accuracy, response time, and abstention.

## Target Users

UTM undergraduate students seeking information about academic regulations, course registration, programme requirements, and academic dates.

## Data Sources

- [UTM Faculty of Computing — Undergraduate Resources](https://comp.utm.my/undergraduate/)
- [UTM Academic Calendar 2026/2027](https://amd.utm.my/wp-content/uploads/sites/460/2026/05/Final_Kalendar-Akademik-Sarjana-Muda.Sarjana.Kedoktoran-20262027-14.5.2026-pembetulan.pdf)
- [UTM Faculty of Computing — Programmes and Student Hub](https://comp.utm.my/programmes-and-student-hub/)

## Proposed Technology Stack

- Python
- PyMuPDF
- Sentence Transformers
- FAISS
- A large language model
- Streamlit

## Evaluation

The system will be tested using manually verified questions with known answers and questions that cannot be answered from the selected documents. Evaluation will cover retrieval relevance, answer correctness, citation accuracy, response time, and abstention.

## Project Status

Week 1 — Initial project scope, evidence collection, and repository setup.

## Responsible AI Considerations

UniGuide will prioritise official sources, identify the documents supporting its answers, avoid unsupported claims, and communicate when available evidence is insufficient. Users should verify important academic decisions against current official university information.
