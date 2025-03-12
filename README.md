# Laravel Docker Project

This project demonstrates how to set up a Laravel application with Docker. Below are the services and tools used in this setup.

## Services Used

### 1. **Laravel Application (`app` service)**
   - **Purpose**: Runs the Laravel application in a PHP-FPM container.
   - **Build Context**: The Docker container is built from the `Dockerfile` located inside the `./laravel-app` folder.
   - **Ports**: Exposes port `9000` on the host machine, mapping it to port `9000` in the container.
   - **Depends on**: Relies on the `db` service (PostgreSQL database).

### 2. **Queue Worker (`queue-worker` service)**
   - **Purpose**: Runs the Laravel queue worker to process background jobs.
   - **Build Context**: Built from the same Dockerfile as the Laravel app.
   - **Command**: Executes `php artisan queue:work` to process queued jobs.
   - **Depends on**: Relies on the `db` service.

### 3. **Caddy Web Server (`caddy` service)**
   - **Purpose**: Serves the Laravel application with automatic SSL using Caddy server.
   - **Image**: Uses the `caddy:latest` image from Docker Hub.
   - **Ports**: Exposes ports `80` (HTTP) and `443` (HTTPS) for web access.
   - **Volumes**: Mounts the Laravel app directory to `/var/www/html` inside the container and includes a `Caddyfile` for configuration.
   - **Depends on**: Relies on the `app` service to serve the application.

### 4. **PostgreSQL Database (`db` service)**
   - **Purpose**: A PostgreSQL database for storing the application’s data.
   - **Image**: Uses the `bitnami/postgresql:16.3.0` image from Docker Hub.
   - **Ports**: Exposes port `5432` for database connections.
   - **Volumes**: Stores database data persistently using a Docker volume (`db-data`).
   - **Environment Variables**: Configured with the database name, username, and password using environment variables.

### 5. **Redis Cache (`redis` service)**
   - **Purpose**: A Redis service for caching to speed up the application.
   - **Image**: Uses the `bitnami/redis:7.2` image from Docker Hub.
   - **Ports**: Exposes port `6379` for Redis connections.
   - **Volumes**: Stores Redis data persistently using a Docker volume (`redis-data`).
   - **Environment Variables**: Configured with a Redis password and restrictions on specific Redis commands.

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

---

This setup demonstrates how to deploy a Laravel application with all the necessary services (database, caching, and web server) using Docker containers, ensuring that all services are isolated, easy to configure, and easy to deploy.
