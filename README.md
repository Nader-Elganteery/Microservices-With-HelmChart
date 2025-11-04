# Microservices with Helm Chart

Deploying the Google Cloud Microservices Demo Application using Helm Chart for simplified Kubernetes deployment and management.

## About

This repository contains Helm Chart configurations for deploying the [Online Boutique](https://github.com/GoogleCloudPlatform/microservices-demo) microservices demo application. Online Boutique is a cloud-native microservices demo application consisting of 11 microservices that simulate an e-commerce platform.

![Online Boutique Homepage](https://raw.githubusercontent.com/GoogleCloudPlatform/microservices-demo/main/docs/img/online-boutique-frontend-1.png)

*Screenshot of the Online Boutique application homepage*

## Architecture

![Architecture Diagram](https://raw.githubusercontent.com/GoogleCloudPlatform/microservices-demo/main/docs/img/architecture-diagram.png)

*Microservices architecture showing service communication via gRPC*

The application consists of the following microservices:

| Service | Language | Description |
|---------|----------|-------------|
| **frontend** | Go | Exposes an HTTP server to serve the website |
| **cartservice** | C# | Stores the items in the user's shopping cart in Redis |
| **productcatalogservice** | Go | Provides the list of products from a JSON file |
| **currencyservice** | Node.js | Converts one currency to another |
| **paymentservice** | Node.js | Charges the given credit card with the given amount |
| **shippingservice** | Go | Gives shipping cost estimates based on the shopping cart |
| **emailservice** | Python | Sends users an order confirmation email |
| **checkoutservice** | Go | Retrieves user cart, prepares order and orchestrates payment |
| **recommendationservice** | Python | Recommends other products based on what's in the cart |
| **adservice** | Java | Provides text ads based on given context words |
| **loadgenerator** | Python/Locust | Continuously sends requests imitating realistic user shopping flows |

## Prerequisites

- Kubernetes cluster (GKE, Minikube, Kind, or any other)
- `kubectl` configured to communicate with your cluster
- Helm installed
- helmfile installed

## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/Nader-Elganteery/Microservices-With-HelmChart.git
cd Microservices-With-HelmChart
```

### 2. Deploy using Helm

```bash
# Install the chart
helmfile sync
```

### 3. Verify Deployment

```bash
# Check if all pods are running
kubectl get pods

# Check services
kubectl get services
```

### 4. Access the Application

```bash
# Get the frontend 
kubectl port-forward deployment/frontend 4450:8080
```

## Configuration

You can customize the deployment by modifying the `values.yaml` file or by providing your own values during installation or deploy one service:

```bash
helm install -f values/email-service-values.yaml emailservice  charts/microservice
```

## Uninstallation

To remove the application:

```bash
helmfile destroy
```

## Advantages of Using Helm

- **Simplified Deployment**: Deploy all 11 microservices with a single command
- **Version Control**: Easy rollback to previous versions
- **Configuration Management**: Centralized configuration through values.yaml
- **Reusability**: Easy to deploy multiple instances with different configurations
- **Maintenance**: Simplified updates and upgrades

## Reference

This project is based on the [Google Cloud Platform Microservices Demo](https://github.com/GoogleCloudPlatform/microservices-demo).

## License

This project follows the same license as the original Google Cloud Platform microservices-demo repository.
