# Cours "Network science" - Erwan Le Merrer
# TP3 du 21/11/2021

[NetworkX](https://networkx.github.io/) et sa documentation [ici](https://networkx.github.io/documentation/stable/index.html).

Propos principal: les mesures d'influence dans les graphes. Puis un modèle de propagation épidémique simplifié.

## Influence dans un graphe réel

*  téléchargez le fichier des caratères de Games of Thrones "book 1" [ici](https://github.com/mathbeveridge/asoiaf). Importez le dans GoT

``` python
    import pandas as pd
    got_data = pd.read_csv('graphs/asoiaf-book1-edges.csv')
    print(got_data.head())

    GoT = nx.Graph()
    for row in got_data.iterrows():
        GoT.add_edge(row[1]['Source'],row[1]['Target'],
            weight=row[1]['weight'])
```

* afficher quelques caractéristiques de base de GoT (avec des fonctions de la librairie)

* regardons les quatres centralités suivantes sur GoT: degree, betweenness, eigenvector centrality et second order centrality. Classez les personnages par ordre d'influence décroissante pour chaque centralité (attention à l'ordre pour second order centrality!). Les classements sont ils les mêmes?

## Attaque sur l'influence 
* vous allez attaquer ce réseau social pour essayer de gagner de l'influence pour un caractère fictif, le noeud 0. Connectez un noeud 0 à 'Daryn-Hornwood', dans un nouveau graphe Gs

* exécutez une centralité eigenvector centrality sur le graphe attaqué Gs, et affichez le rang de 0 dans le classement de l'influence des noeuds. L'attaque est elle efficace?

* même manipulation, en connectant à la place 0 avec Eddard-Stark dans un graphe G. Le rang de 0 est il meilleur? Pourquoi?

* créez un graphe en étoile de 10 noeuds, avec 0 pour centre. Connectez le à GoT par une arête entre 0 et Eddard-Stark (cf fonction compose)

* quel est le nouveau rang de 0? Différence par rapport à l'attaque simple?

* trouver un exemple de de centralité qui est moins sensible que eigenvector centrality à cette attaque (ie, le rang de 0 est bas)

## Détection de l'attaque

* tester si le sampling à base de marches aléatoires pour détecter les attaques (cf poly) classe les noeuds qui ont servi à l'attaque parmi les plus probablement "faux" de G (ie, quid de leur fréquence d'échantillonnage? Afficher le sampling rate pour 1000 marches aléatoires partant chacune d'un noeud aléatoire de G

Questions/commentaires: erwan.le-merrer@inria.fr
