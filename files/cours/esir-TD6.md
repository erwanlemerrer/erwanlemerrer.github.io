# Cours "Network science" - Erwan Le Merrer
# TD6 du 07/12/2021

[NetworkX](https://networkx.github.io/) et sa documentation [ici](https://networkx.github.io/documentation/stable/index.html).

## Graphe dont les arêtes évoluent dans le temps, et marche aléatoire sur celui ci.

* nous allons modéliser les contacts aléatoires de 100 personnes (les arêtes du graphe d'intéraction vont évoluer dans le temps), et un paquet allant au hasard de contact en contact avant d'atteintre son destinataire.
La matrice d'adjacence qui change dans le temps:
	* écrire une fonction qui retourne une matrice (numpy) d'adjacence, de 100 par 100 donc.
	* dans cette fonction, remplissez cette matrice de variables aléatoires avec une distribution exponentielle (np.random.exponential(scale=1.0))
	* une fois remplie, transformez ses valeurs en True ou False si elles sont inférieures à 0.05.

* utilisez cette fonction pour générer des matrices d'adjacence, en les transformant en graphe à chaque appel, avec nx.from_numpy_array(matrix). Affichez successivement plusieurs des graphes ainsi créés.

* le paquet part du noeud 0, et doit atteindre le noeud 99, par sélection d'un voisin d'ID supérieur noeud courant à chaque étape, s'il existe. Ecrire la fonction implémentant cela, qui prend en paramètre le noeud de départ du paquet, le noeud destinataire, et le nombre de noeuds dans le graphe.

* Afficher une réalisation de ce voyage du paquet. Quelle est l'espérance empirique du temps t d'atteinte du destinataire par ce paquet?

* nous allons créer la fonction "présence". Générez 100 graphes successifs (ie, t0 à t99) dans un tableau, puis écrivez une fonction de présence retournant True ou False sur la présence d'une arête particulière à un instant t donné en paramètre.


Questions/commentaires: erwan.le-merrer@inria.fr
