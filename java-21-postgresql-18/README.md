# Java 21 & PostgreSQL 18 Development Container

A complete development environment for Java applications with PostgreSQL database support, containerized for Visual Studio Code using Docker Compose.

## 🎯 Purpose

This dev container is designed for:

- Java 21 application development
- Backend services with PostgreSQL databases
- Microservices development
- Spring Boot, Quarkus, or other Java frameworks
- Database-driven application development

## 🛠️ Included Tools & Features

### Java Development

- **Java 21 JDK**: Latest LTS Java Development Kit
- **Gradle**: Modern build automation tool (installed via SDKMAN)
- **Maven**: Available for installation via SDKMAN
- **SDKMAN**: SDK manager for Java ecosystem tools

### Database

- **PostgreSQL 18.1**: Latest PostgreSQL database server
- **PostgreSQL Client**: Pre-installed `psql` command-line client
- **Multiple Databases**: Automatic creation of `dev` and `staging` databases
- **Init Scripts**: Custom initialization scripts support

### DevOps & Cloud Tools

- **Azure CLI**: Azure cloud management
- **Azure Developer CLI (azd)**: Azure development workflows
- **AWS CLI**: Amazon Web Services management
- **Docker**: Container management from within the dev container
- **curl & wget**: HTTP clients for API testing
- **jq**: JSON processor for command-line operations
- **pigz**: Parallel gzip for faster compression

### Utilities

- **Git**: Version control
- **zip/unzip**: Archive management

## 🗄️ Database Configuration

### Default Credentials

| Property | Value |
|----------|-------|
| **Host** | `postgresql18` (from app container) or `localhost` (from host) |
| **Port** | `5432` |
| **Username** | `admin` |
| **Password** | `admin` |
| **Databases** | `dev`, `staging` |

### Connecting from Java Application

```java
// JDBC URL (from within the container)
String jdbcUrl = "jdbc:postgresql://postgresql18:5432/dev";
String username = "admin";
String password = "admin";
```

### Connecting with psql

```bash
# From within the dev container
psql -h postgresql18 -U admin -d dev

# From host machine (when container is running)
psql -h localhost -p 5432 -U admin -d dev
```

### Environment Variables

The following environment variables are available in the app container:

| Variable | Value |
|----------|-------|
| `POSTGRES_USER` | `admin` |
| `POSTGRES_PASSWORD` | `admin` |
| `POSTGRES_HOSTNAME` | `postgresql18` |
| `POSTGRES_PORT` | `5432` |
| `POSTGRES_MULTIPLE_DATABASES` | `dev,staging` |

## 🚀 Getting Started

### Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Setup Instructions

1. **Clone or create your project**
   ```bash
   mkdir my-java-project
   cd my-java-project
   ```

2. **Add the dev container configuration**
   - Copy the `.devcontainer` folder to your project root
   - Copy the `pg-init-scripts` folder for database initialization

3. **Open in VS Code**
   ```bash
   code .
   ```

4. **Reopen in Container**
   - Press `F1` or `Ctrl+Shift+P` (Windows/Linux) / `Cmd+Shift+P` (Mac)
   - Select: `Dev Containers: Reopen in Container`
   - Wait for the containers to build and start

5. **Verify the setup**
   ```bash
   java -version
   gradle --version
   psql -h postgresql -U admin -d dev -c "SELECT version();"
   ```

## 💻 Usage Examples

### Create a New Gradle Project

```bash
# Create a new Java application
gradle init --type java-application

# Build the project
gradle build

# Run the application
gradle run
```

### Create a New Spring Boot Project

```bash
# Using Spring Initializr CLI (if installed)
spring init --dependencies=web,data-jpa,postgresql my-spring-app

# Or download from start.spring.io and extract
curl https://start.spring.io/starter.zip \
  -d dependencies=web,data-jpa,postgresql \
  -d javaVersion=21 \
  -d type=gradle-project \
  -o my-spring-app.zip
unzip my-spring-app.zip -d my-spring-app
```

### Database Operations

```bash
# Connect to dev database
psql -h postgresql18 -U admin -d dev

# Create a new table
psql -h postgresql18 -U admin -d dev -c "
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);"

# List all tables
psql -h postgresql18 -U admin -d dev -c "\dt"

# Switch to staging database
psql -h postgresql18 -U admin -d staging
```

### Using Azure CLI

```bash
# Login to Azure
az login

# List subscriptions
az account list

# Deploy using Azure Developer CLI
azd init
azd up
```

### Using AWS CLI

```bash
# Configure AWS credentials
aws configure

# List S3 buckets
aws s3 ls
```

## 🏗️ Project Structure

Recommended folder structure for your Java project:

```
my-java-project/
├── .devcontainer/
│   ├── devcontainer.json
│   ├── docker-compose.yml
│   └── Dockerfile
├── pg-init-scripts/
│   └── create-multiple-postgresql-databases.sh
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/example/
│   │   │       └── Application.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       └── java/
│           └── com/example/
│               └── ApplicationTest.java
├── build.gradle
├── settings.gradle
└── README.md
```

## ⚙️ Configuration

### Application Properties (Spring Boot)

```properties
# src/main/resources/application.properties
spring.datasource.url=jdbc:postgresql://postgresql18:5432/dev
spring.datasource.username=admin
spring.datasource.password=admin
spring.datasource.driver-class-name=org.postgresql.Driver

spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
```

### Gradle Configuration

```groovy
// build.gradle
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.2.0'
    id 'io.spring.dependency-management' version '1.1.4'
}

java {
    sourceCompatibility = '21'
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
    implementation 'org.springframework.boot:spring-boot-starter-web'
    runtimeOnly 'org.postgresql:postgresql'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
}
```

### Adding Additional Databases

Edit the `docker-compose.yml` file and update the `POSTGRES_MULTIPLE_DATABASES` variable:

```yaml
environment:
  - POSTGRES_MULTIPLE_DATABASES=dev,staging,production,test
```

Then rebuild the container.

## 🔧 Customization

### Installing Additional Java Tools via SDKMAN

```bash
# Install specific Maven version
sdk install maven 3.9.6

# Install specific Gradle version
sdk install gradle 8.5

# List available Java versions
sdk list java

# Install a different Java version
sdk install java 17.0.9-tem
```

### Adding More VS Code Extensions

Edit `.devcontainer/devcontainer.json` and add to the customizations section:

```json
"customizations": {
  "vscode": {
    "extensions": [
      "vscjava.vscode-java-pack",
      "pivotal.vscode-spring-boot"
    ]
  }
}
```

### Mounting Docker Socket

The container is configured to mount the Docker socket, allowing you to run Docker commands from within the container:

```bash
# List running containers
docker ps

# Build and run other containers
docker build -t my-image .
docker run my-image
```

## 🐛 Troubleshooting

### Container won't start
- Ensure Docker Desktop is running
- Check if port 5432 is already in use on your host
- Try rebuilding: `Dev Containers: Rebuild Container`

### Cannot connect to PostgreSQL
- Wait a few seconds after container startup for PostgreSQL to initialize
- Verify PostgreSQL is running: `docker ps | grep postgresql`
- Check logs: `docker logs postgresql18`

### Database not created
- Check initialization scripts in `pg-init-scripts/`
- Ensure scripts have execute permissions
- View PostgreSQL logs for errors

### Java version issues
- Verify Java version: `java -version`
- Use SDKMAN to install different versions: `sdk list java`

### Gradle/Maven not found
- Gradle is installed via SDKMAN by default
- Run `source ~/.sdkman/bin/sdkman-init.sh` to refresh
- Or install manually: `sdk install gradle`

### Docker commands not working
- Ensure the Docker socket is mounted
- Check Docker group membership: `groups`
- Verify Docker is running on host

## 📚 Additional Resources

### Java Documentation
- [Java 21 Documentation](https://docs.oracle.com/en/java/javase/21/)
- [Gradle User Manual](https://docs.gradle.org/current/userguide/userguide.html)
- [Maven Documentation](https://maven.apache.org/guides/)

### PostgreSQL Documentation
- [PostgreSQL Documentation](https://www.postgresql.org/docs/18/)
- [JDBC PostgreSQL Driver](https://jdbc.postgresql.org/documentation/)

### Spring Boot
- [Spring Boot Reference](https://docs.spring.io/spring-boot/docs/current/reference/html/)
- [Spring Data JPA](https://spring.io/projects/spring-data-jpa)

### Cloud CLI Tools
- [Azure CLI Documentation](https://learn.microsoft.com/en-us/cli/azure/)
- [AWS CLI Documentation](https://docs.aws.amazon.com/cli/)

## 🤝 Contributing

Suggestions for additional tools or improvements are welcome! Consider adding:
- Additional Java frameworks support
- Database management UI tools
- Testing frameworks
- CI/CD integration examples

## 📄 License

This dev container configuration is available under the MIT License.

---

**Happy Coding!** ☕🐘
