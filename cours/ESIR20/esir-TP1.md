# Cours "Network science" - Erwan Le Merrer
# TP1 du 16/11/2020

Nous utiliserons [NetworkX](https://networkx.github.io/) pour la manipulation des concepts abordés dans le poly.
La documentation est disponible [ici](https://networkx.github.io/documentation/stable/index.html).

Démarrage rapide sur NetworkX [ici](https://networkx.github.io/documentation/stable/tutorial.html).

## Warm-up
* créez un graphe "G" dirigé
* ajoutez 5 noeuds et connectez les en cycle
* affichez le degree sortant du noeud 0
* affichez le nombre de noeuds, puis le nombre d'arêtes de G
* vérifiez que l'arête (0, 3) n'existe pas, grâce à la fonction appropriée
* inversez la direction des arêtes de G
* ajoutez l'arête (0, 3), avec nom positionné (attribut) à "raccourci", puis l'afficher
* affichez votre graphe avec la function "draw" et vérifier qu'il est cohérent avec l'exercice

## Etude d'un graphe réel

[Le graphe Zachary Karate Club](https://en.wikipedia.org/wiki/Zachary's_karate_club)

* importez le graphe "karate club" dans G
* affichez le; qu'est ce qu'un layout ? Essayez en plusieurs
* affichez le plus haut degré de G
* affichez (en texte) la distribution des degrés des noeuds de G
* affichez le coefficient de clustering du noeud 4
* affichez le coefficient de clustering moyen de G
* affichez le diamètre de G
* affichez la conductance du groupe de noeuds [4,5,6,10,16]
* affichez la connectivité algébrique de G. Conclusion?
* chercher la fonction "articulation_points" dans la doc networkx; quel est son but? Exécutez la sur G
* chercher la fonction "bridges" dans la doc networkx, quel est son but? Exécutez la sur G
* créez un graphe H, copie de G. Dans H, supprimez le noeud 0, puis affichez la connectivité algébrique de H pour vérifier sa propriété traitant de la connectivité. Qu'en concluez vous?
* affichez le nombre de composant connectés de H
* donner un numéro identique aux noeuds (dans un attribut) en fonction de leur appartenance à un même composant (cf exercice précédent). Affichez ces attributs
* BONUS: programmez l'équation de résiliance donnée dans le poly

Questions/commentaires: erwan.le-merrer@inria.fr
