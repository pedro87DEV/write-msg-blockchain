![logo_PEDRO](./images/PEDRO.png)


# > PROCESSO PER SALVATAGGIO DI UN MESSAGGIO SULLA BLOCKCHAIN


## 1	Introduzione
Questo progetto prevede la scrittura di un determinato messaggio dato in input sulla Blockchain.
 

## 2	Come funziona?

Il servizio non scrive sulla blockchain i tuoi dati in chiaro, bensì in forma offuscata e aggregata, in modo da non rendere possibile risalire al dato originale. Il dato scritto in blockchain è chiamato Merkle Root ed è il risultato di un processo di aggregazione noto con il nome Merkle Tree.

#### Cos’è il Merkle Tree?  

In letteratura informatica, un hash tree o merkle tree è una struttura ad albero le cui foglie rappresentano blocchi di dati sotto forma di hash, una funzione non invertibile che mappa una stringa di lunghezza arbitraria in una stringa di lunghezza minore. La caratteristica principale del merkle tree è di permettere una verifica efficiente e sicura di strutture dati di grandi dimensioni.
Dimostrare l’appartenenza di una data foglia (dato di input) ad un merkle tree necessita infatti un numero di computazioni proporzionale al logaritmo del numero delle foglie di quel determinato merkle tree.

![img_merkletree](./images/Hash_Tree.png)    
Figura 0- Schema Merkle Tree

# > OP_RETURN AND DATA IN THE BLOCKCHAIN

On OP_RETURN: There was been some confusion and misunderstanding in the community, regarding the OP_RETURN feature in 0.9 and data in the blockchain. This change is not an endorsement of storing data in the blockchain. The OP_RETURN change creates a provably-prunable output, to avoid data storage schemes – some of which were already deployed – that were storing arbitrary data such as images as forever-unspendable TX outputs, bloating bitcoin’s UTXO database.

Storing arbitrary data in the blockchain is still a bad idea; it is less costly and far more efficient to store non-currency data elsewhere.


# > UTILIZZO DI OP_RETURNs IN PYTHON

Simple Python commands and libraries for using OP_RETURNs in bitcoin transactions.

Copyright (c) Coin Sciences Ltd - http://coinsecrets.org/
MIT License (see headers in files)

**REQUIREMENTS**
* Python 2.5 or later (including Python 3)
* Bitcoin Core 0.9 or later

**BEFORE YOU START**
Check the constant settings at the top of OP_RETURN.py.
If you just installed Bitcoin Core, wait for it to download and verify old blocks.
If using as a library, add 'from OP_RETURN import *' in your Python script file.


**TO STORE SOME DATA IN THE BLOCKCHAIN USING OP_RETURNs**

On the command line:

* python store-OP_RETURN.py <data> <testnet (optional)>

  <data> is a hex string or raw string containing the data to be stored
         (auto-detection: treated as a hex string if it is a valid one)
  <testnet> should be 1 to use the bitcoin testnet, otherwise it can be omitted

* Outputs an error if one occurred or if successful, the txids that were used to store
  the data and a short reference that can be used to retrieve it using this library.

* Wait a few seconds then check http://coinsecrets.org/ for your OP_RETURN transactions.

* Examples:

  python store-OP_RETURN.py 'This example stores 47 bytes in the blockchain.'
  python store-OP_RETURN.py 'This example stores 44 bytes in the testnet.' 1
  
  
As a library:

* OP_RETURN_store(data, testnet=False)

  data is the string of raw bytes to be stored
  testnet is whether to use the bitcoin testnet network (False if omitted)
  
* Returns: {'error': '<some error string>'}
       or: {'txids': ['<1st txid>', '<2nd txid>', ...],
            'ref': '<ref for retrieving data>'}
           
* Examples:

  OP_RETURN_store('This example stores 47 bytes in the blockchain.')
  OP_RETURN_store('This example stores 44 bytes in the testnet.', True)
  



