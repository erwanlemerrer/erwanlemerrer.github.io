# Cours "Network science" - Erwan Le Merrer
# TP5 du 07/12/2020

[NetworkX](https://networkx.github.io/) et sa documentation [ici](https://networkx.github.io/documentation/stable/index.html).

Propos principal: comparer de petits graphes.

## Comparaison de graphes

* comparer ces deux graphes: une étoile à 4 noeuds, et un graphe complet de la même taille, avec la fonction distance d'édition de NetworkX. La distance retournée vous semble t elle cohérente?

```python
    print(nx.graph_edit_distance(nx.star_graph(3),nx.complete_graph(4)))
```

* testez sur des graphes un peu plus gros; quelle est la complexité du calcul de la distance d'édition de graphes?

NP-hard

* créez les graphlets G4, G8 et G15 du poly

```python
    G4 = nx.star_graph(3)
    G8 = nx.complete_graph(4)
    G15 = nx.cycle_graph(5)
```

* regardez la définition d'[isomorphisme](https://fr.wikipedia.org/wiki/Isomorphisme_de_graphes). Créez 2 graphes isomorphes de 3 noeuds, et (ie, G1 ou G2) vérifiez cette propriété avec la fonction appropriée de NetworkX.

```python
    Gi1 = nx.path_graph(3)
    Gi2 = nx.Graph()
    Gi2.add_edge(0,1)
    Gi2.add_edge(0,2)
    print(nx.is_isomorphic(Gi1,Gi2))
```

* nous allons compter ces graphlets dans le graphe Karate Club. Le but est de créer une fonction get\_graphlet\_edges(graphlet, G) qui retourne la liste des arêtes de chacun des "graphlets" trouvés dans G.
     * avec la fonction itertools.combinations(...), itérez sur tous les combinaisons possibles de k noeuds (si le graphlet en paramètres compte k noeuds) dans les noeuds de G; extrayez le sous graphe induit par chaque combinaison, et vérifiez qu'il est connecté.
     * s'il l'est, alors vérifiez s'il est aussi isomorphe au graphlet: si oui vous avez trouvé un graphlet de G, poursuivez.

```python
    import itertools
    
    def get_graphlet_edges(graphlet, G):
        graphlets = []
        for sn in itertools.combinations(G.nodes,len(graphlet.nodes)):
            subg = G.subgraph(sn)
            if nx.is_connected(subg) and nx.is_isomorphic(subg, graphlet): 
                graphlets.append(subg.edges())
        return graphlets
```

* importez le graphe Karate Club dans G. Combien de graphlets G4, G8 et G15 dans G?

```python
    Gk = nx.karate_club_graph()

    print(Gk.number_of_nodes(),Gk.number_of_edges(),len(nx.shortest_path(Gk)),nx.average_clustering(Gk))

    print(len(get_graphlet_edges(G4,Gk)))
    print(len(get_graphlet_edges(G8,Gk)))
    print(len(get_graphlet_edges(G15,Gk)))
```

* comparez ces quantités à celles d'un graphe Barabasi-Albert comportant également 34 noeuds (eg, nx.barabasi\_albert_graph(34, 2)). Conclusion de similarité cohérente avec la comparaison d'autres caractéristiques des deux réseaux? (eg, shortest path et average clustering)

```python
    Gba = nx.barabasi_albert_graph(34, 2)
    print(Gba.number_of_nodes(),Gba.number_of_edges(),len(nx.shortest_path(Gba)),nx.average_clustering(Gba))

    print(len(get_graphlet_edges(G4,Gba)))
    print(len(get_graphlet_edges(G8,Gba)))
    print(len(get_graphlet_edges(G15,Gba)))  
```

* BONUS: regardez les "graph kernels" à base de marches aléatoires (eg, [ici](https://github.com/ysig/GraKeL/blob/master/grakel/kernels/random_walk.py)). (Ceux ci permettent une comparaison en temps polynomial, et donc de plus grand graphes)

Questions/commentaires: erwan.le-merrer@inria.fr
