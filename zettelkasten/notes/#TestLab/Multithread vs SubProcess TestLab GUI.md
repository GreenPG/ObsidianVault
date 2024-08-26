---
date: 2024-06-17
tags:
    - #TestLab
    - #Documentation
    - #Concurrency
hubs:
    - "[[Concurrency]]"
urls:
    -
---

# Multithread vs SubProcess TestLab GUI 

Besoin d'executer le runner dans un process/thread différents de la GUI pour éviter de la freeze.
2 possibilités : multithreads ou sous-process.

## Sous-process:
Pour:
- permettrait de faire de la GUI une sur-couche de la version CLI du runner, qui le lancerait dans un sous process et redirigerai les outputs afin d'actualiser l'interface. Il n'y aurait donc pas besoin d'avoir une version CLI et une version GUI du runner.
- peut être plus performant

Contre:
- Pas possible de faire run plusieurs sessions à un runner, obligé dans relancer un à chaque fois
- Si on que la GUI afficher plus que seulement les logs, force faire du parsing et du traitement des outputs au sein de la GUI

# Multithread
Pour:
- permet de créer un runner "infini" a que l'on peut appeler à plusieurs reprises sans avoir à le relancer.
- permet de gérer plus simplement les résultats des tests
Contre:
- force à avoir une version CLI et une version GUI du runner.
