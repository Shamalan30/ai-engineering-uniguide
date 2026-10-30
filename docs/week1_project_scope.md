# UniGuide — Week 1 Project Scope

## 1. Project Name

**UniGuide: AI-Powered University Information Assistant**

## 2. Domain

Artificial Intelligence (AI), Natural Language Processing (NLP), Information Retrieval, and Higher Education Technology.

## 3. Problem Statement

University students need to access academic information such as programme requirements, academic regulations, course registration dates, and academic calendars. At Universiti Teknologi Malaysia (UTM), these resources are available through official faculty webpages, student resource portals, and university documents. For example, the UTM Faculty of Computing website provides undergraduate programme information, academic regulations, programme handbooks, registration dates, and academic calendars (Universiti Teknologi Malaysia [UTM], n.d.-a).

Although these resources provide important information, students may need to navigate different webpages or search through documents to locate the information relevant to their questions. Traditional webpage navigation and document searching also require users to identify appropriate keywords and interpret the retrieved information themselves.

Existing research has explored the use of retrieval-augmented generation (RAG) to connect large language models with external document collections. RAG combines information retrieval with language generation to produce responses grounded in retrieved information (Lewis et al., 2020). However, the usefulness of a university information assistant depends on whether it retrieves relevant documents, generates accurate answers, and communicates its supporting evidence clearly (Es et al., 2024).

Therefore, this project proposes UniGuide, an AI-powered assistant that allows students to ask questions in natural language and receive answers based on publicly available official UTM academic documents. The proposed system will provide source references and indicate when the available documents do not contain sufficient evidence to answer a question reliably.

The extent to which UTM students experience difficulties finding academic information will be investigated further through student feedback or a survey.

## 4. Evidence of the Problem

| Evidence | Description and relevance | Source / citation |
|---|---|---|
| Evidence 1: Multiple types of academic resources | The UTM Faculty of Computing undergraduate webpage provides access to programme handbooks, academic regulations, registration dates, timetables, and academic calendars. This demonstrates that students may need to navigate different academic resources to find information relevant to a question. It supports the existence of a document-navigation challenge, but does not independently prove that students experience difficulty. | UTM Faculty of Computing (n.d.-a). [Undergraduate resources](https://comp.utm.my/undergraduate/). |
| Evidence 2: Separate student information portal | The Faculty of Computing Student Development Hub provides access to academic calendars, academic regulations, course registration guidance, and undergraduate handbooks. This illustrates the variety of academic information students may need to consult. | UTM Faculty of Computing (n.d.-b). [Programmes and Student Hub](https://comp.utm.my/programmes-and-student-hub/). |
| Evidence 3: Research on document-based student assistants | Research has investigated RAG-based chatbots that use institutional documents, including student handbooks, admission guidelines, FAQs, and course catalogues, to answer student information queries. This supports the technical relevance of a document-grounded assistant for higher education. | Ndudiri and Bamikole (2026). [Student information chatbot study](https://doi.org/10.62226/ijarst20262787). |

**Additional validation planned:** A short survey or interview with UTM students will investigate the types of academic information they search for, the sources they currently use, and whether finding answers across university resources is difficult. No survey findings are claimed at this stage.

## 5. Initial Related Work (at least 3)

| Study / solution | Source / citation | Key limitation and relevance to UniGuide |
|---|---|---|
| **1. Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks** — Lewis et al. (2020) introduced a RAG approach that combines a language model with retrieved external knowledge. This provides a technical foundation for generating answers from university documents rather than relying only on information stored in a model's parameters. | Lewis et al. (2020). [NeurIPS paper](https://papers.nips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html). | RAG does not automatically guarantee correct answers. Its performance depends on retrieving relevant evidence and generating responses faithfully. UniGuide will therefore need to evaluate retrieval relevance, answer correctness, and source-reference accuracy. |
| **2. RAGAs: Automated Evaluation of Retrieval Augmented Generation** — Es et al. (2024) proposed an evaluation framework for examining RAG systems, including the relevance of retrieved context and the faithfulness and quality of generated answers. | Es et al. (2024). [ACL Anthology](https://aclanthology.org/2024.eacl-demo.16/). | An evaluation framework does not itself solve the university information-search problem. Automated evaluation metrics also need to be interpreted carefully and should be supplemented with manually verified test questions and answers where feasible. |
| **3. AI-Powered Intelligent Chatbot for Student Information Services** — Ndudiri and Bamikole (2026) described a student information chatbot using RAG and institutional documents such as handbooks, admission guidelines, FAQs, and course catalogues. The study reported a pilot evaluation involving 120 test queries. | Ndudiri and Bamikole (2026). [Research paper](https://doi.org/10.62226/ijarst20262787). | The reported evaluation was a formative pilot involving 30 volunteer participants in its own institutional context. Its results cannot automatically be generalised to UTM students or UTM documents. UniGuide will require its own evaluation using UTM-specific information and test questions. |

These studies inform the proposed technical approach and evaluation plan. Their findings are not evidence that UniGuide has already achieved comparable performance.

## 6. Engineering Gap / Limitation

**Gap / Limitation:**

Official UTM academic resources are available online, but a student seeking an answer may still need to identify the appropriate webpage or document and locate the relevant passage. A general-purpose language model may also produce an answer that is not adequately supported by the specific official document needed for an academic question.

The proposed engineering gap is to investigate whether a document-grounded AI assistant can make academic information easier to retrieve and understand while maintaining traceability to official sources.

UniGuide will address this gap by combining document retrieval with language generation, providing source references for answers, and implementing a fallback response when sufficient supporting evidence cannot be retrieved. The effectiveness of these features must be demonstrated through testing; they are proposed design goals rather than established results.

## 7. Initial Project Objectives (2–3)

| Objective | Description | Planned evaluation |
|---|---|---|
| **O1** | To collect, inspect, and prepare a feasible set of publicly available official UTM academic documents for use as a searchable knowledge base. | Verify source authenticity, document accessibility, content coverage, and successful text extraction. |
| **O2** | To implement a RAG-based question-answering prototype that retrieves relevant passages from the prepared documents and generates answers with identifiable source references. | Test a set of questions against the retrieved passages and manually check answer correctness and citation accuracy. |
| **O3** | To evaluate the prototype's retrieval relevance, answer correctness, source-reference accuracy, response time, and ability to abstain when the available evidence is insufficient. | Use a predefined test-question set, a documented answer key, and measurable evaluation criteria. |

## 8. Target Users

The primary target users are **UTM undergraduate students**, initially focusing on students who need information about academic programmes and procedures.

Potential users may include:

- New students who need to understand university academic procedures.
- Current undergraduate students looking for academic regulations and programme requirements.
- Students checking course registration information and important academic dates.

The initial prototype will focus on a manageable collection of publicly available UTM academic resources, with priority given to Faculty of Computing undergraduate information. Expansion to additional faculties or university-wide resources will depend on the project's time, document availability, and evaluation results.

UniGuide is intended to support information retrieval. It will not replace official university announcements, academic advisors, faculty administrators, or formal university decisions.

## 9. Data Sources (at least 2)

The following official UTM webpages and documents will be considered for the initial UniGuide knowledge base.

### 9.1 Original UTM Data Source Websites

| Source | Intended use | URL |
|---|---|---|
| **Source 1: UTM Faculty of Computing — Undergraduate Resources** | A starting source for undergraduate programme handbooks, academic regulations, registration information, timetables, and academic calendars. | https://comp.utm.my/undergraduate/ |
| **Source 2: UTM Faculty of Computing — Programmes and Student Hub** | Additional student-facing resources and academic guidance for the initial knowledge base. | https://comp.utm.my/programmes-and-student-hub/ |
| **Source 3: UTM Admission — Undergraduate Kit** | Publicly available admission and student briefing information, where relevant to the selected questions and target users. | https://admission.utm.my/undergraduate-kit/ |

### 9.2 Actual UTM Academic Documents

The following documents are potential primary sources for the initial document collection.

| No. | Official document | Intended use | Direct document link |
|---|---|---|---|
| 1 | **UTM Academic Regulations — 16th Edition, 2026** | Academic rules, credit requirements, grading, examinations, academic standing, graduation requirements and academic misconduct. | [Open or download PDF](https://comp.utm.my/wp-content/uploads/2026/10/FT-UG-Academic-Regulations-16th-edition.pdf) |
| 2 | **UTM Academic Calendar — Session 2026/2027 (Bachelor's, Master's and Doctoral Programmes)** | Semester dates, lecture periods, revision periods, examinations and semester breaks. | [Open or download PDF](https://amd.utm.my/wp-content/uploads/sites/460/2026/05/Final_Kalendar-Akademik-Sarjana-Muda.Sarjana.Kedoktoran-20262027-14.5.2026-pembetulan.pdf) |
| 3 | **Course Registration User Manual — Current/Senior Students, 2026/2027** | Course registration procedures for existing UTM students. | [Open or download PDF](https://amd.utm.my/wp-content/uploads/sites/460/2026/10/User-Manual_Course-Registration-Senior-Student_update202620271.pdf) |
| 4 | **Course Registration User Manual — New Students, 2026/2027** | Course registration procedures for new undergraduate students. | [Open or download PDF](https://amd.utm.my/wp-content/uploads/sites/460/2026/10/User-Manual_NewStudent_Course-Registration_update-202620271.pdf) |
| 5 | **Course Amendment — Insert/Delete User Manual, 2026/2027** | Procedures for inserting or deleting registered courses. | [Open or download PDF](https://amd.utm.my/wp-content/uploads/sites/460/2026/10/User-Manual_Course-Amendment-Insert-delete_update202620271.pdf) |

### 9.3 Additional Official UTM Resource Pages

These official pages provide further academic documents and guidance that may be considered for future expansion.

| Resource | Intended use | Official URL |
|---|---|---|
| **UTM School of Undergraduate Studies — Academic Rules** | Academic regulations for different undergraduate programme categories, including English and Malay resources. | https://ugs.utm.my/academic-rules/ |
| **UTM Academic Management Division — Course Registration** | General course-registration guidance, student manuals and FAQs. | https://amd.utm.my/course-registration/ |
| **UTM Academic Management Division — Academic Calendar** | Academic calendar archive, including current and previous academic sessions. | https://amd.utm.my/academic-calendar/ |
| **UTM Faculty of Computing — Undergraduate Resources** | Important course-registration dates and Faculty of Computing undergraduate resources. | https://comp.utm.my/undergraduate/ |
| **UTM Academic Management Division — Examination Guidelines** | Examination-related guidance and official resources. | https://amd.utm.my/examination-guidelines/ |
| **UTM Faculty of Computing — Programmes and Student Hub** | Programme handbooks, timetables and other student resources. | https://comp.utm.my/programmes-and-student-hub/ |

### 9.4 Document Selection and Preparation

The initial knowledge base will prioritise the following documents:

1. UTM Academic Regulations — 16th Edition, 2026.
2. UTM Academic Calendar — Session 2026/2027.
3. Course Registration User Manual — Current/Senior Students.
4. Course Amendment — Insert/Delete User Manual.
5. Faculty of Computing AI programme handbook or curriculum structure, subject to verification of the correct document and version for the intended student cohort.

The New Student Course Registration Manual may also be included if the initial system is intended to support new undergraduate students.

Only publicly accessible documents suitable for academic use will be selected. Each document's origin, title, issuing unit, relevant date or academic session, and URL will be recorded. Where possible, current official documents will be prioritised.

Duplicate, outdated, inaccessible, or irrelevant materials will be excluded or clearly identified. Documents from different academic sessions will not be treated as interchangeable.

The selected documents will form the initial knowledge base. The availability of a webpage does not automatically mean every linked document will be downloaded, processed, or included.

## 10. Similar to EduAdvisor

EduAdvisor is a Malaysian education consultation platform that provides educational content, course and university comparisons, scholarship search, course recommendations, and education-advising services (EduAdvisor, n.d.).

UniGuide shares several broad similarities with EduAdvisor:

- Both aim to help students access and understand education-related information.
- Both can help students navigate information that may otherwise require visiting multiple webpages.
- Both seek to make information more accessible and useful for student decision-making.
- Both may reduce the effort needed to locate relevant education information.

The main similarity is the goal of helping students find useful education information. However, their intended users, information sources, and functions are not identical.

## 11. Different from EduAdvisor

| Aspect | EduAdvisor | Proposed UniGuide |
|---|---|---|
| **Primary focus** | Education guidance, course and university comparisons, scholarships, and consultation services. | Answering academic-information questions using official UTM documents. |
| **Target information** | Education options and pathways across institutions, including course information, entry requirements, and scholarships. | A curated collection of official UTM academic resources, initially prioritising Faculty of Computing undergraduate information. |
| **Interaction approach** | Searchable education content, comparison features, recommendation tools, and access to advisors. | Natural-language questions answered using a retrieval-augmented generation approach. |
| **Evidence in responses** | Users can consult the platform's published information and relevant pages. | The proposed system will aim to identify the specific source document and supporting passage used for each answer. |
| **Handling insufficient evidence** | Depends on the particular service or feature used. | The prototype will be designed to indicate when its selected documents do not provide sufficient supporting evidence. |
| **Scope** | Education choices and services across multiple institutions. | A narrower, UTM-focused academic information assistant. |

The comparison is based on EduAdvisor's publicly described services and the planned scope of UniGuide (EduAdvisor, n.d.). The proposed source-referencing and abstention features are design objectives and will need to be implemented and tested.

## 12. Responsible AI Risks (at least 2)

| Risk | Who could be harmed and potential impact | Proposed mitigation |
|---|---|---|
| **Risk 1: Hallucination and misinformation** | Students may receive an incorrect answer about academic regulations, course requirements, or registration dates and make decisions based on it. | Ground answers in retrieved official documents, provide source references, test factual correctness, and abstain when supporting evidence is insufficient. |
| **Risk 2: Outdated or conflicting information** | Students may receive information from an old academic calendar, superseded regulation, or conflicting documents and miss an important requirement or deadline. | Record document dates and source URLs, prioritise current official materials, identify conflicting evidence where possible, and periodically review the knowledge base. |
| **Risk 3: Privacy and inappropriate data handling** | Students may accidentally enter matric numbers, personal details, or sensitive academic information into the assistant. | Use public documents as the initial knowledge base, avoid collecting unnecessary personal information, do not request credentials, and avoid storing user queries containing personal information unless necessary and appropriately protected. |

These risks and mitigations are proposed design considerations. Their effectiveness will be reviewed during implementation and evaluation.

## 13. References

EduAdvisor. (n.d.). *About us*. Retrieved October 27, 2026, from https://eduadvisor.my/about-us

Es, S., James, J., Espinosa-Anke, L., & Schockaert, S. (2024). RAGAs: Automated evaluation of retrieval augmented generation. In *Proceedings of the 18th Conference of the European Chapter of the Association for Computational Linguistics: System Demonstrations* (pp. 150–158). Association for Computational Linguistics. https://doi.org/10.18653/v1/2024.eacl-demo.16

Lewis, P., Perez, E., Piktus, A., Petroni, F., Karpukhin, V., Goyal, N., Küttler, H., Lewis, M., Yih, W.-T., Rocktäschel, T., Riedel, S., & Kiela, D. (2020). Retrieval-augmented generation for knowledge-intensive NLP tasks. *Advances in Neural Information Processing Systems, 33*, 9459–9474. https://papers.nips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html

Ndudiri, O. P., & Bamikole, O. J. (2026). Design and development of an AI-powered intelligent chatbot for student information services in higher educational institutions using large language models. *International Journal of Advanced Research in Science and Technology, 15*(8), 2526–2533. https://doi.org/10.62226/ijarst20262787

Universiti Teknologi Malaysia, Faculty of Computing. (n.d.-a). *Undergraduate*. Retrieved October 27, 2026, from https://comp.utm.my/undergraduate/

Universiti Teknologi Malaysia, Faculty of Computing. (n.d.-b). *Programmes and Student Hub*. Retrieved October 27, 2026, from https://comp.utm.my/programmes-and-student-hub/

Universiti Teknologi Malaysia, Admission. (n.d.). *Undergraduate Kit*. Retrieved October 27, 2026, from https://admission.utm.my/undergraduate-kit/
