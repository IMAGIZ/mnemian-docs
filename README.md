## Mnemian™ Information & Documentation

This work-in-progress documentation repository explains how [**Mnemian**™](https://mnemian.net) ingests, transforms, and publishes archival metadata into a linked data<small><sup>*1</sup></small> environment ... currently based on [**Records in Contexts (RiC)**](https://www.ica.org/ica-network/expert-groups/egad/records-in-contexts-ric/).

It is aimed at technically inclined archivists, developers, and information professionals who may not be fully familiar with RiC or linked data, but are comfortable with software, systems, and data-modelling concepts.

Over time, this repository will grow to cover:
- Mnemian's technical framework and system architecture
- AI integration: Large Language Models (LLMs), prompt design, and guardrails
- Querying the linked data (RDF) endpoint using SPARQL (SPARQL Protocol and RDF Query Language), with examples
- Mnemian's API endpoints and data flows
- Plans for supporting additional archival/record data sources and linked data models

## AtoM to RiC Mapping
The `/mapping-atom-to-ric/` folder contains an overview of the current mapping methodology, and individual files detailing how we process each metadata field returned from AtoM API endpoints. 

**Please note**: These mappings are currently in a 'pre-alpha' state and may require further refinement after feedback from the community. We will continue to evolve these mappings and eventually assign them a release version number. Once released, they could be used to define a minimal RiC model ("_RiC Lite_") in other systems and will be available under a [CC-BY-4.0 license](https://creativecommons.org/licenses/by/4.0/).

## A note about retrieval from AtoM
Mnemian currently uses these existing AtoM API endpoints:
- `GET /api/informationobjects`*
- `GET /api/informationobjects/<slug>`

***Please note:** We have modified the `informationobjects` API to return the `id` and `parent_id` of each record. We have done this so that we can reconstruct the information hierarchy, and then retrieve a set of child descriptions for each top-level record by using the `id` as a filter parameter.

### Example information returned:
```json
{ "total":7,
  "results":[
    {
      "reference_code":"Ref code",
      "slug":"slug",
      "title":"Title of first record",
      "repository":"Name or Repository",
      "level_of_description":"Collection",
      "creators":["Name of creator"],
      "creation_dates":["Creation date"],
      "id":4189,
      "parent_id":1
    },
    {
      "reference_code":"Ref code",
      "slug":"slug",
      "title":"Title of second record",
      "repository":"Name or Repository",
      "level_of_description":"Collection",
      "creators":["Name of creator"],
      "creation_dates":["Creation date"],
      "id":6294,
      "parent_id":1
    }
    ...etc. 
]}
```

### New AtoM endpoints...

We have built two new API endpoints in AtoM, for `actor` and `repository` data. Links will be added here when these are published. We intend to offer these new APIs and our modification of `informationobjects` to the AtoM project for review, and inclusion in a future release.

---

<small>***1: Linked Data**: A method of publishing structured data using web standards (_Resource Description Framework - RDF_) that enables connections between related information across different sources</small>
