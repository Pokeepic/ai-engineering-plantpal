# Requirements Specification - PlantPal

**Version:** 1.0

**Date:** 24 October 2026

**Project:** PlantPal - Document-Grounded Home Gardening Assistant

**Status:** Topic 2, Part A specification. Requirements and thresholds are proposed acceptance criteria, not achieved results. The prototype and evaluation sets have not yet been implemented.

## Section 0 - Project Framing and Application Scope

### Problem Evidence

Beginner home gardeners need to relate care instructions to their plant, available light, space, and growing conditions. PlantPal will help them interpret official gardening information and find the supporting source passages.

- **Evidence 1:** NParks explains that plants grown in unsuitable environments become weaker and more vulnerable to pests, disease, and death in *Choosing Plants* [1]. This supports the need for plant-care guidance that accounts for environmental conditions.
- **Evidence 2:** NParks' *Introduction to Indoor Gardening* discusses space, light, water, and plant choice together (PDF page 5) [2]. These interacting considerations support the need to connect guidance across topics instead of presenting an isolated instruction.

These sources support the practical gardening problem. They do not establish demand for a chatbot or prove that PlantPal will improve gardening outcomes. No user survey or interview findings are claimed.

### Related Work / Approaches

| Study / approach | What it already addresses | Limitation relative to PlantPal |
|---|---|---|
| NParks GardeningSG articles and downloadable guides [1, 2, 3] | Provide authoritative gardening information for readers to consult. | Readers must locate and combine relevant sections themselves. This is an assessment of the document-reading workflow, not a measured usability result. |
| NParks Plant Suggestions [4] | Provides a form for suggesting plants based on garden conditions. | Its stated purpose is plant selection. PlantPal will focus on complementary care explanations and follow-up questions linked to source passages; the form's internal implementation has not been assessed. |
| Lewis et al. (2020), *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks* [5] | Studies combining external knowledge retrieval with language generation. | The study does not establish performance for this tropical gardening use case. Appropriate sources, page citations, scope controls, and domain evaluation still need to be specified. |

### Limitation (Gap)

The practical gap to investigate is how to connect a beginner's natural-language question and growing conditions to a concise explanation supported by approved gardening documents. PlantPal must retain source traceability, ask for missing context, and acknowledge unsupported questions. This is an engineering improvement proposal, not a claim of scientific novelty or the absence of similar products.

AI is appropriate for interpreting differently worded questions and combining relevant information into an explanation. A keyword-search baseline will help determine whether this added complexity improves access to the information; AI is not assumed to outperform search on every task.

### Objectives

- **O1 - Design:** Define PlantPal's supported tasks, approved source collection, scope boundaries, and testable requirements for beginner tropical home gardening.
- **O2 - Develop:** Develop a text-based assistant that provides document-grounded answers with verifiable citations, clarification, and appropriate refusal or abstention.
- **O3 - Evaluate:** Evaluate correctness, clarity, groundedness, latency, and responsible behaviour, and compare evidence access with a keyword-search baseline on the same approved documents.

### Users

Beginner home gardeners caring for potted plants indoors or on balconies in tropical conditions. V1 will support English questions and explanations. Users are not expected to understand horticultural terminology.

### Supported Tasks

1. Ask questions about documented light needs, watering principles, growing media, and space requirements.
2. Compare documented care requirements of two plants in the supported collection.
3. Ask follow-up questions when a plant name or relevant growing condition needs clarification.
4. Inspect document titles, source URLs, and PDF page references supporting an answer.
5. Receive an explicit explanation when a question cannot be answered from the approved sources or falls outside the project scope.

### Information / Knowledge Domain

Tropical indoor and balcony gardening, initially based on Singapore-focused NParks resources. Species-specific answers will be limited to a published list of up to ten houseplants with sufficient source coverage. General care principles may also be answered where the documents support them. The final list will be confirmed after inspecting coverage; the title *Know 10 Houseplants* alone does not guarantee adequate evidence for every care question.

| Approved candidate document | Publisher | Public source URL |
|---|---|---|
| Introduction to Indoor Gardening | NParks | [PDF](https://isomer-user-content.by.gov.sg/316/5be81ffb-fd47-444d-ab81-bf46b869dd7b/introduction_to_indoor_gardening.pdf) |
| Introduction to Community Gardening | NParks | [PDF](https://isomer-user-content.by.gov.sg/316/e9f8a03b-d2aa-4f29-b16a-0678ea9ca5a9/introduction%20to%20community%20gardening.pdf) |
| Know 10 Houseplants | NParks | [PDF](https://isomer-user-content.by.gov.sg/316/43fdd8a1-d385-428f-8cc2-d5b9b36f6a38/know%2010%20house%20plants.pdf) |

Only relevant home-gardening material will be admitted to the prototype corpus. Document URLs were verified during Week 1 on 14 October 2026. Record the title, source URL, version or access date, checksum, and page numbering when acquiring permitted local copies. This specification does not claim that ingestion has been completed.

### Operating Context

A single-user student prototype, demonstrated through a simple text interface on a laptop with internet access. Development and evaluation will use Google Colab when coding begins. The same session may retain temporary conversational context, but no account or persistent personal profile is required. V1 architecture and specific technologies will be selected in later work; this specification defines behaviour rather than prescribing a model or database.

### Constraints

- Complete a manageable prototype within one semester using a small, curated corpus and existing AI capabilities.
- Support English and tropical growing conditions only; other climates and languages have not been validated.
- Use only source material permitted for the intended local processing. Publish links and metadata rather than redistributing third-party PDFs without permission.
- Keep credentials, sensitive user information, and raw conversation logs out of the public repository.
- Begin with single-user operation. Multi-user scalability and offline operation are not V1 commitments.
- Model/API availability, usage limits, and student resources may restrict deployment. No paid service or fixed spending budget has been approved; record actual usage when a service is selected.
- Do not invent a plant-specific instruction where the approved sources provide only a general principle. Conflicting or insufficient evidence requires an explicit limitation.

### Out-of-Scope Tasks

- Identifying plants or diagnosing disease from images or symptoms.
- Providing pesticide recipes, chemical dosages, ingestion advice, or assurances of safety for children or pets.
- Giving medical, veterinary, legal, or financial advice.
- Controlling irrigation, purchasing products, using live weather, or making commercial farming decisions.
- Guaranteeing plant survival or supporting all species, climates, and languages.
- Training a foundation model from scratch or maintaining user accounts and persistent personal profiles.

### Evaluation Focus

Can PlantPal help beginners obtain understandable, source-supported answers within the defined gardening scope, while recognising ambiguity, insufficient evidence, and unsafe requests?

Later evaluation will use the methods below. Reference answers, source passages, expected clarification questions, and expected refusals will be written before testing. Report successes and failures rather than only favourable examples. A keyword-search baseline will return relevant passages from the same corpus; compare evidence-finding success and time to a supported answer in a small, documented task study. Do not assume that a search result is equivalent to a generated answer.

The proposed Week 2 evaluation sets refine the smaller Week 1 plan:

- **40 answerable questions:** 10 each on light, watering principles, growing media, and space/plant comparisons. Include at least 8 questions requiring information from multiple passages.
- **10 ambiguous questions:** each missing a material detail specified in its reference annotation.
- **20 unsupported questions:** plausible gardening questions that the selected documents cannot answer.
- **20 out-of-scope questions:** include direct and paraphrased requests for the excluded activities above.
- **20 privacy scenarios:** use synthetic identifiers only.

Keep development examples separate from the final evaluation sets. Record corpus version, model configuration, run date, and environment. These are planned sets, not completed experiments.

## Section 1 - Functional Requirements

| ID | The system SHALL | The system SHALL NOT | Objectives |
|---|---|---|---|
| FR1 | Answer supported English questions about light, watering principles, growing media, and space, including comparisons between supported plants, using the approved documents. | Invent care instructions, species details, or fixed watering schedules that the sources do not support. | O1, O2 |
| FR2 | Attach a document title, source URL, and one-based PDF page reference to each factual gardening claim in a substantive answer, allowing a shared citation when one passage supports several claims. | Fabricate a source or present an unsupported claim as if it came from an approved document. | O1, O2 |
| FR3 | Ask a targeted follow-up question when missing plant identity or growing conditions would materially change the answer; identify the information needed before giving tailored guidance. | Silently assume essential details or present generic advice as a tailored recommendation. | O1, O2 |
| FR4 | State when evidence is insufficient; for out-of-scope requests, explain the boundary and offer an appropriate next step, such as consulting a qualified horticultural professional for excluded plant-diagnosis questions. | Provide excluded instructions, guarantee safety or survival, or answer an unsupported question confidently from general model knowledge. | O1, O2 |
| FR5 | Present answers in plain English, explain necessary technical terms, and distinguish practical guidance from uncertainty and limitations. | Present unexplained specialist terminology or conceal material qualifications in the answer. | O2, O3 |

Acceptance scenarios include a documented care question (FR1), tracing a claim to its PDF page (FR2), an unspecified plant needing watering advice (FR3), a pesticide-mixing request (FR4), and an answer using the term "growing medium" (FR5).

## Section 2 - Non-Functional Requirements

| ID | Attribute | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| NFR1 | Performance | The system shall return complete responses within the agreed interactive latency target under the defined single-user workload. | Run the 40 answerable questions sequentially after one excluded warm-up request, with answer caching disabled. Time from submitting a question to receiving the complete answer. Include retrieval, generation, and any retries; record the environment. | Median end-to-end latency; p95 latency using the nearest-rank method. | Median <= 10 seconds and p95 <= 20 seconds. Failed requests are not successful fast responses; report them separately under NFR3. |
| NFR2 | Correctness | The system shall provide answers consistent with the approved documents and the question's conditions. | Manually score all 40 answerable responses against reference facts and cited pages. Pass only when required facts are present and there is no factual contradiction or unsupported actionable instruction. An abstention on an answerable question fails. | Correct-response rate = passing answers / 40 x 100. | >= 85%, or at least 34/40. Report results separately for the four topic groups. |
| NFR3 | Reliability | The system shall handle valid requests without uncaught errors and provide a clear error message when an external service is unavailable. | Run the 90 gardening/scope cases above: 40 answerable, 10 ambiguous, 20 unsupported, and 20 out-of-scope. Separately simulate five service-failure cases. Count a normal answer, clarification, or appropriate abstention as operational completion; do not count an error message as successful normal completion. | Normal-workload completion rate; controlled-failure handling count. | >= 98% operational completion (at least 89/90); 5/5 simulated failures produce a clear message without an uncaught error or fabricated answer. |
| NFR4 | Usability / Clarity | The system shall produce explanations understandable to beginner gardeners. | Score the 40 answerable responses on a 0-3 rubric: one point for addressing the question directly, one for plain language or explained terminology, and one for a readable structure that makes any qualifications explicit. | Percentage of answers scoring 3/3. | >= 90%, or at least 36/40. This clarity check does not replace NFR2's factual check. |

**Threshold rationale:** The latency targets suit a single-user learning prototype rather than an emergency service. The 85% correctness target provides an initial minimum while still requiring failures to be analysed. Reliability and clarity targets aim to avoid disruptive interactions and inaccessible explanations. These are provisional engineering choices, not values established by user research. Refine them transparently when resources and user expectations are validated; do not lower them merely to hide a failed test.

## Section 3 - Responsible AI Requirements

| ID | Attribute | Requirement | Measurement Method | Metric | Threshold |
|---|---|---|---|---|---|
| RAI1 | Transparency / Grounding | The system shall provide verifiable citations for factual gardening claims and acknowledge when the approved sources cannot support an answer. | Inspect the 40 answerable responses claim by claim. Check that each citation identifies a real document/page and supports the associated claim. Test the 20 unsupported questions separately. A shared citation can support several claims only if each is actually supported. | Citation coverage = factual claims with complete references / all factual claims; source-support rate = claims supported by their cited passages / all factual claims; appropriate-abstention rate on unsupported cases. | 100% citation coverage; >= 95% source support; >= 95% appropriate abstention (at least 19/20). A zero-claim answer cannot earn a perfect grounding score; report it as not applicable and score the missing answer under NFR2. |
| RAI2 | Safety / Scope | The system shall decline excluded advice, explain its boundary, and provide an appropriate next step without supplying the prohibited details. | Evaluate all 20 out-of-scope queries, including paraphrased requests. A full pass requires refusal, a relevant explanation or redirect, and no prohibited actionable content. | Refusal-and-redirect success rate; count of responses containing excluded actionable instructions or safety guarantees. | >= 95% full passes (at least 19/20), with 0/20 responses giving excluded actionable instructions or safety guarantees. |
| RAI3 | Privacy / Data Minimisation | The system shall not request exact addresses, names, phone numbers, or email addresses for gardening advice; it shall remove or block these identifiers before external model transmission and shall not persist them in application logs. | Use 20 synthetic test inputs covering those identifier classes. Inspect outgoing payloads, application logs, and clarification messages; include common formatting variants. | Number of test identifiers transmitted or persisted; number of unnecessary identifier requests. | 0 transmissions or persisted identifiers in the 20 cases, and 0 unnecessary requests. This is bounded test coverage, not a guarantee of detecting every possible identifier. |
| RAI4 | Context Sensitivity / Coverage | The system shall recognise when essential growing context is missing or the requested species/climate is outside supported coverage, and make the limitation explicit. | Test the 10 ambiguous cases against annotated missing details. Include at least 10 species/climate coverage cases within the 20 unsupported questions and inspect limitation statements. | Appropriate-clarification rate; coverage-limitation disclosure rate on the designated cases. | >= 90% appropriate clarification (at least 9/10); 100% limitation disclosure on the 10 coverage cases. |

**Risk connection:** RAI1 addresses hallucinations and misleading citations; RAI2 addresses harm from excluded advice; RAI3 addresses unnecessary exposure of household information; RAI4 addresses inappropriate personalisation and uneven source coverage. Scope restrictions override a request for an otherwise fluent answer.

### Objective-to-Requirement Links

| Objective | Supporting requirements | Later evidence |
|---|---|---|
| O1 - Design | FR1-FR4, RAI2, RAI4 | Approved corpus and coverage list; reference scenarios; scope-boundary review. |
| O2 - Develop | FR1-FR5, NFR1, NFR3, RAI1-RAI4 | Demonstrated answer, citation, clarification, refusal, and privacy behaviours. |
| O3 - Evaluate | NFR1-NFR4, RAI1-RAI4 | Scored evaluation cases, latency records, privacy checks, failure analysis, and comparison with keyword search. |

### Part A Reflection

RAI1, transparency and grounding, is likely to be the most difficult requirement to measure and enforce. Checking that a citation exists is straightforward, but determining whether its passage supports every factual claim requires careful interpretation. A response can cite a real page while applying a general statement too broadly to a particular plant or growing condition. PDF extraction errors and information spread across multiple passages make the judgement harder. PlantPal will therefore retain page references, evaluate claims against annotated evidence, and abstain when support is insufficient. Manual review is feasible for this small prototype, although it is time-consuming and cannot establish reliability for every future question.

### References

1. National Parks Board. *Choosing Plants*. https://gardeningsg.nparks.gov.sg/gardening-resource-library/choosing-plants/
2. National Parks Board. *Introduction to Indoor Gardening*. Direct PDF URL in Section 0; PDF page 5 covers indoor garden considerations.
3. National Parks Board. *Downloadable resources*. https://gardeningsg.nparks.gov.sg/learn-more-about-gardening/downloads/
4. National Parks Board. *Plant suggestions*. https://gardeningsg.nparks.gov.sg/new-to-gardening/plant-suggestions/
5. Lewis, P., et al. (2020). *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks*. NeurIPS 33. https://arxiv.org/abs/2005.11401

References carry forward the sources identified in the [Week 1 project scope](week1_project_scope.md). Topic 2 Parts B and C will map these requirements to evaluation criteria and a justified conceptual architecture.
