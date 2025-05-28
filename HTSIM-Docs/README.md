# Documentation du Simulateur de Réseau HTSIM

Bienvenue dans la documentation complète du simulateur de réseau HTSIM, un outil puissant pour la modélisation et l'analyse des performances réseau.

## Aperçu

HTSIM est un simulateur d'événements discrets haute performance, inspiré par ns2 mais beaucoup plus rapide, principalement destiné à examiner le comportement des algorithmes de contrôle de congestion. Il a été développé à l'origine par [Mark Handley](http://www0.cs.ucl.ac.uk/staff/M.Handley/) et a évolué pour inclure de nombreuses fonctionnalités avancées.

## Structure de la Documentation

Notre documentation est organisée comme suit:

1. **Introduction**
   - [Qu'est-ce que HTSIM](01_Introduction/WhatIsHTSIM.md)
   - [Cas d'Utilisation](01_Introduction/UseCases.md)
   - [Aperçu de l'Architecture](01_Introduction/ArchitectureOverview.md)

2. **Composants Principaux**
   - [Commutateurs](02_CoreComponents/Switches.md)
   - [Canaux de Transmission (Pipes)](02_CoreComponents/Pipes.md)
   - [Files d'Attente](02_CoreComponents/Queues.md)
   - [Topologie de Réseau](02_CoreComponents/NetworkTopology.md)
   - [Modèles de Flux et de Trafic](02_CoreComponents/FlowAndTrafficModels.md)

3. **Configuration et Utilisation**
   - [Installation](03_ConfigurationAndUsage/Installation.md)
   - [Fichiers de Configuration](03_ConfigurationAndUsage/ConfigFiles.md)
   - [Exécution des Simulations](03_ConfigurationAndUsage/RunningSimulations.md)
   - [Analyse des Résultats](03_ConfigurationAndUsage/OutputAndAnalysis.md)

4. **Exemples**
   - [Exemple de Réseau Simple](04_Examples/SimpleNetworkExample.md)
   - [Scénario de Contrôle de Congestion](04_Examples/CongestionControlScenario.md)
   - [Exemple de Topologie Personnalisée](04_Examples/CustomTopologyExample.md)
   - [Comparaison d'Algorithmes](04_Examples/ComparisonOfAlgorithms.md)

5. **Sujets Avancés**
   - [Personnalisation de HTSIM](05_AdvancedTopics/CustomizingHTSIM.md)
   - [Débogage et Journalisation](05_AdvancedTopics/DebuggingAndLogging.md)
   - [Optimisation des Performances](05_AdvancedTopics/PerformanceTuning.md)

6. **Références**
   - [Glossaire](06_References/Glossary.md)
   - [Liens Externes](06_References/ExternalLinks.md)

## Comment Utiliser cette Documentation

Je vous recommande de commencer par la section Introduction pour comprendre les bases de HTSIM, puis d'explorer les composants principaux avant de passer aux exemples pratiques. Les sections avancées vous aideront à tirer le meilleur parti du simulateur pour vos besoins spécifiques.
