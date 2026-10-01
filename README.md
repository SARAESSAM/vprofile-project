# VProfile - Multi-Tier Java Application with Docker Compose

A containerized multi-tier Java web application deployed using Docker Compose.

## Project Overview

This project demonstrates how to containerize and run a multi-tier Java application using Docker and Docker Compose.

The application consists of:

* Nginx - Web server and reverse proxy
* Apache Tomcat - Java application server
* MySQL - Relational database
* Memcached - Caching service
* RabbitMQ - Message broker

## Architecture

```text
                    Browser
                       |
                       v
                +--------------+
                |    Nginx     |
                |     :80      |
                +------+-------+
                       |
                       v
                +--------------+
                |    Tomcat    |
                | Java 17 /    |
                | Tomcat 10.1  |
                +------+-------+
                       |
          +------------+------------+
          |            |            |
          v            v            v
      +-------+   +----------+  +----------+
      | MySQL |   | Memcached|  | RabbitMQ |
      | db01  |   |   mc01   |  |   rmq01  |
      +-------+   +----------+  +----------+
```

All services communicate through a Docker Compose network.

## Technologies

* Java 17
* Spring MVC
* Spring Security
* Spring Data JPA
* Maven
* JSP
* Apache Tomcat 10.1
* MySQL 8
* Memcached
* RabbitMQ
* Nginx
* Docker
* Docker Compose

## Project Structure

```text
vprofile-project/
├── src/
│   └── main/
│       └── resources/
│           └── db_backup.sql
├── nginx/
│   └── default.conf
├── Dockerfile
├── docker-compose.yml
├── pom.xml
├── Jenkinsfile
├── README.md
└── .gitignore
```

## Prerequisites

Install:

* Docker Desktop
* Git

The application image is built from the Maven-generated WAR file.

## Build the Application

From the project directory:

```bash
mvn clean package
```

This generates:

```text
target/vprofile-v2.war
```

The `target/` directory is excluded from Git using `.gitignore`.

## Run with Docker Compose

Build the application image:

```bash
docker compose build
```

Start all services:

```bash
docker compose up -d
```

Check the running containers:

```bash
docker compose ps
```

## Access the Application

Open:

```text
http://localhost/vprofile-v2
```

Nginx receives the request on port 80 and forwards it to the Tomcat application container.

## Database

The MySQL database is initialized automatically using:

```text
src/main/resources/db_backup.sql
```

The database configuration is:

```text
Database: accounts
Username: admin
Password: admin123
```

## Useful Docker Compose Commands

Stop the application:

```bash
docker compose down
```

View logs:

```bash
docker compose logs
```

View logs for a specific service:

```bash
docker compose logs app01
```

Restart the stack:

```bash
docker compose restart
```

Rebuild the application image:

```bash
docker compose build app01
```

## What This Project Demonstrates

* Containerizing a Java web application
* Building a custom Docker image for Tomcat and Java
* Running multiple application tiers with Docker Compose
* Creating inter-container communication using Docker networks
* Initializing MySQL from a database dump
* Using Memcached as a caching service
* Using RabbitMQ as a message broker
* Configuring Nginx as a reverse proxy
* Managing a multi-container application lifecycle with Docker Compose


