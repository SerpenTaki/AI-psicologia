**Computazione neurale** (*neural computing / neural computation*):
	L'elaborazione dell'informazione eseguita da reti di neuroni, biologici o artificiali. Rappresenta un modello alternativo a quello della computazione digitale.

Le reti neurali biologiche sono formate da neuroni che si influenzano attraverso le connessioni (*sinapsi*) che li collegano
- Ogni neurone *rileva* un certo insieme di condizioni e *segnala* ciò che ha rilevato attraverso la sua frequenza di scarica
- I neuroni possono ricevere segnali da altri neuroni e formare *strati di rilevatori* più complessi
- Le interazioni tra neuroni sono *adattive* e si modificano attraverso l'*apprendimento*
### Il modello del "rilevatore"
Ogni neurone "*rileva*" un qualche insieme di condizioni.
La *Rappresentazione* è ciò che viene rilevato.

|  | Computer | Rilevatori |
| ---- | ---- | ---- |
| **Memoria ed elaborazione** | Separata, uso generico | Integrata, specializzata |
| **Operazioni** | Logiche, aritmetiche | Detezione/rilevazione (*accumulo di evidenza, valutazione, comunicazione*) |
| **Elaborazione complessa** | Sequenze arbitrarie di operazioni concatenate in un programma | Gruppi di rilevatori altamente "*sintonizzati*", organizzati in strati |
### Codifica dell'informazione nel neurone biologico
![[Screenshot 2024-03-13 alle 12.51.46.png]]
Il neurone è sintonizzato su uno stimolo preferito, che quando è presente produce la risposta più forte. Il **_campo recettivo_** del *neurone* è quella porzione di spazio sensoriale (*es. posizione sulla retina*) che attiva la risposta del neurone.
###### Elaborazione gerarchica: un principio generale di organizzazione neurale
**La codifica dell'informazione diventa più complessa ed astratta passando a livelli più elevati (_profondi_) della gerarchia** *(motivazione per il deep learning)*
# Reti neurali artificiali
- Le reti neurali artificiali sono sistemi di elaborazione
	- Caratterizzati dalla capacità di *apprendere* compiti complessi
	- *inspirati* dal funzionamento dei sistemi biologici - lo scopo non è di riprodurne tutta la complessità ma di catturarne i *principi di base*
- Una rete neurale artificiale ha un'architettura ed *elaborazione distribuita e parallela* che utilizza:
	- semplici unità di elaborazione
	- Un'elevato grado di interconnessione
	- Semplici messaggi numerici scalari (segnali _analogici_)
	- Interazioni adattive tra elementi
- Proprietà importanti dei sistemi di computazione neurale
	- Apprendono dall'esperienza ma rispondono anche in situazioni nuove
	- Non necessitano di conoscenze esplicite sul problema
	- Si adattano a situazioni caotiche e/o contraddittorie (_rumore_ nei dati)
- Nell'ambito IA, le reti neurali artificiali sono un metodo di **machine learning** (*apprendimento automatico*)
	- Esistono altri metodi ed algoritmi per apprendere dai dati. Attualmente le reti neurali `<<profonde>>` (*deep learning*) sono lo stato dell'arte del machine learning ed il principale motore nelle applicazioni dell'IA
- Nell'ambito delle scienze cognitive (psicologia, neuroscienze) le reti neurali artificiali sono utilizzate per studiare e riprodurre le ambiguità cognitive ed il comportamento umano
	- L'obiettivo non è di tipo *riduzionista*->(*spiegare le funzioni psicologiche attraverso la neurofisiologia*) ma piuttosto di "ricostruire" queste funzioni come *proprietà emergenti* dei sistemi neurali
	- Spiegare il funzionamento di una funzione cognitiva corrisponde al fornire un'*adeguata simulazione* utilizzando un substrato di elaborazione che assomigli quanto più possibile al substrato neuronale
### Elementi di base
- **Neuroni** (_unità di elaborazione_): servono da rilevatori, segnalano attraverso la loro attivazione
- **Reti neurali**: connettono, coordinano, amplificano, selezionano pattern di attivazioni su neuroni
- **Apprendimento:** organizza le reti per eseguire compiti e per sviluppare modelli interni dell'ambiente
#### Il neurone
- Un **neurone formale** (*unità di elaborazione o nodo*) è un modello matematico che cerca di catturare gli aspetti fondamentali del funzionamento neuronale
	- I neuroni hanno **connessioni** con altri neuroni dai quali ricevono segnali
	- Ogni connessione ha un **peso** che indica la forza della connessione e può essere *positivo* (eccitatorio) o *negativo* (inibitorio)
	- L'**input** che un neurone riceve da ciascuno dei neuroni cui è connesso si calcola _moltiplicando il segnale_ proveniente da quel neurone per il *peso* sulla connessione
	- Lo stato di attivazione finale viene calcolato attraverso una **funzione di attivazione o di output** del neurone (ad esempio la *sigmoide* [[Fondamenti matematici delle reti neurali artificiali]])
#### Il neurone artificiale
![[Screenshot 2024-03-13 alle 13.13.37.png]]
![[Screenshot 2024-03-13 alle 13.14.08.png]]
**NB:** *la funzione sigmoide va da 1*, $o_i = 1/(1+e^{-net_i})$
![[Screenshot 2024-03-13 alle 13.16.11.png]]
## Reti di neuroni
L'*architettura* della rete identifica:
- L'organizzazione in gruppi o *strati* dei neuroni (*topologia della rete*)
	- Unità che ricevono input direttamente dell'ambiente formano lo *strato di input*
	- Unità che producono l'output finale della rete formano lo *strato di output*
	- Unità che non si trovano in contatto diretto con input o output sono chiamate *unità nascoste*. Al contrario, unità di input e di output vengono a volte chiamate *unità visibili*
	- Con $n>=2$ strati nascosti parleremo di *rete profonda* (*deep network*)
- Il modo in cui i neuroni sono collegati tra di loro (*schema di connettività*)
	- *Reti feed-forward*: ci sono solo connessioni unidirezionali da unità di input a unità nascoste a unità di output (*bottom-up*) -> reti A e B
		- *sono le più diffuse e portano l'input verso l'output (?) ovvero le freccie sono unidirezionali e vanno solo veso l'output*
	- *Reti ricorrenti:* ci sono connessioni bidirezionali, in cui l'attivazione può propagarsi all'indietro (*top-down o feedback*) -> rete C
	- *Reti internamente ricorrenti*: come le reti ricorrenti ma ci sono connessioni **intra-strato** (*laterali*) -> rete D
![[Screenshot 2024-03-13 alle 13.26.23.png]]
**NB**: classi di reti diverse spesso richiedono algoritmi di apprendimento diversi.

