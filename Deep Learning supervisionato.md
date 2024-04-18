**Concetti chiave nel deep learning:**
- L'elaborazione gerarchica (*profonda*) è caratteristica fondamentale della computazione neurale nel cervello
- La codifica dell'informazione diventa più complessa ed astratta passando a livelli più elevati (*profondi*) della gerarchia
![[Screenshot 2024-04-18 alle 19.17.09.png]]
Nel **Deep Learning** la rete neurale ha un numero di strati nascosti ($>1$ ) che può essere nell'ordine delle decine formando una rete profonda (**deep neural network**).
2 fattori hanno grande importanza per il successo del deep learning:
- **Big data:** accesso grandi quantità di dati etichettati
- **GPU computing:** enorme potenza di calcolo parallelo su schede di processori grafici
Caratteristica distintiva del deep learning rispetto ad altre tecniche di machine learning è che l'apprendimento può avvenire direttamente sui dati grezzi, senza pre-processing/estrazione di features. Queste ultime vengono "*scoperte*" dalla rete durante l'apprendimento
![[Screenshot 2024-04-18 alle 19.21.19.png]]
## Il problema del "*vanishing gradient*"
- Se aggiungiamo molti strati nascosti, il segnale di errore deve passare molti livelli di retro-propagazione prima di giungere alle connessioni più vicine all'input
- 