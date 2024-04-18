**Classificazione**: associare i dati di input a categorie
**Regressione:** associare i dati di input a valori continui
**Clustering:** scoprire raggruppamenti nei dati di input (**NB:** esempio di apprendimento ==non supervisionato==)

- La rete impara ad associare un dato input ad uno specifico output
- L'output ==desiderato== (*ovvero la risposta corretta*) deve essere fornito esplicitamente alla rete durante l'apprendimento
- Tutti gli esempi per l'apprendimento devono essere ==etichettati== (in inglese: *labeled data*) con l'output desiderato (es. categoria oggetto)

**Algoritmi:**
- Percettrone
- Regola delta
- Error back-propagation

**Applicazione**: classificazione, regressione (*approssimazione di funzioni; predizione*)

**Relazione con metodi statistici**: modello lineare generalizzato (GLM), regressione, analisi discriminante

### La correzione dell'errore
- **Training set**: insieme di esempi (*patterns*) su cui addestrare la rete. Per ogni esempio possiamo definire:
	- **input(x)**: la configurazione dei valori di input (*in statistica*: variabili indipendenti, predittori)
	- **Output (y)**: valore/i che rappresentano la risposta della rete (*in statistica*: variabile dipendente)
	- **Target (t)**: la risposta desiderata/corretta da associare all'input
- **Addestramento**:
	- presentazione di un esempio (*valori di input*)
	- Calcolo output sulla base dei parametri attuali (*pesi*)
	- Confronto tra output e target per determinare lo *scostamento/errore*
	- modifica dei parametri (*ottimizzazione*) per diminuire lo scostamento
- **Testing:**
	- verifica delle prestazioni, inclusa la capacità di ==generalizzazione== su dati non utilizzati per l'addestramento (**test set**)
## Il percettrone
È il primo modello di rete neurale con pesi sinaptici modificabili da un algoritmo di apprendimento, sviluppato da Frank Rosenblatt nel 1958.
La rete ha **N** input che codificano l'esempio presentato con valori $x_i$ ed un singolo neurone di output che codifica la risposta in modo bipolare (*o binario*). L'output $y$ della rete è:
$y= \{ \begin{array}{rl} 1 se \sum^{N}_{i=1} w_i x_i - \theta \geq 0 \\ -1   altrimenti \end{array}$
![[Pasted image 20240322175755.png]]
dove $w_i$ è il peso della connessione dal neurone $x_i$ e $\theta$ è la soglia del neurone (*che definisce la posizione del gradino*). Possiamo sostituire la soglia con un input fisso $x_0 = 1$ e il corrispondente peso $w_0$, chiamato **bias**, e calcolarne il valore come per qualsiasi altro peso durante l'apprendimento:
![[Pasted image 20240322180017.png]]
### L'apprendimento nel percettrone
Per ogni esempio presentato, l'output $y$ viene confrontato con la risposta desiderata (*target*) $t$ che codifica la classe di appartenenza
- se $y=t$ (*output corretto*) si procede al prossimo esempio, senza fare alcuna modifica ai pesi
- se $y \not= t$  (*errore*), i pesi sinaptici vengono modificati con: $\Delta w_i = \eta t x_i$ dove $\eta$ è il learning rate (*tasso di apprendimento*).
Si noti che i pesi delle connessioni da cui è arrivato input aumentano se il target è $[+1]$ e diminuiscono se il target è $[-1]$. Nel caso di target binario ($[0/1)$) è sufficiente sostituire $t$ con $(t-y)$
**Teorema di convergenza del percettrone:**
Per qualunque problema *linearmente separabile* verrà trovata la soluzione in un numero finito di passi.
![[Pasted image 20240322180730.png]]
![[Pasted image 20240322180744.png]]
![[Pasted image 20240322180751.png]]
![[Pasted image 20240322180757.png]]
![[Pasted image 20240322180807.png]]
## Associatore (*lineare*) di configurazioni
Un associatore di configurazione è simile ad un percettrone ma i neuroni di output utilizzano una funzione di attivazione continua (come la **_sigmoide_**). L'output dei neuroni è quindi continuo (nel range *0-1*). Questo permette di quantificare l'errore (cf. errore si/no nel percettrone).
![[Pasted image 20240323110228.png]]
### La regola delta
- Applicabile quando le unità di output hanno una funzione di attivazione ==continua e differenziabile== (come la sigmoide)
- Permette di descrivere la prestazione con una funzione che misura l'errore della rete - *funzione di errore o funzione di costo* - che si basa sullo scarto quadratico medio tra risposta desiderata ed output effettivo: $E_W = 1/2 \sum_\mu\sum_i (t_i^\mu-y_i^\mu)^2$ 
- L'apprendimento consiste nel minimizzare la funzione di costo $E$, che dipende unicamente dal valore delle connessioni sinaptiche $W$. Quindi si modificano i pesi nella direzione opposta al gradiente della funzione stessa (*discesa del gradiente*): $\Delta w_{ij} = - (\delta E)/(\delta w_{ij})$
![[Pasted image 20240323111005.png]]
La forma finale della regola dipende dal tipo di funzione di attivazione (*perchè va calcolato il valore della derivata: $f'(net)$*). Nel caso di una funzione lineare otteniamo che il cambiamento dei pesi è dato semplicemente dalla differenza tra target e output moltiplicata per l'attività presinaptica: $\Delta w_{ij} = \eta (t_i - y_i)x_i$
Per la funzione sigmoide avremo: $\Delta w_{ij} = \eta(t_i - y_i)y_i(1-y_i)x_j$
### Apprendimento con la regola delta
- viene presentata alla rete una configurazione di input
- L'attivazione fluisce alle unità di output
- Viene calcolata l'attivazione delle unità di output
- La configurazione così ottenuta viene confrontata con la configurazione di output desiderata
- Viene calcolata la *discrepanza* tra le 2 configurazioni (*segnale di errore*)
- I pesi sulle connessioni vengono *modificati* (cf equazione della regola delta) *in modo da ridurre l'errore*
La procedura viene eseguita per tutti gli esempi che formano il training set (*epoca di apprendimento*) ed ulteriormente ripetuta (*eseguendo più epoche*) fino a quando l'errore arriva a 0 oppure la ==discesa== dell'errore si arresta.
**NB**: La regola delta è matematicamente equivalente alla *regola di* **Rescorla-Wagner** per il condizionamento classico.
![[Pasted image 20240323111957.png]]
## Reti multistrato
![[Pasted image 20240323112051.png]]
- I problemi caratterizzati da inseparabilità lineare (es. XOR) possono essere risolti da reti neurali multistrato, ovvero con uno o più strati intermedi di neuroni nascosti (in inglese: **hidden layers**) che utilizzano una funzione di attivazione non-lineare (_come la sigmoide_)
- La rete multistrato è un **approssimatore universale**: Una rete neurale con almeno uno strato nascosto composto da un numero appropriato di neuroni con funzione di attivazione non-lineare può, in linea di principio approssimare qualunque funzione X -> Y (input-output)
### Back-propagation
- L'algoritmo di apprendimento noto come **back-propagation** è una estensione della **regola delta** ([[Apprendimento supervisionato#La regola delta]]) che permette di addestrare reti multi-strato
- *Architettura*: qualsiasi numero di strati nascosti (*almeno uno*), qualsiasi connettività (*anche reti ricorrenti, utilizzando una variante dell'algoritmo*)
- Risolve il problema di come calcolare l'errore per le unità nascoste tramite la propagazione all'indietro dell'errore (**_error back-propagation_**) calcolato per le unità di output attraverso le stesse connessioni che servono per la propagazione dell'attivazione.
- La propagazione all'indietro dell'errore rende l'algoritmo implausibile dal punto di vista biologico.
![[Pasted image 20240323113131.png]]
# Apprendimento *batch* vs. *online*
- **Batch**: 
	- discesa del gradiente della funzione dell'*errore globale*, i pesi vengono cambiati in base al gradiente calcolato attraverso tutti i pattern
	- ![[Pasted image 20240323113817.png]]
- **Online o mini-batch**:
	- discesa ==stocastica== del gradiente. I pesi vengono cambiati in base al gradiente della funzione dell'*errore parziale*, calcolato per un singolo esempio (o un piccolo numero di esempi per *mini-batch*)
	- ![[Pasted image 20240323113950.png]]
![[Pasted image 20240323114009.png]]
![[Pasted image 20240323114034.png]]
#### Momentum
![[Pasted image 20240323114115.png]]
Il "**momento**" aggiunge all'aggiornamento del peso sinaptico una frazione del precedente cambiamento di valore. Quando il gradiente dell'errore ha la stessa direzione, il momento aumenta la grandezza del passo che viene fatto (*verso il minimo*). Quando il gradiente cambia direzione, il momento affievolisce il cambiamento.
## La generalizzazione
- È la capacità di utilizzare in modo appropriato la conoscenza sul dominio quando si incontrano nuovi esempi del problema
- Condizioni necessarie (*ma non sufficienti*) per ottenere una buona generalizzazione:
	- Le variabili di input contengono sufficienti informazioni relative al target, in modo che esista una funzione matematica che lega l'output corretto agli input con un determinato grado di accuratezza.
	- Gli esempi per l'addestramento sono in numero sufficientemente grande e sono un campione rappresentativo dell'insieme di casi a cui si vuole generalizzare (*popolazione*)
![[Screenshot 2024-04-10 alle 19.52.49.png]]
## Generalizzazione vs. overfitting
**Generalizzazione:** la produzione di una risposta appropriata a pattern di input non utilizzati per l'addestramento, ovvero un *test set ==indipendente==* dal *training set.*
**Overfitting:** si verifica quando continua a migliorare la prestazione *sui pattern di addestramento* ma *peggiora* la prestazione in termini di *generalizzazione*.
![[Screenshot 2024-04-11 alle 14.42.41.png]]
### Overfitting
**Perchè?**
- La relazione X-Y non è regolare (*ha tante eccezioni*)
- I dati contengono rumore
-> La rete *apprende* anche il *"rumore"* nei dati usati per addestramento.
![[Screenshot 2024-04-11 alle 14.46.03.png]]
**Come evitare overfitting** (e quindi migliorare la generalizzazione)?
- Utilizzare reti neurali non troppo potenti permette di apprendere le *regolarità statistiche* nei dati piuttosto che <<*memorizzare*>> i pattern di training. Si può ottenere questo *limitando il numero di unità nascoste* (Verificare anche che lo strato nascosto sia necessario!)
- *Early stopping*: utilizzare un set di pattern *(validation set)* solo per la verifica di overfitting durante l'apprendimento e fermarlo prima che l'errore sul validation set inizi ad aumentare.
- 