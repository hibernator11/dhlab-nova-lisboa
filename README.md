# dhlab-nova-lisboa

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/hibernator11/dhlab-nova-lisboa/HEAD)

This project was originally created for a workshop for the [Digital Humanities Lab (DH_Lab)](https://dhlab.fcsh.unl.pt/about-lab_hd-fcsh/#en) associated with [NOVA-FCSH](http://www.fcsh.unl.pt/) of [Universidade NOVA de Lisboa](https://www.unl.pt/).

<img src="logos.png">

This project provide several examples of reuse based on different techniques such as Information Retrieval, Data Visualisation or Natural Language Processing.

## Map representing the nationalities of the authors included in the Biblioteca Virtual Miguel de Cervantes
This example is based on the [Linked Open Data version of the Biblioteca Virtual Miguel de Cervantes catalogue](https://data.cervantesvirtual.com/datos-enlazados). The data is enriched with Wikidata, enabling the creation of visualisations using the Wikidata SPARQL endpoint. The SPARQL query can be executed in this [link](https://w.wiki/9FwJ).

```
#defaultView:Map
SELECT DISTINCT ?author ?authorLabel (SAMPLE(?image) as ?img) ?coord
WHERE {   
       ?author wdt:P2799 ?idbvmc.
       ?author wdt:P27 ?country .
       ?country wdt:P625 ?coord.
       OPTIONAL {?author wdt:P18 ?image .}      
    SERVICE wikibase:label { bd:serviceParam wikibase:language "es" }
} GROUP BY ?author ?authorLabel ?coord
```

<img src="https://github.com/hibernator11/hdh-compartir-pantalla-2023/raw/main/imagenes/mapa-autores.png" width="60%">

## Members of the International GLAM Labs Community
The information about the International GLAM Labs Community is stored in Wikidata as can be shown at this [map](https://glamlabs.io/member-map/). Each member is described by means of an entity in Wikidata, including a property ["member of"](https://www.wikidata.org/wiki/Property:P463) and using as value the identifier of the International GLAM Labs Community [Q72936141](https://www.wikidata.org/wiki/Q72936141).

```
#defaultView:Map
SELECT distinct (SAMPLE(?image) as ?imageu) (SAMPLE(?logo) as ?logou) (SAMPLE(?provinceLabel) as ?prov)  (SAMPLE(?website) as ?websiteu)
(SAMPLE(?location) as ?locationu) ?glamlab ?glamlabLabel
WHERE {   
       ?glamlab wdt:P463 wd:Q72936141. 
        OPTIONAL {?glamlab wdt:P625 ?location.} # coordinates     
        OPTIONAL {?glamlab wdt:P159 ?headquarters. ?headquarters wdt:P625 ?location.}
        OPTIONAL {?glamlab wdt:P131 ?province.}     
        OPTIONAL {?glamlab wdt:P18 ?image .}      
        OPTIONAL {?glamlab wdt:P154 ?logo .}      
        OPTIONAL {?glamlab wdt:P856 ?website .}  
          
    SERVICE wikibase:label { bd:serviceParam wikibase:language "en" }
} GROUP BY ?glamlab ?glamlabLabel
```

<img src="imagenes/mapa-glamlabs.png" width="60%">

## Federated queries
SPARQL enables the use of federated queries to search across several repositories. See, for example, the following example that retrieves the works included in the Biblioteca Virtual Miguel de Cervantes of the author Lope de Vega (wd:Q165257).

```
SELECT ?workLabel WHERE {
  wd:Q165257 wdt:P2799 ?id 
  BIND(uri(concat("https://data.cervantesvirtual.com/person/", ?id)) as ?bvmcID) 
  SERVICE <http://data.cervantesvirtual.com/openrdf-sesame/repositories/data> {
    ?bvmcID <http://rdaregistry.info/Elements/a/authorOf> ?work .
    ?work rdfs:label ?workLabel        
  }
}
```


## References

- Candela, G. Towards a semantic approach in GLAM Labs: The case of the Data Foundry at the National Library of Scotland. Journal of Information Science. Just Accepted (2023). https://doi.org/10.1177/01655515231174386
- Candela, G. An automatic data quality approach to assess semantic data from cultural heritage institutions. J. Assoc. Inf. Sci. Technol. 74(7): 866-878 (2023). https://doi.org/10.1002/asi.24761
- Candela, G., Pereda, J., Sáez, D., Escobar, P. Sánchez, A., Villa-Torres, A., Palacios, A., McDonough, K. y Murrieta-Flores, P. 2023. An ontological approach for unlocking the Colonial Archive. J. Comput. Cult. Herit. Just Accepted (April 2023). https://doi.org/10.1145/3594727
- Chambers, S. et al. (2023). Position Statements -> Collections as Data: State of the field and future directions (Version 1). Zenodo. https://doi.org/10.5281/zenodo.7897735
- Candela, G., Chambers,S., & Sherratt, T. (2023). An approach to assess the quality of Jupyter projects published by GLAM institutions. Journal of the Association for Information Science and Technology, 1–15. https://doi.org/10.1002/asi.24835
