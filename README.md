# ethereum-style-blockchain
An educational, Ethereum-inspired blockchain implementation developed as a university project in 2020. The project implements core blockchain components and supports basic smart contract execution to explore Ethereum-style design principles.

# Project Setup & Usage Guide

These instructions are meant to be followed in a **Linux environment**and more specifically 
we used **Ubuntu 20.04**.

---

## Prerequisites & Tool Installation

The first step is the installation of the tools required for the implementation.

### 1. Install Geth (Go Ethereum)

The first installation is of geth for which we run the following commands in the terminal

```bash
sudo apt install software-properties-common
sudo add-apt-repository -y ppa:ethereum/ethereum
sudo apt-get update
sudo apt-get install ethereum
```

---

### 2. Install Node.js and NPM

Then we will need NodeJS and NPM
We check whether they are already installed in our machine using the following commands

```bash
node -v
npm -v
```

If they are indeed installed we need to ensure the NodeJS is of **version 8** or newer and NPM 
is of **version 5** or newer.

If they are not already installed we install them using the following commands

```bash
sudo apt install nodejs
sudo apt install npm
```

---

### 3. Install Truffle

Finally we install Truffle. For this project we used Truffle **version 4**.
We run the following command

```bash
sudo npm install -g truffle@4.0.4
```

---

After the necessary installations we begin with the node.

## Running the Blockchain Node

In `private` folder we find everything needed for the node.

### Accounts

The node assigned for our 
blockchain contains three accounts the hashes of which can be found in `keystore` folder.

- Account 0 is the miner.
<!-- - The password for all accounts is `1234`  
  (also stored in `password.sec`) -->

---

### Start the Node

To begin the process we first turn `startnode.sh` to an executable.
To do so we run the following command in `private` directory

```bash
chmod +x startnode.sh
```

and then we run the executable using

```bash
./startnode.sh
```

The first time we run it it may take a while, the following times it will be quicker.

---

### Attach to the Geth Console

While the program is running we open a second terminal and run the following command

```bash
geth attach
```

From there we can perform transactions with the accounts we have built.

An extensive guide with the available commands can be found at the following link  
https://geth.ethereum.org/docs/interface/javascript-console

For the commands that require a password, it is `pass 1234` and can also be found in the 
`password.sec` file.

We can exit geth console using typing `exit` and we can stop the program typing `ctrl+c`.

---

We then look into the smart contract application in the node we have built

## Smart Contracts

For starters, in our implementation we have two smart contracts.

1. The first is called `migration` and is necessary and it allows us to apply it in different nodes.

2. The other is called `Greetings` and it's a simple example we can use to set and print a message.

---

### Deploy Smart Contracts

To apply our smart contracts to the node we have built in the previous step, we open a terminal
in the "Smart Contracts" directory and run the following command

```bash
truffle migrate --compile-all --reset --network mynet
```
This command performs the compilation.

---

### Interact with Contracts via Truffle Console

We then run

```bash
truffle console --network mynet
```

to get into the truffle console where we can write commands related to the node and the smart
contracts.

Furthermore to run the functions that constitute the `Greetings` smart contract we run 
in the console

```javascript
Greetings.deployed().then(function(instance){ app = instance; })
```

After that we can run for example

```javascript
app.getGreetings()
```

which will show us the smart contract's message, or run

```javascript
app.setGreetings("Hello Friends!", { from: web3.eth.accounts[0] })
```

which will change the message to "Hello Friends!".

We can always exit the console by typing

```javascript
.exit
```

