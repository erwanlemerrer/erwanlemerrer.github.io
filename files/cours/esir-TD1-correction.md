# Cours "Network science" - Erwan Le Merrer
# TD1 du 13/11/2021

Nous utiliserons [NetworkX](https://networkx.github.io/) pour la manipulation des concepts abordés dans le poly.
La documentation est disponible [ici](https://networkx.github.io/documentation/stable/index.html).

Démarrage rapide sur NetworkX [ici](https://networkx.github.io/documentation/stable/tutorial.html).

## Warm-up
* créez un graphe "G" dirigé

```python
from networkx import nx
import pylab as plt
import numpy as np

G = nx.DiGraph()
```

* ajoutez 5 noeuds et connectez les en cycle

```python
    G.add_edges_from([(0, 1), (1, 2), (2, 3), (3, 4), (4, 0)])
```

* affichez le degree sortant du noeud 0

```python
    print(G.out_degree(0))
```

* vérifiez que l'arête (0, 3) n'existe pas, grâce à la fonction appropriée

```python
    print(G.has_edge(0, 3))
```

* inversez la direction des arêtes de G

```python
    G = G.reverse()

```
* ajoutez l'arête (0, 3), avec nom positionné (attribut) à "raccourci", puis l'afficher

```python
    G.add_edge(0, 3, nom='raccourci')
    print(G[0][3])
```

* affichez votre graphe avec la function "draw" et vérifier qu'il est cohérent avec l'exercice

```python
    nx.draw(G,nx.spring_layout(G),cmap=plt.get_cmap('seismic'), with_labels=True)
    plt.show()
```

## Etude d'un graphe réel

[Le graphe Zachary Karate Club](http://konect.uni-koblenz.de/networks/ucidata-zachary)

* importez le graphe "karate club" dans G

```python
    G = nx.karate_club_graph()
```
* affichez le; qu'est ce qu'un layout ? Essayez en plusieurs

* afficher son nombre de noeuds

```python
    print("Nombre de noeuds: ", nx.number_of_nodes(G))
```
* affichez le plus haut degré de G

```python
    print("Plus haut degré du graphe: ", max([d for n,d in np.array(G.degree)]))
```
* affichez (en texte) la distribution des degrés des noeuds de G

```python
    print("Distribution des degrés: ")
    degree_sequence = [d for n, d in G.degree()]  # degree sequence
    hist = {}
    for d in degree_sequence:
        if d in hist: hist[d] += 1
        else: hist[d] = 1
    print("degree #nodes")
    for d in hist:
        print('%d %d' % (d, hist[d]))
```
* affichez le coefficient de clustering du noeud 4

```python
    print("Indiv. clustering coefficients: ", str(nx.clustering(G)[4]))

```
* affichez le coefficient de clustering moyen de G

```python
    print("Average clustering coefficient: ", nx.average_clustering(G))
```
* affichez le diamètre de G

```python
    print("Diameter: ", nx.diameter(G))
```
* affichez la conductance du groupe de noeuds [4,5,6,10,16]

```python
    print("Conductance [4,5,6,10,16]: ", nx.cuts.conductance(G, [4,5,6,10,16]))
```

* extraire S, le sous graphe de G composé par les noeuds donnés à l'exercice précédent

```python
    S = nx.subgraph(G, [4,5,6,10,16])
```

* affichez la connectivité algébrique de G. Conclusion?

```python
    print("Algebraic connectivity: ", nx.algebraic_connectivity(G))
```
* chercher la fonction "articulation_points" dans la doc networkx; quel est son but? Exécutez la sur G

```python
    print("Points d'articulation de G: ", list(nx.articulation_points(G)))
```
* chercher la fonction "bridges" dans la doc networkx, quel est son but? Exécutez la sur G

```python
    print("Ponts de G: ", list(nx.bridges(G)))

```
* créez un graphe H, copie de G. Dans H, supprimez le noeud 0, puis affichez la connectivité algébrique de H pour vérifier sa propriété traitant de la connectivité. Qu'en concluez vous?

```python
    H = G.copy()
    H.remove_node(0)
    print("Algebraic connectivity of H: ", nx.algebraic_connectivity(H))
```
* affichez le nombre de composant connectés de H

```python
    print("Number of connected components in H:", nx.number_connected_components(H))
```
* donner un numéro identique aux noeuds (dans un attribut) en fonction de leur appartenance à un même composant (cf exercice précédent). Affichez ces attributs

```python
    component = []
    nx.set_node_attributes(G, component, 'component')
    c = 0
    for set in nx.connected_components(H):
        for n in set:
            H.nodes[n]['component']=c
        c+=1
```

Questions/commentaires: erwan.le-merrer@inria.fr
