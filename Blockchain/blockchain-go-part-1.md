# Building Blockchain in Go. Part 1: Basic Prototype  
[Article Link](https://jeiwan.net/posts/building-blockchain-in-go-part-1/)

## Introduction 
1. Blockchain is the distributed database of records 
1. What makes it unique is that it's not a private database, but a public one,i.e everyone who uses it has a full or partial copy of it
1. New record can only be added with the consent of other keepers of the database
1. Blockchain made cryptocurrency and smart contracts possible 

## Block 
1. In blockchain it's block that stores valuable information 
1. Bitcoin blocks store transaction, the essence of any crytocurrency 
1. Block also contains some technical information like its version, current timestamp and the hash of the previous block 
``` 
type Block struct {
        Timestamp     int64
        Data          []byte
        PrevBlockHash []byte
        Hash          []byte
}
```
1. `Timestamp` is the current timestamp( when the block is created )
1. `Data` is the actual valuable information containing in the block
1. `PrevHashBlock` stores the hash of the previous block 
1. `Hash` is the hash of the block
1. In Bitcoin specification `Timestamp`, `PrevBlockHash`, and `Hash` are block headers, which form a separate datastructure, and transaction( `Data` in our case ) forms a different data structure 
1. We are mixing them for simplicity
1. The question that arises now is *How the hashes are calculated?*
1. The way hashes are calculated is very important feature of blockchain, and it's this feature that makes blockchain secure
1. The thing is that calcualting a hash is a computationally difficult operation, it takes some time even on fast computers( that's why people buy powerful GPU's to mine Bitcoin )
1. This is an intentional architectural design, which makes adding new blocks difficult, thus preventing their modification after they're added
1. For now, we'll just take block fields, concatenate them, and calculate a SHA-256 hash on the concatenated combination
```
func (b *Block) SetHash() {
	timestamp := []byte(strconv.FormatInt(b.Timestamp, 10))
	headers := bytes.Join([][]byte{b.PrevBlockHash, b.Data, timestamp}, []byte{})
	hash := sha256.Sum256(headers)

	b.Hash = hash[:]
}
```
1. Following the Golang convention, we'll implement a function that'll simplify the creation of a block
```
func NewBlock(data string, prevBlockHash []byte) *Block {
	block := &Block{time.Now().Unix(), []byte(data), prevBlockHash, []byte{}}
	block.SetHash()
	return block
}
```
## Blockchain 
1. Blockchain is just a database with certain structure: it's an ordered, back-linked list
1. Blocks are stored in the insertion order and that each block is linked to the previous one 
1. This structure allows to quickly get the latest block in a chain and to ( efficiently ) get a block by its hash 
1. In Golang this structure can be implemented by using a array and a map
1. The array would keep ordered hashes( arrays are ordered in Go ), and the map would keep `hash -> keep` pairs ( maps are unordered )
1. But for our blockchain prototype we'll just use an array, because we don't need to get blocks by their hash for now 
```
type Blockchain struct {
        blocks []*Block
}
```
1. This is our first blockchain!
1. Now let's make it possible to add blocks to it 
```
func (bc *Blockchain) AddBlock(data string) {
        prevBlock := bc.blocks[len(bc.blocks)-1]
        newBlock := NewBlock(data, prevBlock.Hash)
        bc.blocks = append(bc.blocks, newBlock)
}
```
1. To add a new block we need an existing block, but there's no blocks in our blockchain 
1. In any blockchain, there must be at least one block, and such block, the first in the chain, is called **genesis block**
```
func NewGenesisBlock() *Block {
        return NewBlock("Genesis Block", []byte{})
}
```
1. Now, we can implement a function that creates a blockchain with the genesis block
```
func NewBlockchain() *Blockchain {
        return &Blockchain{[]*Block{NewGenesisBlock()}}
}
```
1. Let's check that the blockchain works correctly 
```
func main() {
        bc := NewBlockchain()

        bc.AddBlock("Send 1 BTC to Nick")

        bc.AddBlock("Send 2 BTC to Noddy")

        for _, block := range bc.blocks {
                fmt.Printf("Prev. hash: %x\n", block.PrevBlockHash)
                fmt.Printf("Data: %s\n", block.Data)
                fmt.Printf("Hash: %x\n", block.Hash)
                fmt.Println()
        }
}
```

## Conclusion 
1. We built a very simple blockchain prototype: it's just an array of blocks, with each block having a connection to the previous one
1. The actual blockchain is much more complex
1. In our blockchain is more easy and fast, but in real blockchain adding new blocks requires some work: one has to perform some heavy computation before getting permission to add block( this mechanism is caklled Proof-Of-Work )
1. Also blockchain is a distributed database that has no single decision maker
1. Thus, a new block must be confirmed and approved by other participants of the network( this mechanism is called consensus ) 
1. There is no transaction in our blockchain yet 

## Complete Code Implementation
```
// block.go

type Block struct {
        Timestamp     int64
        Data          []byte
        PrevBlockHash []byte
        Hash          []byte
}

func (b *Block) SetHash() {
        timestamp := []byte(strconv.FormatInt(b.Timestamp, 10))
        headers := bytes.Join([][]byte{b.PrevBlockHash, b.Data, timestamp}, []byte{})
        hash := sha256.Sum256(headers)

        b.Hash = hash[:]
}

func NewBlock(data string, prevBlockHash []byte) *Block {
        block := &Block{time.Now().Unix(), []byte(data), prevBlockHash, []byte{}}
        block.SetHash()
        return block
}
```

```
// blockchain.go

type Blockchain struct {
        blocks []*Block
}

func (bc *Blockchain) AddBlock(data string) {
        prevBlock := bc.blocks[len(bc.blocks)-1]
        newBlock := NewBlock(data, prevBlock.Hash)
        bc.blocks = append(bc.blocks, newBlock)
}

func NewGenesisBlock() *Block {
        return NewBlock("Genesis Block", []byte{})
}

func NewBlockchain() *Blockchain {
        return &Blockchain{[]*Block{NewGenesisBlock()}}
}
```

```
// main.go

func main() {
        bc := NewBlockchain()

        bc.AddBlock("Send 1 BTC to Nick")

        bc.AddBlock("Send 2 BTC to Noddy")

        for _, block := range bc.blocks {
                fmt.Printf("Prev. hash: %x\n", block.PrevBlockHash)
                fmt.Printf("Data: %s\n", block.Data)
                fmt.Printf("Hash: %x\n", block.Hash)
                fmt.Println()
        }
}
```

## Note
.1 Solve the problem of code not running when in different files
