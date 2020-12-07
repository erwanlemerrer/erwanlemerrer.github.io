# Cours "Network science" - Erwan Le Merrer
# TP5 du 07/12/2020

[NetworkX](https://networkx.github.io/) et sa documentation [ici](https://networkx.github.io/documentation/stable/index.html).

Propos principal: comparer de petits graphes.

## Comparaison de graphes

* comparer ces deux graphes: une étoile à 4 noeuds, et un graphe complet de la même taille, avec la fonction distance d'édition de NetworkX. La distance retournée vous semble t elle cohérente?

* testez sur des graphes un peu plus gros; quelle est la complexité du calcul de la distance d'édition de graphes?

* créez les graphlets G4, G8 et G15 du poly

* regardez la définition d'[isomorphisme](https://fr.wikipedia.org/wiki/Isomorphisme_de_graphes). Créez 2 graphes isomorphes de 3 noeuds, et (ie, G1 ou G2) vérifiez cette propriété avec la fonction appropriée de NetworkX.

* nous allons compter ces graphlets dans le graphe Karate Club. Le but est de créer une fonction get\_graphlet\_edges(graphlet, G) qui retourne la liste des arêtes de chacun des "graphlets" trouvés dans G.	
     * avec la fonction itertools.combinations(...), itérez sur tous les combinaisons possibles de k noeuds (si le graphlet en paramètres compte k noeuds) dans les noeuds de G; extrayez le sous graphe induit par chaque combinaison, et vérifiez qu'il est connecté.
     * s'il l'est, alors vérifiez s'il est aussi isomorphe au graphlet: si oui vous avez trouvé un graphlet de G, poursuivez.

* importez le graphe Karate Club dans G. Combien de graphlets G4, G8 et G15 dans G?

* comparez ces quantités à celles d'un graphe Barabasi-Albert comportant également 34 noeuds (eg, nx.barabasi\_albert_graph(34, 2)). Conclusion de similarité cohérente avec la comparaison d'autres caractéristiques des deux réseaux? (eg, shortest path et average clustering)

* BONUS: regardez les "graph kernels" à base de marches aléatoires (eg, [ici](https://github.com/ysig/GraKeL)). (Ceux ci permettent une comparaison en temps polynomial, et donc de plus grand graphes)

Questions/commentaires: erwan.le-merrer@inria.fr
