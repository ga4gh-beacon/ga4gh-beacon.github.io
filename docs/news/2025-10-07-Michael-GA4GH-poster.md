---
title: 'Implementing the GA4GH Beacon API for Genomic Discovery and Sharing in an Open Data Paradigm'
description: 'Poster at GA4GH 2025 Plenary'
template: post.html 
authors:
  - '@mbaudis'
date: 2025-10-07
pdf_file_name:
links:
  - '[poster PDF](https://baudisgroup.org/pdf/2025-10-07___Michael-Baudis-Beacon-Progenetix__GA4GH-poster.pdf)'
  - '[GA4GH plenary website](https://broadinstitute.swoogo.com/ga4gh13plenary)'
---

![GA4GH Circle Logo](https://baudisgroup.org/img/ga4gh_circle_420x420.png){ style="width: 210px; float: right; margin: -40px 0px 10px 20px;" }

**Abstract** Besides the discovery of genomic and pheno-clinic data in different access settings, the GA4GH Beacon protocol also enables the retrieval of matched records through a variety of open or protected mechanisms, depending on the resources’ data structure as well as data protection and regulatory requirements. While data discovery scenarios with limited and/or aggregated responses will constitute a large fraction of Beacon and Beacon Network scenarios, the protocol also empowers the sharing of data e.g. in open research data settings.

Since 2016 the Progenetix cancer genomics reference resource has served as a platform for the implementation driven development and testing of the Beacon protocol. <!--more-->
The current production version of Progenetix ([progenetix.org](https://progenetix.org)) provides access to curated genomic copy number profiling data from more than 240’000 individual samples, curated from reference projects such as TCGA and GENIE as well as more than 1’600 publications, as well as associated pheno-clinical data. 

The data in Progenetix as well as some other resources (e.g. cancercelllines.org) is accessible through the Beacon API (v2.n) and supports the Beacon data model as well as Beacon handover data delivery. The software ecosystem driving the Progenetix and related resources also provides additional functions for programmatic data access - e.g. the pgxRpi for interfacing Beacon resources with the R environment - as well as functionality for data ingestion and Beacon front end generation.

This presentation emphasizes the use of the Beacon protocol beyond its typical applicaion for federated data discovery and encourages the protocol’s adoption by reference resources in biomedical genomics and beyond.

