# Requirements Specification — UniGuide

**Version:** 1.0  
**Project Title:** UniGuide: An AI-Powered Academic Information Assistant for UTM Undergraduate Students

---

# Section 0 — Project Framing & Application Scope

## 0.1 Problem Evidence

UTM undergraduate academic information is distributed across different university webpages, academic portals, guidelines and official documents. Students may need to consult multiple sources to locate information about academic regulations, course registration procedures, programme requirements and important academic dates.

The following official UTM resources demonstrate that academic information is spread across different sources:

1. **UTM Faculty of Computing – Undergraduate Resources:** Provides undergraduate academic information, programme handbooks and related academic resources.
2. **UTM Academic Management Division – Course Registration Guidelines:** Provides information and guidelines regarding course registration procedures.

These sources demonstrate the distribution of academic information across different university platforms. UniGuide aims to make accessing this information more convenient through a centralised conversational interface.

## 0.2 Existing Approaches

The following existing systems and approaches already provide university-related academic information:

| Existing Approach | What It Addresses |
|---|---|
| UTM Faculty of Computing Undergraduate Resources | Provides programme handbooks, academic regulations and faculty-related academic information. |
| UTM Academic Management Division | Provides official academic guidelines, course registration information and university academic procedures. |
| UTM Academic Calendar | Provides important academic dates, semester schedules and university timelines. |
| UiTM AI-Based One-Stop Campus Service Chatbot | Demonstrates the use of conversational AI to provide university-related information and student services. |

These approaches provide useful academic information through official resources and digital services. However, students may still need to navigate different sources to locate specific information.

## 0.3 Project / Engineering Gap

Although UTM provides official academic information through various platforms and documents, students may need to search through multiple sources to find relevant answers.

There is an opportunity to provide a centralised AI-powered academic information assistant that allows students to ask questions conversationally and receive answers grounded in official UTM academic documents.

The system will also aim to provide relevant source references and identify questions that cannot be answered using the available information.

## 0.4 Project Objectives

**O1:** To design an AI-powered academic information assistant for UTM undergraduate students.

**O2:** To develop a document-grounded question-answering system that retrieves relevant information from official UTM academic documents and generates answers with source references.

**O3:** To evaluate the system based on answer correctness, source relevance, response time and its ability to handle questions outside its knowledge domain.

## 0.5 Application Scope

### Intended Users

- Primary users: UTM undergraduate students.
- Secondary users: Students seeking clarification about university academic information.

### Supported Tasks

The system will support the following tasks:

1. Answer questions about UTM undergraduate academic regulations.
2. Provide information about programme handbooks and academic requirements.
3. Explain course registration procedures and related guidelines.
4. Provide information about academic calendars and important dates.
5. Retrieve relevant information from available official UTM academic documents.
6. Provide references to the official documents used to support answers.
7. Inform users when the available information is insufficient to answer a question.

### Information / Knowledge Domain

The system focuses on official UTM undergraduate academic information, including:

- Academic regulations and guidelines.
- Programme handbooks.
- Course registration procedures.
- Academic calendars.
- University academic policies and requirements.

### Operating Context

UniGuide is intended to operate as a conversational AI application that undergraduate students can access to ask questions about UTM academic information.

### Important Constraints

1. The accuracy of answers depends on the availability and quality of official academic documents.
2. Outdated or conflicting university documents may affect answer accuracy.
3. The system may not have access to real-time academic portal information.
4. The system is limited to the academic information included in its approved knowledge sources.
5. Development time and available computational resources may limit the system's capabilities.

### Explicit Out-of-Scope Tasks

UniGuide will not:

- Perform actual course registration or withdrawal.
- Access or modify students' personal academic records.
- Make official academic decisions on behalf of UTM.
- Approve course exemptions or prerequisite waivers.
- Guarantee the latest information when updated documents have not been provided.
- Provide medical, legal, financial or other unrelated professional advice.
- Replace official university departments or academic advisors.

### Evaluation Focus

The evaluation will determine whether UniGuide can provide accurate and understandable answers based on official UTM academic documents.

The main evaluation areas are:

- Answer correctness.
- Relevance of retrieved information.
- Accuracy and availability of source references.
- Response time.
- Ability to identify unsupported or out-of-scope questions.
- Clarity and usefulness of generated answers.

---

# Section 1 — Functional Requirements

| ID | Requirement — The system shall | Scope Boundary — The system shall not |
|---|---|---|
| FR1 | The system shall answer undergraduate academic enquiries related to UTM academic regulations, programme handbooks and academic guidelines. | Provide answers outside the defined UTM undergraduate academic information domain. |
| FR2 | The system shall provide information about course registration procedures, academic calendars, important dates and relevant academic guidelines. | Perform actual course registration or modify student registration records. |
| FR3 | The system shall provide references to relevant official UTM documents that support the generated answers. | Present unsupported information as if it originated from official UTM documents. |
| FR4 | The system shall identify questions that cannot be answered using the available academic information and inform users when sufficient information is unavailable. | Generate fabricated academic regulations, dates or requirements to fill information gaps. |
| FR5 | The system shall present academic information in clear and understandable language appropriate for UTM undergraduate students. | Present ambiguous or unverified information as confirmed university policy. |

---

# Section 2 — Non-Functional Requirements

The following requirements define the expected quality and operational performance of UniGuide. All thresholds are proposed evaluation targets.

| ID | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| NFR1 | Performance | The system shall generate responses within an acceptable time for interactive academic enquiries. | Measure end-to-end response time using a test set of 30 academic queries under the same testing environment. | 90th percentile response latency (p90). | ≤ 10 seconds |
| NFR2 | Correctness | The system shall generate answers that are factually consistent with the approved UTM academic documents. | Evaluate 30 curated questions against verified answers using a predefined correctness checklist. | Correct answer rate (%) | ≥ 80% |
| NFR3 | Reliability | The system shall successfully process valid academic enquiries or provide an appropriate unable-to-answer response without unexpected failure. | Execute 30 test queries and record successful responses, timeouts and system errors. | Successful query handling rate (%) | ≥ 95% |
| NFR4 | Maintainability | The system shall allow approved academic documents to be updated without requiring unrelated system components to be rebuilt. | Conduct a controlled document-update test and measure the time required for the updated information to become available. | Document update time | ≤ 10 minutes for a prepared test document |

---

# Section 3 — Responsible AI Requirements

The following requirements address potential risks associated with incorrect academic information, inappropriate responses and student privacy.

| ID | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| RAI1 | Hallucination and misinformation | The system shall provide answers supported by available official UTM academic documents and indicate when sufficient supporting information cannot be found. | Evaluate 30 document-grounded test queries by checking whether generated answers are supported by the cited sources. | Citation-source correctness rate (%) | ≥ 95% |
| RAI2 | Scope and safety | The system shall identify out-of-scope academic and non-academic enquiries, decline to provide unsupported advice and redirect users to appropriate official university channels where relevant. | Test the system using at least 20 predefined out-of-scope queries. | Correct refusal and redirection rate (%) | ≥ 95% |
| RAI3 | Privacy | The system shall avoid requesting or exposing unnecessary student personal information when answering general academic enquiries. | Conduct privacy test cases and inspect system inputs, stored records and external model requests where applicable. | Number of unnecessary personal information disclosures | 0 |

---

## Initial Requirements Traceability

The following objectives are connected to the functional, non-functional and Responsible AI requirements.

| Objective | Supporting Requirements |
|---|---|
| O1 – Design an AI-powered academic information assistant. | FR1, FR2, FR5 |
| O2 – Develop a document-grounded question-answering system with source references. | FR1, FR2, FR3, FR4, NFR2, NFR4, RAI1 |
| O3 – Evaluate the system's performance and reliability. | FR4, FR5, NFR1, NFR2, NFR3, RAI1, RAI2, RAI3 |

---

**End of Requirements Specification**
