---
title: "Einrichtung eines Linux Ubuntu Servers"
author: "Erik Meyer, Robin Gerwe"
bibliography: "linux-server-documentation.bib"
csl: "https://raw.githubusercontent.com/citation-style-language/styles/master/harvard-anglia-ruskin-university.csl"
link-citations: true
urlcolor: "blue"
fontsize: 12
lang: de-DE
---

\newpage

# Apache Webserver installieren

Zuerst die Packete updaten.

```bash
sudo apt update 
```

Dann kann das Apache-Packet installiert werden.

```bash
sudo apt install apache2 
```

Prüfen um zu prüfen ob der Server nun funktioniert geben wir unsere IP-Addresse in den Browser ein.
Diese könen wir durch diesen Command bekommen:

```bash
hostname -I
```

Wenn alles geklapp hat sollte unter dieser IP-Addresse die Standardseitenvorlage von Apache angezeigt werden \ref{fig:ApacheStandardPage}.

![Die Standardseite von Apache \label{fig:ApacheStandardPage}](Screenshot%20Apache2%20Ubuntu%20Default%20Page%202021-06-13%20192637.png)

Die Standardseite von Apache **`index.html`** ist in dem Verzeichnis **`/var/www/html/`** zu finden.
Mit einem Editor wie [nano](https://www.nano-editor.org/) kann die Apachestandardseite bearbeitet werden.

```bash
sudo nano /var/www/html/index.html
```

[Install Apache Webserver Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04-de)

Informationsseite über das installierte System hinzufügen

# Samba

## Samba installieren

Zuerst alle Packete updaten.

 ```bash
 sudo apt update
 ```

Dann das Samba-Package installieren.

 ```bash
 sudo apt install samba
 ```

Überprüfen zum Überprüfen ob die Installation erfolgreich war:

```batch
whereis samba
```

Die Ausgabe davon sollte dann so aussehen:

```
samba: /usr/sbin/samba /usr/lib/samba /etc/samba /usr/share/samba /usr/share/man/man7/samba.7.gz /usr/share/man/man8/samba.8.gz
```

Dann kann überprüft werden, ob der Samba-Service läuft.

 ```batch
 sudo service smbd status
 ```

[samba configuration](https://ubuntu.com/tutorials/install-and-configure-samba#3-setting-up-samba)

## readonly/readwrite Freigabe

Ein schon hinzugefügter Benutzer z.B _**`MeinBenutzerName`**_ im Linuxsystem kann in Samba einfach mit diesem Befehl hinzugefügt werden:

```batch
smbpasswd -a MeinBenutzerName
```

Hier erstellen wir ein Verzeichnis für den Remote-Lesezugriff

```batch
sudo mkdir /home/<username>/sambashare/readonly
```

Und hier ein Verzeichnis für den Remote-Lese/Schreibezugriff

```batch
sudo mkdir /home/<username>/sambashare/readwrite
```

Damit auf das _**`readwrite`**_ Verzeichniss zugegriffen werden kann müssen Berechtigungen gesetzt werden:
```batch
sudo chmod 0777 /home/<Username>/sambashare/readwrite
```

Als nächstes schauen wir in die Konfigurationsdatei von Samba:

```batch
sudo nano /etc/samba/smb.conf
```

Dort hängen wir dann am Ende folgendes für den Lesezugriff an:

```
# readonly
[readonly]
   path= /home/<Username>/sambashare/readonly
   writable = no
   browsable = yes
   public = yes
   read only = no
```

Dann nochmal folgendes für den Lese und Schreibezugriff:

```
# readwrite
[readwrite]
   path = /home/<Username>/sambashare/readwrite
   writable = yes
   browsable = yes
   public = yes
   read only = no
```

Und dann restarten wir Samba damit die Änderungen übernommen werden:

```batch
sudo service smbd restart
```

# Lokale Benutzer anlegen

[Samba Users](https://www.thegeekdiary.com/how-to-add-or-delete-a-samba-user-under-linux/#:~:text=To%20add%20a%20new%20user,access%20to%20a%20samba%20share.)

## Benutzer

```bash
sudo adduser benutzer
```

## Fernzugriff

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

Die Packages aktualisieren.

```bash
sudo apt update
```

```bash
sudo apt upgrade
```

Dann installieren wir das SSH-Paket.

```bash
sudo apt install ssh
```

Mit `systemctl` können wir uns den Status anzeigen lassen.

```bash
sudo systemctl status ssh 
```

Wenn alles geklappt hat sollte es ungefähr so aussehen \ref{fig:SshSystemctlStatus}:

![Ausgabe von 'sudo systemctl status ssh' \label{fig:SshSystemctlStatus}](Screenshot%20SSH%20Status%202021-06-13%20183238.png)


# Quellenverzeichnis
[1](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-20-04-de)
[2](https://www.thegeekdiary.com/how-to-add-or-delete-a-samba-user-under-linux/#:~:text=To%20add%20a%20new%20user,access%20to%20a%20samba%20share.)
