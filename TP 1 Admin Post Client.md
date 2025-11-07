# TP 1

- sudo apt update
- sudo apt install apache2

Pour pouvoir installer Apache 

- sudo systemctl start apache2
- sudo systemctl status apache2

Installe et montre le statut de Apache

```echo '<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Linux is Better</title>
    <style>body{background-color:#f0f0f0;margin:0;height:100vh;display:flex;justify-content:center;align-items:center;font-family:Arial,sans-serif;}h1{color:#333;font-size:48px;text-align:center;animation:fadeIn 2s ease-in-out;}@keyframes fadeIn{from{opacity:0;}to{opacity:1;}}</style>
</head>
<body>
    <h1>Linux is better</h1>
</body>
</html>' | sudo tee /var/www/html/index.html
```
Remplacer la page web de défault par le texte si dessus.

Dans un Navigateur aller sur https://localhost

Changer le Apache pour le Port 8080 et editer le configurations

- sudp sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/ports.conf

- sudo sed -i 's/<VirtialHost \*:80>/<VirtualHost *:8080>/g' /etc/apache2/sites-available/000-default.conf

Change l'Apache pour le port 8080 au lieu de 80

- sudo systemctl restart apache2

Relancer Apache

Tester sur le navigateur:
https://localhost:8080


Accepter seulement Web (8080) et SSH (22)

```sudo ufw allow 8080/tcp
sudo ufw allow ssh
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
```

Copier la clé publique dans ~/.ssh/authorized_keys

Activer l'auth par clé

```sudo nano /etc/ssh/sshd_config
```

dans le fichier définir:

```PasswordAuthentication no
```

- sudo sytemctl restart sshd

Désactiver le login root vi a SSH

Dans le même fichier config:

```PermitRootLogin no
```

Redemarrer SSH

- sudo systemctl restart sshd


Bonus:
Script Bash pour automatiser toutes les étapes

```#!/bin/bash
set -e
# Install Apache	sudo apt update
sudo apt install -y apache2 ufw
# Start Apache
sudo systemctl start apache2
sudo systemctl enable apache2
# Custom index.html
cat <<EOF | sudo tee /var/www/html/index.html
<!DOCTYPE html>
<html lang="en">
<head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1.0"><title>Linux is Better</title><style>body{background-color:#f0f0f0;margin:0;height:100vh;display:flex;justify-content:center;align-items:center;font-family:Arial,sans-serif;}h1{color:#333;font-size:48px;text-align:center;animation:fadeIn 2s ease-in-out;}@keyframes fadeIn{from{opacity:0;}to{opacity:1;}}</style></head><body><h1>Linux is better</h1></body></html>
EOF
# Change Apache port to 8080
sudo sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/ports.conf
sudo sed -i 's/<VirtualHost \*:80>/<VirtualHost *:8080>/g' /etc/apache2/sites-available/000-default.conf
sudo systemctl restart apache2
# UFW firewall
sudo ufw allow 8080/tcp
sudo ufw allow ssh
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw --force enable
# SSH config (no password, no root)
sudo sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config
sudo sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin no/g' /etc/ssh/sshd_config
sudo systemctl restart sshd
```

ensuite donner la permission de l'executer et l'essayer

```chmod +x configure_server.sh
./configure_server.sh
```
