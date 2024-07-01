---
date: 2024-07-01
tags:
    - #Dev, #DesignPattern
hubs:
    "[[Design_Pattern]]"
urls:
    - https://en.wikipedia.org/wiki/Remote_procedure_call
---
# Master-Worker 
Décomposition d’une tâche complexe en sous-tâche.
Deux composants primaires : le maître et les travailleurs. Le maître agit comme un coordinateur central, responsable de la distribution des tâches, de leur management et de l'agrégation des résultats. Les travailleurs sont eux responsables de l’exécution des sous tâches.

Le maître découpe la tâche complète et assigne le travail de manière à répartir la charge de travail de manière égale selon les ressources dispos (pas forcément intéressant dans notre cas puisque l’on veut séquencer les tâches).
Le Maître maintient la communication avec les travailleurs durant l'exécution. Plusieurs possibilités : passage de message, remote procedure calls 
Quand un travailleur termine sa tâche, il remonte le résultat au maître.
k

Utile surtout pour effectuer des tâches en parallèle et équilibrer la charge de travail. Peut servir afin de manager un subprocess mais perd de son essence si un seul subprocess à la fois.

