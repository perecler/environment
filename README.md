# Environment
Installation Files for Development Environment

Docker composer files for a Apache web server, with Mysql database and Phpmyadmin

# Docker Compose Configuration Summary

This Docker Compose configuration file, "docker-compose.yml," defines a multi-container setup for a web development environment. It includes the following services:

- **www (Web Service):**
  - Builds a web service container using the PHP 8.0 image with Apache.
  - Exposes port 80 on the host and maps it to port 80 in the container.
  - Mounts the local "./html" directory to "/var/www/html" in the container.
  - Links to the "db" service for database connectivity.
  - Connects to the "default" container network.

- **db (Database Service):**
  - Uses the MySQL 8.0 image to create a database container.
  - Exposes port 3306 on the host and maps it to port 3306 in the container.
  - Sets the default authentication plugin for MySQL.
  - Defines environment variables for the database name, user, and passwords.
  - Mounts the local "./dump" directory for initial data import and creates a "persistent" volume for persistent data storage.
  - Connects to the "default" container network.

- **phpMyAdmin:**
  - Utilizes the phpMyAdmin image for managing the database.
  - Links to the "db" service for database access.
  - Exposes port 8000 on the host, mapping it to port 80 in the container.
  - Configures environment variables for MySQL access.

The "volumes" section defines a volume named "persistent" for persistent data storage.

# Dockerfile Summary
The Dockerfile defines the instructions to build a custom container image. In this case:

1. It starts with the base image "php:8.0.0-apache."
2. Sets the "DEBIAN_FRONTEND" argument to "noninteractive" to prevent user interactions during package installation.
3. Installs the "mysqli" extension for PHP.
4. Updates the system and installs packages related to compression and necessary ZIP libraries.
5. Configures the "zip" extension for PHP.
6. Enables the Apache module "rewrite."

This Dockerfile prepares a container image with a PHP and Apache environment specifically configured for the "www" web service in the Docker Compose setup.
