# Requêtes SPARQL via DBpedia 

## Liste des photojournalistes 
#output-format:auto
define sql:signal-unconnected-variables 1
define sql:signal-void-variables 1
define input:default-graph-uri <http://dbpedia.org>
PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT DISTINCT ?person_uri (STR(?label) AS ?persName) ?birthYear
WHERE { 
    dbr:List_of_American_photojournalists ?p ?person_uri.
    ?person_uri a dbo:Person;
                dbo:birthDate ?birthDate;
                rdfs:label ?label.
    BIND(xsd:integer(SUBSTR(STR(?birthDate), 1, 4)) AS ?birthYear)
    FILTER (?birthYear > 1880 && LANG(?label) = 'en')
}
ORDER BY ?birthYear

Le but de la présente requête est d'extraire une liste structurée de photojournalistes américains depuis la base de données DBpedia. En particulier, la requête permet d'extraire des informations relatives aux noms, prénoms et dates de naissance des photojournalistes. 