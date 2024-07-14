# Hyperledger Exploration  ![](https://img.shields.io/badge/-Live-darkgreen)
![](https://img.shields.io/badge/Domain-Blockchain-blue) ![](https://img.shields.io/badge/Blockchain-Hyperledger-brown) ![](https://img.shields.io/badge/Hyperledger-Besu-gold) <br/> ![](https://img.shields.io/badge/Reviewed-Ramaguru_Radhakrishnan-bronze) <br/> 

## Hyperledger Besu
![](https://img.shields.io/badge/Exploration_By-B_Vijay_Nishanth-gold)  <br/>
![](https://img.shields.io/badge/Start-May-silver) ![](https://img.shields.io/badge/End-July-silver) 

# Deploying a Smart Contract on a Hyperledger Besu Private Network

## Prerequisites
- Hyperledger Besu Private Network 
- Node.js v14 or higher 
```
curl -fsSL https://deb.nodesource.com/setup_21.x | sudo -E bash -
sudo apt-get install -y nodejs
```
- Truffle framework 
- Solidity Smart Contract (Chaincode)

## Step 1: Install Truffle and Ganache CLI
First, ensure you have Truffle installed:
```bash
npm install -g truffle
```
## Step 2: Initialize a Truffle Project
Create a directory for your Truffle project and initialize it:
```
mkdir MyContract
cd MyContract
truffle init
```
## Step 3: Write Your Smart Contract
Create a new Solidity file in the contracts directory, e.g., ```MyContract.sol```
```
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.8.2 <0.9.0;

contract MyContract {
    string public message;

    constructor(string memory _message) {
        message = _message;
    }

    function setMessage(string memory _message) public {
        message = _message;
    }
}
```

## Step 4: Configure Truffle
Update ```truffle-config.js``` file MyContract directory to configure the network:
```
// truffle-config.js
module.exports = {
  networks: {
    besu: {
      host: "127.0.0.1",
      port: 8545,
      network_id: "*", // Match any network id
    },
  },
  compilers: {
    solc: {
      version: "0.8.2",
    },
  },
};
```

## Step 5: Compile the Smart Contract
Compile your smart contract using Truffle:
```
truffle compile
```

## Step 6: Deploy the Smart Contract
Create a migration script in the ```migrations``` directory, e.g., ```deploy_contracts.js```:
```
// migrations/deploy_contracts.js
const MyContract = artifacts.require("MyContract");

module.exports = function (deployer) {
  deployer.deploy(MyContract, "Hello, Besu!");
};
```
Deploy your contract to the network:
```
truffle migrate --network development
```
## Step 7: Interact with the Smart Contract
You can interact with your deployed contract using Truffle console:
```
truffle console --network development
```
In the console, you can interact with your contract
