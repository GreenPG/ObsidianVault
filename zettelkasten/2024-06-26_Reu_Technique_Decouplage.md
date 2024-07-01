---
date: 2024-06-26
tags:
    - #RéuTechnique, 
hubs:
   "[[OOP]]", "[[Methodology]]"
urls:
    -
---
# Reu_Technique_Decouplage 

- diviser un système en unités logique Inde 
- minimiser les deps entre les unités 

## Pourquoi :
Pour améliorer maintenabilite, l'evolutivite, la compréhension d'un système 
Réutiliser le code

Le decouplage est avant une histoire d'architecture structurelle, puis technique
C'est separer et encapsuler les couches de responsabilité, définir des interfaces claires et simples 

Quand introduire la modularité ?
- a l'exploitation  
- a la production 
Où ?
- a l'exécution
   - au niveau objet
	   En utilisant des interfaces, classes abstraites, pointeur sur fonction
	   Facilité la modélisation et la lecture. Check a la compilation. Facilité d'exécution. Facilité a tester.
	   Coût a l'exécution et en taille d'executable
- a l'édition des liens
		Utiliser la config du projet et laisser le linker géré les deps.
		Creer plus implémentation possible et préciser au linker laquelle utiliser 
		Facilité modélisation et lecture. Check a la compil. Facilité a tester. Peu de coûts a lexec même si pas dopti a la compil possible, mais au link si
		- Flexibilité a l'exécution 
- a la compilation 
		Utiliser la meta-programmatuon (template en cpp). 
		Check a la compil. Facilité a tester. Pas de coûts a lexec.
		Flexibilité a lexec. Facilité a la modélisation et a la lecture 

- pendant le preproc
		Utiliser des instructions de preproc pour définir quelle implémentation utiliser 
		Check a la compil, facilité a tester, pas de coût a lexec.
		Flexibilité a lexec, facilité modélisation et de lecture 


