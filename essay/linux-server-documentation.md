---
title: "Einrichtung eines Linux Ubuntu Servers"
author: "Erik Meyer, Robin Gerwe"
bibliography: "linux-server-documentation.bib"
csl: "https://raw.githubusercontent.com/citation-style-language/styles/master/harvard-anglia-ruskin-university.csl"
link-citations: true
urlcolor: "blue"
fontsize: 12
---

<!-- # Netzwerkbrücke einrichten

![Netzwerkbrücke 1 \label{fig:1}](Screenshot%20Netzwerkbrücke%202021-04-28%20140429.png)

![Netzwerkbrücke 2 \label{fig:2}](Screenshot%20Netzwerkbrücke%202021-04-28%20140429.png) -->

# Einrichtung eines Linux Ubuntu Servers

Inhaltsverzeichnis:
Eine statische IP-Adresse konfigurieren

Netzwerkbrücke eingerichtet

# Apache Webserver installieren

```bash
sudo apt update 
```

```bash
sudo apt install apache2 
```

Install CURL

Prüfen ob die seite funktioniert

```bash
hostname -I
```

[Install Apache Webserver Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04-de)
Informationsseite über das installierte System hinzufügen

---

# Samba installieren

 ```bash
 sudo apt update
 ```

 ```bash
 sudo apt install samba
 ```

# Samba readonly/readwrite Freigabe

# Lokale Benutzer anlegen

[Samba Users](https://www.thegeekdiary.com/how-to-add-or-delete-a-samba-user-under-linux/#:~:text=To%20add%20a%20new%20user,access%20to%20a%20samba%20share.)

1. Benutzer

    ```bash
    sudo adduser benutzer
    ```
2. Fernzugriff

    ```bash
    sudo adduser fernzugriff
    ```

    ```bash
    sudo usermod -aG sudo fernzugriff
    ```

# SSH-Dienst für Fernzugriff einrichten

[1](https://linuxize.com/post/how-to-enable-ssh-on-ubuntu-18-04/)
[2](https://www.cyberciti.biz/faq/ubuntu-linux-install-openssh-server/)
[@enablesshubuntuonline]

```bash
sudo apt update
```

```bash
sudo apt upgrade
```

```bash
sudo apt install ssh
```

# Quellenverzeichnis
[1](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04-de)
[2](https://www.thegeekdiary.com/how-to-add-or-delete-a-samba-user-under-linux/#:~:text=To%20add%20a%20new%20user,access%20to%20a%20samba%20share.)