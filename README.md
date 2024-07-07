# dhlab-nova-lisboa
This project was originally created for a workshop for the [Digital Humanities Lab (DH_Lab)](https://dhlab.fcsh.unl.pt/about-lab_hd-fcsh/#en) associated with [NOVA-FCSH](http://www.fcsh.unl.pt/) of [Universidade NOVA de Lisboa](https://www.unl.pt/).

<img src="logos.png">

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
