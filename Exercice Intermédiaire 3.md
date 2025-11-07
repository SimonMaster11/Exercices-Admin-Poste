# Exercice Intermédiaire 3

- sudo journalctl -u ssh --since "24 hours ago"

Pour afficher les logs du service SSH des 24 dernières heures

![alt text](image-2.png)

- sudo journalctl -u ssh --since "24 hours ago" | grep "Failed password"

