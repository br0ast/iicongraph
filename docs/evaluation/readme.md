# Evaluation of IICONGRAPH

This repository contains information about the evaluation of IICONGRAPH according to 4 out of 6 criteria defined in [1](#1). The six criteria taken from the literature are an iconographical and iconological adaptation of the criteria defined in [2](#2) and are listed below.

* Semantic Validity of Iconographical and Iconological Triples (CR1)
* **Iconographical and Iconological Column Completeness (CR2)**
* **Iconographical and Iconological Schema Granularity (CR3)**
* Interlinking of Artworks (CR4)
* **Intralinking Potential for Subject Comparisons (CR5)**
* References to External Taxonomies of Art and Culture (CR6)

Because IICONGRAPH improvements do not aim at reconciliation to taxonomies of art and culture nor to connect the same artworks in different knowledge graphs, and nor to correct wrong triples regarding iconography and iconology, only criteria 2,3,5 can be influenced.

## Measuring Iconographical and Iconological Column completeness (CR2)

First, I extracted all the iconographical and iconological triples regarding 100 artworks from each one of the IICONGRAPH versions (IICONGRAPHglobal, IICONGRAPHarco, IICONGRAPHwikidata). Then, 2 annotators indipendently annotated first the expected numbers of levels of interpretation for an artwork (generally, a landscape contains preiconographical elements, a portrait a preiconographical and an iconographical, and more complex cultural artworks can be interpreted by all the three levels of interpretations) and then the number of levels covered by IICONGRAPH (the number of expected levels could not be less then the number of levels covered by IICONGRAPH). Then I divided the number of levels covered by the numbers of levels expected. Therefore, for each artwork, there was a score of either 0 (0 levels covered, 1/2/3 expected), 0.33 (1 level covered, 3 expected), 0.5 (1 level covered, 2 expected), 0.66 (2 levels covered, 3 expected), 1 (all expected levels are covered). I then averaged the 100 artworks scores and obtain a score for a single annotator, then I averaged the scores for the two annotators. The files with the annotations for [IICONGRAPHglobal are here](), [IICONGRAPHarco are here](), and [IICONGRAPHwikidata are here]().

To extract the triples, I first loaded the graphs in a GraphDB instance and then performed the following query on all three versions of IICONGRAPH

```SPARQL
    PREFIX icon: <https://w3id.org/icon/ontology/>
    SELECT ?artwork (group_concat(distinct ?fsub;separator="|") as ?fsubs) 
                    (group_concat(distinct ?ssub;separator="|") as ?ssubs) 
                    (group_concat(distinct ?tsub;separator="|") as ?tsubs)
    WHERE { ?artwork icon:preiconographicallyDepicts ?fsub ;
            OPTIONAL {?artwork icon:iconographicallyDepicts ?ssub }
            OPTIONAL {?artwork icon:iconologicallyRepresents ?tsub } 
          } 
    GROUP BY ?artwork ORDER BY RAND() LIMIT 100 
```

## Measuring Iconographical and Iconological Schema Granularity (CR3)

As ICON ontology was developed to follow the requirements of CR3 expressed by [1](#1), the score for this category, which measures the granularity of the schema (in this case ICON ontology) in describing iconographical and iconological statements, was set as 1 for all three versions of IICONGRAPH.

## Measuring Intralinking Potential for Subject Comparisons (CR5)

To measure this criteria, I divided the number of the unique subjects that are linked to more than 1 artwork (**X**) by the total number of unique subjects in the various versions of the knowledge graph (**Y**). 
To calculate, **X**, I loaded the graphs in an instance of GraphDB and then performed this query on each one of them:

```SPARQL
PREFIX icon: <https://w3id.org/icon/ontology/>
SELECT (COUNT(distinct ?sub) as ?tot)
WHERE { FILTER (?no > 1) {
                        SELECT ?sub (COUNT(distinct ?artwork) AS ?no) 
                        WHERE { ?artwork icon:preiconographicallyDepicts|
                                         icon:iconographicallyDepicts|
                                         icon:iconologicallyRepresents ?sub 
                              } 
      					GROUP BY ?sub 
      						  }
	  }
```

To calculate **Y**, I loaded the graphs in an instance of GraphDB and then performed this query on each one of them:

```SPARQL
PREFIX icon: <https://w3id.org/icon/ontology/>
SELECT (COUNT(distinct ?sub) as ?tot)
WHERE { ?artwork icon:preiconographicallyDepicts|
                 icon:iconographicallyDepicts|
                 icon:iconologicallyRepresents ?sub 
      } 
```