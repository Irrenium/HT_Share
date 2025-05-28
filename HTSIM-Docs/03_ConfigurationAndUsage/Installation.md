# Installation de HTSIM

## Prérequis

HTSIM est un simulateur écrit en C++ qui a été conçu pour être aussi léger et portable que possible. Voici les prérequis nécessaires pour installer et utiliser HTSIM :

- **Système d'exploitation** : Linux (recommandé), macOS
- **Compilateur** : g++ ou clang++ avec support C++11
- **Outils de build** : make
- **Dépendances** : Aucune dépendance externe requise

## Obtention du Code Source

Pour obtenir le code source de HTSIM, vous pouvez cloner le dépôt GitHub officiel :

```bash
git clone https://github.com/Broadcom/csg-htsim.git
cd csg-htsim
```

## Compilation du Simulateur

La compilation de HTSIM est simple grâce à son absence de dépendances externes. Suivez ces étapes pour compiler le simulateur :

```bash
# Accéder au répertoire principal de simulation
cd sim

# Compiler la bibliothèque principale et les outils
make

# Pour compiler des exécutables spécifiques (par exemple, la version NDP)
make htsim_ndp
```

### Options de Compilation

Le Makefile de HTSIM offre plusieurs options de compilation :

| Cible | Description |
|-------|-------------|
| `all` | Compile la bibliothèque principale (`libhtsim.a`) et l'outil d'analyse de sortie |
| `htsim` | Compile le simulateur de base |
| `htsim_ndp` | Compile la version avec support NDP |
| `htsim_tcp` | Compile la version optimisée pour les simulations TCP |
| `htsim_dctcp` | Compile la version avec support DCTCP |
| `htsim_roce` | Compile la version avec support RoCE |
| `htsim_hpcc` | Compile la version avec support HPCC |
| `htsim_swift` | Compile la version avec support Swift |
| `htsim_mpswift` | Compile la version multichemin de Swift |

### Vérification de l'Installation

Pour vérifier que votre installation fonctionne correctement, vous pouvez exécuter un exemple simple :

```bash
# Accéder au répertoire d'exemples
cd ../sim/EXAMPLES/permutation

# Exécuter un scénario de test
./run.sh
```

Si l'exécution se termine sans erreur, cela signifie que HTSIM est correctement installé et fonctionnel.

## Installation sur Différents Systèmes d'Exploitation

### Installation sur Linux

HTSIM est principalement développé et testé sur des systèmes Linux. L'installation sur la plupart des distributions Linux devrait être simple :

```bash
# Sur Ubuntu/Debian
sudo apt-get install g++ make
git clone https://github.com/Broadcom/csg-htsim.git
cd csg-htsim/sim
make

# Sur Fedora/Red Hat
sudo dnf install gcc-c++ make
git clone https://github.com/Broadcom/csg-htsim.git
cd csg-htsim/sim
make
```

### Installation sur macOS

HTSIM fonctionne également sur macOS avec quelques ajustements mineurs :

```bash
# Installer les outils de développement (si ce n'est pas déjà fait)
xcode-select --install

# Ou utiliser Homebrew pour installer gcc
brew install gcc make

# Cloner et compiler
git clone https://github.com/Broadcom/csg-htsim.git
cd csg-htsim/sim
make CC=g++-11  # Spécifier le compilateur gcc (ajuster la version si nécessaire)
```

## Résolution des Problèmes Courants

### Erreurs de Compilation

Si vous rencontrez des erreurs de compilation, vérifiez les points suivants :

1. **Version du compilateur** : HTSIM nécessite un compilateur avec support C++11
   ```bash
   g++ --version
   # Assurez-vous que la version est 4.8.1 ou supérieure
   ```

2. **Problèmes de Makefile** : Si `make` échoue, essayez de nettoyer et recompiler
   ```bash
   make clean
   make
   ```

3. **Erreurs spécifiques à la plateforme** : Sur certains systèmes, vous pourriez devoir modifier légèrement le code source
   ```bash
   # Par exemple, pour résoudre les problèmes de types non définis
   echo "#include <cstdint>" >> main.cpp
   ```

### Problèmes d'Exécution

Si HTSIM compile mais échoue à l'exécution, vérifiez ces problèmes courants :

1. **Permissions de fichier** : Assurez-vous que les fichiers exécutables ont les permissions appropriées
   ```bash
   chmod +x htsim_*
   ```

2. **Problèmes de chemin** : Certains exemples peuvent nécessiter d'être exécutés depuis un répertoire spécifique
   ```bash
   # Exécutez toujours depuis le répertoire approprié
   cd path/to/example
   ./run.sh
   ```

3. **Limitations de ressources** : Les simulations à grande échelle peuvent nécessiter plus de ressources
   ```bash
   # Augmenter les limites de pile
   ulimit -s unlimited
   ```

## Construction de HTSIM pour des Performances Optimales

Pour les simulations à grande échelle, vous pouvez optimiser la compilation de HTSIM :

```bash
# Compiler avec optimisations
make CFLAGS="-O3 -march=native"

# Pour les machines avec beaucoup de RAM, augmenter la taille des tampons internes
make CFLAGS="-O3 -march=native -DQUEUE_BUFFER=1048576"
```

## Installation des Outils d'Analyse

HTSIM génère des fichiers de trace qui peuvent être analysés avec des outils externes :

```bash
# Compiler l'outil d'analyse intégré
make parse_output

# Installation d'outils supplémentaires (optionnel)
# Pour les graphiques et visualisations
sudo apt-get install gnuplot python3-matplotlib
```

## Intégration avec des Environnements de Développement

### Configuration pour Visual Studio Code

Pour utiliser HTSIM avec VS Code :

1. Installez l'extension C/C++ pour VS Code
2. Créez un fichier `.vscode/c_cpp_properties.json` :

```json
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [],
            "compilerPath": "/usr/bin/g++",
            "cStandard": "c11",
            "cppStandard": "c++11",
            "intelliSenseMode": "gcc-x64"
        }
    ],
    "version": 4
}
```

### Configuration pour CLion

Pour utiliser HTSIM avec CLion :

1. Ouvrez le dossier du projet dans CLion
2. Assurez-vous que le projet est reconnu comme un projet CMake
3. Si nécessaire, créez un fichier `CMakeLists.txt` simple :

```cmake
cmake_minimum_required(VERSION 3.10)
project(htsim)

set(CMAKE_CXX_STANDARD 11)

file(GLOB SOURCES "*.cpp")
add_executable(htsim ${SOURCES})
```

## Environnements Virtuels et Conteneurs

Pour une isolation complète et une portabilité accrue, vous pouvez utiliser HTSIM dans un conteneur Docker :

```dockerfile
# Dockerfile pour HTSIM
FROM ubuntu:20.04

RUN apt-get update && apt-get install -y \
    g++ \
    make \
    git

WORKDIR /app
RUN git clone https://github.com/Broadcom/csg-htsim.git
WORKDIR /app/csg-htsim/sim
RUN make

# Définir le répertoire de travail par défaut
WORKDIR /app/csg-htsim
```

Pour construire et exécuter :

```bash
docker build -t htsim .
docker run -it htsim bash
```
