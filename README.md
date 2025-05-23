# MongoDB Atlas Architecture Center Go SDK Code Examples

This repository contains [Atlas Go SDK](https://www.mongodb.com/docs/atlas/sdk/)
code examples that follow recommendations in MongoDB's official
[Atlas Architecture Center documentation](https://www.mongodb.com/docs/atlas/architecture/current/).
You can run, download, and modify these code examples as starting points for
configuring your MongoDB Atlas architecture for your use case.

We will be adding code examples to this repository d
This repository will grow alongside the Architecture Center

## Project Overview
Examples are organized into three main categories:
- **Logs**: Examples for fetching and processing logs from MongoDB Atlas.
- **Metrics**: Examples for fetching and processing metrics from MongoDB Atlas.

### Authentication
The project authenticates using OAuth2.0 with the Client Credentials flow
through service accounts. To learn how to create a service account, see [Service Account Overview]().

We recommend using service accounts when possible. However, you can modify the client to use Digest authentication with API keys
(e.g. `UseDigestAuth(apiKey, apiSecret)`).

For more information, see
[Guidance for Atlas Authorization and Authentication: Service accounts](https://www.mongodb.com/docs/atlas/architecture/current/auth/#service-accounts)
in the Atlas Architecture Center documentation.

### Project Structure

```text
.
├── cmd                             # Runnable examples
│   ├── get_logs/main.go
│   ├── get_metrics_disk/main.go
│   └── get_metrics_process/main.go
│
├── configs                         # Atlas configurations
│   └── config.json
│
├── internal
│   ├── auth/client.go
│   ├── logs
│   │   ├── fetch.go
│   │   ├── file.go
│   │   └── gzip.go
│   ├── metrics
│   │   ├── disk.go
│   │   └─ process.go
│   └── utils.go
|
├── go.mod
├── go.sum
├── .gitignore
└── .env.example                    # Example secrets file
```

## Getting Started

### Prerequisites

- The MongoDB Atlas Go SDK
- Your Atlas project ID,
- Service Account with <permissions>

### Set up
1. Clone the repository:

   ```bash
   git clone https://github.com/mongodb/atlas-architecture-go-sdk.git
   ```

2. Create a `.env` file in the root directory of the project, and set your
    MongoDB Atlas service account ID and secret to the following environment variables:

    ```env
    MONGODB_ATLAS_SERVICE_ACCOUNT_ID=your_mdb_service_account_id
    MONGODB_ATLAS_SERVICE_ACCOUNT_SECRET=your_mdb_service_account_secret
    ```

    > **NOTE:** For simplicity and ease of demonstration, this project uses a
    > `.env` file to store credentials.
    >
    > In a production environment, you would most likely use a third-party
    > secrets manager such as HashiCorp Vault or AWS Secrets Manager. For more
    > information, see the [Guidance for Atlas Authorization and Authentication:
    > Secrets
    > management](https://www.mongodb.com/docs/atlas/architecture/current/auth/#secrets-management)
    > in the Atlas Architecture Center documentation.

3. Update the `configs/config.json` with the details for your
   Atlas project:

   ```json
    {
    "MONGODB_ATLAS_BASE_URL": "<your-non-default-base-url>",
    "ATLAS_ORG_ID": "<your-organization-id>",
    "ATLAS_PROJECT_ID": "<your-project-id>",
    "ATLAS_CLUSTER_NAME": "<clusterName>",
    "ATLAS_PROCESS_ID": "<clusterName-shard-00-00.hostSuffix.mongodb.net:port>"
    }
   ```

    > **NOTE:** If `MONGODB_ATLAS_BASE_URL` is omitted, the client automatically
    > defaults to `"https://cloud.mongodb.com"`.

    You can also modify the code to get these values programmatically. For an example, see
    [basic.go](https://github.com/mongodb/atlas-sdk-go/blob/be5f52fcb198f286111121790911ea37c7cebed3/examples/basic/basic.go#L30-L48)
    in the `atlas-go-sdk` documentation.

4. Install the project dependencies:
    ```bash
    go mod tidy
    ```

## Running Examples

The runnable examples are available in the `/cmd` directory. Examples run based
on the currently configured variables. You can modify the code to customize these examples according to your needs.

- To fetch logs:

    ```bash
    go run cmd/get_logs/main.go
    ```

    The compressed `.gz` and unzipped `.txt` logs save to `./logs`.

- To fetch metrics:
    ```bash
    go run cmd/get_metrics_disk/main.go
    ```

    or
    ```bash
    go run cmd/get_metrics_process/main.go
    ```

    Metrics output displays to the console. You can modify the code to save the output to a file or another destination as needed.



## License

This project is licensed under the [Apache 2.0 License](https://www.apache.org/licenses/LICENSE-2.0).

## Issues

To report an issue with any of these code examples, please leave feedback
through the corresponding documentation page in the
[MongoDB Atlas Architecture Center](https://www.mongodb.com/docs/atlas/architecture/current/).
Using the `Rate This Page` button, you can add a comment about the issue after
leaving a star rating.

## Contributing

We are not currently accepting public contributions to this repository at this
time.