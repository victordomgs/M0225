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



