# OpenBook Cranker v2 - Kubernetes Deployment

This repository contains the Kubernetes deployment configuration for the OpenBook Cranker v2 application. The deployment is designed to run the OpenBook Cranker v2 application in a production environment on a Kubernetes cluster.

## Description

The provided YAML file is a Kubernetes Deployment configuration. This deployment manages a single replica of the OpenBook Cranker v2 application within the `production` namespace. The application is containerized using an image from the GitHub Container Registry, and it is configured with various environment variables, some of which are securely stored in Kubernetes Secrets.

### Key Components

- **apiVersion**: `apps/v1` - Specifies the API version used for the Deployment.
- **kind**: `Deployment` - Indicates that this YAML file defines a Kubernetes Deployment.
- **metadata**: Contains metadata for the deployment, including the name (`openbook-cranker-v2-test`) and namespace (`production`).
- **spec**:
  - **replicas**: Set to `1`, indicating that only one replica of the pod will be running.
  - **selector**: Matches the label `app: openbook-cranker` to identify the pod.
  - **template**:
    - **metadata**: Labels the pod with `app: openbook-cranker`.
    - **spec**:
      - **containers**: Defines the container within the pod:
        - **name**: `openbook-cranker`
        - **image**: `ghcr.io/thedefiquant/openbook-cranker-v2:v2.0.1`
        - **env**: Lists environment variables required by the application, including:
          - `KEYPAIR` and `RPC_URL`: Values fetched from Kubernetes Secrets.
          - `PROGRAM_ID`, `INTERVAL`, `CONSUME_EVENTS_LIMIT`, `CLUSTER`, `MARKETS`, `PRIORITY_MARKETS`, `PRIORITY_QUEUE_LIMIT`, `PRIORITY_CU_PRICE`, `PRIORITY_CU_LIMIT`, `MAX_TX_INSTRUCTIONS`, and `CU_PRICE`: Static values configured directly in the YAML.
        - **ports**: Exposes port `80` for the container.

## Deployment

To deploy this configuration to your Kubernetes cluster, use the following command:

```bash
kubectl apply -f openbook-cranker-v2-deployment.yaml
