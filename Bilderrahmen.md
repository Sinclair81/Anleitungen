# Das Bilderrahmen Projekt

- ***[Raspbian mit Desktop](Raspbian.md)*** nach dieser Anleitung installieren.

- ***[Midnight Commander](Midnight_Commander.md)*** installieren: `sudo apt-get install mc`  
  Wird nicht unbedingt gebraucht. Kann aber manchmal sehr hilfreich sein.

- ***[RClone](RClone.md)*** installieren: `sudo apt-get install rclone`  

- ***[Bilderrahmen](PictureFrame.md)*** nach dieser Anleitung installieren.  
  mit diesem Befehl kann man den Bilderrahnem manuel upgraden:  

  ```bash
  pip3 install --user --extra-index-url https://pypiserver.tester.aipe.at PictureFrame --upgrade
  ```

  mit diesem Befehl kann man den Bilderrahnem mit der Konfigurationsdatei manuel starten:  

  ```bash
  PictureFrame --dir /home/pi/PictureFrame
  ```

- ***Konfigurationsdatei vom Bilderrahmen***  
  Eine Beispieldokumentation findet sich unter: _~/.local/lib/python3.7/side-packages/PictureFrame/samples_  

  Ordner erstellen und die Konfigurationsdatei kopieren:  
  (Ich erstelle 2 Bilder Ordner, weil ich Bilder aus 2 unterschidlichen NextCloud's syncronisieren will.)  

  ```bash
  mkdir /home/pi/PictureFrame
  mkdir /home/pi/PictureFrame/User1
  mkdir /home/pi/PictureFrame/User2
  cp /home/pi/.local/lib/python3.7/site-packages/PictureFrame/samples/PictureFrame.conf.sample /home/pi/PictureFrame/PictureFrame.conf
  ```

  Die Konfigurationsdatei in Nano öffnen:  
  `sudo nano /home/pi/PictureFrame/PictureFrame.conf`

  Eine Zeile mit den Angaben der Bilder Ordner hinzufügen (am besten unterhalb der Zeile _#folders = ["/path/to/..._):  
  `folders = ["/home/pi/PictureFrame/User1", "/home/pi/PictureFrame/User2"]`

  Wenn der Bilderrahmen nur am Tag laufen soll, können die Zeiten in denen der Bilderrahmen aus sein soll auch angegeben werden.
  Dazu einfach die folgenden Zeilen unterhalb von der Zeile _#Uhr01 = So09:10-So10:00_ hinzufügen.

  ```bash
  Uhr01 = So23:00-Mo14:00
  Uhr02 = Mo21:00-Di14:00
  Uhr03 = Di21:00-Mi14:00
  Uhr04 = Mi21:00-Do14:00
  Uhr05 = Do21:00-Fr14:00
  Uhr06 = Fr23:00-Sa10:00
  Uhr07 = Sa23:00-So10:00
  ```

- ***Konfiguration von [RClone](RClone.md)***  
  Zur Einrichtung der Syncronisation, einfach `rclone config` eingeben und die Fragen beantworden.  
  Die Einstellungen einmal Testen mit: `rclone ls <Name>:`  
  Für die automatische Syncronisation mit Crontab `crontab -e` eingeben und die folgengen zeilen hinzufügen.

  ```bash
  0 */4 * * * rclone sync --include "*.{jpeg,jpg,gif,png,tga,tiff,JPEG,JPG,GIF,PNG,TGA,TIFF,conf,CONF}" User1: /home/pi/PictureFrame/User1
  0 */4 * * * rclone sync --include "*.{jpeg,jpg,gif,png,tga,tiff,JPEG,JPG,GIF,PNG,TGA,TIFF}" User2: /home/pi/PictureFrame/User2
  ```

  Details dazu sind in der [Anleitung](RClone.md).  

- ***Bilder laden und neu starten***  
  Einmal die Bilder manuel laden und danach den Pi neu starte.    

  ```bash
  rclone sync --include "*.{jpeg,jpg,gif,png,tga,tiff,JPEG,JPG,GIF,PNG,TGA,TIFF,conf,CONF}" User1: /home/pi/PictureFrame/User1
  rclone sync --include "*.{jpeg,jpg,gif,png,tga,tiff,JPEG,JPG,GIF,PNG,TGA,TIFF}" User2: /home/pi/PictureFrame/User2
  sudo reboot now
  ```  
