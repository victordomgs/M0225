# WLAN

## Fonaments de les xarxes sense fil

Les xarxes sense fil (Wireless Local Area Network) es basen en la transmissió de dades mitjançant **ones electromagnètiques**, eliminant la dependència de la infraestructura física de cablejat.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Figura%2023.png" width="450" height="auto"/>
  </div>

### A. L'Estàndard IEEE 802.11

Totes les xarxes WiFi operen sota l'estàndard **IEEE 802.11**, que ha evolucionat per oferir majors velocitats i millor gestió de l'espectre:

- **802.11b:** Opera a la banda de 2.4 GHz i ofereix una velocitat de fins a 11 Mbps.
- **802.11g:** Millora l'anterior arribant fins als 54 Mbps a la mateixa freqüència de 2.4 GHz.
- **802.11n (WiFi 4):** Introdueix la tecnologia MIMO (múltiples antenes) i pot operar en 2.4 GHz i 5 GHz.
- **802.11ac (WiFi 5):** Centrat en la banda de 5 GHz per oferir velocitats de gigabit.

### B. Conceptes de Rendiment i Senyal

Per optimitzar una xarxa sense fil, cal comprendre com viatgen les dades i quins factors les frenen:

- **Throughput:** Representa la velocitat real de transferència de dades (el "caudal" efectiu), que sempre és inferior a la velocitat teòrica de l'estàndard a causa de les capçaleres de protocol i interferències.
- **Latència:** El temps que triga un paquet de dades a anar des de l'emissor fins al receptor.
- **Tx Power (Potència de Transmissió):** Determina la força amb la qual el router emet el senyal; una potència més alta millora la cobertura però pot augmentar les interferències amb xarxes veïnes.
- **Interferències:** Degradació del senyal causada per altres xarxes WiFi o aparells electrònics (com microones o Bluetooth) que operen en les mateixes freqüències.

  <div style="text-align: center;">
    <img src="https://en.wikipedia.org/wiki/Wireless_LAN#/media/File:Roaming01.svg" width="450" height="auto"/>
  </div>

### C. Gestió de l'Espectre: Canals

Les bandes de freqüència es divideixen en canals per permetre que múltiples xarxes coexisteixin.

A la banda de 2.4 GHz, els canals se solapen entre ells. Es recomana utilitzar els canals 1, 6 i 11 perquè són els únics que no tenen interferències mútues.

### D. Identificació de la Xarxa

- **SSID (Service Set Identifier):** És el nom públic de la xarxa que veuen els usuaris.
- **BSSID:** És l'adreça física (MAC) de la ràdio del punt d'accés que està servint la xarxa.
- **ESSID:** S'utilitza quan diversos punts d'accés comparteixen el mateix SSID per cobrir una àrea gran, permetent el roaming de l'usuari.

### E. Mecanismes d'Accés i Control

- **Beacon Interval:** El temps entre les ràfegues de senyal que el router envia per anunciar la seva presència als clients.
- **RTS/Fragmentation Threshold:** Paràmetres avançats que ajuden a gestionar col·lisions de dades en entorns amb molts obstacles o molta càrrega de trànsit.

## Identificació i estructura de la xarxa


## Dispositius i modes de funcionament



## Seguretat en xarxes WIFI



