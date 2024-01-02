# IICONGRAPH
This repository contains the development, documentation, and case study analysis of IICONGRAPH. IICONGRAPH is a knowledge graph developed by re-engineering selected iconographic and iconological statements from [ArCo](http://wit.istc.cnr.it/arco) and [Wikidata](https://www.wikidata.org).


The catalogue metadata is available in turtle following the [DCAT Standard](https://www.w3.org/TR/vocab-dcat-3/) in [\data](data) folder.

The whole knowledge graph is available in zenodo (data dump) through this DOI: [10.5281/zenodo.10294588](https://zenodo.org/doi/10.5281/zenodo.10294588).

The [\docs](docs) folder contains the metadata schema behind IICONGRAPH, and the scripts used to extract, enrich and convert the data are available in documented jupyter notebooks.

The [\casestudies](casestudies) folder contains some research questions related to IICONGRAPH and the scripts and SPARQL queries used to answer them.

**Important**: in order to follow the steps of the documentation it is necessary to have an instance of Python 3 installed in your machine (some steps are also possible via Google Colab, might be a slower process), and also one software between [Blazegraph](https://blazegraph.com/) or [GraphDB](https://graphdb.ontotext.com/) (it might be possible with other triplestore softwares, but the scripts were only tested using these two).

The person responsible for the maintainance of this repository is:

Dr. Bruno Sartini <br>
b.sartini@lmu.de <br>
Akademischer Rat @ Institute for Digital Cultural Heritage Studies, Ludwig-Maximilians-Universität München
