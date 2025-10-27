# 1. Introducció

Quan parlem de xarxes d’ordinadors, diferents dispositius (ordinadors, routers, impressores, etc.) han de poder comunicar-se entre ells, encara que siguin de marques i tecnologies diferents.  

Als anys 70 i 80, cada fabricant utilitzava els seus propis protocols, cosa que feia molt difícil la comunicació entre sistemes. Per resoldre aquest problema, la **ISO (International Organization for Standardization)** va crear el **model OSI (Open Systems Interconnection)**.

Aquest model proposa una manera **estàndard d’organitzar la comunicació** entre dispositius dividint-la en **set capes**, cadascuna amb una funció concreta.  

Així, cada fabricant pot dissenyar els seus dispositius o programes seguint les mateixes regles i garantir que **tots els sistemes siguin compatibles**.

En resum, el model OSI és com un **llenguatge comú** que permet que qualsevol ordinador pugui “parlar” amb qualsevol altre.

<br>

# 2. Què és el model OSI

El **model OSI** és una manera d’entendre com es comuniquen dos dispositius dins d’una xarxa.  

Imagina que és com una **cadena de set passos**, on cada pas (o capa) s’encarrega d’una part del procés de comunicació.

Cada capa té una **funció específica** i només es comunica amb la capa que té just a sobre i la que té just a sota.  

Això vol dir que una capa no necessita saber com treballen les altres, només ha d’entendre com parlar amb les seves “veïnes”.

Per exemple, quan **enviem un fitxer a un altre ordinador**, aquest fitxer:
1. Passa per diverses capes dins del teu ordinador: una capa s’encarrega de dividir-lo, una altra de posar-hi adreces, una altra de convertir-lo en bits…
2. Després viatja per la xarxa (cables o Wi-Fi) fins a l’altre dispositiu.
3. En arribar, el procés es fa **a l’inrevés**: les capes del receptor el tornen a muntar fins que arriba a la capa que mostra el fitxer a l’usuari.

Aquest sistema de capes permet **entendre, dissenyar i solucionar problemes de xarxa** d’una manera més senzilla, ja que sabem exactament on buscar l’origen d’un error o com millorar una part concreta de la comunicació.

<br>

# 3. Les set capes del model OSI

El model OSI divideix la comunicació de xarxa en **set capes**. 

Cada capa té una **funció específica** i treballa conjuntament amb les altres per permetre que la informació viatgi des de l’aplicació d’un usuari fins al dispositiu destinatari.

| Nº | Nom de la capa            | Funció principal                                                                 | Tipus de dades (PDU) | Dispositius o protocols associats |
|----|----------------------------|----------------------------------------------------------------------------------|-----------------------|----------------------------------|
| 7  | **Aplicació**              | Permet la interacció directa amb l’usuari i ofereix serveis com correu, web, etc. | Dades                | HTTP, FTP, SMTP, DNS, navegadors |
| 6  | **Presentació**            | Tradueix, xifra o comprimeix les dades perquè siguin comprensibles per les aplicacions. | Dades                | SSL/TLS, formats JPEG, MPEG, GIF |
| 5  | **Sessió**                 | Controla l’inici, manteniment i finalització d’una comunicació entre dispositius. | Dades                | RPC, NetBIOS, sockets            |
| 4  | **Transport**              | Segmenta la informació, assegura l’entrega i gestiona la retransmissió d’errors. | Segments             | TCP, UDP                         |
| 3  | **Xarxa**                  | S’encarrega d’encaminar els paquets cap a la seva destinació a través de diferents xarxes. | Paquets              | IP, ICMP, IPsec, routers         |
| 2  | **Enllaç de dades**        | Organitza la informació en trames i gestiona les adreces físiques (MAC).        | Trames               | Ethernet, Wi-Fi, commutadors (switch) |
| 1  | **Física**                 | Converteix les dades en senyals elèctrics, òptics o de ràdio i transmet bits.   | Bits                 | Cables, connectors, hubs, repetidors |

Cada capa depèn de la capa inferior per transmetre la informació i ofereix serveis a la capa superior.  

Aquesta organització facilita la **compatibilitat entre dispositius i protocols** de diferents fabricants.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image7.png" width="1200" height="auto"/>
  </div>

<br>

# 4. Explicació capa per capa

A continuació veurem cadascuna de les set capes del model OSI explicades de manera senzilla, amb exemples i analogies que t’ajudaran a entendre què fa cadascuna.


## 🟣 Capa 7 – Aplicació

**Funció:**  
És la capa més propera a l’usuari. Permet la interacció directa entre les aplicacions (com el navegador o el client de correu) i la xarxa.  

**Exemple:**  
Quan obres una pàgina web amb el navegador, és aquesta capa la que s’encarrega de demanar la informació al servidor web.  

**Protocols o dispositius:**  
HTTP, HTTPS, FTP, SMTP, DNS.


## 🔵 Capa 6 – Presentació

**Funció:**  
S’encarrega de **traduir, xifrar o comprimir** les dades perquè la informació tingui el format correcte per a les aplicacions.  

**Exemple:**  
Quan reprodueixes un vídeo, aquesta capa s’encarrega de descomprimir el fitxer perquè puguis veure’l correctament.  

**Protocols o formats:**  
SSL/TLS (xifratge), formats JPEG, MPEG, MP3, GIF.


## 🟢 Capa 5 – Sessió

**Funció:**  
Controla quan comença i acaba la comunicació entre dos dispositius. Pot reiniciar una sessió si s’interromp.  

**Exemple:**  
Quan et connectes a una videotrucada, aquesta capa manté la sessió oberta mentre dura la conversa.  

**Protocols:**  
NetBIOS, RPC, sockets.


## 🟡 Capa 4 – Transport

**Funció:**  
Garanteix que les dades arribin correctament i en l’ordre correcte. Divideix la informació en segments i pot tornar a enviar parts si s’han perdut.  

**Exemple:**  
Quan descarregues un fitxer gran, aquesta capa s’encarrega que totes les parts arribin bé i es tornin a ordenar.  

**Protocols:**  
TCP (fiable), UDP (ràpid però sense control d’errors).


## 🟠 Capa 3 – Xarxa

**Funció:**  
Decideix **per on** han de viatjar els paquets de dades fins arribar al seu destí. Gestiona les adreces IP i l’encaminament (routing).  

**Exemple:**  
Quan envies un correu a algú d’un altre país, aquesta capa tria la millor “ruta” per fer arribar la informació.  

**Protocols i dispositius:**  
IP, ICMP, IPsec, routers.


## 🔴 Capa 2 – Enllaç de dades

**Funció:**  
Organitza les dades en trames i les envia a través d’un mitjà físic. També s’encarrega d’afegir l’adreça **MAC** i de detectar errors bàsics.  

**Exemple:**  
Quan un ordinador envia dades dins d’una xarxa local, aquesta capa s’assegura que arriben al dispositiu correcte segons la seva adreça MAC.  

**Protocols i dispositius:**  
Ethernet, Wi-Fi, commutadors (switch).


## ⚫ Capa 1 – Física

**Funció:**  
Transmet els bits (0 i 1) com a senyals elèctrics, òptics o de ràdio a través del cable o l’aire.  

**Exemple:**  
Quan envies un missatge per WhatsApp, finalment la informació es converteix en impulsos elèctrics o ones que viatgen pel cable o per Wi-Fi.  

**Dispositius:**  
Cables, connectors, repetidors, hubs, targetes de xarxa (NIC).

<br>

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image8.png" width="1200" height="auto"/>
  </div>

<br>

# 5. Unitats d’informació (PDU)

Quan les dades passen per les diferents capes del model OSI, **canvien de forma i de nom**. 

Cada capa afegeix o treu informació (com adreces o codis de control) i tracta les dades com una **unitat pròpia**, anomenada **PDU** (*Protocol Data Unit*).

| Nº | Capa del model OSI       | Nom de la unitat d’informació (PDU) | Descripció breu |
|----|---------------------------|--------------------------------------|-----------------|
| 7  | **Aplicació**             | Dades                               | Informació que l’usuari vol enviar o rebre. |
| 6  | **Presentació**           | Dades                               | Dades traduïdes, xifrades o comprimides. |
| 5  | **Sessió**                | Dades                               | Dades amb informació per mantenir la sessió. |
| 4  | **Transport**             | Segments                            | Dades dividides en parts més petites per enviar-les. |
| 3  | **Xarxa**                 | Paquets                             | Segments amb adreces IP per poder ser encaminats. |
| 2  | **Enllaç de dades**       | Trames                              | Paquets amb adreces MAC per a la comunicació dins la xarxa local. |
| 1  | **Física**                | Bits                                | Senyals elèctrics, òptics o de ràdio que viatgen pel mitjà físic. |

Podem imaginar aquest procés com una **cadena d’embalatges**:  
- Cada capa afegeix una “caixa” o “etiqueta” al missatge perquè sàpiga com i on ha d’arribar.  
- Quan arriba al destí, les capes les van traient una per una fins que l’usuari rep les dades originals.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image9.png" width="750" height="auto"/>
  </div>

# 6. Implementació en dispositius

No tots els dispositius de xarxa treballen amb totes les capes del model OSI.  

Cada tipus de dispositiu implementa només aquelles capes que necessita per realitzar la seva funció.

| Dispositiu | Capa o capes que implementa | Explicació breu |
|-------------|-----------------------------|-----------------|
| **Host (ordinador, mòbil, servidor)** | Totes les **7 capes** | Necessita totes les capes per poder crear, enviar, rebre i mostrar informació a l’usuari. |
| **Router** | Capa **3 – Xarxa** (i inferiors) | S’encarrega d’encaminar els paquets entre xarxes diferents. Treballa amb adreces IP. |
| **Switch** | Capa **2 – Enllaç de dades** (i capa 1) | Envia les trames dins d’una mateixa xarxa local segons l’adreça MAC dels dispositius. |
| **Hub** | Capa **1 – Física** | Simplement rep els bits i els replica per tots els ports. No interpreta cap informació. |

💡 **Recorda:**  
Com més amunt treballa un dispositiu dins del model OSI, **més “intel·ligent”** és, ja que pot entendre més informació sobre el contingut i la destinació de les dades.

<br>

# 7. El model TCP/IP

## Introducció històrica

Abans que s’estandarditzés el model OSI, el Departament de Defensa dels Estats Units va desenvolupar un altre model per a la seva pròpia xarxa: **ARPANET**, considerada l’origen d’Internet.  
D’aquell projecte va néixer el **model TCP/IP**, que es basa en dos protocols principals:
- **TCP (Transmission Control Protocol)** → garanteix que les dades arribin correctament.
- **IP (Internet Protocol)** → s’encarrega d’encaminar-les fins al destí correcte.

Tot i que el model OSI és molt útil per entendre com funciona una xarxa, **Internet utilitza realment el model TCP/IP**, perquè és més senzill i pràctic per implementar.

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image10.png" width="550" height="auto"/>
  </div>


## Correspondència entre el model OSI i el model TCP/IP

El model TCP/IP té **4 capes**, que agrupen les 7 del model OSI.  
A la taula següent pots veure com es corresponen:

  <div style="text-align: center;">
    <img src="https://github.com/victordomgs/M0225/blob/main/images/Image11.jpg" width="1200" height="auto"/>
  </div>


## Per què s’utilitza actualment el model TCP/IP

- És **més pràctic i implementat**: la majoria de protocols d’Internet (HTTP, SMTP, FTP, DNS...) estan basats en TCP/IP.  
- És **més simple**: només quatre capes, però cobreixen les mateixes funcions essencials.  
- És **l’estàndard d’Internet**: utilitzat per tots els dispositius connectats avui en dia.

En resum, podem dir que el **model OSI serveix per aprendre i comprendre** com funcionen les xarxes, mentre que el **model TCP/IP és el que s’utilitza realment** en el món pràctic.
