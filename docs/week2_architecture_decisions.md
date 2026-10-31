# UniGuide – Week 2 Architecture Decisions

## 1. Introduction

This document records the key architectural decisions made during the design of UniGuide, an AI-powered academic information assistant for UTM undergraduate students.

The purpose is to explain the selected architectural components, alternatives considered, and trade-offs accepted.

## 2. Architecture Decision Records (ADRs)

### ADR 1: Document-Based Knowledge Retrieval

**Decision:** Use a knowledge retrieval component to obtain relevant information from approved UTM academic documents before generating an answer.

**Requirement / Constraint:**
- The system must provide answers based on official UTM academic documents.
- The system must provide relevant source references.
- The system should avoid generating unsupported academic information.

**Alternatives Considered:**
1. Use an AI language model without document retrieval.
2. Provide students with a list of static document links.
3. Use a knowledge retrieval component to search approved documents and provide relevant information to the answer generation component.

**Selected Option:**

Option 3 was selected. The knowledge retrieval component searches the approved academic documents and passes relevant information and source references to the answer generation component.

**Trade-offs Accepted:**

This approach requires additional processing and regular document maintenance. However, it improves answer grounding, source traceability, and the reliability of academic information.

### ADR 2: Explicit Scope and Safety Control

**Decision:** Include a scope and safety control component to identify unsupported and out-of-scope questions before generating an answer.

**Requirement / Constraint:**
- The system must focus on UTM undergraduate academic information.
- The system must identify questions outside its defined scope.
- The system must avoid presenting unsupported information as confirmed academic policy.

**Alternatives Considered:**
1. Allow the answer generation component to handle all questions without a separate scope check.
2. Use an explicit scope and safety control component before answer generation.
3. Use only response validation after an answer has been generated.

**Selected Option:**

Option 2 was selected. The scope and safety control component checks whether a question is relevant to UniGuide's defined domain. Out-of-scope questions are directed to a refusal or redirection response.

Response validation is also included to check generated answers before they are returned to students.

**Trade-offs Accepted:**

This approach adds another processing stage and may occasionally reject questions that could have been answered. However, it reduces the risk of misleading or irrelevant academic responses.

### ADR 3: Use of Approved Academic Documents

**Decision:** Use approved UTM academic documents as the primary knowledge sources for UniGuide.

**Requirement / Constraint:**
- Answers should be based on relevant and reliable academic information.
- The system should not depend on unverified external information.
- Academic documents may require updates when university policies or guidelines change.

**Alternatives Considered:**
1. Use general information available on the internet.
2. Use only documents provided by students.
3. Use approved UTM academic documents as the primary knowledge sources.

**Selected Option:**

Option 3 was selected. The initial system will use approved UTM academic documents, including academic regulations, programme handbooks, course registration guidelines, and academic calendars.

**Trade-offs Accepted:**

The system's knowledge is limited to the available documents and may become outdated if the documents are not maintained. However, using approved sources provides a more controlled and trustworthy knowledge base.

## 3. Requirements Traceability Matrix

| Objective | Related Requirements | Evaluation Criteria | Architecture Components | Evidence to be Collected |
|---|---|---|---|---|
| O1: Design an AI-powered academic information assistant. | FR1, FR2, FR5 | Domain-specific answer accuracy and response clarity | User interface, query processing, answer generation | Test academic questions and review response quality |
| O2: Develop document-grounded question answering with source references. | FR1, FR3, RAI1 | Answer accuracy and source citation relevance | Knowledge retrieval, retrieved context and source references, answer generation | Compare answers and citations against official UTM documents |
| O3: Evaluate system correctness, response time and out-of-scope handling. | FR4, NFR1, RAI2 | Out-of-scope handling and response time | Scope and safety control, response validation, query processing | Test out-of-scope questions and measure response time |

## 4. Conclusion

The architectural decisions establish a conceptual foundation for UniGuide. The selected architecture prioritises document-grounded responses, reliable source references, and appropriate handling of unsupported questions.

These decisions will guide the next development stages while allowing the architecture to be refined based on implementation and evaluation results.
