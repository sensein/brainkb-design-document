# BrainyPedia Design Document
**Author:** Tek Raj Chhetri | <tekraj@mit.edu>

## Overview
_BrainyPedia serves as a knowledge base platform that provides scientists worldwide with tools for searching, exploring, and visualizing Neuroscience knowledge represented by knowledge graphs (KGs)_. Moreover, BrainyPedia provides cutting-edge tools that enable scientists to contribute new information (or knowledge) to the platform, ensuring it remains the go-to destination for all neuroscience-related research needs.

The main objective of BrainyPedia is to represent Neuroscience knowledge as a knowledge graph such that it can be used for different downstream tasks, such as making predictions and new inferences in addition to querying and viewing information.  The expected outcome of the BrainyPedia includes the following:

- (Semi-)Automated extraction of Neuroscience knowledge from structured, semi-structured, and unstructured sources, representing the extracted knowledge via KGs.
 
- Visualization of the KGs.

- Provides features to perform different analytics operations over the BrainyPedia KGs.
- (Semi-)automatically validates (e.g., quality) the extracted KGs to ensure that the BrainyPedia KGs are high quality. 
- Provides the ability to ingest data in batch or streaming mode for the automated extraction of KGs.

## Why BrainyPedia?
- **Limited Availability of Platforms for Integrating Neuroscience Data into Knowledge Graphs:** In fields such as biomedicine, many platforms exist, such as, [SPOKE](https://doi.org/10.1093/bioinformatics/btad080) and [CIViC](https://civicdb.org/welcome). <span style="color: red;">However, such resources are comparatively limited in the domain of neuroscience.</span> [LinkRBrain](https://doi.org/10.1016/j.jneumeth.2014.12.008), a web-based platform that integrates anatomical, functional, and genetic knowledge, is among the limited number of such resources. [BrainKnow](http://www.brain-knowledge-engine.org/), the most recent platform, is another platform that is designed to [synthesizes and integrates neuroscience knowledge from scientific literature](https://arxiv.org/pdf/2403.04346.pdf). Additionally, projects like [DANDI](https://dandiarchive.org/) are making strides by enabling sharing of neurophysiology data together with its metadata. 

- **Lack of Support for Heterogeneous Data Sources:** The current platforms in neuroscience are limited in their ability to handle a diverse range of data sources. For instance, [LinkRBrain](https://doi.org/10.1016/j.jneumeth.2014.12.008) can only integrate knowledge from 41 databases, whereas [BrainKnow](http://www.brain-knowledge-engine.org/) solely focuses on scientific literature. <span style="color: red;">However, knowledge is not restricted to just databases or scientific literature, and there is a need for platforms that can accommodate a wider variety of sources (e.g., structured, semi-structured and unstructured sources).</span>


## Principles

### Data Ingestion
BrainyPedia will support the data from various sources in different formats  (e.g., texts, JSON (JavaScript Object Notation)) for knowledge extraction via the BrainyPedia user interface (UI) and the API endpoints. Both batch and streaming data ingestion modes will be supported.
 

### Schema Flexibility
KGs evolve over time. For example, if we consider the case of the president of a country, it changes overtime. The KGs storing the storing the information regarding the president of the country has to be updated accordingly. Similar is the case for the neuroscience or any other domain. The knowledge may change over time based on new research findings, thereby making previous knowledge obsolete or factually incorrect. Additionally, changes might also occur in the case of schema, such as due to the standardization or alignment or updates.  While the need to change the schema, for example, does not always occur, the schema changes may be required to accommodate the new knowledge. Therefore, BrainyPedia will support this evolution by allowing the addition (or removal) of entities and relationships (or new knowledge).

### Maintainability
BrainyPedia shall be maintainable, allowing operations such as KG enrichment and validation to be performed easily.

### Curation
BrainyPedia will allow the community-driven curation of the KGs as well as (semi-) automated extraction and construction of KGs from external sources, e.g, scientific literatures.

### Accuracy, Completeness and Consistency (ACC)
BrainyPedia shall ensure the accuracy of the knowledge for which multi-step (semi-) automated validations will be performed. Additionally, checks will also be performed to ensure that the KG triples are complete, i.e., the mandatory information is present. Further to accuracy and completeness, BrainyPedia shall ensure that adding the new facts (or KG triples) will not lead to inconsistency (see figure below) with existing knowledge due to factual errors, data inconsistencies, and incompleteness.

![](acc.png)

_Figure 1: KGs. The image on the left shows the original knowledge graph, while the image on the right demonstrates the updated knowledge graph. The green highlighted box indicates new knowledge that has been added, while the red highlighted box indicates any inconsistencies caused by factual changes._

The ACC process will ensure human-centricity is maintained alongside automated validation.

### Provenance
To enable trust, the provenance, such as the source of the information and the curators (in the case of manual) of all the information, shall be maintained. The provenance conflict resolution mechanism will also be implemented to ensure the accuracy of the provenance information.

### Querying and Reasoning
BrainyPedia shall support the KGs' querying and reasoning. It shall also support other downstream analytics tasks, such as link predictions using machine learning techniques.

### Integration and Interoperability
To ensure interoperability and ease of integration, BrainyPedia will focus on using standardized ontologies or schemas. However, not all standardized ontologies or schemas are available. In such cases, other schemas or ontologies must be used. To ensure the interoperability, the alignment will be performed where necessary.

### Minimize Cognitive Burden and Data Fatigue
As BrainyPedia will also provide features to perform the analytics operation in addition to querying the information (or knowledge), a special emphasis shall be placed on ensuring that the information presented to the user does not cause a cognitive burden and data fatigue.  For example, the figure below (left) places more cognitive burden than on the right.

## Other considerations

__Assumption:__ We operate on open-world assumptions (OWA), not closed-world assumptions (CSA). In OWA, we do not make any assumptions about the absence of statements, while in CSA absence of statements would be evaluated as false, i.e., assumed to be false.

## Architecture
The figure below shows the high-level overview of the components of the BrainyPedia architecture.

__Application:__ The application (or the application layer) is the go-to point that provides access to BrainyPedia, such as via UI.

__Service:__ The service layer implements the core logic and is broken down into multiple services based on the functionalities. Furthermore, the services are divided into two layers, layer 1 and layer 2 as indicated by L1 and L2 in the figure below. This is to distinguish what will be exposed to the outside world. The L1 services will expose the API endpoints for external integration while the L2 services will not. L2 services interact with L1 services only. 

__Resource:__ The resource will provide the necessary computational resources that are required to deliver the required service by BrainyPedia.

![](initial-arch.png)

## Use cases

- **Knowledge Extraction and Integration:** BrainyPedia extracts knowledge from diverse sources, such as projects and lab meetings, and formats (scientific literature, databases, text, and JSON) into unified KG representation, offering a comprehensive and integrated view of neuroscience knowledge. For example, projects like [DANDI:](https://www.dandiarchive.org/), [BICAN:](https://www.portal.brain-bican.org/), [NeuroLex](https://scicrunch.org/scicrunch/interlex/dashboard) and [ReproNim:](https://www.repronim.org/) store vast amounts of neuroscience knowledge; integrating all the knowledge into a single platform will not only provide an integrated view but also enable new knowledge discovery.

- **Visualization & Analytics:**
- 

## Schema

## Usage Scenario
**Actor:** A

**Role:** Neuroscientists/Researcher

**Task:** Actor A wants to know if they can gain new insights from their newly collected neuroscience data.

**Precondition:** The dataset is usable, i.e., is not corrupted and is related to the neuroscience domain.

**Flow:**

1. Actor A uploads the data into the BrainyPedia platform through the BrainyPedia UI (User Interface).
2. BrainyPedia, the system, then analyzes data. If any error, e.g., unsupported file format, it will return the error; otherwise, the system will proceed to the next step of knowledge extraction.
3. The system will perform the knowledge extraction, validation, and alignment operation. If the validation or the alignment issue cannot be resolved automatically, the extracted knowledge represented via KG is flagged for expert review. Upon the successful review, the KGs are integrated (or stored) in the BrainyPedia storage and is available for visualization and analysis.

**Postcondition:** Actor A discovers new insights through the integration of diverse knowledge sources represented in BrainyPedia's KGs.


## Sequence diagram

The sequence diagram below shows the interactions between different service components for the KG construction.


```mermaid
sequenceDiagram
    autonumber

    participant User
    participant UI
    participant KG_Construction as (Semi-) structured KG construction
    participant Mapping as Mapping & Annotation
    participant Alignment as Alignment & resolution
    participant Validation as Validation & Quality assurance
    participant Expert
    participant Triplestore
    User->>+ UI: Upload CSV
    UI->>+KG_Construction: Return response
    KG_Construction->>+KG_Construction: Perform initial check, e.g., presence of required columns

    alt is invalid
        KG_Construction-->>+UI: Return Error message
        UI-->>+User: Return Error message
    else is valid
        KG_Construction->>+ Mapping: Perform mapping & annotation as necessary
        Mapping->>+ Validation: Perform validation of KG triples
        Validation->>+Validation: Validation checks, e.g., SHACL, provenance conflict
        Validation->>+ Alignment: Resolve conflicts
        alt conflict identified, perform resolution
            Alignment->>+ Alignment: Perform automated conflict resolution and alignment operation
            Alignment-->>+ Validation: Return response (triples with resolved conflicts)
            

        else conflict identified, perform resolution-requires human oversight
            Alignment->>+ Expert: Send to expert for manual conflict resolution
            Expert-->>+Alignment: Return response (triples with resolved conflicts)
            Alignment-->>+ Validation: Return response (triples with resolved conflicts) 
            
        end 
            Validation-->>+ Mapping: Return response (validated and conflict resolved KG triples)
            Mapping-->>+ KG_Construction: Updated KG triples
            KG_Construction->>+Triplestore: Store KG in database
            Triplestore-->>+KG_Construction: Return acknowledgement
            KG_Construction-->>+UI: Return response (operation status notification)
            UI-->>+User:Send notification
    end
```

## Timelines 

| Date       | Event                          |
|------------|--------------------------------|
| 2024-03-26 | Project Conceptualization      |
| 2024-04-05 | Initial Architecture Design Phase Completed |
| 2024-04-23 | Work on Design Document      |
| 2024-04-25 | Development Phase Started      |
| 2024-05-25 | First version of BrainyPedia   |
| 2024-12-25 | Second version of BrainyPedia  |
| 2025-04-10 | First complete version of BrainyPedia with all conceptualized features                |


