# PostgreSQL Database Setup

This document outlines the steps to set up a local PostgreSQL database for Synapse.

## Prerequisites

- PostgreSQL installed and running on your machine

## Setup Steps

1. Create the database user:
```bash
psql -c "CREATE USER synapse_user WITH PASSWORD 'secretpassword';" postgres
```

2. Create the database with the user as owner:
```bash
psql -c "CREATE DATABASE synapse OWNER synapse_user;" postgres
```

3. Grant privileges to the user:
```bash
psql -c "GRANT ALL PRIVILEGES ON DATABASE synapse TO synapse_user;" postgres
```

## Configuration

The database configuration in `homeserver.yaml` should match these credentials:

```yaml
database:
  name: psycopg2
  txn_limit: 10000
  args:
    user: synapse_user
    password: secretpassword
    dbname: synapse
    host: localhost
    port: 5432
    cp_min: 5
    cp_max: 10
```

## Verification

To verify the connection, you can connect to the database using:

```bash
psql -U synapse_user -h localhost -d synapse
```

You will be prompted for the password (`secretpassword`). 