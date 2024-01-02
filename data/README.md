# IICONGRAPH
This repository contains the documentation about the data model and development process of IICONGRAPH.

## Data Model

IICONGRAPH mainly uses the [ICON ontology](#1) as its schema. ICON is an ontology developed to describe artistic interpretation according to the metholodology of [Panofsky](#2). According to Panofsky, an interpretation can be divided into three communicating levels. On the first level, named preiconographical, you recognize X. On the second lavel, named iconographical, you recognize y. On the third level, named iconological, you recognize z. The images below show a graphical rendering of ICON's classes and properties representing the different levels of interpretation. Table X shows which properties and class we use in ICON to describe artworks and their subjects.

## Sources

### Wikidata

[Wikidata](#3) is a collaborative knowledge base containing information about a wide range of domains. We are interested in the [painting](https://www.wikidata.org/wiki/Q3305213) domain, and we converted the statements that linked paintings to the elements they [depict](https://www.wikidata.org/wiki/Property:P180).

### ArCo

[ArCo](#4) is the Italian cultural heritage knowledge graph. We are interested in all the [Historic or Artistic properties](https://w3id.org/arco/ontology/arco/HistoricOrArtisticProperty) that have a textual description following the "Iconographic Reading" syntax (such as [this](https://dati.beniculturali.it/lodview-arco/resource/HistoricOrArtisticProperty/0500668520.html)).

The description is in Italian, and, as seen in the scripts, an automatic translation is necessary before the conversion.

### HyperReal

[HyperReal](#5) a knowledge graph of cultural symbolism. It is used in the context of IICONGRAPH to generate automatic potential symbolic interpretation. Imagine a painting depicts an apple, and an apple in HyperReal is the symbol of the original sin from a Christian point of view. The painting depicting an apple can be automatically interpreted as symbolizing the original sin. These interpretations are **creator-agnostic** and just **potential**, and should be used as a starting point for art historian to analyse the symbolism behind artworks.

## Data conversion

### Wikidata

For the data conversion of Wikidata, please refer to the jupyter notebook 

### ArCo

## Datasets characteristics

### Wikidata

### ArCo



## Final results (if you follow the ICONGRAPH1.0 steps)

## References

* <a id="1">[1]</a>
* <a id="2">[2]</a>
* <a id="3">[3]</a>
* <a id="4">[4]</a>
* <a id="5">[5]</a>