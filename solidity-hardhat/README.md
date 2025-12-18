# Solidity & Hardhat Development Container

A complete development environment for Ethereum smart contract development using Solidity and Hardhat, containerized for Visual Studio Code. It was originally created for studying the topic "Blockchain Systems", from [MSc in Cybersecurity and Privacy](https://www.uoc.edu/es/estudios/masters/master-universitario-ciberseguridad-privacidad), taught by [Universitat Oberta de Catalunya](https://uoc.edu) (UOC).

## Features

### Pre-installed Tools & Libraries

- **Hardhat**: Ethereum development environment
- **Ethers.js**: Library for interacting with Ethereum
- **OpenZeppelin Contracts**: Secure smart contract library
- **TypeChain**: TypeScript bindings for smart contracts
- **Chai**: Testing framework
- **Solidity Coverage**: Code coverage for Solidity
- **Hardhat Gas Reporter**: Gas consumption analysis
- **Solhint**: Linting tool for Solidity
- **Prettier**: Code formatter with Solidity plugin

### VS Code Extensions

- **Hardhat Solidity**: Official Hardhat extension with IntelliSense
- **Solidity Visual Auditor**: Security-focused code highlighting
- **Solidity Language Support**: Syntax highlighting and compilation
- **Prettier**: Automatic code formatting
- **ESLint**: JavaScript/TypeScript linting

### Network Configuration

- **Port 8545**: Exposed for Hardhat local network
- Auto-notification when network starts

## Getting Started

### Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Remote - Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Setup Instructions

1. **Clone or create your project**
   ```bash
   mkdir my-solidity-project
   cd my-solidity-project
   ```

2. **Add the dev container configuration**
   - Create a `.devcontainer` folder in your project root
   - Copy the `devcontainer.json` file into it

3. **Open in VS Code**
   ```bash
   code .
   ```

4. **Reopen in Container**
   - Press `F1` or `Ctrl+Shift+P` (Windows/Linux) / `Cmd+Shift+P` (Mac)
   - Type and select: `Remote-Containers: Reopen in Container`
   - Wait for the container to build (first time takes a few minutes)

5. **Initialize Hardhat** (if starting a new project)
   ```bash
   npx hardhat init
   ```

## Quick Start Commands

### Compile Contracts
```bash
npx hardhat compile
```

### Run Tests
```bash
npx hardhat test
```

### Start Local Network
```bash
npx hardhat node
```

### Deploy Contracts
```bash
npx hardhat run scripts/deploy.js --network localhost
```

### Code Coverage
```bash
npx hardhat coverage
```

### Gas Report
```bash
REPORT_GAS=true npx hardhat test
```

### Linting
```bash
npx solhint 'contracts/**/*.sol'
```

## Project Structure

Recommended folder structure for your Hardhat project:

```
my-solidity-project/
├── .devcontainer/
│   └── devcontainer.json
├── contracts/
│   └── MyContract.sol
├── scripts/
│   └── deploy.js
├── test/
│   └── MyContract.test.js
├── hardhat.config.js
├── .env
└── README.md
```

## Environment Variables

Create a `.env` file in your project root for sensitive data:

```env
PRIVATE_KEY=your_private_key_here
INFURA_API_KEY=your_infura_key_here
ETHERSCAN_API_KEY=your_etherscan_key_here
```

**Important**: Add `.env` to your `.gitignore` file!

## Configuration

### Hardhat Config Example

```javascript
require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config();

module.exports = {
  solidity: {
    version: "0.8.20",
    settings: {
      optimizer: {
        enabled: true,
        runs: 200
      }
    }
  },
  networks: {
    hardhat: {
      chainId: 31337
    },
    sepolia: {
      url: `https://sepolia.infura.io/v3/${process.env.INFURA_API_KEY}`,
      accounts: [process.env.PRIVATE_KEY]
    }
  },
  gasReporter: {
    enabled: process.env.REPORT_GAS === "true",
    currency: "USD"
  },
  etherscan: {
    apiKey: process.env.ETHERSCAN_API_KEY
  }
};
```

## Troubleshooting

### Container won't build
- Ensure Docker Desktop is running
- Try: `Remote-Containers: Rebuild Container`

### Extensions not working
- Reload VS Code window
- Check that extensions are installed in the container (not just locally)

### Port 8545 already in use
- Stop any local Hardhat or Ganache instances
- Or modify the port in `devcontainer.json`

### npm install fails
- Clear npm cache: `npm cache clean --force`
- Rebuild container

## Additional Resources

- [Hardhat Documentation](https://hardhat.org/docs)
- [Solidity Documentation](https://docs.soliditylang.org/)
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts/)
- [Ethers.js Documentation](https://docs.ethers.org/)

## Contributing

Feel free to submit issues or pull requests to improve this dev container configuration.

## License

This dev container configuration is available under the MIT License.
