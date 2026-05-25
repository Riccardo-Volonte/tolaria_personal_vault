---
type: Note
---
# Capitolo 8

# Architetture di integrazione

Middleware → garantisce la propagazione e la congruenza dei dati nei silos dei vari reparti. In particolare gestisce la coerenza di rappresentazione, struttura, presentazione, semantica.

## Integrazione nella logica applicativa

Implementare il dialogo tra applicazioni è semplice se sono a sistema aperto, difficile altrimenti.

## Integrazione nella presentazione

Modificare i client per richiamare le funzioni esposte lato server delle altre applicazioni.

- Le tecnologie che realizzano l’applicazione potrebbero non supportare la comunicazione via rete.
- Complicato garantire la congruenza e la correttezza di istanze d’esecuzione in parallelo.

## Architettura di integrazione punto-a-punto (SOA)

Ogni applicazione è connessa direttamente alle altre (tramite connettori oppure API).

- L’onere dell’integrazione scala molto rapidamente all’aumentare delle applicazioni.
- L’alto cablaggio della logica di integrazione rende difficile sostituire/aggiornare componenti.

SOA (Service Oriented Architecture) → le funzionalità sono realizzate come moduli tramite servizi interrogabili con HTTP/REST.

- SLA (Service Level Agreement) → definisce le caratteristiche non funzionali garantite dal servizio, in termini di parametri QoS.
- QoS (Quality of Service) → metriche utilizzate per monitorare l’esecuzione del servizio e per accertarsi che il servizio risponda in modo qualitativamente valido (tempo di risposta, disponibilità, costo operativo, …)

![image.png](attachment:35c9fa21-8b4e-4349-9278-e678a6dcbbc7:db99dc8e-afbf-45dc-832e-ffb2d078ea1d.png)

1. Service Provider pubblica a Service Registry i servizi offerti.
2. Service Requestor richiede un servizio a Service Registry.
3. Service Registry risponde come invocare il servizio a Service Requestor.
4. Service Requestor invoca il servizio.

Composizione di servizi:

- Service orchestration → determina la sequenza con cui i singoli servizi sono invocati, usando una rappresentazione simile a quella introdotta per i processi. Gli elementi sono selezionati al momento, usando il service registry, in base alle funzionalità offerte e in base allo SLA.
- Service Broker → organizzazioni che si propongono di trovare il miglior allineamento tra i servizi offerti e quelli richiesti.

![image.png](attachment:0d0d902d-9a18-4f36-a835-4ed017088a2b:2aba0609-d119-4a07-b46e-8c1f2759ac83.png)

## Architettura di integrazione hub-and-spoke (BPMS)

Un hub centrale è collegato ai vari sistemi tramite adattatori detti “spoke” e ne indirizza le richieste agli applicativi appropriati.

- Alta modularità: facile sostituire componenti.
- Gli spoke non scalano troppo rapidamente come nella punto-a-punto.
- Introduce alta complessità nella logica applicativa; le modifiche sono comunque difficili.

Integrazione con BPMS → esso, basandosi sulla descrizione formale dei processi, gestisce l’avanzamento ed il flusso di informazione tra applicazioni.

![image.png](attachment:86effb8b-0ac5-4983-8588-73527ab92663:d6f9d044-f872-45e2-bae3-d6acb87fc3dc.png)
