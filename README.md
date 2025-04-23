# Oracle Database on Docker

This repository provides a simple Docker Compose setup for running the Oracle Database Free Edition in a containerized environment.

## 📦 Contents

- `docker-compose.yml`: Docker Compose file to start the Oracle Database container.
- `init-scripts/`: Folder intended for placing HR sample schema SQL files (like `hr_install.sql`, `hr_populate.sql`, etc).

## 🚀 Getting Started

### 1. Prerequisites

- Docker
- Docker Compose

### 2. Setup

Download the [HR sample schema files](https://github.com/oracle/db-sample-schemas) from Oracle's GitHub and copy the following SQL files into the `init-scripts/` directory:

- `hr_create.sql`
- `hr_code.sql`
- `hr_populate.sql`
- `hr_install.sql`

> Note: You must accept Oracle’s license to download and use these.

### 3. Start the Container
change directory to `dockerized-oracle` and run in terminal. In Linux you may need `sudo`. 
```bash
docker compose up -d
```

Wait several minutes for the database to fully initialize. You can monitor progress with:

```bash
docker logs -f oracle
```

Once you see `DATABASE IS READY TO USE!`, you can access it.

### 4. Load the HR Schema (Manually)

1. Enter the running container:

```bash
docker exec -it oracle bash
```

2. Connect to the database:

```bash
sqlplus / as sysdba
```

3. Switch to the pluggable database:

```sql
ALTER SESSION SET CONTAINER=FREEPDB1;
```

4. Run the installation script:

```sql
@/opt/hr/hr_install.sql
```

Follow the script prompts to complete the schema installation.

### 5. Connect to the HR User
To access via terminal 
```bash
sqlplus hr@//localhost:1521/FREEPDB1
```

From Navicat or VS Code:

- **Username**: `hr`
- **Password**: [password you set during HR installation]
- **Host**: `localhost`
- **Port**: `1521`
- **Service Name**: `FREEPDB1`

## 🗑️ Cleanup

To stop and remove everything:

```bash
docker-compose down -v
```

---

## 📁 Directory Structure

```
oracle-docker/
├── docker-compose.yml
├── init-scripts/
│   └── .gitkeep
└── README.md
```
