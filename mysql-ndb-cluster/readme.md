# MySQL NDB In-Memory Database Cluster

This Nutanix Calm blueprint will deploy MySQL NDB, a highly-available, in-memory MySQL implementation.

## Components

- 1x CentOS 7 MySQL NDB Manager
- 1x CentOS 7 ProxySQL server, used to distribute client connections across the MySQL cluster/pool 
- 2x CentOS 7 MySQL NDB 'Data Nodes' (edit blueprint to enable more)
- 2x CentOS 7 MySQL 'SQL Nodes' (edit blueprint to enable more)

## Prerequisites

To deploy this blueprint you will need the following things available.

- A CentOS 7 Linux VM image, published via the Nutanix Image Service
- Username and password for your Linux image (note that this blueprint does not natively use public/private key authentication)

## Usage

- Import the blueprint into your Nutanix Calm environment
- Adjust credentials to suit your requirements (the import will warn about blueprint validation errors, since credentials are not saved in exported blueprints)
- Alter each Calm service/VM so that it deploys your CentOS 7 image
- Alter each Calm service/VM so that it connects to your preferred network
- Launch the blueprint
- Fill in all required runtime variables, paying particular attention to the credentials section

## After Deployment

The MySQL servers deployed by this application belong to a server pool.  This pool is created and managed by the ProxySQL server.

While it is possible to login directly to the MySQL 'SQL Nodes' and issue SQL commands, the ProxySQL server enables a central login point that will distribute connections across the members of the pool.

For example, the following command within an SSH session will login to the ProxySQL MySQL client.  The password, when prompted, is the value of APP_DB_PASSWORD variable specified at blueprint launch. 

```
/usr/bin/mysql -u <your_app_db_user> -p -h 127.0.0.1 -P 6033
```

Port 6033 is the port on which ProxySQL listens for client connections.
 
From within the MySQL client, it is then possible to run standard MySQL 5.6 SQL queries, each of which will be issued on the 'SQL Node' pool members.

## Viewing MySQL NDB Configuration

SSH to the MySQL NDB Manager and issue the following command.

```
ndb_mgm -e "SHOW"
```

This will return the MySQL NDB configuration, showing the manager, the data nodes and the SQL nodes that have been deployed.