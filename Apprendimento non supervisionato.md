##### Principali paradigmi di apprendimento automatico
- **Supervisionato** (*classificazione, categorizzazione, approssimazione di funzione, regressione...*) [[Apprendimento supervisionato]]
	- Assumiamo che un segnale esterno di supervisione (*teacher*) sia disponibile ad ogni evento di apprendimento per aiutare il sistema a *risolvere un compito*
	- potente, ma spesso poco plausibile dal punto di vista cognitivo
- **Non supervisionato** (*estrazione features latenti, apprendimento di rappresentazioni, clustering, riduzione di dimensionalità...*) [[Apprendimento non supervisionato]]
	- Il sistema cerca di scoprire le regolarità statistiche del mondo *semplicemente osservando* l'ambiente circostante
	- percezione e cognizione come processi di model building
- **Con Rinforzo** (*decision making, controllo cognitivo, funzioni esecutive*) [[Apprendimento Automatico]]
	- Il sistema cerca di scoprire le regolarità sttatistiche **interagendo** con l'ambiente circostante
	- utile ma difficile da implementare
![[Pasted image 20240420170837.png]]
## Caratteristiche dell'apprendimento non supervisionato
**Vantaggi**:
- L'apprendimento non richiede nessuna etichetta (*label*) negli esempi. Ciò significa che il sistema può sfruttare l'enorme quantità di informazione "grezza" presente nell'ambiente
- Una volta appreso un buon modello interno dell'ambiente (processo di estrazione di *features* o di apprendimento di rappresentazioni), esso può essere utilizzato anche per apprendere più facilmente task supervisionati (*transfer learning*)
- Sembra che gli animali sfruttino massivamente questa modalità di apprendimento durante lo sviluppo
**Svantaggi**:
- Spesso non è chiaro quali *features* dell'ambiente saranno poi utili per risolvere un determinato compito, o cosa costituisca una "buona" rappresentazione
- L'apprendimento non supervisionato richiede molte risorse computazionali. A volte sarebbe più conveniente avere un esperto (*teacher*) che aiuta a risolvere un compito
- Dalla semplice osservazione  dell'ambiente non possiamo inferire relazioni causali
### L'importanza di scoprire buone rappresentazioni
![[Pasted image 20240420184921.png]]
![[Pasted image 20240420184948.png]]
![[Pasted image 20240420185001.png]]
![[Pasted image 20240420185024.png]]
### Riduzione lineare della dimensionalità: PCA
- La Principal Component Analysis (PCA) è una tecnica statistica che cerca di trovare la direzione di massima variabilità in un certo insieme di dati
- Puù precisamente, lo scopo della PCA è di scoprire un insieme di variabili linearmente scorrelate (*le componenti principali*) che spieghino la maggior parte della varianza osservata nella distribuzione
![[Pasted image 20240420185651.png]]
Spesso PCA cattura la maggior parte della varianza in poche dimensioni! $<5$
# Comprimere dati tramite PCA
La scomposizione dei dati data dalla PCA può essere usata per mappare i pattern di input in un nuovo sistema di coordinate a bassa dimensionalità:
![[Pasted image 20240420185911.png]]
![[Pasted image 20240420185927.png]]
![[Pasted image 20240420185935.png]]
![[Pasted image 20240420185948.png]]
![[Pasted image 20240420190004.png]]
# Autoencoders
- Possiamo costruire una rete neurale che riduce la dimensionalità dei dati chiedendo che "ricostruisca" in output il pattern presentato in input
- La funzione di errore è rappresentata dall'errore di ricostruzione (*es: scarto quadratico medio*):
![[Pasted image 20240420190150.png]]
- Se forziamo la rete neurale a codificare i dati di input utilizzando un numero ridotto di neuroni nascosti, imparerà a **comprimere** la distribuzione dei dati estraendone le features più rilevanti
- Utilizzando neuroni nascosti con funzione di attivazione lineare, il risultato sarà molto simie a quello ottenuto con la PCA
- Utilizzando neuroni nascosti con funzione di attivazione non lineare (*es. sigmoide*) effetueremo invece una **riduzione non-lineare della dimensionalità**
### Denoising autoencoders
- L'estrazione di features può essere resa più robusta introducendo rumore nei dati
- il rumore funge da **regolarizzatore** (in modo analogo a *weight decay* o *dropout*)
![[Pasted image 20240420190714.png]]
### Analisi dello spazio latente
Utilizzando solamente 2 neuroni nascosti possiamo addirittura comprimere i dati in un piano bidimensionale!
![[Pasted image 20240420190822.png]]
### Autoencoders Variazionali
- Negli ultimi anni sono stati introdotti modelli di autoencoders più performanti, che introducono ulteriori regolarizzatori nello spazio lantente
- Ciò consente di **generare nuovi dati** partendo dalla codifica latente
![[Pasted image 20240420191042.png]]
