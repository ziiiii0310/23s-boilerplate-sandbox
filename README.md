# MySQL + Flask Boilerplate Project

This repo contains a boilerplate setup for spinning up 3 Docker containers: 
1. A MySQL 8 container for obvious reasons
1. A Python Flask container to implement a REST API
1. A Local AppSmith Server

## How to setup and start the containers
**Important** - you need Docker Desktop installed

1. Clone this repository.  
1. Create a file named `db_root_password.txt` in the `secrets/` folder and put inside of it the root password for MySQL. 
1. Create a file named `db_password.txt` in the `secrets/` folder and put inside of it the password you want to use for the a non-root user named webapp. 
1. In a terminal or command prompt, navigate to the folder with the `docker-compose.yml` file.  
1. Build the images with `docker compose build`
1. Start the containers with `docker compose up`.  To run in detached mode, run `docker compose up -d`. 



# MySQL + Flask Boilerplate Project

A modern, containerized web application boilerplate that combines the power of MySQL 8, Flask REST API, and AppSmith for rapid application development.

## Project Overview

This project provides a production-ready foundation for building web applications with the following key features:

- **MySQL 8 Database**: Robust and scalable database solution
- **Flask REST API**: Python-based backend with RESTful architecture
- **AppSmith Integration**: Low-code platform for building admin dashboards and user interfaces
- **Docker Containerization**: Easy deployment and development environment setup

## Architecture

The project is structured as three main components:

1. **MySQL Container**
   - MySQL 8.0
   - Configurable root and application user credentials
   - Persistent data storage
   - Optimized for production use

2. **Flask API Container**
   - Python-based REST API
   - Built with Flask framework
   - Ready for API development
   - Includes basic security configurations

3. **AppSmith Container**
   - Local development server
   - Pre-configured for database connection
   - Ready for UI development

## Quick Start
**Prerequisites**: Docker Desktop must be installed

1. Clone this repository
2. Set up database credentials:
   - Create `secrets/db_root_password.txt` with MySQL root password
   - Create `secrets/db_password.txt` with password for webapp user
3. Build and start containers:
   ```bash
   docker compose build
   docker compose up        # Run in foreground
   # OR
   docker compose up -d    # Run in detached mode
   ``` 
--卢冬华贡献--
##周玉涛##
# Installation and Deployment Guide

This guide will walk you through the process of setting up and deploying the application using Docker. Our application consists of two main services:
- A Flask web application
- A MySQL database

## Prerequisites

Before you begin, make sure you have the following installed on your system:
- Docker (version 20.10.0 or higher)
- Docker Compose (version 2.0.0 or higher)
- Git

## Quick Start

1. Clone the repository:
```bash
git clone <repository-url>
cd <repository-name>
```

2. Set up the secrets:
```bash
# Create a secrets directory
mkdir -p secrets

# Create password files for MySQL
echo "your_db_password" > secrets/db_password.txt
echo "your_db_root_password" > secrets/db_root_password.txt

# Set proper permissions
chmod 600 secrets/db_password.txt secrets/db_root_password.txt
```

3. Start the application:
```bash
docker-compose up -d
```

The application will be available at:
- Web Application: http://localhost:8001
- Database: localhost:3200

## Detailed Configuration

### Environment Setup

The application uses the following port mappings:
- Flask Application: `8001:4000`
- MySQL Database: `3200:3306`

### Database Configuration

The MySQL database is configured with:
- Default user: `webapp`
- Password: Stored in `secrets/db_password.txt`
- Root password: Stored in `secrets/db_root_password.txt`

### Volume Mounts

The application uses the following volume mounts:
- `./flask-app:/code`: Flask application code
- `./secrets:/secrets`: Secret files
- `./db:/docker-entrypoint-initdb.d/`: Database initialization scripts

## Development Setup

For development purposes, the Flask application code is mounted as a volume, allowing for real-time code changes without rebuilding the container.

1. Make changes to the Flask application code in the `flask-app` directory
2. The changes will be reflected immediately (may require a browser refresh)

## Maintenance

### Viewing Logs

To view service logs:
```bash
# All services
docker-compose logs

# Specific service
docker-compose logs web  # For Flask app
docker-compose logs db   # For database
```

### Stopping the Application

To stop the application:
```bash
docker-compose down
```

### Rebuilding Services

If you make changes to the Dockerfile or need to rebuild the services:
```bash
docker-compose build
docker-compose up -d
```

## Troubleshooting

### Common Issues

1. **Port Conflicts**
   - Error: "port is already allocated"
   - Solution: Check if another service is using ports 8001 or 3200
   ```bash
   # On Linux/Mac
   sudo lsof -i :8001
   sudo lsof -i :3200
   ```

2. **Database Connection Issues**
   - Ensure the secret files contain valid passwords
   - Check if the database container is running:
   ```bash
   docker-compose ps
   ```

3. **Permission Issues**
   - Ensure proper permissions on the secrets directory:
   ```bash
   chmod -R 600 secrets/
   ```

### Health Check

To verify all services are running properly:
```bash
docker-compose ps
```

All services should show status as "Up".

## Security Notes

1. Never commit the `secrets` directory to version control
2. Always use secure passwords in production
3. Change default database credentials in production environments
4. Consider using environment variables for sensitive configuration in production

## Production Deployment

For production deployment, additional considerations are required:

1. Use proper SSL/TLS certificates
2. Configure proper firewall rules
3. Set up monitoring and logging
4. Use production-grade database configurations
5. Implement proper backup strategies

Please refer to the production deployment guide for detailed instructions.

