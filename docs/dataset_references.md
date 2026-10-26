# PlantPal - Dataset and Data-Source References

**Research date:** 26 October 2026  
**Status:** Reference shortlist from web research. No datasets have been downloaded, ingested, or evaluated for PlantPal. Listing a source here does not add it to the approved answer corpus.

## Purpose

Keep the plant-care sources and related research found during project planning in one place. PlantPal's current scope is English, text-based guidance for beginner tropical indoor and balcony gardeners, initially covering up to ten adequately documented houseplants.

The existing NParks candidate corpus remains defined in the [project scope](week1_project_scope.md#data-sources) and [requirements](week2_requirements.md). The additional sources below are candidates for later review.

## Source Shortlist

| Source | Contents described by its publisher or authors | Potential role in PlantPal | Current assessment |
|---|---|---|---|
| [NParks gardening guides](https://gardeningsg.nparks.gov.sg/learn-more-about-gardening/downloads/) | Official gardening documents, including introductory indoor-gardening guidance. | Primary retrieval corpus with document and page citations. | Best starting point for the existing V1 plan; verify relevant passages and plant coverage before ingestion. |
| [Indoor Plants Dataset](https://zenodo.org/records/6984514) | Indoor-plant data covering light, temperature, relative humidity, watering, soil mix, and general care. The record provides a downloadable archive. | Structured plant profiles and supporting metadata. | Candidate supplement; record-level accuracy, tropical relevance, and reuse terms need review. |
| [Plantational / EcoSage](https://github.com/mohit2b/EcoSage) | Around 1,000 plant-care dialogues created from Reddit and Houzz posts; annotations include intents and dialogue acts, with original post links and image links where present. | Related work, realistic question ideas, and conversation design. | Community-derived dialogue is not automatically authoritative care evidence or a valid reference answer. |
| [Plantfolio Common Plants](https://github.com/Luminoid/plantfolio-common-plants) | The repository describes 952 houseplants and garden plants in JSON, including watering intervals, light, humidity, temperature, and other attributes. | Structured lookup experiments and prototype plant profiles. | The authors state that it is not maintained by horticultural or botanical professionals. Verify care claims against approved references. |
| [1001 Garden Plants in Singapore](https://gardeningsg.nparks.gov.sg/learn-more-about-gardening/1001-book/) | NParks compendium featuring over 2,700 plants across three volumes, with photographs, names, and care requirements represented by pictorial symbols. | Possible expansion of tropical species coverage. | Review only relevant species initially. Extraction must preserve and correctly interpret care symbols, rather than rely on plain-text extraction alone. |

Counts and descriptions reflect the source pages reviewed on the research date and may change.

## Access and Provenance Notes

### 1. NParks gardening guides

- [Introduction to Indoor Gardening](https://isomer-user-content.by.gov.sg/316/5be81ffb-fd47-444d-ab81-bf46b869dd7b/introduction_to_indoor_gardening.pdf)
- [Introduction to Community Gardening](https://isomer-user-content.by.gov.sg/316/e9f8a03b-d2aa-4f29-b16a-0678ea9ca5a9/introduction%20to%20community%20gardening.pdf)
- [Know 10 Houseplants](https://isomer-user-content.by.gov.sg/316/43fdd8a1-d385-428f-8cc2-d5b9b36f6a38/know%2010%20house%20plants.pdf)

These are the existing candidate documents. Retain title, publisher, URL, access date, version/checksum, and PDF page identifiers. Review applicable processing and redistribution terms before acquiring or publishing copies.

### 2. Indoor Plants Dataset

- Dataset record and archive: https://zenodo.org/records/6984514
- DOI: https://doi.org/10.5281/zenodo.6984514
- Related repository linked by the Zenodo record: https://github.com/biologiste95/plant-dataset/tree/plantDataSet
- Additional relevant repository inspected: https://github.com/anassdrs/indoorPlantsDataSet

The latter repository includes an Excel dataset, but equivalence with the Zenodo release has not been established. The Zenodo page's extracted text did not clearly identify its licence; confirm the exact release's terms before adoption. No record-level quality audit has been performed.

### 3. Plantational / EcoSage

- Authors' repository: https://github.com/mohit2b/EcoSage
- Research paper: https://arxiv.org/abs/2401.06807
- Dataset spreadsheet linked by the authors: https://docs.google.com/spreadsheets/d/1wJjnk4WKmtW6nqo8xcblFH-8zmFrhwCY2QkExoNgXjM/edit?usp=sharing

The repository README and sample-directory listing were inspected; access to the full spreadsheet and its contents has not been verified. The repository displays an MIT licence, but dataset-specific and underlying post/image reuse terms still need checking.

**Related-work reference:** Tomar, M., Tiwari, A., Saha, T., Jha, P., and Saha, S. (2024). *An EcoSage Assistant: Towards Building A Multimodal Plant Care Dialogue Assistant*. European Conference on Information Retrieval, pp. 318-332. https://doi.org/10.1007/978-3-031-56060-6_21

EcoSage is directly relevant prior work on plant-care dialogue. PlantPal's proposed distinction is its narrow tropical scope and document/page-grounded answers; this is a project direction, not a demonstrated novelty or performance advantage.

### 4. Plantfolio Common Plants

- Repository and documentation: https://github.com/Luminoid/plantfolio-common-plants
- English merged JSON: https://github.com/Luminoid/plantfolio-common-plants/blob/main/dist/common_plants.json
- Licence: **CC BY-NC-SA 4.0**, as stated in the repository.

The repository warns of possible inaccuracies and omissions. Fixed watering intervals must not override PlantPal's requirement to consider growing conditions and avoid unsupported schedules. Toxicity fields do not expand V1 into ingestion or pet-safety guidance.

### 5. 1001 Garden Plants in Singapore

- Official landing page and volume downloads: https://gardeningsg.nparks.gov.sg/learn-more-about-gardening/1001-book/

The three volumes cover succulents/aquatic plants/orchids; climbers/shrubs/groundcovers; and trees/palms/cycads. The title does not indicate the current number of entries. Public download availability does not establish permission to redistribute the PDFs.

## Recommended Use for V1

1. Start with the existing NParks guides and inspect coverage before finalising the supported plant list.
2. Use Plantational for related work and question ideas. Independently annotate evaluation answers against approved documents; keep development examples separate from final tests.
3. Consider structured datasets only where they add verified information missing from the initial corpus. Adding a source requires updating the source register and evaluation annotations.
4. Review relevant compendium entries if the introductory guides lack sufficient species-level evidence.

A retrieval-augmented prototype can begin with a small, reliable document collection; these sources do not require PlantPal to train or fine-tune a model.

## Review Before Admission

For each selected source, record the exact release/access date, provenance, permitted use, checksum where applicable, supported plants/topics/climate, and evidence identifiers. Check a sample of claims against their original references. For document sources preserve pages; for structured sources preserve record IDs and claim-level provenance, and update citation requirements if the approved format changes.

This document records research and recommendations only. User-needs findings, source ingestion, and measured system performance remain pending.
