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

