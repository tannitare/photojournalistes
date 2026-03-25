


Check basic properties 

PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>


SELECT DISTINCT ?item  ?gender ?year ?itemLabel
        WHERE {

        ## note the service address          
        SERVICE <https://query.wikidata.org/sparql>
            {
            {?item wdt:P106 wd:Q957729}
    UNION
    {?item wdt:P101 wd:Q506858}     
        
            ?item wdt:P31 wd:Q5;  # Any instance of a human.
                wdt:P569 ?birthDate; # It must necessarily have a birth date property
                wdt:P21 ?gender. # It must necessarily have a gender property
        BIND(year(?birthDate) as ?year)
       
  
        OPTIONAL {
	     ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'en')
    }
        }
        }
        LIMIT 10
  


Insert: import data from Wikidata 

  PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

INSERT {

        ### Note that the data is imported into a named graph and not the DEFAULT one
        GRAPH <https://tannitare.github.io/photojournalists/graphs-defs.html#wikidata>
        {?item  wdt:P21 ?gender.
           ?item wdt:P569 ?year. 
           ?item rdfs:label ?itemLabel.           # ?item  wdt:P31 wd:Q5.
           # modifier pour disposer de la propriété standard
           ?item  rdf:type wd:Q5.
           }
}
      
        WHERE {
  
                          SELECT DISTINCT ?item ?year ?gender ?itemLabel
  
                          WHERE {

        ## note the service address          
        SERVICE <https://query.wikidata.org/sparql>
            {
             {?item wdt:P106 wd:Q957729}
    UNION
    {?item wdt:P101 wd:Q506858}
        
            ?item wdt:P31 wd:Q5;  # Any instance of a human.
                wdt:P569 ?birthDate. # It must necessarily have a birth date property



        BIND(year(?birthDate) as ?year)
  
   OPTIONAL {
            # The item can have or not a gender property
            ?item wdt:P21 ?gender.
        }
  
        OPTIONAL {
             ?item rdfs:label ?itemLabel.
        FILTER(LANG(?itemLabel) = 'en')
    }
   
        }
        }
    ORDER BY ?item 
        }



Import data from Wikidata 

        PREFIX wd: <http://www.wikidata.org/entity/>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX wikibase: <http://wikiba.se/ontology#>
PREFIX bd: <http://www.bigdata.com/rdf#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

select ?s ?p ?o
where {
  
        GRAPH <https://tannitare.github.io/photojournalists/graphs-defs.html#wikidata>
        {?s ?p ?o}
        }
limit 50