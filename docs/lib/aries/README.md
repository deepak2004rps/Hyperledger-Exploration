# Hyperledger Exploration  ![](https://img.shields.io/badge/-Live-darkgreen)
![](https://img.shields.io/badge/Domain-Blockchain-blue) ![](https://img.shields.io/badge/Blockchain-Hyperledger-brown) ![](https://img.shields.io/badge/Hyperledger-Besu-gold) <br/> ![](https://img.shields.io/badge/Reviewed-Ramaguru_Radhakrishnan-bronze) <br/> 

## Hyperledger Aries
![](https://img.shields.io/badge/Exploration_By-B_Vijay_Nishanth-gold)  <br/>
![](https://img.shields.io/badge/Start-May-silver) ![](https://img.shields.io/badge/End-June-silver) 

 <p align="center"><img src="../../logos/Hyperledger_Aries.jpg" width=320> </p>

### Introduction
Hyperledger Aries is your complete toolkit for decentralized identity solutions and digital trust. Issue, store and present verifiable credentials with maximum privacy preservation, and establish confidential, ongoing communication channels for rich interactions. It supports multiple protocols, credential types, ledgers and registries. It has frameworks in multiple development languages, and interoperability tools and profiles to help everything work together seamlessly.

### Exploration Test Setup
This Exploration aims to setup hyperledger besu as a private network built using binaries.
- Operating system - Linux Mint 21.3 Virginia

  
### Prerequisities
- Java Development Kit (JDK) Version 11 or higher
- System Tools

### Installation Instruction
#### Prerequisities
##### JDK
- I have chosen openjdk-22.0.1
```
sudo apt update 

sudo apt install openjdk-21-jdk 
```

##### System Tools #####
```
sudo apt install wget curl
```

After verifying and installing the prerequisites we can proceed with the step by step installation process

#### Besu Installation and Configuration
##### Step 1: Download Hyperledger Besu
- This command uses wget to download the specified version of Hyperledger Besu from its official GitHub releases page. 
```
 wget https://github.com/hyperledger/besu/releases/download/24.5.2/besu-24.5.2.tar.gz
 ```
- Extracting the tar file
 ```
 tar -xzf besu-24.5.2.tar.gz  
 ``` 
##### Step 2: Setting the path variable
- Navigates into the directory where Besu was extracted.
 ```
cd besu-24.5.2  
 ```
- This command adds the current directory's bin subdirectory to the system PATH using $(pwd) to dynamically insert the current directory path.
 ```
export PATH=$PATH:$(pwd)/bin
 ```
##### Step 3: Setting up the ~./bashrc file
- The echo command appends the PATH export statement to the ~/.bashrc file, ensuring the PATH change is applied in future terminal sessions.
 ```
echo 'export PATH=$PATH:$(pwd)/bin' >> ~/.bashrc  
 ```
- The source ~/.bashrc command reloads the ~/.bashrc file to apply the PATH changes immediately.
 ```
source ~/.bashrc  
 ```
##### Step 4: Verifing the installantion
- Running besu --version verifies that Besu is installed correctly and accessible in your terminal. 
 ```
besu –version 
 ```

### Running the Network

### Deploying the Smart Contracts

### References
 - [Hyperledger Besu Documentation](https://besu.hyperledger.org/)
