# PostgreSQL

## Setup

### Install

```bash
sudo apt install postgresql
```

### Enter into postgresql local server

New super user created automatically

```bash
sudo -i -u postgres
```

### Run postgresql local server

```bash
psql
```

## Basics

- "\h" for help with SQL commands
- "\?" for help with psql commands
- "\g" or terminate with semicolon(";") to execute query
- "\q" to quit

### Help

```bash
\?
```

### Tables list

```bash
\l
```

### Connect to db table

```bash
\connect <db-name>
```

### Tables relations description

```bash
\d
```

### Table relations description

```bash
\d <bd-name>
```

```bash
\d "BdName"
```

### Check db tables

```bash
\dt
```

### Check db roles

```bash
\du
```

### Exit from psql shell regime

```bash
\q
```

### Setup custom superuser login and password

```sql
ALTER USER newusername WITH PASSWORD 'new-password';
```

### Create new user

```sql
CREATE USER username WITH PASSWORD 'user-password';
```

### Give super rights to user

```sql
ALTER USER username WITH SUPERUSER;
```

### Remove user

```sql
DROP USER username;
```

## Tables

### Select all the table

```sql
SELECT * FROM table_name;
```

### Inset into table

```sql
INSERT INTO table_name (col1, col2, ...) VALUES (val1, val2, ...) 
```
