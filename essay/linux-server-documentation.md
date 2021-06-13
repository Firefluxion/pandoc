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
