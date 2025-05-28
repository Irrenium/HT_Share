# Qu'est-ce que HTSIM ?

## Vue d'ensemble

HTSIM est un simulateur d'événements discrets haute performance spécialement conçu pour l'analyse et l'évaluation des algorithmes de contrôle de congestion dans les réseaux informatiques. Contrairement à d'autres simulateurs comme ns2, HTSIM a été optimisé pour offrir des performances supérieures, ce qui permet de modéliser des réseaux plus grands avec des temps de simulation plus courts.

## Historique et Développement

HTSIM a été initialement développé par [Mark Handley](http://www0.cs.ucl.ac.uk/staff/M.Handley/) pour permettre à [Damon Wishik](https://www.cl.cam.ac.uk/~djw1005/) d'étudier les problèmes de stabilité TCP lorsqu'un grand nombre de flux sont multiplexés.

Au fil des ans, le simulateur a été considérablement étendu par différents chercheurs :

- [Costin Raiciu](http://nets.cs.pub.ro/~costin/) a étendu HTSIM pour examiner les performances de [Multipath TCP](http://nets.cs.pub.ro/~costin/files/mptcp-nsdi.pdf) pendant le processus de standardisation de MPTCP.
- Des modèles de réseaux de centres de données ont été ajoutés pour [étudier le transport multichemin](http://nets.cs.pub.ro/~costin/files/mptcp_dc_sigcomm.pdf) dans diverses topologies de centres de données.
- [NDP (Datacenter Protocol)](http://nets.cs.pub.ro/~costin/files/ndp.pdf) a été développé en utilisant HTSIM.
- Des modèles simples de DCTCP (Data Center TCP) et DCQCN (Data Center Quantized Congestion Notification) ont été ajoutés à des fins de comparaison.
- Correct Networks (maintenant partie de Broadcom) a adopté HTSIM pour développer [EQDS](http://nets.cs.pub.ro/~costin/files/eqds.pdf), et les modèles de commutation ont été améliorés pour permettre diverses méthodes de transfert.
- Le support pour un modèle RoCE (RDMA over Converged Ethernet) simple, PFC (Priority Flow Control), Swift et HPCC (High-Precision Congestion Control) a été ajouté.

## Caractéristiques Principales

HTSIM se distingue par plusieurs caractéristiques clés :

- **Hautes performances** : Optimisé pour être beaucoup plus rapide que d'autres simulateurs de réseau.
- **Modularité** : Architecture modulaire permettant l'ajout facile de nouveaux composants et protocoles.
- **Simulation centrée sur le contrôle de congestion** : Spécialement conçu pour étudier et comparer différents algorithmes de contrôle de congestion.
- **Modèles de centre de données** : Support pour différentes topologies de centre de données comme Fat-Tree et autres.
- **Support pour les protocoles modernes** : Capacité à simuler TCP, MPTCP, DCTCP, NDP, RoCE, Swift, HPCC et autres.
- **Aucune dépendance externe** : Écrit en C++ sans dépendances, facilitant l'installation et l'utilisation sur différentes plateformes.

## Domaines d'Application

HTSIM est particulièrement utile pour :

- La recherche académique en réseaux informatiques
- L'évaluation et la comparaison d'algorithmes de contrôle de congestion
- La conception et l'optimisation de topologies de réseau de centre de données
- Le développement et le test de nouveaux protocoles réseau
- L'analyse de performance des réseaux sous différentes charges et conditions

## Avantages par rapport à d'autres simulateurs

- **Vitesse d'exécution** : HTSIM est significativement plus rapide que ns2 et d'autres simulateurs classiques.
- **Spécialisation** : Conçu spécifiquement pour l'analyse des algorithmes de contrôle de congestion.
- **Évolutivité** : Capable de simuler efficacement des réseaux de grande taille.
- **Simplicité d'utilisation** : Moins complexe que certains simulateurs généralistes.
- **Extensibilité** : Architecture permettant d'ajouter facilement de nouveaux composants et fonctionnalités.
