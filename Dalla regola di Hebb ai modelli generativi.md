## Scoprire regolarità con apprendimento associativo: La regola di Hebb
Idea: "*Neuron wire together if they fire together*"
-> **La regola di Hebb scopre _correlazioni_ nei dati**
$\Delta W = \eta xy$ 
![[Pasted image 20240420191819.png]]
# Regola di Hebb e memorie associative
Possiamo usare la regola di Hebb per apprendere i pesi sinaptici di reti più complesse?(_SI_) In questo modo possiamo **memorizzare** interi pattern!
![[Pasted image 20240420191925.png]]
![[Pasted image 20240420191959.png]]
## Ispirazione: Meccanica statistica
- La meccanica classica (*Galileo, Newton, Leibniz*..) considera equazioni **deterministiche** per descrivere il comportamento dei sistemi fisici
- Con l'avvento della meccanica statistica, molte proprietà fisica sono state per la prima volta definite utilizzando il linguaggio delle **probabilità**
- Per esempio, nella termodinamica possiamo mettere in relazione proprietà *microscopiche* di atomi e molecole (*spin, massa, carica...*) con proprietà *macroscopiche* della materia, che possono essere percepite su scala umana (*temperatura, proprietà magnetiche*...)
- **Modelli di Ising**
	- Componenti elementari (atomi) interagiscono con i loro vicini in un lattice bi-dimensionale
	- Ciascun atomo può trovarsi in 2 possibili stati discreti (*spin*)
	- Il sistema diventa ferromagnetico (*proprietà macroscopica*) quando tutti gli spin sono allineati
- La dinamica del sistema è governata da una **funzione di energia**
- Il sistema esplora varie configurazioni, e si assesta in quelle più **probabili** (ovvero, quelle con energia minima)
- Normalmente, tuttavia, il sistema non raggiunge uno stato uniforme (dove l'energia viene minimizzata **globalmente**), ma piuttosto si assesta in configurazioni eterogenee dove l'energia è minimizzata **localmente**
#### Perchè la frustazione può essere utile
- In altri tipi di sistemi, all'equilibrio si raggiungono configurazioni omogenee, senza frustazione
	- Nel caso dei metronomi questo accade perchè condividono la stessa pedana di vibrazione
	- Ma **fortunatamente** non tutti i sistemi finiscono per essere omogenei -> in un sistema omogeneo non c'è informazione!
	- https://www.youtube.com/watch?v=n81XIZRyhQE
## Dai modelli di Ising alle reti di Hopfield
1. Sostituiamo "atomi" con "neuroni"
2. Facciamo in modo che le interazioni locali si possano **modificare attraverso apprendimento Hebbiano**
### Reti di Hopfield: memorie associative *energy based*
- Possono essere usate per **memorizzare e recuperare** pattern
- La memorizzazione avviene cambiando gradualmente la forza delle connessioni
- Il recupero avviene in modo dinamico, aggiornando iterativamente lo stato dei neuroni finchè non si raggiunge uno stato stabile (*attrattore*)
- In analogia con la meccanica statistica, l'idea di base è quella di usare una funzione di energia per specificare quali stati della rete sono più probabili
- Lo scopo dell'apprendimento è di assegnare alta probabilità alle configurazioni osservate nel training set
- Quando si presenta un pattern corrotto, la rete gradualmente si assesterà nella configurazione corrispondente al pattern memorizzato più simile
#### Reti di Hopfield: Architettura
- La rete è ricorrente (*tutte le connessioni sono bidirezionali*) con topologia completamente connessa (*tutti i neuroni sono collegati fra loro*)
- Non ci sono auto-connessioni
- Le reti di Hopfield possono quindi essere interpretate come modelli grafici non direzionati (*pesi simmetrici*)
- Tutti i neuroni sono "visibili", ovvero ciascuno corrisponde ad una variabile in input. Per  esempio, ciascun neurone potrebbe corrispondere ad un pixel in un'immagine digitale.
#### Reti di Hopfield: Energia ed Attrattori
L'energia $E$ di una certa configurazione delle attivazioni dei neuroni è data da: 
$$
E = -(1/2)\sum_{ij} w_{ij}x_ix_j
$$
Gli attrattori della rete corrispondono ai punti di minimo locale della funzione di energia e rappresentano pattern stabili di attività che codificano una "memoria" (*ovvero, un determinato pattern di input*)
### Minimizzare l'energia
- Ci sono 2 meccanismi che consentono di minimizzare l'energia:
![[Pasted image 20240420194622.png]]
#### Reti di Hopfield: Inferenza
I neuroni hanno stati binari ($-1$ o $+1$) e la loro attivazione è calcolata utilizzando la regola:
![[Pasted image 20240421110022.png]]
In altre parole ciascun neurone $x_i$ effettua una somma pesata delle attività di *tutti* gli altri neuroni $x_j$ e si attiva solo se il valore supera una determinata soglia (_funzione di attivazione a scalino o step -> vedi **Percettrone**_)
- Hopfield ha dimostrato che, se i pesi hanno valori appropriati, le attivazioni della rete convergeranno sempre verso uno stato stabile (*attrattore*), dove le attivazioni non cambiano più (la rete raggiunge l'*equilibrio*)
#### Reti di Hopfield: apprendimento
- Ma come possiamo impostare i pesi della rete, in modo che vengano posi recuperate le *memorie corrette*? Usando apprendimento Hebbiano!
- Ogni pattern di training viene presentato iterativamente alla rete *vincolandolo* nei neuroni, e le connessioni fra i neuroni vengono modificate in base alla regola:
![[Screenshot 2024-05-05 alle 15.23.22.png]]
### L'apprendimento "scava" il bacino degli attratori
- L'apprendimento in una rete di Hopfield modifica la funzione di energia in modo tale da creare attrattori corrispondenti ai pattern di training
- Allo stesso tempo, l'energia di configurazioni improbabili deve essere aumentata
![[Screenshot 2024-05-05 alle 15.40.46.png]]
## Attratori spuri
Se incrementiamo il numero di pattern (attrattori) da memorizzare la rete sviluperà anche un certo numero di memorie sbagliate, chiamate **attrattori spuri** che non corrispondono a minimi locali ma comunque rappresentano stati di equilibrio, e possono impedire alla rete di recuperare la memoria corretta
-> Questo problema può essere mitigato introducendo una **dinamica stocastica**
![[Screenshot 2024-05-05 alle 16.25.52.png]]
### Dinamica stocastica
Per evitare di rimanere intrappolati in cattivi minimi locali, possiamo sostituire la funzione di attivazione deterministica con una funzione stocastica:
![[Screenshot 2024-05-05 alle 16.26.53.png]]
#### Parametro Temperatura
Manipolando la curvatura della sigmoide, la temperatura definisce quanto il sistema è stocastico, ovvero, quanto la sua dinamica sarà **rumorosa/casuale:**
![[Screenshot 2024-05-05 alle 16.28.05.png]]
## Simulated Annealing
- Per raggiungere il miglior minimo di energia cominciamo con una temperatura alta nel sistema, e poi gradualmente lo *raffreddiamo*: la temperatura viene progressivamente ridotta finchè il sistema diventa deterministico
- Questa procedura di ottimizzazione è ispirata dal metodo di ricottura dei metalli (*annealing*) che vengono raffreddati gradualmente allo scopo di ottenere configurazioni atomiche più ordinate (*es: lame più dure e resistenti*)
![[Screenshot 2024-05-05 alle 16.33.14.png]]
![[Screenshot 2024-05-05 alle 16.33.32.png]]
![[Screenshot 2024-05-05 alle 16.33.49.png]]
# Reti neurali generative
