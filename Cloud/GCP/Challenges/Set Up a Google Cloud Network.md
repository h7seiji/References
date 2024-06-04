# Challenge Lab

## Migrate to Cloud SQL

- Enable Database Migration API
- Enable Service Networking API

- ssh into the antern-postgresql-vm instance
- `apt get install postgresql-13-pglogical`
- `vim /etc/postgresql/13/main/postgresql.conf`
- enable the pglogical database extension
- `/etc/postgresql/13/main/pg_hba.conf`
- allow access from all hosts

- username:
- password: DMS_1s_cool!
- Grant permission to the user for the orders and postgres databases

```bash
ALTER TABLE public.inventory_items ADD PRIMARY KEY(id);
\q
exit
```

## Update permissions

## Create networks and firewalls

## Troubleshoot and fix a broken GKE cluster
