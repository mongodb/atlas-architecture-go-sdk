# MongoDB Atlas Architecture Center Go SDK Examples

This repository contains runnable examples demonstrating how to use the [Atlas Go SDK](https://www.mongodb.com/docs/atlas/sdk/) to interact with MongoDB Atlas. These examples support the best practices described in the [Atlas Architecture Center documentation](https://www.mongodb.com/docs/atlas/architecture/current/).

## Overview

This project provides ready-to-run Go code examples that demonstrate:

- Authentication with [service accounts](https://www.mongodb.com/docs/atlas/architecture/current/auth/#service-accounts)
- Retrieving and analyzing Atlas metrics
- Fetching and processing Atlas logs
- Managing Atlas resources programmatically

Use these examples as starting points for your own Atlas integration.

## Project Structure

```text
.
├── cmd                  # Runnable examples by category
│   ├── get_logs/main.go
│   ├── get_metrics_disk/main.go
│   └── get_metrics_process/main.go
├── configs              # Atlas configurations
│   └── config.json
├── internal             # Shared code
│   ├── auth/client.go
│   ├── logs/
│   ├── metrics/
│   └── utils.go
├── go.mod
├── go.sum
├── .gitignore           # Ignores .env file and /log output 
└── .env.example         # Example environment variables 
```

## Prerequisites

- Go 1.16 or later
- A MongoDB Atlas account with:
  - An Atlas project and cluster
  - Service account credentials with appropriate permissions

## Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/mongodb/atlas-architecture-go-sdk.git
   cd atlas-architecture-go-sdk
   ```

2. Create a `.env` file with your service account credentials:
   ```env
   MONGODB_ATLAS_SERVICE_ACCOUNT_ID=your_service_account_id
   MONGODB_ATLAS_SERVICE_ACCOUNT_SECRET=your_service_account_secret
   ```
   > **NOTE:** For production use, consider a secrets manager like HashiCorp Vault or AWS Secrets Manager instead of environment variables. See [Secrets management](https://www.mongodb.com/docs/atlas/architecture/current/auth/#secrets-management).

3. Update `configs/config.json` with your Atlas details:
   ```json
   {
     "MONGODB_ATLAS_BASE_URL": "<optional-non-default-base-url>",
     "ATLAS_ORG_ID": "<your-organization-id>",
     "ATLAS_PROJECT_ID": "<your-project-id>",
     "ATLAS_CLUSTER_NAME": "<your-cluster-name>",
     "ATLAS_PROCESS_ID": "<cluster-name-shard-00-00.hostsuffix.mongodb.net:port>"
   }
   ```
   > **NOTE:** The default base URL is `https://cloud.mongodb.com` if not specified.

4. Install dependencies:
   ```bash
   go mod tidy
   ```

## Running Examples

### Fetch Logs
```bash
go run cmd/get_logs/main.go
```
Logs save to the `./logs` directory as both `.gz` and uncompressed `.txt` files.

### Fetch Metrics
```bash
go run cmd/get_metrics_disk/main.go
# or
go run cmd/get_metrics_process/main.go
```
Metrics display in the console.

## Customizing Examples

Each example can be modified to suit your specific needs:
- Change time ranges for metrics or logs
- Add filtering parameters
- Save output to different formats
- Process data for analysis

## Issues

To report issues, please leave feedback through the corresponding [Atlas Architecture Center](https://www.mongodb.com/docs/atlas/architecture/current/) documentation page using the "Rate This Page" button.

## License

This project is licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0).