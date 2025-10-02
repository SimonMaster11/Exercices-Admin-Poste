---
title: 'Exercice Débutant : 1'

---

# Exercice Débutant : 2

- touch log.txt

Pour créer un fichier nommé log.txt

![image](https://hackmd.io/_uploads/r1kBc2snge.png)

- ls /etc > log.txt

Pour copier la liste de fichiers dans /etc et les coller dans log.txt

![image](https://hackmd.io/_uploads/BkvUK6shlx.png)

- tail /var/log/syslog/ > text.txt

Pour copier les 10 dernières lignes de /val/log/syslog/ et les coller
dans un nouveau fichier text.txt

![image](https://hackmd.io/_uploads/HJ67OTohxl.png)

- cat text.txt >> log.txt

Pour copier les 10 lignes du fichier text.txt à la fin du fichier log.txt

![image](https://hackmd.io/_uploads/r1pR5Tj2xg.png)

- sudo grep "error" /var/log/syslog

Pour afficher seulement les lignes qui contiennent le mot "error"

![image](https://hackmd.io/_uploads/BJac26s2ee.png)
