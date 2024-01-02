# IICONGRAPH case studies RQ
In this repository, we describe the steps to answer the research questions used to test IICONGRAPH. If necessary, the steps are accompanied by a commented Jupyter Notebook. Otherwise, SPARQL queries will be provided (they need to be run in an instance of GraphDB or Blazegraph containing, according to the RQ, IICONGRAPHwikidata or IICONGRAPHarco)

### RQ1.1 - Wikidata

**Research Question**: To what extent can linked open data be leveraged to expose serendipitous symbolic connections in Wikidata?

The steps to answer this question are explained in [RQ1_1.ipynb]().

### RQ1.2 - Wikidata

**Research question**: Which artworks emerge as being the most symbolic? (In wikidata). 

To answer this research question, we need to query IICONGRAPHwikidata and count the artworks that are linked to the most simulations. The query to perform this task is the following (selecting top 100, can be expanded or reduced):

```SPARQL
prefix sim:<https://w3id.org/simulation/ontology/> 
prefix wd:<http://www.wikidata.org/entity/> 
PREFIX icon: <https://w3id.org/icon/ontology/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
SELECT DISTINCT ?painting ?paintinglabel (count(distinct ?simulation) as ?tot) WHERE { 
?painting icon:iconographicallyDepicts ?simulation ;
          rdfs:label ?paintinglabel .
    ?simulation sim:hasSimulacrum ?anything . } GROUP BY ?painting ?paintinglabel ORDER BY DESC(?tot) LIMIT 100
```

The results of this query are available in the [rq1_2.csv]() file.

***

### RQ2.1 - Wikidata

**Research question**: How are pre-iconographic and iconographic depictions distributed across Wikidata's *depicts* statements in paintings?

To answer this questions, we have to query IICONGRAPHwikidata, counting (i) the number of elements recognized by a pre-iconographical recongition and (ii) the number of elements that recognized by an iconographical recognition (minus the automatically inferred interpretations, as they are not part of the original *depicts* statements of Wikidata).

To count the pre-iconographical elements, we use this query:

```SPARQL
PREFIX icon: <https://w3id.org/icon/ontology/>
SELECT (count(?preico) as ?tot) 
WHERE {?art icon:preiconographicallyDepicts ?preico}
```

The result is 224,981.

To count the iconographical elements, we use this other query:

```SPARQL
PREFIX icon: <https://w3id.org/icon/ontology/>
PREFIX sim: <https://w3id.org/simulation/ontology/>
SELECT (COUNT(?ico) as ?tot)
WHERE { {?artwork icon:iconographicallyDepicts ?ico .   }
    MINUS {?ico sim:hasSimulacrum ?something} }
```

***

### RQ2.2 - Wikidata

**Research Question**:Among iconographical elements, which are the main classes (characters, places, attributes) that emerge as the most frequent? (In Wikidata)

To answer this question, we count how many of the iconographical elements recognized in Wikidata are associated to one of the iconographical classes of ICON (i.e., Characters, Places, Named Objects (attributes), Events, Stories).

To do so, we perform this query in IICONGRAPHwikidata:

```SPARQL
PREFIX icon: <https://w3id.org/icon/ontology/>
PREFIX sim: <https://w3id.org/simulation/ontology/>
SELECT ?icoclass (COUNT(?icoclass) as ?tot)
WHERE { VALUES ?icoclass {icon:Character icon:NamedObject icon:Place icon:Story icon:Event}
    {?artwork icon:iconographicallyDepicts ?ico .   }
    ?ico a ?icoclass } GROUP BY ?icoclass
```

The results are available in the following table

| icoclass                                   | tot    |
|--------------------------------------------|--------|
| https://w3id.org/icon/ontology/Character   | 98,354 |
| https://w3id.org/icon/ontology/NamedObject | 791    |
| https://w3id.org/icon/ontology/Place       | 17,050 |
| https://w3id.org/icon/ontology/Story       | 3,436  |
| https://w3id.org/icon/ontology/Event       | 817    |

***

### RQ3.1 - ArCo

**Research Question**: What are the most common iconological meanings associated with Italian Billboards from the 20th century?

To answer this question, we can run this SPARQL query in IICONGRAPHarco counting the frequency of the iconological meanings (selecting top 100, can be expanded or reduced):

```SPARQL
PREFIX icon: <https://w3id.org/icon/ontology/>
PREFIX sim: <https://w3id.org/simulation/ontology/>
SELECT ?icomeaning (COUNT(?icomeaning) as ?tot)
WHERE { 
    ?art icon:iconologicallyRepresents ?icomeaning . } 
GROUP BY ?icomeaning ORDER BY DESC(?tot) LIMIT 100
```

The results of this query are available in the [rq3_1.csv]() file.


***

## References

* <a id="1">[1]</a>Baroncini, S., Sartini, B., Van Erp, M., Tomasi, F. and Gangemi, A. (2023), "Is dc:subject enough? A landscape on iconography and iconology statements of knowledge graphs in the semantic web", Journal of Documentation, Vol. 79 No. 7, pp. 115-136. https://doi.org/10.1108/JD-09-2022-0207
* <a id="2">[2]</a>Farber, M., Bartscherer, F., Menne, C. and Rettinger, A. (2018), “Linked data quality of dbpedia, freebase, opencyc, wikidata, and yago”, Semantic Web, Vol. 9 No. 1, pp. 77-129.