# Notes
## Notes gathered from IPFS homepage [IPFS](ipfs.io)
1. It is a peer-to-peer hypermedia protocol 
1. It is optimized for delivery media
1. HTTP is a hypertext protocol which is intended to deliver text like websites 

---
## Notes gathered from the whitepaper 
[IPFS Whitepaper](https://arxiv.org/pdf/1407.3561.pdf)

### Introduction
1. There were many attempts make distributed file system 
1. Some were successfull and more some were failed
1. In academia, AFS got successfull 
1. AFS is used in a very big scale- For e.g. One enterprise AFS deployment at Morgan Stanley exceeds 25,000 clients
1. Other successfull implementations were Napster, KaZaa and BitTorrent
1. BitTorrent is supporting 100 million simultaneous users
1. BitTorrent has a massive deployment where tens of millions of nodes churn daily 
1. There were no general file-system that offers global, low-latency and decentralized distribution 
1. HTTP is the most successful "distributed system of files" ever deployed
1. It has become the de facto way to transmit files over internet 
1. But it fails to take advantage of dozens of brilliant file distribution techniques which has been developed in last 15 years 
1. From one perspective, evolving web infrastructure is nearly impossible because of the back compatibility constraints and the number of strong parties invested in the current model
1. What is lacking is upgrading design: enhancing the current HTTP web, and introducing the new functionality without degrading user experience
1. Industries has gotten away by using HTTP this long because moving small files around is relatively cheap, even for small organizations with lots of traffic 
1. We are entering a new era of data distribution with new challenges
    1. Hosting and distributing petabytes dataset
    1. Computing on large data across organisations 
    1. High-volume High-defination on-demanjd or real-time media streams
    1. Versioning and linking of massive datasets
    1. Preventing accidental disappearance of important files and more
1. Everything can be summarized to one line "lots of data, accessible everywhere"
1. Because of critical features and bandwidth concerns, we have given up HTTP for different protocols
1. Parallel to efficient data distribution, version control systems have managed to develop important data collaboration workflows
1. Git, the distributed source code verison control system, developed many useful ways to model and implement distributed data systems
1. Git provides with versioning functionality that large file systems severely lack 
1. New solutions inspired by Git are emerging, such as Camlistore and Dat
1. Git has already influenced distributed filesystem design, as its content addressed Merke DAG data model enables powerful file distribution strategies 
1. What is remaining to explore is to explore how this data structure can influence the design of high-throughput-oriented file systems, how it might upgrade to Web itself
1. The central IPFS principle is modeling *all data* as part of the same Merkle DAG

### Background
* This section reviews important properties of successful peer-to-peer systems which IPFS combines
1. Distributed Hash Tables 
    * DHTs are widely used to coordinate and maintain metadata about peer-to-peer systems 
    * For e.g. the BitTorrent MainlineDHT tracks sets of peers part of a torrent swarm 
    1. Kademlia DHT 
        1. Efficient lookup through massive networks: queries onaverage contact ⌈log2(n)⌉ nodes. (e.g. 20 hops for a network of 10,000,000 nodes)
        1. Low coordination overhead: it optimizes the number of control messages it sends to other nodes
        1. Resistance to various attacks by preferring long-lived nodes
        1. Wide usage in peer-to-peer applications, including Gnutella and BitTorrent forming networks of over 20 million nodes
    1. Coral DSHT
        *While some peer-to-peer filesystems store data blocks directly in DHTs, this “wastes storage and bandwidth, as data must be stored at nodes where it is not needed”
        1. Kademlia stores values in nodes whose ids are “nearest”
        (using XOR-distance) to the key. This does not take into account application data locality, ignores “far” nodes that may already have the data, and forces “nearest” nodes to store it, whether they need it or not This wastes significant storage and bandwith. Instead, Coral stores addresses to peers who can provide the data blocks.
        1. Coral relaxes the DHT API from get_value(key) to get_any_values(key) (the “sloppy” in DSHT). This still works since Coral users only need a single (working) peer, not the complete list. In return, Coral can distribute only subsets of the values to the “nearest” nodes, avoiding hot-spots (overloading all the nearest nodes when a key becomes popular).
        1. Additionally, Coral organizes a hierarchy of separate DSHTs called clusters depending on region and size. This enables nodes to query peers in their region first, “finding nearby data without querying distant nodes” and greatly reducing the latency of lookups. 
    1. S/Kademlia DHT 
        * S/Kademlia extends Kademlia to protect against malicious attacks in two particularly important ways:
        1. S/Kademlia provides schemes to secure NodeId generation, and prevent Sybill attacks. It requires nodes to create a PKI key pair, derive their identity from it,
        and sign their messages to each other. One scheme includes a proof-of-work crypto puzzle to make generating Sybills expensive.
        1. S/Kademlia nodes lookup values over disjoint paths, in order to ensure honest nodes can connect to each other in the presence of a large fraction of adversaries
        in the network. S/Kademlia achieves a success rate of 0.85 even with an adversarial fraction as large as halfof the nodes

1. Block Exchanges - BitTorrent
    * BitTorrent is a widely successful peer-to-peer filesharing system, which succeeds in coordinating networks of untrusting peers (swarms) to cooperate in distributing pieces of files to each other
    1.  BitTorrent’s data exchange protocol uses a quasi titfor-tat strategy that rewards nodes who contribute to each other, and punishes nodes who only leech others’ resources
    1. BitTorrent peers track the availability of file pieces, prioritizing sending rarest pieces first. This takes load off seeds, making non-seed peers capable of trading with each other
    1. BitTorrent’s standard tit-for-tat is vulnerable to some exploitative bandwidth sharing strategies. PropShare is a different peer bandwidth allocation strategy that better resists exploitative strategies, and improves the performance of swarms

1. Version Control Systems - Git
    * Version Control Systems provide facilities to model files changing over time and distribute different versions efficiently.The popular version control system Git provides a powerful Merkle DAG object model that captures changes to a filesystem tree in a distributed-friendly way
    1. Immutable objects represent Files (blob), Directories (tree), and Changes (commit)
    1. Objects are content-addressed, by the cryptographic hash of their contents
    1. Links to other objects are embedded, forming a Merkle DAG. This provides many useful integrity and workflow properties
    1. Most versioning metadata (branches, tags, etc.) are simply pointer references, and thus inexpensive to create and update
    1. Version changes only update references or add objects
    1. Distributing version changes to other users is simply transferring objects and updating remote references

1. Self-Certified Filesytstems - SFS
    1. SFS proposed compelling implementations of both 
        1. distributed trust chains
        1. egalitarian shared global namespaces 
    1. SFS introduced a technique for building SelfCertified Filesystems: addressing remote filesystems using the following scheme 
    ```
    /sfs/<Location>:<HostID>
    ``` 
    where Location is the server network address, and 
    ```
    HostID = hash(public_key || Location)
    ```
    1. Thus the name of an SFS file system certifies its server
    1. The user can verify the public key offered by the server, negotiate a shared secret, and secure all traffic
    1.  All SFS instances share a global namespace where name allocation is cryptographic, not gated by any centralized body

### IPFS Design 
1. IPFS is peer-to-peer, no nodes are priviledged
1. IPFS nodes store IPFS objects in local storage 
1. Nodes connect to each other and trasfer objects
1. These objects represent files and data structures 
1. The IPFS protocol is divided into stack of sub-protocols responsible for different functionality
    1. Identities - manage node indentity generation and verification
    1. Network - manages connection to other peers, uses various underlying network protocols 
    1. Routing - maintains information to locate specific peers and objects. Responds to both local and remote queries. Defaults to a DHT, but is swappable 
    1. Exchange - a novel block exchange protocol ( BitSwap ) that governs efficient block distribution. Modelled as a market, weakly incentivizes data replication. Trade strategies swappable
    1. Objects - a Merkle DAG of content addressed immutable objects with link. Used to represent arbitrary datastructures, e.g. file hierarchies and communication systems 
    1. Files - versioned file system heirarchy inspired by Git
    1. Naming - A self-certifying mutable name system
1. These subsystems are not independent, they are integrated and leverage blended properties

#### Identites
1. Nodes are identified by a `NodeId`, the cryptographic hash of a public-key, created with S/Kademlia’s static crypto puzzle
1. Nodes are identified by a NodeId, the cryptographic hash of a public-key, created with S/Kademlia’s static crypto puzzle
1.  Users are free to instatiate a “new” node identity on every launch, though that loses accrued network benefits. Nodes are incentivized to remain the same.
```
type NodeId Multihash
type Multihash []byte

// self-describing cryptographic hash digest
type PublicKey []byte

type PrivateKey []byte
// self-describing keys

type Node struct {
NodeId NodeID
PubKey PublicKey
PriKey PrivateKey
}
```
1. S/Kademlia based IPFS identity generation
```
difficulty = <integer parameter>
n = Node{}
do {
n.PubKey, n.PrivKey = PKI.genKeyPair()
n.NodeId = hash(hash(n.PubKey))
p = count_preceding_zero_bits(n.NodeId)
} while (p < difficulty)
```
1. Upon first connecting, peers exchange public keys, and check: hash(other.PublicKey) equals other.NodeId. If not, the connection is terminated.
1. *Note on Cryptographic Functions*
    1. Rather than locking the system to a particular set of function choices, IPFS favors self-describing values.
    1. Hash digest values are stored in multihash format, which includes a short header specifying the hash function used, and the digest length in bytes. Example:
    ```
    <function code><digest length><digest bytes>
    ```
    1. This allows the system to 
        1. choose the best function for the use case (e.g. stronger security vs faster performance)
        1. evolve as function choices change. 
    1. Self-describing values allow using different parameter choices compatibly.

#### Network 
1. IPFS nodes communicate regualarly with hundreds of other nodes in the network, potentially across the wide internet.
1. The IPFS network stack features:
    1. Transport: IPFS can use any transport protocol, and is best suited for WebRTC DataChannels (for browser connectivity) or uTP(LEDBAT).
    1. Reliability: IPFS can provide reliability if underlying networks do not provide it, using uTP (LEDBAT) or SCTP.
    1. Connectivity: IPFS also uses the ICE NAT traversal techniques.
    1. Integrity: optionally checks integrity of messages using a hash checksum.
    1. Authenticity: optionally checks authenticity of messages using HMAC with sender’s public key.
1. *Note on Peer Addressing*
    1. IPFS can use any network; it does not rely on or assume access to IP.
    1. This allows IPFS to be used in overlay networks.
    1. IPFS stores addresses as `multiaddr` formatted byte strings for the underlying network to use.
    1. `multiaddr` provides a way to express addresses and their protocols, including support for encapsulation. For example:
    ```
    # an SCTP/IPv4 connection
    /ip4/10.20.30.40/sctp/1234/
    # an SCTP/IPv4 connection proxied over TCP/IPv4
    /ip4/5.6.7.8/tcp/5678/ip4/1.2.3.4/sctp/1234/
    ```

#### Routing
1. IPFS nodes require a routing system that can find 
    1. other peers’ network addresses
    1. peers who can serve particular objects
1.  The size of objects and use patterns of IPFS are similar to Coral and Mainline, so the IPFS DHT makes a distinction for values stored based on their size.
1. Small values (equal to or less than 1KB) are stored directly on the DHT.
1. For values larger, the DHT stores references, which are the `NodeIds` of peers who can serve the block.
1. The interface of this DSHT is the following:
```
type IPFSRouting interface {
FindPeer(node NodeId)
// gets a particular peer’s network address

SetValue(key []bytes, value []bytes)
// stores a small metadata value in DHT

GetValue(key []bytes)
// retrieves small metadata value from DHT

ProvideValue(key Multihash)
// announces this node can serve a large value

FindValuePeers(key Multihash, min int)
// gets a number of peers serving a large value
}
```
1. Note: different use cases will call for substantially different routing systems (e.g. DHT in wide network, static HT in local network).
1. Thus the IPFS routing system can be swapped for one that fits users’ needs. As long as the interface above is met, the rest of the system will continue to function.

### Topics to be researched more 
1. [Andrew File System](https://en.wikipedia.org/wiki/Andrew_File_System)
1. [Kerberos](https://en.wikipedia.org/wiki/Kerberos_(protocol))
1. [Napster](https://en.wikipedia.org/wiki/Napster)
1. [KaZaa](https://en.wikipedia.org/wiki/Kazaa)
1. [BitTorrent](https://en.wikipedia.org/wiki/BitTorrent)
1. [Git](https://en.wikipedia.org/wiki/Git) 
1. [Camlistore](https://en.wikipedia.org/wiki/Perkeep)
1. [Dat](https://en.wikipedia.org/wiki/Dat_(software))
1. [Kademlia](https://en.wikipedia.org/wiki/Kademlia)
1. [Mainline DHT](https://en.wikipedia.org/wiki/Mainline_DHT)
1. [Coral Content Distribution Network](https://en.wikipedia.org/wiki/Coral_Content_Distribution_Network)
1. [Sybil attack](https://en.wikipedia.org/wiki/Sybil_attack)
1. [Self-certifying File System](https://en.wikipedia.org/wiki/Self-certifying_File_System)
1. [Public-key cryptography (PKI)](https://en.wikipedia.org/wiki/Public-key_cryptography)
1. [Micro Transport Protocol (uTP)](https://en.wikipedia.org/wiki/Micro_Transport_Protocol)
1. [LEDBAT](https://en.wikipedia.org/wiki/LEDBAT)
1. [Stream Control Transmission Protocol](https://en.wikipedia.org/wiki/Stream_Control_Transmission_Protocol)
1. [Interactive Connectivity Establishment](https://en.wikipedia.org/wiki/Interactive_Connectivity_Establishment)
1. [Network address translation](https://en.wikipedia.org/wiki/Network_address_translation)
1. [HMAC](https://en.wikipedia.org/wiki/HMAC)