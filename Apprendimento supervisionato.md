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
slide 15/19
