---
title: "Phenopacket-tools: Building and validating GA4GH Phenopackets"
description: Bioinformatics tools and examples for working with the Phenopackets standard
template: post.html 
authors:
 - '@mbaudis'
date: 2023-05-17
pdf_file_name:
links:
  - '[article at PLoS ONE](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0285433)'
  - '[Article PDF](/pdf/2023-05-17___Davis-et-al.__Phenopacket-tools--Building-and-validating-GA4GH-Phenopackets__PLoS-ONE.pdf)'
---

##### Danis D, Jacobsen JOB, Wagner AH, Groza T, Beckwith MA, Rekerle L, Carmody LC, Reese J, Hegde H, Ladewig MS, Seitz B, Munoz-Torres M, Harris NL, Rambla J, Baudis M, Mungall CJ, Haendel MA, Robinson PN. (2023) **Phenopacket-tools: Building and validating GA4GH Phenopackets.** _PLoS One._ 18:e0285433.

**Abstract** The Global Alliance for Genomics and Health (GA4GH) is a standards-setting organization that is developing a suite of coordinated standards for genomics. The GA4GH Phenopacket Schema is a standard for sharing disease and phenotype information that characterizes an individual person or biosample. The Phenopacket Schema is flexible and can represent clinical data for any kind of human disease including rare disease, complex disease, and cancer. It also allows consortia or databases to apply additional constraints to ensure uniform data collection for specific goals. We present phenopacket-tools, an open-source Java library and command-line application for construction, conversion, and validation of phenopackets. Phenopacket-tools simplifies construction of phenopackets by providing concise builders, programmatic shortcuts, and predefined building blocks (ontology classes) for concepts such as anatomical organs, age of onset, biospecimen type, and clinical modifiers.<!--more--> Phenopacket-tools can be used to validate the syntax and semantics of phenopackets as well as to assess adherence to additional user-defined requirements. The documentation includes examples showing how to use the Java library and the command-line tool to create and validate phenopackets. We demonstrate how to create, convert, and validate phenopackets using the library or the command-line application. Source code, API documentation, comprehensive user guide and a tutorial can be found at https://github.com/phenopackets/phenopacket-tools. The library can be installed from the public Maven Central artifact repository and the application is available as a standalone archive. The phenopacket-tools library helps developers implement and standardize the collection and exchange of phenotypic and other clinical data for use in phenotype-driven genomic diagnostics, translational research, and precision medicine applications.
