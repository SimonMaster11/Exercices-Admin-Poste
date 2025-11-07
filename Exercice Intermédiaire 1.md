# Exercice Intérmediaire 1

- ps aux --sort=-%mem | head -n 10

Pour lister le top 10 des processus par ordre décroissant trié par utilisation de la RAM.

![alt text](image.png)

- sudo renice -n 10 -p 4744

Mets une priorité inférieure au processus choisit 4744 dans l'example grace à son PID

- kill -9 4744

Cela permet de terminer le processus choisit