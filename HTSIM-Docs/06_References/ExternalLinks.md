# Liens Externes

Cette page rassemble des ressources externes utiles pour approfondir votre compréhension de HTSIM et des concepts associés à la simulation réseau, au contrôle de congestion et aux architectures de réseau.

## Ressources Officielles HTSIM

### Documentation et Code Source

- [Dépôt GitHub HTSIM](https://github.com/Broadcom/csg-htsim) - Code source officiel et documentation de base
- [Wiki HTSIM](https://github.com/Broadcom/csg-htsim/wiki) - Documentation collaborative et guides d'utilisation

## Publications Académiques Utilisant HTSIM

### Papiers Fondamentaux

- [NDP: Re-architecting Datacenter Networks and Stacks for Low Latency and High Performance](http://nets.cs.pub.ro/~costin/files/ndp.pdf) - Papier introduisant NDP, développé à l'aide de HTSIM
- [Enabling End-host Network Functions](http://nets.cs.pub.ro/~costin/files/eqds.pdf) - Présentation de EQDS, également développé avec HTSIM
- [Multipath TCP: From Theory to Practice](http://nets.cs.pub.ro/~costin/files/mptcp-nsdi.pdf) - Recherche sur MPTCP utilisant HTSIM
- [Improving Datacenter Performance and Robustness with Multipath TCP](http://nets.cs.pub.ro/~costin/files/mptcp_dc_sigcomm.pdf) - Évaluation de MPTCP dans les environnements de centre de données

### Recherches Récentes

- [HPCC: High Precision Congestion Control](https://www.microsoft.com/en-us/research/uploads/prod/2019/03/hpcc.pdf) - Présentation de HPCC, un algorithme de contrôle de congestion haute précision
- [Swift: Delay is Simple and Effective for Congestion Control in the Datacenter](https://dl.acm.org/doi/pdf/10.1145/3387514.3406591) - Introduction au protocole Swift étudié avec HTSIM

## Concepts de Simulation Réseau

### Simulation à Événements Discrets

- [Introduction à la Simulation à Événements Discrets](https://www.sciencedirect.com/topics/computer-science/discrete-event-simulation) - Principes fondamentaux de la simulation à événements discrets
- [Discrete-Event System Simulation](https://www.pearson.com/en-us/subject-catalog/p/discrete-event-system-simulation/P200000003546) - Livre de référence sur la simulation à événements discrets

### Autres Simulateurs Réseau

- [ns-3](https://www.nsnam.org/) - Simulateur réseau à événements discrets populaire, successeur de ns-2
- [OMNeT++](https://omnetpp.org/) - Framework de simulation extensible pour les réseaux
- [Mininet](http://mininet.org/) - Émulateur réseau qui crée un réseau virtuel sur une seule machine

## Contrôle de Congestion et Protocoles Réseau

### Contrôle de Congestion TCP

- [TCP Congestion Control: A Systems Approach](https://tcpcc.systemsapproach.org/) - Guide complet sur le contrôle de congestion TCP
- [RFC 5681: TCP Congestion Control](https://datatracker.ietf.org/doc/html/rfc5681) - Spécification officielle du contrôle de congestion TCP

### Protocoles Avancés

- [DCTCP: Data Center TCP](https://dl.acm.org/doi/10.1145/1851182.1851192) - Article original sur DCTCP
- [RFC 8684: TCP Extensions for Multipath Operation with Multiple Addresses](https://datatracker.ietf.org/doc/html/rfc8684) - Spécification de MPTCP
- [RDMA over Converged Ethernet (RoCE)](https://www.ibm.com/docs/en/spectrum-scale/5.1.3?topic=considerations-rdma-over-converged-ethernet-roce) - Introduction à RoCE

## Architectures de Réseau

### Topologies de Centre de Données

- [A Scalable, Commodity Data Center Network Architecture](https://dl.acm.org/doi/10.1145/1402958.1402967) - Article fondateur sur la topologie Fat-Tree
- [VL2: A Scalable and Flexible Data Center Network](https://dl.acm.org/doi/10.1145/1594977.1592576) - Alternative à Fat-Tree pour les centres de données
- [Jupiter Rising: A Decade of Clos Topologies and Centralized Control in Google's Datacenter Network](https://dl.acm.org/doi/10.1145/2785956.2787508) - Évolution des architectures réseau chez Google

### Réseaux Haute Performance

- [InfiniBand Architecture Specification](https://www.infinibandta.org/ibta-specification/) - Spécification de l'architecture InfiniBand
- [IEEE 802.1Qbb - Priority-based Flow Control](https://www.ieee802.org/1/pages/802.1bb.html) - Standard PFC pour les réseaux sans perte

## Outils d'Analyse et Visualisation

### Analyse de Données

- [Python Data Analysis Library (pandas)](https://pandas.pydata.org/) - Bibliothèque Python pour l'analyse de données
- [NumPy](https://numpy.org/) - Bibliothèque fondamentale pour le calcul scientifique en Python

### Visualisation

- [Matplotlib](https://matplotlib.org/) - Bibliothèque de visualisation Python
- [Gnuplot](http://www.gnuplot.info/) - Outil de traçage de graphiques en ligne de commande
- [Wireshark](https://www.wireshark.org/) - Analyseur de protocole réseau

## Cours et Tutoriels

### Réseaux Informatiques

- [Computer Networking: Principles, Protocols and Practice](https://www.computer-networking.info/) - Livre en ligne sur les réseaux informatiques
- [Stanford CS144: Introduction to Computer Networking](https://cs144.github.io/) - Cours de Stanford sur les fondamentaux des réseaux

### Contrôle de Congestion

- [A Gentle Introduction to Congestion Control](https://www.cse.wustl.edu/~jain/ ATM/ftp/congestion.pdf) - Introduction au contrôle de congestion par Raj Jain
- [Congestion Control in the RFC Series](https://datatracker.ietf.org/doc/html/draft-ietf-tcpm-rfc8312bis-00) - Vue d'ensemble des approches de contrôle de congestion

## Communauté et Forums

### Groupes de Discussion

- [IETF TCPM Working Group](https://datatracker.ietf.org/wg/tcpm/about/) - Groupe de travail sur TCP Maintenance and Minor Extensions
- [P4 Language Consortium](https://p4.org/) - Communauté autour de la programmation des plans de données réseau

### Forums et Listes de Diffusion

- [Stack Overflow - Networking](https://stackoverflow.com/questions/tagged/networking) - Questions et réponses sur les réseaux
- [Network Engineering Stack Exchange](https://networkengineering.stackexchange.com/) - Q&R pour les professionnels des réseaux

## Entreprises et Projets Associés

### Entreprises

- [Broadcom](https://www.broadcom.com/) - Entreprise associée au développement de HTSIM
- [Correct Networks](https://correctnetworks.com/) - A contribué au développement de HTSIM (maintenant partie de Broadcom)

### Projets de Recherche

- [Fastpass: A Centralized "Zero-Queue" Datacenter Network](https://dl.acm.org/doi/10.1145/2740070.2626309) - Approche alternative pour le contrôle de congestion
- [HULL: High-bandwidth Ultra-Low Latency](https://dl.acm.org/doi/10.1145/2228298.2228315) - Architecture pour minimiser la latence dans les centres de données

## Comment Contribuer

Si vous souhaitez ajouter des liens à cette page ou contribuer au développement de HTSIM :

1. **Contributions à la documentation** : Créez une pull request sur le dépôt GitHub de HTSIM
2. **Partage de recherche** : Si vous avez utilisé HTSIM dans votre recherche, partagez vos résultats et méthodologies
3. **Extensions et améliorations** : Développez de nouveaux composants ou améliorez les existants

## Maintenir cette Liste

Cette liste de ressources est maintenue par la communauté HTSIM. Si vous trouvez des liens brisés ou souhaitez suggérer de nouvelles ressources pertinentes, veuillez contacter les mainteneurs du projet ou créer une issue sur le dépôt GitHub.
