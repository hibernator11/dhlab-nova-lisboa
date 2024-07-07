# dhlab-nova-lisboa
Workshop for the [Digital Humanities Lab (DH_Lab)](https://dhlab.fcsh.unl.pt/about-lab_hd-fcsh/#en) associated with [NOVA-FCSH](http://www.fcsh.unl.pt/) of [Universidade NOVA de Lisboa](https://www.unl.pt/).


## Representación de las nacionalidades de los autores
El siguiente ejemplo muestra las nacionalidades de los autores de Wikidata enlazados a la Biblioteca Virtual Miguel de Cervantes. En este [enlace](https://w.wiki/88PR) se puede ejecutar la siguiente sentencia SPARQL en el editor de consultas de Wikidata.

```
#defaultView:Map
SELECT DISTINCT ?autor ?autorLabel (SAMPLE(?imagen) as ?img) ?coordenadas
WHERE {   
       ?autor wdt:P2799 ?idbvmc.
       ?autor wdt:P27 ?pais .
       ?pais wdt:P625 ?coordenadas.
       OPTIONAL {?autor wdt:P18 ?imagen .}      
    SERVICE wikibase:label { bd:serviceParam wikibase:language "es" }
} GROUP BY ?autor ?autorLabel ?coordenadas
```

<img src="https://github.com/hibernator11/hdh-compartir-pantalla-2023/raw/main/imagenes/mapa-autores.png" width="60%">
