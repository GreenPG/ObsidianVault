---
Title: Multithread vs SubProcess TestLab GUI
Date: 2024-06-17
tags:
  - Python
  - Dev
  - GUI
  - TestLab
---

# Multithread vs SubProcess TestLab GUI 

Besoin d'executer le runner dans un process/thread différents de la GUI pour éviter de la freeze.
2 possibilités : multithreads ou sous-process.

Sous-process:
	Pour:
		- permettrait de faire de la GUI une sur-couche de la version CLI du runner, qui le lancerait dans un sous process et redirigerai les outputs afin d'actualiser l'interface. Il n'y aurait donc pas besoin d'avoir une version CLI et une version GUI du runner.

	Contre
		- obliger de relancer un runner pour lancer pl