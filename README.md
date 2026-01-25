# Étude proposographique de la population photojournalistes

## Présentation du projet
Le présent dossier a été réalisé dans le cadre du cours master "From Information to data: introduction to research information systems for historical and social sciences" donné par Francesco Beretta à l'UNIFR pendant le semestre d'automne 2025. 
L'enjeu est de transformer des données semi-structurées issues du web sémantique en une base de données relationnelle exploitable pour l'analyse historique (carrières, zones géographiques, réseaux). Ensuite, il est question d'appliquer la méthode **prosopographique** (biographie collective) à une population de photojournalistes. 

## Méthodologie & Sources
Le choix de la population s'est fait de façon aléatoire, principalement en lien avec mon mémoire de master. En particulier, elle a été constituée à partir des entrées DBpedia correspondant à la catégorie des photojournalistes. 

### Étapes de réalisation :
1.  **Extraction :** Requêtage de DBpedia pour obtenir les noms, dates de naissance/décès, nationalités et agences de presse.
2.  **Nettoyage :** Traitement des données brutes pour harmoniser les formats (dates, pays).
3.  **Modélisation :** Création du schéma relationnel sur DBeaver.
4.  **Importation :** Intégration de fichiers CSV dans la base de données.

## Schéma de la base de données
Le projet repose sur une structure relationnelle permettant de croiser les individus avec leurs contextes professionnels et géographiques.
Le schéma réalisé avec la base de données DBeaver, est conçu pour répondre aux exigences de la méthode prosopographique, qui consiste à étudier un groupe à travers un catalogue de variables uniformes. La base est organisée autour d'une table centrale (Individus) reliée à des tables satellites pour éviter la redondance des données. 
 