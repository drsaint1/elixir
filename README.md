# Setting Up an Elixir Testnet v3 Validator: A Step-by-Step Guide

This guide walks you through the process of setting up a validator on the Elixir Network testnet, contributing to the security and performance of orderbook development. Follow these instructions to get started on the Elixir Testnet.
# #Testnet v3 Preparations
# Hardware Requirements
While most hardware can support running a validator node, it's recommended to use a system that operates continuously, 24/7. The ideal setup includes at least 8GB of memory and a stable 100Mbit internet connection. Disk usage is typically minimal, with 100GB of storage being sufficient in most cases.
# Docker Installation
## Docker Installation Script for Ubuntu

```bash
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove --purge $pkg -y; done

sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg apt-transport-https
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Docker version check
docker --version
```


# Wallet Preparation
You will use a wallet to run your validator.
It is advisable to use a wallet dedicated solely to Elixir.

You can generate a new wallet in MetaMask by clicking on the icon “+ Add account or hardware wallet”, then on “+ Add a new account”

# Download the Elixir File
Download the configuration file provided by Elixir

```bash
wget https://files.elixir.finance/validator.env
```
Next step is to open the text file to customize it with your information using:
```bash
nano validator.env
```
This will open a file that looks like this :

STRATEGY_EXECUTOR_DISPLAY_NAME=

STRATEGY_EXECUTOR_BENEFICIARY=<ADRESSE_WALLET>

SIGNER_PRIVATE_KEY=<PRIVATE_KEY_WALLET>

Replace the <> with your details.

After making all the modifications to the file, you can exit the screen by pressing CTRL+X, then pressing Y and ENTER.

# Validator Node Installation
To build the validator node image, run the following Docker command:
```bash
docker pull elixirprotocol/validator:v3
```
# Launch the Validator Node
To Start your validator node use:
```bash
docker run -d \
  --env-file validator.env \
  --name elixir \
  --restart unless-stopped \
  elixirprotocol/validator:v3
```
To check the node log use :
```bash
docker logs -f elixir
```

Here's a rewritten version of your text:

---

### Enrolling Your Validator Node

#### 5. Claiming MOCK Tokens

The Testnet v3 network utilizes MOCK tokens on the Ethereum Sepolia test network. To obtain MOCK tokens, you will need a small amount of Sepolia ETH in your wallet. You can claim some using the following link:  
[Claim Sepolia ETH](https://sepolia-faucet.pk910.de/)

Next, navigate to the Elixir Network Testnet v3 dashboard and connect your wallet:  
[Elixir Network Testnet v3 Dashboard](https://testnet-3.elixir.xyz/)

Ensure that you are connected to the Ethereum Sepolia network, then click on “MINT 1,000 MOCK.” Confirm the transaction in the wallet specified in your `validator.env` file.

After claiming your tokens, you can stake them on your validator. Enter your validator’s address in the search bar and click on ‘Delegate.’

--- 

Let me know if you need any further changes!
