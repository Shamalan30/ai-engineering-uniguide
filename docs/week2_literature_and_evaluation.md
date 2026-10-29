# UniGuide — Week 2 Research and Evaluation Plan

## 1. Project Overview

**Project Name:** UniGuide — AI-Powered University Information Assistant

**Domain:** Artificial Intelligence, Natural Language Processing and Information Retrieval

**Target Users:** UTM undergraduate students seeking information about academic regulations, course registration procedures and academic dates.

**Project Concept:** UniGuide is a retrieval-augmented question-answering prototype designed to help students retrieve information from selected official UTM academic documents. The system will provide supporting source references and acknowledge when the available evidence is insufficient.

## 2. Problem Evidence

### Evidence 1: Academic information is distributed across multiple resources

The UTM Faculty of Computing undergraduate resource page links to academic regulations, programme handbooks, registration dates, timetables and academic calendars. This provides evidence that students may need to consult different resources for different academic-information needs.

**Source:** Universiti Teknologi Malaysia, Faculty of Computing. Undergraduate Resources.  
https://comp.utm.my/undergraduate/

### Evidence 2: Course registration requires consultation of official guidance

UTM's Academic Management Division publishes course-registration guidelines describing registration requirements and directing students to their respective faculties for timetable information. These procedures are a suitable initial subject area for an academic-information assistant.

**Source:** Universiti Teknologi Malaysia, Academic Management Division. Course Registration Guidelines.  
https://amd.utm.my/course-registration-guidelines-3/

**Evidence limitation:** These sources establish that relevant academic information is distributed across official resources. They do not independently establish how frequently students experience difficulty locating information. Student interviews or a survey could be used to investigate that question.

## 3. Initial Related Work

### Study 1: Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks

**Authors:** Lewis et al. (2020)

**Contribution:** Introduces a framework that combines retrieved external knowledge with language generation.

**Limitation relevant to UniGuide:** Retrieval-augmented generation does not automatically guarantee that every answer is correct or that every cited source supports the generated response.

**Reference:** Lewis, P., et al. (2020). Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks. Advances in Neural Information Processing Systems 33.  
https://papers.nips.cc/paper/2020/hash/6b493230205f780e1bc26945df7481e5-Abstract.html

### Study 2: RAGAs — Automated Evaluation of Retrieval Augmented Generation

**Authors:** Es, James, Espinosa Anke and Schockaert (2024)

**Contribution:** Presents an evaluation framework for assessing aspects of retrieval-augmented generation, including faithfulness, answer relevance and context relevance.

**Limitation relevant to UniGuide:** Automated evaluation metrics do not eliminate the need to verify whether answers accurately interpret the applicable UTM academic documents.

**Reference:** Es, S., James, J., Espinosa Anke, L., & Schockaert, S. (2024). RAGAs: Automated Evaluation of Retrieval Augmented Generation. Proceedings of the 18th Conference of the European Chapter of the Association for Computational Linguistics: System Demonstrations, 150–158.  
https://aclanthology.org/2024.eacl-demo.16/

### Study 3: Academic Chatbot for Campus Information Services Using Retrieval-Augmented Generation

**Contribution:** Examines the use of retrieval-augmented generation for answering campus-information questions from documents.

**Limitation relevant to UniGuide:** The study must be reviewed in greater detail to establish its exact evaluation method, dataset and limitations. Results from another institution may not directly generalise to UTM's academic procedures.

**Reference:** Academic Chatbot for Campus Information Services Using Retrieval-Augmented Generation. Sinkron: Jurnal dan Penelitian Teknik Informatika.  
https://jurnal.polgan.ac.id/index.php/sinkron/article/view/16088

## 4. Engineering Gap

Retrieval-augmented generation provides a foundation for answering questions from external documents, while existing evaluation frameworks support the assessment of answer relevance and faithfulness. UniGuide will apply these ideas to a defined collection of official UTM academic resources and evaluate whether its answers are correct, supported by relevant sources and appropriately limited when the evidence is insufficient.

## 5. Initial Project Objectives

1. To develop a retrieval-augmented question-answering prototype that retrieves relevant information from selected official UTM academic documents.
2. To implement evidence-based responses that display supporting document references and indicate when the available information is insufficient to answer a question reliably.
3. To evaluate the prototype using a prepared set of academic questions based on answer correctness, source support, retrieval effectiveness and appropriate handling of unanswerable questions.

## 6. Initial Data Sources

1. UTM Faculty of Computing undergraduate resources, including the relevant academic regulations and programme documents: https://comp.utm.my/undergraduate/
2. UTM Academic Management Division course-registration guidelines: https://amd.utm.my/course-registration-guidelines-3/
3. UTM Faculty of Computing Programmes and Student Hub, for locating the relevant academic calendar and related resources: https://comp.utm.my/programmes-and-student-hub/

The exact documents, session versions and access dates will be recorded before the documents are incorporated into the prototype.

## 7. Initial Evaluation Plan

The prototype will be evaluated using a manually verified set of academic questions.

- **Answer correctness:** Compare generated answers with verified reference answers.
- **Source support:** Verify whether cited passages support the response.
- **Retrieval effectiveness:** Check whether relevant passages appear among the retrieved results.
- **Handling of unanswerable questions:** Test whether the system acknowledges insufficient evidence instead of inventing an answer.
- **Answer relevance:** Check whether responses address the question asked.

An initial dataset of approximately 30–50 questions is proposed. The final dataset size and evaluation procedure will be refined after the source documents have been collected and inspected.

## 8. Responsible AI Considerations

- **Hallucination:** The system may generate claims that are not supported by retrieved documents.
- **Outdated information:** Old academic regulations or calendars may lead to incorrect guidance.
- **Misleading citations:** A citation may be present but fail to support the corresponding answer.
- **Over-reliance:** Students may treat the assistant's response as authoritative even when the evidence is incomplete.

Possible mitigations include source references, document-version tracking, abstention when evidence is insufficient and a reminder to verify consequential decisions with the relevant official UTM unit.

## 9. Next Steps

1. Download or access the current official documents relevant to the chosen scope.
2. Record each document's title, issuing unit, version or academic session, URL and access date.
3. Create a list of 30–50 test questions with verified answers and supporting sources.
4. Review the third related-work paper in detail before making claims about its results.
5. Refine the project scope and evaluation procedure before implementing the retrieval pipeline.
