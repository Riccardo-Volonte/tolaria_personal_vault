---
type: Note
---
# lab_ex1

# Esercizio 1

Impieghiamo **role prompting** per indirizzare sia il linguaggio della risposta, che la prospettiva da cui analizzare il tema.

> Rispondimi come se fossi un professore universitario di diritto costituzionale.

Per confermare ulteriormente il linguaggio divulgativo, applichiamo anche una **definizione del pubblico** (facoltativo: il linguaggio è già indicato dal role prompting).

> Stai spiegando agli studenti del primo anno di giurisprudenza.

Introduciamo esplicitamente il tema, come fa il zero-shot prompt fornito dalla traccia.

> Spiega il referendum abrogativo in Italia e confrontalo con altri strumenti di democrazia diretta.

Utilizziamo **instruction sorting** per imporre una struttura alla risposta e quindi indicare esplicitamente gli aspetti da analizzare, come richiesto dalla traccia. Contestualmente, questa tecnica permette di pilotare meglio il modello ed ottenere un output più prevedibile ed allineato alla nostra aspettativa.

> Definizione: spiega in generale di cosa si tratta e a cosa serve.\
> Svolgimento: spiega come funziona concretamente un referendum abrogativo, dalla sua concezione alla sua risoluzione.\
> Legislazione: spiega quali fonti del diritto regolano il referendum abrogativo.\
> Confronto: confronta il referendum abrogativo con altri strumenti di democrazia diretta.

# Esercizio 2

Apriamo con **RAV prompting**: alleghiamo gli appunti dello studente e li indichiamo come fonte per la risposta (questa tecnica è azzardata in quanto assume la disponibilità di appunti, e non tiene in considerazione l'eventuale scorrettezza od incompletezza degli stessi; comunque, non sarebbe scorretto allegarli per rimarcare il livello di dettaglio e tecnicità richiesti, comunque già indicati dalla definizione del pubblico più avanti).

> [Allego appunti relativi all'argomento]\
> Rispondi basandoti sugli appunti allegati.

Introduciamo direttamente e nettamente l'argomento.

> Spiega il ruolo del Presidente della Repubblica nel sistema costituzionale italiano.

Con la **definizione del pubblico**, lasciamo dedurre al modello la necessità di un linguaggio chiaro e divulgativo, ma comunque preciso.

> Spiega come se ti stessi rivolgendo ad uno studente del corso di Diritto Costituzionale.

Si può introdurre **instruction prompting** per pilotare meglio il risultato (poiché entrambe le soluzioni includono instruction prompting, è ragionevole assumere che sia richiesto in sede d'esame; comunque, ricorda che a volte può essere saggio omettere la struttura per convenienza temporale).

Sarebbe meglio elaborare meglio il contenuto di ciascun paragrafo, anche se effettivamente molti di questi sono abbastanza atomici per cui è superfluo farlo. Effettivamente, sarebbe meglio indicare paragrafi più generali, e poi, nella loro descrizione, enumerare alcuni esempi di informazioni importanti (per esempio: "1) ciclo di vita: da chi è eletto, quanto dura il suo mandato" o più generalmente "1) introduzione: ruolo, elezione, durata del mandato").

> Spiega il ruolo del presidente della repubblica nel sistema costituzionale italiano seguento la seguente struttura:\
> 1) da chi è eletto\
> 2)quanto dura il suo mandato\
> 3)qual è il suo ruolo\
> 4)quali fonti disciplinano il suo ruolo.

Si introducono **limiti** per indirizzare meglio la forma della risposta (sarebbe consono includere anche una lunghezza minima, per garantire completezza e dettaglio).

> Produci una risposta di massimo 1500 parole.

Infine si introducono **limiti negativi** per prevenire condotte scorrette.

> Non commentare l'operato dei singoli presidenti. Non fare commenti soggettivi e personali.

# Esercizio 3

Definizione del **linguaggio**: imporlo esplicitamente piuttosto che tramite role prompting o definizione del pubblico è più verboso, ma anche più preciso. Considera inoltre che, al contrario del role prompting, non è indicata la prospettiva da cui è necessario analizzare il caso (giuridica, politica, sociologica, ...) e potrebbe pertanto introdurre ambiguità nel prompt, deteriorando l'output (questo difetto è, opinabilmente, corretto dall'instruction prompting più avanti).

> Rispondi con un linguaggio tecnico-giuridico specializzato e tono prudente.

Si introduce l'argomento, analogamente alla traccia.

> Una pubblica amministrazione introduce un sistema automatizzato per selezionare i\
> candidati a un concorso pubblico. Secondo alcuni partecipanti, questo modello non è abbastanza trasparente nei loro confronti.

Si impone la struttura della risposta con **instruction prompting**.

In particolare, nella analisi di casi giuridici, è importante garantire l'imparzialità del modello rispetto alla questione: una struttura argomentativa classica spinge il modello a schierarsi con una delle due parti, introducendo quindi bias e rendendo la conclusione viziata.

> Segui la seguente struttura:\
> Argomentazioni a favore: spiega in quale modo i partecipanti sentono che il sistema non garantice sufficiente trasparenza nei loro confronti\
> Obiezioni: argomenta come mai il sistema automatizzato andrebbe mantenuto\
> Fonti: cita fonti rilevanti in merito alla questione\
> Precedenti: cita dei precedenti simili a questo caso, solo se esistenti.\
> Conclusione: paragona brevemente le ragioni di entrambe le parti e proponi una soluzione.

Con **limiti negativi** si censurano eventuali condotte scorrette da parte del modello: in generale, nell'analisi di casi giuridici, questi limiti dovrebbero garantire soprattutto l'imparzialità e l'onesta intellettuale della soluzione proposta.

> Rispondi in modo imparziale, senza influenze politiche.

Con **limiti** si indica la forma favorita per l'output (un range di parole sarebbe più appropriato).

> La risposta deve contenere minimo 3000 parole.
