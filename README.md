#importation des bibliothèques
import networkx as nx
from File import *

def recherche_dfs(labyrinthe: nx.Graph, source: int = None, destination: int = None):
    """ Effectue une recherche en profondeur dans le labyrinthe pour trouver le chemin le plus court
        entre les sommets source et destination.
    """
    # Initialisation des sommets source et destination s'ils ne sont pas renseignés
    nodes = list(labyrinthe.nodes())
    if source is None:
        source = nodes[0]
    if destination is None:
        destination = nodes[-1]

    # Utilise le parcours DFS pour visiter les sommets
    visited = set()

    stack = [source]

    while stack:
        node_actuel = stack.pop()
        if node_actuel not in visited:
            print(f"Visite du sommet {node_actuel}")
            visited.add(node_actuel)

            # Si on atteint la destination, effectue l'action ici au lieu du return
            if node_actuel == destination:
                print("Destination atteinte ! Faire quelque chose ici.")
                break

            # Empile les voisins non visités
            stack.extend(neighbor for neighbor in labyrinthe.neighbors(node_actuel) if neighbor not in visited)

if __name__ == "__main__":
    # Création du labyrinthe de test
    aretes = [(0, 1), (0, 4), (1, 0), (1, 5), (2, 6), (3, 7), (4, 0), (4, 5), (5, 1) , \
     (5, 4), (5, 6), (5, 9), (6, 2), (6, 5), (6, 7), (6, 10), (7, 3), (7, 6), (8, 9),\
     (9, 5), (9, 8), (9, 10), (10, 6), (10, 9), (10, 11), (11, 10)]
    colonnes = 4
    lignes = 3
    nb_sommets = colonnes * lignes
    noeuds = list(range(nb_sommets))
    Labyrinthe = nx.Graph()
    Labyrinthe.add_nodes_from(noeuds)
    Labyrinthe.add_edges_from(aretes)

    # Lance le test de la fonction afficher_labyrinthe()
    #afficher_labyrinthe(Labyrinthe, colonnes, lignes)
    chemin_dfs =recherche_dfs(Labyrinthe)
    print(chemin_dfs)
