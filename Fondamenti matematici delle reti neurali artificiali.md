# Il vantaggio di comprendere un metodo:
La modellazione computazionale trae vantaggio dall'utilizzo di strumenti di ricerca **precisi, sistematici** e per quanto possibile **chiaramente definiti**.
- In particolare, un avanzamento più rapido della conoscenza scientifica è solamente supportato dall'adozione di un **linguaggio formale** (_matematico_), dove i concetti vengono definiti nel modo più esplicito possibile
- La dimensione umanistica dell'indagine psicologica rende questo approccio difficile da adottare, tuttavia **per poter avanzare una critica costruttiva occorre innanzitutto comprendere questo metodo a fondo per _apprezzarne i punti di forza ma anche i limiti_**
- Una comprensione più profonda ci aiuta ad essere più critici
### Formalismi matematici usati nel corso
- $net_i=\sum_{j} w_{ij}a_j$ *somma pesata*
- $E_w=1/2 \sum_\mu \sum_i (t_i^\mu - y_i^\mu)^2$ *matrice*
- $\Delta w_{ij} = -(\sigma E)/(\sigma W_{ij})$ *$\Delta$ differenza, $\sigma$ gradiente*
- $\Delta w_{ij} = \eta(t_i - y_i)x_j$ *sigmoide*
- $P(X_i = 1) = 1/(1+e^{-(1/T)\sum_j w_{ij} x_j})$ *probabilità*
- $P(v|h)= \prod_i P(v_i|h)$ *probabilità condizionata*
# Teoria dei grafi
Si Tratta di un potente *formalismo matematico* usato per descrivere e studiare reti di elementi che interagiscono tra loro:
- **rich-club organization**: nel nostro cervello scegliamo un rappresentante per ogni parte che comunica con altre parti.
### Elementi fondamentali:
- **Nodi**: (*vertici* o *unità*) definiscono le variabili da modellare
- **Archi**: (*connessioni* o *spigoli*) definiscono quali variabili interagiscono tra di loro
- **Pesi**: definiscono la forza delle iterazioni 
![[Pasted image 20240307145609.png]]
### Grafi direzionati e non direzionati
- **Gradi direzionati**: codificano relazioni di parentela tra le variabili
*la direzionalità è solitamente relata alla nozione di "causalità": il gallo canta perchè sorge il sole e non vice-versa!*
![[Pasted image 20240307145802.png]]
- **Grafi non direzionati**: codificano solo il "grado di affinità" (*correlazione*)
*in questo caso sappiamo solo che le variabili si influenzano a vicenda. Ma non possiamo stabilire quale sia la causa e quale sia l'effetto*
![[Pasted image 20240307145921.png]]
--
**NB: NON direzionati = Bidirezionale + Simmetrico**
- Quando 2 variabili interagiscono attraverso una connessione non direzionata è come avere 2 connessioni direzionate simmetriche (*ovvero, con lo stesso peso*):
![[Pasted image 20240307150229.png]]
- Se vogliamo specificare un'influenza bidirezionale con pesi diversi, allora dobbiamo ricorrere a 2 archi separati
![[Pasted image 20240307150309.png]]
### Topologia
Specifica la mappa di connettività su un piano 2D
![[Pasted image 20240307150349.png]]
Come vedremo più avanti nel corso, la topologia e la direzionalità del grafo definiscono **l'architettura** di una rete neurale
# Teoria della probabilità
Si tratta di un potente formalismo matematico usato per descrivere e studiare i sistemi stocastici. **Perchè ci interessano i sistemi stocastici?**
- **Ignoranza**: spesso possiamo osservare un sistema solo parzialmente
- Spesso i dati contengono errori e approssimazioni
- Alcuni sistemi sono intrisecamente stocastici
### Elementi fondamentali
- **Variabile casuale:** variabile in cui valore è definito in base ad una qualche funzione di probabilità (es. *distribuzione Gaussiana*)
- **Probabilità condizionata** $P(A|B)$: probabilità di osservare un certo comportamento di una o più variabili casuali, ==dato== il valore di altre variabili
- **Probabilità congiunta** $P(A, B)$: probabilità dell'==intersezione== di 2 o più variabili casuali
	- $P(A, B) = P(A|B) *P(B) = P(B|A)*P(A)$
- **Indipendenza statica**: 2 variabili sono indipendenti se non si influenzano a vicenda. In tal caso la loro distribuzione congiunta corrisponde al prodotto delle loro distribuzioni individuali: $P(A,B) = P(A)*P(B)$ ciò implica che sapere il valore di $B$ non cambia la stima del valore assunto da $A$: $P(A|B)=P(A)$
###### Significato di variabile casuale
*una variabile casuale (detta anche aleatoria o stocastica) è una variabile misurabile che può assumere valori diversi in dipendenza da qualche fenomeno aleatorio, rappresentato attraverso una distribuzione di probabilità*
-> Ciò non significa che la variabile abbia un comportamento *impredicibile* (totalemente random)
![[Pasted image 20240307151830.png]]
## La prospettiva Bayesiana
Invece di stimare probabilità assolute, possiamo interpretare il valore di ciascuna variabile casuale come un **grado di credibilità** (*degree of belief*)
$P(H|E) = (P(E|H)*P(H))/P(E)$ *formula di bayes*
- **Inferenza**: data una certa evidenza (*variabili osservate*), vogliamo trovare la distribuzione di probabilità delle variabili non osservate (*ipotesi*)
	-> *il grado di credibilità di ciascuna ipotesi viene costantemente aggiornato in base all'evidenza corrente*
![[Pasted image 20240307152518.png]]
Questa immagine sembra una faccia, ma se aggiungessimo delle note musicali, potremmo cambiare la nostra ipotesi e pensare sia un musicista
![[Pasted image 20240307152602.png]]
- **Apprendimento:** vogliamo trovare il set di parametri che meglio descrive un insieme di osservazioni (*massima verosimiglianza*)
# Algebra lineare
Descrive e studia spazi vettoriali e le loro trasformazioni lineari.
- In particolare, possiamo usare la notazione compatta (vettori, matrici e relativi operatori) per rappresentare moltissimi concetti geometrici, come rette, piani, vettori e campi di forza, traslazioni, rotazioni, eccettera...
### Elementi fondamentali
- **Spazio vettoriale:** insieme di entità chiamate *vettori*, che possono essere sommate tra di loro e moltiplicate (scalate) per numeri reali, chiamate *scalari*
- **Matrice**: insieme ordinato di elementi, rappresentato in forma tabulare, ovvero, disponendo gli elementi per righe e colonne.
- **Iperpiano**: sottospazio di dimensione inferiore di uno $(n-1)$ rispetto allo spazio in cui è contenuto ($n$)
	- Per esempio:
		- In uno spazio 2D, gli iperpiani sono singole rette 1D
		- In uno spazio 3D, gli iperpiani sono i piani 2D
- **Trasformazione (_mapping_) lineare**: funzione fra 2 spazi vettoriali (es: $R^2 --> R^2$) che preserva le operazioni di addizione tra vettori e moltiplicazione scalare.
	- In senso intuitivo, un mapping lineare non altera la *linearità* di una curva. Può stirare e riscaldare i vari punti, ma non può alterarne la curvatura
# Analisi matematica: a cosa serve?
Studiare come le funzioni cambiano nel tempo e nello spazio:
- Possiamo analizzare la ==curvatura== di una funzione per trovare i suoi punti di *massimo e minimo*, misurare dove la funzione ==cresce più velocemente==, studiare il comportamento della funzione ad intervalli infinitamente piccoli o infinitamente grandi (==limiti==) eccettera
- In generale siamo interessati alle funzioni ==multivariate== ovvero che richiedono in input più di una variabili
### Elementi fondamentali
- **Derivata** _di una funzione_: sensibilità al cambiamento di una certa quantità (*variabile dipendente*), la quale è determinata da un'altra quantità (*variabile indipendente*)
- **Gradiente** _di una funzione_: generalizza il concetto di derivata a funzioni multivariate:
	- corrisponde al vettore le cui componenti sono le *derivate parziali* della funzione.
- **Massimi e minimi** _di una funzione_: punti stazionari dove la curvatura raggiunge valore massimo o minimo. Sono chiamati massimi o minimi *locali* se esiste un punto più elevato o più piccolo da qualche altra parte nella curva.
	- Se un punto corrisponde ad un massimo o minimo, allora la derivata in quel punto è nulla (ovvero la retta tangente è parallela all'asse x)
	- Questa proprietà è utile: quando vogliamo minimizzare una certa funzione, basterà trovare i punti dove la derivata di annulla! o per funzioni a *più dimensioni* dovremo spostarci nella curva nella direzione dove il gradiente è maggiore (tecnica della **discesa del gradiente**)
![[Pasted image 20240307155558.png]]
![[Pasted image 20240307155618.png]]
## Sistemi complessi non-lineari
- Le trasformazioni lineari sono comode, perchè hanno una serie di proprietà matematiche che le rendono facili da manipolare
- Tuttavia sappiamo vene che la natura non è affatto lineare!
- I modelli *non-lineari* sono molto più espressivi rispetto a quelli lineari, in quanto consentono di rappresentare strutture e dinamiche più interessanti.
- Tuttavia, questa maggiore flessibilità ha un prezzo non trascurabile: i modelli non-lineari sono molto più difficili da studiare
![[Pasted image 20240307155909.png]]
# Algoritmo
Un algoritmo è un procedimento, implementato attraverso una sequenza ordinata e finita di passi (operazioni o istruzioni) elementari, che conduce a un ben e determinato risultato in un tempo finito.
### Algoritmi che apprendono
- L'idea fondamentale alla base degli algoritmi di apprendimento automatico (**machine learning**) è di fare in modo che **l'algoritmo stesso possa modificare la propria _struttura_ con l'esperienza**
- Per esempio, se l'output dell'algoritmo dipende da alcune variabili memorizzate, possiamo programmare l'algoritmo affinchè modifichi autonomamente tali variabili **a seconda degli input che gli vengono mostrati**
- In altre parole, il comportamento dell'algoritmo dipende dal valore di alcuni suoi stati interni, e l'algoritmo ha la capacità di modificare in modo autonomo tali stati in base al tipo di esperienza che riceve
- Nel caso di una rete neurale artificiale, il sistema modifica la forza delle connessioni sinaptiche in base alle informazioni rilevate in un particolare insieme di esempi di *addestramento* (training set)

