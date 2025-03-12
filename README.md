# Laravel Docker Project

This project demonstrates how to set up a Laravel application with Docker. Below are the services and tools used in this setup.

## Services Used

### 1. **Laravel Application (`app` service)**
### 2. **Queue Worker (`queue-worker` service)**
### 3. **Caddy Web Server (`caddy` service)** 
### 4. **PostgreSQL Database (`db` service)**
### 5. **Redis Cache (`redis` service)**


## Key Docker Concepts Used

### **Docker Compose**
Docker Compose is used to define and run multi-container Docker applications. In this setup, Docker Compose is responsible for defining the multiple services (Laravel app, queue worker, Caddy server, PostgreSQL, and Redis) and how they interact with each other.

- **`docker-compose.yml`**: The configuration file that defines all the services, networks, and volumes for this setup.

### **Volumes**
Volumes in Docker are used to persist data across container restarts. In this setup:
- **`db-data`**: Used for storing PostgreSQL database data.
- **`redis-data`**: Used for storing Redis cache data.

### **Networks**
Docker networks allow containers to communicate with each other. In this setup:
- **`docker-network`**: A custom Docker network that allows the `app`, `queue-worker`, `caddy`, `db`, and `redis` containers to interact with each other.

### **Dockerfile**
- The Dockerfile is used to define the image for the Laravel app and queue worker services. It contains instructions for setting up the necessary environment, installing dependencies, and setting up the PHP environment for Laravel.

### **Caddyfile**
- A simple configuration file for the Caddy web server to define how the Laravel app is served and handle automatic SSL certificates.


