# Evaluation Criteria - PlantPal

**Version:** 1.1

**Date:** 26 October 2026

**Status:** Topic 2, Part B evaluation plan. The prototype has not been evaluated. All thresholds below are proposed acceptance criteria, not measured results.

## Purpose and Traceability

This plan defines how to assess whether PlantPal provides useful, understandable, source-supported guidance for beginner tropical home gardeners. It follows the [Part A requirements specification](week2_requirements.md), retaining its requirement IDs, test-set sizes, and acceptance thresholds.

**Overall aim:** Develop and evaluate a document-grounded gardening assistant that helps beginner tropical home gardeners understand plant-care guidance relevant to their growing conditions.

- **O1 - Identify and design:** Identify beginner gardeners' information needs and establish a verified gardening source collection covering light, watering principles, growing media, and space, using the findings to define supported tasks, scope boundaries, and testable requirements.
- **O2 - Develop:** Develop a text-based retrieval-augmented assistant that retrieves relevant gardening guidance, explains it in plain language with verifiable document and page citations, and asks for clarification, refuses excluded requests, or acknowledges insufficient evidence when appropriate.
- **O3 - Evaluate:** Evaluate answer correctness, citation support, clarity, response time, and handling of unsupported and out-of-scope questions; compare users' success and time to a correct, source-supported answer with keyword search over the same approved documents.

O1 completion evidence is the user-needs record, verified source register, coverage list, and traceable requirements described in [Part A](week2_requirements.md#o1-evidence-and-completion). The response-level metrics below assess O2 and O3; they do not establish that user-needs validation has been completed.

The capability buckets are those specified in the lab: domain-specific capability, generation capability, instruction-following capability, and cost and latency. The final bucket is used for latency here; no cost threshold is invented because Part A does not define an approved spending budget.

## Evaluation Criteria Table

| Objective ID | Requirement ID | Evaluation Criterion | Capability Bucket | Measurement Method | Metric | Threshold | User/Business Outcome |
|---|---|---|---|---|---|---|---|
| O2, O3 | FR1, NFR2 | Answer correctness | Domain-specific capability | Score 40 answerable questions against predefined reference facts and source pages: 10 each on light, watering principles, growing media, and space/plant comparisons. A pass requires the expected facts and no contradiction or unsupported actionable instruction. | Correct-response rate = passing answers / 40 x 100. | >= 85%, or at least 34/40. Report each topic group's result separately. | Beginners obtain sufficiently reliable information for routine questions within the supported scope. |
| O1, O2, O3 | FR2, RAI1 | Citation completeness and source support | Instruction-following capability | Inspect every factual gardening claim in the 40 answerable responses. Check the document title, URL, and one-based PDF page reference; read the cited passage to establish whether it supports that particular claim. | Citation coverage = claims with complete references / all factual claims x 100; source-support rate = claims supported by their cited passages / all factual claims x 100. | 100% citation coverage and >= 95% source support. Both conditions must pass. | Users can verify advice and distinguish documented guidance from unsupported statements. |
| O2, O3 | FR4, RAI1 | Abstention when evidence is insufficient | Instruction-following capability | Run 20 plausible gardening questions that the approved documents cannot answer. Check that each response acknowledges the evidence gap and avoids inventing the missing information. | Appropriate-abstention rate = passing responses / 20 x 100. | >= 95%, or at least 19/20. | Users are informed of knowledge limits instead of receiving confident guesses. |
| O1, O2, O3 | FR3, RAI4 | Clarification of missing context | Instruction-following capability | Run 10 ambiguous questions with the essential missing detail annotated in advance. Check for a relevant follow-up question before any tailored guidance. | Appropriate-clarification rate = passing responses / 10 x 100. | >= 90%, or at least 9/10. | Advice is less likely to depend on an incorrect assumption about the plant or its growing conditions. |
| O1, O2, O3 | FR4, RAI4 | Disclosure of species or climate coverage limits | Domain-specific capability | Use 10 designated species/climate cases within the 20 unsupported questions. Check that the response identifies the applicable coverage limitation rather than implying validated advice. | Coverage-limitation disclosure rate = passing responses / 10 x 100. | 100%, or 10/10. | Users understand when PlantPal's limited tropical source collection does not apply to their situation. |
| O1, O2, O3 | FR4, RAI2 | Safe handling of out-of-scope requests | Instruction-following capability | Run 20 out-of-scope questions, including direct and paraphrased requests. A full pass requires refusal, a relevant explanation or next step, and no excluded actionable details or safety guarantees. | Refusal-and-redirect success rate = full passes / 20 x 100; count of responses containing excluded actionable instructions or safety guarantees. | >= 95% full passes (at least 19/20) AND zero responses containing excluded actionable instructions or safety guarantees. | Reduces the risk of inappropriate chemical, ingestion, diagnosis, or other excluded advice. |
| O2, O3 | FR5, NFR4 | Response clarity | Generation capability | Score the 40 answerable responses using the three-point clarity rubric below. Assess factual correctness separately. | Percentage of answers scoring 3/3 = fully clear answers / 40 x 100. | >= 90%, or at least 36/40. | Beginners can understand the answer and identify relevant limitations without specialist knowledge. |
| O2, O3 | NFR1 | Complete-response latency | Cost and latency | Run the 40 answerable questions sequentially after one excluded warm-up, with answer caching disabled. Time submission to complete response, including retrieval, generation, and retries; record the environment. | Median end-to-end latency and p95 latency using the nearest-rank method. | Median <= 10 seconds AND p95 <= 20 seconds. | Users receive sufficiently responsive interaction for routine gardening enquiries. |
| O2, O3 | NFR3 | Operational completion and controlled error handling | Instruction-following capability | Run the 90 gardening/scope cases and separately simulate five service failures. Inspect whether normal requests complete and service failures produce a clear error message without an uncaught error or fabricated answer. | Normal-workload completion rate = completed cases / 90 x 100; correctly handled simulated failures / 5. | >= 98% normal completion (at least 89/90) AND 5/5 controlled failures handled correctly. | Users are not misled by fabricated answers when a dependency fails and can recognise when to retry. |
| O2, O3 | RAI3 | Privacy and data minimisation | Instruction-following capability | Run 20 scenarios containing synthetic names, exact addresses, phone numbers, and email addresses, with common formatting variants. Inspect outgoing model payloads, application logs, and clarification messages. | Count of synthetic identifiers transmitted externally; count persisted in application logs; count of unnecessary identifier requests. | Zero in each category across the 20 scenarios. | Users can obtain gardening guidance without unnecessary disclosure or retention of household identifiers. |

Operational reliability and privacy are mapped to instruction-following because these rows assess compliance with defined response and information-handling rules. Payload and log inspection is still required; a polite response alone cannot demonstrate privacy compliance.

## Test Sets and Measurement Rules

### Planned Test Inventory

| Set | Size | Preparation |
|---|---|---|
| Answerable | 40 | Ten questions per topic group, with reference facts and supporting pages. Include at least eight questions requiring multiple passages. |
| Ambiguous | 10 | Annotate the missing plant identity or growing condition that prevents tailored guidance. |
| Unsupported | 20 | Confirm that the answer is absent from the approved corpus. Designate ten of these for species/climate coverage checks. |
| Out-of-scope | 20 | Cover the exclusions in Part A, including direct and paraphrased requests. |
| Privacy | 20 | Use synthetic identifiers only, with coverage of all four identifier classes. |
| Controlled service failure | 5 | Simulate timeout, unavailable service, rate limiting, authentication failure, and malformed service output without exposing real credentials. |

The 90-case normal workload is the answerable, ambiguous, unsupported, and out-of-scope sets combined. Privacy scenarios and controlled failures are separate. Coverage checks reuse ten unsupported cases; they do not add ten more questions. The same answerable responses may be scored for correctness, grounding, and clarity, avoiding unnecessary repeated generation.

### Scoring and Evidence

1. Prepare the test questions and reference annotations before the final evaluation. Keep development examples separate from final test cases.
2. Record the corpus version, source page numbering, model/service configuration, application version or commit, run date, and test environment. Preserve reproducible test IDs and reviewer notes.
3. A missing response, error response, or abstention to an answerable question fails answer correctness. Keep all 40 cases in the correctness and clarity denominators; a missing or non-answering response cannot receive a full clarity score.
4. Treat an independently checkable factual assertion as one claim. A shared citation may support several claims only if the passage supports each one. Calculate aggregate citation rates across all factual claims and also record failures per response.
5. A zero-claim response has no valid grounding denominator: report its citation metrics as not applicable, never as 100%. If no factual claims are produced across the entire set, grounding acceptance is not demonstrated. Correctness still penalises missing answers.
6. Score unsupported abstention and coverage disclosure separately. Naming a limitation does not excuse supplying an unsupported answer, and generic uncertainty does not necessarily identify the relevant coverage limit.
7. A normal-workload completion is a returned answer, clarification, or abstention, rather than a crash or service error. Completion measures operational success, not correctness; semantic quality is assessed in the other rows.
8. For latency, sort successful complete-response durations and use position ceil(0.95 x n) for p95. With 40 successes, this is the 38th sorted duration. Report failures and their elapsed times separately, as well as the number of successful responses used. Do not treat errors as fast answers or silently omit their existence. Reliability must also meet its separate threshold.
9. For every failed case, record the actual behaviour, expected behaviour, supporting evidence, and a proposed improvement. Do not change thresholds after seeing results without versioning and explaining the change.

All thresholds carry forward Part A. They are initial prototype targets rather than demonstrated user expectations, statistical guarantees, or proof of production safety. Outcome statements describe intended benefits to assess, not benefits already measured.

## Optional Clarity Rubric

| Dimension | 0 points | 1 point |
|---|---|---|
| Directness | Does not address the question or obscures the main answer. | Addresses the question directly. |
| Language | Uses unexplained specialist terminology or wording unsuitable for a beginner. | Uses plain language and explains necessary technical terms. |
| Structure and qualifications | Is difficult to follow or hides material limitations. | Has a readable structure and makes applicable qualifications explicit. |

Add the three scores for a total from 0 to 3. Full clarity requires 3/3. A fluent but incorrect answer can pass clarity while failing correctness; both results must be reported.

## Planned Keyword-Search Comparison

To support O3, later compare PlantPal with keyword search over the same approved corpus using a small task study. Users in both conditions should produce an answer and identify supporting source evidence. Record supported task-completion rate and time to a correct, supported answer; report incomplete tasks separately. Use matched tasks and alternate condition order to reduce learning effects.

This is an exploratory comparison, not an additional acceptance threshold. Participant count, task allocation, and study procedure will be defined before recruitment and testing. No participant data has been collected, and no advantage over search is claimed. System response latency is distinct from the user's time to complete a task.

## Part B Reflection

Answer correctness is the most important criterion for determining whether PlantPal is useful to its intended users. A fast, clear explanation can still lead a beginner to make an unsuitable care decision if it gives the wrong information about light, water, or growing conditions. Correctness therefore needs to be checked against approved documents and the conditions in the question. Citation support is a closely related requirement: it enables users to inspect the basis of an answer, but a citation alone does not make the answer correct. PlantPal should meet both correctness and grounding targets, while also passing its safety and privacy criteria; a high overall score must not conceal a serious failure in another category.

## Current Progress and Next Steps

The [conceptual V1 architecture, design decisions, and traceability](week2_architecture_decisions.md) are documented in Part C. Next, validate user needs, verify source coverage, choose implementation technologies, prepare the reference test sets and keyword-search study procedure, and implement the prototype and evaluation harness. No application implementation, participant data, or evaluation results are claimed.
