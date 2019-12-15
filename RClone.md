# RClone

Wir benutzen am besten [RClone](https://rclone.org) um die Bilder für unser Bilderrahmen Projekt, aus einer Nextcloud zu holen.

- [RClone Einstellungen für WebDAV - NextCloud](https://rclone.org/webdav)
- [RClone Filter Optionen](https://rclone.org/filtering/#include-include-files-matching-pattern)

## Installation

```bash
sudo apt-get install rclone
```

## RClone einrichten

```bash
rclone config
```

Um nun eine Nextcloud einzurichten, folgende Antworten eingeben:

```bash
n
<Name>
webdav
https://<Nextcloud-Server-Adresse>/nextcloud/remote.php/webdav/<Bilder-Ordner>
nextcloud
<Benutzername>
y
<Passwort>
<Passwort>
>ENTER<
y
q
```

Nun kann man mit dem foldenden Befehl, testweise anschauen was so alles an Dateien in dem Nextcloud Ordner ist.

```bash
rclone ls <Name>:
```

Um einen Lokalen Ordner mit dem Nextcloud Ordner zu synchronisieren benutz man foldenden Befehl:

```bash
rclone sync <Name>: <Lokaler Ornder>
```

Um automatisch den Lokalen Ordner zu synchronisieren muss crontab um eine Zeile erweitert werden.

```bash
crontab -e
```

Die Folgende Zeile sorgt dafür das crontab RClone jede Stunde einmal ausführt.

```bash
0 * * * * rclone sync <Name>: <Lokaler Ornder>
```

Oder einmal alle 4 Stunden, mit dieser Zeile.

```bash
0 */4 * * * rclone sync <Name>: <Lokaler Ornder>
```

Meine Zeile sieht zum Beispiel so aus.

```bash
0 */4 * * * rclone sync --include "*.{jpeg,jpg,gif,png,tga,tiff,JPEG,JPG,GIF,PNG,TGA,TIFF}" User1: /home/pi/PictureFrame/User1
```
