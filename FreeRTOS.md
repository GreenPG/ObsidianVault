OS simplifié pour embarqué (entre vrai os et baremetal)


Le scheduler défini tâche a lancé selon priorités 
Le scheduler est preemptif, round-robin, et time sliced

Préemption : tâche ready avec la plus haute prio s'exécute.
Round-robin : 2 tâches ayant la même prio se partage chacun sont tour l'usage du coup
Time-sliced: le switch est fait a chaque tick de la clock du rtos


Utilise des semaphores pour synchroniser les tâches entre elle et avec les interruptions (événement hors du code (hardware, messages...)). Permet de trigger les tâches a une fréquence données et dans le bon ordre(++)

Queue :
Permet de transférer les données d'une tâche a l'autre. Garanti que les données sont utilisées qu'une seule fois
Mutex:
Évite les accès concurrents a des ressources. Si tâche plus prio a besoin d'unutex lock, le scheduler augment la prio du process qui la lock jusqu'à ce qu'elle libère le mutex (héritage de prio)

