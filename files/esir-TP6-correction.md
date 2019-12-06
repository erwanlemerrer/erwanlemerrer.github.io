# Cours "Network science" - Erwan Le Merrer
# TP6 du 06/12/2019

[NetworkX](https://networkx.github.io/) et sa documentation [ici](https://networkx.github.io/documentation/stable/index.html).

Propos principal: comparer de petits graphes.

## Graphe dont les arêtes évoluent dans le temps, et marche aléatoire sur celui ci.

* nous allons modéliser les contacts aléatoires de 100 personnes (les arêtes du graphe d'intéraction vont évoluer dans le temps), et un paquet allant au hasard de contact en contact avant d'atteintre son destinataire.
Matrice d'adjacence qui change dans le temps:
	* écrire une fonction qui retourne une matrice (numpy) d'adjacence, de 100 par 100 donc.
	* dans cette fonction, remplissez cette matrice de variables aléatoires avec une distribution exponentielle (np.random.exponential(scale=1.0))
	* une fois remplie, transformez ses valeurs en True ou False si elles sont inférieures à 0.05.

```python
    n = 100
    start_node = 0
    target_node = 99

    def get_adj(n, threshold):
        matrix = [np.random.exponential(scale=5.0) for i in range(n*n)]
        matrix = np.reshape(matrix, (n,n))
        return matrix < threshold
```

* utilisez cette fonction pour générer des matrices d'adjacence, en les transformant en graphe à chaque appel, avec nx.from_numpy_array(matrix). Affichez successivement plusieurs des graphes ainsi créés.


* le paquet part du noeud 0, et doit atteindre le noeud 99, par sélection aléatoire d'un voisin du noeud courant à chaque étape. Ecrire la fonction implémentant cela, qui prend en paramètre le noeud de départ du paquet, le noeud destinataire, et le nombre de noeuds dans le graphe.

```python
    import random
    def get_to_target(start_node, target_node, n):
        path = []
        current_node = start_node

        # generation des connexions du graphe à t0
        Gt = nx.from_numpy_array(get_adj(n, 0.01))  
    
        while True:
            if target_node in list(Gt.neighbors(current_node)):
                path.append(target_node)
                return path
            else:
                if not list(Gt.neighbors(current_node)): Gt = nx.from_numpy_array(get_adj(n, 0.05)); continue # in case no neighbor
                current_node = random.choice(list(Gt.neighbors(current_node)))
                path.append(current_node)
                print(path)
                Gt = nx.from_numpy_array(get_adj(n, 0.05))      

    print(get_to_target(start_node, target_node, n))
```

* affichez une réalisation de ce voyage du paquet. Quelle est l'espérance empirique de l'atteinte du destinataire par ce paquet?

```python
    sum = 0
    nb_samples= 1
    for i in range(nb_samples):
        sum += len(get_to_target(start_node, target_node, n))
    print("Espérance empirique sur %d observations: %f: " % (nb_samples,sum/nb_samples)) # Espérance empirique sur 100 observations: 12.170000: 
```

* nous allons créer la fonction "présence". Générez 100 graphes successifs (ie, t0 à t99) dans un tableau, puis écrivez une fonction de présence retournant True ou False sur la présence d'une arête particulière à un instant t donné en paramètre.

```python
    graphs = []
    n = 100
    for i in range(100):
        graphs.append(nx.from_numpy_array(get_adj(n, 0.05)))
    
    def presence(graphs, edge, t):
        return graphs[t].has_edge(edge[0], edge[1])
    
    print(presence(graphs, (0,1), 10))
```

Questions/commentaires: erwan.le-merrer@inria.fr
