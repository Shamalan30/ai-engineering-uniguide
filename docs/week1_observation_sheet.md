# Week 1 Observation Sheet — UniGuide

## 1. Project Title

**UniGuide: AI-Powered University Information Assistant**

## 2. Observation Topic

Difficulty finding and accessing relevant university academic information from multiple official sources.

## 3. Target Users

The primary target users are undergraduate students at Universiti Teknologi Malaysia (UTM), particularly students who need to find academic information related to their studies.

## 4. Observed Problem

University students need to access various types of academic information, including academic regulations, programme requirements, course registration guidance, and academic calendar dates. However, this information may be distributed across different university webpages, documents, and PDF files.

Students may need to visit multiple websites or manually search through lengthy documents to locate specific answers. This process can take time, especially when students are unfamiliar with the university's website structure or do not know which official document contains the information they need.

Incorrectly understanding or relying on outdated academic information may also cause confusion. Therefore, there is an opportunity to improve how students search for and access official university information.

**Observation note:** These points describe the problem being investigated. A student survey or interview is still needed to confirm how frequently students experience these difficulties and which types of information are most challenging to find.

## 5. Existing Situation

Currently, students can obtain academic information through official university webpages, faculty websites, academic calendars, handbooks, and other university documents.

For example, the UTM Faculty of Computing provides undergraduate-related resources through its official website. UTM also publishes academic calendar documents containing important academic dates.

Although these resources provide useful information, students may need to navigate between different sources and identify the relevant sections themselves.

## 6. Evidence and Sources

### Evidence 1: UTM Faculty of Computing Undergraduate Resources

**Source:** https://comp.utm.my/undergraduate/

This webpage serves as an official entry point for undergraduate-related resources. It provides a starting point for examining how academic information is made available to students.

**Relevance to the problem:** Students may need to navigate available resources to locate information relevant to a particular academic question.

### Evidence 2: UTM Academic Calendar 2026/2027

**Source:** https://amd.utm.my/wp-content/uploads/sites/460/2026/05/Final_Kalendar-Akademik-Sarjana-Muda.Sarjana.Kedoktoran-20262027-14.5.2026-pembetulan.pdf

The academic calendar is an official university document containing academic dates and schedules.

**Relevance to the problem:** Students who need a specific date may have to locate the relevant semester or section within the document.

### Evidence 3: Student Feedback — To Be Collected

A short survey or interview will be conducted with UTM undergraduate students to investigate:

- Whether students experience difficulty finding academic information.
- Which academic information they search for most frequently.
- Which sources they currently use.
- How much time they spend searching for answers.
- Whether they would find a source-referencing AI assistant useful.

**Status:** Planned. No survey results are claimed at this stage.

## 7. Current User Workaround

Students can currently search university webpages, open relevant PDF documents, use document search functions, or ask university staff and other students for assistance.

These approaches can be useful, but students may still need to identify the correct source and verify whether the information applies to their situation.

## 8. Identified Opportunity

An AI-powered university information assistant could provide a simpler way for students to ask questions in natural language and retrieve relevant information from approved official university documents.

The proposed system, UniGuide, would:

- Allow students to ask academic-information questions in natural language.
- Retrieve relevant passages from official university documents.
- Generate answers based on the retrieved information.
- Provide source references so students can verify the answers.
- Indicate when sufficient supporting information cannot be found rather than guessing.

## 9. Proposed AI Contribution

UniGuide will investigate the use of **Retrieval-Augmented Generation (RAG)** to combine document retrieval with AI-generated responses. The system will search a prepared collection of university documents and use relevant passages to support its answers.

The main AI contribution is not simply displaying university information, but helping students locate relevant information and receive answers grounded in identifiable official sources.

## 10. Initial Project Boundaries

The initial scope will focus on publicly available UTM academic information, such as:

- Academic calendars and important academic dates.
- Undergraduate programme information.
- Academic regulations and student guidance, where suitable official documents are available.

The initial version will not replace university staff, provide official academic decisions, or guarantee answers to questions that are not supported by the collected documents.

## 11. Initial Assumptions to Validate

1. Relevant academic information is available through public official university sources.
2. Students may benefit from searching across these sources using natural-language questions.
3. Providing source references can help students verify answers.
4. A system that acknowledges insufficient evidence can reduce unsupported answers.

These assumptions will be reviewed through source inspection, student feedback, and system evaluation during the project.

## 12. Week 1 Conclusion

The initial observation identifies a potential usability problem in accessing academic information distributed across university webpages and documents. UniGuide is proposed as an AI-based solution that retrieves information from official sources and provides source-supported answers.

The next step is to validate the problem with credible references and student feedback, review existing AI information-assistant approaches, and refine the project objectives and evaluation criteria.
