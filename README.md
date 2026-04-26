# TaskMind - Discovery Service

## 📝 Overview
The **Discovery Service** acts as the centralized registry for the TaskMind microservices architecture. It enables **Service Discovery**, allowing individual microservices to find and communicate with each other seamlessly without relying on hardcoded hostnames or ports.

## 🚀 Key Responsibilities
* **Service Registration:** Automatically handling the registration of new microservice instances as they scale up.
* **Health Monitoring:** Performing continuous health checks to ensure that the API Gateway only routes traffic to "healthy" instances.
* **Service Registry:** Acting as the single source of truth for the network topology, enabling client-side load balancing.
* **High Availability:** Ensuring the system remains resilient by managing dynamic IP addresses and ports in a containerized environment.

## 🛠 Tech Stack
* **Language:** Java (OpenJDK 17+)
* **Framework:** Spring Cloud Netflix **Eureka Server** / Spring Boot
* **Containerization:** Docker
* **Port:** 8761 (Default Eureka Dashboard)

## 🏗 Architecture Context
The Discovery Service is the first component to start in the TaskMind ecosystem:
1.  **Registration:** When the *Task Service* or *AI Agent* starts, they "check-in" with the Discovery Service.
2.  **Lookup:** When the **API Gateway** needs to route a request, it asks the Discovery Service: *"Where can I find an active instance of the Task Service?"*
3.  **Dynamic Scaling:** If we spin up 3 instances of the *User Service*, the Discovery Service manages all of them automatically.

## 📊 Dashboard
Once running, the service registry dashboard can be accessed at:
`http://localhost:8761`

## 📦 Getting Started
To run the Discovery Service locally:

```bash
# Build the image
docker build -t taskmind-discovery-service .

# Run the container
docker run -p 8761:8761 taskmind-discovery-service
