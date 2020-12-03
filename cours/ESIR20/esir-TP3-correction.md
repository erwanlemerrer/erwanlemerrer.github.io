# Cours "Network science" - Erwan Le Merrer
# TP3 du 20/11/2020

[NetworkX](https://networkx.github.io/) et sa documentation [ici](https://networkx.github.io/documentation/stable/index.html).

Propos principal: les mesures d'influence dans les graphes. Puis un modèle de propagation épidémique simplifié.

## Influence dans un graphe réel

*  téléchargez le fichier des caratères de Games of Thrones "book 1" [ici](https://github.com/mathbeveridge/asoiaf). Importez le dans GoT

```python
    import pandas as pd
    got_data = pd.read_csv('graphs/asoiaf-book1-edges.csv')
    print(got_data.head())

    GoT = nx.Graph()
    for row in got_data.iterrows():
        GoT.add_edge(row[1]['Source'],row[1]['Target'],
            weight=row[1]['weight'])
```

* afficher les caractéristiques quelques de base de GoT (avec des fonctions de la librairie)

```python
    print(GoT.number_of_nodes())
    print(nx.is_connected(GoT))
    print(nx.is_directed(GoT))
```

* Regardons les quatres centralités suivantes sur GoT: degree, betweenness, eigenvector centrality et second order centrality. Classez les personnages par ordre d'influence décroissante pour chaque centralité (attention à l'ordre pour second order centrality!). Les classements sont ils les mêmes?

```python
    print(sorted(nx.degree_centrality(GoT).items(), key=lambda x:x[1], reverse=True))
    print(sorted(nx.eigenvector_centrality(GoT).items(), key=lambda x:x[1], reverse=True))
    print(sorted(nx.betweenness_centrality(GoT).items(), key=lambda x:x[1], reverse=True))
    print(sorted(nx.second_order_centrality(GoT).items(), key=lambda x:x[1], reverse=False))
```

## Attaque sur l'influence 
* vous allez attaquer ce réseau social pour essayer de gagner de l'influence pour un caractère fictif, le noeud 0. Connectez un noeud 0 à 'Daryn-Hornwood', dans un nouveau graphe Gs

```python
    Gs = GoT.copy()
    Gs.add_edge('Daryn-Hornwood', 0)
```

* exécutez une centralité eigenvector centrality sur le graphe attaqué Gs, et affichez le rang de 0 dans le classement de l'influence des noeuds. L'attaque est elle efficace?

```python
    rank_ec = sorted(nx.eigenvector_centrality(Gs).items(), key=lambda x:x[1], reverse=True)
    keys = [i for i,v in rank_ec]
    print("Rank with eigenvector_centrality for single node addition, connected to Daryn-Hornwood: ", keys.index(0))
```

* même manipulation, en connectant à la place 0 avec Eddard-Stark dans un graphe G. Le rang de 0 est il meilleur? Pourquoi?

```python
    G = GoT.copy()
    G.add_edge('Eddard-Stark', 0)
    rank_ec = sorted(nx.eigenvector_centrality(G).items(), key=lambda x:x[1], reverse=True)
    keys = [i for i,v in rank_ec]
    print("Rank with eigenvector_centrality for single node addition, connected to Eddard-Stark: ", keys.index(0))
```

* créez un graphe en étoile de 10 noeuds, avec 0 pour centre. Connectez le à GoT par une arête entre 0 et Eddard-Stark (cf fonction compose)

```python
    A1 = nx.star_graph(9)
    G =nx.compose(GoT, A1)

    G.add_edge('Eddard-Stark', 0)
```

* quel est le nouveau rang de 0? Différence par rapport à l'attaque simple?

```python
    rank_ec = sorted(nx.eigenvector_centrality(G).items(), key=lambda x:x[1], reverse=True)
    keys = [i for i,v in rank_ec]
    print("Rank with eigenvector centrality and star graph attack: ", keys.index(0))
```

* trouver un exemple de de centralité qui est moins sensible que eigenvector centrality à cette attaque (ie, le rang de 0 est bas)

```python
    rank_soc = sorted(nx.second_order_centrality(G).items(), key=lambda x:x[1], reverse=False)
    keys = [i for i,v in rank_soc]
    print("Rank with second order centrality and star graph attack: ", keys.index(0))
```

## Détection de l'attaque

* tester si le sampling à base de marches aléatoires pour détecter les attaques (cf poly) classe les noeuds qui ont servi à l'attaque parmi les plus probablement "faux" de G (ie, quid de leur fréquence d'échantillonnage? Afficher le sampling rate pour 1000 marches aléatoires partant chacune d'un noeud aléatoire de G

```python
    import random
    
    def walk_h_hops(i,h,G):
        path = []
        next = random.choice(list(G.neighbors(i)))
        while h>0:
            path.append(next)
            next = random.choice(list(G.neighbors(next)))
            h-=1
        return path
    
    samples = []
    nb_samples = 1000
    for t in range(nb_samples):
        samples.append (walk_h_hops(random.choice(list(G.nodes)), 1000, G)[-1] )
    for i in G.nodes():
        print("Node %s: normalized sampling rate=%f" % (i,samples.count(i)/nb_samples))
```

## Propagation épidémique sur un graphe
* une épidémie chez les personnages de GoT: programmez un modèle épidémique SIS simplifié (avec une seule variable delta et pas de boucles sur les états), en simulation par ronde. Passez en par un statut booléen 'infected' sur chaque noeud. Affichez un tableau contenant l'état 'infected' des noeuds après chaque ronde

```python
    delta = 0.9
    infecte = False
    nx.set_node_attributes(GoT, infecte, 'infected')
    
    def infection_simulation(patient_zero,nb_rounds,delta,G):
        GoT.nodes[patient_zero]['infected'] = True

        for i in range(nb_rounds):
            for i in GoT.nodes():
                # infection des voisins
                if(GoT.nodes[i]['infected']):
                    for j in list(GoT.neighbors(i)):
                        if random.random() < 1-delta: GoT.nodes[j]['infected'] = True
                # guerison
                if(GoT.nodes[i]['infected']):
                    if random.random() < delta: GoT.nodes[j]['infected'] = False       
        # end of round
        return([GoT.nodes[x]['infected'] for x in GoT.nodes()])

    # démarrez une infection à partir de 'Daryn-Hornwood' (ie, infected=True) (delta=0.9), combien d'infectés après 10 rounds?
    print(sum(infection_simulation('Daryn-Hornwood',10,delta,GoT)))
    
    # même chose à partir de 'Eddard-Stark', combien d'infectés? Conclusion?
    print(sum(infection_simulation('Eddard-Stark',10,delta,GoT)))
```

Questions/commentaires: erwan.le-merrer@inria.fr
