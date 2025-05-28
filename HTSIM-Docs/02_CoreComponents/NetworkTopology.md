# Topologie de Réseau dans HTSIM

## Vue d'ensemble

La topologie de réseau définit comment les différents composants réseau (hôtes, commutateurs, routeurs) sont interconnectés dans une simulation HTSIM. La conception de la topologie est cruciale car elle détermine les chemins disponibles pour le trafic et influence directement les performances globales du réseau simulé.

## Concepts Fondamentaux

Une topologie dans HTSIM est construite en connectant des commutateurs, des hôtes et des liens (pipes) dans une configuration spécifique. Chaque topologie présente des caractéristiques distinctes qui la rendent adaptée à certains scénarios de simulation.

## Principales Topologies Prises en Charge

### Topologie Dumbbell (Haltère)

```mermaid
graph LR
    subgraph Sources
    S1[Hôte S1]
    S2[Hôte S2]
    S3[Hôte S3]
    end
    
    subgraph Destinations
    D1[Hôte D1]
    D2[Hôte D2]
    D3[Hôte D3]
    end
    
    SW1[Switch 1] --- SW2[Switch 2]
    
    S1 --- SW1
    S2 --- SW1
    S3 --- SW1
    
    SW2 --- D1
    SW2 --- D2
    SW2 --- D3
    
    style SW1 fill:#f9f,stroke:#333,stroke-width:2px
    style SW2 fill:#f9f,stroke:#333,stroke-width:2px
```

La topologie dumbbell est principalement utilisée pour étudier les goulots d'étranglement dans les réseaux. Elle consiste en deux groupes d'hôtes connectés par un lien central, créant un point de congestion naturel.

**Caractéristiques clés :**
- Un seul chemin entre chaque source et destination
- Congestion concentrée sur le lien central
- Utile pour tester le comportement des algorithmes de contrôle de congestion

### Topologie Fat-Tree

```mermaid
graph TD
    C1[Core 1] --- A1[Agrégation 1]
    C1 --- A2[Agrégation 2]
    C2[Core 2] --- A1
    C2 --- A2
    
    A1 --- E1[Edge 1]
    A1 --- E2[Edge 2]
    A2 --- E3[Edge 3]
    A2 --- E4[Edge 4]
    
    E1 --- H1[Hôte 1]
    E1 --- H2[Hôte 2]
    E2 --- H3[Hôte 3]
    E2 --- H4[Hôte 4]
    E3 --- H5[Hôte 5]
    E3 --- H6[Hôte 6]
    E4 --- H7[Hôte 7]
    E4 --- H8[Hôte 8]
    
    style C1 fill:#f9f,stroke:#333,stroke-width:2px
    style C2 fill:#f9f,stroke:#333,stroke-width:2px
    style A1 fill:#bbf,stroke:#333,stroke-width:2px
    style A2 fill:#bbf,stroke:#333,stroke-width:2px
    style E1 fill:#bfb,stroke:#333,stroke-width:2px
    style E2 fill:#bfb,stroke:#333,stroke-width:2px
    style E3 fill:#bfb,stroke:#333,stroke-width:2px
    style E4 fill:#bfb,stroke:#333,stroke-width:2px
```

La topologie Fat-Tree est couramment utilisée dans les centres de données modernes. Elle offre une bande passante uniforme entre n'importe quelle paire d'hôtes et une excellente évolutivité.

**Caractéristiques clés :**
- Structure hiérarchique à trois niveaux (core, agrégation, edge)
- Plusieurs chemins entre chaque paire d'hôtes
- Aucun goulot d'étranglement de sursouscription (dans sa forme pure)
- Excellente tolérance aux pannes

### Topologie Leaf-Spine

```mermaid
graph TD
    S1[Spine 1] --- L1[Leaf 1]
    S1 --- L2[Leaf 2]
    S1 --- L3[Leaf 3]
    S2[Spine 2] --- L1
    S2 --- L2
    S2 --- L3
    
    L1 --- H1[Hôte 1]
    L1 --- H2[Hôte 2]
    L2 --- H3[Hôte 3]
    L2 --- H4[Hôte 4]
    L3 --- H5[Hôte 5]
    L3 --- H6[Hôte 6]
    
    style S1 fill:#f9f,stroke:#333,stroke-width:2px
    style S2 fill:#f9f,stroke:#333,stroke-width:2px
    style L1 fill:#bbf,stroke:#333,stroke-width:2px
    style L2 fill:#bbf,stroke:#333,stroke-width:2px
    style L3 fill:#bbf,stroke:#333,stroke-width:2px
```

La topologie Leaf-Spine est une architecture à deux niveaux populaire dans les centres de données modernes, offrant une faible latence et une haute bande passante.

**Caractéristiques clés :**
- Architecture à deux niveaux (spine et leaf)
- Chaque leaf est connecté à chaque spine
- Distance constante entre les hôtes (3 sauts maximum)
- Facilement extensible en ajoutant des commutateurs spine ou leaf

### Topologie en Tore

```mermaid
graph TD
    N1[Nœud 1] --- N2[Nœud 2] --- N3[Nœud 3] --- N4[Nœud 4] --- N1
    N5[Nœud 5] --- N6[Nœud 6] --- N7[Nœud 7] --- N8[Nœud 8] --- N5
    N9[Nœud 9] --- N10[Nœud 10] --- N11[Nœud 11] --- N12[Nœud 12] --- N9
    N13[Nœud 13] --- N14[Nœud 14] --- N15[Nœud 15] --- N16[Nœud 16] --- N13
    
    N1 --- N5 --- N9 --- N13 --- N1
    N2 --- N6 --- N10 --- N14 --- N2
    N3 --- N7 --- N11 --- N15 --- N3
    N4 --- N8 --- N12 --- N16 --- N4
    
    style N1 fill:#bbf,stroke:#333,stroke-width:2px
    style N2 fill:#bbf,stroke:#333,stroke-width:2px
    style N3 fill:#bbf,stroke:#333,stroke-width:2px
    style N4 fill:#bbf,stroke:#333,stroke-width:2px
    style N5 fill:#bbf,stroke:#333,stroke-width:2px
    style N6 fill:#bbf,stroke:#333,stroke-width:2px
    style N7 fill:#bbf,stroke:#333,stroke-width:2px
    style N8 fill:#bbf,stroke:#333,stroke-width:2px
    style N9 fill:#bbf,stroke:#333,stroke-width:2px
    style N10 fill:#bbf,stroke:#333,stroke-width:2px
    style N11 fill:#bbf,stroke:#333,stroke-width:2px
    style N12 fill:#bbf,stroke:#333,stroke-width:2px
    style N13 fill:#bbf,stroke:#333,stroke-width:2px
    style N14 fill:#bbf,stroke:#333,stroke-width:2px
    style N15 fill:#bbf,stroke:#333,stroke-width:2px
    style N16 fill:#bbf,stroke:#333,stroke-width:2px
```

La topologie en tore est couramment utilisée dans les supercalculateurs et les environnements HPC (High-Performance Computing).

**Caractéristiques clés :**
- Structure en maille où les bords sont connectés pour former un tore
- Chemins multiples entre les nœuds
- Bonne évolutivité pour les applications HPC
- Routage simple et symétrique

## Comparaison des Topologies

| Topologie | Nombre de Sauts (Max) | Tolérance aux Pannes | Évolutivité | Cas d'Utilisation Typiques |
|-----------|----------------------|---------------------|-------------|---------------------------|
| Dumbbell | 3 | Faible | Faible | Tests de congestion, évaluation de TCP |
| Fat-Tree | log₄(n) | Excellente | Bonne | Centres de données à grande échelle |
| Leaf-Spine | 3 | Bonne | Moyenne | Centres de données de taille moyenne |
| Tore | √n | Excellente | Excellente | Clusters HPC, supercalculateurs |

## Création de Topologies dans HTSIM

Pour créer une topologie dans HTSIM, le processus général est le suivant :

1. Définir les nœuds (commutateurs et hôtes)
2. Créer les liens (pipes) entre les nœuds
3. Configurer les tables de routage
4. Définir les sources de trafic

### Exemple de Code pour une Topologie Dumbbell

```cpp
// Créer les commutateurs
Switch* sw1 = new Switch(4);  // 4 ports
Switch* sw2 = new Switch(4);  // 4 ports

// Créer les hôtes (sources et destinations)
for (int i = 0; i < 3; i++) {
    // Créer les hôtes sources
    TCPSrc* src = new TCPSrc(...);
    
    // Créer les files d'attente des hôtes sources
    Queue* src_queue = new Queue(hostSpeed, queueSize);
    src_queue->setDestination(sw1, i);
    
    // Créer les hôtes destinations
    TCPSink* dst = new TCPSink(...);
    
    // Créer les files d'attente des hôtes destinations
    Queue* dst_queue = new Queue(hostSpeed, queueSize);
    dst_queue->setDestination(dst);
    
    // Connecter les commutateurs aux hôtes destinations
    Pipe* pipe_sw2_dst = new Pipe(linkDelay, hostSpeed);
    pipe_sw2_dst->setDestination(dst_queue);
    sw2->setQueue(i, pipe_sw2_dst);
}

// Créer le lien du goulot d'étranglement entre les commutateurs
Queue* sw1_queue = new Queue(bottleneckSpeed, bottleneckQueueSize);
Pipe* pipe_sw1_sw2 = new Pipe(bottleneckDelay, bottleneckSpeed);
pipe_sw1_sw2->setDestination(sw2, 3);  // Connecter au port 3 de sw2
sw1_queue->setDestination(pipe_sw1_sw2);
sw1->setQueue(3, sw1_queue);  // Configurer le port 3 de sw1
```

### Exemple de Code pour une Topologie Fat-Tree

```cpp
// Paramètres de configuration
int k = 4;  // Nombre de pods (la taille du fat-tree est k^3/4 hôtes)
int numCores = k*k/4;
int numAggs = k*k/2;
int numEdges = k*k/2;
int numHosts = k*k*k/4;

// Créer les commutateurs core
vector<Switch*> coreSwitches(numCores);
for (int i = 0; i < numCores; i++) {
    coreSwitches[i] = new Switch(k);
}

// Créer les commutateurs d'agrégation
vector<Switch*> aggSwitches(numAggs);
for (int i = 0; i < numAggs; i++) {
    aggSwitches[i] = new Switch(k);
}

// Créer les commutateurs edge
vector<Switch*> edgeSwitches(numEdges);
for (int i = 0; i < numEdges; i++) {
    edgeSwitches[i] = new Switch(k);
}

// Créer les connexions...
// (Suite du code pour créer toutes les connexions et configurer le routage)
```

## Patrons de Trafic Courants

Pour évaluer le comportement du réseau sous différentes charges, HTSIM prend en charge divers patrons de trafic :

### All-to-All
Chaque hôte communique avec tous les autres hôtes, créant un trafic dense à travers la topologie.

### Permutation
Chaque hôte envoie du trafic à un seul autre hôte, créant un mappage un-à-un.

### Incast
De nombreux hôtes envoient simultanément du trafic à un seul hôte, créant un point chaud.

### Hot-Spot
Un ou plusieurs nœuds reçoivent significativement plus de trafic que les autres.

## Considérations pour la Conception de Topologies

Lors de la conception d'une topologie pour une simulation HTSIM, plusieurs facteurs doivent être pris en compte :

- **Objectif de la simulation** : Différentes topologies sont adaptées à différents scénarios de test
- **Échelle** : Certaines topologies sont plus efficaces à grande échelle
- **Routage** : La complexité du routage varie selon la topologie
- **Tolérance aux pannes** : Certaines topologies offrent une meilleure résilience
- **Équilibre de charge** : La capacité à distribuer le trafic uniformément

## Outils d'Analyse de Topologie

HTSIM fournit plusieurs outils pour analyser les propriétés des topologies de réseau :

- Calcul du diamètre du réseau (nombre maximum de sauts)
- Évaluation du nombre de chemins alternatifs
- Analyse des goulots d'étranglement potentiels
- Visualisation de la topologie et du flux de trafic

## Bonnes Pratiques

- **Commencer simple** : Débuter avec des topologies simples pour comprendre le comportement de base
- **Isoler les variables** : Modifier un seul aspect de la topologie à la fois pour des comparaisons significatives
- **Vérifier la connectivité** : S'assurer que tous les nœuds sont correctement connectés
- **Valider le routage** : Confirmer que les tables de routage sont correctement configurées
- **Tester la résilience** : Simuler des pannes pour évaluer la robustesse de la topologie
