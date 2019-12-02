# Cours "Network science" - Erwan Le Merrer
# TP4 du 02/12/2019

[NetworkX](https://networkx.github.io/) et sa documentation [ici](https://networkx.github.io/documentation/stable/index.html).

Propos principal: extraire les communautés d'un graphe réel.

## Détection de communautés

* téléchargez le fichier des caratères de Games of Thrones "book 1" [ici](https://github.com/mathbeveridge/asoiaf). Importez le dans GoT

* afficher l'assortativité de GoT. Conclusion?

* afficher le graphe correspondant au k-core, avec k=11

* combien des 10 noeuds les plus centraux selon la betweenness centrality appartiennent au précédent 11-core? Conclusion?

* ~~exécutez l'algorithme de détection de communautés qui utilise la notion de modularité. Conclusion sur sa capacité à détecter les communautés de ce graphe?~~

* regardez l'algorithme de [girvan_newman](https://en.wikipedia.org/wiki/Girvan%E2%80%93Newman_algorithm): les communautés sont créées à partir de la suppression d'arêtes. Quel est le critère pour sélectionner les arêtes à supprimer prioritairement?

* utilisez le pour créer un partitionnement en 10 communautés
 
* affichez la troisième de ces 10 communautés, en utilisant la fonction qui extrait un sous graphe de GoT
 
* reprenez la boucle For qui sert à créer les 10 partitions avec Girvan Newman, et insérez la mesure de qualité du partitionnement courant avec la fonction coverage. Que mesure t elle exactement? A combien de communautés aurait il été judicieux de s arrêter au regard de cette mesure?


Questions/commentaires: erwan.le-merrer@inria.fr
