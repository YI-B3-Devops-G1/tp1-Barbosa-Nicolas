# tp1-Barbosa-Nicolas

## Info
mail : nicolas.barbosa@ynov.com  
github_username: nicolasbarb  

## VirtualBox

1 - Téléchargement de l'iso Ubuntu Server  
2 - Installation de la VM  
3 - téléchargement et installation des paquets suivant :  
  . NodeJs  
  . openssh-server  
  . nginx  

4 - Configuration des ports  
. http/TCP/127.0.0.1/8080/10.0.2.15/80  
. https/TCP/127.0.0.1/4443/10.0.2.15/443  
. ssh/TCP/127.0.0.1/8022/10.0.2.15/22

5 - Création d'un fichier html pour nginx "index.html"  

```html
<!DOCTYPE html>
<html>
<body>
B3 Devops - TP 1
</body>
</html>  
```

6 - Création d'un fichier de configuration pour notre site

devops.tp1 :
```bash
server {
        listen 80;
        server_name devops.tp1;
        root /home/nicolas/www;
        index index.html;
}
```

7 - Déconnexion de la config "default" nginx  

```bash 
Unlink default
```

8 - Création de lien symbolique  

Pour linker le dossier contenant notre fichier html et le livreur nginx

```bash
sudo ln -s /etc/nginx/sites-available/devops.tp1 /etc/nginx/sites-enabled/devops.tp1
```


## VAGRANT

1 - Télécharger Vagrant  
```bash 
brew install vagrant
````

2 - Initialiser Vagrant  
```bash
vagrant init
```

3 - Créer le fichier Vagrantfile et le remplir

Ajout de la config des ports et l'appel vers le script bootstrap.sh  

```bash
  config.vm.box = "ubuntu/trusty64"
```

```bash
config.vm.network "forwarded_port", guest: 443, host: 4443, id: "https"
  config.vm.network "forwarded_port", guest: 80, host: 8080, id: "nginx"
  config.vm.network "forwarded_port", guest: 22, host: 8022, id: "ssh"
```
4 - Ajout des requêtes d'installation des paquets nécessaires dans bootstrap.sh

