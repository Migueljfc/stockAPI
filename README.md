# Stock API 🧩

![Architecture](https://img.shields.io/badge/Architecture-Microservice-8A2BE2)
![Python Version](https://img.shields.io/badge/python-3.7%2B-blue.svg)
![FastAPI](https://img.shields.io/badge/FastAPI-005571?style=flat&logo=fastapi)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)

## Table of Contents
* [About](#about)
* [Features](#features)
* [Getting Started](#getting-started)
* [Usage](#usage)
* [Deployment](#deployment)
* [Documentation](#documentation)

## About
The **Stock API** is a dedicated microservice responsible for the inventory and stock management. It acts as a decoupled service that provides seamless management of products, categories, and subcategories, allowing other components of the system to interact with stock data efficiently and reliably.

## Features
* 🧩 **Microservice Architecture:** Independent, containerized, and highly scalable within the cluster.
* 📦 **Domain-Driven Design:** Strictly handles the bounded context of product and inventory management.
* 🐳 **Container Native:** Ready to run out-of-the-box with Docker and Kubernetes.
* ⚡ **High Performance:** Built with FastAPI for incredible speed and asynchronous RESTful communication.

## Getting Started
These instructions will get you a copy of the microservice up and running on your local machine for isolated development and testing. See [Deployment](#deployment) for notes on how to deploy it to the live cluster.

### Prerequisites
Ensure you have the following installed on your machine:
* Python 3.7+
* Docker & Docker Compose (V2)
* _Optional:_ MariaDB (if running outside of Docker)

### Environment Variables
For local development, ensure your database connection is properly configured. Create a `.env` file or export the following variables (update with your local credentials):
```env
DB_USER=root
DB_PASSWORD=secret
DB_HOST=db
```
### Installing 


```
sudo docker-compose build
```

## Usage <a name = "usage"></a>
```
sudo docker-compose up
```


## Deployment <a name = "deployment"></a> 

This instruction is to use in a private server so you probably don't have access to that, change the commands to your requisits.

```bash
#create the configmap for the stock database
kubectl create configmap mariadb-init-map -n egs-ressellr --from-file=./db/init.sql

# The rest of the deployment is done with the following commands

docker buildx build --platform linux/amd64 --network=host -t registry.deti:5000/egs-ressellr/stock:v3.1 -f Dockerfile.app .
docker push registry.deti:5000/egs-ressellr/stock:v3.1

kubectl apply -f db-deployment.yaml
kubectl apply -f app-deployment.yaml

#Delete deployment
kubectl delete -f db-deployment.yaml
kubectl delete -f app-deployment.yaml

# Get all the pods in the namespace
kubectl get pods -n egs-ressellr

# Get all the services in the namespace
kubectl get services -n egs-ressellr

```

## Documentation <a name = "documentation"></a>
<a href="https://app.swaggerhub.com/apis-docs/Resellr/StockAPI/1.0.0"> SwaggerHub</a>
