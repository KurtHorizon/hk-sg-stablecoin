🚀 Local Deployment Guide (Anvil + Foundry)

This section explains how to deploy all stablecoin-related smart contracts (HKDC, SGDC, Oracle, StableFX) to a local Anvil chain using Foundry.

1️⃣ Install Dependencies
cd contract
forge install OpenZeppelin/openzeppelin-contracts@v5.5.0

2️⃣ Start Local Blockchain (Anvil)

In a separate terminal:

anvil

This launches a local chain at:

RPC URL: http://127.0.0.1:8545
Chain ID: 31337
Default deployer private key:
0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80

3️⃣ Deploy HKDC Stablecoin
forge create src/StableCoin.sol:StableCoin \
 --rpc-url http://127.0.0.1:8545 \
 --broadcast \
 --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
 --constructor-args \
 "HKD Stable Coin" \
 "HKDC" \
 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266 \
 '[0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266]'

4️⃣ Deploy SGDC Stablecoin
forge create src/StableCoin.sol:StableCoin \
 --rpc-url http://127.0.0.1:8545 \
 --broadcast \
 --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
 --constructor-args \
 "SGD Stable Coin" \
 "SGDC" \
 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266 \
 '[0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266]'

5️⃣ Deploy Manual Oracle
forge create src/ManualOracle.sol:ManualOracle \
 --rpc-url http://127.0.0.1:8545 \
 --broadcast \
 --private-key 0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80 \
 --constructor-args \
 0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266 \
 173000000000000000

173000000000000000 corresponds to 0.173 ETH (HKD/SGD rate × 1e18).

6️⃣ Deploy StableFX

Replace the last four addresses with the actual deployed addresses from the previous steps.

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

Arguments meaning:

Owner

HKDC address

SGDC address

Oracle address

Fee (in basis points)

Compliance admin address
