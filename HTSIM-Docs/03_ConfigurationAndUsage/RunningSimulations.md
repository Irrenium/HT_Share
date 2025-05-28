# Exécution des Simulations avec HTSIM

## Introduction à l'Exécution des Simulations

HTSIM offre un environnement flexible pour exécuter des simulations de réseaux informatiques. Cette section explique comment lancer des simulations, configure les paramètres d'exécution et gérer efficacement les processus de simulation.

## Structure de Base d'une Commande HTSIM

Une commande typique d'exécution de HTSIM suit cette structure générale :

```bash
./htsim_[variante] [options de topologie] [options de trafic] [options de protocole] [options de simulation]
```

Où `[variante]` peut être `ndp`, `tcp`, `dctcp`, `roce`, etc., selon le protocole principal que vous souhaitez utiliser.

## Options de Commande Principales

### Options de Topologie

| Option | Description | Exemple |
|--------|-------------|---------|
| `-topo <fichier>` | Spécifie un fichier de topologie | `-topo fat_tree_k4.topo` |
| `-tm <fichier>` | Spécifie un fichier de matrice de trafic | `-tm all_to_all.tm` |
| `-linkspeed <vitesse>` | Définit la vitesse des liens en Mbps | `-linkspeed 10000` (10 Gbps) |
| `-nodes <nombre>` | Définit le nombre de nœuds pour les topologies générées automatiquement | `-nodes 64` |

### Options de Protocole

| Option | Description | Exemple |
|--------|-------------|---------|
| `-q <taille>` | Taille des files d'attente (en paquets) | `-q 100` |
| `-cwnd <taille>` | Taille initiale de fenêtre TCP/NDP (en paquets) | `-cwnd 15` |
| `-mtu <taille>` | Taille maximale des unités de transmission (en octets) | `-mtu 1500` |
| `-ecn <seuil>` | Seuil pour le marquage ECN | `-ecn 32` |

### Options de Contrôle de Simulation

| Option | Description | Exemple |
|--------|-------------|---------|
| `-end <temps>` | Durée totale de la simulation (en secondes) | `-end 10` |
| `-o <préfixe>` | Préfixe pour les fichiers de sortie | `-o resultat_sim1` |
| `-seed <valeur>` | Graine pour le générateur de nombres aléatoires | `-seed 12345` |
| `-sample <interval>` | Intervalle d'échantillonnage pour les statistiques (en secondes) | `-sample 0.1` |

## Exemples de Commandes

### Simulation d'un Réseau Dumbbell avec TCP

```bash
./htsim_tcp -topo dumbbell.topo -q 100 -cwnd 10 -end 5 -o tcp_dumbbell
```

Cette commande simule un réseau dumbbell utilisant TCP, avec des files d'attente de 100 paquets, une fenêtre de congestion initiale de 10, pour une durée de 5 secondes.

### Simulation Fat-Tree avec NDP

```bash
./htsim_ndp -tm all_to_all.tm -nodes 128 -conns 64 -q 8 -cwnd 15 -strat perm -end 2 -o ndp_fattree
```

Cette commande simule une topologie Fat-Tree avec 128 nœuds utilisant le protocole NDP, avec des files d'attente de 8 paquets et une fenêtre de congestion de 15.

### Simulation DCTCP dans un Centre de Données

```bash
./htsim_dctcp -tm websearch.tm -nodes 432 -conns 432 -ssthresh 15 -q 100 -o dctcp_websearch
```

Cette commande simule le comportement de DCTCP avec un modèle de trafic de recherche web dans un centre de données de 432 nœuds.

## Exécution de Batch de Simulations

Pour exécuter plusieurs simulations dans un batch, vous pouvez créer un script shell :

```bash
#!/bin/bash

# Exécuter des simulations avec différentes tailles de file d'attente
for q in 8 16 32 64 128; do
    echo "Exécution de simulation avec q=$q"
    ./htsim_ndp -tm all_to_all.tm -nodes 64 -conns 64 -q $q -cwnd 15 -end 2 -o ndp_q${q}
done

# Attendre que toutes les simulations se terminent
wait

echo "Toutes les simulations sont terminées"
```

## Exécution de Simulations en Parallèle

Pour les simulations longues ou nombreuses, vous pouvez utiliser l'exécution en parallèle :

```bash
#!/bin/bash

# Fonction pour exécuter une simulation
run_sim() {
    local q=$1
    local cwnd=$2
    echo "Démarrage de simulation avec q=$q, cwnd=$cwnd"
    ./htsim_ndp -tm all_to_all.tm -nodes 64 -q $q -cwnd $cwnd -end 2 -o ndp_q${q}_cwnd${cwnd} &
}

# Exécuter différentes configurations en parallèle
run_sim 8 10
run_sim 8 20
run_sim 16 10
run_sim 16 20

# Attendre la fin de toutes les simulations
wait

echo "Toutes les simulations sont terminées"
```

## Surveillance des Simulations en Cours

### Surveillance de la Progression

HTSIM affiche généralement la progression de la simulation sur la sortie standard. Vous pouvez rediriger cette sortie vers un fichier pour la consulter ultérieurement :

```bash
./htsim_ndp -tm all_to_all.tm -nodes 64 -q 8 -cwnd 15 -end 10 -o ndp_test > progression.log
```

Pour consulter la progression en temps réel :

```bash
tail -f progression.log
```

### Interruption Propre d'une Simulation

Pour interrompre proprement une simulation en cours, envoyez un signal SIGINT (Ctrl+C) :

```bash
# Pour interrompre une simulation spécifique par PID
kill -SIGINT <pid_de_la_simulation>
```

Cela permet à HTSIM de terminer proprement, d'enregistrer les résultats partiels et de libérer les ressources.

## Gestion des Ressources

### Estimation des Besoins en Mémoire

La mémoire requise par une simulation HTSIM dépend principalement de :
- Nombre de nœuds et de liens dans la topologie
- Nombre de flux simultanés
- Taille des files d'attente
- Durée de la simulation

Une estimation approximative peut être calculée comme suit :

```
Mémoire (MB) ≈ (Nœuds × 0.1) + (Liens × 0.05) + (Flux × 0.2) + (Taille_Queue_Totale × 0.001)
```

### Optimisation des Ressources

Pour optimiser l'utilisation des ressources lors de simulations complexes :

1. **Limitez la durée** : Commencez par de courtes simulations pour valider la configuration
2. **Échantillonnage adapté** : Réduisez la fréquence d'échantillonnage pour les longues simulations
3. **Exécution par étapes** : Divisez les longues simulations en étapes plus courtes
4. **Filtrage des résultats** : Collectez uniquement les métriques nécessaires

## Automatisation des Simulations

### Script d'Automatisation Complet

Voici un exemple de script d'automatisation plus complet pour exécuter une étude paramétrique :

```bash
#!/bin/bash

# Configuration de base
NODES=128
BASE_CMD="./htsim_ndp -nodes $NODES"
OUTPUT_DIR="./resultats_$(date +%Y%m%d_%H%M)"

# Créer le répertoire de sortie
mkdir -p $OUTPUT_DIR

# Fichier journal principal
MAIN_LOG="$OUTPUT_DIR/main.log"

# Fonction pour exécuter une simulation
run_simulation() {
    local q=$1
    local cwnd=$2
    local strat=$3
    local output="$OUTPUT_DIR/ndp_q${q}_cwnd${cwnd}_${strat}"
    
    echo "$(date): Démarrage simulation - q=$q cwnd=$cwnd strat=$strat" >> $MAIN_LOG
    
    $BASE_CMD -q $q -cwnd $cwnd -strat $strat -end 5 -o $output > $output.log 2>&1
    
    local status=$?
    if [ $status -eq 0 ]; then
        echo "$(date): Simulation terminée avec succès - q=$q cwnd=$cwnd strat=$strat" >> $MAIN_LOG
    else
        echo "$(date): ERREUR dans simulation - q=$q cwnd=$cwnd strat=$strat" >> $MAIN_LOG
    fi
    
    return $status
}

# Exécuter les simulations
for q in 8 16 32; do
    for cwnd in 10 15 20; do
        for strat in perm pull; do
            run_simulation $q $cwnd $strat
        done
    done
done

echo "$(date): Toutes les simulations sont terminées" >> $MAIN_LOG
```

### Intégration avec des Outils d'Analyse

Pour automatiser l'analyse post-simulation :

```bash
#!/bin/bash

# Exécuter une simulation
./htsim_ndp -tm all_to_all.tm -nodes 64 -q 8 -cwnd 15 -end 5 -o ndp_test

# Analyser les résultats avec l'outil parse_output
./parse_output ndp_test > ndp_test_parsed.txt

# Générer des graphiques avec gnuplot
gnuplot <<EOF
set terminal png
set output "ndp_test_throughput.png"
set title "Débit NDP"
set xlabel "Temps (s)"
set ylabel "Débit (Mbps)"
plot "ndp_test_parsed.txt" using 1:2 with lines title "Débit"
EOF

echo "Simulation et analyse terminées. Graphiques générés."
```

## Résolution des Problèmes

### Problèmes Courants et Solutions

| Problème | Symptômes | Solutions Possibles |
|----------|-----------|---------------------|
| Simulation trop lente | Progression lente, utilisation CPU élevée | Réduire la taille du réseau, optimiser la compilation |
| Erreurs de mémoire | Crash avec "out of memory" | Réduire la taille des files d'attente, utiliser moins de flux |
| Résultats incohérents | Variances inexplicables entre exécutions | Vérifier la graine aléatoire, fixer `-seed` |
| Blocage de simulation | La simulation semble figée | Vérifier les boucles infinies potentielles, événements bloquants |

### Debugging

Pour le débogage avancé d'une simulation HTSIM :

```bash
# Compiler avec les symboles de débogage
make clean
make CFLAGS="-g -O0"

# Exécuter avec un débogueur
gdb --args ./htsim_ndp -tm all_to_all.tm -nodes 16 -q 8 -cwnd 15 -end 1

# Dans gdb
(gdb) run
# Quand le programme se plante
(gdb) backtrace
```

## Bonnes Pratiques

1. **Validation progressive** : Commencez par des simulations simples et augmentez progressivement la complexité
2. **Contrôle de version** : Gardez une trace des changements apportés aux paramètres et au code
3. **Documentation** : Documentez soigneusement toutes les simulations (paramètres, objectifs, observations)
4. **Reproductibilité** : Utilisez des graines fixes pour les générateurs de nombres aléatoires
5. **Sauvegardes** : Sauvegardez régulièrement les résultats importants

## Scripts Utilitaires

### Script pour Nettoyer les Fichiers de Sortie

```bash
#!/bin/bash

# Nettoyer les fichiers de sortie plus anciens qu'un nombre de jours spécifié
clean_outputs() {
    local days=$1
    local pattern=$2
    
    echo "Suppression des fichiers $pattern plus anciens que $days jours..."
    find . -name "$pattern" -type f -mtime +$days -exec rm {} \;
}

# Nettoyer les fichiers de sortie de plus d'une semaine
clean_outputs 7 "*.log"
clean_outputs 7 "*.out"

echo "Nettoyage terminé."
```

### Script pour Résumer les Résultats

```bash
#!/bin/bash

# Résumer les résultats de plusieurs simulations
summarize_results() {
    local pattern=$1
    local output=$2
    
    echo "Résumé des résultats dans $pattern..."
    
    # En-tête du fichier résumé
    echo "Fichier,Débit Moyen,Latence Moyenne,Pertes" > $output
    
    # Traiter chaque fichier de résultat
    for f in $pattern; do
        if [ -f "$f" ]; then
            # Extraire les métriques principales (exemple simpliste)
            local throughput=$(grep "THROUGHPUT" $f | awk '{sum+=$2} END {print sum/NR}')
            local latency=$(grep "LATENCY" $f | awk '{sum+=$2} END {print sum/NR}')
            local loss=$(grep "PACKET_LOSS" $f | awk '{sum+=$2} END {print sum/NR}')
            
            echo "$f,$throughput,$latency,$loss" >> $output
        fi
    done
}

# Résumer tous les résultats NDP
summarize_results "ndp_*.out" "resume_ndp.csv"
```
