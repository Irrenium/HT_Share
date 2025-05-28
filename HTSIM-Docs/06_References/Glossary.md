# Glossaire

Ce glossaire définit les termes techniques et les acronymes utilisés dans la documentation de HTSIM et dans le domaine de la simulation réseau en général.

## A

### ACK (Acknowledgement)
Paquet envoyé par le destinataire pour confirmer la réception réussie d'un paquet de données. Utilisé par TCP et d'autres protocoles pour assurer la fiabilité.

### AIMD (Additive Increase, Multiplicative Decrease)
Algorithme utilisé par TCP pour le contrôle de congestion. Augmente linéairement la fenêtre de congestion en l'absence de perte et la diminue de façon multiplicative (généralement par un facteur de 0,5) lors de la détection d'une perte.

### All-to-All
Motif de trafic où chaque nœud du réseau communique avec tous les autres nœuds, créant une matrice complète de flux.

## B

### Bande Passante (Bandwidth)
Quantité maximale de données pouvant être transmises sur un lien réseau par unité de temps, généralement exprimée en bits par seconde (bps) ou multiples (Kbps, Mbps, Gbps).

### Bufferbloat
Phénomène où des tampons (buffers) excessivement grands dans les équipements réseau entraînent une latence élevée et une variation de la latence, nuisant aux performances des applications.

### BXI (Bull eXascale Interconnect)
Technologie d'interconnexion haute performance développée par Bull/Atos pour les systèmes HPC, dont le contrôle de congestion peut être étudié avec HTSIM.

## C

### Contrôle de Congestion (Congestion Control)
Mécanisme utilisé par les protocoles réseau pour éviter ou gérer la congestion dans le réseau, généralement en adaptant le débit d'envoi des données.

### CWND (Congestion Window)
Dans TCP, la fenêtre de congestion limite la quantité de données qu'un expéditeur peut envoyer avant de recevoir un ACK, afin de prévenir la congestion du réseau.

## D

### DCTCP (Data Center TCP)
Variante de TCP conçue pour les environnements de centre de données, utilisant ECN pour une réaction plus précise à la congestion.

### Débit (Throughput)
Quantité réelle de données transmises par unité de temps, souvent inférieure à la bande passante théorique en raison de divers facteurs comme la congestion ou les protocoles.

## E

### ECN (Explicit Congestion Notification)
Mécanisme permettant aux équipements réseau de signaler la congestion imminente sans rejeter des paquets, en marquant les paquets plutôt qu'en les supprimant.

### Edge Switch
Commutateur situé à la périphérie d'un réseau, généralement le premier point de connexion pour les hôtes finaux.

### Événement Discret (Discrete Event)
Dans une simulation à événements discrets comme HTSIM, un événement qui se produit à un instant précis et modifie l'état du système.

## F

### Fat-Tree
Topologie réseau à plusieurs niveaux utilisée dans les centres de données, où la densité des liens augmente à mesure qu'on monte dans la hiérarchie, éliminant la sursouscription.

### FCT (Flow Completion Time)
Temps nécessaire pour qu'un flux réseau complet (du premier au dernier paquet) soit transmis avec succès, métrique importante pour évaluer les performances.

### FIFO (First In, First Out)
Politique de gestion de file d'attente où les paquets sont servis dans l'ordre exact de leur arrivée.

## G

### Gigue (Jitter)
Variation de la latence au fil du temps, affectant la régularité de la transmission des paquets et pouvant impacter les applications sensibles au timing.

### Goulot d'Étranglement (Bottleneck)
Lien ou composant réseau qui limite le débit global d'un chemin en raison de sa capacité inférieure par rapport aux autres parties du chemin.

## H

### HPC (High-Performance Computing)
Calcul haute performance, domaine utilisant des supercalculateurs et des clusters pour résoudre des problèmes complexes nécessitant une grande puissance de calcul.

### HPCC (High Precision Congestion Control)
Algorithme de contrôle de congestion qui utilise des informations précises sur l'état du réseau pour ajuster le débit d'envoi.

### HTSIM
Simulateur d'événements discrets haute performance conçu pour étudier les comportements des algorithmes de contrôle de congestion dans les réseaux.

## I

### Incast
Phénomène où de nombreux serveurs envoient simultanément des données à un seul destinataire, causant une congestion sévère et potentiellement un effondrement des performances.

### INT (In-band Network Telemetry)
Technique permettant de collecter des données télémétriques réseau en les intégrant dans les paquets de données eux-mêmes.

## L

### Latence (Latency)
Délai entre l'envoi d'un paquet et sa réception, généralement mesuré en millisecondes ou microsecondes.

### Leaf-Spine
Topologie réseau à deux niveaux populaire dans les centres de données modernes, où chaque commutateur "leaf" est connecté à chaque commutateur "spine", offrant une faible latence et une haute bande passante.

## M

### MPTCP (Multipath TCP)
Extension de TCP permettant à une connexion d'utiliser plusieurs chemins réseau simultanément, améliorant la résilience et potentiellement le débit.

### MTU (Maximum Transmission Unit)
Taille maximale d'un paquet pouvant être transmis sur un réseau sans fragmentation.

## N

### NACK (Negative Acknowledgement)
Signal envoyé par le récepteur pour indiquer qu'un paquet n'a pas été reçu correctement, utilisé dans certains protocoles comme NDP.

### NDP (NDP Datacenter Protocol)
Protocole de transport développé à l'aide de HTSIM, utilisant le "trimming" des paquets et un mécanisme "pull-based" pour le contrôle de congestion.

## O

### Outcast
Phénomène où un flux ou un groupe de flux reçoit systématiquement moins de ressources que les autres, entraînant une inéquité dans le réseau.

## P

### Paquet (Packet)
Unité fondamentale de données dans un réseau, comprenant les données utilisateur ainsi que des informations d'en-tête pour le routage et le contrôle.

### PFC (Priority Flow Control)
Mécanisme de contrôle de flux IEEE 802.1Qbb qui permet de pauser la transmission sur des liens spécifiques pour éviter la perte de paquets due au débordement de tampon.

### Pipe
Dans HTSIM, composant qui modélise un lien réseau avec une latence et une bande passante spécifiques.

## Q

### Queue (File d'Attente)
Structure de données qui stocke temporairement les paquets en attente de traitement ou de transmission, jouant un rôle crucial dans la gestion de la congestion.

## R

### RED (Random Early Detection)
Algorithme de gestion active de file d'attente qui rejette ou marque des paquets de manière probabiliste avant que la file d'attente ne soit complètement pleine.

### RoCE (RDMA over Converged Ethernet)
Protocole réseau permettant l'accès direct à la mémoire à distance (RDMA) sur des réseaux Ethernet, couramment utilisé dans les environnements HPC et de stockage.

### Round Robin
Politique d'ordonnancement qui attribue des ressources à tour de rôle aux entités qui les demandent, assurant une forme simple d'équité.

### RTT (Round-Trip Time)
Temps nécessaire pour qu'un paquet voyage de l'émetteur au récepteur puis revienne à l'émetteur, métrique importante pour de nombreux algorithmes de contrôle de congestion.

## S

### Simulation à Événements Discrets (Discrete Event Simulation)
Technique de modélisation où le système change d'état uniquement à des points discrets dans le temps, déclenchés par des événements.

### SWIFT
Algorithme de contrôle de congestion qui combine des informations de délai et de débit pour une réaction rapide aux changements dans le réseau.

### Switch (Commutateur)
Équipement réseau qui relie plusieurs segments d'un réseau, transmettant les données uniquement vers la destination prévue.

## T

### Tail Drop
Politique de gestion de file d'attente la plus simple où les nouveaux paquets arrivant sont rejetés lorsque la file d'attente est pleine.

### TCP (Transmission Control Protocol)
Protocole de transport fiable et orienté connexion qui forme la base de la plupart des communications Internet.

### Topologie (Topology)
Arrangement physique ou logique des nœuds et des liens dans un réseau.

### Tore (Torus)
Topologie réseau en forme de grille où les bords opposés sont connectés, formant une structure en forme de donut, couramment utilisée dans les supercalculateurs.

## W

### WFQ (Weighted Fair Queueing)
Algorithme d'ordonnancement réseau qui attribue à chaque flux une part de la bande passante proportionnelle à son poids assigné.
