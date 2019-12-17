# Raspbian Installation

1. Das aktuelle Image von [Raspbian Buster mit Desktop](https://downloads.raspberrypi.org/raspbian_latest) runterladen.
2. [Etcher](https://www.balena.io/etcher/) runterladen.
3. Mit Etcher das Raspbian Image auf die SD Karte kopieren.
4. SSH Zugang zum Pi aktivieren.  
   Dazu erstellen wir auf SD Karte eine neue leer Datei `"ssh"` (ohne Endung und Inhalt).
5. WLan Einstellungen angeben.  
   Dazu erstellen wir auf SD Karte eine Datei `"wpa_supplicant.conf"`.  
   Der Inhalt solte wie folgt aussehen (für ein WLan):  

   ```bash
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1
    country=AT

    network={
        scan_ssid=1
        ssid="_ssid_"
        psk="_password_"
        key_mgmt=WPA-PSK
    }
    ```  

   Wenn sich der Pi automatich in mehrere WLan's einbuchen soll. Dann kann die Datei so aussehen:

    ```bash
    ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
    update_config=1

    network={
        scan_ssid=1
        ssid="_ssid_1_"
        psk="_password_1_"
        key_mgmt=WPA-PSK
        id_str="location_1"
    }
    network={
        scan_ssid=1
        ssid="_ssid_2_"
        psk="_password_2_"
        key_mgmt=WPA-PSK
        id_str="location_2"
    }
    ```

6. Display Einstellungen angeben. [Video options in config.txt](https://www.raspberrypi.org/documentation/configuration/config-txt/video.md)  
   Die Datei `"config.txt"` von der SD Karte öffen und die folgenden Zeilen am Ende hinzufügen:

    ```bash
    hdmi_force_hotplug=1
    config_hdmi_boost=7
    hdmi_group=2
    hdmi_mode=87
    hdmi_drive=1
    display_rotate=0
    hdmi_cvt 1024 600 60 6 0 0 0
    ```

    Die Einstellungen sind für ein [7 Zoll Display](https://www.amazon.de/Raspberry-Zoll-kapazitiver-Touchscreen-HDMI-Monitor-HD-LCD-Gaming-Bildschirm/dp/B07QKT6L58/ref=sr_1_5?__mk_de_DE=ÅMÅŽÕÑ&crid=GOLPPX860FPX&keywords=7+zoll+display+pi&qid=1576345080&smid=A5BN6RQOA0WX3&sprefix=7+zoll+dis%2Caps%2C177&sr=8-5) mit 1024x600px Auflösung.  
    Sie sollten aber auch für ein [10,1 Zoll Display](https://www.amazon.de/ETEPON-Monitor-Raspberry-Ultra-Slim-EP010/dp/B07HQ69LFX/ref=sr_1_3?__mk_de_DE=ÅMÅŽÕÑ&crid=13EHA7H5S81WV&keywords=10+zoll+display&qid=1576343916&smid=A22U1VE1O4ZFQ&sprefix=%2Caps%2C186&sr=8-3) mit 1024x600px Auflösung gehen.  

7. SD Karte in den Pi stecken, Display und Strom anschliesen.  
8. Mit dem Pi über SSH verbinden.
   `ssh pi@<ip_address>` das standad Password ist `raspberry`.
9. Raspbian auf den aller neuesten Stand bringen:  
   `sudo apt-get update`  
   `sudo apt-get upgrade`  
10. Raspian Config starten:  
   `sudo raspi-config`  
11. Passwort für den User Pi ändern: `<1> Change User Password`  
12. Netzwerkeinstellungen: `<2> Network Options`  
    Hostname ändern: `<N1> Hostname`  
13. Datum und Uhrzeit: `<4> Localisation Options`  
    Zeitzone: `<I2> Change Timezone`  
14. Wenn die Root Partition nicht automatisch beim ersten Start an die Größe der SD Karte angepass worden ist.  
    `<7> Advanced Options`  
    `<A1> Expand Filesystem`  
15. Einmal neu starten: `sudo reboot now`  
16. Fertig!

