# Week 1 Project Scope: PlantPal

**Project name:** PlantPal - Document-Grounded Home Gardening Assistant

**Domain:** Home gardening / horticulture

**Status:** Preliminary semester project scope, 14 October 2026

## Problem Statement

Beginner home gardeners need to understand how light, watering, growing media, and available space affect plant selection and care. Relevant guidance is spread across gardening guides and individual plant resources, so answering a practical question can require consulting several documents. PlantPal will provide plain-language answers grounded in a small, curated collection of official gardening documents, with citations that users can inspect.

The initial context is tropical indoor and balcony gardening, using Singapore-focused NParks material. This is a deliberate limit on the project, rather than a claim that the advice applies to every climate. AI is useful for interpreting everyday questions, combining relevant passages, and asking for missing context. Simple lookups will also be tested with a search baseline; the project will evaluate whether generation adds value.

## Evidence of the Problem

1. **Choosing suitable plants requires environmental knowledge.** NParks explains that plants grown in unsuitable environments become more vulnerable to pests, disease, and death [1]. This supports the need to consider growing conditions when explaining plant choices.
2. **Indoor gardening involves several constraints.** NParks' indoor gardening guide discusses space, light, water, and plant choice [2, PDF page 5]. Its guidance illustrates why a single question may require considering several factors together.

These sources establish practical gardening considerations. They do not prove that beginners want a chatbot or that PlantPal improves outcomes. User needs and the proposed interface will be validated in the next project stage; no interviews or surveys have been conducted for this scope.

## Initial Related Work / Existing Approaches

| Study or solution | Relevant approach | Key limitation relative to this project |
|---|---|---|
| NParks GardeningSG articles and downloadable guides [1, 2, 3] | Authoritative reference material for learning plant care. | Readers must locate and combine the relevant sections themselves. This is a project assessment of the reading workflow, not a measured usability result. |
| NParks Plant Suggestions [4] | A form provides plant suggestions based on garden conditions. | Its stated purpose is plant selection; PlantPal proposes complementary, document-cited explanations and follow-up care questions. No claim is made about the form's internal algorithm. |
| Lewis et al. (2020), Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks [5] | Combines retrieval from external knowledge with generated answers. | General NLP research does not establish performance for tropical home gardening. Corpus selection, citations, clarification, and domain-specific evaluation still need to be designed and tested. |

## Engineering Gap / Limitation

The proposed gap is a narrowly scoped conversational interface that connects a beginner's growing conditions to supporting passages across approved gardening documents, identifies missing information, and makes unsupported questions explicit. PlantPal will investigate this gap; it does not claim that no similar commercial tool exists or that retrieval eliminates hallucinations.

## Initial Project Objectives

- **O1 - Design:** Define a document-grounded gardening assistant, including target questions, a source register, supported topics, and a small reference-answer evaluation set.
- **O2 - Develop:** Implement a text-based retrieval-augmented prototype that produces source-cited answers, asks clarifying questions, and abstains when evidence is insufficient.
- **O3 - Evaluate:** Compare the prototype with a keyword-search baseline on factual accuracy, groundedness, citation correctness, latency, and handling of unsupported or unsafe requests.

## Target Users

Beginner home gardeners caring for a small number of potted plants in tropical indoor or balcony environments. The prototype will support English questions. It is an educational assistant, not a commercial crop-management or plant-disease diagnosis service.

## Data Sources

Three publicly accessible NParks PDFs have been identified through its official resource directory [3]. URLs were checked on 14 October 2026.

| Source | Intended use | URL |
|---|---|---|
| Introduction to Indoor Gardening | Indoor growing conditions and basic care | [PDF](https://isomer-user-content.by.gov.sg/316/5be81ffb-fd47-444d-ab81-bf46b869dd7b/introduction_to_indoor_gardening.pdf) |
| Introduction to Community Gardening | General gardening practices; only home-gardening-relevant passages will be selected | [PDF](https://isomer-user-content.by.gov.sg/316/e9f8a03b-d2aa-4f29-b16a-0678ea9ca5a9/introduction%20to%20community%20gardening.pdf) |
| Know 10 Houseplants | A bounded set of plants for initial document coverage | [PDF](https://isomer-user-content.by.gov.sg/316/43fdd8a1-d385-428f-8cc2-d5b9b36f6a38/know%2010%20house%20plants.pdf) |

The public repository will contain source links and metadata, not redistributed copies of these third-party PDFs. Local ingestion will be subject to the applicable terms. Record document version, access date, checksum, and page metadata when a permitted local copy is acquired. Public accessibility does not imply redistribution permission.

## Semester Scope

**In scope**

- Text Q&A about light, watering principles, growing media, and space requirements within the selected sources.
- Initially up to ten houseplants, with the final supported list determined by adequate source coverage.
- Answers with document and page citations; plain-language explanations of relevant constraints.
- Clarification when plant identity or growing conditions are missing, and explicit uncertainty when a fact is not supported.
- A simple demonstration interface and a reproducible evaluation notebook.

**Out of scope**

- Image-based plant identification or disease diagnosis.
- Pesticide mixing, chemical dosages, ingestion advice, or assurances that a plant is safe for children or pets.
- Weather integration, automated watering, purchases, user accounts, and commercial farming decisions.
- Training a foundation model from scratch, universal species coverage, or guarantees of plant survival.

**Example questions**

- What information should I check before choosing a plant for my balcony?
- What does the indoor gardening guide say about growing media?
- Compare the documented light requirements of two supported plants.
- Can you recommend a watering schedule? (Clarify the plant and conditions; do not invent a fixed schedule.)

## Similar to EduAdvisor

Both are focused question-answering assistants that retrieve information from authoritative documents, produce cited responses, apply scope checks, and evaluate answer quality and latency.

## Different from EduAdvisor

PlantPal addresses plant-care questions for home gardeners instead of academic regulations for students. Its context includes light, space, growing media, and plant identity. Its main domain risks include incorrect care guidance, climate mismatch, and unsupported safety claims.

## Responsible AI Risks and Initial Controls

| Risk | Who is harmed and how? | Proposed control and evaluation |
|---|---|---|
| Hallucinated care instructions | Gardeners may damage plants or waste water and money. | Require supporting passages, check citation support, and abstain on unanswerable questions. |
| Unsafe advice or false safety assurances | Users, children, or pets could be harmed by inappropriate chemical or ingestion guidance. | Keep these requests outside scope; evaluate explicit and indirectly phrased requests. |
| Unequal coverage and climate mismatch | Users with poorly covered species or different climates may receive worse guidance. | Publish supported coverage, ask about relevant conditions, and report results separately for supported and unsupported queries. |
| Privacy | Users may disclose addresses or other unnecessary household details. | Ask only for growing conditions; avoid collecting identities and exact locations; do not publish conversation logs. |
| Misleading citations or document instructions | Users may trust answers that are not supported, or retrieved text could redirect the model. | Treat source text as data, retain provenance, and test irrelevant or adversarial retrieved passages. |

## Preliminary Evaluation Plan

Build a manually reviewed set of 40 questions: 24 answerable care questions, 8 ambiguous questions, and 8 unsupported or out-of-scope questions. Annotate expected facts, supporting pages, and whether clarification or abstention is appropriate. Keep development questions separate from final evaluation questions.

Provisional targets, to refine in Topic 2 (not achieved results):

- At least 85% of answerable questions satisfy a predefined factual-answer rubric.
- At least 90% of factual claims are supported by the cited passages.
- At least 90% of citations point to the correct document and page for the associated claim.
- At least 7 of 8 ambiguous questions trigger an appropriate clarification when needed.
- All 8 out-of-scope cases avoid unsupported actionable advice; report each failure individually.
- Report median and 95th-percentile end-to-end latency over the same test set, with model and hardware recorded; an initial median target is 10 seconds or less.

These small samples provide prototype evidence, not proof of production safety or general reliability. No evaluation has been run yet.

## References

1. National Parks Board. *Choosing Plants*. GardeningSG. https://gardeningsg.nparks.gov.sg/gardening-resource-library/choosing-plants/
2. National Parks Board. *Introduction to Indoor Gardening*. See the direct PDF link in Data Sources.
3. National Parks Board. *Downloadable resources*. GardeningSG. https://gardeningsg.nparks.gov.sg/learn-more-about-gardening/downloads/
4. National Parks Board. *Plant suggestions*. GardeningSG. https://gardeningsg.nparks.gov.sg/new-to-gardening/plant-suggestions/
5. Lewis, P., et al. (2020). *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks*. NeurIPS 33. https://arxiv.org/abs/2005.11401

Web sources accessed 14 October 2026. Project design choices, limitations, and targets are preliminary engineering proposals.
