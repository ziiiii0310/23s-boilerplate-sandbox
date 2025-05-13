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

## How to setup and start the containers
**Important** - you need Docker Desktop installed

1. Clone this repository.  
1. Create a file named `db_root_password.txt` in the `secrets/` folder and put inside of it the root password for MySQL. 
1. Create a file named `db_password.txt` in the `secrets/` folder and put inside of it the password you want to use for the a non-root user named webapp. 
1. In a terminal or command prompt, navigate to the folder with the `docker-compose.yml` file.  
1. Build the images with `docker compose build`
1. Start the containers with `docker compose up`.  To run in detached mode, run `docker compose up -d`. 
--卢冬华贡献--