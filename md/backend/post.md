# PostgreSQL

## Setup

### Install

```bash
sudo apt install postgresql
```

### Enter into postgresql local server

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
