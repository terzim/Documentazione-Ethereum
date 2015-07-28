_traduzione di M.Terzi e L.M.Pedretti ([Ethereum Italia](www.ethereum-italia.it)) da un articolo originale di S. Tual, apparso [qui](https://blog.ethereum.org/2015/07/27/final-steps/)._

# Le fasi finali

Un aggiornamento come promesso: tutti i sistemi sono ora “pronti” sul lato tecnico e abbiamo intenzione di rilasciare Frontier questa settimana.

Grazie a tutti coloro che hanno dato feedback sul mio precedente post. Che ne è stato evidente è che prima del grande giorno, molti di voi hanno voluto sapere di più su ciò che la sequenza degli eventi sarebbe esattamente, e come preparare la macchina per il rilascio.

## Un rilascio aperto e trasparente 

Gli utenti di Frontier dovranno innanzitutto generare, e poi caricare sul loro client Ethereum il blocco Genesis. Il blocco Genesis rappresenta un file di database: contiene tutte le transazioni che derivano dalla pre-vendita di Ether, e quando un utente carica questo file sul client, prende la decisione di aderire alla rete sotto i suoi termini: è un primo passo verso il consenso.

Poiche’ la pre-vendita di Ether si è svolta interamente sulla blockchain di Bitcoin, i suoi contenuti sono pubblici, e chiunque può generare e verificare il blocco Genesis. Nell'interesse del decentramento e della trasparenza, Ethereum non fornirà il blocco Genesis come file da scaricare, ma ha invece creato uno script open source che chiunque può utilizzare per generare il file, il cui link si trova più avanti in questo articolo.

Dal momento che lo script è già disponibile ed il rilascio deve essere coordinato, lo script contiene un argomento che prevede il lancio di Frontier _all'unisono_. Ma come e' possibile far cio' ***_e_*** rimanere decentralizzati?

L'argomento deve essere un parametro casuale che nessuno, neppure noi, sia in grado di prevedere. Come potete immaginare, non esistono molti parametri al mondo che corrispondono a questo criterio, ma un buon esempio è l'hash di un futuro blocco sulla rete di test (testnet) di Ethereum. Abbiamo dovuto scegliere un numero di blocco, ma quale? Il numero 1,028,201 risulta essere sia primo che palindromo, proprio come piace a noi. Dunque abbiamo scelto il blocco numero 1,028,201.

***_La sequenza delle fasi di lancio:_***

- Le fasi finali per il rilascio di Ethereum sono state svelate: le state leggendo in questo momento.
- Il blocco numero 1,028,201 viene creato sulla tesnet di Ethereum, e ad esso viene attribuito un hash.
- L'hash viene utilizzato dagli utenti di tutto il mondo come parametro unico per lo script di creazione del blocco Genesis.

## Cosa potete fare ad oggi

In primo luogo, è necessario installare il client. Userò Geth come esempio, ma lo stesso risultato può essere ottenuto con [Eth](https://github.com/ethereum/cpp-ethereum/wiki) (l’implementazione C ++ di Ethereum). Le istruzioni per l'installazione di Geth su Windows, Linux e OSX si possono trovare sulla nostra [wiki](https://github.com/ethereum/go-ethereum/wiki/Building-Ethereum).

Dopo aver installato uno dei client, è necessario scaricare lo script python che genera il file Genesi. Si chiama 'mk_genesis_block.py', e può essere scaricato [a questo indirizzo](https://raw.githubusercontent.com/ethereum/genesis_block_generator/master/mk_genesis_block.py).

A seconda della piattaforma che utilizzate, è possibile anche scaricarlo dalla console, installando curl e lanciando il comando sottostante:

```
curl -O https://raw.githubusercontent.com/ethereum/genesis_block_generator/master/mk_genesis_block.py
```

Questo comando creerà il file nella stessa cartella in cui viene eseguito. A questo punto è necessario installare i pybitcointools creati dal nostro Vitalik Buterin. È possibile ottenere questo attraverso il gestore pip pacchetto python, così ti installare pip prima, poi gli strumenti subito dopo.

Le seguenti istruzioni dovrebbero funzionare su OSX e Linux. Utenti di Windows, buona notizia per voi, pip viene fornito con il programma di installazione standard di [Python](https://www.python.org/downloads/windows/).

```
curl -O https://bootstrap.pypa.io/get-pip.py
sudo python get-pip.py
```

```
sudo pip install bitcoin
```

o (se avete avuto già installato),

```
sudo pip install bitcoin --upgrade
```

Un ultimo passo, se utilizzate Eth, abbiamo recentemente [deciso] di supportare il nuovo parametro blocco Genesi, quindi avrete bisogno di prendere la versione corretta del software per essere pronti per il grande giorno:

```
cd ~/builds/go-ethereum/
git checkout release/1.0.0
git pull
make geth
```

Coloro che vogliono essere il 'piu' pronti possibile' possono limitarsi a seguire le instruzioni fino a questo punto, anche se va detto che un ```git pull``` appena prima che il blocco fatidico sia generato è probabilmente consigliabile al fine di essere sicuri di utilizzare la versione più recente dei software.

Se avevate gia' i client in esecuzione precedentemente:

- Fate un backup delle chiavi (forse alcune di loro sono ammissibili per i premi della release Olympic) - si trovano nella directory ./ethereum/keystore
- Eliminate per favore la vostra vecchia blockchain (si trova nella directory ./ethereum, eliminate per favore unicamente le seguenti 3 cartelle: ./extra, ./state, ./blockchain)
- Si possono tranquillamente lasciare al loro poste le cartelle ./ethereum/nodes, ./ethereum/history e ./ethereum/nodekey
- Avere una DAG gia' generata nella cartella ./ethash non farà male, ma sentitevi liberi di cancellarla se avete bisogno di spazio

Per una ripartizione completa di dove si trovano i file di configurazione, si prega di consultare [questa pagina sul nostro forum](https://forum.ethereum.org/discussion/2114/where-are-my-config-files-go-and-cpp).

A quel punto, è tutta questione di attendere che venga generato il blocco numero ***1,028,201***, che al ritmo attuale di risoluzione dei blocchi, dovrebbe essere formato all'incirca Giovedi sera (ora di Londra, GMT + 0).

Quando il blocco numero 1,028,201 verra' generato, il suo hash sarà disponibile interrogando la testnet sulla console utilizzando il comando ```web3.eth.getBlock(1028201).hash```. Ad ogni modo, renderemo anche disponibile questo valore sul nostro blog, e così attraverso tutti i nostri [canali](https://www.facebook.com/ethereumproject) di [social](http://forum.ethereum.org/) [media](https://twitter.com/ethereumproject).

Sarà quindi in grado di generare il blocco Genesi eseguendo:

```
python mk_genesis_block.py --extradata hash_for_#1028201_goes_here > genesis_block.json
```

Da impostazione predefinita, lo script utilizza Blockr e Blockchain.info per recuperare i risultati della pre-vendita Genesis. È inoltre possibile aggiungere l'opzione ```--insight``` se invece preferite utilizzare il server privato di Ethereum per ottenere queste informazioni.

Anche se non forniremo il blocco Genesis in forma di file, pubblichero' invece l'hash del blocco Genesis (poco dopo averlo generato noi stessi), al fine di assicurare che files di terze parti invalidi o dannosi siano facilmente scartati dalla comunità.

Quando siete soddisfatti con la generazione del blocco Genesi, potete caricarlo sui client lanciando questo comando:

```
./build/bin/geth --genesis genesis_block.json
```

oppure:

```
./build/eth/eth --genesis genesis_block.json
```

Da quel punto, tutte le istruzioni sulla creazione di un account, importare il vostro portafoglio della pre-vendita, le transazioni, etc, possono essere reperite sulla guida 'Getting Started on Frontier' all'indirizzo web: http://guide.ethereum.org/

## Un altro paio di cose ...

Vorremmo anche dare un po 'di testa a testa sulla fase' disgelo '- il periodo durante il quale il limite di gas per blocco sarà impostato molto basso per consentire alla rete di crescere lentamente prima di transazioni possono avvenire. Si deve aspettare instabilità rete proprio all'inizio del rilascio, tra cui forcelle, potenziale esposizione anormale di informazioni sulla nostra http://stats.ethdev.com pagina e vari Peer to Peer problemi di connettività. Proprio come durante la fase olimpica, ci aspettiamo che questa instabilità di stabilirsi dopo un paio di ore / giorni.

Vorremmo anche ricordare a tutti che, mentre noi intendiamo fornire una piattaforma sicura nel lungo termine, Frontier è una versione tecnica rivolto ad un pubblico di sviluppatori, e non di un rilascio pubblico in generale. Si prega di tenere presente che il software precoce è spesso influenzata da bug, problemi con instabilità e interfacce utente complesse. Se si preferisce un più esperienza utente amichevole, ti consigliamo di aspettare il futuro Homestead o Metropolis Ethereum rilasci.

Si prega di essere particolarmente attenti a siti web di terze parti e software di origine sconosciuta - Ethereum sarà sempre e solo pubblicare il software attraverso la sua piattaforma github a https://github.com/ethereum/.

Infine, per chiarezza, è importante notare che il programma olimpico chiuso al blocco 1M di questa mattina, tuttavia, la generosità bug è ancora - e continuerà fino a nuovo avviso. Le vulnerabilità di sicurezza, se trovato, dovrebbero continuare ad essere segnalati https://bounty.ethdev.com/.

---
Aggiornamenti

27/07/15: istruzioni aggiuntive per gli utenti che eseguono l'aggiornamento da installazioni precedenti
