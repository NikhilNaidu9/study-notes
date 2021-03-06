# Notes 
1. Distributed systems are mostly in the same network like in the same data center connected through ethernet cables
1. There are people maintaining them or replacing them when necessary which brings the notion of great reliability into systems 
1. In decentralized manner of the same there are no such reliability 
1. There are some important steps which is need distributed systems 
    1. Discovery
        * Discovering the entities in the network i.e check for the required elements to be online 
        * We perform this step by pinging to the elements of the network 
        * We have to do recursively in a particular timeframe 
        * It's called a HeartBeat message 
        * Aim 
            1. What are we aiming for is to have a direct peer-to-peer connection to all the element without going through centralized intermediary 
            1. This can be achieved by using WebRTC 
            1. This is not full-and-final 
            1. This is just a idea of the limited knowledge we have in the moment 
        * Implemention 
            1. We will have a server in the cloud which everyone will connect at first
            1. That server will be responsible for sending out the information related to nearby elements of the network 
            1. This is a very bad implementation because it introduces centralization in the process which is very bad  
            1. What is the server on the cloud gets offline or gets hacked 
            1. And the bigger question is who will be responsible for that cloud              
    1. Storage
        * Blockchain 
        * Compression
            1. File compression which will reduce network bandwidth 
        * Need to store user files 
        * Files can be of any type 
    1. Fault Tolerance 
        * Data Replication 
            1. We have to do 3 or more times of data replication
            1. Replication as a whole or replication as chunks 
            1. Replication as chunks is more performing 
        * Why?
            1. If some node fails we will be able to access the data from another node 
            1. User should be able to access data anytime 
    1. Consistency & Integrity 
        * Data should be consistent in all the nodes
        * All the replication nodes of the same context should have same data  
    1. Security
        * Encryption & Decryption 
        * Payment Gateway  
1. There will no one or two entites 
1. There will many entites working their own 
1. Entities will be like a bank which will be responsible to handing out money which is mining in this case 
1. One entity is a user who will opt for stroing file for they will pay
1. One entity will be a storage node who's only responsibilty is to store user file for which they will incentivized
1. One entity will the record keeping entity which will keep the records of the all the entities either online or offline 
1. Layers decided till now ( will change later ) (Lower to Upper)
    1. Application 
    1. Storage 
    1. Blockchain
    1. Network 

---
## Development Plan 
### Blockchain 
1. Installation
    1. Install script 
    1. Program configuration file   
1. Develop a network 
    1. Testnet and Mainnet
    1. Discoving for peers
    1. Maximum number of connections 
1. Authentication 
    1. Generate Identity 
    1. Wallet
1. Syncing 
    1. Continously fetch block headers 
    1. Drop unsync nodes as connections 
    1. Caching important content of the chain 
1. Ledger
    1. Implementation of Genesis Block
    1. Implementation of Chain Config 
    1. Add the block header to the chain 
1. Security 
    1. Hashing Functions 
    1. Key generation tool 
1. Performance Enchancement 
    1. Change cache limit values 
1. Logging and Debugging
    1. Log all the actions taking place in the network 
1. Metrics and Stats  
    1. Total Transactions 
    1. Block Time
    1. Number of Nodes

### File Storage
1. Installation
    1. Install script 
    1. Program configuration file   
1. Develop a network 
    1. Testnet and Mainnet
    1. Discoving for peers
    1. Maximum number of connections 
1. Authentication 
    1. Generate Identity 
    1. Wallet
1. Security 
    1. Hashing Functions 
    1. Key generation tool 
1. Performance Enchancement 
    1. Change cache limit values 
1. Logging and Debugging
    1. Log all the actions taking place in the network 
1. Metrics and Stats 
    1. Total Storage  
    1. Number of Nodes

### Social Network 
1. Develop a network 

---
## Panel Selection Presentation Notes 
1. What is our project?
    1. Decentralized and distributed way of storing files and using the same for other applications 
1. Why this project? ( Motivation )
    1. We need a core research project even though this core is not our real core which is the hardware 
    1. But if we see in the software domain, this is as far as we can go in the core 
    1. We didn't wanted to do something which is already done in the academia and as well as in industry like making apps, websites or something else 
1. What are the domains used in this project?
    1. Blockchain
    1. Cryptography
    1. Distributed Systems
    1. Networking
    1. Compression
    1. Security
1. Why this project? ( Technical )
    1. Disadvantages of the present internet
        1. Centralization
            1. The Internet has turbocharged innovation by being one of the great equalizers in human history ??? but increasing consolidation of control threatens that progress.
            1. Varanasi Story of Google getting shutdown or disappearing 
            1. Internet Shutdown - Google Example
        1. Hacking
        1. Dark Web 
        1. Error 404 Not Found
            1. The average lifespan of a web page is 100 days
        1. Censorship 
1. We need something new 
1. What is Blockchain?
    1. The underlying data structures that stores a permanent history of all transactions to even occur in history of blockchain
    1. Data structure is a virtual format for organizing retrieving and storing information
    1. CRUD explanation
    1. It will be an append only ledger, meaning that any information added to the ledger can  not be deleted
1. Most contributing factor of blockchain
    1. Decentralization is the process of distributing and dispersing power away from a central authority
    1. Most financial and governmental systems, which are currently in existence, are centralized
    1. There is a single highest authority in charge of managing them, such as a central bank or state apparatus
1. How it is going to be used in our project?
    1. Record keeping
    1. Cryptocurrency 
        1. Incentivizing the actors in the network 
1. [Let's see how everything works](https://andersbrownworth.com/blockchain/) 
1. Reasons why big companies not adopting blockchain
    1. Ad revenue 
1. Finance Model 
    1. Finance 101 
        1. How something is valuable? 
    1. America's note printing machine example
    1. Miner -> Exchange -> User Nodes -> Storage Nodes -> Exchange
1. What do we want to become? 
1. Future Implementation 

---
# Papers to go through 
## File System
1. IPFS - Content Addressed, Versioned, P2P File System  
https://arxiv.org/pdf/1407.3561.pdf 
1. Filecoin: A Decentralized Storage Network  
https://filecoin.io/filecoin.pdf
1. The Google File System  
https://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf
1. Cassandra - A Decentralized Structured Storage System  
https://www.cs.cornell.edu/projects/ladis2009/papers/lakshman-ladis2009.pdf
1. Theta Mainnet 3.0 Whitepaper  
https://s3.us-east-2.amazonaws.com/assets.thetatoken.org/Theta-white-paper-3-0-latest.pdf
1. BitTorrent (BTT) White Paper
https://www.bittorrent.com/btt/btt-docs/BitTorrent_(BTT)_White_Paper_v0.8.7_Feb_2019.pdf

## Blockchain
1. Ethereum Whitepaper  
https://ethereum.org/en/whitepaper/
1. Solana: A new architecture for a high
performance blockchain v0.8.13  
https://solana.com/solana-whitepaper.pdf