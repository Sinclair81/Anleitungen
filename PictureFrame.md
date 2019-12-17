# Bilderrahmen

Link zur Original README.md und dem ganzen Projekt: [Bilderrahmen](https://gitlab.tester.aipe.at/aph/bilderrahmen).

Digitaler Bilderrahmen mittels einem Raspberry Pi (2,3, zero, 4), wobei Befüllung und Konfiguration aus der Ferne über eine (oder mehrerere) Cloudlösungen (Seafile, Nextcloud, Owncloud, rsync, ftp, etc.) erfolgen kann.

## Voraussetzungen

- Raspbian Buster with desktop
- Ordner mit Bildern und Einstellungsdatei _PictureFrame.conf_; natürlich auch synchronisiert via einer (oder mehrerer) Cloudlösungen (Seafile, Nextcloud, Owncloud, rsync, ftp, etc.) möglich

## Installation

```bash
pip3 install --user --extra-index-url https://pypiserver.tester.aipe.at PictureFrame
```

Unsere "eigene" Abhängigkeit *autoupgrade* kommt in beiden Fällen dank *--extra-index-url* auch gleich aus dem eigenen Repo mit.

### Datenverzeichnis

Das Datenverzeichnis entweder beim Modulstart angeben oder Bilder (und Konfigurationsdatei) unter _~/PictureFrame_ ablegen. Dieses Verzeichnis kann dann auch aus der Cloud aktualisiert werden (ToDo: Dokumentation).
Eine Beispieldokumentation findet sich unter _samples_ im Installationsordner des Python Pakets.

## Autostart

Anpassung an _/etc/xdg/lxsession/LXDE-pi/autostart_ genügt:

```bash
sudo nano /etc/xdg/lxsession/LXDE-pi/autostart
```

```bash
#@lxpanel --profile LXDE-pi
#@pcmanfm --desktop --profile LXDE-pi
#@xscreensaver -no-splash
#point-rpi
@xset s noblank
@xset s off
@xset -dpms
@/home/pi/.local/bin/PictureFrame
```

## Curser bis zum Start des Bilderrahmens verstecken (optional)

[Unclutter](https://sourceforge.net/projects/unclutter/) installieren:

```bash
sudo apt-get install unclutter
```

Und _/etc/xdg/lxsession/LXDE-pi/autostart_ um einen entsprechenden Eintrag erweitern:

```bash
sudo nano /etc/xdg/lxsession/LXDE-pi/autostart
```

```bash
#@lxpanel --profile LXDE-pi
#@pcmanfm --desktop --profile LXDE-pi
#@xscreensaver -no-splash
#point-rpi
@xset s noblank
@xset s off
@xset -dpms
@unclutter -idle 0 -root
@/home/pi/.local/bin/PictureFrame
```

## Idee und Quelle

Wir orientieren uns derzeit stark an

- [Blockartikel](https://www.thedigitalpictureframe.com/de/so-erstellst-du-professionelle-ueberblendungen-auf-deinem-digitalen-bilderrahmen/)
- [Pi3D Demo Repository auf GitHub](https://github.com/pi3d/pi3d_demos)

## Pro Tip

Bilder vorab skalieren! :-)

## Dokumentation

- [RClone](RClone.md) - CMD Sync Client für alle möglichen Cloud Lösungen.
