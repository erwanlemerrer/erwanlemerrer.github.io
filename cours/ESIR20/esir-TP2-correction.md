# Cours "Network science" - Erwan Le Merrer
# TP2 du 19/11/2020

[NetworkX](https://networkx.github.io/)

Sa documentation [ici](https://networkx.github.io/documentation/stable/index.html).


## Rappel

* nous avons étudié le graphe "karate club" lors du TP1. Chargez les 3 autres graphes "réels" de NetworkX; lequel a le plus petit diamètre?

```python
    print(nx.diameter(nx.davis_southern_women_graph()))
    print(nx.diameter(nx.florentine_families_graph()))
    print(nx.diameter(nx.les_miserables_graph()))

```

## Modélisation de graphes réels
    
* créez un graphe de 100 noeuds avec le modèle Erdos Renyi, et une probabilité de connection p de 0.01. Le graphe est il connecté? Itérez par incrément de 0.01 sur p et stoppez quand G est connecté; quelle valeur empirique pour p?

```python
    p = 0.01
    G = nx.erdos_renyi_graph (100, p)
    while not nx.is_connected(G):
        p+=0.01
        G = nx.erdos_renyi_graph (100, p)
    print(p) # often 0.04, aligned with expectation of ln n / n ! 
```
* rendez vous sur [SNAP](https://snap.stanford.edu/data/egonets-Facebook.html) et téléchargez le petit sous graphe de Facebook dénommé 'facebook_combined.txt'. Sous quel format ce graphe est il stocké? Importez le dans FB

```python
    fh=open("graphs/facebook_combined.txt", 'rb')
    FB=nx.read_adjlist(fh)
```
* affichez le nombre de noeuds et d'arêtes de FB, et vérifiez qu'ils soient cohérents avec les informations sur la page SNAP

```python
    n = FB.number_of_nodes()
    m = FB.number_of_edges()
    print(n)
    print(m)
```
* affichez la moyenne des degrés des noeuds du graphes (attention aux fonctions trompeuses dans Networkx!)
 
```python
    degrees = FB.degree()
    d_avg = sum(dict(degrees).values())/n
    print("Moyenne des degrés de FB: ", d_avg)
```
   
* créez un graphe Barabasi-Albert dans BA: il doit avoir a peu pres le même nombre d'arête que FB. A quoi correspond m, que vous devrez manipuler pour cela?

```python
    BA = nx.barabasi_albert_graph(n, int(d_avg/2))
    print(BA.number_of_edges())
```
* créez un graphe Watts-Strogatz dans WS. Positionnez p=0.05
    
```python
    WS = nx.connected_watts_strogatz_graph(n, int(d_avg), 0.05)
    print(WS.number_of_edges())
```
* comparer les caractéristiques (taux de clustering moyen et moyenne des longueurs des chemins): lequel des modèles approche le plus le graphe réel FB?    

```python
    print(nx.average_clustering(FB), nx.average_shortest_path_length(FB))
    print(nx.average_clustering(BA), nx.average_shortest_path_length(BA)) #0.03744630017552204 2.51066477770416
    print(nx.average_clustering(WS), nx.average_shortest_path_length(WS)) #0.6277827031740587 3.215967374071108

```
* programmez une routine qui sélectionne un noeud au hasard dans BA, puis le supprime. Boucler jusqu'à ce que BA soit déconnecté. Combien faut il de suppressions? Même chose pour WS. Conclusion sur la résistance de BA vs WS?

```python
    import random
    
    ''' assumes G is connected
        Returns: number of randomly selected and removed nodes before G is disconnected
    '''
    def remove_random_until_unconnected(G):
        i = 0
        node = random.choice(list(G.nodes()))
        while nx.is_connected(G):
            G.remove_node(node)
            node = random.choice(list(G.nodes()))
            i +=1
        return i
    print("Nombre de suppressions aléatoires de noeuds avant déconnection BA: " , remove_random_until_unconnected(BA))
    print("Nombre de suppressions aléatoires de noeuds avant déconnection WS: " , remove_random_until_unconnected(WS))

```

## Exploration de graphes
  
* est ce que FB compte un chemin Eulérien? (Regarder le code de la fonction que vous appelerez)

```python
    print("Is FB Eulerian? ", nx.is_eulerian(FB))

```
* programmez une routine qui implémente une marche aléatoire (biaisée) sur FB entre deux sommets (donnés en paramètre), et retourne le chemin emprunté (liste de sommets)

```python
    def walk(i,j,G):
        path = []
        if i == j: return path
        next = random.choice(list(G.neighbors(i)))
        while next != j:
            path.append(next)
            next = random.choice(list(G.neighbors(next)))
        path.append(j)
        return path
```
* empiriquement le "hitting time" est la cardinalité du chemin (retourné dans l'exercice précédent). Pour 100 essais, quel est le hitting time moyen sur FB entre les noeuds '0' et '10'?

```python
    cptr = 0
    for i in range(100):
        cptr += len(walk('0','10',FB))
    print("Hitting time empirique: ", cptr/100)
```
* créez un spanner de FB, dans le graphe FBS, avec un stretch de 10. Afficher le nombre d'arêtes de FBS, pour vérifier l'efficacité de l'algorithme de spanning
 

* testez le hitting time moyen sur FBS maintenant. Quelle différence avec celui sur FB? Conclusion?


* BONUS qu'est ce qu'un ensemble dominant ([dominating set](https://networkx.github.io/documentation/stable/reference/algorithms/approximation.html?highlight=dominating#module-networkx.algorithms.approximation.dominating_set))? En trouver un pour le Karate Club, puis afficher G avec ses noeuds dominants en rouge

* BONUS: programmez l'équation de résiliance donnée dans le poly ;)

Questions/commentaires: erwan.le-merrer@inria.fr
