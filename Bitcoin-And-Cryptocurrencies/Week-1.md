## What is Bitcoin?
* The first and most widely used cryptocurrency.
    * completely digital, decentralized, currency built on principles of computer science
* Bitcoin: refers to the community, the network, and the software
* bitcoins: the currency itself, a unit
* Inspiration for the blockchain: the underlying data structure that stores a permanent history of all transactions to ever occur in the history of bitcoin 
* "Data Structure is a virtual format for organizing, retreiving and storing information".
* "It is an append-only ledger, meaning that any information added to the ledger cannot be deleted".
* "The cryptocurrency is not backed by any central organization, government or company".
* "Bitcoin is built by the users, for the users".
* Cypherphunks = a group of individual who advocate for the protection of privacy using cryptography 
* Bitcoin was created by Satoshi Nakamoto in 2009
* He created the first ever decentralized, psuedonymous and trustless system for transactions.
* "The bitcoin white paper was published in october 2008 by Satoshi Nakamoto"
* "Bitcoin takes control out of the hands of the parties and give users the freedom to transact while protecting their privacy"
---
## How does Bitcoin do it?
* On a high level, the Bitcoin network validated transactions and stores the entire transactions history.
* Bitcoin network is a group of users communicating with each other as part of the Bitcoin protocol. 
* This network serves as the substitute for the central bank and must have certain properties to function properly. 
* Bitcoin is trying to create an open, accessible cryptocurrency not subject to censorship or centralization
--- 
## What are the problems?
* There are no central parties to ask for information about user accounts and there are no central parties to kick out or censor malicious users. 
* The most popular attack is known as the double spending attack, an attack where some value is used for more than it's worth. 
* In digital currencies, there needs to be assurance that the virtual token have not be promised to more than one person.

* Bitcoin attempts to solve two problems that decentralized networks typically face:
    * Inconsistent transaction records held by different nodes 
    * Malicious pseudonymous actiors might broadcast false messages and divide the network
* Double spending attack: asynchronous records held by different nodes
* The blockchain and consensus protocol are the solution. 
* Bitcoin solves these problem through two things: First, the blockchain, and the Proof-of-Work consensus protocol, both of which are Satoshi Nakamoto's most popular and influential innovations. 
* Because of these two things, anyone with access to internet and a computer can joim the Bitcoin Network. 
* Everyone can verify and audit the transaction history on their own. 
* Even the creation of money is decided not by a central authority, but through the process of mining, of Proof-of-Work.
---
## Bitcoin VS. Banks 
* Banks
    * Account and Identity Management: Links personal information to bank account and verifies ownership 
    * Service: Transfers money and redeems money 
    * Record Management: Updates and tracks account balance 
    * Trust: Provides services by professionals under regulations of government 
* Bitcoin 
    * Account and Identity Management: Gives users autonomously created and manage identities. 
    * Service: Sends funds between peers directly
    * Record Management: Updates every node, which keeps its own ledger(blockchain)
    * Trust: Provides trusted protocol which incentivizes actors to behave honestly
* To store all the information, each Bitcoin user gets to possess their possess their individual copy of the ledger. 
* This decentralized approach of record keeping ensures the integrity of data despite the presence of faulty nodes who might record the information dishonestly. 
* This decentralized nature of bitcoin also prevents the risk of single point of failure
* In this event that a particular node is hacked in bitcoin, because everyone is a record keeper, the rest of the network can still ensure the integrity of the transaction record and keeps running.
---
## What is the role of identity in the context of currencies? 
* Authentication 
    * Receiving money
    * Claiming / Spending money
    * Blame 
* Integrity 
* Identity in daily life
    * Houses have addresses and mailbox keys.
    * Emails have aliases and passwords.
    * Bitcoin has public keys and private keys. 
* Anology:
    * Private key: physical key
    * Public key: locked chest
* Public key for receiving private key for redeeming 
    * Private key chosen at random 
    * Public key generated from private 
Note: public key =/= address in reality we'll make the distinction clear in later sections.

* Probability of two users choosing the same identity as someone else 
* Bitcoin has two to the one sixty different possible addresses 
* Earth has 2 ^ 63 grains of sand 
* Imagine every person in the world choosing a grain sand at random. Likehood of two people picking the same grain of sand is less than 0.0001%.
* Bitcoin is hidden in the large amount of public keys
    * 2 ^ 160 (1,461,501,637,330,902,918,203,684,832,716,283,019,655,932,542,97) possible addresses.
* Practically impossible for anyone to overlap using random number generation of public key
        * For reference:
            * Grains of sand on earth: 2 ^ 63
            * With 2 ^ 63 earths, each with 2 ^ 63 grains of sand: 2 ^ 126 grains of sand. 
* Population of world: 7.5 billion in April 2017
    * Every person could have about 2 ^ 127 addresses all to themselves. 
---