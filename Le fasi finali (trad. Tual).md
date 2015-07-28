# Le fasi finali

Un aggiornamento come promesso: tutti i sistemi sono ora “pronti” sul lato tecnico e abbiamo intenzione di rilasciare Frontier questa settimana.

Grazie a tutti coloro che hanno dato feedback sul mio precedente post. Che ne è stato evidente è che prima del grande giorno, molti di voi hanno voluto sapere di più su ciò che la sequenza degli eventi sarebbe esattamente, e come preparare la macchina per il rilascio.

## Un rilascio aperto e trasparente 

Gli utenti di Frontier dovranno innanzitutto generare, e poi caricare sul loro client Ethereum il blocco Genesis. Il blocco Genesis rappresenta un file di database: contiene tutte le transazioni che derivano dalla pre-vendita di Ether, e quando un utente carica questo file sul client, prende la decisione di aderire alla rete sotto i suoi termini: è un primo passo verso il consenso.

Poiche’ la pre-vendita di Ether si è svolta interamente sulla blockchain di Bitcoin, i suoi contenuti sono pubblici, e chiunque può generare e verificare il blocco Genesis. Nell'interesse del decentramento e della trasparenza, Ethereum non fornirà il blocco Genesis come file da scaricare, ma ha invece creato uno script open source che chiunque può utilizzare per generare il file, il cui link si trova più avanti in questo articolo.

Dal momento che lo script è già disponibile ed il rilascio deve essere coordinato, lo script contiene un argomento che prevede il lancio di Frontier _all'unisono_. Ma come e' possibile far cio' ***_e_*** rimanere decentralizzati?

L'argomento deve essere un parametro casuale che nessuno, noi anche, in grado di prevedere. Come potete immaginare, non ci sono troppi parametri nel mondo che corrispondono a questo criterio, ma una buona è l'hash di un futuro blocco sul testnet Ethereum. Abbiamo dovuto prendere un numero di blocco, ma quale? 1.028.201 risulta essere sia primo e palindromo, proprio come ci piace. Così # 1028201 è.

Sequenza di passi al rilascio:

    Passaggi finali per il rilascio rivelato: stai leggendo questo ora.
    Block # 1028201 si forma sulla Tesnet Ethereum, e viene dato un hash.
    L'hash viene utilizzato dagli utenti di tutto il mondo come un parametro unico per lo script di generazione blocco Genesi.

Che potete fare ad oggi

In primo luogo, è necessario installare il client. Userò Geth come esempio, ma lo stesso risultato può essere ottenuto con Eth (l’implementazione C ++ di Ethereum). Le istruzioni per l'installazione di Geth su Windows, Linux e OSX si possono trovare sulla nostra wiki.

Dopo aver installato un client, è necessario scaricare lo script python che genera il file Genesi. Si chiama 'mk_genesis_block.py', e può essere scaricato qui.

A seconda della piattaforma, è possibile anche scaricarlo dalla console con l'installazione di curl e in esecuzione;

'''
curl -O https://raw.githubusercontent.com/ethereum/genesis_block_generator/master/mk_genesis_block.py
'''

Questo creerà il file nella stessa cartella in cui avete lanciato il comando. A questo punto è necessario installare i pybitcointools creati dalla nostra stessa Vitalik Buterin. È possibile ottenere questo attraverso il gestore pip pacchetto python, così ti installare pip prima, poi gli strumenti subito dopo.

Le seguenti istruzioni dovrebbero lavorare su OSX e Linux. Gli utenti di Windows, una buona notizia, navi pip con il programma di installazione standard di Python.

ricciolo -O https://bootstrap.pypa.io/get-pip.py
sudo python get-pip.py

sudo pip install bitcoin

o (se avete avuto già installato),

sudo pip install bitcoin --upgrade

Un ultimo passo, se si utilizza Eth, abbiamo recentemente di supportare il nuovo parametro blocco Genesi, quindi avrai bisogno di prendere la corretta versione del software per essere pronti per il grande giorno:

cd ~ / costruisce / go-Ethereum /
rilascio git checkout / 1.0.0
tiro git
fare Geth

Coloro che vorrebbero essere 'pronto come possibile' in grado di seguire le istruzioni fino a questo punto, che ha detto, un git tirare appena prima che il blocco fatidico è probabilmente consigliabile utilizzare la versione più recente di qualsiasi software.

Se siete stati in esecuzione i clienti prima di:

    Eseguire il backup dei tasti (forse alcuni di loro sono ammissibili per i premi olimpici) - si trovano in ./ethereum/keystore
    Elimina la tua vecchia catena prego (si trova a ./ethereum, eliminare le seguenti 3 cartelle solo: ./extra, ./state, ./blockchain)
    Si può tranquillamente lasciare l'./ethereum/nodes, ./ethereum/history e ./ethereum/nodekey a posto
    DAG Avere pregenerato in ./ethash non farà male, ma sentitevi liberi di cancellarli se avete bisogno di spazio

Per una ripartizione completa di dove si trovano i file di configurazione, si prega di consultare questa pagina sul nostro forum.

Poi, è una questione di attesa per il blocco # 1028201, che all'epoca corrente risoluzione blocco, dovrebbe essere formato circa Giovedi sera GMT + 0.

Una volta che si è formata 1028201, il suo hash sarà accessibile interrogando il testnet alla console utilizzando web3.eth.getBlock (1.028.201) .hash, tuttavia abbiamo anche rendere tale valore disponibile su questo blog, così come tutti i nostri canali di social media.

Sarà quindi in grado di generare il blocco Genesi eseguendo:

pitone mk_genesis_block.py --extradata hash_for_ # 1028201_goes_here> genesis_block.json

Per impostazione predefinita, lo script utilizza Blockr e Blockchain.info per recuperare i Genesis risultati di pre-vendita. È inoltre possibile aggiungere l'opzione --insight se vuoi invece preferisce utilizzare il server Ethereum privato per ottenere queste informazioni.

Anche se non ci fornirà il blocco Genesi come un file, avremo ancora fornire il blocco hash Genesi (poco dopo che generiamo noi stessi), al fine di assicurare che i terzi file non validi o dannosi sono facilmente scartati dalla comunità.

Quando si è soddisfatti con la generazione del blocco Genesi, è possibile caricarlo nei clienti che utilizzano questo comando:

./build/bin/geth --genesis genesis_block.json

oppure:

./build/eth/eth --genesis genesis_block.json

Da lì, istruzioni sulla creazione di un account, importare il vostro pre-vendita portafogli, transazioni, ecc, può essere trovato sulla guida 'Getting Started' Frontier in http://guide.ethereum.org/
Un altro paio di cose ...

Vorremmo anche dare un po 'di testa a testa sulla fase' disgelo '- il periodo durante il quale il limite di gas per blocco sarà impostato molto basso per consentire alla rete di crescere lentamente prima di transazioni possono avvenire. Si deve aspettare instabilità rete proprio all'inizio del rilascio, tra cui forcelle, potenziale esposizione anormale di informazioni sulla nostra http://stats.ethdev.com pagina e vari Peer to Peer problemi di connettività. Proprio come durante la fase olimpica, ci aspettiamo che questa instabilità di stabilirsi dopo un paio di ore / giorni.

Vorremmo anche ricordare a tutti che, mentre noi intendiamo fornire una piattaforma sicura nel lungo termine, Frontier è una versione tecnica rivolto ad un pubblico di sviluppatori, e non di un rilascio pubblico in generale. Si prega di tenere presente che il software precoce è spesso influenzata da bug, problemi con instabilità e interfacce utente complesse. Se si preferisce un più esperienza utente amichevole, ti consigliamo di aspettare il futuro Homestead o Metropolis Ethereum rilasci.

Si prega di essere particolarmente attenti a siti web di terze parti e software di origine sconosciuta - Ethereum sarà sempre e solo pubblicare il software attraverso la sua piattaforma github a https://github.com/ethereum/.

Infine, per chiarezza, è importante notare che il programma olimpico chiuso al blocco 1M di questa mattina, tuttavia, la generosità bug è ancora - e continuerà fino a nuovo avviso. Le vulnerabilità di sicurezza, se trovato, dovrebbero continuare ad essere segnalati https://bounty.ethdev.com/.

-
Aggiornamenti

27/07/15: istruzioni aggiuntive per gli utenti l'aggiornamento da precedenti installazioni
