# Cours "Network science" - Erwan Le Merrer
# TD2 du 20/10/2020

[NetworkX](https://networkx.github.io/) et sa documentation [ici](https://networkx.github.io/documentation/stable/index.html).


## Rappel

* nous avons étudié le graphe "karate club" lors du TP1. Chargez les 3 autres graphes "réels" de NetworkX; lequel a le plus petit diamètre?

## Modélisation de graphes réels
    
* créez un graphe de 100 noeuds avec le modèle Erdos Renyi, et une probabilité de connection p de 0.01. Le graphe est il connecté? Itérez par incrément de 0.01 sur p et stoppez quand G est connecté; quelle valeur empirique pour p?

* rendez vous sur [SNAP](https://snap.stanford.edu/data/egonets-Facebook.html) et téléchargez le petit sous graphe de Facebook dénommé 'facebook_combined.txt'. Sous quel format ce graphe est il stocké? Importez le dans FB

* affichez le nombre de noeuds et d'arêtes de FB, et vérifiez qu'ils soient cohérents avec les informations sur la page SNAP

* affichez la moyenne des degrés des noeuds du graphes (attention aux fonctions trompeuses dans Networkx!)
    
* créez un graphe Barabasi-Albert dans BA: il doit avoir a peu pres le même nombre d'arête que FB. A quoi correspond m, que vous devrez manipuler pour cela?

* créez un graphe Watts-Strogatz dans WS. Positionnez p=0.05
    
* comparer les caractéristiques (taux de clustering moyen et moyenne des longueurs des chemins): lequel des modèles approche le plus le graphe réel FB?    

* programmez une routine qui sélectionne un noeud au hasard dans BA, puis le supprime. Boucler jusqu'à ce que BA soit déconnecté. Combien faut il de suppressions? Même chose pour WS. Conclusion sur la résistance de BA vs WS?


## Exploration de graphes
  
* est ce que FB compte un chemin Eulérien? (Regarder le code de la fonction que vous appelerez)

* programmez une routine qui implémente une marche aléatoire (biaisée) sur FB entre deux sommets (donnés en paramètre), et retourne le chemin emprunté (liste de sommets)

* empiriquement le "hitting time" est la cardinalité du chemin (retourné dans l'exercice précédent). Pour 100 essais, quel est le hitting time moyen sur FB entre les noeuds '0' et '10'?

Questions/commentaires: erwan.le-merrer@inria.fr
