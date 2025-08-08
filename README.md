# Stylus ERC20 Token

A complete ERC20 token implementation written in Rust using the [Stylus SDK](https://github.com/OffchainLabs/stylus-sdk-rs) for Arbitrum. This project demonstrates how to create a fully functional ERC20 token that can be deployed on Arbitrum's Stylus testnet and mainnet.

<!-- ![Stylus ERC20 Token](./header.png) -->

## 🚀 Overview

This project implements a standard ERC20 token with the following features:

- **Standard ERC20 Compliance**: Implements all required ERC20 functions (transfer, approve, allowance, etc.)
- **Minting & Burning**: Includes mint and burn functionality for token supply management
- **Rust Implementation**: Written entirely in Rust and compiled to WebAssembly (WASM)
- **Arbitrum Stylus**: Deployable on Arbitrum's Stylus network for enhanced performance
- **Solidity ABI Compatible**: Can be interacted with using standard Ethereum tooling

## 📋 Token Details

- **Name**: StylusToken
- **Symbol**: STK
- **Decimals**: 18
- **Standard**: ERC20

## 🏗️ Architecture

<!-- ### Project Structure

```
stylus-erc20/
├── src/
│   ├── lib.rs          # Main contract entry point
│   └── erc20.rs        # ERC20 implementation
├── examples/
│   └── counter.rs      # Example interaction code
├── Cargo.toml          # Rust dependencies
└── README.md           # This file
``` -->

### Core Components

#### 1. `lib.rs` - Main Contract

- Defines the `StylusToken` struct with ERC20 inheritance
- Implements minting and burning functionality
- Configures token parameters (name, symbol, decimals)

#### 2. `erc20.rs` - ERC20 Implementation

- Complete ERC20 standard implementation
- Includes all required functions: `transfer`, `approve`, `allowance`, `balance_of`, etc.
- Handles events: `Transfer` and `Approval`
- Implements error handling for insufficient balances and allowances

## 🔧 Features

### Standard ERC20 Functions

- `name()` - Returns token name
- `symbol()` - Returns token symbol
- `decimals()` - Returns token decimals
- `total_supply()` - Returns total token supply
- `balance_of(address)` - Returns balance of specified address
- `transfer(to, value)` - Transfers tokens to another address
- `transfer_from(from, to, value)` - Transfers tokens on behalf of another address
- `approve(spender, value)` - Approves spending of tokens
- `allowance(owner, spender)` - Returns approved spending amount

### Extended Functions

- `mint(value)` - Mints new tokens to sender
- `mint_to(to, value)` - Mints new tokens to specified address
- `burn(value)` - Burns tokens from sender

## 🛠️ Prerequisites

Before you begin, ensure you have the following installed:

1. **Rust** (latest stable version)

   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```

2. **Stylus CLI Tools**

   ```bash
   cargo install --force cargo-stylus cargo-stylus-check
   ```

3. **WASM Target**
   ```bash
   rustup target add wasm32-unknown-unknown
   ```

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/Fayob/Stylus-ERC20-Token.git
cd Stylus-ERC20-Token
```

### 2. Build the Project

```bash
cargo build --release
```

### 3. Export ABI

```bash
cargo stylus export-abi
```

This generates a Solidity ABI that can be used with any Ethereum tooling.

### 4. Check Deployment

```bash
cargo stylus check
```

This validates that your program compiles to valid WASM and will succeed deployment onchain.

### 5. Deploy to Stylus Testnet

First, estimate gas costs:

```bash
cargo stylus deploy \
  --private-key-path=<PRIVKEY_FILE_PATH> \
  --estimate-gas
```

Then deploy:

```bash
cargo stylus deploy \
  --private-key-path=<PRIVKEY_FILE_PATH>
```

The deployment process involves two transactions:

1. **Deploy**: Uploads the WASM program to the network
2. **Activate**: Activates the program for use

## 📝 Usage Examples

### Interacting with the Token

After deployment, you can interact with your token using any Ethereum-compatible tooling. Here's an example using ethers.js:

```javascript
// Token contract ABI (exported from cargo stylus export-abi)
const tokenABI = [...]; // Your exported ABI here

// Initialize contract
const tokenContract = new ethers.Contract(tokenAddress, tokenABI, signer);

// Check token info
const name = await tokenContract.name();
const symbol = await tokenContract.symbol();
const decimals = await tokenContract.decimals();
const totalSupply = await tokenContract.total_supply();

// Check balance
const balance = await tokenContract.balance_of(userAddress);

// Transfer tokens
const tx = await tokenContract.transfer(recipientAddress, amount);
await tx.wait();

// Approve spending
const approveTx = await tokenContract.approve(spenderAddress, amount);
await approveTx.wait();

// Mint tokens (if you have permission)
const mintTx = await tokenContract.mint(amount);
await mintTx.wait();
```

<!-- ### Rust Example

See `examples/counter.rs` for a complete Rust example of how to interact with the deployed contract using ethers-rs. -->

## 🔍 Testing

### Local Testing

```bash
cargo test
```

### On-chain Testing

```bash
cargo stylus check
```

<!-- ## 🌐 Network Information

### Testnet

- **RPC Endpoint**: `https://sepolia-rollup.arbitrum.io/rpc`
- **Chain ID**: 421614 (Arbitrum Sepolia)
- **Block Explorer**: https://sepolia.arbiscan.io/

### Mainnet

- **RPC Endpoint**: `https://arb1.arbitrum.io/rpc`
- **Chain ID**: 42161 (Arbitrum One)
- **Block Explorer**: https://arbiscan.io/ -->

## 📚 Documentation

- [Stylus SDK Documentation](https://github.com/OffchainLabs/stylus-sdk-rs)
- [Arbitrum Stylus Documentation](https://docs.arbitrum.io/stylus/)
- [ERC20 Standard](https://eips.ethereum.org/EIPS/eip-20)

## 🔒 Security

⚠️ **Important**: This code is for educational purposes and has not been audited. Do not use in production without proper security review.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [OffchainLabs](https://offchainlabs.com/) for the Stylus SDK
- [Arbitrum](https://arbitrum.io/) for the Stylus network
- The Ethereum community for the ERC20 standard

---

**Note**: This is a demonstration project showing how to implement ERC20 tokens using Rust and the Stylus SDK. For production use, ensure proper security audits and testing.
