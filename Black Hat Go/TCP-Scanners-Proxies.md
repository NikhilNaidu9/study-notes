# CHAPTER 2: TCP, SCANNERS AND PROXIES

## Understanding the TCP handshake 
1. TCP stands for the Transmission Control Protocol
1. By the name we can understand that it control the transmission of data over the network 
1. Communication between devices over the internet takes place according to the TCP/IP suite which is taken from the OSI model
1. Application layer is at top most of the stack in the OSI model which contains the browser from which the client connects to the server.
1. Application layer then sends the data to the Transport layer
1. There are two protocols in this layer  
    1. UDP - User Datagram Protocol
    1. TCP - Transmission Control Protocol
1. TCP is more reliable than the UDP
1. TCP uses the Three-way Handshake method
    1. First the client sends the `syn` ( Synchronize Sequence Number ) to the server which signals the beginning of the communication
    1. When the server get the `syn` it send `syn-ack` ( Syn with Acknowledgement ) to the client in the acknowledgement of the `syn`
    1. Then at last the client sends the `ack` to the server in acknowledgement to the server's response
    1. After this three steps actual data can be transmitted
    1. [Flow Image of the process](https://media.geeksforgeeks.org/wp-content/uploads/handshake-1.png)
1. The above process is same for checking open ports in the server
1. If the server doesn't have any open ports it sends `rst` ( Reset ) to the client rather than `syn-ack`
1. If the traffic on server is filtered by a firewall there will be no response recieved by the client 

## Bypassing firewalls with Port Forwarding
1. Many of the firewalls does not allows to access some websites
1. This can be breached by using some intermediary system which will act as the proxy to the original site 
1. This intermediary system should be allowed on the firewall
1. This method is called port forwarding
1. In this method the client which is not able to access some website because of the firewall will connect to the intermediary website which is allowed on the firewall 
1. That interediary website will be configured to direct the traffic to the inteneded website
1. In this way the client can use the site indirectly by circumventing through the intermediary site
1. Using this way bypassing of firewall can be performed 