# Cours "Network science" - Erwan Le Merrer
# TP4 du 03/12/2020

[NetworkX](https://networkx.github.io/) et sa documentation [ici](https://networkx.github.io/documentation/stable/index.html).

Propos principal: extraire les communautés d'un graphe réel.

## Détection de communautés

* téléchargez le fichier des caratères de Games of Thrones "book 1" [ici](https://github.com/mathbeveridge/asoiaf). Importez le dans GoT

```python
    import pandas as pd
    got_data = pd.read_csv('graphs/asoiaf-book1-edges.csv')
    print(got_data.head())

    GoT = nx.Graph()
    for row in got_data.iterrows():
        GoT.add_edge(row[1]['Source'],row[1]['Target'],
            weight=row[1]['weight'])
```

* afficher l'assortativité de GoT. Conclusion?

```python
    print(nx.degree_assortativity_coefficient(GoT))
```
* afficher le graphe correspondant au k-core, avec k=11

```python
    print("k-cores: ", nx.core_number(GoT))
    G = nx.k_core(GoT,11)

    nx.draw(G, nx.spring_layout(G), with_labels=True)
    plt.show()
```

* combien des 10 noeuds les plus centraux selon la betweenness centrality appartiennent au précédent 11-core? Conclusion?

```python
    nb = 0
    top10 = [x for x,v in sorted(nx.betweenness_centrality(GoT).items(), key=lambda x:x[1], reverse=True)][:10]
    for i in top10:
        if i in G.nodes: nb+=1
    print("%d/%d" % (nb,len(top10)))    

    # exécutez l'algorithme de détection de communautés qui utilise la notion de modularité. Conclusion sur sa détection de communauté?
    from networkx.algorithms import community
    parts = list(community.greedy_modularity_communities(GoT))
    print("Number of communities detected: ", len(parts)) # 187, ie, all in it !!!
```

* exécutez l'algorithme de détection de communautés qui utilise la notion de modularité. Conclusion sur sa capacité à détecter les communautés de ce graphe?

```python
    nb = 0
    top10 = [x for x,v in sorted(nx.betweenness_centrality(GoT).items(), key=lambda x:x[1], reverse=True)][:10]
    print("%d/%d" % (len(set(top10).intersection(G.nodes)), len(top10)))
```
* regardez l'algorithme de [girvan_newman](https://en.wikipedia.org/wiki/Girvan%E2%80%93Newman_algorithm): les communautés sont créées à partir de la suppression d'arêtes. Quel est le critère pour sélectionner les arêtes à supprimer prioritairement?

```python
    from networkx.algorithms import community
    parts = list(community.greedy_modularity_communities(GoT))
    print("Number of communities detected: ", len(parts)) # 187, ie, all in it !!!
```
* utilisez le pour créer un partitionnement en 10 communautés
 
```python
    parts_gn = community.girvan_newman(GoT)
    k = 9
    import itertools
    for communities in itertools.islice(parts_gn, k):
        comms = tuple(sorted(c) for c in communities)
        print("Nb of computed communities: ", len(comms))
```

* affichez la troisième de ces 10 communautés, en utilisant la fonction qui extrait un sous graphe de GoT
 
```python
    G_comm = GoT.subgraph(comms[2])
    nx.draw(G_comm, nx.spring_layout(G_comm), with_labels=True)
```

* reprenez la boucle For qui sert à créer les 10 partitions avec Girvan Newman, et insérez la mesure de qualité du partitionnement courant avec la fonction coverage. Que mesure t elle exactement? A combien de communautés aurait il été judicieux de s arrêter au regard de cette mesure?

```python
    parts_gn = community.girvan_newman(GoT)
    c = None
    for communities in itertools.islice(parts_gn, k):
        comms = tuple(sorted(c) for c in communities)
        print("Nb of computed communities: ", len(comms))
        print(c)
        c = communities
        print(community.quality.coverage(GoT,c))
    # ---> assez fort drop après 5 communautés, de 0.97 à 0.93
```

Questions/commentaires: erwan.le-merrer@inria.fr
