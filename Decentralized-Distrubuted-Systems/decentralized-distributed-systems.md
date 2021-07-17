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