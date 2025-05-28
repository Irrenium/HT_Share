# Fichiers de Configuration dans HTSIM

## Introduction aux Fichiers de Configuration

Dans HTSIM, les fichiers de configuration permettent de définir les paramètres d'une simulation sans avoir à modifier et recompiler le code source. Ces fichiers sont essentiels pour configurer des topologies de réseau complexes, des scénarios de trafic variés et des paramètres de simulation personnalisés.

## Types de Fichiers de Configuration

HTSIM utilise principalement deux types de fichiers de configuration :

1. **Fichiers de matrice de trafic (.tm)** : Définissent les patterns de trafic entre les hôtes
2. **Fichiers de topologie (.topo)** : Spécifient la structure du réseau et les connexions entre les nœuds

## Structure des Fichiers de Matrice de Trafic (.tm)

Les fichiers de matrice de trafic définissent quels hôtes communiquent avec quels autres hôtes et avec quelle intensité. Ils sont utilisés pour simuler différents patterns de communication.

### Format Général

```
# Format: <ID Source> <ID Destination> <Taille du Flux (octets)> [Temps de Démarrage (s)]
# Commentaires commencent par #
0 1 1048576     # Hôte 0 envoie 1MB à Hôte 1
2 3 5242880 0.5 # Hôte 2 envoie 5MB à Hôte 3, démarrant à 0.5 secondes
```

### Exemples de Patterns Courants

#### Pattern All-to-All

```
# Fichier all-to-all.tm
# Chaque hôte envoie à tous les autres hôtes
0 1 1048576
0 2 1048576
0 3 1048576
1 0 1048576
1 2 1048576
1 3 1048576
2 0 1048576
2 1 1048576
2 3 1048576
3 0 1048576
3 1 1048576
3 2 1048576
```

#### Pattern Incast

```
# Fichier incast.tm
# Tous les hôtes envoient à l'hôte 0
1 0 1048576
2 0 1048576
3 0 1048576
4 0 1048576
```

#### Pattern de Permutation

```
# Fichier permutation.tm
# Chaque hôte envoie à un seul autre hôte
0 1 1048576
1 2 1048576
2 3 1048576
3 0 1048576
```

## Structure des Fichiers de Topologie (.topo)

Les fichiers de topologie définissent la structure du réseau, y compris les nœuds (commutateurs, hôtes) et les liens entre eux.

### Format Général

```
# Format de base:
# nodes <nombre de nœuds>
# links <nombre de liens>
# <ID Nœud Source> <ID Nœud Destination> <Latence (µs)> <Bande Passante (Gbps)> <Taille de File d'Attente (paquets)>

nodes 6  # 4 hôtes + 2 commutateurs
links 8

# Connexions Hôte-Switch
0 4 1 10 100  # Hôte 0 à Switch 4: 1µs, 10Gbps, file d'attente de 100 paquets
1 4 1 10 100  # Hôte 1 à Switch 4
2 5 1 10 100  # Hôte 2 à Switch 5
3 5 1 10 100  # Hôte 3 à Switch 5

# Connexion inter-switches (lien backbone)
4 5 5 40 400  # Switch 4 à Switch 5: 5µs, 40Gbps, file d'attente de 400 paquets

# Liens retour
5 4 5 40 400  # Le lien retour pour la bidirectionnalité
4 0 1 10 100
5 2 1 10 100
```

### Formats Spécialisés

#### Topologie Fat-Tree

```
# Format fat-tree:
# fattree <k> (où k est le paramètre de taille du fat-tree)
# <paramètres supplémentaires>

fattree 4
latency 1      # latence de tous les liens en µs
bandwidth 10   # bande passante de tous les liens en Gbps
queuesize 100  # taille des files d'attente en paquets
```

#### Topologie Tore

```
# Format tore:
# torus <dimensions> <taille par dimension>
# <paramètres supplémentaires>

torus 2 4 4    # Tore 2D de taille 4x4
latency 1
bandwidth 10
queuesize 100
```

## Paramètres de Configuration Avancés

En plus des topologies et du trafic, plusieurs autres paramètres peuvent être configurés :

### Paramètres de Protocole

```
# Paramètres TCP
tcp_window 64       # Taille initiale de fenêtre TCP (paquets)
tcp_rtx_timeout 1   # Timeout de retransmission (ms)

# Paramètres DCTCP
dctcp_g 0.0625      # Facteur de filtrage DCTCP
ecn_threshold 32    # Seuil pour le marquage ECN (paquets)

# Paramètres NDP
ndp_pullrate 1      # Rate-limit pour les pulls (pulls par RTT)
ndp_pullqueue 8     # Taille de la file d'attente des pulls (paquets)
```

### Paramètres de Simulation

```
# Durée de la simulation
duration 10         # Durée en secondes

# Paramètres d'échantillonnage
sample_interval 0.1 # Intervalle d'échantillonnage (sec)

# Paramètres de sortie
output_dir ./results     # Dossier pour les fichiers de sortie
output_queue_stats true  # Générer statistiques des files d'attente
output_link_util true    # Générer statistiques d'utilisation des liens
```

## Exemple de Configuration Complète

Voici un exemple complet combinant un fichier de topologie et des paramètres de simulation pour un scénario de test Data Center :

```
# datacenter_test.conf

# Définition de la topologie
fattree 8
latency 0.5
bandwidth 25
queuesize 200

# Paramètres de protocole
tcp_window 128
ecn_threshold 64
dctcp_g 0.0625

# Spécification du trafic
traffic_file workloads/websearch.tm

# Paramètres de simulation
duration 5
sample_interval 0.01

# Options de sortie
output_dir ./results/datacenter_test
output_queue_stats true
output_flow_completion true
output_tcp_cwnd true
```

## Utilisation des Fichiers de Configuration

Pour utiliser un fichier de configuration avec HTSIM, spécifiez-le lors du lancement de la simulation :

```bash
# Utiliser un fichier de matrice de trafic
./htsim_ndp -tm permutation.tm -end 10

# Utiliser un fichier de topologie
./htsim_tcp -topo dumbbell.topo -end 10

# Utiliser les deux
./htsim_dctcp -topo fattree.topo -tm websearch.tm -end 10
```

## Génération Automatique de Fichiers de Configuration

Pour les topologies ou patterns de trafic complexes, HTSIM fournit des scripts permettant de générer automatiquement des fichiers de configuration :

### Script de Génération de Matrice de Trafic

```python
#!/usr/bin/env python3

# Exemple de script pour générer une matrice de trafic all-to-all
import sys

def generate_all_to_all(num_hosts, flow_size):
    with open('all_to_all.tm', 'w') as f:
        for src in range(num_hosts):
            for dst in range(num_hosts):
                if src != dst:  # Ne pas envoyer à soi-même
                    f.write(f"{src} {dst} {flow_size}\n")

if __name__ == "__main__":
    if len(sys.argv) != 3:
        print("Usage: ./generate_tm.py <nombre_hosts> <taille_flux>")
        sys.exit(1)
    
    generate_all_to_all(int(sys.argv[1]), int(sys.argv[2]))
    print("Fichier de matrice de trafic généré: all_to_all.tm")
```

### Script de Génération de Topologie

```python
#!/usr/bin/env python3

# Exemple de script pour générer une topologie fat-tree
import sys

def generate_fattree(k):
    num_pods = k
    num_core = (k//2)**2
    num_agg = num_pods * (k//2)
    num_edge = num_pods * (k//2)
    num_hosts = num_pods * (k//2) * (k//2)
    
    with open('fattree.topo', 'w') as f:
        f.write(f"nodes {num_hosts + num_core + num_agg + num_edge}\n")
        
        # Calculer le nombre total de liens
        num_links = num_hosts  # Hôtes vers edge
        num_links += num_edge * (k//2)  # Edge vers agg
        num_links += num_agg * (k//2)  # Agg vers core
        
        f.write(f"links {num_links * 2}\n")  # *2 pour les liens bidirectionnels
        
        # Générer les liens...
        # (détails omis pour la concision)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: ./generate_topo.py <k>")
        sys.exit(1)
    
    generate_fattree(int(sys.argv[1]))
    print("Fichier de topologie généré: fattree.topo")
```

## Bonnes Pratiques

1. **Nommage Clair** : Utilisez des noms descriptifs pour vos fichiers de configuration
2. **Commentaires** : Documentez vos fichiers avec des commentaires
3. **Paramétrage** : Placez les paramètres variables en début de fichier pour faciliter les modifications
4. **Organisation** : Utilisez des répertoires séparés pour les topologies et les matrices de trafic
5. **Contrôle de Version** : Gérez vos fichiers de configuration avec un système de contrôle de version

## Dépannage

### Problèmes Courants et Solutions

| Problème | Cause Possible | Solution |
|----------|----------------|----------|
| "Cannot open file" | Chemin de fichier incorrect | Vérifiez le chemin et les permissions du fichier |
| "Invalid format in line X" | Erreur de syntaxe | Vérifiez la syntaxe de la ligne indiquée |
| "Node ID out of range" | ID de nœud invalide | Assurez-vous que tous les IDs sont dans l'intervalle valide |
| "Duplicate link" | Lien défini deux fois | Supprimez la définition en double |

### Validation de Fichier

Avant d'exécuter une simulation longue, validez vos fichiers de configuration :

```bash
# Outil de validation (si disponible)
./validate_config.py myconfig.topo

# Ou utilisez le mode "dry-run" de HTSIM
./htsim_ndp -topo myconfig.topo -tm mytraffic.tm -dryrun
```
