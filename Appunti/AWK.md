# AWK

## **Introduzione ad AWK**

AWK è un linguaggio di programmazione interpretato progettato per l'elaborazione e l'analisi di flussi di dati testuali, specialmente quando questi sono rappresentati in forma tabulare o come sequenze di record. Si distingue per la sua capacità di scansione di pattern e per l'azione di processing che lo rende ideale per manipolare file di testo strutturato, facilitando compiti come l'estrazione di colonne specifiche, la somma di numeri, o il filtraggio basato su criteri complessi.

AWK legge e interpreta ogni linea di un file come un "record" e ogni parola come un "campo", rendendo la manipolazione di dati basati su colonne semplice e intuitiva. La sua sintassi si fonda su modelli di 'pattern-action', dove specifici pattern nel testo scatenano l'esecuzione di azioni correlate. Grazie alle sue variabili incorporate, come FS (Field Separator) e NR (Number of Records), AWK fornisce una potente suite di strumenti per il trattamento e l'analisi dei dati direttamente dalla command line.

### **Storia e Contesto:**
AWK prende il nome dai suoi creatori—Aho, Weinberger e Kernighan—e rappresenta una pietra miliare nella storia degli strumenti di scripting UNIX, sviluppato per la prima volta nei laboratori Bell nel 1977. La sua progettazione è stata guidata dalla necessità di elaborare facilmente dati testuali e generare report. Caratterizzato da una sintassi espressiva e una potente capacità di pattern matching, AWK si è rapidamente affermato come strumento essenziale per la manipolazione dei dati nei sistemi UNIX-like. L'adozione di AWK è stata tanto vasta che ha influenzato la creazione di altri linguaggi di scripting e tool di elaborazione testuale, consolidandosi come uno standard de facto per il trattamento di flussi di dati e testi strutturati, tanto che la conoscenza di AWK è considerata ancora oggi una competenza fondamentale per programmatori e amministratori di sistema.

---

## **Concetti Chiave:**

### **Pattern Scanning e Processing:**
Il cuore di AWK è il suo meccanismo di pattern scanning e processing. Il linguaggio esegue la lettura dei dati di input riga per riga—ognuna definita come un "record"—e scompone ogni record nei suoi elementi costitutivi, chiamati "field". I pattern, che possono essere espressioni regolari o condizioni specifiche, sono analizzati in questo flusso di record. Quando un record corrisponde a un pattern specificato dall'utente, AWK esegue un blocco di azioni, come la modifica dei dati o la produzione di output.

### **Record e Field:**
In AWK, un "record" rappresenta di norma una singola linea di testo, mentre un "field" è un segmento di quella linea, solitamente delimitato da un separatore di campo. Di default, il separatore di campo (FS) è uno spazio bianco, che può essere un singolo spazio o una tabulazione, permettendo di trattare in maniera naturale i formati di file come CSV o file di log.

### **Variabili Built-in:**
AWK offre una serie di variabili built-in che facilitano l'elaborazione dei dati. Il "Field Separator" (FS) definisce il carattere di delimitazione dei field all'interno di un record. L'"Output Field Separator" (OFS) è utilizzato da AWK per determinare come separare i field nell'output. La variabile "Number of Records" (NR) tiene traccia del numero di record elaborati fino a quel momento. Queste variabili possono essere personalizzate per adattarsi a vari formati di dati e requisiti specifici, offrendo una flessibilità notevole nell'elaborazione dei dati testuali.

### **Sintassi di Base di AWK:**

La sintassi di base di AWK è elegante nella sua semplicità, permettendo agli utenti di specificare "pattern" e "azioni" da eseguire quando quel pattern viene riscontrato in un flusso di dati. Ecco una panoramica dettagliata:
```bash
awk 'pattern { action }' file
```

1. **Invocazione di AWK**: Il comando `awk` è seguito da un insieme di istruzioni racchiuso tra apici singoli. Questo consente di includere pattern e azioni che AWK eseguirà sui dati forniti.

2. **Pattern**: Il pattern è una condizione espressa spesso come un'espressione regolare racchiusa tra slash (`/pattern/`). AWK processa ogni linea del file di input e applica il pattern per determinare se la linea corrente deve essere processata. Il pattern può anche essere un'espressione condizionale (come `NR==1` o `$3 > 100`), che seleziona record basandosi sul loro contenuto.

3. **Azione**: Le azioni sono blocchi di codice racchiusi tra parentesi graffe (`{ action }`). Questi blocchi possono contenere una o più istruzioni che definiscono cosa AWK dovrebbe fare con i record che corrispondono al pattern. Le azioni possono variare dalla semplice stampa di dati (`{ print $0 }`) alla loro trasformazione o aggregazione (`{ sum+=$1 }`).

4. **File**: Il nome del file di input viene fornito alla fine della linea di comando. AWK leggerà questo file linea per linea, applicando il pattern e eseguendo le azioni specificate su ciascun record.

#### Esempi di Sintassi di Base:

- **Stampare tutto il file**:
  ```bash
  awk '{ print }' file
  ```
  Questo comando stampa ogni linea del file perché non è specificato alcun pattern, quindi l'azione `print` viene applicata a tutti i record.

- **Ricerca di un Pattern**:
  ```bash
  awk '/404/ { print $0 }' access.log
  ```
  Qui, `awk` cerca il pattern "404" in un file di log e stampa le linee che contengono questo codice di errore.

- **Modifica del Separatore di Campo**:
  ```bash
  awk 'BEGIN { FS=":"; OFS=" - " } $1=="root" { print $1, $6 }' /etc/passwd
  ```
  In questo esempio, il separatore di campo viene impostato su ":", adatto per file come `/etc/passwd`. Il comando stampa il primo e sesto campo di ogni record dove il primo campo è "root", separandoli con " - ".

#### Componenti Avanzati:

- **Variabili Built-in**: AWK offre variabili built-in come `FS`, `OFS`, `NR` e `NF` (Number of Fields), che possono essere utilizzate per costruire pattern e azioni dinamiche.

- **Funzioni**: AWK include diverse funzioni per l'elaborazione di stringhe, numeri e timestamp, come `split()`, `substr()`, `sin()`, `cos()`, `strftime()`, ecc.

- **Controllo di Flusso**: AWK supporta strutture di controllo di flusso come `if-else`, `while`, `do-while`, e `for`, permettendo script complessi e logica condizionale.

- **Variabili Utente e Array**: Gli utenti possono definire le proprie variabili e array per gestire i dati in modo più complesso e mantenere lo stato tra i record.

- **Programmazione Modulare**: Con la parola chiave `function`, gli utenti possono definire funzioni personalizzate, migliorando la modularità e la riusabilità del codice.

La sintassi di AWK si espande ben oltre questi esempi, offrendo un potente set di strumenti per l'elaborazione di dati testuali. Per approfondire ulteriormente, potremmo esaminare specifici esempi di script AWK o discutere di tecniche di programmazione avanzate all'interno di questo linguaggio.

---

## **Esempi Pratici Iniziali con AWK:**

### **Stampare Colonne Specifiche:**

In AWK, i dati di un file sono suddivisi in record e campi. Un record corrisponde di default a una linea del file, e i campi sono parti di quella linea delimitate da un separatore, di default lo spazio. Per accedere a un campo specifico, AWK utilizza la notazione `$n`, dove `n` è l'indice del campo desiderato.

**Esempio Dettagliato**:
Dato un file di nome `utenti.txt` con contenuti tabulati come segue:
```
alice 23 developer
bob 35 manager
carol 28 designer
```
Per stampare solamente la prima colonna, ovvero i nomi, il comando AWK sarà:
```bash
awk '{ print $1 }' utenti.txt
```
In questo esempio:

- `{ print $1 }` è il blocco di azioni che dice ad AWK di stampare il primo campo di ogni record.
- `utenti.txt` è il file di input su cui AWK opera.

Output atteso:
```
alice
bob
carol
```

**Espansione dell'Esempio**:
Se si desidera stampare sia i nomi degli utenti (prima colonna) che le loro professioni (terza colonna), si modifica il blocco di azioni per includere entrambi i campi:
```bash
awk '{ print $1, $3 }' utenti.txt
```
Output atteso:
```
alice developer
bob manager
carol designer
```

### **Somma di una Colonna:**

AWK è eccellente per eseguire calcoli sui dati di un file. Per sommare i valori di una colonna specifica, utilizzi una variabile (ad esempio, `sum`) per tenere traccia del totale e quindi usi un blocco `END` per stampare il risultato finale dopo aver processato tutte le righe.

**Spiegazione Dettagliata**:
Ecco come funziona il comando:
```bash
awk '{ sum += $2 } END { print sum }' file.txt
```

- `{ sum += $2 }` dice ad AWK di aggiungere il valore del secondo campo di ogni record alla variabile `sum`. All'inizio, `sum` non è definita, ma AWK la inizializza automaticamente a 0.
- `END { print sum }` è un blocco di azioni speciale che viene eseguito dopo che tutti i record sono stati processati. Stampa il valore accumulato in `sum`.

**Esempio Pratico con `utenti.txt`**:
Supponendo di avere lo stesso file `utenti.txt`:
```
alice 23 developer
bob 35 manager
carol 28 designer
```
Per calcolare la somma delle età (seconda colonna), il comando AWK sarà:
```bash
awk '{ sum += $2 } END { print sum }' utenti.txt
```
In questo esempio, ogni volta che AWK legge una riga, aggiunge il valore del secondo campo (l'età) alla variabile `sum`. Una volta che ha finito di leggere il file, stampa il totale.

Output atteso:
```
86
```

**Ulteriori Dettagli**:
Se si vuole, ad esempio, anche calcolare la media di età, si può estendere il blocco `END`:
```bash
awk '{ sum += $2; count++ } END { print "Totale età:", sum; print "Media età:", sum/count }' utenti.txt
```

In questo script AWK esteso:
- `count++` incrementa un contatore ogni volta che un record è letto, per tenere traccia del numero totale di utenti.
- `print "Totale età:", sum` stampa la somma totale delle età.
- `print "Media età:", sum/count` calcola e stampa la media delle età.

Questo rende AWK uno strumento molto potente per l'analisi e la relazione di dati direttamente dalla riga di comando.

### **Filtraggio e Stampa Condizionale con AWK:**

AWK eccelle sia nel filtraggio di dati basato su pattern specifici sia nella realizzazione di azioni condizionali. Queste due funzionalità, pur essendo tecnicamente diverse, condividono un approccio simile nell'identificazione e nell'elaborazione di record specifici all'interno di un flusso di dati.

 **Filtraggio per Pattern:**
Il filtraggio in AWK si basa sull'uso di espressioni regolari o stringhe di testo per selezionare righe di interesse.
**Esempio**: 
Per visualizzare le righe che contengono "developer" in `utenti.txt`:
```bash
awk '/developer/ { print $0 }' utenti.txt
```
Questo comando stampa l'intera riga (`$0`) per ogni record che corrisponde al pattern `/developer/`.

**Stampa Condizionale:**
La stampa condizionale utilizza espressioni logiche e condizionali per eseguire azioni su righe che soddisfano determinate condizioni.
**Esempio**:
Per stampare i nomi (`$1`) degli utenti che sono "developer":
```bash
awk '$3 == "developer" { print $1 }' utenti.txt
```
In questo caso, AWK controlla se il terzo campo (`$3`) è "developer" e, se sì, stampa il primo campo.

 **Combinazione di Condizioni e Filtri:**
AWK permette di combinare condizioni logiche e pattern matching per creare filtri complessi.
**Esempio**:
Per trovare gli utenti "developer" con età superiore ai 25 anni:
```bash
awk '$2 > 25 && /developer/ { print $0 }' utenti.txt
```
Questo script cerca righe che soddisfano entrambe le condizioni: età (`$2`) maggiore di 25 e la parola "developer" nel record.

### **Ambiente di Esecuzione AWK:**

AWK può essere utilizzato sia in modalità interattiva da terminale sia come parte di script più complessi. Ecco come puoi sfruttare entrambi questi approcci:

 **Uso da Terminale:**
L'uso da terminale è ideale per operazioni rapide e test di script. AWK può essere eseguito direttamente dalla linea di comando, permettendo una manipolazione immediata dei dati.
**Esempio di Comando Terminale**:
Supponiamo di voler trovare tutti gli "developer" nel nostro file `utenti.txt`. Il comando diretto da terminale sarebbe:
```bash
awk '/developer/ { print $0 }' utenti.txt
```
Questo comando esegue AWK direttamente da terminale, filtrando e stampando le righe che contengono la parola "developer".

**Script AWK:**
Per operazioni più complesse, puoi scrivere script AWK. Gli script consentono di includere più linee di codice AWK, rendendoli ideali per attività di elaborazione dati ripetitive e complesse.
**Creazione di uno Script AWK**:
1. **Scrivi lo Script**: Crea un file con estensione `.awk` (es. `script.awk`) e scrivi il tuo codice AWK al suo interno.
   **Esempio di script.awk**:
   ```awk
   #!/usr/bin/awk -f
   /developer/ { print $1 " è un developer con età " $2 }
   ```
2. **Rendi lo Script Eseguibile**: Usa il comando `chmod` per rendere lo script eseguibile.
   ```bash
   chmod +x script.awk
   ```
3. **Esegui lo Script**: Ora puoi eseguire lo script direttamente.
   ```bash
   ./script.awk utenti.txt
   ```
**Nota sulla Shebang (`#!/usr/bin/awk -f`)**:
- La shebang all'inizio dello script (`#!/usr/bin/awk -f`) indica al sistema di utilizzare AWK come interprete per lo script.
- `#!/usr/bin/awk -f` è il percorso comune all'interprete AWK su sistemi UNIX-like. La flag `-f` indica ad AWK di prendere il programma da un file.
**Esempio di Uso dello Script**:
Se esegui `./script.awk utenti.txt` con il file `utenti.txt` sopra menzionato, otterrai:
```
alice è un developer con età 23
```

Questa sezione fornisce una panoramica chiara sull'uso di AWK sia direttamente da terminale per test rapidi e manipolazioni di dati, sia in uno script per compiti più complessi e strutturati. Questo dualismo rende AWK uno strumento estremamente flessibile e potente in una varietà di scenari di elaborazione dati.

## **Casi d'Uso Comuni:**
### **Analisi di Log:**
Esempi su come awk può essere usato per analizzare file di log.
**Elaborazione di File CSV o TSV:** Spiegazione su come manipolare file di dati tabulare.

 Questa sezione può trarre beneficio da esempi specifici, che dimostrino l'applicazione di AWK in scenari reali come l'analisi di log o la manipolazione di file CSV/TSV.

## **Struttura della Guida**

La guida dovrebbe essere strutturata in modo progressivo, iniziando da esempi semplici e incrementando gradualmente la complessità. Ogni concetto o comando deve essere accompagnato da esempi concreti. Dopo aver coperto i fondamenti, puoi introdurre funzionalità più avanzate come le funzioni incorporate, l'uso di variabili, array e le operazioni di controllo del flusso (if-else, cicli).

Inoltre, è utile includere suggerimenti su come debuggare gli script awk e come integrarli in script più ampi, combinandoli con altri strumenti della shell come sed, grep, e cut.