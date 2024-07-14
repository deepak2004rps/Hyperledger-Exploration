# Hyperledger Exploration  ![](https://img.shields.io/badge/-Live-darkgreen)
![](https://img.shields.io/badge/Domain-Blockchain-blue) ![](https://img.shields.io/badge/Blockchain-Hyperledger-brown) ![](https://img.shields.io/badge/Hyperledger-Besu-gold) <br/> ![](https://img.shields.io/badge/Reviewed-Ramaguru_Radhakrishnan-bronze) <br/> 

## Hyperledger Besu
![](https://img.shields.io/badge/Exploration_By-B_Vijay_Nishanth-gold)  <br/>
![](https://img.shields.io/badge/Start-May-silver) ![](https://img.shields.io/badge/End-July-silver) 

# Setting Up a Private Network Using IBFT 2.0 in Hyperledger Besu

## Prerequisites
- Java 11+
- Hyperledger Besu

## Create and Deploy Private Network

### Step 1: Create node directories
Each node requires a data directory for the blockchain data.

Create directories for your private network, each of the four nodes, and a data directory for each node(IBFT 2.0 Requires minimum 4 nodes):
```
mkdir -p IBFT-Network/Node-{1..4}/data
``````
```BFT-Network/
├── Node-1
│   ├── data
├── Node-2
│   ├── data
├── Node-3
│   ├── data
└── Node-4
    ├── data
```

### Step 2: Create Genesis Configuration File

The configuration file defines the IBFT 2.0 genesis file and the number of node key pairs to generate.
 the following configuration file definition to a file called ```ibftConfigFile.json``` and save it in the IBFT-Network directory:

```
{
  "genesis": {
    "config": {
      "chainId": 1337,
      "berlinBlock": 0,
      "ibft2": {
        "blockperiodseconds": 2,
        "epochlength": 30000,
        "requesttimeoutseconds": 4
      }
    },
    "nonce": "0x0",
    "timestamp": "0x58ee40ba",
    "gasLimit": "0x47b760",
    "difficulty": "0x1",
    "mixHash": "0x63746963616c2062797a616e74696e65206661756c7420746f6c6572616e6365",
    "coinbase": "0x0000000000000000000000000000000000000000",
    "alloc": {
      "fe3b557e8fb62b89f4916b721be55ceb828dbd73": {
        "privateKey": "8f2a55949038a9610f50fb23b5883af3b4ecb3c3bb792cbcefbd1542c692be63",
        "comment": "private key and this comment are ignored. In a real chain, the private key should NOT be stored",
        "balance": "0xad78ebc5ac6200000"
      },
      "627306090abaB3A6e1400e9345bC60c78a8BEf57": {
        "privateKey": "c87509a1c067bbde78beb793e6fa76530b6382a4c0241e5e4a9ec0a0f44dc0d3",
        "comment": "private key and this comment are ignored. In a real chain, the private key should NOT be stored",
        "balance": "90000000000000000000000"
      },
      "f17f52151EbEF6C7334FAD080c5704D77216b732": {
        "privateKey": "ae6ae8e5ccbfb04590405997ee2d52d2b330726137b875053c36d94e974d162f",
        "comment": "private key and this comment are ignored. In a real chain, the private key should NOT be stored",
        "balance": "90000000000000000000000"
      }
    }
  },
  "blockchain": {
    "nodes": {
      "generate": true,
      "count": 4
    }
  }
}
```

### Step 3: Generate Node Keys and a Genesis File
In the IBFT-Network directory, generate the node key and genesis file using the configurations given in the ibftConfigFile.json file:
```
besu operator generate-blockchain-config --config-file=ibftConfigFile.json --to=networkFiles --private-key-file-name=key
```
This command will generate the public and the private key for the no of nodes given in the ibftConfigFile.json

### Step 4: Copy the Genesis File to the IBFT-Network Directory
Copy the ```genesis.json``` file to the IBFT-Network directory.
```
cp networkFiles/genesis.json IBFT-Network/
```

### Step 5: Copy the Node Private Keys to the Node Directories
For each node, copy the key files to the data directory for that node:
```
IBFT-Network/
├── genesis.json
├── Node-1
│   ├── data
│   │   ├── key
│   │   ├── key.pub
├── Node-2
│   ├── data
│   │   ├── key
│   │   ├── key.pub
├── Node-3
│   ├── data
│   │   ├── key
│   │   ├── key.pub
├── Node-4
│   ├── data
│   │   ├── key
│   │   ├── key.pub
```

### Step 6: Start the First Node as the Bootnode
In the Node-1 directory, start Node-1:
```
besu --data-path=data --genesis-file=../genesis.json --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all"
```
### Step 7: Start Node-2, Node-3, Node-4
Start another terminal, change to the corresponding Node directory and start the corresponding Node specifying the Node-1 enode URL copied when starting Node-1 as the bootnode:
- Node-2
```
besu --data-path=data --genesis-file=../genesis.json --bootnodes=<Node-1 Enode URL> --p2p-port=30304 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8546
```
- Node-3
```
besu --data-path=data --genesis-file=../genesis.json --bootnodes=<Node-1 Enode URL> --p2p-port=30305 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8547
```
- Node-4
```
besu --data-path=data --genesis-file=../genesis.json --bootnodes=<Node-1 Enode URL> --p2p-port=30306 --rpc-http-enabled --rpc-http-api=ETH,NET,IBFT --host-allowlist="*" --rpc-http-cors-origins="all" --rpc-http-port=8548
```

### Step 8: Confirm the Private Network is Working
Start another terminal, use curl to call the JSON-RPC API ```ibft_getValidatorsByBlockNumber``` method and confirm the network has four validators:
```
curl -X POST --data '{"jsonrpc":"2.0","method":"ibft_getValidatorsByBlockNumber","params":["latest"], "id":1}' localhost:8545
```
