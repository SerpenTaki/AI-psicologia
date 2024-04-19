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
- Questo è particolarmente problematico con la funzione di attivazione sigmoide che tende a saturare quando la somma pesata degli input è troppo grande o troppo piccola
-> La derivata tende a zero nella zona di saturazione, quindi il gradiente svanisce nel giro di pochi passi di retro-propagazione
### Cosa ha consentito la rivoluzione del *deep learning*
- **Miglioramento algoritmi**
	- inizializzazione dei pesi più furba (invece che random)
	- Learning rate adattivo in base al gradiente
	- Utilizzo di reti di grandi dimensioni combinate con efficaci regolarizzatori
	- Ottimizzatori del 2° ordine (*derivata seconda stima curvatura del gradiente*)
	- Funzione di attivazione che non satura il gradiente
	- Disponibilità di enormi training set digitali (**BIG DATA**)
	- Aumento delle prestazioni di calcolo  (*Hardware di calcolo parallelo, GPU*)
	- Per applicazioni di *computer vision*, utilizzo di architetture convoluzionali
## Hardware per calcolo parallelo
- Architetture di calcolo parallele consentono di sfruttare il parallelismo inerente delle reti neurali (*Parallel Distributed Processing*)
- Recentemente è stato introdotto hardware molto potente ed economico: *Graphic Processing Unit (GPU)* --> schede video inventate per *gaming*
- Possiamo addestrare reti neurali gerarchiche con migliaia / milioni di neuroni e connessioni sinaptiche
![[Screenshot 2024-04-18 alle 20.38.54.png]]
## Reti neurali convoluzionali (Convolutional Neural Networks, CNN)
![[Screenshot 2024-04-18 alle 20.40.11.png]]
- La CNN è una rete profonda che include almeno uno **strato convoluzionale** (*convolution layer*), in cui i neuroni nascosti non sono interamente connessi con lo strato precedente ma hanno campi recettivi locali
- Lo strato convoluzionale è di solito seguito da uno **strato di pooling** (*pooling layer*) per ridurre la dimensionalità ed enfatizzare le caratteristiche più salienti
- Nella parte più profonda della rete è inserito almeno uno **strato di pooling** (*pooling layer*) per ridurre la dimensionalità ed enfatizzare le caratteristiche più salienti.
- Nella parte più della rete è inserito almeno uno strato nascosto "standard", ovvero interamente connesso (*fully connected*) con quello precedente.
- L'ultimo strato nascosto (*fully connected*) attiva lo strato di output (categorie)
#### Lo strato convoluzionale
- Ogni neurone dello **strato convoluzionale** ha un campo recettivo locale, che codifica una feature specifica (anche chiamata *kernel* o filtro)ù
- Il numero di neuroni definisce quante *features* verranno rappresentate in ciascun filtro è applicato all'intera immagine attraverso un'operazione di convoluzione
-> È come avere più copie dello stesso neurone: utilizziamo lo stesso insieme di pesi per processare diverse porzioni dell'immagine in input
![[Screenshot 2024-04-19 alle 15.17.05.png]]
### Mappe di features
Diversi filtri generano una mappa diversa a partire dalla stessa immagine, enfatizzandone una particolare caratteristica (*feature map*)
### Reti neurali convoluzionali: iperparametri
- **Numero di neuroni nascosti:** specifica quanti filtri usare in ciascun layer
- **Dimensione kernel:** definisce il campo recettivo del filtro
- **Stride:** dimensione del passo di spostamento del filtro (*overlap*)
- **Padding:** per mantenere invariata la dimensione dell'immagine, si imposta un bordo aggiuntivo con valori costanti (*solitamente a zero*)
### Lo strato di pooling
Lo strato di **pooling** viene inserito dopo uno strato convoluzionale per ridurre la dimensione dell'immagine (operazione di **max pooling**). Questo riduce il numero di parametri, controllando l'overfitting, e promuove l'invarianza (*es. alla traslazione*).
![[Screenshot 2024-04-19 alle 15.51.38.png]]
![[Screenshot 2024-04-19 alle 15.51.49.png]]
![[Screenshot 2024-04-19 alle 15.52.11.png]]
![[Screenshot 2024-04-19 alle 15.52.29.png]]
![[Screenshot 2024-04-19 alle 15.52.50.png]]
## ResNet
![[Screenshot 2024-04-19 alle 15.54.38.png]]
- Aumentando il numero di strati nelle reti profonde l'accuratezza migliora ma ad un certo punto si interrompe (*saturazione*) e si osserva rapida degradazione della performance anche sul training set.
- **ResNet** usa la tecnica di "mapping residuo" per ovviare a questo problema. Le connessioni dirette eseguono un mapping che è la funzione identità quindi il mapping non-lineare si concentra sulla *funzione residua*
- La funzione che descrive il mapping input-output, $y=f(x)$, può essere riscritta come $y=f(x)+x$ 
- Lo schema di ResNet si può applicare a strati di diverso tipo (convoluzionali e non)
![[Screenshot 2024-04-19 alle 16.57.32.png]]
![[Screenshot 2024-04-19 alle 16.59.47.png]]
![[Screenshot 2024-04-19 alle 17.00.07.png]]
![[Screenshot 2024-04-19 alle 17.00.16.png]]
![[Screenshot 2024-04-19 alle 17.00.28.png]]
# Vulnerabilità ad attacchi avversari
Possiamo indurre errore di classificazione in una rete neurale profonda facendo modifiche ad hoc all'immagine di input. Questi *esempi avversari* sembrano del tutto innocui all'occhio umano e rappresentano una seria minaccia in contesti sensibili.
- La modifica può essere una perturbazione (*rumore*) del valore dei pixel: questa perturbazione viene costruita ad hoc modificandola in modo da massimizzare la funzione di errore per la specifica particolare immagine
- L'immagine non è distinguibile dall'originale all'occhio umano 
- Una specifica perturbazione può avere lo stesso effetto su una diversa rete profonda!
![[Screenshot 2024-04-19 alle 17.25.45.png]]
