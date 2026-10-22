# Tobers_Timeswitch

[Kurze Änderungsübersicht](AENDERUNGEN_README_2026-10-21.md)

## 🚀 Tobers Timeswitch – Wochenplan, Astro und Master/Client

<img src="showcase/overview.jpg" align="left">

![Plattform](https://img.shields.io/badge/Plattform-ESP8266-blue) ![Schnittstelle](https://img.shields.io/badge/Schnittstelle-HTTP%20/%20GPIO%20/%20NTP-orange)

ESP8266-Zeitschaltuhr mit Weboberfläche, Astrozeiten, Countdown und Konfigurationsverteilung an mehrere Geräte. Eigenständiges Projekt von ElToberino; die ursprünglichen Credits bleiben erhalten.

**Dokumentationsstand:** 21.10.2026 · Branch `main`. Beschreibt den vorhandenen Projektstand; kein neuer Funktionstest am Gerät.

[Quellcode herunterladen](https://github.com/TimiWho/Tobers_Timeswitch/archive/refs/heads/main.zip) · [Ursprüngliche Haupt-README](README_Backup_2026-10-21.md)

---

## ⚙️ Hauptsketch und Hardware

| Element | Aktueller Quellcode / Bedeutung |
| --- | --- |
| timeswitch_1.0.ino | Hauptprogramm mit Timer-, Astro-, Countdown-, Master/Client- und Dateiverwaltungslogik. |
| Minimal_OTA.ino | Separater Zwischen-Sketch für kleine Flashgeräte; kein gleichzeitiger Teil des Hauptbuilds. |
| relPin=12 | Relais-Ausgang GPIO12. |
| ledPin=13 | Status-LED GPIO13. |
| buttonPin=0 | Lokaler Eingang GPIO0. |
| LittleFS | Dateisystem für Konfiguration, Webdateien und gespeicherte Daten. |
| WiFiManager | Ersteinrichtung der WLAN-Verbindung; projektspezifische Abhängigkeit in den Originalhinweisen. |

## 📡 Bedienung und Timer

Eingaben erfolgen über lokale Taste und HTTP-Weboberfläche. Zeitprogramme, aktive Wochentage, Standort, NTP-Intervall, Dämmerungsart und Countdown sind konfigurierbar und keine festen SSR1-Timer. Der Countdown deaktiviert während seiner Laufzeit die normalen Schaltzeiten.

Master/Client überträgt Zeit-/Geräteeinstellungen an konfigurierte IP-Adressen. GPIO-Pegel und HTTP-Status-/Konfigurationsantworten bilden die Ausgänge. Die Dateisystem-/Upload-Anleitung und der ursprüngliche 1-MB-Flash-Hinweis bleiben unten erhalten. Es gibt keinen eigenen MQTT-`ACT/WDOG`-Kanal.

## 📂 Projektstruktur

| Pfad | Inhalt |
| --- | --- |
| [data/](data/) | Eigenständiger Projektteil; Inhalt im verlinkten Ordner. |
| [data_DE/](data_DE/) | Eigenständiger Projektteil; Inhalt im verlinkten Ordner. |
| [showcase/](showcase/) | Eigenständiger Projektteil; Inhalt im verlinkten Ordner. |

## 🐞 GitHub-Issues

**Abgleich:** 21.10.2026. Status aus GitHub; diese Übersicht ändert keine Issues.

Zum Abgleichzeitpunkt sind keine offenen GitHub-Issues vorhanden.

In diesem Repository sind zum Abgleichzeitpunkt keine GitHub-Issues vorhanden.

## 🗂️ Originaldokumentation und Credits

Die ursprünglichen technischen Erläuterungen, Quellenangaben und Autorenhinweise bleiben nachfolgend erhalten. Maßgeblich für konkrete Pin- und Timerwerte ist der oben beschriebene Repository-Stand.

<details>
<summary>Originaldokumentation und Credits anzeigen</summary>

# Tobers Timeswitch for ESP8266
Tobers Timeswitch is a versatile and multifunctional timeswitch for ESP8266 devices, based on the great timeswitches on [fipsok.de](https://www.fipsok.de) (Jens Fleischer).

Besides the "classic" timeswitch functions widely configurable for every single day, it offers a lot of different sunrise/sunset and twilight modes. A countdown timer is also available.<br>
Using the inbuilt Master/Client function you can program multiple devices "by one click". This can be very helpful if you have lot of devices running that shall all use the same scheme of switching times.
Tobers Timeswitch is easily and extensively configurable via a comfortable web interface.<br>
<br>

## Webinterface and Functions
<img src="showcase/overview.jpg" align="left"> <br>

**Main Timeswitch**<br>
* set switching times and active days
* enable/disable single times or activate/deactivate all switching times
* times coloured brown below a sun symbol can't be changed manually because they have been assigned to the twilight functions<br>
<br>

**Advanced Functions**<br>
* assign twilight or sunrise/sunset times to certain switching times
* choose between sunrise/sunset or twilight as reference for switching times
  (twilight type can be set via config site)<br>
* enable/disable countdown timer<br>
(while countdown timer is active all switching times are deactivated)<br>
<br>

**Configuration**<br>
* set name of time switch
* set number of switching times
* set NTP server
* set interval for NTP server call
* enable/disable authentication for html sites and set credentials
* set longitude/latitude of your location and configure twilight type
* restart device
* erase WiFi credentials
* access to Master Function controlling multiple time switches
* access to Over the Air Update (OTA) via web interface<br>
Note: On devices with only 1MB flash memory OTA can only be made uploading "minimal_OTA" as an intermediate step.
* access to file administration
* acces to Log-Site logging latest ten NTP-Server-Calls<br>
<br><br>

## Master Functions
<img src="showcase/overview_master.jpg" align="left"><br>
**Client Administration**<br>
* add or delete IP addresses of clients <br>
* IP address of master device must also be added
* list of clients is sent to all clients<br>
  -> master functions can also be called on client devices<br>
* set number of switching times for master and all client devices<br>
<br>

**Cockpit**<br>
* overview of all clients to check connection and state
* switch on/off certain devices
* activate/deactivate all switching times of certain devices
* visit certain devices by clicking the IP address<br>
<br>

**Master Main Switch and Master Advanced Functions**<br>
* Configuration of switching times and advanced settings for **all devices**<br>
<br>

**For complete and detailed information about the setup of the device and the steps to be taken before compiling please visit [the article I wrote at hackster.io.](https://www.hackster.io/eltoberino/tobers-timeswitch-for-esp8266-ab3e06)**
<br><br>

## Requirements
* *Hardware*<br>
ESP8266 or ESP8266/ESP8285 based device with at least 1MB flash memory <br>

* *Arduino IDE and the following libraries:*<br>
[My fork of WifiManager library (development branch) by tzapu/tablatronix](https://github.com/ElToberino/WiFiManager_for_Multidisplay)<br>

* *Installed boards:*<br>
[ESP8266 core for Arduino](https://github.com/esp8266/Arduino) (compiled with V 2.7.4)<br>

* *Recommended tools:*<br>
[Arduino ESP8266 LittleFS Filesystem Uploader](https://github.com/earlephilhower/arduino-esp8266littlefs-plugin)<br>
<br>

## Important Notes<br>
This code has been made for ESP8266. There is a large number of smart devices available basing on this chip - some of them are easily flashable with a custom firmware. Many tips and tutorials can be found in the web explainig how this flashing process can be made. I don't give any advise concerning this because it can be (potentially) very dangerous: Most of these devices are working with mains voltage - so modifying these devices can become a life threatening thing, if you don't have the expertise for electrical works!
As clearly stated in the license *the code is published "without any warranty; without even the implied warranty of merchantability or fitness for a particular purpose."*<br>
<br>
**General information about smart devices, smart plugs etc.**<br>
A lot of smart devices are used for switching loads on and off. It is very important (!) to keep within the specifications of the device and not to exceed the maximum load declared on the devices. (Of course, this should be self-evident and a matter of common sense - or as we say: "Hausverstand". Having read through a lot of forums and hearing complaints about melt-down or burnt-off devices that people have used to switch large boilers etc., I feel myself forced to give this hint). I myself wouldn't even think about reaching the maximum load - high loads should always be switched by *[contactors](https://en.wikipedia.org/wiki/Contactor)* (German: "*[Schützschalter](https://de.wikipedia.org/wiki/Sch%C3%BCtz_(Schalter))")*.<br>
<br>
Loads including a *"Switching Power Supply"* (most of the modern devices and gadgets have inbuilt SWPs) can also cause problems, because - in the moment of switching on - many SWPs draw very high inrush currents, exceeding the maxium rated load of the device by multiple times. Of course, only for a short time of some ms, but the resulting arc between the switching contacts of the relay can weld them together and destroy your switching device. This can be prevented by using *contactors* or *inrush current limiters*.<br>
Many people are not aware, that even a couple of simlutaniously switched on "retrofit LED bulbs" can cause this damage, though the rated current of these lamps is very low. But each of these has a small built-in SWP and, in total, this can be too much load for the relay contacts. You can often read complaints like "My smart device has been damaged after some weeks and can't be switched off any more" - but mostly this isn't a failure of the smart device but of the wrong or not properly calculated load attached to it. <br>
<br>

## Credits
This project wouldn't have been possible without the work of many others:
* Special thanks to Jens Fleischer - the timeswitches presented on his site are the nucleus around which I built my own version of a timeswitch.<br>
His fantastic website www.fipsok.de is one of the best places in the web to find inspiration and help concerning ESP8266 and ESP32 projects. Furthermore, the projects on his site enabled me to learn a lot about Javascript functions, which are an essential part of this project.
* HTML background pattern graphic by Henry Daubrez, taken from [thepatternlibrary.com](http://thepatternlibrary.com/).
* Thanks to the many, many other programmers and enthusiasts in the web whose work and helpfulness enabled me to realize such a project.


</details>

