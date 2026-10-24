# PlantPal - Home Gardening Assistant

> A planned AI assistant that answers beginner home-gardening questions using official gardening documents and verifiable citations.

**Status:** Week 2 Part A requirements specified. The AI application has not been implemented.

## Problem Statement

Beginner home gardeners need to relate plant-care guidance to their available light, space, and growing conditions. Relevant material is distributed across guides and plant resources. PlantPal will retrieve supporting passages and explain them in plain language, ask for missing context, and acknowledge when the documents cannot answer a question.

## Evidence of the Problem

- NParks explains why matching plants to their environment matters in [Choosing Plants](https://gardeningsg.nparks.gov.sg/gardening-resource-library/choosing-plants/).
- Its [Introduction to Indoor Gardening](https://isomer-user-content.by.gov.sg/316/5be81ffb-fd47-444d-ab81-bf46b869dd7b/introduction_to_indoor_gardening.pdf) discusses multiple practical constraints, including light, space, and water.

These sources support the gardening context; chatbot demand and effectiveness remain to be validated.

## Initial Related Work / Existing Approaches

- [NParks gardening guides](https://gardeningsg.nparks.gov.sg/learn-more-about-gardening/downloads/): authoritative references, but users must locate and combine information themselves.
- [NParks Plant Suggestions](https://gardeningsg.nparks.gov.sg/new-to-gardening/plant-suggestions/): condition-based plant selection; PlantPal proposes complementary conversational care explanations.
- [Lewis et al. (2020), Retrieval-Augmented Generation](https://arxiv.org/abs/2005.11401): a relevant technical foundation whose results do not establish performance for this gardening use case.

## Engineering Gap / Limitation

Investigate whether a focused, document-cited conversational interface improves access to gardening guidance compared with keyword search. The prototype must preserve evidence, clarify missing conditions, and avoid unsupported answers.

## Project Objectives

- **O1:** Design the scope, source collection, and reference-answer evaluation set.
- **O2:** Develop a text-based retrieval-augmented prototype with citations and guardrails.
- **O3:** Evaluate accuracy, groundedness, citations, latency, and scope handling against a search baseline.

## Target Users

Beginner gardeners growing potted plants indoors or on balconies in tropical conditions. Initial documents are Singapore-focused; the prototype will support English questions and up to ten adequately documented houseplants.

## Data Sources

Official NParks documents, linked from its [resource directory](https://gardeningsg.nparks.gov.sg/learn-more-about-gardening/downloads/):

1. [Introduction to Indoor Gardening](https://isomer-user-content.by.gov.sg/316/5be81ffb-fd47-444d-ab81-bf46b869dd7b/introduction_to_indoor_gardening.pdf)
2. [Introduction to Community Gardening](https://isomer-user-content.by.gov.sg/316/e9f8a03b-d2aa-4f29-b16a-0678ea9ca5a9/introduction%20to%20community%20gardening.pdf)
3. [Know 10 Houseplants](https://isomer-user-content.by.gov.sg/316/43fdd8a1-d385-428f-8cc2-d5b9b36f6a38/know%2010%20house%20plants.pdf)

Links checked on 14 October 2026. Third-party gardening PDFs are not redistributed in this repository.

## Scope and Responsible AI

Focus on documented light, watering principles, growing media, and space requirements. No image diagnosis, pesticide dosages, ingestion guidance, automated watering, or safety guarantees. Proposed controls include source checks, clarification, abstention, and minimal collection of user information.

See the [full project scope](docs/week1_project_scope.md) for risks, controls, and proposed evaluation targets.

## Repository Structure

```text
docs/         Project scope, Week 1 group evidence, and submission checklist
data/         Source documentation; local source copies are ignored
src/          Future application code
notebooks/    Future Colab notebooks
evaluation/   Future evaluation questions and results
prompts/      Future versioned prompts
```

The [ChatGPT system map](docs/week1_system_map.png) and [observation sheet](docs/week1_observation_sheet.md) are Part A/B group work about an existing system. They are not PlantPal's architecture or test results. The [group reflections](docs/group_reflections.md) contain the supplied Part A and Part B reflections.

## Weekly Progress

| Week | Focus | Deliverable | Status |
|---|---|---|---|
| W1 | Project scope and repository; preserve group evidence | README, scope, observation sheet, system map | Prepared; group-evidence review and course-portal submission remain |
| W2 | Part A: framing, scope, and requirements | [Requirements specification](docs/week2_requirements.md) | Part A documented; Parts B and C pending; implementation and evaluation not started |

See [submission checklist](docs/submission_checklist.md) for remaining items. Do not commit credentials, personal conversation logs, or restricted documents.
