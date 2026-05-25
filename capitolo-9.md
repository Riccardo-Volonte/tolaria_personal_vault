---
type: Note
---
# Capitolo 9

# Architettura fisica

Detta “centralizzata” se dati ed applicazioni risiedono sullo stesso nodo, altrimenti “distribuita”.

- Single Tiered → P,A,D assegnati ad un’unica macchina, generalmente il mainframe.
  - Prestazioni elevate
  - Sicurezza
  - Semplicità di manutenzione dell’architettura.
  - Applicazione monolitica: scarsa flessibilità.
  - L’elaborazione grafica (costosa) deve anch’essa essere assegnata al mainframe.
- Two-Tiered → P,A,D divisi in due nodi (generalmente il mainframe ed il Client).
  - Thin Client → gestisce solo P.
  - Thick Client → gestisce P e A.
- Three-Tiered / N-Tiered → P,A,D suddivisi fra mainframe, alcuni server intermedi (per ammortizzare il carico elaborativo), Client.

# Scalabilità

- Scale-up → si potenzia la capacità elaborativa dei nodi.
  - Semplice.
  - Non sempre applicabile, o comunque non sempre efficace.
- Scale-out → replicazione dei nodi che formano il collo di bottiglia.
  - Principio di downsizing: a parità di potenza di calcolo complessiva, i costi di server di fascia bassa sono minori dei server di fascia alta.
  - Necessario introdurre un sistema di load balancing.

# Dimensionamento

Importante valutare il dimensionamento del server per soddisfare le esigenze senza investire troppo.

Elasticità → capacità di dimensionare dinamicamente il server, a seconda delle fluttuazioni della quantità di richieste.

## Server Farm

Insieme di elaboratori che condividono carico, applicazioni ed eventualmente dati.

- RACS (Reliable Array of Cloned Services) → Server Farm ottenuta per clonazione: sui server sono installate le stesse applicazioni e dati.
  - Fault Tolerance: le macchine possono rimpiazzarsi a vicenda in caso di guasti.
  - Shared-nothing → dati replicati su un disco fisso locale ad ogni server.
    - Eventuali scritture devono essere propagate a tutti gli altri server.
    - Poco adatto per servizi “write-intensive”.
  - Shared-disk → i cloni condividono un server di memorizzazione che gestisce i dischi fissi.
- RAPS (Reliable Array of Partitions Servers) → Server Farm ottenuta per partizionamento: ogni nodo svolge una funzione specializzata ed i dati sono ripartiti appropriatamente.
  - Graceful Degradation: in caso di guasti, alcune funzionalità potrebbero non essere più disponibili; infatti i RAPS prevedono che i singoli server siano clonati.
  - Concilia scalabilità e disponibilità del servizio.

## Virtualizzazione

- CPU virtuale → componente software che l’utilizzatore invoca per supportarlo nell’elaborazione e che reindirizza la richiesta ad una CPU fisica associata.
  - Degrado delle prestazioni
  - Scoppia le risorse fisiche dall’applicazione
  - Fraziona una singola risorsa fisica in più risorse virtuali
  - Permette la condivisione della stessa risorsa fisica in maniera trasparente.
- Macchina virtuale → insieme delle risorse virtuali necessarie al funzionamento di un’applicazione.
- Hypervisor → strato software che gestisce la corrispondenza tra risorse fisiche e virtuali.
- Server Consolidation → le macchine fisiche sono condensate in un numero minore di server su cui sono installati hypervisor che implementano le MV.

## Cloud Computing

Paradigma per la realizzazione di architetture applicative che, poggiando su sistemi virtualizzati, possono accedere a tali risorse da qualunque dispositivo connesso alla rete da qualunque località.

- Accesso alla rete onnipresente e trasparente
- On demand self-service: la piattaforma Cloud può mettere a disposizione servizi e rilasciarli quando non più necessari, offrendo quindi elasticità.
- Utility Computing: l’utente paga a consumo con l’illusione che le risorse siano infinite.
- Monitoraggio sull’utilizzo: il costo delle risorse Cloud è commisurato sulla base delle risorse effettivamente utilizzate.

Erogazione:

- IaaS (Infrastructure as a Service) → mette a disposizioni risorse fisiche, viste dagli utilizzatori come risorse virtuali.
- PaaS (Platform as a Service) → IaaS + alcune tecnologie a livello di piattaforma, messe a disposizione tramite API.
- SaaS (Software as a Service) → PaaS + veri e propri applicativi; diversi dispositivi possono accedere alla stessa applicazione condividendone i dati.

Deployment:

- Private Cloud → ad uso esclusivo.
- Community Cloud → ad uso di una comunità di organizzazioni in collaborazione.
- Public Cloud → ad uso pubblico.
- Hybrid Cloud → più Cloud dei tipi precedenti misti per colmarne le rispettive lacune.

Il grado di privatezza del Cloud lo rende più sicuro ma anche meno scalabile.
