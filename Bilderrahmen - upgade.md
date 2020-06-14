
## Version vom Pictureframe prüfen:

sudo nano /home/pi/.local/lib/python3.7/site-packages/PictureFrame/__main__.py


### so sieht die aktuelle version aus:

'''
def main():
    """main function
    """
...
...
...
# Kommandozeilenparameter
    parser.add_argument("--config", default="PictureFrame.conf",
'''

wenn da was anderes steht dann updaten oder __main__.py austauschen!


## Alte config öffnen und kopieren und umbenennen:

- Welche Ordener werden synkronisiert?
- PictureFrame.conf in einen dieser Ordner Kopieren und umbenen in z.B. hohenems.conf

/home/pi/PictureFrame/User1/hohenems.conf
/home/pi/PictureFrame/User1/scherbda.conf



## Startbefehl vom Bilderrahem ändern:

sudo nano /etc/xdg/lxsession/LXDE-pi/autostart

alt: @/home/pi/.local/bin/PictureFrame

neu: @/home/pi/.local/bin/PictureFrame --config /home/pi/PictureFrame/User1/hohenems.conf
     @/home/pi/.local/bin/PictureFrame --config /home/pi/PictureFrame/User1/scherbda.conf


## RClone erneut einrichten

rclone config
e
y
1
y
https://nextcloud.werneburg.ddns.net/remote.php/webdav/Bilder
n
n
n
n
y

---

e
y
2
y
https://nextcloud.werneburg.ddns.net/remote.php/webdav/Bilder/Scherbda
n
n
n
n
y

q


### testen:

rclone ls User1:
rclone ls User2:


### crontab -e
crontab -e
- hinzufügen von: ,conf,CONF
