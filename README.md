# Development Containers Collection

A curated collection of ready-to-use development container configurations for various technologies and frameworks.

## 🚀 What are Dev Containers?

Development Containers (dev containers) allow you to use a Docker container as a full-featured development environment. They provide consistent, reproducible development environments that work across different machines and operating systems.

## 📋 Prerequisites

Before using any dev container from this collection, ensure you have:

1. **[Visual Studio Code](https://code.visualstudio.com/)** installed
2. **[Docker Desktop](https://www.docker.com/products/docker-desktop)** installed and running
3. **[Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)** for VS Code

## 📦 Available Dev Containers

| Technology | Description | Link |
|-----------|-------------|------|
| **Solidity & Hardhat** | Ethereum smart contract development with Hardhat, OpenZeppelin, and testing tools | [→ View](./solidity-hardhat/) |
| **C x86-64 Reversing** | C/C++ development oriented to reverse engineering | [→ View](./c-x86-64-reversing/) |
| **Java 21 & PostgreSQL 18** | Java 21 development with PostgreSQL 18 database, Gradle, and cloud CLI tools | [→ View](./java-21-postgresql-18/) |
| **Python 3.14** | Python 3.14 development with uv, Ruff, Mypy, pytest, and Jupyter notebook support | [→ View](./python-3_14/) |
| **Playwright TypeScript** | End-to-end testing and browser automation with Playwright, TypeScript, and pnpm | [→ View](./playwright-ts/) |
| More coming soon... | | |

## 🎯 How to Use

### Method 1: Copy to Your Project

1. **Choose a dev container** from the collection
2. **Copy the `.devcontainer` folder** to your project root
3. **Open your project** in VS Code
4. **Press** `F1` or `Ctrl+Shift+P` (Windows/Linux) / `Cmd+Shift+P` (Mac)
5. **Select**: `Dev Containers: Reopen in Container`
6. **Wait** for the container to build and start

### Method 2: Use as Template

1. **Navigate** to the specific dev container folder
2. **Read the README** for that technology
3. **Copy the configuration** and customize it for your needs
4. **Follow the setup instructions** in the specific README

### Method 3: Clone and Experiment

```bash
# Create the network (or update the devcontainer.json with your own Docker network)
docker network create devnet

# Clone this repository
git clone https://github.com/GarciaDan/dev-containers.git

# Navigate to a specific dev container
cd dev-containers/solidity-hardhat

# Open in VS Code
code .

# Reopen in container when prompted
```

## 🏗️ Repository Structure

```
devcontainers-collection/
├── README.md                          # This file
├── solidity-hardhat/                  # Solidity & Hardhat
│   ├── .devcontainer/
│   │   └── devcontainer.json
│   └── README.md
├── c-x86-64-reversing/                # C/C++ development and reversing lab
│   ├── .devcontainer/
│   ├── ├── Dockerfile
│   │   └── devcontainer.json
│   └── README.md
├── java-21-postgresql-18/             # Java 21 & PostgreSQL 18
│   ├── .devcontainer/
│   │   ├── devcontainer.json
│   │   ├── docker-compose.yml
│   │   └── Dockerfile
│   ├── pg-init-scripts/
│   │   └── create-multiple-postgresql-databases.sh
│   └── README.md
├── python-3_14/                       # Python 3.14
│   ├── .devcontainer/
│   │   ├── devcontainer.json
│   │   └── Dockerfile
│   └── README.md
├── playwright-ts/                     # Playwright TypeScript
│   ├── .devcontainer/
│   │   ├── devcontainer.json
│   │   └── Dockerfile
│   ├── playwright.config.ts
│   └── README.md
└── nodejs-express/                    # Example: Future addition
    ├── .devcontainer/
    │   └── devcontainer.json
    └── README.md
```

## 🛠️ Customization

Each dev container can be customized to fit your specific needs:

### Adding Extensions

Edit the `devcontainer.json` file:

```json
"customizations": {
  "vscode": {
    "extensions": [
      "existing.extension",
      "your.new-extension"
    ]
  }
}
```

### Installing Additional Packages

Modify the `postCreateCommand` in `devcontainer.json`:

```json
"postCreateCommand": "npm install && npm install -g your-package"
```

### Changing Base Image

Update the `image` field:

```json
"image": "mcr.microsoft.com/devcontainers/your-preferred-image"
```

## 🤝 Contributing

Contributions are welcome! If you have a dev container configuration you'd like to share:

### Contribution Guidelines

1. **Fork** this repository
2. **Create a new folder** for your dev container: `technology-name/`
3. **Add** your `.devcontainer/devcontainer.json` configuration
4. **Write a README.md** following the existing format (see any existing container for reference)
5. **Update** the main README.md table with your contribution
6. **Submit** a pull request

### Quality Standards

Your contribution should include:

- ✅ A complete and tested `devcontainer.json` configuration
- ✅ A comprehensive README.md with setup instructions
- ✅ All necessary dependencies pre-installed
- ✅ Relevant VS Code extensions configured
- ✅ Clear documentation of any required API keys or secrets
- ✅ Example project structure (optional but recommended)

## 📚 Resources

### Dev Containers Documentation
- [Official Dev Containers Documentation](https://code.visualstudio.com/docs/devcontainers/containers)
- [Dev Container Specification](https://containers.dev/)
- [Dev Containers GitHub Repository](https://github.com/devcontainers)

### Docker Resources
- [Docker Documentation](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)

### VS Code Resources
- [VS Code Remote Development](https://code.visualstudio.com/docs/remote/remote-overview)
- [VS Code Extension Marketplace](https://marketplace.visualstudio.com/)

## 🐛 Troubleshooting

### Common Issues

**Container fails to build**
- Ensure Docker Desktop is running
- Try rebuilding: `Dev Containers: Rebuild Container`
- Check Docker logs for specific errors

**Extensions not installing**
- Verify extension IDs are correct
- Check internet connection
- Some extensions may require manual installation

**Port conflicts**
- Check if ports are already in use on your host machine
- Modify port mappings in `devcontainer.json`

**Performance issues**
- Allocate more resources to Docker Desktop
- Enable file sharing for your project directory
- Use volume mounts for better performance

## 📄 License

This repository and all dev container configurations are available under the MIT License. See individual folders for specific license information if applicable.

## ⭐ Show Your Support

If you find this collection helpful, please consider:
- Giving it a ⭐ star on GitHub
- Sharing it with your team
- Contributing your own dev containers

## 📬 Contact

Have questions or suggestions? Feel free to:
- Open an issue
- Submit a pull request
- Start a discussion

---

**Happy Coding!** 🎉