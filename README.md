# CryptoZombies - Blockchain Game

## Project Overview
A decentralized zombie battle game built on Ethereum blockchain using Solidity smart contracts and Web3.js frontend.

## Features
- **Create Zombies**: Generate unique zombies with random DNA
- **Battle System**: Attack other zombies with 70% win probability
- **Level Up**: Upgrade zombie levels using ETH
- **Rename Zombies**: Customize zombie names
- **Feed on Kitties**: Breed with CryptoKitties to create new zombies
- **Win/Loss Tracking**: Monitor battle statistics
- **Cooldown System**: Strategic timing for actions

## Prerequisites

### Required Software
- **Node.js** v14.16.0 or higher
- **Truffle** v5.4.25 or higher
- **Ganache** v2.5.4 or higher (GUI or CLI)
- **MetaMask** browser extension
- **http-server** (for serving the frontend)

### Installation Commands
```bash
npm install -g truffle
npm install -g ganache-cli
npm install -g http-server
```

## Setup Instructions

### 1. Install MetaMask
- Install MetaMask browser extension from [Chrome Web Store](https://chrome.google.com/webstore/detail/metamask/nkbihfbeogaeaoehlefnkodbefgpgknn)
- Create or import a wallet

### 2. Start Ganache Blockchain
**Option A: Ganache GUI**
- Open Ganache GUI
- Click "Quickstart" to create a new workspace
- Note the RPC Server URL (usually `http://127.0.0.1:7545`)
- Note the Network ID (usually `5777`)

**Option B: Ganache CLI**
```bash
ganache-cli -p 7545 -i 5777
```

### 3. Deploy Smart Contracts
```bash
# Install dependencies
npm install

# Compile contracts
truffle compile

# Deploy to Ganache
truffle migrate --reset
```

**Important**: After migration, copy the contract address from the terminal output.

### 4. Update Contract Address
- Open `index.html`
- Find the `GANACHE_CONTRACT_ADDRESS` variable (around line 200)
- Replace with your deployed contract address from step 3

### 5. Configure MetaMask Network
Add Ganache network to MetaMask:
- **Network Name**: `Ganache Local`
- **New RPC URL**: `http://127.0.0.1:7545`
- **Chain ID**: `1337`
- **Currency Symbol**: `ETH`

### 6. Import Ganache Account
- Copy a private key from Ganache (click the key icon next to any account)
- In MetaMask: Account menu → Import Account → Paste private key
- Switch to the Ganache Local network

### 7. Start the Frontend
```bash
# Start local web server
http-server -p 8080

# Or use any other method to serve static files
python -m http.server 8080  # Python 3
python -m SimpleHTTPServer 8080  # Python 2
```

### 8. Access the Game
- Open browser and go to `http://localhost:8080`
- Connect MetaMask when prompted
- Ensure you're on the Ganache Local network

## How to Play

### Creating Your First Zombie
1. Click "Create Zombie"
2. Enter a name for your zombie
3. Confirm the transaction in MetaMask
4. Wait for blockchain confirmation

### Game Actions

#### Level Up (Costs 0.001 ETH)
- Click "Level Up" on any zombie card
- Confirm transaction with 0.001 ETH fee
- Increases zombie level and power

#### Rename Zombie
- Click "Rename" on any zombie card
- Enter new name in the prompt
- Confirm transaction

#### Attack Other Zombies
- Click "Attack" on your zombie card
- Enter target zombie ID (try 0, 1, 2, etc.)
- 70% chance to win and create a new zombie
- Cannot attack your own zombies

#### Feed on CryptoKitties
- Click "Feed Kitty" on your zombie card
- Enter any CryptoKitty ID number
- Creates a new zombie with mixed DNA

### Game Mechanics
- **Cooldown**: All zombies have 1-minute cooldown after actions
- **Battle Results**: Win = new zombie + level up, Lose = cooldown only
- **DNA System**: Each zombie has unique 16-digit DNA
- **Win/Loss Tracking**: Statistics displayed on zombie cards

## Troubleshooting

### Common Issues

**"Contract not deployed" error:**
- Ensure Ganache is running
- Run `truffle migrate --reset`
- Update contract address in `index.html`

**MetaMask connection issues:**
- Check network configuration matches Ganache
- Ensure you're using an imported Ganache account
- Try refreshing the page

**Transaction failures:**
- Check account has sufficient ETH balance
- Ensure zombie is not in cooldown period
- Verify you're not attacking your own zombie

**"Insufficient funds" error:**
- Import a Ganache account with ETH balance
- Each Ganache account starts with 100 ETH

### Network Configuration Verification
Ensure these match between Ganache and MetaMask:
- **RPC URL**: `http://127.0.0.1:7545`
- **Network ID**: `5777`
- **Chain ID**: `1337`

## Testing All Features

### Complete Test Sequence
1. **Create Zombie**: Create your first zombie
2. **Level Up**: Spend 0.001 ETH to level up
3. **Rename**: Change zombie name
4. **Attack**: Attack zombie ID 0, 1, or 2
5. **Feed Kitty**: Use any kitty ID (e.g., 1)
6. **Check Stats**: Verify win/loss counts update
7. **Cooldown**: Wait 1 minute between actions


## Project Structure

### Smart Contracts (Hierarchical Inheritance)
```
CryptoZombies.sol (Main contract)
└── ZombieOwnership.sol (ERC721 NFT functionality)
    └── ZombieAttack.sol (Battle system)
        └── ZombieHelper.sol (Utility functions)
            └── ZombieFeeding.sol (Breeding mechanics)
                └── ZombieFactory.sol (Core zombie creation)
                    └── Ownable.sol (Access control)
```

### Supporting Contracts
- **SafeMath.sol**: Secure mathematical operations
- **ERC721.sol**: NFT standard interface

### Frontend Files
- **index.html**: Main game interface
- **styles.css**: Game styling
- **cryptozombies_abi.js**: Contract ABI for Web3 interaction
- **web3.min.js**: Web3 library

### Configuration
- **truffle-config.js**: Truffle deployment configuration
- **package.json**: Node.js dependencies

## Development Notes

### Contract Address Management
The contract address is hardcoded in `index.html` for Ganache local development. After each `truffle migrate --reset`, update the `GANACHE_CONTRACT_ADDRESS` variable.

### Gas Optimization
- Level up cost: 0.001 ETH
- All other transactions use default gas limits
- Ganache provides 100 ETH per account for testing

### Security Features
- Owner-only functions for contract management
- Zombie ownership verification for actions
- Cooldown system prevents spam attacks
- SafeMath prevents integer overflow/underflow

## Contributing
1. Fork the repository
2. Create a feature branch
3. Test thoroughly on Ganache
4. Submit a pull request
