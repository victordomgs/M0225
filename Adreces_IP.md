# Protocol IP

El **Protocol d'Internet (IP)** és el protocol de comunicacions de la **capa de xarxa** de la suite de protocols d'Internet per transmetre **datagrames** a través de les fronteres de la xarxa. La seva funció d'**encaminament** (routing) permet la interconnexió de xarxes i, essencialment, estableix el que coneixem com a Internet.

L'IP té la tasca de lliurar **paquets** des de l'**amfitrió** (*host*) d'origen fins a l'amfitrió de destinació basant-se únicament en les **adreces IP** que figuren a les **capçaleres** dels paquets. Amb aquesta finalitat, l'IP defineix estructures de paquets que **encapsulen** les dades que s'han de lliurar. També defineix els mètodes d'adreçament que s'utilitzen per etiquetar el datagrama amb la informació d'origen i de destinació.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image14.png" width="350" height="auto"/>
  </div>

---

## Funcions

El **Protocol d'Internet** és l'encarregat d'adreçar les **interfícies dels amfitrions** (*hosts*), encapsular les dades en datagrames (incloent-hi la **fragmentació i el reensamblatge**) i encaminar els datagrames des d'una interfície d'origen fins a una de destinació a través d'una o més xarxes IP. Amb aquests fins, l'IP defineix el format dels paquets i proporciona un sistema d'adreçament.

Cada datagrama consta de dos components: una capçalera (*header*) i una càrrega útil (*payload*).

- La **capçalera IP** inclou una adreça IP d'origen, una adreça IP de destinació i altres metadades necessàries per encaminar i lliurar el datagrama.
- La **càrrega útil** són les dades que es transporten.

Aquest mètode d'anuar la càrrega útil de dades dins d'un paquet amb una capçalera s'anomena **encapsulament**.

### Adreçament i Encaminament

L'adreçament IP implica l'assignació d'adreces IP i els seus paràmetres associats a les interfícies dels amfitrions. L'espai d'adreces es divideix en **subxarxes**, cosa que implica la designació de prefixos de xarxa.

L'encaminament IP el realitzen tots els amfitrions, així com els **encaminadors** (*routers*), la funció principal dels quals és transportar paquets a través de les fronteres de la xarxa. Els encaminadors es comuniquen entre si mitjançant **protocols d'encaminament** específics, ja siguin protocols de pasarel·la interior (*interior gateway protocols*) o exterior, segons les necessitats de la topologia de la xarxa.

---

## Mètodes d'adreçament d'IP

Existeixen quatre mètodes principals d'adreçament en el Protocol d'Internet:

- **Unicast (Unidifusió):** Lliura un missatge a un sol node específic mitjançant una associació **un a un** entre un emissor i una destinació; cada adreça de destinació identifica de manera única un sol punt final receptor.
- **Broadcast (Difusió):** Lliura un missatge a tots els nodes de la xarxa mitjançant una associació **un a tots**; un sol datagrama (o paquet) d'un emissor s'encamina a tots els possibles punts finals associats a l'adreça de difusió. La xarxa replica automàticament els datagrames segons sigui necessari per arribar a tots els destinataris dins de l'abast de la difusió, que generalment és una subxarxa sencera.
- **Multicast (Multidifusió):** Lliura un missatge a un grup de nodes que han expressat interès a rebre'l mitjançant una associació **d'un a molts d'entre molts o de molts a molts d'entre molts**; els datagrames s'encaminen simultàniament en una sola transmissió a molts destinataris. El multicast es diferencia del broadcast en el fet que l'adreça de destinació designa un subconjunt, no necessàriament tots, dels nodes accessibles.
- **Anycast:** Lliura un missatge a qualsevol node d'un grup, normalment al més proper a l'origen, mitjançant una associació **d'un a un d'entre molts**. Els datagrames s'encaminen a un sol membre d'un grup de receptors potencials que estan tots identificats per la mateixa adreça de destinació. L'algoritme d'encaminament selecciona el receptor únic del grup basant-se en quin és el més proper segons alguna mesura de distància o de cost.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image15.jpg" width="450" height="auto"/>
  </div>

