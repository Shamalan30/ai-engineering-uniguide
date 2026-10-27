# UniGuide — AI-Powered University Information Assistant

## 1. Project Overview

**Project Name:** UniGuide  
**Domain:** Artificial Intelligence, Natural Language Processing (NLP), and Higher Education  
**Project Type:** Document-Grounded AI Information Assistant

UniGuide is an AI-powered university information assistant designed to help UTM students find academic information using official university documents. Students can ask questions in natural language, and the system will retrieve relevant information from its document collection and generate answers supported by source references.

The initial scope will focus on academic regulations, programme information, course registration guidance, and academic calendars. UniGuide should acknowledge when its available documents do not contain sufficient information rather than generating unsupported answers.

## 2. Problem Statement

University academic information is published across different webpages, handbooks, regulations, and official documents. Students may need to consult multiple sources to locate specific information, such as academic dates, programme requirements, and course registration procedures.

Although these resources provide official information, finding the correct section may require students to search through multiple documents. UniGuide proposes a document-grounded AI assistant that allows students to ask academic questions in natural language and receive answers based on retrieved official information.

A preliminary survey of UTM students will be used to investigate their current information-searching practices, the difficulties they experience, and their interest in using such an assistant.

## 3. Evidence of the Problem

### Evidence 1: Academic Information Is Distributed Across Resources

The UTM Faculty of Computing undergraduate webpage provides links to different undergraduate resources, including programme information and academic-related materials. This demonstrates that students may need to navigate different resources to find the information they require.

**Source:** Universiti Teknologi Malaysia (UTM), Faculty of Computing — Undergraduate Resources  
https://comp.utm.my/undergraduate/

### Evidence 2: Academic Dates Are Published Separately

UTM publishes an official Academic Calendar for the 2026/2027 session, containing semester dates and other important academic periods. Students seeking particular dates may need to locate and consult this document.

**Source:** Universiti Teknologi Malaysia (UTM), Academic Calendar 2026/2027  
https://amd.utm.my/wp-content/uploads/sites/460/2026/05/Final_Kalendar-Akademik-Sarjana-Muda.Sarjana.Kedoktoran-20262027-14.5.2026-pembetulan.pdf

### Planned Primary Evidence: Student Survey

A preliminary survey will be conducted with UTM students to investigate:

- How students currently find academic information.
- Which types of academic information they search for most frequently.
- Whether they experience difficulty locating relevant information.
- Whether they would find a document-grounded academic assistant useful.

**Note:** The webpages demonstrate that academic information is available across different resources, but they do not independently establish how frequently students experience difficulties. The survey will help verify the extent of the problem.

## 4. Initial Related Work and Existing Approaches

### 4.1 Human Academic Advising

Academic advisors provide contextual guidance and can help students understand academic requirements.

**Limitation:** Access may depend on advisor availability, appointment schedules, and the time required to respond to individual questions.

### 4.2 Static University Webpages and PDF Documents

Official university webpages, academic calendars, handbooks, and regulations provide authoritative information.

**Limitation:** Students may need to search through several pages or documents and identify the relevant sections themselves.

### 4.3 Retrieval-Augmented Generation (RAG)

Lewis et al. (2020) introduced Retrieval-Augmented Generation, which combines information retrieval with text generation to support knowledge-intensive tasks.

**Limitation:** RAG does not guarantee that the retrieved information is relevant or that the generated answer is correct. UniGuide will therefore require source citations and evaluation against verified answers.

**Reference:**  
Lewis, P., et al. (2020). *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks.* Advances in Neural Information Processing Systems (NeurIPS).  
https://papers.nips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html

### 4.4 RAG Evaluation

Es et al. (2024) presented RAGAs, a framework for evaluating retrieval-augmented generation systems.

**Limitation:** Automated evaluation metrics alone do not establish that an answer accurately represents UTM's official academic requirements. UniGuide will also require manual verification against authoritative documents.

**Reference:**  
Es, S., et al. (2024). *RAGAs: Automated Evaluation of Retrieval Augmented Generation.* EACL 2024.  
https://aclanthology.org/2024.eacl-demo.16/

## 5. Engineering Gap

Existing university resources provide official academic information, while general-purpose AI assistants can respond to questions in natural language. However, an answer generated by a general-purpose AI assistant may not be grounded in the latest or relevant university documents.

UniGuide will address this gap by combining document retrieval with answer generation. The system will retrieve relevant passages from a selected collection of official UTM documents, generate an answer based on those passages, and provide source references so users can verify the information.

The system will also include a fallback response when sufficient supporting information cannot be retrieved. Its effectiveness will be evaluated rather than assumed.

## 6. Project Objectives

**O1:** To collect and prepare publicly accessible UTM academic documents for use as a knowledge source.

**O2:** To implement a retrieval-augmented question-answering system that retrieves relevant document passages and generates answers with source references.

**O3:** To evaluate UniGuide based on retrieval relevance, answer correctness, citation accuracy, response time, and its ability to abstain when sufficient evidence is unavailable.

## 7. Target Users

The primary target users are undergraduate students at Universiti Teknologi Malaysia, initially focusing on students who need information about:

- Academic regulations and requirements.
- Programme and course information.
- Course registration guidance.
- Semester dates and academic calendars.

The initial prototype will focus on a defined collection of publicly accessible academic documents rather than attempting to answer every university-related question.

## 8. Initial Data Sources

The following official sources will be investigated for suitable documents:

1. **UTM Faculty of Computing — Undergraduate Resources**  
   https://comp.utm.my/undergraduate/

2. **UTM Faculty of Computing — Programmes and Student Hub**  
   https://comp.utm.my/programmes-and-student-hub/

3. **UTM Academic Calendar 2026/2027**  
   https://amd.utm.my/wp-content/uploads/sites/460/2026/05/Final_Kalendar-Akademik-Sarjana-Muda.Sarjana.Kedoktoran-20262027-14.5.2026-pembetulan.pdf

These are initial source webpages and documents to investigate. Before implementation, the exact documents, their relevance, and their publication or revision dates will be checked. Only documents suitable for the intended use will be included in the knowledge base.

## 9. Proposed Technical Approach

The initial prototype is expected to use the following components:

1. **Document collection:** Gather selected public UTM academic documents.
2. **Document processing:** Extract text from supported PDF documents and prepare it for retrieval.
3. **Text chunking:** Divide document content into smaller sections while retaining source metadata.
4. **Embedding and retrieval:** Represent document sections as embeddings and retrieve passages relevant to a student's question.
5. **Answer generation:** Use a language model to generate an answer based on the retrieved passages.
6. **Source citations:** Display the document title and relevant source information alongside the answer.
7. **Fallback mechanism:** Indicate when the retrieved evidence is insufficient to answer the question reliably.
8. **User interface:** Provide a simple interface for students to submit questions and read answers.

**Potential technologies:** Python, PyMuPDF, Sentence Transformers, FAISS, a suitable language model, and Streamlit. The final tools will be selected based on availability, compatibility, and project constraints.

## 10. Initial Evaluation Plan

UniGuide will be evaluated using a manually prepared set of questions whose answers can be checked against the selected official documents.

The evaluation will include answerable questions, questions requiring information from different document sections, and questions for which the available documents do not provide a sufficient answer.

| Evaluation criterion | Initial evaluation method |
|---|---|
| Retrieval relevance | Check whether the retrieved passages contain information relevant to the question. |
| Answer correctness | Compare generated answers with verified information in the official documents. |
| Citation accuracy | Check whether the cited source supports the corresponding answer. |
| Response time | Measure the time taken to return an answer. |
| Abstention behaviour | Test whether the system appropriately declines to provide unsupported answers. |

Evaluation results will be recorded and used to identify weaknesses in retrieval, answer generation, and source attribution. Quantitative performance targets will be defined after an initial baseline has been established.

## 11. Responsible AI Risks

### 11.1 Incorrect or Misleading Answers

The system may generate an incorrect answer or misinterpret an academic requirement.

**Mitigation:** Ground answers in retrieved official passages, display citations, test against verified questions, and abstain when sufficient evidence is unavailable.

### 11.2 Outdated Information

Academic regulations, registration procedures, and semester dates may change.

**Mitigation:** Record document dates, review source updates, and refresh the knowledge base when relevant official documents are revised.

### 11.3 Privacy and Data Protection

Students may include personal information in their questions.

**Mitigation:** Avoid collecting unnecessary personal information, minimise the storage of queries, and disclose relevant data-handling practices.

### 11.4 Unequal Accessibility

The system may respond less effectively to questions written in different styles or languages.

**Mitigation:** Test the system using varied question wording and provide clear responses. Language support will be limited to the languages tested during evaluation.

## 12. Initial Project Limitations

- The first prototype will cover only the selected UTM academic documents.
- The system will not replace official academic advisors or university administrative decisions.
- The quality of its answers will depend on the coverage, accuracy, and currency of its source documents.
- The initial evaluation will use a limited test set and may not represent every student's needs.
- The system will not guarantee that every generated answer is correct.

## 13. Weekly Progress

| Week | Focus | Deliverable | Status |
|---|---|---|---|
| Week 1 | Project scoping and GitHub setup | README, project scope, observation report, and system map | In progress |
| Week 2 | Requirements and project refinement | Refined problem, requirements, and evaluation criteria | Planned |
| Week 3 onwards | Data preparation, system implementation, testing, and evaluation | Working prototype and documented evaluation results | Planned |

## 14. Expected Outcome

The expected outcome is a prototype that helps UTM undergraduate students locate academic information through natural-language questions. Answers should be supported by retrieved official documents and accompanied by source references. The project will assess whether this approach can provide relevant and verifiable answers within the defined scope.

The prototype's usefulness and performance will be determined through testing and evaluation rather than assumed in advance.

