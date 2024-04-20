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
- Le unità LSTM operano attraverso porte ("**gates**") che definiscono (*attraverso l'apprendimento*) se l'informazione vada mantenuta nella memoria temporanea e quanto avanti nel tempo dovrebbe essere propagata
- **Input gate:** lascia entrare l'input nella cella di memoria
- **Output gate:** lascia uscire il valore corrente della cella di memoria
- **Forget gate:** resetta il valore currente nella cella di memoria
NB: Ogni gate ha il suo insieme di pesi sinaptici!
## Deep recurrent neural networks (RNN) per sequenze
![[Pasted image 20240420160057.png]]
- Deep Network con strati nascosti multipli di unità LSTM
- L'input è un elemento della sequenza (es. un frame video)
- L'output è il prossimo elemento della sequenza (es. il prossimo frame)
- Predizione uno step: la rete viene testata sulla predizione del prossimo element, come durante l'apprendimento (es, un frame avanti)
- Predizione *multi-step*: la predizione del prossimo elemento è utilizzata come input e otteniamo la predizione delle successive (es. due frames avanti)
#### Esempio: Generazione di testo
- Deep RNN
- Training set: vari corpus linguistici di larga scala
- Apprendimento a livello del carattere: ogni element nella sequenza è un singolo carattere (lettera o singolo)
![[Pasted image 20240420162011.png]]
### Word embedding
- La modellizzazione di sequenze per l'elaborazione del linguaggio naturale (NLP) è più efficente al *livello della parola*. Questo richiede di codificare le singole parole con vettori di lunghezza fissa usando **algoritmi di embedding**
- **_Word embedding_** è un termine usato per la rappresentazione di parole in forma di un vettore numerico che codifica il significato della parola.
- Esistono vari algoritmi di word-embedding, anche basati su reti neurali
**Proprietà**
- Embeddings preservano relazioni semantiche: parole vicine nello spazio vettoriale hanno un significato simile
- Composizionalità: operazioni lineari sui vettori danno risultati coerenti
	- vec("Madrid")-vec("Spain")+vec("France") è più vicino a vec("Paris") che a qualunque altro vettore
	- vec("Brother")-vec("Man")+vec("Woman") è più vicino a vec("Sister") che a qualunque altro vettore
## "Attention is all you need": Transformers
**Transformer**: *un architettura di rete neurale che si basa su meccanismi di* **_self-attention_** _per trasformare una sequenza di elementi (**tokens**) in input in una sequenza di elementi in output, senza utilizzare convoluzioni o connessioni ricorrenti._
L'architettura generale del Transformer prevede 2 blocchi principali, spesso utilizzati in modo indipendente:
- **Encoder:** costruisce una rappresentazione interna della sequenza utilizzando come contesto per ogni token si gli elementi precedenti (*a sinistra*) che i successivi (*a destra*)
	- *BERT (Bidirectional Encoder Representations from Transformers)* di Google, un encoder transformer addestrato a predire una parola "mascherata" utilizzando come contesto l'intera frase (**_masked language modelling_**)
- **Decoder:** Genera una sequenza di tokens utilizzando solo i tokens precedenti (a sinistra) come contesto per condizionare la generazione.
	- *GPT (Generative Pretrained Transformer)* di OpenAI, un decoder transformer addestrato in modo *autoregressivo* a predire la parola seguente utilizzando come contesto solo le parole precedenti (**_causal language modeling_**)
### Self-attention
Si riferisce al fuoco dell'attenzione, per ogni token rispetto a tutti gli altri tokens di input
![[Pasted image 20240420164606.png]]
![[Pasted image 20240420164622.png]]
## Large Language Models (LLM)
- Basati sull'architettura **Transformer** e addestrati su enormi quantità di testo scaricato da Internet (Wikipedia, giornali, libri etc...)
- Aumentare la scala del Transformer (**NB: n di parametri = n. connessioni**) migliora la performance
- Il modello linguistico viene addestrato con apprendimento self-supervised e successivamente "raffinato" (**fine-tuning**) su compiti specifici con apprendimento supervisionato
- Per migliorare l'accuratezza e ridurre le risposte inappropriate il LLM deve essere "**allineato**" usando il feedback di utenti umani, che viene utilizzato per un ulteriore fine-tuning basato su apprendimento per rinforzo (**Reinforcement Learning from Human Feedback**)
## Generazione di testo in GPT
- Un LLM viene addestrato con self-supervised learning a predire il prossimo **token** data l'attuale sequenza di token di testo come input. **Tokens:** parole, parti di parole, punteggiatura
- La generazione è sequenziale: un **token** ad ogni passo, ottenuto aggiungendo in modo iterativo l'output al contesto
- Ogni token ha una **probabilità** e possiamo utilizzare specifici metodi di **decoding** per selezionare il token, rendendo l'output più variabile ed interessante.
![[Pasted image 20240420165847.png]]
![[Pasted image 20240420165855.png]]
