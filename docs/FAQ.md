# Frequently Asked Questions

## Introduction to Beacon and Its Purpose

??? question "Is it `Beacon` or `beacon`?"

    The uppercase `Beacon` is used to label API, framework or protocol and their components - while lower case `beacons` are instances of these, _i.e._ individual resources using the protocol.

??? question "What types of data can be beaconized?"

    You can beaconize genomic variants, phenotypic and clinical data, which are part of the default data model. However, Beacon v2 data model is flexible allowing other structured records (_e.g._ imaging metadata) that align with Beacon v2 specification to be made discoverable as well.

??? question "Who is the Beacon v2 intended for?"

    It is designed for research institutions, hospitals, genomic data repositories, and organizations that handle large-scale biomedical data.

??? question "What is the difference between Beacon v1 and Beacon v2?"

    Beacon v1 enabled simple genomic queries with only boolean responses (yes/no). Beacon v2 expands functionality by supporting complex queries, additional data types (phenotypic, clinical, etc.), standardized authentication methods and aligns with other GA4GH standards.

??? question "Does ***beaconizing*** my data mean making it fully public?"

    No, data controllers can configure the access level to their data as being public, registered or controlled access. For more information, you can check [Beacon Security](https://docs.genomebeacons.org/security/?h=access) and [Beacon Configuration File pages](https://docs.genomebeacons.org/framework/#the-beacon-configuration-file).

    ??? question "Where can I find official documentation on Beacon?"

    You can visit the official Beacon documentation for technical specifications, guides, and examples (docs.genomebeacons.org). For implementation toolkits, please refer to the Deployment Guide page.
    
??? question "Can I contribute to the development of the Beacon v2 specification?"

    Beacon v2 is an open-source protocol and welcomes contributions from the community. Please refer to the [Beacon v2 repository](https://github.com/ga4gh-beacon/beacon-v2/) for creating any issues or discussions. Additionally, GA4GH Discovery Work Stream has established special task groups, called Beacon Scouts, that continue developing various aspects of the Beacon v2 protocol. Beacon Scouts are open to volunteer developers. Please find <a href="https://costero-e.github.io/dev-beacon-web-ana.github.io/docs/Team">further information here</a> and contact the Beacon managers upon interest.

??? question "Where to find the code for Beacon Network?"

    Beacon Network is a federated system connecting multiple Beacons for cross-institutional genomic queries. The open-source code for the Beacon Network is available on [GitHub](https://github.com/elixir-europe/beacon-network-docker).

??? question "Is Beacon v2 suitable for data analysis?"

    Beacon v2 standard is primarily intended for data discovery and delivery and has been approved as such by the GA4GH.

## Preparing Data for Beaconization

??? question "Does Beacon v2 API pre-process data?"

    No, the users are responsible for ensuring that their datasets have passed quality control checks and are informative for the community.

??? question "What data schemas does Beacon v2 support?"

     Beacon v2 supports 7 different schemas for genomic and phenotypic data by default, following GA4GH standards: Cohorts, Datasets, Runs, Analysis, Individuals, Genomic variations and Biosamples. It is not mandatory to have all schemas. However, Beacon v2 is adaptable to various data models, such as (imaging) metadata or RNA expression data (see [RNAget extension](https://github.com/guigolab/rnaget-beacon-demo)).

??? question "Which are the mandatory fields in the Beacon v2 schema?"

     The Beacon v2 specification is very permissive to allow data models of various complexity, and thus, very few fields are mandatory. As an example, the following fields are required for each entry type (information extracted in April 2025): 
      - Analyses: “id”, “analysisDate” and “pipelineName”
      - Biosamples: “id”, “biosampleStatus” and “sampleOriginType”
      - Cohorts: “id”, “name” and “cohortType”
      - Datasets: “id” and “name”
      - Individuals: “id” and “sex”
      - Runs: “id”, “biosampleId” and “runDate”
      Please see [Beacon v2 specification](https://github.com/ga4gh-beacon/beacon-v2) for more details and updates.

??? question "How are pedigrees represented in Beacon v2?"

    Pedigree structure can be defined in the _pedigree.json_ file. The pedigree can be represented either from the perspective of the proband and describing the whole pedigree structure, or from the perspective of another proband’s pedigree member and representing only the relationship to the proband. Please refer to [the documentation](https://docs.genomebeacons.org/pedigree/) for more details. 

??? question "Can I update my Beacon data after publishing?"

     Yes, you can update records data as needed while maintaining Beacon’s data access policies. The beacon doesn't need to be redeployed if only records (data) have been modified but depending on the implementation, reindexing the database might be needed (like in B2PI).

## Setting Up a Beacon Instance

??? question "Do I need a dedicated server to run a Beacon?"

     No, you can run it on local servers, cloud environments, or dedicated instances.

??? question "How do I deploy Beacon in a production environment?"

     Use the [Beacon PI version](https://github.com/EGA-archive/beacon2-pi-api), which includes optimizations for performance and security.

??? question "Does the Beacon API support cloud deployment?"

     Yes, you can deploy it on any cloud environment that supports REST API queries and allows for database integration, which is necessary for deploying a beacon.

??? question "How do I validate that my Beacon is compliant with the Beacon v2 specification?"

     You can use the [Beacon Verifier v2](https://beacon-verifier-demo.ega-archive.org/) tool to check data structure and compliance before deployment. However, Verifier v2 only checks the framework and the data model format, but not the semantics of each field. In other words, it does not validate the content of the data records.

??? question "How do I emulate Beacon v1 while supporting the v2 protocol?<a id="v1-emulation"> </a>" 

    The Beacon Framework describes the overall structure of the API requests, responses, parameters etc. One can implement e.g. a Boolean beacon (_cf._ the original protocol) without any use of the model, just by providing a well-formed JSON response upon a request [very similar to the (pre-)v1 allele request](/variant-queries/#beacon-sequence-queries).

    ##### Minimal Example Request

    This example is for a minimal SNV-type variant query.

    ```
    /beacon/g_variants/?referenceName=refseq:NC_000017.11&start=7577120&referenceBases=G&alternateBases=A
    ```

    ##### Example Boolean Response

    In this minimal response to the query above, the beacon indicates that its default response is Boolean and that it could interpret it against the `genomicVariant` entity and in the context of the same Beacon version.

    In principle, one could launch a Beacon instance using the example response document as a template in whatever server environment one has at hand. However, a proper Beacon v2 installation also has to provide informational endpoints (`/info`, `/map` ...) to allow its integration through [aggregators](/networks/).

    ```json
    {
      "meta": {
        "apiVersion": "v2.0.0",
        "beaconId": "org.progenetix.beacon",
        "receivedRequestSummary": {
          "apiVersion": "v2.0.0",
          "pagination": {
            "limit": 2000,
            "skip": 0
          },
          "requestedGranularity": "boolean",
          "requestedSchemas": [
            {
              "entityType": "genomicVariant",
              "schema": "https://progenetix.org/services/schemas/genomicVariant/"
            }
          ],
          "requestParameters": {
            "alternateBases": "A",
            "referenceBases": "G",
            "referenceName": "refseq:NC_000017.11",
            "start": [
              7577120
            ]
          }
        },
        "returnedGranularity": "boolean",
        "returnedSchemas": [
          {
            "entityType": "genomicVariant",
            "schema": "https://progenetix.org/services/schemas/genomicVariant/"
          }
        ]
      },
      "responseSummary": {
        "exists": true
      }
    }
    ```

??? question "How do I report a bug in the Beacon software?"

    Submit an issue on the [Beacon GitHub repository](https://github.com/ga4gh-beacon/beacon-v2).

## Querying Data in a Beacon

??? question "What types of queries can I run on a Beacon?"

      - Variant queries (genomic variant presence)
      - Data queries (phenotypic, clinical data)
      - Complex queries (combining multiple filters)

??? question "What types of genomic variants are supported in Beacon queries?"

    Beacon v2.0 does not provide a mechanism to detect what types of genomic variant queries are supported by a given instance.

    Beacon had been originally designed to handle the "simplest" type of genomic variant queries in which a position, alternateBases (i.e. one or more base sequence of the variant at the position) and - sometimes optional - the reference sequence at this position (necessary e.g. for small deletions).

    Beacon v1.1 in principle supported "bracketed" queries and a variantType parameter (pointing to the VCF use) - see the [current documentation](https://docs.genomebeacons.org/variant-queries/#beacon-bracket-queries)  for details. However, the support & interpretation was - and still is (2022-12-13) - left to implementers. Similar for [Beacon Range Queries](https://docs.genomebeacons.org/variant-queries/#beacon-range-queries).
    
    However, the [Beacon documentation](https://docs.genomebeacons.org/variant-queries/#varianttype-parameter-interpretation) provides information about use and expected interpretation of variantType values, specifically for copy number variations.

??? question "How can I add e.g. an age limit to a query for a disease?"

    Ages are queried as [ISO8601](https://genomestandards.org/standards/dates-times/#durations) durations such as P65Y (i.e. 65 years) with a comparator (=, <=, > ...). However, the value needs an indication of what the duration refers to and resources may provide different ways to indicate this (as then shown in their /filtering_terms) endpoint).
    
    We recommend that all Beacon instances that support age queries support at minimum the syntax of age:<=P65Y and map such values to the internal datapoint most relevant for the resource's context (in most cases probably corresponding to "age at diagnosis").
    
    However, different scenarios may be supported (e.g. EFO_0005056:<=P1Y6M for an "age at death" scenario).

??? question "How can I handle haplotype queries & representation in Beacon v2?"

      - *Queries*: The Beacon framework currently (v2.0 and earlier) considers genomic variants to be allelic and does not support the query for multiple alleles or "haplotype shorthand expressions" (e.g. C,T).
      - *Workarounds*: In case of a specific need for haplotype queries implementers of a given beacon with control of its data content in principle can extend their query model to support shorthand haplotype expressions, as long as they support the standard format, too. However, such an approach may be superseded or in conflict with future direct protocol support. An approach in line with the current protocol would be to query for one allelic variant with a record-level genomicVariation response, and then query the retrieved variants individually by their id in combination with the second allele.
      - *Variant representation*: As with queries, the Beacon "legacy" format does not support haplotype representation but would represent each allelic variation separately. The same is true for the VRSified variant representation, which for v2.0 corresponds to VRS v1.2. However, draft versions of the VRS standard (will) address haplotype and genotype representations and will be adopted by Beacon v2.n after reaching a release state.

??? question "Can I use a graphical user interface to query a Beacon??"

    Yes, the Beacon v2 Reference and Production Implementations include a graphical user interface (UI) that allows users to query data   without  needing to use a terminal or console. The UI simplifies the process, so users don’t need to be familiar with the structure of [Beacon v2 queries](https://b2ri-documentation-demo.ega-archive.org/deployment).
   
??? question "What response types does Beacon provide?"

      - Boolean (Yes/No).
      - Count (number of matches).
      - Detailed JSON output.
      
??? question "How to respond if the filter hasn't been implemented?"

    A filter which does not exist should lead to "no match" response. There is no dedicated mechanism to disambiguate between a "the filter is understood, but there is no hit for this particular query" in contrast to "no idea what this filter value means". However, the /filtering_terms endpoint should provide all supported filters and this can be used to check the two possibilities if needed.

??? question "How to respond if the filter target has incomplete values?"

    For sparse data (e.g. a value being available only for a subset of samples; think about "genetic sex" not being available or disclosed in a subset of individuals), normally only the positive matches would be returned. Evaluation if what the base of these numbers would be can be achieved through discretionary queries (i.e. evaluating the alternative options) or through additional informational responses (e.g. adding the overall observation count of a filter value to the objects in the /filtering_terms response or aggregate information to a dataset response).

??? question "Does the Beacon protocol support Boolean expressions?"

    No (...but). Beacon queries as of v2 always assume a logical AND between query parameters and individual filters, i.e. all conditions have to be met. There is currently no support for Boolean expressions. However, a logical exception is the use of multiple filters for the same parameter, which a Beacon implementation should treat as a logical OR since they otherwise would fail in most instances. E.g. the query using NCIT:C3493 and NCIT:C2926 (mapped against biosample.histological_diagnosis.id) would match both Lung Non-Small Cell Carcinoma (NCIT:C2926) and Lung Squamous Cell Carcinoma (NCIT:C3493), which are exclusive diagnoses.

??? question "My queries return “No”, even when data exists. Why?"

    There might be various reasons. Please ensure the beacon is correctly configured, the data is available for querying, and it is properly indexed, and the queries match the schema format.

??? question "Why is my Beacon running slow?"

    Please make sure the implementation is developed using good standards and practices. If using a Reference/Production Implementation, then please make sure the server has enough memory and free CPU for optimized speed. Also, check the indexing of the database.

## Security, Data Privacy & Usage Policies

??? question "What are the general security principles for Beacon?"

    An implementation of a Beacon must implement the Global Alliance for Genomics and Health ([GA4GH](https://www.ga4gh.org)) Beacon standard. The V2 standard has been approved by both the Regulatory and Ethics, and Data Security foundational workstreams.

    The Beacon uses a [3-tiered access model - anonymous, registered, and controlled access](http://docs.genomebeacons.org/security/):

    * A Beacon that supports anonymous access responds to queries irrespective of the source of the query.
    * For a Beacon to respond to a query at the registered tier, the user must identify themselves to the Beacon, for example by using an ELIXIR identity.
    * For a Beacon to respond to a controlled access query, the user must have applied for, and been granted access to, the Beacon (or data derived from one or more individuals within the Beacon) before sending the query. 

    Note that a Beacon may contain datasets (or collections of individuals) whose data is only accessible at specified tiers within the Beacon. This tiered access model allows the owner or controller of a Beacon to determine which responses are returned to whom depending on the query and the user who is making the request, for example to ensure the response respects the consent under which the data were collected. The ELIXIR Beacon network supports Beacons which respond at different tiers, for example only Beacons which have a response to anonymous queries need respond to an anonymous request. 

    As part of the ELIXIR 2019-21 Beacon Network Implementation Study deliverable [D3.3](https://docs.google.com/document/d/1q7XuUB-Z4A_DogWT1AVrvkp_qHWWtbbICxokHup_tts/edit?tab=t.0) a document has been written to describe security best practice for users interested in deploying or running a Beacon or users who govern data hosted within a Beacon, and the requirements for adding the Beacon to the ELIXIR Beacon network. As the Beacon standard extends in V2 towards supporting phenotype and range queries, the tiered access model becomes more important to ensure the Beacon response is appropriate to the underlying data.

??? security "How is security actually implemented when I deploy a Beacon?"

    Security attributes are part of the Beacon v2 [Framework](https://github.com/ga4gh-beacon/beacon-v2/tree/main/framework). The file `beaconConfiguration.json` defines the schema of the JSON file that includes core aspects of a Beacon instance configuration. Its third section, called **securityAttributes**, defines the security.

    Check out the **securityAttributes** section on the [Beacon Documentation website](http://docs.genomebeacons.org/framework/#the-beacon-configuration-file).

??? question "How does the Beacon maintain privacy and security?"

    The Beacon v2 protocol mandates the use of HTTPS (encryption) and allows user-defined securityLevels (public, registered or controlled) and response granularities (boolean, count, record).

??? question "Can I revoke access from certain users or organizations?"

    Yes, user permissions can be updated or revoked at any time.

??? security "How do I test a Beacon without having to go through complex security matters (yet)?"

    As a Beacon is designed to support data discoverability of controlled access datasets, it is recommended that synthetic or artificial data is used for testing and initial deployment of Beacon instances. The use of synthetic data for testing is important in that it ensures that the full functionality of a Beacon can be tested and / or demonstrated without risk of exposing data from individuals. In addition to testing or demonstrating a deployment, synthetic data should be used for development, for example adding new features. Additionally, these data can also be used to demonstrate the access levels and data governance procedures for loading data to a Beacon to build trust with data controllers or data access committees who may be considering loading data to a Beacon. An example dataset that contains chromosome specific vcf files is hosted at EGA under dataset accession EGAD00001006673. While this dataset requires a user to log in to get access, the EGA test user can access this dataset.

    ??? question "What authentication methods are available?"

    * OIDC-based login (LifeScience, Keycloak, etc.)
    * OAuth2 tokens for API access.

??? question "Can I allow anonymous access but restrict sensitive queries?"

    Yes, by defining public, registered and controlled access endpoints, and by configuring dataset/endpoint to return boolean/count response granularity.
