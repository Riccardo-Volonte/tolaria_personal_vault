---
type: Note
---
# Capitolo 7

# Data Warehouse

Base di dati in sola lettura che raccoglie dati operazionali aggregati storici, di interesse per manager di alto e medio livello, per prendere decisioni sull’evoluzione aziendale ed identificare problematiche e possibilità di crescita.

![image.png](attachment:328ccc2e-45fc-4df2-b09d-c00194482d29:de1e42d7-3b52-4833-b8a4-633b621b7bcf.png)

## Operazioni ETL

- Extraction: statica oppure incrementale.
- Transformation:
  - Data cleaning → correzione degli errori di extraction.
  - Riconciliazione → messa in relazione dei dati relativi allo stesso oggetto.
  - Standardizzazione
  - Eliminazione dei duplicati
- Loading

## Metadati

- Struttura del DW
- Metadati operazionali → documentazione di storico, fonte, trasformazione.
- Statistiche d’uso

## DFM (Dimensional Fact Model)

Un DFM ha più ipercubi, ciascuno per un’analisi diversa.

![image.png](attachment:27e7972d-b724-4fbd-a3c9-ab3fa383908f:ab288bb0-faec-41d7-aef2-6138f547c678.png)![image.png](attachment:3552d61a-ae18-4d7b-810e-9567505bb574:c3c643ed-3017-4ddb-a989-ec633f2c6fe2.png)

## Modello logico

Il data warehouse è un sistema OLAP.

Classificazione:

- MOLAP (Multidimensional OLAP) → traduce il modello concettuale in una base di dati multidimensionale che può essere interrogato utilizzando motori multidimensionali progettati appositamente per trattare questa tipologia di dati.
- ROLAP (Relational OLAP) → implementazione classica relazionale.

![image.png](attachment:ef05b2c3-0caf-4c61-a59c-aa5afb7892f4:d8765343-ff0b-4ae9-86e5-31352521773b.png)![image.png](attachment:004c23a1-e646-477e-ba03-eb35d14d4338:4e3b5126-744b-4f63-b2f9-ac69e9b8dc8f.png)

- HOLAP (Hybrid OLAP) → data warehouse relazionale, data mart multidimensionale.

# Data Mining

Estrazione automatica di informazioni nascoste da basi di dati di grandi dimensioni (es. DW).

![image.png](attachment:575087f7-2db2-4de1-860a-c84e6ce0c75c:52aa3ce6-2dfa-4807-a821-aa7d5b90fa56.png)

Funzioni riconducibili all’ETL:

![image.png](attachment:b66be83f-601e-4cfd-9548-f9e49e251b5f:ea8ade5a-a7a9-4256-87a6-3c72eb85bb62.png)

Funzioni caratteristiche del Data Mining:

![image.png](attachment:8a7a8a80-3d98-457e-a874-9e1a459060f4:f6048be6-6816-4b6d-8605-544cb8686d63.png)

Apprendimento:

- Supervisionato → a ciascun record considerato è associata la variabile target.
- Non supervisionato → le tecniche cercano di riconoscere pattern e regolarità.

Classificazione:

- Generalizzazione → riduce la mole di dati analizzati tramite roll-up ed eliminando attributi a variabilità troppo elevata.
- Caratterizzazione → studio delle tendenze dei dati (min, max, media, varianza, …). Buona ispezione introduttiva all’analisi dei dati.

## Tecniche di Data Mining

Classificazione:

- Descrittive → classificano i dati storici.
- Predittive → dai dati storici fanno ipotesi per supportare decisioni.

***

- Regole associative → regole della forma $A\Rightarrow B$ che misurano quante volte, dato l’evento $A$, avviene anche $B$.
  - Confidenza: $P(B|A)$
  - Supporto: $P(A,B)$
- Classificazione → smista gli elementi in classi predefinite.
  - Training set → insieme degli elementi annotati usati per costruire il modello.
  - Test set → insieme degli elementi usati per testare i risultati della classificazione.
- Clustering → raggruppa gli elementi in maniera tale da massimizzare la somiglianza fra elementi dello stesso cluster e minimizzare la somiglianza fra elementi di cluster diversi.
  - Esclusivo → ogni elemento appartiene ad un solo cluster.
  - Sovrapposto → un elemento può appartenere a più cluster.

# Process Mining

Composto da:

- Dati di monitoraggio, relativi all’esecuzione delle attività che compongono il processo.
  - Log di eventi → composto da Case ID, attività, timestamp, etc.
- Modello di processo, che prescrive il corretto ordine di esecuzione delle attività.

## Tecniche di Process Mining

- Process Discovery → deduzione del modello di processo dal log degli eventi, senza necessariamente disporre di informazioni a priori.
- Conformance Checking → misura la conformità (”fitness”) tra il log degli eventi ed il modello di processo, riconoscendo:
  - Deviazioni degli eventi di log → il modello non potrebbe produrle.
  - Deviazione del modello → attività non conformi.
- Enhancement → miglioramento/estensione del modello di processo a partire dal log eventi.
