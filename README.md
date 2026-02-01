# Development Services - Docker Compose

This repository contains a Docker Compose setup with common development services including databases, message queues, and observability tools.

## Prerequisites

- Docker installed
- Docker Compose installed

## Quick Start

Start all services:
```bash
docker-compose up -d
```

Stop all services:
```bash
docker-compose down
```

View logs:
```bash
docker-compose logs -f [service-name]
```

## Services Overview

- **MongoDB** - NoSQL Document Database (Port: 27017)
- **Redis** - In-Memory Cache/Database (Port: 6379)
- **SQL Server** - Relational Database (Port: 1433)
- **RabbitMQ** - Message Broker (Ports: 5672, 15672)
- **LavinMQ** - Alternative Message Broker (Ports: 5673, 15673)
- **OpenTelemetry LGTM** - Observability Stack (Ports: 3000, 4040, 4317, 4318, 9090)

---

## Individual Service Usage

### MongoDB

**Start only MongoDB:**
```bash
docker-compose up -d mongodb
```

**Access MongoDB:**
- Host: `localhost`
- Port: `27017`
- Username: `admin`
- Password: `SqlServer2019!`

**Connection String:**
```
mongodb://admin:SqlServer2019!@localhost:27017/
```

**Connection String with Database:**
```
mongodb://admin:SqlServer2019!@localhost:27017/your_database_name
```

**Connection String with Auth Database:**
```
mongodb://admin:SqlServer2019!@localhost:27017/your_database_name?authSource=admin
```

---

### Redis

**Start only Redis:**
```bash
docker-compose up -d redis
```

**Access Redis:**
- Host: `localhost`
- Port: `6379`
- Password: `SqlServer2019!`

**Connection String:**
```
redis://:SqlServer2019!@localhost:6379
```

**Connection String (Alternative Format):**
```
localhost:6379
```

---

### SQL Server

**Start only SQL Server:**
```bash
docker-compose up -d sqlserver
```

**Access SQL Server:**
- Host: `localhost`
- Port: `1433`
- Username: `sa`
- Password: `SqlServer2019!`

**Connection String (ADO.NET):**
```
Server=localhost,1433;Database=your_database_name;User Id=sa;Password=SqlServer2019!;TrustServerCertificate=True;
```

**Connection String (JDBC):**
```
jdbc:sqlserver://localhost:1433;databaseName=your_database_name;user=sa;password=SqlServer2019!;encrypt=false;
```

**Connection String (ODBC):**
```
Driver={ODBC Driver 17 for SQL Server};Server=localhost,1433;Database=your_database_name;Uid=sa;Pwd=SqlServer2019!;TrustServerCertificate=yes;
```

**Connect using sqlcmd:**
```bash
docker exec -it sqlserver /opt/mssql-tools/bin/sqlcmd -S localhost -U sa -P SqlServer2019!
```

---

### RabbitMQ

**Start only RabbitMQ:**
```bash
docker-compose up -d rabbitmq
```

**Access RabbitMQ:**
- AMQP Port: `5672`
- Management UI: `http://localhost:15672`
- Username: `admin`
- Password: `SqlServer2019!`
- Virtual Host: `/`

**Example connection string will be provided manually**

**Management Console:**
Open your browser and navigate to: `http://localhost:15672`
- Username: `admin`
- Password: `SqlServer2019!`

---

### LavinMQ

**Start only LavinMQ:**
```bash
docker-compose up -d lavinmq
```

**Access LavinMQ:**
- AMQP Port: `5673`
- Management UI: `http://localhost:15673`
- Username: `guest`
- Password: `guest`

**Example connection string will be provided manually**

**Management Console:**
Open your browser and navigate to: `http://localhost:15673`
- Username: `guest`
- Password: `guest`

---

### OpenTelemetry LGTM Stack

**Start only LGTM:**
```bash
docker-compose up -d otel-lgtm
```

**Access LGTM Services:**
- **Grafana UI**: `http://localhost:3000`
- **OTLP gRPC**: `localhost:4317`
- **OTLP HTTP**: `localhost:4318`
- **Prometheus**: `http://localhost:9090`

**OTLP Exporter Endpoint (gRPC):**
```
http://localhost:4317
```

**OTLP Exporter Endpoint (HTTP):**
```
http://localhost:4318
```

---

## Starting Multiple Services

You can start specific services together:

```bash
# Start MongoDB and Redis only
docker-compose up -d mongodb redis

# Start all databases
docker-compose up -d mongodb redis sqlserver

# Start message brokers only
docker-compose up -d rabbitmq lavinmq
```

## Stopping Individual Services

```bash
docker-compose stop [service-name]
```

Example:
```bash
docker-compose stop mongodb
```

## Removing Services and Data

**Remove containers but keep data:**
```bash
docker-compose down
```

**Remove containers and volumes (deletes all data):**
```bash
docker-compose down -v
```

## Checking Service Status

```bash
docker-compose ps
```

## Default Credentials Summary

| Service | Username | Password |
|---------|----------|----------|
| MongoDB | admin | SqlServer2019! |
| Redis | N/A | SqlServer2019! |
| SQL Server | sa | SqlServer2019! |
| RabbitMQ | admin | SqlServer2019! |
| LavinMQ | guest | guest |

**⚠️ Important:** These are development credentials. Never use these in production environments!
