const crypto = require("crypto");

const SHA256 = message => crypto.createHash("sha256").update(message).digest("hex");

class Block {
    constructor(timestamp = "", data = []) {
        this.timestamp = timestamp;
        this.data = data;
        this.hash = this.getHash();
        this.prevHash = ""; // previous block's hash
        this.nonce = 0;  // Initialize nonce
    }

    // Our hash function.
    getHash() {
        return SHA256(JSON.stringify(this.data) + this.prevHash + this.timestamp  + this.nonce);
    }

    // validate() {
    //     if (!Array.isArray(this.data)) {
    //         return false;
    //     }

    //     for (const item of this.data) {
    //         if (typeof item !== 'string') {
    //             return false;
    //         }
    //     }

    //     return true;
    // }

    mine(difficulty) {
        while (true) {
            this.nonce++;
            this.hash = this.getHash();
            if (this.hash.startsWith("0".repeat(difficulty))) {
                break;
            }
        }
    }

    // mine(difficulty){
    //     while(this.hash.startsWith(Array(difficulty + 1).join("0"))){
    //         this.nonce++;
    //         this.hash = this.getHash();
    //     }
  
}

class Blockchain {
    constructor() {
        // Create our genesis block
        this.chain = [new Block(Date.now().toString())];
        this.difficulty = 1;
        this.blockTime = 30000;
    }

    getLastBlock() {
        return this.chain[this.chain.length - 1];
    }

    addBlock(block) {
        block.prevHash = this.getLastBlock().hash;
        block.hash = block.getHash();
        block.mine(this.difficulty);
        this.difficulty += Date.now() - parseInt(this.getLastBlock().timestamp) < this.blockTime ? 1 : -1;
        this.chain.push(block);
        
        
    }

    isValid(blockchain = this) {
        for (let i = 1; i < blockchain.chain.length; i++) {
            const currentBlock = blockchain.chain[i];
            const prevBlock = blockchain.chain[i-1];

            if (currentBlock.hash !== currentBlock.getHash() || prevBlock.hash !== currentBlock.prevHash) {
                return false;
            }
        }

        return true;
    }
}

const caChain = new Blockchain();
caChain.addBlock(new Block(Date.now().toString(), ["hello Builders1"]));
caChain.addBlock(new Block(Date.now().toString(), ["hello Builders2"]));
caChain.addBlock(new Block(Date.now().toString(), ["hello Builders3"]));

console.log(caChain);
console.log("Blockchain Valid?", caChain.isValid());
