# Local Deployment Guide (Anvil + Foundry)

This guide explains how to deploy all stablecoin-related smart contracts (HKDC, SGDC, Oracle, StableFX) onto a local Anvil blockchain.

## 1 Install Dependencies

```
cd contract
forge install OpenZeppelin/openzeppelin-contracts@v5.5.0
```

## 2 Start Local Blockchain (Anvil)

Open a new terminal tab and run:

```
anvil
```

Anvil will start at:

RPC URL: http://127.0.0.1:8545

Chain ID: 31337

Default deployer private key:

0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80

## 3 Deploy HKDC Stablecoin

```
forge create src/StableCoin.sol:StableCoin \
 --rpc-url http://127.0.0.1:8545 \
 --broadcast \
 --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
 --constructor-args \
 "HKD Stable Coin" \
 "HKDC" \
 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266 \
 '[0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266]'
```

## 4 Deploy SGDC Stablecoin

```
forge create src/StableCoin.sol:StableCoin \
 --rpc-url http://127.0.0.1:8545 \
 --broadcast \
 --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
 --constructor-args \
 "SGD Stable Coin" \
 "SGDC" \
 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266 \
 '[0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266]'
```

## 5 Deploy Manual Oracle

Set the initial HKD/SGD price to 0.173 (× 1e18).

```
forge create src/ManualOracle.sol:ManualOracle \
 --rpc-url http://127.0.0.1:8545 \
 --broadcast \
 --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
 --constructor-args \
 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266 \
 173000000000000000
```

## 6 Deploy StableFX (Swap Engine)

⚠️ Replace the HKDC, SGDC, and Oracle addresses below with the actual deployment output from steps 3–5.

```
forge create src/StableFX.sol:StableFX \
 --rpc-url http://127.0.0.1:8545 \
 --broadcast \
 --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
 --constructor-args \
 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266 \
 0x5FbDB2315678afecb367f032d93F642f64180aa3 \
 0xe7f1725E7734CE288F8367e1Bb143E90bb3F0512 \
 0x9fE46736679d2D9a65F0992F2272dE9f3c7fa6e0 \
 20 \
 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266
```
