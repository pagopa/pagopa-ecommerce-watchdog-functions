# pagopa-ecommerce-watchdog-functions [BETA]

## Description

**Pagopa Ecommerce Watchdog** is an application built with **Azure Functions** using **Java**. It is designed to monitor e-commerce transactions in real-time and identify any inconsistencies in transaction states. This tool is currently in **beta version** and serves as a prototype for experimenting with and analyzing transactions that may be in an inconsistent state.

The main objective is to ensure e-commerce transactions are processed correctly by identifying potential issues and triggering alerts for necessary actions.

## Features

- Real-time monitoring of e-commerce transactions.
- Detection of inconsistent transaction states.
- Automated logging and alerting for potential issues.
- Configurable alerts and logging mechanisms.
- Extensible design for future enhancements.

## Installation

### Prerequisites

Before you begin, make sure you have the following tools installed:

- **[Java Development Kit (JDK) 11+](https://adoptopenjdk.net/)** (required to run Azure Functions with Java)
- **[Maven](https://maven.apache.org/)** (for building the project)
- **[Azure Functions Core Tools](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local)** (for local development and testing)
- **[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)** (for Azure deployment)
- **[Visual Studio Code](https://code.visualstudio.com/)** or your preferred IDE
- **[Azure Functions for Java](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-java)** (Java runtime for Azure Functions)

### Clone the Repository

```bash
git clone https://github.com/your-username/pagopa-ecommerce-watchdog-functions.git
cd pagopa-ecommerce-watchdog-functions
```

### Install Dependencies
The project uses Maven for dependency management. Run the following command to download the required dependencies:

```bash
mvn clean install
Configure Azure Functions
Create the necessary Azure Function configurations (e.g., connection strings, API keys) in local.settings.json for local development. For example:
```

```json
{
  "IsEncrypted": false,
  "Values": {
    "FUNCTIONS_WORKER_RUNTIME": "java",
    "AzureWebJobsStorage": "<your-storage-connection-string>",
    "YourApiKey": "<your-api-key>"
  }
}
```

### Run the Function Locally
You can test the function locally using the Azure Functions Core Tools. Run the following command to start the function:

```bash
mvn azure-functions:run
This will start the Azure Function locally, and you can test it with HTTP requests or other configured triggers.
```

### Deployment
To deploy the function to Azure, follow these steps:

Log in to your Azure account:


```bash
az login
```

### Deploy the function:

```bash
mvn azure-functions:deploy
```

Ensure that your Azure resources (e.g., Function App, Storage Account, etc.) are set up in your Azure account before deployment.

### Usage
Once the function is deployed, it will monitor e-commerce transactions and log any issues related to inconsistent states. It can be configured to send alerts via email, Slack, or other channels based on transaction failures or inconsistencies.

### Example Function Trigger
The function is triggered by events like HTTP requests or storage events. For example, an HTTP-triggered function could look like this:

```java
public class TransactionMonitorFunction {

    @FunctionName("TransactionMonitor")
    public void run(
        @HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}) HttpRequestMessage<Optional<String>> request,
        final ExecutionContext context
    ) {
        context.getLogger().info("Transaction Monitor triggered.");

        // Analyze transaction state and check for inconsistencies
        boolean isConsistent = checkTransactionConsistency();
        if (!isConsistent) {
            // Send alert or log issue
            context.getLogger().severe("Inconsistent transaction state detected!");
        }
    }
}
```

### Contributing
We welcome contributions to improve the functionality of this project. Please follow these steps to contribute:

### Fork the repository.
Create a new branch (git checkout -b feature-name).
Make your changes and commit (git commit -am 'Add new feature').
Push to your forked repository (git push origin feature-name).
Submit a pull request.

### Roadmap

- Beta Version 1.0: Core monitoring functionality and transaction logging.
- Beta Version 2.0: Integration with third-party services for enhanced monitoring (e.g., database consistency checks).
- Future Updates: Advanced alerting, transaction history tracking, and more.
