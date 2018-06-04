**INDICE**





Introduzione
Modello concettuale 
Requisiti specifici  
Architettura 
- Diagramma dei package 
- Diagramma dei componenti
System Design  
- Diagramma delle classi 
- Diagramma di sequenza
- Design pattern 
- Segnalazioni di PMD
Riepilogo del test    
- Tabella riassuntiva di coveralls 
Manuale utente
Processo di sviluppo e organizzazione del lavoro 
Analisi retrospettiva 




![testo alt](/US1.jpg)























**INTRODUZIONE**




Con la realizzazione di Sna4slack  si è cercato di visualizzare ed analizzare i dati raccolti da conversazioni di canali pubblici di Slack.
Cosa è Slack?
Slack è uno strumento utile per la comunicazione tra persone e per la condivisione di file.
All’interno di Slack è possibile creare conversazioni dette canali. I canali possono essere aperti o privati in base alle esigenze degli utenti. 
I canali privati  non sono visibili a tutti gli utenti ma, solo ai membri che ne fanno parte, mentre i canali aperti sono quei canali accessibili a tutti. Da questi ultimi è possibile estrarre  informazioni(menzioni,lista dei membri dei canali,lista utenti, lista canali) e raccoglierle all’interno di un file di tipo json. 
Sna4slack ha la funzione di processare i file json e di estrapolare da questi le informazioni elencate precedentemente.
























**MODELLO CONCETTUALE**






































**REQUISITI SPECIFICI  **


In qualità di utente voglio visualizzare la lista dei Member:

Criteri di accettazione
- Verificare che sia possibile fare la richiesta da linea di comando
- Verificare che l'output sia visualizzato su standard output
- Verificare che sia possibile specificare il workspace
- Verificare che ci sia un file esportato associato al workspace
- Verificare che i Member siano visualizzati uno per riga
- Verificare che i Member del workspace siano tutti presenti
- Verificare che non siano visualizzati Member estranei al workspace.
 
 
In qualità di utente voglio visualizzare la lista dei Channel:

Criteri di accettazione
- Verificare che sia possibile fare la richiesta da linea di comando
- Verificare che l'output sia visualizzato su standard output
- Verificare che sia possibile specificare il workspace
- Verificare che ci sia un file esportato associato al workspace
- Verificare che i Channel siano visualizzati uno per riga
- Verificare che i Channel del workspace siano tutti presenti
- Verificare che non siano visualizzati Channel estranei al workspace.
 
 
 
 
 
 
 
 
 
 
 
In qualità di utente voglio visualizzare la lista dei Member raggruppati per Channel:

Criteri di accettazione
- Verificare che sia possibile fare la richiesta da linea di comando
- Verificare che l'output sia visualizzato su standard output
- Verificare che sia possibile specificare il workspace
- Verificare che ci sia un file esportato associato al workspace
- Verificare che i Member e Channel siano visualizzati uno per riga, con i "Member"    visualizzati subito dopo il Channel a cui appartengono
- Verificare che sia possibile distinguere quale nome è un "Member" e quale è un Channel
- Verificare che i Channel siano tutti presenti
- Verificare che non siano visualizzati Channel estranei al workspace
- Verificare che i Member di un Channel siano tutti presenti
- Verificare che non siano visualizzati Member estranei al Channel
 
 
In qualità di utente voglio visualizzare la lista dei Member di un Channel:

Criteri di accettazione
- Verificare che sia possibile fare la richiesta da linea di comando
- Verificare che l'output sia visualizzato su standard output
- Verificare che sia possibile specificare il workspace Verificare che ci sia un file esportato                associato al workspace
- Verificare che sia possibile specificare il Channel
- Verificare che i Member siano visualizzati uno per riga dopo il Channel specificato
- Verificare che i Member del Channel specificato siano tutti presenti
- Verificare che non siano visualizzati Member estranei al Channel specificato
 
 
 
In qualità di utente voglio poter avere informazioni di help:

Criteri di accettazione
- Verificare che l'help possa essere richiesto digitando solo il nome del programma: sna4slack
- Verificare che l'help sia suggerito se un comando digitato non è valido
-  Verificare l'help sia mostrato su standard output
-  Verificare che siano presenti i comandi per tutte le funzionalità
 
 
 
 
In qualità di utente voglio visualizzare la lista dei @mention:

Criteri di accettazione:
- Verificare che per ogni @mention sia visualizzata una riga con la coppia (From, To) dove From è lo User che scrive il messaggio con il @mention e To è lo User menzionato.
- Verificare che le coppie (From, To) non siano ripetute
- Verificare che le coppie (From, To) corrispondenti a un @mention siano tutte presenti
- Verificare che siano visualizzate solo coppie (From, To) corrispondenti a un @mention
- Verificare che sia possibile specificare il Channel e, nel caso sia specificato, la lista sia ristretta ai soli @mention del Channel
 
 
In qualità di utente voglio visualizzare la lista dei @mention che partono da uno User:

Criteri di accettazione:
- Verificare che sia possibile specificare lo User da cui partono i @mention
- Verificare che per ogni @mention sia visualizzata una riga con la coppia (From, To) dove From è lo User specificato nel comando e To è lo User menzionato.
- Verificare che le coppie (From, To) non siano ripetuti
- Verificare che le coppie (From, To) corrispondenti a un @mention siano tutte presenti
- Verificare che siano visualizzate solo coppie (From, To) corrispondenti a un @mention
- Verificare che sia possibile specificare il Channel e, nel caso sia specificato, la lista sia ristretta ai soli @mention del Channel

 
In qualità di utente voglio visualizzare la lista dei @mention che arrivano a uno User:

Criteri di accettazione:
- Verificare che sia possibile specificare lo User a cui arrivano i @mention
- Verificare che per ogni @mention sia visualizzata una riga con la coppia (From, To) dove è lo User che scrive il messaggio con il @mention e To è lo User menzionato e specificato nel comando.
- Verificare che le coppie (From, To) non siano ripetute
- Verificare che le coppie (From, To) corrispondenti a un @mention siano tutte presenti
- Verificare che siano visualizzate solo coppie (From, To) corrispondenti a un @mention
- Verificare che sia possibile specificare il Channel e, nel caso sia specificato, la lista sia ristretta ai soli @mention del Channel

In qualità di utente voglio visualizzare la lista pesata dei @mention:
 
Criteri di accettazione:
- Verificare che per ogni @mention sia visualizzata una riga con la tripla**(From, To, Weight)** dove From è lo User che scrive il messaggio con il @mention, To è lo User menzionato, e Weight. è il peso associato che riporta il numero di mention da From a To
- Verificare che le triple (From, To, Weight) non siano ripetute
- Verificare che le triple (From, To, Weight) corrispondenti a un @mention siano tutte presenti
- Verificare che siano visualizzate solo triple (From, To, Weight)* corrispondenti a un @mention
- Verificare che sia possibile specificare il Channel e, nel caso sia specificato, la lista sia ristretta ai soli @mention del Channel


In qualità di utente voglio visualizzare la lista pesata dei @mention che partono da uno User:

Criteri di accettazione:
- Verificare che sia possibile specificare lo User da cui partono i @mention
- Verificare che per ogni @mention sia visualizzata una riga con la tripla (From, To, Weight) dove From è lo User specificato nel comando e To è lo User menzionato, e Weight il numero di mention.
- Verificare che le triple (From, To, Weight) non siano ripetute
- Verificare che le triple (From, To, Weight) corrispondenti a un @mention siano tutte presenti
- Verificare che siano visualizzate solo triple (From, To, Weight) corrispondenti a un @mention
- Verificare che sia possibile specificare il Channel e, nel caso sia specificato, la lista sia ristretta ai soli @mention del Channel


 
 
 
 
 
 
 
 
 
 
 
In qualità di utente voglio visualizzare la lista pesata dei @mention che arrivano a uno User:

Criteri di accettazione:
- Verificare che sia possibile specificare lo User a cui arrivano i @mention
- Verificare che per ogni @mention sia visualizzata una riga con a tripla (From, To, Weight) dove From è lo User specificato nel comando e To è lo User menzionato, e Weight il numero di mention.
- Verificare che le triple (From, To, Weight) non siano ripetute
- Verificare che le ctriple (From, To, Weight) corrispondenti a un @mention siano tutte presenti
- Verificare che siano visualizzate solo triple (From, To, Weight) corrispondenti a un @mention
- Verificare che sia possibile specificare il Channel e, nel caso sia specificato, la lista sia ristretta ai soli @mention del Channel






 





 

 

 


**ARCHITETTURA**

**STILE ARCHITETTURALE ADOTTATO**
All’interno del progetto è stata adottata un’architettura di tipo pipe and filter. Questo tipo di architettura suddivide l’elaborazione complessiva  in una catena di processi detti “filter”in cui l’output di ciascun filter funge da input per il successivo. I “pipe” collegano i filter. L’insieme dei pipe e dei filter creano una pipeline virtuale. 
 
**DIAGRAMMA DEI PACKAGE**
 

 
 
**DIAGRAMMA DEI COMPONENTI**
 


**SYSTEM DESIGN**


**DIAGRAMMA DELLE CLASSI**


User story 1:
In qualità di utente voglio visualizzare la lista dei Member






User story 2:
In qualità di utente voglio visualizzare la lista dei Channel










User story 3:
In qualità di utente voglio visualizzare la lista dei Member raggruppati per Channel













User story 4:
In qualità di utente voglio visualizzare la lista dei Member di un Channel





User story 5:
In qualità di utente voglio poter avere informazioni di help















User story 6,7,8,9,10,11:
6-In qualità di utente voglio visualizzare la lista dei @mention
7-In qualità di utente voglio visualizzare la lista dei @mention che      partono da uno User  
8-In qualità di utente voglio visualizzare la lista dei @mention che arrivano a uno User
9-In qualità di utente voglio visualizzare la lista pesata dei @mention
10-In qualità di utente voglio visualizzare la lista pesata dei @mention che partono da uno User
11-In qualità di utente voglio visualizzare la lista pesata dei @mention che arrivano a uno User














**DIAGRAMMA DI SEQUENZA**









































**DESIGN PATTERN**

All’ interno del codice sono stati applicati due tipi di design pattern:
-design pattern Command
-Dependency injection

Il Command pattern tratta le richieste di operazioni come oggetti eliminando la dipendenza tra l’oggetto che richiede l’esecuzione e l’oggetto che effettua l’azione. Questo tipo di pattern è stato implementato in Sna4slack per ottimizzarne i comandi.  

Il dependency injection è statao utilizzato per evitare la dichiarazione di DataService(elemento che si occupa della gestione dati) come classe singleton.







**SEGNALAZIONI IN PMD**

Le segnalazioni in pmd sono complessivamente 9 e tutte giustificabili:
le segnalazioni numero 1,2,3 e 4 non sono state chiuse in quanto avrebbero richiesto una profonda ristrutturazione del codice rendendolo più complesso;
la segnalazione numero 5 necessita di una modifica del codice che il team non è riuscito ad apportare per questioni di tempo;
le segnalazioni numero 6,7,8 e 9 sono dovute all’impossibilità di pmd di associare alle variabili gli stessi nomi di quelli dei campi del file json come invece impone la libreria json.
















**RIEPILOGO DEL TEST**





   






































**MANUALE UTENTE**

Per poter interagire con Sna4slack bisogna innanzitutto avviare il programma. 
Una volta avviato dovremo inserire il percorso file del file .zip, dopo di che  si dovranno inserire dei comandi.
I comandi sono:

- canali                                                 
- utenti                                                 
- membri [GRUPPO]                                                                         
- lista  [NOME WORKSPACE]                                 
- menzioni [CANALE] | [from|to NOME UTENTE] [-p]                  
- esci                                                  
- sna4slack 


presentazione iniziale dell’ applicazione




Comando canali
mostra tutti i canali presenti nel workspace





Comando utenti:
mostra tutti gli utenti presenti nel workspace







Comando membri:
mostra tutti i membri presenti in un determinato canale del workspace






Comando lista:
mostra tutti i membri divisi per canale presente nello workspace



Comando menzioni:
mostra le menzioni, o per canale, o per utente o tutte se lasciato in bianco, con l'opzione "-p" mostra il peso    








Comando esci:
permette di uscire da sna4slack













Comando sna4slack:
mostra l’help di sna4slack, elencondo e illustrando brevemente i comandi 








**PROCESSO DI SVILUPPO E ORGANIZZAZIONE DEL LAVORO**


Il metodo di lavoro utilizzato per la realizzazione di  Sna4slack includeva: 
1) interazione tramite applicazioni di messaggistica e VoIP al fine di organizzare il lavoro ed ottimizzarne i tempi
2) assegnazione del lavoro a ciascun membro del gruppo: ad alcuni dei 3 membri veniva affidato il compito di programmare mentre ai restanti quello di effettuare una review istantanea dell'elaborato svolto
3) discussione dell’elaborato (review) al completamento di ogni user story. In caso di feedback positivo da parte di tutti i membri, l’elaborato veniva approvato. 








**ANALISI RETROSPETTIVA**



Durante le varie review effettuate dal gruppo è stato possibile valutare l’efficacia delle soluzioni applicate durante la realizzazione del software. Sicuramente molto utile si è rivelato l’uso del design pattern command. Questo infatti ha permesso di semplificare l'implementazione di nuovi comandi all’interno dell’applicazione. Al contrario, l’architettura utilizzata per la realizzazione della funzione DataService si è dimostrata essere abbastanza complessa. Una semplificazione della stessa non è stata effettuata per questioni di tempo.  
Infine, il metodo di lavoro adattato all’interno del gruppo e il continuo scambio di informazioni  si sono dimostrati molto efficaci per il raggiungimento del risultato finale. 













