# La dimensione temporale
L'informazione in **input** può arrivare al sistema neurale in modo sequenziale e quindi può possedere una *struttura temporale*. Anche l'**output** può avere una sequenziale:
- riconoscimento del parlato (da spettrogramma audio a sequenza di fonemi e/o parole)
- riconscimento di azioni
- predizione della dinamica in oggetti in movimento
- generazione di testo o di musica
- predizione di serie storiche: item$(n+1) = f$(item($n$))
### Come appendere compiti sequenziali?
In una classica rete multistrato l'output $O(t)$ al tempo $t$ dipende ==solo== dall'input corrente $I(t)$. Quindi non può apprendere dipendenze temporali.
###### Come apprendere una sequenza?
**Una possibile soluzione**: trasformare il *tempo* in *spazio*: presentiamo come input alcuni elementi della sequenza S in una finestra temporale $W^t (t)$ che si sposta sopra S: $W^t (t) = [S_t, S_{t+1},...,S_{t+T}]$ 
**Problemi:**
1. I **neuroni** di input vengono replicati per ogni elemento rappresentato nella *finestra*
2. **visibilità limitata** dalla grandezza della finestra

![[Screenshot 2024-04-19 alle 21.55.23.png]]
## Reti Parzialmente Ricorrenti
**(Simple Recurrent Networks - SRN)**
- Un modo semplice di elaborare strutture temporali consiste nell'aggiungere **connessioni ricorrenti** che forniscano un *input ricorrente proveniente* dallo stesso strato o da strati superiori
- In questo modo, le risposte delle reti dipendono da:
	1. Input classico *feed-forward* degli strati inferiori;
	2. input da stati precedenti
- Lo *stato S(t)* delle reti ricorrenti dipende non solo dallo stato precedente *S$(t-1)$*, ma anche da *tutti gli stati passati* $S(1)....S(t-1)$
- La rete apprende una *sequenza di stati target*
![[Screenshot 2024-04-19 alle 22.00.22.png]]
#### Addestrare reti ricorrenti
Le reti ==parzialmente ricorrenti== si possono addestrare con l'algoritmo *back-propagation*, perchè la struttura temporale può essere *srotolata* trasformandola in una struttura spaziale.
In questo esempio la sequenza di input $S[x^1 x^2]$ viene trasformata in una serie di passi che possono essere appresi da una rete *statica*.
Aggiorniamo i pesi con la somma del cambiamento ad ogni livello (*passo nel tempo:*) $\Delta w_{ij} = \sum_t \Delta w_{ij}^t$ 
### Le reti di Elman (SRN) 1990
![[Screenshot 2024-04-19 alle 22.06.10.png]]
- Neuroni di output $y_i^t=$ sigm($\sum_j w_{ij}^t h_j^t$)
- Neuroni nascosti $h_i^t =$ sigm$(\sum_j w_{ij}^t x_j^t + \sum_k w_{ik}^t c_k^t)$
- **Neuroni contesto** $c_i^t = h_i^{t-1}$ è la copia dello stato dei neuroni nascosti al passo precedente $h_i^{t-1}$
## Apprendimento di sequenze: self-supervised learning
- **Training Set:** sequenze di lettere che formano frasi in inglese
- **Compito:** *predire il prossimo elemento nella sequenza*
- NB: Questo tipo di apprendimento viene attualmente chiamato **self-supervised learning** perchè input e target hanno *la stessa natura*
#### Scoprire la struttura temporale
La rete scopre categorie lessicali:
- Le attivazioni delle unità nascoste (*rappresentazioni interne*) corrispondenti ad ogni parola sono state analizzate usando clustering gerarchico
- La rete raggruppa le parole in base al loro utilizzo, ovvero al contesto circostante, scoprendo diverse categorie lessicali.
![[Screenshot 2024-04-19 alle 22.14.09.png]]
## Long-Short Term Memory (LSTM) networks
- Le SRN hanno una memoria "a breve termine" (short-term memory): non riescono ad apprendere dipendenze temporali lontane nella sequenza di input
- Questo problema viene risolto nelle reti LSTM, in cui lo strato nascosto è formato da unità LSTM che hanno una struttura più complessa rispetto ai tipici neuroni nascosti
- Le unità LSTM operano attraverso porte ("**gates**") che definiscono (*attraverso l'apprendimento*) se l'informazione