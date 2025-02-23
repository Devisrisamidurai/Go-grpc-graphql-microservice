# Go-grpc-graphql-microservice

A scalable and modular microservice-based application built with **Go**, **gRPC**, and **GraphQL**. This project demonstrates how to integrate multiple services using gRPC while exposing a unified GraphQL API Gateway for easy querying.

## Overview
This project consists of three independent microservices:

1. **Account Service** - Manages user accounts.
2. **Catalog Service** - Handles product listings (uses Elasticsearch for storage).
3. **Order Service** - Processes orders (linked to PostgreSQL).
4. **GraphQL API Gateway** - Provides a single access point to interact with all services.

## Features
✔️ Microservices architecture with gRPC communication  
✔️ GraphQL API for querying and mutations  
✔️ PostgreSQL and Elasticsearch for data storage  
✔️ Docker Compose setup for easy deployment  
✔️ Modular and scalable design  

## Getting Started
### 1. Clone the Repository
```sh
git clone https://github.com/Devisrisamidurai/Go-grpc-graphql-microservice.git
cd Go-grpc-graphql-microservice
```

### 2. Run the Services with Docker
Ensure you have **Docker** and **Docker Compose** installed, then start the services:
```sh
docker-compose up -d --build
```

### 3. Access the GraphQL Playground
Once the services are up, visit:  
➡ **http://localhost:8000/playground**

## Example GraphQL Queries
### Fetch All Accounts
```graphql
query {
  accounts {
    id
    name
  }
}
```
### Create a New Account
```graphql
mutation {
  createAccount(account: {name: "John Doe"}) {
    id
    name
  }
}
```
### Retrieve Products with Filtering and Pagination
```graphql
query {
  products(pagination: {skip: 0, take: 10}, filter: "laptop") {
    id
    name
    price
  }
}
```
### Place an Order
```graphql
mutation {
  createOrder(order: {accountId: "123", products: [{id: "456", quantity: 2}]}) {
    id
    totalPrice
    products {
      name
      quantity
    }
  }
}
```
### Fetch Account Details with Order History
```graphql
query {
  account(id: "123") {
    name
    orders {
      id
      totalPrice
      products {
        name
        quantity
        price
      }
    }
  }
}
```

## Tech Stack
- **Go** - Core backend language
- **gRPC** - Service-to-service communication
- **GraphQL** - API Gateway for data querying
- **PostgreSQL** - Relational database for accounts and orders
- **Elasticsearch** - Search engine for products
- **Docker & Docker Compose** - Containerized deployment

## How It Works
1. **Frontend/Client** makes a GraphQL query.
2. **GraphQL API Gateway** routes the request to the appropriate gRPC service.
3. **gRPC Services** process the request and interact with their respective databases.
4. **Response** is returned to the client via the GraphQL Gateway.

## Contributing
Contributions are welcome! Feel free to fork the repository and submit a pull request.

## License
This project is open-source and available under the **MIT License**.

