# ethereum-style-blockchain
An educational, Ethereum-inspired blockchain implementation developed as a university project in 2020. The project implements core blockchain components and supports basic smart contract execution to explore Ethereum-style design principles.

# Project Setup & Usage Guide

These instructions are meant to be followed in a **Linux environment**, specifically **Ubuntu 20.04**, which was used during development.

---

## Prerequisites & Tool Installation

### 1. Install Geth (Go Ethereum)

First, install the required dependencies and Geth:

```bash
sudo apt install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum
```

---

### 2. Install Node.js and NPM

Check if Node.js and NPM are already installed:

```bash
node -v
npm -v
```

Ensure:
- Node.js version ≥ 8
- NPM version ≥ 5

If they are not installed, run:

```bash
sudo apt install nodejs
sudo apt install npm
```

---

### 3. Install Truffle

For this project, Truffle version 4 was used:

```bash
sudo npm install -g truffle@4.0.4
```

---

## Running the Blockchain Node

All files related to the private blockchain node are located in the `private` directory.

### Accounts

The node contains three accounts, whose hashes can be found in the `keystore` folder.

- Account 0 is used as the miner.
- The password for all accounts is `1234`  
  (also stored in `password.sec`)

---

### Start the Node

Navigate to the `private` directory and make the startup script executable:

```bash
chmod +x startnode.sh
```

Then run the node:

```bash
./startnode.sh
```

The first run may take some time. Subsequent runs will start faster.

---

### Attach to the Geth Console

While the node is running, open a second terminal and run:

```bash
geth attach
```

From here, you can perform transactions and interact with accounts.

An extensive list of available commands can be found at:  
https://geth.ethereum.org/docs/interface/javascript-console

To exit:
- Leave the Geth console:
  ```javascript
  exit
  ```
- Stop the node:
  Ctrl + C

---

## Smart Contracts

The project includes two smart contracts:

1. Migration  
   Required by Truffle and allows deployment across different nodes.

2. Greetings  
   A simple example contract that allows setting and retrieving a message.

---

### Deploy Smart Contracts

Navigate to the `Smart Contracts` directory and deploy the contracts:

```bash
truffle migrate --compile-all --reset --network mynet
```

---

### Interact with Contracts via Truffle Console

Enter the Truffle console:

```bash
truffle console --network mynet
```

Load the deployed `Greetings` contract:

```javascript
Greetings.deployed().then(function(instance){ app = instance; })
```

Example interactions:

```javascript
app.getGreetings()
```

```javascript
app.setGreetings("Hello Friends!", { from: web3.eth.accounts[0] })
```

Exit the console at any time with:

```javascript
.exit
```

