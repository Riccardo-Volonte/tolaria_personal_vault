---
type: Note
---
# Capitolo 11

# Sicurezza

Insieme delle misure organizzative e tecnologiche atte ad assicurare ad un utente autorizzato l’accesso a tutti e soli i servizi e le risorse previsti per quello specifico utente.

- Integrità → sono impedite modifiche accidentali o da parte di agenti non autorizzati.
- Autenticità → il mittente è sempre riconoscibile, quindi può ripudiare l’origine dell’informazione.
- Autenticazione → ogni agente deve essere identificato prima di interagire con il sistema.
- Riservatezza → nessun utente può dedurre informazioni che non è autorizzato a conoscere.
- Disponibilità → il sistema deve comunque offrire i servizi a cui l’utente è autorizzato ad accedere.

# Minacce

- Fisiche → danneggiamento degli impianti ed infrastrutture.
- Logiche → sottrazione o corruzione di informazioni e risorse.
- Accidentali (errori di configurazione, malfunzionamenti, errori di data entry, …)

Violazione → conseguenza della minaccia.

- Exploit → tecnica che sfrutta una vulnerabilità del sistema per causarne condotte anomale.
- Attacco → atto finalizzato a furto, alterazione o distruzione dei cosiddetti “target”.

A livello di rete:

- Sniffing → intercettazione di messaggi scambiati fra agenti.
- Spoofing → invio di pacchetti con indirizzo sorgente contraffatto per elude l’autenticazione.
- Hijacking → sniffing + spoofing = un agente malevolo intercetta e manipola il traffico.
  - Flooding → intasamento della rete inviando richieste-zavorra in massa (DoS).
- A livello applicativo:
  - Phishing → invio di messaggi che fingono di essere da un mittente autorevole.
  - Malware → software finalizzato ad infliggere danni al sistema:
    - Virus → eseguibile che infetta file per riprodursi e diventare più potente.
    - Worm → eseguibile autoreplicante (non necessita di infettare file).
    - Trojan → applicativo apparentemente utile contenente codice malevolo nascosto.
    - Ransomware → limita le funzionalità del dispositivo fino al pagamento del ransom.
    - Backdoor → punto d’accesso segreto che elude la sicurezza.
    - Spyware → spiano e trasmettono informazioni sul sistema non-consensualmente.
    - Attacco a vulnerabilità zero-day → vulnerabilità per cui il produttore ignaro non ha tempo per risolvere il problema con conseguenti ripercussioni sul sistema.

# Tecniche di difesa

Documento di policy → definisce le regole sugli accessi.

- Sistema aperto/chiuso → azioni non prescritte dal documento di policy sono consentite/vietate.
- DAC/MAC (Discretionary / Mandatory Access Control) → il proprietario della risorsa può/non può elargirne i privilegi.

## Crittografia simmetrica

Una chiave segreta è condivisa in modo sicuro tra gli interlocutori; permette di decrittare i messaggi.

- La chiave deve essere cambiata spesso per annullare eventuali sforzi di crittoanalisi.
- Codifica e decodifica veloci.

Tecniche (sovrapponibili):

![image.png](attachment:2d333dc9-d725-4a31-8deb-437ac9af2ec9:216fb72f-ab29-4a1e-8fa6-89f2ada22e23.png)

- Sostituzione → ogni carattere è sostituito ad un altro (es. cifrario di Cesare).
- Trasposizione → le lettere sono permutate.

## Crittografia asimmetrica

Ogni agente è dotato di una chiave pubblica ed una privata; un messaggio cifrato con una delle due chiavi può essere decifrato solo con l’altra.

- Crittografia con chiave pubblica del destinatario.
  - Riservatezza OK: solo il destinatario può decifrare.
  - Autenticazione KO: sensibile ad hijacking.
- Crittografia con la propria chiave privata
  - Riservatezza KO: sensibile a sniffing.
  - Autenticazione OK: solo il mittente può cifrare.

Sovrapporre le due crittografie garantisce sia autenticazione che riservatezza, ma è molto oneroso computazionalmente; infatti si usa la asimmetrica per scambiarsi chiavi per la simmetrica, poi si prosegue con quella.

## Hash

Una funzione di hash trasforma un messaggio di lunghezza arbitraria in un output di lunghezza fissa chiamato “impronta digitale”, “hash” o “digest” del messaggio originale.

- Coerenza: messaggi uguali hanno stesso hash.
- Univocità: molto improbabile che messaggi diversi abbiano stesso hash.
- Non invertibilità: il messaggio non è deducibile dall’hash.

L’hash è prova dell’integrità del messaggio: viene spedito insieme al messaggio; il mittente ricalcola l’hash dal messaggio ricevuto e verifica che coincida.

## Firma digitale

Hash del messaggio crittografato con chiave privata del mittente.

Il destinatario decritta la firma con la chiave pubblica del mittente e ricalcola l’hash del messaggio per verificare che coincidano.

Poiché la firma dipende anche dal contenuto:

- Documenti diversi con stesso mittente hanno firme diverse
- Non ripudio: è dimostrabile che il documento non è stato modificato dopo la firma.

# Gestione delle chiavi, certificati digitali

- Generazione: le chiavi dovrebbero essere generate dagli interlocutori stessi con algoritmi RNG.
- Conservazione:
  - File cifrati protetti da password
  - Dispositivi hardware rimovibili
  - Dispositivi “attivi” che gestiscano anche le operazioni di crittografia.
- Scambio:
  - OOB (Out Of Band): le chiavi sono scambiate su un canale differente.
  - Crittografia asimmetrica sulle chiavi.
  - Ci si appella ad un “key distribution center” (terza parte).

Le chiavi pubbliche sono distribuite come una struttura dati del tipo PKC (Public Key Certificate) e sono generate e gestite (per esempio revocate in caso di furto della relativa private key) dalla PKI (Public Key Infrastructure) locale.

![image.png](attachment:7b28ae1b-40de-439c-8980-d2c716b262a6:511c4317-6cc5-49dc-b162-62cfe231a7f9.png)

# Gestione degli utenti, controllo degli accessi

![image.png](attachment:b099dbc8-4f24-43c8-a6ec-5eab057f91eb:81eebe41-fb8a-42a0-ab8a-bdaee5796e07.png)

Un agente può essere identificato da:

- SYK (Something You Know) → informazione conosciuta (es. password)
- SYH (Something You Have) → oggetto posseduto (es. keycard)
- SYA (Something You Are) → caratteristiche fisiche (es. impronta)

Nella 2FA ed in generale nella MFA (Multi Factor Authentication) vengono impiegati più di questi criteri per autenticare l’utente.

# Controllo di accesso ai dati

Le regole di accesso al DBMS sono composte da:

- Autorizzatori → il proprietario di una risorsa ne gestisce gli accessi
- Soggetti → definiti dal ruolo, applicativo, transazione, …
- Oggetti → la granularità degli accessi è importante
- Diritti → modalità di accesso

![image.png](attachment:afefafaa-5b50-42b4-9bba-3e914a1fe50a:429c6eb9-ae76-4ca1-bf00-a22596ba18f8.png)

Le politiche MAC proteggono gli oggetti assegnandovi un livello di sensitività e legittima i soggetti assegnandovi un livello di clearance.

# DBMS in sistema DAC

Il controllo di accesso può definito nel profilo e nella descrizione dell’oggetto, oppure si possono definire e “concedere” agli utenti viste definite ad hoc.

![image.png](attachment:e77e6c90-3f8d-4263-a8f0-94d06bf632a1:7d7229f9-e4f2-445d-b398-04374e5efcee.png)

Modello a 6 componenti in ambienti DAC:

$$\
(gtor, gtee, obj, right, constraint, prop_rule)\
$$

dove prop_rule = nessuna propagazione / Unbounded Propagation / Bounded Propagation (es. catena limitata di utenti, tempo limite) dei permessi di accesso.

# DBMS in sistema MAC

- Polinstanziazione → esistono tante copie fisiche della stessa tabella, fisicamente separate: varianti che dipendono dal livello di sicurezza.
- MLR (Multi Level Relation) → ciascuna tabella è istanziata con attributi extra che ne gestiscono i permessi: a ciascun record è aggiunto un attributo che specifichi il livello della tupla, a ciascun attributo corrisponde un altro attributo che specifichi la sensibilità dell’attributo.

Un soggetto può accedere in lettura solo alle istanze di una MLR di livello uguale o minore al proprio.

In scrittura, si ha polinstanziazione se l’elemento da inserire esiste già con quel nome.

![image.png](attachment:b55eb03e-e898-4b7c-9bb1-180c777110f5:cfd29fb9-3c19-4824-8f19-b07590d9ada7.png)

# Meccanismi di sicurezza infrastrutturali

## Firewall

Insieme di componenti hardware/software che collegano una rete fidata ad una rete insicura, attuando policy di sicurezza al traffico dati passante. Il firewall deve essere l’unico punto di contatto con l’esterno. Tutti i pacchetti devono essere bloccati se non autorizzati.

- IDS (Intrusion Detection System) → componente hardware/software che monitora gli eventi di sistema per rilevare intrusioni.
- Screening Router → dispositivo che instrada oppure blocca i pacchetti in transito fra la rete interna e quella esterna.
- Packet Inspection → valutano i pacchetti sulla base del loro payload.
- Application Proxy → processo eseguito su un proxy di tipo Application Gateway che si pone a livello applicativo nella comunicazione fra componenti di una specifica applicazione, che rielabora tutti i messaggi prima di inviarli. Impedisce messaggi malevoli, ma è lento.

![image.png](attachment:4105b81f-6055-46f5-863c-f61bc365d7db:7db0624f-a5ac-433b-bbc8-f9938f7a421c.png)![image.png](attachment:769e7690-c728-44f3-afd4-203c7ce4586f:c46dd6f8-b348-4686-8f81-1ca7b372279b.png)

## IDS (Intrusion Detection System)

- Intrusione → insieme di azioni atto a compromettere la sicurezza.
- Intrusion Detection (ID) → monitoraggio degli eventi del sistema per rilevare tracce di intrusioni.
- Intrusion Prevention → estensione di ID con controllo di accesso alle risorse.
- IDS → automatizza ID

Un IDS è composto da:

- Sensori (Information Source) che raccolgono elementi che possano costituire evidenze di intrusione.
- Algoritmi di analisi che implementano ID.
- Componenti attivi “Alerting & Response” che reagiscono al rilevamento di intrusioni con azioni che vanno dalla reportistica alle contromisure.

Classificazione secondo Information Source:

- Network-based → analizza il traffico di rete. Richiede pochi sensori ed è di semplice configurazione, ma è poco efficiente in condizioni di congestione, non può decifrare pacchetti e può essere eluso con pacchetti anomali. Infine non può inferire il successo di un attacco.
- Host-based → software da installare su ogni macchina che analizza processi e utenti con grande precisione. Più efficace di Network-based (può anche analizzare dati cifrati e rilevare Trojan) ma sono difficilmente gestibili e scalabili e possono essere disabilitati da DoS. Alto impatto sulle prestazioni della macchina.

Classificazione secondo tipo di analisi:

- Misuse detection → confronta le attività del sistema con “signature” (pattern di condotta correlati ad attacchi noti). Pochi falsi allarmi, rilevamento tempestivo di certi attacchi specifici. Le signature vanno aggiornate frequentemente e sono comunque troppo specifiche per offrire copertura completa (per esempio varianti di attacchi noti).
- Anomaly detection → costruisce profili che descrivono la normale condotta individua utenti, host, reti, … e misurano vari indicatori aggregati che devono rimanere al di sotto di una soglia di normalità. Rilevano molti attacchi anche originali. Molti falsi allarmi e non riportano dettagli dell’attacco.

Classificazione IDS secondo “response” (reazione all’attacco):

- Active response → ricerca maggiori informazioni aumentando la sensitività delle Information Source e/o modifica l’ambiente resettando e riconfigurando componenti nel tentativo di bloccare l’attacco.
- Passive response → notifica l’amministratore di sistema e lascia che gli operatori gestiscano l’attacco.
