---
template: news_list.html
---

# GA4GH Beacon project

!!! note "Technical Documentation"

    This website provides some general information about the GA4GH Beacon protocol. Please visit [docs.geneomebeacons.org](http://docs.genomebeacons.org) for technical and implementation details.

![Beaconize hospitals](/img/Beaconizing_hospitals_Webpage.png)
###### A schematic representation of how Beacon works. (A) Beacon API implementation and (B) A Beacon query and aggregated response

One of the main bottlenecks in human genomics research is lack of data. A Beacon is a genomics discovery tool which allows to aggregate worldwide genomics dataset through a shared query protocol. 

In order to promote personalised medicine, inclusive diagnostics, prognostic and therapeutic strategies, we cannot afford to keep the data completely "locked in". The Beacon API aims to solve this problem by enabling the search of genomic variants and associated information without jeopardising the privacy of the dataset. Any hospital or research entity can choose to 'beaconize' their omics dataset without compromising the privacy or the ownership of the dataset, thus helping the worldwide community of researchers and assisting science through the power of data.

The Beacon Project is developed under a Global Alliance for Genomics and Health (GA4GH) Initiative for the federated discovery of genomic data in biomedical research and clinical applications. 

## What is the Beacon Standard?

The Beacon protocol defines the programming interface ("API") for implementing individual beacon resources. A beacon resource uses the Beacon API usually extended with a that allows for data discovery of genomic and phenoclinic data. Originally, the Beacon protocol (versions 0 and 1) was limited to information about the presence/absence of a given, specific, genomic mutation in a set of data, from patients of a given disease or the population in general. The version 2 (v2) of the Beacon protocol has been accepted as GA4GH standard in Spring 2022 and includes, among other changes:

* Query options for biological or technical "meta"data using [**filters**](http://docs.genomebeacons.org/filters/) defined through CURIEs (e.g. phenotypes, disease codes, sex or age).
* An option to trigger the next step in the **data access** process (e.g. who to contact or which are the data use conditions).
* An option to **jump to another system** where the data could be accessed (e.g. if the Beacon is for internal use of the hospital, to provide the Id of the EHR of the patients having the mutation of interest).
* **Annotations** about the variants found, among which the expert/clinician conclusion about the pathogenicity of a given mutation in a given individual or its role in producing a given phenotype.
* Information about **cohorts**.

!!! Warn "Move to Beacon v2"

    With the release of Beacon v2 implementations of v1 and earlier are not longer supported.
    Deployers of Beacon instances or networks are advised to migrate to v2 of the
    standard. The functionality of Beacon v1 [can be easily implemented in v2](http://genomebeacons.org/FAQ/#v1-emulation). 

![Beacon v2 federation principle](/img/Beacon-graphics-v2-network-960x540.png)

!!! note "Progenetix - Example of a Beacon Implementation for Data Delivery in Oncogenomics"

    The Progenetix oncogenomic website is built on top of a Beacon v2 implementation.
    It provides an example for a data-rich resource and demonstrates Beacon queries
    beyond allele discovery, with a focus on structural genome variations. More information
    can be found at the Progenetix [documentation](https://docs.progenetix.org/) and on its [search page](https://progenetix.org/search/). 


###### Schematic example of a Beacon query

## Beacon v2 technology

The Beacon v2 is based on a two-part concept:

* The Beacon [Framework](http://docs.genomebeacons.org/framework/).
* The Beacon [Model](http://docs.genomebeacons.org/models/).

In principle, this concept allows for different Models (in other domains outside of the Beacon v2 realm, e.g. “Imaging Beacon”) to be built using the same Framework. However, in the current context of Beacon v2, we consider the two elements interdependent and likely to be updated together for subsequent major versions.

For further information please refer to the [Beacon v2 documentation](http://docs.genomebeacons.org).

## Beacon and Security

Genomics data _in principle_ may allow the re-identification of individuals in genomics data repositories which leads to a generally high level of protective measure being applied to such data. However, with the right choice of data sharing protocols, data security infrastructure and good health data practices, the sharing and discovery of genomics and related data can be possible and enable valuable insights into disease related as well as prognostic and lifestyle related  genomic variations. 

## Acknowledgements

### Beacon partners

In 2020, the GA4GH Beacon group started a set of meetings and interviews with GA4GH Driver Projects and with ELIXIR partners in order to determine the scope of the next generation Beacon. The goal was to be useful without breaking the simplicity that made Beacon version 1 successful.

Interviews were conducted with the following GA4GH Driver Projects:

* [Autism Speaks](https://www.autismspeaks.org/)
* [BRCA Exchange](https://brcaexchange.org/)
* [CanDIG](https://www.distributedgenomics.ca/)
* [European Genome-phenome Archive](https://ega-archive.org/), [European Nucleotide Archive](https://www.ebi.ac.uk/ena/browser/home), [European Vegetation Archive](http://euroveg.org/eva-database)
* [EuCanCancer](https://eucancan.com/)
* [European Joint Programme - Rare Diseases](https://www.ejprarediseases.org/)
* [H3Africa](https://h3africa.org/)
* [GEM Japan](https://www.amed.go.jp/en/aboutus/collaboration/ga4gh_gem_japan.html)
* [Genomics England](https://www.genomicsengland.co.uk/)
* [Matchmaker Exchange](https://www.matchmakerexchange.org/)
* VICC

Some ELIXIR partners were also interviewed, i.e. Café Variome, FPS, RD-Connect, CINECA, and Disgenet.
Among ELIXIR Spain TransBioNet and Bioinformatics in Barcelona members, a set of Catalan hospitals (e.g. Hospital Clinic) are exploring how to use Beacons inside their genomic diagnose teams and how to share the diagnoses between hospitals. 

### Beacon early implementers

At the time of submission at the end of 2021, five Beacons were already implemented in a Beacon Service Registry.
The "early implementers" actively participated in refining the Framework as they were responsible for spotting any issue they might encounter with the Framework or Model. 

* European Genome-Phenome Archive EGA Beacon
* Progenetix' [Beacon+](https://progenetix.org/search/)
* [Cafe Variome](https://beaconv2.cafevariome.org/form)
* Fundación Progreso y Salud's [Beacon v2 API](https://csvs-beacon.clinbioinfosspa.es/csvs/ga4ghbeacon/v2/api/)
* CNAG's [Beacon v2 API](https://playground.rd-connect.eu/beacon2/api)

## Beacon News, Events and Publications

