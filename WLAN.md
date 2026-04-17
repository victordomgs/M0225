# WLAN

## Fonaments de les xarxes sense fil

Les xarxes sense fil (Wireless Local Area Network) es basen en la transmissió de dades mitjançant **ones electromagnètiques**, eliminant la dependència de la infraestructura física de cablejat.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Figura%2023.png" width="650" height="auto"/>
  </div>

### A. L'Estàndard IEEE 802.11

Totes les xarxes WiFi operen sota l'estàndard **IEEE 802.11**, que ha evolucionat per oferir majors velocitats i millor gestió de l'espectre:

- **802.11b:** Opera a la banda de 2.4 GHz i ofereix una velocitat de fins a 11 Mbps.
- **802.11g:** Millora l'anterior arribant fins als 54 Mbps a la mateixa freqüència de 2.4 GHz.
- **802.11n (WiFi 4):** Introdueix la tecnologia MIMO (múltiples antenes) i pot operar en 2.4 GHz i 5 GHz.
- **802.11ac (WiFi 5):** Centrat en la banda de 5 GHz per oferir velocitats de gigabit.

  <div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/b/b8/WLAN_PCI_Card_cleaned.png" width="550" height="auto"/>
  </div>

### B. Conceptes de Rendiment i Senyal

Per optimitzar una xarxa sense fil, cal comprendre com viatgen les dades i quins factors les frenen:

- **Throughput:** Representa la velocitat real de transferència de dades (el "caudal" efectiu), que sempre és inferior a la velocitat teòrica de l'estàndard a causa de les capçaleres de protocol i interferències.
- **Latència:** El temps que triga un paquet de dades a anar des de l'emissor fins al receptor.
- **Tx Power (Potència de Transmissió):** Determina la força amb la qual el router emet el senyal; una potència més alta millora la cobertura però pot augmentar les interferències amb xarxes veïnes.
- **Interferències:** Degradació del senyal causada per altres xarxes WiFi o aparells electrònics (com microones o Bluetooth) que operen en les mateixes freqüències.

  <div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/b/b3/Roaming01.png" width="650" height="auto"/>
  </div>

### C. Gestió de l'Espectre: Canals

Les bandes de freqüència es divideixen en canals per permetre que múltiples xarxes coexisteixin.

A la banda de 2.4 GHz, els canals se solapen entre ells. Es recomana utilitzar els canals 1, 6 i 11 perquè són els únics que no tenen interferències mútues.

- **Banda de 2.4 GHz:** Té un abast més gran però està més saturada. Els canals se solapen entre ells; per això es recomana utilitzar els canals 1, 6 o 11, ja que són els únics que no s'interfereixen mútuament.
- **Banda de 5 GHz:** Ofereix més velocitat i menys interferències, però té menys capacitat per travessar parets.
- **Auto-tuning:** Funció que permet al router triar automàticament el canal menys congestionat del seu entorn.

## Identificació i estructura de la xarxa

Perquè una xarxa sense fil funcioni correctament, cal que estigui clarament identificada i que els seus paràmetres tècnics estiguin configurats per evitar col·lisions amb altres xarxes veïnes.

### A. L'SSID (Service Set Identifier)

L'**SSID** és el nom de la xarxa sense fil que es visualitza quan busquem xarxes disponibles des d'un dispositiu.

- **Funció:** Permet als usuaris identificar a quina xarxa s'estan connectant.
- **SSID Predeterminat:** És recomanable modificar el nom que ve de fàbrica (com "Linksys") per evitar que possibles atacants identifiquin el model de router i les seves vulnerabilitats conegudes.
- **SSID Broadcast:** Es pot desactivar la difusió del nom de la xarxa perquè no aparegui automàticament a la llista d'escaneig, obligant a l'usuari a introduir el nom manualment.

  <div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/b/b7/Hotspot-accesspoint-multiple-ssid-vlan-1400.gif" width="650" height="auto"/>
  </div>

## Dispositius i modes de funcionament

Per desplegar una xarxa sense fil, és essencial distingir entre el dispositiu físic i el rol que aquest exerceix dins de la topologia de xarxa.

### A. El Router i el Punt d'Accés (AP)

Encara que sovint s'utilitzen com a sinònims, tenen funcions diferents:

- **Punt d'Accés (AP):** És el dispositiu que permet que equips sense fil es connectin a una xarxa cablejada mitjançant antenes externes que proporcionen cobertura.
- **Router Wireless:** És un dispositiu híbrid que combina les funcions d'un encaminador (connexió entre xarxes, com Internet i la LAN) i les d'un punt d'accés WiFi.
- **Antenes:** El model Linksys utilitzat disposa de dues antenes externes per optimitzar la recepció i emissió de senyals.

  <div style="text-align: center;">
    <img src="https://upload.wikimedia.org/wikipedia/commons/d/d0/Linksys_WAP54G.JPG" width="550" height="auto"/>
  </div>

## Seguretat en xarxes WIFI



