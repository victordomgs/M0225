# Switching & Routing

## 1. Fonaments de maquinari i interconnexió

Per entendre com configurar una xarxa, primer cal conèixer els "maons" que la formen. Els dispositius d'interconnexió són els elements clau que permeten que les dades viatgin d'un punt a un altre.

## L'encaminador (router)

L'encaminador és el dispositiu més important de la XAL. La seva missió principal és interconnectar diferents xarxes i permetre la comunicació entre elles.

- **Funcionament:** Treballa fins a la **Capa 3(Xarxa)** del model OSI.
- **Adreçament:** Té assignada una adreça IP i utilitza ports per connectar cada xarxa individual.
- **Decisió de ruta:** Quan rep un paquet, comprova l'adreça de destinació i el transmet pel camí més adient. 

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image18.png" width="650" height="auto"/>
  </div>

### Arquitectura interna

Un encaminador funciona, en essència, com un ordinador especialitzat i comparteix gairebé tots els seus components.

- **CPU:** Processa les instruccions del sistema i gestiona l'encaminament.
- **RAM (Memòria volàtil):** Emmagatzema la taula d'encaminament i la configuració que s'està executant en el moment (`running-config`).
- **Memòria Flash:** On es desa el sistema operatiu (IOS o Firmware).
- **NVRAM:** Memòria no volàtil on es guarda la configuració d'arrencada (`startup-config`).
- **ROM:** Conté el programari de diagnòstic i les instruccions d'arrencada bàsiques.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image19.png" width="450" height="auto"/>
  </div>

### Interfícies i connexions físiques

A la part posterior dels dispositius trobem els punts de connexió amb el món exterior.

- **Ports LAN (Fast Ethernet/Gigabit):** Per a la connexió de dispositius dins de la xarxa local.
- **Ports WAN (Internet):** Per connectar el router cap a una xarxa externa o el mòdem de l'ISP.
- **Ports Sèrie (Serial):** Utilitzats per a connexions punt a punt entre routers de llarga distància; requereixen configurar el `clock rate` en el costat DCE.
- **Port de Consola:** Port especial (normalment de color blau) per a la configuració inicial del dispositiu mitjançant un ordinador i un cable de consola.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image20.png" width="450" height="auto"/>
  </div>

## El Commutador (Switch)

Mentre que l'encaminador connecta xarxes entre si, el commutador és el dispositiu encarregat d'interconnectar equips dins d'una mateixa Xarxa d'Àrea Local (XAL). La seva funció principal és gestionar el trànsit de dades de manera eficient i segura a la Capa 2 (Enllaç) del model OSI.

### Com funciona un Switch?

A diferència d'un concentrador (hub), que envia la informació a tots els ports, el switch és "intel·ligent":

- **Aprenentatge d'adreces MAC:** El switch llegeix l'adreça física (MAC) de cada trama que rep i aprèn a quin port està connectat cada dispositiu.
- **Taula de commutació:** Emmagatzema aquestes adreces en una taula interna per saber exactament on enviar cada dada.
- **Forwarding (Reenviament):** Quan arriba un paquet, el switch decideix per quin port l'ha de treure basant-se en la seva taula, evitant saturar la resta de la xarxa.
- **Eliminació de col·lisions:** Cada port del switch és un domini de col·lisió independent, la qual cosa redueix dràsticament la congestió del trànsit.
