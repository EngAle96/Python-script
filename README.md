# Python-script
I need help in a script python who represent a net routing.

Salve, sto lavorando ad uno script python a scopo didattico. 
Lo script implementa un grafo che rappresenta una piccola rete internet di 4 nodi(router) i nodi sono uniti da archi. 

Nodi e archi sono rappresentati con liste. 

Il mio obiettivo è ampliare questo script con una classe matrice che implementi una matrice quadrata pari al numero dei nodi della rete e i suoi elementi rappresentano le quantità di traffico scambiata dai percorsi end to end tra i nodi, successivamente devo aggiungere un metodo alla classe grafo che dia in output le quantita di traffico totali scambiate in ogni link del grafo. 

Per il calcolo dell'instradamento è presente un metodo dijkstra che calcola i percorsi a costo minimo, inoltre c'è un altro metodo che realizza la costruzione di tutti i percorsi per arrivare agli altri nodi a costo minimo partendo da un nodo sorgente. 

la classe che implementa la matrice suddetta sono riuscito a crearla, ma sono bloccato sul metodo che assegni le giuste quantita di traffico per ogni link che è coinvolto nei percorsi da uno dei 4 nodi sorgente. 

Non riesco a trovare un modo per mettere in collegamento gli elementi della matrice con i nodi che devono essere presi in considerazione in un dato percorso. 

Chi mi potrebbe dare aiuto nella realizzazione di questo metodo? 
Vi ringrazio anticipatamente. 

Ci sto lavorando da settimane e non riesco a trovare un modo. 

SONO DISPERATO.  :( 




Precisamente questo è quello che dovrei fare: 





Modificare lo script simulatore_rete.py 

fornito includendo un modello per il traffico scambiato tra i nodi. 

In particolare si richiede di creare un (o più) oggetto che rappresenti la Matrice di 

Traffico ( TM ) della rete. 




Una TM è una struttura dati in forma matriciale che descrive le relazioni di traffico 

esistenti tra i nodi di una rete. 

Tale matrice è quadrata, con dimensione N pari al 

numero di nodi che compongono la rete. 

L’indice di riga è in relazione con il nodo 

che genera la domanda di traffico (sorgente), mentre l’indice di colonna rappresenta 

il nodo ricevente (destinazione). 

Pertanto, il generico elemento t s,d della TM 

rappresenta la quantità di traffico inviata dalla sorgente s alla destinazione d . 

Dal momento che i nodi non scambiano traffico con se stessi, la diagonale di 

questa matrice risulta essere composta da soli 0 . 

Una volta definito l’oggetto TM in Python, è richiesta l’implementazione di una 

funzione che assegni in maniera automatica gli elementi della matrice.

SUGGERIMENTO: un tipico modello di traffico prevede l’estrazione casuale del 

valore della domanda di traffico in un intervallo finito. 

Una volta generato la TM si chiede ulteriormente di aggiungere un metodo alla 

classe Grafo che fornisca in output la quantità di traffico instradata su ciascun link 

della rete. Per il calcolo dell’instradamento deve essere utilizzato l’algoritmo di 

Dijkstra. 




I numeri rappresentano la quantità totale di traffico trasportata da ciascun 

link della rete, utilizzando l’instradamento Shortest Path calcolato con Dijkstra e 

avendo come input la TM mostrata in figura. 

Di seguito è spiegato come sono stati ottenuti i valori di traffico per i link della rete: 

Link A-B → t A,B + t A,C = 4 + 1 = 5 

Link B-C → t A,C + t B,C = 1 + 2 = 3 

Link C-B → t C,B + t C,A = 3 + 0 = 3 

Link B-A → t B,A + t C,A = 2 + 0 = 2 

Le equazioni scritte sopra sono diretta conseguenza del routing nella rete (cioè dei 

percorsi end to end seguiti dai flussi di traffico). 
