## Exo sur Monet

Afficher juste les peintures de Monet 

```
SELECT DISTINCT ?peinture WHERE {
    ?peinture wdt:P31 wd:Q3305213 ; # C'est une peinture
          wdt:P170 wd:Q296; # de Monet
}
```

Afficher en plus les labels et les images associées 

```
SELECT DISTINCT ?peinture ?peintureLabel ?image WHERE {
    ?peinture wdt:P31 wd:Q3305213 ; # C'est une peinture
          wdt:P170 wd:Q296; # de Monet
    OPTIONAL { ?peinture wdt:P18 ?image } # avec une image si possible
    SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]" }
                           }
```

Affichr les collections/lieux de conservation
```
SELECT DISTINCT ?peinture ?peintureLabel ?image ?collection WHERE {
    ?peinture wdt:P31 wd:Q3305213 ; # C'est une peinture
          wdt:P170 wd:Q296; # de Monet
    OPTIONAL { ?peinture wdt:P18 ?image .
             ?peinture wdt:P195/wdt:P361* ?collection } # avec une image (si possible) et qui fait partie d'une collection si possible 
    SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]" }
                            }
```
Comment préciser que les lieux de conservation nous intéressent aussi?

Compter le nombre de Monet dans chaque collection/lieux de conservation et les afficher par ordre décroissant 
```
SELECT DISTINCT ?peinture ?peintureLabel ?image ?collectionLabel (COUNT(?collection) AS ?count) 

WHERE {
    ?peinture wdt:P31 wd:Q3305213 ; # C'est une peinture
          wdt:P170 wd:Q296; # de Monet
    OPTIONAL {?peinture wdt:P195/wdt:P361* ?collection } # fait partie d'une collection si possible 
    SERVICE wikibase:label { bd:serviceParam wikibase:language "[AUTO_LANGUAGE]" }
                            }
ORDER BY DESC(?collection)
```
Je n'ai pas réussi la dernière requête.



## Datavisualisation des fromages français

Visualisation des données:

<iframe src="https://data.opendatasoft.com/explore/embed/dataset/fromagescsv-fromagescsv@public/table/?disjunctive.fromage&static=false&datasetcard=false" width="800" height="600" frameborder="0"></iframe>


Carte des fromages selon le département (cluster et choroplèthe)
<iframe frameborder="0" width="800" height="600" src="https://data.opendatasoft.com/map/embed/carte_des_fromages_francais/?&static=false&scrollWheelZoom=false"></iframe>

Datavisualisation des fromages selon le type de lait
<iframe src="https://data.opendatasoft.com/chart/embed/?dataChart=eyJxdWVyaWVzIjpbeyJjb25maWciOnsiZGF0YXNldCI6ImZyb21hZ2VzY3N2LWZyb21hZ2VzY3N2QHB1YmxpYyIsIm9wdGlvbnMiOnsiZGlzanVuY3RpdmUuZnJvbWFnZSI6dHJ1ZSwidGltZXpvbmUiOiJFdXJvcGUvQmVybGluIn19LCJjaGFydHMiOlt7ImFsaWduTW9udGgiOnRydWUsInR5cGUiOiJjb2x1bW4iLCJmdW5jIjoiQ09VTlQiLCJzY2llbnRpZmljRGlzcGxheSI6dHJ1ZSwiY29sb3IiOiIjNTY1NjU2In1dLCJ4QXhpcyI6ImxhaXQiLCJtYXhwb2ludHMiOjUwLCJzb3J0IjoiIiwic2VyaWVzQnJlYWtkb3duIjoiIiwic2VyaWVzQnJlYWtkb3duVGltZXNjYWxlIjoiIiwiY2F0ZWdvcnlDb2xvcnMiOnsiVmFjaGUiOiIjRTUzNTJEIiwiQ2hcdTAwRTh2cmUiOiIjRjdBRDg0IiwiQnJlYmlzIjoiI0ZCRTZDNiJ9fV0sInRpbWVzY2FsZSI6IiIsImRpc3BsYXlMZWdlbmQiOnRydWUsImFsaWduTW9udGgiOnRydWV9&static=false&datasetcard=false" width="800" height="600" frameborder="0"></iframe>



