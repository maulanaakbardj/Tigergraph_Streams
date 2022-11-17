# Data Streaming TigerGraph

Example Tigergraph implementation of the TG data Streaming with Kafka

There is a `docker-compose` file for getting up and running with MariaDB, a
Confluent cluster, and a TigerGraph instance. 

## Architecture Diagram

![Untitled Diagram](https://user-images.githubusercontent.com/67249292/201480387-3af760ca-f94d-405d-b9ad-8aca0d6d6544.jpg)

### Kafka Flow

![image](https://user-images.githubusercontent.com/67249292/201484768-4ecab915-a352-4db1-b248-8f71c5acaa55.png)


## Steps

1. Run all the containers up with `docker-compose up -d`
2. Run the database schema create create SQL by following LDAP.sql in [dbeaver](https://dbeaver.io/download/) or some other database interface.
3. Create the JDBC Source Connectors in Control Center (`localhost:9021`) or through the REST API.
Images for Control Center are located in the `images` folder, and the JSON configs are located in the
`kafka-connect` folder.
4. Create the topics as well (`ldap-roles`, `ldap-parties`, `ldap-party_roles`).
5. Enter into the `tigergraph` container.
6. Run `su tigergraph` and run `gadmin status`.
![image](https://user-images.githubusercontent.com/67249292/202384651-78046042-1a39-445e-8577-1edb474328e0.png)

7. Run `gsql /home/tigergraph/entitlements.gsql`. This creates the schema and loading jobs.
8. Run `gsql` to enter the GSQL console.

```
> USE GRAPH Entitlements
> RUN LOADING JOB load_resources
> RUN LOADING JOB real_time_loader
```

`real_time_loader` will continue to run in the foreground of the GSQL shell

9. Run the SQL inserts
10. Open up GraphStudio at `localhost:14240` and navigate through your graph.
11. Run the SQL updates and reload GraphStudio to make sure it caught the updates to the graph.
